---
title: '方法 : TableLayoutPanel コントロールの行と列を拡大する'
ms.date: 03/30/2017
f1_keywords:
- net.ComponentModel.StyleCollectionEditor.TLP.SpanRowsColumns
helpviewer_keywords:
- columns [Windows Forms], spanning
- merging cells
- TableLayoutPanel control [Windows Forms], spanning rows and columns
- rows [Windows Forms], spanning
- cells [Windows Forms], merging
ms.assetid: a8a2fdd3-a848-48b0-a4cd-4e85ebded87e
ms.openlocfilehash: a78286be8ef64212d945b3cb11a2963d5a1b2e79
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-span-rows-and-columns-in-a-tablelayoutpanel-control"></a>方法 : TableLayoutPanel コントロールの行と列を拡大する
コントロールで、<xref:System.Windows.Forms.TableLayoutPanel>コントロールが隣接する行と列にまたがることができます。  
  
> [!NOTE]
>  実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](http://msdn.microsoft.com/library/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
### <a name="to-span-columns-and-rows"></a>列と行にまたがること  
  
1.  ドラッグ、<xref:System.Windows.Forms.TableLayoutPanel>から制御、**ツールボックス**フォーム上にします。  
  
2.  ドラッグ、<xref:System.Windows.Forms.Button>から制御、**ツールボックス**の左上隅のセルに、<xref:System.Windows.Forms.TableLayoutPanel>コントロール。  
  
3.  設定、<xref:System.Windows.Forms.Button>コントロールの**ColumnSpan**プロパティを**2**です。 なお、<xref:System.Windows.Forms.Button>コントロールが最初と 2 番目の列にまたがってです。  
  
4.  設定、<xref:System.Windows.Forms.Button>コントロールの**RowSpan**プロパティを**2**です。 なお、<xref:System.Windows.Forms.Button>コントロールの最初と 2 番目の行にまたがって表示します。  
  
5.  設定、<xref:System.Windows.Forms.Button>コントロールの**ColumnSpan**プロパティを**1**です。 なお、<xref:System.Windows.Forms.Button>コントロールは、最初の列に移動し、最初と 2 番目の行にまたがるです。  
  
## <a name="see-also"></a>関連項目  
 [TableLayoutPanel コントロール](../../../../docs/framework/winforms/controls/tablelayoutpanel-control-windows-forms.md)
