---
title: 从 .NET Framework 1.1 迁移
ms.date: 03/30/2017
helpviewer_keywords:
- .NET Framework 4.5, migrating from 1.1
- .NET Framework 1.1, migrating to .NET Framework 4.5
ms.assetid: 7ead0cb3-3b19-414a-8417-a1c1fa198d9e
ms.openlocfilehash: f74b75827770524299f9a25a5854503186139cb4
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73126292"
---
# <a name="migrating-from-the-net-framework-11"></a>从 .NET Framework 1.1 迁移

[!INCLUDE[win7](../../../includes/win7-md.md)] 及更高版本的 Windows 操作系统不支持 .NET Framework 1.1。 因此，面向 .NET Framework 1.1 的应用程序在未进行修改的情况下将不会在 [!INCLUDE[win7](../../../includes/win7-md.md)] 或更高版本的操作系统上运行。 本主题介绍了在 [!INCLUDE[win7](../../../includes/win7-md.md)] 及更高版本的 Windows 操作系统控制下运行面向 .NET Framework 1.1 的应用程序时需要执行的步骤。 有关 .NET Framework 1.1 和 [!INCLUDE[win8](../../../includes/win8-md.md)] 的详细信息，请参阅[在 Windows 8 及更高版本上运行 .NET Framework 1.1 应用](../install/run-net-framework-1-1-apps.md)。

## <a name="retargeting-or-recompiling"></a>重定目标或重新编译

可通过两种方式让使用 .NET Framework 1.1 编译的应用程序在 [!INCLUDE[win7](../../../includes/win7-md.md)] 或更高版本的 Windows 操作系统上运行：

- 你可以重定向应用程序以在 .NET Framework 4 及更高版本中运行。 重定向要求将 [\<supportedRuntime>](../configure-apps/file-schema/startup/supportedruntime-element.md) 元素添加到应用程序的配置文件中，以允许它在 .NET Framework 4 及更高版本中运行。 此配置文件采用以下形式：

    ```xml
    <configuration>
       <startup>
          <supportedRuntime version="v4.0"/>
       </startup>
    </configuration>
    ```

- 可以使用面向 .NET Framework 4 及更高版本的编译器重新编译应用程序。 如果你最初使用 Visual Studio 2003 开发和编译解决方案，则可在 Visual Studio 2010（也可能是更高版本）中打开它，然后使用“项目兼容性”  对话框将该解决方案和项目文件从 Visual Studio 2003 使用的格式转换为 Microsoft 生成引擎 (MSBuild) 格式。

无论您是想重新编译应用程序还是重定应用程序的目标，都必须确定应用程序是否会受更高版本的 .NET Framework 中引入的任何更改的影响。 这些更改分为两类：

- .NET Framework 1.1 与更高版本的 .NET Framework 之间存在的重大更改。

- .NET Framework 1.1 与更高版本的 .NET Framework 之间已标记为弃用或过时的类型和类型成员。

无论重定应用程序的目标还是重新编译应用程序，都应查看 .NET Framework 1.1 之后发布的各个版本的 .NET Framework 的重大更改和已过时类型和成员。

## <a name="breaking-changes"></a>重大更改

发生重大更改时，解决方法可能对重定目标的应用程序和重新编译的应用程序都可用，这取决于具体的更改。 在某些情况下，可以在应用程序配置文件的 [\<runtime>](../configure-apps/file-schema/startup/supportedruntime-element.md) 元素中添加子元素，从而还原旧行为。 例如，下面的配置文件将还原 .NET Framework 1.1 中使用的字符串排序和比较行为，可以将该文件与重定目标的应用程序或重新编译的应用程序一起使用。

```xml
<configuration>
   <runtime>
      <CompatSortNLSVersion enabled="4096"/>
   </runtime>
</configuration>
```

但某些情况下，您可能必须修改源代码和重新编译应用程序。

若要评估重大更改对应用程序产生的影响，您必须查看以下更改列表：

- [.NET Framework 2.0 中的重大更改](https://go.microsoft.com/fwlink/?LinkId=125263)记录了 .NET Framework 2.0 SP1 中会影响面向 .NET Framework 1.1 的应用程序的更改。

- [.NET Framework 3.5 SP1 中的更改](https://go.microsoft.com/fwlink/?LinkID=186989)记录了 .NET Framework 3.5 和 .NET Framework 3.5 SP1 之间的更改。

- [.NET Framework 4 迁移问题](net-framework-4-migration-issues.md)记录了 .NET Framework 3.5 SP1 和 .NET Framework 4 之间的更改。

## <a name="obsolete-types-and-members"></a>已过时的类型和成员

弃用的类型和成员对重定目标的应用程序和重新编译的应用程序产生的影响略有不同。 使用已过时的类型和成员将不会影响重定目标的应用程序，除非已从其程序集中物理删除这些过时的类型或成员。 重新编译使用过时的类型或成员的应用程序通常会产生编译器警告而不是编译器错误。 但某些情况下会产生编译器错误，且无法成功编译使用过时的类型或成员的代码。 在此情况下，你必须先重新编写调用过时的类型或成员的源代码，然后再重新编译应用程序。 若要详细了解已过时类型和成员，请参阅[类库中过时的内容](../whats-new/whats-obsolete.md)。

若要评估自发布 .NET Framework 2.0 SP1 后弃用的类型和成员的影响，请参阅[类库中过时的内容](../whats-new/whats-obsolete.md)。 请查看 .NET Framework 2.0 SP1、.NET Framework 3.5 和 .NET Framework 4 的过时类型和成员列表。
