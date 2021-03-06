---
title: 仮想ディレクトリのセットアップ手順
ms.date: 03/30/2017
ms.assetid: 3c62cab5-81a4-48b6-ac8c-9ce33a85a157
ms.openlocfilehash: 3ff578b69590071ef2135e777b3105e7c226563e
ms.sourcegitcommit: 15109844229ade1c6449f48f3834db1b26907824
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2018
---
# <a name="virtual-directory-setup-instructions"></a>仮想ディレクトリのセットアップ手順
Windows Communication Foundation (WCF) サンプルは %SystemDrive%\inetpub\wwwroot\servicemodelsamples フォルダーにマップされている servicemodelsamples という仮想ディレクトリを共有します。  
  
> [!NOTE]
>  %SystemDrive% は、インターネット インフォメーション サービス (IIS) がインストールされているドライブの場所に応じて、通常は C: または D: になります。  
  
 ファイルを Setupvroot.bat と Cleanupvroot.bat を実行することができます、 [Windows Communication Foundation サンプルの 1 回限りのセットアップ手順](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)仮想ディレクトリを作成します。 この仮想ディレクトリを手動で作成する場合は、次の手順に従います。  
  
## <a name="procedures"></a>手順  
  
#### <a name="to-create-a-virtual-directory-in-iis-70-or-75"></a>IIS 7.0 または 7.5 で仮想ディレクトリを作成するには  
  
1.  **開始** メニューのをクリックして**実行**、入力**inetmgr**を開くには、インターネット インフォメーション サービス (IIS) MMC スナップイン。  
  
2.  左側のウィンドウで、コンピューターの名前を持つノードを展開し、展開、**サイト**ノード。  
  
3.  右クリック**既定の Web サイト**、し、**アプリケーションの追加**を開くには、**追加のアプリケーション ウィンドウ**します。  
  
4.  ウィンドウで、次のように入力します。`servicemodelsamples`として作成している仮想ディレクトリのエイリアスです。  
  
5.  次のディレクトリを作成します。%SystemDrive%\inetpub\wwwroot\servicemodelsamples  
  
6.  物理パスを %SystemDrive%\inetpub\wwwroot\servicemodelsamples に設定します。  WCF サンプルの多くは、ビルド時にサービス実行可能ファイルをこの場所にコピーします。  
  
7.  **[OK]** をクリックします。 Web アプリケーションが、WCF サンプル用に作成されました。  
  
    > [!NOTE]
    >  このタスクは、同じ servicemodelsamples Web アプリケーションを使用するすべての WCF サンプルために、1 回だけ実行する必要があります。  
  
    > [!NOTE]
    >  このドキュメントでは、`virtual directory`という用語は `Web application`と同じ意味で使用しています。  
  
     仮想ディレクトリを作成するだけでなく、実行する WCF サービスを有効にするには、そのプロパティを設定することも必要があります。 詳細については、以下を参照してください。  
  
#### <a name="to-create-a-virtual-directory-in-iis-51-or-60"></a>仮想ディレクトリを IIS 5.1 または 6.0 で作成するには  
  
1.  コマンド プロンプト ウィンドウを開き`start inetmgr`を開くには、インターネット インフォメーション サービス (IIS) MMC スナップイン。  
  
2.  左側のウィンドウで、コンピューターの名前を持つノードを展開し、展開、 **Websites**ノード。  
  
3.  右クリック**既定の Web サイト**選択**、新しい仮想ディレクトリ**仮想ディレクトリの作成ウィザードを開きます。  
  
4.  ウィザードで、次のように入力します。`servicemodelsamples`として作成している仮想ディレクトリのエイリアスです。  
  
5.  パスを %SystemDrive%\inetpub\wwwroot\servicemodelsamples に設定します。 WCF サンプルの多くは、ビルド時にサービス実行可能ファイルをこの場所にコピーします。  
  
6.  **[次へ]** をクリックします。  
  
