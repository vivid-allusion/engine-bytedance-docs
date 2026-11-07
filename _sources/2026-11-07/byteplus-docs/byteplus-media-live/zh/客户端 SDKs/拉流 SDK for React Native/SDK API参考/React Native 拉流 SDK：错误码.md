---
title: "React Native 拉流 SDK：错误码"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-error-code-zh-CN"
---

<span id="veliveplayererror"></span>
## VeLivePlayerError

类型：`class`

回放错误。

<span id="d8ff1226"></span>
### errorCode

类型：`number`

`Readonly`，错误码。

<span id="b154dc48"></span>
### errorMsg

类型：`string`

`Readonly`，错误信息。

<span id="9b9c7921"></span>
## VeLivePlayerErrorCode

类型：`enum`

回放错误码。


|属性 |值 |描述 |
|---|---|---|
|VeLivePlayerNoError |`0` |无错误。 |
|VeLivePlayerInvalidLicense |`-1` |SDK 许可证无效。该错误可能由于许可证集成不正确或许可证已过期导致。请检查许可证的集成方式，并确保其仍然有效。 |
|VeLivePlayerInvalidParameter |`-2` |参数无效。请检查输入参数并重新调用方法。 |
|VeLivePlayerErrorRefused |`-3` |方法调用被拒绝。该错误发生在方法调用时机不正确的情况下。 |
|VeLivePlayerErrorLibraryLoadFailed |`-4` |库文件加载失败。该错误可能由于 SDK 集成不正确导致。 |
|VeLivePlayerErrorPlayUrl |`-100` |拉流地址不存在或无效。该错误可能由于拉流地址为空，或地址格式或长度无效导致。 |
|VeLivePlayerErrorNoStreamData |`-101` |无法获取流数据。该错误可能由于直播流不存在、中断或已结束导致。请检查直播流状态。 |
|VeLivePlayerErrorInternalRetryStart |`-102` |播放器因内部错误触发了直播流的内部重试。 |
|VeLivePlayerErrorInternalRetryFailed |`-103` |内部重试失败，且已达到最大重试次数。播放器已停止重试。可尝试手动重试。 |
|VeLivePlayerErrorDnsParseFailed |`-200` |DNS 解析失败。该错误可能由于拉流地址错误或客户端网络状况异常导致。若你已验证拉流地址和网络状况后仍然报错，请联系 BytePlus 技术支持协助。 |
|VeLivePlayerErrorNetworkRequestFailed |`-201` |网络请求失败。请检查网络状况。若错误持续，请联系 BytePlus 技术支持协助。 |
|VeLivePlayerErrorDemuxFailed |`-300` |视频解封装失败。该错误可能由于直播流使用了不支持的格式或协议，或音视频出现错误导致。若错误持续，请联系 BytePlus 技术支持协助。 |
|VeLivePlayerErrorDecodeFailed |`-301` |解码失败。该错误可能由于直播流使用了不支持的音视频格式导致。若错误持续，请联系 BytePlus 技术支持协助。 |
|VeLivePlayerErrorAVOutputFailed |`-302` |渲染失败。该错误可能由于音视频输出设备异常导致。若错误持续，请联系 BytePlus 技术支持协助。 |
|VeLivePlayerErrorSRDeviceUnsupported |`-303` |当前设备型号不支持超分。如需协助，请联系 BytePlus 技术支持。 |
|VeLivePlayerErrorSRResolutionUnsupported |`-304` |当前分辨率超出超分允许的上限。如需协助，请联系 BytePlus 技术支持。 |
|VeLivePlayerErrorSRFpsUnsupported |`-305` |当前帧率超出超分允许的上限。如需协助，请联系 BytePlus 技术支持。 |
|VeLivePlayerErrorSRInitFail |`-306` |超分初始化失败。若错误持续，请联系 BytePlus 技术支持。 |
|VeLivePlayerErrorSRExecuteFail |`-307` |视频应用超分失败。若错误持续，请联系 BytePlus 技术支持。 |
|VeLivePlayerLicenseUnsupportedH265 |`-308` |当前 SDK 许可证不支持 H.265 功能。 |
|VeLivePlayerDRMFetchCKCFailed |`-400` |DRM 认证失败。 |
|VeLivePlayerDRMFetchSPCFailed |`-401` |无法生成服务器回放上下文（SPC）。 |
|VeLivePlayerErrorInternal |`-999` |内部错误。请联系 BytePlus 技术支持以获取帮助。 |
