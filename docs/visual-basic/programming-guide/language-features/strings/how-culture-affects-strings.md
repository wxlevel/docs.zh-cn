---
title: 区域性对字符串的影响 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- locale [Visual Basic], effect on strings
- strings [Visual Basic], locale dependence
ms.assetid: c4664444-ee0d-47bf-bef1-eaa3c54bdd7f
ms.openlocfilehash: d090a6e89a470958dd323c3f249ed0658dc1cefa
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69955101"
---
# <a name="how-culture-affects-strings-in-visual-basic"></a>区域性对字符串的影响 (Visual Basic)
此帮助页讨论 Visual Basic 如何使用区域性信息来执行字符串转换和比较。  
  
## <a name="when-to-use-culture-specific-strings"></a>何时使用特定于区域性的字符串  
 通常, 应为向用户显示的所有数据使用特定于区域性的字符串, 并对应用程序的内部数据使用区域性固定字符串。  
  
 例如, 如果您的应用程序要求用户以字符串的形式输入日期, 则应期望用户根据其区域性设置字符串的格式, 并且应用程序应正确地转换字符串。 如果你的应用程序在其用户界面中显示该日期, 则它应以用户的区域性显示该日期。  
  
 但是, 如果应用程序将日期上传到中央服务器, 则应根据特定区域性设置字符串的格式, 以防止可能不同的日期格式之间发生混淆。  
  
## <a name="culture-sensitive-functions"></a>区分区域性的函数  
 所有 Visual Basic 字符串转换函数 ( `Str`和`Val`函数除外) 都使用应用程序的区域性信息来确保转换和比较适用于应用程序的区域性用户.  
  
 在具有不同区域性设置的计算机上运行的应用程序中成功使用字符串转换函数的关键是要了解哪些函数使用特定的区域性设置, 以及哪些函数使用当前区域性设置。 请注意, 应用程序的区域性设置默认情况下从操作系统的区域性设置继承而来。 有关详细信息, 请<xref:Microsoft.VisualBasic.Strings.Asc%2A>参阅<xref:Microsoft.VisualBasic.Strings.AscW%2A> <xref:Microsoft.VisualBasic.Strings.Chr%2A>、、 <xref:Microsoft.VisualBasic.Strings.ChrW%2A>、 <xref:Microsoft.VisualBasic.Strings.Format%2A>、、、和[类型转换函数。](../../../../visual-basic/language-reference/functions/type-conversion-functions.md) <xref:Microsoft.VisualBasic.Conversion.Hex%2A> <xref:Microsoft.VisualBasic.Conversion.Oct%2A>  
  
 在`Str`字符串和数字之间进行转换时`Val` , (将数字转换为字符串) 和 (将字符串转换为数字) 函数不使用应用程序的区域性信息。 相反, 它们仅将句点 (.) 识别为有效的小数点分隔符。 这些函数的区域性感知物是:  
  
- **使用当前区域性的转换。** 和函数将数字转换为字符串, `CDbl`并且和`CInt`函数将字符串转换为数字。 `Format` `CStr`  
  
- **使用特定区域性的转换。** 每个 number 对象都`ToString(IFormatProvider)`有一个将数字转换为字符串的方法, `Parse(String, IFormatProvider)`以及用于将字符串转换为数字的方法。 例如, `Double`类型<xref:System.Double.ToString%28System.IFormatProvider%29>提供了和<xref:System.Double.Parse%28System.String%2CSystem.IFormatProvider%29>方法。  
  
 有关详细信息，请参阅 <xref:Microsoft.VisualBasic.Conversion.Str%2A> 和 <xref:Microsoft.VisualBasic.Conversion.Val%2A>。  
  
