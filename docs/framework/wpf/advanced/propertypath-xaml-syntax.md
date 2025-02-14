---
title: PropertyPath XAML 语法
ms.date: 03/30/2017
helpviewer_keywords:
- PropertyPath object [WPF]
- XAML [WPF], PropertyPath object
ms.assetid: 0e3cdf07-abe6-460a-a9af-3764b4fd707f
ms.openlocfilehash: b2530793bfe1a158a0df1c34b2768e0c7ca351f3
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2019
ms.locfileid: "73459361"
---
# <a name="propertypath-xaml-syntax"></a>PropertyPath XAML 语法

<xref:System.Windows.PropertyPath> 对象支持复杂的内联 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 语法，用于设置采用 <xref:System.Windows.PropertyPath> 类型作为值的各种属性。 本主题将 <xref:System.Windows.PropertyPath> 语法记录为应用于绑定和动画语法。

<a name="where"></a>

## <a name="where-propertypath-is-used"></a>PropertyPath 的使用情景

<xref:System.Windows.PropertyPath> 是在多个 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 功能中使用的公共对象。 尽管使用 common <xref:System.Windows.PropertyPath> 来传达属性路径信息，但每个功能区域的用法（其中 <xref:System.Windows.PropertyPath> 用作类型）各不相同。 因此，基于每个功能来讨论语法更为可行。

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 使用 <xref:System.Windows.PropertyPath> 来描述对象模型路径，以便遍历对象数据源的属性，以及描述目标动画的目标路径。

