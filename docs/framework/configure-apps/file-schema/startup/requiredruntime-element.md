---
title: <requiredRuntime> 元素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#requiredRuntime
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/startup/requiredRuntime
helpviewer_keywords:
- requiredRuntime element
- <requiredRuntime> element
- container tags, <requiredRuntime> element
ms.assetid: 9fa1639e-beb8-43be-b7a4-12f7b229c34b
ms.openlocfilehash: fe96673b95f48cb75d36662a680bf56a59363f9f
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2019
ms.locfileid: "71697486"
---
# <a name="requiredruntime-element"></a>\<requiredRuntime > 元素

指定应用程序仅支持 1.0 版本的公共语言运行时。 此元素已弃用，不应再使用。 应改为使用[`supportedRuntime`](supportedruntime-element.md)元素。

[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **\<startup >** ](startup-element.md)  
&nbsp; @ no__t-1 @ no__t-2 @ no__t **\<requiredRuntime >**  

## <a name="syntax"></a>语法

```xml
   <requiredRuntime  
version="runtime version"
safemode="true|false"/>
```

## <a name="attributes-and-elements"></a>特性和元素

下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|`version`|可选特性。<br /><br /> 一个字符串值，该值指定此应用程序支持的 .NET Framework 的版本。 字符串值必须与 .NET Framework 安装根下的目录名称匹配。 不分析字符串值的内容。|
|`safemode`|可选特性。<br /><br /> 指定运行时启动代码是否在注册表中搜索以确定运行时版本。|

## <a name="safemode-attribute"></a>安全模式特性

|ReplTest1|描述|
|-----------|-----------------|
|`false`|运行时启动代码在注册表中查找。 这是默认值。|
|`true`|运行时启动代码不会在注册表中查找。|

### <a name="child-elements"></a>子元素

无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|
|`startup`|`<requiredRuntime>`包含元素。|

## <a name="remarks"></a>备注
 构建为仅支持1.0 版运行时的应用程序必须使用 `<requiredRuntime>` 元素。 使用版本1.1 或更高版本的运行时生成的应用程序必须使用 `<supportedRuntime>` 元素。

> [!NOTE]
> 如果使用[CorBindToRuntimeByCfg](../../../unmanaged-api/hosting/corbindtoruntimebycfg-function.md)函数来指定配置文件，则必须对所有版本的运行时使用 `<requiredRuntime>` 元素。 当使用[CorBindToRuntimeByCfg](../../../unmanaged-api/hosting/corbindtoruntimebycfg-function.md)时，将忽略 `<supportedRuntime>` 元素。

 @No__t 的 .NET Framework 属性字符串必须与指定版本的的安装文件夹名称匹配。 不解释此字符串。 如果运行时启动代码找不到匹配的文件夹，则不加载运行时;启动代码将显示一条错误消息并退出。

> [!NOTE]
> 在 Microsoft Internet Explorer 中托管的应用程序的启动代码将忽略 `<requiredRuntime>` 元素。

## <a name="example"></a>示例

下面的示例演示如何在配置文件中指定运行时版本。

```xml
<configuration>
   <startup>
      <requiredRuntime version="v1.0.3705" safemode="true"/>
   </startup>
</configuration>
```

## <a name="see-also"></a>请参阅

- [启动设置架构](index.md)
- [配置文件架构](../index.md)
- [如何：将应用配置为支持 .NET Framework 4 或更高版本](../../../migration-guide/how-to-configure-an-app-to-support-net-framework-4-or-4-5.md)
