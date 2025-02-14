---
title: 如何：使用焦点事件更改元素的颜色
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- focus events [WPF], changing element color for
- colors of elements [WPF], changing
- elements [WPF], changing color of
ms.assetid: 7e246802-3625-47a7-ae9d-c8a2a40fd040
ms.openlocfilehash: 5c59dc5f2f8f26fac69933f9ef641a3a51306619
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004833"
---
# <a name="how-to-change-the-color-of-an-element-using-focus-events"></a>如何：使用焦点事件更改元素的颜色
此示例演示如何在使用 @no__t 0 和 @no__t 1 事件时更改元素的颜色，并使其失去焦点。  
  
 此示例由一个 @no__t 0 文件和一个代码隐藏文件组成。  
  
## <a name="example"></a>示例  
 以下 XAML 创建用户界面，该用户界面由两个 @no__t 0 对象组成，并将 @no__t 的事件处理程序和 @no__t 2 事件附加 @no__t 到3个对象。  
  
 [!code-xaml[gotfocusLostfocusEffectUsingEvent#GotLostFocusSampleXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/gotfocusLostfocusEffectUsingEvent/CSharp/Window1.xaml#gotlostfocussamplexaml)]  
  
 下面的代码将创建 @no__t 0 和 @no__t 事件处理程序。  当 @no__t 0 获取键盘焦点时，<xref:System.Windows.Controls.Button> 的 @no__t 更改为红色。  当 @no__t 0 失去键盘焦点时，@no__t 的 @no__t 1 将改回为白色。  
  
 [!code-csharp[gotfocusLostfocusEffectUsingEvent#GotLostFocusSampleEventHandlers](~/samples/snippets/csharp/VS_Snippets_Wpf/gotfocusLostfocusEffectUsingEvent/CSharp/Window1.xaml.cs#gotlostfocussampleeventhandlers)]
 [!code-vb[gotfocusLostfocusEffectUsingEvent#GotLostFocusSampleEventHandlers](~/samples/snippets/visualbasic/VS_Snippets_Wpf/gotfocusLostfocusEffectUsingEvent/VisualBasic/Window1.xaml.vb#gotlostfocussampleeventhandlers)]  
  
## <a name="see-also"></a>请参阅

- [输入概述](input-overview.md)
