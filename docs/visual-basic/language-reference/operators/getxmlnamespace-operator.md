---
title: GetXmlNamespace 运算符 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.GetXmlNamespace
- GetXmlNamespace
helpviewer_keywords:
- GetXmlNamespace operator [Visual Basic]
- GetXmlNamespace keyword [Visual Basic]
ms.assetid: d0d28cfd-0755-4896-ae0b-4981aa35517c
ms.openlocfilehash: bfccdcd9b5d35418b206dfa9fefffb5ddab69c66
ms.sourcegitcommit: 35da8fb45b4cca4e59cc99a5c56262c356977159
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2019
ms.locfileid: "71592171"
---
# <a name="getxmlnamespace-operator-visual-basic"></a>GetXmlNamespace 运算符 (Visual Basic)
获取与指定的 XML 命名空间前缀相对应的 @no__t 0 对象。  
  
## <a name="syntax"></a>语法  
  
```vb  
GetXmlNamespace(xmlNamespacePrefix)  
```  
  
## <a name="parts"></a>部件  
 `xmlNamespacePrefix`  
 可选。 标识 XML 命名空间前缀的字符串。 如果提供，则此字符串必须是有效的 XML 标识符。 有关详细信息，请参阅已[声明的 XML 元素和属性的名称](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)。 如果未指定前缀，则返回默认命名空间。 如果未指定默认命名空间，则返回空命名空间。  
  
## <a name="return-value"></a>返回值  
 与 XML 命名空间前缀相对应的 @no__t 0 对象。  
  
## <a name="remarks"></a>备注  
 @No__t-0 运算符获取对应于 XML 命名空间前缀 `xmlNamespacePrefix` 的 @no__t 1 对象。  
  
 您可以直接在 XML 文本和 XML 轴属性中使用 XML 命名空间前缀。 但是，必须使用 `GetXmlNamespace` 运算符将命名空间前缀转换为 @no__t 的对象，然后才能在代码中使用它。 可以将未限定的元素名称追加到 @no__t 0 对象，以获取完全限定的 @no__t 1 对象，这很多 @no__t 2 方法都需要。  
  
## <a name="example"></a>示例  
 下面的示例导入 `ns` 作为 XML 命名空间前缀。 然后，它使用命名空间的前缀创建 XML 文本，并访问具有限定名 `ns:phone` 的第一个子节点。 然后，它将该子节点传递到 `ShowName` 子例程，该子例程使用 `GetXmlNamespace` 运算符构造限定名称。 然后 @no__t，将限定名称传递给 <xref:System.Xml.Linq.XNode.Ancestors%2A> 方法，以获取父 @no__t 2 节点。  
  
 [!code-vb[VbXMLSamples#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/GetXmlNamespace.vb#38)]  
  
 调用 `TestGetXmlNamespace.RunSample()` 时，将显示一个消息框，其中包含以下文本：  
  
 `Name: Patrick Hines`  
  
## <a name="see-also"></a>请参阅

- [Imports 语句（XML 命名空间）](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)
- [在 Visual Basic 中访问 XML](../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)
