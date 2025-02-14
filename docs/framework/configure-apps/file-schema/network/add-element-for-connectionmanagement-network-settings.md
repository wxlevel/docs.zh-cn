---
title: connectionManagement 的 <add> 元素（网络设置）
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#add
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/connectionManagement/add
helpviewer_keywords:
- <add> element, connectionManagement
- <connectionManagement>, add element
- add element, connectionManagement
- connectionManagement, add element
ms.assetid: 856bf57d-1c63-46c7-a178-03d97b0a4149
ms.openlocfilehash: 3742a040e8c16c38e495a0fd886c4c1f23780758
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2019
ms.locfileid: "71698389"
---
# <a name="add-element-for-connectionmanagement-network-settings"></a>用于 connectionManagement 的 0add > 元素（网络设置） @no__t
将 IP 地址或 DNS 名称添加到连接管理列表。  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t[ **\<system >** ](system-net-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t-2 @ no__t[ **\<connectionManagement >** ](connectionmanagement-element-network-settings.md)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<添加 >**  
  
## <a name="syntax"></a>语法  
  
```xml  
<add   
  address="address expression"   
  maxconnection="integer"   
/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|**特性**|**说明**|  
|-------------------|---------------------|  
|`address`|描述 IP 地址或 DNS 名称的字符串。|  
|`maxconnection`|允许连接至服务器的最大连接数。 如果未提供，则默认为 2。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|**元素**|**说明**|  
|-----------------|---------------------|  
|[connectionManagement](connectionmanagement-element-network-settings.md)|指定到网络主机的最大连接数。|  
  
## <a name="remarks"></a>备注  
 `address` 特性的值应该是一个星号以指示所有连接，或为 `<schema>://<idn_hostname>[:<port>]` 格式的字符串。  
  
 如果传递到任何 HTTP API 的 URI 包含 Unicode，那么将使用 <xref:System.Uri.DnsSafeHost%2A> 内部转换名称，这可能会返回一个 punicode 字符串（行为取决于当前 IDN 配置）。  
  
## <a name="configuration-files"></a>配置文件  
 此元素可在应用程序配置文件或计算机配置文件 (Machine.config) 中使用。  
  
## <a name="example"></a>示例  
 下面的示例将应用程序配置为使用服务器 @no__t 的四个连接，并将两个连接连接到所有其他服务器。  
  
```xml  
<configuration>  
  <system.net>  
    <connectionManagement>  
      <add address="http://www.contoso.com" maxconnection="4" />  
      <add address="*" maxconnection="2" />  
    </connectionManagement>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅

- <xref:System.Net.ServicePoint>
- <xref:System.Net.ServicePointManager>
- [网络设置架构](index.md)
