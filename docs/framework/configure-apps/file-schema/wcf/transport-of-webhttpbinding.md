---
title: '&lt;webHttpBinding&gt; の &lt;transport&gt;'
ms.date: 03/30/2017
ms.assetid: f150fb19-7de1-44af-81f4-86cad881cd05
ms.openlocfilehash: 17468bc2354dc2865f10384e918ffb821a28f059
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="lttransportgt-of-ltwebhttpbindinggt"></a>&lt;webHttpBinding&gt; の &lt;transport&gt;
HTTP 要求を受信するように構成されたサービス エンドポイントのトランスポート レベルのセキュリティ設定を定義します。  
  
 \<system.ServiceModel >  
\<bindings>  
\<webHttpBinding>  
\<binding>  
\<セキュリティ >  
\<transport>  
  
## <a name="syntax"></a>構文  
  
```xml  
<webHttpBinding>  
    <binding>  
        <security  
        mode="None|Transport|Message|TransportWithMessageCredential|TransportCredentialOnly">  
            <transport clientCredentialType="None|Basic|Digest|Ntlm|Windows"  
             proxyCredentialType="None|Basic|Digest|Ntlm|Windows" realm="string" >  
                <extendedProtectionPolicy  
                     policyEnforcement="Never|WhenSupported|Always"  
                     protectionScenario="TransportSelected|TrustedProxy">  
                    <customServiceNames></customServiceNames>  
                        </extendedProtectionPolicy>  
            </transport>  
        </security>  
    </binding>  
</WebHttpBinding>  
```  
  
## <a name="type"></a>型  
 <xref:System.ServiceModel.HttpTransportSecurity>  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`clientCredentialType`|サービスに対するクライアントの認証に使用される資格情報を指定します。 この属性は <xref:System.ServiceModel.HttpClientCredentialType> 型です。|  
|`proxyCredentialType`|ドメイン プロキシに対するクライアントの認証に使用される資格情報を指定します。 この属性は <xref:System.ServiceModel.HttpProxyCredentialType> 型です。|  
|`realm`|ダイジェストまたは基本認証の認証レルムを指定する文字列。 既定値は空の文字列です。<br /><br /> 認証レルムでは、少なくとも、認証を実行するホストの名前を指定します。 アクセス権のあるユーザーのコレクションも指定できます。 ユーザーは、認証レルムを照会して、複数のユーザー名およびパスワードの候補のうち、どれを使用できるかを確認することができます。|  
|`policyEnforcement`|この列挙体は、<xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy> を適用するタイミングを指定します。<br /><br /> 1.Never – ポリシーが適用されることはありません (拡張保護は無効になります)。<br />2.WhenSupported – ポリシーが適用されるのは、クライアントが拡張保護をサポートしている場合のみです。<br />3.Always – ポリシーは常に適用されます。 拡張保護をサポートしていないクライアントは認証に失敗します。|  
  
## <a name="clientcredentialtype-attribute"></a>clientCredentialType 属性  
  
|値|説明|  
|-----------|-----------------|  
|`None`|セキュリティを無効にします。|  
|`Basic`|基本認証を使用します。|  
|`Certificate`|X.509 証明書を使用して、クライアントを認証します。|  
|`Digest`|ダイジェスト認証を使用します。|  
|`Ntlm`|Windows ドメインのフォールバックとして NTLM 認証を使用します。|  
|`Windows`|統合 Windows 認証を使用します。|  
  
## <a name="proxycredentialtype-attribute"></a>proxyCredentialType 属性  
  
|値|説明|  
|-----------|-----------------|  
|`None`|セキュリティを無効にします。|  
|`Basic`|基本認証を使用します。|  
|`Digest`|ダイジェスト認証を使用します。|  
|`Ntlm`|Windows ドメインのフォールバックとして NTLM を使用します。|  
|`Windows`|統合 Windows 認証を使用します。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<security>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-webhttpbinding.md)|セキュリティ機能を表す、 [ \<wsHttpBinding >](../../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)要素。|  
  
## <a name="see-also"></a>関連項目  
 <xref:System.ServiceModel.HttpTransportSecurity>  
 <xref:System.ServiceModel.Configuration.WebHttpSecurityElement.Transport%2A>  
 <xref:System.ServiceModel.WebHttpSecurity.Transport%2A>  
 <xref:System.ServiceModel.Configuration.HttpTransportSecurityElement>  
 [サービスおよびクライアントのセキュリティ保護](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)  
 [バインディング](../../../../../docs/framework/wcf/bindings.md)  
 [システムが提供するバインディングの構成](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)  
 [バインディングを使用して、Windows Communication Foundation サービスとクライアントを構成するには](http://msdn.microsoft.com/library/bd8b277b-932f-472f-a42a-b02bb5257dfb)  
 [\<binding>](../../../../../docs/framework/misc/binding.md)  
 [WCF Web HTTP プログラミング モデル](../../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)
