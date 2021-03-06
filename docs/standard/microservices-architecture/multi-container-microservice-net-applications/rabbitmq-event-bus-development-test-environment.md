---
title: 開発環境またはテスト環境の RabbitMQ でイベント バスを実装する
description: コンテナー化された .NET アプリケーションの .NET マイクロサービス アーキテクチャ | 開発環境またはテスト環境の RabbitMQ でイベント バスを実装する
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 12/11/2017
ms.openlocfilehash: e2b0f1a6152df5d323164fb2eca102fcb973667e
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="implementing-an-event-bus-with-rabbitmq-for-the-development-or-test-environment"></a>開発環境またはテスト環境の RabbitMQ でイベント バスを実装する

eShopOnContainers アプリケーションの場合のようにコンテナーで実行される RabbitMQ に基づいてカスタム イベント バスを作成した場合、その使用は開発環境およびテスト環境に限定する必要があるということを述べることから始めます。 カスタム イベント バスについては、実働可能なサービス バスの一部として作成していない限り、運用環境で使用すべきではありません。 単純なカスタム イベント バスには、商用サービス バスが備えている重要な実働可能機能の多くが不足している可能性があります。

eShopOnContainers でのイベント バスのカスタム実装の 1 つは基本的には RabbitMQ API を使用するライブラリです (Azure Service Bus に基づく別の実装もあります)。 

図 8-21 に示すように、RabbitMQ でのイベント バスの実装により、マイクロサービスはイベントのサブスクライブ、イベントの発行、およびイベントの受け取りを行うことができます。

![](./media/image22.png)

**図 8-21** イベント バスの RabbitMQ 実装

コードの中で、EventBusRabbitMQ クラスは汎用的な IEventBus インターフェイスを実装します。 これは、この開発/テスト バージョンから運用環境バージョンに切り替えられるように、依存関係挿入に基づいて行われます。

```csharp
public class EventBusRabbitMQ : IEventBus, IDisposable
{
    // Implementation using RabbitMQ API
    //...
```

サンプルの開発/テスト イベント バスの RabbitMQ 実装は定型的なコードです。 これは、RabbitMQ サーバーへの接続を処理し、メッセージ イベントをキューに発行するためのコードを提供します。 また、イベントの種類ごとに統合イベント ハンドラーのコレクションから成る辞書を実装する必要があります。このようなイベントの種類では、図 8-21 に示すように、受信側のマイクロサービスごとに、インスタンス化したものが異なり、さまざまなサブスクリプションが存在する場合があります。

## <a name="implementing-a-simple-publish-method-with-rabbitmq"></a>RabbitMQ で単純な発行方法を実装する

次のコードは RabbitMQ 用の簡略化されたイベント バスの実装です。eShopOnContainers の[実際のコード](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/BuildingBlocks/EventBus/EventBusRabbitMQ/EventBusRabbitMQ.cs)では機能が強化されます。 通常、機能強化を行うのでなければ、このコードを変更する必要はありません。 このコードでは、RabbitMQ への接続とチャネルを取得し、メッセージを作成し、キューにメッセージを発行します。

```csharp
public class EventBusRabbitMQ : IEventBus, IDisposable
{
    // Member objects and other methods ...
    // ...

    public void Publish(IntegrationEvent @event)
    {
        var eventName = @event.GetType().Name;
        var factory = new ConnectionFactory() { HostName = _connectionString };
        using (var connection = factory.CreateConnection())
        using (var channel = connection.CreateModel())
        {
            channel.ExchangeDeclare(exchange: _brokerName,
                type: "direct");
            string message = JsonConvert.SerializeObject(@event);
            var body = Encoding.UTF8.GetBytes(message);
            channel.BasicPublish(exchange: _brokerName,
                routingKey: eventName,
                basicProperties: null,
                body: body);
       }
    }
}
```

eShopOnContainers アプリケーションの Publish メソッドの[実際のコード](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/BuildingBlocks/EventBus/EventBusRabbitMQ/EventBusRabbitMQ.cs)は、[Polly](https://github.com/App-vNext/Polly) 再試行ポリシーで機能強化されています。このポリシーでは、RabbitMQ コンテナーが準備完了状態にない場合にタスクが特定の回数試行されます。 これは docker-compose がコンテナーを開始する場合に発生する可能性があります。たとえば、RabbitMQ コンテナーは他のコンテナーより緩やかに開始します。

前述したように、RabbitMQ には可能な構成が多数存在するため、このコードは開発環境およびテスト環境でのみの使用に限定する必要があります。

## <a name="implementing-the-subscription-code-with-the-rabbitmq-api"></a>RabbitMQ API でサブスクリプション コードを実装する

発行コードの場合と同様に、次のコードも RabbitMQ 用のイベント バス実装の一部を簡略化したものです。 繰り返しますが、機能強化を行うのでなければ、これを変更する必要はありません。

```csharp
public class EventBusRabbitMQ : IEventBus, IDisposable
{
    // Member objects and other methods ...
    // ...

    public void Subscribe<T, TH>()
        where T : IntegrationEvent
        where TH : IIntegrationEventHandler<T>
    {
        var eventName = _subsManager.GetEventKey<T>();
        
        var containsKey = _subsManager.HasSubscriptionsForEvent(eventName);
        if (!containsKey)
        {
            if (!_persistentConnection.IsConnected)
            {
                _persistentConnection.TryConnect();
            }

            using (var channel = _persistentConnection.CreateModel())
            {
                channel.QueueBind(queue: _queueName,
                                    exchange: BROKER_NAME,
                                    routingKey: eventName);
            }
        }

        _subsManager.AddSubscription<T, TH>();
    }
}
```

各種のイベントには、RabbitMQ からイベントを取得ための関連チャネルがあります。 チャネルとイベントの種類ごとにイベント ハンドラーを必要な数だけ使用することができます。

Subscribe メソッドは IIntegrationEventHandler オブジェクト (現在のマイクロサービスでのコールバック メソッドに似ている) に加えて、それに関連する IntegrationEvent オブジェクトを受け入れます。 コードは次にそのイベント ハンドラーを、各種の統合イベントがクライアント マイクロサービスごとに保持できるイベント ハンドラーの一覧に追加します。 クライアント コードがまだサブスクライブしていないイベントがある場合、コードは該当するイベントの種類に対してチャネルを作成します。これにより、そのイベントが他のサービスから発行されたときに RabbitMQ からプッシュ スタイルでイベントを受け取ることができます。


>[!div class="step-by-step"]
[Previous] (integration-event-based-microservice-communications.md) [Next] (subscribe-events.md)
