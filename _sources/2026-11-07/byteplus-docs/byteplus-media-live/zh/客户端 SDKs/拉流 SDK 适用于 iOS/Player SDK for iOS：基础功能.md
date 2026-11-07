---
title: "Player SDK for iOS：基础功能"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-basic-features-3-zh-CN"
---

本文介绍如何实现 Player SDK for iOS 的基础功能。

## 前提条件

你已按照 [集成 Player SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios) 和 [初始化 Player SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-ios) 中提供的说明，完成 Player SDK 的集成和初始化。

## 注意事项

Player SDK 使用多种 iOS 音视频 API，这些 API 在模拟器上可能无法正常工作。建议使用真机进行调试。

## 创建播放器

Player SDK for iOS 中的播放器类是 `TVLManager`。以下示例代码创建了一个播放器。

```objectivec
TVLManager *livePlayer = [[TVLManager alloc] init];
```

> **说明**

* > 请根据播放器类型选择初始化方法：

   * > `VeLivePlayerTypeOwn`：SDK 内置播放器。调用 [init](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#init) 会创建此类型的播放器。你也可以调用 [initWithType:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#initwithtype) 并传入 `VeLivePlayerTypeOwn`。只有此类型支持 [画中画](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#picture-in-picture)。

   * > `VeLivePlayerTypeSystem`：系统播放器。如需创建此类型的播放器，请调用 [initWithType:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#initwithtype) 并传入 `VeLivePlayerTypeSystem`。使用此类型播放 DRM 加密流。更多信息，请参见 [播放 DRM 加密流](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-3#playing-a-drm-encrypted-stream)。此类型仅支持 M3U8 拉流地址，且不支持以下功能：

      * > 主备流切换

      * > 自适应码率（ABR）拉流

      * > 截图

      * > 视频镜像

      * > 自定义音视频渲染

      * > 超分辨率

      * > 补充增强信息（SEI）

* > 为确保最佳播放效果，建议为每次播放会话创建新的播放器实例，而不是复用现有实例。

## 配置播放器

使用 [VeLivePlayerConfiguration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayerconfiguration) 配置播放器的初始设置，并调用 [setConfig:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setconfig) 应用配置。请在调用 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play) 前完成配置。下表说明了 `VeLivePlayerConfiguration` 中的参数。

|参数 |类型 |描述 |
|---|---|---|
|enableSei |BOOL |是否启用字符串 SEI 消息解析。默认值为 `NO`。 |
|enableBinarySei |BOOL |是否启用二进制 SEI 消息解析。默认值为 `NO`。启用后，播放器会接收二进制 SEI 消息，不再触发字符串 SEI 消息回调。 |
|enableHardwareDecode |BOOL |是否启用硬件解码。默认值为 `YES`。启用后，如果硬件解码启动失败或在播放期间失败，播放器会自动切换到软件解码。 |
|networkTimeoutMs |NSInteger |网络超时时长，单位为毫秒。默认值为 `5000`。发送网络请求后，如果在此时间内未收到服务器响应，播放器会认为请求失败。 |
|retryIntervalTimeMs |NSInteger |重试间隔，单位为毫秒。默认值为 `5000`。如果网络错误或类似问题中断直播播放，播放器会按此间隔重试播放。 |
|retryMaxCount |NSInteger |网络连接错误后的最大重试次数。默认值为 `5`。值为 `0` 时会禁用播放器内部重试。 |
|stallRetryTimeout |NSInteger |因卡顿而停止重试的超时阈值，单位为毫秒。默认值为 `10000`（10 秒）。当卡顿时长超过此阈值时，播放器会停止重试。 |
|enableLiveDNS |BOOL |是否启用本地 DNS 预取。默认值为 `YES`。启用本地 DNS 预取可减少起播所需时间。<br><br>> **警告**<br><br><br>> 本地 DNS 预取期间出现错误可能会影响播放器正常运行。<br> |
|enableStatisticsCallback |BOOL |是否启用播放信息的周期性回调。默认值为 `NO`。 |
|statisticsCallbackInterval |NSInteger |提供播放信息的周期性回调时间间隔，单位为秒。默认值为 `5`。 |

以下示例代码展示如何配置播放器的初始设置。

```objectivec
// 创建 VeLivePlayerConfiguration 实例。
VeLivePlayerConfiguration *config = [[VeLivePlayerConfiguration alloc] init];
// 启用提供播放信息的周期性回调。
config.enableStatisticsCallback = YES;
// 启用本地 DNS 预取。
config.enableLiveDNS = YES;
// 配置播放器的初始设置。
[self.livePlayer setConfig:config];
```

## 设置播放器观察者

调用 [setObserver:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setobserver) 设置播放器观察者，并使用 [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver) 协议监听播放器状态更新、错误、首个音视频帧事件以及周期性播放统计。请在调用 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play) 前设置观察者。示例代码如下。

