---
title: <bypassTrustedAppStrongNames> 元素
ms.date: 03/30/2017
helpviewer_keywords:
- strong-name bypass feature
- bypassTrustedAppStrongNames element
- strong-named assemblies, loading into trusted application domains
- <bypassTrustedAppStrongNames> element
ms.assetid: 71b2ebf6-3843-41e2-ad52-ffa5cd083a40
ms.openlocfilehash: 50e67e97d74b896a680cc18270d32aa7a8eb8035
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73118180"
---
# <a name="bypasstrustedappstrongnames-element"></a>\<bypassTrustedAppStrongNames> 元素

指定是否绕过对加载到完全信任的 <xref:System.AppDomain>中的完全信任程序集的强名称的验证。

[ **\<configuration>** ](../configuration-element.md)\
&nbsp; &nbsp;[ **\<runtime >** ](runtime-element.md) \
&nbsp;&nbsp;&nbsp;&nbsp; **\<bypasstrustedappstrongnames> element >**

## <a name="syntax"></a>语法

```xml
<bypassTrustedAppStrongNames
   enabled="true|false"/>
```

## <a name="attributes-and-elements"></a>特性和元素

下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|`enabled`|必需的特性。<br /><br /> 指定是否启用回避功能，以避免为完全信任程序集验证强名称。 当启用此功能时，加载程序集时，不会验证强名称是否正确。 默认值为 `true`。|

## <a name="enabled-attribute"></a>enabled 特性

|“值”|描述|
|-----------|-----------------|
|`true`|将程序集加载到完全信任 <xref:System.AppDomain>中时，不会验证完全信任程序集上的强名称签名。 这是默认设置。|
|`false`|将程序集加载到完全信任的 <xref:System.AppDomain>时，会验证完全信任程序集上的强名称签名。 仅对签名正确性检查强名称签名;与另一个匹配的强名称没有比较。|

### <a name="child-elements"></a>子元素

无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|
|`runtime`|包含有关程序集绑定和垃圾回收的信息。|

## <a name="remarks"></a>备注

强名称跳过功能可避免完全信任程序集的强名称签名验证的系统开销。

跳过功能适用于使用强名称进行签名及具有以下特征的任何程序集：

- 完全受信任，无 <xref:System.Security.Policy.StrongName> 证据（例如，具有 `MyComputer` 区域证据）。

- 加载到完全受信任的 <xref:System.AppDomain>。

- 加载自该 <xref:System.AppDomain> 的 <xref:System.AppDomainSetup.ApplicationBase%2A> 属性下的某个位置。

- 签名没有延迟。

> [!NOTE]
> 如果对计算机上的所有应用程序使用注册表项关闭了绕过功能，则此配置文件设置将不起作用。 有关详细信息，请参阅[如何：禁用强名称跳过功能](../../../app-domains/how-to-disable-the-strong-name-bypass-feature.md)。

## <a name="example"></a>示例

下面的示例演示如何指定对完全信任程序集的强名称签名进行验证的行为。

```xml
<configuration>
   <runtime>
      <bypassTrustedAppStrongNames enabled="false"/>
   </runtime>
</configuration>
```

## <a name="see-also"></a>请参阅

- [运行时设置架构](index.md)
- [配置文件架构](../index.md)
- [如何：禁用强名称跳过功能](../../../../standard/assembly/disable-strong-name-bypass-feature.md)
