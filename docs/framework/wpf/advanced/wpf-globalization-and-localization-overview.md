---
title: WPF 全球化和本地化概述
ms.date: 03/30/2017
helpviewer_keywords:
- globalization [WPF], about globalization
- localization [WPF], about localization
ms.assetid: 56e5a5c8-6c96-4d19-b8e1-a5be1dc564af
ms.openlocfilehash: a912e0437bf986aff65fc722065e912571427189
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2019
ms.locfileid: "73035785"
---
# <a name="wpf-globalization-and-localization-overview"></a>WPF 全球化和本地化概述

当你将自己的产品限制为只能通过一种语言使用时，便将潜在的客户群限制为全球 65 亿人口中的一小部分。 如果想让自己的应用程序被全球用户所接受，那么对产品进行经济而有效的本地化将是赢得更多客户的最好、最经济的方法。

本概述介绍 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]中的全球化和本地化。 全球化是指设计和开发在多个地点执行的应用程序。 例如，全球化支持适用于不同区域性用户的本地化用户界面和区域数据。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了全球化设计功能，包括自动布局、附属程序集以及本地化特性和注释。

本地化是针对应用程序所支持的特定区域性将应用程序资源转换为本地化版本的过程。 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]中进行本地化时，使用 <xref:System.Windows.Markup.Localizer> 命名空间中的 Api。 这些 Api 支持[LocBaml 工具的示例](https://go.microsoft.com/fwlink/?LinkID=160016)命令行工具。 有关如何生成和使用 LocBaml 的信息，请参阅[本地化应用程序](how-to-localize-an-application.md)。

## <a name="best-practices-for-globalization-and-localization-in-wpf"></a>在 WPF 中进行全球化和本地化的最佳做法

通过遵循本部分提供的 UI 设计和本地化相关提示，你可以充分利用中 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内置的大多数全球化和本地化功能。

### <a name="best-practices-for-wpf-ui-design"></a>WPF UI 设计的最佳做法

设计基于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]时，请考虑实施以下最佳做法：

- 将 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 写入 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]中;避免在代码中创建 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。 使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]创建 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 时，可以通过内置的本地化 Api 公开此。

- 避免使用绝对位置和固定大小对内容进行布局;请改用相对或自动调整大小。

  - 使用 <xref:System.Windows.Window.SizeToContent%2A>，并将宽度和高度设置为 `Auto`。

  - 避免使用 <xref:System.Windows.Controls.Canvas> 对 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]进行布局。

  - 使用 <xref:System.Windows.Controls.Grid> 及其大小的共享功能。

- 在边距中提供额外的空间，因为本地化文本通常需要更多空间。 额外空间为可能会延伸的字符预留了余地。

- 启用 <xref:System.Windows.Controls.TextBlock> 上的 <xref:System.Windows.Controls.TextBlock.TextWrapping%2A> 以避免剪辑。

- 设置 `xml:lang` 特性。 此属性描述特定元素及其子元素的区域性。 此属性的值更改 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]中多个功能的行为。 例如，它可以更改断字、拼写检查、数字替换、复杂脚本成型和字体回退的行为。 有关[在 XAML 中设置 xml： Lang 处理](../../xaml-services/xml-lang-handling-in-xaml.md)的详细信息，请参阅适用于[WPF 的全球化](globalization-for-wpf.md)。

- 创建自定义的复合字体，以更好地控制用于不同语言的字体。 默认情况下，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 使用 Windows\Fonts 目录中的 GlobalUserInterface 字体。

- 当你创建的导航应用程序可能在以从右向左格式呈现文本的区域性中进行本地化时，请显式设置每个页面的 <xref:System.Windows.FlowDirection>，以确保页面不会从 <xref:System.Windows.Navigation.NavigationWindow>继承 <xref:System.Windows.FlowDirection>。

