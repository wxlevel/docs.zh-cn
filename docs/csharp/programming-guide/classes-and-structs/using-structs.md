---
title: 使用 struct - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- structs [C#], using
ms.assetid: cea4a459-9eb9-442b-8d08-490e0797ba38
ms.openlocfilehash: 8b2810af81a57cf21b9a2e2438f7f6aa2cb7a669
ms.sourcegitcommit: 559259da2738a7b33a46c0130e51d336091c2097
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72772073"
---
# <a name="using-structs-c-programming-guide"></a>使用结构（C# 编程指南）

`struct` 类型适用于表示轻量级对象，如 `Point`、 `Rectangle`和 `Color`。 尽管用它来表示一个点就如同具有 [Auto-Implemented Properties（自动实现的属性）](../../language-reference/keywords/class.md) 的 [类](./auto-implemented-properties.md)那样方便，但在某些情况下，使用 [结构](../../language-reference/keywords/struct.md) 可能更高效。 例如，如果你声明具有 1000 个 `Point` 对象的数组，那么你将分配额外的内存用于引用每个对象；在这种情况下，使用结构将更为便宜。 因为 .NET Framework 包含一个名为 <xref:System.Drawing.Point> 的对象，所以本示例中的结构名称为 `Coords`。

[!code-csharp[csProgGuideObjects#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#1)]

为结构定义无参数构造函数是错误的。 在结构体中初始化实例字段也是错误的。 只能通过使用参数化构造函数、隐式、无参数构造函数、[对象初始值设定项](object-and-collection-initializers.md)或在声明结构后单独访问成员来初始化外部可访问的结构成员。 任何私有或其他不可访问的成员需要以独占方式使用构造函数。

使用 [new](../../language-reference/operators/new-operator.md) 运算符创建结构对象时，会创建结构对象且会遵循[构造函数签名](constructors.md#constructor-syntax)来调用相应的构造函数。 与类不同，可以对结构进行实例化，而无需使用 `new` 运算符。 在这种情况下，没有调用任何构造函数，从而提高了分配效率。 但是，字段将保持为未分配状态且必须在在初始化所有字段之后才可使用对象。 这包括无法通过属性获取或设置值。

如果使用无参数构造函数实例化结构对象，则根据成员的[默认值](../../language-reference/keywords/default-values-table.md)分配所有成员。

为结构编写带有参数的构造函数时，必须显式初始化所有成员，否则一个或多个成员将保持未分配状态，并且无法使用该结构，从而生成编译器错误 [CS0171](../../misc/cs0171.md)。

由于全都是用于类的继承，因此没有用于结构的继承。 一个结构无法继承自另一个结构或类，并且它不能为类的基类。 但是，它可以从基类 <xref:System.Object>继承。 结构也可以实现接口，且实现方法与类相同。

不能使用关键字 `struct`声明一个类。 在 C# 中，类和结构在语义上是不同的。 结构是值类型，而类是引用类型。 有关详细信息，请参阅[值类型](../../language-reference/keywords/value-types.md)和[引用类型](../../language-reference/keywords/reference-types.md)。

除非需要引用类型语义，将较小的类声明为结构，可以提高系统的处理效率。

## <a name="example-1"></a>示例 1

此示例同时使用了无参数构造函数和参数化构造函数来演示 `struct` 初始化。

[!code-csharp[csProgGuideObjects#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#1)]

[!code-csharp[csProgGuideObjects#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#2)]

## <a name="example-2"></a>示例 2

此示例演示了一个特定于结构的功能。 此功能可以创建 Coords 对象，而无需使用 `new` 运算符。 如果将 `struct` 替换为 `class`，程序将不会进行编译。

[!code-csharp[csProgGuideObjects#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#1)]

[!code-csharp[csProgGuideObjects#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#3)]

## <a name="see-also"></a>请参阅

- [C# 编程指南](../index.md)
- [类和结构](index.md)
- [结构](structs.md)
