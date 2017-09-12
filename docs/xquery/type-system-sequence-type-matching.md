---
title: "序列的类型匹配 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- sequence type matching [XQuery]
- XQuery, sequence type matching
ms.assetid: 8c56fb69-ca04-4aba-b55a-64ae216c492d
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 707a939ce112e612874fefb956b8ebbc3142c0c5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="type-system---sequence-type-matching"></a>类型系统的序列的类型匹配
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery 表达式的值始终是零序列或多项序列。 一个项可以是一个原子值，也可以是一个节点。 序列类型匹配是指将查询表达式返回的序列类型与特定类型进行匹配的能力。 例如：  
  
-   如果表达式值是原子值，则您可能希望知道该值是整数类型、小数类型还是字符串类型。  
  
-   如果表达式的值是一个 XML 节点，则您可能希望知道此节点是注释节点、处理指令节点还是文本节点。  
  
-   您可能希望知道表达式返回的是 XML 元素还是特定名称和类型的属性节点。  
  
 您可以在序列类型匹配时使用 `instance of` 布尔运算符。 有关详细信息`instance of`表达式，请参阅[SequenceType 表达式 &#40;XQuery &#41;](../xquery/sequencetype-expressions-xquery.md).  
  
## <a name="comparing-the-atomic-value-type-returned-by-an-expression"></a>比较表达式返回的原子值类型  
 如果表达式返回的是原子值序列，则您可能必须弄清序列中值的类型。 下列示例说明如何使用序列类型语法来估计表达式返回的原子值类型。  
  
### <a name="example-determining-whether-a-sequence-is-empty"></a>示例：确定序列是否为空  
 **Empty()**序列类型可以使用序列类型表达式，以确定指定的表达式返回的序列是否为空序列。  
  
 在下面的示例中，XML 架构允许 <`root`> 元素为空：  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" nillable="true" type="byte"/>  
</schema>'  
GO  
```  
  
 现在，如果类型化的 XML 实例为 <`root`> 元素指定值，则 `instance of empty()` 将返回 False。  
  
```  
DECLARE @var XML(SC1)  
SET @var = '<root>1</root>'  
-- The following returns False  
SELECT @var.query('data(/root[1]) instance of  empty() ')  
GO  
```  
  
 如果 <`root`> 元素在实例中为空，则它的值将是一个空序列并且 `instance of empty()` 将返回 True。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" />'  
SELECT @var.query('data(/root[1]) instance of  empty() ')  
GO  
```  
  
### <a name="example-determining-the-type-of-an-attribute-value"></a>示例：确定属性值的类型  
 有时，您可能希望在进行处理前估计表达式返回的序列类型。 例如，您可能有一个 XML 架构，其中，节点被定义为联合类型。 在下面的示例中，集合中的 XML 架构将属性 `a` 定义为联合类型，该类型的值可以是十进制值，也可以是字符串类型。  
  
```  
-- Drop schema collection if it exists.  
-- DROP XML SCHEMA COLLECTION SC.  
-- GO  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
  <element name="root">  
    <complexType>  
       <sequence/>  
         <attribute name="a">  
            <simpleType>  
               <union memberTypes="decimal string"/>  
            </simpleType>  
         </attribute>  
     </complexType>  
  </element>  
</schema>'  
GO  
```  
  
 处理类型化 XML 实例之前，您可能需要了解属性 `a` 的值类型。 在下面的示例中，属性 `a` 的值是十进制类型。 因此`, instance of xs:decimal`，则返回 True。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root a="2.5"/>'  
SELECT @var.query('data((/root/@a)[1]) instance of xs:decimal')  
GO  
```  
  
 现在，将属性 `a` 的值更改为字符串类型。 `instance of xs:string` 将返回 True。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root a="Hello"/>'  
SELECT @var.query('data((/root/@a)[1]) instance of xs:string')  
GO  
```  
  
### <a name="example-cardinality-in-sequence-expressions"></a>示例：序列表达式中的基数  
 此示例说明基数在序列表达式中的作用。 下列 XML 架构定义了 <`root`> 元素，该元素属于字节类型且可为空。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" nillable="true" type="byte"/>  
</schema>'  
GO  
```  
  
 在下列查询中，由于表达式返回的是单字节类型，因此 `instance of` 将返回 True。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root>111</root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte ')   
GO  
```  
  
 如果使 <`root`> 元素为空，则它的值将是一个空序列。 也就是说，表达式 `/root[1]` 将返回一个空序列。 因此，`instance of xs:byte` 将返回 False。 注意，在这种情况下默认基数为 1。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"></root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte ')   
GO  
-- result = false  
```  
  
 如果通过添加出现指示符 (`?`) 来指定基数,则序列表达式将返回 True。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"></root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte? ')   
GO  
-- result = true  
```  
  
 注意，在序列类型表达式中的测试分两个阶段完成：  
  
1.  测试先确定表达式类型是否与指定的类型匹配。  
  
2.  如果匹配，测试将确定表达式返回的项数是否与指定的出现指示符匹配。  
  
 如果两种情况都匹配，`instance of` 表达式将返回 True。  
  
### <a name="example-querying-against-an-xml-type-column"></a>示例：对 xml 类型列进行查询  
 在下面的示例中，针对 Instructions 列指定的查询**xml**键入[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]数据库。 因为它具有关联的架构，因此是类型化 XML 列。 XML 架构定义整数类型的 `LocationID` 属性。 因此，在序列表达式中， `instance of xs:integer?` ，则返回 True。  
  
```  
SELECT Instructions.query('   
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
data(/AWMI:root[1]/AWMI:Location[1]/@LocationID) instance of xs:integer?') as Result   
FROM Production.ProductModel   
WHERE ProductModelID = 7  
```  
  
## <a name="comparing-the-node-type-returned-by-an-expression"></a>比较表达式返回的节点类型  
 如果表达式返回节点序列，则您可能必须弄清此序列中节点的类型。 下列示例说明如何使用序列类型语法估计表达式返回的节点类型。 您可以使用下列序列类型：  
  
-   **item()** – 匹配序列中的任何项。  
  
-   **node （)** – 确定序列是否是一个节点。  
  
