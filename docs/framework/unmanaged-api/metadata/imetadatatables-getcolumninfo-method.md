---
title: IMetaDataTables::GetColumnInfo 方法
ms.date: 10/10/2019
api_name:
- IMetaDataTables.GetColumnInfo
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataTables::GetColumnInfo
helpviewer_keywords:
- IMetaDataTables::GetColumnInfo method [.NET Framework metadata]
- GetColumnInfo method [.NET Framework metadata]
ms.assetid: 68c160ea-ae7d-4750-985d-a038b2c8e7d9
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: dd67d9faafedf4fb92c69618d4464ebb2ce47dcc
ms.sourcegitcommit: 559259da2738a7b33a46c0130e51d336091c2097
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72774261"
---
# <a name="imetadatatablesgetcolumninfo-method"></a>IMetaDataTables::GetColumnInfo 方法
获取有关指定表中指定列的数据。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetColumnInfo (   
    [in]  ULONG        ixTbl,  
    [in]  ULONG        ixCol,  
    [out] ULONG        *poCol,  
    [out] ULONG        *pcbCol,  
    [out] ULONG        *pType,  
    [out] const char   **ppName  
);  
```  
  
## <a name="parameters"></a>参数
=======

 `ixTbl`  
 中所需表的索引。  
  
 `ixCol`  
 中所需列的索引。  
  
 `poCol`  
 弄指向行中列的偏移量的指针。  
  
 `pcbCol`  
 弄一个指针，指向列的大小（以字节为单位）。  
  
 `pType`  
 弄一个指针，指向列中值的类型。  
  
 `ppName`  
 弄指向列名的指针的指针。  
 
## <a name="remarks"></a>备注

返回的列类型位于值的范围内：

| pType                    | 描述   | Helper 函数                   |
|--------------------------|---------------|-----------------------------------|
| `0`.。`iRidMax`<br>（0-63）   | 去掉           | **IsRidType**<br>**IsRidOrToken** |
| `iCodedToken`.。`iCodedTokenMax`<br>（64.. 95） | 编码标记 | **IsCodedTokenType** <br>**IsRidOrToken** |
| `iSHORT` （96）            | Int16         | **IsFixedType**                   |
| `iUSHORT` （97）           | UInt16        | **IsFixedType**                   |
| `iLONG` （98）             | Int32         | **IsFixedType**                   |
| `iULONG` （99）            | UInt32        | **IsFixedType**                   |
| `iBYTE` （100）            | 字节          | **IsFixedType**                   |
| `iSTRING` （101）          | 字符串        | **IsHeapType**                    |
| `iGUID` （102）            | GUID          | **IsHeapType**                    |
| `iBLOB` （103）            | Blob          | **IsHeapType**                    |

可以使用读取存储在*堆*中的值（即 `IsHeapType == true`）：

- `iSTRING`： **IMetadataTables. GetString**
- `iGUID`： **IMetadataTables. GetGUID**
- `iBLOB`： **IMetadataTables. GetBlob**

> [!IMPORTANT]
> 若要使用上表中定义的常量，请包含*cor*头文件提供的指令 `#define _DEFINE_META_DATA_META_CONSTANTS`。

## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Cor  
  
 **库：** 用作 Mscoree.dll 中的资源  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [IMetaDataTables 接口](../../../../docs/framework/unmanaged-api/metadata/imetadatatables-interface.md)
- [IMetaDataTables2 接口](../../../../docs/framework/unmanaged-api/metadata/imetadatatables2-interface.md)
