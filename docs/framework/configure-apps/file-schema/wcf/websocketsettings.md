---
title: '&lt;webSocketSettings&gt;'
ms.date: 03/30/2017
ms.assetid: bbf97e02-8dd1-4922-acac-3cd33397b249
ms.openlocfilehash: 84aee31b6c15beb32732f89eae7c3d176f57971d
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="ltwebsocketsettingsgt"></a>&lt;webSocketSettings&gt;
Web ソケット設定を指定するために使用される構成要素。  
  
\<system.ServiceModel >  
\<bindings>  
\<netHttpBinding>  
  
## <a name="syntax"></a>構文  
  
```xml  
<netHttpBinding>  
  <binding>   
    <webSocketSettings createNotificationOnConnection="boolean" 
                       disablePayloadMasking="boolean" 
                       keepAliveInterval="TimeSpan" 
                       maxPendingConnections="Integer" 
                       receiveBufferSize="Integer" 
                       sendBufferSize="Integer" 
                       subProtocol="String" 
                       transportUsage="WhenDuplex/Always/Never"/>
  </binding>  
</netHttpBinding>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|createNotificationOnConnection|通知を接続時に送信するかどうかを指定します。|  
|disablePayloadMasking|Web ソケットのマスクが無効であるかどうかを指定します。|  
|keepAliveInterval|接続維持の間隔を指定します。|  
|maxPendingConnections|サービスでのディスパッチを待機している接続の最大数を指定します。|  
|receiveBufferSize|受信バッファーのサイズを指定します。|  
|sendBufferSize|送信バッファーのサイズを指定します。|  
|subProtocol|Web ソケットのサブプロトコルを指定します。|  
|transportUsage|Web ソケットを使用するタイミングを指定します。|  
  
## <a name="transportusage-attribute"></a>transportUsage 属性  
  
|値|説明|  
|-----------|-----------------|  
|WhenDuplex|コントラクトが双方向の場合に、Web ソケット プロトコルを使用します。|  
|Always|コントラクトにかかわらず、常にWeb ソケット プロトコルを使用します。|  
|Never|Web ソケット プロトコルを使用しません。|  
  
### <a name="child-elements"></a>子要素  
 なし  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|\<netHttpBinding>|NetHttpBinding を指定します。|  
  
## <a name="example"></a>例  
 次の例を使用する方法を示しています、 \<webSocketSettings > 要素。  
  
```xml  
<netHttpBinding>  
        <binding>  
          <webSocketSettings createNotificationOnConnection="true"  
                              disablePayloadMasking="false  
                              keepAliveInterval="00:10:00"  
                              maxPendingConnections="100"  
                              receiveBufferSize="1000"  
                              sendBufferSize="1000"  
                              subProtocol="Soap"  
                              transportUsage="WhenDuplex/Always/Never"/>  
  
        </binding>  
      </netHttpBinding>  
```  
  
## <a name="see-also"></a>関連項目  
 <xref:System.ServiceModel.Channels.Binding>  
 <xref:System.ServiceModel.Channels.BindingElement>  
 <xref:System.ServiceModel.BasicHttpBinding>  
 <xref:System.ServiceModel.Configuration.BasicHttpBindingElement>  
 [バインディング](../../../../../docs/framework/wcf/bindings.md)  
 [システムが提供するバインディングの構成](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)  
 [バインディングを使用して、Windows Communication Foundation サービスとクライアントを構成するには](http://msdn.microsoft.com/library/bd8b277b-932f-472f-a42a-b02bb5257dfb)  
 [\<binding>](../../../../../docs/framework/misc/binding.md)