7.  既定では、次のチェック ボックスがオンになっています。  
  
    -   **読み取り**  
  
    -   **(ASP) などのスクリプトを実行します。**  
  
8.  をクリックして **[次へ]**、順にクリック**完了**ウィザードを完了します。  
  
    > [!NOTE]
    >  このタスクは、すべての WCF サンプルには、同じ servicemodelsamples 仮想ディレクトリが使用するため、1 回だけ実行する必要があります。  
  
#### <a name="to-set-additional-virtual-directory-properties-in-iis-70-or-75"></a>IIS 7.0 での他の仮想ディレクトリのプロパティまたは 7.5 を設定するには  
  
1.  servicemodelsamples ノードをクリックします。 ウィンドウの下端に沿って 2 つのビューが表示されます。 選択**機能ビュー**が選択されていない場合。  
  
2.  エントリをダブルクリックして**ディレクトリの参照**です。  
  
3.  [操作] ウィンドウで、選択、**を有効にする**オプション。 これにより、Internet Explorer でディレクトリにアクセスできるようになり、サービスのデバッグに役立ちます。  
  
 最後に、servicemodelsamples フォルダーのセキュリティ プロパティを、他のユーザーがアクセスできるように設定する必要があります。 詳細については、以下を参照してください。  
  
#### <a name="to-set-additional-virtual-directory-properties-in-iis-51-or-60"></a>仮想ディレクトリの追加プロパティを IIS 5.1 または 6.0 で設定するには  
  
1.  Servicemodelsamples ノードを右クリックし、をクリックして**プロパティ**です。  
  
2.  既定では、次のチェック ボックスがオンになっています。  
  
    -   **読み取り**  
  
    -   **[ログ アクセス]**  
  
    -   **このリソースします。**  
  
3.  選択、**ディレクトリの参照**チェック ボックスをオンします。 これにより、Internet Explorer でディレクトリにアクセスできるようになり、サービスのデバッグに役立ちます。  
  
#### <a name="to-set-security-properties-of-the-folder-in-iis-70-or-75"></a>IIS 7.0 または 7.5 でフォルダーのセキュリティ プロパティを設定するには  
  
1.  %SystemDrive%\inetpub\wwwroot\servicemodelsamples に移動します。  
  
2.  Servicemodelsamples フォルダーを右クリックし、をクリックして**共有**または**共有で**です。  
  
3.  左側にある下向きの矢印をクリックして、**追加**ボタンをクリックします。  
  
4.  選択、**検索**エントリです。 **ユーザーまたはグループ**ウィンドウが開きます。  
  
5.  **[詳細設定]** をクリックします。  
  
6.  をクリックして**場所**です。 **場所**ウィンドウが開きます。  
  
7.  使用するコンピューターのエントリを選択します。 一覧表示されているドメインやネットワークのエントリではなく、ローカル コンピューターを選択してください。 コンピューターを選択した後にをクリックして**OK**です。  
  
8.  をクリックして**今すぐ検索**です。 これで、ローカル コンピューターに関連付けられたオブジェクトが検索結果に表示されます。  
  
9. 検索、 **IIS_IUSRS**内のエントリ、**名 (相対識別名)** 列です。 そのエントリを選択し、をクリックして**OK**結果ウィンドウの検索を閉じます。  
  
10. をクリックして**OK**を閉じる、 **ユーザーまたはグループ**ウィンドウです。  
  
11. をクリックして**共有**変更を保持します。  
  
12. 共有を有効にする変更が完了した後にをクリックして**完了**を閉じる、**ファイルの共有**ウィンドウです。  
  
#### <a name="to-set-security-properties-of-the-folder-in-iis-51-or-60"></a>フォルダーのセキュリティ プロパティを IIS 5.1 または 6.0 で設定するには  
  
1.  %SystemDrive%\inetpub\wwwroot\servicemodelsamples に移動します。  
  
2.  右クリックし、 **servicemodelsamples**フォルダーをクリックして**共有とセキュリティ。**  
  
