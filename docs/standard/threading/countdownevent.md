---
title: CountdownEvent
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- synchronization primitives, CountdownEvent
ms.assetid: eec3812a-e20f-4ecd-bfef-6921d508b708
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f98e2388cb31e62d974c8b0bae0bdf833f5963a5
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="countdownevent"></a>CountdownEvent
<xref:System.Threading.CountdownEvent?displayProperty=nameWithType> は同期プリミティブであり、特定の回数シグナル状態になった後、待機スレッドのブロックを解除します。 <xref:System.Threading.CountdownEvent> は、通常は <xref:System.Threading.ManualResetEvent> または <xref:System.Threading.ManualResetEventSlim> を使用して、イベントをシグナル化する前に変数を手動でデクリメントする必要があるシナリオ用に設計されています。 たとえば、fork/join シナリオでは、単にシグナル数 5 の <xref:System.Threading.CountdownEvent> を作成し、スレッド プールで 5 つの作業項目を開始し、完了時に各作業項目呼び出し <xref:System.Threading.CountdownEvent.Signal%2A> を使用できます。 <xref:System.Threading.CountdownEvent.Signal%2A> を呼び出すたびに、シグナル数が 1 だけデクリメントします。 メイン スレッドでは、シグナル数がゼロになるまで、<xref:System.Threading.CountdownEvent.Wait%2A> の呼び出しがブロックされます。  
  
> [!NOTE]
>  レガシ .NET Framework の同期 API と対話する必要がないコードの場合は、fork と join の並列実行をさらに簡単に表すために <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> オブジェクトまたは <xref:System.Threading.Tasks.Parallel.Invoke%2A> メソッドの使用を検討してください。  
  
 <xref:System.Threading.CountdownEvent> には以下の追加機能があります。  
  
-   取り消しトークンを使用して、待機操作を取り消すことができます。  
  
-   インスタンスの作成後に、シグナル数をインクリメントできます。  
  
-   <xref:System.Threading.CountdownEvent.Reset%2A> メソッドを呼び出すことで <xref:System.Threading.CountdownEvent.Wait%2A> が返された後、インスタンスを再利用できます。  
  
-   インスタンスは、<xref:System.Threading.WaitHandle.WaitAll%2A> などの他の .NET Framework の同期 API との統合のために <xref:System.Threading.WaitHandle> を公開します。  
  
## <a name="basic-usage"></a>基本的な使用方法  
 <xref:System.Threading.CountdownEvent> と <xref:System.Threading.ThreadPool> 作業項目を使用する方法を次の例に示します。  
  
 [!code-csharp[CDS_CountdownEvent#01](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_countdownevent/cs/countdownevent.cs#01)]
 [!code-vb[CDS_CountdownEvent#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_countdownevent/vb/module1.vb#01)]  
  
## <a name="countdownevent-with-cancellation"></a>CountdownEvent と Cancellation  
 次の例は、取り消しトークンを使用して、<xref:System.Threading.CountdownEvent> での待機操作を取り消す方法を示しています。 基本的なパターンでは、[!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] で導入された、統合取り消しのモデルに従います。 詳細については、「[マネージ スレッドのキャンセル](../../../docs/standard/threading/cancellation-in-managed-threads.md)」を参照してください。  
  
 [!code-csharp[CDS_CountdownEvent#02](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_countdownevent/cs/countdownevent.cs#02)]
 [!code-vb[CDS_CountdownEvent#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_countdownevent/vb/canceleventwait.vb#02)]  
  
 待機操作では、それをシグナル化するスレッドが取り消されないことに注意してください。 通常、取り消しは論理操作に適用され、待機が同期中のすべての作業項目だけでなく、イベントでの待機を含めることができます。 この例では、各作業項目には同じ取り消しトークンのコピーが渡されるため、取り消し要求に応答することができます。  
  
## <a name="see-also"></a>参照  
 [EventWaitHandle、AutoResetEvent、CountdownEvent、ManualResetEvent](../../../docs/standard/threading/eventwaithandle-autoresetevent-countdownevent-manualresetevent.md)
