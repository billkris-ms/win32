﻿---
Description: '.'
ms.assetid: 'CD3DBBA5-AE5C-4DC1-BE52-696138494701'
title: 'DOT4\_ACTIVITY structure'
---

# DOT4\_ACTIVITY structure

## Syntax


```C++
typedef struct _DOT4_ACTIVITY {
  ULONG          ulMessage;
  ULONG          ulByteCount;
  CHANNEL_HANDLE hChannel;
} DOT4_ACTIVITY, *PDOT4_ACTIVITY;
```



## Members

<dl> <dt>

**ulMessage**
</dt> <dd></dd> <dt>

**ulByteCount**
</dt> <dd></dd> <dt>

**hChannel**
</dt> <dd></dd> </dl>

## Requirements



|                   |                                                                                      |
|-------------------|--------------------------------------------------------------------------------------|
| Header<br/> | <dl> <dt>D4iface.h</dt> </dl> |



 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bprint\print%5D:%20DOT4_ACTIVITY%20structure%20%20RELEASE:%20%285/12/2018%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/en-us/default.aspx. "Send comments about this topic to Microsoft")



