---
title: 118 - WorkflowInstanceUnhandledExceptionRecordWithId
ms.date: 03/30/2017
ms.assetid: 2ce4b193-e141-4cc4-86a3-2e8c984c110d
ms.openlocfilehash: eb69fc4760cd89294e24680b5aab83fcd058feb0
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="118---workflowinstanceunhandledexceptionrecordwithid"></a>118 - WorkflowInstanceUnhandledExceptionRecordWithId
## <a name="properties"></a>プロパティ  
  
|||  
|-|-|  
|ID|118|  
|キーワード|HealthMonitoring、WFTracking|  
|レベル|Error|  
|チャネル|Microsoft-Windows-Application Server-Applications/Analytic|  
  
## <a name="description"></a>説明  
 このイベントは、ワークフロー インスタンスが WorkflowInstanceUnhandledExceptionRecord を生成したときに、ETW 追跡参加要素によって生成されます。  
  
## <a name="message"></a>メッセージ  
 TrackRecord = WorkflowInstanceUnhandledExceptionRecord, InstanceID = %1、RecordNumber = %2、EventTime = %3、ActivityDefinitionId = %4、SourceName = %5、SourceId = %6、SourceInstanceId = %7、SourceTypeName = %8、Exception = %9、Annotations = %10、ProfileName =%11、WorkflowDefinitionIdentity = %12  
  
## <a name="details"></a>説明  
  
|データ項目名|データ項目の型|説明|  
|--------------------|--------------------|-----------------|  
|InstanceId|xs:GUID|ワークフローのインスタンス ID|  
|RecordNumber|xs:long|生成されたレコードのシーケンス番号|  
|EventTime|xs:dateTime|イベントの生成時刻 (UTC)|  
|ActivityDefinitionId|xs:string|ワークフローのルート アクティビティの名前|  
|SourceName|xs:string|失敗して unhandledException が発生した原因のアクティビティ名|  
|SourceId|xs:string|エラーの原因であるアクティビティのアクティビティ ID|  
|SourceInstanceId|xs:string|エラーの原因であるアクティビティのアクティビティ インスタンス ID|  
|SourceTypeName|xs:string|失敗して unhandledException が発生した原因のアクティビティの型名|  
|例外|xs:string|ハンドルされない例外の詳細|  
|状態|xs:string|ワークフローの現在の状態。|  
|コメント|xs:string|このイベントに追加された注釈。 形式で xml 要素に値が格納されている\<項目 >\<項目名 ="annotationName"type="System.String"> annotationValue\<項目/>\</items >。 注釈が指定されていない場合、文字列が含まれる\<項目/>。 ETW イベントのサイズは、ETW バッファーのサイズまたは ETW イベントの最大ペイロードに制限されます。 イベントのサイズが ETW の制限を超えるかどうかは、注釈を削除しを持つ注釈の値を置き換えることによって、イベントが切り捨てられ\<項目 >.\</items >。|  
|ProfileName|xs:string|このイベントを生成した追跡プロファイルの名前|  
|WorkflowDefinitionIdentity|xs:string|ワークフロー定義 ID|  
|AppDomain|xs:string|AppDomain.CurrentDomain.FriendlyName で返される文字列。|
