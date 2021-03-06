---
title: 'チュートリアル : ツールボックスへのカスタム コンポーネントの自動設定'
ms.date: 03/30/2017
helpviewer_keywords:
- IToolboxService interface
- Toolbox [Windows Forms], populating
- custom components [Windows Forms], adding to Toolbox
ms.assetid: 2fa1e3e8-6b9f-42b2-97c0-2be57444dba4
ms.openlocfilehash: d446ab84cfe135e56483b8b309b696f7f15044fa
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="walkthrough-automatically-populating-the-toolbox-with-custom-components"></a>チュートリアル : ツールボックスへのカスタム コンポーネントの自動設定
現在開いているソリューション内のプロジェクトで定義された、コンポーネント場合、自動的に表示されます、**ツールボックス**操作は必要とします。 手動で設定することができます、**ツールボックス**を使用して、カスタム コンポーネントで、[選択ツールボックス項目 ダイアログ ボックス (Visual Studio)](http://msdn.microsoft.com/library/bd07835f-18a8-433e-bccc-7141f65263bb)、ですが、**ツールボックス**考慮ソリューションの内の項目は、ビルドの次のすべての特性を持つ出力を。  
  
-   実装して<xref:System.ComponentModel.IComponent>です。  
  
-   いない<xref:System.ComponentModel.ToolboxItemAttribute>'éý'`false`です。  
  
-   いない<xref:System.ComponentModel.DesignTimeVisibleAttribute>'éý'`false`です。  
  
> [!NOTE]
>  **ツールボックス**に従わなかった場合、参照チェーンのため、ソリューションのプロジェクトで構築されていないアイテムは表示されません。  
  
 このチュートリアルでは、カスタム コンポーネントに自動的にでの表示方法、**ツールボックス**コンポーネントをビルドします。 このチュートリアルでは、以下のタスクを行います。  
  
-   Windows フォーム プロジェクトを作成します。  
  
-   カスタム コンポーネントを作成します。  
  
-   カスタム コンポーネントのインスタンスを作成します。  
  
-   アンロードし、カスタム コンポーネントを再読み込みします。  
  
 完了したら、\outputfromtestproviderdebugmode.txt、**ツールボックス**作成したコンポーネントが格納されます。  
  
> [!NOTE]
>  実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](http://msdn.microsoft.com/library/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
## <a name="creating-the-project"></a>プロジェクトの作成  
 まず、プロジェクトを作成し、フォームを設定します。  
  
#### <a name="to-create-the-project"></a>プロジェクトを作成するには  
  
1.  `ToolboxExample` という Windows ベースのアプリケーション プロジェクトを作成します。  
  
     詳細については、「[方法 : Windows アプリケーション プロジェクトを作成する](http://msdn.microsoft.com/library/b2f93fed-c635-4705-8d0e-cf079a264efa)」を参照してください。  
  
2.  新しいコンポーネントをプロジェクトに追加します。 それを呼び出す`DemoComponent`です。  
  
     詳細については、次を参照してください。 [NIB: 方法: 新しいプロジェクト項目の追加](http://msdn.microsoft.com/library/63d3e16b-de6e-4bb5-a0e3-ecec762201ce)です。  
  
3.  プロジェクトをビルドします。  
  
4.  **ツール** メニューをクリックして、**オプション**項目。 をクリックして**全般**下にある、 **Windows フォーム デザイナー**項目のことを確認して、 **AutoToolboxPopulate**オプションに設定されて**True**です。  
  
## <a name="creating-an-instance-of-a-custom-component"></a>カスタム コンポーネントのインスタンスを作成します。  
 次の手順では、フォームでカスタム コンポーネントのインスタンスを作成します。 **ツールボックス**自動的に新しいコンポーネントのアカウントは、これは他のコンポーネントまたはコントロールの作成と同じくらい簡単です。  
  
#### <a name="to-create-an-instance-of-a-custom-component"></a>カスタム コンポーネントのインスタンスを作成するには  
  
1.  プロジェクトのフォームを開いて、**フォーム デザイナー**です。  
  
2.  **ツールボックス**と呼ばれる新しいタブをクリックして**ToolboxExample コンポーネント**です。  
  
     タブをクリックすると表示されます**と**です。  
  
    > [!NOTE]
    >  パフォーマンス上の理由から、コンポーネントの自動設定された領域で、**ツールボックス**カスタムのビットマップを表示しないと、<xref:System.Drawing.ToolboxBitmapAttribute>はサポートされていません。 カスタムのコンポーネントのアイコンを表示する、**ツールボックス**を使用して、**ツールボックス アイテムの選択**ダイアログ ボックスで、コンポーネントの読み込みをします。  
  
3.  コンポーネントをフォームにドラッグします。  
  
     コンポーネントのインスタンスが作成され、追加、**コンポーネント トレイ**です。  
  
## <a name="unloading-and-reloading-a-custom-component"></a>アンロードして、カスタム コンポーネントを再読み込み  
 **ツールボックス**の各コンポーネントのではアカウントには、プロジェクトが読み込まれ、プロジェクトが読み込まれると、プロジェクトのコンポーネントへの参照を削除します。  
  
#### <a name="to-experiment-with-the-effect-on-the-toolbox-of-unloading-and-reloading-components"></a>アンロードとコンポーネントを再読み込みのツールボックスへの影響をテストするには  
  
1.  ソリューションからプロジェクトをアンロードします。  
  
     プロジェクトのアンロードの詳細については、次を参照してください。 [NIB: 方法:: アンロードし、プロジェクトの再読み込み](http://msdn.microsoft.com/library/abc0155b-8fcb-4ffc-95b6-698518a7100b)です。 保存するメッセージが表示されたら、選択**はい**です。  
  
2.  新しい**Windows アプリケーション**プロジェクトがソリューションにします。 フォームを開いて、**デザイナー**です。  
  
     **ToolboxExample コンポーネント**前のプロジェクトからタブは削除します。  
  
3.  再読み込み、`ToolboxExample`プロジェクト。  
  
     **ToolboxExample コンポーネント** タブのようになりましたが再表示されます。  
  
## <a name="next-steps"></a>次の手順  
 このチュートリアルで説明する、**ツールボックス**、プロジェクトのコンポーネントの考慮ですが、**ツールボックス**コントロールもです。 追加と管理プロジェクトをソリューションから削除して、独自のカスタム コントロールをテストします。  
  
## <a name="see-also"></a>関連項目  
 [一般に、Windows フォーム デザイナー、オプション ダイアログ ボックス](http://msdn.microsoft.com/library/8dd170af-72f0-4212-b04b-034ceee92834)  
 [方法: [ツールボックス] タブの操作](http://msdn.microsoft.com/library/21285050-cadd-455a-b1f5-a2289a89c4db)  
 [[ツールボックス アイテムの選択] ダイアログ ボックス (Visual Studio)](http://msdn.microsoft.com/library/bd07835f-18a8-433e-bccc-7141f65263bb)  
 [Windows フォームへのコントロールの追加](../../../../docs/framework/winforms/controls/putting-controls-on-windows-forms.md)
