---
title: ICorDebugProcess5::EnableNGENPolicy メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcess5::EnableNGenPolicy
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess5::EnableNGENPolicy
helpviewer_keywords:
- ICorDebugProcess5::EnableNGENPolicy method [.NET Framework debugging]
- EnableNGENPolicy method, ICorDebugProcess5 interface [.NET Framework debugging]
ms.assetid: 3b8e15ca-3c72-4685-a937-da4c739cb9e9
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c598491acd27223a8a41234ddf2c6b8e6f005d52
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="icordebugprocess5enablengenpolicy-method"></a>ICorDebugProcess5::EnableNGENPolicy メソッド
アプリケーションがマネージ デバッガーで実行中にネイティブ イメージを読み込む方法を決定する値を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT EnableNGENPolicy(  
    [in] CorDebugNGENPolicy ePolicy  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ePolicy`  
 [in]A [CorDebugNGenPolicy](../../../../docs/framework/unmanaged-api/debugging/cordebugngenpolicy-enumeration.md)アプリケーションがマネージ デバッガーで実行中にネイティブ イメージを読み込む方法を決定する定数。  
  
## <a name="remarks"></a>コメント  
 メソッドを返しますのかどうか、ポリシーは正常に設定、`S_OK`です。 場合`ePolicy`によって定義された列挙値の範囲外である[CorDebugNGenPolicy](../../../../docs/framework/unmanaged-api/debugging/cordebugngenpolicy-enumeration.md)、メソッドを返します`E_INVALIDARG`メソッドの呼び出しには影響しません。 ネイティブ イメージ ジェネレーター (Ngen.exe) のポリシーを更新できないかどうか、メソッドを返します`E_FAIL`です。  
  
 `ICorDebugProcess5::EnableNGenPolicy`メソッドは、プロセスの有効期間中にいつでも呼び出すことができます。 ポリシーは有効で、ポリシーを設定した後に読み込まれる任意のモジュールです。  
  
## <a name="requirements"></a>要件  
 **プラットフォーム:** を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET framework のバージョン:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目  
 [ICorDebugProcess5 インターフェイス](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-interface.md)  
 [デバッグ インターフェイス](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)  
 [デバッグ](../../../../docs/framework/unmanaged-api/debugging/index.md)
