---
title: 扩大转换和收缩转换 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- widening conversions [Visual Basic]
- narrowing conversions [Visual Basic]
- conversions [Visual Basic], type
- data types [Visual Basic], changing
- variables [Visual Basic], changing data type
- conversions [Visual Basic], exceptions during conversion
- type conversion [Visual Basic], exceptions during conversion
- conversions [Visual Basic], data type
- conversions [Visual Basic], narrowing
- type conversion [Visual Basic], narrowing
- data type conversion [Visual Basic], widening
- data type conversion [Visual Basic], narrowing
- changing data types [Visual Basic]
- type conversion [Visual Basic], widening
- data type conversion [Visual Basic], exceptions during conversion
- conversions [Visual Basic], widening
ms.assetid: 058c3152-6c28-4268-af44-2209e774f0bd
ms.openlocfilehash: d1822afc4b10a725e13c1469a068c30813d3a2d3
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72582740"
---
# <a name="widening-and-narrowing-conversions-visual-basic"></a>扩大转换和收缩转换 (Visual Basic)
类型转换的一个重要注意事项是转换的结果是否在目标数据类型的范围内。  
  
 *扩大转换*将值更改为数据类型，可允许原始数据的任何可能值。  扩大转换保留源值，但可以更改其表示形式。 如果从整型转换为 `Decimal` 或从 `Char` 转换为 `String`，则会发生这种情况。  
  
 *“收缩转换”* 将值更改为可能无法保存某些可能值的数据类型。 例如，小数值在转换为整型时进行舍入，并且转换为 `Boolean` 的数值类型减小为 `True` 或 `False`。  
  
## <a name="widening-conversions"></a>扩大转换  
 下表显示了标准扩大转换。  
  
