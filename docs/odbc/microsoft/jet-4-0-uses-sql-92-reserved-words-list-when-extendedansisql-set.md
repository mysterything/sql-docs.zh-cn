---
title: "Jet 4.0 使用 SQL 92 保留的字列表时 ExtendedAnsiSQL_Set |Microsoft 文档"
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
- extendedANSISQL [ODBC], reserved words
ms.assetid: 7645187e-7777-4c07-9686-0a80d5c5834d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: adc457cee71093222b102fad15e4a47042758ac9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="jet-40-uses-sql-92-reserved-words-list-when-extendedansisqlset"></a>Jet 4.0 使用 SQL 92 保留的字列表时 ExtendedAnsiSQL_Set
启用 ExtendedAnsiSQL 标志后，Jet 4.0 将使用的 SQL 92 保留的字列表。 尝试使用 SQL 92 保留字，因为不带引号的对象名称将导致语法错误。 当关闭 ExtendedAnsiSQL 标志时，新的保留的字可以用作对象名称作为之前。