---
title: チュートリアルと技術は、開始の概要を取得します。
description: Azure のクラウドと Windows コンテナーの既存の .NET アプリケーションを最新化 |チュートリアルと技術は、開始の概要を取得します。
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 04/28/2018
ms.openlocfilehash: 27de9d1c5475855a22f2d8a3518982605277f6d9
ms.sourcegitcommit: 88f251b08bf0718ce119f3d7302f514b74895038
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2018
---
# <a name="walkthroughs-and-technical-get-started-overview"></a>チュートリアルと技術は、開始の概要を取得します。

この電子書籍のサイズを制限するには、追加のテクニカル ドキュメントと完全のチュートリアルで行われた使用可能な GitHub リポジトリです。 オンラインの一連のこの章で説明されているチュートリアルでは、Windows コンテナー、および Azure へのデプロイに基づいて複数の環境の詳細な手順のセットアップについて説明します。

次のセクションでは、各チュートリアルでは、その目標と高レベルのビジョンを通知し、関連するタスクを次の図は、について説明します。 チュートリアル自体を取得することができますに、 *eShopModernizing*でアプリの GitHub リポジトリの wiki [ https://github.com/dotnet-architecture/eShopModernizing/wiki](https://github.com/dotnet-architecture/eShopModernizing/wiki)です。

## <a name="technical-walkthrough-list"></a>技術的なチュートリアルの一覧

はじめに-次のチュートリアルでは、リフトしコンテナーを使用して、シフトし、し、Azure で複数の展開の選択肢を使用して、移動するサンプル アプリの一貫性のあるで包括的なに関するテクニカル ガイダンスを提供します。

次のチュートリアルの各アプリケーションを使用して、新しいサンプル eShopLegacy と eShopModernizing で GitHub で利用可能である[ https://github.com/dotnet-architecture/eShopModernizing](https://github.com/dotnet-architecture/eShopModernizing)です。

- **EShop レガシ アプリ (基準の最新化) のツアー**

- **Windows コンテナーで (WebForms & MVC) 既存の ASP.NET web アプリを containerize します。**

- **Windows コンテナーで既存の WCF サービス (N 層アプリケーション) を containerize します。**

- **Azure Vm を Windows コンテナー ベースのアプリを展開します。**

- **Azure のコンテナー サービスで Kubernetes に Windows コンテナー ベースのアプリを展開します。**

- **Azure Service Fabric に Windows コンテナー ベースのアプリを展開します。**


## <a name="walkthrough-1-tour-of-eshop-legacy-apps"></a>EShop レガシ アプリケーションのチュートリアル 1: ツアー

### <a name="technical-walkthrough-availability"></a>技術的なチュートリアルの可用性

技術的なチュートリアルは、eShopModernizing GitHub リポジトリの wiki で入手できます。

[eShopModernizing wiki チュートリアル](https://github.com/dotnet-architecture/eShopModernizing/wiki)


### <a name="overview"></a>概要

このチュートリアルでは、次の 3 つのサンプルのレガシ アプリケーションの最初の実装を調べることができます。 最初の 2 つのサンプル web アプリケーションは、単体のアーキテクチャを持ち、従来の ASP.NET を使用して作成されました。 1 つのアプリケーションが ASP.NET に基づく 4.x MVC です。2 番目のアプリケーションは、ASP.NET 4.x Web フォームに基づいています。 3 番目のアプリはクライアント WinForms アプリケーションとサーバー側で構成される 3 層アプリ[Windows Communication Foundation (WCF)](../../framework/wcf/whats-wcf.md)サービス。

これらすべてのアプリケーションは、 [GitHub リポジトリの eShopModernizing](https://github.com/dotnet-architecture/eShopModernizing)です。

### <a name="goals"></a>目的

このチュートリアルの主な目的は、これらのアプリとそのコードおよび構成について理解するだけです。 テスト目的で SQL データベースを使用せず、モック データを使用して、生成されるように、アプリを構成することができます。 このオプションの構成は、分離された方法で依存関係の挿入に基づいています。

### <a name="scenario-1-aspnet-web-apps"></a>シナリオ 1: ASP.NET Web アプリ

次の図は、元のレガシ ASP.NET web アプリケーションの簡単なシナリオを示します。

> ![元のレガシ ASP.NET web アプリケーションのシナリオを単純なアーキテクチャ](./media/image5-1.png)
>

ビジネス ドメインの観点から両方のアプリは管理機能に同じカタログを提供します。 EShop エンタープライズ チームのメンバーは表示および製品カタログを編集するアプリを使用します。 

次の図は、最初のアプリのスクリーン ショットを示します。

![ASP.NET MVC と ASP.NET Web フォーム アプリケーション (既存の/レガシ テクノロジ)](./media/image5-2.png)

依存関係 ASP.NET 4.x か (いずれかの MVC または Web フォームの) 以前のバージョンは、コードが ASP.NET Core MVC を使用して、完全に記述し直すされない限り、これらのアプリケーションを .NET Core で実行されないことです。 

### <a name="scenario-2-wcf-service-and-winforms-client-app-3-tier-app"></a>シナリオ 2: WCF サービスと WinForms クライアント アプリ (アプリが 3 層)

次の図は、元の 3 層のレガシ アプリケーションの簡単なシナリオを示します。

> ![WCF サービスと元レガシ 3 層アプリケーションおよび WinForms クライアント アプリのシナリオを単純なアーキテクチャ](./media/image5-1.5.png)
>

### <a name="benefits"></a>利点

このチュートリアルのメリットは、単純な: コードと最初のアプリに精通して表示します。

### <a name="next-steps"></a>次の手順

GitHub wiki 上には、このコンテンツをさらに詳しい情報を表示します。

  - [ASP.NET MVC のベースラインをツアーと Web フォーム「レガシ」アプリ](https://github.com/dotnet-architecture/eShopModernizing/wiki/01.-Tour-on-the-ASP.NET-MVC-and-WebForms-apps-implementation-code)
  - [WCF サービスの基準と WinForms (3 層)「レガシ」アプリのツアー](https://github.com/dotnet-architecture/eShopModernizing/wiki/21.-Tour-on-the-WCF-service-and-WinForms-apps)


## <a name="walkthrough-2-containerize-your-existing-net-applications-with-windows-containers"></a>チュートリアル 2: Windows コンテナーで、既存の .NET アプリケーションを Containerize します。

### <a name="overview"></a>概要

Windows コンテナーの MVC、Web フォーム、または WCF、運用、開発、およびテスト環境に基づくように、既存の .NET アプリケーションの展開を向上させるために使用します。

### <a name="goals"></a>目的

このチュートリアルの目的は、既存の .NET Framework アプリケーションを containerizing いくつかのオプションを表示します。 次の操作を行うことができます。

- 使用してアプリを containerize [Docker 用の Visual Studio 2017 Tools](/aspnet/core/host-and-deploy/docker/visual-studio-tools-for-docker) (Visual Studio 2017 年 1 またはそれ以降のバージョン)。

- 手動で追加することによってアプリを containerize する[Dockerfile](https://docs.docker.com/engine/reference/builder/)を使用して、 [Docker CLI](https://docs.docker.com/engine/reference/commandline/cli/)です。

- 使用してアプリを containerize、 [Img2Docker](https://github.com/docker/communitytools-image2docker-win)ツール (Docker からオープン ソース ツール)。

このチュートリアルは、Docker 方法は、Visual Studio 2017 ツールに焦点を当てていますが、他の 2 つのアプローチが Dockerfile を使用してに関して類似しています。

### <a name="scenario-1-containerized-aspnet-web-apps"></a>シナリオ 1: コンテナーの ASP.NET web アプリ

次の図は、コンテナー化 eShop レガシ web アプリのアプリケーションのシナリオを示します。

> ![開発環境での ASP.NET アプリケーションのコンテナーの簡略化されたアーキテクチャ図](./media/image5-3.png)
>


### <a name="scenario-2-containerized-wcf-service"></a>シナリオ 2: コンテナーの WCF サービス

次の図は、コンテナー化の WCF サービスと 3 層アプリケーションのシナリオを示します。 

> ![開発環境でのコンテナー化の WCF サービスのアーキテクチャ図を簡素化されます。](./media/image5-3.5.png)
>

### <a name="benefits"></a>利点

これには、コンテナーでモノリシックなアプリケーションを実行する利点があります。 最初に、アプリケーションのイメージを作成します。 その時点から、それぞれの配置を同じ環境で実行します。 すべてのコンテナーは、同じ OS バージョンを使用がインストールされている依存関係の同じバージョン、同じ .NET framework のバージョンを使用して、および同じ処理を使用してビルドされたをします。 基本的には、Docker イメージを使用して、アプリケーションの依存関係を制御します。 依存関係は、コンテナーを展開するときに、アプリケーションに移動します。

その他の利点は、開発者が Windows コンテナーによって提供されている一貫した環境でアプリケーションを実行できることです。 特定のバージョンでのみ表示される問題は、ステージングまたは運用環境での表示ではなく、すぐに発見できます。 開発チームのメンバーで使用される開発環境での違いは重要アプリケーション コンテナーで実行時に小さいです。

コンテナー化アプリケーションは、テクスチャのスケール アウト曲線を含めます。 コンテナー化アプリケーションでは、VM または物理マシンのマシンあたりの通常のアプリケーション展開と比較してで有効にすると、複数のアプリケーションとサービス インスタンス (コンテナーに基づく) があります。 これにより、高密度」および「減らすために必要なリソース、orchestrators Kubernetes など Service Fabric を使用する場合に特にです。

コンテナリゼーション、理想的な状況では、アプリケーション コードに変更を加える必要ありません (C\#)。 ほとんどのシナリオでは、Docker の展開のメタデータ ファイル (Dockerfile と Docker Compose ファイル) だけができます。

### <a name="next-steps"></a>次の手順

GitHub wiki 上には、このコンテンツをさらに詳しい情報を表示します。

  - [Windows コンテナーと Docker で .NET Framework の web アプリを containerize する方法](https://github.com/dotnet-architecture/eShopModernizing/wiki/02.-How-to-containerize-the-.NET-Framework-web-apps-with-Windows-Containers-and-Docker)
  - [WCF サービスに Docker のサポートを追加します。](https://github.com/dotnet-architecture/eShopModernizing/wiki/22.-Adding-Docker-Support)



## <a name="walkthrough-3-deploy-your-windows-containers-based-app-to-azure-vms"></a>チュートリアル 3: Azure Vm を Windows コンテナー ベースのアプリを展開します。

### <a name="technical-walkthrough-availability"></a>技術的なチュートリアルの可用性

技術的なチュートリアルは、eShopModernizing GitHub リポジトリの wiki で入手できます。 [https://github.com/dotnet-architecture/eShopModernizing/wiki/03.-How-to-deploy-your-Windows-Containers-based-app-into-Azure-VMs-(Including-CI-CD)](https://github.com/dotnet-architecture/eShopModernizing/wiki/03.-How-to-deploy-your-Windows-Containers-based-app-into-Azure-VMs-(Including-CI-CD))

### <a name="overview"></a>概要

Azure の Windows Server 2016 仮想マシン (VM) 上の Docker ホストに展開するには、開発/テスト/ステージング環境をすばやくセットアップすることができます。 アプリを検証するには、テスト担当者またはビジネス ユーザー用の共通の場所も示します。 Vm は、Service (IaaS) の実稼働環境として有効なインフラストラクチャをすることもできます。

### <a name="goals"></a>目的

このチュートリアルの目的は、Windows Server 2016、またはそれ以降のバージョンに基づいて Azure Vm を Windows コンテナーを展開する場合がある複数の代替を示すためです。

### <a name="scenarios"></a>シナリオ

このチュートリアルでは、いくつかのシナリオについて説明します。

#### <a name="scenario-a-deploy-to-an-azure-vm-from-a-dev-pc-through-docker-engine-connection"></a>シナリオ a: 展開は、Docker エンジン接続から開発用コンピューターから Azure VM に

![Docker エンジン接続を介して開発用コンピューターから Azure の仮想マシンを展開します。](./media/image5-4.png)

> **図 5-4** Docker エンジン接続を介して開発用コンピューターから Azure の仮想マシンを展開します。

#### <a name="scenario-b-deploy-to-an-azure-vm-through-a-docker-registry"></a>シナリオ b: Docker のレジストリを使用する Azure VM を展開します。

![Docker レジストリを使用して Azure の仮想マシンを配置します。](./media/image5-5.png)

> **図 5-5** Docker レジストリを使用して Azure の仮想マシンを配置します。

#### <a name="scenario-c-deploy-to-an-azure-vm-from-cicd-pipelines-in-visual-studio-team-services"></a>シナリオ c: Azure の仮想マシンに Visual Studio Team Services での CI/CD パイプラインから展開します。

![Visual Studio Team Services での CI/CD パイプラインから Azure の仮想マシンを展開します。](./media/image5-6.png)

> **図 5-6** Visual Studio Team Services での CI/CD パイプラインから Azure の仮想マシンを展開します。

### <a name="azure-vms-for-windows-containers"></a>Windows コンテナーの azure Vm

Windows コンテナーの azure Vm は Vm の Windows Server 2016、Windows 10、またはそれ以降のバージョンに基づく、Docker エンジンがどちらも設定します。 ほとんどの場合は、Windows Server 2016 は Azure Vm で使用されます。

Azure は、という名前の VM を現在提供**コンテナーと Windows Server 2016**です。 この VM を使用して、Windows Server Core または Nano Server の Windows で、新しい Windows Server コンテナー機能を試みることができます。 コンテナー OS イメージがインストールされ、その VM は Docker で使用できるようにします。

### <a name="benefits"></a>利点

Windows コンテナーは、Azure にデプロイするときに、内部設置型 Windows Server 2016 の Vm を配置できますが、すぐに使用できる Windows Server コンテナーの Vm で、作業を開始する簡単な方法を取得します。 また、テスト担当者、および Azure の仮想マシン スケール セットによる自動スケーラビリティにアクセスできる一般的なオンラインの場所を取得します。

### <a name="next-steps"></a>次の手順

GitHub wiki 上には、このコンテンツをさらに詳しい情報を表示します。

[https://github.com/dotnet-architecture/eShopModernizing/wiki/03.-How-to-deploy-your-Windows-Containers-based-app-into-Azure-VMs-(Including-CI-CD)](https://github.com/dotnet-architecture/eShopModernizing/wiki/03.-How-to-deploy-your-Windows-Containers-based-app-into-Azure-VMs-(Including-CI-CD))

## <a name="walkthrough-4-deploy-your-windows-containers-based-apps-to-azure-container-instances-aci"></a>チュートリアル 4: Azure のコンテナー インスタンス (ACI) に Windows コンテナー ベースのアプリを展開します。

### <a name="technical-walkthrough-availability"></a>技術的なチュートリアルの可用性

技術的なチュートリアルは、eShopModernizing GitHub リポジトリの wiki で入手できます。

[ACI (Azure のコンテナー インスタンス) に、アプリを展開します。](https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-Deploying-the-Apps-to-ACI-(Azure-Container-Instances))

### <a name="overview"></a>概要

[Azure コンテナー インスタンス (ACI)](https://docs.microsoft.com/en-us/azure/container-instances/)コンテナーの単一のインスタンスを展開するコンテナー開発/テスト/ステージング環境がある最も簡単な方法です。

### <a name="goals"></a>目的

このチュートリアルは、主なシナリオ Azure コンテナー インスタンス (ACI) と ACI に eShopModernizing アプリを展開する方法に Windows コンテナーを展開するときにします。

### <a name="scenarios"></a>シナリオ

1 つまたはすべて (MVC アプリ、web フォーム アプリケーションまたは WCF サービス) のアプリの展開など ACI に eShopModernizing アプリの展開のバリエーションがあります。 次に示す次のシナリオでことができます、コンテナーとして ACI (Azure のコンテナー インスタンス) に ASP.NET MVC アプリケーションと、これらの両方に展開されている SQL Server のコンテナーを参照します。

![開発環境から ACI を展開します。](./media/image5-3.5.6.png)

### <a name="benefits"></a>利点

Azure のコンテナー インスタンスでは、簡単に作成し、仮想マシンをプロビジョニングまたは高レベルのサービスを採用することがなく、Azure では、Docker コンテナーを管理します。 ACI で直接 Azure での Windows コンテナーを展開してへの公開インターネット完全修飾ドメイン名 (FQDN) を数秒で (Docker Hub または Azure コンテナーのように Docker レジストリで準備ができて、Windows コンテナー イメージがある場合にレジストリ)。

### <a name="considerations"></a>注意事項

いずれか完全な .NET Framework による Windows コンテナーを展開する/ASP.NET または SQL Server には、Azure コンテナー インスタンス (ACI) が Docker イメージに存在するために (Windows コンテナーでの Windows Server 2016) のような通常の Docker ホストに展開すると非常に高速ではありませんたびに (プル Docker レジストリから) ダウンロードし、SQL コンテナー イメージ (15.1 GB) と ASP.NET のコンテナーのイメージ (13.9 GB) のサイズは大幅に大きなただし、これは、独自の docker ホスト (永続的にオンラインを維持することよりはるかに低コストAzure で Windows コンテナーの VM で Windows Server 2016) であり、その一方で、運用環境の配置の優れた選択肢 (AKS/ACS) を Azure または Azure Service Fabric で Kubernetes と同様に全体の orchestrator を言うまでもありません。

メイン最後に、としては、Azure コンテナー インスタンスを使用して開発およびテスト シナリオの場合とパイプラインの CI/CD に非常に説得力のあるオプション。

## <a name="next-steps"></a>次の手順

GitHub wiki 上には、このコンテンツをさらに詳しい情報を表示します。 

[https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-Deploying-the-Apps-to-ACI-(Azure-Container-Instances)](https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-Deploying-the-Apps-to-ACI-(Azure-Container-Instances)TBD)


## <a name="walkthrough-5-deploy-your-windows-containers-based-apps-to-kubernetes-in-azure-container-service"></a>チュートリアル 5: Azure のコンテナー サービスで Kubernetes に Windows コンテナー ベースのアプリを展開します。

### <a name="technical-walkthrough-availability"></a>技術的なチュートリアルの可用性

技術的なチュートリアルは、eShopModernizing GitHub リポジトリの wiki で入手できます。

[https://github.com/dotnet-architecture/eShopModernizing/wiki/04.-How-to-deploy-your-Windows-Containers-based-apps-into-Kubernetes-in-Azure-Container-Service-(Including-C-CD)](https://github.com/dotnet-architecture/eShopModernizing/wiki/04.-How-to-deploy-your-Windows-Containers-based-apps-into-Kubernetes-in-Azure-Container-Service-(Including-C-CD))

### <a name="overview"></a>概要

Windows コンテナーに基づいているアプリケーションはすばやく遠ざかる、さらに IaaS Vm からプラットフォームを使用する必要があります。 これを簡単に高いスケーラビリティを実現するために必要なよりスケーラビリティ、自動化され、では、大幅な向上を配置およびバージョン管理を自動化します。 これらの目標を達成するには、orchestrator を使用して、 [Kubernetes](https://kubernetes.io/)で使用できる、 [Azure コンテナー サービス](https://azure.microsoft.com/services/container-service/)です。

### <a name="goals"></a>目的

Kubernetes に Windows コンテナー ベースのアプリケーションを展開する方法については、このチュートリアルの目的は、(とも呼ばれる*K8s*) Azure コンテナー サービスでします。 2 段階のプロセスは、最初から Kubernetes への展開します。

1.  Azure コンテナー サービスに Kubernetes クラスターを展開します。

2.  Kubernetes クラスターに関連するリソースとアプリケーションを展開します。

### <a name="scenarios"></a>シナリオ

#### <a name="scenario-a-deploy-directly-to-a-kubernetes-cluster-from-a-dev-environment"></a>開発環境から Kubernetes クラスターに直接シナリオ a: 配置

![開発環境から Kubernetes クラスターに直接展開します。](./media/image5-7.png)

> **図 5-7** 開発環境から Kubernetes クラスターに直接展開します。

#### <a name="scenario-b-deploy-to-a-kubernetes-cluster-from-cicd-pipelines-in-team-services"></a>Team Services でパイプライン シナリオ b: Kubernetes クラスターに CI/CD から展開します。

![Team Services での CI/CD パイプラインから Kubernetes クラスターを展開します。](./media/image5-8.png)

> **図 5-8** Team Services での CI/CD パイプラインから Kubernetes クラスターを展開します。

### <a name="benefits"></a>利点

Kubernetes でクラスターに展開する多くの利点があります。 最大のメリットは、運用環境で環境をスケール アウトできます (既存のノードでは内部スケーラビリティ) を使用して、クラスター (ノードまたは Vm の数に基づくコンテナーのインスタンスの数に基づいて、アプリケーションを取得します。グローバルなスケーラビリティはクラスターの)。

Azure のコンテナー サービスは、具体的には Azure の一般的なオープン ソース ツールとテクノロジを最適化します。 移植性をコンテナーと、アプリケーションの構成の両方を提供する、開いているソリューションが表示されます。 ホストの数、サイズを選択し、orchestrator ツール-コンテナーのサービスが他のすべてを処理します。

Kubernetes と開発者は他のユーザー間で、次の機能を容易にするコンテナーを中心としたインフラストラクチャの計画を考えた物理および仮想マシンに進むことができます。

- 複数のコンテナーに基づくアプリケーション

- コンテナーのインスタンスと自動スケールを水平方向にレプリケートします。

- 名前付けと (たとえば、内部 DNS) を検出します。

- 負荷を分散

- ローリング アップデート

- シークレットを配布します。

- アプリケーションの正常性チェック

## <a name="next-steps"></a>次の手順

GitHub wiki 上には、このコンテンツをさらに詳しい情報を表示します。 [https://github.com/dotnet-architecture/eShopModernizing/wiki/04.-How-to-deploy-your-Windows-Containers-based-apps-into-Kubernetes-in-Azure-Container-Service-(Including-C-CD)](https://github.com/dotnet-architecture/eShopModernizing/wiki/04.-How-to-deploy-your-Windows-Containers-based-apps-into-Kubernetes-in-Azure-Container-Service-(Including-C-CD))

## <a name="walkthrough-6-deploy-your-windows-containers-based-apps-to-azure-service-fabric"></a>チュートリアル 6: Azure Service Fabric を Windows コンテナー ベースのアプリを展開します。

### <a name="technical-walkthrough-availability"></a>技術的なチュートリアルの可用性

技術的なチュートリアルは、eShopModernizing GitHub リポジトリの wiki で入手できます。

[https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-How-to-deploy-your-Windows-Containers-based-apps-into-Azure-Service-Fabric-(Including-CI-CD)](https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-How-to-deploy-your-Windows-Containers-based-apps-into-Azure-Service-Fabric-(Including-CI-CD))

### <a name="overview"></a>概要

Windows コンテナーをすばやくに基づいてアプリケーションは、プラットフォームでは、遠ざかる、さらに IaaS Vm からを使用する必要があります。 これを簡単に高いスケーラビリティを実現するために必要なよりスケーラビリティ、自動化され、では、大幅な向上を配置およびバージョン管理を自動化します。 Orchestrator は、Azure クラウドで使用できますが、内部設置型の使用にも使用可能で、Azure Service Fabric を使用するか、別のパブリック クラウドであっても、これらの目標を実現できます。

### <a name="goals"></a>目的

このチュートリアルの目的では、azure Service Fabric クラスターを Windows コンテナー ベースのアプリケーションを展開する方法を理解します。 Service Fabric を最初から展開するには、2 段階のプロセスです。

1.  Azure (または、別の環境) は、Service Fabric クラスターを展開します。

2.  Service Fabric クラスターをアプリケーションと関連するリソースを展開します。

### <a name="scenarios"></a>シナリオ

#### <a name="scenario-a-deploy-directly-to-a-service-fabric-cluster-from-a-dev-environment"></a>Service Fabric クラスターに直接開発環境からのシナリオ a: 配置

![開発環境から Service Fabric クラスターを直接展開します。](./media/image5-9.png)

> **図 5-9** 開発環境から Service Fabric クラスターを直接展開します。

### <a name="scenario-b-deploy-to-a-service-fabric-cluster-from-cicd-pipelines-in-team-services"></a>Team Services でパイプライン シナリオ b: Service Fabric クラスターを CI/CD から展開します。

![Visual Studio Team Services での CI/CD パイプラインから Service Fabric クラスターを展開します。](./media/image5-10.png)

> **図 5-10** Visual Studio Team Services での CI/CD パイプラインから Service Fabric クラスターを展開します。

## <a name="benefits"></a>利点

Service Fabric クラスターを展開する利点は、Kubernetes を使用する利点と似ています。 1 つの違いは Service Fabric Kubernetes バージョン 1.9 で Windows コンテナーのベータ版のフェーズでは Kubernetes と比較して、Windows アプリケーションの運用環境より完成度の高い (2017 年 12 月)。 Kubernetes は、for Linux より完成度の高い環境です。

Azure Service Fabric を使用する主な利点は、運用環境で環境をスケール アウトできます (既存のノードでは内部スケーラビリティ) を使用するの数に基づいて、コンテナー インスタンスの数に基づいて、アプリケーションを取得します。ノードまたはクラスター (クラスターのグローバルな拡張性) で Vm です。

Azure Service Fabric は、コンテナーと、アプリケーションの構成の両方の移植性を提供します。 Azure では、クラスター、または独自のデータ センターに内部設置型インストールに Service Fabric ことができます。 同様にも別のクラウドにこの Service Fabric クラスターをインストールすることができます[Amazon AWS](https://blogs.msdn.microsoft.com/azureservicefabric/2017/05/18/tutorial-how-to-create-a-service-fabric-standalone-cluster-with-aws-ec2-instances/)です。

Service Fabric で開発者は他のユーザー間で、次の機能を容易にするコンテナーを中心としたインフラストラクチャの計画を考えた物理および仮想マシンに進むことができます。

- 複数のコンテナーに基づくアプリケーションです。

- コンテナーのインスタンスおよび水平方向の自動スケーリングをレプリケートしています。

- 名前付けと (たとえば、内部 DNS) を検出します。

- 負荷を分散します。

- 更新プログラムの展開です。

- シークレットを配布します。

- アプリケーションの正常性を確認します。

次の機能は、(他の orchestrators と比較して)、Service Fabric で排他が。

- ステートフル サービスの機能、信頼性の高いサービス アプリケーションのモデルを使用します。

- アクター パターン、Reliable Actors アプリケーション モデルを使用します。

- Windows または Linux のコンテナーに加え、ベア骨のプロセスを展開します。

- 高度なローリング更新プログラムとの正常性チェックします。

### <a name="next-steps"></a>次の手順

GitHub wiki 上には、このコンテンツをさらに詳しい情報を表示します。

[https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-How-to-deploy-your-Windows-Containers-based-apps-into-Azure-Service-Fabric-(Including-CI-CD)](https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-How-to-deploy-your-Windows-Containers-based-apps-into-Azure-Service-Fabric-(Including-CI-CD))

>[!div class="step-by-step"]
[前へ](lift-and-shift-existing-apps-devops/migrate-to-hybrid-cloud-scenarios.md)
[次へ](conclusions.md)
