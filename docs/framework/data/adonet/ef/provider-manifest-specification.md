---
title: 提供程序清单规范
ms.date: 03/30/2017
ms.assetid: bb450b47-8951-4f99-9350-26f05a4d4e46
ms.openlocfilehash: bef4868ccc52d287baaceca32c4943723be7531f
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2019
ms.locfileid: "73040496"
---
# <a name="provider-manifest-specification"></a>提供程序清单规范
本节讨论数据存储提供程序如何可以支持数据存储中的类型和功能。  
  
 实体服务独立于特定的数据存储提供程序进行操作，但仍允许数据提供程序显式定义模型、映射和查询与基础数据存储进行交互的方式。 由于没有抽象层，只能在特定的数据存储或数据提供程序中以实体服务为目标。  
  
 提供程序支持的类型由基础数据库直接或间接地提供支持。 这些类型不一定是精确的存储类型，而是提供程序用于支持实体框架的类型。 提供程序/存储类型在实体数据模型 (EDM) 条目中进行了说明。  
  
 在 EDM 条目中指定了数据存储支持的函数的参数和返回类型。  
  
## <a name="requirements"></a>要求  
 实体框架和数据存储需要能够在已知类型中来回传递数据，而不会发生任何数据丢失或截断。  
  
 提供程序清单必须可由工具在设计时加载，而不必打开与数据存储的连接。  
  
 实体框架区分大小写，但基础数据存储可能不是。 当在清单中定义和使用 EDM 项目（例如，标识符和类型名称）时，它们必须使用实体框架区分大小写。 如果可能区分大小写的数据存储元素出现在提供程序的清单中，则在提供程序清单中需要维持大小写区分。  
  
 实体框架需要所有数据提供程序的提供程序清单。 如果尝试使用的提供程序不具有具有实体框架的提供程序清单，则会出现错误。  
  
 下表描述了当通过提供程序交互引发异常时实体框架将引发的异常的种类：  
  
|问题|例外|  
|-----------|---------------|  
|提供程序不支持 DbProviderServices 中的 GetProviderManifest。|ProviderIncompatibleException|  
|缺少提供程序清单：在尝试检索提供程序清单时，提供程序返回 `null`。|ProviderIncompatibleException|  
|无效的提供程序清单：在尝试检索提供程序清单时，提供程序返回无效的 XML。|ProviderIncompatibleException|  
  
## <a name="scenarios"></a>方案  
 提供程序应支持下面的方案：  
  
### <a name="writing-a-provider-with-symmetric-type-mapping"></a>使用对称类型映射编写提供程序  
 您可以为实体框架编写提供程序，其中每个商店类型都映射到单个 EDM 类型，而不考虑映射方向。 对于具有非常简单的映射（与 EDM 类型对应）的提供程序类型，您可以使用对称解决方案，因为此类型系统很简单或者匹配 EDM 类型。  
  
 您可以利用提供程序的域的简单性，生成一个静态声明性提供程序清单。  
  
 编写具有两部分的 XML 文件：  
  
- 以存储类型或函数的“EDM 对应项”的形式表示的提供程序类型列表。 存储类型具有对应的 EDM 类型。 存储函数具有对应的 EDM 函数。 例如，varchar 是一个 SQL Server 类型，但对应的 EDM 类型是字符串。  
  
- 提供程序支持的函数列表，其中的参数和返回类型用 EDM 术语表示。  
  
### <a name="writing-a-provider-with-asymmetric-type-mapping"></a>使用非对称类型映射编写提供程序  
 写入实体框架的数据存储提供程序时，某些类型的 EDM 到提供程序类型的映射可能不同于提供程序到 EDM 的类型映射。 例如，无限制的 EDM PrimitiveTypeKind.String 可能会映射到提供程序上的 nvarchar(4000)，而 nvarchar(4000) 将映射到 EDM PrimitiveTypeKind.String(MaxLength=4000)。  
  
 编写具有两部分的 XML 文件：  
  
- 用 EDM 术语表示的提供程序类型的列表，其中定义了两个方向的映射：EDM 到提供程序的映射和提供程序到 EDM 的映射。  
  
- 提供程序支持的函数列表，其中的参数和返回类型用 EDM 术语表示。  
  
