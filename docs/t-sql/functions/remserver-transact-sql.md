---
title: "@@REMSERVER (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@REMSERVER'
- '@@REMSERVER_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], remote servers
- remote servers [SQL Server], logins
- '@@REMSERVER function'
ms.assetid: 0bb451a9-3866-4064-963d-b74a2f864049
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 23ae1a37bcc84561a0ccedf10b1bb0c6ee7b6b73
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="remserver-transact-sql"></a>@@REMSERVER (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] 请改用链接服务器和链接服务器存储过程。  
  
 返回远程 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库服务器在登录记录中显示的名称。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
@@REMSERVER  
```  
  
## <a name="return-types"></a>返回类型  
 **nvarchar （128)**  
  
## <a name="remarks"></a>注释  
 @@REMSERVER使存储的过程以检查运行该过程时数据库服务器的名称。  
  
## <a name="examples"></a>示例  
 以下示例将创建返回远程服务器名称的过程 `usp_CheckServer`。  
  
```  
CREATE PROCEDURE usp_CheckServer  
AS  
SELECT @@REMSERVER;  
```  
  
 以下存储过程是在本地服务器 `SEATTLE1` 上创建的。 用户登录到远程服务器 `LONDON2` 上，然后运行 `usp_CheckServer`。  
  
```  
EXEC SEATTLE1...usp_CheckServer;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------------  
LONDON2  
```  
  
## <a name="see-also"></a>另请参阅  
 [配置函数 (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [远程服务器](../../database-engine/configure-windows/remote-servers.md)  
  
  