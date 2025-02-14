---
title: Operator 语句（Visual Basic）
ms.date: 07/20/2015
f1_keywords:
- vb.operator
helpviewer_keywords:
- operators [Visual Basic]
- procedures [Visual Basic], operator
- Narrowing keyword [Visual Basic], conversion operators
- Visual Basic code, operators
- Widening keyword [Visual Basic], conversion operators
- syntax [Visual Basic], Operator procedures
- operators [Visual Basic], overloading
- overloaded operators [Visual Basic]
- operator overloading
- operator procedures
- Operator statement [Visual Basic]
- CType function [Visual Basic], Operator statement
ms.assetid: b12ec4af-1ad7-4a17-865b-c5ee96320ae5
ms.openlocfilehash: c4fae40992fa665121aff637ae427ef0cafbf547
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72582387"
---
# <a name="operator-statement"></a>Operator Statement

声明在类或结构上定义运算符过程的运算符符号、操作数和代码。

## <a name="syntax"></a>语法

```vb
[ <attrlist> ] Public [ Overloads ] Shared [ Shadows ] [ Widening | Narrowing ]
Operator operatorsymbol ( operand1 [, operand2 ]) [ As [ <attrlist> ] type ]
    [ statements ]
    [ statements ]
    Return returnvalue
    [ statements ]
End Operator
```

## <a name="parts"></a>部件

`attrlist`  
可选。 请参阅[特性列表](../../../visual-basic/language-reference/statements/attribute-list.md)。

`Public`  
必须的。 指示此运算符过程具有[公共](../../../visual-basic/language-reference/modifiers/public.md)访问权限。

`Overloads`  
可选。 请参阅[重载](../../../visual-basic/language-reference/modifiers/overloads.md)。

`Shared`  
必须的。 指示此运算符过程是一个[共享](../../../visual-basic/language-reference/modifiers/shared.md)过程。

`Shadows`  
可选。 请参阅[阴影](../../../visual-basic/language-reference/modifiers/shadows.md)。

`Widening`  
对于转换运算符是必需的，除非指定 `Narrowing`。 指示此运算符过程定义[扩大](../../../visual-basic/language-reference/modifiers/widening.md)转换。 请参阅此帮助页上的 "扩大和收缩转换"。

`Narrowing`  
对于转换运算符是必需的，除非指定 `Widening`。 指示此运算符过程定义[收缩](../../../visual-basic/language-reference/modifiers/narrowing.md)转换。 请参阅此帮助页上的 "扩大和收缩转换"。

`operatorsymbol`  
必须的。 此运算符过程所定义的运算符的符号或标识符。

`operand1`  
必须的。 一元运算符的单个操作数的名称和类型（包括转换运算符）或二元运算符的左操作数。

`operand2`  
对于二元运算符是必需的。 二元运算符的右操作数的名称和类型。

`operand1` 和 `operand2` 具有以下语法和部分：

`[ ByVal ] operandname [ As operandtype ]`

