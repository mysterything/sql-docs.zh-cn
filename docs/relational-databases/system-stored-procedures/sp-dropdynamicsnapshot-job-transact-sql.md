---
title: sp_dropdynamicsnapshot_job (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropdynamicsnapshot_job_TSQL
- sp_dropdynamicsnapshot_job
helpviewer_keywords:
- sp_dropdynamicsnapshot_job
ms.assetid: 128e428a-01b3-4062-8c6e-d22d5fa268a9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e4612c7b20e448eecbd6c83a3d09d0796dcff542
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54126252"
---
# <a name="spdropdynamicsnapshotjob-transact-sql"></a>sp_dropdynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为具有参数化行筛选器的发布删除筛选的数据快照作业。 在发布服务器上对发布数据库执行此存储的过程。 删除作业时，所有相关数据将被删除从[MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md)系统表。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_dropdynamicsnapshot_job [ @publication = ] 'publication'   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]   
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]   
    [ , [ @ignore_distributor =] ignore_distributor ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publication=**] **'**_发布_  
 要从中删除筛选数据快照作业的发布的名称。 *发布*是**sysname**，无默认值。  
  
 [ **@dynamic_snapshot_jobname**=] **'**_dynamic_snapshot_jobname_  
 要删除的筛选数据快照作业的名称。 *dynamic_snapshot_jobname*数据类型为 sysname，并提供的默认设置，如果任意作业名称与相关联*dynamic_snapshot_jobid*。  
  
 [ **@dynamic_snapshot_jobid**=] **'**_dynamic_snapshot_jobid_  
 要删除的筛选数据快照作业的标识符。 *dynamic_snapshot_jobid*是**uniqueidentifier**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  仅*dynamic_snapshot_jobid*或*dynamic_snapshot_jobname*可以指定。 如果值未提供*dynamic_snapshot_jobid*或*dynamic_snapshot_jobname*，删除发布的所有动态快照作业。  
  
 [  **@ignore_distributor =**] *ignore_distributor*  
 *ignore_distributor*是**位**，默认值为**0**。 该参数可用于删除动态快照作业但不清除分发服务器上的任务。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_dropdynamicsnapshot**合并复制中使用。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_dropdynamicsnapshot**。  
  
## <a name="see-also"></a>请参阅  
 [sp_adddynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md)  
  
  
