---
title: '方法: MEX 以外のバインディングを介してメタデータを取得する'
ms.date: 03/30/2017
ms.assetid: 2292e124-81b2-4317-b881-ce9c1ec66ecb
ms.openlocfilehash: 198c343aa6f25d55e518990dc1dbd2667a8c17ad
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-retrieve-metadata-over-a-non-mex-binding"></a>方法: MEX 以外のバインディングを介してメタデータを取得する
ここでは、MEX 以外のバインディングを介して MEX エンドポイントからメタデータを取得する方法を説明します。 このサンプルのコードがに基づいて、[カスタム セキュリティで保護されたメタデータ エンドポイント](../../../../docs/framework/wcf/samples/custom-secure-metadata-endpoint.md)サンプルです。  
  
### <a name="to-retrieve-metadata-over-a-non-mex-binding"></a>MEX 以外のバインディングを介してメタデータを取得するには  
  
1.  MEX エンドポイントで使用されているバインディングを特定します。 Windows Communication Foundation (WCF) サービスのサービスの構成ファイルにアクセスして、MEX のバインディングを指定できます。 この場合、MEX バインディングは、次のサービス構成で定義されています。  
  
    ```xml  
    <services>  
        <service name="Microsoft.ServiceModel.Samples.CalculatorService"  
                behaviorConfiguration="CalculatorServiceBehavior">  
         <!-- Use the base address provided by the host. -->  
         <endpoint address=""  
           binding="wsHttpBinding"  
           bindingConfiguration="Binding2"  
           contract="Microsoft.ServiceModel.Samples.ICalculator" />  
         <endpoint address="mex"  
           binding="wsHttpBinding"  
           bindingConfiguration="Binding1"  
           contract="IMetadataExchange" />  
         </service>  
     </services>  
     <bindings>  
       <wsHttpBinding>  
         <binding name="Binding1">  
           <security mode="Message">  
             <message clientCredentialType="Certificate" />  
           </security>  
         </binding>  
         <binding name="Binding2">  
           <reliableSession inactivityTimeout="00:01:00" enabled="true" />  
           <security mode="Message">  
             <message clientCredentialType="Certificate" />  
           </security>  
         </binding>  
       </wsHttpBinding>  
     </bindings>  
    ```  
  
2.  クライアント構成ファイルで、同じカスタム バインディングを構成します。 ここでクライアントは `clientCredentials` 動作も定義して、MEX エンドポイントからメタデータを要求するときに、サービスに対する認証で使用する証明書を指定します。 カスタム バインドを介してメタデータを要求するときに Svcutil.exe を使用する場合は、Svcutil.exe の構成ファイル (Svcutil.exe.config) に MEX エンドポイント構成を追加する必要があります。また、エンドポイント構成の名前が、次のコードに示すように、MEX エンドポイントのアドレスの URI スキームと一致する必要があります。  
  
    ```xml  
    <system.serviceModel>  
      <client>  
        <endpoint name="http"  
                  binding="wsHttpBinding"  
                  bindingConfiguration="Binding1"  
                  behaviorConfiguration="ClientCertificateBehavior"  
                  contract="IMetadataExchange" />  
      </client>  
      <bindings>  
        <wsHttpBinding>  
          <binding name="Binding1">  
            <security mode="Message">  
              <message clientCredentialType="Certificate"/>  
            </security>  
          </binding>  
        </wsHttpBinding>  
      </bindings>  
      <behaviors>  
        <endpointBehaviors>  
          <behavior name="ClientCertificateBehavior">  
            <clientCredentials>  
              <clientCertificate findValue="client.com" storeLocation="CurrentUser" storeName="My" x509FindType="FindBySubjectName" />  
              <serviceCertificate>  
                <authentication certificateValidationMode="PeerOrChainTrust" />  
              </serviceCertificate>  
            </clientCredentials>  
          </behavior>  
        </endpointBehaviors>  
      </behaviors>    
    </system.serviceModel>  
    ```  
  
3.  `MetadataExchangeClient` を作成して `GetMetadata` を呼び出します。 これを行うには、次の例に示すように、構成でカスタム バインドを指定する方法と、コードでカスタム バインドを指定する方法の 2 つの方法があります。  
  
    ```  
    // The custom binding is specified in configuration.  
    EndpointAddress mexAddress = new EndpointAddress("http://localhost:8000/ServiceModelSamples/Service/mex");  
  
    MetadataExchangeClient mexClient = new MetadataExchangeClient("http");  
    mexClient.ResolveMetadataReferences = true;  
    MetadataSet mexSet = mexClient.GetMetadata(mexAddress);  
  
    // The custom binding is specified in code.  
    // Specify the Metadata Exchange binding and its security mode.  
    WSHttpBinding mexBinding = new WSHttpBinding(SecurityMode.Message);  
    mexBinding.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;  
  
    // Create a MetadataExchangeClient and set the certificate details.  
    MetadataExchangeClient mexClient = new MetadataExchangeClient(mexBinding);  
    mexClient.SoapCredentials.ClientCertificate.SetCertificate(  
        StoreLocation.CurrentUser, StoreName.My,  
        X509FindType.FindBySubjectName, "client.com");  
    mexClient.SoapCredentials.ServiceCertificate.Authentication.  
        CertificateValidationMode =  
        X509CertificateValidationMode.PeerOrChainTrust;  
    mexClient.SoapCredentials.ServiceCertificate.SetDefaultCertificate(  
        StoreLocation.CurrentUser, StoreName.TrustedPeople,  
        X509FindType.FindBySubjectName, "localhost");  
    MetadataExchangeClient mexClient2 = new MetadataExchangeClient(customBinding);  
    mexClient2.ResolveMetadataReferences = true;  
    MetadataSet mexSet2 = mexClient2.GetMetadata(mexAddress);  
    ```  
  
4.  次のコードに示すように、`WsdlImporter` を作成して `ImportAllEndpoints` を呼び出します。  
  
    ```  
    WsdlImporter importer = new WsdlImporter(mexSet);  
    ServiceEndpointCollection endpoints = importer.ImportAllEndpoints();  
    ```  
  
5.  この時点で、サービス エンドポイントのコレクションが取得されます。 メタデータのインポートの詳細については、次を参照してください。[する方法: サービス エンドポイントにメタデータのインポート](../../../../docs/framework/wcf/feature-details/how-to-import-metadata-into-service-endpoints.md)です。  
  
## <a name="see-also"></a>関連項目  
 [メタデータ](../../../../docs/framework/wcf/feature-details/metadata.md)
