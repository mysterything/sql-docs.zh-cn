---
title: Wtd (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9a548f25d9114e9032f2462bbc97bda637abd6d9
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743777"
---
# <a name="wtd-mdx"></a>Wtd (MDX)


  按照时间维度中的周级别的约束，从给定成员所在的级别返回一组同级成员，从第一个同级成员开始到给定成员为止。  
  
## <a name="syntax"></a>语法  
  
```  
  
Wtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>Remarks  
 如果未指定一个成员表达式，默认值是第一个层次结构使用的类型级别的当前成员类型时的第一个维度中的周数 (**Time.CurrentMember**) 度量值组中。  
  
 **Wtd**函数是快捷函数[PeriodsToDate](../mdx/periodstodate-mdx.md)函数其中的级别设置为*周*。 也就是说，`Wtd(Member_Expression)` 等效于 `PeriodsToDate(Week_Level_Expression,Member_Expression)`。  
  
## <a name="see-also"></a>请参阅  
 [Qtd &#40;MDX&#41;](../mdx/qtd-mdx.md)   
 [Mtd &#40;MDX&#41;](../mdx/mtd-mdx.md)   
 [Ytd &#40;MDX&#41;](../mdx/ytd-mdx.md)   
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
