---
title: '方法: がかどうか、ファイル アセンブリ (Visual Basic)'
ms.date: 07/20/2015
ms.assetid: de26f410-9bd1-4b55-a343-cc82f81684be
ms.openlocfilehash: 84d45cea4a2557350edacd5f05b12c8ffcac4df8
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="how-to-determine-if-a-file-is-an-assembly-visual-basic"></a>方法: がかどうか、ファイル アセンブリ (Visual Basic)
ファイルが管理されていて、ファイルのメタデータにアセンブリ エントリが含まれている場合、そのファイルはアセンブリです。 アセンブリとメタデータの詳細については、「[アセンブリ マニフェスト](../../../../framework/app-domains/assembly-manifest.md)」を参照してください。  
  
## <a name="how-to-manually-determine-if-a-file-is-an-assembly"></a>ファイルがアセンブリかどうかを手動で確認する方法  
  
1.  [Ildasm.exe (IL 逆アセンブラー)](https://msdn.microsoft.com/library/f7dy01k1) を起動します。  
  
2.  テストするファイルを読み込みます。  
  
3.  **ILDASM** で、そのファイルが移植可能な実行可能 (PE) ファイルではないと報告された場合、そのファイルはアセンブリでありません。 詳細については、「[方法: アセンブリの内容を表示する](../../../../framework/app-domains/how-to-view-assembly-contents.md)」を参照してください。  
  
## <a name="how-to-programmatically-determine-if-a-file-is-an-assembly"></a>ファイルがアセンブリかどうかをプログラムによって確認する方法  
  
1.  テストするファイルの完全パスと名前を渡して、<xref:System.Reflection.AssemblyName.GetAssemblyName%2A> メソッドを呼び出します。  
  
2.  <xref:System.BadImageFormatException> 例外がスローされた場合、ファイルはアセンブリでありません。  
  
## <a name="example"></a>例  
 次の例では、DLL がアセンブリかどうかをテストして確認します。  
  
```vb  
Module Module1  
    Sub Main()  
        Try  
            Dim testAssembly As Reflection.AssemblyName =  
                                Reflection.AssemblyName.GetAssemblyName("C:\Windows\Microsoft.NET\Framework\v3.5\System.Net.dll")  
            Console.WriteLine("Yes, the file is an Assembly.")  
        Catch ex As System.IO.FileNotFoundException  
            Console.WriteLine("The file cannot be found.")  
        Catch ex As System.BadImageFormatException  
            Console.WriteLine("The file is not an Assembly.")  
        Catch ex As System.IO.FileLoadException  
            Console.WriteLine("The Assembly has already been loaded.")  
        End Try  
        Console.ReadLine()  
    End Sub  
End Module  
' Output (with .NET Framework 3.5 installed):  
'        Yes, the file is an Assembly.  
```
  
 <xref:System.Reflection.AssemblyName.GetAssemblyName%2A> メソッドはテスト ファイルを読み込み、情報が読み取られた時点で解放します。  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Reflection.AssemblyName>  
 [プログラミングの概念](../../../../visual-basic/programming-guide/concepts/index.md)  
 [アセンブリとグローバル アセンブリ キャッシュ (Visual Basic)](index.md)
