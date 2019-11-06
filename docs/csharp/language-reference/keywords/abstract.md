---
title: abstract - C# 参考
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- abstract
- abstract_CSharpKeyword
helpviewer_keywords:
- abstract keyword [C#]
ms.assetid: b0797770-c1f3-4b4d-9441-b9122602a6bb
ms.openlocfilehash: a6c0ac86689c5d095fc077beb39d6281f77aab24
ms.sourcegitcommit: 14ad34f7c4564ee0f009acb8bfc0ea7af3bc9541
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/01/2019
ms.locfileid: "73422946"
---
# <a name="abstract-c-reference"></a>abstract（C# 参考）
`abstract` 修饰符指示被修饰内容的实现有缺省或不完整。 abstract 修饰符可用于类、方法、属性、索引和事件。 在类声明中使用 `abstract` 修饰符来指示某个类仅用作其他类的基类，而不用于自行进行实例化。 标记为`abstract`的成员必须由派生自抽象类的非抽象类来实现。
  
## <a name="example"></a>示例  
 在此示例中，类 `Square` 必须提供 `GetArea` 的实现，因为它派生自 `Shape`：  
  
 [!code-csharp[csrefKeywordsModifiers#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#1)]
  
 抽象类具有以下功能：  
  
- 抽象类不能实例化。  
  
- 抽象类可能包含抽象方法和访问器。  
  
- 无法使用 [sealed](./sealed.md) 修饰符来修改抽象类，因为两个修饰符的含义相反。 `sealed` 修饰符阻止类被继承，而 `abstract` 修饰符要求类被继承。  
  
- 派生自抽象类的非抽象类，必须包含全部已继承的抽象方法和访问器的实际实现。  
  
 在方法或属性声明中使用 `abstract` 修饰符，以指示该方法或属性不包含实现。  
  
 抽象方法具有以下功能：  
  
- 抽象方法是隐式的虚拟方法。  
  
- 只有抽象类中才允许抽象方法声明。  
  
- 由于抽象方法声明不提供实际的实现，因此没有方法主体；方法声明仅以分号结尾，且签名后没有大括号 ({ })。 例如:  
  
    ```csharp  
    public abstract void MyMethod();  
    ```  
  
     实现由方法 [override](./override.md) 提供，它是非抽象类的成员。  
  
- 在抽象方法声明中使用 [static](./static.md) 或 [virtual](./virtual.md) 修饰符是错误的。  
  
 除了声明和调用语法方面不同外，抽象属性的行为与抽象方法相似。  
  
- 在静态属性上使用 `abstract` 修饰符是错误的。  
  
- 通过包含使用 [override](./override.md) 修饰符的属性声明，可在派生类中重写抽象继承属性。  
  
 有关抽象类的详细信息，请参阅[抽象类、密封类及类成员](../../programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)。  
  
 抽象类必须为所有接口成员提供实现。  
  
 实现接口的抽象类有可能将接口方法映射到抽象方法上。 例如:  
  
[!code-csharp[csrefKeywordsModifiers#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#2)]
  
## <a name="example"></a>示例  
 在此示例中，类 `DerivedClass` 派生自抽象类 `BaseClass`。 抽象类包含抽象方法 `AbstractMethod`，以及两个抽象属性 `X` 和 `Y`。  
  
[!code-csharp[csrefKeywordsModifiers#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#3)]
  
 在前面的示例中，如果你尝试通过使用如下语句来实例化抽象类：  
  
```csharp
BaseClass bc = new BaseClass();   // Error  
```  
  
将遇到一个错误，告知编译器无法创建抽象类“BaseClass”的实例。  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [修饰符](index.md)
- [virtual](./virtual.md)
- [override](./override.md)
- [C# 关键字](./index.md)
