---
title: CorDebugEHClause 構造体
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- CorDebugEHClause
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 0e350a1b-6997-46d0-bfc5-962a5011ef43
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 40820a805310786eeb0effd7c5284c1a70a6e70b
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="cordebugehclause-structure"></a>CorDebugEHClause 構造体
[.NET Framework 4.5.2 以降のバージョンでのみでサポート]  
  
 中間言語 (IL) コードの特定の部分の例外処理 (EH) 句を表しています。  
  
## <a name="syntax"></a>構文  
  
```cpp
typedef struct _CorDebugEHClause {  
   ULONG32 Flags;  
   ULONG32 TryOffset;  
   ULONG32 TryLength;  
   ULONG32 HandlerOffset;  
   ULONG32 HandlerLength;  
   ULONG32 ClassToken;  
   ULONG32 FilterOffset;  
} CorDebugEHClause;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|`Flags`|EH 句の例外情報について説明しているビット フィールド。 詳細については、「解説」を参照してください。|  
|`TryOffset`|メソッド本体の先頭からの `try` ブロックのオフセット (バイト単位)。|  
|`TryLength`|`try` ブロックの長さ (バイト単位)。|  
|`HandlerOffset`|この `try` ブロックのハンドラーの場所。|  
|`HandlerLength`|ハンドラー コードのサイズ (バイト単位)。|  
|`ClassToken`|型に基づく例外ハンドラーのメタデータ トークン。|  
|`FilterOffset`|フィルターに基づく例外ハンドラーのメソッド本体の先頭からのオフセット (バイト単位)。|  
  
## <a name="remarks"></a>コメント  
 配列`CoreDebugEHClause`によって値が返される、 [GetEHClauses](../../../../docs/framework/unmanaged-api/debugging/icordebugilcode-getehclauses-method.md)メソッドです。  
  
 EH 句の情報は CLI 仕様によって定義されます。 詳細については、次を参照してください。[標準の ECMA-355: 共通言語基盤 (CLI), 6 Edition](http://www.ecma-international.org/publications/standards/Ecma-335.htm)です。  
  
 `flags` フィールドには、次のフラグを含めることができます。 これらは、CorDebug.idl または CorDebug.h に定義されていないことに注意してください。  
  
|フラグ|値|説明|  
|----------|-----------|-----------------|  
|`COR_ILEXCEPTION_CLAUSE_EXCEPTION`|0x00000000|入力された例外句。|  
|`COR_ILEXCEPTION_CLAUSE_FILTER`|0x00000001|例外フィルターおよびハンドラー句。|  
|`COR_ILEXCEPTION_CLAUSE_FINALLY`|0x00000002|`finally` 句。|  
|`COR_ILEXCEPTION_CLAUSE_FAULT`|0x00000004|fault 句 (例外がスローされた場合にのみ `finally` 句が呼び出される)。|  
  
## <a name="requirements"></a>要件  
 **プラットフォーム:** を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET framework のバージョン:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>関連項目  
 [GetEHClauses メソッド](../../../../docs/framework/unmanaged-api/debugging/icordebugilcode-getehclauses-method.md)  
 [デバッグ構造体](../../../../docs/framework/unmanaged-api/debugging/debugging-structures.md)