-   **processing-instruction()** – 确定表达式是否返回处理指令。  
  
-   **comment()** – 确定表达式是否返回注释。  
  
-   **document-node()** – 确定表达式是否返回文档节点。  
  
 以下示例说明这些序列类型。  
  
### <a name="example-using-sequence-types"></a>示例：使用序列类型  
 在此示例中，针对非类型化的 XML 变量执行了若干查询。 这些查询说明序列类型的使用方法。  
  
```  
DECLARE @var XML  
SET @var = '<?xml-stylesheet href="someValue" type="text/xsl" ?>  
<root>text node  
  <!-- comment 1 -->   
  <a>Data a</a>  
  <!-- comment  2 -->  
</root>'  
```  
  
 在第一个查询中，表达式返回元素 <`a`> 的类型化值。 在第二个查询中，表达式返回元素 <`a`>。 两个返回值都是项。 因此，两个查询都返回 True。  
  
```  
SELECT @var.query('data(/root[1]/a[1]) instance of item()')  
SELECT @var.query('/root[1]/a[1] instance of item()')  
```  
  
 下列三个查询中的所有 XQuery 表达式都返回 <`root`> 元素节点子级。 因此，序列类型表达式 `instance of node()` 将返回 True，另外两个表达式 `instance of text()` 和 `instance of document-node()` 将返回 False。  
  
```  
SELECT @var.query('(/root/*)[1] instance of node()')  
SELECT @var.query('(/root/*)[1] instance of text()')  
SELECT @var.query('(/root/*)[1] instance of document-node()')   
```  
  
 在下列查询中，`instance of document-node()` 表达式将返回 True，因为 <`root`> 元素的父级是文档节点。  
  
```  
SELECT @var.query('(/root/..)[1] instance of document-node()') -- true  
```  
  
 在下列查询中，表达式检索 XML 实例中的第一个节点。 由于此节点是处理指令节点，因此 `instance of processing-instruction()` 表达式将返回 True。  
  
