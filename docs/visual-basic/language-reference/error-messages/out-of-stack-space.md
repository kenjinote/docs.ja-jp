---
title: スタック領域が不足しています。(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vbrID28
ms.assetid: bfcd792b-ac29-4158-81fc-ea0c13f4ffa2
ms.openlocfilehash: e39be5913fe877cf7b3396e4f13f4440288cb8f3
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="out-of-stack-space-visual-basic"></a>スタック領域が不足しています。(Visual Basic)
スタックは、実行しているプログラムの要求で動的に拡大および縮小するメモリの作業領域です。 上限を超えました。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1.  プロシージャが深すぎます。 入れ子にできないことを確認してください。  
  
2.  再帰プロシージャが正常に終了することを確認します。  
  
3.  ローカル変数では、ローカル変数領域を超える領域がある必要がある場合は、モジュール レベルでのいくつかの変数を宣言してみてください。 宣言することも、プロシージャのすべての変数静的前に追加して、 `Property`、 `Sub`、または`Function`キーワード`Static`です。 使用することができます、`Static`ステートメントをプロシージャ内で個別に静的変数を宣言します。  
  
4.  固定長文字列可変長文字列よりも多くのスタック領域を使用すると、可変長文字列として、固定長文字列の一部を再定義します。 ここでは必要ありませんスタック領域モジュール レベルで文字列を定義することもできます。  
  
5.  数を確認して入れ子になった`DoEvents`関数を使用して呼び出し、`Calls`ダイアログ ボックスで、スタック上でアクティブなプロシージャ ビューをします。  
  
6.  スタックで既にイベント プロシージャを呼び出すイベントをトリガーすることによって、「イベントの連鎖」を発生しないことを確認してください。 イベント cascade は、未終了の再帰的なプロシージャの呼び出しに似ていますのコード内の明示的な呼び出しではなく、Visual Basic での呼び出しが行われるために、わかりにくいがします。 使用して、`Calls`ダイアログ ボックスで、スタック上でアクティブなプロシージャ ビューをします。  
  
## <a name="see-also"></a>関連項目  
 [[メモリ] ウィンドウ](/visualstudio/debugger/memory-windows)
