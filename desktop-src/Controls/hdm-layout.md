---
title: HDM\_LAYOUT message
description: Retrieves information used to set the size and position of the header control within the target rectangle of the parent window. You can send this message explicitly or use the Header\_Layout macro.
ms.assetid: '0763e483-f01d-4739-8c61-1c52d1aad0b4'
keywords: ["HDM_LAYOUT message Windows Controls"]
topic_type:
- apiref
api_name:
- HDM_LAYOUT
api_location:
- Commctrl.h
api_type:
- HeaderDef
---

# HDM\_LAYOUT message

Retrieves information used to set the size and position of the header control within the target rectangle of the parent window. You can send this message explicitly or use the [**Header\_Layout**](header-layout.md) macro.

## Parameters

<dl> <dt>

*wParam* 
</dt> <dd>Must be zero.</dd> <dt>

*lParam* 
</dt> <dd>

A pointer to an [**HDLAYOUT**](hdlayout.md) structure. The **prc** member specifies the coordinates of a rectangle, and the **pwpos** member receives the size and position for the header control within the rectangle.

</dd> </dl>

## Return value

Returns **TRUE** if successful, or **FALSE** otherwise.

## Remarks

The **pwpos** member of the *lParam* structure receives size and position values appropriate for positioning the control along the top of the specified rectangle. The height value is the sum of the heights of the control's horizontal borders and the average height of characters in the font currently selected into the control's device context.

To use **HDM\_LAYOUT** to set the initial size and position of a header control, set the initial visibility state of the control so that it is hidden. After sending **HDM\_LAYOUT** to retrieve the size and position values, use the [**SetWindowPos**](https://msdn.microsoft.com/library/windows/desktop/ms633545) function to set the new size, position, and visibility state.

## Requirements



|                                     |                                                                                       |
|-------------------------------------|---------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows�Vista \[desktop apps only\]<br/>                                        |
| Minimum supported server<br/> | Windows Server�2003 \[desktop apps only\]<br/>                                  |
| Header<br/>                   | <dl> <dt>Commctrl.h</dt> </dl> |



�

�




