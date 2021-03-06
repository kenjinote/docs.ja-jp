---
title: Windows Communication Foundation サンプルの 1 回限りのセットアップの手順
ms.date: 03/30/2017
ms.assetid: a5848ffd-3eb5-432d-812e-bd948ccb6bca
ms.openlocfilehash: e3bf4d70217a8231fe4ddc5b9a15afdfe8f0522e
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="one-time-setup-procedure-for-the-windows-communication-foundation-samples"></a>Windows Communication Foundation サンプルの 1 回限りのセットアップの手順
ほとんどの Windows Communication Foundation (WCF) サンプルでは、インターネット インフォメーション サービス (IIS) でホストされているされ、共通の仮想ディレクトリから実行することができます。 この 1 回限りのセットアップの手順では、ディスクにフォルダーを作成します。という名前の iis 仮想ディレクトリも追加**ServiceModelSamples**です。  
  
 **ServiceModelSamples**の構築と、IIS でホストされるサービスを使用するすべてのサンプルを実行する仮想ディレクトリを使用します。 サンプルの実行に必要な仮想ディレクトリはこれだけです。 サンプルをビルドすると、この仮想ディレクトリにある、以前に配置されたサービスがすべて置き換えられます。この仮想ディレクトリには最近ビルドされたサンプルだけが配置されるため、そのサンプルしか使用できません。  
  
> [!NOTE]
>  すべてのコマンドは、ローカル管理者アカウントで実行する必要があります。 Windows 7、[!INCLUDE[windowsver](../../../../includes/windowsver-md.md)]、または Windows Server 2008 R2 を使用している場合は、コマンド プロンプトも管理者権限で実行する必要があります。 これを行うには、コマンド プロンプト アイコンを右クリックし、をクリックして**管理者として実行**です。 このトピックで使用するすべてのコマンドは、適切なパスが設定されているコマンド プロンプトで実行する必要があります。  このようにするための最も簡単な方法は、Visual Studio コマンド プロンプトを使用する方法です。 このプロンプトを開くにはクリックして**開始****すべてのプログラム**、まで下にスクロール**Visual Studio 2010**を選択**Visual Studio Tools**、右クリック**Visual Studio コマンド プロンプト (2010)**、クリックして**管理者として実行**です。 Visual Studio Express Editions のいずれかがインストールされている場合は、このコマンド プロンプトを使用できません。この場合、システム パスに "C:\Windows\Microsoft.Net\Framework\v4.0" を追加する必要があります。  
  
### <a name="one-time-setup-procedure-for-wcf-samples"></a>WCF サンプルの 1 回限りのセットアップの手順  
  
1.  [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] がセットアップされていることを確認します。 設定する方法の詳細についての[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]を参照してください[インターネット情報サービスのホスティング手順](../../../../docs/framework/wcf/samples/internet-information-service-hosting-instructions.md)です。  
  
2.  [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)] がインストールされていることを確認します。 V4.0 のディレクトリ (またはそれ以降)、次を検索: **\Windows\Microsoft.NET\Framework**  
  
3.  場合[!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)]がインストールされていないオペレーティング システムが Windows Server 2008 SP2 または後で、インストールと[修正プログラム 251798](http://go.microsoft.com/fwlink/?LinkId=184693)です。  
  
4.  次のコマンドを実行します。 これらのコマンドを実行する必要があります理由の詳細については、次を参照してください。 [IIS ホストされるサービスが失敗した](http://msdn.microsoft.com/library/ee5499fc-1b10-4cda-a9b1-13dba70f05f8)です。  
  
    > [!WARNING]
    >  IIS を再インストールした場合は、次のコマンドを再実行します。  
  
    ```  
    "%WINDIR%\Microsoft.Net\Framework\v4.0.30319\aspnet_regiis" –i –enable  
    "%WINDIR%\Microsoft.Net\Framework\v4.0.30319\ServiceModelReg.exe" -r  
    ```  
  
    > [!WARNING]
    >  コマンドを実行して`aspnet_regiis –i –enable`すると、既定のアプリケーション プールを使用して実行[!INCLUDE[netfx40_short](../../../../includes/netfx40-short-md.md)]アプリケーションが同じコンピューター上の非互換性問題が発生する可能性があります。  
  
5.  以下の[ファイアウォール手順](../../../../docs/framework/wcf/samples/firewall-instructions.md)サンプルで使用されるポートを有効にするためです。  
  
6.  次の既定のディレクトリの確認: \<InstallDrive >:**\WF_WCF_Samples**です。 サンプルが既にインストールされている場合は、これが既定のディレクトリです。  
  
7.  サンプルがインストールされていない場合、サンプルのダウンロード場所からのインストール[Visual c#](http://go.microsoft.com/fwlink/?LinkId=190939)または[Visual Basic](http://go.microsoft.com/fwlink/?LinkID=193373)です。  
  
8.  サンプルのインストール後に移動: \<InstallDrive >:**\WF_WCF_Samples\WCF\Setup\\**  
  
9. 実行、 **Setupvroot.bat**バッチ ファイルです。 次の手順が実行されます。  
  
    -   ServiceModelSamples という名前の仮想ディレクトリが IIS に作成されます。  
  
    -   %SystemDrive%\Inetpub\wwwroot\ServiceModelSamples and %SystemDrive%\Inetpub\wwwroot\ServiceModelSamples\bin という名前の新しいディスク ディレクトリが作成されます。  
  
     これらのディレクトリを手動で設定する場合を参照してください、[仮想ディレクトリのセットアップ手順](../../../../docs/framework/wcf/samples/virtual-directory-setup-instructions.md)です。 この手順で行ったすべての変更を元に戻すには、サンプルの使用が終わった後で cleanupvroot.bat を実行します。  
  
    > [!NOTE]
    >  cleanupvroot.bat を実行しない限り、この手順を実行するのは、1 台のコンピューターで 1 回だけです。  
  
10. サンプルおよび Network Service ユーザーのビルドに使用するアカウントに対し、%SystemDrive%\inetpub\wwwroot の変更権限を付与する必要があります。 ビルドの実行時に、Web ホストの一部のサンプルがコンパイル済みバイナリを前述の場所にコピーしようとする場合があり、適切な権限が設定されていないと、ビルドは破損します。 代わりに、アクセス許可の設定はそのままにして、SDK コマンド プロンプトまたは Visual Studio コマンド プロンプト (2012) を管理者として実行するか、[!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] を管理者として実行し、サンプルをビルドすることもできます。  
  
    > [!NOTE]
    >  この手順を完了していない場合は、ビルドの実行時に IIS でホストされているすべてのサンプルでエラーが発生します。 アクセス許可が正しく設定されていることを確認するか、SDK コマンド プロンプトと Visual Studio コマンド プロンプト (2012) を管理者として実行してください。  
  
11. コンピューター上に C:\logs ディレクトリを作成します (一部のサンプルで必要になることがあります)。 このフォルダーに対する書き込みアクセスが適切なアカウントに付与されていることを確認してください。 Windows 7、 [!INCLUDE[wv](../../../../includes/wv-md.md)]、このアカウントは、Windows Server 2008 R2、および**Network Service**です。 [!INCLUDE[lserver](../../../../includes/lserver-md.md)] では NT Authority\Network Service、 [!INCLUDE[wxp](../../../../includes/wxp-md.md)] および [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] では ASPNET です。  
  
12. Setupcerttool.bat ファイルを実行します。 このファイルにあります、 \<InstallPath > \WF_WCF_Samples\WCF\Setup\ フォルダーです。  このスクリプトでは、次のタスクが実行されます。  
  
    -   FindPrivateKey ツールをビルドします。  
  
    -   %ProgramFiles%\ServiceModelSampleTools という名前のディレクトリを作成します。  
  
    -   新しい FindPrivateKey ツールをこのディレクトリにコピーします。  
  
     このツールは、証明書を使用して IIS でホストされるサンプルで必要です。  
  
    > [!NOTE]
    >  セキュリティの目的で、サンプルの使用が終わったら、このセットアップ手順で付与された仮想ディレクトリの定義とアクセス許可を必ず削除してください。削除するには、Cleanupvroot.bat という名前のバッチ ファイルを実行します。  
  
13. 自己ホスト型の (IIS でホストされていない) サンプルでは、リッスンを行うコンピューター上で HTTP アドレスを登録するためのアクセス許可が必要です。 HTTP 名前空間予約のアクセス許可は、サンプルの実行に使用されるユーザー アカウントから提供されます。 既定では、管理者アカウントには、任意の HTTP アドレスを登録するためのアクセス許可があります。 管理者以外のアカウントの場合は、サンプルで使用される HTTP 名前空間へのアクセス許可が付与される必要があります。 名前空間の予約を構成する方法の詳細については、次を参照してください。[を構成する HTTP および HTTPS](../../../../docs/framework/wcf/feature-details/configuring-http-and-https.md)です。  
  
14. 一部のサンプルにはメッセージ キューが必要です。 参照してください[をインストールするメッセージ キュー (MSMQ)](../../../../docs/framework/wcf/samples/installing-message-queuing-msmq.md)インストール手順についてはします。  
  
    > [!NOTE]
    >  メッセージ キューが必要なサンプルを実行する場合は、MSMQ サービスを事前に開始しておいてください。  
  
15. 一部のサンプルには証明書が必要です。 参照してください[インターネット インフォメーション サービス (IIS) サーバー証明書のインストール手順](../../../../docs/framework/wcf/samples/iis-server-certificate-installation-instructions.md)です。  
  
## <a name="see-also"></a>関連項目
