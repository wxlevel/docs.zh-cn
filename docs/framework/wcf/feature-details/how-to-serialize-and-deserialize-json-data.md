---
title: 如何：使用 DataContractJsonSerializer
ms.date: 03/25/2019
ms.assetid: 88abc1fb-8196-4ee3-a23b-c6934144d1dd
ms.openlocfilehash: ad126616e0665c6de3aa7a64969c83b23be9f830
ms.sourcegitcommit: 2e95559d957a1a942e490c5fd916df04b39d73a9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72395995"
---
# <a name="how-to-use-datacontractjsonserializer"></a>如何：使用 DataContractJsonSerializer

JSON（JavaScript 对象符号）是一种高效的数据编码格式，可用于在客户端浏览器和支持 AJAX 的 Web 服务之间快速交换少量数据。

本文演示如何将 .NET 类型对象序列化为 JSON 编码数据，然后将 JSON 格式的数据反序列化为 .NET 类型的实例。 此示例使用数据协定演示用户定义的 @no__t 0 类型的序列化和反序列化，并使用 @no__t。

通常，当你在服务操作中使用在支持 AJAX 的终结点上公开的数据协定类型时，将 Windows Communication Foundation 自动处理 JSON 序列化和反序列化。 但是，在某些情况下，您可能需要直接处理 JSON 数据。

> [!NOTE]
> 本文介绍 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>。 对于涉及对 JSON 进行序列化和反序列化的大多数方案，建议采用[system.web 命名空间](../../../standard/serialization/system-text-json-overview.md)中的工具。

本文基于[DataContractJsonSerializer 示例](../samples/json-serialization.md)。

## <a name="to-define-the-data-contract-for-a-person-type"></a>为 Person 类型定义数据协定

1. 通过将 `Person` 附加到类并将 <xref:System.Runtime.Serialization.DataContractAttribute> 特性附加到要序列化的成员，为 <xref:System.Runtime.Serialization.DataMemberAttribute> 定义数据协定。 有关数据协定的详细信息，请参阅[设计服务协定](../designing-service-contracts.md)。

    ```csharp
    [DataContract]
    internal class Person
    {
        [DataMember]
        internal string name;

        [DataMember]
        internal int age;
    }
    ```

## <a name="to-serialize-an-instance-of-type-person-to-json"></a>将 Person 类型的实例序列化为 JSON

> [!NOTE]
> 如果在服务器上的传出答复序列化过程中出现错误，或出于其他原因导致错误，则可能不会将其作为错误返回到客户端。

1. 创建 `Person` 类型的实例。

    ```csharp
    var p = new Person();
    p.name = "John";
    p.age = 42;
    ```

2. 使用 @no__t 将 @no__t 0 对象序列化到内存流。

    ```csharp
    var stream1 = new MemoryStream();
    var ser = new DataContractJsonSerializer(typeof(Person));
    ```

3. 使用 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.WriteObject%2A> 方法将 JSON 数据写入到流中。

    ```csharp
    ser.WriteObject(stream1, p);
    ```

4. 显示 JSON 输出。

    ```csharp
    stream1.Position = 0;
    var sr = new StreamReader(stream1);
    Console.Write("JSON form of Person object: ");
    Console.WriteLine(sr.ReadToEnd());
    ```

## <a name="to-deserialize-an-instance-of-type-person-from-json"></a>从 JSON 反序列化 Person 类型的实例

1. 通过使用 `Person` 的 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.ReadObject%2A> 方法，将 JSON 编码数据反序列化为一个新的 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 实例。

    ```csharp
    stream1.Position = 0;
    var p2 = (Person)ser.ReadObject(stream1);
    ```

2. 显示结果。

    ```csharp
    Console.WriteLine($"Deserialized back, got name={p2.name}, age={p2.age}");
    ```

## <a name="example"></a>示例

```csharp
// Create a User object and serialize it to a JSON stream.
public static string WriteFromObject()
{
    // Create User object.
    var user = new User("Bob", 42);

    // Create a stream to serialize the object to.
    var ms = new MemoryStream();

    // Serializer the User object to the stream.
    var ser = new DataContractJsonSerializer(typeof(User));
    ser.WriteObject(ms, user);
    byte[] json = ms.ToArray();
    ms.Close();
    return Encoding.UTF8.GetString(json, 0, json.Length);
}

// Deserialize a JSON stream to a User object.
public static User ReadToObject(string json)
{
    var deserializedUser = new User();
    var ms = new MemoryStream(Encoding.UTF8.GetBytes(json));
    var ser = new DataContractJsonSerializer(deserializedUser.GetType());
    deserializedUser = ser.ReadObject(ms) as User;
    ms.Close();
    return deserializedUser;
}
```

> [!NOTE]
> 对于包含多个具有相同名称的成员的数据协定，JSON 序列化程序将引发一个序列化异常，如以下示例代码中所示。

```csharp
[DataContract]
public class TestDuplicateDataBase
{
    [DataMember]
    public int field1 = 123;
}

[DataContract]
public class TestDuplicateDataDerived : TestDuplicateDataBase
{
    [DataMember]
    public new int field1 = 999;
}
```

## <a name="see-also"></a>请参阅

- [.NET 中的 JSON 序列化](../../../standard/serialization/system-text-json-overview.md)
