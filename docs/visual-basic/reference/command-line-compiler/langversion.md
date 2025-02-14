---
title: -langversion （Visual Basic）
ms.date: 03/10/2018
helpviewer_keywords:
- /langversion compiler option [Visual Basic]
- langversion compiler option [Visual Basic]
- -langversion compiler option [Visual Basic]
ms.assetid: 59b7b0c8-2dde-4e9b-94e7-0237f7e0bafb
ms.openlocfilehash: 5f59f1c4c269a52131a324bbd2bfbe817ab794a4
ms.sourcegitcommit: 5a28f8eb071fcc09b045b0c4ae4b96898673192e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73197085"
---
# <a name="-langversion-visual-basic"></a>-langversion （Visual Basic）
导致编译器仅接受指定 Visual Basic 语言版本中包含的语法。  
  
## <a name="syntax"></a>语法  
  
```console  
-langversion:version  
```  
  
## <a name="arguments"></a>自变量  
 `version`  
 必须的。 要在编译过程中使用的语言版本。 接受的值为 `9`、`10`、`11`、`12`、`14`、`15`、`15.3`、`15.5`、`default` 和 `latest`。

 还可以使用 `.0` 作为次要版本来指定任何整数，例如 `11.0`。

 可以通过在命令行上指定 `-langversion:?`，查看所有可能值的列表。  
  
## <a name="remarks"></a>备注  
 `-langversion` 选项指定编译器接受的语法。 例如，如果指定语言版本为9.0，则编译器将生成仅在版本10.0 和更高版本中有效的语法错误。  
  
 当开发面向不同版本的 .NET Framework 的应用程序时，可以使用此选项。 例如，如果以 .NET Framework 3.5 为目标，则可以使用此选项来确保不使用语言版本10.0 中的语法。  
  
 只能使用命令行直接设置 `-langversion`。 有关详细信息，请参阅[面向特定的 .NET Framework 版本](/visualstudio/ide/visual-studio-multi-targeting-overview)。  
  
## <a name="example"></a>示例  
 下面的代码编译 Visual Basic 9.0 `sample.vb`。  
  
```console  
vbc -langversion:9.0 sample.vb  
```  
  
## <a name="see-also"></a>请参阅

- [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)
- [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [面向特定的 .NET Framework 版本](/visualstudio/ide/visual-studio-multi-targeting-overview)
