---
title: SQL Workflow Instance Store
ms.date: 03/30/2017
ms.assetid: 8cd2f8a5-4bf8-46ea-8909-c7fdb314fabc
ms.openlocfilehash: 81f11b9f88fbe425a07e553e64a08761dca3a2b4
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="sql-workflow-instance-store"></a>SQL Workflow Instance Store
[!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] には SQL Workflow Instance Store が含まれます。これを使用すると、ワークフロー インスタンスに関する状態情報を SQL Server 2005 または SQL Server 2008 のデータベースに永続化できます。 この機能は主に <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> クラスの形式で実装されます。このクラスは永続化フレームワークの <xref:System.Runtime.DurableInstancing.InstanceStore> 抽象クラスから派生します。 SQL Workflow Instance Store 機能によって SQL 永続性プロバイダーを構成します。このプロバイダーは、ホストが永続化コマンドをストアに送信するときに使用する永続化 API の具象実装です。  
  
 SQL Workflow Instance Store は、セルフホストされているワークフローや、<xref:System.Activities.WorkflowApplication> または <xref:System.ServiceModel.WorkflowServiceHost> を使用するワークフロー サービスだけでなく、<xref:System.ServiceModel.WorkflowServiceHost> を使用して WAS でホストされるサービスをサポートします。 セルフホストされているサービスの SQL Workflow Instance Store 機能をプログラムで構成するには、この機能が公開しているオブジェクト モデルを使用します。 プログラムでオブジェクト モデルや XML 構成ファイルを使用することにより、<xref:System.ServiceModel.WorkflowServiceHost> でホストされるサービスについてこの機能を構成できます。  
  
 SQL Workflow Instance Store 機能 (**SqlWorkflowInstanceStore**クラス) を実装していません<xref:System.ServiceModel.Persistence.PersistenceProviderFactory>非ワークフローの永続性の WCF サービスの永続性サポートを提供しないためです。 また、<xref:System.Workflow.Runtime.Hosting.WorkflowPersistenceService> を実装していないため、3.x ワークフローの永続化は提供しません。 この機能は、WF 4.0 以降のワークフローとワークフロー サービスについてのみ永続化をサポートします。 また、SQL Server 2005 と SQL Server 2008 以外のデータベースはサポートしません。  
  
 このセクションのトピックでは、SQL Workflow Instance Store のプロパティと機能、およびストアの構成方法の詳細を説明します。  
  
 Windows Server App Fabric には、インスタンス ストアを簡単に構成および使用できる独自のインスタンス ストアとツールが用意されています。 詳細については、次を参照してください。 を参照してください[Windows Server App Fabric のインスタンス ストア](http://go.microsoft.com/fwlink/?LinkId=201201)です。 App Fabric SQL サーバー永続性データベース参照の詳細については[App Fabric SQL Server 永続化データベース](http://go.microsoft.com/fwlink/?LinkId=201202)  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [SQL Workflow Instance Store のプロパティ](../../../docs/framework/windows-workflow-foundation/properties-of-sql-workflow-instance-store.md)  
  
-   [ワークフローとワークフロー サービスの SQL 永続性を有効にする方法](../../../docs/framework/windows-workflow-foundation/how-to-enable-sql-persistence-for-workflows-and-workflow-services.md)  
  
-   [インスタンスのアクティブ化処理](../../../docs/framework/windows-workflow-foundation/instance-activation.md)  
  
-   [クエリのサポート](../../../docs/framework/windows-workflow-foundation/support-for-queries.md)  
  
-   [ストア拡張](../../../docs/framework/windows-workflow-foundation/store-extensibility.md)  
  
-   [セキュリティ](../../../docs/framework/windows-workflow-foundation/security.md)  
  
-   [SQL Server 永続性データベース](../../../docs/framework/windows-workflow-foundation/sql-server-persistence-database.md)  
  
## <a name="see-also"></a>関連項目  
 [永続性のサンプル](http://go.microsoft.com/fwlink/?LinkID=177735)
