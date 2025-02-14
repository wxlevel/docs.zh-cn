---
title: Inherits 语句（Visual Basic）
ms.date: 07/20/2015
f1_keywords:
- vb.Inherits
- Inherits
helpviewer_keywords:
- Inherits statement [Visual Basic]
- Inherits statement [Visual Basic], syntax
ms.assetid: 9e6fe042-9af3-4341-8093-fc3537770cf2
ms.openlocfilehash: e92e12908c89bb7a0bf385a2122b0c8f1eb8a6f7
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72581754"
---
# <a name="inherits-statement"></a>Inherits Statement
导致当前类或接口继承其他类或接口集的属性、变量、属性、过程和事件。  
  
## <a name="syntax"></a>语法  
  
```vb  
Inherits basetypenames  
```  
  
## <a name="parts"></a>部件  
  
|术语|定义|  
|---|---|  
|`basetypenames`|必须的。 此类派生自的类的名称。<br /><br /> 或<br /><br /> 此接口派生自的接口的名称。 使用逗号分隔多个名称。|  
  
## <a name="remarks"></a>备注  
 如果使用，则 `Inherits` 语句必须是类或接口定义中的第一个非空白非注释行。 它应紧跟 `Class` 或 `Interface` 语句之后。  
  
 只能在类或接口中使用 `Inherits`。 这意味着继承的声明上下文不能是源文件、命名空间、结构、模块、过程或块。  
  
## <a name="rules"></a>规则  
  
- **类继承。** 如果类使用 `Inherits` 语句，则只能指定一个基类。  
  
     类不能从嵌套在它中的类继承。  
  
- **接口继承。** 如果接口使用 `Inherits` 语句，则可以指定一个或多个基接口。 即使两个接口都定义了具有相同名称的成员，也可以从两个接口继承。 如果这样做，则实现代码必须使用名称限定来指定要实现的成员。  
  
     接口不能从具有限制性更强的访问级别的其他接口继承。 例如，`Public` 接口无法从 `Friend` 接口继承。  
  
     接口不能从嵌套在它内的接口继承。  
  
 .NET Framework 中的类继承示例是 <xref:System.ArgumentException> 类，该类继承自 <xref:System.SystemException> 类。 这将提供系统异常所需的所有预定义属性和过程 <xref:System.ArgumentException>，如 <xref:System.Exception.Message%2A> 属性和 <xref:System.Exception.ToString%2A> 方法。  
  
 .NET Framework 中的接口继承示例是从 <xref:System.Collections.IEnumerable> 接口继承的 <xref:System.Collections.ICollection> 接口。 这会导致 <xref:System.Collections.ICollection> 继承遍历集合所需的枚举器的定义。  
  
## <a name="example"></a>示例  
 下面的示例使用 `Inherits` 语句来显示名为 `thisClass` 的类如何继承名为 `anotherClass` 的基类的所有成员。  
  
 [!code-vb[VbVbalrStatements#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#37)]  
  
## <a name="example"></a>示例  
 下面的示例演示多个接口的继承。  
  
 [!code-vb[VbVbalrStatements#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#38)]  
  
 名为 `thisInterface` 的接口现在包括 <xref:System.IComparable>、<xref:System.IDisposable> 和 <xref:System.IFormattable> 接口中的所有定义。继承成员分别为两个对象的特定于类型的比较提供了这些定义，释放了已分配的资源，并表示的值。作为 `String` 的对象。 实现 `thisInterface` 的类必须实现每个基接口的每个成员。  
  
## <a name="see-also"></a>请参阅

- [MustInherit](../../../visual-basic/language-reference/modifiers/mustinherit.md)
- [NotInheritable](../../../visual-basic/language-reference/modifiers/notinheritable.md)
- [对象和类](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
- [继承的基础知识](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)
- [接口](../../../visual-basic/programming-guide/language-features/interfaces/index.md)
