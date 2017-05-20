---
title: "企业范围的自动化管理 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- enterprise automatic administration [SQL Server]
- multiserver administration [SQL Server]
- SQL Server Agent jobs, multiserver administration
- jobs [SQL Server Agent], multiserver administration
- master servers [SQL Server], about master servers
- target servers [SQL Server], about target servers
- master servers [SQL Server]
- multiple instances of SQL Server
- target servers [SQL Server]
ms.assetid: 44d8365b-42bd-4955-b5b2-74a8a9f4a75f
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 618e199812a39ec29e032f8371419ec6184c713f
ms.lasthandoff: 04/11/2017

---
# <a name="automated-administration-across-an-enterprise"></a>企业范围的自动化管理
跨多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 实例的自动化管理称为“多服务器管理”**。 使用多服务器管理可以执行下列操作：  
  
-   管理两台或多台服务器。  
  
-   在企业服务器之间安排数据仓库的信息流。  
  
若要利用多服务器管理，您必须至少有一台主服务器且至少有一台目标服务器。 主服务器将作业分发到目标服务器并从它那里接收事件。 主服务器还存储在目标服务器上运行的作业的作业定义的中央副本。 目标服务器定期连接到主服务器来更新它们的作业计划。 如果主服务器上存在新作业，目标服务器将下载该作业。 目标服务器在完成作业后，会重新连接到主服务器并报告作业状态。 请注意，执行任何活动相关的数据库时，作业定义必须相同。  
  
以下图例显示了主服务器与目标服务器之间的关系。  
  
![多服务器管理配置](../../ssms/agent/media/multisvr.gif "多服务器管理配置")  
  
如果管理大公司内的部门服务器，则可以定义以下内容：  
  
-   一个包含作业步骤的备份作业。  
  
-   备份失败时通知的操作员。  
  
-   备份作业的执行计划。  
  
将该备份作业一次性写入主服务器，然后将部门服务器登记为目标服务器。 从它们登记时刻起，所有部门服务器将运行相同的备份作业，而您只需定义一次作业。  
  
> [!NOTE]  
> 多服务器管理功能用于 sysadmin 角色成员。 然而，目标服务器上的 sysadmin 角色成员无法编辑目标服务器上由主服务器执行的操作。 这项安全措施可防止意外删除作业步骤，并可防止目标服务器上的操作中断。  
  
## <a name="in-this-section"></a>本节内容  
[创建多服务器环境](../../ssms/agent/create-a-multiserver-environment.md)  
包含有关如何创建和管理主服务器和目标服务器的信息。  
  
[为多服务器环境选择正确的 SQL Server 代理服务帐户](../../ssms/agent/choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md)  
包含有关使用非管理 Windows 帐户或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理服务的本地系统帐户如何影响多服务器环境的信息。  
  
[在目标服务器上设置加密选项](../../ssms/agent/set-encryption-options-on-target-servers.md)  
包含有关在目标服务器上设置 MsxEncryptChannelOptions[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理注册表子项的信息。  
  
[管理整个企业内的作业](../../ssms/agent/manage-jobs-across-an-enterprise.md)  
包含有关检查作业状态、更改作业的目标服务器、同步目标服务器时钟以及轮询主服务器以获取当前作业状态的信息。  
  
[排除使用代理的多服务器作业的故障](../../ssms/agent/troubleshoot-multiserver-jobs-that-use-proxies.md)  
包含有关排除使用失败代理的多服务器作业故障的信息。  
  
[轮询服务器](../../ssms/agent/poll-servers.md)  
包含有关如何隐式和显式使目标服务器轮询主服务器以同步作业信息的信息。  
  
[管理事件](../../ssms/agent/manage-events.md)  
包含有关将事件从目标服务器转发到主服务器的信息。  
  
[在企业中优化自动化管理](../../ssms/agent/tune-automated-administration-across-an-enterprise.md)  
包含有关多服务器环境中的自动化管理如何利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]自我优化功能的信息。  
  
## <a name="see-also"></a>另请参阅  
[有关安装 SQL Server 数据库引擎的向后兼容性主题](http://msdn.microsoft.com/en-us/10de5ec6-d3cf-42ef-aa62-1bdf3fbde841)  
[注册服务器](http://msdn.microsoft.com/en-us/c2a2513e-fa09-419c-99e7-a12d57c5a0db)  
[sp_add_targetservergroup](http://msdn.microsoft.com/en-us/acb69343-d766-46ff-b771-0c7655c5231a)  
[sp_delete_targetserver](http://msdn.microsoft.com/en-us/cc438701-ad91-419d-9f23-ebc4c548c700)  
[sp_delete_targetservergroup](http://msdn.microsoft.com/en-us/d8dd838e-64aa-419f-9ccb-ff04908cf3e4)  
[sp_help_downloadlist](http://msdn.microsoft.com/en-us/745b265b-86e8-4399-b928-c6969ca1a2c8)  
[sp_help_jobserver](http://msdn.microsoft.com/en-us/57971787-f9f5-4199-9f64-c2b61a308906)  
[sp_help_targetservergroup](http://msdn.microsoft.com/en-us/ec3a4a68-b591-431c-9518-053ede522d0c)  
[sp_resync_targetserver](http://msdn.microsoft.com/en-us/40e44df7-d3e3-44ee-b149-08aba629a21f)  
[sp_update_targetservergroup](http://msdn.microsoft.com/en-us/4ac65ed6-e07e-40e4-a282-13bfd92dfa41)  
[sysjobservers](http://msdn.microsoft.com/en-us/9abcc20f-a421-4591-affb-62674d04575e)  
[syslogins](http://msdn.microsoft.com/en-us/4cb34f17-a4bb-469f-a218-71f074e6308f)  
[systargetservers](http://msdn.microsoft.com/en-us/479d1314-be37-4d19-ac9c-419fc9110e53)  
  
