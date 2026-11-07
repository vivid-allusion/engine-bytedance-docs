---
title: "iOS 播放器 SDK：API"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api-zh-CN"
---

# TVLManager(VeLivePlayer)

```objectivec
@interface TVLManager (VeLivePlayer)
```

直播播放器。

## 成员属性

|类型 |名称 |
|---|---|
|id |[observer](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-observer) |
|UIView\* |[playerView](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-playerview) |
|float |[volume](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-volume) |
|BOOL |[isPlaying](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-isplaying) |

## 静态函数

|返回值 |名称 |
|---|---|
|void |[setLogLevel:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setloglevel) |
|NSString\* |[getVersion](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-getversion) |

## 成员函数

|返回值 |名称 |
|---|---|
|instancetype |[init](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-init) |
|instancetype |[initWithType:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-initwithtype) |
|void |[setConfig:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setconfig) |
|void |[setObserver:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setobserver) |
|void |[setRenderFillMode:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setrenderfillmode) |
|void |[setPlayUrl:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setplayurl) |
|void |[setUrlHostIP:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-seturlhostip) |
|void |[setProperty:value:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setproperty-value) |
|void |[setPlayStreamData:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setplaystreamdata) |
|void |[play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-play) |
|void |[stop](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-stop) |
|void |[destroy](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-destroy) |
|int |[isSupportResolutionSwitch:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-issupportresolutionswitch) |
|void |[switchResolution:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-switchresolution) |
|void |[setMute:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setmute) |
|BOOL |[isMute](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-ismute) |
|void |[setRenderRotation:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setrenderrotation) |
|void |[setRenderMirror:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setrendermirror) |
|int |[snapshot](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-snapshot) |
|void |[enableVideoFrameObserver:pixelFormat:bufferType:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enablevideoframeobserver-pixelformat-buffertype) |
|void |[enableAudioFrameObserver:enableRendering:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enableaudioframeobserver-enablerendering) |
|void |[setEnableSuperResolution:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setenablesuperresolution) |
|void |[setEnableSharpen:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setenablesharpen) |
|VeLivePlayerStreamInfo |[getStreamList](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-getstreamlist) |

## 说明

### observer

```objectivec
@property (nonatomic, weak, readonly, nullable) id<VeLivePlayerObserver> observer;
```

播放器观察者。

### playerView

```objectivec
@property (nonatomic, strong, readonly) UIView *playerView;
```

播放器用于渲染视频的视图。将 `playerView` 添加到应用的视图层级中，以显示视频内容。

### volume

```objectivec
@property (nonatomic, assign) float volume;
```

播放器音量。默认值为 `1.0`。取值范围为 [0.0, 1.0]。

### isPlaying

```objectivec
@property (nonatomic, assign, readonly) BOOL isPlaying;
```

检查播放器是否正在播放。

## 说明

### setLogLevel:

```objectivec
+ (void)setLogLevel:(VeLivePlayerLogLevel)logLevel;
```

设置输出日志的级别。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|logLevel |VeLivePlayerLogLevel |输出日志的级别。详情请参见 [VeLivePlayerLogLevel](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerLogLevel)。 |

### getVersion

```objectivec
+ (NSString *_Nonnull )getVersion;
```

获取播放器 SDK 的版本号。

**返回值**

播放器 SDK 的版本号。

### init

```objectivec
- (instancetype)init;
```

初始化播放器。

### initWithType:

```objectivec
- (instancetype)initWithType:(VeLivePlayerType)type;
```

初始化指定类型的播放器。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|type |VeLivePlayerType |播放器类型。详情请参见 [VeLivePlayerType](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerType)。 |

### setConfig:

```objectivec
- (void)setConfig:(VeLivePlayerConfiguration *_Nonnull)config;
```

配置播放器设置，包括是否开启 SEI 消息、硬件解码和本地 DNS 预取。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|config |VeLivePlayerConfiguration\* |播放器配置。详情请参见 [VeLivePlayerConfiguration](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration)。 |

