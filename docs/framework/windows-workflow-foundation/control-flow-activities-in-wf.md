---
title: WF 内の制御フロー アクティビティ
ms.date: 03/30/2017
ms.assetid: 6892885b-f7c5-4aea-8f5e-28863fb4ae75
ms.openlocfilehash: bcbb12210af2d0172977dca6f81355031baa043a
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
---
# <a name="control-flow-activities-in-wf"></a>WF 内の制御フロー アクティビティ
[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] には、ワークフロー内の実行フローを制御するアクティビティがいくつか用意されています。 これらのアクティビティの一部 (など`Switch`と`If`) Visual c# などの他の環境、プログラミングのようなフロー制御構造を実装する (など`Pick`) 新しいプログラミング構造をモデル化します。  
  
 `Parallel` や `ParallelForEach` などのアクティビティは、同時実行のために複数の子アクティビティをスケジュールできますが、シングル スレッドのみがワークフローに使用されます。 これらのアクティビティのそれぞれの子アクティビティは連続して実行され、連続するアクティビティは前のアクティビティが完了するかアイドルになるまで実行されません。 その結果、これらのアクティビティは、ブロック処理の可能性がある複数のアクティビティがインターリーブ形式で実行されるアプリケーションの場合に最も有効です。 これらのアクティビティにアイドルになる子アクティビティがない場合、`Parallel` アクティビティは `Sequence` アクティビティとまったく同様に実行され、`ParallelForEach` アクティビティは `ForEach` アクティビティとまったく同様に実行されます。 しかし、非同期アクティビティ (<xref:System.Activities.AsyncCodeActivity> から派生するアクティビティなど) またはメッセージング アクティビティが使用されると、子アクティビティがそのメッセージ受信を待っていても、または非同期作業を完了する必要があっても、コントロールは次の分岐にパスします。  
  
## <a name="flow-control-activities"></a>フロー制御アクティビティ  
  
|アクティビティ|説明|  
|--------------|-----------------|  
|<xref:System.Activities.Statements.DoWhile>|含まれるアクティビティを 1 回実行し、条件が `true` の間はその実行を続行します。|  
|<xref:System.Activities.Statements.ForEach%601>|コレクション内の要素ごとに埋め込みステートメントを順番に実行します。 <xref:System.Activities.Statements.ForEach%601> はキーワード `foreach` と似ていますが、言語ステートメントではなくアクティビティとして実装されます。|  
|<xref:System.Activities.Statements.If>|条件が `true` の場合は含まれるアクティビティを実行します。条件が <xref:System.Activities.Statements.If.Else%2A> の場合は `false` プロパティに含まれるアクティビティを実行できます。|  
|<xref:System.Activities.Statements.Parallel>|含まれるアクティビティを並列実行します。|  
|<xref:System.Activities.Statements.ParallelForEach%601>|コレクション内の要素ごとに埋め込みステートメントを並行実行します。|  
|<xref:System.Activities.Statements.Pick>|イベント ベースの制御フロー モデリングを提供します。|  
|<xref:System.Activities.Statements.PickBranch>|<xref:System.Activities.Statements.Pick> アクティビティ内の実行パスを表します。|  
|<xref:System.Activities.Statements.Sequence>|含まれるアクティビティを連続実行します。|  
|<xref:System.Activities.Statements.Switch%601>|指定された式の値に基づいて、実行する複数のアクティビティから 1 つを選択します。|  
|<xref:System.Activities.Statements.While>|条件が `true` である間は、含まれるアクティビティを実行します。|
