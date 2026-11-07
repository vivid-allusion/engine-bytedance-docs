---
title: "Player SDK for Android: Error codes"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-errorcode"
---

<span id="VeLivePlayerError"></span>
# VeLivePlayerError

```java
public class com.ss.videoarch.liveplayer.VeLivePlayerError
```


The Player SDK error.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |`-` |[mErrorCode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerError-merrorcode) |
|String |`-` |[mErrorMsg](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerError-merrormsg) |
|int |\-1 |[mSubCode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerError-msubcode) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|VeLivePlayerError |[VeLivePlayerError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerError-veliveplayererror-4) |


<span id="instructions"></span>
## Instructions

<span id="VeLivePlayerError-merrorcode"></span>
### mErrorCode

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerError.mErrorCode
```


The Player SDK error code.

<span id="VeLivePlayerError-merrormsg"></span>
### mErrorMsg

```java
public String com.ss.videoarch.liveplayer.VeLivePlayerError.mErrorMsg
```


The Player SDK error message.

<span id="VeLivePlayerError-msubcode"></span>
### mSubCode

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerError.mSubCode = -1
```


The Player SDK sub error code.

<span id="instructions"></span>
## Instructions

<span id="VeLivePlayerError-veliveplayererror-4"></span>
### VeLivePlayerError

```java
public com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerError(
    int errorCode,
    int subCode,
    String errorMsg
)
```


Create a `VeLivePlayerError` instance containing the error code, sub error code, and error message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|errorCode |int |The error code. |
|subCode |int |The sub error code. |
|errorMsg |String |The error message. |


**Return Value**

The `VeLivePlayerError` instance.

<span id="VeLivePlayerErrorCode"></span>
# VeLivePlayerErrorCode

```java
public static class com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode
```


The Player SDK error codes.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |0 |[VeLivePlayerNoError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayernoerror) |
|int |\-1 |[VeLivePlayerInvalidLicense](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayerinvalidlicense) |
|int |\-2 |[VeLivePlayerInvalidParameter](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayerinvalidparameter) |
|int |\-3 |[VeLivePlayerErrorRefused](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorrefused) |
|int |\-4 |[VeLivePlayerErrorLibraryLoadFailed](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlibraryloadfailed) |
|int |\-100 |[VeLivePlayerErrorPlayUrl](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorplayurl) |
|int |\-101 |[VeLivePlayerErrorNoStreamData](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrornostreamdata) |
|int |\-102 |[VeLivePlayerErrorInternalRetryStart](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorinternalretrystart) |
|int |\-103 |[VeLivePlayerErrorInternalRetryFailed](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorinternalretryfailed) |
|int |\-200 |[VeLivePlayerErrorDnsParseFailed](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrordnsparsefailed) |
|int |\-201 |[VeLivePlayerErrorNetworkRequestFailed](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrornetworkrequestfailed) |
|int |\-300 |[VeLivePlayerErrorDemuxFailed](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrordemuxfailed) |
|int |\-301 |[VeLivePlayerErrorDecodeFailed](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrordecodefailed) |
|int |\-302 |[VeLivePlayerErrorAVOutputFailed](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererroravoutputfailed) |
|int |\-303 |[VeLivePlayerErrorSRDeviceUnsupported](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorsrdeviceunsupported) |
|int |\-304 |[VeLivePlayerErrorSRResolutionUnsupported](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorsrresolutionunsupported) |
|int |\-305 |[VeLivePlayerErrorSRFpsUnsupported](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorsrfpsunsupported) |
|int |\-306 |[VeLivePlayerErrorSRInitFail](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorsrinitfail) |
|int |\-307 |[VeLivePlayerErrorSRExecuteFail](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorsrexecutefail) |
|int |\-308 |[VeLivePlayerLicenseUnsupportedH265](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayerlicenseunsupportedh265) |
|int |\-309 |[VeLivePlayerErrorSharpenDeviceUnsupported](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorsharpendeviceunsupported) |
|int |\-310 |[VeLivePlayerErrorSharpenResolutionUnsupported](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorsharpenresolutionunsupported) |
|int |\-312 |[VeLivePlayerErrorSharpenFpsUnsupported](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorsharpenfpsunsupported) |
|int |\-313 |[VeLivePlayerErrorSharpenInitFail](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorsharpeninitfail) |
|int |\-314 |[VeLivePlayerErrorLicenseUnsupportedH266](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedh266) |
|int |\-315 |[VeLivePlayerErrorLicenseUnsupportedABR](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedabr) |
|int |\-316 |[VeLivePlayerErrorLicenseUnsupportedDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupporteddrm) |
|int |\-317 |[VeLivePlayerErrorLicenseUnsupportedSEI](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedsei) |
|int |\-318 |[VeLivePlayerErrorLicenseUnsupportedSuperResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedsuperresolution) |
|int |\-319 |[VeLivePlayerErrorLicenseUnsupportedSharpen](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedsharpen) |
|int |\-320 |[VeLivePlayerErrorLicenseUnsupportedQUIC](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedquic) |
|int |\-321 |[VeLivePlayerErrorLicenseUnsupportedCMAF](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedcmaf) |
|int |\-323 |[VeLivePlayerErrorLicenseUnsupportedRTM](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedrtm) |
|int |\-324 |[VeLivePlayerErrorLicenseUnsupportedMainBackup](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedmainbackup) |
|int |\-325 |[VeLivePlayerErrorLicenseUnsupportedFLVLowLatency](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedflvlowlatency) |
|int |\-400 |[VeLivePlayerDRMFetchCKCFailed](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayerdrmfetchckcfailed) |
|int |\-401 |[VeLivePlayerDRMFetchSPCFailed](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayerdrmfetchspcfailed) |
|int |\-510 |[VeLivePlayerErrorNotSupportResolutionSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrornotsupportresolutionswitch) |
|int |\-999 |[VeLivePlayerErrorInternal](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorinternal) |


