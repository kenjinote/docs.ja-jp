---
title: '方法: プロジェクト データ ソースを使用してデータをバインドする (WCF Data Services)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data binding, WCF Data Services
- WCF Data Services, data binding
ms.assetid: 2477af0a-676f-44f7-b73d-e66208785509
ms.openlocfilehash: 0807b8de6bad5e70fbf522cb1cc20872c59fe1b4
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-bind-data-using-a-project-data-source-wcf-data-services"></a>方法: プロジェクト データ ソースを使用してデータをバインドする (WCF Data Services)
生成されたデータ オブジェクトに基づいて [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] クライアント アプリケーション内にデータ ソースを作成できます。 使用してデータ サービスへの参照を追加すると、**サービス参照の追加**ダイアログ ボックスで、生成されたクライアント データ クラスと一緒にプロジェクト データ ソースが作成されます。 データ サービスが公開する各エンティティ セットに対して 1 つのデータ ソースが作成されます。 これらのデータ ソース アイテムをドラッグして、サービスからデータを表示するフォームを作成することができます、**データソース**ウィンドウからデザイナーにします。 これらの項目は、データ ソースにバインドされているコントロールになります。 インスタンスに、実行中にこのデータ ソースがバインドされている、<xref:System.Data.Services.Client.DataServiceCollection%601>クラスは、データ サービスに、クエリによって返されるオブジェクトが挿入されます。 詳細については、次を参照してください。[コントロールへのデータ バインディング](../../../../docs/framework/data/wcf/binding-data-to-controls-wcf-data-services.md)です。  
  
 このトピックの例では、Northwind サンプル データ サービスおよび自動生成されたクライアント データ サービス クラスを使用します。 完了したときにこのサービスおよびクライアント データ クラスが作成された、 [WCF Data Services クイック スタート](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)です。  
  
### <a name="to-use-a-project-data-source-in-a-wpf-window"></a>WPF ウィンドウでプロジェクト データ ソースを使用するには  
  
1.  WPF プロジェクトで Northwind データ サービスへの参照を追加します。 詳細については、次を参照してください。[する方法: データ サービス参照の追加](../../../../docs/framework/data/wcf/how-to-add-a-data-service-reference-wcf-data-services.md)です。  
  
2.  **データソース**ウィンドウで、展開、`Customers`内のノード、 **NorthwindEntities**プロジェクト データ ソース。  
  
3.  をクリックして、 **CustomerID**項目で、 **ComboBox**ドラッグし、一覧から、 **CustomerID**項目を**顧客**ノードをデザイナー。  
  
     ウィンドウの XAML ファイルに次のオブジェクト要素が作成されます。  
  
    -   <xref:System.Windows.Data.CollectionViewSource> という名前の `customersViewSource` 要素。 最上位レベルの <xref:System.Windows.FrameworkElement.DataContext%2A> オブジェクト要素の <xref:System.Windows.Controls.Grid> プロパティが、この新しい <xref:System.Windows.Data.CollectionViewSource> に設定されます。  
  
    -   <xref:System.Windows.Controls.ComboBox> という名前のデータ バインド `CustomerID`。  
  
    -   <xref:System.Windows.Controls.Label>。  
  
4.  ドラッグ、 **Orders**デザイナーへのナビゲーション プロパティ。  
  
     ウィンドウの XAML ファイルに次の追加オブジェクト要素が作成されます。  
  
    -   <xref:System.Windows.Data.CollectionViewSource> という名前の 2 番目の `customersOrdersViewSource` 要素。このソースは `customerViewSource` です。  
  
    -   <xref:System.Windows.Controls.DataGrid> という名前のデータ バインド `ordersDataGrid` コントロール。  
  
5.  (省略可能)追加の項目をドラッグして、**顧客**をデザイナーにノードです。  
  
