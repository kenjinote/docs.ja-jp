---
title: Visual Basic の演算子および式
ms.date: 07/20/2015
helpviewer_keywords:
- operators [Visual Basic], operands
- operators [Visual Basic]
- operands [Visual Basic], definition
- Visual Basic code, operators
- Visual Basic code, expressions
- operands
- expressions [Visual Basic]
ms.assetid: b86f3131-94ee-448f-96cd-79611e028b26
ms.openlocfilehash: 06397cf05fc4da977cfecb8e412f12766a2a342d
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="operators-and-expressions-in-visual-basic"></a>Visual Basic の演算子および式
*演算子*は、値が格納されている 1 つ以上のコード要素に対して演算を実行するコード要素です。 値要素は、変数、定数、リテラル、プロパティ、`Function` プロシージャおよび `Operator` プロシージャからの戻り値、式などです。  
  
 *式*は、演算子で結合され、新しい値を生成する一連の値要素です。 演算子は、値要素に対して、計算、比較、またはその他の演算を実行します。  
  
## <a name="types-of-operators"></a>演算子の種類  
 Visual Basic では、次の種類の演算子を提供します。  
  
-   [算術演算子](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)は、数値に対して一般的な計算を実行します (ビット パターンのシフトも含まれます)。  
  
-   [比較演算子](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)は、2 つの式を比較し、比較の結果を表す `Boolean` 値を返します。  
  
-   [連結演算子](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md)は、複数の文字列を結合して 1 つの文字列にします。  
  
-   [Visual Basic の論理演算子およびビット処理演算子](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)は、`Boolean` 値または数値を組み合わせて、同じデータ型の結果を値として返します。  
  
 演算子で結合される値要素は、演算子の*オペランド*と呼ばれます。 演算子は値要素と結合されると*式*になります。ただし、代入演算子は例外で、これはステートメントになります。 詳細については、「[ステートメント](../../../../visual-basic/programming-guide/language-features/statements.md)」を参照してください。  
  
## <a name="evaluation-of-expressions"></a>式の評価  
 式の最終的な結果は、通常、`Boolean`、`String`、または数値型などの一般的なデータ型で表されます。  
  
 次に式の例をいくつか示します。  
  
 `5 + 4`  
  
 `' The preceding expression evaluates to 9.`  
  
 `15 * System.Math.Sqrt(9) + x`  
  
 `' The preceding expression evaluates to 45 plus the value of x.`  
  
 `"Concat" & "ena" & "tion"`  
  
 `' The preceding expression evaluates to "Concatenation".`  
  
 `763 < 23`  
  
 `' The preceding expression evaluates to False.`  
  
 次の例のように、1 つの式またはステートメントで複数の演算子を使うこともできます。  
  
 [!code-vb[VbVbalrOperators#56](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/index_1.vb)]  
  
 上記の例では、Visual Basic は、代入演算子の右側にある式での操作を実行 (`=`)、結果の値を変数に代入`x`左側です。 1 つの式で使用できる演算子の数には、事実上制限はありません。ただし、正しい結果を得るには、[Visual Basic における演算子の優先順位](../../../../visual-basic/language-reference/operators/operator-precedence.md)を理解する必要があります。  
  
 使用例を含む詳細については、「[Visual Basic 2005 での演算子のオーバーロード](http://go.microsoft.com/fwlink/?LinkId=101703)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [演算子](../../../../visual-basic/language-reference/operators/index.md)  
 [演算子の効率のよい組み合わせ](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/efficient-combination-of-operators.md)  
 [ステートメント](../../../../visual-basic/language-reference/statements/index.md)
