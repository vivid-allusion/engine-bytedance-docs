---
title: "Android 版 Player SDK：错误码"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-errorcode-zh-CN"
---

# VeLivePlayerError

```java
public class com.ss.videoarch.liveplayer.VeLivePlayerError
```

Player SDK 错误。

## 成员属性

|类型 |默认值 |名称 |
|---|---|---|
|int |`-` |[mErrorCode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerError-merrorcode) |
|String |`-` |[mErrorMsg](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerError-merrormsg) |
|int |\-1 |[mSubCode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerError-msubcode) |

## 成员函数

|返回值 |名称 |
|---|---|
|VeLivePlayerError |[VeLivePlayerError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-errorcode#VeLivePlayerError-veliveplayererror-4) |

## 说明

### mErrorCode

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerError.mErrorCode
```

Player SDK 错误码。

### mErrorMsg

```java
public String com.ss.videoarch.liveplayer.VeLivePlayerError.mErrorMsg
```

Player SDK 错误消息。

### mSubCode

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerError.mSubCode = -1
```

Player SDK 子错误码。

## 说明

### VeLivePlayerError

```java
public com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerError(
    int errorCode,
    int subCode,
    String errorMsg
)
```

创建包含错误码、子错误码和错误消息的 `VeLivePlayerError` 实例。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|errorCode |int |错误码。 |
|subCode |int |子错误码。 |
|errorMsg |String |错误消息。 |

**返回值**

`VeLivePlayerError` 实例。

# VeLivePlayerErrorCode

```java
public static class com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode
```

Player SDK 错误码。

## 成员属性

|类型 |默认值 |名称 |
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

## 说明

### VeLivePlayerNoError

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerNoError = 0
```

无错误。

### VeLivePlayerInvalidLicense

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerInvalidLicense = -1
```

License 无效。可能是 License 集成错误或 License 已过期。

**请检查 License 集成和有效期。如果问题仍然存在，请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**

### VeLivePlayerInvalidParameter

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerInvalidParameter = -2
```

参数无效。

**请检查并重试。**

### VeLivePlayerErrorRefused

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorRefused = -3
```

调用时机不正确，调用被拒绝。

**请检查调用时机并重试。建议在开发阶段处理此错误。**

### VeLivePlayerErrorLibraryLoadFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLibraryLoadFailed = -4
```

加载库文件失败。可能是 SDK 集成错误。

**请检查 SDK 集成并重试。建议在开发阶段处理此错误。**

### VeLivePlayerErrorPlayUrl

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorPlayUrl = -100
```

拉流地址不存在或无效。可能是拉流地址为空、格式无效或超出长度限制。

**开发期间，你可以监控此错误以排查使用问题。如果此错误发生在生产环境，建议通过醒目提示通知观众播放器不可用，并要求观众重启播放器。**

### VeLivePlayerErrorNoStreamData

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorNoStreamData = -101
```

流数据不存在或网络请求失败。可能是直播流不存在、中断或已结束。

**建议更换拉流地址、切换到低码率流，或提示观众网络问题。**

### VeLivePlayerErrorInternalRetryStart

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorInternalRetryStart = -102
```

播放器内部重试。可能是播放器内部错误导致。

**建议更换拉流地址、切换到低码率流，或提示观众网络问题。**

### VeLivePlayerErrorInternalRetryFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorInternalRetryFailed = -103
```

播放器内部重试失败。播放器达到最大重试次数后已停止重试。

**建议更换拉流地址、切换到低码率流，或提示观众网络问题。**

### VeLivePlayerErrorDnsParseFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorDnsParseFailed = -200
```

DNS 解析失败。可能是拉流地址异常或客户端网络状况异常。

**建议更换拉流地址、切换到低码率流，或提示观众网络问题。**

### VeLivePlayerErrorNetworkRequestFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorNetworkRequestFailed = -201
```

网络请求失败。

**建议更换拉流地址、切换到低码率流，或提示观众网络问题。**

### VeLivePlayerErrorDemuxFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorDemuxFailed = -300
```

解复用失败。可能是流格式或协议不受支持，或音视频流错误。

**建议更换拉流地址、切换到低码率流，或提示观众网络问题。**

### VeLivePlayerErrorDecodeFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorDecodeFailed = -301
```

视频解码失败。可能是直播流音视频格式不受支持或解码器错误。

**建议更换拉流地址、切换到低码率流，或提示观众网络问题。如果问题仍然存在，请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**

### VeLivePlayerErrorAVOutputFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorAVOutputFailed = -302
```

渲染失败。可能是音频或视频输出设备异常。

**如果此错误发生在生产环境，建议通过醒目提示通知观众播放器不可用，并要求观众重启播放器。**

### VeLivePlayerErrorSRDeviceUnsupported

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSRDeviceUnsupported = -303
```

当前设备不在超分机型白名单中，不支持超分功能。

**开发期间，你可以监控此错误以排查使用问题。请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**

### VeLivePlayerErrorSRResolutionUnsupported

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSRResolutionUnsupported = -304
```

分辨率超出超分限制。

**开发期间，你可以监控此错误以排查使用问题。请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**

### VeLivePlayerErrorSRFpsUnsupported

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSRFpsUnsupported = -305
```

帧率超出超分限制。

**开发期间，你可以监控此错误以排查使用问题。请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**

### VeLivePlayerErrorSRInitFail

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSRInitFail = -306
```

初始化超分失败。

**开发期间，你可以监控此错误以排查使用问题。请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**

### VeLivePlayerErrorSRExecuteFail

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSRExecuteFail = -307
```

执行超分失败。

**开发期间，你可以监控此错误以排查使用问题。请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**

### VeLivePlayerLicenseUnsupportedH265

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerLicenseUnsupportedH265 = -308
```

你使用的基础 License 不支持 H.265 硬解和软解功能。

**请购买并使用高级 License。有关如何获取高级 License 的更多信息，请参见** [获取 SDK License](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorSharpenDeviceUnsupported

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSharpenDeviceUnsupported = -309
```

设备不支持视频锐化功能。

**开发期间，你可以监控此错误以排查使用问题。请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**

### VeLivePlayerErrorSharpenResolutionUnsupported

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSharpenResolutionUnsupported = -310
```

分辨率超出视频锐化限制。

**开发期间，你可以监控此错误以排查使用问题。请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**

### VeLivePlayerErrorSharpenFpsUnsupported

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSharpenFpsUnsupported = -312
```

帧率超出视频锐化限制。

**开发期间，你可以监控此错误以排查使用问题。请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**

### VeLivePlayerErrorSharpenInitFail

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorSharpenInitFail = -313
```

初始化视频锐化失败。

**开发期间，你可以监控此错误以排查使用问题。请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**

### VeLivePlayerErrorLicenseUnsupportedH266

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedH266 = -314
```

你使用的基础 License 不支持 H.266 软解功能。

**请购买并使用高级 License。有关如何获取高级 License 的更多信息，请参见** [获取 SDK License](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorLicenseUnsupportedABR

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedABR = -315
```

你使用的基础 License 不支持自适应码率（ABR）流功能。

**请购买并使用高级 License。有关如何获取高级 License 的更多信息，请参见** [获取 SDK License](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorLicenseUnsupportedDRM

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedDRM = -316
```

你使用的基础 License 不支持播放 DRM（Digital Rights Management）加密流。

**请购买并使用高级 License。有关如何获取高级 License 的更多信息，请参见** [获取 SDK License](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorLicenseUnsupportedSEI

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedSEI = -317
```

你使用的基础 License 不支持补充增强信息（SEI）消息接收功能。

**请购买并使用高级 License。有关如何获取高级 License 的更多信息，请参见** [获取 SDK License](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorLicenseUnsupportedSuperResolution

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedSuperResolution = -318
```

你使用的基础 License 不支持超分功能。

**请购买并使用高级 License。有关如何获取高级 License 的更多信息，请参见** [获取 SDK License](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorLicenseUnsupportedSharpen

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedSharpen = -319
```

你使用的基础 License 不支持视频锐化功能。

**请购买并使用高级 License。有关如何获取高级 License 的更多信息，请参见** [获取 SDK License](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorLicenseUnsupportedQUIC

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedQUIC = -320
```

你使用的基础 License 不支持 QUIC 协议。

**请购买并使用高级 License。有关如何获取高级 License 的更多信息，请参见** [获取 SDK License](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorLicenseUnsupportedCMAF

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedCMAF = -321
```

你使用的基础 License 不支持播放 CMAF 流。

**请购买并使用高级 License。有关如何获取高级 License 的更多信息，请参见** [获取 SDK License](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorLicenseUnsupportedRTM

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedRTM = -323
```

你使用的基础 License 不支持播放 RTM 流。

**请购买并使用高级 License。有关如何获取高级 License 的更多信息，请参见** [获取 SDK License](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorLicenseUnsupportedMainBackup

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedMainBackup = -324
```

你使用的基础 License 不支持主备流切换功能。

**请购买并使用高级 License。有关如何获取高级 License 的更多信息，请参见** [获取 SDK License](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerErrorLicenseUnsupportedFLVLowLatency

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorLicenseUnsupportedFLVLowLatency = -325
```

你使用的基础 License 不支持播放低延迟 FLV 流（延迟为 2 到 3 秒）。

**请购买并使用高级 License。有关如何获取高级 License 的更多信息，请参见** [获取 SDK License](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**

### VeLivePlayerDRMFetchCKCFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerDRMFetchCKCFailed = -400
```

DRM 鉴权失败。

**如果此错误发生在生产环境，建议通过醒目提示通知观众播放器不可用，并要求观众重启播放器。**

### VeLivePlayerDRMFetchSPCFailed

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerDRMFetchSPCFailed = -401
```

生成 Server Playback Context（SPC）失败。

**如果此错误发生在生产环境，建议通过醒目提示通知观众播放器不可用，并要求观众重启播放器。**

### VeLivePlayerErrorNotSupportResolutionSwitch

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorNotSupportResolutionSwitch = -510
```

播放器不支持清晰度档位切换。

**开发期间，你可以监控此错误以排查使用问题。请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**

### VeLivePlayerErrorInternal

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerErrorCode.VeLivePlayerErrorInternal = -999
```

内部错误。

**请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**
