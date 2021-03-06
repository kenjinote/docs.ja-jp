---
title: OperationScope
ms.date: 03/30/2017
ms.assetid: 56206a21-1e63-422d-b92a-e5d8b713e707
ms.openlocfilehash: bca5a32e25537aea8c8fad7b80eb296d66fadf77
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="operationscope"></a>OperationScope
このサンプルでは、メッセージング アクティビティの <xref:System.ServiceModel.Activities.Receive> および <xref:System.ServiceModel.Activities.SendReply> を使用して、既存のカスタム アクティビティをワークフロー サービス内の操作として公開する方法を示します。 このサンプルには、`OperationScope` という新しいカスタム アクティビティが含まれています。 このアクティビティは、ユーザーが操作の本文をカスタム アクティビティとして個別に作成できるようにし、それを `OperationScope` アクティビティを使用してサービス操作として簡単に公開できるようにすることで、ワークフロー サービスの開発を容易にするためのものです。 たとえば、2 つの `Add` 引数を受け取って 1 つの `in` 引数を返すカスタム `out` アクティビティは、`Add` にドロップすることでワークフロー サービスの `OperationScope` 操作として公開できます。  
  
 スコープは、本文として提供されたアクティビティを調べることによって機能します。 バインドされていない `in` 引数は、受信メッセージからの入力であると見なされます。 `out` 引数はすべて、バインドされているかどうかに関係なく、後続の応答メッセージの出力であると見なされます。 公開される操作の名前は、`OperationScope` アクティビティの表示名から取得されます。 最後に、本文アクティビティは、アクティビティの引数にバインドされたメッセージからのパラメーターを使用して、<xref:System.ServiceModel.Activities.Receive> および <xref:System.ServiceModel.Activities.SendReply> にラップされます。  
  
 このサンプルでは、HTTP エンドポイントを使用してワークフロー サービスを公開します。 サンプルを実行するには、適切な URL ACL を追加する必要があります。 詳細については、次を参照してください。[を構成する HTTP および HTTPS](http://go.microsoft.com/fwlink/?LinkId=70353)です。 管理者特権のプロンプトで次のコマンドを実行する適切な Acl を追加します (% ドメインのドメインとユーザー名に置き換えられることを確認してください。\\%username%)。  
  
 **netsh http 追加 urlacl url =http://+:8000/ユーザー ドメイン % =\\%username%**  
  
### <a name="to-run-the-sample"></a>サンプルを実行するには  
  
1.  [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] で OperationScope.sln ソリューションを開きます。  
  
2.  複数のスタートアップ プロジェクトを設定するには、ソリューション エクスプ ローラーでソリューションを右クリックしを選択すると**スタートアップ プロジェクトの**します。 複数のスタートアップ プロジェクトとして Scenario および Scenario_Client を (この順序で) 追加します。  
  
3.  Ctrl キーと Shift キーを押しながら B キーを押して、ソリューションをビルドします。  
  
    > [!WARNING]
    >  カスタム アクティビティ `OperationScope` が原因で、BankService.xaml ワークフローを表示するためにこの手順が必要になります。  
  
4.  Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。 Scenario_Client コンソールで入力が求められ、対応する出力が Scenario コンソールに表示されます。  
  
> [!IMPORTANT]
>  サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  このディレクトリが存在しない場合に、 [Windows Communication Foundation (WCF) および .NET Framework 4 向けの Windows Workflow Foundation (WF) サンプル](http://go.microsoft.com/fwlink/?LinkId=150780)すべて Windows Communication Foundation (WCF) をダウンロードして[!INCLUDE[wf1](../../../../includes/wf1-md.md)]サンプルです。 このサンプルは、次のディレクトリに格納されます。  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\Services\OperationScope`