1. 设置播放器观察者。

   ```objectivec
   @interface VeLivePullViewController () <VeLivePlayerObserver>
   @end
   
   // 设置播放器观察者。
   [self.livePlayer setObserver:self];
   ```

2. 处理播放器事件。

   ```objectivec
   - (void)onError:(TVLManager *)player error:(VeLivePlayerError *)error {
       // 播放器发生错误时触发。
   }
   
   - (void)onInfo:(TVLManager *)player info:(VeLivePlayerError *)info {
       // 播放器遇到内部错误时触发。
   }
   
   - (void)onFirstVideoFrameRender:(TVLManager *)player isFirstFrame:(BOOL)isFirstFrame {
       // 首个视频帧渲染时触发。
   }
   
   - (void)onFirstAudioFrameRender:(TVLManager *)player isFirstFrame:(BOOL)isFirstFrame {
       // 首个音频帧渲染时触发。
   }
   
   - (void)onStallStart:(TVLManager *)player {
       // 播放卡顿开始时触发。
   }
   
   - (void)onStallEnd:(TVLManager *)player {
       // 播放卡顿停止时触发。
   }
   
   - (void)onVideoRenderStall:(TVLManager *)player stallTime:(int64_t)stallTime  {
       // 视频渲染卡顿时触发。
   }
   
   - (void)onAudioRenderStall:(TVLManager *)player stallTime:(int64_t)stallTime  {
       // 音频渲染卡顿时触发。
   }
   
   - (void)onResolutionSwitch:(TVLManager *)player resolution:(VeLivePlayerResolution)resolution error:(VeLivePlayerError *)error reason:(VeLivePlayerResolutionSwitchReason)reason  {
       // 播放器切换到不同清晰度时触发。
   }
   
   - (void)onVideoSizeChanged:(TVLManager *)player width:(int)width height:(int)height  {
       // 视频尺寸变化时触发。
   }
   
   - (void)onReceiveSeiMessage:(TVLManager *)player message:(NSString *)message  {
       // 播放器收到字符串 SEI 消息时触发。
   }
   
   - (void)onReceiveBinarySeiMessage:(TVLManager *)player message:(NSData *)message  {
       // 播放器收到二进制 SEI 消息时触发。启用 enableBinarySei 以接收此回调。启用后，不再触发字符串 SEI 消息回调。
   }
   
   - (void)onMainBackupSwitch:(TVLManager *)player streamType:(VeLivePlayerStreamType)streamType error:(VeLivePlayerError *)error  {
       // 播放器在主备流之间切换时触发。
   }
   
   - (void)onStreamFormatSwitch:(TVLManager *)player fromStreamFormat:(VeLivePlayerFormat)fromStreamType toStreamFormat:(VeLivePlayerFormat)toStreamType error:(VeLivePlayerError *)error extraInfo:(NSDictionary *)extraInfo {
       // 播放器切换流格式时触发。
   }
   
   - (void)onPlayerStatusUpdate:(TVLManager *)player status:(VeLivePlayerStatus)status  {
       // 播放器状态变化时触发。
   }
   
   - (void)onPlayerStatusUpdate:(TVLManager *)player status:(VeLivePlayerStatus)status extraInfo:(NSDictionary *)extraInfo  {
       // 播放器状态变化时触发。extraInfo 参数提供当前播放流的补充信息。
   }
   
   - (void)onStatistics:(TVLManager *)player statistics:(VeLivePlayerStatistics *)statistics {
       // 周期性触发，用于上报播放统计信息。
   }
   
   - (void)onSnapshotComplete:(TVLManager *)player image:(UIImage *)image  {
       // 截图完成时触发。
   }
   
   - (void)onRenderVideoFrame:(TVLManager *)player videoFrame:(VeLivePlayerVideoFrame *)videoFrame  {
       // 播放器解码视频帧时触发。
   }
   
   - (void)onRenderAudioFrame:(TVLManager *)player audioFrame:(VeLivePlayerAudioFrame *)audioFrame  {
       // 播放器解码音频帧时触发。
   }
   
   - (void)onStreamFailedOpenSuperResolution:(TVLManager *)player error:(VeLivePlayerError *)error {
       // SDK 启用超分辨率失败时触发。
   }
   ```

