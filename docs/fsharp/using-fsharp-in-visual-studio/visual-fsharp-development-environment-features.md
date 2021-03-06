---
title: F# の開発環境の機能
description: F# でサポートされる Visual Studio 2012 の機能について説明します。
ms.date: 05/16/2016
ms.openlocfilehash: 0ea2bfa439692045647efa29b2a051eb11f9f1dc
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="visual-f-development-environment-features"></a>Visual F# の開発環境の機能

> [!NOTE]
この記事は、最新の Visual Studio と最新の状態はありません。  これは更新されます。

このトピックには、f# での Visual Studio 2012 の機能のサポートについての情報が含まれます。

## <a name="project-features"></a>プロジェクトの機能
次の表は、f# プロジェクトで使用するために使用できるテンプレートをまとめたものです。 プロジェクトと項目テンプレートについては、次を参照してください。 [NIB テンプレートからプロジェクトの作成](https://msdn.microsoft.com/library/7c36d86a-6b79-4480-8228-0f925f1204b2)です。

|テンプレートの種類|説明|サポートされているテンプレート|
|-------------|-----------|-------------------|
|プロジェクト テンプレート|使用できるプロジェクトの種類、**新しいプロジェクト** ダイアログ ボックス。|<ul><li>F# アプリケーション<br /></li><li>F# ライブラリ<br /></li><li>F# チュートリアル<br /></li><li>F# ポータブル ライブラリ<br /></li><ul/>|
|項目テンプレート|ファイルの種類で使用できる、**新しい項目の追加** ダイアログ ボックス。|<ul><li>F# ソース ファイル (.fs)<br /></li><li>F# スクリプト (ファイル.fsx)<br /></li><li>F# シグネチャ ファイル (.fsi)<br /></li><li>構成ファイル (.config)<br /></li><li>SQL データベース接続 (LINQ to SQL 型プロバイダー)<br /></li><li>SQL データベース接続 (LINQ to Entities 型プロバイダー)<br /></li><li>OData サービス接続 (LINQ 型プロバイダー)<br /></li><li>WSDL サービス接続 (型プロバイダー)<br /></li><li>XML ファイル (.xml)<br /></li><li>テキスト ファイル<br /></li><ul/>|
スタンドアロンの実行可能ファイルとして実行できるアプリケーションを作成するには、f# アプリケーション プロジェクトの種類を選択します。 ライブラリを作成する (つまり、マネージ アセンブリまたはします。DLL ファイル)、Windows デスクトップ プラットフォームで使用する、f# ライブラリを選択します。 サポートされている任意のプラットフォームで使用できるポータブル ライブラリを作成するには、f# ポータブル ライブラリを選択します。 F# ポータブル ライブラリ プロジェクトでは、Windows ストア アプリ、.NET Framework 4.5、Xamarin.iOS および Xamarin.Android などのプラットフォームで実行されるアプリケーションで使用できる f# ライブラリを作成するには、適切な FSharp.Core.dll のバージョンを参照します。

データ アクセスのアイテム テンプレートについての詳細については、次を参照してください。[型プロバイダー](../tutorials/type-providers/index.md)です。

次の表は、プロジェクト プロパティの機能サポートし、f# でサポートされていません。 詳細については、次を参照してください。[構成プロジェクト](configuring-projects.md)と[プロジェクト デザイナーの概要](https://msdn.microsoft.com/library/898dd854-c98d-430c-ba1b-a913ce3c73d7)です。

|プロジェクト設定|F# でサポートされているか。|メモ|
|---------------|----------------|-----|
|リソース ファイル|[はい]||
|ビルド、デバッグ、および参照の設定|[はい]||
|マルチ ターゲット|[はい]||
|アイコンとマニフェスト|×|コンパイラのコマンド ライン オプションを使用します。|
|サービスの ASP.NET クライアント|×||
|ClickOnce|×|該当する場合は、別の .NET Framework 言語でクライアント プロジェクトを使用します。|
|厳密な名前付け|×|コンパイラのコマンド ライン オプションを使用します。|
|アセンブリの発行とバージョン管理|×||
|コード分析|×|コード分析ツールは、手動でまたはビルド後コマンドの一部として実行できます。|
|セキュリティ (信頼レベルの変更)|×||

