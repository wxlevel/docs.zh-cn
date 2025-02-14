---
title: XML 子轴属性 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.XmlPropertyChildAxis
helpviewer_keywords:
- Visual Basic code, accessing XML
- XML axis [Visual Basic], child
- child axis property [Visual Basic]
- XML child axis property [Visual Basic]
- XML [Visual Basic], accessing
ms.assetid: 89a59d00-985e-4f5c-b59f-29b47bad11cb
ms.openlocfilehash: 88d0b1f315bc1bb9dc474604d222a8ebcc1e40aa
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72582243"
---
# <a name="xml-child-axis-property-visual-basic"></a>XML 子轴属性 (Visual Basic)
提供对以下一项的子级的访问：<xref:System.Xml.Linq.XElement> 对象、<xref:System.Xml.Linq.XDocument> 对象、<xref:System.Xml.Linq.XElement> 对象的集合或 <xref:System.Xml.Linq.XDocument> 对象的集合。  
  
## <a name="syntax"></a>语法  
  
```vb  
object.<child>  
```  
  
## <a name="parts"></a>部件  
  
|术语|定义|  
|---|---|  
|`object`|必须的。 <xref:System.Xml.Linq.XElement> 对象、<xref:System.Xml.Linq.XDocument> 对象、<xref:System.Xml.Linq.XElement> 对象的集合或 <xref:System.Xml.Linq.XDocument> 对象的集合。|  
|。 <|必须的。 表示子轴属性的开头。|  
|`child`|必须的。 要访问的子节点的名称，格式为 [`prefix:]name`。<br /><br /> -    `Prefix`-可选。 子节点的 XML 命名空间前缀。 必须是使用 `Imports` 语句定义的全局 XML 命名空间。<br />-    `Name`-必需。 本地子节点名。 请参阅已[声明的 XML 元素和属性的名称](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)。|  
|>|必须的。 表示子轴属性的结尾。|  
  
## <a name="return-value"></a>返回值  
 <xref:System.Xml.Linq.XElement> 对象的集合。  
  
## <a name="remarks"></a>备注  
 可以使用 XML 子轴属性，从 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XDocument> 对象，或从 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XDocument> 对象的集合，按名称访问子节点。 使用 XML `Value` 属性来访问返回的集合中第一个子节点的值。 有关详细信息，请参阅[XML Value 属性](../../../visual-basic/language-reference/xml-axis/xml-value-property.md)。  
  
 Visual Basic 编译器将子轴属性转换为对 <xref:System.Xml.Linq.XContainer.Elements%2A> 方法的调用。  
  
## <a name="xml-namespaces"></a>XML 命名空间  
 子轴属性中的名称仅可使用通过 `Imports` 语句全局声明的 XML 命名空间前缀。 它不能使用在 XML 元素文本中局部声明的 XML 命名空间前缀。 有关详细信息，请参阅[Imports 语句（XML 命名空间）](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)。  
  
## <a name="example"></a>示例  
 下面的示例演示如何从 `contact` 对象访问名为 `phone` 的子节点。  
  
 [!code-vb[VbXMLSamples#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples7.vb#17)]  
  
 此代码显示以下文本：  
  
 `Home Phone = 206-555-0144`  
  
## <a name="example"></a>示例  
 下面的示例演示如何从由 `contacts` 对象的 `contact` 子轴属性返回的集合访问名为 `phone` 的子节点。  
  
 [!code-vb[VbXMLSamples#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples7.vb#18)]  
  
 此代码显示以下文本：  
  
 `Home Phone = 206-555-0144`  
  
## <a name="example"></a>示例  
 下面的示例声明 `ns` 作为 XML 命名空间前缀。 然后它使用该命名空间前缀来创建 XML 文本并访问具有限定名称 `ns:name` 的第一个子节点。  
  
 [!code-vb[VbXMLSamples#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples8.vb#19)]  
  
 此代码显示以下文本：  
  
 `Patrick Hines`  
  
## <a name="see-also"></a>请参阅

- <xref:System.Xml.Linq.XElement>
- [XML 轴属性](../../../visual-basic/language-reference/xml-axis/index.md)
- [XML 文本](../../../visual-basic/language-reference/xml-literals/index.md)
- [在 Visual Basic 中创建 XML](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)
- [已声明的 XML 元素和特性的名称](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)
