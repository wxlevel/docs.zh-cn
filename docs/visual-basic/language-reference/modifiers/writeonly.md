---
title: WriteOnly (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- WriteOnly
- vb.WriteOnly
helpviewer_keywords:
- write-only properties
- WriteOnly keyword [Visual Basic]
- sensitive data, protecting
- properties [Visual Basic], write-only
- sensitive data
ms.assetid: 488d2899-b09f-4cee-92f0-6f9f9fc4f944
ms.openlocfilehash: 43507ac8e9b5843e8fa9496737a3d77b3a425a7f
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963772"
---
# <a name="writeonly-visual-basic"></a>WriteOnly (Visual Basic)
指定可以写入但不能读取属性。  
  
## <a name="remarks"></a>备注  
  
## <a name="rules"></a>规则  
 **声明上下文。** 只能在模块级别使用 `WriteOnly`。 这意味着`WriteOnly`属性的声明上下文必须是类、结构或模块, 不能是源文件、命名空间或过程。  
  
 可以将属性声明为, `WriteOnly`但不能将变量声明为。  
  
## <a name="when-to-use-writeonly"></a>何时使用 WriteOnly  
 有时, 您希望使用的代码能够设置一个值, 但不会发现它是什么。 例如, 需要保护敏感数据 (例如社交注册号或密码) 不会被任何未设置的组件访问。 在这些情况下, 可以使用`WriteOnly`属性来设置值。  
  
> [!IMPORTANT]
> 定义和使用`WriteOnly`属性时, 请考虑下列附加保护措施:  
  
- **取代.** 如果该属性是类的成员, 则允许它默认为[NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md), 而不是将其`Overridable`声明为或。 `MustOverride` 这会阻止派生类通过重写进行不需要的访问。  
  
- **访问级别。** 如果将属性的敏感数据保存在一个或多个变量中, 请将它们声明为[私有](../../../visual-basic/language-reference/modifiers/private.md), 使其他代码都不能访问它们。  
  
- **密匙.** 以加密形式而不是纯文本格式存储所有敏感数据。 如果恶意代码通过某种方式获得了对该内存区域的访问权限, 则更难使用数据。 如果需要序列化敏感数据, 则加密也很有用。  
  
- **重置.** 如果正在终止定义属性的类、结构或模块, 请将敏感数据重置为默认值或其他无意义的值。 这会在为常规访问释放内存区域时提供额外的保护。  
  
- **保持.** 如果可以避免任何敏感数据, 请不要将其保存在磁盘上。 此外, 不要将任何敏感数据写入剪贴板。  
  
 可以在此上下文中使用修饰符:`WriteOnly`  
  
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)  
  
## <a name="see-also"></a>请参阅

- [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)
- [Private](../../../visual-basic/language-reference/modifiers/private.md)
- [关键字](../../../visual-basic/language-reference/keywords/index.md)
