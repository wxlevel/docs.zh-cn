---
title: WPF 图形呈现疑难解答
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [WPF], rendering
- rendering graphics [WPF]
ms.assetid: 6dec9657-4d8c-4e46-8c54-40fb80008265
ms.openlocfilehash: 09f5f026ed320aaa253d8cdf6e0b271235aff604
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004164"
---
# <a name="wpf-graphics-rendering-overview"></a>WPF 图形呈现疑难解答
本主题概述 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 可视化层。 它侧重于 <xref:System.Windows.Media.Visual> 类的角色，以便在 @no__t 模型中呈现支持。  

<a name="role_of_visual_object"></a>   
## <a name="role-of-the-visual-object"></a>视觉对象的角色  
 @No__t 0 类是派生每个 @no__t 对象的基本抽象。 该类还用作在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中编写新控件的入口点，在 Win32 应用程序模型中，该类在许多方面可视为窗口句柄 (HWND)。  
  
 @No__t 0 对象是核心 @no__t 1 对象，其主要角色是提供呈现支持。 用户界面控件（如 @no__t 0 和 <xref:System.Windows.Controls.TextBox>）派生自第 2 @no__t 类，并使用它来保存其呈现数据。 @No__t 0 对象提供对以下各项的支持：  
  
- 输出显示：呈现视觉对象的持久的序列化绘制内容。  
  
- 转换对视觉对象执行转换。  
  
- 修剪为视觉对象提供剪辑区域支持。  
  
- 命中测试：确定坐标或几何图形是否包含在视觉对象的边界内。  
  
- 边界框计算：确定视觉对象的边框。  
  
 但 @no__t 0 对象不包括对非渲染功能的支持，例如：  
  
- 事件处理  
  
- 布局  
  
- 样式  
  
- 数据绑定  
  
- 全球化  
  
 <xref:System.Windows.Media.Visual> 作为公共抽象类公开，子类必须派生自该类。 下图显示了 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中所公开的视觉对象的层次结构。  
  
 ![从 Visual 对象派生的类的示意图](./media/wpf-graphics-rendering-overview/classes-derived-visual-object.png)    
  
### <a name="drawingvisual-class"></a>DrawingVisual 类  
 @No__t-0 是一个轻型绘图类，用于呈现形状、图像或文本。 此类之所以为轻量类是因为它不提供布局或事件处理，从而提升其运行时性能。 因此，绘图非常适用于背景和剪贴画。 @No__t-0 可用于创建自定义视觉对象。 有关详细信息，请参阅[使用 DrawingVisual 对象](using-drawingvisual-objects.md)。  
  
### <a name="viewport3dvisual-class"></a>Viewport3DVisual 类  
 @No__t-0 在 2D <xref:System.Windows.Media.Visual> 和 @no__t 2 对象之间提供桥梁。 @No__t-0 类是所有三维可视元素的基类。 @No__t-0 要求您定义 @no__t 1 值和 @no__t 2 值。 借助照相机，可以查看场景。 视区确定投影映射到 2D 图面的位置。 有关 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中 3D 的详细信息，请参阅 [3-D 图形概述](3-d-graphics-overview.md)。  
  
### <a name="containervisual-class"></a>ContainerVisual 类  
 @No__t-0 类用作 @no__t 1 对象的集合的容器。 @No__t-0 类派生自 @no__t 类，使其可以包含视觉对象的集合。  
  
### <a name="drawing-content-in-visual-objects"></a>视觉对象中的绘图内容  
 @No__t 0 对象将其呈现数据存储为**矢量图形指令列表**。 指令列表中的每一项都以序列化格式表示一组低级别的图形数据及其相关资源。 共有四种不同类型的呈现数据可以包含绘图内容。  
  
