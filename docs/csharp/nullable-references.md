---
title: 可为空引用类型
description: 本文概述了在 C# 8.0 中添加的可为空引用类型。 你将了解该功能如何为新项目和现有项目提供针对空引用异常的安全性。
ms.technology: csharp-null-safety
ms.date: 02/19/2019
ms.openlocfilehash: e20ea6efa389ba1aa0d8432a408c0b2a06a61c30
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2019
ms.locfileid: "73039769"
---
# <a name="nullable-reference-types"></a>可为空引用类型

C#8.0 引入了“可为空引用类型”和“不可为空引用类型”，使你能够对引用类型变量的属性作出重要声明   ：

- 引用不应为 null  。 当变量不应为 null 时，编译器会强制执行规则，以确保在不首先检查它们是否为 null 的情况下取消引用这些变量是安全的：
  - 必须将变量初始化为非 null 值。
  - 变量永远不能赋值为 `null`。
- 引用可为 null  。 当变量可以为 null 时，编译器会强制执行不同的规则以确保你已正确检查空引用：
  - 只有当编译器可以保证该值不为 null 时，才可以取消引用该变量。
  - 这些变量可以使用默认的 `null` 值进行初始化，也可以在其他代码中赋值为 `null`。

在 C# 的早期版本中，无法从变量声明中确定设计意图，与处理引用变量相比，这个新功能提供了显著的好处。 编译器不提供针对引用类型的空引用异常的安全性：

- 引用可为 null  。 将引用类型初始化为 null 或稍后将其指定为 null 时，编译器不会发出警告。
- 假定引用不为 null  。 当引用类型被取消引用时，编译器不会发出任何警告。 （使用可为空引用，只要取消引用可能为 null 的变量，编译器就会发出警告）。

通过添加可为空引用类型，你可以更清楚地声明你的意图。 `null` 值是表示变量不引用值的正确方法。 请勿使用此功能从代码中删除所有 `null` 值。 相反，应该向编译器和其他读取代码的开发人员声明你的意图。 通过声明意图，编译器会在你编写与该意图不一致的代码时通知你。

使用与[可为空值类型](programming-guide/nullable-types/index.md)相同的语法记录**可为空引用类型**：将 `?` 附加到变量的类型。 例如，以下变量声明表示可为空的字符串变量 `name`：

```csharp
string? name;
```

未将 `?` 附加到类型名称的任何变量都是“不可为空引用类型”  。 这包括启用此功能时现有代码中的所有引用类型变量。

编译器使用静态分析来确定可为空引用是否为非 null。 如果你在一个可为空引用可能是 null 时对其取消引用，编译器将向你发出警告。 可以通过使用 [NULL 包容运算符](language-reference/operators/null-forgiving.md) `!` 后跟变量名称来替代此行为。 例如，若知道 `name` 变量不为 null 但编译器仍发出警告，则可以编写以下代码来覆盖编译器的分析：

```csharp
name!.Length;
```

## <a name="nullability-of-types"></a>类型为 Null 性

任何引用类型都可以具有四个“为 Null 性”中的一个，它描述了何时生成警告  ：

- *不可为空*：无法将 null 分配给此类型的变量。 在取消引用之前，无需对此类型的变量进行 null 检查。
- *可为空*：可将 null 分配给此类型的变量。 在不首先检查 `null` 的情况下取消引用此类型的变量时发出警告。
- *无视*：这是 C# 8.0 之前版本的状态。 可以取消引用或分配此类型的变量而不发出警告。
- *未知*：这通常针对类型参数，约束不告知编译器类型是否必须是“可为空”或“不可为空”   。

变量声明中类型的为 Null 性由声明变量的“可为空上下文”控制  。

## <a name="nullable-contexts"></a>可为空上下文

可为空上下文可以对编译器如何解释引用类型变量进行精细控制。 可以启用或禁用任何给定源代码行的“可为空注释上下文”  。 可以将 C# 8.0 之前的编译器视为在禁用的可为空上下文中编译所有代码：任何引用类型都可以为空。 还可以启用或禁用可为空警告上下文  。 可为空警告上下文指定编译器使用其流分析生成的警告。