|部件|描述|
|----------|-----------------|
|`ByVal`|可选，但传递机制必须是[ByVal](../../../visual-basic/language-reference/modifiers/byval.md)。|
|`operandname`|必须的。 表示此操作数的变量的名称。 请参阅 [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。|
|`operandtype`|除非 `On` `Option Strict`，否则为可选。 此操作数的数据类型。|

`type`  
除非 `On` `Option Strict`，否则为可选。 运算符过程返回的值的数据类型。

`statements`  
可选。 运算符过程运行的语句块。

`returnvalue`  
必须的。 运算符过程返回到调用代码的值。

`End` `Operator`  
必须的。 终止此运算符过程的定义。

## <a name="remarks"></a>备注

只能在类或结构中使用 `Operator`。 这意味着运算符的*声明上下文*不能是源文件、命名空间、模块、接口、过程或块。 有关详细信息，请参阅[声明上下文和默认访问级别](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)。

所有运算符都必须 `Public Shared`。 不能为任一操作数指定 `ByRef`、`Optional` 或 `ParamArray`。

不能使用运算符符号或标识符来保存返回值。 必须使用 `Return` 语句，并且必须指定一个值。 任意数量的 `Return` 语句可以出现在过程中的任何位置。

以这种方式定义运算符称为*运算符重载*，无论是否使用 `Overloads` 关键字。 下表列出了可定义的运算符。

|键入|运算符|
|----------|---------------|
|一元|`+`, `-`, `IsFalse`, `IsTrue`, `Not`|
|二进制|`+`, `-`, `*`, `/`, `\`, `&`, `^`, `>>`, `<<`, `=`, `<>`, `>`, `>=`, `<`, `<=`, `And`, `Like`, `Mod`, `Or`, `Xor`|
|转换（一元）|`CType`|

请注意，二元列表中的 `=` 运算符是比较运算符，而不是赋值运算符。

在定义 `CType` 时，必须指定 `Widening` 或 `Narrowing`。

## <a name="matched-pairs"></a>匹配对

必须将某些运算符定义为匹配对。 如果定义此类对的任一运算符，则还必须定义其他运算符。 匹配对如下所示：

- `=` 和 `<>`

- `>` 和 `<`

- `>=` 和 `<=`

- `IsTrue` 和 `IsFalse`

## <a name="data-type-restrictions"></a>数据类型限制

你定义的每个运算符都必须涉及你定义它的类或结构。 这意味着，类或结构必须显示为以下类型的数据类型：

- 一元运算符的操作数。

- 二元运算符的至少一个操作数。

- 转换运算符的操作数或返回类型。

 某些运算符具有额外的数据类型限制，如下所示：

- 如果定义 `IsTrue` 和 `IsFalse` 运算符，则它们必须返回 `Boolean` 类型。

- 如果定义 `<<` 和 `>>` 运算符，则它们必须为 `operand2` 的 `operandtype` 指定 `Integer` 类型。

返回类型不一定对应于任一操作数的类型。 例如，即使两个操作数都不 `Boolean`，`=` 或 `<>` 这样的比较运算符也可能返回 `Boolean`。

## <a name="logical-and-bitwise-operators"></a>逻辑运算符和位运算符

@No__t_0、`Or`、`Not` 和 `Xor` 运算符可在 Visual Basic 中执行逻辑或按位运算。 但是，如果在类或结构上定义这些运算符之一，则只能定义其按位运算。

不能使用 `Operator` 语句直接定义 `AndAlso` 运算符。 不过，如果已满足以下条件，则可以使用 `AndAlso`：

- 已在要用于 `AndAlso` 的相同操作数类型上定义 `And`。

- @No__t_0 的定义返回的类型与定义它的类或结构的类型相同。

- 您已在定义了 `And` 的类或结构上定义 `IsFalse` 运算符。

同样，如果已使用类或结构的返回类型在同一操作数上定义了 `Or`，并且已在类或结构上定义了 `IsTrue`，则可以使用 `OrElse`。

## <a name="widening-and-narrowing-conversions"></a>Widening and Narrowing Conversions

在运行时，*扩大转换*始终会成功，而*收缩转换*可能会在运行时失败。 有关详细信息，请参阅 [Widening and Narrowing Conversions](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)。

如果声明要 `Widening` 的转换过程，则过程代码不得生成任何失败。 这意味着：

- 它必须始终返回 `type` 类型的有效值。

- 它必须处理所有可能的异常和其他错误情况。

- 它必须处理它所调用的任何过程中的任何错误。

如果转换过程可能会失败或可能导致未经处理的异常，则必须将其声明为 `Narrowing`。

## <a name="example"></a>示例

下面的代码示例使用 `Operator` 语句来定义结构的轮廓，其中包括 `And`、`Or`、`IsFalse` 和 `IsTrue` 运算符的运算符过程。 `And` 和 `Or` 每个都采用类型 `abc` 和返回类型 `abc` 两个操作数。 `IsFalse` 和 `IsTrue` 每个都采用 `abc` 类型的单个操作数并返回 `Boolean`。 这些定义允许调用代码将 `And`、`AndAlso`、`Or` 和 `OrElse` 与 `abc` 类型的操作数一起使用。

[!code-vb[VbVbalrStatements#44](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#44)]

## <a name="see-also"></a>请参阅

- [IsFalse 运算符](../../../visual-basic/language-reference/operators/isfalse-operator.md)
- [IsTrue 运算符](../../../visual-basic/language-reference/operators/istrue-operator.md)
- [Widening](../../../visual-basic/language-reference/modifiers/widening.md)
- [Narrowing](../../../visual-basic/language-reference/modifiers/narrowing.md)
- [扩大转换和收缩转换](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)
- [如何：定义运算符](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)
- [如何：定义转换运算符](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)
- [如何：调用运算符过程](../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-operator-procedure.md)
- [如何：使用定义运算符的类](../../../visual-basic/programming-guide/language-features/procedures/how-to-use-a-class-that-defines-operators.md)
