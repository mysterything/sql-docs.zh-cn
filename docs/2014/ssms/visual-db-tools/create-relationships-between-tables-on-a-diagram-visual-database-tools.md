---
title: 创建关系表间的关系图 (Visual Database Tools) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- diagrams [SQL Server], designing
ms.assetid: 28e9630c-dff4-46cc-bb0e-fe77998b6ac2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ab36ebfefbfd3d8cee8e6da7caadf86eb4a10032
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52781619"
---
# <a name="create-relationships-between-tables-on-a-diagram-visual-database-tools"></a>在关系图中创建表间的关系（可视化数据库工具）
  您可以在关系图设计器中通过在各个表之间拖动列来创建不同表的列之间的关系。  
  
### <a name="to-create-a-relationship-graphically"></a>以图形方式创建关系  
  
1.  在数据库设计器中，单击想要将其与另一个表中的列建立关系的一个或多个数据库列的行选择器。  
  
2.  将所选列拖动到相关的表中。  
  
3.  出现两个对话框：**外键关系**并**表和列**，后者在前台显示。  
  
4.  “关系名”使用系统提供的名称，其格式为 FK_*localtable*_*foreigntabl*。 您可以更改此值。  
  
5.  验证“主键表”是否指定了正确的表。  
  
6.  网格列出了本地列及与其匹配的外部列。 您可以添加或删除表列或者更改映射。  
  
7.  选择“确定”。  
  
     此时将出现“外键关系”对话框。 “选定的关系”中显示了已创建的关系。  
  
8.  在网格中更改关系的属性。  
  
9. 选择 **“确定”** 以创建该关系。  
  
     数据库设计器将显示所选列之间的关系。  
  
## <a name="see-also"></a>请参阅  
 [表和列对话框&#40;可视化数据库工具&#41;](visual-database-tools.md)   
 [唯一约束和 Check 约束](../../relational-databases/tables/unique-constraints-and-check-constraints.md)   
 [使用数据库关系图中的表 (Visual Database Tools)](work-with-tables-in-database-diagram-visual-database-tools.md)  
  
  
