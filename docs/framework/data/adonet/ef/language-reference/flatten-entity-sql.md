---
title: FLATTEN (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 1a670c63-0a29-4738-80e6-101f66af05c3
ms.openlocfilehash: 84b846e3db86c664bc42363f3d983a1001f5c318
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833809"
---
# <a name="flatten-entity-sql"></a>FLATTEN (Entity SQL)
将一个由多个集合组成的集合转换为一个平展集合。 新集合与旧集合包含所有相同的元素，但没有嵌套结构。  
  
## <a name="syntax"></a>语法  
  
```sql  
FLATTEN ( collection )  
```  
  
## <a name="arguments"></a>参数  
 `collection`  
 任何有效的表达式，该表达式返回一个由值集合组成的集合以平展为单个集合。  
  
## <a name="remarks"></a>备注  
 `FLATTEN` 是 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 集运算符之一。 所有 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 集运算符都是从左到右进行求值。 请参阅除 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 集运算符的优先级信息[外](except-entity-sql.md)。  
  
## <a name="example"></a>示例  
 以下 Entity SQL 查询使用 `FLATTEN` 运算符以将一个由多个集合组成的集合转换为一个平展集合。 若要编译并运行此查询，请执行下列步骤：  
  
1. 按照 [How 中的过程执行以下操作：执行返回 StructuralType Results @ no__t-0 的查询。  
  
2. 将以下查询作为参数传递给 `ExecuteStructuralTypeQuery` 方法：  
  
 [!code-sql[DP EntityServices Concepts#FLATTEN](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#flatten)]  
  
## <a name="see-also"></a>请参阅

- [实体 SQL 引用](entity-sql-reference.md)
