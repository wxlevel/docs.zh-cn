---
title: WPF 体系结构
ms.date: 03/30/2017
helpviewer_keywords:
- properties [WPF], attached
- attached properties [WPF]
- architecture [WPF]
- unmanaged components [WPF]
- affinity thread [WPF]
- Storyboards [WPF]
- milcore [WPF]
- components [WPF], unmanaged
- painter's algorithm
- interfaces [WPF], INotifyPropertyChange
- CommandBindings [WPF]
- data templates [WPF]
- thread [WPF], affinity
ms.assetid: 8579c10b-76ab-4c52-9691-195ce02333c8
ms.openlocfilehash: 02a70e65cd53a8998395987770cd32efc82293d0
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2019
ms.locfileid: "73459609"
---
# <a name="wpf-architecture"></a>WPF 体系结构
本主题提供 Windows Presentation Foundation （WPF）类层次结构的指导教程。 本主题涵盖了 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的大部分主要子系统，并说明它们的交互方式。 本主题还详细介绍了 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 架构师所做的一些选择。  

<a name="System_Object"></a>   
## <a name="systemobject"></a>System.Object  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 主要编程模型通过托管代码公开。 在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的早期设计阶段，曾有过大量关于如何界定系统的托管组件和非托管组件的争论。 CLR 提供了许多功能，这些功能使得开发更高效、更可靠（包括内存管理、错误处理、通用类型系统等），但会产生费用。  
  
 下图说明了 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的主要组件。 关系图的红色部分（PresentationFramework、PresentationCore 和 milcore）是 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的主要代码部分。 在这些组件中，只有一个是非托管组件 - milcore。 Milcore 以非托管代码编写，以便实现与 DirectX 的紧密集成。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的所有显示都是通过 DirectX 引擎完成的，因此可以实现高效的硬件和软件呈现。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 还要求对内存和执行进行精细控制。 Milcore 中的组合引擎对性能的影响非常高，需要具有 CLR 的许多优点才能获得性能。  
  
 ![WPF 在 .NET Framework 中的位置。](./media/wpf-architect1.PNG "wpf_architect1")  
  
 本主题的后面部分将讨论 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的托管和非托管部分之间的通信。 下面介绍托管编程模型的其余部分。  
  