## <a name="code-and-text-editor-features"></a>コードとテキスト エディターの機能
Visual Studiocode とテキスト エディターの次の機能は、f# でサポートされます。 Visual Studio、およびテキスト エディターの機能のコードの編集の詳細については、次を参照してください。[コード エディターとテキスト エディターでコードを記述](/visualstudio/ide/writing-code-in-the-code-and-text-editor)です。

|機能|説明|F# でサポートされているか。|
|-------|-----------|----------------|
|自動的にコメント|使用すると、コメント、またはコードのセクションのコメントを解除できます。|はい|
|自動的に書式設定します。|標準のインデントとスタイルでコードを再フォーマットします。|×|
|ブックマーク|エディターでの場所を保存できます。|[はい]|
|インデントを変更します。|インデントを設定または選択した行のインデントを設定解除します。|[はい]|
|[テキストの検索と置換](/visualstudio/ide/finding-and-replacing-text)|使用すると、ファイル、プロジェクト、またはソリューションで検索し、可能性のあるテキストを変更できます。|[はい]|
|.NET Framework API の定義へ移動します。|.NET Framework API のカーソルの位置が、.NET Framework メタデータから生成されたコードを示します。|×|
|ユーザー定義の API の定義へ移動します。|エンティティが定義されているコード内の場所にカーソルを移動、定義したプログラム エンティティにカーソルがあるときです。|[はい]|
|[指定行へのジャンプ]|行番号を指定してファイルの特定の行に移動できます。|[はい]|
|ファイルの上部にあるナビゲーション バー|ジャンプするコードでは、場所、たとえば、関数名を有効にします。|[はい]|
|アウトライン 参照してください[アウトライン](/visualstudio/ide/outlining)です。|使用するよりコンパクトなビューを作成するコードのセクションを折りたたんだりできます。|[はい]|
|タブを設定します。|スペースをタブに変換します。|[はい]|
|型の色づけ|表示は、特別な色で型の名前を定義します。|[はい]|
|クイック検索します。 クイック検索 検索し、置換 ウィンドウを参照してください。|ファイルまたはプロジェクトで検索できます。|[はい]|

## <a name="intellisense-features"></a>IntelliSense 機能
次の表は、IntelliSense の機能サポートし、f# でサポートされていません。 IntelliSense の詳細については、次を参照してください。 [IntelliSense の使用](/visualstudio/ide/using-intellisense)です。