|绘图内容类型|描述|  
|--------------------------|-----------------|  
|矢量图形|表示向量图形数据以及任何关联的 @no__t 0 和 @no__t 信息。|  
|图像|表示由 <xref:System.Windows.Rect> 定义的区域内的图像。|  
|标志符号|表示呈现 <xref:System.Windows.Media.GlyphRun> 的绘图，它是指定字体资源中的一系列字形。 这是文本的表示方式。|  
|视频|表示用于呈现视频的绘图。|  
  
 @No__t-0 允许使用视觉对象内容填充 @no__t 1。 使用 @no__t 0 对象的绘图命令时，实际上存储的是图形系统稍后将使用的一组呈现数据;您不会实时绘制到屏幕上。  
  
 当你创建一个 @no__t 0 的控件（如 @no__t）时，控件将隐式生成呈现数据以便绘图本身。 例如，设置 @no__t 的 <xref:System.Windows.Controls.ContentControl.Content%2A> 属性会导致该控件存储字形的渲染表示形式。  
  
 @No__t-0 将其内容描述为一个或多个包含在 @no__t 2 中的 @no__t 1 对象。 @No__t 还介绍了不透明蒙板、转换、位图效果以及应用于其内容的其他操作。 呈现内容时，<xref:System.Windows.Media.DrawingGroup> 操作按以下顺序应用： <xref:System.Windows.Media.DrawingGroup.OpacityMask%2A>、<xref:System.Windows.Media.DrawingGroup.Opacity%2A>、<xref:System.Windows.Media.DrawingGroup.BitmapEffect%2A>、<xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A>、<xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A>，然后 <xref:System.Windows.Media.DrawingGroup.Transform%2A>。  
  
 下图显示了在呈现顺序中应用 <xref:System.Windows.Media.DrawingGroup> 操作的顺序。  
  
 ![操作 graphcismm_drawinggroup_order 的 DrawingGroup 顺序](./media/graphcismm-drawinggroup-order.png "")  
DrawingGroup 操作的顺序  
  
 有关详细信息，请参阅 [Drawing 对象概述](drawing-objects-overview.md)。  
  
