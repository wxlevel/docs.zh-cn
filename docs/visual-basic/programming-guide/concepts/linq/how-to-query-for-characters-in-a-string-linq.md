---
title: 如何：查询字符串中的字符（LINQ）（Visual Basic）
ms.date: 07/20/2015
ms.assetid: 499ebbe0-746c-4235-9dba-ce722c12b50e
ms.openlocfilehash: f2102a8cb149fa9c7886826e509bf254fad5eb95
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72582716"
---
# <a name="how-to-query-for-characters-in-a-string-linq-visual-basic"></a>如何：查询字符串中的字符（LINQ）（Visual Basic）

因为 <xref:System.String> 类可实现泛型 <xref:System.Collections.Generic.IEnumerable%601> 接口，因此任何字符串都可以字符序列的形式进行查询。 但是，这不是 LINQ 的一般用法。 对于复杂的模式匹配操作，请使用 <xref:System.Text.RegularExpressions.Regex> 类。

## <a name="example"></a>示例

以下示例查询一个字符串以确定它所包含的数字数量。 请注意，在第一次执行此查询后将“重用”此查询。 这是可能的，因为查询本身并不存储任何实际的结果。

```vb
Class QueryAString

    Shared Sub Main()

        ' A string is an IEnumerable data source.
        Dim aString As String = "ABCDE99F-J74-12-89A"

        ' Select only those characters that are numbers
        Dim stringQuery = From ch In aString
                          Where Char.IsDigit(ch)
                          Select ch
        ' Execute the query
        For Each c As Char In stringQuery
            Console.Write(c & " ")
        Next

        ' Call the Count method on the existing query.
        Dim count As Integer = stringQuery.Count()
        Console.WriteLine(System.Environment.NewLine & "Count = " & count)

        ' Select all characters before the first '-'
        Dim stringQuery2 = aString.TakeWhile(Function(c) c <> "-")

        ' Execute the second query
        For Each ch In stringQuery2
            Console.Write(ch)
        Next

        Console.WriteLine(System.Environment.NewLine & "Press any key to exit")
        Console.ReadKey()
    End Sub
End Class
' Output:
' 9 9 7 4 1 2 8 9
' Count = 8
' ABCDE99F
```

## <a name="compiling-the-code"></a>编译代码

使用 VB.NET 命名空间的 `Imports` 语句创建一个控制台应用程序项目。

## <a name="see-also"></a>请参阅

- [LINQ 和字符串（Visual Basic）](../../../../visual-basic/programming-guide/concepts/linq/linq-and-strings.md)
- [如何：将 LINQ 查询与正则表达式合并（Visual Basic）](../../../../visual-basic/programming-guide/concepts/linq/how-to-combine-linq-queries-with-regular-expressions.md)
