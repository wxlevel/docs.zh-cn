---
title: 如何：查找根元素（LINQ to XML）（Visual Basic）
ms.date: 07/20/2015
ms.assetid: 72c3aed5-9522-4454-a876-2070aad13f2e
ms.openlocfilehash: d8ac28b698b0c61a4d9e3beea61ff8a8e1074b88
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72320587"
---
# <a name="how-to-find-the-root-element-xpath-linq-to-xml-visual-basic"></a>如何：查找根元素（LINQ to XML）（Visual Basic）
本主题演示如何使用 XPath 和 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 获取根元素。  
  
 XPath 表达式为：  
  
 `/PurchaseOrders`  
  
## <a name="example"></a>示例  
 此示例查找根元素。  
  
 本示例使用以下 XML 文档：[示例 XML 文件：多个采购订单 (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-multiple-purchase-orders-linq-to-xml.md)。  
  
```vb  
Dim po As XDocument = XDocument.Load("PurchaseOrders.xml")  
  
' LINQ to XML query  
Dim el1 As XElement = po.Root  
  
' XPath expression  
Dim el2 As XElement = po.XPathSelectElement("/PurchaseOrders")  
  
If el1 Is el2 Then  
    Console.WriteLine("Results are identical")  
Else  
    Console.WriteLine("Results differ")  
End If  
Console.WriteLine(el1.Name)  
```  
  
 该示例产生下面的输出：  
  
```console  
Results are identical  
PurchaseOrders  
```  
  
## <a name="see-also"></a>请参阅

- [XPath 用户的 LINQ to XML （Visual Basic）](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
