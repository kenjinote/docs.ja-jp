---
title: "ICorProfilerInfo::GetAssemblyInfo メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerInfo.GetAssemblyInfo
api_location: mscorwks.dll
api_type: COM
f1_keywords: GetAssemblyInfo Method
helpviewer_keywords:
- GetAssemblyInfo method [.NET Framework profiling]
- ICorProfilerInfo::GetAssemblyInfo method [.NET Framework profiling]
ms.assetid: 7a3c97c3-1e31-47b1-bf23-386785c509c4
topic_type: apiref
caps.latest.revision: "20"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: d4eab4a4bfbf91fd86a3742600f3383a8d374905
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="icorprofilerinfogetassemblyinfo-method"></a>ICorProfilerInfo::GetAssemblyInfo メソッド
アセンブリ ID を受け入れ、アセンブリの名前とアセンブリのマニフェスト モジュールの ID を返します。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT GetAssemblyInfo(  
    [in]  AssemblyID  assemblyId,  
    [in]  ULONG       cchName,  
    [out] ULONG       *pcchName,  
    [out, size_is(cchName), length_is(*pcchName)]  
          WCHAR       szName[] ,  
    [out] AppDomainID *pAppDomainId,  
    [out] ModuleID    *pModuleId);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `assemblyId`  
 [in] アセンブリの識別子。  
  
 `cchName`  
 [in] `szName` の長さ (文字数)。  
  
 `pcchName`  
 [out] アセンブリ名の文字列長の合計へのポインター。  
  
 `szName`  
 [out] 呼び出し元が提供したワイド文字バッファー。 関数が戻るときに、この関数の中にアセンブリ名が格納されます。  
  
 `pAppDomainId`  
 [out] アセンブリを含むアプリケーション ドメインの ID へのポインター。  
  
 `pModuleId`  
 [out] アセンブリのマニフェスト モジュールの ID へのポインター。  
  
## <a name="remarks"></a>コメント  
 このメソッドから制御が戻った後で、`szName` バッファーのサイズが十分で、アセンブリの完全名を格納できたかどうかを確認する必要があります。 これを行うには、`pcchName` が指している値を `cchName` パラメーターの値と比較します。 `pcchName` が指している値が `cchName` の値より大きい場合は、`szName` バッファーの割り当てを増やし、`cchName` を新しい大きいサイズに更新して、`GetAssemblyInfo` を再度呼び出します。  
  
 別の方法として、最初に `GetAssemblyInfo` を長さゼロの `szName` バッファーで呼び出して、適切なバッファーのサイズを取得します。 その後、バッファーのサイズを `pcchName` で返された値に基づいて調整し、`GetAssemblyInfo` を再度呼び出します。  
  
## <a name="requirements"></a>要件  
 **プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目  
 [ICorProfilerInfo インターフェイス](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)  
 [プロファイリングのインターフェイス](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)  
 [プロファイル](../../../../docs/framework/unmanaged-api/profiling/index.md)