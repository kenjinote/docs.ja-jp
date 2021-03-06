---
title: F# では、Visual Studio での概要します。
description: Visual Studio で f# を使用する方法を説明します。
ms.date: 02/13/2017
ms.openlocfilehash: 22fbe8086ec133605e1d9b4b28e524fe2ed8ac28
ms.sourcegitcommit: bbf70abe6b46073148f78cbf0619de6092b5800c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2018
ms.locfileid: "34728535"
---
# <a name="get-started-with-f-in-visual-studio"></a>F# では、Visual Studio での概要します。

Visual Studio IDE では、f# および Visual f# ツールがサポートされます。  作業を開始するには[Visual Studio のダウンロード](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs)まだ行っていない場合は、します。  この記事の内容が Visual Studio 2017 Community Edition を使用しますが、任意のバージョンの F# で使用することができます。

## <a name="installing-f"></a>F# をインストールします。 #

最初に Visual Studio をダウンロードしている場合、Visual Studio インストーラーが最初にインストールされます。  インストーラーから Visual Studio 2017 の任意のバージョンをインストールします。 既にインストールされていることをクリックして**変更**です。

次に、ワークロードの一覧を表示されます。 F# では、次のワークロードのを通じてにインストールできます。

|ワークロード|アクション|
|--------|------|
| .NET Core クロスプラットフォームの開発 | 既定では、f# のアクションがインストールされていません |
| ASP.NET と Web 開発 | 既定では、f# のアクションがインストールされていません |
| Azure の開発 | 既定では、f# のアクションがインストールされていません |
| .NET によるモバイル開発 | 既定では、f# のアクションがインストールされていません |
| データ サイエンスと分析のアプリケーション | 既定では、f# のアクションがインストールされていません |
| .NET デスクトップ開発 | 選択**f# デスクトップの言語サポート**右側から |
| データ ストレージとデータ処理 | 選択**f# デスクトップの言語サポート**右側から |

次に、をクリックして**変更**右下にします。  選択したすべてのものがインストールされます。  クリックして、f# 言語のサポートを備えた Visual Studio 2017 を開くことができますし、**起動**です。

## <a name="creating-a-console-application"></a>コンソール アプリケーションを作成します。

Visual Studio での最も基本的なプロジェクトの 1 つは、コンソール アプリケーションです。  これを行う方法を次に示します。  Visual Studio が起動したら。

1. **ファイル** メニューのをポイント**新規**を選択し**プロジェクト**です。

2.  新規のプロジェクトのダイアログ ボックスで、**テンプレート**、表示されるはず**Visual f#** です。  F# のテンプレートを表示する場合に選択します。

3. いずれかを選択 **.NET Core コンソール アプリ**または**コンソール アプリ**です。

3. 選択、**わかりました**f# プロジェクトを作成するボタンです。  ソリューション エクスプ ローラーで f# プロジェクトが表示されます。

## <a name="writing-your-code"></a>コードの記述

最初にいくつかのコードを記述して開始しましょう。  確認して、`Program.fs`ファイルが開いている場合と、その内容を次に置き換えます。

[!code-fsharp[HelloSquare](../../../samples/snippets/fsharp/getting-started/hello-square.fs)]

前のコード例の関数で`square`が定義されているという名前の入力を取り`x`単独で乗算します。  F# で使用されるため[型の推論](../language-reference/type-inference.md)の型`x`を指定する必要はありません。  F# コンパイラは乗算が有効で型を認識し、型に割り当てられます`x`方法に基づいて`square`と呼びます。  ポインターを合わせる場合`square`次を参照する必要があります。

```
val square: x:int -> int
```

これは、関数の型のシグネチャと呼ばれるものです。  次のように読み取ることができます:"正方形をという名前の整数を受け取る関数は、x と整数が生成されます"です。  コンパイラから受け取った注`square`、`int`型ここでは、これは、ジェネリックであるため乗算いない間は*すべて*型しますが、ではなくがジェネリック型の closed set 間でします。  選択、f# コンパイラ`int`このポイントが調整されます型シグネチャを呼び出す場合`square`と、別の入力など、型、`float`です。

別の関数、 `main`、定義されるで装飾されている、 `EntryPoint` f# コンパイラにそのプログラムの実行を指示する属性を開始する必要がありますがあります。  その他のと同じ規則に従う[C スタイルのプログラミング言語](https://en.wikipedia.org/wiki/Entry_point#C_and_C.2B.2B)コマンドライン引数は、この関数に渡すことが、整数コードが返されます (通常`0`)。

このために呼び出される関数では、`square`関数の引数を持つ`12`します。  F# コンパイラの型が割り当てられます`square`する`int -> int`(を受け取る関数は、`int`を生成し、 `int`)。  呼び出し`printfn`を C スタイルのプログラミング言語、書式指定文字列で指定された値に対応するパラメーターに類似した形式の文字列を使用して書式設定された印刷機能であり、結果と新しい行に出力します。

## <a name="running-your-code"></a>コードの実行

コードを実行し、キーを押して結果を表示することができます**ctrl + f5**です。  これは、デバッグを行わず、プログラムを実行し、結果を確認することができます。  または、選択することができます、**デバッグ**トップレベル メニューは、Visual Studio 内の項目し、選択**デバッグなしで開始**です。

Visual Studio のポップをコンソール ウィンドウに出力され、次が表示されます。

```
12 squared is 144!
```

おめでとうございます!   Visual Studio で初めての f# プロジェクトを作成、f# の関数は、その関数の呼び出しの結果を印刷書き込まれ、いくつかの結果を表示するプロジェクトを実行しました。

## <a name="next-steps"></a>次の手順

まだの場合はチェック アウト、[ツアーの f#](../tour.md)、f# 言語のコア機能の一部をカバーします。  一部の f# では、機能の概要を知るされ Visual Studio にコピーし、実行できる十分なコード サンプルを入力します。  使用できますが、いくつかの優れた外部リソースからの[f# ガイド](../index.md)です。

## <a name="see-also"></a>関連項目
 [Visual F#](index.md)  
 [F# のツアー](../tour.md)  
 [F# 言語リファレンス](../language-reference/index.md)  
 [型の推論](../language-reference/type-inference.md)  
 [シンボルと演算子のリファレンス](../language-reference/symbol-and-operator-reference/index.md)  