**注意事项**

请在调用 play 前调用此方法。

### setObserver:

```objectivec
- (void)setObserver:(id<VeLivePlayerObserver> _Nullable)observer;
```

设置播放器观察者，用于监听 VeLivePlayer 的事件，例如播放错误或状态更新、首个音视频帧渲染以及分辨率切换。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|observer |id |播放器观察者。详情请参见 [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver)。 |

**注意事项**

请在调用 play 前调用此方法。

### setRenderFillMode:

```objectivec
- (void)setRenderFillMode:(VeLivePlayerFillMode)fillMode;
```

设置播放器画面的填充模式。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|fillMode |VeLivePlayerFillMode |SurfaceView 的填充模式。默认值为 `VeLivePlayerFillModeAspectFill`。详情请参见 [VeLivePlayerFillMode](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerFillMode)。 |

**注意事项**

* 调用 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-play) 前调用此方法，设置播放器的初始填充模式。

* 播放期间可以调用此方法动态调整填充模式。

### setPlayUrl:

```objectivec
- (void)setPlayUrl:(NSString *_Nonnull)url;
```

设置拉流地址。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|url |NSString\* |拉流地址。 |

**注意事项**

请在调用 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-play) 前调用此方法。

### setUrlHostIP:

```objectivec
- (void)setUrlHostIP:(NSDictionary *_Nonnull)hostIpMap;
```

设置域名到服务器 IP 地址的映射关系。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|hostIpMap |NSDictionary\* |域名到服务器 IP 地址的映射关系。`Map` 对象使用域名作为键，对应的值是与该域名关联的服务器 IP 地址列表。该值为 `List` 类型。 |

### setProperty:value:

```objectivec
- (void)setProperty:(NSString *_Nonnull)key value:(id _Nonnull)value;
```

配置播放器的高级设置，包括离屏渲染、最大缓冲时长和自适应码率（ABR）算法。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|key |NSString\* |高级设置的参数名称。 |
|value |id |高级设置的参数值。 |

### setPlayStreamData:

```objectivec
- (void)setPlayStreamData:(VeLivePlayerStreamData *_Nonnull)streamData;
```

设置多个直播流。当需要启用需要多个直播流的功能时调用此方法，例如自适应码率（ABR）、手动分辨率切换以及主备流。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|streamData |VeLivePlayerStreamData\* |多个拉流地址的配置。详情请参见 [VeLivePlayerStreamData](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData)。 |

**注意事项**

请在调用 play 前调用此方法。

### play

```objectivec
- (void)play;
```

开始或恢复播放。

**注意事项**

调用此方法后，在播放器完成拉流准备以及首帧渲染时，都会触发 [onPlayerStatusUpdate:status:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status) 回调。

### stop

```objectivec
- (void)stop;
```

停止播放。此方法不会销毁播放器。

**注意事项**

调用此方法后，当播放停止时，会触发 [onPlayerStatusUpdate:status:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status) 回调。

### destroy

```objectivec
- (void)destroy;
```

停止播放并销毁播放器。

### isSupportResolutionSwitch:

```objectivec
- (int)isSupportResolutionSwitch:(VeLivePlayerResolution)resolution;
```

检查播放器当前是否支持指定的分辨率档位。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|resolution |VeLivePlayerResolution |分辨率档位。详情请参见 [VeLivePlayerResolution](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerResolution)。 |

**返回值**

* 0：支持；

* 其他：不支持。其他返回值的详情请参见 [VeLivePlayerSupportResolutionSwitchError](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerSupportResolutionSwitchError)。

### switchResolution:

```objectivec
- (void)switchResolution:(VeLivePlayerResolution)resolution;
```

更改视频分辨率。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|resolution |VeLivePlayerResolution |视频分辨率。详情请参见 [VeLivePlayerResolution](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerResolution)。 |

