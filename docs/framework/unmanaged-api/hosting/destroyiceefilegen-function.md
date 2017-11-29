---
title: "DestroyICeeFileGen 関数"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: DestroyICeeFileGen
api_location:
- mscoree.dll
- mscorpehost.dll
- mscorpe.dll
api_type: COM
f1_keywords: DestroyICeeFileGen
helpviewer_keywords: DestroyICeeFileGen function [.NET Framework hosting]
ms.assetid: dc1e2235-e721-4cb2-a0b8-6b0c030d7bab
topic_type: apiref
caps.latest.revision: "17"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 11f0bd03532668196f85713459fe103f9120c82e
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2017
---
# <a name="destroyiceefilegen-function"></a><span data-ttu-id="29b71-102">DestroyICeeFileGen 関数</span><span class="sxs-lookup"><span data-stu-id="29b71-102">DestroyICeeFileGen Function</span></span>
<span data-ttu-id="29b71-103">破棄、 [ICeeFileGen](../../../../docs/framework/unmanaged-api/hosting/iceefilegen-class.md)オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="29b71-103">Destroys an [ICeeFileGen](../../../../docs/framework/unmanaged-api/hosting/iceefilegen-class.md) object.</span></span>  
  
 <span data-ttu-id="29b71-104">この関数は、[!INCLUDE[net_v40_long](../../../../includes/net-v40-long-md.md)] では推奨されていません。</span><span class="sxs-lookup"><span data-stu-id="29b71-104">This function has been deprecated in the [!INCLUDE[net_v40_long](../../../../includes/net-v40-long-md.md)].</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="29b71-105">構文</span><span class="sxs-lookup"><span data-stu-id="29b71-105">Syntax</span></span>  
  
```  
HRESULT DestroyICeeFileGen (  
    [in] ICeeFileGen  **ceeFileGen  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="29b71-106">パラメーター</span><span class="sxs-lookup"><span data-stu-id="29b71-106">Parameters</span></span>  
 `ceeFileGen`  
 <span data-ttu-id="29b71-107">[in]`ICeeFileGen`オブジェクトを破棄します。</span><span class="sxs-lookup"><span data-stu-id="29b71-107">[in] The `ICeeFileGen` object to destroy.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="29b71-108">戻り値</span><span class="sxs-lookup"><span data-stu-id="29b71-108">Return Value</span></span>  
 <span data-ttu-id="29b71-109">このメソッドは、標準の COM エラー コードを返します。</span><span class="sxs-lookup"><span data-stu-id="29b71-109">This method returns standard COM error codes.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="29b71-110">コメント</span><span class="sxs-lookup"><span data-stu-id="29b71-110">Remarks</span></span>  
 <span data-ttu-id="29b71-111">`DestroyICeeFileGen`破棄、`ICeeFileGen`によって作成されたオブジェクト、 [CreateICeeFileGen](../../../../docs/framework/unmanaged-api/hosting/createiceefilegen-function.md)関数。</span><span class="sxs-lookup"><span data-stu-id="29b71-111">`DestroyICeeFileGen` destroys the `ICeeFileGen` object created by the [CreateICeeFileGen](../../../../docs/framework/unmanaged-api/hosting/createiceefilegen-function.md) function.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="29b71-112">要件</span><span class="sxs-lookup"><span data-stu-id="29b71-112">Requirements</span></span>  
 <span data-ttu-id="29b71-113">**プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。</span><span class="sxs-lookup"><span data-stu-id="29b71-113">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="29b71-114">**ヘッダー:** ICeeFileGen.h</span><span class="sxs-lookup"><span data-stu-id="29b71-114">**Header:** ICeeFileGen.h</span></span>  
  
 <span data-ttu-id="29b71-115">**ライブラリ:** MSCorPE.dll</span><span class="sxs-lookup"><span data-stu-id="29b71-115">**Library:** MSCorPE.dll</span></span>  
  
 <span data-ttu-id="29b71-116">**.NET framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="29b71-116">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="29b71-117">関連項目</span><span class="sxs-lookup"><span data-stu-id="29b71-117">See Also</span></span>  
 [<span data-ttu-id="29b71-118">推奨されなくなった CLR ホスト関数</span><span class="sxs-lookup"><span data-stu-id="29b71-118">Deprecated CLR Hosting Functions</span></span>](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)