## <a name="provider-manifest-discoverability"></a>提供程序清单的可发现性  
 清单可以由实体服务中的若干组件类型（例如“工具”或“查询”）间接地使用，但更多的是通过使用数据存储元数据加载程序由元数据直接利用。  
  
 ![dfb3d02b&#45;7a8c&#45;4d51&#45;ac5a&#45;a73d8aa145e6](./media/dfb3d02b-7a8c-4d51-ac5a-a73d8aa145e6.gif "dfb3d02b-7a8c-4d51-ac5a-a73d8aa145e6")  
  
 但是，给定的提供程序可能支持不同的存储或相同存储的不同版本。 因此，对于每个支持的数据存储，提供程序必须报告不同的清单。  
  
### <a name="provider-manifest-token"></a>提供程序清单标记  
 当打开数据存储连接时，提供程序可以查询信息以返回正确的清单。 在无法获取连接信息的脱机方案中，或者在无法连接到存储的情况下，上述方法可能不可行。 通过使用 .ssdl 文件中的 `ProviderManifestToken` 元素的 `Schema` 特性可标识清单。 此特性没有必需的格式要求，提供程序可选择所需的最少信息来标识清单，而无需打开与存储的连接。  
  
 例如:  
  
```xml  
<Schema Namespace="Northwind" Provider="System.Data.SqlClient" ProviderManifestToken="2005" xmlns:edm="http://schemas.microsoft.com/ado/2006/04/edm/ssdl" xmlns="http://schemas.microsoft.com/ado/2006/04/edm/ssdl">  
```  
  
## <a name="provider-manifest-programming-model"></a>提供程序清单编程模型  
 提供程序派生自 <xref:System.Data.Common.DbXmlEnabledProviderManifest>，这使得它们可以通过声明方式指定其清单。 下图显示了提供程序的类层次结构：  
  
 ![无](./media/d541eba3-2ee6-4cd1-88f5-89d0b2582a6c.gif "d541eba3-2ee6-4cd1-88f5-89d0b2582a6c")  
  
### <a name="discoverability-api"></a>可发现性 API  
 通过使用数据存储连接或提供程序清单标记，存储元数据加载程序 (StoreItemCollection) 可加载提供程序清单。  
  
#### <a name="using-a-data-store-connection"></a>使用数据存储连接  
 如果数据存储连接可用，则调用 <xref:System.Data.Common.DbProviderServices.GetProviderManifestToken%2A?displayProperty=nameWithType> 以返回传递给 <xref:System.Data.Common.DbProviderServices.GetProviderManifest%2A> 方法的令牌，该令牌返回 <xref:System.Data.Common.DbProviderManifest>。 此方法委托给提供程序的 `GetDbProviderManifestToken`实现。  
  
```csharp
public string GetProviderManifestToken(DbConnection connection);  
public DbProviderManifest GetProviderManifest(string manifestToken);  
```  
  
#### <a name="using-a-provider-manifest-token"></a>使用提供程序清单标记  
 对于脱机方案，此标记从 SSDL 表示形式中选取。 SSDL 允许您指定 ProviderManifestToken （有关详细信息，请参阅[Schema 元素（SSDL）](/ef/ef6/modeling/designer/advanced/edmx/ssdl-spec#schema-element-ssdl) ）。 例如，如果无法打开某个连接，则 SSDL 会具有一个提供程序清单标记，用于指定有关清单的信息。  
  
```csharp  
public DbProviderManifest GetProviderManifest(string manifestToken);  
```  
  
### <a name="provider-manifest-schema"></a>提供程序清单架构  
 为每个提供程序定义的信息架构包含元数据要使用的静态信息：  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema elementFormDefault="qualified"  
   xmlns:xs="http://www.w3.org/2001/XMLSchema"  
   targetNamespace="http://schemas.microsoft.com/ado/2006/04/edm/providermanifest"  
   xmlns:pm="http://schemas.microsoft.com/ado/2006/04/edm/providermanifest">  
  
  <xs:element name="ProviderManifest">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="Types" type="pm:TTypes" minOccurs="1" maxOccurs="1" />  
        <xs:element name="Functions" type="pm:TFunctions" minOccurs="0" maxOccurs="1"/>  
      </xs:sequence>  
      <xs:attribute name="Namespace" type="xs:string" use="required"/>  
    </xs:complexType>  
  </xs:element>  
  <xs:complexType name="TVersion">  
    <xs:attribute name="Major" type="xs:int" use="required" />  
    <xs:attribute name="Minor" type="xs:int" use="required" />  
    <xs:attribute name="Build" type="xs:int" use="required" />  
    <xs:attribute name="Revision" type="xs:int" use="required" />  
  </xs:complexType>  
  
  <xs:complexType name="TIntegerFacetDescription">  
    <xs:attribute name="Minimum" type="xs:int" use="optional" />  
    <xs:attribute name="Maximum" type="xs:int" use="optional" />  
    <xs:attribute name="DefaultValue" type="xs:int" use="optional" />  
    <xs:attribute name="Constant" type="xs:boolean" default="false" />  
  </xs:complexType>  
  
  <xs:complexType name="TBooleanFacetDescription">  
    <xs:attribute name="DefaultValue" type="xs:boolean" use="optional" />  
    <xs:attribute name="Constant" type="xs:boolean" default="true" />  
  </xs:complexType>  
  
  <xs:complexType name="TDateTimeFacetDescription">  
    <xs:attribute name="Constant" type="xs:boolean" default="false" />  
  </xs:complexType>  
  
  <xs:complexType name="TFacetDescriptions">  
    <xs:choice maxOccurs="unbounded">  
      <xs:element name="Precision" minOccurs="0" maxOccurs="1" type="pm:TIntegerFacetDescription"/>  
      <xs:element name="Scale" minOccurs="0" maxOccurs="1" type="pm:TIntegerFacetDescription"/>  
      <xs:element name="MaxLength" minOccurs="0" maxOccurs="1" type="pm:TIntegerFacetDescription"/>  
      <xs:element name="Unicode" minOccurs="0" maxOccurs="1" type="pm:TBooleanFacetDescription"/>  
      <xs:element name="FixedLength" minOccurs="0" maxOccurs="1" type="pm:TBooleanFacetDescription"/>  
    </xs:choice>  
  </xs:complexType>  
  
  <xs:complexType name="TType">  
    <xs:sequence>  
      <xs:element name="FacetDescriptions" type="pm:TFacetDescriptions" minOccurs="0" maxOccurs="1"/>  
    </xs:sequence>  
    <xs:attribute name="Name" type="xs:string" use="required"/>  
    <xs:attribute name="PrimitiveTypeKind" type="pm:TPrimitiveTypeKind" use="required" />  
  </xs:complexType>  
  
  <xs:complexType name="TTypes">  
    <xs:sequence>  
      <xs:element name="Type" type="pm:TType" minOccurs="0" maxOccurs="unbounded"/>  
    </xs:sequence>  
  </xs:complexType>  
  
  <xs:attributeGroup name="TFacetAttribute">  
    <xs:attribute name="Precision" type="xs:int" use="optional"/>  
    <xs:attribute name="Scale" type="xs:int" use="optional"/>  
    <xs:attribute name="MaxLength" type="xs:int" use="optional"/>  
    <xs:attribute name="Unicode" type="xs:boolean" use="optional"/>  
    <xs:attribute name="FixedLength" type="xs:boolean" use="optional"/>  
  </xs:attributeGroup>  
  
  <xs:complexType name="TFunctionParameter">  
    <xs:attribute name="Name" type="xs:string" use="required" />  
    <xs:attribute name="Type" type="xs:string" use="required" />  
    <xs:attributeGroup ref="pm:TFacetAttribute" />  
    <xs:attribute name="Mode" type="pm:TParameterDirection" use="required" />  
  </xs:complexType>  
  
  <xs:complexType name="TReturnType">  
    <xs:attribute name="Type" type="xs:string" use="required" />  
    <xs:attributeGroup ref="pm:TFacetAttribute" />  
  </xs:complexType>  
  
  <xs:complexType name="TFunction">  
    <xs:choice minOccurs="0" maxOccurs ="unbounded">  
      <xs:element name ="ReturnType" type="pm:TReturnType" minOccurs="0" maxOccurs="1" />  
      <xs:element name="Parameter" type="pm:TFunctionParameter" minOccurs="0" maxOccurs="unbounded"/>  
    </xs:choice>  
    <xs:attribute name="Name" type="xs:string" use="required" />  
    <xs:attribute name="Aggregate" type="xs:boolean" use="optional" />  
    <xs:attribute name="BuiltIn" type="xs:boolean" use="optional" />  
    <xs:attribute name="StoreFunctionName" type="xs:string" use="optional" />  
    <xs:attribute name="NiladicFunction" type="xs:boolean" use="optional" />  
    <xs:attribute name="ParameterTypeSemantics" type="pm:TParameterTypeSemantics" use="optional" default="AllowImplicitConversion" />  
  </xs:complexType>  
  
  <xs:complexType name="TFunctions">  
    <xs:sequence>  
      <xs:element name="Function" type="pm:TFunction" minOccurs="0" maxOccurs="unbounded"/>  
    </xs:sequence>  
  </xs:complexType>  
  
  <xs:simpleType name="TPrimitiveTypeKind">  
    <xs:restriction base="xs:string">  
      <xs:enumeration value="Binary"/>  
      <xs:enumeration value="Boolean"/>  
      <xs:enumeration value="Byte"/>  
      <xs:enumeration value="Decimal"/>  
      <xs:enumeration value="DateTime"/>  
      <xs:enumeration value="Time"/>  
      <xs:enumeration value="DateTimeOffset"/>          
      <xs:enumeration value="Double"/>  
      <xs:enumeration value="Guid"/>  
      <xs:enumeration value="Single"/>  
      <xs:enumeration value="SByte"/>  
      <xs:enumeration value="Int16"/>  
      <xs:enumeration value="Int32"/>  
      <xs:enumeration value="Int64"/>  
      <xs:enumeration value="String"/>  
    </xs:restriction>  
  </xs:simpleType>  
  
  <xs:simpleType name="TParameterDirection">  
    <xs:restriction base="xs:string">  
      <xs:enumeration value="In"/>  
      <xs:enumeration value="Out"/>  
      <xs:enumeration value="InOut"/>  
    </xs:restriction>  
  </xs:simpleType>  
  
  <xs:simpleType name="TParameterTypeSemantics">  
    <xs:restriction base="xs:string">  
      <xs:enumeration value="ExactMatchOnly" />  
      <xs:enumeration value="AllowImplicitPromotion" />  
      <xs:enumeration value="AllowImplicitConversion" />  
    </xs:restriction>  
  </xs:simpleType>  
</xs:schema>  
```  
  
#### <a name="types-node"></a>Types 节点  
 提供程序清单中的 Types 节点包含有关数据存储区本身支持的或通过提供程序支持的 Type 的信息。  
  
##### <a name="type-node"></a>Type 节点  
 每个 Type 节点以 EDM 的形式定义一个提供程序类型。 Type 节点描述提供程序类型的名称、与其映射到的模型类型相关的信息以及用于描述类型映射的各个方面。  
  
 为了在提供程序清单中表示此类型信息，每个 TypeInformation 声明必须为每个 Type 定义几个方面的说明：  
  
|特性名|数据类型|必需|默认值|描述|  
|--------------------|---------------|--------------|-------------------|-----------------|  
|“属性”|字符串|是|不可用|提供程序特定的数据类型名称|  
|PrimitiveTypeKind|PrimitiveTypeKind|是|不可用|EDM 类型名称|  
  
###### <a name="function-node"></a>Function 节点  
 每个 Function 定义一个可通过提供程序使用的函数。  
  
|特性名|数据类型|必需|默认值|描述|  
|--------------------|---------------|--------------|-------------------|-----------------|  
|“属性”|字符串|是|不可用|函数的标识符/名称|  
|ReturnType|字符串|No|Void|函数的 EDM 返回类型|  
|聚合|布尔值|No|False|如果函数为聚合函数，则为 True。|  
|BuiltIn|布尔值|No|True|如果函数内置于数据存储中，则返回 True|  
|StoreFunctionName|字符串|No|\<名称 >|数据存储中的函数名称。  考虑了函数名称的重定向级别。|  
|NiladicFunction|布尔值|No|False|如果函数不需要任何参数且在调用时不使用任何参数，则返回 True。|  
|ParameterType<br /><br /> 语义|ParameterSemantics|No|AllowImplicit<br /><br /> 转换|有关查询管道应如何处理参数类型替换的选项：<br /><br /> - ExactMatchOnly<br />- AllowImplicitPromotion<br />- AllowImplicitConversion|  
  
 **Parameters 节点**  
  
 每个函数都具有包含一个或多个 Parameter 节点的集合。  
  
|特性名|数据类型|必需|默认值|描述|  
|--------------------|---------------|--------------|-------------------|-----------------|  
|“属性”|字符串|是|不可用|参数的标识符/名称。|  
|键入|字符串|是|不可用|参数的 EDM 类型。|  
|模式|参数<br /><br /> 方向|是|不可用|参数的方向：<br /><br /> -在中<br />-out<br />-inout|  
  
##### <a name="namespace-attribute"></a>Namespace 属性  
 每个数据存储提供程序必须为清单中定义的信息定义一个命名空间或一组命名空间。 此命名空间可在 Entity SQL 查询中用来解析函数和类型的名称。 例如，SqlServer。 此命名空间必须与规范命名空间 EDM 不同，EDM 是由实体服务为 Entity SQL 查询要支持的标准函数定义的。  
  
## <a name="see-also"></a>请参阅

- [编写实体框架数据提供程序](writing-an-ef-data-provider.md)
