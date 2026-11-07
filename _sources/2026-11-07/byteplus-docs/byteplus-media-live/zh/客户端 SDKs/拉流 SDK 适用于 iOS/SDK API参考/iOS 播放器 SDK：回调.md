---
title: "iOS 播放器 SDK：回调"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback-zh-CN"
---

# VeLivePlayerObserver

```objectivec
@protocol VeLivePlayerObserver <NSObject>
```

直播播放器观察者。

## 成员函数

|返回值 |名称 |
|---|---|
|void |[onError:error:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onerror-error) |
|void |[onInfo:info:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-oninfo-info) |
|void |[onFirstVideoFrameRender:isFirstFrame:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onfirstvideoframerender-isfirstframe) |
|void |[onFirstAudioFrameRender:isFirstFrame:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onfirstaudioframerender-isfirstframe) |
|void |[onStallStart:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstallstart) |
|void |[onStallEnd:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstallend) |
|void |[onVideoRenderStall:stallTime:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onvideorenderstall-stalltime) |
|void |[onAudioRenderStall:stallTime:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onaudiorenderstall-stalltime) |
|void |[onResolutionSwitch:resolution:error:reason:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onresolutionswitch-resolution-error-reason) |
|void |[onVideoSizeChanged:width:height:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onvideosizechanged-width-height) |
|void |[onReceiveSeiMessage:message:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onreceiveseimessage-message) |
|void |[onReceiveBinarySeiMessage:message:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onreceivebinaryseimessage-message) |
|void |[onMainBackupSwitch:streamType:error:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onmainbackupswitch-streamtype-error) |
|void |[onStreamFormatSwitch:fromStreamFormat:toStreamFormat:error:extraInfo:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstreamformatswitch-fromstreamformat-tostreamformat-error-extrainfo) |
|void |[onPlayerStatusUpdate:status:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status) |
|void |[onPlayerStatusUpdate:status:extraInfo:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status-extrainfo) |
|void |[onStatistics:statistics:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstatistics-statistics) |
|void |[onSnapshotComplete:image:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onsnapshotcomplete-image) |
|void |[onRenderVideoFrame:videoFrame:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onrendervideoframe-videoframe) |
|void |[onRenderAudioFrame:audioFrame:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onrenderaudioframe-audioframe) |
|void |[onStreamFailedOpenSuperResolution:error:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution-error) |
|nullable NSData\* |[getDrmResourceLoaderCertificateData:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-getdrmresourceloadercertificatedata) |
|nullable NSString\* |[getDrmResourceLoaderLicenseUrl:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-getdrmresourceloaderlicenseurl) |

## 说明

### onError:error:

```objectivec
- (void)onError:(TVLManager *_Nonnull)player error:(VeLivePlayerError *_Nonnull)error;
```

播放器发生错误时触发。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |触发回调函数的播放器对象。 |
|error |VeLivePlayerError\* |错误消息。详情请参见 [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError)。 |

### onInfo:info:

```objectivec
- (void)onInfo:(TVLManager *_Nonnull)player info:(VeLivePlayerError *_Nonnull)info;
```

播放器遇到内部错误时触发。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |触发回调的播放器对象。详情请参见 [TVLManager](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer))。 |
|info |VeLivePlayerError\* |播放器信息。详情请参见 [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError)。 |

### onFirstVideoFrameRender:isFirstFrame:

```objectivec
- (void)onFirstVideoFrameRender:(TVLManager *_Nonnull)player isFirstFrame:(BOOL)isFirstFrame;
```

播放开始时或播放期间重试后渲染首个视频帧时触发。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |触发回调函数的播放器对象。 |
|isFirstFrame |BOOL |视频帧是否为播放开始时渲染的首个视频帧。<br><br><br>* `YES`：该视频帧是播放开始时渲染的首个视频帧；<br><br>* `NO`：该视频帧是播放期间重试后渲染的首个视频帧。 |

### onFirstAudioFrameRender:isFirstFrame:

```objectivec
- (void)onFirstAudioFrameRender:(TVLManager *_Nonnull)player isFirstFrame:(BOOL)isFirstFrame;
```

播放开始时或播放期间重试后渲染首个音频帧时触发。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |触发回调函数的播放器对象。 |
|isFirstFrame |BOOL |音频帧是否为播放开始时渲染的首个音频帧。<br><br><br>* `YES`：该音频帧是播放开始时渲染的首个音频帧；<br><br>* `NO`：该音频帧是播放期间重试后渲染的首个音频帧。 |

### onStallStart:

```objectivec
- (void)onStallStart:(TVLManager *_Nonnull)player;
```

播放卡顿开始时触发。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |触发回调函数的播放器对象。 |

### onStallEnd:

```objectivec
- (void)onStallEnd:(TVLManager *_Nonnull)player;
```

播放卡顿停止时触发，即音频缓冲充足后恢复播放时触发。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |触发回调函数的播放器对象。 |

### onVideoRenderStall:stallTime:

```objectivec
- (void)onVideoRenderStall:(TVLManager *_Nonnull)player stallTime:(int64_t)stallTime;
```

