---
title: Visual Basic における文字列の基本
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], Like operator
- strings [Visual Basic], Visual Basic
- strings [Visual Basic], regular expressions
ms.assetid: 5674418d-f00d-4f72-9f98-d15897793350
ms.openlocfilehash: 7d2477070dce558aa932c822852ac8ac9c6721e4
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="string-basics-in-visual-basic"></a>Visual Basic における文字列の基本
`String` データ型は、一連の文字を表します (各文字は `Char` データ型のインスタンスを表しています)。 このトピックでは、Visual Basic における文字列の基本的な概念について説明します。  
  
## <a name="string-variables"></a>文字列変数  
 文字列のインスタンスには、一連の文字を表すリテラル値を代入できます。 例えば:  
  
 [!code-vb[VbVbalrStrings#63](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_1.vb)]  
  
 `String` 変数は、文字列に評価される任意の式も受け取ることができます。 以下に例を示します。  
  
 [!code-vb[VbVbalrStrings#64](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_2.vb)]  
  
 `String` 変数に代入されるすべてのリテラルは、引用符 ("") で囲む必要があります。 これは、文字列内の引用符を引用符で表すことができないことを意味します。 たとえば、次のコードはコンパイラ エラーになります。  
  
 [!code-vb[VbVbalrStrings#65](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_3.vb)]  
  
 このコードでは、2 つ目の引用符の後で文字列が終了し、残りの部分はコードであるとコンパイラが解釈するため、エラーが発生します。 この問題を解決するためには、Visual Basic は、文字列内の 1 つの引用符としてリテラル文字列内の 2 つの引用符を解釈します。 次の例は、引用符を文字列に含めるための正しい方法を示しています。  
  
 [!code-vb[VbVbalrStrings#66](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_4.vb)]  
  
 前の例で、`Look` という単語の前の 2 つの引用符は、文字列内では 1 つの引用符になります。 行の末尾の 3 つの引用符は、文字列内の 1 つの引用符と文字列終端文字を表します。  
  
 文字列リテラルには、複数の行を含めることができます。  
  
```vb  
Dim x = "hello  
world"  
```  
  
 結果の文字列には、文字列リテラルで使用する改行シーケンス (vbcr、vbcrlf など) が含まれます。  古い回避策を使用する必要はなくなりました。  
  
```vb  
Dim x = <xml><![CDATA[Hello  
World]]></xml>.Value  
```  
  
## <a name="characters-in-strings"></a>文字列内の文字  
 文字列は、一連の `Char` 値であると考えることができます。また、配列の場合と同様に、`String` 型には文字列に対してさまざまな操作を行うことができる、組み込み関数があります。 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] のすべての配列のように、これらは 0 ベース配列です。 文字列内の特定の文字は、`Chars` プロパティを通じて参照できます。このプロパティでは、文字列内で文字が現れる位置を使用して、文字にアクセスできます。 例えば:  
  
 [!code-vb[VbVbalrStrings#67](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_5.vb)]  
  
 上の例で、文字列の `Chars` プロパティは、文字列内の 4 番目の文字 (つまり `D`) を返し、`myChar` に代入します。 `Length` プロパティを通じて、特定の文字列の長さを取得することもできます。 文字列に対して複数の配列型の操作を実行する必要がある場合は、文字列の `ToCharArray` 関数を使用して、文字列を `Char` インスタンスの配列に変換することができます。 例えば:  
  
 [!code-vb[VbVbalrStrings#68](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_6.vb)]  
  
 これで、変数 `myArray` の内容は、`Char` 値の配列になりました。各値は `myString` の文字を表しています。  
  
## <a name="the-immutability-of-strings"></a>文字列の不変性  
 文字列は*不変*つまり、その値を 1 回変更することはできませんが作成されました。 ただし、文字列変数に複数の値を代入できないわけではありません。 次に例を示します。  
  
 [!code-vb[VbVbalrStrings#69](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_7.vb)]  
  
 ここでは、文字列変数が作成され、値を設定され、その値が変更されています。  
  
 より具体的には、最初の行で型 `String` のインスタンスが作成され、値 `This string is immutable` が設定されます。 例の 2 番目の行では、新しいインスタンスが作成され、値 `Or is it?` が設定されます。文字列変数は、最初のインスタンスへの参照を破棄し、新しいインスタンスへの参照を格納します。  
  
 他の組み込みのデータ型とは異なり、`String` は参照型です。 参照型の変数が関数またはサブルーチンへの引数として渡されると、文字列の実際の値ではなく、データが格納されているメモリ アドレスへの参照が渡されます。 そのため、前の例では変数の名前は変わりませんが、新しい値を保持している、`String` クラスの新しい別のインスタンスを指すようになります。  
  
## <a name="see-also"></a>関連項目  
 [Visual Basic の文字列の概要](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)  
 [String データ型](../../../../visual-basic/language-reference/data-types/string-data-type.md)  
 [Char データ型](../../../../visual-basic/language-reference/data-types/char-data-type.md)  
 [基本的な文字列操作](../../../../standard/base-types/basic-string-operations.md)
