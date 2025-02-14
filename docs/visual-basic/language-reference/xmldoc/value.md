---
title: <value> （Visual Basic）
ms.date: 07/20/2015
helpviewer_keywords:
- <value> XML tag
- value XML tag
ms.assetid: 0b84b02e-9e6d-41b5-a926-0d5dc76dacb5
ms.openlocfilehash: 516ff6ba534478d066b8ca06baee46bdd4b35265
ms.sourcegitcommit: 4f4a32a5c16a75724920fa9627c59985c41e173c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2019
ms.locfileid: "72524606"
---
# <a name="value-visual-basic"></a>\<value > （Visual Basic）
指定属性的说明。  
  
## <a name="syntax"></a>语法  
  
```xml  
<value>property-description</value>  
```  
  
## <a name="parameters"></a>参数  
 `property-description`  
 属性的说明。  
  
## <a name="remarks"></a>备注  
 使用 `<value>` 标记来描述属性。 请注意，当您使用 Visual Studio 开发环境中的代码向导添加属性时，它将为新属性添加一个[\<summary >](../../../visual-basic/language-reference/xmldoc/summary.md)标记。 然后，你应该手动添加 `<value>` 标记来描述属性表示的值。  
  
 使用 [-doc](../../../visual-basic/reference/command-line-compiler/doc.md) 进行编译以便将文档注释处理到文件中。  
  
## <a name="example"></a>示例  
 此示例使用 `<value>` 标记来描述 `Counter` 属性包含的值。  
  
 [!code-vb[VbVbcnXmlDocComments#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#1)]  
  
## <a name="see-also"></a>请参阅

- [XML 注释标记](../../../visual-basic/language-reference/xmldoc/index.md)
