---
title: WPF 中的双向功能概述
ms.date: 03/30/2017
helpviewer_keywords:
- Span elements [WPF]
- bidirectional features [WPF]
ms.assetid: fd850e25-7dba-408c-b521-8873e51dc968
ms.openlocfilehash: 7d648741676ba947d901d26e3ee7c1289d3d4bc3
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2019
ms.locfileid: "73453874"
---
# <a name="bidirectional-features-in-wpf-overview"></a>WPF 中的双向功能概述

与任何其他开发平台不同，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 具有许多功能，这些功能支持快速开发双向内容，例如，在同一文档中从左到右和向左的数据进行混合。 同时，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 为需要双向功能（如阿拉伯语和希伯来语用户）的用户创建了绝佳的体验。

以下各节结合一些示例阐释了如何获得双向内容的最佳显示效果，并对许多双向功能进行了说明。 大多数示例都使用 XAML，但你可以轻松地将概念应用于C#或 Microsoft Visual Basic 代码。

<a name="FlowDirection"></a>

## <a name="flowdirection"></a>FlowDirection

在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序中定义内容流方向的基本属性是 <xref:System.Windows.FrameworkElement.FlowDirection%2A>的。 此属性可设置为以下两个枚举值之一： <xref:System.Windows.FlowDirection.LeftToRight> 或 <xref:System.Windows.FlowDirection.RightToLeft>。 属性可用于从 <xref:System.Windows.FrameworkElement>继承的所有 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素。

下面的示例设置 <xref:System.Windows.Controls.TextBox> 元素的流动方向。

**从左向右的流方向**

