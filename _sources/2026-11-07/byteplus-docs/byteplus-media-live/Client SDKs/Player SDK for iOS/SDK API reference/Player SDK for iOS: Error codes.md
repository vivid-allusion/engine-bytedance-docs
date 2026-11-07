---
title: "Player SDK for iOS: Error codes"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api-error-code"
---

<span id="VeLivePlayerError"></span>
# VeLivePlayerError

```objectivec
@interface VeLivePlayerError : NSError
```


The Player SDK error.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSInteger |[errorCode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError-errorcode) |
|NSInteger |[subErrorCode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError-suberrorcode) |
|NSString\* |[errorMsg](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError-errormsg) |


<span id="instructions"></span>
## Instructions

<span id="VeLivePlayerError-errorcode"></span>
### errorCode

```objectivec
@property (nonatomic, readonly) NSInteger errorCode;
```


The Player SDK error code.

<span id="VeLivePlayerError-suberrorcode"></span>
### subErrorCode

```objectivec
@property (nonatomic, readonly) NSInteger subErrorCode;
```


The Player SDK sub error code.

<span id="VeLivePlayerError-errormsg"></span>
### errorMsg

```objectivec
@property (nonatomic, readonly, nullable) NSString* errorMsg;
```


The Player SDK error message.

