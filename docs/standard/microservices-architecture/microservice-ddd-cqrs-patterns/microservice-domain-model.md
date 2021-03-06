---
title: マイクロサービス ドメイン モデルの設計
description: コンテナー化された .NET アプリケーションの .NET マイクロサービス アーキテクチャ | マイクロサービス ドメイン モデルの設計
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 11/09/2017
ms.openlocfilehash: 2776412b96d4ed141f48814d19d2deaa1a71520d
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="designing-a-microservice-domain-model"></a>マイクロサービス ドメイン モデルの設計

*ビジネス マイクロサービスまたは有界コンテキストごとに 1 つのリッチ ドメイン モデルを定義する*

ここでの目標は、ビジネス マイクロサービスまたは有界コンテキスト (BC) ごとに 1 つのまとまりのあるドメイン モデルを作成することです。 ただし、BC またはビジネス マイクロサービスは、1 つのドメイン モデルを共有する複数の物理サービスから構成される場合があることに注意してください。 ドメイン モデルは、それが表す 1 つの有界コンテキストまたはビジネス マイクロサービスのルール、ビヘイビアー、ビジネス言語、および制約をキャプチャする必要があります。

## <a name="the-domain-entity-pattern"></a>ドメイン エンティティ パターン

エンティティは、ドメイン オブジェクトを表すもので、主にその ID、継続性、および永続化によって時間とともに定義されます。エンティティを構成する属性によってのみ定義されるわけではありません。 Eric Evans が言うように、"主にその ID で定義されるオブジェクトは、エンティティと呼ばれます。" エンティティは、モデルの基礎となるため、ドメイン モデルで非常に重要です。 したがって、エンティティは、慎重に識別し、設計する必要があります。

*エンティティの ID は、複数のマイクロサービスまたは有界コンテキストを横断できる。*

同じ ID (ただし、同じエンティティではない) を複数の有界コンテキストまたはマイクロサービス全体でモデリングできます。 ただし、同じ属性とロジックを持つ同じエンティティが複数の有界コンテキストに実装されるわけではありません。 代わりに、それぞれの有界コンテキストのエンティティは、その属性とビヘイビアーを有界コンテキストのドメインで必要なものに制限します。

たとえば、バイヤー エンティティは、プロファイルまたは ID マイクロサービスのユーザー エンティティで定義された個人の属性の大部分を持っている可能性があります (ID を含む)。 しかし、注文マイクロサービスのバイヤー エンティティは、持っている属性が少ない可能性があります。注文プロセスに特定のバイヤー データしか関連付けられていないからです。 各マイクロサービスまたは有界コンテキストのコンテキストは、そのドメイン モデルに影響を与えます。

*ドメイン エンティティは、データ属性を実装するだけでなく、ビヘイビアーも実装する必要がある*

DDD のドメイン エンティティは、エンティティ データ (アクセスされるメモリ内のオブジェクト) に関連するドメイン ロジックまたはビヘイビアーを実装する必要があります。 たとえば、注文エンティティ クラスの一部として、ビジネス ロジックと操作を、タスク (注文項目の追加、データ検証、合計計算など) のメソッドとして実装する必要があります。 エンティティのメソッドは、エンティティのルールをアプリケーション レイヤー全体に広げるのではなく、エンティティの不変量とルールを処理します。

図 9-8 は、データの属性だけではなく、操作やメソッドを、関連するドメイン ロジックとともに実装するドメイン エンティティを示しています。

![](./media/image9.png)

**図 9-8**. データとビヘイビアーを実装するドメイン エンティティ設計の例

もちろん、エンティティ クラスの一部としてどのロジックも実装しないエンティティを持つ場合もあります。 この状況は、大部分のロジックが集計ルートで定義されており、子エンティティが特別なロジックを持たない場合に、集計内の子エンティティで発生する場合があります。 ドメイン エンティティではなく、サービス クラスに多数のロジックが実装されている複雑なマイクロサービスがある場合は、ドメイン モデル貧血症になる場合があります。ドメイン モデル貧血症については、次のセクションで説明します。

### <a name="rich-domain-model-versus-anemic-domain-model"></a>リッチ ドメイン モデルと貧血症ドメイン モデルの比較