- 当你创建在浏览器外部托管的独立导航应用程序时，将初始应用程序的 <xref:System.Windows.Application.StartupUri%2A> 设置为 <xref:System.Windows.Navigation.NavigationWindow> 而不是页（例如 `<Application StartupUri="NavigationWindow.xaml">`）。 利用此设计，您可以更改窗口和导航栏的 <xref:System.Windows.FlowDirection>。 有关详细信息和示例，请参阅[全球化主页示例](https://go.microsoft.com/fwlink/?LinkID=159990)。

### <a name="best-practices-for-wpf-localization"></a>WPF 本地化的最佳做法

当你对基于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]的应用程序进行本地化时，请考虑实施下列最佳做法：

- 使用本地化注释为本地化人员提供额外的上下文。

- 使用本地化特性来控制本地化，而不是选择性地省略元素上的 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性。 有关详细信息，请参阅[本地化特性和注释](localization-attributes-and-comments.md)。

- 使用 `msbuild -t:updateuid` 和 `-t:checkuid` 添加和检查 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]中的 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性。 使用 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性跟踪开发和本地化之间的更改。 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性可帮助你本地化新的开发更改。 如果手动将 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性添加到 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]中，则该任务通常单调乏味且不太准确。

  - 开始本地化后，请不要编辑或更改 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性。

  - 不要使用重复的 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性（在使用复制和粘贴命令时请记住此提示）。

  - 设置 AssemblyInfo 中的 `UltimateResourceFallback` 位置，以便为回退指定适当的语言（例如，`[assembly: NeutralResourcesLanguage("en-US",   UltimateResourceFallbackLocation.Satellite)]`）。

    如果通过省略项目文件中的 `<UICulture>` 标记来决定在主程序集中包含源语言，请将 `UltimateResourceFallback` 位置设置为主程序集而不是附属程序集（例如 `[assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.MainAssembly)]`）。

## <a name="localize-a-wpf-application"></a>对 WPF 应用程序进行本地化

对 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序进行本地化时，有几个选项。 例如，可以将应用程序中的可本地化资源绑定到 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 文件，将可本地化的文本存储在 resx 表中，或让本地化人员使用 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 文件。 本部分介绍使用 XAML 的 BAML 形式的本地化工作流，该工作流提供以下几个优点：

- 您可以在生成后进行本地化。

- 您可以使用 XAML 的 BAML 形式的更早版本中的本地化更新为 XAML 的 BAML 形式的更高版本，以便您可以在开发时进行本地化。

- 可以在编译时验证原始源元素和语义，因为 XAML 的 BAML 形式是 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]的编译形式。

### <a name="localization-build-process"></a>本地化生成过程

开发 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序时，本地化的生成过程如下所示：

- 开发人员创建并其全球化 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序。 在开发人员将 `<UICulture>en-US</UICulture>` 的项目文件中，这样，在编译应用程序时，将生成一个非特定语言的主程序集。 此程序集具有一个附属 .resources.dll 文件，其中包含所有可本地化的资源。 您可以根据需要将源语言保留在主程序集中，因为我们的本地化 Api 支持从主程序集进行提取。

- 将该文件编译为生成时，[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 将转换为 XAML 的 BAML 形式。 非特定区域性 `MyDialog.exe` 和与区域性相关的（英语） `MyDialog.resources.dll` 文件将发布给英语客户。

### <a name="localization-workflow"></a>本地化工作流

本地化过程在生成未本地化 `MyDialog.resources.dll` 文件后开始。 原始 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素和属性通过使用 <xref:System.Windows.Markup.Localizer>下的 Api 从 XAML 的 BAML 形式提取到键值对。 本地化人员使用键/值对来对应用程序进行本地化。 在本地化完成之后，可以从新值生成一个新的 .resource.dll。

键/值对的键是 `x:Uid` 开发人员置于原始 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]中的值。 这些 `x:Uid` 值使 API 能够跟踪和合并本地化期间开发人员和本地化人员之间发生的更改。 例如，如果在本地化人员开始本地化后，开发人员更改了 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，则可以将开发更改与已完成的本地化工作合并，以便最小翻译工作丢失。

