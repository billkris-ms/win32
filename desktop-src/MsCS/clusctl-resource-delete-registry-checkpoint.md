---
title: CLUSCTL\_RESOURCE\_DELETE\_REGISTRY\_CHECKPOINT control code
description: Removes a registry tree from the list of registry trees that are being replicated for a resource. Applications use this control code as a ClusterResourceControl parameter.
audience: developer
author: REDMOND\\markl
manager: REDMOND\\markl
ms.assetid: 'ff1bd331-d401-41e7-b07b-60b10816d301'
ms.prod: 'windows-server-dev'
ms.technology: 'failover-clustering'
ms.tgt_platform: multiple
keywords: ["CLUSCTL_RESOURCE_DELETE_REGISTRY_CHECKPOINT control code Failover Cluster"]
topic_type:
- apiref
api_name:
- CLUSCTL_RESOURCE_DELETE_REGISTRY_CHECKPOINT
api_location:
- ClusAPI.h
api_type:
- HeaderDef
---

# CLUSCTL\_RESOURCE\_DELETE\_REGISTRY\_CHECKPOINT control code

Removes a registry tree from the list of registry trees that are being replicated for a [resource](resources.md). Applications use this [control code](about-control-codes.md) as a [**ClusterResourceControl**](clusterresourcecontrol.md) parameter.


```C++
ClusterResourceControl( 
  hResource,                                   // resource handle
  hHostNode,                                   // optional node handle
  CLUSCTL_RESOURCE_DELETE_REGISTRY_CHECKPOINT, // this control code 
  lpInBuffer,                                  // input buffer: string
  cbInBufferSize,                              // input buffer size (bytes)
  NULL,                                        // not used
  0,                                           // not used
  NULL );                                      // not used
```



## Parameters

The following control code function parameters are specific to this control code. For complete parameter descriptions, see [**ClusterResourceControl**](clusterresourcecontrol.md).

<dl> <dt>

*lpInBuffer* 
</dt> <dd>

Pointer to a null-terminated Unicode string containing the registry key name at the root of the subtree that should be replicated for the resource. This is a key name that is relative to **HKEY\_LOCAL\_MACHINE**, such as **Software\\Microsoft**\\*My Application*. Do not use a leading backslash character ("\\") in the relative path or the call will fail.

</dd> </dl>

## Return value

[**ClusterResourceControl**](clusterresourcecontrol.md) returns one of the following values:

<dl> <dt>

**ERROR\_SUCCESS**
</dt> <dd>

The operation was successful.

</dd> <dt>

**ERROR\_FILE\_NOT\_FOUND**
</dt> <dd>

The specified key is not currently being checkpointed.

</dd> <dt>

**[System error code](https://msdn.microsoft.com/library/windows/desktop/ms681381)**
</dt> <dd>

The operation failed.

</dd> </dl>

## Remarks

ClusAPI.h defines the 32 bits of CLUSCTL\_RESOURCE\_DELETE\_REGISTRY\_CHECKPOINT as follows (for more information, see [Control Code Architecture](control-code-architecture.md)).



| Component      | Bit location | Value                                                         |
|----------------|--------------|---------------------------------------------------------------|
| Object code    | 24�31        | **CLUS\_OBJECT\_RESOURCE** (0x1)<br/>                   |
| Global bit     | 23           | **CLUS\_NOT\_GLOBAL** (0x0)<br/>                        |
| Modify bit     | 22           | **CLUS\_MODIFY** (0x1)<br/>                             |
| User bit       | 21           | **CLCTL\_CLUSTER\_BASE** (0x0)<br/>                     |
| Type bit       | 20           | External (0x0)<br/>                                     |
| Operation code | 0�23         | **CLCTL\_DELETE\_REGISTRY\_CHECKPOINT** (0x4000a6)<br/> |
| Access code    | 0�1          | **CLUS\_ACCESS\_WRITE** (0x2)<br/>                      |



�

### Resource DLL Support

The CLUSCTL\_RESOURCE\_DELETE\_REGISTRY\_CHECKPOINT control code is handled by the [Cluster service](cluster-service.md) and is not passed to [resource DLLs](resource-dlls.md).

## Requirements



|                                     |                                                                                      |
|-------------------------------------|--------------------------------------------------------------------------------------|
| Minimum supported client<br/> | None supported<br/>                                                            |
| Minimum supported server<br/> | Windows Server�2008 Enterprise, Windows Server�2008 Datacenter<br/>            |
| Header<br/>                   | <dl> <dt>ClusAPI.h</dt> </dl> |



## See also

<dl> <dt>

[CLUSCTL\_RESOURCE\_ADD\_REGISTRY\_CHECKPOINT](clusctl-resource-add-registry-checkpoint.md)
</dt> <dt>

[**ClusterResourceControl**](clusterresourcecontrol.md)
</dt> <dt>

[**ResourceControl**](resourcecontrol.md)
</dt> </dl>

�

�




