---
title: "ICorDebugThread::EnumerateChains メソッド"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugThread.EnumerateChains
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugThread::EnumerateChains
helpviewer_keywords:
- EnumerateChains method [.NET Framework debugging]
- ICorDebugThread::EnumerateChains method [.NET Framework debugging]
ms.assetid: ec00bc21-117e-4acd-9301-2cfafd5be8d3
topic_type: apiref
caps.latest.revision: "13"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 67b5a5da0a0053536ab4331e9d134464a4330500
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugthreadenumeratechains-method"></a><span data-ttu-id="a650b-102">ICorDebugThread::EnumerateChains メソッド</span><span class="sxs-lookup"><span data-stu-id="a650b-102">ICorDebugThread::EnumerateChains Method</span></span>
<span data-ttu-id="a650b-103">この ICorDebugThread オブジェクト内のすべてのスタック チェーンを含む ICorDebugChainEnum 列挙子へのインターフェイス ポインターを取得します。</span><span class="sxs-lookup"><span data-stu-id="a650b-103">Gets an interface pointer to an ICorDebugChainEnum enumerator that contains all the stack chains in this ICorDebugThread object.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="a650b-104">構文</span><span class="sxs-lookup"><span data-stu-id="a650b-104">Syntax</span></span>  
  
```  
HRESULT EnumerateChains (  
    [out] ICorDebugChainEnum **ppChains  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="a650b-105">パラメーター</span><span class="sxs-lookup"><span data-stu-id="a650b-105">Parameters</span></span>  
 `ppChains`  
 <span data-ttu-id="a650b-106">[out]アドレスへのポインター、`ICorDebugChainEnum`このスレッドは、アクティブな (つまり、最も最近) チェーンの先頭でチェーンでつながってオブジェクトにより、すべてのスタックの列挙体です。</span><span class="sxs-lookup"><span data-stu-id="a650b-106">[out] A pointer to the address of an `ICorDebugChainEnum` object that allows enumeration of all the stack chains in this thread, starting at the active (that is, the most recent) chain.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="a650b-107">コメント</span><span class="sxs-lookup"><span data-stu-id="a650b-107">Remarks</span></span>  
 <span data-ttu-id="a650b-108">スタック チェーンでは、スレッドの物理呼び出し履歴を表します。</span><span class="sxs-lookup"><span data-stu-id="a650b-108">The stack chain represents the physical call stack for the thread.</span></span> <span data-ttu-id="a650b-109">次の状況では、スタック チェーンの境界を作成します。</span><span class="sxs-lookup"><span data-stu-id="a650b-109">The following circumstances create a stack chain boundary:</span></span>  
  
-   <span data-ttu-id="a650b-110">アンマネージ コードへマネージまたはアンマネージからマネージへの遷移です。</span><span class="sxs-lookup"><span data-stu-id="a650b-110">A managed-to-unmanaged or unmanaged-to-managed transition.</span></span>  
  
-   <span data-ttu-id="a650b-111">コンテキストの切り替え。</span><span class="sxs-lookup"><span data-stu-id="a650b-111">A context switch.</span></span>  
  
-   <span data-ttu-id="a650b-112">A デバッガーのユーザー スレッドのハイジャックです。</span><span class="sxs-lookup"><span data-stu-id="a650b-112">A debugger hijacking of a user thread.</span></span>  
  
 <span data-ttu-id="a650b-113">純粋なマネージ コードを 1 つのコンテキストで実行されているスレッドの簡単な例で、一対一の対応は、スレッドとスタック チェーンの間存在します。</span><span class="sxs-lookup"><span data-stu-id="a650b-113">In the simple case for a thread that is running purely managed code in a single context, a one-to-one correspondence will exist between threads and stack chains.</span></span>  
  
 <span data-ttu-id="a650b-114">デバッガーは、論理呼び出し履歴にすべてのスレッドの物理呼び出し履歴を再配置する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a650b-114">A debugger may want to rearrange the physical call stacks of all threads into logical call stacks.</span></span> <span data-ttu-id="a650b-115">これには、すべてのスレッドのチェーンの呼び出し元/呼び出し先の関係を順に並べ替えられ、それらが含まれます。</span><span class="sxs-lookup"><span data-stu-id="a650b-115">This would involve sorting all the threads' chains by their caller/callee relationships and regrouping them.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="a650b-116">要件</span><span class="sxs-lookup"><span data-stu-id="a650b-116">Requirements</span></span>  
 <span data-ttu-id="a650b-117">**プラットフォーム:**を参照してください[システム要件](../../../../docs/framework/get-started/system-requirements.md)です。</span><span class="sxs-lookup"><span data-stu-id="a650b-117">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="a650b-118">**ヘッダー:** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="a650b-118">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="a650b-119">**ライブラリ:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="a650b-119">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="a650b-120">**.NET framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="a650b-120">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>