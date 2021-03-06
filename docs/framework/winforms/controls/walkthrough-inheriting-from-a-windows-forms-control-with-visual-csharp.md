---
title: 'チュートリアル : Visual C# による Windows フォーム コントロールからの継承'
ms.date: 03/30/2017
helpviewer_keywords:
- inheritance [Windows Forms], custom controls
- inheritance [Windows Forms], control
- Windows Forms controls, inheritance
- inheritance [Windows Forms], walkthroughs
- custom controls [Windows Forms], inheritance
ms.assetid: 09476da0-8d4c-4a4c-b969-649519dfb438
ms.openlocfilehash: 1e9231065369640fa49e04a491b92ebfb1e91912
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="walkthrough-inheriting-from-a-windows-forms-control-with-visual-c"></a>チュートリアル : Visual C# による Windows フォーム コントロールからの継承 #
[!INCLUDE[csprcslong](../../../../includes/csprcslong-md.md)] では、*継承*によって強力なカスタム コントロールを作成できます。 継承を使用すると、標準の Windows フォーム コントロールの固有の機能をすべて保持しながら、カスタム機能も組み込んだコントロールを作成できます。 このチュートリアルでは、`ValueButton` という単純な継承されたコントロールを作成します。 このボタンは、標準の Windows フォームの機能を継承<xref:System.Windows.Forms.Button>制御、およびと呼ばれるカスタム プロパティを公開`ButtonValue`です。  
  