<span id="instructions"></span>
## Instructions

<span id="VeLivePlayerErrorCode-veliveplayernoerror"></span>
### VeLivePlayerNoError

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerNoError = 0
```


No error.

<span id="VeLivePlayerErrorCode-veliveplayerinvalidlicense"></span>
### VeLivePlayerInvalidLicense

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerInvalidLicense = -1
```


The license is invalid. This may be caused by a license integration error or an expired license.

**Please check the license integration and validity period. If the problem persists, please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.** 

<span id="VeLivePlayerErrorCode-veliveplayerinvalidparameter"></span>
### VeLivePlayerInvalidParameter

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerInvalidParameter = -2
```


Invalid parameters.

**Please check and try again.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorrefused"></span>
### VeLivePlayerErrorRefused

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorRefused = -3
```


The call was rejected due to incorrect timing.

**Please check the timing and try again. It is recommended to handle this error during the development phase.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorlibraryloadfailed"></span>
### VeLivePlayerErrorLibraryLoadFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLibraryLoadFailed = -4
```


Failed to load the library file. This may be caused by an SDK integration error.

**Please check the SDK integration and try again. It is recommended to handle this error during the development phase.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorplayurl"></span>
### VeLivePlayerErrorPlayUrl

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorPlayUrl = -100
```


The pull stream address does not exist or is invalid. This may be caused by the pull stream address being empty, having an invalid format, or exceeding the length limit.

**During development, you can monitor this error to troubleshoot usage issues. If this error occurs in a production environment, it is recommended to notify viewers with a prominent alert that the player is unavailable and ask them to restart the player.** 

<span id="VeLivePlayerErrorCode-veliveplayererrornostreamdata"></span>
### VeLivePlayerErrorNoStreamData

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorNoStreamData = -101
```


The stream data does not exist or the network request failed. This may be caused by the live stream not existing, being interrupted, or having ended.

**It is recommended to replace the pull stream address, switch to a low\-bitrate stream, or prompt viewers about network issues.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorinternalretrystart"></span>
### VeLivePlayerErrorInternalRetryStart

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorInternalRetryStart = -102
```


An internal retry of the player. This may be caused by an internal player error.

