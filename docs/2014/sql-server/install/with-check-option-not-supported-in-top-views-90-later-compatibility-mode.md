---
title: WITH CHECK OPTION 不支持在 90 或更高版本的兼容模式下，包含 TOP 的视图 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- TOP clause
- WITH CHECK OPTION clause
ms.assetid: 1b9581d0-bad9-43e0-b8fc-f32d8a8a04ca
caps.latest.revision: 14
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c8c64ce7395b5ecbb33530672d93817f7938db6d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243987"
---
# <a name="with-check-option-is-not-supported-in-views-that-contain-top-in-90-or-later-compatibility-modes"></a>在 90 或更高的兼容模式下，包含 TOP 的视图不支持 WITH CHECK OPTION
  升级顾问检测到了使用 WITH CHECK OPTION 的视图，并在该视图或者被引用视图的 SELECT 语句中检测到了 TOP 子句。 当数据库兼容模式设置为 80 或更低时，用此方式定义的视图会错误地允许通过视图修改数据，从而产生不准确的结果。 如果使用 WITH CHECK OPTION 的视图或者被引用视图使用了 TOP 子句，且数据库兼容模式设置为 90 或更高，则无法通过该视图插入或更新数据。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>纠正措施  
 升级时，用户数据库将保持其兼容模式。 如果需要通过使用 WITH CHECK OPTION 和 TOP 的视图来修改数据，请在将数据库兼容模式更改为 100 或更高前修改这类视图。 有关详细信息，请参阅[sp_dbcmptlevel &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbcmptlevel-transact-sql)。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  