---
title: mc:Ignorable 特性
ms.date: 03/30/2017
helpviewer_keywords:
- mc XML namespace prefix [WPF]
- mc:Ignorable attribute
- XML [WPF], mc namespace prefix
- XAML [WPF], mc:Ignorable attribute
- mc:ProcessContent attribute
- XAML [WPF], mc:ProcessContent attribute
ms.assetid: acd9a6ef-b7ca-4146-abb6-60f3b366e9ec
ms.openlocfilehash: d8fdeec8784c9a44c9b272a0a5a8b9c56ace5230
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2019
ms.locfileid: "73458826"
---
# <a name="mcignorable-attribute"></a>mc:Ignorable 特性
指定 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器可能会忽略在标记文件中遇到的 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 命名空间前缀。 `mc:Ignorable` 特性支持用于自定义命名空间映射和 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 版本控制的标记兼容性。  
  
## <a name="xaml-attribute-usage-single-prefix"></a>XAML 特性用法（单前缀）  
  
```xaml  
<object  
  xmlns:ignorablePrefix="ignorableUri"  
  xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
  mc:Ignorable="ignorablePrefix"...>  
    <ignorablePrefix1:ThisElementCanBeIgnored/>  
</object>  
```  
  
## <a name="xaml-attribute-usage-two-prefixes"></a>XAML 特性用法（两个前缀）  
  
```xaml  
<object  
  xmlns:ignorablePrefix1="ignorableUri"  
  xmlns:ignorablePrefix2="ignorableUri2"  
  xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
  mc:Ignorable="ignorablePrefix1 ignorablePrefix2"...>  
    <ignorablePrefix1:ThisElementCanBeIgnored/>  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 值  
  
|||  
|-|-|  
|*ignorablePrefix、ignorablePrefix1 等。*|根据 XML 1.0 规范的任何有效的前缀字符串。|  
|*ignorableUri*|根据 XML 1.0 规范指定命名空间的任何有效 URI。|  
|*ThisElementCanBeIgnored*|如果无法解析基础类型，则 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 处理器实现可忽略的元素。|  
  
## <a name="remarks"></a>备注  
 `mc` [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 命名空间前缀是在映射 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 兼容性命名空间 `http://schemas.openxmlformats.org/markup-compatibility/2006`时要使用的建议前缀约定。  
  
 元素名称的前缀部分标识为 `mc:Ignorable` 在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器处理时不会引发错误的元素或属性。 如果该特性未能解析为基础类型或编程构造，则将忽略该元素。 但请注意，如果忽略元素，则忽略的元素可能仍会生成其他元素要求的分析错误。 例如，特定的元素内容模型可能只需要一个子元素，但如果指定的子元素位于 `mc:Ignorable` 前缀中，并且指定的子元素未能解析为类型，则 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器可能会引发错误。  
  
 `mc:Ignorable` 仅适用于标识符字符串的命名空间映射。 `mc:Ignorable` 不适用于将命名空间映射到程序集，这些程序集指定 CLR 命名空间和程序集（或作为程序集的当前可执行文件的默认值）。  
  
 如果要实现 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器，则处理器实现对于由标识为 `mc:Ignorable`的前缀限定的任何元素或属性，都不得引发分析或处理错误。 但您的处理器实现仍可能引发异常，这些异常是无法加载或处理元素的辅助结果，如前面给出的一个子元素示例。  
  
 默认情况下，[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器将忽略忽略元素中的内容。 但是，您可以指定一个附加属性[mc： ProcessContent 特性](mc-processcontent-attribute.md)，以要求在下一个可用的父元素中继续处理被忽略元素内的内容。  
  
 可以使用一个或多个空白字符作为分隔符，在属性中指定多个前缀，例如： `mc:Ignorable="ignore1 ignore2"`。  

 `http://schemas.openxmlformats.org/markup-compatibility/2006` 命名空间定义 SDK 的此区域中未记录的其他元素和特性。 有关详细信息，请参阅[XML 标记兼容性规范](/office/open-xml/introduction-to-markup-compatibility#markup-compatibility-in-the-open-xml-file-formats-specification)。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Windows.Markup.XamlReader>
- [PresentationOptions:Freeze 特性](presentationoptions-freeze-attribute.md)
- [XAML 概述 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
- [WPF 中的文档](documents-in-wpf.md)
