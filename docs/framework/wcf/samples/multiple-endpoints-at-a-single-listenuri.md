---
title: 単一 ListenUri に対する複数のエンドポイント
ms.date: 03/30/2017
ms.assetid: 911ffad4-4d47-4430-b7c2-79192ce6bcbd
ms.openlocfilehash: f3eb2036ffbb7c5e8cae77ebc1a86e07d31626c9
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="multiple-endpoints-at-a-single-listenuri"></a>単一 ListenUri に対する複数のエンドポイント
このサンプルでは、単一 `ListenUri` で複数のエンドポイントをホストするサービスを示します。 このサンプルがに基づいて、[作業の開始](../../../../docs/framework/wcf/samples/getting-started-sample.md)電卓サービスを実装します。  
  
> [!NOTE]
>  このサンプルのセットアップ手順とビルド手順については、このトピックの最後を参照してください。  
  
 ように、[複数のエンドポイント](../../../../docs/framework/wcf/samples/multiple-endpoints.md)サンプルでは、サービスは、それぞれ異なるアドレス、またはまた各種のバインディングが複数のエンドポイントをホストできます。 このサンプルは、同じアドレスで複数のエンドポイントをホストできることを示しています。 さらに、サービス エンドポイントが持つ、`EndpointAddress` と `ListenUri` の 2 種類のアドレスの違いも示します。  
  
 `EndpointAddress` とは、サービスの論理アドレスです。 これは、SOAP メッセージの宛先となるアドレスです。 `ListenUri` とはサービスの物理アドレスです。 これには、サービス エンドポイントが現在のコンピュータで実際にメッセージをリッスンする、ポートとアドレスの情報が含まれます。 ほとんどの場合、これらのアドレスが異なっている必要はありません。`ListenUri` が明示的に指定されていない場合は、エンドポイントの `EndpointAddress` の URI が既定値になります。 ただし、複数の異なるサービス宛てのメッセージを受け入れることができるルーターを構成する場合など、2 つのアドレスを区別すると便利な場合もあります。  
  
## <a name="service"></a>サービス  
 このサンプルのサービスには、`ICalculator` と `IEcho` という 2 つのコントラクトがあります。 また、一般的な `IMetadataExchange` エンドポイントに加え、次のコードに示すように 3 つのアプリケーション エンドポイントがあります。  
  
```xml  
<endpoint address="urn:Stuff"  
        binding="wsHttpBinding"  
        contract="Microsoft.ServiceModel.Samples.ICalculator"   
        listenUri="http://localhost/servicemodelsamples/service.svc" />  
<endpoint address="urn:Stuff"  
        binding="wsHttpBinding"  
        contract="Microsoft.ServiceModel.Samples.IEcho"   
        listenUri="http://localhost/servicemodelsamples/service.svc" />  
<endpoint address="urn:OtherEcho"  
        binding="wsHttpBinding"  
        contract="Microsoft.ServiceModel.Samples.IEcho"   
        listenUri="http://localhost/servicemodelsamples/service.svc" />  
```  
  
 3 つすべてのエンドポイントは、同じ `ListenUri` でホストされ、同じ `binding` を使用します。`ListenUri` が同じエンドポイントは、コンピュータの物理アドレスでメッセージをリッスンする 1 つのチャネル スタックを共有するので、同じバインディングを使用する必要があります。 各エンドポイントの `address` は URN です。通常、アドレスは物理的な場所を表し、実際は任意の種類の URI を設定できますが、サンプルで示すようにこのアドレスは照合とフィルタ処理を行う目的で使用されるので、このように設定されています。  
  
 次の 3 つのすべてのエンドポイントが同じため`ListenUri`メッセージが到着したときに、Windows Communication Foundation (WCF) がメッセージの送信先のエンドポイントを決定する必要があります。 各エンドポイントにはメッセージ フィルタがあり、これはアドレス フィルタとコントラクト フィルタの 2 つの部分で構成されます。 アドレス フィルタは、SOAP メッセージの `To` とサービス エンドポイントのアドレスを照合します。 たとえば、`To "Urn:OtherEcho"` 宛てのメッセージだけが、このサービスの 3 つ目のエンドポイントの対象となります。 コントラクト フィルタは、特定のコントラクトの操作に関連付けられたアクションを照合します。 たとえば、`IEcho` のアクションが含まれるメッセージを照合します。 `Echo` は、このサービスの 2 つ目と 3 つ目の、両方のエンドポイントのコントラクト フィルターと照合します。これらのエンドポイントは、どちらも `IEcho` コントラクトをホストするからです。  
  
 このように、アドレス フィルタとコントラクト フィルタを組み合わせることによって、このサービスの `ListenUri` に到着する各メッセージを、正しいエンドポイントにルーティングすることができます。 3 つ目のエンドポイントは、他の 2 つのエンドポイントと区別されます。このエンドポイントは、他のエンドポイントとは異なるアドレスに送信されるメッセージを受け入れるからです。 1 つ目のエンドポイントと 2 つ目のエンドポイントは、コントラクト (受信メッセージのアクション) に基づいて相互に区別されます。  
  
