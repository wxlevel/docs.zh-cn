---
title: 版本 2.2 到 3.0 的加密中断性变更 - .NET Core
description: 列出 .NET Core、ASP.NET Core 和 EF Core 的版本 2.2 到 3.0 的中断性变更。
ms.date: 09/10/2019
ms.openlocfilehash: ba330bdef4be8cfe0e74f5645adaf66b2e0051ac
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73089586"
---
# <a name="breaking-changes-for-migration-from-version-22-to-30"></a>从版本 2.2 迁移到 3.0 的中断性变更

> [!IMPORTANT]
> 本文正在构建中。 这并不是 .NET Core 中断性变更的完整列表。 如需详细了解 .NET Core 重大变更，请参阅 GitHub 上 dotnet/docs 存储库中的各个[重大变更问题](https://github.com/dotnet/docs/issues?q=is%3Aissue+is%3Aopen+label%3Abreaking-change)。 

若要从 .NET Core、ASP.NET Core 或 EF Core 的版本 2.2 迁移至 3.0，请参阅以下主题，了解可能影响应用的中断性变更：

## <a name="corefx"></a>CoreFx

[!INCLUDE[APIs that report version now report product and not file version](~/includes/core-changes/corefx/version-information-changes.md)]

***

[!INCLUDE[Custom EncoderFallbackBuffer instances cannot fall back recursively](~/includes/core-changes/corefx/custom-encoderfallbackbuffer-cannot-be-recursive.md)]

***

[!INCLUDE[Floating point formatting and parsing behavior changes](~/includes/core-changes/corefx/floating-point-changes.md)]

***

[!INCLUDE[InvalidAsynchronousStateException moved to another assembly](~/includes/core-changes/corefx/move-invalidasynchronousstateexception.md)]

***

[!INCLUDE[NET Core 3.0 follows Unicode best practices when replacing ill-formed UTF-8 byte sequences](~/includes/core-changes/corefx/net-core-3-0-follows-unicode-utf8-best-practices.md)]

***

[!INCLUDE[TypeDescriptionProviderAttribute moved to another assembly](~/includes/core-changes/corefx/move-typedescriptionproviderattribute.md)]

***

[!INCLUDE[ZipArchiveEntry no longer handles archives with inconsistent entry sizes](~/includes/core-changes/corefx/ziparchiveentry-and-inconsistent-entry-sizes.md)]

## <a name="cryptography"></a>密码

[!INCLUDE[EnvelopedCms defaults to AES-256 encryption](~/includes/core-changes/cryptography/envelopedcms-defaults-to-aes256.md)]

***

[!INCLUDE[Minimum size for RSAOpenSsl key generation has increased](~/includes/core-changes/cryptography/minimum-rsaopenssl-key-size-change.md)]

***

[!INCLUDE[.NET Core 3.0 prefers OpenSSL 1.1.x to OpenSSL 1.0.x](~/includes/core-changes/cryptography/net-core-3-0-prefers-openssl-1-1-x.md)]

## <a name="globalization"></a>全球化

[!INCLUDE["C" locale maps to the invariant locale](~/includes/core-changes/globalization/c-locale-maps-to-invariant-locale.md)]

## <a name="visual-basic"></a>Visual Basic

[!INCLUDE[vbNewLine is obsolete](~/includes/core-changes/visualbasic/vbnewline-is-obsolete.md)]

## <a name="entity-framework-core"></a>Entity Framework Core

[Entity Framework Core 重大变更](/ef/core/what-is-new/ef-core-3.0/breaking-changes)