|数据类型|扩大到数据类型<sup>1</sup>|  
|---|---|  
|[SByte](../../../../visual-basic/language-reference/data-types/sbyte-data-type.md)|`SByte`, `Short`, `Integer`, `Long`, `Decimal`, `Single`, `Double`|  
|[Byte](../../../../visual-basic/language-reference/data-types/byte-data-type.md)|`Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `Long`, `ULong`, `Decimal`, `Single`, `Double`|  
|[Short](../../../../visual-basic/language-reference/data-types/short-data-type.md)|`Short`、 `Integer`、 `Long`、 `Decimal`、 `Single`、 `Double`|  
|[UShort](../../../../visual-basic/language-reference/data-types/ushort-data-type.md)|`UShort`, `Integer`, `UInteger`, `Long`, `ULong`, `Decimal`, `Single`, `Double`|  
|[Integer](../../../../visual-basic/language-reference/data-types/integer-data-type.md)|`Integer`，`Long`，`Decimal`，`Single`，`Double`<sup>2</sup>|  
|[UInteger](../../../../visual-basic/language-reference/data-types/uinteger-data-type.md)|`UInteger`、`Long`、`ULong`、`Decimal`、`Single`、`Double`<sup>2</sup>|  
|[Long](../../../../visual-basic/language-reference/data-types/long-data-type.md)|`Long`、`Decimal`、`Single` `Double`<sup>2</sup>|  
|[ULong](../../../../visual-basic/language-reference/data-types/ulong-data-type.md)|`ULong`、`Decimal`、`Single` `Double`<sup>2</sup>|  
|[小数](../../../../visual-basic/language-reference/data-types/decimal-data-type.md)|`Decimal`，`Single`，`Double`<sup>2</sup>|  
|[单精度](../../../../visual-basic/language-reference/data-types/single-data-type.md)|`Single`，`Double`|  
|[双精度](../../../../visual-basic/language-reference/data-types/double-data-type.md)|`Double`|  
|任何枚举类型（[枚举](../../../../visual-basic/language-reference/statements/enum-statement.md)）|它的基础整型类型和基础类型扩展到的任何类型。|  
|[Char](../../../../visual-basic/language-reference/data-types/char-data-type.md)|`Char`，`String`|  
|`Char` 数组|`Char` 数组，`String`|  
|任何类型|[对象](../../../../visual-basic/language-reference/data-types/object-data-type.md)|  
|任何派生类型|它派生自的任何基类型<sup>3</sup>。|  
|任何类型|它所实现的任何接口。|  
|[Nothing](../../../../visual-basic/language-reference/nothing.md)|任何数据类型或对象类型。|  
  
 <sup>1</sup>根据定义，每个数据类型扩大到自身。  
  
 <sup>2</sup> `Integer`、`UInteger`、`Long`、`ULong` 或 `Decimal` 到 `Single` 或 `Double` 的转换可能会导致精度损失，但绝不会损失。 在这种意义上，它们不会导致信息丢失。  
  
 <sup>3</sup>从派生类型到它的某个基类型的转换都是扩大的。 理由是，派生类型包含基类型的所有成员，因此它限定为基类型的实例。 相反，基类型不包含由派生类型定义的任何新成员。  
  
 扩大转换始终会在运行时成功，不会导致数据丢失。 无论[选项 Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)是将类型检查开关设置为 `On` 还是 `Off`，都可以始终隐式执行它们。  
  
## <a name="narrowing-conversions"></a>收缩转换  
 标准收缩转换包括：  
  
- 上表中的扩大转换的反向方向（除了每个类型扩大到自身之外）  
  
- [布尔值](../../../../visual-basic/language-reference/data-types/boolean-data-type.md)和任何数值类型之间的任意方向转换  
  
- 从任何数值类型到任何枚举类型的转换（`Enum`）  
  
- 在[字符串](../../../../visual-basic/language-reference/data-types/string-data-type.md)和任何数值类型、`Boolean` 或[日期](../../../../visual-basic/language-reference/data-types/date-data-type.md)之间的任意方向转换  
  
- 从数据类型或对象类型转换为派生自它的类型  
  
 收缩转换在运行时并不总是成功，可能会失败或导致数据丢失。 如果目标数据类型无法接收正在转换的值，则会发生错误。 例如，数字转换可能会导致溢出。 编译器不允许隐式执行收缩转换，除非[Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)将类型检查开关设置为 `Off`。  
  
> [!NOTE]
> 对于从 `For Each…Next` 集合中的元素到循环控制变量的转换，禁止转换收缩转换错误。 有关详细信息和示例，请参阅中的 "收缩转换" 一节[。下一语句](../../../../visual-basic/language-reference/statements/for-each-next-statement.md)。  
  
### <a name="when-to-use-narrowing-conversions"></a>何时使用收缩转换  
 如果知道源值可转换为目标数据类型，而不会出错或丢失数据，则可以使用收缩转换。 例如，如果你有一个已知包含 "True" 或 "False" 的 `String`，则可以使用 `CBool` 关键字将其转换为 `Boolean`。  
  
## <a name="exceptions-during-conversion"></a>转换过程中的异常  
 因为扩大转换始终会成功，所以它们不会引发异常。 收缩转换在失败时，通常会引发以下异常：  
  
- <xref:System.InvalidCastException>-如果在这两个类型之间未定义转换  
  
- <xref:System.OverflowException>-（仅整型）如果转换的值对于目标类型来说太大  
  
 如果某个类或结构定义了一个[CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md)，该函数将充当该类或结构的转换运算符，则该 `CType` 可能会引发它认为合适的任何异常。 此外，该 `CType` 可能会调用 Visual Basic 函数或 .NET Framework 方法，这反过来会引发各种异常。  
  
## <a name="changes-during-reference-type-conversions"></a>引用类型转换期间的更改  
 从*引用类型*进行的转换只复制指向值的指针。 值本身既不会进行复制，也不会更改。 唯一可以更改的是保存指针的变量的数据类型。 在下面的示例中，数据类型从派生类转换为其基类，但这两个变量现在指向的对象是不变的。  
  
```vb  
' Assume class cSquare inherits from class cShape.  
Dim shape As cShape  
Dim square As cSquare = New cSquare  
' The following statement performs a widening  
' conversion from a derived class to its base class.  
shape = square  
```  
  
## <a name="see-also"></a>请参阅

- [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)
- [Visual Basic 中的类型转换](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)
- [隐式转换和显式转换](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
- [字符串和其他类型之间的转换](../../../../visual-basic/programming-guide/language-features/data-types/conversions-between-strings-and-other-types.md)
- [如何：在 Visual Basic 中将对象转换为另一种类型](../../../../visual-basic/programming-guide/language-features/data-types/how-to-convert-an-object-to-another-type.md)
- [数组转换](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md)
- [数据类型](../../../../visual-basic/language-reference/data-types/index.md)
- [类型转换函数](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)