Martin Fowler は、投稿した [AnemicDomainModel](https://martinfowler.com/bliki/AnemicDomainModel.html) で、ドメイン モデル貧血症について、次のように述べています。

ドメイン モデル貧血症の基本的な症状は、一見、それが本物のドメイン モデルに見えるという点です。 オブジェクトがいくつかあり、それらはドメイン空間にある名詞から名前をつけられています。それから、オブジェクト同士がしっかりとしたリレーションで結びついており、本物のドメイン モデルと同じような構造を持っているのです。 ただし、オブジェクトのビヘイビアーを見れば違いがわかります。それらのオブジェクトにはわずかなビヘイビアーしかなく、ゲッターとセッターの入れ物にすぎないということに気づくと思います。

もちろん、貧血症ドメイン モデルを使用する場合、これらのデータ モデルは、すべてのドメインまたはビジネス ロジックをキャプチャする一連のサービス オブジェクト (従来名は "*ビジネス レイヤー*") から使用されます。 ビジネス レイヤーは、データ モデル上にあり、データ モデルを単にデータとして使用します。

貧血症ドメイン モデルは、手続き型の設計にすぎません。 貧血症エンティティ オブジェクトは、ビヘイビアー (メソッド) がないため、本当のオブジェクトではありません。 また、データ プロパティを保持するだけなので、オブジェクト指向設計ではありません。 すべてのビヘイビアーをサービス オブジェクト (ビジネス レイヤー) に入れると、どうしても最後には[スパゲッティ コード](https://en.wikipedia.org/wiki/Spaghetti_code)や[トランザクション スクリプト](https://martinfowler.com/eaaCatalog/transactionScript.html)が出来上がり、その結果、ドメイン モデルが持つ利点が失われます。

とにかく、マイクロサービスまたは有界コンテキストが非常にシンプル (CRUD サービス) である場合は、エンティティ オブジェクト形式でデータ プロパティしか持たない貧血症ドメイン モデルで十分であり、より複雑な DDD パターンを実装する価値はないかもしれません。 その場合、CRUD を目的としてデータしか持たないエンティティを意図的に作成したので、これは単に永続化モデルになります。

このため、有界コンテキストにもよりますが、マイクロサービス アーキテクチャは、マルチアーキテクチャ手法に最適となります。 たとえば、eShopOnContainers の場合、注文マイクロサービスは、DDD パターンを実装しますが、カタログ マイクロサービス (シンプルな CRUD サービス) は、DDD パターンを実装しません。

貧血症ドメイン モデルは、アンチパターンであると言われる場合があります。 実際、このモデルは、実装する内容に依存しています。 作成するマイクロサービスが十分にシンプルである場合 (CRUD サービスなどである場合) は、貧血症ドメイン モデルに従い、アンチパターンになりません。 ただし、絶えず変化するビジネス ルールを多数含むマイクロサービスのドメインの複雑さに取り組む必要がある場合、貧血症ドメイン モデルは、そのマイクロサービスまたは有界コンテキストのアンチ パターンになる可能性があります。 その場合は、データとビヘイビアーを含み、追加の DDD パターン (集計や値オブジェクトなど) を実装するエンティティを持つリッチ モデルとして貧血症ドメイン モデルを設計すると、そのようなマイクロサービスを長期的に成功させるために必要な大きな利点が得られる可能性があります。

#### <a name="additional-resources"></a>その他の技術情報

-   **DevIQ。ドメイン エンティティ**
    [*http://deviq.com/entity/*](http://deviq.com/entity/)

-   **Martin Fowler。ドメイン モデル**
    [*https://martinfowler.com/eaaCatalog/domainModel.html*](https://martinfowler.com/eaaCatalog/domainModel.html)

-   **Martin Fowler。ドメイン モデル貧血症に関する記事**

    <https://martinfowler.com/bliki/AnemicDomainModel.html>

### <a name="the-value-object-pattern"></a>値オブジェクト パターン

Eric Evans は、"多くのオブジェクトは、概念 ID を持ちません。 これらのオブジェクトは、あるものについての特定の特性を記述しています。" と述べています。

エンティティには ID が必要ですが、システム内には値オブジェクト パターンのように ID を持たないオブジェクトが多数あります。 値オブジェクトは、ドメインのアスペクトを記述する概念 ID を持たないオブジェクトです。 これは、一時的にしか関係しない設計要素を表すためにインスタンス化するオブジェクトです。 関心を持つ必要があるのは、それが "*誰*" であるのかではなく、"*何*" であるのかという点です。 例には数値と文字列が含まれていますが、属性グループのような上位レベルの概念にすることもできます。

あるマイクロサービスではエンティティであるものが、別のマイクロサービスではエンティティでないことがあります。これは、2 番目のケースで、有界コンテキストが別の意味を持つことがあるからです。 たとえば、eコマース アプリケーションのアドレスは、ID を持たない場合があります。これは、個人または会社の顧客プロファイルの属性グループしか表さない場合があるためです。 この場合、アドレスは、値オブジェクトとして分類する必要があります。 ただし、電力会社のアプリケーションでは、顧客のアドレスがビジネス ドメインで重要になります。 そのため、請求システムがアドレスに直接リンクできるようにするために、アドレスには ID が必要です。 この場合、アドレスは、ドメイン エンティティとして分類する必要があります。

通常、個人は ID を持つため、名と姓を持つ個人はエンティティです。これは、その名と姓が別の値セットに一致した場合 (たとえば、それらの名前が別の個人も指している場合) にも当てはまります。

値オブジェクトは、関係データベースや ORM (EF など) では管理が難しいですが、ドキュメント指向データベースでは簡単に実装して使用できます。

#### <a name="additional-resources"></a>その他の技術情報

-   **Martin Fowler。値オブジェクト パターン**
    [*https://martinfowler.com/bliki/ValueObject.html*](https://martinfowler.com/bliki/ValueObject.html)

-   **値オブジェクト**
    [*http://deviq.com/value-object/*](http://deviq.com/value-object/)

-   **テスト駆動型開発での値オブジェクト**
    [*https://leanpub.com/tdd-ebook/read\#leanpub-auto-value-objects*](https://leanpub.com/tdd-ebook/read#leanpub-auto-value-objects)

-   **Eric Evans。Domain-Driven Design: Tackling Complexity in the Heart of Software (ドメイン駆動設計: ソフトウェア中心部の複雑さへの取り組み)。** (書籍、値オブジェクトについての記載あり) [*https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/*](https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/)

### <a name="the-aggregate-pattern"></a>集計パターン

ドメイン モデルには、機能の重要な領域 (注文調達やインベントリなど) を制御できる、さまざまなデータ エンティティやプロセスのクラスターが含まれています。 より細かな DDD 単位は集計であり、まとまりのある単位として処理できるエンティティとビヘイビアーのクラスターまたはグループが記述されています。

通常は、必要なトランザクションに基づいて集計を定義します。 典型的な例は、注文項目のリストも含まれる注文です。 通常、注文項目は、エンティティになります。 ただし、注文集計内では子エンティティとなり、注文エンティティもそのルート エンティティとして含まれます (通常、ルート エンティティは、集計ルートと呼ばれます)。

集計を識別することが困難な場合があります。 集計は、互いに一致する必要があるオブジェクトのグループですが、オブジェクトのグループを選び、集計のラベルをつけることはできません。 ドメインの概念から開始し、その概念に関連する最も一般的なトランザクションで使用されるエンティティについて考える必要があります。 トランザクションで一致する必要があるエンティティは、集計を形成するエンティティです。 トランザクションの操作について考えることが、おそらく集計を識別するための最良の方法です。

### <a name="the-aggregate-root-or-root-entity-pattern"></a>集計ルートまたはルート エンティティ パターン

集計は、集計ルートという 1 つ以上のエンティティから構成されています (集計ルートは、ルート エンティティまたはプライマリ エンティティとも呼ばれます)。 また、集計は、複数の子エンティティと値オブジェクトを持つことができ、すべてのエンティティとオブジェクトが連携して、必要なビヘイビアーやトランザクションを実装しています。

集計ルートの目的は、集計の一貫性を維持することです。集計ルートは、集計ルート クラスのメソッドまたは操作を通じて集計に入るための唯一の更新用のエントリ ポイントである必要があります。 集計内のエンティティを変更するときは、必ず集計ルートを経由する必要があります。 これは、集計の一貫性を管理するもので、集計で従う必要のあるすべての不変量および一貫性のルールを考慮しています。 子エンティティまたは値オブジェクトを別々に変更した場合、集計ルートは、集計が有効な状態であることを保証できません。 本来の機能を発揮できなくなるでしょう。 一貫性の管理は、集計のルートの主も重要な目的です。

図 9-9 には、バイヤー集計などのサンプル集計が示されています。バイヤー集計には、1 つのエンティティ (集計ルート バイヤー) が含まれています。 注文集計には、複数のエンティティと値オブジェクトが含まれています。

![](./media/image10.png)

**図 9-9**. 複数のエンティティまたは 1 つのエンティティを含む集計の例

バイヤー集計は、ドメインによっては、eShopOnContainers 参照アプリケーションの注文マイクロサービスの場合と同様、追加の子エンティティを持つことができることに注意してください。 図 9-9 は、集計ルートのみを含む集計の例として、バイヤーが 1 つのエンティティを持つケースを示しています。

集計を分離し、集計間の境界を明確にし続けるためには、DDD ドメイン モデルで、集計間の直接の移動を禁止し、eShopOnContainers の[注文マイクロサービス ドメイン モデル](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/Services/Ordering/Ordering.Domain/AggregatesModel/OrderAggregate/Order.cs)に実装されている外部キー (FK) フィールドのみを持つことをお勧めします。 注文エンティティは、次のコードに示すように、バイヤーの FK フィールドのみを持ち、EF コア ナビゲーション プロパティは持ちません。

```csharp
public class Order : Entity, IAggregateRoot
{
    private DateTime _orderDate;
    public Address Address { get; private set; }
    private int? _buyerId; //FK pointing to a different aggregate root
    public OrderStatus OrderStatus { get; private set; }
    private readonly List<OrderItem> _orderItems;
    public IReadOnlyCollection<OrderItem> OrderItems => _orderItems;
    // ... Additional code
}
```

集計を識別し、操作するには、研究と経験が必要です。 詳細については、次の「その他の技術情報」のリストを参照してください。

#### <a name="additional-resources"></a>その他の技術情報

-   **Vaughn Vernon。効果的な集計設計 - パート I: 1 つの集計のモデリング**
    [*https://vaughnvernon.co/wordpress/wp-content/uploads/2014/10/DDD\_COMMUNITY\_ESSAY\_AGGREGATES\_PART\_1.pdf*](https://vaughnvernon.co/wordpress/wp-content/uploads/2014/10/DDD_COMMUNITY_ESSAY_AGGREGATES_PART_1.pdf)

-   **Vaughn Vernon。効果的な集計設計 - パート II: 集計処理の連携**
    *<https://vaughnvernon.co/wordpress/wp-content/uploads/2014/10/DDD_COMMUNITY_ESSAY_AGGREGATES_PART_2.pdf> *

-   **Vaughn Vernon。効果的な集計設計 - パート III: 探索によるインサイトの獲得**
    *<https://vaughnvernon.co/wordpress/wp-content/uploads/2014/10/DDD_COMMUNITY_ESSAY_AGGREGATES_PART_3.pdf> *

-   **Sergey Grybniak。DDD 戦術的デザイン パターン**
    [*https://www.codeproject.com/Articles/1164363/Domain-Driven-Design-Tactical-Design-Patterns-Part*](https://www.codeproject.com/Articles/1164363/Domain-Driven-Design-Tactical-Design-Patterns-Part)

-   **Chris Richardson。集計を使用したトランザクション マイクロサービスの開発**
    [*https://www.infoq.com/articles/microservices-aggregates-events-cqrs-part-1-richardson*](https://www.infoq.com/articles/microservices-aggregates-events-cqrs-part-1-richardson)

-   **DevIQ。集計パターン**
    [*http://deviq.com/aggregate-pattern/*](http://deviq.com/aggregate-pattern/)


>[!div class="step-by-step"]
[前] (ddd-oriented-microservice.md) [次] (net-core-microservice-domain-model.md)
