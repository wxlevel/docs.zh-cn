---
title: 非托管类型 - C# 参考
ms.date: 09/06/2019
helpviewer_keywords:
- unmanaged type [C#]
ms.openlocfilehash: 25aa42ba8c8f0023b4f818feb2edbb325f805fb6
ms.sourcegitcommit: c70542d02736e082e8dac67dad922c19249a8893
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2019
ms.locfileid: "70374115"
---
# <a name="unmanaged-types-c-reference"></a>非托管类型（C# 参考）

如果某个类型是以下类型之一，则它是非托管类型  ：

- `sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、`float`、`double`、`decimal` 或 `bool`
- 任何[枚举](../keywords/enum.md)类型
- 任何[指针](../../programming-guide/unsafe-code-pointers/pointer-types.md)类型
- 任何用户定义的 [struct](../keywords/struct.md) 类型，只包含非托管类型的字段，并且在 C# 7.3 及更早版本中，不是构造类型（包含至少一个类型参数的类型）

从 C# 7.3 开始，可使用 [`unmanaged` 约束](../../programming-guide/generics/constraints-on-type-parameters.md#unmanaged-constraint)指定：类型参数为“非指针非托管类型”。

从 C# 8.0 开始，仅包含非托管类型的字段的*构造*结构类型也是非托管类型，如以下示例所示：

[!code-csharp[unmanaged constructed types](~/samples/csharp/language-reference/builtin-types/UnmanagedTypes.cs#ProgramExample)]

泛型结构可以是非托管类型的源，也可以是不是非托管构造类型的源。 前面的示例定义一个泛型结构 `Coords<T>`，并提供非托管构造类型的示例。 不是非托管类型情况的示例是 `Coords<object>`。 它不是非托管性质，因为它具有不是非托管性质的 `object` 类型的字段。 如果你希望所有  构造类型都是非托管类型，请在泛型结构的定义中使用 `unmanaged` 约束：

[!code-csharp[unmanaged constraint in type definition](~/samples/csharp/language-reference/builtin-types/UnmanagedTypes.cs#AlwaysUnmanaged)]

## <a name="c-language-specification"></a>C# 语言规范

有关详细信息，请参阅 [C# 语言规范](~/_csharplang/spec/introduction.md)的[指针类型](~/_csharplang/spec/unsafe-code.md#pointer-types)部分。

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [指针类型](../../programming-guide/unsafe-code-pointers/pointer-types.md)
- [内存和跨度相关类型](../../../standard/memory-and-spans/index.md)
- [sizeof 运算符](../operators/sizeof.md)
- [stackalloc 运算符](../operators/stackalloc.md)