<a name="System_Threading_DispatcherObject"></a>   
## <a name="systemthreadingdispatcherobject"></a>System.Threading.DispatcherObject  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的大多数对象都派生自 <xref:System.Windows.Threading.DispatcherObject>，后者提供了用于处理并发和线程处理的基本构造。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 基于调度程序实现的消息系统。 其工作方式与常见的 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 消息泵非常类似；事实上，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 调度程序使用 User32 消息执行跨线程调用。  
  
 要讨论 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的并发，首先必须真正理解两个核心概念 - 调度程序和线程关联。  
  
 在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的设计阶段，目标是移动到单一线程的执行，但这不是一种与线程“关联的”模型。 当一个组件使用执行线程的标识来存储某种类型的状态时，将发生线程关联。 最常见的形式是使用线程本地存储 (TLS) 来存储状态。 线程关联要求执行的每个逻辑线程仅由操作系统中的一个物理线程所拥有，这将占用大量内存。 最后，WPF 的线程处理模型通过线程关联与单一线程执行的现有 User32 线程处理模型保持同步。 主要原因是互操作性 - 类似于 [!INCLUDE[TLA2#tla_ole2.0](../../../../includes/tla2sharptla-ole2-0-md.md)] 的系统、剪贴板和 Internet Explorer 均需要单一线程关联 (STA) 执行。  
  
 假设你具有带有 STA 线程的对象，则需要在线程之间通信并验证你是否位于正确的线程上的一种方法。 调度程序的作用就在于此。 调度程序是一个基本的消息调度系统，具有多个按优先顺序排列的队列。 消息的示例包括原始输入通知（鼠标移动）、框架函数（布局）或用户命令（执行此方法）。 通过从 <xref:System.Windows.Threading.DispatcherObject>派生，你可以创建一个具有 STA 行为的 CLR 对象，并在创建时为其提供指向调度程序的指针。  
  
<a name="System_Windows_DependencyObject"></a>   
## <a name="systemwindowsdependencyobject"></a>System.Windows.DependencyObject  
 生成 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 时使用的主要体系结构原理之一是首选属性而不是方法或事件。 属性具有声明性，可更方便地指定用途而不是操作。 它还支持模型驱动或数据驱动的系统，以显示用户界面内容。 这种理念的预期效果是创建更多可以绑定到的属性，从而更好地控制应用程序的行为。  
  
 为了获得更多由属性驱动的系统，需要的属性系统比 CLR 提供的更多。 这种丰富性的一个简单示例是更改通知。 若要实现双向绑定，需要绑定的双方支持更改通知。 若要使行为与属性值相关联，需要在属性值更改时收到通知。 Microsoft .NET 框架有一个接口**INotifyPropertyChange**，该接口允许对象发布更改通知，但是它是可选的。  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 提供了更丰富的属性系统，派生自 <xref:System.Windows.DependencyObject> 类型。 该属性系统实际是一个“依赖”属性系统，因为它会跟踪属性表达式之间的依赖关系，并在依赖关系更改时自动重新验证属性值。 例如，如果你有一个继承的属性（如 <xref:System.Windows.Controls.Control.FontSize%2A>），则在继承值的元素的父级上更改该属性时，系统会自动更新。  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 属性系统的基础是属性表达式的概念。 在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的第一个版本中，属性表达式系统是关闭的，表达式均作为框架的一部分提供。 表达式致使属性系统不具有数据绑定、样式调整或继承硬编码，而是由框架内后面的层来提供这些功能。  
  
 属性系统还提供属性值的稀疏存储。 因为对象可能有数十个（如果达不到上百个）属性，并且大部分值处于其默认状态（被继承、由样式设置等），所以并非对象的每个实例都需要具有在其上定义的每个属性的完全权重。  
  
 属性系统的最后一个新功能是附加属性的概念。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 元素是基于组合和组件重用的原则生成的。 通常情况下，一些包含元素（如 <xref:System.Windows.Controls.Grid> layout 元素）需要对子元素的其他数据来控制其行为（如行/列信息）。 任何对象都可以为任何其他对象提供属性定义，而不是将所有这些属性与每个元素相关联。 这与 JavaScript 中的“expando”功能相似。  
  
<a name="System_Windows_Media_Visual"></a>   
## <a name="systemwindowsmediavisual"></a>System.Windows.Media.Visual  
 定义一个系统后，下一步是将像素绘制到屏幕上。 <xref:System.Windows.Media.Visual> 类可用于生成视觉对象的树，每个对象都可以有选择性地包含绘制说明以及有关如何呈现这些说明的元数据（剪辑、转换等）。 <xref:System.Windows.Media.Visual> 旨在实现非常轻量且灵活，因此，大多数功能都没有公共 API 泄露，并且很大程度上依赖于受保护的回调函数。  
  
 <xref:System.Windows.Media.Visual> 确实是 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 组合系统的入口点。 <xref:System.Windows.Media.Visual> 是这两个子系统之间的连接点，即托管 API 和非托管 milcore。  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 通过遍历由 milcore 管理的非托管数据结构来显示数据。 这些结构（称为组合节点）代表层次结构显示树，其中每个节点都有呈现指令。 只能通过消息传递协议来访问此树（如下图右侧所示）。  
  
 在对 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]进行编程时，可以创建 <xref:System.Windows.Media.Visual> 元素和派生类型，这些派生类型在内部通过此消息传递协议与组合树通信。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的每个 <xref:System.Windows.Media.Visual> 可以创建一个、无或多个组合节点。  
  
 ![Windows Presentation Foundation 的可视化树。](./media/wpf-architecture2.PNG "wpf_architecture2")  
  
 请注意一个非常重要的体系结构细节 - 会缓存整个可视化树和绘制指令。 在图形方面，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 使用一个保留的绘制系统。 这可以实现以高刷新率重绘系统，并且组合系统不会阻止对用户代码的回调。 这有助于防止出现应用程序无响应的情况。  
  
 关系图中容易忽略的另一个重要细节是系统实际执行组合的方式。  
  
 在 User32 和 GDI 中，系统在即时模式剪辑系统上工作。 当需要绘制一个组件时，系统会建立一个剪裁边界，在此边界外，不允许组件接触像素，然后会要求组件在该框中绘制像素。 此系统在内存受限的系统上工作良好，因为当某些内容更改时，只需处理受影响的组件即可 - 不会由两个组件同时处理一个像素的颜色。  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 使用“绘画器的算法”绘制模型。 要求每个组件从显示内容的背面绘制到正面，而不是剪裁每个组件。 这允许每个组件在先前组件的显示内容上绘制。 此模型的优点是可以生成部分透明的复杂形状。 在当今的新式图形硬件中，此模型的速度相对较快（这种情况并不是在创建 User32/GDI 的情况下）。  
  
 如上所述，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的一个核心原理是转移到一个更具声明性且“以属性为中心”的编程模型。 在可视化系统中，这体现在有意思的几个方面。  
  
 首先，对于保留的模式图形系统，这实际上是从命令性 DrawLine/DrawLine 类型模型移动到面向数据的模型 new Line()/new Line()。 通过这种向数据驱动的绘制的移动，可以使用属性表达绘制指令上的复杂操作。 派生自 <xref:System.Windows.Media.Drawing> 的类型实际上是用于呈现的对象模型。  
  
 第二，如果评估动画系统，你会发现它几乎是完全声明性的。 可以将动画表示为动画对象上的一组属性，无需要求开发人员计算下一个位置或下一个颜色。 这些动画可以表达开发人员或设计人员的意图（在 5 秒内将此按钮从一个位置移动到另一个位置），系统可以确定完成此任务的最高效方式。  
  
<a name="System_Windows_UIElement"></a>   
## <a name="systemwindowsuielement"></a>System.Windows.UIElement  
 <xref:System.Windows.UIElement> 定义包括布局、输入和事件在内的核心子系统。  
  
 布局是 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的核心概念。 在许多系统中，可能有一组固定的布局模型（HTML 支持三种布局模型：流、绝对和表），也可能没有布局模型（User32 实际仅支持绝对定位）。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 先假设开发人员和设计人员需要灵活的可扩展布局模型，该模型可能是由属性值而不是命令性逻辑驱动的。 在 <xref:System.Windows.UIElement> 级别，会引入布局的基本协定–两阶段模型，其中包含 <xref:System.Windows.UIElement.Measure%2A> 和 <xref:System.Windows.UIElement.Arrange%2A>。  
  
 <xref:System.Windows.UIElement.Measure%2A> 允许组件确定要采用的大小。 这是与 <xref:System.Windows.UIElement.Arrange%2A> 分离的阶段，因为在很多情况下，父元素会请求子元素多次测量，以确定其最佳位置和大小。 父元素要求子元素测量这一事实体现了 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的另一关键原则 - 调整内容大小。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的所有控件支持调整到内容自然大小的功能。 这使本地化更加容易，并可实现调整内容大小时进行动态元素布局。 <xref:System.Windows.UIElement.Arrange%2A> 阶段允许父项定位并确定每个子级的最终大小。  
  
 经常会花费大量时间来谈论 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的输出端– <xref:System.Windows.Media.Visual> 和相关对象。 然而，在输入端也有许多创新。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 输入模型中的最基本更改也许是一致模型，借助此模型可通过系统对输入事件进行路由。  
  
 输入是作为内核模式设备驱动程序上的信号发出的，并通过涉及 Windows 内核和 User32 的复杂过程路由到正确的进程和线程。 与输入相对应的 User32 消息路由到 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 后，转换为 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 原始输入消息，并发送到调度程序。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 允许将原始输入事件转换为多个实际事件，在保证传递到位的情况下在低系统级别实现类似“MouseEnter”的功能。  
  
 每个输入事件至少会转换为两个事件 -“预览”事件和实际事件。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的所有事件都具有通过元素树路由的概念。 如果事件从目标向上遍历到根，则称为 "冒泡"; 如果从根开始向下遍历到目标，则称为 "隧道"。 输入预览事件隧道，使树中的任何元素都有机会筛选事件或对事件采取操作。 然后，常规（非预览）事件将从目标向上浮升到根。  
  
 隧道和浮升阶段之间的划分使键盘快捷键等功能的实现在复合环境中采用一致的方式。 在 User32 中，可以通过使用一个全局表来实现键盘快捷键，该表中包含你希望支持的所有快捷键（Ctrl+N 映射到“新建”）。 在应用程序的调度程序中，可以调用 **TranslateAccelerator**，它会探查 User32 中的输入消息，并确定是否有任何消息与已注册的快捷键匹配。 在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中，上述内容无效，因为系统是完全“可组合”的 - 任何元素都可以处理和使用任何键盘快捷键。 将此两阶段模型用于输入，可允许组件实现其自己的“TranslateAccelerator”。  
  
 为了进一步执行此步骤，<xref:System.Windows.UIElement> 还介绍了 CommandBindings 的概念。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 命令系统使开发人员可以根据命令终结点（实现 <xref:System.Windows.Input.ICommand>的内容）定义功能。 命令绑定使元素可以定义输入笔势 (Ctrl+N) 和命令（“新建”）之间的映射。 输入笔势和命令定义都是可扩展的，并且可以在使用时联系到一起。 这使得一些操作（例如，允许最终用户自定义其要在应用程序内使用的键绑定）显得无关紧要。  
  
 至此，本主题已重点讨论了 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的“核心”功能 - PresentationCore 程序集中实现的功能。 在构建 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]时，基础组件（如与**度量值**和**排列**布局的协定）和框架块（如 <xref:System.Windows.Controls.Grid>的特定布局的实现）之间的完全分离是所需的结果。 目标是提供在堆栈中处于较低位置的可扩展性点，这将允许外部开发人员在需要时创建自己的框架。  
  