```  
SELECT @var.query('(/node())[1] instance of processing-instruction()')  
```  
  
### <a name="implementation-limitations"></a>实现限制  
 具体的限制如下：  
  
-   **document-node()**内容类型不支持语法。  
  
-   **processing-instruction(name)**不支持语法。  
  
## <a name="element-tests"></a>元素测试  
 元素测试用于将表达式返回的元素节点与具有特定名称和类型的元素节点相匹配。 您可以使用下列元素测试：  
  
```  
element ()  
element(ElementName)  
element(ElementName, ElementType?)   
element(*, ElementType?)  
```  
  
## <a name="attribute-tests"></a>属性测试  
 属性测试决定了表达式返回的属性是否为属性节点。 您可以使用下列属性测试。  
  
 `attribute()`  
  
 `attribute(AttributeName)`  
  
 `attribute(AttributeName, AttributeType)`  
  
## <a name="test-examples"></a>测试示例  
 下面的示例说明了适合采用元素测试和属性测试的情形。  
  
### <a name="example-a"></a>示例 A  
 以下 XML 架构定义 `CustomerType` 复杂类型，其中 <`firstName`> 和 <`lastName`> 元素是可选的。 对于指定的 XML 实例，您可能需要确定特定客户的名字是否存在。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
targetNamespace="myNS" xmlns:ns="myNS">  
  <complexType name="CustomerType">  
     <sequence>  
        <element name="firstName" type="string" minOccurs="0"   
                  nillable="true" />  
        <element name="lastName" type="string" minOccurs="0"/>  
     </sequence>  
  </complexType>  
  <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