**返回值**

* `YES`：成功；

* `NO`：失败。

**注意事项**

* 调用此方法前，请调用 [setPlayStreamData:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setplaystreamdata) 设置多个分辨率。

* 调用此方法后，播放器切换到新分辨率时，会触发 [onResolutionSwitch:resolution:error:reason:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onresolutionswitch-resolution-error-reason) 回调。

* 为避免切换分辨率时出现黑屏或卡顿，请将 [enableSmoothSwitchResolution](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-enablesmoothswitchresolution) 设置为 `YES`。

### setMute:

```objectivec
- (void)setMute:(BOOL)mute;
```

设置是否静音播放。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|mute |BOOL |是否静音播放。默认值为 `NO`。<br><br><br>* `YES`：静音；<br><br>* `NO`：不静音。 |

### isMute

```objectivec
- (BOOL)isMute;
```

检查播放是否静音。

**返回值**

播放是否静音。

* `YES`：已静音；

* `NO`：未静音。

### setRenderRotation:

```objectivec
- (void)setRenderRotation:(VeLivePlayerRotation)rotation;
```

设置视频的顺时针旋转角度。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|rotation |VeLivePlayerRotation |视频的顺时针旋转角度。默认禁用旋转。详情请参见 [VeLivePlayerRotation](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerRotation)。 |

**注意事项**

* 可以在播放前和播放期间更改旋转角度。

* 每次调用此方法时，播放器都会基于原始视频旋转视频。

* 同时对视频应用旋转和镜像时，播放器会先镜像视频，然后旋转视频。

### setRenderMirror:

```objectivec
- (void)setRenderMirror:(VeLivePlayerMirror)mirror;
```

配置镜像设置。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|mirror |VeLivePlayerMirror |镜像设置。默认禁用镜像。详情请参见 [VeLivePlayerMirror](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerMirror)。 |

**注意事项**

* 可以在播放前和播放期间更改镜像设置。

* 每次调用此方法时，播放器都会将镜像设置应用到原始视频。

* 同时对视频应用旋转和镜像时，播放器会先镜像视频，然后旋转视频。

### snapshot

```objectivec
- (int)snapshot;
```

截取视频截图。

**返回值**

* 0：允许截图；

* VeLivePlayerErrorRefused：不允许截图。

**注意事项**

* 此方法仅在播放期间生效。

* 调用此方法后，截图完成时会触发 [onSnapshotComplete:image:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onsnapshotcomplete-image) 回调，回调中包含截图的 `UIImage` 对象。

### enableVideoFrameObserver:pixelFormat:bufferType:

```objectivec
- (void)enableVideoFrameObserver:(BOOL)enable pixelFormat:(VeLivePlayerPixelFormat)pixelFormat bufferType:(VeLivePlayerVideoBufferType)bufferType;
```

设置视频帧观察者。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|enable |BOOL |是否启用视频帧回调。默认值为 `NO`。<br><br><br>* `YES`：启用；<br><br>* `NO`：禁用。 |
|pixelFormat |VeLivePlayerPixelFormat |回调中视频帧的像素格式。详情请参见 [VeLivePlayerPixelFormat](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerPixelFormat)。 |
|bufferType |VeLivePlayerVideoBufferType |回调中视频数据的封装格式。详情请参见 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoBufferType)。 |

**注意事项**

* 可以调用此方法订阅解码后的视频数据，用于外部渲染。

* 调用此方法后，SDK 收到视频帧时会触发 onRenderVideoFrame:videoFrame:is 回调。该回调包含视频帧的详细信息。

* 如果使用外部渲染，需要确保视频和音频同步。

### enableAudioFrameObserver:enableRendering:

```objectivec
- (void)enableAudioFrameObserver:(BOOL)enable enableRendering:(BOOL)enableRendering;
```

