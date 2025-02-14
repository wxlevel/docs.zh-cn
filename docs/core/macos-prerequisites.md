---
title: Mac 上 .NET Core 的先决条件
description: 在 macOS 计算机上开发、部署和运行 .NET Core 应用程序所支持的 macOS 版本和 .NET Core 依赖项。
author: thraka
ms.author: adegeo
ms.custom: updateeachvsrelease
ms.date: 10/11/2019
ms.openlocfilehash: 2d4fc0b37be08988440325db8b507124c36bf053
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72318315"
---
# <a name="prerequisites-for-net-core-on-macos"></a>macOS 上 .NET Core 的先决条件

本文介绍了在 macOS 计算机上开发、部署和运行 .NET Core 应用程序所需的受支持的 macOS 版本和 .NET Core 依赖项。 支持的操作系统版本和随附的依赖项适用于在 Mac 上开发 .NET Core 应用的三种方法：[结合使用常用编辑器和命令行](tutorials/using-with-xplat-cli.md)、[Visual Studio Code](https://code.visualstudio.com/) 和 [Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)。

## <a name="downloads-and-dependencies"></a>下载和依赖项

<!-- markdownlint-disable MD025 -->

# <a name="net-core-30tabnetcore30"></a>[.NET Core 3.0](#tab/netcore30)

.NET Core 3.0 在 macOS High Sierra（版本 10.13）及更高版本上受支持  。 需要 x64 CPU 体系结构  。

从 [.NET Core 3.0 下载](https://dotnet.microsoft.com/download/dotnet-core/3.0)页面下载并安装 .NET Core SDK。 要在完整列表中了解 .NET Core 3.0 支持的操作系统、发行版本和版本、生命周期策略链接和不支持的 OS 版本，请参阅 [.NET Core 3.0 支持的 OS 版本](https://github.com/dotnet/core/blob/master/release-notes/3.0/3.0-supported-os.md)。

有关已知问题的列表，请参阅 [.NET Core 已知问题](https://github.com/dotnet/core/blob/master/release-notes/3.0/3.0-known-issues.md)。

# <a name="net-core-22tabnetcore22"></a>[.NET Core 2.2](#tab/netcore22)

.NET Core 2.2 在 macOS Sierra（版本 10.12）及更高版本上受支持  。 需要 x64 CPU 体系结构  。

从 [ .NET Core 2.2 下载](https://dotnet.microsoft.com/download/dotnet-core/2.2)页面下载并安装 .NET Core SDK。 要在完整列表中了解 .NET Core 2.2 支持的操作系统、发行版本和版本、生命周期策略链接和不支持的 OS 版本，请参阅 [.NET Core 2.2 支持的 OS 版本](https://github.com/dotnet/core/blob/master/release-notes/2.2/2.2-supported-os.md)。

有关已知问题的列表，请参阅 [.NET Core 已知问题](https://github.com/dotnet/core/blob/master/release-notes/2.2/2.2-known-issues.md)。

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

.NET Core 2.1 在 macOS Sierra（版本 10.12）及更高版本上受支持  。 需要 x64 CPU 体系结构  。

从 [.NET Core 2.1 下载](https://dotnet.microsoft.com/download/dotnet-core/2.1)页面下载并安装 .NET Core SDK。 要在完整列表中了解 .NET Core 2.1 支持的操作系统、发行版本和版本、生命周期策略链接和不支持的 OS 版本，请参阅 [.NET Core 2.1 支持的 OS 版本](https://github.com/dotnet/core/blob/master/release-notes/2.1/2.1-supported-os.md)。

有关已知问题的列表，请参阅 [.NET Core 已知问题](https://github.com/dotnet/core/blob/master/release-notes/2.1/2.1-known-issues.md)。

---

## <a name="libgdiplus"></a>libgdiplus

使用 System.Drawing.Common  程序集的 .NET Core 应用程序要求安装 libgdiplus。

获取 libgdiplus 的一个简单方法是使用适用于 macOS 的 [Homebrew (“brew”)](https://brew.sh/) 包。 在安装 brew 后，通过在终端（命令）提示符处执行以下命令来安装 libgdiplus  ：

```console
brew update
brew install libgdiplus
```

## <a name="visual-studio-for-mac"></a>Visual Studio for Mac

可以使用任何编辑器，通过 .NET Core SDK 开发 .NET Core 应用程序。 但是，若要在集成的开发环境中的 Mac 上开发 .NET Core 应用程序，可以使用 [Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)。
