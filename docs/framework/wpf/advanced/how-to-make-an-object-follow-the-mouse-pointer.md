---
title: 如何：使对象跟随鼠标指针移动
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- following the mouse pointer (cursor)
- mouse pointer (cursor), making objects follow
- cursor (mouse pointer), making objects follow
ms.assetid: 50b20415-14bc-405c-baf3-2fb254fffde3
ms.openlocfilehash: 4ef3028b6c71b94a593d168ad6570c4aec12b86b
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005062"
---
# <a name="how-to-make-an-object-follow-the-mouse-pointer"></a>如何：使对象跟随鼠标指针移动
此示例演示当鼠标指针移动到屏幕上时如何更改对象的尺寸。  
  
 该示例包含一个 @no__t 0 文件，该文件创建 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 和一个创建事件处理程序的代码隐藏文件。  
  
## <a name="example"></a>示例  
 以下 XAML 将创建 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，其中包含 <xref:System.Windows.Controls.StackPanel> 内的 @no__t，并附加 @no__t 3 事件的事件处理程序。  
  
 [!code-xaml[mouseMoveWithPointer#MouseMoveWithPointerXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/mouseMoveWithPointer/CSharp/Window1.xaml#mousemovewithpointerxaml)]  
  
 下面的代码将创建 <xref:System.Windows.UIElement.MouseMove> 事件处理程序。  当鼠标指针移动时，将增加和减少 @no__t 的高度和宽度。  
  
 [!code-csharp[mouseMoveWithPointer#MouseMovePointerGetPosition](~/samples/snippets/csharp/VS_Snippets_Wpf/mouseMoveWithPointer/CSharp/Window1.xaml.cs#mousemovepointergetposition)]
 [!code-vb[mouseMoveWithPointer#MouseMovePointerGetPosition](~/samples/snippets/visualbasic/VS_Snippets_Wpf/mouseMoveWithPointer/VisualBasic/Window1.xaml.vb#mousemovepointergetposition)]  
  
## <a name="see-also"></a>请参阅

- [输入概述](input-overview.md)
