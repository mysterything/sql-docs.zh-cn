---
title: sysmergesubscriptions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergesubscriptions_TSQL
- sysmergesubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergesubscriptions system table
ms.assetid: 6adc78da-991d-4c08-98c3-ecb4762e0e99
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: baea56d983ac1c2fff9016d1a385c8b4d918fb7a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52802789"
---
# <a name="sysmergesubscriptions-transact-sql"></a>sysmergesubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  每个已知订阅服务器在表中对应一行，并且该表是发布服务器的本地表。 此表存储在发布和订阅数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|subscriber_server|**sysname**|服务器的 ID。 将订阅数据库的复本迁移到其他服务器时，用于将 srvid 字段映射到服务器特定的值。|  
|db_name|**sysname**|对订阅数据库的名称。|  
|pubid|**uniqueidentifier**|从中创建当前订阅的发布 ID。|  
|datasource_type|**int**|数据源的类型：<br /><br /> **0** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> **2** = jet OLE DB。|  
|subid|**uniqueidentifier**|订阅的唯一标识号。|  
|replnickname|**binary**|复制的压缩别名。|  
|replicastate|**uniqueidentifier**|一个唯一标识符，它通过将发布服务器中的值与订阅服务器中的值进行比较来确定以前的同步是否成功。|  
|status|**tinyint**|订阅的状态：<br /><br /> **0** = 非活动状态。<br /><br /> **1** = 活动。<br /><br /> **2** = 已删除。|  
|subscriber_type|**int**|订阅服务器的类型：<br /><br /> **1** = 全局。<br /><br /> **2** = 本地。<br /><br /> **3** = 匿名。|  
|subscription_type|**int**|订阅的类型：<br /><br /> **0** = 推送。<br /><br /> **1** = 请求。<br /><br /> **2** = 匿名。|  
|sync_type|**tinyint**|同步类型：<br /><br /> **1** = automatic。<br /><br /> **2** = 不同步。|  
|description|**nvarchar(255)**|对订阅的简短说明。|  
|priority|**real**|指定订阅优先级并允许实现基于优先级的冲突解决。 等于**0.00**的所有本地或匿名订阅。|  
|recgen|**bigint**|上次接收的生成的编号。|  
|recguid|**uniqueidentifier**|上次接收的生成的唯一 ID。|  
|sentgen|**bigint**|上次发送的生成的编号。|  
|sentguid|**uniqueidentifier**|上次发送的生成的唯一 ID。|  
|schemaversion|**int**|上次接收的架构的编号。|  
|schemaguid|**uniqueidentifier**|上次接收的架构的唯一 ID。|  
|last_validated|**datetime**|**Datetime**的上次成功验证的订阅者数据。|  
|attempted_validate|**datetime**|上次**datetime**尝试验证的订阅。|  
|last_sync_date|**datetime**|**Datetime**同步。|  
|last_sync_status|**int**|订阅状态：<br /><br /> **0** = 所有作业都在等待启动。<br /><br /> **1** = 一个或多个作业正在启动。<br /><br /> **2** = 所有作业都已成功执行。<br /><br /> **3** = 至少一个作业正在执行。<br /><br /> **4** = 所有作业计划和空闲。<br /><br /> **5** = 至少一个作业正在尝试在上一次失败后执行。<br /><br /> **6** = 至少一个作业无法成功执行。|  
|last_sync_summary|**sysname**|上一个同步结果的说明。|  
|metadatacleanuptime|**datetime**|上次**datetime**过期元数据已从合并复制系统表中删除。|  
|partition_id|**int**|标识订阅所属的预先计算的分区。|  
|cleanedup_unsent_changes|**bit**|标识已在订阅服务器上清除了未发送更改的元数据。|  
|replica_version|**int**|标识订阅所属的订阅服务器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本，可以为以下值之一：<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|supportability_mode|**int**|仅限内部使用。|  
|application_name|**nvarchar(128)**|仅限内部使用。|  
|subscriber_number|**int**|仅限内部使用。|  
|last_makegeneration_datetime|**datetime**|上次**datetime** makegeneration 进程为发布服务器上运行。 有关详细信息，请参阅中的-MakeGenerationInterval 参数[复制合并代理](../../relational-databases/replication/agents/replication-merge-agent.md)。|  
  
## <a name="see-also"></a>请参阅  
 [复制表 (Transact-SQL)](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
