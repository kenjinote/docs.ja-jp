---
title: 3501 - InferredContractDescription
ms.date: 03/30/2017
ms.assetid: 21a70849-4fc0-41d2-b9a4-db5aa2acdf1a
ms.openlocfilehash: 47a5d98f4510e8c6092e8533a98366141d4b24db
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="3501---inferredcontractdescription"></a>3501 - InferredContractDescription
## <a name="properties"></a>プロパティ  
  
|||  
|-|-|  
|ID|3501|  
|キーワード|WFServices|  
|レベル|情報|  
|チャネル|Microsoft-Windows-Application Server-Applications/Analytic|  
  
## <a name="description"></a>説明  
 ContractDescription が WorkflowService から推論されたことを示します。  
  
## <a name="message"></a>メッセージ  
 Name='%1' で Namespace='%2' の ContractDescription が WorkflowService から推論されました。  
  
## <a name="details"></a>詳細  
  
|データ項目名|データ項目の型|説明|  
|--------------------|--------------------|-----------------|  
|名前|xs:string|ContractDescription の名前。|  
|Namespace|xs:string|ContractDescription の名前空間。|  
|AppDomain|xs:string|AppDomain.CurrentDomain.FriendlyName で返される文字列。|