|機能|説明|F# でサポートされているか。|
|-------|-----------|----------------|
|インターフェイスを自動的に実装します。|インターフェイス メソッドのコード スタブを生成します。|×|
|コード スニペット|トピックには、一般的なコーディングのコンス トラクターのライブラリからコードを挿入します。|×|
|入力候補|単語や名前を入力すると完了することによって、入力を保存します。|[はい]|
|使用する最初の入力候補モード|有効な場合と入力すると、いずれかを選択するか押して待機しているのではなく、最初の一致を選択する単語補完**CTRL + SPACE**です。|×|
|コード要素を生成します。|使用すると、さまざまな構成要素のスタブ コードを生成できます。|×|
|リスト メンバー|メンバー アクセス演算子 (.) を入力すると、型のメンバーを示します。|[はい]|
|Using/オープンを整理します。|によって参照される名前空間を整理**を使用して**(C#) ステートメントまたは**開く**f# でのディレクティブ。|×|
|パラメーター ヒント|関数呼び出しを入力すると、パラメーターに関する有用な情報を示します。|[はい]|
|クイック ヒント|コード内の識別子の完全な宣言を表示します。|[はい]|
Visual Studio 2012 で f# コードのリファクタリングはサポートされていません。

## <a name="debugging-features"></a>デバッグ機能
次の表では、f# コードをデバッグするときに使用できる機能を示します。 Visual Studio デバッガーの詳細については、次を参照してください。 [Visual Studio でデバッグ](https://msdn.microsoft.com/library/sc65sadd.aspx)です。

|機能|説明|F# でサポートされているか。|
|-------|-----------|----------------|
|[自動変数] ウィンドウ|自動または一時変数を示しています。|×|
|ブレークポイント|デバッグ中に特定の時点でコードが実行を一時停止できます。|[はい]|
|条件付きブレークポイント|実行を一時停止するかどうかを決定する条件をテストするブレークポイントを有効にします。|[はい]|
|エディット コンティニュ|コードを変更し、停止してデバッガーを再起動することがなく実行中のプログラムをデバッグする際のコンパイルを有効にします。|×|
|式エバリュエーター|評価し、実行時にコードを実行します。|いいえ、できませんが、c# の式エバリュエーターは c# の構文を使用する必要がありますが、使用できます。|
|デバッグ履歴|使用すると、以前に実行されたコードにステップ インできます。|[はい]|
|[ローカル] ウィンドウ|ローカルでの表示には、値および変数が定義されています。|[はい]|
|カーソル行の前まで実行|カーソルを含む行に到達するまで、コードを実行できます。|[はい]|
|[ステップ イン]|使用すると、実行を進めるし、関数呼び出しに移動できます。|[はい]|
|[ステップ オーバー]|使用すると、現在のスタック フレームで実行を進めるし、関数呼び出しの直後に移動できます。|[はい]|

## <a name="additional-tools"></a>その他のツール
次の表は、Visual Studio ツールでは、f# のサポートをまとめたものです。

|ツール|説明|F# でサポートされているか。|
|----|-----------|----------------|
|呼び出し階層|コードで関数の入れ子になった構造体の呼び出しを表示します。|×|
|コード メトリックス|行の数など、コードに関する情報を収集します。|×|
|クラス ビュー|プロジェクト内のコードの種類ベースのビューを提供します。|×|
|[[エラー一覧] ウィンドウ](/visualstudio/ide/reference/error-list-window)|コードでは、エラーの一覧を示します。|[はい]|
|[F# Interactive](../tutorials/fsharp-interactive/index.md)|入力 (またはコピーして貼り付ける) f# コードおよびプロジェクトのビルドとは無関係に、すぐに実行できるようにします。 F# Interactive ウィンドウは、読み取り、Evaluate、Print ループ (REPL) です。|[はい]|
|オブジェクト ブラウザー|使用すると、アセンブリ内の型を表示できます。|F# の型コンパイル済みアセンブリに表示されるとおりに表示されない正確にそれらを作成します。 F# の型のコンパイル済み表現を参照することができますが、F# から表示される種類を表示することはできません。|
|[[出力] ウィンドウ](/visualstudio/ide/reference/output-window)|ビルド出力を表示します。|[はい]|
|パフォーマンスの分析|コードのパフォーマンスを測定するためのツールを提供します。|[はい]|
|[プロパティ] ウィンドウ|表示し、フォーカスのある開発環境でオブジェクトのプロパティの編集を有効にします。|[はい]|
|[サーバー エクスプ ローラー](https://msdn.microsoft.com/library/x603htbk.aspx)|さまざまなサーバー リソースと対話する方法を提供します。|[はい]|
|ソリューション エクスプローラー|プロジェクトとファイルを表示および管理できます。|[はい]|
|タスク一覧|コードに関連する作業項目を管理できます。|[はい]|
|テスト プロジェクト|コードをテストできるようにする機能を提供します。|×|
|ツールボックス|コントロールとテキストまたはコードのセクションなどのドラッグ可能なオブジェクトが含まれているタブを表示します。|[はい]|

## <a name="see-also"></a>関連項目
 [F# では、Visual Studio での概要します。](../get-started/get-started-visual-studio.md)  
 [プロジェクトの構成](configuring-projects.md)  
