---
title: "iOS 播放器 SDK：错误码"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api-error-code-zh-CN"
---

# VeLivePlayerError

```objectivec
@interface VeLivePlayerError : NSError
```

播放器 SDK 错误。

## 成员属性

|类型 |名称 |
|---|---|
|NSInteger |[errorCode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError-errorcode) |
|NSInteger |[subErrorCode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError-suberrorcode) |
|NSString\* |[errorMsg](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError-errormsg) |

## 说明

### errorCode

```objectivec
@property (nonatomic, readonly) NSInteger errorCode;
```

播放器 SDK 错误码。

### subErrorCode

```objectivec
@property (nonatomic, readonly) NSInteger subErrorCode;
```

播放器 SDK 子错误码。

### errorMsg

```objectivec
@property (nonatomic, readonly, nullable) NSString* errorMsg;
```

播放器 SDK 错误消息。

# VeLivePlayerErrorCode

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerErrorCode
)
```

播放器 SDK 错误码。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerNoError |0 |无错误。 |
|VeLivePlayerInvalidLicense |\-1 |许可证无效。原因可能是许可证集成错误，或许可证已过期。<br><br>**请检查许可证集成和有效期。如问题仍然存在，请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**  |
|VeLivePlayerInvalidParameter |\-2 |参数无效。<br><br>**请检查后重试。**  |
|VeLivePlayerErrorRefused |\-3 |由于调用时机不正确，调用被拒绝。<br><br>**请检查调用时机后重试。建议在开发阶段处理此错误。**  |
|VeLivePlayerErrorLibraryLoadFailed |\-4 |加载库文件失败。原因可能是 SDK 集成错误。<br><br>**请检查 SDK 集成后重试。建议在开发阶段处理此错误。**  |
|VeLivePlayerErrorPlayUrl |\-100 |拉流地址不存在或无效。原因可能是拉流地址为空、格式无效，或超过长度限制。<br><br>**开发期间，你可以监控此错误以排查使用问题。如果此错误发生在生产环境中，建议通过醒目提示告知观众播放器不可用，并要求他们重启播放器。**  |
|VeLivePlayerErrorNoStreamData |\-101 |流数据不存在或网络请求失败。原因可能是直播流不存在、被中断，或已结束。<br><br>**建议替换拉流地址、切换到低码率流，或提示观众网络问题。**  |
|VeLivePlayerErrorInternalRetryStart |\-102 |播放器内部重试。原因可能是播放器内部错误。<br><br>**建议替换拉流地址、切换到低码率流，或提示观众网络问题。**  |
|VeLivePlayerErrorInternalRetryFailed |\-103 |播放器内部重试失败。播放器在达到最大重试次数后已停止重试。<br><br>**建议替换拉流地址、切换到低码率流，或提示观众网络问题。**  |
|VeLivePlayerErrorDnsParseFailed |\-200 |DNS 解析失败。原因可能是拉流地址异常，或客户端网络状况异常。<br><br>**建议替换拉流地址、切换到低码率流，或提示观众网络问题。**  |
|VeLivePlayerErrorNetworkRequestFailed |\-201 |网络请求失败。<br><br>**建议替换拉流地址、切换到低码率流，或提示观众网络问题。**  |
|VeLivePlayerErrorDemuxFailed |\-300 |解复用失败。原因可能是不支持的流格式或协议，或音视频流错误。<br><br>**建议替换拉流地址、切换到低码率流，或提示观众网络问题。**  |
|VeLivePlayerErrorDecodeFailed |\-301 |视频解码失败。原因可能是不支持的直播流音视频格式，或解码器错误。<br><br>**建议替换拉流地址、切换到低码率流，或提示观众网络问题。如问题仍然存在，请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**  |
|VeLivePlayerErrorAVOutputFailed |\-302 |渲染失败。原因可能是音频或视频输出设备异常。<br><br>**如果此错误发生在生产环境中，建议通过醒目提示告知观众播放器不可用，并要求他们重启播放器。**  |
|VeLivePlayerErrorSRDeviceUnsupported |\-303 |当前设备不在超分辨率模型白名单中，不支持超分辨率功能。<br><br>**开发期间，你可以监控此错误以排查使用问题。请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**  |
|VeLivePlayerErrorSRResolutionUnsupported |\-304 |分辨率超过超分辨率限制。<br><br>**开发期间，你可以监控此错误以排查使用问题。请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**  |
|VeLivePlayerErrorSRFpsUnsupported |\-305 |帧率超过超分辨率限制。<br><br>**开发期间，你可以监控此错误以排查使用问题。请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**  |
|VeLivePlayerErrorSRInitFail |\-306 |初始化超分辨率失败。<br><br>**开发期间，你可以监控此错误以排查使用问题。请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**  |
|VeLivePlayerErrorSRExecuteFail |\-307 |执行超分辨率失败。<br><br>**开发期间，你可以监控此错误以排查使用问题。请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**  |
|VeLivePlayerLicenseUnsupportedH265 |\-308 |你正在使用的基础许可证不支持 H.265 硬件和软件解码功能。<br><br>**请购买并使用高级许可证。有关如何获取高级许可证的更多信息，请参见** [获取 SDK 许可证](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**  |
|VeLivePlayerErrorSharpenDeviceUnsupported |\-309 |设备不支持视频锐化功能。<br><br>**开发期间，你可以监控此错误以排查使用问题。请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**  |
|VeLivePlayerErrorSharpenResolutionUnsupported |\-310 |分辨率超过视频锐化限制。<br><br>**开发期间，你可以监控此错误以排查使用问题。请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**  |
|VeLivePlayerErrorSharpenFpsUnsupported |\-312 |帧率超过视频锐化限制。<br><br>**开发期间，你可以监控此错误以排查使用问题。请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**  |
|VeLivePlayerErrorSharpenInitFail |\-313 |初始化视频锐化失败。<br><br>**开发期间，你可以监控此错误以排查使用问题。请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**  |
|VeLivePlayerErrorLicenseUnsupportedABR |\-315 |你正在使用的基础许可证不支持自适应码率（ABR）流功能。<br><br>**请购买并使用高级许可证。有关如何获取高级许可证的更多信息，请参见** [获取 SDK 许可证](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**  |
|VeLivePlayerErrorLicenseUnsupportedDRM |\-316 |你正在使用的基础许可证不支持播放 DRM（数字版权管理）加密流。<br><br>**请购买并使用高级许可证。有关如何获取高级许可证的更多信息，请参见** [获取 SDK 许可证](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**  |
|VeLivePlayerErrorLicenseUnsupportedSEI |\-317 |你正在使用的基础许可证不支持补充增强信息（SEI）消息接收功能。<br><br>**请购买并使用高级许可证。有关如何获取高级许可证的更多信息，请参见** [获取 SDK 许可证](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**  |
|VeLivePlayerErrorLicenseUnsupportedSuperResolution |\-318 |你正在使用的基础许可证不支持超分辨率功能。<br><br>**请购买并使用高级许可证。有关如何获取高级许可证的更多信息，请参见** [获取 SDK 许可证](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**  |
|VeLivePlayerErrorLicenseUnsupportedSharpen |\-319 |你正在使用的基础许可证不支持视频锐化功能。<br><br>**请购买并使用高级许可证。有关如何获取高级许可证的更多信息，请参见** [获取 SDK 许可证](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**  |
|VeLivePlayerErrorLicenseUnsupportedQUIC |\-320 |你正在使用的基础许可证不支持 QUIC 协议。<br><br>**请购买并使用高级许可证。有关如何获取高级许可证的更多信息，请参见** [获取 SDK 许可证](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**  |
|VeLivePlayerErrorLicenseUnsupportedRTM |\-323 |你正在使用的基础许可证不支持播放 RTM 流。<br><br>**请购买并使用高级许可证。有关如何获取高级许可证的更多信息，请参见** [获取 SDK 许可证](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**  |
|VeLivePlayerErrorLicenseUnsupportedMainBackup |\-324 |你正在使用的基础许可证不支持主备流切换功能。<br><br>**请购买并使用高级许可证。有关如何获取高级许可证的更多信息，请参见** [获取 SDK 许可证](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**  |
|VeLivePlayerErrorLicenseUnsupportedFLVLowLatency |\-325 |你正在使用的基础许可证不支持播放低延迟 FLV 流（延迟为 2 到 3 秒）。<br><br>**请购买并使用高级许可证。有关如何获取高级许可证的更多信息，请参见** [获取 SDK 许可证](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management?lang=en) **。**  |
|VeLivePlayerDRMFetchCKCFailed |\-400 |DRM 身份验证失败。<br><br>**如果此错误发生在生产环境中，建议通过醒目提示告知观众播放器不可用，并要求他们重启播放器。**  |
|VeLivePlayerDRMFetchSPCFailed |\-401 |生成服务器播放上下文（SPC）失败。<br><br>**如果此错误发生在生产环境中，建议通过醒目提示告知观众播放器不可用，并要求他们重启播放器。**  |
|VeLivePlayerErrorNotSupportResolutionSwitch |\-510 |播放器不支持清晰度档位切换。<br><br>**开发期间，你可以监控此错误以排查使用问题。请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**  |
|VeLivePlayerErrorInternal |\-999 |内部错误。<br><br>**请联系** [BytePlus 技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) **了解详情。**  |