> [!NOTE]
>  実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](http://msdn.microsoft.com/library/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
## <a name="creating-the-project"></a>プロジェクトの作成  
 新しいプロジェクトを作成するときは、ルート名前空間、アセンブリ名、プロジェクト名を設定し、既定のコンポーネントが適切な名前空間に含まれるようにするために、プロジェクトの名前を指定します。  
  
#### <a name="to-create-the-valuebuttonlib-control-library-and-the-valuebutton-control"></a>ValueButtonLib コントロール ライブラリと ValueButton コントロールを作成するには  
  
1.  **[ファイル]** メニューの **[新規作成]** をポイントし、**[プロジェクト]** をクリックして **[新しいプロジェクト]** ダイアログ ボックスを開きます。  
  
2.  選択、 **Windows フォーム コントロール ライブラリ**Visual c# プロジェクト、および種類の一覧からプロジェクト テンプレート`ValueButtonLib`で、**名前**ボックス。  
  
     プロジェクト名 `ValueButtonLib` は、既定でルート名前空間にも割り当てられます。 ルート名前空間は、アセンブリ内のコンポーネント名の修飾に使用されます。 たとえば、`ValueButton` という名前のコンポーネントが 2 つのアセンブリに含まれている場合、`ValueButtonLib.ValueButton` を使用して目的の `ValueButton` コンポーネントを指定できます。 詳細については、「[名前空間](../../../csharp/programming-guide/namespaces/index.md)」を参照してください。  
  
3.  **ソリューション エクスプローラー**で、**[UserControl1.cs]** を右クリックし、ショートカット メニューの **[名前の変更]** をクリックします。 ファイル名を `ValueButton.cs` に変更します。 コード要素 "`UserControl1`" へのすべての参照の名前を変更するかどうかをたずねられたら、**[はい]** をクリックします。  
  
4.  **ソリューション エクスプローラー**で、**[ValueButton.cs]** を右クリックし、**[コードの表示]** をクリックします。  
  
5.  検索、`class`明細行`public partial class ValueButton`、このコントロールから継承する型を変更および<xref:System.Windows.Forms.UserControl>に<xref:System.Windows.Forms.Button>です。 これにより、継承されたコントロールのすべての機能を継承する、<xref:System.Windows.Forms.Button>コントロール。  
  
6.  **ソリューション エクスプローラー**で、**[ValueButton.cs]** ノードを開いて、デザイナーによって生成されたコード ファイル (**ValueButton.Designer.cs**) を表示します。 このファイルを**コード エディター**で開きます。  
  
7.  検索、`InitializeComponent`メソッドおよび削除を代入する行、<xref:System.Windows.Forms.ContainerControl.AutoScaleMode%2A>プロパティです。 このプロパティに存在しません、<xref:System.Windows.Forms.Button>コントロール。  
  
8.  **[ファイル]** メニューの **[すべて保存]** をクリックして、プロジェクトを保存します。  
  
    > [!NOTE]
    >  ビジュアル デザイナーは使用できなくなっています。 <xref:System.Windows.Forms.Button>コントロールは独自の描画、デザイナーでその外観を変更することができません。 ビジュアル表現は同じでなければから継承するクラスと (つまり、 <xref:System.Windows.Forms.Button>) コードで変更しない限り、します。 UI 要素のないコンポーネントをデザイン サーフェイスに追加することは可能です。  
  
## <a name="adding-a-property-to-your-inherited-control"></a>継承されたコントロールへのプロパティの追加  
 継承された Windows フォーム コントロールの考えられる用途の 1 つとして、外観は標準の Windows フォーム コントロールと同じでありながら、カスタム プロパティを公開するコントロールの作成があります。 このセクションでは、`ButtonValue` というプロパティをコントロールに追加します。  
  
#### <a name="to-add-the-value-property"></a>Value プロパティを追加するには  
  
1.  **ソリューション エクスプローラー**で、**[ValueButton.cs]** を右クリックし、ショートカット メニューの **[コードの表示]** をクリックします。  
  
2.  `class` ステートメントを見つけます。 `{` の直後に次のコードを入力します。  
  
    ```csharp  
    // Creates the private variable that will store the value of your   
    // property.  
    private int varValue;  
    // Declares the property.  
    public int ButtonValue  
    {  
       // Sets the method for retrieving the value of your property.  
       get  
       {  
          return varValue;  
       }  
       // Sets the method for setting the value of your property.  
       set  
       {  
          varValue = value;  
       }  
    }  
    ```  
  
     このコードでは、`ButtonValue` プロパティを格納し、取得するメソッドを設定しています。 `get` ステートメントは、返された値を `varValue` プライベート変数に格納されている値に設定します。`set` ステートメントは、`value` キーワードを使用してプライベート変数の値を設定します。  
  
3.  **[ファイル]** メニューの **[すべて保存]** をクリックして、プロジェクトを保存します。  
  
## <a name="testing-your-control"></a>コントロールのテスト  
 コントロールはスタンドアロン プロジェクトではないため、コンテナー内でホストする必要があります。 コントロールをテストするには、コントロールを実行するテスト プロジェクトを指定する必要があります。 また、コントロールをビルド (コンパイル) して、テスト プロジェクトからアクセスできるようにする必要があります。 このセクションでは、コントロールをビルドし、Windows フォームでテストします。  
  
#### <a name="to-build-your-control"></a>コントロールをビルドするには  
  
1.  **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。  
  
     コンパイル エラーも警告も発生せずに、ビルドが正常に完了します。  
  
#### <a name="to-create-a-test-project"></a>テスト プロジェクトを作成するには  
  
1.  **[ファイル]** メニューの **[追加]** をポイントし、**[新しいプロジェクト]** をクリックして **[新しいプロジェクトの追加]** ダイアログ ボックスを開きます。  
  
2.  **[Visual C#]** ノードの下の **[Windows]** ノードを選択し、**[Windows フォーム アプリケーション]** をクリックします。  
  
3.  **[名前]** ボックスに「`Test`」と入力します。  
  
4.  **ソリューション エクスプローラー**で、テスト プロジェクトの **[参照設定]** ノードを右クリックし、ショートカット メニューの **[参照の追加]** をクリックして **[参照の追加]** ダイアログ ボックスを表示します。  
  
5.  **[プロジェクト]** というラベルのタブをクリックします。 **[プロジェクト名]** に `ValueButtonLib` プロジェクトが表示されます。 プロジェクトをダブルクリックして、テスト プロジェクトへの参照を追加します。  
  
6.  **ソリューション エクスプローラー**で、**[Test]** を右クリックし、**[ビルド]** をクリックします。  
  
#### <a name="to-add-your-control-to-the-form"></a>コントロールをフォームに追加するには  
  
1.  **ソリューション エクスプローラー**で、**[Form1.cs]** を右クリックし、ショートカット メニューの **[デザイナーの表示]** をクリックします。  
  
2.  **ツールボックス**の **[ValueButtonLib コンポーネント]** をクリックします。 **[ValueButton]** をダブルクリックします。  
  
     **ValueButton** がフォームに表示されます。  
  
3.  **[ValueButton]** を右クリックし、ショートカット メニューの **[プロパティ]** をクリックします。  
  
4.  **[プロパティ]** ウィンドウで、このコントロールのプロパティを調べます。 プロパティは、追加のプロパティである `ButtonValue` がある点を除き、標準ボタンで公開されるプロパティと同じです。  
  
5.  `ButtonValue` プロパティを `5` に設定します。  
  
6.  **すべての Windows フォーム**のタブ、**ツールボックス**をダブルクリックして**ラベル**を追加する、<xref:System.Windows.Forms.Label>をフォームにコントロールです。  
  
7.  ラベルをフォームの中央に配置し直します。  
  
8.  `valueButton1` をダブルクリックします。  
  
     **コード エディター**が開き、`valueButton1_Click` イベントが表示されます。  
  
9. 次のコード行を挿入します。  
  
    ```csharp  
    label1.Text = valueButton1.ButtonValue.ToString();  
    ```  
  
10. **ソリューション エクスプローラー**で、**[Test]** を右クリックし、ショートカット メニューの **[スタートアップ プロジェクトに設定]** をクリックします。  
  
11. **[デバッグ]** メニューの **[デバッグの開始]** をクリックします。  
  
     `Form1` が表示されます。  
  
12. [`valueButton1`] をクリックします。  
  
     `label1` に数字の "5" が表示されます。これは、継承されたコントロールの `ButtonValue` プロパティが、`valueButton1_Click` メソッドによって `label1` に渡されたことを示しています。 このようにして、`ValueButton` コントロールは標準の Windows フォーム ボタンの機能をすべて継承しながら、追加のカスタム プロパティを公開します。  
  
## <a name="see-also"></a>関連項目  
 [コンポーネントによるプログラミング](http://msdn.microsoft.com/library/d4d4fcb4-e0b8-46b3-b679-7ee0026eb9e3)  
 [コンポーネント作成のチュートリアル](http://msdn.microsoft.com/library/c414cca9-2489-4208-8b38-954586d91c13)  
 [方法: [ツールボックス アイテムの選択] ダイアログ ボックスにコントロールを表示する](../../../../docs/framework/winforms/controls/how-to-display-a-control-in-the-choose-toolbox-items-dialog-box.md)  
 [チュートリアル: Visual C# による複合コントロールの作成](../../../../docs/framework/winforms/controls/walkthrough-authoring-a-composite-control-with-visual-csharp.md)
