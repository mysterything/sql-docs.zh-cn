---
title: "表名 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL grammar [ODBC], table names
- table names [ODBC]
ms.assetid: f7a5cb0a-3be7-4f46-82f9-64ffdbceaa9b
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 480ca31108b608139b5563f0c18d1fa020e76f75
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="table-names"></a>表名称
当 dBASE、 Microsoft Excel、 Paradox，或使用驱动程序的文本、 表名称中发生的 SELECT 或 DELETE，FROM 子句后 INTO 子句在插入、 更新和之后，CREATE TABLE 和 DROP TABLE 可以包含有效的路径、 主服务器名称和文件扩展名.  
  
 使用 SQL 语句中的其他位置的表名称不支持的路径或扩展使用，但将接受主名称 (例如，EMP 从 C:\ABC\EMP)。  
  
 可以使用相关名称 （别名）。 例如：  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```