﻿---
Description: 'Sets the signing key and two sequence numbers on a protected output object.'
ms.assetid: '278a80f5-198d-4311-aa43-10b6dc33b3a4'
title: SetOPMSigningKeyAndSequenceNumbers function
---

# SetOPMSigningKeyAndSequenceNumbers function

> \[!Important\]  
> This function is used by [Output Protection Manager](output-protection-manager.md) (OPM) to access functionality in the display driver. Applications should not call this function.

 

Sets the signing key and two sequence numbers on a protected output object.

## Syntax


```C++
NTSTATUS WINAPI SetOPMSigningKeyAndSequenceNumbers(
  _In_        OPM_PROTECTED_OUTPUT_HANDLE      opoOPMProtectedOutput,
  _Out_ const DXGKMDT_OPM_ENCRYPTED_PARAMETERS *pParameters
);
```



## Parameters

<dl> <dt>

*opoOPMProtectedOutput* \[in\]
</dt> <dd>

A handle to the protected output object. This handle is obtained by calling [**CreateOPMProtectedOutputs**](createopmprotectedoutputs.md).

</dd> <dt>

*pParameters* \[out\]
</dt> <dd>

A pointer to a [**DXGKMDT\_OPM\_ENCRYPTED\_PARAMETERS**](display.dxgkmdt_opm_encrypted_parameters) structure that contains a 256-byte array. For more information about how to initialize this array, see [DxgkDdiOPMSetSigningKeyAndSequenceNumbers](http://msdn.microsoft.com/en-us/library/aa906703.aspx).

</dd> </dl>

## Return value

If the method succeeds, it returns **STATUS\_SUCCESS**. Otherwise, it returns an **NTSTATUS** error code.

## Remarks

Applications should call [**IOPMVideoOutput::FinishInitialization**](iopmvideooutput-iopmvideooutput--finishinitialization.md) instead of calling this function.

This function has no associated import library. To call this function, you must use the [**LoadLibrary**](base.loadlibrary) and [**GetProcAddress**](base.getprocaddress) functions to dynamically link to Gdi32.dll.

## Requirements



|                                     |                                                                                      |
|-------------------------------------|--------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows Vista \[desktop apps only\]<br/>                                       |
| Minimum supported server<br/> | Windows Server 2008 \[desktop apps only\]<br/>                                 |
| DLL<br/>                      | <dl> <dt>Gdi32.dll</dt> </dl> |



## See also

<dl> <dt>

[OPM Functions](opm-functions.md)
</dt> <dt>

[Output Protection Manager](output-protection-manager.md)
</dt> </dl>

 

 



