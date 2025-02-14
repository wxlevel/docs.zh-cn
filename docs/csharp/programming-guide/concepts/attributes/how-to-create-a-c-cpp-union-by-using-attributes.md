---
title: 如何：使用特性创建 C-C++ 联合 (C#)
ms.date: 07/20/2015
ms.assetid: 85f35e56-26e0-4d31-9f3a-89bd4005e71a
ms.openlocfilehash: fdadc9505b93f40c66001ac36345efada2edd270
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2019
ms.locfileid: "69595370"
---
# <a name="how-to-create-a-cc-union-by-using-attributes-c"></a>如何：使用属性创建 C/C++ 联合 (C#)
通过使用特性，可自定义结构在内存中的布局方式。 例如，可使用 `StructLayout(LayoutKind.Explicit)` 和 `FieldOffset` 特性在 C/C++ 中创建所谓的联合。  
  
## <a name="example"></a>示例  
 在此代码段中，`TestUnion` 的所有字段均从内存中的同一位置开始。  
  
```csharp  
// Add a using directive for System.Runtime.InteropServices.  
  
       [System.Runtime.InteropServices.StructLayout(LayoutKind.Explicit)]  
       struct TestUnion  
       {  
           [System.Runtime.InteropServices.FieldOffset(0)]  
           public int i;  
  
           [System.Runtime.InteropServices.FieldOffset(0)]  
           public double d;  
  
           [System.Runtime.InteropServices.FieldOffset(0)]  
           public char c;  
  
           [System.Runtime.InteropServices.FieldOffset(0)]  
           public byte b;  
       }  
```  
  
## <a name="example"></a>示例  
 下面是另一个示例，其中的字段从不同的显式设置位置开始。  
  
```csharp  
// Add a using directive for System.Runtime.InteropServices.  
  
       [System.Runtime.InteropServices.StructLayout(LayoutKind.Explicit)]  
       struct TestExplicit  
       {  
           [System.Runtime.InteropServices.FieldOffset(0)]  
           public long lg;  
  
           [System.Runtime.InteropServices.FieldOffset(0)]  
           public int i1;  
  
           [System.Runtime.InteropServices.FieldOffset(4)]  
           public int i2;  
  
           [System.Runtime.InteropServices.FieldOffset(8)]  
           public double d;  
  
           [System.Runtime.InteropServices.FieldOffset(12)]  
           public char c;  
  
           [System.Runtime.InteropServices.FieldOffset(14)]  
           public byte b;  
       }  
```  
  
 两个整数字段 `i1` 和 `i2` 共享与 `lg` 相同的内存位置。 使用平台调用时，这种对结构布局的控制很有用。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Reflection>
- <xref:System.Attribute>
- [C# 编程指南](../../index.md)
- [特性](../../../../standard/attributes/index.md)
- [反射 (C#)](../reflection.md)
- [特性 (C#)](./index.md)
- [创建自定义特性 (C#)](./creating-custom-attributes.md)
- [使用反射访问特性 (C#)](./accessing-attributes-by-using-reflection.md)
