---
title: IHpublishercolumnindexes (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishercolumnindexes
- IHpublishercolumnindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumnindexes system table
ms.assetid: 95b95a1d-b502-4838-825f-82a456487e25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 70fce3c0c919a9d898e0dadf9d56e5ae5adaa0a7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52802479"
---
# <a name="ihpublishercolumnindexes-transact-sql"></a>IHpublishercolumnindexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublishercolumnindexes**系统表中的非 SQL Server 发布的列映射[IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md)系统表中的索引为[IHpublisherindexes](../../relational-databases/system-tables/ihpublisherindexes-transact-sql.md)系统表。 此表存储在分发数据库中。  
  
## <a name="definition"></a>定义  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|标识从列[IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md)使用关联索引。|  
|**publisherindex_id**|**int**|标识的索引[IHpublisherindexes](../../relational-databases/system-tables/ihpublisherindexes-transact-sql.md)与列关联的表。|  
|**indid**|**int**|指示列在已发布表中的位置。|  
  
## <a name="see-also"></a>请参阅  
 [异类数据库复制](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