可以使用 .csproj 文件中的 `Nullable` 元素为项目设置可为空注释上下文和可为空警告上下文。  此元素配置编译器如何解释类型的为 Null 性以及生成哪些警告。 有效设置如下：

- `enable`：“启用”可为空注释上下文  。 “启用”可为空警告上下文  。
  - 引用类型的变量，例如 `string` 是“不可为空”。  启用所有为 Null 性警告。
- `warnings`：“禁用”可为空注释上下文  。 “启用”可为空警告上下文  。
  - 引用类型的变量是“无视”。 启用所有为 Null 性警告。
- `annotations`：“启用”可为空注释上下文  。 “禁用”可为空警告上下文  。
  - 引用类型的变量（例如字符串）不可为 null。 禁用所有为 Null 性警告。
- `disable`：“禁用”可为空注释上下文  。 “禁用”可为空警告上下文  。
  - 引用类型的变量是“无视”，就像早期版本的 C# 一样。 禁用所有为 Null 性警告。

**示例**：

```xml
<Nullable>enable</Nullable>
```

你还可以使用指令在项目的任何位置设置这些相同的上下文：

- `#nullable enable`：将可为空注释上下文和可为空警告上下文设置为“已启用”  。
- `#nullable disable`：将可为空注释上下文和可为空警告上下文设置为“已禁用”  。
- `#nullable restore`：将可为空注释上下文和可为空警告上下文还原到项目设置。
- `#nullable disable warnings`：将可为空警告上下文设置为“已禁用”  。
- `#nullable enable warnings`：将可为空警告上下文设置为“已启用”  。
- `#nullable restore warnings`：将可为空警告上下文还原到项目设置。
- `#nullable disable annotations`：将可为空注释上下文设置为“禁用”  。
- `#nullable enable annotations`：将可为空注释上下文设置为“启用”  。
- `#nullable restore annotations`：将注释警告上下文还原到项目设置。

默认情况下，可为空注释和警告上下文处于禁用状态  。 这意味着无需更改现有代码即可进行编译，并且不会生成任何新警告。

## <a name="nullable-annotation-context"></a>可为空注释上下文

编译器在已禁用的可为空注释上下文中使用以下规则：

- 不能在已禁用的上下文中声明可为空引用。
- 可以将所有引用变量分配为 null。
- 取消引用引用类型的变量时不会生成警告。
- 可能不会在禁用的上下文中使用 null 包容运算符。

该行为与以前版本的 C# 相同。

编译器在已启用的可为空注释上下文中使用以下规则：

- 引用类型的任何变量都是“不可为空引用”  。
- 任何不可为空引用都可以安全地取消引用。
- 任何可为空引用类型（在变量声明中的类型之后由 `?` 标记）可为 null。 静态分析确定在取消引用该值时是否已知该值不为 null。 否则，编译器会发出警告。
- 你可以使用 null 包容运算符声明可为空引用不为 null。

在已启用的可为空注释上下文中，附加到引用类型的 `?` 字符声明“可为空引用类型”  。 可将 NULL 包容运算符 `!` 附加到表达式以声明表达式不为 NULL  。

## <a name="nullable-warning-context"></a>可为空警告上下文

可为空警告上下文与可为空注释上下文不同。 即使禁用新注释，也可以启用警告。 编译器使用静态流分析来确定任何引用的“null 状态”  。 当“可为空警告上下文”未被“禁用”时，null 状态为“非 null”或“可能为 null”     。 如果在编译器确定引用“可能为 null”时取消引用该引用，编译器会向你发出警告  。 除非编译器可以确定以下两个条件之一，否则引用的状态为“可能为 null”  ：

1. 该变量已明确分配给非 null 值。
1. 在取消引用之前，已检查变量或表达式是否为 null。

当可为空警告上下文处于启用状态时，只要取消引用“可能为 null”状态的变量或表达式，编译器就会生成警告  。 此外，在将“可能为 null”变量或表达式分配给已启用的可为空注释上下文中的不可为空引用类型时，将生成警告  。

## <a name="see-also"></a>请参阅

- [可为空引用类型规范草案](~/_csharplang/proposals/csharp-8.0/nullable-reference-types-specification.md)
- [可为空引用教程简介](tutorials/nullable-reference-types.md)
- [将现有代码库迁移到可为空引用](tutorials/upgrade-to-nullable-references.md)
