---
title: 演练：在 WPF 中承载 Windows 窗体控件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hosting Windows Forms control in WPF [WPF]
ms.assetid: 9cb88415-39b0-4c46-80c4-ff325b674286
ms.openlocfilehash: 3cd01126e22927151f3c7fb08726c006c710dd34
ms.sourcegitcommit: 5a28f8eb071fcc09b045b0c4ae4b96898673192e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73197921"
---
# <a name="walkthrough-hosting-a-windows-forms-control-in-wpf"></a>演练：在 WPF 中承载 Windows 窗体控件

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了许多具有丰富功能集的控件。 但是，有时您可能希望在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 页上使用 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 控件。 例如，您可能在现有 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 控件中有大量投资，或者您可能有一个提供独特功能的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 控件。

本演练演示如何使用代码在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 页上承载 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] <xref:System.Windows.Forms.MaskedTextBox?displayProperty=nameWithType> 控件。

有关本演练中所示任务的完整代码列表，请参阅[在 WPF 中承载 Windows 窗体控件示例](https://go.microsoft.com/fwlink/?LinkID=160057)。

## <a name="prerequisites"></a>Prerequisites

若要完成本演练，必须具有 Visual Studio。

## <a name="hosting-the-windows-forms-control"></a>承载 Windows 窗体控件

### <a name="to-host-the-maskedtextbox-control"></a>承载 MaskedTextBox 控件

1. 创建一个名为 `HostingWfInWpf`的 WPF 应用程序项目。

2. 添加对下列程序集的引用。

    - WindowsFormsIntegration

    - System.Windows.Forms

3. 在 [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)]中打开 Mainwindow.xaml。

4. 将 <xref:System.Windows.Controls.Grid> 元素命名为 `grid1`。

     [!code-xaml[HostingWfInWPF#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingWfInWPF/CSharp/HostingWfInWPF/Window1.xaml#1)]

5. 在设计视图或 XAML 视图中，选择 <xref:System.Windows.Window> 元素。

6. 在属性窗口中，单击 "**事件**" 选项卡。

7. 双击 "<xref:System.Windows.FrameworkElement.Loaded>" 事件。

8. 插入以下代码来处理 <xref:System.Windows.FrameworkElement.Loaded> 事件。

     [!code-csharp[HostingWfInWPF#10](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingWfInWPF/CSharp/HostingWfInWPF/Window1.xaml.cs#10)]
     [!code-vb[HostingWfInWPF#10](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HostingWfInWPF/VisualBasic/HostingWfInWpf/Window1.xaml.vb#10)]

9. 在该文件的顶部，添加以下 `Imports` 或 `using` 语句。

     [!code-csharp[HostingWfInWPF#11](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingWfInWPF/CSharp/HostingWfInWPF/Window1.xaml.cs#11)]
     [!code-vb[HostingWfInWPF#11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HostingWfInWPF/VisualBasic/HostingWfInWpf/Window1.xaml.vb#11)]

10. 按 F5 生成并运行该应用程序。

## <a name="see-also"></a>请参阅

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [在 Visual Studio 中设计 XAML](/visualstudio/xaml-tools/designing-xaml-in-visual-studio)
- [演练：使用 XAML 在 WPF 中托管 Windows 窗体控件](walkthrough-hosting-a-windows-forms-control-in-wpf-by-using-xaml.md)
- [演练：在 WPF 中托管 Windows 窗体复合控件](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
- [演练：在 Windows 窗体中承载 WPF 复合控件](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
- [Windows 窗体控件和等效的 WPF 控件](windows-forms-controls-and-equivalent-wpf-controls.md)
- [在 WPF 示例中承载 Windows 窗体控件](https://go.microsoft.com/fwlink/?LinkID=160057)
