---
title: 动画概述
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Storyboards [WPF], animations
- animations [WPF], overview
ms.assetid: bd9ce563-725d-4385-87c9-d7ee38cf79ea
ms.openlocfilehash: 870fc1d1f02dca7d4488a27385fcfeaec8098ced
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2019
ms.locfileid: "73039179"
---
# <a name="animation-overview"></a>动画概述

<a name="introduction"></a>
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 提供了一组功能强大的图形和布局功能，使你能够创建引人注目的用户界面和引人注目的文档。 动画不仅可以使引起注意的用户界面更加引人注目，还可以使其更加便于使用。 只需对背景色进行动画处理或应用动画的 <xref:System.Windows.Media.Transform>，就可以创建生动的屏幕过渡或提供有用的视觉提示。

本概述介绍了 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 动画和计时系统。 它侧重于使用情节提要 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 对象的动画。

<a name="introducinganimations"></a>

## <a name="introducing-animations"></a>动画简介

动画是快速循环播放一系列图像（其中每个图像与下一个图像略微不同）给人造成的一种幻觉。 大脑感觉这组图像是一个变化的场景。 在电影中，摄像机每秒钟拍摄许多照片（帧），便可使人形成这种幻觉。 用投影仪播放这些帧时，观众便可以看电影了。

计算机上的动画与此类似。 例如，使一个矩形图形逐渐从视野中消失的程序可能按以下方式工作。

- 程序创建一个计时器。

- 程序按照设定的时间间隔检查计时器以查看经历了多长时间。

- 程序每次检查计时器时，它将根据经历的时间来计算矩形的当前不透明度值。

- 然后，程序用新值更新矩形并重画此矩形。

在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]之前，Microsoft Windows 开发人员必须创建和管理自己的计时系统或使用特殊的自定义库。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 包括通过托管代码公开的有效计时系统，并 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 并深度集成到 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 框架中。 通过使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 动画，可以轻松地对控件和其他图形对象进行动画处理。

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 可以高效地处理管理计时系统和重绘屏幕的所有后台任务。 它提供了计时类，使用户能够重点关注要创造的效果，而非实现这些效果的机制。 此外，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 通过公开动画基类（你使用的类可以继承这些类）可以轻松创建自己的动画，这样便可以制作自定义动画。 这些自定义动画获得了标准动画类的许多性能优点。

<a name="thewpftimingsystem"></a>

## <a name="wpf-property-animation-system"></a>WPF 属性动画系统

如果你了解有关计时系统的几个重要概念，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 动画可能更易于使用。 最重要的是，在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]中，可以通过将动画应用于各自的属性来对对象进行动画处理。 例如，若要使框架元素增长，请对其 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 属性进行动画处理。 若要使对象从视图中淡化，请对其 <xref:System.Windows.UIElement.Opacity%2A> 属性进行动画处理。

若要使属性具有动画功能，属性必须满足以下三个要求：

- 它必须是依赖属性。

- 它必须属于从 <xref:System.Windows.DependencyObject> 继承并实现 <xref:System.Windows.Media.Animation.IAnimatable> 接口的类。

- 必须存在可用的兼容动画类型。 （如果 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 未提供，你可以创建自己的。 请参阅[自定义动画概述](custom-animations-overview.md)。）

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 包含许多具有 <xref:System.Windows.Media.Animation.IAnimatable> 属性的对象。 控件（如 <xref:System.Windows.Controls.Button> 和 <xref:System.Windows.Controls.TabControl>）以及 <xref:System.Windows.Controls.Panel> 和 <xref:System.Windows.Shapes.Shape> 对象从 <xref:System.Windows.DependencyObject>继承。 其中大多数属性都是依赖属性。

几乎可以在任何地方使用动画，包括在样式和控件模板中使用。 动画未必可见；如果不属于用户界面的对象满足本部分中所述的条件，则可以对其进行动画处理。

<a name="storyboardwalkthrough"></a>

