---
title: 交叉验证报表中的度量值 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- root mean square error [data mining]
- cross-validation [data mining]
- mean absolute error [data mining]
- log score [data mining]
- likelihood [data mining]
ms.assetid: a07b1665-7f72-4266-82a4-43a91ae2571d
caps.latest.revision: 27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a7d45c1ff8501dff8c74de22a16ac47b69c5375a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304631"
---
# <a name="measures-in-the-cross-validation-report"></a>交叉验证报表中的度量值
  在交叉验证过程中， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将挖掘结构中的数据划分为多个交叉部分，然后对该结构和任何关联的挖掘模型反复进行测试。 基于此分析，它将为该结构和每个模型输出一组标准的准确性度量值。  
  
 该报表包含有关数据中折叠数以及每个折叠中的数据量的一些基本信息，还包含描述数据分布的一组一般性的指标。 通过比较各交叉部分的一般性的指标，您可以评估该结构或模型的可靠性。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 还为挖掘模型显示一组详细的度量值。 这些度量值依赖于模型类型以及要分析的属性的类型：例如，是离散的还是连续的。  
  
 本节提供“交叉验证”报表中包含的度量值列表以及各度量值的含义。 有关如何计算各度量值的详细信息，请参阅[交叉验证公式](cross-validation-formulas.md)。  
  
## <a name="list-of-measures-in-the-cross-validation-report"></a>交叉验证报表中度量值的列表  
 下表列出了交叉验证报表中出现的度量值。 这些度量值按测试类型进行分组，测试类型在下表的左侧列中提供。 右侧列列出了度量值在报表中出现时的名称，并且简要解释了其含义。  
  
|测试类型|度量值和说明|  
|---------------|-------------------------------|  
|群集|适用于聚类分析模型的度量值：<br /><br /> **事例可能性**： 此度量值通常指示可能性是，某个事例属于特定分类。 <br />                      对于交叉验证，将对分数求和，然后除以事例数，因此在这里，分数是平均事例可能性。|  
|分类|应用于分类模型的度量值：<br /><br /> **真警报**/<br />                      **真负**/ **误报**/ **误报**： 中行或值的预测的状态与目标状态相匹配的分区的计数和预测概率大于指定的阈值。 排除具有目标属性缺失值的情况下，这意味着所有值的计数可能未加总|  
||**通过/失败**： 预测的状态与目标状态匹配并且预测概率值大于 0 的行或分区中的值的计数。|  
|可能性|可能性度量值适用于多个模型类型：<br /><br /> **提升**： 与边缘概率测试用例中实际预测概率的比率。 排除对目标属性具有缺失值的行。 此度量值通常显示使用模型时目标结果的概率提高的程度。<br /><br /> **均方根误差**： 所有分区事例的平均误差的平方根除以分区中，不包括缺少目标属性值的行中的事例数。 RMSE 是预测模型的一种流行的估计器。 该分数对每个事例的余数求平均值，以便生成模型误差的单个指示器。<br /><br /> **对数评分**： 每个事例的实际概率的对数求和，和除以输入数据集，不包括缺少目标属性值的行中的行数。 由于概率用小数表示，因此，对数分数始终是负数。 接近 0 的数字是较好的分数。 原始分数可以具有非常不规则或扭曲的分布，而对数评分与百分比相似。|  
|估计|仅适用于估算模型预测连续数值属性的度量值：<br /><br /> **均方根误差**： 预测的值与实际值进行比较时的平均误差。 RMSE 是预测模型的一种流行的估计器。 该分数对每个事例的余数求平均值，以便生成模型误差的单个指示器。<br /><br /> **平均绝对误差**： 预测的值与实际值，计算公式为错误的绝对值之和的平均值进行比较时的平均误差。 平均绝对误差用于理解预测与实际值在整体上的接近程度。 较小的分数意味着预测更准确。<br /><br /> **对数评分**： 每个事例的实际概率的对数求和，和除以输入数据集，不包括缺少目标属性值的行中的行数。 由于概率用小数表示，因此，对数分数始终是负数。 接近 0 的数字是较好的分数。 原始分数可以具有非常不规则或扭曲的分布，而对数评分与百分比相似。|  
|聚合|聚合度量值提供每个分区的结果中的变体的指示：<br /><br /> **意味着**： 特定度量值的平均分区值。<br /><br /> **标准偏差**： 从特定的度量值，在模型中的所有分区的平均值偏差的平均值。 对于交叉验证，此分数值越高，则意味着折叠之间的差异越大。|  
  
## <a name="see-also"></a>请参阅  
 [测试和验证&#40;数据挖掘&#41;](testing-and-validation-data-mining.md)  
  
  