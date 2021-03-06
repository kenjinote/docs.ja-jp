---
title: 秘密キー検索ツール (FindPrivateKey.exe)
ms.date: 09/11/2017
ms.assetid: b8846a95-3fcc-4e8c-b9c0-128d975a6307
ms.openlocfilehash: 8f156cbb2f4fad8d51e356bd4dee2d72d9397ffb
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="find-private-key-tool-findprivatekeyexe"></a>秘密キー検索ツール (FindPrivateKey.exe)

このコマンド ライン ツールを使用して、証明書ストアから秘密キーを取得できます。 たとえば、 *FindPrivateKey.exe*証明書ストアで特定の X.509 証明書に関連付けられている秘密キー ファイルの名前と場所の検索に使用できます。

> [!IMPORTANT]
> FindPrivateKey ツールは、WCF のサンプルとして付属しています。 サンプルの検索場所とそれをビルドする方法の詳細については、次を参照してください。 [FindPrivateKey](./samples/findprivatekey.md)です。

## <a name="syntax"></a>構文

```
FindPrivateKey<storeName> <storeLocation> [{ {-n <subjectName>} | {-t <thumbprint>} } [-f | -d | -a]]
```

## <a name="remarks"></a>コメント

次の表では、秘密キー検索ツール (FindPrivateKey.exe) で使用できる引数とオプションについて説明します。

|引数|説明|
|--------------|-----------------|
|`storeName`|証明書ストアの名前。|
|`storeLocation`|証明書ストアの場所。|

|オプション|説明|
|------------|-----------------|
|`/n <` *subjectName* `>`|証明書のサブジェクト名を指定します。|
|`/t <` *拇印* `>`|証明書のサムプリントを指定します。 Certmgr.exe を使用して証明書のサムプリントを取得します。|
|`/f`|ファイル名だけを出力します。|
|`/d`|ディレクトリだけを出力します。|
|`/a`|絶対ファイル名を出力します。|

## <a name="examples"></a>使用例

次のコマンドは、John Doe の秘密キーを取得します。

```
FindPrivateKey My CurrentUser -n "CN=John Doe"
```

次のコマンドは、ローカル コンピューター用の秘密キーを取得します。

```
FindPrivateKey My LocalMachine -t "03 33 98 63 d0 47 e7 48 71 33 62 64 76 5c 4c 9d 42 1d 6b 52" –a
```