设置音频帧观察者。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|enable |BOOL |是否启用音频帧回调。默认值为 `NO`。<br><br><br>* `YES`：启用；<br><br>* `NO`：禁用。 |
|enableRendering |BOOL |是否启用播放器渲染。默认值为 `NO`。<br><br><br>* `YES`：启用；<br><br>* `NO`：禁用。 |

**注意事项**

* 可以调用此方法订阅解码后的音频数据，用于外部渲染。

* 调用此方法后，SDK 收到音频帧时会触发 [onRenderAudioFrame:audioFrame:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onrenderaudioframe-audioframe) 回调。该回调包含音频帧的详细信息。

* 如果使用外部渲染，需要确保视频和音频同步。

### setEnableSuperResolution:

```objectivec
- (void)setEnableSuperResolution:(BOOL)enable;
```

启用或禁用超分辨率。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|enable |BOOL |是否启用超分辨率。默认值为 `NO`。<br><br><br>* `YES`：开启；<br><br>* `NO`：关闭。 |

**注意事项**

* 请在收到 onFirstVideoFrameRender:isFirstFrame:callback 后或播放期间调用此方法。

* 支持在播放期间调用此方法开启或关闭超分辨率。

* 如果 SDK 因设备型号、视频分辨率或帧率而无法启用超分辨率，你将收到 [onStreamFailedOpenSuperResolution:error:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution-error)。

### setEnableSharpen:

```objectivec
- (void)setEnableSharpen:(BOOL)enable;
```

设置是否启用视频锐化。启用后，视频中的边缘和细节会更突出，使画面看起来更清晰、更生动。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|enable |BOOL |是否启用视频锐化。默认值为 `NO`。有效值：<br><br><br>* `YES`：启用。<br><br>* `NO`：禁用。 |

### getStreamList

```objectivec
- (NSArray<VeLivePlayerStreamInfo *> *)getStreamList;
```

获取流信息。

**返回值**

流信息。

**注意事项**

* 当 [VeLivePlayerStatus](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatus)（播放器状态）为 `VeLivePlayerStatusPrepared` 时调用此方法。

* 此方法当前仅适用于 HLS 格式的流。

# TVLManager(PictureInPicture)

```objective-c
@interface TVLManager (PictureInPicture)
```

直播播放器的画中画（PiP）能力。

## 成员变量

|名称 |类型 |
|---|---|
|[enablePictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-enablepictureinpicture) |BOOL |
|[pictureInPictureRequiresLinearPlayback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-pictureinpicturerequireslinearplayback) |BOOL |
|[canStartPictureInPictureAutomaticallyFromInline](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-canstartpictureinpictureautomaticallyfrominline) |BOOL |
|[avPictureInPictureController](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-avpictureinpicturecontroller) |AVPictureInPictureController \* |
|[pictureInPictureDelegate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-pictureinpicturedelegate) |id |
|[pictureInPicturePlaybackDelegate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-pictureinpictureplaybackdelegate) |id |

## 静态函数

|名称 |返回值 |
|---|---|
|[isPictureInPictureSupported](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-ispictureinpicturesupported) |BOOL |
|[isPictureInPictureStarted](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-ispictureinpicturestarted) |BOOL |

## 成员函数

|名称 |返回值 |
|---|---|
|[startPictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-startpictureinpicture) |void |
|[stopPictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-stoppictureinpicture) |void |
|[invalidatePictureInPicturePlaybackState](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-invalidatepictureinpictureplaybackstate) |void |

## 变量说明

### enablePictureInPicture

```objective-c
@property (nonatomic, assign) BOOL enablePictureInPicture;
```

是否启用 PiP 功能。默认值为 `NO`。

* `YES`：启用 PiP 功能。随后可以调用 PiP 相关方法或设置 PiP 相关属性。

* `NO`：禁用 PiP 功能。

**说明**

将此属性设置为 `YES` 前，请确保满足以下条件：

