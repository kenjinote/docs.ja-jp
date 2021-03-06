---
title: ワークフロー サービス ホストの拡張機能
ms.date: 03/30/2017
ms.assetid: c0e8f7bb-cb13-49ec-852f-b85d7c23972f
ms.openlocfilehash: 3393843e6be75e122c3993b3ccfb7c56d63cebad
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="workflow-service-host-extensibility"></a>ワークフロー サービス ホストの拡張機能
[!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] には、ワークフロー サービスをホストするための <xref:System.ServiceModel.Activities.WorkflowServiceHost> クラスがあります。 このクラスは、マネージ アプリケーションまたは Windows サービスで、ワークフロー サービスを自己ホストするときに使用します。 また、このクラスは、インターネット インフォメーション サービス (IIS) または Windows プロセス アクティブ化サービス (WAS) を使用してワークフロー サービスをホストするときにも使用します。 <xref:System.ServiceModel.Activities.WorkflowServiceHost> クラスは、カスタムの拡張機能の追加、アイドル動作の変更、およびサービス以外のワークフロー (メッセージング アクティビティを使用しないワークフロー) のホストを可能にする拡張ポイントを提供します。  
  
## <a name="workflow-service-host-extensions"></a>ワークフロー サービス ホストの拡張機能  
 <xref:System.ServiceModel.Activities.WorkflowServiceHost> には、<xref:System.ServiceModel.Activities.WorkflowServiceHost.WorkflowExtensions%2A> に拡張機能を追加するメソッドを提供する、<xref:System.Activities.Hosting.WorkflowInstanceExtensionManager> 型の <xref:System.ServiceModel.Activities.WorkflowServiceHost> プロパティがあります。 各ワークフロー サービス インスタンスに拡張機能を追加するには、<xref:System.Activities.Hosting.WorkflowInstanceExtensionManager.Add%2A> メソッドを使用します。 指定されたデリゲートは、ワークフロー サービス インスタンスが作成されるとき、または永続化ストアから読み込まれるときに、新しい拡張機能を作成するために呼び出されます。 各ワークフロー サービス ホストに拡張機能を追加するには、<xref:System.Activities.Hosting.WorkflowInstanceExtensionManager.Add%2A> メソッドを使用します。追加された拡張機能の 1 つのインスタンスが、すべてのワークフロー サービス インスタンスで共有されます。  
  
## <a name="react-to-unhandled-exceptions"></a>ハンドルされない例外の処理  
 <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> を使用すると、ワークフロー サービス内でハンドルされない例外が発生したときに実行されるアクションを指定できます。 <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior.Action%2A> プロパティには、次の <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction> 値のいずれかを指定します。  
  
-   <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction.Abandon> – ワークフロー サービス インスタンスを中止します。  
  
-   <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction.AbandonAndSuspend> – 前回永続化された状態にロールバックし、ワークフロー サービス インスタンスを中断します。 これは、ワークフローが既に 1 回以上、永続化されている場合にのみ実行されます。 永続化されたことがない場合は、ワークフロー インスタンスが中止されます。  
  
-   <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction.Cancel> – インスタンスを取り消します。  
  
-   <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction.Terminate> – ワークフロー インスタンスを終了します。  
  
 この動作は、次の例に示すように、コードで構成できます。  
  
```csharp  
host.Description.Behaviors.Add(new WorkflowUnhandledExceptionBehavior { Action = WorkflowUnhandledExceptionAction.Abandon });  
```  
  
 また、次の例のように、構成ファイルで構成することもできます。  
  
```xml
<behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
          <serviceDebug includeExceptionDetailInFaults="False" />  
          <workflowUnhandledExceptionBehavior action="Abandon" />        
        </behavior>  
      </serviceBehaviors>  
```  
  
## <a name="hosting-non-service-workflows"></a>サービス以外のワークフローのホスティング  
 <xref:System.ServiceModel.Activities.WorkflowServiceHost> を使用すると、サービス以外のワークフロー、つまり、<xref:System.ServiceModel.Activities.Receive> アクティビティで開始されないワークフロー、またはメッセージング アクティビティを使用しないワークフローをホストできます。 ワークフロー サービスは、通常、<xref:System.ServiceModel.Activities.Receive> アクティビティで開始されます。 <xref:System.ServiceModel.Activities.WorkflowServiceHost> がワークフロー サービスに対するメッセージを受信すると、ワークフロー サービスが実行 (または永続化) されていない場合は、新しいワークフロー サービス インスタンスが作成されます。 ワークフローが Receive アクティビティで開始されない場合は、メッセージを受信するアクティビティがないため、このワークフローは、メッセージを送信して開始することはできません。 サービス以外のワークフローをホストするには、<xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> から派生クラスを作成し、<xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnGetInstanceId%2A>、<xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnGetCreationContext%2A>、および <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnResolveBookmark%2A> をオーバーライドします。 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnGetInstanceId%2A> をオーバーライドすると、優先するインスタンスの ID を指定できます。 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnGetCreationContext%2A> をオーバーライドすると、カスタムのワークフロー作成コンテキストを作成したり、既存の <xref:System.ServiceModel.Activities.WorkflowCreationContext> インスタンスを設定したりできます。 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnResolveBookmark%2A> をオーバーライドすると、受信メッセージから手動でブックマークを抽出できます。 このメソッドをオーバーライドすると、WorkflowHostingEndpoint に送信されたメッセージに応答するために本文で <xref:System.ServiceModel.Activities.WorkflowHostingResponseContext.SendResponse%2A> を呼び出す必要があります。 これを呼び出さないと、<xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A> の制限を最終的に超過する可能性があります。 双方向コントラクトでは、応答を受信するために発生したクライアントのエラーのために、<xref:System.ServiceModel.Activities.WorkflowHostingResponseContext.SendResponse%2A> の呼び出しで発生したエラーを検出できる可能性があります。 一方向コントラクトでは、<xref:System.ServiceModel.Activities.WorkflowHostingResponseContext.SendResponse%2A> スロットルの制限を超過するまで <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A> を呼び出していないというミスを認識しない可能性があります。 詳細についてを参照してください、 [WorkflowHostingEndpoint 再開ブックマーク](../../../../docs/framework/windows-workflow-foundation/samples/workflowhostingendpoint-resume-bookmark.md)サービス以外のワークフローの新しいインスタンスを作成するには、新しいインスタンスを作成する操作を定義しているサービス コントラクトを宣言します。 作成操作は、IDictionary を受け取る必要があります\<文字列, オブジェクト > いずれかを通過するワークフローのパラメーターが必要です。 このコントラクトは、<xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> の派生クラスによって、暗黙で実装されます。 インスタンスを追加、ワークフローをホストする場合に、 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint>-派生クラスを呼び出すことによって、ホストに<xref:System.ServiceModel.Activities.WorkflowServiceHost.AddServiceEndpoint%2A>を呼び出すと<!--zz xref:System.ServiceModel.Activities.WorkflowServiceHost.Open%2A-->`System.ServiceModel.Activities.WorkflowServiceHost.Open`です。 ワークフローのインスタンスを作成するには、使用するサービス コントラクト型の <xref:System.ServiceModel.ChannelFactory%601> を作成し、<xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A> を呼び出します。 これで、サービス コントラクトに定義されている作成操作を呼び出すことができます。  
  
## <a name="see-also"></a>関連項目  
 [ワークフロー サービス](../../../../docs/framework/wcf/feature-details/workflow-services.md)  
 [メッセージング アクティビティ](../../../../docs/framework/wcf/feature-details/messaging-activities.md)
