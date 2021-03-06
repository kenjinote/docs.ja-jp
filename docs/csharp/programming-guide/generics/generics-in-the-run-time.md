---
title: ランタイムのジェネリック (C# プログラミング ガイド)
ms.date: 07/20/2015
helpviewer_keywords:
- generics [C#], at run time
ms.assetid: 119df7e6-9ceb-49df-af36-24f8f8c0747f
ms.openlocfilehash: c7cc0580398eeb5c70422cba3569340133107b12
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="generics-in-the-run-time-c-programming-guide"></a>ランタイムのジェネリック (C# プログラミング ガイド)
ジェネリック型またはメソッドが Microsoft 中間言語 (MSIL) にコンパイルされるとき、型パラメーターありとして識別するメタデータが追加されます。 ジェネリック型の MSIL の使われ方は、指定した型パラメーターの種類 (値型または参照型) によって異なります。  
  
 ジェネリック型が値型をパラメーターとして最初に構築されるとき、ランタイムにより、特殊なジェネリック型が作成されます。このとき、MSIL の適切な場所で指定のパラメーターが代わりに使用されます。 特殊なジェネリック型は、パラメーターとして使用される一意の値型ごとに 1 回作成されます。  
  
 たとえば、プログラム コードで、整数で構成されるスタックを宣言したとします。  
  
 [!code-csharp[csProgGuideGenerics#42](../../../csharp/programming-guide/generics/codesnippet/CSharp/generics-in-the-run-time_1.cs)]  
  
 この時点で、整数がそのパラメーターに合わせて置き換えられた <xref:System.Collections.Generic.Stack%601> クラスの特殊なバージョンがランタイムにより生成されます。 プログラム コードで整数のスタックを使用するたびに、ランタイムは、生成された特殊な <xref:System.Collections.Generic.Stack%601> クラスを再利用します。 次の例では、整数のスタックの 2 つのインスタンスが作成され、`Stack<int>` コードの単一インスタンスを共有します。  
  
 [!code-csharp[csProgGuideGenerics#43](../../../csharp/programming-guide/generics/codesnippet/CSharp/generics-in-the-run-time_2.cs)]  
  
 ただし、`long` のような異なる値型を持つか、パラメーターとしてユーザー定義構造を持つ別の <xref:System.Collections.Generic.Stack%601> クラスがコード内の別のポイントで作成されると想定します。 結果として、ランタイムによりジェネリック型の別バージョンが生成され、MSIL 内の適切な場所で `long` を代わりに使います。 特殊なジェネリック クラスにはそれぞれ、ネイティブで値型が含まれているため、変換は必要ありません。  
  
 参照型の場合、ジェネリックの動作は少し異なります。 何らかの参照型でジェネリック型を初めて構築するとき、ランタイムは、MSIL のパラメーターの代わりに使用されているオブジェクト参照を利用して特殊なジェネリック型を作成します。 その後、構築された型が参照型をそのパラメーターとしてインスタンス化されるたびに、型に関係なく、ランタイムは、以前に利用した特殊なバージョンのジェネリック型を再利用します。 すべての参照のサイズが同じであるため、これが可能になります。  
  
 たとえば、`Customer` クラスと `Order` クラスという 2 つの参照型があるとき、`Customer` 型のスタックを作成したとします。  
  
 [!code-csharp[csProgGuideGenerics#47](../../../csharp/programming-guide/generics/codesnippet/CSharp/generics-in-the-run-time_3.cs)]  
  
 [!code-csharp[csProgGuideGenerics#44](../../../csharp/programming-guide/generics/codesnippet/CSharp/generics-in-the-run-time_4.cs)]  
  
 この時点で、オブジェクト参照を格納する <xref:System.Collections.Generic.Stack%601> クラスの特殊なバージョンがランタイムにより生成されます。データを保存しなくても、後にオブジェクト参照にデータが入力されます。 次のコード行により、`Order` という名前のもう 1 つの参照型のスタックが作成されるとします。  
  
 [!code-csharp[csProgGuideGenerics#45](../../../csharp/programming-guide/generics/codesnippet/CSharp/generics-in-the-run-time_5.cs)]  
  
 値型とは異なり、<xref:System.Collections.Generic.Stack%601> クラスのもう 1 つの特殊なバージョンは `Order` 型に対して作成されません。 代わりに、<xref:System.Collections.Generic.Stack%601> クラスの特殊なバージョンのインスタンスが作成され、それを参照するように `orders` 変数が設定されます。 その後、`Customer` 型のスタックを作成するコード行が見つかったとします。  
  
 [!code-csharp[csProgGuideGenerics#46](../../../csharp/programming-guide/generics/codesnippet/CSharp/generics-in-the-run-time_6.cs)]  
  
 `Order` 型を利用して作成された <xref:System.Collections.Generic.Stack%601> クラスの前の使用と同様に、特殊な <xref:System.Collections.Generic.Stack%601> クラスのもう 1 つのインスタンスが作成されます。 そこに含まれるポインターは、`Customer` 型のサイズのメモリ領域を参照するように設定されています。 参照型はプログラムによって大きく異なることがあるため、ジェネリックの C# 実装では、コードの量が大幅に、参照型のジェネリック クラスのコンパイラにより作成された特殊なクラスの数まで減ります。  
  
 また、ジェネリック C# クラスが値型または参照型パラメーターの利用によりインスタンス化されるとき、ランタイム時にリフレクションがクエリを実行し、その型パラメーターを確かめることができます。  
  
## <a name="see-also"></a>参照  
 <xref:System.Collections.Generic>  
 [C# プログラミング ガイド](../../../csharp/programming-guide/index.md)  
 [ジェネリックの概要](../../../csharp/programming-guide/generics/introduction-to-generics.md)  
 [ジェネリック](~/docs/standard/generics/index.md)
