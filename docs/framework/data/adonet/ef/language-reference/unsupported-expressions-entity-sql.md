---
title: サポートされていない式 (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 5e79da7e-e78a-413c-8fb0-f3f9cd84f579
dev_langs:
- sql
ms.openlocfilehash: bf20bb92010d5031e973cb1cc004b6b8f13d0091
ms.sourcegitcommit: 22c3c8f74eaa138dbbbb02eb7d720fce87fc30a9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2018
---
# <a name="unsupported-expressions"></a>サポートされていない式

このトピックでは、[!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] でサポートされていない [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 式について説明します。 詳細については、次を参照してください。[エンティティの SQL と TRANSACT-SQL の異なる](../../../../../../docs/framework/data/adonet/ef/language-reference/how-entity-sql-differs-from-transact-sql.md)です。

## <a name="quantified-predicates"></a>定量化された述語

[!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] では、次の形式のコンストラクターを使用できます。

```sql
sal > all (select salary from employees)
sal > any (select salary from employees)
```

ただし、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、このようなコンストラクターがサポートされていません。 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] では、これに相当する式を次のように記述できます。

```sql
not exists(select 0 from employees as e where sal <= e.salary)
exists(select 0 from employees as e where sal > e.salary)
```

## <a name="-operator"></a>* 演算子

[!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] では、すべての列を投影する必要があることを示すために、SELECT 句で * 演算子を使用できます。これは [!INCLUDE[esql](../../../../../../includes/esql-md.md)] でサポートされていません。

## <a name="see-also"></a>関連項目

[Entity SQL の概要](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)  
[Entity SQL と Transact-SQL の相違点](../../../../../../docs/framework/data/adonet/ef/language-reference/how-entity-sql-differs-from-transact-sql.md)  
