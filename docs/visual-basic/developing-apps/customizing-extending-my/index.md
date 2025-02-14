---
title: 利用 Visual Basic 自定义项目并扩展 My 对象
ms.date: 07/20/2015
helpviewer_keywords:
- My namespace [Visual Basic], customizing
- My namespace
- My namespace [Visual Basic], extending
ms.assetid: 06ca80b9-1192-4eb5-8537-8ef5edfb9be0
ms.openlocfilehash: 97933a9d014a54d5b6e333090cddccace99fcc3c
ms.sourcegitcommit: 9b2ef64c4fc10a4a10f28a223d60d17d7d249ee8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2019
ms.locfileid: "72960945"
---
# <a name="customizing-projects-and-extending-my-with-visual-basic"></a>利用 Visual Basic 自定义项目并扩展 My 对象

你可以自定义项目模板以提供额外的 `My` 对象。 这样，其他开发人员便可以轻松查找和使用您的对象。

## <a name="in-this-section"></a>本节内容

- [扩展 Visual Basic 中的 My 命名空间](extending-the-my-namespace.md)  
 描述如何将自定义成员和值添加到 Visual Basic 中的 `My` 命名空间。
- [打包和部署自定义 My 扩展](packaging-and-deploying-custom-my-extensions.md)  
 介绍如何使用 Visual Studio 模板发布自定义 `My` 命名空间扩展。
- [扩展 Visual Basic 应用程序模型](extending-the-visual-basic-application-model.md)  
 介绍如何通过重写 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> 类的成员，为应用程序模型指定您自己的扩展。
- [自定义 My 中可用的对象](customizing-which-objects-are-available-in-my.md)  
 介绍如何通过设置项目的 \_MYTYPE 条件编译常量来控制要启用的 `My` 对象。

## <a name="related-sections"></a>相关章节

- [使用 My 开发](../development-with-my/index.md)  
 说明默认情况下，不同项目类型中可用的 `My` 对象。
- [Visual Basic 应用程序模型概述](../development-with-my/overview-of-the-visual-basic-application-model.md)  
 介绍 Visual Basic 用于控制 Windows 窗体应用程序行为的模型。
- [My 对项目类型的依赖方式](../development-with-my/how-my-depends-on-project-type.md)  
 说明默认情况下，不同项目类型中可用的 `My` 对象。
- [条件编译](../../programming-guide/program-structure/conditional-compilation.md)  
 讨论编译器如何使用条件编译来选择代码的特定部分，以便编译和排除其他部分。
- <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>  
 介绍提供与当前应用程序相关的属性、方法和事件的 `My` 对象。

## <a name="see-also"></a>请参阅

- [使用 Visual Basic 开发应用程序](../index.md)