* 系统运行 iOS 15.0 或更高版本。

* 应用已在 **Background Modes** 中启用 **Audio, AirPlay, and Picture in Picture**。

### pictureInPictureRequiresLinearPlayback

```objective-c
@property (nonatomic, assign) BOOL pictureInPictureRequiresLinearPlayback;
```

PiP 窗口中是否隐藏快进和快退按钮。默认值为 `YES`。有效值：

* `YES`：隐藏快进和快退按钮。

* `NO`：显示快进和快退按钮。

### canStartPictureInPictureAutomaticallyFromInline

```objective-c
@property (nonatomic, assign) BOOL canStartPictureInPictureAutomaticallyFromInline;
```

应用进入后台时，PiP 是否可以自动启动。默认值为 `YES`。有效值：

* `YES`：允许系统在应用进入后台时尝试自动启动 PiP。

* `NO`：阻止系统在应用进入后台时自动启动 PiP。

### avPictureInPictureController

```objective-c
@property (nonatomic, strong, readonly, nullable) AVPictureInPictureController *avPictureInPictureController;
```

与当前播放器关联的 [AVPictureInPictureController](https://developer.apple.com/documentation/AVKit/AVPictureInPictureController) 实例，可用于读取系统级 PiP 状态和相关信息。

### pictureInPictureDelegate

```objective-c
@property (nonatomic, weak, nullable) id<AVPictureInPictureControllerDelegate> pictureInPictureDelegate API_AVAILABLE(ios(15.0));
```

实现 [AVPictureInPictureControllerDelegate](https://developer.apple.com/documentation/avkit/avpictureinpicturecontrollerdelegate) 的代理对象，用于接收 PiP 生命周期回调，例如启动、停止和失败事件。

**说明**

SDK 提供基础 PiP 功能。如需自定义相关代理回调的处理方式，请将此属性设置为你的代理对象。仅当同时满足以下条件时，此属性才会生效：

* 系统运行 iOS 15.0 或更高版本。

* [enablePictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-enablepictureinpicture) 属性设置为 `YES`。

### pictureInPicturePlaybackDelegate

```objective-c
@property (nonatomic, weak, nullable) id<AVPictureInPictureSampleBufferPlaybackDelegate> pictureInPicturePlaybackDelegate API_AVAILABLE(ios(15.0));
```

实现 [AVPictureInPictureSampleBufferPlaybackDelegate](https://developer.apple.com/documentation/avkit/avpictureinpicturesamplebufferplaybackdelegate) 的代理对象，用于处理 PiP 中的播放和暂停请求，判断 PiP 窗口中的播放控件应显示播放还是暂停，并提供可播放时间范围。

**说明**

SDK 提供基础 PiP 功能。如需自定义相关代理回调的处理方式，请将此属性设置为你的代理对象。仅当同时满足以下条件时，此属性才会生效：

* 系统运行 iOS 15.0 或更高版本。

* [enablePictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-enablepictureinpicture) 属性设置为 `YES`。

## 函数说明

### isPictureInPictureSupported

```objective-c
+ (BOOL) isPictureInPictureSupported;
```

当前设备是否支持 PiP。

**返回值**

* `YES`：支持。

* `NO`：不支持。

### isPictureInPictureStarted

```objective-c
+ (BOOL) isPictureInPictureStarted;
```

PiP 是否已成功启动。

**返回值**

* `YES`：PiP 已成功启动。

* `NO`：PiP 未启动。

### startPictureInPicture

```objective-c
- (void) startPictureInPicture;
```

手动启动 PiP。

### stopPictureInPicture

```objective-c
- (void) stopPictureInPicture;
```

手动停止 PiP 并关闭 PiP 窗口。

### invalidatePictureInPicturePlaybackState

```objective-c
- (void) invalidatePictureInPicturePlaybackState;
```

手动更新 PiP 窗口中的播放/暂停按钮状态和进度显示。
