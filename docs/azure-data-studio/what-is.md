---
title: 概述
titleSuffix: Azure Data Studio
description: Azure Data Studio 是免费的轻型工具，用于管理 SQL Server、 Azure SQL 数据库和 Azure SQL 数据仓库运行在 Windows、 macOS 和 Linux。
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: overview
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f7369893be3cd42dab0e0c0cd870a52c639083b5
ms.sourcegitcommit: 11ab8a241a6d884b113b3cf475b2b9ed61ff00e3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161604"
---
# <a name="what-is-azure-data-studio"></a>什么是 Azure Data Studio？

Azure Data Studio是一种跨平台数据库工具，适用于在Windows，MacOS和Linux上使用Microsoft系列内部部署和云数据平台的数据专业人员。

此前在预览名称SQL Operations Studio下发布的Azure Data Studio提供了现代化编辑器体验，包括Intellisense，代码片段，源代码控制集成和集成终端。 它在设计时考虑了数据平台用户，内置了查询结果集和可自定义的仪表板。

**[下载并安装 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)**


## <a name="sql-code-editor-with-intellisense"></a>使用 IntelliSense 的 SQL 代码编辑器

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 提供了现代、 键盘焦点位于 SQL 编码经验，这与内置功能，例如多个选项卡窗口、 丰富的 SQL 编辑器、 IntelliSense、 关键字完成、 代码段、 代码导航和源代码管理简化日常任务(Git) 的集成。 运行按需 SQL 查询、 查看并将结果保存为文本、 JSON 或 Excel。 编辑数据、组织最喜欢的数据库连接，以及以熟悉的对象浏览体验浏览数据库对象。 若要了解如何使用 SQL 编辑器，请参阅[使用 SQL 编辑器来创建数据库对象](tutorial-sql-editor.md)。

## <a name="smart-sql-code-snippets"></a>智能 SQL 代码段

SQL 代码段生成正确的 SQL 语法来创建数据库、 表、 视图、 存储的过程、 用户、 登录名、 角色、 等，并更新现有数据库对象。 使用智能代码片段来快速创建开发或测试目的，数据库的副本和要生成并执行创建和插入脚本。

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 此外提供了功能，以创建自定义 SQL 代码段。 若要了解详细信息，请参阅[创建和使用代码片段](code-snippets.md)。


## <a name="customizable-server-and-database-dashboards"></a>可自定义服务器和数据库仪表板

创建丰富的可定制仪表板，以监视并快速解决数据库中的性能瓶颈。 若要了解见解小组件和数据库（以及服务器）仪表板，请参阅[使用见解小组件管理服务器和数据库](insight-widgets.md)。

## <a name="connection-management-server-groups"></a>连接管理（服务器组）

可以通过服务器组来组织所用服务器和数据库的连接信息。 有关详细信息，请参阅[服务器组](server-groups.md)。

## <a name="integrated-terminal"></a>集成的终端

使用你最喜爱的命令行工具 (例如 Bash、 PowerShell、 sqlcmd、 bcp 和 ssh 配合使用) 在集成终端窗口中右[!INCLUDE[name-sos](../includes/name-sos-short.md)]用户界面。 若要了解有关集成终端的信息，请参阅[集成的终端](integrated-terminal.md)。

## <a name="extensibility-and-extension-authoring"></a>可扩展性和扩展创建

增强[!INCLUDE[name-sos](../includes/name-sos-short.md)]通过扩展功能的基本安装体验。 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 数据管理活动，以及对扩展创建的支持，提供了扩展点。

若要了解有关中的可扩展性[!INCLUDE[name-sos](../includes/name-sos-short.md)]，请参阅[扩展性](extensibility.md)。
若要了解有关创作扩展，请参阅[扩展插件创作](extension-authoring.md)。

## <a name="feature-comparison-with-sql-server-management-studio-ssms"></a>使用 SQL Server Management Studio (SSMS) 的功能比较