3.  **[セキュリティ]** タブをクリックします。  
  
4.  IIS 6.0 を使用している場合、**グループまたはユーザー名**ボックスで、チェックするかどうか**インターネット ゲスト アカウント**が表示されています。  
  
     表示されていない場合:  
  
    1.  をクリックして**開始**] をクリックし、**コントロール パネルの [** です。  
  
    2.  表示されない場合、**ユーザー アカウント** アイコンをクリックして**カテゴリのビューに切り替えます**です。  
  
    3.  クリックして、**ユーザー アカウント**アイコン。  
  
    4.  「またはコントロール パネルを選んで」クリックして**ユーザー アカウント**です。  
  
    5.  **ユーザー アカウント**ダイアログ ボックスで、をクリックして、**詳細** タブ。  
  
    6.  **[詳細設定]** をクリックします。  
  
    7.  **ローカル ユーザーとグループ**ダイアログ ボックスで、クリックして展開し、**ユーザー**フォルダーです。  
  
    8.  右側のウィンドウでダブルクリック**インターネット ゲスト アカウント**です。  
  
    9. **プロパティ**名前は、インターネット ゲスト アカウントとして使用 ダイアログ ボックスで、コピーします。 既定では、その名前は "USR_" で始まり、その次にコンピューターの名前が続きます。  
  
    10. **[プロパティ]** ダイアログ ボックスを閉じます。  
  
    11. 閉じる、**ローカル ユーザーとグループ** ダイアログ ボックス。  
  
    12. 閉じる、**ユーザー アカウント** ダイアログ ボックス。  
  
    13. もう一方を閉じる**ユーザー アカウント** ダイアログ ボックス。  
  
    14. **Servicemodelsamples プロパティ** ダイアログ ボックスで、**セキュリティ** タブで、をクリックして**追加**です。  
  
    15. 円記号の後にコンピューターの名前を入力し、たとえば、myMachineName でインターネット ユーザー アカウントの名前を貼り付けます\\InternetGuestAccountName %  
  
    16. をクリックして**名前の確認**追加を確認します。 名前が有効な場合は、すべての文字が下線付きの大文字になります。  
  
5.  IIS 6.0 でもチェックのネットワーク サービスが表示されていること、**グループまたはユーザー名**ボックス。  
  
     NETWORK SERVICE が表示されていない場合:  
  
    1.  **[追加]** をクリックします。  
  
    2.  **ユーザーまたはグループ**に円記号が、コンピューターの名の後にダイアログ ボックスで入力します。  
  
    3.  型**サービス**円記号 (空白なし) 後にします。  
  
    4.  をクリックして**名前の確認**です。  
  
    5.  複数の名前が見つかった場合は、選択**NETWORK SERVICE**  をクリック**OK**です。  
  
    6.  をクリックして**OK**を閉じる、 **[ユーザーまたはグループ**] ダイアログ ボックス。  
  
6.  Windows XP SP2 で IIS 5.1 を使用している場合は、インターネット ゲスト アカウントと"aspnet"の両方が表示されていることを確認、**グループまたはユーザー名**ボックス。  
  
     ASPNET ユーザーは、組み込みのメンバーである可能性があります**ユーザー**セキュリティ グループです。 場合は、場合、**ユーザー**  ダイアログ ボックスでグループが一覧表示されて、別のアイテムとして許可されているユーザーの一覧に追加する必要はありません。  
  
     ASPNET の一部であるかどうかを確認する、**ユーザー**セキュリティ グループ。  
  
    1.  **開始**] メニューのをクリックして**コントロール パネルの [** です。  
  
    2.  クリックして、**ユーザー アカウント**アイコン。  
  
    3.  **グループ**列、ことを確認の値は、 **ASPNET** "Users"は、  
  
## <a name="see-also"></a>関連項目  
 [インターネット インフォメーション サービスのホスティング手順](../../../../docs/framework/wcf/samples/internet-information-service-hosting-instructions.md)
