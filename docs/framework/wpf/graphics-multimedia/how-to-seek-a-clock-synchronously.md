---
title: '方法 : クロックを同期的にシークする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- clocks [WPF], seeking synchronously
- seeking clocks synchronously [WPF]
ms.assetid: e5b7529b-b7d0-40d2-9e1d-fa4b5e736e96
ms.openlocfilehash: d8e7b0f4bfa3a59814d87bfb6d7e8b40bd80f6e3
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-seek-a-clock-synchronously"></a>方法 : クロックを同期的にシークする
使用して、<xref:System.Windows.Media.Animation.ClockController.SeekAlignedToLastTick%2A>メソッドを特定の時点までのクロックを同期的にシークします。 次の例では、両方を示しています、<xref:System.Windows.Media.Animation.ClockController.Seek%2A>と<xref:System.Windows.Media.Animation.ClockController.SeekAlignedToLastTick%2A>のメソッド、<xref:System.Windows.Media.Animation.ClockController>です。  
  
 この例では、シーク、 <xref:System.Windows.Media.Animation.Clock>; を参照してください、ストーリー ボードをシークする方法を示す例については[、ストーリー ボード同期的にシーク](../../../../docs/framework/wpf/graphics-multimedia/how-to-seek-a-storyboard-synchronously.md)です。  
  
## <a name="example"></a>例  
 [!code-csharp[ClockController_procedural_snip#ClockControllerSeekExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ClockController_procedural_snip/CSharp/SeekAlignedToLastTickExample.cs#clockcontrollerseekexample)]
 [!code-vb[ClockController_procedural_snip#ClockControllerSeekExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ClockController_procedural_snip/visualbasic/seekalignedtolasttickexample.vb#clockcontrollerseekexample)]
