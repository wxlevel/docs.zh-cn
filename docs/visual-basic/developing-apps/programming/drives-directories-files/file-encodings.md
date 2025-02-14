---
title: 文件编码 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- character encodings
- files [Visual Basic], encoding
- Unicode, file encoding
- file encoding
ms.assetid: ea2c5f5f-bbb1-4150-9928-b9951fa6bc57
ms.openlocfilehash: d73226c58d39c970ec02c32a2c188f2747a7d87e
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72583468"
---
# <a name="file-encodings-visual-basic"></a>文件编码 (Visual Basic)

文件编码也称为字符编码，用于指定在处理文本时如何表示字符。 虽然 Unicode 是最常用的编码，但根据编码能否处理某种语言字符，另一种编码可能更优。

读取或写入文件时，未正确匹配文件编码可能会导致发生异常或产生不正确的结果。

## <a name="types-of-encodings"></a>编码类型

处理文件时，Unicode 是首选编码。 Unicode 是全球范围的字符编码标准，使用 16 位代码值来表示现代计算中使用的所有字符，包括印刷中使用的技术符号和特殊字符。

以前的字符编码标准包括传统的字符集，如 Windows ANSI 字符集，该字符集使用 8 位代码值或 8 位值组合来表示特定语言或地理区域中使用的字符。

## <a name="encoding-class"></a>编码类

<xref:System.Text.Encoding> 类表示字符编码。 下表列出并描述了每个可用的编码类型。

|name|说明|
|---|---|
|<xref:System.Text.ASCIIEncoding>|表示 Unicode 字符的 ASCII 字符编码。|
|<xref:System.Text.UnicodeEncoding>|表示 Unicode 字符的 UTF-16 编码。|
|<xref:System.Text.UTF32Encoding>|表示 Unicode 字符的 UTF-32 编码。|
|<xref:System.Text.UTF7Encoding>|表示 Unicode 字符的 UTF-7 编码。|
|<xref:System.Text.UTF8Encoding>|表示 Unicode 字符的 UTF-8 编码。|

## <a name="see-also"></a>请参阅

- [从文件读取](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)
- [写入文件](../../../../visual-basic/developing-apps/programming/drives-directories-files/writing-to-files.md)
