---
title: WCF の  &lt;activityScheduledQuery&gt;
ms.date: 03/30/2017
ms.assetid: 25f6eee1-3d98-4c39-b517-c0813f03f106
ms.openlocfilehash: 4efd6ba13e8a54d3338c25b077477d4abdbe9ab5
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="ltactivityscheduledquerygt-of-wcf"></a>WCF の  &lt;activityScheduledQuery&gt;
親アクティビティによる実行がスケジュールされているアクティビティを追跡するために使用する、クエリのコレクションを表します。 アクティビティがスケジュールされたレコードを追跡参加要素が定期受信するには、このクエリが必要です。  
  
 追跡プロファイルのクエリの詳細については、次を参照してください[追跡プロファイル。](../../../../../docs/framework/windows-workflow-foundation/tracking-profiles.md)  
  
 \<system.serviceModel>  
\<追跡 >  
\<trackingProfile>  
\<ワークフロー >  
\<activityScheduledQueries >  
\<activityScheduledQuery >  
  
## <a name="syntax"></a>構文  
  
```xml
<tracking>     <trackingProfile name="Name">       <workflow>          <activityScheduledQueries>             <activityScheduledQuery activityName="String"                 childActivityName="String"/>          </activityScheduledQueries>       </workflow>     </trackingProfile></tracking>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|activityName|キャンセルを要求しているアクティビティの名前を指定する文字列。|  
|childActivityName|キャンセルが要求された子アクティビティの名前を指定する文字列。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<activityScheduledQuery >](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/activityscheduledquery.md)|親アクティビティによる実行がスケジュールされているアクティビティを追跡するために使用するクエリ。|  
  
## <a name="see-also"></a>関連項目  
 <xref:System.ServiceModel.Activities.Tracking.Configuration.ActivityScheduledQueryElement>     
 <xref:System.Activities.Tracking.ActivityScheduledQuery>     
 [ワークフローの追跡とトレース](../../../../../docs/framework/windows-workflow-foundation/workflow-tracking-and-tracing.md)  
 [追跡プロファイル](../../../../../docs/framework/windows-workflow-foundation/tracking-profiles.md)
