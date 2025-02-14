---
title: 如何：控制变量的可用性 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- access levels, declared elements
- Private keyword [Visual Basic], accessing variables
- access levels, variables
- Public keyword [Visual Basic], accessing variables
- Friend keyword [Visual Basic], accessing variables
- variables [Visual Basic], access level
- declared elements [Visual Basic], access level
- Protected keyword [Visual Basic], accessing variables
ms.assetid: eaf4f073-7922-43ce-ae1e-90ff376ae947
ms.openlocfilehash: 84aaeecdbd3cc8ab12589c0342b982bf3f1c8529
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72582616"
---
# <a name="how-to-control-the-availability-of-a-variable-visual-basic"></a>如何：控制变量的可用性 (Visual Basic)
可以通过指定变量的*访问级别*来控制变量的可用性。 访问级别确定哪些代码有权读取或写入变量。  
  
- *成员变量*（在模块级别和在任何过程外部定义）默认为公共访问，这意味着可以看到它们的任何代码都可以访问这些变量。 可以通过指定访问修饰符来更改此。  
  
- 尽管*本地变量*（在过程中定义）通常具有公共访问权限，但只有其过程中的代码可以访问这些变量。 不能更改本地变量的访问级别，但可以更改包含它的过程的访问级别。  
  
 有关详细信息，请参阅[Visual Basic 中的访问级别](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
## <a name="private-and-public-access"></a>私有和公共访问  
  
#### <a name="to-make-a-variable-accessible-only-from-within-its-module-class-or-structure"></a>仅允许从其模块、类或结构内部访问变量  
  
1. 将变量的[Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md)放入模块、类或结构中，但放在任何过程之外。  
  
2. 在 `Dim` 语句中包含[Private](../../../../visual-basic/language-reference/modifiers/private.md)关键字。  
  
     可以从模块、类或结构中的任何位置读取或写入变量，但不能从外部读取或写入。  
  
#### <a name="to-make-a-variable-accessible-from-any-code-that-can-see-it"></a>使变量可从可查看它的任何代码进行访问  
  
1. 对于成员变量，请将变量的 `Dim` 语句放入模块、类或结构中，但放在任何过程之外。  
  
2. 在 `Dim` 语句中包含[Public](../../../../visual-basic/language-reference/modifiers/public.md)关键字。  
  
     可以从与程序集互操作的任何代码读取或写入变量。  
  
 或  
  
1. 对于局部变量，请将变量的 `Dim` 语句放置到过程内。  
  
2. 不要在 `Dim` 语句中包含 `Public` 关键字。  
  
     可以从过程中的任何位置读取或写入变量，但不能从外部读取或写入。  
  
## <a name="protected-and-friend-access"></a>受保护和友元访问  
 可以将变量的访问级别限制为其类和派生类，或限制为其程序集。 您还可以指定这些限制的联合，这允许从任何派生类中的代码或同一程序集中的任何其他位置进行访问。 通过组合同一声明中的 `Protected` 和 `Friend` 关键字来指定此联合。  
  
#### <a name="to-make-a-variable-accessible-only-from-within-its-class-and-any-derived-classes"></a>使变量只能从其类和任何派生类中访问  
  
1. 将变量的 `Dim` 语句放置在类中，但在任何过程之外。  
  
2. 在 `Dim` 语句中包含[Protected](../../../../visual-basic/language-reference/modifiers/protected.md)关键字。  
  
     可以从类中的任何位置以及从派生的任何类（而不是从派生链中的任何类）读取或写入变量。  
  
#### <a name="to-make-a-variable-accessible-only-from-within-the-same-assembly"></a>使变量只能从同一程序集内访问  
  
1. 将变量的 `Dim` 语句放入模块、类或结构中，但在任何过程之外。  
  
2. 在 `Dim` 语句中包含[Friend](../../../../visual-basic/language-reference/modifiers/friend.md)关键字。  
  
     你可以从模块、类或结构中的任何位置读取或写入变量，也可以从同一程序集中的任何代码读取或写入到程序集之外的任何代码。  
  
## <a name="example"></a>示例  
 下面的示例演示具有 `Public`、`Protected`、`Friend`、`Protected Friend` 和 `Private` 访问级别的变量的声明。 请注意，如果 `Dim` 语句指定了访问级别，则不需要包括 `Dim` 关键字。  
  
```vb  
Public Class classForEverybody  
Protected Class classForMyHeirs  
Friend stringForThisProject As String  
Protected Friend stringForProjectAndHeirs As String  
Private numberForMeOnly As Integer  
```  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 变量访问级别的限制性越多，恶意代码使用它的可能性就越小。  
  
## <a name="see-also"></a>请参阅

- [Visual Basic 中的访问级别](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)
- [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md)
- [COMClassAttribute](../../../../visual-basic/language-reference/modifiers/public.md)
- [Protected](../../../../visual-basic/language-reference/modifiers/protected.md)
- [Friend](../../../../visual-basic/language-reference/modifiers/friend.md)
- [Private](../../../../visual-basic/language-reference/modifiers/private.md)
