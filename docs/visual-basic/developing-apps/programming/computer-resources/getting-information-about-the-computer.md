---
title: 获取有关计算机的信息 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- My.Computer.Info object [Visual Basic], tasks
ms.assetid: 13c145bc-5c85-4fea-a5dd-2ca8681a0252
ms.openlocfilehash: c313f96ec17e2cfb1d94fedebbce5b2f5b8dbc95
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72581262"
---
# <a name="getting-information-about-the-computer-visual-basic"></a>获取有关计算机的信息 (Visual Basic)

`My.Computer.Info` 对象提供了一些属性，可用于获取有关计算机内存、已加载的程序集、名称以及操作系统的信息。

## <a name="remarks"></a>备注

下表列出了通常使用 `My.Computer.Info` 对象完成的任务，并提供了演示如何执行每个任务的主题链接。

|功能|查看|
|---|---|
|确定在安装应用程序的计算机上有多少可用的虚拟地址空间|<xref:Microsoft.VisualBasic.Devices.ComputerInfo.TotalVirtualMemory%2A>|
|确定正在运行应用程序的计算机的平台类型|<xref:Microsoft.VisualBasic.Devices.ComputerInfo.OSPlatform%2A>|
|确定正在运行应用程序的计算机的操作系统|<xref:Microsoft.VisualBasic.Devices.ComputerInfo.OSFullName%2A>|
|确定正在运行应用程序的计算机上已安装的服务包|<xref:Microsoft.VisualBasic.Devices.ComputerInfo.OSVersion%2A>|
|确定正在运行应用程序的计算机上已安装的 `UICulture`。|<xref:Microsoft.VisualBasic.Devices.ComputerInfo.InstalledUICulture%2A>|

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualBasic.Devices.ServerComputer.Info%2A>
