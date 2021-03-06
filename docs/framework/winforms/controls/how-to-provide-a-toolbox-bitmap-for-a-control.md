---
title: '方法 : コントロールにツールボックス ビットマップを指定する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Toolbox [Windows Forms], adding bitmaps for custom controls
- custom controls [Windows Forms], Toolbox bitmaps
- bitmaps [Windows Forms], custom controls
ms.assetid: 0ed0840a-616d-41ba-a27d-3573241932ad
ms.openlocfilehash: 3698d2fdbd0375d0a154d6ecea3a248b31da2aeb
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-provide-a-toolbox-bitmap-for-a-control"></a>方法 : コントロールにツールボックス ビットマップを指定する
コントロールの特別なアイコンが表示する場合、**ツールボックス**を使用して特定のイメージを指定することができます、<xref:System.Drawing.ToolboxBitmapAttribute>です。 このクラスは "*属性*" であり、他のクラスに追加できる特殊なクラスです。 属性の詳細については、次を参照してください。[ビルド内にありません: Visual Basic での属性の概要](http://msdn.microsoft.com/library/0d0cff64-892d-4f57-83bd-bef388553d4f)Visual basic の場合と[属性](http://msdn.microsoft.com/library/ae334cee-d96c-4243-a5e3-06dd7fcaf205)Visual c# の場合。  
  
 使用して、 <xref:System.Drawing.ToolboxBitmapAttribute>16 で 16 ピクセルのビットマップのパスとファイル名を示す文字列を指定できます。 コントロールを**ツールボックス**に追加すると、このビットマップがコントロールの横に表示されます。 指定することも、 <xref:System.Type>、その種類に関連付けられたビットマップが読み込まれている場合。 両方を指定する場合、<xref:System.Type>文字列、コントロールを検索対象のイメージ リソースで指定された型を含むアセンブリの文字列パラメーターで指定された名前を持つ、<xref:System.Type>パラメーター。  
  
### <a name="to-specify-a-toolbox-bitmap-for-your-control"></a>コントロールのツールボックス ビットマップを指定するには  
  
1.  追加、<xref:System.Drawing.ToolboxBitmapAttribute>する前に、コントロールのクラス宣言に、 `Class` visual basic および Visual c# のクラスの宣言の上のキーワードです。  
  
    ```vb  
    ' Specifies the bitmap associated with the Button type.  
    <ToolboxBitmap(GetType(Button))> Class MyControl1  
    ' Specifies a bitmap file.  
    End Class  
    <ToolboxBitmap("C:\Documents and Settings\Joe\MyPics\myImage.bmp")> _  
       Class MyControl2  
    End Class  
    ' Specifies a type that indicates the assembly to search, and the name   
    ' of an image resource to look for.  
    <ToolboxBitmap(GetType(MyControl), "MyControlBitmap")> Class MyControl  
    End Class  
    ```  
  
    ```csharp  
    // Specifies the bitmap associated with the Button type.  
    [ToolboxBitmap(typeof(Button))]  
    class MyControl1 : UserControl  
    {  
    }  
    // Specifies a bitmap file.  
    [ToolboxBitmap(@"C:\Documents and Settings\Joe\MyPics\myImage.bmp")]  
    class MyControl2 : UserControl  
    {  
    }  
    // Specifies a type that indicates the assembly to search, and the name   
    // of an image resource to look for.  
    [ToolboxBitmap(typeof(MyControl), "MyControlBitmap")]  
    class MyControl : UserControl  
    {  
    }  
    ```  
  
2.  プロジェクトをリビルドします。  
  
    > [!NOTE]
    >  ビットマップは、自動生成されたコントロールとコンポーネントのツールボックスには表示されません。 ビットマップを表示するには、**[ツールボックス アイテムの選択]** ダイアログ ボックスを使用してコントロールを再読み込みします。 詳細については、「[チュートリアル: ツールボックスへのカスタム コンポーネントの自動設定](../../../../docs/framework/winforms/controls/walkthrough-automatically-populating-the-toolbox-with-custom-components.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Drawing.ToolboxBitmapAttribute>  
 [チュートリアル: ツールボックスへのカスタム コンポーネントの自動設定](../../../../docs/framework/winforms/controls/walkthrough-automatically-populating-the-toolbox-with-custom-components.md)  
 [デザイン時の Windows フォーム コントロールの開発](../../../../docs/framework/winforms/controls/developing-windows-forms-controls-at-design-time.md)  
 [属性 (Visual Basic)](~/docs/visual-basic/language-reference/attributes.md)  
 [属性](http://msdn.microsoft.com/library/ae334cee-d96c-4243-a5e3-06dd7fcaf205)