<a name="System_Windows_FrameworkElement"></a>   
## <a name="systemwindowsframeworkelement"></a>System.Windows.FrameworkElement  
 可以通过两种不同的方式查看 <xref:System.Windows.FrameworkElement>。 它在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的较低层中引入的子系统上引入一组策略和自定义项。 它还引入了一组新的子系统。  
  
 <xref:System.Windows.FrameworkElement> 引入的主要策略围绕应用程序布局。 <xref:System.Windows.FrameworkElement> 以 <xref:System.Windows.UIElement> 引入的基本布局约定为基础，并添加布局 "槽" 的概念，这使得布局作者可以更轻松地使用一致的属性驱动布局语义集。 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>、<xref:System.Windows.FrameworkElement.VerticalAlignment%2A>、<xref:System.Windows.FrameworkElement.MinWidth%2A>和 <xref:System.Windows.FrameworkElement.Margin%2A> 等属性（几个属性）将从布局容器内 <xref:System.Windows.FrameworkElement> 一致的行为中获得派生的所有组件。  
  
 <xref:System.Windows.FrameworkElement> 还为 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]的核心层中的许多功能提供了更轻松的 API 公开。 例如，<xref:System.Windows.FrameworkElement> 通过 <xref:System.Windows.FrameworkElement.BeginStoryboard%2A> 方法提供对动画的直接访问。 <xref:System.Windows.Media.Animation.Storyboard> 提供了一种针对一组属性编写多个动画的脚本的方法。  
  
 <xref:System.Windows.FrameworkElement> 介绍的两个最关键的方面是数据绑定和样式。  
  
 对于已使用 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 或 ASP.NET 创建应用程序 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]的任何人而言，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的数据绑定子系统应相对熟悉。 在上述每个系统中，可通过一种简单的方式来表达希望将给定元素中的一个或多个属性绑定到一个数据片段。 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 完全支持属性绑定、转换和列表绑定。  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中数据绑定的最值得关注的功能之一是引入了数据模板。 利用数据模板，可以通过声明方式指定某个数据片断的可视化方式。 无需创建可绑定到数据的自定义用户界面，而是转而让数据来确定要创建的显示内容。  
  
 样式实际上是轻量型的数据绑定。 使用样式，可以将共享定义的一组属性绑定到元素的一个或多个实例。 样式通过显式引用（通过设置 <xref:System.Windows.FrameworkElement.Style%2A> 属性）或通过将样式与元素的 CLR 类型关联来隐式应用于元素。  
  