## 设置播放器视图

将 [playerView](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#playerview) 添加到你的自定义视图中，以渲染视频。

```objectivec
// 使用 Metal 进行渲染。
self.livePlayer.playerViewRenderType = TVLPlayerViewRenderTypeMetal;

// 设置 playerView 的尺寸。
self.livePlayer.playerView.frame = UIScreen.mainScreen.bounds;

// 将 playerView 作为子视图添加到你的自定义视图。
[self.view addSubview:self.livePlayer.playerView];
```

## 设置播放 URL

调用 [setPlayUrl:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setplayurl) 设置单个播放 URL。该方法支持 RTMP、FLV 和 HLS 等直播协议。请将示例代码中的 URL 替换为你的实际直播播放 URL。请在调用 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play) 前调用此方法。示例代码如下。

```objectivec
NSString *playUrl = @"http://pull.example.com/live/stream.flv";
[self.livePlayer setPlayUrl:playUrl]; // 设置播放 URL。
```

> **说明**

> 如需配置多个播放 URL，请调用 [setPlayStreamData:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setplaystreamdata)。该方法支持 RTM 拉流、QUIC 拉流、主备流切换、多清晰度和自适应码率（ABR）等功能。请在调用 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play) 前调用此方法。更多信息，请参见 [Player SDK for iOS：高级功能](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3)。

## 调整播放画面

你可以配置填充模式、镜像和旋转，以获得更好的播放体验。

### 设置填充模式

调用 [setRenderFillMode:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setrenderfillmode) 设置播放画面的填充模式。播放器支持以下填充模式。

|填充模式 |描述 |
|---|---|
|VeLivePlayerFillModeAspectFit |显示完整视频帧。视频帧会按比例缩放，直到整个帧适配画布。如果视频帧宽高比与画布宽高比不同，未填充区域将显示为黑色。 |
|VeLivePlayerFillModeFullFill |使视频帧适配画布。视频帧会非等比缩放，直到填满画布。在此过程中，视频帧的宽高比可能会发生变化。 |
|VeLivePlayerFillModeAspectFill |用视频填满画布。视频帧会按比例缩放，直到填满画布。超出屏幕的视频帧部分会被裁剪。因此，视频帧的某些部分可能不可见。 |

```objectivec
// 将填充模式设置为 aspect fill。
[self.livePlayer setRenderFillMode:VeLivePlayerFillModeAspectFill];
```

### 设置镜像

调用 [setRenderMirror:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setrendermirror) 设置播放画面的镜像。播放器支持以下镜像模式。