6.  フォームのコード ページを開き、次に示す `using` ステートメント (Visual Basic の場合は `Imports`) を追加します。  
  
     [!code-csharp[Astoria Northwind Client#CustomersOrdersUsingWpf](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerorderswpf2.xaml.cs#customersordersusingwpf)]  
  
7.  フォームを定義する部分クラスで、<xref:System.Data.Objects.ObjectContext> インスタンスを作成し、`customerID` の定数を定義する次のコードを追加します。  
  
     [!code-csharp[Astoria Northwind Client#CustomersOrdersDefinitionWpf](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerorderswpf2.xaml.cs#customersordersdefinitionwpf)]
     [!code-vb[Astoria Northwind Client#CustomersOrdersDefinitionWpf](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorderswpf2.xaml.vb#customersordersdefinitionwpf)]  
  
8.  デザイナーでウィンドウを選択します。  
  
    > [!NOTE]
    >  ウィンドウ内にある内容を選択するのではなく、ウィンドウ自身を選択します。 ウィンドウが選択されている場合、**名前**の上部にあるテキスト ボックス、**プロパティ**ウィンドウは、ウィンドウの名前を含める必要があります。  
  
9. **プロパティ**ウィンドウで、**イベント**ボタンをクリックします。  
  
10. 検索、 **Loaded**イベント、およびこのイベントの横にあるドロップダウン リストのリストをダブルクリックします。  
  
     Visual Studio でウィンドウの分離コード ファイルが開き、<xref:System.Windows.FrameworkElement.Loaded> イベント ハンドラーが生成されます。  
  
11. 新しく作成された <xref:System.Windows.FrameworkElement.Loaded> イベント ハンドラーで、次のコードをコピーして貼り付けます。  
  
     [!code-csharp[Astoria Northwind Client#CustomersOrdersDataBindingWpf](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerorderswpf2.xaml.cs#customersordersdatabindingwpf)]
     [!code-vb[Astoria Northwind Client#CustomersOrdersDataBindingWpf](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorderswpf2.xaml.vb#customersordersdatabindingwpf)]  
  
12. このコードは、関連する <xref:System.Data.Services.Client.DataServiceCollection%601> オブジェクトと一緒に `Customers` の <xref:System.Collections.Generic.IEnumerable%601> を Northwind データ サービスから返す LINQ クエリの実行に基づいて `Customers` 型の `Orders` のインスタンスを作成し、`customersViewSource` にバインドします。  
  
### <a name="to-use-a-project-data-source-in-a-windows-form"></a>Windows フォームでプロジェクト データ ソースを使用するには  
  
1.  **データソース**ウィンドウで、展開、**顧客**内のノード、 **NorthwindEntities**プロジェクト データ ソース。  
  
2.  をクリックして、 **CustomerID**項目で、 **ComboBox**ドラッグし、一覧から、 **CustomerID**項目を**顧客**ノードをデザイナー。  
  
     次のコントロールがフォーム上に作成されます。  
  
    -   <xref:System.Windows.Forms.BindingSource> という名前の `customersBindingSource` のインスタンス。  
  
    -   <xref:System.Windows.Forms.BindingNavigator> という名前の `customersBindingNavigator` のインスタンス。 このコントロールは必要ないので削除できます。  
  
    -   <xref:System.Windows.Forms.ComboBox> という名前のデータ バインド `CustomerID`。  
  
    -   <xref:System.Windows.Forms.Label>。  
  
3.  ドラッグ、 **Orders**フォームへのナビゲーション プロパティ。  
  
4.  これにより、`ordersBindingSource` プロパティが <xref:System.Windows.Forms.BindingSource.DataSource%2A> に設定され、`customersBindingSource` プロパティが <xref:System.Windows.Forms.BindingSource.DataMember%2A> に設定された `Customers` コントロールが作成されます。 また、`ordersDataGridView` データ バインド コントロールも、適切なタイトルのラベル コントロールと共にフォーム上に作成されます。  
  
5.  (省略可能)追加の項目をドラッグして、**顧客**をデザイナーにノードです。  
  
6.  フォームのコード ページを開き、次に示す `using` ステートメント (Visual Basic の場合は `Imports`) を追加します。  
  
     [!code-csharp[Astoria Northwind Client#CustomersOrdersUsing](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerorders.cs#customersordersusing)]
     [!code-vb[Astoria Northwind Client#CustomersOrdersUsing](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorders.vb#customersordersusing)]  
  
7.  フォームを定義する部分クラスで、<xref:System.Data.Objects.ObjectContext> インスタンスを作成し、`customerID` の定数を定義する次のコードを追加します。  
  
     [!code-csharp[Astoria Northwind Client#CustomersOrdersDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerorders.cs#customersordersdefinition)]
     [!code-vb[Astoria Northwind Client#CustomersOrdersDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorders.vb#customersordersdefinition)]  
  
8.  フォーム デザイナーで、フォームをダブルクリックします。  
  
     フォームのコード ページが開き、フォームの `Load` イベントを処理するメソッドが作成されます。  
  
9. `Load` イベント ハンドラーで、次のコードをコピーして貼り付けます。  
  
     [!code-csharp[Astoria Northwind Client#CustomersOrdersDataBinding](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerorders.cs#customersordersdatabinding)]
     [!code-vb[Astoria Northwind Client#CustomersOrdersDataBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorders.vb#customersordersdatabinding)]  
  
10. このコードは、Northwind データ サービスから <xref:System.Data.Services.Client.DataServiceCollection%601> の `Customers` を返す <xref:System.Data.Services.Client.DataServiceQuery%601> の実行に基づいて <xref:System.Collections.Generic.IEnumerable%601> 型の `Customers` のインスタンスを作成し、`customersBindingSource` にバインドします。  
  
## <a name="see-also"></a>関連項目  
 [WCF Data Services クライアント ライブラリ](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)  
 [方法: Windows Presentation Foundation 要素にデータをバインドする](../../../../docs/framework/data/wcf/bind-data-to-wpf-elements-wcf-data-services.md)