视频渲染卡顿时触发。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |触发回调函数的播放器对象。 |
|stallTime |int64_t |卡顿时长，单位为毫秒。 |

### onAudioRenderStall:stallTime:

```objectivec
- (void)onAudioRenderStall:(TVLManager *_Nonnull)player stallTime:(int64_t)stallTime;
```

音频渲染卡顿时触发。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |触发回调函数的播放器对象。 |
|stallTime |int64_t |卡顿时长，单位为毫秒。 |

### onResolutionSwitch:resolution:error:reason:

```objectivec
- (void)onResolutionSwitch:(TVLManager *_Nonnull)player resolution:(VeLivePlayerResolution)resolution error:(VeLivePlayerError *)error reason:(VeLivePlayerResolutionSwitchReason)reason;
```

视频分辨率变化时触发。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |触发回调函数的播放器对象。 |
|resolution |VeLivePlayerResolution |更新后的分辨率。详情请参见 [VeLivePlayerResolution](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerResolution)。 |
|error |VeLivePlayerError\* |切换分辨率时是否发生错误。详情请参见 [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError)。 |
|reason |VeLivePlayerResolutionSwitchReason |切换分辨率的原因。详情请参见 [VeLivePlayerResolutionSwitchReason](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerResolutionSwitchReason)。 |

### onVideoSizeChanged:width:height:

```objectivec
- (void)onVideoSizeChanged:(TVLManager *_Nonnull)player width:(int)width height:(int)height;
```

视频尺寸变化时触发。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |触发回调函数的播放器对象。 |
|width |int |更新后的视频宽度，单位为像素。 |
|height |int |更新后的视频高度，单位为像素。 |

### onReceiveSeiMessage:message:

```objectivec
- (void)onReceiveSeiMessage:(TVLManager *_Nonnull)player message:(NSString *_Nonnull)message;
```

字符串 SEI 消息回调。播放器 SDK 收到 SEI 消息时触发该回调。需要在 `VeLivePlayerConfiguration` 中启用 `enableSei` 属性。启用 `enableBinarySei` 属性后，将不再发送字符串 SEI 消息。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |触发回调函数的播放器对象。 |
|message |NSString\* |SEI 消息。 |

### onReceiveBinarySeiMessage:message:

```objectivec
- (void)onReceiveBinarySeiMessage:(TVLManager *_Nonnull)player message:(NSData *_Nonnull)message;
```

二进制 SEI 消息回调。播放器 SDK 收到 SEI 消息时触发该回调。需要在 `VeLivePlayerConfiguration` 中启用 `enableBinarySei` 属性。启用 `enableBinarySei` 属性后，将不再发送字符串 SEI 消息。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |触发回调函数的播放器对象。 |
|message |NSData\* |SEI 消息。 |

### onMainBackupSwitch:streamType:error:

```objectivec
- (void)onMainBackupSwitch:(TVLManager *_Nonnull)player streamType:(VeLivePlayerStreamType)streamType error:(VeLivePlayerError *)error;
```

播放器在主流和备流之间切换时触发。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |触发回调函数的播放器对象。 |
|streamType |VeLivePlayerStreamType |更新后的流类型。详情请参见 [VeLivePlayerStreamType](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamType)。 |
|error |VeLivePlayerError\* |切换原因。详情请参见 [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError)。 |

### onStreamFormatSwitch:fromStreamFormat:toStreamFormat:error:extraInfo:

```objectivec
- (void)onStreamFormatSwitch:(TVLManager *_Nonnull)player fromStreamFormat:(VeLivePlayerFormat)fromStreamType toStreamFormat:(VeLivePlayerFormat)toStreamType error:(VeLivePlayerError *)error extraInfo:(nullable NSDictionary *)extraInfo;
```

播放器切换流格式时触发。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |触发回调的播放器对象。详情请参见 [TVLManager](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer))。 |
|fromStreamType |VeLivePlayerFormat |切换前的流格式。详情请参见 [VeLivePlayerFormat](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerFormat)。 |
|toStreamType |VeLivePlayerFormat |切换后的流格式。详情请参见 [VeLivePlayerFormat](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerFormat)。 |
|error |VeLivePlayerError\* |流格式切换的原因。详情请参见 [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError)。 |
|extraInfo |nullable NSDictionary\* |附加信息，包含与切换相关的详细数据。 |

### onPlayerStatusUpdate:status:

```objectivec
- (void)onPlayerStatusUpdate:(TVLManager *_Nonnull)player status:(VeLivePlayerStatus)status;
```

播放状态变化时触发。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |播放状态发生变化的播放器。 |
|status |VeLivePlayerStatus |播放器更新后的状态。详情请参见 [VeLivePlayerStatus](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatus)。 |

### onPlayerStatusUpdate:status:extraInfo:

```objectivec
- (void)onPlayerStatusUpdate:(TVLManager *_Nonnull)player status:(VeLivePlayerStatus)status extraInfo:(nullable NSDictionary *)extraInfo;
```

播放状态变化时触发。与 [onPlayerStatusUpdate:status:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status) 相比，该回调通过 `extraInfo` 返回当前播放流的补充信息。