<a name="System_Windows_Controls_Control"></a>   
## <a name="systemwindowscontrolscontrol"></a>System.Windows.Controls.Control  
 控件的最重要功能是模板化。 如果将 WPF 的组合系统视为一个保留模式绘制系统，则控件可通过模板化以一种参数化的声明性方式描述其绘制。 <xref:System.Windows.Controls.ControlTemplate> 实际上只是一个脚本，用于创建一组子元素，并将绑定到控件提供的属性。  
  
 <xref:System.Windows.Controls.Control> 提供了一组常用属性（<xref:System.Windows.Controls.Control.Foreground%2A>、<xref:System.Windows.Controls.Control.Background%2A><xref:System.Windows.Controls.Control.Padding%2A>）来命名几个模板，然后模板作者可以使用这些属性自定义控件的显示。 控件的实现提供了数据模型和交互模型。 交互模型定义了一组命令（如窗口的“关闭”），以及到输入笔势的绑定（如单击窗口右上角的红叉）。 数据模型提供了一组属性，用于自定义交互模型或自定义显示内容（由模板确定）。  
  
 数据模型（属性）、交互模型（命令和事件）及显示模型（模板）之间的划分，可实现对控件的外观和行为的完全自定义。  
  
 最常见的控件数据模型是内容模型。 如果你查看类似 <xref:System.Windows.Controls.Button>的控件，你会看到它有一个类型为 "Content" 的属性 <xref:System.Object>。 在 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 和 ASP.NET 中，此属性通常是一个字符串，但它限制了可放入按钮中的内容的类型。 按钮的内容可以是简单的字符串、复杂的数据对象或整个元素树。 如果是数据对象，可以使用数据模板构造显示内容。  
  
