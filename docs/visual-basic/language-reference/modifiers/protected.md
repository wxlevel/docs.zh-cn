---
title: Protected (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Protected
helpviewer_keywords:
- Protected Friend keyword combination
- Protected keyword [Visual Basic], and Friend
- Protected keyword [Visual Basic], syntax
- Protected access modifier
- Protected keyword [Visual Basic]
ms.assetid: 74ad3d56-309f-49d2-b60c-1d0157d010e8
ms.openlocfilehash: 8370d15e99a6f7ed0868441a4e44360fb258be13
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72583066"
---
# <a name="protected-visual-basic"></a>Protected (Visual Basic)

一个成员访问修饰符，它指定一个或多个已声明的编程元素只能从自己的类或派生类中访问。

## <a name="remarks"></a>备注

有时，在类中声明的编程元素包含敏感数据或受限制的代码，并希望限制对元素的访问。 但是，如果类可继承并且你需要派生类的层次结构，则这些派生类可能需要访问数据或代码。 在这种情况下，你希望可以从基类和所有派生类中访问元素。 若要以这种方式限制对某个元素的访问，可使用 `Protected` 声明该元素。

> [!NOTE]
> @No__t_0 访问修饰符可以与其他两个修饰符结合使用：
>
> - [受保护的 Friend](protected-friend.md)修饰符使类成员可从该类、派生类以及在其中定义该类的同一程序集中访问。
> - [私有受保护](private-protected.md)的修饰符使类成员可由派生类型访问，但仅包含在其包含的程序集中。

## <a name="rules"></a>规则

**声明上下文。** 只能在类级别使用 `Protected`。 这意味着 `Protected` 元素的声明上下文必须是类，且不能是源文件、命名空间、接口、模块、结构或过程。

## <a name="behavior"></a>行为

- **访问级别。** 类中的所有代码都可以访问其元素。 从基类派生的任何类中的代码都可以访问基类的所有 `Protected` 元素。 这适用于派生的所有代。 这意味着，类可以访问基类的基类的 `Protected` 元素，等等。

     受保护的访问不是友元访问的超集或子集。

- **访问修饰符。** 指定访问级别的关键字称为*访问修饰符*。 有关访问修饰符的比较，请参阅[Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。

`Protected` 修饰符可用于下面的上下文中：

- [Class 语句](../../../visual-basic/language-reference/statements/class-statement.md)

- [Const 语句](../../../visual-basic/language-reference/statements/const-statement.md)

- [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)

- [Delegate 语句](../../../visual-basic/language-reference/statements/delegate-statement.md)

- [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)

- [Enum 语句](../../../visual-basic/language-reference/statements/enum-statement.md)

- [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)

- [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)

- [Interface 语句](../../../visual-basic/language-reference/statements/interface-statement.md)

- [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)

- [Structure 语句](../../../visual-basic/language-reference/statements/structure-statement.md)

- [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)

## <a name="see-also"></a>请参阅

- [COMClassAttribute](../../../visual-basic/language-reference/modifiers/public.md)
- [Friend](../../../visual-basic/language-reference/modifiers/friend.md)
- [Private](../../../visual-basic/language-reference/modifiers/private.md)
- [Private Protected](private-protected.md)
- [Protected Friend](protected-friend.md)
- [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)
- [过程](../../../visual-basic/programming-guide/language-features/procedures/index.md)
- [结构](../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [对象和类](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
