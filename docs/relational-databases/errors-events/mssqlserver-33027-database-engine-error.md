---
title: MSSQLSERVER_33027 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 33027 (Database Engine error)
ms.assetid: bfdc626e-7958-4511-987d-3b687824e8af
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 880abcd92943e9a9083f69d7c41b6b33147c9ed1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47597515"
---
# <a name="mssqlserver33027"></a>MSSQLSERVER_33027
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|33027|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SEC_CRYPTOPROV_CANTLOADDLL|  
|消息正文|由于 Authenticode 签名或文件路径无效，未能加载加密提供程序“%.*ls”。 请检查以前的消息，了解其他失败信息。|  
  
## <a name="explanation"></a>解释  
SQL Server 无法使用错误消息中列出的加密提供程序，因为 SQL Server 无法加载 DLL。 原因是名称无效或 Authenticode 签名无效。  
  
## <a name="user-action"></a>用户操作  
请检查该文件是否存在以及 SQL Server 是否拥有访问该位置的权限。 请查看错误日志以获得其他相关消息。 否则，请联系加密服务供应商以获得详细信息。  
  