DECLARE @var XML(SC)  
SET @var = '<x:customer xmlns:x="myNS">  
<firstName>SomeFirstName</firstName>  
<lastName>SomeLastName</lastName>  
</x:customer>'  
```  
  
 下列查询使用 `instance of element (firstName)` 表达式确定 <`customer`> 的第一个子元素是否名为 <`firstName`>。 在这种情况下，查询将返回 True。  
  
```  
SELECT @var.query('declare namespace x="myNS";   
     (/x:customer/*)[1] instance of element (firstName)')  
GO  
```  
  
 如果从实例中删除 <`firstName`> 元素，查询将返回 False。  
  
 您也可以使用下列内容：  
  
-   `element(ElementName, ElementType?)` 序列类型语法，如以下查询中所示。 它将与名为 `firstName`、类型为 `xs:string` 的空元素节点或非空元素节点进行匹配。  
  
    ```  
    SELECT @var.query('declare namespace x="myNS";   
    (/x:customer/*)[1] instance of element (firstName, xs:string?)')  
    ```  
  
-   `element(*, type?)` 序列类型语法，如以下查询中所示。 它将与类型为 `xs:string`（名称不限）的元素节点进行匹配。  
  
    ```  
    SELECT @var.query('declare namespace x="myNS"; (/x:customer/*)[1] instance of element (*, xs:string?)')  
    GO  
    ```  
  
### <a name="example-b"></a>示例 B  
 下列示例说明如何确定表达式返回的节点是否为具有特定名称的元素节点。 它使用**element()**测试。  
  
 在下面的示例中，正在查询的 XML 实例中的两个 <`Customer`> 元素属于两种不同的类型：`CustomerType` 和 `SpecialCustomerType`。 假定您希望知道表达式返回的 <`Customer`> 元素的类型。 以下 XML 架构集合定义 `CustomerType` 和 `SpecialCustomerType` 类型。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
          targetNamespace="myNS"  xmlns:ns="myNS">  
  <complexType name="CustomerType">  
    <sequence>  
      <element name="firstName" type="string"/>  
      <element name="lastName" type="string"/>  
    </sequence>  
  </complexType>  
  <complexType name="SpecialCustomerType">  
     <complexContent>  
       <extension base="ns:CustomerType">  
        <sequence>  
            <element name="Age" type="int"/>  
        </sequence>  
       </extension>  
     </complexContent>  
    </complexType>  
   <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
```  
  
 此 XML 架构集合用于创建类型化**xml**变量。 分配给此变量的 XML 实例具有两个属于两种不同类型的 <`customer`> 元素。 第一个元素属于 `CustomerType` 类型，第二个元素属于 `SpecialCustomerType` 类型。  
  
```  
DECLARE @var XML(SC)  
SET @var = '  
<x:customer xmlns:x="myNS">  
   <firstName>FirstName1</firstName>  
   <lastName>LastName1</lastName>  
</x:customer>  
<x:customer xsi:type="x:SpecialCustomerType" xmlns:x="myNS" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
   <firstName> FirstName2</firstName>  
   <lastName> LastName2</lastName>  
   <Age>21</Age>  
</x:customer>'  
```  
  
 在以下查询中，由于表达式返回的第一个客户元素不属于 `instance of element (*, x:SpecialCustomerType ?)` 类型，因此，`SpecialCustomerType` 表达式返回 False。  
  
```  
SELECT @var.query('declare namespace x="myNS";   
    (/x:customer)[1] instance of element (*, x:SpecialCustomerType ?)')  
```  
  
 如果更改上一个查询的表达式并检索第二个 <`customer`> 元素 (`/x:customer)[2]`)，则 `instance of` 将返回 True。  
  
### <a name="example-c"></a>示例 C  
 此示例使用属性测试。 下列 XML 架构定义了带有 CustomerID 属性和 Age 属性的 CustomerType 复杂类型。 Age 属性是可选的。 对于特定的 XML 实例，您可能希望确定 <`customer`> 元素中是否存在 Age 属性。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
       targetNamespace="myNS" xmlns:ns="myNS">  
<complexType name="CustomerType">  
  <sequence>  
     <element name="firstName" type="string" minOccurs="0"   
               nillable="true" />  
     <element name="lastName" type="string" minOccurs="0"/>  
  </sequence>  
  <attribute name="CustomerID" type="integer" use="required" />  
  <attribute name="Age" type="integer" use="optional" />  
 </complexType>  
 <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
```  
  
 由于正在查询的 XML 实例中具有名称为 `Age` 的属性节点，因此，以下查询返回 True。 此表达式中使用了 `attribute(Age)` 属性测试。 由于属性是无序的，查询使用 FLWOR 表达式检索所有属性，然后使用 `instance of` 表达式测试每个属性。 此示例首先创建 XML 架构集合创建类型化**xml**变量。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<x:customer xmlns:x="myNS" CustomerID="1" Age="22" >  
<firstName>SomeFName</firstName>  
<lastName>SomeLName</lastName>  
</x:customer>'  
SELECT @var.query('declare namespace x="myNS";   
FOR $i in /x:customer/@*  
RETURN  
    IF ($i instance of attribute (Age)) THEN  
        "true"  
        ELSE  
        ()')     
GO  
  
```  
  
 如果从实例中删除了可选的 `Age` 属性，则上述查询将返回 False。  
  
 您可以在属性测试中指定属性名称和类型 (`attribute(name,type)`)。  
  
```  
SELECT @var.query('declare namespace x="myNS";   
FOR $i in /x:customer/@*  
RETURN  
    IF ($i instance of attribute (Age, xs:integer)) THEN  
        "true"  
        ELSE  
        ()')  
```  
  
 或者，您可以指定`attribute(*, type)`序列类型语法。 如果属性类型与指定类型匹配（名称不限），则此序列类型语法将与属性节点匹配。  
  
### <a name="implementation-limitations"></a>实现限制  
 具体的限制如下：  
  
-   在元素测试中，类型名称后面必须跟发生指示符 (**？**)。  
  
-   **元素 （ElementName，TypeName）**不支持。  
  
-   **元素 (\*，TypeName)**不支持。  
  
-   **schema-element()**不支持。  
  
-   **schema-attribute(AttributeName)**不支持。  
  
-   显式查询**xsi: type**或**xsi: nil**不支持。  
  
## <a name="see-also"></a>另请参阅  
 [类型系统 &#40;XQuery &#41;](../xquery/type-system-xquery.md)  
  
  