---
title: トランスポート セキュリティでの偽装の使用
ms.date: 03/30/2017
ms.assetid: 426df8cb-6337-4262-b2c0-b96c2edf21a9
author: BrucePerlerMS
manager: mbaldwin
ms.openlocfilehash: 5a4b05031061183cf0dddd82c900065155b1e561
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="using-impersonation-with-transport-security"></a>トランスポート セキュリティでの偽装の使用
*権限借用*クライアントの id で実行するサーバー アプリケーションの機能です。 リソースへのアクセスを検証するときに、サービスでは偽装が広く使用されます。 サーバー アプリケーションはサービス アカウントを使用して実行されますが、クライアントの接続を受け入れたサーバーは、クライアントの資格情報を使用してアクセス チェックが実行できるようにクライアントを偽装します。 トランスポート セキュリティは、資格情報を渡すこと、および渡された資格情報を使用して通信をセキュリティで保護することの 2 つの機構から成ります。 このトピックを使用してトランスポート セキュリティには、Windows Communication Foundation (WCF) と共に偽装機能について説明します。 メッセージ セキュリティを使用して権限借用の詳細については、次を参照してください。[委任と偽装](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)です。  
  
## <a name="five-impersonation-levels"></a>5 つの偽装レベル  
 トランスポート セキュリティでは、次の表で説明するように 5 つの偽装レベルを使用します。  
  
|偽装レベル|説明|  
|-------------------------|-----------------|  
|なし|サーバー アプリケーションは、クライアントの偽装を試みません。|  
|Anonymous|サーバー アプリケーションはクライアントの資格情報に対してアクセス チェックを実行できますが、クライアントの ID に関する情報は一切受け取りません。 この偽装レベルは、名前付きパイプなど、コンピューター上での通信にのみ意味があります。 リモート接続で `Anonymous` レベルを使用すると、Identify レベルの偽装に昇格されます。|  
|Identify|サーバー アプリケーションは、クライアントの ID を認識し、クライアントの資格情報に対するアクセスの検証を実行できますが、クライアントを偽装することはできません。 識別は、トークン プロバイダーが異なる権限借用レベルを提供しない限り、WCF での SSPI 資格情報で使用される既定の権限借用レベルです。|  
|Impersonate|サーバー アプリケーションは、アクセス チェックを実行できるだけでなく、クライアントとしてサーバー コンピューターのリソースにアクセスできます。 偽装されたトークンにはネットワーク資格情報が含まれないため、サーバー アプリケーションはクライアントの ID を使用してリモート コンピューター上のリソースにアクセスできません。|  
|Delegate|`Impersonate` と同じ機能に加えて、Delegate レベルの偽装では、サーバー アプリケーションがクライアントの ID を使用してリモート コンピューターのリソースにアクセスし、この ID を他のアプリケーションに渡すことができます。<br /><br /> **重要な**サーバーのドメイン アカウントをマークする必要がありますをこれらの追加機能を使用するドメイン コント ローラー上で委任に対して信頼します。 このレベルの偽装は、機密としてマークされているクライアント ドメイン アカウントでは使用できません。|  
  
 トランスポート セキュリティで最もよく使用されるレベルは`Identify`と`Impersonate`です。 `None` および `Anonymous` レベルは、通常の使用にはお勧めしません。トランスポートの多くでは認証でこのレベルの使用をサポートしていません。 `Delegate` レベルの機能は強力であり、使用に際しては注意が必要です。 資格情報を委任するアクセス許可は、信頼できるサーバー アプリケーションにのみ与える必要があります。  
  
 `Impersonate` または `Delegate` レベルで偽装を使用するには、サーバー アプリケーションが `SeImpersonatePrivilege` 特権を持っている必要があります。 管理者グループのアカウントまたはサービス SID (Network Service、Local Service、または Local System) を持つアカウントでアプリケーションを実行している場合は、アプリケーションに既定でこの特権があります。 偽装ではクライアントとサーバーの相互認証は必要ありません。 NTLM など、偽装をサポートする認証方式の中には、相互認証を使用できないものもあります。  
  
## <a name="transport-specific-issues-with-impersonation"></a>偽装でのトランスポート固有の問題  
 WCF でのトランスポートの選択では、権限借用の選択肢に影響します。 このセクションでは、標準 HTTP に影響する問題について説明し、名前付きパイプ トランスポートで WCF です。 カスタム トランスポートには、偽装のサポートに関して独自の制限があります。  
  
### <a name="named-pipe-transport"></a>名前付きパイプ トランスポート  
 次の項目が名前付きパイプ トランスポートと共に使用されます。  
  
-   名前付きパイプ トランスポートはローカル コンピューター上のみで使用します。 WCF では、名前付きパイプ トランスポートは、コンピューター間の接続を明示的に否定します。  
  
-   名前付きパイプは、`Impersonate` または `Delegate` 偽装レベルでは使用できません。 これらの偽装レベルでは、名前付きパイプはコンピューター上で保障されません。  
  
 名前付きパイプの詳細については、次を参照してください。[トランスポート選択](../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)です。  
  
### <a name="http-transport"></a>HTTP トランスポート  
 HTTP トランスポートを使用するバインディング (<xref:System.ServiceModel.WSHttpBinding>と<xref:System.ServiceModel.BasicHttpBinding>) で説明したようにいくつかの認証スキームをサポート[Understanding HTTP 認証](../../../../docs/framework/wcf/feature-details/understanding-http-authentication.md)です。 サポートされる偽装レベルは、認証方式によって異なります。 次の項目が HTTP トランスポートと共に使用されます。  
  
-   `Anonymous` 認証方式は偽装を無視します。  
  
-   `Basic`のみ認証スキームをサポート、`Delegate`レベル。 これより低い偽装レベルは、アップグレードされます。  
  
-   `Digest` 認証方式では、`Impersonate` レベルと `Delegate` レベルのみをサポートします。  
  
-   `NTLM` 認証方式は、直接またはネゴシエーション経由で選択可能で、ローカル コンピューターで `Delegate` レベルのみをサポートします。  
  
-   Kerberos 認証方式は、ネゴシエーション経由でのみ選択可能で、サポートされるすべての偽装レベルで使用できます。  
  
 HTTP トランスポートの詳細については、次を参照してください。[トランスポート選択](../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)です。  
  
## <a name="see-also"></a>関連項目  
 [委任と偽装](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)  
 [承認](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)  
 [方法: サービスでクライアントに偽装する](../../../../docs/framework/wcf/how-to-impersonate-a-client-on-a-service.md)  
 [HTTP 認証の理解](../../../../docs/framework/wcf/feature-details/understanding-http-authentication.md)