#### <a name="drawing-content-at-the-visual-layer"></a>可视化层中的绘图内容  
 永远不会直接实例化 <xref:System.Windows.Media.DrawingContext>;不过，您可以从某些方法（如 <xref:System.Windows.Media.DrawingGroup.Open%2A?displayProperty=nameWithType> 和 <xref:System.Windows.Media.DrawingVisual.RenderOpen%2A?displayProperty=nameWithType>）获取一个绘图上下文。 下面的示例从 @no__t 中检索 <xref:System.Windows.Media.DrawingContext>，并使用它来绘制矩形。  
  
 [!code-csharp[drawingvisualsample#101](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#101)]
 [!code-vb[drawingvisualsample#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#101)]  
  
#### <a name="enumerating-drawing-content-at-the-visual-layer"></a>在可视化层中枚举绘图内容  
 除了其他用途以外，@no__t 0 对象还提供用于枚举 @no__t 的内容的对象模型。  
  
> [!NOTE]
> 枚举视觉对象的内容时，将检索 <xref:System.Windows.Media.Drawing> 对象，而不是矢量图形指令列表中的呈现数据的基础表示形式。  
  
 下面的示例使用 <xref:System.Windows.Media.VisualTreeHelper.GetDrawing%2A> 方法检索 @no__t 2 的 @no__t 值并对其进行枚举。  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMRetrieveDrawings](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/EnumerateDrawingsExample.xaml.cs#graphicsmmretrievedrawings)]  
  
<a name="how_visual_objects_are_used_to_build_controls"></a>   
## <a name="how-visual-objects-are-used-to-build-controls"></a>如何使用视觉对象来生成控件  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的许多对象都由其他视觉对象组成，这意味着它们可以包含子代对象的各种层次结构。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的许多用户界面元素（如控件）都由多个表示不同类型呈现元素的视觉对象组成。 例如，<xref:System.Windows.Controls.Button> 控件可以包含多个其他对象，包括 <xref:Microsoft.Windows.Themes.ClassicBorderDecorator>、<xref:System.Windows.Controls.ContentPresenter> 和 @no__t。  
  
 下面的代码演示在标记中定义的 @no__t 0 控件。  
  
 [!code-xaml[VisualsOverview#VisualsOverviewSnippet1](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml#visualsoverviewsnippet1)]  
  
 如果要枚举构成默认 <xref:System.Windows.Controls.Button> 控件的视觉对象，可以找到如下所示的视觉对象的层次结构：  
  
 ![可视化树层次结构示意图](./media/wpf-graphics-rendering-overview/visual-object-diagram.gif) 
  
 @No__t-0 控件包含一个 @no__t 元素，该元素又包含一个 @no__t 2 元素。 @No__t-0 元素负责绘制 @no__t 的边框和背景。 @No__t-0 元素负责显示 @no__t 的内容。 在这种情况下，由于显示的是文本，@no__t 0 元素包含 @no__t 1 元素。 @No__t-0 控件使用 <xref:System.Windows.Controls.ContentPresenter> 意味着内容可以由其他元素（如 <xref:System.Windows.Controls.Image> 或几何）表示，例如 <xref:System.Windows.Media.EllipseGeometry>。  
  
### <a name="control-templates"></a>控件模板  
 控件展开为控件层次结构的关键是 <xref:System.Windows.Controls.ControlTemplate>。 控件模板为控件指定了默认的可视化层次结构。 显式引用某个控件时，会隐式引用它的可视化层次结构。 可以重写控件模板的默认值，以便为控件创建自定义的可视化外观。 例如，可以修改 <xref:System.Windows.Controls.Button> 控件的背景颜色值，以便它使用线性渐变颜色值而不是纯色值。 有关详细信息，请参阅[按钮样式和模板](../controls/button-styles-and-templates.md)。  
  
 用户界面元素（例如 <xref:System.Windows.Controls.Button> 控件）包含多个矢量图形指令列表，它们描述控件的整个呈现定义。 下面的代码演示在标记中定义的 @no__t 0 控件。  
  
 [!code-xaml[VisualsOverview#VisualsOverviewSnippet2](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml#visualsoverviewsnippet2)]  
  
 如果要枚举由 <xref:System.Windows.Controls.Button> 控件组成的视觉对象和矢量图形指令列表，可找到如下所示的对象层次结构：  
  
 ![可视化树和呈现数据示意图](./media/wpf-graphics-rendering-overview/visual-tree-rendering-data.png)  
  
 @No__t-0 控件包含一个 @no__t 元素，该元素又包含一个 @no__t 2 元素。 @No__t-0 元素负责绘制构成按钮的边框和背景的所有离散图形元素。 @No__t-0 元素负责显示 @no__t 的内容。 在这种情况下，由于显示的是图像，@no__t 0 元素包含 @no__t 1 元素。  
  
 对于视觉对象和矢量图形指令列表的层次结构，需要注意多个事项：  
  
- 该层次结构中的排序表示绘图信息的呈现顺序。 从可视化元素的根，按照从左到右、从上到下的顺序遍历子元素。 如果某个元素有可视化子元素，则会先遍历该元素的子元素，然后再遍历该元素的同级。  
  
- 层次结构中的非叶节点元素（例如 <xref:System.Windows.Controls.ContentPresenter>）用于包含子元素，它们不包含指令列表。  
  
- 如果可视化元素既包含矢量图形指令列表又包含可视化子级，则会先呈现父级可视化元素中的指令列表，然后再呈现任何可视化子对象中的绘图。  
  
- 矢量图形指令列表中的项按照从左到右的顺序呈现。  
  
<a name="visual_tree"></a>   
## <a name="visual-tree"></a>可视化树  
 可视化树中包含某个应用程序的用户界面所使用的所有可视化元素。 由于可视化元素中包含持久的绘图信息，因此可以将可视化树视为场景图，其中包含将输出写入显示设备所必需的全部呈现信息。 该树汇集了由该应用程序在代码或标记中直接创建的所有可视化元素。 该可视化树还包含由元素（如控件和数据对象）的模板扩展功能创建的所有可视化元素。  
  
 下面的代码演示在标记中定义的 @no__t 0 元素。  
  
 [!code-xaml[VisualsOverview#VisualsOverviewSnippet3](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml#visualsoverviewsnippet3)]  
  
 如果要枚举标记示例中包含 <xref:System.Windows.Controls.StackPanel> 元素的视觉对象，可找到如下所示的视觉对象的层次结构：  
  
 ![可视化树层次结构示意图](./media/wpf-graphics-rendering-overview/visual-tree-hierarchy.gif)  
  
### <a name="rendering-order"></a>呈现顺序  
 通过可视化树，可以确定 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 可视化对象和绘图对象的呈现顺序。 将从位于可视化树中最顶层节点中的可视化元素根开始遍历。 然后，将按照从左到右的顺序遍历可视化元素根的子级。 如果可视化元素有子级，则将先遍历该可视化元素的子级，然后再遍历其同级。 这意味着子可视化元素的内容先于该可视化元素本身的内容呈现。  
  
 ![可视化树呈现顺序示意图](./media/wpf-graphics-rendering-overview/visual-tree-rendering-order.gif) 
  
### <a name="root-visual"></a>可视化元素根  
 **可视化元素根**是可视化树层次结构中最顶层的元素。 在大多数应用程序中，根视觉对象的基类 @no__t 为-0 或 @no__t 为-1。 但是，如果在 Win32 应用程序中承载视觉对象，则可视化元素根将是在 Win32 窗口中承载的最顶层的可视化元素。 有关详细信息，请参阅[教程：在 Win32 应用程序中承载视觉对象 @ no__t-0。  
  
### <a name="relationship-to-the-logical-tree"></a>与逻辑树的关系  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的逻辑树表示应用程序在运行时的元素。 尽管不直接操作该树，但是该应用程序视图对于了解属性继承和事件路由非常有用。 与可视化树不同，逻辑树可以表示非可视数据对象，例如 <xref:System.Windows.Documents.ListItem>。 在许多情况下，逻辑树密切映射到应用程序的标记定义。 下面的代码演示在标记中定义的 @no__t 0 元素。  
  
 [!code-xaml[VisualsOverview#VisualsOverviewSnippet5](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml#visualsoverviewsnippet5)]  
  
 如果要枚举包含标记示例中 <xref:System.Windows.Controls.DockPanel> 元素的逻辑对象，可找到如下所示的逻辑对象的层次结构：  
  
 ![树形框图](./media/tree1-wcp.gif "Tree1_wcp")  
逻辑树关系图  
  
 可视化树和逻辑树与当前的应用程序元素集合同步，并反映对元素进行的任何添加、删除或修改。 但是，这些树表示不同的应用程序视图。 与可视化树不同，逻辑树不展开控件的 <xref:System.Windows.Controls.ContentPresenter> 元素。 这意味着同一组对象的逻辑树和可视化树之间不存在直接的一对一对应关系。 事实上，使用与参数相同的元素调用**system.windows.logicaltreehelper>** 对象的 <xref:System.Windows.LogicalTreeHelper.GetChildren%2A> 方法和**VisualTreeHelper**对象的 @no__t 3 方法会产生不同的结果。  
  
 有关逻辑树的详细信息，请参阅 [WPF 中的树](../advanced/trees-in-wpf.md)。  
  
### <a name="viewing-the-visual-tree-with-xamlpad"></a>使用 XamlPad 查看可视化树  
 @No__t-0 工具 XamlPad 提供了一个选项，用于查看和浏览与当前定义的 XAML 内容相对应的可视化树。 单击菜单栏上的“显示可视化树”按钮可显示相应的可视化树。 下面演示了如何在 XamlPad 的**可视化树资源管理器**面板中将 XAML 内容扩展为可视化树节点：  
  
 ![XamlPad 中的“可视化树资源管理器”面板](./media/wpf-graphics-rendering-overview/visual-tree-explorer.png)  

 请注意 <xref:System.Windows.Controls.Label>、<xref:System.Windows.Controls.TextBox> 和 <xref:System.Windows.Controls.Button> 控件如何在 XamlPad 的**可视化树资源管理器**面板中显示单独的视觉对象层次结构。 这是因为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件具有一个包含该控件的可视化树的 @no__t 1。 显式引用某个控件时，会隐式引用它的可视化层次结构。  
  
### <a name="profiling-visual-performance"></a>分析可视化性能  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了一套性能分析工具，此工具可帮助分析应用程序的运行时行为，并确定可应用的性能优化类型。 可视化探查器工具通过直接映射到应用程序的可视化树来为性能数据提供一个丰富的图形视图。 在此屏幕快照中，通过可视化探查器的“CPU 使用率”部分可以清楚地了解对象对 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 服务（如呈现和布局）的使用情况。  
  
 ![可视化探查器显示输出](./media/wpfperf-visualprofiler-04.png "WPFPerf_VisualProfiler_04")  
可视化探查器显示输出  
  
<a name="visual_rendering_behavior"></a>   
## <a name="visual-rendering-behavior"></a>视觉对象的呈现行为  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 引入了多个影响可视化对象呈现行为的功能：保留的模式图形、矢量图形和与设备无关的图形。  
  
### <a name="retained-mode-graphics"></a>保留的模式图形  
 了解 Visual 对象角色的关键之一是，了解**即时模式**和**保留模式**图形系统之间的区别。 基于 GDI 或 GDI+ 的标准 Win32 应用程序使用即时模式图形系统。 这意味着应用程序负责重新绘制由于某项操作（如重设窗口大小）或者对象的可视化外观发生变化而失效的工作区部分。  
  
 ![Win32 呈现序列示意图](./media/wpf-graphics-rendering-overview/win32-rendering-squence.png)  
  
 相比之下，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 使用保留模式系统。 这意味着具有可视化外观的应用程序对象定义一组序列化绘图数据。 在定义了绘图数据之后，系统会响应所有的重新绘制请求来呈现应用程序对象。 甚至在运行时，用户可以修改或创建应用程序对象，并仍依赖于系统响应绘制请求。 保留模式图形系统中有一个强大功能，即绘图信息总是由应用程序保持为序列化状态，但是呈现功能仍由系统负责。 以下关系图演示应用程序如何依赖 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 来响应绘制请求。  
  
 ![WPF 呈现序列示意图](./media/wpf-graphics-rendering-overview/wpf-rendering-sequence.png)  

#### <a name="intelligent-redrawing"></a>智能重绘  
 使用保留模型图形的最大好处之一就是，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 可以高效率地优化需要在应用程序中重绘的内容。 即使存在一个具有各种不透明度的复杂场景，通常也不必编写特殊用途的代码来优化重绘功能。 将该功能与 Win32 编程进行比较，在后者中可以通过最小化更新区域中的重绘量来尽力优化应用程序。 有关在 Win32 应用程序中优化重绘功能时涉及到的复杂度类型的示例，请参阅[在更新区域中重绘](/windows/desktop/gdi/redrawing-in-the-update-region)。  
  
### <a name="vector-graphics"></a>矢量图形  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 使用**矢量图形**作为其呈现数据的格式。 矢量图形（包括可缩放的矢量图形 (SVG)、Windows 元文件 (.wmf) 和 TrueType 字体）存储呈现数据，并以指令列表的形式传输呈现数据，这些指令描述如何使用图形基元来重新创建图像。 例如，TrueType 字体是描述一组直线、曲线和命令（而不是像素数组）的矢量字。 矢量图形的主要好处之一就是能够缩放到任何大小和分辨率。  
  
 与矢量图形不同，位图图形以图像的逐像素表示形式来存储呈现数据，并在特定的分辨率下预先呈现。 位图图形格式和矢量图形格式的主要区别之一是对原始源图像的保真度。 例如，当修改了某个源图像的大小发时，位图图形系统会拉伸该图像，而矢量图形系统会缩放该图像，从而保持图像的保真度。  
  
 下图显示了其大小重设为 300% 的源图像。 请注意，当源图像作为位图图形图像拉伸而不是作为矢量图形图像缩放时会发生失真。  
  
 ![光栅图与矢量图之间的区别](./media/wpf-graphics-rendering-overview/raster-vector-differences.png)  
  
 以下标记显示了两个已定义 <xref:System.Windows.Shapes.Path> 元素。 第二个元素使用 <xref:System.Windows.Media.ScaleTransform> 将第一个元素的绘图指令的大小调整为 300%。 请注意，<xref:System.Windows.Shapes.Path> 元素中的绘图说明保持不变。  
  
 [!code-xaml[VectorGraphicsSnippets#VectorGraphicsSnippet1](~/samples/snippets/csharp/VS_Snippets_Wpf/VectorGraphicsSnippets/CS/PageOne.xaml#vectorgraphicssnippet1)]  
  
### <a name="about-resolution-and-device-independent-graphics"></a>关于与分辨率和设备无关的图形  
 确定屏幕上的文本和图形的大小有两个系统因素：分辨率和 DPI。 分辨率描述屏幕上显示的像素数。 因为分辨率变得越来越高，像素将变得更小，从而导致图形和文本会显得更小。 在设置为 1024 x 768 的监视器上所显示的图形将在分辨率更改为 1600 x 1200 时显示得小很多。  
  
 另一个系统设置 DPI 描述屏幕英寸的大小（以像素为单位）。 大多数 Windows 系统的 DPI 均为96，这意味着屏幕英寸为96像素。 增加 DPI 设置会使屏幕英寸更大；降低 DPI 可使屏幕英寸更小。 这意味着屏幕英寸与实际英寸不同；在大多数系统上，可能不相同。 当增加 DPI 时，可感知 DPI 的图形和文本会变大，因为已增加了屏幕英寸的大小。 增加 DPI 可以使文本更易于阅读，尤其是使用较高的分辨率时。  
  
 并非所有应用程序都可感知 DPI：一些将硬件像素用作主要计量单位；更改系统 DPI 对这些应用程序没有影响。 其他许多应用程序使用可感知 DPI 的单位来描述字体大小，但使用像素来描述其他所有内容。 使 DPI 太小或太大，可能导致这些应用程序的布局问题，因为应用程序的文本会随着系统的 DPI 设置而缩放，但应用程序的 UI 并不会。 对于使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 开发的应用程序，已消除此问题。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 通过使用与设备无关的像素（而不是硬件像素）作为主要测量单位支持自动缩放；图形和文本可正确缩放，而无需应用程序开发者执行任何额外的工作。 下图显示 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 文本和图形如何采用不同 DPI 设置进行显示的示例。  
  
 ![不同 DPI 设置的图形和文本](./media/graphicsmm-dpi-setting-examples.png "graphicsmm_dpi_setting_examples")  
采用不同 DPI 设置的图形和文本  
  
<a name="visualtreehelper_class"></a>   
## <a name="visualtreehelper-class"></a>VisualTreeHelper 类  
 @No__t-0 类是静态帮助器类，它提供了用于在视觉对象级别进行编程的低级功能，这在非常特定的情况下非常有用，例如开发高性能的自定义控件。 在大多数情况下，更高级别 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 框架对象（如 @no__t，<xref:System.Windows.Controls.TextBlock>）提供更大的灵活性和易用性。  
  
### <a name="hit-testing"></a>命中测试  
 当默认的命中测试支持无法满足您的需求时，<xref:System.Windows.Media.VisualTreeHelper> 类提供用于对视觉对象进行命中测试的方法。 您可以使用 <xref:System.Windows.Media.VisualTreeHelper> 类中的 <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> 方法来确定几何或点坐标值是否在给定对象（如控件或图形元素）的边界内。 例如，可以使用命中测试确定对象的边框内的鼠标单击落在圆的几何内。还可以选择重写命中测试的默认实现，以执行自己的自定义命中测试计算。  
  
 有关命中测试的详细信息，请参阅[可视化层中的命中测试](hit-testing-in-the-visual-layer.md)。  
  
### <a name="enumerating-the-visual-tree"></a>枚举可视化树  
 @No__t-0 类提供用于枚举可视化树成员的功能。 若要检索父级，请调用 <xref:System.Windows.Media.VisualTreeHelper.GetParent%2A> 方法。 若要检索可视对象的子元素或直接后代，请调用 <xref:System.Windows.Media.VisualTreeHelper.GetChild%2A> 方法。 此方法返回父级在指定索引处的子 @no__t 0。  
  
 下面的示例演示如何枚举视觉对象的所有后代，如果你对序列化可视化对象层次结构的所有呈现信息感兴趣，则可能希望使用该技术。  
  
 [!code-csharp[VisualsOverview#101](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml.cs#101)]
 [!code-vb[VisualsOverview#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsOverview/visualbasic/window1.xaml.vb#101)]  
  
 在大多数情况下，逻辑树是 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序中元素的更有用的表示形式。 尽管不直接操作逻辑树，但是该应用程序视图对于了解属性继承和事件路由非常有用。 与可视化树不同，逻辑树可以表示非可视数据对象，例如 <xref:System.Windows.Documents.ListItem>。 有关逻辑树的详细信息，请参阅 [WPF 中的树](../advanced/trees-in-wpf.md)。  
  
 @No__t-0 类提供用于返回视觉对象的边框的方法。 可以通过调用 <xref:System.Windows.Media.VisualTreeHelper.GetContentBounds%2A> 来返回视觉对象的边框。 可以通过调用 <xref:System.Windows.Media.VisualTreeHelper.GetDescendantBounds%2A>，返回可视对象的所有子代的边框，包括视觉对象本身。 下面的代码演示如何计算可视化对象及其所有子代的边框。  
  
 [!code-csharp[VisualsOverview#102](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml.cs#102)]
 [!code-vb[VisualsOverview#102](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsOverview/visualbasic/window1.xaml.vb#102)]  
  
## <a name="see-also"></a>请参阅

- <xref:System.Windows.Media.Visual>
- <xref:System.Windows.Media.VisualTreeHelper>
- <xref:System.Windows.Media.DrawingVisual>
- [2D 图形和图像处理](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
- [可视化层中的命中测试](hit-testing-in-the-visual-layer.md)
- [使用 DrawingVisual 对象](using-drawingvisual-objects.md)
- [教程：在 Win32 应用程序中承载视觉对象 @ no__t-0
- [优化 WPF 应用程序性能](../advanced/optimizing-wpf-application-performance.md)
