---
title: 如何：链接轴方法调用 (LINQ to XML) (C#)
ms.date: 07/20/2015
ms.assetid: 067e6da2-ee32-486d-803c-e611b328e39a
ms.openlocfilehash: 3dfb2849bc2e2af9290738ed06938f80f3416f72
ms.sourcegitcommit: 14ad34f7c4564ee0f009acb8bfc0ea7af3bc9541
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/01/2019
ms.locfileid: "73418409"
---
# <a name="how-to-chain-axis-method-calls-linq-to-xml-c"></a>如何：链接轴方法调用 (LINQ to XML) (C#)
一个在代码中常用的模式是调用轴方法，然后调用一个扩展方法轴。  
  
 有两个返回元素集合、名称为 `Elements` 的轴：<xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType> 方法和 <xref:System.Xml.Linq.Extensions.Elements%2A?displayProperty=nameWithType> 方法。 可以合并这两个轴，在树的给定深度，查找具有指定名称的所有元素。  
  
## <a name="example"></a>示例  
 本示例使用 <xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType> 和 <xref:System.Xml.Linq.Extensions.Elements%2A?displayProperty=nameWithType> 在所有 `Name` 元素中查找所有 `Address` 元素中的所有 `PurchaseOrder` 元素。  
  
 本示例使用下面的 XML 文档：[示例 XML 文件：多个采购订单 (LINQ to XML)](./sample-xml-file-multiple-purchase-orders-linq-to-xml.md)。  
  
```csharp  
XElement purchaseOrders = XElement.Load("PurchaseOrders.xml");  
IEnumerable<XElement> names =  
    from el in purchaseOrders  
        .Elements("PurchaseOrder")  
        .Elements("Address")  
        .Elements("Name")  
    select el;  
foreach (XElement e in names)  
    Console.WriteLine(e);  
```  
  
 该示例产生下面的输出：  
  
```xml  
<Name>Ellen Adams</Name>  
<Name>Tai Yee</Name>  
<Name>Cristian Osorio</Name>  
<Name>Cristian Osorio</Name>  
<Name>Jessica Arnold</Name>  
<Name>Jessica Arnold</Name>  
```  
  
 此方法有效是因为其中有一个 `Elements` 轴实现充当 <xref:System.Collections.Generic.IEnumerable%601> 的 <xref:System.Xml.Linq.XContainer> 的扩展方法。 <xref:System.Xml.Linq.XElement> 是从 <xref:System.Xml.Linq.XContainer> 派生的，因此可以对调用 <xref:System.Xml.Linq.Extensions.Elements%2A?displayProperty=nameWithType> 方法的结果调用 <xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType> 方法。  
  
## <a name="example"></a>示例  
 有时，当可能存在或不存在间隔上级时，您希望在特定的元素深度，检索所有的元素。 例如，在下面的文档中，您可能要检索属于 `ConfigParameter` 元素的子元素的所有 `Customer` 元素，而不是属于 `ConfigParameter` 元素的子元素的 `Root`。  
  
```xml  
<Root>  
  <ConfigParameter>RootConfigParameter</ConfigParameter>  
  <Customer>  
    <Name>Frank</Name>  
    <Config>  
      <ConfigParameter>FirstConfigParameter</ConfigParameter>  
    </Config>  
  </Customer>  
  <Customer>  
    <Name>Bob</Name>  
    <!--This customer doesn't have a Config element-->  
  </Customer>  
  <Customer>  
    <Name>Bill</Name>  
    <Config>  
      <ConfigParameter>SecondConfigParameter</ConfigParameter>  
    </Config>  
  </Customer>  
</Root>  
```  
  
 若要执行此操作，您可以使用 <xref:System.Xml.Linq.Extensions.Elements%2A?displayProperty=nameWithType> 轴，如下所示：  
  
```csharp  
XElement root = XElement.Load("Irregular.xml");  
IEnumerable<XElement> configParameters =   
    root.Elements("Customer").Elements("Config").  
    Elements("ConfigParameter");  
foreach (XElement cp in configParameters)  
    Console.WriteLine(cp);  
```  
  
 该示例产生下面的输出：  
  
```xml  
<ConfigParameter>FirstConfigParameter</ConfigParameter>  
<ConfigParameter>SecondConfigParameter</ConfigParameter>  
```  
  
## <a name="example"></a>示例  
 下面的示例演示针对命名空间中的 XML 的相同技术。 有关详细信息，请参阅[命名空间概述(LINQ to XML) (C#)](namespaces-overview-linq-to-xml.md)。  
  
 本示例使用下面的 XML 文档：[示例 XML 文件：命名空间中的多个采购订单](./sample-xml-file-multiple-purchase-orders-in-a-namespace.md)。  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XElement purchaseOrders = XElement.Load("PurchaseOrdersInNamespace.xml");  
IEnumerable<XElement> names =  
    from el in purchaseOrders  
        .Elements(aw + "PurchaseOrder")  
        .Elements(aw + "Address")  
        .Elements(aw + "Name")  
    select el;  
foreach (XElement e in names)  
    Console.WriteLine(e);  
```  
  
 该示例产生下面的输出：  
  
```xml  
<aw:Name xmlns:aw="http://www.adventure-works.com">Ellen Adams</aw:Name>  
<aw:Name xmlns:aw="http://www.adventure-works.com">Tai Yee</aw:Name>  
<aw:Name xmlns:aw="http://www.adventure-works.com">Cristian Osorio</aw:Name>  
<aw:Name xmlns:aw="http://www.adventure-works.com">Cristian Osorio</aw:Name>  
<aw:Name xmlns:aw="http://www.adventure-works.com">Jessica Arnold</aw:Name>  
<aw:Name xmlns:aw="http://www.adventure-works.com">Jessica Arnold</aw:Name>  
```  
  
## <a name="see-also"></a>请参阅

- [LINQ to XML 轴 (C#)](linq-to-xml-axes-overview.md)