|镜像模式 |描述 |
|---|---|
|VeLivePlayerMirrorNone |无镜像。 |
|VeLivePlayerMirrorHorizontal |水平镜像。 |
|VeLivePlayerMirrorVertical |垂直镜像。 |

```objectivec
// 设置水平镜像。
[self.livePlayer setRenderMirror:VeLivePlayerMirrorHorizontal];
```

### 设置旋转角度

调用 [setRenderRotation:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setrenderrotation) 设置播放画面的旋转角度。播放器支持以下旋转角度。

|旋转角度 |描述 |
|---|---|
|`VeLivePlayerRotation0` |不旋转。 |
|`VeLivePlayerRotation90` |将视频顺时针旋转 90 度。 |
|`VeLivePlayerRotation180` |将视频顺时针旋转 180 度。 |
|`VeLivePlayerRotation270` |将视频顺时针旋转 270 度。 |

```objectivec
// 将视频顺时针旋转 90 度。
[self.livePlayer setRenderRotation:VeLivePlayerRotation90];
```

## 开始播放

调用 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play) 开始播放。

```objectivec
[self.livePlayer play]; // 开始播放。
```

你可以调用 [isPlaying](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#isplaying) 获取当前播放状态。

```objectivec
BOOL isPlaying = [self.livePlayer isPlaying]; // 获取播放状态。
```

## 停止播放

调用 [stop](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#stop) 停止播放。调用 `stop` 不会销毁播放器。

```objectivec
[self.livePlayer stop]; // 停止播放。
```

## 销毁播放器

停止播放后，如果不再需要播放器，请调用 [destroy](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#destroy) 销毁播放器并释放其关联内存。

```objectivec
[self.livePlayer destroy]; // 销毁播放器并释放其关联内存。
```

## 处理应用前后台切换

默认情况下，应用进入后台后播放器会继续播放音频。为防止音频在后台继续播放，请在应用进入后台时停止播放，并在应用返回前台时恢复播放，如以下代码所示：

```objectivec
// 添加观察者，用于监听应用切换到前台时的通知。
[NSNotificationCenter.defaultCenter addObserver:self
            selector:@selector(applicationDidBecomeActive:)
            name:UIApplicationDidBecomeActiveNotification
            object:nil];
// 添加观察者，用于监听应用切换到后台时的通知。
[NSNotificationCenter.defaultCenter addObserver:self
            selector:@selector(applicationWillResignActive:)
            name:UIApplicationWillResignActiveNotification
            object:nil];

- (void)applicationDidBecomeActive:(NSNotification *)notification {
    [self.livePlayer play]; // 应用切换到前台时恢复播放。
}

- (void)applicationWillResignActive:(NSNotification *)notification {
    [self.livePlayer stop]; // 应用切换到后台时停止播放。
}
```

## 静音播放

调用 [setMute:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setmute) 将音频静音或取消静音。

```objectivec
[self.livePlayer setMute:YES]; // 静音播放。
```

你可以通过调用 [isMute](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#ismute) 查询音频是否已静音。

```objectivec
BOOL isMute = [self.livePlayer isMute]; // 获取静音状态。
```

## 设置播放器音量

使用 [volume](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#volume) 属性设置播放器音量。该属性用于指定音量级别。默认值为 `1.0`。有效范围为 `[0.0, 1.0]`。

```objectivec
[self.livePlayer setVolume:0.5];
```

## 设置日志级别

调用 [setLogLevel:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setloglevel) 设置打印到控制台的日志级别。

```objectivec
// 将日志级别设置为 INFO。将输出 INFO、WARNING 和 ERROR 级别的日志。
[TVLManager setLogLevel:VeLivePlayerLogLevelInfo];
```

## 故障排除

错误：无法从 <TVLOwnPlayer 0x2817e9290\> 移除键路径 "status" 的观察者 <TTAVPlayerItem 0x2806577a0\>，因为它未注册为观察者

如果从不同线程调用直播播放器的方法，可能会发生此错误。为防止此错误，请确保从主线程调用直播播放器的方法。
