---
ms.openlocfilehash: d35de48dd22003c851cf5dba9e8517ec48b9217b
ms.sourcegitcommit: 5a28f8eb071fcc09b045b0c4ae4b96898673192e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73198353"
---
### <a name="c-locale-maps-to-the-invariant-locale"></a>“C”区域设置映射到固定区域设置

.NET Core 2.2 及更早版本依赖于默认 ICU 行为，该行为将“C”区域设置映射到 en_US_POSIX 区域设置。 En_US_POSIX 区域设置的排序行为并不可取，因为它不支持不区分大小写的字符串比较。 用户会遇到意外行为是因为部分 Linux 分发版将“C”区域设置设置为了默认区域设置。

#### <a name="change-description"></a>更改描述

从 .NET Core 3.0 开始，“C”区域设置映射已更改为使用固定区域设置，而不是 en_US_POSIX。 “C”区域设置到固定的映射还应用于 Windows，以实现一致性。

将“C”映射到 en_US_POSIX 区域性会导致客户混乱，因为 en_US_POSIX 不支持不区分大小写的字符串排序/搜索操作。 由于“C”区域设置用作部分 Linux 分发版中的默认区域设置，因此客户在这些操作系统上会遭遇此类不良行为。

#### <a name="version-introduced"></a>引入的版本

3.0

### <a name="recommended-action"></a>建议的操作

除了解此变更外，没有什么特别之处需要注意。 此变更仅影响使用“C”本地映射的应用程序。

### <a name="category"></a>类别

全球化

### <a name="affected-apis"></a>受影响的 API

所有排序规则和区域性 API 都会受到此变更的影响。

<!--

-->