## <a name="example-make-an-element-fade-in-and-out-of-view"></a>示例：使元素逐渐进入视野并从视野中逐渐消失

此示例演示如何使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 动画对依赖属性的值进行动画处理。 它使用 <xref:System.Windows.Media.Animation.DoubleAnimation>，它是一种用于生成 <xref:System.Double> 值以对 <xref:System.Windows.Shapes.Rectangle>的 <xref:System.Windows.UIElement.Opacity%2A> 属性进行动画处理的动画类型。 因此，<xref:System.Windows.Shapes.Rectangle> 淡入和淡出视野。

该示例的第一部分创建一个 <xref:System.Windows.Shapes.Rectangle> 元素。 下面的步骤演示如何创建动画并将其应用到矩形的 <xref:System.Windows.UIElement.Opacity%2A> 属性。

下面演示了如何在 XAML 中的 <xref:System.Windows.Controls.StackPanel> 中创建 <xref:System.Windows.Shapes.Rectangle> 元素。

[!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_1](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_1)]

下面演示了如何在代码中的 <xref:System.Windows.Controls.StackPanel> 中创建 <xref:System.Windows.Shapes.Rectangle> 元素。

[!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_1](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_1)]
[!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_1)]

<a name="opacity_animation_step1"></a>

### <a name="part-1-create-a-doubleanimation"></a>第 1 部分：创建 DoubleAnimation

使元素淡入和淡出的一种方法是对其 <xref:System.Windows.UIElement.Opacity%2A> 属性进行动画处理。 由于 <xref:System.Windows.UIElement.Opacity%2A> 属性的类型 <xref:System.Double>，因此需要一个生成双精度值的动画。 <xref:System.Windows.Media.Animation.DoubleAnimation> 是一种动画。 <xref:System.Windows.Media.Animation.DoubleAnimation> 在两个双精度值之间创建过渡。 若要指定其起始值，请设置其 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> 属性。 若要指定其结束值，请设置其 <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> 属性。

1. `1.0` 的不透明度值使对象完全不透明，而不透明度值 `0.0` 使其完全不可见。 若要使动画从 `1.0` 过渡到 `0.0` 请将其 <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> 属性设置为 `1.0`，并将其 <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> 属性设置为 `0.0`。 下面演示了如何在 XAML 中创建 <xref:System.Windows.Media.Animation.DoubleAnimation>。

    [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_2](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_2)]

    下面演示了如何在代码中创建 <xref:System.Windows.Media.Animation.DoubleAnimation>。

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_2](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_2)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_2)]

2. 接下来，必须指定 <xref:System.Windows.Media.Animation.Timeline.Duration%2A>。 动画的 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 指定从起始值到其目标值需要多长时间。 下面演示了如何在 XAML 中将 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 设置为五秒。

    [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_3](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_3)]

    下面演示了如何在代码中将 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 设置为五秒。

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_3](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_3)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_3)]

3. 前面的代码显示了从 `1.0` 过渡到 `0.0`的动画，这会导致目标元素从完全不透明逐渐消失到完全不可见。 若要使元素消失后变为视野，请将动画的 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 属性设置为 `true`。 若要使动画无限重复，请将其 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 属性设置为 <xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A>。 下面演示了如何在 XAML 中设置 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 和 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 属性。

    [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_4](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_4)]

    下面演示了如何在代码中设置 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 和 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 属性。

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_4](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_4)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_4)]

<a name="opacity_animation_step2"></a>

### <a name="part-2-create-a-storyboard"></a>第 2 部分：创建演示图板

若要将动画应用于对象，请创建 <xref:System.Windows.Media.Animation.Storyboard>，并使用 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 并 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 附加属性指定要进行动画处理的对象和属性。