**It is recommended to replace the pull stream address, switch to a low\-bitrate stream, or prompt viewers about network issues.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorinternalretryfailed"></span>
### VeLivePlayerErrorInternalRetryFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorInternalRetryFailed = -103
```


Internal retry of the player failed. The player has stopped retrying after reaching the maximum number of retry attempts.

**It is recommended to replace the pull stream address, switch to a low\-bitrate stream, or prompt viewers about network issues.** 

<span id="VeLivePlayerErrorCode-veliveplayererrordnsparsefailed"></span>
### VeLivePlayerErrorDnsParseFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorDnsParseFailed = -200
```


DNS parsing failed. This may be caused by an abnormal pull stream address or abnormal client network conditions.

**It is recommended to replace the pull stream address, switch to a low\-bitrate stream, or prompt viewers about network issues.** 

<span id="VeLivePlayerErrorCode-veliveplayererrornetworkrequestfailed"></span>
### VeLivePlayerErrorNetworkRequestFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorNetworkRequestFailed = -201
```


The network request failed.

**It is recommended to replace the pull stream address, switch to a low\-bitrate stream, or prompt viewers about network issues.** 

<span id="VeLivePlayerErrorCode-veliveplayererrordemuxfailed"></span>
### VeLivePlayerErrorDemuxFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorDemuxFailed = -300
```


Demuxing failed. This may be caused by an unsupported stream format or protocol, or audio/video stream errors.

**It is recommended to replace the pull stream address, switch to a low\-bitrate stream, or prompt viewers about network issues.** 

<span id="VeLivePlayerErrorCode-veliveplayererrordecodefailed"></span>
### VeLivePlayerErrorDecodeFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorDecodeFailed = -301
```


Video decoding failed. This may be caused by an unsupported live stream audio/video format or a decoder error.

**It is recommended to replace the pull stream address, switch to a low\-bitrate stream, or prompt viewers about network issues. If the problem persists, please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.** 

<span id="VeLivePlayerErrorCode-veliveplayererroravoutputfailed"></span>
### VeLivePlayerErrorAVOutputFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorAVOutputFailed = -302
```


Rendering failed. This may be caused by an abnormal audio or video output device.

**If this error occurs in a production environment, it is recommended to notify viewers with a prominent alert that the player is unavailable and ask them to restart the player.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorsrdeviceunsupported"></span>
### VeLivePlayerErrorSRDeviceUnsupported

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSRDeviceUnsupported = -303
```


The current device is not on the allowlist of super\-resolution models and does not support the super\-resolution feature.

**During development, you can monitor this error to troubleshoot usage issues. Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorsrresolutionunsupported"></span>
### VeLivePlayerErrorSRResolutionUnsupported

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSRResolutionUnsupported = -304
```


The resolution exceeds the super\-resolution limit.

**During development, you can monitor this error to troubleshoot usage issues. Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorsrfpsunsupported"></span>
### VeLivePlayerErrorSRFpsUnsupported

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSRFpsUnsupported = -305
```


The frame rate exceeds the super\-resolution limit.

**During development, you can monitor this error to troubleshoot usage issues. Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorsrinitfail"></span>
### VeLivePlayerErrorSRInitFail

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSRInitFail = -306
```


Failed to initialize super\-resolution.

**During development, you can monitor this error to troubleshoot usage issues. Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorsrexecutefail"></span>
### VeLivePlayerErrorSRExecuteFail

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSRExecuteFail = -307
```


Failed to execute super\-resolution.

**During development, you can monitor this error to troubleshoot usage issues. Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.** 

<span id="VeLivePlayerErrorCode-veliveplayerlicenseunsupportedh265"></span>
### VeLivePlayerLicenseUnsupportedH265

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerLicenseUnsupportedH265 = -308
```


The basic license you are using does not support the H.265 hardware and software decoding features.

**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorsharpendeviceunsupported"></span>
### VeLivePlayerErrorSharpenDeviceUnsupported

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSharpenDeviceUnsupported = -309
```


The device does not support the video sharpening feature.

**During development, you can monitor this error to troubleshoot usage issues. Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorsharpenresolutionunsupported"></span>
### VeLivePlayerErrorSharpenResolutionUnsupported

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSharpenResolutionUnsupported = -310
```


