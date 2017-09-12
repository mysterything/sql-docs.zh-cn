---
title: "QueryDefinition 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- QueryDefinition Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- QueryDefinition
helpviewer_keywords:
- QueryDefinition element
ms.assetid: 25bf0e93-d5c5-41df-b310-a253a4ace80e
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e28cd4413efa9f1695de339c38ee25fa959df13b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="querydefinition-element-assl"></a>QueryDefinition 元素 (ASSL)
  包含关联的查询的不透明表达式[数据源](../../../analysis-services/scripting/objects/datasource-element-assl.md)中的元素[QueryBinding](../../../analysis-services/scripting/data-type/querybinding-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<QueryBinding>  
   ...  
   <QueryDefinition>...</QueryDefinition>  
   ...  
</QueryBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[QueryBinding](../../../analysis-services/scripting/data-type/querybinding-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**QueryDefinition**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.QueryBinding>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  