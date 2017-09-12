---
title: "GOTO (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GOTO
- GOTO_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- skipping statements
- Transact-SQL statements, skipping
- labels [SQL Server]
- statements [SQL Server], skipping
- GOTO statement
ms.assetid: 589b6f8e-dc80-416f-9e74-48bed5337f58
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4c5614843f961d1ff3188ba1f3caa589d77c4735
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="goto-transact-sql"></a>GOTO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  将执行流更改到标签处。 跳过 GOTO 后面的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，并从标签位置继续处理。 GOTO 语句和标签可在过程、批处理或语句块中的任何位置使用。 GOTO 语句可嵌套使用。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
Define the label:   
label:   
Alter the execution:  
GOTO label   
```  
  
## <a name="arguments"></a>参数  
 *标签*  
 如果 GOTO 语句指向该标签，则其为处理的起点。 标签必须遵循的规则[标识符](../../relational-databases/databases/database-identifiers.md)。 无论是否使用 GOTO 语句，标签均可作为注释方法使用。  
  
## <a name="remarks"></a>注释  
 GOTO 可出现在条件控制流语句、语句块或过程中，但它不能跳转到该批以外的标签。 GOTO 分支可跳转到定义在 GOTO 之前或之后的标签。  
  
## <a name="permissions"></a>Permissions  
 GOTO 语句的权限默认情况下授予任何有效用户。  
  
## <a name="examples"></a>示例  
 以下示例显示如何将 `GOTO` 用作分支机制。  
  
```  
DECLARE @Counter int;  
SET @Counter = 1;  
WHILE @Counter < 10  
BEGIN   
    SELECT @Counter  
    SET @Counter = @Counter + 1  
    IF @Counter = 4 GOTO Branch_One --Jumps to the first branch.  
    IF @Counter = 5 GOTO Branch_Two  --This will never execute.  
END  
Branch_One:  
    SELECT 'Jumping To Branch One.'  
    GOTO Branch_Three; --This will prevent Branch_Two from executing.  
Branch_Two:  
    SELECT 'Jumping To Branch Two.'  
Branch_Three:  
    SELECT 'Jumping To Branch Three.';  
```  
  
## <a name="see-also"></a>另请参阅  
 [控制流语言 &#40;Transact SQL &#41;](~/t-sql/language-elements/control-of-flow.md)   
 [开始...结束 &#40;Transact SQL &#41;](../../t-sql/language-elements/begin-end-transact-sql.md)   
 [中断 &#40;Transact SQL &#41;](../../t-sql/language-elements/break-transact-sql.md)   
 [继续 &#40;Transact SQL &#41;](../../t-sql/language-elements/continue-transact-sql.md)   
 [如果...其他 &#40;Transact SQL &#41;](../../t-sql/language-elements/if-else-transact-sql.md)   
 [WAITFOR &#40;Transact SQL &#41;](../../t-sql/language-elements/waitfor-transact-sql.md)   
 [WHILE (Transact-SQL)](../../t-sql/language-elements/while-transact-sql.md)  
  
  
