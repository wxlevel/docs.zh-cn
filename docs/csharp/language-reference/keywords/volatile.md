---
title: volatile - C# 参考
ms.custom: seodec18
ms.date: 10/24/2018
f1_keywords:
- volatile_CSharpKeyword
- volatile
helpviewer_keywords:
- volatile keyword [C#]
ms.assetid: 78089bc7-7b38-4cfd-9e49-87ac036af009
ms.openlocfilehash: e72173ba1b91f03ccb1c15ca6451ac997666bc7f
ms.sourcegitcommit: 14ad34f7c4564ee0f009acb8bfc0ea7af3bc9541
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/01/2019
ms.locfileid: "73422131"
---
# <a name="volatile-c-reference"></a>volatile（C# 参考）

`volatile` 关键字指示一个字段可以由多个同时执行的线程修改。 出于性能原因，编译器，运行时系统甚至硬件都可能重新排列对存储器位置的读取和写入。 声明了 `volatile` 的字段不进行这些优化。 添加 `volatile` 修饰符可确保所有线程观察易失性写入操作（由任何其他线程执行）时的观察顺序与写入操作的执行顺序一致。 不确保从所有执行线程整体来看时所有易失性写入操作均按执行顺序排序。

`volatile` 关键字可应用于以下类型的字段：

- 引用类型。
- 指针类型（在不安全的上下文中）。 请注意，虽然指针本身可以是可变的，但是它指向的对象不能是可变的。 换句话说，不能声明“指向可变对象的指针”。
- 简单类型，如 `sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`char`、`float` 和 `bool`。
- 具有以下基本类型之一的 `enum` 类型：`byte`、`sbyte`、`short`、`ushort`、`int` 或 `uint`。
- 已知为引用类型的泛型类型参数。
- <xref:System.IntPtr> 和 <xref:System.UIntPtr>。

其他类型（包括 `double` 和 `long`）无法标记为 `volatile`，因为对这些类型的字段的读取和写入不能保证是原子的。 若要保护对这些类型字段的多线程访问，请使用 <xref:System.Threading.Interlocked> 类成员或使用 [`lock`](lock-statement.md) 语句保护访问权限。

`volatile` 关键字只能应用于 `class` 或 `struct` 的字段。 不能将局部变量声明为 `volatile`。

## <a name="example"></a>示例

下面的示例说明如何将公共字段变量声明为 `volatile`。

[!code-csharp[declareVolatile](~/samples/snippets/csharp/language-reference/keywords/volatile/Program.cs#Declaration)]

下面的示例演示如何创建辅助线程，并用它与主线程并行执行处理。 有关多线程处理的详细信息，请参阅[托管线程处理](../../../standard/threading/index.md)。

[!code-csharp[declareVolatile](~/samples/snippets/csharp/language-reference/keywords/volatile/Program.cs#Volatile)]

将 `volatile` 修饰符添加到 `_shouldStop` 的声明中，将始终获得相同的结果（类似于前面代码中显示的片段）。 但是，如果 `_shouldStop` 成员上没有该修饰符，则行为是不可预测的。 `DoWork` 方法可能会优化成员访问，从而导致读取陈旧数据。 鉴于多线程编程的性质，读取陈旧数据的次数是不可预测的。 不同的程序运行会产生一些不同的结果。

## <a name="c-language-specification"></a>C# 语言规范

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>请参阅

- [C# 语言规范：可变关键字](../../../../_csharplang/spec/classes.md#volatile-fields)
- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 关键字](index.md)
- [修饰符](index.md)
- [lock 语句](lock-statement.md)
- <xref:System.Threading.Interlocked>
