---
title: 分离数据库 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.detachdatabase.f1
helpviewer_keywords:
- database detaching [SQL Server]
- detaching databases [SQL Server]
ms.assetid: f63d4107-13e4-4bfe-922d-5e4f712e472d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 050220781f484b4a9e595551496d7e58c06f954c
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54134637"
---
# <a name="detach-a-database"></a>分离数据库
  本主题介绍如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中分离数据库。 分离的文件将会予以保留，并且可以使用带有 FOR ATTACH 或 FOR ATTACH_REBUILD_LOG 选项的 CREATE DATABASE 重新附加它们。 这些文件可以移动并附加到其他服务器上。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要分离数据库，可使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
 有关限制和局限的列表，请参阅 [数据库分离和附加 (SQL Server)](database-detach-and-attach-sql-server.md)中分离数据库。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 要求具有 db_owner 固定数据库角色中的成员资格。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-detach-a-database"></a>分离数据库  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 对象资源管理器中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的实例，然后展开该实例。  
  
2.  展开 **“数据库”**，并选择要分离的用户数据库的名称。  
  
3.  右键单击数据库名称，指向“任务”，再单击“分离”。 将出现 **“分离数据库”** 对话框。  
  
     **要分离的数据库**  
     列出要分离的数据库。  
  
     **Database Name**  
     显示要分离的数据库的名称。  
  
     **删除连接**  
     断开与指定数据库的连接。  
  
    > [!NOTE]  
    >  不能分离连接为活动状态的数据库。  
  
     **更新统计信息**  
     默认情况下，分离操作将在分离数据库时保留过期的优化统计信息；若要更新现有的优化统计信息，请单击此复选框。  
  
     **保留全文目录**  
     默认情况下，分离操作保留所有与数据库关联的全文目录。 若要删除全文目录，请清除 **“保留全文目录”** 复选框。 只有从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]升级数据库时，才会显示此选项。  
  
     **“状态”**  
     显示以下状态之一：**准备好**或**未就绪**。  
  
     **Message**  
     **“消息”** 列可显示关于数据库的如下信息：  
  
    -   当数据库进行了复制操作，则 **“状态”** 为 **“未就绪”** ， **“消息”** 列将显示 **“已复制数据库”**。  
  
    -   当数据库有一个或多个活动连接，**状态**是**未就绪**并**消息**列将显示 _< number_of_active_connections>_**个活动连接**-例如：**1 个活动连接**。 在分离数据库之前，需要通过选择 **“删除连接”** 断开所有活动连接。  
  
     若要获取有关消息的详细信息，请单击相应的超链接文本打开活动监视器。  
  
4.  分离数据库准备就绪后，请单击 **“确定”**。  
  
> [!NOTE]  
>  新分离的数据库将一直显示在对象资源管理器的 **“数据库”** 节点中，直到刷新该视图。 你可以刷新在任何时间视图：单击对象资源管理器窗格中，然后从菜单栏中选择**视图**，然后**刷新**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-detach-a-database"></a>分离数据库  
  
1.  连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例将分离 AdventureWorks2012 数据库，同时将 skipchecks 设置为 true。  
  
```  
EXEC sp_detach_db 'AdventureWorks2012', 'true';  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库分离和附加 (SQL Server)](database-detach-and-attach-sql-server.md)   
 [sp_detach_db (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-detach-db-transact-sql)  
  
  
