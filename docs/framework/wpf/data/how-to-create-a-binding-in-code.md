---
title: '方法 : コードでバインディングを作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- binding data [WPF], creating
- data binding [WPF], creating
ms.assetid: 1a606db9-cf5f-42ed-a1c5-9e4722ec77a0
ms.openlocfilehash: 62c5610bf5590594f34a3401b9397bb17d23f5ab
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-create-a-binding-in-code"></a>方法 : コードでバインディングを作成する
この例を作成し、設定する方法を示しています、<xref:System.Windows.Data.Binding>のコードにします。  
  
## <a name="example"></a>例  
 <xref:System.Windows.FrameworkElement>クラスおよび<xref:System.Windows.FrameworkContentElement>両方を公開するクラス、`SetBinding`メソッドです。 これらのクラスを継承する要素をバインドする場合を呼び出すことができます、<xref:System.Windows.FrameworkElement.SetBinding%2A>メソッドを直接です。  
  
 次の例は、という名前のクラスを作成`MyData`、という名前のプロパティが含まれています`MyDataProperty`です。  
  
 [!code-csharp[CodeOnlyBinding#DataObject](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CodeOnlyBinding/CSharp/MyData.cs#dataobject)]
 [!code-vb[CodeOnlyBinding#DataObject](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CodeOnlyBinding/VisualBasic/MyData.vb#dataobject)]  
  
 次の例では、バインディングのソースを設定するバインディング オブジェクトを作成する方法を示します。  この例では<xref:System.Windows.FrameworkElement.SetBinding%2A>にバインドする、<xref:System.Windows.Controls.TextBlock.Text%2A>プロパティの`myText`、これは、<xref:System.Windows.Controls.TextBlock>コントロールを`MyDataProperty`です。  
  
 [!code-csharp[CodeOnlyBinding#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CodeOnlyBinding/CSharp/binding.cs#1)]
 [!code-vb[CodeOnlyBinding#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CodeOnlyBinding/VisualBasic/App.vb#1)]  
  
 完全なコード サンプルでは、次を参照してください。[コードのみのバインドのサンプル](http://msdn.microsoft.com/library/764aaf0b-2216-4941-9548-9c98da18d1a6)です。  
  
 呼び出し元ではなく<xref:System.Windows.FrameworkElement.SetBinding%2A>、使用することができます、<xref:System.Windows.Data.BindingOperations.SetBinding%2A>の静的メソッド、<xref:System.Windows.Data.BindingOperations>クラスです。 次の例を呼び出して<xref:System.Windows.Data.BindingOperations.SetBinding%2A?displayProperty=nameWithType>の代わりに<xref:System.Windows.FrameworkElement.SetBinding%2A?displayProperty=nameWithType>にバインドする`myText`に`myDataProperty`です。  
  
 [!code-csharp[CodeOnlyBinding#BOSetBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CodeOnlyBinding/CSharp/binding.cs#bosetbinding)]
 [!code-vb[CodeOnlyBinding#BOSetBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CodeOnlyBinding/VisualBasic/App.vb#bosetbinding)]  
  
## <a name="see-also"></a>関連項目  
 [データ バインディングの概要](../../../../docs/framework/wpf/data/data-binding-overview.md)  
 [方法トピック](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)
