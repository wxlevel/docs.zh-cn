---
title: 处理 XML 文件 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- XML comments [Visual Basic], parsing [Visual Basic]
ms.assetid: 78a15cd0-7708-4e79-85d1-c154b7a14a8c
ms.openlocfilehash: 91583612940282b05ebbf38bd5f0a59d6af5bbcd
ms.sourcegitcommit: 4f4a32a5c16a75724920fa9627c59985c41e173c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2019
ms.locfileid: "72524445"
---
# <a name="processing-the-xml-file-visual-basic"></a>处理 XML 文件 (Visual Basic)
编译器为代码（已标记以生成文档）中的每个构造生成一个 ID 字符串。 （有关如何标记代码的信息，请参阅[XML 注释标记](../../../visual-basic/language-reference/xmldoc/index.md)。）ID 字符串唯一地标识构造。 处理 XML 文件的程序可以使用 ID 字符串来标识相应的 .NET Framework 元数据/反射项。  
  
 XML 文件不是代码的层次结构表示形式;它是一个平面列表，其中每个元素都有一个生成的 ID。  
  
 编译器在生成 ID 字符串时应遵循以下规则：  
  
- 字符串不得包含空格。  
  
- ID 字符串的第一部分标识被标识的成员类型，单个字符后跟一个冒号。 使用以下成员类型。  
  
|字符|描述|  
|---|---|  
|N|namespace<br /><br /> 不能将文档注释添加到命名空间，但可以对其进行 CREF 引用（如果支持）。|  
|T|类型： `Class`、`Module`、`Interface`、`Structure`、`Enum`、`Delegate`|  
|F|字段： `Dim`|  
|P|属性： `Property` （包括默认属性）|  
|M|方法： `Sub`、`Function`、`Declare`、`Operator`|  
|E|事件： `Event`|  
|!|错误字符串<br /><br /> 字符串的其余部分提供有关错误的信息。 Visual Basic 编译器将为无法解析的链接生成错误信息。|  
  
- @No__t_0 的第二部分是从命名空间的根开始的项的完全限定名称。 项的名称、其封闭类型和命名空间用句点分隔。 如果项本身的名称包含句点，则将其替换为数字符号（#）。 假定没有任何项在其名称中直接具有数字符号。 例如，将 `System.String.#ctor` `String` 构造函数的完全限定名称。  
  
- 对于属性和方法，如果方法带有自变量，则后跟用括号括起来的自变量列表。 如果没有任何自变量，则不会出现括号。 确保自变量之间用逗号分隔。 每个参数的编码会直接在 .NET Framework 签名中对其进行编码。  
  
## <a name="example"></a>示例  
 下面的代码演示如何生成类及其成员的 ID 字符串。  
  
 [!code-vb[VbVbcnXmlDocComments#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#10)]  
  
## <a name="see-also"></a>请参阅

- [-doc](../../../visual-basic/reference/command-line-compiler/doc.md)
- [如何：创建 XML 文档](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)
