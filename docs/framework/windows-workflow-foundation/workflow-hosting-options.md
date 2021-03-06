---
title: ワークフロー ホスティングのオプション
ms.date: 03/30/2017
ms.assetid: 37bcd668-9c5c-4e7c-81da-a1f1b3a16514
ms.openlocfilehash: 7713044e40532c431d090b1cb1795876ead2a899
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="workflow-hosting-options"></a>ワークフロー ホスティングのオプション
Windows Workflow Foundation (WF) のサンプルのほとんどは、コンソール アプリケーションでホストされるワークフローを使用しますが、実際のワークフローにとって現実的なシナリオはありません。 実際のビジネス アプリケーションのワークフローは、開発者が作成した Windows サービス、[!INCLUDE[iisver](../../../includes/iisver-md.md)] や AppFabric などのサーバー アプリケーションのいずれかの永続的なプロセスでホストされます。 これらの方法の違いを次に示します。  
  
## <a name="hosting-workflows-in-iis-with-windows-appfabric"></a>Windows AppFabric を使用した IIS でのワークフローのホスト  
 IIS と AppFabric は、ワークフローに推奨されるホストです。 AppFabric を使用したワークフローのホスト アプリケーションは Windows プロセス アクティブ化サービスで、これは IIS を介した HTTP への依存関係のみを解消します。  
  
## <a name="hosting-workflows-in-iis-alone"></a>IIS のみでのワークフローのホスト  
 [!INCLUDE[iisver](../../../includes/iisver-md.md)] のみを使用することは推奨されていません。AppFabric には、実行中のアプリケーションのメンテナンスを容易にする管理ツールと監視ツールがあるためです。 ワークフローを [!INCLUDE[iisver](../../../includes/iisver-md.md)] のみでホストする必要があるのは、AppFabric への移行に関してインフラストラクチャ上の問題がある場合だけです。  
  
> [!WARNING]
>  さまざまな理由により、アプリケーション プールは [!INCLUDE[iisver](../../../includes/iisver-md.md)] によって定期的にリサイクルされます。 アプリケーション プールがリサイクルされると、IIS は古いプールへのメッセージの受け取りを中止し、新しいアプリケーション プールをインスタンス化して新しい要求を受け取ります。 ワークフローが応答の送信後も動作し続ける場合、[!INCLUDE[iisver](../../../includes/iisver-md.md)] は作業が完了したことを認識せず、ホスト アプリケーション プールをリサイクルする可能性があります。 このエラーは、ワークフローが中断され、追跡サービスが記録される場合、 [1004 - WorkflowInstanceAborted](../../../docs/framework/windows-workflow-foundation/1004-workflowinstanceaborted.md)理由フィールドが空白のメッセージ。  
>   
>  永続化を使用する場合、ホストは、最後の永続性ポイントから、中止されたインスタンスを明示的に再開する必要があります。  
>   
>  AppFabric を使用する場合、永続化を使用すると、ワークフロー管理サービスは、最終的に、最後に成功した永続性ポイントからワークフローを再開します。 永続化を使用せず、ワークフローが要求/応答パターン以外の操作を実行している場合、ワークフローが中止されるとデータは失われます。  
  
## <a name="hosting-a-workflow-in-a-custom-windows-service"></a>カスタム Windows サービスでのワークフローのホスト  
 カスタム ワークフロー サービスを作成してワークフローをホストする場合、開発者は AppFabric に標準搭載されている多くの機能を複製する必要がありますが、カスタム機能をより柔軟に使用できるようになります。 このオプションは、AppFabric を選択できない場合にのみ検討してください。
