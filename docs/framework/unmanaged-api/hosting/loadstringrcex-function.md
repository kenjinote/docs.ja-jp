---
title: LoadStringRCEx 関数
ms.date: 03/30/2017
api_name:
- LoadStringRCEx
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- LoadStringRCEx
helpviewer_keywords:
- LoadStringRCEx function [.NET Framework hosting]
ms.assetid: bc789636-ca14-4f07-8f77-9305874d7495
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 38c942b9a94c83f5a3316cf3ae3ccbbad2b0ec69
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="loadstringrcex-function"></a>LoadStringRCEx 関数
HRESULT 値を、指定したカルチャの適切なエラー メッセージに変換します。  
  
 この関数は、[!INCLUDE[net_v40_long](../../../../includes/net-v40-long-md.md)] では非推奨とされました。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT LoadStringRCEx (  
    [in]  LCID    lcid,   
    [in]  UINT    iResouceID,   
    [out] LPWSTR  szBuffer,   
    [in]  int     iMax,   
    [in]  int     bQuiet,   
    [out] int    *pcwchUsed  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `lcid`  
 [in]カルチャ識別子です。 場合、-1 を渡します`lcid`の既定のカルチャを使用します。  
  
 `iResourceID`  
 [in]HRESULT。  
  
 `szBuffer`  
 [out]正常完了時にエラー メッセージを格納するバッファー。  
  
 `iMax`  
 [in]エラー メッセージ バッファーのサイズ。  
  
 `bQuiet`  
 [in]無視されます。  
  
 `pcwchUsed`  
 [out]エラー メッセージの長さへのポインター。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは、次の値に加え、WinError.h で定義されている標準の COM エラー コードを返します。  
  
|リターン コード|説明|  
|-----------------|-----------------|  
|S_OK|メソッドは正常に完了しました。|  
|E_INVALIDARG|`szBuffer` null、または`iMax`はゼロ (0) です。|  
  
## <a name="remarks"></a>コメント  
 メソッドが正常に完了しない場合`szBuffer`空の文字列が含まれています。  
  
## <a name="requirements"></a>要件  
 **プラットフォーム:** を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。  
  
 **ヘッダー:** MSCorEE.h  
  
 **ライブラリ:** MSCorEE.dll  
  
 **.NET framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Globalization.CultureInfo.LCID%2A?displayProperty=nameWithType>  
 [LoadStringRC 関数](../../../../docs/framework/unmanaged-api/hosting/loadstringrc-function.md)  
 
  [非推奨の CLR ホスト関数](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
