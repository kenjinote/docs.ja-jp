---
title: '方法 : ペンの色を設定する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- pens [Windows Forms], setting color
- colored pens
ms.assetid: a9df06f9-a6d5-4d9b-a2d1-583943540775
ms.openlocfilehash: 37bc289fa1eeb7ef5510474dff062ae76be5fc65
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-set-the-color-of-a-pen"></a>方法 : ペンの色を設定する
この例は、既存の色を変更<xref:System.Drawing.Pen>オブジェクト  
  
## <a name="example"></a>例  
 [!code-cpp[System.Drawing.ConceptualHowTos#9](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/cpp/form1.cpp#9)]
 [!code-csharp[System.Drawing.ConceptualHowTos#9](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/CS/form1.cs#9)]
 [!code-vb[System.Drawing.ConceptualHowTos#9](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConceptualHowTos/VB/form1.vb#9)]  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 この例で必要な要素は次のとおりです。  
  
-   A<xref:System.Drawing.Pen>という名前のオブジェクト`myPen`です。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 呼び出す必要があります<xref:System.Drawing.Pen.Dispose%2A>システム リソースを消費しているオブジェクトの (など<xref:System.Drawing.Pen>オブジェクト) を使用してそれらが完了した後です。  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Drawing.Pen>  
 [グラフィックス プログラミングについて](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)  
 [方法: ペンを作成する](../../../../docs/framework/winforms/advanced/how-to-create-a-pen.md)  
 [ペンを使用した直線と図形の描画](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)  
 [GDI+ でのペン、直線、および四角形](../../../../docs/framework/winforms/advanced/pens-lines-and-rectangles-in-gdi.md)
