---
title: <permission> （Visual Basic）
ms.date: 07/20/2015
helpviewer_keywords:
- <permission> XML tag
- permission XML tag
ms.assetid: 0edf0500-5cd7-49c0-9255-64c48f972b77
ms.openlocfilehash: 904d573514bf35b773d47321b7fd3b6a86e90262
ms.sourcegitcommit: 4f4a32a5c16a75724920fa9627c59985c41e173c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2019
ms.locfileid: "72524698"
---
# <a name="permission-visual-basic"></a>\<permission > （Visual Basic）
指定成员所需的权限。  
  
## <a name="syntax"></a>语法  
  
```xml  
<permission cref="member">description</permission>  
```  
  
## <a name="parameters"></a>参数  
 `member`  
 对可从当前编译环境调用的成员或字段的引用。 编译器检查是否存在给定的代码元素，并将 `member` 转换为输出 XML 中规范的元素名称。 将 `member` 括在引号（""）中。  
  
 `description`  
 对成员访问权限的说明。  
  
## <a name="remarks"></a>备注  
 使用 `<permission>` 标记来记录成员的访问。 使用 <xref:System.Security.PermissionSet> 类指定对成员的访问权限。  
  
 使用 [-doc](../../../visual-basic/reference/command-line-compiler/doc.md) 进行编译以便将文档注释处理到文件中。  
  
## <a name="example"></a>示例  
 此示例使用 `<permission>` 标记来描述 `ReadFile` 方法所需的 <xref:System.Security.Permissions.FileIOPermission>。  
  
 [!code-vb[VbVbcnXmlDocComments#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#7)]  
  
## <a name="see-also"></a>请参阅

- [XML 注释标记](../../../visual-basic/language-reference/xmldoc/index.md)
