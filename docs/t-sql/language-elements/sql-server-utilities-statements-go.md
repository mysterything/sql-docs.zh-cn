---
title: "转到 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
f1_keywords:
- GO
- GO_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- batches [SQL Server], ending
- ending batches [SQL Server]
- GO command
ms.assetid: b2ca6791-3a07-4209-ba8e-2248a92dd738
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 17b78d6ca719088ade9d54db73b8ee10ef8072a5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="sql-server-utilities-statements---go"></a>SQL Server 实用工具语句-转到
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供了命令不[!INCLUDE[tsql](../../includes/tsql-md.md)]语句，但识别**sqlcmd**和**osql**实用程序和[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]代码编辑器。 这些命令可用于提高批处理和脚本的可读性和执行效率。  
  
  转到表示一批的结束[!INCLUDE[tsql](../../includes/tsql-md.md)]向语句[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实用程序。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
GO [count]  
```  
  
## <a name="arguments"></a>参数  
 *计数*  
 为一个正整数。 GO 之前的批处理将执行指定的次数。  
  
## <a name="remarks"></a>注释  
 转到不是[!INCLUDE[tsql](../../includes/tsql-md.md)]语句; 它识别命令**sqlcmd**和**osql**实用程序和[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]代码编辑器。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具将 GO 解释为应该向 [!INCLUDE[tsql](../../includes/tsql-md.md)] 实例发送当前批 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语句的信号。 当前批语句由上一 GO 命令后输入的所有语句组成，如果是第一条 GO 命令，则由即席会话或脚本开始后输入的所有语句组成。  
  
 GO 命令和 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句不能在同一行中。 但在 GO 命令行中可包含注释。  
  
 用户必须遵照使用批处理的规则。 例如，在批处理中的第一条语句后执行任何存储过程必须包含 EXECUTE 关键字。 局部（用户定义）变量的作用域限制在一个批处理中，不可在 GO 命令后引用。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyMsg VARCHAR(50)  
SELECT @MyMsg = 'Hello, World.'  
GO -- @MyMsg is not valid after this GO ends the batch.  
  
-- Yields an error because @MyMsg not declared in this batch.  
PRINT @MyMsg  
GO  
  
SELECT @@VERSION;  
-- Yields an error: Must be EXEC sp_who if not first statement in   
-- batch.  
sp_who  
GO  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 应用程序可以将多个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句作为一个批发送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例来执行。 然后，该批中的语句被编译成一个执行计划。 程序员在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中执行特殊语句，或生成 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的脚本在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中运行时，使用 GO 作为批结束的信号。  
  
 如果基于 ODBC 或 OLE DB API 的应用程序试图执行 GO 命令，会收到语法错误。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具从不向服务器发送 GO 命令。  
  
 不要将分号用作 GO 后的语句终止符。  
  
## <a name="permissions"></a>Permissions  
 GO 是一个不需任何权限的实用工具命令。 它可以由任何用户执行。  
  
```  
-- Yields an error because ; is not permitted after GO  
SELECT @@VERSION;  
GO;  
```  
  
## <a name="examples"></a>示例  
 以下示例创建两个批。 第一批包含仅`USE``AdventureWorks2012`语句将数据库上下文设置。 其余的语句使用局部变量。 因此，所有局部变量声明必须组成一个批。 为此，必须在最后一条引用此变量的语句之后才使用 `GO` 命令。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @NmbrPeople int  
SELECT @NmbrPeople = COUNT(*)  
FROM Person.Person;  
PRINT 'The number of people as of ' +  
      CAST(GETDATE() AS char(20)) + ' is ' +  
      CAST(@NmbrPeople AS char (10));  
GO  
```  
  
 下面的示例执行了批处理中的语句两次。  
  
```  
SELECT DB_NAME();  
SELECT USER_NAME();  
GO 2  
```  
  
  
