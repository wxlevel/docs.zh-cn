---
title: <paramref> (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- paramref XML tag
- <paramref> XML tag
ms.assetid: 8979d53b-beb1-41b7-b41e-6bbea1c17a03
ms.openlocfilehash: 85171bd8deeb5f54c4560bb8b2339107bb8d8c68
ms.sourcegitcommit: 4f4a32a5c16a75724920fa9627c59985c41e173c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2019
ms.locfileid: "72524706"
---
# <a name="paramref-visual-basic"></a>\<paramref > （Visual Basic）
将单词设置为参数格式。  
  
## <a name="syntax"></a>语法  
  
```xml  
<paramref name="name"/>  
```  
  
## <a name="parameters"></a>参数  
 `name`  
 要引用的参数的名称。 用双引号 (" ") 将名称引起来。  
  
## <a name="remarks"></a>备注  
 @No__t_0 标记为你提供了一种方法，用于指示某个字是一个参数。 可以处理 XML 文件，以便以某种不同的方式格式化此参数。  
  
 使用 [-doc](../../../visual-basic/reference/command-line-compiler/doc.md) 进行编译以便将文档注释处理到文件中。  
  
## <a name="example"></a>示例  
 此示例使用 `<paramref>` 标记来引用 `id` 参数。  
  
 [!code-vb[VbVbcnXmlDocComments#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#6)]  
  
## <a name="see-also"></a>请参阅

- [XML 注释标记](../../../visual-basic/language-reference/xmldoc/index.md)
