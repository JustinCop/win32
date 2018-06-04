---
title: IPropFindMultiResponse GetLength method
description: IPropFindMultiResponse GetLength method
ms.assetid: 92f2578d-d403-4892-b0d1-f670c8e9e75c
keywords:
- GetLength method Windows Mail (formerly Outlook Express)
- GetLength method Windows Mail (formerly Outlook Express) , IPropFindMultiResponse interface
- IPropFindMultiResponse interface Windows Mail (formerly Outlook Express) , GetLength method
topic_type:
- apiref
api_name:
- IPropFindMultiResponse.GetLength
api_location:
- Inetcomm.dll
api_type:
- COM
ms.technology: desktop
ms.prod: windows
ms.author: windowssdkdev
ms.topic: article
ms.date: 05/31/2018
---

# IPropFindMultiResponse::GetLength method

\[**IPropFindMultiResponse::GetLength** is available for use in the operating systems specified in the Requirements section. It may be altered or unavailable in subsequent versions.\]

## Syntax


```C++
HRESULT GetLength(
  [out] ULONG *pulLength
);
```



## Parameters

<dl> <dt>

*pulLength* \[out\]
</dt> <dd>

Type: **ULONG\***

Returns address of length variable.

</dd> </dl>

## Return value

Type: **HRESULT**

If this method succeeds, it returns **S\_OK**. Otherwise, it returns an **HRESULT** error code.

## Requirements



|                                     |                                                                                                                |
|-------------------------------------|----------------------------------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows XP \[desktop apps only\]<br/>                                                                    |
| Minimum supported server<br/> | Windows Server 2003 \[desktop apps only\]<br/>                                                           |
| Product<br/>                  | Outlook Express 6.0<br/>                                                                                 |
| Header<br/>                   | <dl> <dt>Imnxport.h</dt> </dl>                          |
| IDL<br/>                      | <dl> <dt>Imnxport.idl</dt> </dl>                        |
| DLL<br/>                      | <dl> <dt>Inetcomm.dll (version 6.0 or later)</dt> </dl> |



 

 