某些样式和模板属性（如 <xref:System.Windows.Setter.Property%2A?displayProperty=nameWithType>）采用表面上类似于 <xref:System.Windows.PropertyPath>的限定属性名称。 但这并不是真正的 <xref:System.Windows.PropertyPath>;相反，它是限定*所有者。* 由 WPF [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器与 <xref:System.Windows.DependencyProperty>的类型转换器一起启用的属性字符串格式使用情况。

<a name="databinding_s"></a>

## <a name="propertypath-for-objects-in-data-binding"></a>数据绑定中对象的 PropertyPath

数据绑定是 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 功能，借此可以绑定到任意依赖属性的目标值。 但是，此类数据绑定的源不需要是依赖属性；可以是适用数据提供程序能识别的任意属性类型。 属性路径特别用于 <xref:System.Windows.Data.ObjectDataProvider>，后者用于从公共语言运行时（CLR）对象及其属性获取绑定源。

请注意，对 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 的数据绑定不使用 <xref:System.Windows.PropertyPath>，因为它不使用 <xref:System.Windows.Data.Binding>中的 <xref:System.Windows.Data.Binding.Path%2A>。 相反，可以使用 <xref:System.Windows.Data.Binding.XPath%2A>，并在数据的 [!INCLUDE[TLA#tla_xmldom](../../../../includes/tlasharptla-xmldom-md.md)] 中指定有效的 XPath 语法。 还将 <xref:System.Windows.Data.Binding.XPath%2A> 指定为字符串，但此处未记录此内容;请参阅[使用 XMLDataProvider 和 XPath 查询绑定到 XML 数据](../data/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md)。

理解数据绑定中的属性路径的关键是将绑定到单个属性值设置为目标，或者改为绑定到采用列表或集合的目标属性。 如果要绑定集合，例如绑定将根据集合中的数据项数扩展的 <xref:System.Windows.Controls.ListBox>，则属性路径应引用集合对象，而不是单个集合项。 数据绑定引擎会自动将用作数据源的集合与绑定目标的类型匹配，从而导致诸如使用 items 数组填充 <xref:System.Windows.Controls.ListBox> 的行为。

<a name="singlecurrent"></a>

### <a name="single-property-on-the-immediate-object-as-data-context"></a>直接对象上作为数据上下文的单个属性

```xml
<Binding Path="propertyName" .../>
```

*propertyName*必须解析为当前 <xref:System.Windows.FrameworkElement.DataContext%2A> 中的属性的名称，以供 <xref:System.Windows.Data.Binding.Path%2A> 使用。 如果绑定更新源，则属性必须是可读取/写入的，并且源对象必须可变。

<a name="singleindex"></a>

### <a name="single-indexer-on-the-immediate-object-as-data-context"></a>直接对象上作为数据上下文的单个索引器

```xml
<Binding Path="[key]" .../>
```

`key` 必须是字典或哈希表的类型化索引，或者是数组的整数索引。 此外，键值必须是可直接绑定到所应用属性的类型。 例如，可以通过这种方式使用包含字符串键和字符串值的哈希表绑定到 <xref:System.Windows.Controls.TextBox>的文本。 或者，如果键指向集合或子索引，则可使用此语法绑定到目标集合属性。 否则，需要通过 `<Binding Path="[key].propertyName" .../>` 等语法来引用特定属性。

如有必要，可以指定索引的类型。 有关索引属性路径的这一方面的详细信息，请参阅 <xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType>。

<a name="multipleindirect"></a>

### <a name="multiple-property-indirect-property-targeting"></a>多个属性（间接属性目标设置）

```xml
<Binding Path="propertyName.propertyName2" .../>
```

`propertyName` 必须解析为作为当前 <xref:System.Windows.FrameworkElement.DataContext%2A>的属性的名称。 路径属性 `propertyName` 和 `propertyName2` 可以是关系中的任意属性，其中 `propertyName2` 是存在于类型中的值为 `propertyName` 的属性。

<a name="singleattached"></a>

### <a name="single-property-attached-or-otherwise-type-qualified"></a>附加的或类型限定的单个属性

```xml
<object property="(ownerType.propertyName)" .../>
```

圆括号指示 <xref:System.Windows.PropertyPath> 中的此属性应使用部分限定构造。 它可以使用 XML 命名空间来查找具有适当映射的类型。 `ownerType` 通过每个程序集中的 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 声明搜索 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器有权访问的类型。 大部分应用程序都具有映射到 [!INCLUDE[TLA#tla_wpfxmlnsv1](../../../../includes/tlasharptla-wpfxmlnsv1-md.md)] 命名空间的默认 XML 命名空间，因此通常仅有自定义类型或该命名空间之外的类型才需要前缀。  `propertyName` 必须解析为 `ownerType` 中存在的属性名称。 此语法一般用于以下任一情况：

- 路径是在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中的样式或模板（该样式或模板没有指定的目标类型）中指定的。 除此之外，限定用法一般无效，因为在非样式、非模板情况下，属性存在于实例中，而不是类型中。

- 属性为附加属性。

- 要绑定到静态属性中。

要用作情节提要目标，指定为 `propertyName` 的属性必须是 <xref:System.Windows.DependencyProperty>。

<a name="sourcetraversal"></a>

### <a name="source-traversal-binding-to-hierarchies-of-collections"></a>源遍历（绑定到集合的层次结构）

```xml
<object Path="propertyName/propertyNameX" .../>
```

此语法中的 / 用于在分层数据源对象中导航，并且支持使用连续的 / 字符分多个步骤导航层次结构。 源遍历说明了当前记录指针位置，该位置是通过将数据与其视图的 UI 同步而确定的。 有关与分层数据源对象绑定的详细信息，以及数据绑定中当前记录指针的概念，请参阅[对分层数据使用主-从模式](../data/how-to-use-the-master-detail-pattern-with-hierarchical-data.md)或[数据绑定概述](../../../desktop-wpf/data/data-binding-overview.md)。

> [!NOTE]
> 此语法看起来类似 [!INCLUDE[TLA2#tla_xpath](../../../../includes/tla2sharptla-xpath-md.md)]。 绑定到 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 数据源的 true [!INCLUDE[TLA2#tla_xpath](../../../../includes/tla2sharptla-xpath-md.md)] 表达式不用作 <xref:System.Windows.Data.Binding.Path%2A> 值，应改为用于互斥 <xref:System.Windows.Data.Binding.XPath%2A> 属性。

### <a name="collection-views"></a>集合视图

若要引用一个已命名的集合视图，请使用哈希字符 (`#`) 为集合视图名称添加前缀。

### <a name="current-record-pointer"></a>当前记录指针

若要引用集合视图的当前记录指针或引用主从数据绑定方案，请启用带正斜杠 (`/`) 的路径字符串。 从当前记录指针开始遍历任何超出正斜杠的路径。

### <a name="multiple-indexers"></a>多个索引器

```xaml
<object Path="[index1,index2...]" .../>
```

或

```xaml
<object Path="propertyName[index,index2...]" .../>
```

如果给定的对象支持多个索引器，则可以按顺序指定这些索引器，类似于数组引用语法。 上述对象可以是当前上下文，也可以是包含多个索引对象的属性的值。

默认情况下，通过使用基础对象的特性来类型化索引器值。 如有必要，可以指定索引的类型。 有关键入索引器的详细信息，请参阅 <xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType>。

<a name="mixing"></a>

### <a name="mixing-syntaxes"></a>混合语法

上述每条语法都可以独立使用。 例如，下面的示例创建了一个属性路径，该属性指向 `ColorGrid` 属性（包含 <xref:System.Windows.Media.SolidColorBrush> 对象的像素网格数组）的特定 x、y 的颜色：

```xml
<Rectangle Fill="{Binding ColorGrid[20,30].SolidColorBrushResult}" .../>
```

### <a name="escapes-for-property-path-strings"></a>属性路径字符串的转义

对于某些业务对象，你可能会遇到这样的情况：属性路径字符串需要转义序列以进行正确分析。 因为大多数此类字符在常用于定义业务对象的语言方面具有类似的命名交互问题，因此转义需要非常少见。

- 在索引器 ([ ]) 内部，脱字符号 (^) 用于对下一个字符进行转义。

- 必须（使用 XML 实体）对 XML 语言定义专用的某些字符进行转义。 使用 `&` 对字符“&”进行转义。 使用 `>` 对结束标记“>”进行转义。

- 必须（使用反斜杠 `\`）对特定于 WPF XAML 分析程序行为的字符进行转义，以处理标记扩展。

  - 反斜杠 (`\`) 本身是转义字符。

  - 等号 (`=`) 将属性名与属性值分隔开。

  - 逗号 (`,`) 用于分隔属性。

  - 右大括号 (`}`) 是标记扩展的结尾。

> [!NOTE]
> 从技术上讲，这些转义符还适用于情节提要属性路径，但通常会遍历适用于现有 WPF 对象的对象模型，转义应该是不必要的。

<a name="databinding_sa"></a>

## <a name="propertypath-for-animation-targets"></a>动画目标的 PropertyPath

动画的 target 属性必须是采用 <xref:System.Windows.Freezable> 或基元类型的依赖项属性。 但是，类型中的目标属性和最终动画属性可以存在于不同的对象中。 对于动画，属性路径用于通过遍历属性值中的对象-属性关系，定义命名动画目标对象的属性和预期目标动画属性之间的连接。

<a name="general"></a>

### <a name="general-object-property-considerations-for-animations"></a>动画的一般对象-属性注意事项

有关一般动画概念的详细信息，请参阅[情节提要概述](../graphics-multimedia/storyboards-overview.md)和[动画概述](../graphics-multimedia/animation-overview.md)。

要进行动画处理的值类型或属性必须是 <xref:System.Windows.Freezable> 类型或基元类型。 启动路径的属性必须解析为存在于指定 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 类型上的依赖属性的名称。

为了支持克隆以对已冻结 <xref:System.Windows.Freezable> 进行动画处理，<xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 指定的对象必须是 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement> 派生类。

<a name="singlestepanim"></a>

### <a name="single-property-on-the-target-object"></a>目标对象上的单个属性

```xml
<animation Storyboard.TargetProperty="propertyName" .../>
```

`propertyName` 必须解析为存在于指定 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 类型上的依赖属性的名称。

<a name="indirectanim"></a>

### <a name="indirect-property-targeting"></a>间接属性目标设定

```xml
<animation Storyboard.TargetProperty="propertyName.propertyName2" .../>
```

`propertyName` 必须是指定 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 类型上存在 <xref:System.Windows.Freezable> 值类型或基元类型的属性。

`propertyName2` 必须为依赖属性的名称，该属性存在于作为 `propertyName` 值的对象中。 换句话说，`propertyName2` 必须作为 `propertyName` <xref:System.Windows.DependencyProperty.PropertyType%2A>的类型的依赖项属性存在。

因为应用了样式和模板，所以间接设定动画的目标是必要的。 若要以动画为目标，需要对目标对象具有 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A>，且该名称是由[x：Name](../../xaml-services/x-name-directive.md)或 <xref:System.Windows.FrameworkElement.Name%2A>建立的。 虽然模板和样式元素也可以有名称，但这些名称仅在样式和模板的命名范围内有效。 （如果模板和样式与应用程序标记共享命名范围，则名称不唯一。 样式和模板按字面方式在实例之间共享，并且将保持重复的名称。）因此，如果您想要对某个元素的单个属性进行动画处理，则需要从样式或模板开始，而不是从样式模板开始，然后以样式或模板可视化树为目标，以到达属性要进行动画处理。

例如，<xref:System.Windows.Controls.Panel> 的 <xref:System.Windows.Controls.Panel.Background%2A> 属性是来自主题模板的完整 <xref:System.Windows.Media.Brush> （实际上是 <xref:System.Windows.Media.SolidColorBrush>）。 若要完全对 <xref:System.Windows.Media.Brush> 进行动画处理，需要 BrushAnimation （可能每个 <xref:System.Windows.Media.Brush> 类型都有一个），并且没有此类类型。 若要对画笔进行动画处理，请改为对特定 <xref:System.Windows.Media.Brush> 类型的属性进行动画处理。 需要从 <xref:System.Windows.Media.SolidColorBrush> 到 <xref:System.Windows.Media.SolidColorBrush.Color%2A>，以便在其中应用 <xref:System.Windows.Media.Animation.ColorAnimation>。 本示例的属性路径是 `Background.Color`。

<a name="attachedanim"></a>

### <a name="attached-properties"></a>附加属性

```xml
<animation Storyboard.TargetProperty="(ownerType.propertyName)" .../>
```

圆括号指示 <xref:System.Windows.PropertyPath> 中的此属性应使用部分限定构造。 可以使用 XML 命名空间来查找类型。 `ownerType` 通过每个程序集中的 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 声明搜索 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器有权访问的类型。 大部分应用程序都具有映射到 [!INCLUDE[TLA#tla_wpfxmlnsv1](../../../../includes/tlasharptla-wpfxmlnsv1-md.md)] 命名空间的默认 XML 命名空间，因此通常仅有自定义类型或该命名空间之外的类型才需要前缀。 `propertyName` 必须解析为 `ownerType` 中存在的属性名称。 指定为 `propertyName` 的属性必须是 <xref:System.Windows.DependencyProperty>。 （所有 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 附加属性都实现为依赖属性，因此该问题仅与自定义附加属性相关。）

<a name="indexanim"></a>

### <a name="indexers"></a>索引器

```xml
<animation Storyboard.TargetProperty="propertyName.propertyName2[index].propertyName3" .../>
```

大多数依赖属性或 <xref:System.Windows.Freezable> 类型不支持索引器。 因此，动画路径中唯一使用索引器的地方是在用于启动命名目标上的链的属性与最终动画属性之间的中间位置。 在提供的语法中，为 `propertyName2`。 例如，如果中间属性是 <xref:System.Windows.Media.TransformGroup>的集合（如 `RenderTransform.Children[1].Angle`），则可能需要使用索引器。

<a name="ppincode"></a>

## <a name="propertypath-in-code"></a>代码中的 PropertyPath

<xref:System.Windows.PropertyPath>的代码用法（包括如何构造 <xref:System.Windows.PropertyPath>）记录在有关 <xref:System.Windows.PropertyPath>的参考主题中。

通常，<xref:System.Windows.PropertyPath> 旨在使用两个不同的构造函数，一个用于绑定使用情况和最简单的动画用法，另一个用于复杂动画用法。 将 <xref:System.Windows.PropertyPath.%23ctor%28System.Object%29> 签名用于绑定用法，其中，对象是一个字符串。 为单步动画路径（其中对象是一个 <xref:System.Windows.DependencyProperty>）使用 <xref:System.Windows.PropertyPath.%23ctor%28System.Object%29> 签名。 对复杂动画使用 <xref:System.Windows.PropertyPath.%23ctor%28System.String%2CSystem.Object%5B%5D%29> 签名。 后一种构造函数使用第一个参数的令牌字符串，以及在该令牌字符串中填充位置的对象的数组，以定义属性路径关系。

## <a name="see-also"></a>请参阅

- <xref:System.Windows.PropertyPath>
- [数据绑定概述](../../../desktop-wpf/data/data-binding-overview.md)
- [演示图板概述](../graphics-multimedia/storyboards-overview.md)
