---
Description: 'This topic describes how to register with the fax service.'
ms.assetid: '797a4d48-7676-4b0d-93bf-ebe3043da4a0'
title: Registration of a Fax Routing Extension
---

# Registration of a Fax Routing Extension

To register with the fax service, it is recommended that a fax routing extension DLL perform the following steps.

## To install an extension and register

1.  Copy the fax routing extension DLL to the location specified by the *ImageName* parameter to the [**FaxRegisterRoutingExtension**](-mfax-faxregisterroutingextension.md) function.
2.  Call the [**FaxConnectFaxServer**](-mfax-faxconnectfaxserver.md) function, specifying a **NULL** pointer in the *MachineName* parameter, to obtain a fax server handle to the local server.
3.  Call the [**FaxRegisterRoutingExtension**](-mfax-faxregisterroutingextension.md) function to register the fax routing extension DLL with the fax service. The function calls the [**FaxRoutingInstallationCallback**](-mfax-faxroutinginstallationcallback.md) function once for each fax routing method in the fax routing extension DLL.

If you install a fax routing extension by using a call to [**FaxRegisterRoutingExtension**](-mfax-faxregisterroutingextension.md), you must restart the fax service to use a fax routing method exported by that extension.

For information about developing a routing extension DLL, see [About the Fax Routing Extension API](-mfax-about-the-fax-routing-extension-api.md).

 

 