**如果使用 Azure Data Studio 您：**
- 需要在 macOS 或 Linux 上运行
- 要连接到 SQL Server 2019 大数据群集
- 花大部分时间编辑或执行查询
- 需要快速图表和可视化结果集的能力
- 可以执行大多数管理任务通过使用 sqlcmd 或 Powershell 集成终端
- 对向导体验的最小需求
- 不需要进行深度管理配置

**如果使用 SQL Server Management Studio 您：**
- 数据库管理任务上花费的大部分时间
- 正在执行深度管理配置
- 正在执行安全管理，包括用户管理、 漏洞评估和安全功能的配置
- 为 SQL Server Query Store 使用的报表
- 需要进行性能优化顾问和仪表板的使用
- 正在执行的 Dacpac 导入/导出
- 需要已注册的服务器访问权限，而想要控制 SQL Server 在 Windows 上的服务

### <a name="shell"></a>Shell

|功能|Azure Data Studio|SSMS|
|:---|:---|:---|
|Azure 登录|用户帐户控制|用户帐户控制|
|面板|用户帐户控制||
|Extensions|用户帐户控制||
|集成的终端|用户帐户控制||
|“对象资源管理器”|用户帐户控制|用户帐户控制|
|对象脚本|用户帐户控制|用户帐户控制|
|项目系统|用户帐户控制||
|从表中选择|用户帐户控制|用户帐户控制|
|源代码管理|用户帐户控制||
|任务窗格|用户帐户控制||
|主题设置|用户帐户控制||
|深色模式|用户帐户控制||
|Azure 资源浏览器|预览||
|生成脚本向导||用户帐户控制|
|Import\Export DACPAC||用户帐户控制|
|对象属性||用户帐户控制|
|表设计器||用户帐户控制|


### <a name="query-editor"></a>查询编辑器

|功能|Azure Data Studio|SSMS|
|:---|:---|:---|
|图表查看器|用户帐户控制||
|将结果导出到 CSV、 JSON、 XLSX|用户帐户控制||
|IntelliSense|用户帐户控制|用户帐户控制|
|代码段|用户帐户控制|用户帐户控制|
|显示计划|预览|用户帐户控制|
|客户端统计信息||用户帐户控制|
|实时查询统计信息||用户帐户控制|
|查询选项||用户帐户控制|
|将结果保存到文件||用户帐户控制|
|以文本格式显示结果||用户帐户控制|
|空间查看器||用户帐户控制|
|SQLCMD||用户帐户控制|

### <a name="operating-system-support"></a>操作系统支持

|功能|Azure Data Studio|SSMS|
|:---|:---|:---|
|Linux|用户帐户控制||
|macOS|用户帐户控制||
|Windows|用户帐户控制|用户帐户控制|

### <a name="data-engineering"></a>数据工程

|功能|Azure Data Studio|SSMS|
|:---|:---|:---|
|创建外部表向导|预览||
|HDFS 的集成|预览||
|笔记本|预览||

### <a name="database-administration"></a>数据库管理

|功能|Azure Data Studio|SSMS|
|:---|:---|:---|
|备份/还原|用户帐户控制|用户帐户控制|
|平面文件导入|预览|用户帐户控制|
|SQL 代理|预览|用户帐户控制|
|SQL Profiler|预览|用户帐户控制|
|AlwaysOn||用户帐户控制|
|始终加密||用户帐户控制|
|复制数据向导||用户帐户控制|
|数据优化顾问||用户帐户控制|
|错误日志查看器||用户帐户控制|
|维护计划||用户帐户控制|
|多服务器查询||用户帐户控制|
|基于策略的管理||用户帐户控制|
|PolyBase||用户帐户控制|
|查询存储||用户帐户控制|
|已注册的服务器||用户帐户控制|
|Replication||用户帐户控制|
|安全管理||用户帐户控制|
|Service Broker||用户帐户控制|
|SQL Mail||用户帐户控制|
|Template Explorer||用户帐户控制|
|漏洞评估||用户帐户控制|
|XEvent 管理||用户帐户控制|



## <a name="next-steps"></a>后续步骤
- [下载并安装 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)
- [连接和查询 SQL Server](quickstart-sql-server.md)
- [连接和查询 Azure SQL 数据库](quickstart-sql-database.md)
