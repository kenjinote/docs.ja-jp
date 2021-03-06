---
title: アクセサーのアクセシビリティの制限 (C# プログラミング ガイド)
ms.date: 07/20/2015
helpviewer_keywords:
- read-only properties [C#]
- read-only indexers [C#]
- accessors [C#]
- properties [C#], read-only
- asymmetric accessor accesibility [C#]
- indexers [C#], read-only
ms.assetid: 6e655798-e112-4301-a680-6310a6e012e1
ms.openlocfilehash: bf9ead7934630d3974657107ca38e08bbd3bed85
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="restricting-accessor-accessibility-c-programming-guide"></a>アクセサーのアクセシビリティの制限 (C# プログラミング ガイド)
プロパティまたはインデクサーの [get](../../../csharp/language-reference/keywords/get.md) および [set](../../../csharp/language-reference/keywords/set.md) 部分は、*アクセサー*と呼ばれます。 既定では、これらのアクセサーは、それらが属するプロパティまたはインデクサーと同じ可視性またはアクセス レベルを持っています。 詳細については、「[アクセシビリティ レベル](../../../csharp/language-reference/keywords/accessibility-levels.md)」を参照してください。 ただし、これらのアクセサーのいずれかにアクセスを制限すると便利な場合があります。 通常、これには、`set` アクセサーのアクセシビリティを制限しながら、`get` アクセサーのパブリック アクセスを維持する操作が含まれます。 例:  
  
 [!code-csharp[csProgGuideIndexers#6](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/restricting-accessor-accessibility_1.cs)]  
  
 この例では、`Name` というプロパティが `get` および `set` アクセサーを定義します。 `get` アクセサーは、プロパティ自体のアクセシビリティ レベル (この場合は `public`) を受け取り、同時に `set` アクセサーは、[protected](../../../csharp/language-reference/keywords/protected.md) アクセサー修飾子をアクセサー自体に適用することによって明示的に制限されます。  
  
## <a name="restrictions-on-access-modifiers-on-accessors"></a>アクセサーのアクセス修飾子の制限  
 プロパティまたはインデクサーでのアクセサー修飾子の使用は、以下の条件の対象になります。  
  
-   インターフェイスまたは明示的な [interface](../../../csharp/language-reference/keywords/interface.md) メンバーの実装でアクセサー修飾子を使用することはできません。  
  
-   アクセサー修飾子は、プロパティまたはインデクサーに `set` と `get` アクセサーの両方がある場合にのみ使用できます。 この場合、修飾子は、2 つのアクセサーのいずれかでのみ許可されます。  
  
-   プロパティまたはインデクサーに [override](../../../csharp/language-reference/keywords/override.md) 修飾子がある場合は、アクセサー修飾子はオーバーライドされるアクセサーのアクセサー (存在する場合) と一致する必要があります。  
  
-   アクセサーのアクセシビリティ レベルは、プロパティまたはインデクサー自体のアクセシビリティ レベルよりも制限されていなければなりません  
  
## <a name="access-modifiers-on-overriding-accessors"></a>オーバーライドするアクセサーのアクセス修飾子  
 プロパティまたはインデクサーをオーバーライドする場合は、オーバーライドされたアクセサーがオーバーライドするコードにアクセスできなければなりません。 プロパティ/インデクサーの両方のアクセシビリティ レベル、およびアクセサーのアクセシビリティレベルが、対応するオーバーライドされるプロパティ/インデクサーおよびアクセサーと一致している必要があります。 例:  
  
 [!code-csharp[csProgGuideIndexers#7](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/restricting-accessor-accessibility_2.cs)]  
  
## <a name="implementing-interfaces"></a>インターフェイスの実装  
 アクセサーを使用してインターフェイスを実装する場合、アクセサーがアクセス修飾子を持つことはできません。 ただし、`get` などの 1 つのアクセサーを使用してインターフェイスを実装する場合、他のアクセサーは、次の例のように、アクセス修飾子を持つことができます。  
  
 [!code-csharp[csProgGuideIndexers#8](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/restricting-accessor-accessibility_3.cs)]  
  
## <a name="accessor-accessibility-domain"></a>アクセサー アクセシビリティ ドメイン  
 アクセサーでアクセス修飾子を使用する場合、アクセサーの[アクセシビリティ ドメイン](../../../csharp/language-reference/keywords/accessibility-domain.md)はこの修飾子によって決まります。  
  
 アクセサーでアクセス修飾子を使用しなかった場合、アクセサーのアクセシビリティ ドメインは、プロパティまたはインデクサーのアクセシビリティ レベルによって決まります。  
  
## <a name="example"></a>例  
 次の例は、`BaseClass`、`DerivedClass`、および `MainClass` という 3 つのクラスを含んでいます。 すべてのクラスの `BaseClass`、`Name`、`Id` に 2 つのプロパティがあります。 この例は、[protected](../../../csharp/language-reference/keywords/protected.md) や [private](../../../csharp/language-reference/keywords/private.md) などの制限アクセス修飾子を使用するときに、`BaseClass` のプロパティ `Id` によって `DerivedClass` のプロパティ `Id` を非表示にする方法を示しています。 そのため、このプロパティに値を割り当てるときには、代わりに `BaseClass` クラスのプロパティが呼び出されます。 [public](../../../csharp/language-reference/keywords/public.md) によってアクセス修飾子を置き換えると、プロパティがアクセス可能になります。  
  
 この例はまた、`DerivedClass` の `Name` プロパティの `set` アクセサー上の `private` や `protected` などの制限されるアクセス修飾子が、アクセサーへのアクセスを防ぎ、アクセサーに割り当てたときにエラーが生成されることも示しています。  
  
 [!code-csharp[csProgGuideIndexers#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/restricting-accessor-accessibility_4.cs)]  
  
## <a name="comments"></a>コメント  
 宣言 `new private string Id` を `new public string Id` によって置き換えた場合、次の出力を取得します。  
  
 `Name and ID in the base class: Name-BaseClass, ID-BaseClass`  
  
 `Name and ID in the derived class: John, John123`  
  
## <a name="see-also"></a>参照  
 [C# プログラミング ガイド](../../../csharp/programming-guide/index.md)  
 [プロパティ](../../../csharp/programming-guide/classes-and-structs/properties.md)  
 [インデクサー](../../../csharp/programming-guide/indexers/index.md)  
 [アクセス修飾子](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)