## <a name="client"></a>クライアント  
 サーバー上のエンドポイントに 2 つの異なるアドレスがあるのと同様に、クライアント エンドポイントにも 2 つのアドレスがあります。 サーバーとクライアントのどちらでも、論理アドレスは `EndpointAddress` と呼ばれます。 ただし、サーバーの物理アドレスは `ListenUri` と呼ばれるのに対し、クライアントの物理アドレスは `Via` と呼ばれます。  
  
 これら 2 つのアドレスがサーバー上にある場合、既定では同じアドレスを示します。 クライアントで、エンドポイントのアドレスとは異なる `Via` を指定するには、次のように `ClientViaBehavior` を使用します。  
  
```  
Uri via = new Uri("http://localhost/ServiceModelSamples/service.svc");  
CalculatorClient calcClient = new CalculatorClient();  
calcClient.ChannelFactory.Endpoint.Behaviors.Add(  
        new ClientViaBehavior(via));  
```  
  
 このアドレスは、通常どおりクライアントの構成ファイルで指定します。この構成ファイルは Svcutil.exe によって生成されたものです。 `Via` (サービスの `ListenUri` に相当) は、サービスのメタデータ内では示されません。したがってこの情報は、(サービスのメタデータ アドレスと同様に) クライアントに帯域外で伝達する必要があります。  
  
 このサンプルでは、クライアントはサーバーの 3 つの各アプリケーション エンドポイントにメッセージを送信し、3 つすべてのエンドポイントと通信できる (さらにそれらのエンドポイントを区別できる) ことを示します。これらすべてのエンドポイントが同じ `Via` を持つ場合でも同様です。  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには  
  
1.  実行したことを確認してください、 [Windows Communication Foundation サンプルの 1 回限りのセットアップ手順](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)です。  
  
2.  ソリューションの C# 版または Visual Basic .NET 版をビルドするには、「 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)」の手順に従います。  
  
3.  1 つまたは複数コンピューター構成でサンプルを実行する手順についてで[Windows Communication Foundation サンプルの実行](../../../../docs/framework/wcf/samples/running-the-samples.md)です。  
  
    > [!NOTE]
    >  複数コンピューターの場合は、Client.cs ファイルで、localhost をサービス コンピューターの名前に置き換える必要があります。  
  
> [!IMPORTANT]
>  サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  このディレクトリが存在しない場合に、 [Windows Communication Foundation (WCF) および .NET Framework 4 向けの Windows Workflow Foundation (WF) サンプル](http://go.microsoft.com/fwlink/?LinkId=150780)すべて Windows Communication Foundation (WCF) をダウンロードして[!INCLUDE[wf1](../../../../includes/wf1-md.md)]サンプルです。 このサンプルは、次のディレクトリに格納されます。  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\MultipleEndpointsSingleUri`  
  
## <a name="see-also"></a>関連項目