下图显示了一个基于 XAML 的 BAML 形式的典型本地化工作流。 此关系图假设开发人员用英语编写应用程序。 开发人员创建 WPF 应用程序并将其全球化。 开发人员将 `<UICulture>en-US</UICulture>` 的项目文件设置为在生成时，使用包含所有可本地化资源的附属. .resources 生成语言中性主程序集。 或者，因为 WPF 本地化 API 支持从主程序集进行提取，所以还可以保留主程序集中的源语言。 生成过程结束之后，XAML 会编译为 BAML。 将向说英语的客户提供非特定区域性的 MyDialog.exe.resources.dll。

![显示本地化工作流的关系图。](./media/wpf-globalization-and-localization-overview/localization-workflow.png)

![显示未本地化工作流的关系图。](./media/wpf-globalization-and-localization-overview/unlocalized-workflow.png)

## <a name="examples-of-wpf-localization"></a>WPF 本地化示例

本部分包含可帮助你了解如何生成和本地化 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序的本地化应用程序的示例。

#### <a name="run-dialog-box-example"></a>“运行”对话框示例

下图显示 "**运行**" 对话框示例的输出。

**英语：**

![显示 "英语运行" 对话框的屏幕截图。](./media/wpf-globalization-and-localization-overview/run-dialog-box-english.png)

**德语：**

![显示德语 "运行" 对话框的屏幕截图。](./media/wpf-globalization-and-localization-overview/run-dialog-box-german.png)

**设计全球化“运行”对话框**

此示例通过使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]生成一个 "**运行**" 对话框。 此对话框等效于 Microsoft Windows "开始" 菜单中提供的 "**运行**" 对话框。

生成全球化对话框的一些要点包括：

**自动布局**

*在 Window1.xaml 中：*

`<Window SizeToContent="WidthAndHeight">`

以前的 Window 属性会根据内容大小自动调整窗口大小。 此属性可以防止窗口切断在本地化之后大小增加的内容；它还可以在内容由于本地化而大小减小时删除不必要的空格。

`<Grid x:Uid="Grid_1">`

要使 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的本地化 Api 正常工作，<xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性是必需的。

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 本地化 Api 使用这些方法跟踪 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]的开发和本地化之间的更改。 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性使你能够将较新版本的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 与 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]的较旧本地化合并在一起。 可以通过在命令行界面中运行 `msbuild -t:updateuid RunDialog.csproj` 来添加 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性。 这是添加 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性的建议方法，因为手动添加它们通常是耗时且不太准确的。 可以通过运行 `msbuild -t:checkuid RunDialog.csproj`来检查 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> 属性是否正确设置。

通过使用 <xref:System.Windows.Controls.Grid> 控件来构造 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，这是在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]中利用自动布局的有用控件。 请注意，对话框拆分成三行五列。 不是行和列定义中的一个具有固定的大小;因此，位于每个单元格中的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素可以在本地化过程中适应大小的增加和减小。

