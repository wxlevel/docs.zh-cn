---
title: 在 UI 自动化提供程序中支持控件模式
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- control patterns, supporting in UI Automation provider
- UI Automation, supporting control patterns in provider
ms.assetid: 0d635c35-ffa8-4dc8-bbc9-12fcd5445776
ms.openlocfilehash: 67f37dfe1fe63f2130646cb227fec855ccc7bf75
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2019
ms.locfileid: "71042593"
---
# <a name="support-control-patterns-in-a-ui-automation-provider"></a>在 UI 自动化提供程序中支持控件模式

> [!NOTE]
> 本文档适用于想要使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 命名空间中定义的托管 <xref:System.Windows.Automation> 类的 .NET Framework 开发人员。 有关的最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], 请[参阅 Windows 自动化 API:UI 自动化](https://go.microsoft.com/fwlink/?LinkID=156746)。

本主题演示如何在 UI 自动化提供程序上实现一个或多个控件模式，以便客户端应用程序可以操作控件并从中获取数据。

## <a name="support-control-patterns"></a>支持控件模式

1. 为元素应支持的控件模式实现相应的接口，例如为 为 <xref:System.Windows.Automation.Provider.IInvokeProvider> 实现 <xref:System.Windows.Automation.InvokePattern>。

2. 返回包含 <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.GetPatternProvider%2A?displayProperty=nameWithType>实现中每个控件接口的实现的对象

## <a name="example"></a>示例

下面的示例演示了对单项选择自定义列表框实现 <xref:System.Windows.Automation.Provider.ISelectionProvider> 。 它返回三个属性并获取当前所选的项。

[!code-csharp[UIAFragmentProvider_snip#119](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAFragmentProvider_snip/CSharp/ListPattern.cs#119)]
[!code-vb[UIAFragmentProvider_snip#119](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAFragmentProvider_snip/VisualBasic/ListPattern.vb#119)]

## <a name="example"></a>示例

下面的示例演示了返回实现 <xref:System.Windows.Automation.Provider.IRawElementProviderSimple.GetPatternProvider%2A> 的类的 <xref:System.Windows.Automation.Provider.ISelectionProvider>的实现。 大多数列表框控件还支持其他模式，但在此示例中，为所有其他模式`Nothing`标识符返回了 null 引用（在 Microsoft Visual Basic .net 中）。

[!code-csharp[UIAFragmentProvider_snip#120](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAFragmentProvider_snip/CSharp/ListFragment.cs#120)]
[!code-vb[UIAFragmentProvider_snip#120](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAFragmentProvider_snip/VisualBasic/ListFragment.vb#120)]

## <a name="see-also"></a>请参阅

- [UI 自动化提供程序概述](ui-automation-providers-overview.md)
- [服务器端 UI 自动化提供程序实现](server-side-ui-automation-provider-implementation.md)