1. 创建 <xref:System.Windows.Media.Animation.Storyboard>，并将动画添加为其子级。 下面演示了如何在 XAML 中创建 <xref:System.Windows.Media.Animation.Storyboard>。

    [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_5](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_5)]

    若要在代码中创建 <xref:System.Windows.Media.Animation.Storyboard>，请在类级别声明一个 <xref:System.Windows.Media.Animation.Storyboard> 变量。

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_100](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_100)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_100](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_100)]

    然后初始化 <xref:System.Windows.Media.Animation.Storyboard>，并将动画添加为其子级。

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_101](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_101)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_101)]

2. <xref:System.Windows.Media.Animation.Storyboard> 必须知道要应用动画的位置。 使用 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A?displayProperty=nameWithType> 附加属性指定要进行动画处理的对象。 下面演示了如何在 XAML 中将 <xref:System.Windows.Media.Animation.DoubleAnimation> 的目标名称设置为 `MyRectangle`。

    [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_6](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_6)]

    下面演示了如何在代码中将 <xref:System.Windows.Media.Animation.DoubleAnimation> 的目标名称设置为 `MyRectangle`。

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_102](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_102)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_102](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_102)]

3. 使用 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 附加属性指定要进行动画处理的属性。 下面演示了如何将动画配置为面向 XAML 中 <xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.UIElement.Opacity%2A> 属性。

    [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_7](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_7)]

    下面演示了如何将动画配置为面向代码中 <xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.UIElement.Opacity%2A> 属性。

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_103](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_103)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_103](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_103)]

有关 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 语法和其他示例的详细信息，请参阅[情节提要概述](storyboards-overview.md)。

<a name="opacity_animation_step3"></a>

### <a name="part-3-xaml-associate-the-storyboard-with-a-trigger"></a>第 3 部分 (XAML)：将演示图板与触发器关联

在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中应用和启动 <xref:System.Windows.Media.Animation.Storyboard> 的最简单方法是使用事件触发器。 本部分说明如何将 <xref:System.Windows.Media.Animation.Storyboard> 与 XAML 中的触发器相关联。

1. 创建 <xref:System.Windows.Media.Animation.BeginStoryboard> 对象并将你的情节提要关联起来。 <xref:System.Windows.Media.Animation.BeginStoryboard> 是一种应用和启动 <xref:System.Windows.Media.Animation.Storyboard>的 <xref:System.Windows.TriggerAction> 类型。

    [!code-xaml[animation_ovws_snippet#RectangleOpacityFadeExampleInline_3](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/RectangleOpacityFadeExample.xaml#rectangleopacityfadeexampleinline_3)]

2. 创建 <xref:System.Windows.EventTrigger>，并将 <xref:System.Windows.Media.Animation.BeginStoryboard> 添加到其 <xref:System.Windows.EventTrigger.Actions%2A> 集合。 将 <xref:System.Windows.EventTrigger> 的 <xref:System.Windows.EventTrigger.RoutedEvent%2A> 属性设置为要启动 <xref:System.Windows.Media.Animation.Storyboard>的路由事件。 （有关路由事件的详细信息，请参阅[路由事件概述](../advanced/routed-events-overview.md)。）

    [!code-xaml[animation_ovws_snippet#RectangleOpacityFadeExampleInline_2](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/RectangleOpacityFadeExample.xaml#rectangleopacityfadeexampleinline_2)]

3. 将 <xref:System.Windows.EventTrigger> 添加到矩形的 <xref:System.Windows.FrameworkElement.Triggers%2A> 集合。

    [!code-xaml[animation_ovws_snippet#RectangleOpacityFadeExampleInline_1](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/RectangleOpacityFadeExample.xaml#rectangleopacityfadeexampleinline_1)]

<a name="opacity_animation_step3code"></a>

### <a name="part-3-code-associate-the-storyboard-with-an-event-handler"></a>第 3 部分（代码）：将演示图板与事件处理程序关联

在代码中应用和启动 <xref:System.Windows.Media.Animation.Storyboard> 的最简单方法是使用事件处理程序。 本部分演示如何在代码中将 <xref:System.Windows.Media.Animation.Storyboard> 与事件处理程序相关联。

1. 注册矩形的 <xref:System.Windows.FrameworkElement.Loaded> 事件。

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_104](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_104)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_104](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_104)]

2. 声明事件处理程序。 在事件处理程序中，使用 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 方法应用情节提要。

    [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_105](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_105)]
    [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_105](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_105)]

### <a name="complete-example"></a>完整的示例

下面的示例演示如何创建在 XAML 中淡入和淡出视图的矩形。

[!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml#rectangleopacityfadeexamplexaml)]

下面演示了如何在代码中创建逐渐进入视野并从视野中逐渐消失的矩形。

[!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode)]
[!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode)]