The resolution exceeds the video sharpening limit.

**During development, you can monitor this error to troubleshoot usage issues. Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorsharpenfpsunsupported"></span>
### VeLivePlayerErrorSharpenFpsUnsupported

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSharpenFpsUnsupported = -312
```


The frame rate exceeds the video sharpening limit.

**During development, you can monitor this error to troubleshoot usage issues. Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorsharpeninitfail"></span>
### VeLivePlayerErrorSharpenInitFail

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSharpenInitFail = -313
```


Failed to initialize video sharpening.

**During development, you can monitor this error to troubleshoot usage issues. Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedh266"></span>
### VeLivePlayerErrorLicenseUnsupportedH266

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedH266 = -314
```


The basic license you are using does not support the H.266 software decoding feature.

**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedabr"></span>
### VeLivePlayerErrorLicenseUnsupportedABR

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedABR = -315
```


The basic license you are using does not support the adaptive bitrate (ABR) streaming feature.

**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorlicenseunsupporteddrm"></span>
### VeLivePlayerErrorLicenseUnsupportedDRM

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedDRM = -316
```


The basic license you are using does not support playing DRM (Digital Rights Management)\-encrypted streams.

**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedsei"></span>
### VeLivePlayerErrorLicenseUnsupportedSEI

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedSEI = -317
```


The basic license you are using does not support the Supplemental Enhancement Information (SEI) message reception feature.

**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedsuperresolution"></span>
### VeLivePlayerErrorLicenseUnsupportedSuperResolution

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedSuperResolution = -318
```


The basic license you are using does not support the super\-resolution feature.

**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedsharpen"></span>
### VeLivePlayerErrorLicenseUnsupportedSharpen

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedSharpen = -319
```


The basic license you are using does not support the video sharpening feature.

**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedquic"></span>
### VeLivePlayerErrorLicenseUnsupportedQUIC

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedQUIC = -320
```


The basic license you are using does not support the QUIC protocol.

**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedcmaf"></span>
### VeLivePlayerErrorLicenseUnsupportedCMAF

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedCMAF = -321
```


The basic license you are using does not support playing CMAF streams.

**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedrtm"></span>
### VeLivePlayerErrorLicenseUnsupportedRTM

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedRTM = -323
```


The basic license you are using does not support playing RTM streams.

**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedmainbackup"></span>
### VeLivePlayerErrorLicenseUnsupportedMainBackup

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedMainBackup = -324
```


The basic license you are using does not support the primary\-backup stream switching feature.

**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorlicenseunsupportedflvlowlatency"></span>
### VeLivePlayerErrorLicenseUnsupportedFLVLowLatency

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedFLVLowLatency = -325
```


The basic license you are using does not support playing low\-latency FLV streams (with a latency of 2 to 3 seconds).

**Please purchase and use the premium license. For more information on how to get the premium license, see** [Getting your SDK license](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **.** 

<span id="VeLivePlayerErrorCode-veliveplayerdrmfetchckcfailed"></span>
### VeLivePlayerDRMFetchCKCFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerDRMFetchCKCFailed = -400
```


DRM authentication failed.

**If this error occurs in a production environment, it is recommended to notify viewers with a prominent alert that the player is unavailable and ask them to restart the player.** 

<span id="VeLivePlayerErrorCode-veliveplayerdrmfetchspcfailed"></span>
### VeLivePlayerDRMFetchSPCFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerDRMFetchSPCFailed = -401
```


Failed to generate the Server Playback Context (SPC).

**If this error occurs in a production environment, it is recommended to notify viewers with a prominent alert that the player is unavailable and ask them to restart the player.** 

<span id="VeLivePlayerErrorCode-veliveplayererrornotsupportresolutionswitch"></span>
### VeLivePlayerErrorNotSupportResolutionSwitch

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorNotSupportResolutionSwitch = -510
```


The player does not support quality level switching.

**During development, you can monitor this error to troubleshoot usage issues. Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.** 

<span id="VeLivePlayerErrorCode-veliveplayererrorinternal"></span>
### VeLivePlayerErrorInternal

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorInternal = -999
```


Internal error.

**Please contact** [BytePlus technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **for details.**
