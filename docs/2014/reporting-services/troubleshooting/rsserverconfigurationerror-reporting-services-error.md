---
title: rsServerConfigurationError - Reporting Services 错误 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rsServerConfigurationError
ms.assetid: 0913afc2-34b4-4713-b570-cfd5718975ac
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: a0017be7f7ac6117c1512cbaf3e46b662f0a06f0
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56021675"
---
# <a name="rsserverconfigurationerror---reporting-services-error"></a>rsServerConfigurationError - Reporting Services 错误
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|rsServerConfiguration|  
|事件源|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|组件|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|消息正文|报表服务器遇到配置错误。|  
  
## <a name="explanation"></a>解释  
 这是一个在报表服务器或报表创作工具具有无效配置设置时出现的常规错误。 通常该错误还附带另一条消息，该消息声明此错误的实际原因。  
  
 下面的列表汇总了可能的原因：  
  
-   找不到或无法读取 RSReportServer.config 或 RSReportDesigner.config 文件。  
  
-   这两个配置文件中有一个文件的 XML 元素丢失或无效。  
  
-   一个或多个 XML 元素的值丢失或无效。  
  
-   注册表设置无效。  
  
## <a name="user-action"></a>用户操作  
 如果该错误在您手动编辑配置文件后开始出现，请删除所做的更改并输入以前的值，或者如果您有备份，请还原先前的版本。  
  
 若要查看其他错误消息信息附带`rsServerConfiguration`错误，查看报表服务器跟踪日志文件，位于 \Microsoft SQL Server\MSRS12。\<实例名 > services\logfiles。 有关详细信息，请参阅 [Reporting Services 日志文件和源](../report-server/reporting-services-log-files-and-sources.md)。  
  
## <a name="internal-only"></a>仅内部  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 配置文件](../report-server/reporting-services-configuration-files.md)   
 [修改 Reporting Services 配置文件 (RSreportserver.config)](../report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
  
  
