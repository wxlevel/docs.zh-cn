---
title: Module 语句（Visual Basic）
ms.date: 07/20/2015
f1_keywords:
- Module
- vb.Module
helpviewer_keywords:
- modules, classes
- modules
- Module statement [Visual Basic]
- modules, declaring
- standard modules
- classes [Visual Basic], vs. modules
- declarations [Visual Basic], modules
ms.assetid: a1243afc-14a5-45df-95d5-51118aeac362
ms.openlocfilehash: 9b1aae08d0009a9fd23d6441207f1601ffec2568
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72583098"
---
# <a name="module-statement"></a>Module 语句

声明模块的名称，并引入模块包含的变量、属性、事件和过程的定义。

## <a name="syntax"></a>语法

```vb
[ <attributelist> ] [ accessmodifier ]  Module name
    [ statements ]
End Module
```

## <a name="parts"></a>部件

`attributelist`  
可选。 请参阅[特性列表](../../../visual-basic/language-reference/statements/attribute-list.md)。

`accessmodifier`  
可选。 可以是以下各项之一：

- [COMClassAttribute](../../../visual-basic/language-reference/modifiers/public.md)

- [Friend](../../../visual-basic/language-reference/modifiers/friend.md)

请参阅 [Access levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。

`name`  
必须的。 此模块的名称。 请参阅 [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。

`statements`  
可选。 定义此模块的变量、属性、事件、过程和嵌套类型的语句。

`End Module`  
终止 `Module` 定义。

## <a name="remarks"></a>备注

@No__t_0 语句定义一个在其命名空间中可用的引用类型。 *模块*（有时称为*标准模块*）与类相似，但有一些重要的区别。 每个模块都有一个实例，无需创建或分配给变量。 模块不支持继承或实现接口。 请注意，如果某个模块不是类或结构的*类型*，则不能将编程元素声明为具有模块的数据类型。

只能在命名空间级别使用 `Module`。 这意味着模块的*声明上下文*必须是源文件或命名空间，不能是类、结构、模块、接口、过程或块。 不能将模块嵌套在其他模块或任何类型中。 有关详细信息，请参阅[声明上下文和默认访问级别](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)。

模块与程序具有相同的生存期。 因为其成员都是 `Shared` 的，所以它们的生存期也等于程序的生存期。

模块默认为[Friend](../../../visual-basic/language-reference/modifiers/friend.md)访问。 您可以使用访问修饰符调整其访问级别。 有关详细信息，请参阅[Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。

模块的所有成员都隐式 `Shared`。

## <a name="classes-and-modules"></a>类和模块

这些元素具有许多相似之处，但也存在一些重要的差异。

- **规范.** Visual Basic 的早期版本可识别两种类型的模块：*类模块*（cls 文件）和*标准模块*（bas 文件）。 当前版本分别调用这些*类*和*模块*。

- **共享成员。** 您可以控制某个类的成员是共享成员还是实例成员。

- **对象方向。** 类是面向对象的，但模块不是。 因此，只有类可以实例化为对象。 有关详细信息，请参阅[对象和类](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)。

## <a name="rules"></a>规则

- **组成.** 所有模块成员都是隐式[共享](../../../visual-basic/language-reference/modifiers/shared.md)的。 在声明成员时，不能使用 `Shared` 关键字，也不能更改任何成员的共享状态。

- **继承。** 模块无法从所有模块继承的 <xref:System.Object> 以外的任何类型继承。 特别是，一个模块不能从另一个模块继承。

  不能在模块定义中使用[Inherits 语句](../../../visual-basic/language-reference/statements/inherits-statement.md)，甚至可以指定 <xref:System.Object>。

- **默认属性。** 不能在模块中定义任何默认属性。 有关详细信息，请参阅[默认值](../../../visual-basic/language-reference/modifiers/default.md)。

## <a name="behavior"></a>行为

- **访问级别。** 在模块中，你可以使用其自己的访问级别声明每个成员。 模块成员默认为[公共](../../../visual-basic/language-reference/modifiers/public.md)访问权限，变量和常量除外，默认为[私有](../../../visual-basic/language-reference/modifiers/private.md)访问。 当某个模块的访问权限超过其成员之一时，将优先使用指定的模块访问级别。

- **内.** 模块在其命名空间中的作用域。

  每个模块成员的作用域都是整个模块。 请注意，所有成员都接受*类型提升*，这会导致其作用域升级到包含该模块的命名空间。 有关详细信息，请参阅[类型提升](../../../visual-basic/programming-guide/language-features/declared-elements/type-promotion.md)。

- **限定.** 项目中可以有多个模块，可以在两个或多个模块中声明同名的成员。 但是，如果引用来自模块外部，则必须使用适当的模块名称来限定对此类成员的任何引用。 有关详细信息，请参阅 [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)。

## <a name="example"></a>示例

[!code-vb[VbVbalrStatements#69](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#69)]

## <a name="see-also"></a>请参阅

- [Class 语句](../../../visual-basic/language-reference/statements/class-statement.md)
- [Namespace 语句](../../../visual-basic/language-reference/statements/namespace-statement.md)
- [Structure 语句](../../../visual-basic/language-reference/statements/structure-statement.md)
- [Interface 语句](../../../visual-basic/language-reference/statements/interface-statement.md)
- [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)
- [类型提升](../../../visual-basic/programming-guide/language-features/declared-elements/type-promotion.md)