[!code-xaml[GlobalizationRunDialog#GridColumnDef](~/samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationRunDialog/CS/Window1.xaml#gridcolumndef)]

放置**打开的：** 标签和 <xref:System.Windows.Controls.ComboBox> 的前两列使用 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 总宽度的10%。

[!code-xaml[GlobalizationRunDialog#GridColumnDef2](~/samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationRunDialog/CS/Window1.xaml#gridcolumndef2)]

请注意，此示例使用 <xref:System.Windows.Controls.Grid>的共享大小调整功能。 最后三列通过将其放在同一 <xref:System.Windows.Controls.DefinitionBase.SharedSizeGroup%2A>中来利用这一点。 正如属性名称所示，此属性允许不同的列采用相同大小。 因此，当 "浏览 ..."已本地化为较长的字符串 "Durchsuchen ... ..."，所有按钮的宽度都将增加，而不是使用较小的 "确定" 按钮和不成比例的 "Durchsuchen ... ..."鼠标.

**xml： lang**

`xml:lang="en-US"`

请注意， [XAML 中的 xml： Lang 处理](../../xaml-services/xml-lang-handling-in-xaml.md)置于 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]的根元素中。 此属性描述给定元素及其子元素的区域性。 此值由 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的多个功能使用，并且应在本地化过程中相应地进行更改。 此值会更改在断字以及对字词进行拼写检查时所使用的字典。 它还会影响数字的显示以及字体回退系统选择所用字体的方式。 最后，该属性会影响数值的显示方式，形成在复杂脚本中编写文本的方式。 默认值为“en-US”。

**生成附属资源程序集**

*在 .csproj 中：*

编辑 `.csproj` 文件，并将以下标记添加到无条件 `<PropertyGroup>`：

`<UICulture>en-US</UICulture>`

请注意，添加了 `UICulture` 值。 如果将此项设置为有效 <xref:System.Globalization.CultureInfo> 值（例如 en-us），则生成项目时将生成包含其中所有可本地化资源的附属程序集。

`<Resource Include="RunIcon.JPG">`

`<Localizable>False</Localizable>`

`</Resource>`

不需要对 `RunIcon.JPG` 进行本地化，因为它对于所有区域性都应该是相同的。 `Localizable` 设置为 `false`，以使其保留在语言中性主程序集中，而不是附属程序集。 所有 noncompilable 资源的默认值均 `Localizable` 设置为 `true`。

**本地化“运行”对话框**

**分析**

生成应用程序之后，对其进行本地化的第一步是将可本地化的资源从附属程序集中分析出来。 出于本主题的目的，请使用示例 LocBaml 工具，该工具可在[LocBaml 工具示例](https://go.microsoft.com/fwlink/?LinkID=160016)中找到。 请注意，LocBaml 只是一个示例工具，用于帮助你了解有关如何生成适合你的本地化过程的本地化工具的入门知识。 使用 LocBaml，运行以下内容来分析： **LocBaml/Parse rundialog.csproj/out：** 生成 "rundialog.csproj" 文件的文件。

**本地化**

使用你喜欢的支持 Unicode 的 CSV 编辑器来编辑此文件。 筛选掉本地化类别为“None”的所有项。 应看到下面的项：

|资源键|本地化类别|“值”|
|-|-|-|
|Button_1:System.Windows.Controls.Button.$Content|Button|确定|
|Button_2:System.Windows.Controls.Button.$Content|Button|取消|
|Button_3:System.Windows.Controls.Button.$Content|Button|浏览...|
|ComboBox_1:System.Windows.Controls.ComboBox.$Content|组合框||
|TextBlock_1:System.Windows.Controls.TextBlock.$Content|Text|Windows 将根据您所输入的名称，为您打开相应的程序、文件夹、文档或 Internet 资源。|
|TextBlock_2:System.Windows.Controls.TextBlock.$Content|Text|打开:|
|Window_1:System.Windows.Window.Title|Title|运行|

将该应用程序本地化为德语版本需要进行下面的翻译：

|资源键|本地化类别|“值”|
|-|-|-|
|Button_1:System.Windows.Controls.Button.$Content|Button|确定|
|Button_2:System.Windows.Controls.Button.$Content|Button|Abbrechen|
|Button_3:System.Windows.Controls.Button.$Content|Button|Durchsuchen…|
|ComboBox_1:System.Windows.Controls.ComboBox.$Content|组合框||
|TextBlock_1:System.Windows.Controls.TextBlock.$Content|Text|Geben Sie den Namen eines Programms, Ordners, Dokuments oder einer Internetresource an.|
|TextBlock_2:System.Windows.Controls.TextBlock.$Content|Text|Öffnen:|
|Window_1:System.Windows.Window.Title|Title|运行|

**生成**

本地化的最后一步涉及创建新进行本地化的附属程序集。 可以使用下面的 LocBaml 命令完成此操作：

**LocBaml.exe /generate RunDialog.resources.dll /trans:RunDialog.resources.dll.CSV /out: . /cul:de-DE**

在德语窗口上，如果将此资源 .dll 放置在主程序集旁边的取消拖放文件夹中，则此资源将自动加载，而不是 en-us 文件夹中的一个。 如果你没有德语版本的 Windows 来测试这种情况，请将区域性设置为要使用的 Windows 的任何区域性（例如 `en-US`），并替换原始的资源 DLL。

**附属资源加载**

|MyDialog.exe|en-US\MyDialog.resources.dll|de-DE\MyDialog.resources.dll|
|------------------|------------------------------------|------------------------------------|
|代码|原始英语版 BAML|本地化的 BAML|
|非特定区域性资源|其他英语资源|已本地化为德语的其他资源|

.NET framework 会根据应用程序的 `Thread.CurrentThread.CurrentUICulture`自动选择要加载的附属资源程序集。 此值默认为 Windows OS 的区域性。 因此，如果您使用的是德语 Windows，则会加载 de-DE\MyDialog.resources.dll，如果您使用的是英语 Windows，则 en-US\MyDialog.resources.dll 会加载。 通过在项目的 AssemblyInfo.* 中指定 NeutralResourcesLanguage，可以设置应用程序的最终回退资源。 例如，如果指定：

`[assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.Satellite)]`

如果 de-DE\MyDialog.resources.dll 和 de\MyDialog.resources.dll 都不可用，则德语版 Windows 将使用 en-US\MyDialog.resources.dll。

### <a name="microsoft-saudi-arabia-homepage"></a>Microsoft 沙特阿拉伯主页

下图显示了英语和阿拉伯语主页。 有关生成这些图形的完整示例，请参阅[全球化主页示例](https://go.microsoft.com/fwlink/?LinkID=159990)。

**英语：**

![显示英语主页的屏幕截图。](./media/wpf-globalization-and-localization-overview/english-home-page-sample.jpg)

**阿拉伯语：**

![显示阿拉伯语主页的屏幕截图。](./media/wpf-globalization-and-localization-overview/arabic-home-page-sample.jpg)

### <a name="designing-a-global-microsoft-home-page"></a>设计全球 Microsoft 主页

Microsoft 沙特阿拉伯网站的这个实体模型说明了针对从右向左布局语言提供的全球化功能。 希伯来语和阿拉伯语等语言具有从右到左的阅读顺序，因此，[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 布局的布局通常与从左到右的语言（如英语）的布局不同。 从从左到右布局语言本地化到从右到左布局语言可能相当困难，反之亦然。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 可使此类本地化工作变得更容易。

**FlowDirection**

*Homepage.xaml:*

[!code-xaml[GlobalizationHomepage#Homepage](~/samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationHomepage/CS/Homepage.xaml#homepage)]

请注意 <xref:System.Windows.Controls.Page>上的 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 属性。 将此属性更改为 "<xref:System.Windows.FlowDirection.RightToLeft> 将更改 <xref:System.Windows.Controls.Page> 及其子元素的 <xref:System.Windows.FrameworkElement.FlowDirection%2A>，以便将此 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的布局反向转换为与阿拉伯语用户所期望的从右到左。 通过在任何元素上指定显式 <xref:System.Windows.FrameworkElement.FlowDirection%2A>，可以重写继承行为。 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 属性可用于任何 <xref:System.Windows.FrameworkElement> 或文档相关元素，并且具有隐式值 <xref:System.Windows.FlowDirection.LeftToRight>。

请注意，当根 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 更改时，即使背景渐变画笔也能正确翻转：

**FlowDirection="LeftToRight"**

![显示从左到右的渐变流的屏幕截图。](./media/wpf-globalization-and-localization-overview/gradient-flow-left-right.png)

**FlowDirection="RightToLeft"**

![显示从右到左渐变流的屏幕截图。](./media/wpf-globalization-and-localization-overview/gradient-flow-right-left.png)

**避免对面板和控件使用固定维度**

浏览主页 .xaml，注意除了为顶部 <xref:System.Windows.Controls.DockPanel>上的整个 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 指定的固定宽度和高度以外，没有其他固定尺寸。 请勿使用固定尺寸，以防裁剪可能比源文本长的本地化文本。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 面板和控件将根据其所包含的内容自动调整大小。 大多数控件也具有可以设置以进行更多控制的最小和最大尺寸（例如，MinWidth = "20"）。 使用 <xref:System.Windows.Controls.Grid>，还可以通过使用 "\*" （例如 `Width="0.25*"`）或使用其单元大小共享功能设置相对宽度和高度。

**本地化注释**

在很多情况下，内容可能不太明确，难以翻译。 开发人员或设计人员可通过本地化注释为本地化人员提供额外的上下文和注释。 例如，下面的 Localization.Comments 阐明了字符“|”的用法。

[!code-xaml[GlobalizationHomepage#LocalizationComment](~/samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationHomepage/CS/Homepage.xaml#localizationcomment)]

此注释与 TextBlock_1's 内容相关联，在 LocBaml 工具的情况下（请参阅[本地化应用程序](how-to-localize-an-application.md)），可以在输出 .csv 文件的 TextBlock_1 行的第6列中看到该注释：

|资源键|类别|可读性|可修改性|注释|“值”|
|-|-|-|-|-|-|
|TextBlock_1:System.Windows.Controls.TextBlock.$Content|Text|true|true|此字符用作装饰性规则。|&#124;|

使用下面的语法可以将注释放置在任何元素的内容或属性上：

[!code-xaml[GlobalizationHomepage#LocalizationCommentsProp](~/samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationHomepage/CS/Homepage.xaml#localizationcommentsprop)]

**本地化特性**

通常，开发人员或本地化经理需要控制本地化人员能够阅读和修改的内容。 例如，可能不希望本地化人员翻译你公司的名称或法律用语。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了一些特性，使用这些特性可以设置元素的内容或属性（本地化工具可以使用这些内容或属性锁定、隐藏元素或对元素进行排序）的可读性、可修改性和类别。 有关更多信息，请参见<xref:System.Windows.Localization.Attributes%2A>。 此示例中 LocBaml 工具仅输出这些特性的值。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件对这些特性都使用默认值，但可以替代这些默认值。 例如，下面的示例将重写 `TextBlock_1` 的默认本地化属性，并将内容设置为可读但对于本地化人员是不可修改的。

[!code-xaml[LocalizationComAtt#LocalizationAttributes](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationComAtt/CSharp/Attributes.xaml#localizationattributes)]

除了可读性和可修改性特性之外，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 还提供了一个可用于向本地化人员提供更多上下文的常见 UI 类别（<xref:System.Windows.LocalizationCategory>）的枚举。 还可以在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中覆盖平台控件 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 默认类别：

[!code-xaml[LocalizationComAtt#LocalizationAttributesOverridden](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationComAtt/CSharp/Attributes.xaml#localizationattributesoverridden)]

还可以通过代码覆盖 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供的默认本地化特性，以便为自定义控件正确设置正确的默认值。 例如:

```csharp
[Localizability(Readability = Readability.Readable, Modifiability=Modifiability.Unmodifiable, LocalizationCategory.None)]
public class CorporateLogo : TextBlock
{
    // ...
}
```

在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中设置的每个实例属性将优先于在自定义控件的代码中设置的值。 有关属性和注释的详细信息，请参阅[本地化特性和注释](localization-attributes-and-comments.md)。

**字体回退和复合字体**

如果指定的字体不支持给定的点区范围，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 将自动回退到使用 Windows\Fonts 目录中的全局用户界面的 compositefont。 复合字体的工作方式与任何其他字体一样，可通过设置元素的 `FontFamily` （例如，`FontFamily="Global User Interface"`）来显式使用。 通过创建你自己的复合字体并指定针对特定代码点范围和语言所使用的字体，可以指定你自己的字体回退首选项。

有关复合字体的详细信息，请参阅 <xref:System.Windows.Media.FontFamily>。

**本地化 Microsoft 主页**

可以按照“运行”对话框示例中的相同步骤对此应用程序进行本地化。 在[全球化主页示例](https://go.microsoft.com/fwlink/?LinkID=159990)中提供了适用于阿拉伯语的本地化 .csv 文件。