**输入参数**

|参数名称 |类型 |描述 |
|---|---|---|
|player |TVLManager\* |播放状态发生变化的播放器。 |
|status |VeLivePlayerStatus |播放器更新后的状态。详情请参见 [VeLivePlayerStatus](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatus)。 |
|extraInfo |nullable NSDictionary\* |当前播放流补充信息的字典。该字典可能包含以下键：<br><br><br>* `url` (NSString)：当前正在播放的流 URL。<br><br>* `all_resolution_urls` (NSDictionary<NSString \*, NSString \*\>)：所有分辨率的播放地址映射。`Key` 为分辨率标识，`Value` 为对应的播放 URL。仅当当前流为多分辨率流时，才存在该键。<br><br>* `resolution` (NSString)：当前播放流的分辨率标识。仅当当前流为多分辨率流时，才存在该键。<br><br>* `enable_abr` (NSNumber)：是否启用自适应码率（Adaptive Bitrate，ABR）。仅当当前流为多分辨率流时，才存在该键。有效值：<br><br>   * `YES`：已启用。<br><br>   * `NO`：已禁用。<br><br>* `enable_smooth_switch_resolution` (NSNumber)：是否启用平滑分辨率切换。仅当当前流为多分辨率流时，才存在该键。有效值：<br><br>   * `YES`：已启用。<br><br>   * `NO`：已禁用。<br><br>* `max_retry_count` (NSNumber, NSInteger)：当前流的最大重试次数。<br><br>* `retry_interval_time_ms` (NSNumber, NSInteger)：当前流的重试间隔，单位为毫秒。<br><br>* `priority` (NSNumber, NSInteger)：当前流在拉流列表中的优先级。 |

### onStatistics:statistics:

```objectivec
- (void)onStatistics:(TVLManager *_Nonnull)player statistics:(VeLivePlayerStatistics *_Nonnull)statistics;
```

定期触发，用于上报当前拉流地址、码率和帧率等信息。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |触发回调函数的播放器对象。 |
|statistics |VeLivePlayerStatistics\* |播放统计信息。详情请参见 [VeLivePlayerStatistics](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics)。 |

### onSnapshotComplete:image:

```objectivec
- (void)onSnapshotComplete:(TVLManager *_Nonnull)player image:(UIImage *_Nonnull)image;
```

调用 snapshot 后完成截图时触发。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |触发回调函数的播放器对象。 |
|image |UIImage\* |截图的 UIImage 对象。 |

### onRenderVideoFrame:videoFrame:

```objectivec
- (void)onRenderVideoFrame:(TVLManager *_Nonnull)player videoFrame:(VeLivePlayerVideoFrame *_Nonnull)videoFrame;
```

播放器解码视频帧时触发。调用 [enableVideoFrameObserver:pixelFormat:bufferType:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enablevideoframeobserver-pixelformat-buffertype) 可启用视频帧回调。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |触发回调函数的播放器对象。 |
|videoFrame |VeLivePlayerVideoFrame\* |视频帧，包含像素格式、封装格式、视频宽高等信息。详情请参见 [VeLivePlayerVideoFrame](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame)。 |

**注意事项**

如果使用纹理格式进行外部渲染，建议在回调线程中渲染视频。

### onRenderAudioFrame:audioFrame:

```objectivec
- (void)onRenderAudioFrame:(TVLManager *_Nonnull)player audioFrame:(VeLivePlayerAudioFrame *_Nonnull)audioFrame;
```

播放器解码音频帧时触发。调用 [enableAudioFrameObserver:enableRendering:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enableaudioframeobserver-enablerendering) 可启用音频帧回调。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |触发回调函数的播放器对象。 |
|audioFrame |VeLivePlayerAudioFrame\* |音频帧。详情请参见 [VeLivePlayerAudioFrame](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame)。 |

**注意事项**

回调返回的音频数据类型为 Float32，字节序为大端序。

### onStreamFailedOpenSuperResolution:error:

```objectivec
- (void)onStreamFailedOpenSuperResolution:(TVLManager *_Nonnull)player error:(VeLivePlayerError *_Nullable)error;
```

调用 [setEnableSuperResolution:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setenablesuperresolution) 后，SDK 启用超分失败时触发。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |触发回调函数的播放器对象。 |
|error |VeLivePlayerError\* |失败原因。详情请参见 [VeLivePlayerErrorCode](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api-error-code#VeLivePlayerErrorCode)。 |

### getDrmResourceLoaderCertificateData:

```objectivec
- (nullable NSData *)getDrmResourceLoaderCertificateData:(nonnull TVLManager *_Nonnull)player;
```

需要在此回调中返回 NSData 格式的 FairPlay 证书。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |触发回调的播放器实例。 |

### getDrmResourceLoaderLicenseUrl:

```objectivec
- (nullable NSString *)getDrmResourceLoaderLicenseUrl:(nonnull TVLManager *_Nonnull)player;
```

需要在此回调中返回 DRM 许可证的 URL。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |TVLManager\* |触发回调的播放器实例。 |
