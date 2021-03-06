---
title: ポインターに対する算術演算 (C# プログラミング ガイド)
ms.date: 07/20/2015
helpviewer_keywords:
- pointers [C#], arithmetic operations
ms.assetid: d4f0b623-827e-45ce-8649-cfcebc8692aa
ms.openlocfilehash: c40b125e42649093aa1f1fe860a3e8f5d2690359
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="arithmetic-operations-on-pointers-c-programming-guide"></a>ポインターに対する算術演算 (C# プログラミング ガイド)
このトピックでは、算術演算子 `+` と **-** を使用したポインター操作について説明します。  
  
> [!NOTE]
>  void ポインターには、算術演算を実行できません。  
  
## <a name="adding-and-subtracting-numeric-values-to-or-from-pointers"></a>ポインターに対する数値の加算と減算  
 型が [int](../../../csharp/language-reference/keywords/int.md)、[uint](../../../csharp/language-reference/keywords/uint.md)、[long](../../../csharp/language-reference/keywords/long.md)、[ulong](../../../csharp/language-reference/keywords/ulong.md) のいずれかである値 `n` は、`void*` 型以外のあらゆるポインター `p` に加算できます。 結果の `p+n` は `n * sizeof(p) to the address of p` を加算した結果を表すポインターです。 同様に、`p-n` は `p` のアドレスから `n * sizeof(p)` を減算した結果を表すポインターです。  
  
## <a name="subtracting-pointers"></a>ポインターの減算  
 同じ型のポインターを減算することもできます。 結果は常に `long` 型になります。 たとえば場合、`p1` と `p2` が `pointer-type*` 型のポインターである場合、式 `p1-p2` の結果は次のようになります。  
  
 `((long)p1 - (long)p2)/sizeof(pointer_type)`  
  
 算術演算がポインターのドメインをオーバーフローしても、例外は生成されません。生じる結果は実装によって異なります。  
  
## <a name="example"></a>例  
 [!code-csharp[csProgGuidePointers#14](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/arithmetic-operations-on-pointers_1.cs)]  
  
 [!code-csharp[csProgGuidePointers#15](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/arithmetic-operations-on-pointers_2.cs)]  
  
## <a name="c-language-specification"></a>C# 言語仕様  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>参照  
 [C# プログラミング ガイド](../../../csharp/programming-guide/index.md)  
 [アンセーフ コードとポインター](../../../csharp/programming-guide/unsafe-code-pointers/index.md)  
 [ポインター式](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)  
 [C# 演算子](../../../csharp/language-reference/operators/index.md)  
 [ポインターの操作](../../../csharp/programming-guide/unsafe-code-pointers/manipulating-pointers.md)  
 [ポインター型](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)  
 [型](../../../csharp/language-reference/keywords/types.md)  
 [unsafe](../../../csharp/language-reference/keywords/unsafe.md)  
 [fixed ステートメント](../../../csharp/language-reference/keywords/fixed-statement.md)  
 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)
