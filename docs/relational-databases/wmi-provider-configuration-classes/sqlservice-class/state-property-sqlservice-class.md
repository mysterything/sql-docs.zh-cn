---
title: "状态属性 （SqlService 类） |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: State Property (SqlService Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: State property
ms.assetid: 9e09f419-947c-4d4b-9a49-2d3396c847cd
caps.latest.revision: "36"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 31b49dea8026ee0aae4406451179ee8bafd5c712
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="state-property-sqlservice-class"></a>State 属性（SqlService 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]获取或设置服务的当前状态。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.State [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 一个表示服务的 [SqlService 类](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定服务状态的 uint32 值。  
  
 可以是下列值之一。  
  
 1  
 已停止。 服务已停止。  
  
 2  
 启动挂起。 服务正在等待启动。  
  
 3  
 停止挂起。 服务正在等待停止。  
  
 4  
 正在运行。 服务正在运行。  
  
 5  
 继续挂起。 服务正在等待继续。  
  
 6  
 暂停挂起。 服务正在等待暂停。  
  
 7  
 已暂停。 服务已暂停。  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  