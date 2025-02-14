---
title: WebContentTypeMapper 示例
ms.date: 03/30/2017
ms.assetid: a4fe59e7-44d8-43c6-a1f8-40c45223adca
ms.openlocfilehash: a259f459606c9745fe10276d967946eb675a7f5e
ms.sourcegitcommit: 14ad34f7c4564ee0f009acb8bfc0ea7af3bc9541
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/01/2019
ms.locfileid: "73423799"
---
# <a name="webcontenttypemapper-sample"></a>WebContentTypeMapper 示例
此示例演示如何将新内容类型映射到 Windows Communication Foundation （WCF）消息正文格式。  
  
 <xref:System.ServiceModel.Description.WebHttpEndpoint> 元素将插入 Web 消息编码器，这允许 WCF 在同一终结点接收 JSON、XML 或原始二进制消息。 编码器通过查看请求的 HTTP 内容类型来确定消息的正文格式。 本示例介绍 <xref:System.ServiceModel.Channels.WebContentTypeMapper> 类，该类允许用户控制内容类型和正文格式之间的映射。  
  
 WCF 为内容类型提供了一组默认映射。 例如，`application/json` 映射到 JSON，`text/xml` 映射到 XML。 未映射到 JSON 或 XML 的任何内容类型都将映射到原始二进制格式。  
  
 在某些方案（例如推送式 API）中，服务开发人员不控制由客户端返回的内容类型。 例如，客户端可以将 JSON 作为 `text/javascript` 而不是 `application/json` 返回。 在这种情况下，服务开发人员必须提供从 <xref:System.ServiceModel.Channels.WebContentTypeMapper> 派生的类型以正确处理给定的内容类型，如下面的示例代码所示。  
  
```csharp  
public class JsonContentTypeMapper : WebContentTypeMapper  
{  
    public override WebContentFormat  
               GetMessageFormatForContentType(string contentType)  
    {  
        if (contentType == "text/javascript")  
        {  
            return WebContentFormat.Json;  
        }  
        else  
        {  
            return WebContentFormat.Default;  
        }  
    }  
}  
```  
  
 该类型必须重写 <xref:System.ServiceModel.Channels.WebContentTypeMapper.GetMessageFormatForContentType%28System.String%29> 方法。 该方法必须计算 `contentType` 参数并返回下列值之一：<xref:System.ServiceModel.Channels.WebContentFormat.Json>、<xref:System.ServiceModel.Channels.WebContentFormat.Xml>、<xref:System.ServiceModel.Channels.WebContentFormat.Raw> 或 <xref:System.ServiceModel.Channels.WebContentFormat.Default>。 返回 <xref:System.ServiceModel.Channels.WebContentFormat.Default> 时将遵从默认的 Web 消息编码器映射。 在前面的示例代码中，`text/javascript` 内容类型映射到 JSON，所有其他映射保持不变。  
  
 若要使用 `JsonContentTypeMapper` 类，请在你的 Web.config 中使用以下设置：  
  
```xml  
<system.serviceModel>  
  <standardEndpoints>  
    <webHttpEndpoint>  
      <standardEndpoint name="" contentTypeMapper="Microsoft.Samples.WebContentTypeMapper.JsonContentTypeMapper, JsonContentTypeMapper, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />  
    </webHttpEndpoint>  
  </standardEndpoints>  
</system.serviceModel>  
```  
  
 若要验证使用 JsonContentTypeMapper 的需求，请从上面的配置文件中移除 contentTypeMapper 特性。 在尝试使用 `text/javascript` 来发送 JSON 内容时，客户端页加载将失败。  
  
### <a name="to-set-up-build-and-run-the-sample"></a>设置、生成和运行示例  
  
1. 确保已对[Windows Communication Foundation 示例执行了一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2. 按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中所述生成解决方案 WebContentTypeMapperSample。  
  
3. 导航到 `http://localhost/ServiceModelSamples/JCTMClientPage.htm` （不要在浏览器中从项目目录中打开 JCTMClientPage）。  
  
> [!IMPORTANT]
> 您的计算机上可能已安装这些示例。 在继续操作之前，请先检查以下（默认）目录：  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 如果此目录不存在，请参阅[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）示例](https://go.microsoft.com/fwlink/?LinkId=150780)以下载所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。 此示例位于以下目录：  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Ajax\WebContentTypeMapper`  