## <a name="using-a-specific-culture"></a>使用特定区域性  
 假设您正在开发一个应用程序, 该应用程序将日期 (格式为字符串) 发送到 Web 服务。 在这种情况下, 应用程序必须使用特定的区域性进行字符串转换。 为了阐明原因, 请考虑使用日期<xref:System.DateTime.ToString>方法的结果:如果你的应用程序使用该方法格式化日期2005年7月4日, 则它会在使用美国英语 (zh-cn) 区域性运行时返回 "7/4/2005 12:00:00 AM", 但当使用德语 (de de) 区域性运行时, 它将返回 "04.07.2005 00:00:00"。  
  
 如果需要以特定的区域性格式执行字符串转换, 则应使用`CultureInfo`内置到 .NET Framework 中的类。 可以通过将区域性名称`CultureInfo`传递<xref:System.Globalization.CultureInfo.%23ctor%2A>到构造函数, 为特定区域性创建新的对象。 <xref:System.Globalization.CultureInfo>类帮助页中列出了支持的区域性名称。  
  
 或者, 您可以从<xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType>属性获取*固定区域性*的实例。 固定区域性基于英语区域性, 但有一些差异。 例如, 固定区域性指定24小时制, 而不是12小时制时钟。  
  
 若要将日期转换为区域性的字符串, 请将<xref:System.Globalization.CultureInfo>对象传递给 date 对象的<xref:System.DateTime.ToString%28System.IFormatProvider%29>方法。 例如, 下面的代码显示 "07/04/2005 00:00:00", 而不管应用程序的区域性设置如何。  
  
 [!code-vb[VbVbalrConcepts#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConcepts/VB/Class1.vb#1)]  
  
> [!NOTE]
> 始终根据英语区域性解释日期文本。  
  
## <a name="comparing-strings"></a>比较字符串  
 需要进行字符串比较的两个重要情况如下:  
  
- **为向用户显示的数据排序。** 使用基于当前区域性的操作, 以便字符串进行适当排序。  
  
- **确定两个应用程序内部字符串是否完全匹配 (通常出于安全目的)。** 使用忽略当前区域性的操作。  
  
 您可以与 Visual Basic <xref:Microsoft.VisualBasic.Strings.StrComp%2A>函数同时执行这两种类型的比较。 指定用于控制`Compare`比较类型的可选参数: `Text`对于用于确定完全匹配项的`Binary`大多数输入和输出。  
  
 `StrComp`函数返回一个整数, 该整数指示这两个比较的字符串与排序顺序之间的关系。 如果结果为正值, 则指示第一个字符串大于第二个字符串。 如果结果为负, 则指示第一个字符串较小, 0 表示字符串之间相等。  
  
 [!code-vb[VbVbalrStrings#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class1.vb#22)]  
  
 你还可以使用该`StrComp`函数的 .NET Framework 合作伙伴<xref:System.String.Compare%2A?displayProperty=nameWithType> , 即方法。 这是基字符串类的静态重载方法。 下面的示例演示如何使用此方法:  
  
 [!code-vb[VbVbalrStrings#48](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#48)]  
  
 为了更好地控制执行比较的方式, 您可以使用<xref:System.String.Compare%2A>方法的其他重载。 使用方法, 可以使用参数指定要使用的比较类型。 `comparisonType` <xref:System.String.Compare%2A?displayProperty=nameWithType>  
  
|参数的`comparisonType`值|比较类型|何时使用|  
|---|---|---|  
|`Ordinal`|基于字符串的组件字节的比较。|比较时使用此值: 区分大小写的标识符、与安全相关的设置, 或字节必须完全匹配的其他非语言标识符。|  
|`OrdinalIgnoreCase`|基于字符串的组件字节的比较。<br /><br /> `OrdinalIgnoreCase`使用固定区域性信息确定两个字符的大小写不同。|比较时使用此值: 不区分大小写的标识符、与安全相关的设置和存储在 Windows 中的数据。|  
|`CurrentCulture` 或 `CurrentCultureIgnoreCase`|基于当前区域性中的字符串解释的比较。|比较时使用这些值: 向用户显示的数据、大多数用户输入和需要语言解释的其他数据。|  
|`InvariantCulture` 或 `InvariantCultureIgnoreCase`|基于字符串在固定区域性中的解释的比较。<br /><br /> 这不同于`Ordinal`和`OrdinalIgnoreCase`, 因为固定区域性会将其接受范围外的字符视为等效的固定字符。|仅在比较持久化数据或显示需要固定排序顺序的语言相关数据时, 才使用这些值。|  
  
### <a name="security-considerations"></a>安全注意事项  
 如果你的应用程序根据比较或大小写更改操作的结果做出安全决策, 则操作应<xref:System.String.Compare%2A?displayProperty=nameWithType>使用方法, 并传递`Ordinal`或`OrdinalIgnoreCase`作为`comparisonType`参数。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Globalization.CultureInfo>
- [Visual Basic 中的字符串简介](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)
- [类型转换函数](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)
