---
title: 属性
ms.date: 03/30/2017
ms.assetid: a941c53f-fc97-42c2-8832-0fb9f1d55c06
ms.openlocfilehash: 97d934ac581e7b1a923bf77dcf46121782fe8eab
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783170"
---
# <a name="property"></a>属性
"*属性*" 是[实体类型](entity-type.md)和[复杂类型](complex-type.md)的基本构建基块。 属性定义了实体类型实例或复杂类型实例要包含的数据的形状和特征。 概念模型中的属性类似于为类定义的属性。 正如类的属性定义类的形状和携带有关对象的信息一样，概念模型中的属性也定义实体类型的形状和携带有关实体类型实例的信息。  
  
> [!NOTE]
> 本主题中描述的属性不同于导航属性。 有关详细信息，请参阅[导航属性](navigation-property.md)。  
  
 属性定义包含以下信息：  
  
- 属性名。 （必需）  
  
- 属性类型。 （必需）  
  
- 一组[方面](facet.md)。 （可选）  
  
 属性可以包含基元数据（例如字符串、整数或布尔值）或结构化数据（例如复杂类型）。 基元类型的属性也称为标量属性。 有关详细信息，请[参阅实体数据模型：基元数据类型](entity-data-model-primitive-data-types.md)。  
  
> [!NOTE]
> 复杂类型本身可以具有复杂类型的属性。  
  
## <a name="example"></a>示例  
 下图显示了一个具有三个实体类型的概念模型：`Book`、`Publisher` 和 `Author`。 每个实体类型具有多个属性，但图中没有传达每个属性的类型信息。 作为[实体键](entity-key.md)的属性用（Key）表示。  
  
 ![具有三个实体类型的示例模型](./media/property/example-model-three-entity-types.gif)  
  
 [ADO.NET 实体框架](./ef/index.md)使用一种称为概念架构定义语言（[CSDL](./ef/language-reference/csdl-specification.md)）的域特定语言（DSL）来定义概念模型。 下面的 CSDL 定义了 `Book` 实体类型（如上图所示）并使用 XML 特性表明了每个属性的类型和名称。 此外，还使用 XML 特性定义了一个可选方面 `Nullable`。  
  
 [!code-xml[EDM_Example_Model#EntityExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entityexample)]  
  
 图中所示的其中一个属性还可以是复杂类型属性。 例如，`Address` 实体类型的 `Publisher` 属性可以是由多个标量属性（例如 `StreetAddress`、`City`、`StateOrProvince`、`Country` 和 `PostalCode`）构成的复杂类型属性。 这种复杂类型的 CSDL 表示方式如下所示：  
  
 [!code-xml[EDM_Example_Model#ComplexTypeExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books2.edmx#complextypeexample)]  
  
## <a name="see-also"></a>请参阅

- [实体数据模型关键概念](entity-data-model-key-concepts.md)
- [实体数据模型](entity-data-model.md)