<a name="animationtypes"></a>

## <a name="animation-types"></a>动画类型

由于动画生成属性值，因此不同的属性类型具有不同的动画类型。 若要对采用 <xref:System.Double>的属性（如元素的 <xref:System.Windows.FrameworkElement.Width%2A> 属性）进行动画处理，请使用生成 <xref:System.Double> 值的动画。 若要对采用 <xref:System.Windows.Point>的属性进行动画处理，请使用生成 <xref:System.Windows.Point> 值的动画等。 由于有许多不同的属性类型，因此 <xref:System.Windows.Media.Animation> 命名空间中有几个动画类。 幸运的是，它们都遵循严格的命名约定，因此可以轻松地区分它们：

- \<*类型*> 动画

  这些动画称为“From/To/By”或“基本”动画，它们在起始值和目标值之间进行动画处理，或者通过将偏移量值与其起始值相加来进行动画处理。

  - 若要指定起始值，请设置动画的“From”属性。

  - 若要指定终止值，请设置动画的“To”属性。

  - 若要指定偏移量值，请设置动画的“By”属性。

  此概述中的示例使用这些动画，因为这些动画使用起来最简单。 From/to/By 动画在 From/To/By 动画概述中进行了详细说明。

- \<*类型*> AnimationUsingKeyFrames

  关键帧动画的功能比“From/To/By”动画的功能更强大，因为可以指定任意多个目标值，甚至可以控制它们的插值方法。 某些类型只能用关键帧动画进行动画处理。 关键帧动画[概述](key-frame-animations-overview.md)中详细描述了关键帧动画。

- \<*类型*> AnimationUsingPath

  路径动画支持使用几何路径来生成动画值。

- \<*类型*> AnimationBase

  一个抽象类，它在实现它时将 \<*类型*> 值进行动画处理。 此类用作 \<*类型*> 动画和 \<*类型*> AnimationUsingKeyFrames 类的基类。 只有在想要创建自己的自定义动画时，才需要直接处理这些类。 否则，请使用 \<*类型*> 动画或关键帧\<*类型*> 动画。

在大多数情况下，您需要使用 \<*类型*> 动画类，如 <xref:System.Windows.Media.Animation.DoubleAnimation> 和 <xref:System.Windows.Media.Animation.ColorAnimation>。

下表显示了一些常用动画类型以及一些与这些类型一起使用的属性。

|属性类型|对应的基本 (From/To/By) 动画|对应的关键帧动画|对应的路径动画|用法示例|
|-------------------|----------------------------------------------------|---------------------------------------|----------------------------------|-------------------|
|<xref:System.Windows.Media.Color>|<xref:System.Windows.Media.Animation.ColorAnimation>|<xref:System.Windows.Media.Animation.ColorAnimationUsingKeyFrames>|None|对 <xref:System.Windows.Media.SolidColorBrush> 或 <xref:System.Windows.Media.GradientStop>的 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 进行动画处理。|
|<xref:System.Double>|<xref:System.Windows.Media.Animation.DoubleAnimation>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath>|对 <xref:System.Windows.Controls.DockPanel> 的 <xref:System.Windows.FrameworkElement.Width%2A> 或 <xref:System.Windows.Controls.Button>的 <xref:System.Windows.FrameworkElement.Height%2A> 进行动画处理。|
|<xref:System.Windows.Point>|<xref:System.Windows.Media.Animation.PointAnimation>|<xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames>|<xref:System.Windows.Media.Animation.PointAnimationUsingPath>|对 <xref:System.Windows.Media.EllipseGeometry>的 <xref:System.Windows.Media.EllipseGeometry.Center%2A> 位置进行动画处理。|
|<xref:System.String>|None|<xref:System.Windows.Media.Animation.StringAnimationUsingKeyFrames>|None|对 <xref:System.Windows.Controls.TextBlock> 的 <xref:System.Windows.Controls.TextBlock.Text%2A> 或 <xref:System.Windows.Controls.Button>的 <xref:System.Windows.Controls.ContentControl.Content%2A> 进行动画处理。|

