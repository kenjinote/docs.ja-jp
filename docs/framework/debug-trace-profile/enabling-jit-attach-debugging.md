---
title: JIT アタッチ デバッグの有効化
ms.date: 03/30/2017
helpviewer_keywords:
- JIT-attach debugging
- debugging [.NET Framework], JIT-attach debugging
ms.assetid: f91fc5f7-de5a-4f23-b6ac-f450e63c662e
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 67db256f4c328b12d6cc30abfbe5d5ccc12e8b0a
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="enabling-jit-attach-debugging"></a>JIT アタッチ デバッグの有効化
JIT アタッチ デバッグとは、エラーが発生したとき、または特定のメソッドまたは関数によってトリガーすることで、プロセスにデバッガーをアタッチすることを表すために使用される語句です。  
  
 JIT アタッチ デバッグは、次のエラー状態で使用されます。  
  
-   未処理の例外 (ネイティブ コードとマネージ コードの両方)。  
  
-   <xref:System.Environment.FailFast%2A?displayProperty=nameWithType> メソッドまたは [RaiseFailFastException](http://go.microsoft.com/fwlink/?LinkId=182107) 関数 (Windows 7 ファミリ)。  
  
-   実行時の致命的なエラー。  
  
 JIT アタッチ デバッグは、次のメソッドや関数への呼び出しによってもトリガーされます。  
  
-   <xref:System.Diagnostics.Debugger.Launch%2A?displayProperty=nameWithType> メソッド  
  
-   <xref:System.Diagnostics.Debugger.Break%2A?displayProperty=nameWithType> メソッド  
  
-   [DebugBreak](http://go.microsoft.com/fwlink/?LinkId=182106) 関数 (Win32)。  
  
 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] より前のバージョンでは、.NET Framework がネイティブ デバッガーとマネージ デバッガーの動作を制御するために別々のレジストリ キーを提供していました。 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 以降では、制御が 1 つのレジストリ キー、HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\Current Version\AeDebug に統合されました。 このキーに設定できる値により、デバッガーを呼び出すかどうか、呼び出す場合は、ユーザーの操作を必要とするダイアログ ボックスによって呼び出すかどうかが決まります。 このレジストリ キーを設定する方法の詳細については、次を参照してください。[自動のデバッグを構成する](http://go.microsoft.com/fwlink/?LinkId=181767)です。  
  
## <a name="see-also"></a>関連項目  
 [デバッグ、トレース、およびプロファイリング](../../../docs/framework/debug-trace-profile/index.md)  
 [イメージのデバッグの簡略化](../../../docs/framework/debug-trace-profile/making-an-image-easier-to-debug.md)  
 [プロファイルの有効化](http://msdn.microsoft.com/library/3b669676-f0e0-4ebf-8674-68986dd2020d)