[!code-xaml[LTRRTL#LTR](~/samples/snippets/csharp/VS_Snippets_Wpf/LTRRTL/CS/Pane1.xaml#ltr)]

**从右向左的流方向**

[!code-xaml[LTRRTL#RTL](~/samples/snippets/csharp/VS_Snippets_Wpf/LTRRTL/CS/Pane1.xaml#rtl)]

下图显示了前面代码的呈现方式。

![说明不同流方向的图形。](./media/bidirectional-features-in-wpf-overview/left-right-right-left.png)

[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 树中的元素将从其容器继承 <xref:System.Windows.FrameworkElement.FlowDirection%2A>。 在下面的示例中，<xref:System.Windows.Controls.TextBlock> 在 <xref:System.Windows.Controls.Grid> 中，后者驻留在 <xref:System.Windows.Window> 中。 设置 <xref:System.Windows.Window> 的 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 意味着也将其设置为 <xref:System.Windows.Controls.Grid> 和 <xref:System.Windows.Controls.TextBlock>。

下面的示例演示如何设置 <xref:System.Windows.FrameworkElement.FlowDirection%2A>。

[!code-xaml[FlowDirection#FlowDirection](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDirection/CS/Window1.xaml#flowdirection)]

顶层 <xref:System.Windows.Window> 具有 <xref:System.Windows.FlowDirection.RightToLeft><xref:System.Windows.FlowDirection>，因此其中包含的所有元素也继承同一个 <xref:System.Windows.FrameworkElement.FlowDirection%2A>。 若要使元素重写指定的 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 它必须添加显式方向更改，如上一个示例中的第二个 <xref:System.Windows.Controls.TextBlock> 更改为 <xref:System.Windows.FlowDirection.LeftToRight>。 未定义 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 时，将应用默认 <xref:System.Windows.FlowDirection.LeftToRight>。

下图显示了上一示例的输出：

![阐释显式流方向更改的图形。](./media/bidirectional-features-in-wpf-overview/explicit-direction-change.png)

<a name="FlowDocument"></a>

## <a name="flowdocument"></a>FlowDocument

许多开发平台（如 HTML、[!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 和 Java）都为双向内容开发提供特殊支持。 标记语言（如 HTML）向内容编写人员提供必要的标记，以在任何所需方向显示文本，例如 HTML 4.0 标记、以 "rtl" 或 "ltr" 作为值的 "dir"。 此标记类似于 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 属性，但 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 属性的工作方式更高级，可用于布局文本内容并可用于文本以外的内容。

在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]中，<xref:System.Windows.Documents.FlowDocument> 是一种通用的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素，它可以托管文本、表、图像和其他元素的组合。 以下各节中的示例均使用此元素。

将文本添加到 <xref:System.Windows.Documents.FlowDocument> 可以通过一种方式进行更多操作。 实现此目的的一种简单方法是使用 <xref:System.Windows.Documents.Paragraph>，它是用于对文本等内容进行分组的块级别元素。 若要将文本添加到内联级别元素，示例使用 <xref:System.Windows.Documents.Span> 和 <xref:System.Windows.Documents.Run>。 <xref:System.Windows.Documents.Span> 是一种内联级别的流内容元素，用于对其他内联元素进行分组，而 <xref:System.Windows.Documents.Run> 是旨在包含非格式化文本运行的内联级别流内容元素。 <xref:System.Windows.Documents.Span> 可以包含多个 <xref:System.Windows.Documents.Run> 元素。

第一个文档示例包含具有多个网络共享名称的文档;例如 `\\server1\folder\file.ext`。 无论此网络链接是包含在阿拉伯语文档还是英语文档中，建议始终以相同的方式显示它。 下图演示了如何使用 Span 元素并显示了阿拉伯语 <xref:System.Windows.FlowDirection.RightToLeft> 文档中的链接：

![使用 Span 元素阐释的图形。](./media/bidirectional-features-in-wpf-overview/flow-direction-span-element.png "FlowDocument")

因为文本是 <xref:System.Windows.FlowDirection.RightToLeft> 的，所以所有特殊字符（如 "\\"）都将文本从右到左的顺序分开。 这会导致链接不按正确的顺序显示，因此，若要解决此问题，必须嵌入文本以保持单独 <xref:System.Windows.Documents.Run> 流动 <xref:System.Windows.FlowDirection.LeftToRight>。 若要解决此问题，一种更好的方法是将不常使用的英语文本嵌入更大的阿拉伯语 <xref:System.Windows.Documents.Span>，而不是为每种语言都单独 <xref:System.Windows.Documents.Run>。

下图通过使用在 Span 元素中嵌入的 Run 元素说明了这一点：

![说明嵌入到 Span 元素中的 Run 元素的图形。](./media/bidirectional-features-in-wpf-overview/embedded-span-element.png)

下面的示例演示如何在文档中使用 <xref:System.Windows.Documents.Run> 和 <xref:System.Windows.Documents.Span> 元素。

[!code-xaml[RunSpan#RunSpan](~/samples/snippets/csharp/VS_Snippets_Wpf/RunSpan/CS/Window1.xaml#runspan)]

<a name="SpanElements"></a>

## <a name="span-elements"></a>Span 元素

<xref:System.Windows.Documents.Span> 元素作为具有不同流方向的文本之间的边界分隔符。  即使 <xref:System.Windows.Documents.Span> 具有相同流方向的元素也被视为具有不同的双向作用域，这意味着 <xref:System.Windows.Documents.Span> 元素在容器的 <xref:System.Windows.FlowDirection> 中排序，仅 <xref:System.Windows.Documents.Span> 元素中的内容遵循 <xref:System.Windows.FlowDirection> 的 <xref:System.Windows.Documents.Span>.

下图显示了多个 <xref:System.Windows.Controls.TextBlock> 元素的流方向。

![说明具有不同流方向的文本块的图形。](./media/bidirectional-features-in-wpf-overview/flow-direction-text-blocks.png)

下面的示例演示如何使用 <xref:System.Windows.Documents.Span> 和 <xref:System.Windows.Documents.Run> 元素生成上图中显示的结果。

[!code-xaml[Span#Span](~/samples/snippets/csharp/VS_Snippets_Wpf/Span/CS/Window1.xaml#span)]

在示例中的 <xref:System.Windows.Controls.TextBlock> 元素中，<xref:System.Windows.Documents.Span> 元素根据其父元素的 <xref:System.Windows.FlowDirection> 进行布局，而每个 <xref:System.Windows.Documents.Span> 元素中的文本将根据其自己的 <xref:System.Windows.FlowDirection> 流动。 这适用于拉丁语和阿拉伯语，也适用于任何其他语言。

### <a name="adding-xmllang"></a>添加 xml:lang

下图显示了使用数字和算术表达式的另一个示例，如 `"200.0+21.4=221.4"`。 请注意，仅设置 <xref:System.Windows.FlowDirection>。

![仅使用 System.windows.flowdirection> 显示数字的图形。](./media/bidirectional-features-in-wpf-overview/numbers-flow-right-left.png)

此应用程序的用户将不会受到输出的失望，即使 <xref:System.Windows.FlowDirection> 是正确的，也不会将数字整形为阿拉伯数字。

XAML 元素可以包含一个 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 特性（`xml:lang`），该特性定义每个元素的语言。 XAML 还支持 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 语言原则，其中，应用于树中的父元素的 `xml:lang` 值由子元素使用。 在上面的示例中，由于没有为 <xref:System.Windows.Documents.Run> 元素或其任何顶级元素定义语言，因此使用了默认的 `xml:lang`，这对于 XAML 是 `en-US` 的。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 的内部数字整形算法选择相应语言的数字（在本例中为英语）。 若要使阿拉伯数字正确呈现 `xml:lang` 需要设置。

下图显示了添加了 `xml:lang` 的示例。

![图示从右到左排列的阿拉伯数字的图形。](./media/bidirectional-features-in-wpf-overview/arabic-numbers-flow-right-left.png)

下面的示例将 `xml:lang` 添加到应用程序。

[!code-xaml[LangAttribute#LangAttribute](~/samples/snippets/csharp/VS_Snippets_Wpf/LangAttribute/CS/Window1.xaml#langattribute)]

请注意，许多语言具有不同的 `xml:lang` 值，具体取决于目标区域，例如 `"ar-SA"` 和 `"ar-EG"` 表示阿拉伯语的两个变体。 前面的示例演示需要同时定义 `xml:lang` 值和 <xref:System.Windows.FlowDirection> 值。

<a name="FlowDirectionNontext"></a>

## <a name="flowdirection-with-non-text-elements"></a>非文本元素的 FlowDirection

<xref:System.Windows.FlowDirection> 不仅定义文本在文本元素中的流动方式，还定义几乎所有其他 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素的流动方向。 下图显示了一个 <xref:System.Windows.Controls.ToolBar>，它使用水平 <xref:System.Windows.Media.LinearGradientBrush> 以从左到右的渐变来绘制其背景。

![显示具有从左到右渐变的工具栏的图形。](./media/bidirectional-features-in-wpf-overview/toolbar-left-right-gradient.png)

将 <xref:System.Windows.FlowDirection> 设置为 "<xref:System.Windows.FlowDirection.RightToLeft>" 后，不仅 <xref:System.Windows.Controls.ToolBar> 按钮按从右到左的顺序排列，甚至 <xref:System.Windows.Media.LinearGradientBrush> popup 其偏移量（从右到左）。

下图显示了 <xref:System.Windows.Media.LinearGradientBrush> 的校准。

![显示具有从右到左渐变的工具栏的图形。](./media/bidirectional-features-in-wpf-overview/toolbar-right-left-gradient.png)

下面的示例将绘制一个 <xref:System.Windows.FlowDirection.RightToLeft> <xref:System.Windows.Controls.ToolBar>。 （若要将其从左到右绘制，请删除 <xref:System.Windows.Controls.ToolBar> 上的 <xref:System.Windows.FlowDirection> 属性。

[!code-xaml[Gradient#Gradient](~/samples/snippets/csharp/VS_Snippets_Wpf/Gradient/CS/Window1.xaml#gradient)]

<a name="FlowDirectionExceptions"></a>

### <a name="flowdirection-exceptions"></a>FlowDirection 异常

在某些情况下，<xref:System.Windows.FlowDirection> 不会按预期方式运行。 本部分介绍其中两种异常。

**Image**

一个 <xref:System.Windows.Controls.Image> 表示显示图像的控件。 在 XAML 中，它可用于定义要显示的 <xref:System.Windows.Controls.Image> 的统一资源标识符（URI）的 <xref:System.Windows.Controls.Image.Source%2A> 属性。

与其他 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素不同，<xref:System.Windows.Controls.Image> 不从容器继承 <xref:System.Windows.FlowDirection>。 但是，如果 <xref:System.Windows.FlowDirection> 显式设置为 <xref:System.Windows.FlowDirection.RightToLeft>，则 <xref:System.Windows.Controls.Image> 显示为水平翻转。 这可作为一种便捷功能提供给双向内容的开发人员，因为在某些情况下，水平翻转图像会达到所需的效果。

下图显示了翻转的 <xref:System.Windows.Controls.Image>。

![说明翻转图像的图形。](./media/bidirectional-features-in-wpf-overview/flipped-image-example.png)

下面的示例演示 <xref:System.Windows.Controls.Image> 无法从包含它的 <xref:System.Windows.Controls.StackPanel> 继承 <xref:System.Windows.FlowDirection>。

> [!NOTE]
> C：\ 上必须有一个名为**ms_logo**的文件运行此示例的驱动器。

[!code-xaml[Image#Image](~/samples/snippets/csharp/VS_Snippets_Wpf/Image/CS/Window1.xaml#image)]

> [!NOTE]
> 下载文件中包含一个**ms_logo**文件。 该代码假定 .jpg 文件不在项目中，而是位于 C:\ 驱动器中的某个位置。 必须将 .jpg 从项目文件复制到 C:\ 驱动器或更改代码才能在项目内查找该文件。 若要执行此更改 `Source="file://c:/ms_logo.jpg"` `Source="ms_logo.jpg"`。

**Path**

除了 <xref:System.Windows.Controls.Image> 之外，还 <xref:System.Windows.Shapes.Path> 另一个有趣的元素。 Path 是可用于绘制一系列连接的直线和曲线的对象。 它的行为方式类似于与 <xref:System.Windows.FlowDirection> 相关的 <xref:System.Windows.Controls.Image>;例如，<xref:System.Windows.FlowDirection.RightToLeft> <xref:System.Windows.FlowDirection> 是其 <xref:System.Windows.FlowDirection.LeftToRight> 的水平镜像。 但是，与 <xref:System.Windows.Controls.Image> 不同，<xref:System.Windows.Shapes.Path> 从容器继承其 <xref:System.Windows.FlowDirection>，而不需要显式指定它。

下面的示例使用 3 条线绘制简单的箭头。 第一个箭头从 <xref:System.Windows.Controls.StackPanel> 中继承 <xref:System.Windows.FlowDirection.RightToLeft> flow 方向，使其起点和终点从右侧的根进行测量。 具有显式 <xref:System.Windows.FlowDirection.RightToLeft> 的第二个箭头 <xref:System.Windows.FlowDirection> 也会在右侧开始。 但第三个箭头的起始根位于左侧。 有关绘制的详细信息，请参阅 <xref:System.Windows.Media.LineGeometry> 和 <xref:System.Windows.Media.GeometryGroup>。

[!code-xaml[Paths#Paths](~/samples/snippets/csharp/VS_Snippets_Wpf/Paths/CS/Window1.xaml#paths)]

下图显示了上一示例的输出，其中使用 `Path` 元素绘制了箭头：

![说明使用 Path 元素绘制的箭头的图形。](./media/bidirectional-features-in-wpf-overview/arrows-drawn-path-element.png)

<xref:System.Windows.Controls.Image> 和 <xref:System.Windows.Shapes.Path> 是 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 如何使用 <xref:System.Windows.FlowDirection>的两个示例。 除了在容器中布局特定方向 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素外，<xref:System.Windows.FlowDirection> 可用于在图面上呈现墨迹的 <xref:System.Windows.Controls.InkPresenter> 元素，<xref:System.Windows.Media.LinearGradientBrush>，<xref:System.Windows.Media.RadialGradientBrush>。 无论何时需要对从左到右行为进行模拟的内容执行从右到左行为，[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 都可以提供该功能。

<a name="NumberSubstitution"></a>

## <a name="number-substitution"></a>数字替换

从历史上看，Windows 提供了支持的数字替换，允许不同的区域性形状以相同的位数表示，同时保持这些数字在不同区域设置中统一的内部存储，例如，数字存储在众所周知的十六进制值，0x40，0x41 向，但会根据所选的语言显示。

这样，应用程序就可以处理数值，而无需将其从一种语言转换为另一种语言，例如，用户可以在本地化的阿拉伯语窗口中打开 Microsoft Excel 电子表格，并查看阿拉伯语中的数字，但在欧洲版本的 Windows，并查看相同数字的欧洲表示形式。 这对其他符号（如逗号分隔符和百分比符号）来说也是必需的，因为在同一文档中它们通常随数字一起出现。

[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 沿承了这一传统，并为此功能提供了进一步支持，以允许更多的用户对使用替换的时间和方式进行控制。 虽然此功能适用于任何语言，但它对双向内容尤其有用；由于应用程序可能会在各种区域性下运行，因此针对特定语言来设置数字形状通常是应用程序开发人员所面临的难题。

控制数字替换在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中的工作方式的核心属性是 <xref:System.Windows.Media.NumberSubstitution.Substitution%2A> 依赖关系属性。 <xref:System.Windows.Media.NumberSubstitution> 类指定如何显示文本中的数字。 它有三个定义其行为的公共属性。 下面是每个属性的摘要：

**CultureSource：**

此属性指定如何确定数字的区域性。 它采用三个 <xref:System.Windows.Media.NumberCultureSource> 枚举值之一。

- Override：数字区域性是 <xref:System.Windows.Media.NumberSubstitution.CultureOverride%2A> 属性的。

- Text：数字区域性是文本运行的区域性。 在标记中，这将是 `xml:lang`或其别名 `Language` 属性（<xref:System.Windows.FrameworkElement.Language%2A> 或 <xref:System.Windows.FrameworkContentElement.Language%2A>）。 此外，它是从 <xref:System.Windows.FrameworkContentElement> 派生的类的默认值。 此类包括 <xref:System.Windows.Documents.Paragraph?displayProperty=nameWithType>、<xref:System.Windows.Documents.Table?displayProperty=nameWithType> <xref:System.Windows.Documents.TableCell?displayProperty=nameWithType> 等。

- User：数字区域性是当前线程的区域性。 此属性是 <xref:System.Windows.FrameworkElement> 的所有子类的默认属性，如 <xref:System.Windows.Controls.Page>、<xref:System.Windows.Window> 和 <xref:System.Windows.Controls.TextBlock>。

**CultureOverride**：

仅当 <xref:System.Windows.Media.NumberSubstitution.CultureSource%2A> 属性设置为 <xref:System.Windows.Media.NumberCultureSource.Override> 时才使用 <xref:System.Windows.Media.NumberSubstitution.CultureOverride%2A> 属性，否则将忽略此属性。 该属性指定数字区域性。 默认值为 `null` 的值被解释为 en-us。

**Substitution**：

此属性指定要执行的数字替换类型。 它采用以下 <xref:System.Windows.Media.NumberSubstitutionMethod> 枚举值之一：

- <xref:System.Windows.Media.NumberSubstitutionMethod.AsCulture>：替换方法取决于数字区域性的 <xref:System.Globalization.NumberFormatInfo.DigitSubstitution%2A?displayProperty=nameWithType> 属性。 这是默认设置。

- <xref:System.Windows.Media.NumberSubstitutionMethod.Context>：如果数字区域性为阿拉伯语或波斯语区域性，则它指定数字取决于上下文。

- <xref:System.Windows.Media.NumberSubstitutionMethod.European>：数字始终呈现为欧洲数字。

- <xref:System.Windows.Media.NumberSubstitutionMethod.NativeNational>：使用由区域性的 <xref:System.Globalization.CultureInfo.NumberFormat%2A>指定的数字区域性的国家/地区来呈现数字。

- <xref:System.Windows.Media.NumberSubstitutionMethod.Traditional>：使用数字区域性的传统数字呈现数字。 对于大多数区域性，这与 <xref:System.Windows.Media.NumberSubstitutionMethod.NativeNational> 相同。 但 <xref:System.Windows.Media.NumberSubstitutionMethod.NativeNational> 会导致某些阿拉伯语区域性采用拉丁数字，而此值将导致所有阿拉伯区域性的阿拉伯数字。

这些值对双向内容开发人员意味着什么？ 在大多数情况下，开发人员可能只需要定义每个文本 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素 <xref:System.Windows.FlowDirection> 和语言，例如 `Language="ar-SA"`，<xref:System.Windows.Media.NumberSubstitution> 逻辑负责根据正确的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]显示数字。 下面的示例演示在 Windows 的阿拉伯语版本中运行的 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 应用程序中使用阿拉伯和英文数字。

[!code-xaml[Numbers#Numbers](~/samples/snippets/csharp/VS_Snippets_Wpf/Numbers/CS/Window1.xaml#numbers)]

下图显示了上一示例的输出：如果你在显示了阿拉伯和英文版的 Windows 阿拉伯语版本中运行：

![显示阿拉伯数字和英文数字的图形。](./media/bidirectional-features-in-wpf-overview/arabic-english-numbers.png)

在这种情况下，<xref:System.Windows.FlowDirection> 很重要，因为将 <xref:System.Windows.FlowDirection> 设置为 <xref:System.Windows.FlowDirection.LeftToRight> 会生成欧洲数字。 以下各节介绍如何在整个文档内统一显示数字。 如果未在阿拉伯语版 Windows 上运行此示例，所有数字都将显示为欧洲数字。

**定义替换规则**

在实际的应用程序中，可能需要以编程方式设置语言。 例如，你希望将 `xml:lang` 特性设置为与系统 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]所使用的特性相同，或可能更改语言，具体取决于应用程序状态。

如果要根据应用程序的状态进行更改，请使用 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]提供的其他功能。

首先，设置应用程序组件的 `NumberSubstitution.CultureSource="Text"`。 使用此设置可确保设置不是从 "User" 作为默认值的文本元素的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，如 <xref:System.Windows.Controls.TextBlock>。

例如:

```xaml
<TextBlock
   Name="text1" NumberSubstitution.CultureSource="Text">
   1234+5679=6913
</TextBlock>
```

在相应C#的代码中，将 `Language` 属性设置为，例如 `"ar-SA"`。

```csharp
text1.Language = System.Windows.Markup.XmlLanguage.GetLanguage("ar-SA");
```

如果需要将 `Language` 属性设置为当前用户的 UI 语言，请使用以下代码。

```csharp
text1.Language = System.Windows.Markup.XmlLanguage.GetLanguage(System.Globalization.CultureInfo.CurrentUICulture.IetfLanguageTag);
```

<xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> 表示当前线程在运行时使用的当前区域性。

最终 XAML 示例应与下面的示例类似。

[!code-xaml[Numbers2#Numbers2](~/samples/snippets/csharp/VS_Snippets_Wpf/Numbers2/CS/Window1.xaml#numbers2)]

最终C#示例应类似于以下内容。

[!code-csharp[NumbersCSharp#NumbersCSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/NumbersCSharp/CSharp/Window1.xaml.cs#numberscsharp)]

下图显示了两种编程语言的窗口外观，其中显示了阿拉伯数字：

![显示阿拉伯数字的图形。](./media/bidirectional-features-in-wpf-overview/displays-arabic-numbers.png)

**使用 Substitution 属性**

[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中数字替换的方式取决于文本元素的语言及其 <xref:System.Windows.FlowDirection>。 如果 <xref:System.Windows.FlowDirection> 从左到右，则会呈现欧洲数字。 但是，如果它前面有阿拉伯语文本，或将语言设置为 "ar" 并且 <xref:System.Windows.FlowDirection.RightToLeft> <xref:System.Windows.FlowDirection>，则改为呈现阿拉伯数字。

但在某些情况下，建议创建统一的应用程序，例如适用于所有用户的欧洲数字。 或使用特定 <xref:System.Windows.Style> <xref:System.Windows.Documents.Table> 单元中的阿拉伯数字。 执行此操作的一种简单方法是使用 <xref:System.Windows.Media.NumberSubstitution.Substitution%2A> 属性。

在下面的示例中，第一个 <xref:System.Windows.Controls.TextBlock> 没有设置 <xref:System.Windows.Media.NumberSubstitution.Substitution%2A> 属性，因此算法会按预期显示阿拉伯数字。 但是，在第二个 <xref:System.Windows.Controls.TextBlock> 中，替换设置为 "欧洲" 覆盖阿拉伯数字的默认替换，并显示欧洲数字。

[!code-xaml[Numbers3#Numbers3](~/samples/snippets/csharp/VS_Snippets_Wpf/Numbers3/CS/Window1.xaml#numbers3)]
