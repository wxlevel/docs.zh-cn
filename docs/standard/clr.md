---
title: 公共语言运行时 (CLR) 概述 - .NET Framework
ms.date: 04/02/2019
ms.technology: dotnet-standard
helpviewer_keywords:
- compiling source code, runtime functionality
- code, execution
- managed data
- runtime
- common language runtime
- metadata, runtime functionality
- .NET Framework, common language runtime
- language compilers
- managed code
- source code execution
- code, runtime functionality
ms.assetid: 059a624e-f7db-4134-ba9f-08b676050482
ms.custom: updateeachrelease
ms.openlocfilehash: c866e3d1a4de31361843f5c071510fd18247cb39
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73132815"
---
# <a name="common-language-runtime-clr-overview"></a>公共语言运行时 (CLR) 概述

.NET Framework 提供了一个称为公共语言运行时的运行时环境，它运行代码并提供使开发过程更轻松的服务。

公共语言运行时的功能通过编译器和工具公开，你可以编写利用此托管执行环境的代码。 使用基于公共语言运行时的语言编译器开发的代码称为托管代码；托管代码具有许多优点，例如：跨语言集成、跨语言异常处理、增强的安全性、版本控制和部署支持、简化的组件交互模型、调试和分析服务等。

> [!NOTE]
> 编译器和工具可以产生公共语言运行时可以使用的输出，因为类型系统、元数据格式和该运行时环境（虚拟执行系统）都由公共标准（ECMA 公共语言基础结构规范）定义。 有关详细信息，请参阅 [ECMA C# 和公共语言基础结构规范](https://visualstudio.microsoft.com/license-terms/ecma-c-common-language-infrastructure-standards/)。

若要使公共语言运行时能够向托管代码提供服务，语言编译器必须生成一些元数据来描述代码中的类型、成员和引用。 元数据与代码一起存储；每个可加载的公共语言运行时可迁移执行 (PE) 文件都包含元数据。 公共语言运行时使用元数据来完成以下任务：查找和加载类，在内存中安排实例，解析方法调用，生成本机代码，强制安全性，以及设置运行时上下文边界。

公共语言运行时自动处理对象布局并管理对象引用，当不再使用对象时释放它们。 按这种方式实现生存期管理的对象称为托管数据。 垃圾回收消除了内存泄漏以及其他一些常见的编程错误。 如果你编写的代码是托管代码，则可以在 .NET Framework 应用程序中使用托管数据、非托管数据或者同时使用这两种数据。 由于语言编译器会提供自己的类型（如基元类型），因此你可能并不总是知道（或需要知道）这些数据是否是托管的。

有了公共语言运行时，就可以很容易地设计出对象能够跨语言交互的组件和应用程序。 也就是说，用不同语言编写的对象可以互相通信，并且它们的行为可以紧密集成。 例如，可以定义一个类，然后使用不同的语言从原始类派生出另一个类或调用原始类的方法。 还可以将一个类的实例传递到用不同的语言编写的另一个类的方法。 这种跨语言集成之所以成为可能，是因为基于公共语言运行时的语言编译器和工具使用由公共语言运行时定义的常规类型系统，而且它们遵循公共语言运行时关于定义新类型以及创建、使用、保持和绑定到类型的规则。

所有托管组件都带有生成它们所基于的组件和资源的信息，这些信息构成了元数据的一部分。 公共语言运行时使用这些信息确保组件或应用程序具有它需要的所有内容的指定版本，这样就使代码不太可能由于某些未满足的依赖项而发生中断。 注册信息和状态数据不再保存在注册表中（因为在注册表中建立和维护这些信息很困难）。 取而代之的是，有关你定义的类型（及其依赖项）的信息作为元数据与代码存储在一起，这样大大降低了组件复制和移除任务的复杂性。

语言编译器和工具公开公共语言运行时的功能的方式对于开发人员来说不仅很有用，而且很直观。 这意味着，公共语言运行时的某些功能可能在一个环境中比在另一个环境中更突出。 你对公共语言运行时的体验取决于所使用的语言编译器或工具。 例如，如果你是一位 Visual Basic 开发人员，你可能会注意到：有了公共语言运行时，Visual Basic 语言的面向对象的功能比以前多了。 运行时提供如下优点：

- 性能得到了改进。

- 能够轻松使用用其他语言开发的组件。

- 类库提供的可扩展类型。

- 语言功能，如面向对象的编程的继承、接口和重载。

- 允许创建多线程的可缩放应用程序的显式自由线程处理支持。

- 结构化异常处理支持。

- 自定义特性支持。

- 垃圾回收。

- 使用委托取代函数指针，从而增强了类型安全和安全性。 有关委派的详细信息，请参阅[通用类型系统](../../docs/standard/base-types/common-type-system.md)。

## <a name="clr-versions"></a>CLR 版本

.NET Framework 的版本号无需对应于它所包含的 CLR 的版本号。 下表演示了两个版本号关联的方式：

|.NET Framework 版本|包括 CLR 版本|
|----------------------------|--------------------------|
|1.0|1.0|
|1.1|1.1|
|2.0|2.0|
|3.0|2.0|
|3.5|2.0|
|4|4|
|4.5（包括 4.5.1 和 4.5.2）|4|
|4.6（包括 4.6.1 和 4.6.2）|4|
|4.7（包括 4.7.1 和 4.7.2）|4|
|4.8|4|

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[托管执行过程](managed-execution-process.md)|描述使用公共语言运行时所需要的步骤。|
|[自动内存管理](automatic-memory-management.md)|描述垃圾回收器如何分配和释放内存。|
|[.NET Framework 概述](../framework/get-started/overview.md)|描述关键的 .NET Framework 概念，例如通用类型系统、跨语言互操作性、托管执行、应用程序域和程序集。|
|[常规类型系统](./base-types/common-type-system.md)|描述在运行时中如何声明、使用和管理类型以支持跨语言集成。|

## <a name="see-also"></a>请参阅

- [版本和依赖关系](../framework/migration-guide/versions-and-dependencies.md)
