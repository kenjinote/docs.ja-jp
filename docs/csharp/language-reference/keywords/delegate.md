---
title: delegate (C# リファレンス)
ms.date: 07/20/2015
f1_keywords:
- delegate_CSharpKeyword
- delegate
- CS0123
helpviewer_keywords:
- delegate keyword [C#]
- function pointers [C#]
ms.assetid: 0bb8cb6d-2f87-47c7-9d1f-d65c1cd01e9f
ms.openlocfilehash: 4eafd0ffb6da191db80fd69f1980a167dbfc742b
ms.sourcegitcommit: 89c93d05c2281b4c834f48f6c8df1047e1410980
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2018
---
# <a name="delegate-c-reference"></a>delegate (C# リファレンス)
デリゲート型の宣言は、メソッド シグネチャに似ています。 戻り値 1 つのほか、任意の型のパラメーターをいくつでも指定することができます。  
  
```csharp  
public delegate void TestDelegate(string message);  
public delegate int TestDelegate(MyType m, long num);  
```  
  
 `delegate` は、名前付きメソッドまたは匿名メソッドをカプセル化することができる参照型です。 デリゲートは C++ の関数ポインターに似ていますが、タイプ セーフであり安全です。 デリゲートの使い方については、[デリゲート](../../../csharp/programming-guide/delegates/index.md)と[汎用デリゲート](../../../csharp/programming-guide/generics/generic-delegates.md)に関するページを参照してください。  
  
## <a name="remarks"></a>コメント  
 デリゲートは[イベント](../../../csharp/programming-guide/events/index.md)の土台となる働きをします。  
  
 デリゲートは名前付きメソッドまたは匿名メソッドに関連付けることによって、インスタンス化することができます。 詳細については、[名前付きメソッド](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md)と[匿名メソッド](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)に関するページを参照してください。  
  
 デリゲートは、適合する入力パラメーターと戻り値の型を持ったメソッドまたはラムダ式でインスタンス化する必要があります。 メソッドのシグネチャでどの程度の変性が許容されるかについて詳しくは、[デリゲートの変性](../../programming-guide/concepts/covariance-contravariance/using-variance-in-delegates.md)に関するページを参照してください。 匿名メソッドで使用する場合は、デリゲートとそれに関連付けるコードとを一緒に宣言します。 このセクションでは、その両方の方法でデリゲートをインスタンス化しています。  
  
## <a name="example"></a>例  
 [!code-csharp[csrefKeywordsTypes#8](../../../csharp/language-reference/keywords/codesnippet/CSharp/delegate_1.cs)]  
  
## <a name="c-language-specification"></a>C# 言語仕様  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>参照  
 [C# リファレンス](../../../csharp/language-reference/index.md)  
 [C# プログラミング ガイド](../../../csharp/programming-guide/index.md)  
 [C# のキーワード](../../../csharp/language-reference/keywords/index.md)  
 [参照型](../../../csharp/language-reference/keywords/reference-types.md)  
 [デリゲート](../../../csharp/programming-guide/delegates/index.md)  
 [イベント](../../../csharp/programming-guide/events/index.md)  
 [名前付きメソッドを使用したデリゲートと匿名メソッドを使用したデリゲート](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md)  
 [匿名メソッド](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)
