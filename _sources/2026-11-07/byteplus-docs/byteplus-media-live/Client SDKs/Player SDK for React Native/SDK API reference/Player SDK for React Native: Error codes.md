---
title: "Player SDK for React Native: Error codes"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-error-code"
---

<span id="veliveplayererror"></span>
## VeLivePlayerError  

Type：`class`

The playback error.

<span id="errorcode"></span>
### errorCode  

Type：`number`

`Readonly`, The error code.

<span id="errormsg"></span>
### errorMsg  

Type：`string`

`Readonly`, The error message.

<span id="veliveplayererrorcode"></span>
## VeLivePlayerErrorCode  

Type：`enum`

The playback error code.


|Property |Value |Description |
|---|---|---|
|VeLivePlayerNoError |`0` |No error. |
|VeLivePlayerInvalidLicense |`-1` |The SDK license is invalid. This error may occur due to incorrect integration of the license or if the license has expired. Review how the license was integrated and ensure that it is still valid. |
|VeLivePlayerInvalidParameter |`-2` |Invalid parameters. Check the input parameter and call the method again. |
|VeLivePlayerErrorRefused |`-3` |The method call has been rejected. This error occurs when the method is called at an incorrect time. |
|VeLivePlayerErrorLibraryLoadFailed |`-4` |Failed to load the library file. This error may occur due to incorrect integration of the SDK. |
|VeLivePlayerErrorPlayUrl |`-100` |The pull stream address does not exist or is invalid. This error may occur if the pull stream address is empty, or if the format or length of the address is invalid. |
|VeLivePlayerErrorNoStreamData |`-101` |Unable to get the stream data. This error may occur if the live stream does not exist, is interrupted, or has ended. Please check the status of the live stream. |
|VeLivePlayerErrorInternalRetryStart |`-102` |An internal retry to play the live stream, which might happen due to an internal player error. |
|VeLivePlayerErrorInternalRetryFailed |`-103` |An internal retry failed and the maximum number of internal retries is reached. The player has stopped retrying. You may attempt a manual retry. |
|VeLivePlayerErrorDnsParseFailed |`-200` |DNS parsing failed. This error may occur due to an error in the pull stream address or the client's network conditions. If the error persists after you verify the pull stream address and network conditions, contact BytePlus technical support for assistance. |
|VeLivePlayerErrorNetworkRequestFailed |`-201` |The network request failed. Check the network conditions. If the error persists, contact BytePlus technical support for assistance. |
|VeLivePlayerErrorDemuxFailed |`-300` |Video decapsulation failed. This error may occur if the live stream uses an unsupported format or protocol, or if there is an audio or video error. If the error persists, contact BytePlus technical support for assistance. |
|VeLivePlayerErrorDecodeFailed |`-301` |Decoding failed. This error may occur if the live stream uses an unsupported audio or video format. If the error persists, contact BytePlus technical support for assistance. |
|VeLivePlayerErrorAVOutputFailed |`-302` |Rendering failed. This error may occur if there is an issue with the audio or video output devices. If the error persists, contact BytePlus technical support for assistance. |
|VeLivePlayerErrorSRDeviceUnsupported |`-303` |The device model does not support super resolution. Contact BytePlus technical support for any assistance you may need. |
|VeLivePlayerErrorSRResolutionUnsupported |`-304` |The current resolution exceeds the upper limit allowed for super resolution. Contact BytePlus technical support for any assistance you may need. |
|VeLivePlayerErrorSRFpsUnsupported |`-305` |The current frame rate exceeds the upper limit allowed for super resolution. Contact BytePlus technical support for any assistance you may need. |
|VeLivePlayerErrorSRInitFail |`-306` |Fails to initialize super resolution. Contact BytePlus technical support if the error persists. |
|VeLivePlayerErrorSRExecuteFail |`-307` |Fails to apply super resolution to the video. Contact BytePlus technical support if the error persists. |
|VeLivePlayerLicenseUnsupportedH265 |`-308` |The current SDK license does not provide support for the H.265 feature. |
|VeLivePlayerDRMFetchCKCFailed |`-400` |DRM authentication fails. |
|VeLivePlayerDRMFetchSPCFailed |`-401` |Fails to generate Server Playback Context (SPC). |
|VeLivePlayerErrorInternal |`-999` |Internal error. Please contact BytePlus technical support for assistance. |