<a name="animationsaretimelines"></a>

### <a name="animations-are-timelines"></a>动画是时间线

所有动画类型都继承自 <xref:System.Windows.Media.Animation.Timeline> 类;因此，所有动画都是特定类型的时间线。 <xref:System.Windows.Media.Animation.Timeline> 定义时间段。 您可以指定时间线的*计时行为*：其 <xref:System.Windows.Media.Animation.Timeline.Duration%2A>、重复的次数，甚至还可以加快的时间。

由于动画是一个 <xref:System.Windows.Media.Animation.Timeline>，因此它也表示时间段。 动画还会在输出值通过其指定时间段（或 <xref:System.Windows.Media.Animation.Timeline.Duration%2A>）时进行计算。 在运行或“播放”动画时，动画将更新与其关联的属性。

三个频繁使用的计时属性为 <xref:System.Windows.Media.Animation.Timeline.Duration%2A>、<xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>和 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>。

#### <a name="the-duration-property"></a>Duration 属性

如前文所述，时间线表示时间段。 该时间段的长度由时间线的 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 确定，通常使用 <xref:System.Windows.Duration.TimeSpan%2A> 值来指定该时间线。 当时间线达到其持续时间的终点时，表示时间线完成了一次迭代。

动画使用其 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 属性来确定其当前值。 如果没有为动画指定 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 值，则使用默认值1秒。

下面的语法演示了 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 属性的 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 特性语法的简化版本。

*小时* `:` *分钟* `:` *秒*

下表显示了几个 <xref:System.Windows.Duration> 设置及其结果值。

|设置|所得值|
|-------------|---------------------|
|0:0:5.5|5.5 秒。|
|0:30:5.5|30 分 5.5 秒。|
|1:30:5.5|1 小时 30 分 5.5 秒。|

在代码中指定 <xref:System.Windows.Duration> 的一种方法是使用 <xref:System.TimeSpan.FromSeconds%2A> 方法创建 <xref:System.TimeSpan>，然后使用该 <xref:System.TimeSpan>声明一个新的 <xref:System.Windows.Duration> 结构。

有关 <xref:System.Windows.Duration> 值和完整 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 语法的详细信息，请参阅 <xref:System.Windows.Duration> 结构。

#### <a name="autoreverse"></a>AutoReverse

<xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 属性指定时间线在到达其 <xref:System.Windows.Media.Animation.Timeline.Duration%2A>的末尾后是否向后播放。 如果将此动画属性设置为 "`true`"，动画将在到达其 <xref:System.Windows.Media.Animation.Timeline.Duration%2A>的末尾后反转，并从其结束值播放回其起始值。 默认情况下，此属性 `false`。

#### <a name="repeatbehavior"></a>RepeatBehavior

<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 属性指定时间线的播放次数。 默认情况下，时间线的迭代次数为 `1.0`，这意味着它们只播放一次，根本不重复。

有关这些属性和其他属性的详细信息，请参阅[计时行为概述](timing-behaviors-overview.md)。

<a name="applyanimationstoproperty"></a>

## <a name="applying-an-animation-to-a-property"></a>对属性应用动画

前面部分介绍了动画的不同类型及其计时属性。 本部分演示如何对要进行动画处理的属性应用动画。 <xref:System.Windows.Media.Animation.Storyboard> 对象提供了一种将动画应用于属性的方式。 <xref:System.Windows.Media.Animation.Storyboard> 是为其所包含的动画提供目标信息的*容器时间线*。

### <a name="targeting-objects-and-properties"></a>以对象和属性为目标

<xref:System.Windows.Media.Animation.Storyboard> 类提供 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 和 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 附加属性。 通过在动画上设置这些属性，告诉动画对哪些内容进行动画处理。 但是，通常必须为对象提供一个名称，动画才能以该对象作为目标。

为 <xref:System.Windows.FrameworkElement> 分配名称不同于为 <xref:System.Windows.Freezable> 对象指定名称。 大多数控件和面板是框架元素；而大多数纯图形对象（如画笔、转换和几何图形）是 Freezable 对象。 如果您不确定某个类型是 <xref:System.Windows.FrameworkElement> 还是 <xref:System.Windows.Freezable>，请参阅其参考文档的 "**继承层次结构**" 部分。

- 若要将 <xref:System.Windows.FrameworkElement> 动画目标，请通过设置其 <xref:System.Windows.FrameworkElement.Name%2A> 属性为其指定一个名称。 在代码中，还必须使用 <xref:System.Windows.FrameworkElement.RegisterName%2A> 方法将元素名称注册到它所属的页面。

- 若要使 <xref:System.Windows.Freezable> 对象成为 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]中的动画目标，请使用[X：Name 指令](../../xaml-services/x-name-directive.md)为其分配名称。 在代码中，只需使用 <xref:System.Windows.FrameworkElement.RegisterName%2A> 方法将对象注册到它所属的页面。

下面的部分提供了在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 和代码中命名元素的示例。 有关命名和设定目标的更多详细信息，请参阅[情节提要概述](storyboards-overview.md)。

### <a name="applying-and-starting-storyboards"></a>应用和启动演示图板

若要在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]中启动情节提要，请将其与 <xref:System.Windows.EventTrigger>相关联。 <xref:System.Windows.EventTrigger> 是一个对象，该对象描述在发生指定事件时要执行的操作。 其中一个操作可以是 <xref:System.Windows.Media.Animation.BeginStoryboard> 操作，用于启动情节提要。 事件触发器与事件处理程序的概念类似，因为通过它们可以指定应用程序响应特定事件的方式。 与事件处理程序不同的是，事件触发器可以在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]中完全描述。不需要任何其他代码。

若要在代码中启动 <xref:System.Windows.Media.Animation.Storyboard>，可以使用 <xref:System.Windows.EventTrigger> 或使用 <xref:System.Windows.Media.Animation.Storyboard> 类的 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 方法。

<a name="controllingstoryboards"></a>

## <a name="interactively-control-a-storyboard"></a>以交互方式控制演示图板

前面的示例演示了如何在事件发生时启动 <xref:System.Windows.Media.Animation.Storyboard>。 你还可以在启动后以交互方式控制 <xref:System.Windows.Media.Animation.Storyboard>：可以暂停、继续、停止、将其前进到填充期、查找和删除 <xref:System.Windows.Media.Animation.Storyboard>。 有关演示如何以交互方式控制 <xref:System.Windows.Media.Animation.Storyboard>的详细信息和示例，请参阅[情节提要概述](storyboards-overview.md)。

<a name="fillbehaviorsection"></a>

## <a name="what-happens-after-an-animation-ends"></a>动画结束后，会发生什么情况？

<xref:System.Windows.Media.Animation.FillBehavior> 属性指定时间线在结束时的行为方式。 默认情况下，时间线在结束时 <xref:System.Windows.Media.Animation.ClockState.Filling> 开始。 <xref:System.Windows.Media.Animation.ClockState.Filling> 保存其最终输出值的动画。

上一示例中的 <xref:System.Windows.Media.Animation.DoubleAnimation> 未结束，因为其 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 属性设置为 <xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A>。 下面的示例使用类似的动画对矩形进行动画处理。 与前面的示例不同，此动画的 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> 和 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> 属性将保留其默认值。 因此，动画运行五秒钟使其不透明度值从 1 转变成 0，然后停止。

[!code-xaml[animation_ovws_snippet#FillBehaviorExampleRectangleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/FillBehaviorExample.xaml#fillbehaviorexamplerectangleinline)]

[!code-csharp[animation_ovws_procedural_snip#FillBehaviorExampleRectangleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_procedural_snip/CSharp/FillBehaviorExample.cs#fillbehaviorexamplerectangleinline)]
[!code-vb[animation_ovws_procedural_snip#FillBehaviorExampleRectangleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws_procedural_snip/visualbasic/fillbehaviorexample.vb#fillbehaviorexamplerectangleinline)]

由于未将其 <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> 更改为其默认值（这是 <xref:System.Windows.Media.Animation.FillBehavior.HoldEnd>的），因此动画结束时将保留其最终值0。 因此，在动画结束后，矩形的 <xref:System.Windows.UIElement.Opacity%2A> 保持为0。 如果将矩形的 <xref:System.Windows.UIElement.Opacity%2A> 设置为另一个值，则代码看起来不起作用，因为动画仍会影响 <xref:System.Windows.UIElement.Opacity%2A> 属性。

在代码中重新获取动画属性的控制的一种方法是使用 <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> 方法，并为 <xref:System.Windows.Media.Animation.AnimationTimeline> 参数指定 null。 有关详细信息和示例，请参阅[使用情节提要对属性进行动画处理后设置该属性](how-to-set-a-property-after-animating-it-with-a-storyboard.md)。

请注意，虽然设置具有 <xref:System.Windows.Media.Animation.ClockState.Active> 或 <xref:System.Windows.Media.Animation.ClockState.Filling> 动画的属性值似乎不起作用，但属性值确实会更改。 有关详细信息，请参阅[动画和计时系统概述](animation-and-timing-system-overview.md)。

<a name="databindingAndAnimatingAnimationsSection"></a>

## <a name="data-binding-and-animating-animations"></a>对动画进行数据绑定和动画处理

大多数动画属性可进行数据绑定或动画处理;例如，可以对 <xref:System.Windows.Media.Animation.DoubleAnimation>的 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> 属性进行动画处理。 但是，由于计时系统工作方式的缘故，进行了数据绑定和动画处理的动画的行为与其他进行了数据绑定和动画处理的对象不同。 若要了解它们的行为，请了解对属性应用动画的意义，这将十分有用。

请参阅上一节中的示例，该示例演示如何对矩形的 <xref:System.Windows.UIElement.Opacity%2A> 进行动画处理。 加载上一示例中的矩形时，其事件触发器会应用 <xref:System.Windows.Media.Animation.Storyboard>。 计时系统创建 <xref:System.Windows.Media.Animation.Storyboard> 及其动画的副本。 这些副本会被冻结（变为只读），并从它们创建 <xref:System.Windows.Media.Animation.Clock> 对象。 这些时钟将执行对目标属性进行动画处理的实际工作。

计时系统为 <xref:System.Windows.Media.Animation.DoubleAnimation> 创建一个时钟，并将其应用于 <xref:System.Windows.Media.Animation.DoubleAnimation>的 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 和 <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 指定的对象和属性。 在这种情况下，计时系统会将时钟应用于名为 "MyRectangle" 的对象的 <xref:System.Windows.UIElement.Opacity%2A> 属性。

尽管还为 <xref:System.Windows.Media.Animation.Storyboard>创建了时钟，但时钟不会应用于任何属性。 其目的是控制其子时钟，即为 <xref:System.Windows.Media.Animation.DoubleAnimation>创建的时钟。

若要使动画反映数据绑定或动画更改，必须重新生成时钟。 系统不会自动生成时钟。 若要使动画反映更改，请使用 <xref:System.Windows.Media.Animation.BeginStoryboard> 或 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 方法重新应用它的情节提要。 当使用其中一种方法时，动画将重新启动。 在代码中，可以使用 <xref:System.Windows.Media.Animation.Storyboard.Seek%2A> 方法将演示图板移回其之前的位置。

有关数据绑定动画的示例，请参阅[主要曲线动画示例](https://go.microsoft.com/fwlink/?LinkID=160011)。 有关动画和计时系统的工作原理的详细信息，请参阅[动画和计时系统概述](animation-and-timing-system-overview.md)。

<a name="otherWaysToAnimateSection"></a>

## <a name="other-ways-to-animate"></a>其他动画处理方式

此概述中的示例演示如何使用演示图板进行动画处理。 如果使用代码，可以采用一些其他方法进行动画处理。 有关详细信息，请参阅[属性动画技术概述](property-animation-techniques-overview.md)。

<a name="animation_samples"></a>

## <a name="animation-samples"></a>动画示例

以下示例有助于开始向应用程序添加动画。

- [From、To 和 By 动画目标值示例](https://go.microsoft.com/fwlink/?LinkID=159988)

  演示不同的 From/To/By 设置。

- [动画计时行为示例](https://go.microsoft.com/fwlink/?LinkID=159970)

  演示可控制动画计时行为的不同方法。 此示例还演示如何对动画的目标值进行数据绑定。

<a name="related_topics"></a>

## <a name="related-topics"></a>相关主题

|Title|描述|
|-----------|-----------------|
|[动画和计时系统概述](animation-and-timing-system-overview.md)|介绍计时系统如何使用 <xref:System.Windows.Media.Animation.Timeline> 和 <xref:System.Windows.Media.Animation.Clock> 类，这允许您创建动画。|
|[动画提示和技巧](animation-tips-and-tricks.md)|列出用于解决与动画有关的问题（如性能）的有用提示。|
|[自定义动画概述](custom-animations-overview.md)|描述如何使用关键帧、动画类或逐帧回叫来扩展动画系统。|
|[From/To/By 动画概述](from-to-by-animations-overview.md)|描述如何创建在两个值之间转换的动画。|
|[关键帧动画概述](key-frame-animations-overview.md)|描述如何使用多个目标值创建动画（包括控制内插方法的功能）。|
|[缓动函数](easing-functions.md)|说明如何将数学公式应用于动画以获得真实行为（如反弹）。|
|[路径动画概述](path-animations-overview.md)|描述如何沿复杂路径移动或旋转对象。|
|[属性动画技术概述](property-animation-techniques-overview.md)|描述使用演示图板、本地动画、时钟以及逐帧动画的属性动画。|
|[演示图板概述](storyboards-overview.md)|描述如何将演示图板与多个时间线一起使用，以创建复杂动画。|
|[计时行为概述](timing-behaviors-overview.md)|介绍动画中使用的 <xref:System.Windows.Media.Animation.Timeline> 类型和属性。|
|[计时事件概述](timing-events-overview.md)|介绍 <xref:System.Windows.Media.Animation.Timeline> 上可用的事件，以及在时间线中执行代码的 <xref:System.Windows.Media.Animation.Clock> 对象，如开始、暂停、继续、跳过或停止。|
|[帮助主题](animation-and-timing-how-to-topics.md)|包含演示在应用程序中使用动画和时间线的代码示例。|
|[时钟操作说明主题](clocks-how-to-topics.md)|包含在应用程序中使用 <xref:System.Windows.Media.Animation.Clock> 对象的代码示例。|
|[关键帧操作说明主题](key-frame-animation-how-to-topics.md)|包含在应用程序中使用关键帧动画的代码示例。|
|[路径动画操作说明主题](path-animation-how-to-topics.md)|包含在应用程序中使用路径动画的代码示例。|

<a name="reference"></a>

## <a name="reference"></a>参考

- <xref:System.Windows.Media.Animation.Timeline>

- <xref:System.Windows.Media.Animation.Storyboard>

- <xref:System.Windows.Media.Animation.BeginStoryboard>

- <xref:System.Windows.Media.Animation.Clock>
