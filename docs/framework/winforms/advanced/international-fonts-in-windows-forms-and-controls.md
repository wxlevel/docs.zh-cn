---
title: Windows 窗体和控件中的国际字体
ms.date: 03/30/2017
helpviewer_keywords:
- fonts [Windows Forms], international
- international applications [Windows Forms], character display
- fonts [Windows Forms], globalization considerations
- localization [Windows Forms], fonts
- Windows Forms controls, labels
- font fallback in Windows Forms
- globalization [Windows Forms], character sets
dev_langs:
- csharp
- vb
ms.assetid: 2c3066df-9bac-479a-82b2-79e484b346a3
ms.openlocfilehash: 0ddbd6d7a1b614d588a2572b410957a5ed3b768c
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71956906"
---
# <a name="international-fonts-in-windows-forms-and-controls"></a>Windows 窗体和控件中的国际字体

在国际应用程序中，建议尽可能使用字体回退来选择字体。 字体回退是指系统确定字符所属的脚本。

## <a name="using-font-fallback"></a>使用字体回退

若要利用此功能，请不要为窗体或任何其他元素设置 <xref:System.Drawing.Font> 属性。 应用程序将自动使用默认系统字体，该字体不同于操作系统的一种本地化语言。 当应用程序运行时，系统会自动为操作系统中选定的区域性提供正确的字体。

不设置字体的规则有一个例外，即更改字体样式。 这对于应用程序而言很重要，用户在该应用程序中单击按钮以使文本框中的文本以粗体显示。 为此，您可以编写一个函数，根据窗体的字体是，将文本框的字体样式更改为粗体。 在两个位置调用此函数很重要：在按钮的 @no__t 0 事件处理程序中，以及在 @no__t 事件处理程序中。 如果仅在 @no__t 0 事件处理程序中调用函数，而其他代码段更改整个窗体的字体系列，则文本框不会随窗体的其余部分而更改。

```vb
Private Sub MakeBold()
   ' Change the TextBox to a bold version of the form font
   TextBox1.Font = New Font(Me.Font, FontStyle.Bold)
End Sub

Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
   ' Clicking this button makes the TextBox bold
   MakeBold()
End Sub

Private Sub Form1_FontChanged(ByVal sender As Object, ByVal e As System.EventArgs) Handles MyBase.FontChanged
   ' If the TextBox is already bold and the form's font changes,
   ' change the TextBox to a bold version of the new form font
   If (TextBox1.Font.Style = FontStyle.Bold) Then
      MakeBold()
   End If
End Sub
```

```csharp
private void button1_Click(object sender, System.EventArgs e)
{
   // Clicking this button makes the TextBox bold
   MakeBold();
}

private void MakeBold()
{
   // Change the TextBox to a bold version of the form's font
   textBox1.Font = new Font(this.Font, FontStyle.Bold);
}

private void Form1_FontChanged(object sender, System.EventArgs e)
{
   // If the TextBox is already bold and the form's font changes,
   // change the TextBox to a bold version of the new form font
   if (textBox1.Font.Style == FontStyle.Bold)
   {
      MakeBold();
   }
}
```

但是，在对应用程序进行本地化时，对于某些语言，粗体字显示的字体可能会很差。 如果需要考虑这一点，您希望本地化人员可以选择将字体从粗体切换为普通文本。 由于本地化人员通常不是开发人员，因此不能访问源代码，因此，只需在资源文件中设置此选项。 为此，请将 <xref:System.Drawing.Font.Bold%2A> 属性设置为 `true`。 这会导致将字体设置写出到资源文件，本地化人员可以在这些资源文件中对其进行编辑。 然后，在 `InitializeComponent` 方法之后编写代码，以根据窗体的字体为，但使用资源文件中指定的字体样式来重置字体。

```vb
TextBox1.Font = New System.Drawing.Font(Me.Font, TextBox1.Font.Style)
```

```csharp
textBox1.Font = new System.Drawing.Font(this.Font, textBox1.Font.Style);
```
  
## <a name="see-also"></a>请参阅

- [使用字体和文本](using-fonts-and-text.md)