<a name="Summary"></a>   
## <a name="summary"></a>总结  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 可创建动态的数据驱动的演示系统。 系统的每一部分均可通过驱动行为的属性集来创建对象。 数据绑定是系统的基础部分，在每一层中均进行了集成。  
  
 传统的应用程序创建一个显示内容，然后绑定到某些数据。 在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中，控件的所有内容、显示内容的所有方面都是由某种类型的数据绑定生成的。 通过在按钮内部创建复合控件并将其显示内容绑定到按钮的内容属性，会显示按钮中的文本。  
  
 当开始开发基于 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的应用程序时，你应感到非常熟悉。 可以设置属性、使用对象和数据绑定，其方式与使用 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 或 ASP.NET 的方式大致相同。 如果对 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 体系结构有更深的了解，将能够创建更丰富的应用程序，这些应用程序在根本上会将数据视为应用程序的核心驱动要素。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Windows.Media.Visual>
- <xref:System.Windows.UIElement>
- <xref:System.Windows.Input.ICommand>
- <xref:System.Windows.FrameworkElement>
- <xref:System.Windows.Threading.DispatcherObject>
- <xref:System.Windows.Input.CommandBinding>
- <xref:System.Windows.Controls.Control>
- [数据绑定概述](../../../desktop-wpf/data/data-binding-overview.md)
- [布局](layout.md)
- [动画概述](../graphics-multimedia/animation-overview.md)