<span id="VeLivePlayerErrorCode"></span>
# VeLivePlayerErrorCode

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerErrorCode
)
```


The Player SDK error codes.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerNoError |0 |No error. |
|VeLivePlayerInvalidLicense |\-1 |The license is invalid. This may be caused by a license integration error or an expired license.<br><br>**Please check the license integration and validity period. If the problem persists, please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.**  |
|VeLivePlayerInvalidParameter |\-2 |Invalid parameters.<br><br>**Please check and try again.**  |
|VeLivePlayerErrorRefused |\-3 |The call was rejected due to incorrect timing.<br><br>**Please check the timing and try again. It is recommended to handle this error during the development phase.**  |
|VeLivePlayerErrorLibraryLoadFailed |\-4 |Failed to load the library file. This may be caused by an SDK integration error.<br><br>**Please check the SDK integration and try again. It is recommended to handle this error during the development phase.**  |
|VeLivePlayerErrorPlayUrl |\-100 |The pull stream address does not exist or is invalid. This may be caused by the pull stream address being empty, having an invalid format, or exceeding the length limit.<br><br>**During development, you can monitor this error to troubleshoot usage issues. If this error occurs in a production environment, it is recommended to notify viewers with a prominent alert that the player is unavailable and ask them to restart the player.**  |
|VeLivePlayerErrorNoStreamData |\-101 |The stream data does not exist or the network request failed. This may be caused by the live stream not existing, being interrupted, or having ended.<br><br>**It is recommended to replace the pull stream address, switch to a low\-bitrate stream, or prompt viewers about network issues.**  |
|VeLivePlayerErrorInternalRetryStart |\-102 |An internal retry of the player. This may be caused by an internal player error.<br><br>**It is recommended to replace the pull stream address, switch to a low\-bitrate stream, or prompt viewers about network issues.**  |
|VeLivePlayerErrorInternalRetryFailed |\-103 |Internal retry of the player failed. The player has stopped retrying after reaching the maximum number of retry attempts.<br><br>**It is recommended to replace the pull stream address, switch to a low\-bitrate stream, or prompt viewers about network issues.**  |
|VeLivePlayerErrorDnsParseFailed |\-200 |DNS parsing failed. This may be caused by an abnormal pull stream address or abnormal client network conditions.<br><br>**It is recommended to replace the pull stream address, switch to a low\-bitrate stream, or prompt viewers about network issues.**  |
|VeLivePlayerErrorNetworkRequestFailed |\-201 |The network request failed.<br><br>**It is recommended to replace the pull stream address, switch to a low\-bitrate stream, or prompt viewers about network issues.**  |
|VeLivePlayerErrorDemuxFailed |\-300 |Demuxing failed. This may be caused by an unsupported stream format or protocol, or audio/video stream errors.<br><br>**It is recommended to replace the pull stream address, switch to a low\-bitrate stream, or prompt viewers about network issues.**  |
|VeLivePlayerErrorDecodeFailed |\-301 |Video decoding failed. This may be caused by an unsupported live stream audio/video format or a decoder error.<br><br>**It is recommended to replace the pull stream address, switch to a low\-bitrate stream, or prompt viewers about network issues. If the problem persists, please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.**  |
|VeLivePlayerErrorAVOutputFailed |\-302 |Rendering failed. This may be caused by an abnormal audio or video output device.<br><br>**If this error occurs in a production environment, it is recommended to notify viewers with a prominent alert that the player is unavailable and ask them to restart the player.**  |
|VeLivePlayerErrorSRDeviceUnsupported |\-303 |The current device is not on the allowlist of super\-resolution models and does not support the super\-resolution feature.<br><br>**During development, you can monitor this error to troubleshoot usage issues. Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.**  |
|VeLivePlayerErrorSRResolutionUnsupported |\-304 |The resolution exceeds the super\-resolution limit.<br><br>**During development, you can monitor this error to troubleshoot usage issues. Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.**  |
|VeLivePlayerErrorSRFpsUnsupported |\-305 |The frame rate exceeds the super\-resolution limit.<br><br>**During development, you can monitor this error to troubleshoot usage issues. Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.**  |
|VeLivePlayerErrorSRInitFail |\-306 |Failed to initialize super\-resolution.<br><br>**During development, you can monitor this error to troubleshoot usage issues. Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.**  |
|VeLivePlayerErrorSRExecuteFail |\-307 |Failed to execute super\-resolution.<br><br>**During development, you can monitor this error to troubleshoot usage issues. Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.**  |
|VeLivePlayerLicenseUnsupportedH265 |\-308 |The basic license you are using does not support the H.265 hardware and software decoding features.<br><br>**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.**  |
|VeLivePlayerErrorSharpenDeviceUnsupported |\-309 |The device does not support the video sharpening feature.<br><br>**During development, you can monitor this error to troubleshoot usage issues. Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.**  |
|VeLivePlayerErrorSharpenResolutionUnsupported |\-310 |The resolution exceeds the video sharpening limit.<br><br>**During development, you can monitor this error to troubleshoot usage issues. Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.**  |
|VeLivePlayerErrorSharpenFpsUnsupported |\-312 |The frame rate exceeds the video sharpening limit.<br><br>**During development, you can monitor this error to troubleshoot usage issues. Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.**  |
|VeLivePlayerErrorSharpenInitFail |\-313 |Failed to initialize video sharpening.<br><br>**During development, you can monitor this error to troubleshoot usage issues. Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.**  |
|VeLivePlayerErrorLicenseUnsupportedABR |\-315 |The basic license you are using does not support the adaptive bitrate (ABR) streaming feature.<br><br>**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.**  |
|VeLivePlayerErrorLicenseUnsupportedDRM |\-316 |The basic license you are using does not support playing DRM (Digital Rights Management)\-encrypted streams.<br><br>**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.**  |
|VeLivePlayerErrorLicenseUnsupportedSEI |\-317 |The basic license you are using does not support the Supplemental Enhancement Information (SEI) message reception feature.<br><br>**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.**  |
|VeLivePlayerErrorLicenseUnsupportedSuperResolution |\-318 |The basic license you are using does not support the super\-resolution feature.<br><br>**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.**  |
|VeLivePlayerErrorLicenseUnsupportedSharpen |\-319 |The basic license you are using does not support the video sharpening feature.<br><br>**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.**  |
|VeLivePlayerErrorLicenseUnsupportedQUIC |\-320 |The basic license you are using does not support the QUIC protocol.<br><br>**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.**  |
|VeLivePlayerErrorLicenseUnsupportedRTM |\-323 |The basic license you are using does not support playing RTM streams.<br><br>**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.**  |
|VeLivePlayerErrorLicenseUnsupportedMainBackup |\-324 |The basic license you are using does not support the primary\-backup stream switching feature.<br><br>**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.**  |
|VeLivePlayerErrorLicenseUnsupportedFLVLowLatency |\-325 |The basic license you are using does not support playing low\-latency FLV streams (with a latency of 2 to 3 seconds).<br><br>**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.**  |
|VeLivePlayerDRMFetchCKCFailed |\-400 |DRM authentication failed.<br><br>**If this error occurs in a production environment, it is recommended to notify viewers with a prominent alert that the player is unavailable and ask them to restart the player.**  |
|VeLivePlayerDRMFetchSPCFailed |\-401 |Failed to generate the Server Playback Context (SPC).<br><br>**If this error occurs in a production environment, it is recommended to notify viewers with a prominent alert that the player is unavailable and ask them to restart the player.**  |
|VeLivePlayerErrorNotSupportResolutionSwitch |\-510 |The player does not support quality level switching.<br><br>**During development, you can monitor this error to troubleshoot usage issues. Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.**  |
|VeLivePlayerErrorInternal |\-999 |Internal error.<br><br>**Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.**  |
