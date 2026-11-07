---
title: "Android 播放器 SDK：API"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference-zh-CN"
---

# VeLivePlayer

```java
public abstract class com.ss.videoarch.liveplayer.VeLivePlayer
```

直播播放器。

## 静态函数

|返回值 |名称 |
|---|---|
|static String |[getVersion](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-getversion) |
|static void |[setLogLevel](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setloglevel) |

## 成员函数

|返回值 |名称 |
|---|---|
|abstract void |[setConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setconfig) |
|abstract void |[setObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setobserver) |
|abstract void |[setRenderFillMode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setrenderfillmode) |
|abstract void |[setSurfaceHolder](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurfaceholder) |
|abstract void |[setSurface](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurface) |
|abstract void |[setPlayUrl](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplayurl) |
|abstract void |[setPlayStreamData](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplaystreamdata) |
|abstract void |[play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) |
|abstract void |[stop](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-stop) |
|abstract void |[destroy](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-destroy) |
|abstract boolean |[switchResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-switchresolution) |
|abstract boolean |[isPlaying](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-isplaying) |
|abstract void |[setPlayerVolume](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplayervolume) |
|abstract void |[setMute](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setmute) |
|abstract boolean |[isMute](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-ismute) |
|abstract void |[setUrlHostIP](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-seturlhostip) |
|abstract void |[setProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setproperty) |
|abstract int |[snapshot](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-snapshot) |
|abstract void |[enableVideoFrameObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-enablevideoframeobserver) |
|abstract void |[enableAudioFrameObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-enableaudioframeobserver) |
|abstract void |[setRenderRotation](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setrenderrotation) |
|abstract void |[setRenderMirror](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setrendermirror) |
|abstract void |[setEnableSuperResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setenablesuperresolution) |
|abstract void |[setEnableSharpen](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setenablesharpen) |
|abstract ArrayList |[getStreamList](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-getstreamlist) |

## 说明

### getVersion

```java
public static String com.ss.videoarch.liveplayer.VeLivePlayer.getVersion()
```

获取 Player SDK 的版本号。

**返回值**

Player SDK 的版本号。

### setLogLevel

```java
public static void com.ss.videoarch.liveplayer.VeLivePlayer.setLogLevel(VeLivePlayerLogConfig.VeLivePlayerLogLevel logLevel)
```

设置输出日志的级别。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|logLevel |VeLivePlayerLogConfig.VeLivePlayerLogLevel |输出日志的级别。详情请参见 [VeLivePlayerLogLevel](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerLogLevel)。 |

### setConfig

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setConfig(VeLivePlayerConfiguration config)
```

初始化播放器，并配置是否开启 SEI 消息、硬件解码、本地 DNS 预取及其他配置。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|config |VeLivePlayerConfiguration |播放器配置。详情请参见 [VeLivePlayerConfiguration](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerConfiguration)。 |

**说明**

在调用 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 之前，调用此方法初始化播放器。

### setObserver

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setObserver(VeLivePlayerObserver observer)
```

设置播放器观察者，用于监听直播播放器的事件，例如播放错误或状态更新、首个音频和视频帧渲染，以及分辨率切换。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|observer |VeLivePlayerObserver |播放器观察者。详情请参见 [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver)。 |

**说明**

在调用 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 之前调用此方法。

### setRenderFillMode

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setRenderFillMode(VeLivePlayerFillMode fillMode)
```

设置播放器画面的填充模式。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|fillMode |VeLivePlayerFillMode |SurfaceView 的填充模式。默认值为 `VeLivePlayerFillModeAspectFill`。详情请参见 [VeLivePlayerFillMode](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerFillMode)。 |

**说明**

* 在调用 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 之前调用此方法，设置播放器的初始填充模式。

* 你可以在播放期间调用此方法，动态调整填充模式。

### setSurfaceHolder

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setSurfaceHolder(SurfaceHolder surfaceHolder)
```

设置用于视频渲染和播放的 `SurfaceHolder` 对象。如果你使用 `SurfaceView` 播放，请使用此方法。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|surfaceHolder |SurfaceHolder |`SurfaceHolder` 对象。 |

**说明**

如果同时调用 setSurfaceHolder 和 [setSurface](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurface) 设置 `Surface` 对象，播放器会优先使用 `surfaceHolder` 的配置。

### setSurface

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setSurface(Surface surface)
```

设置用于视频渲染和播放的 `Surface` 对象。如果你使用 `SurfaceView` 或 `TextureView` 播放，请使用此方法。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|surface |Surface |`Surface` 对象。 |

**说明**

如果同时调用 [setSurfaceHolder](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurfaceholder) 和 `setSurface` 设置 `Surface` 对象，播放器会优先使用 `surfaceHolder` 的配置。

### setPlayUrl

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setPlayUrl(String url)
```

设置拉流地址。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|url |String |拉流地址。 |

**说明**

在调用 play 之前调用此方法。

### setPlayStreamData

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setPlayStreamData(VeLivePlayerStreamData streamData)
```

设置多个直播流。如果需要启用依赖多个直播流的功能，例如自适应码率（ABR）、手动分辨率切换，以及主备流，请调用此方法。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|streamData |VeLivePlayerStreamData |多个拉流地址的配置。详情请参见 [VeLivePlayerStreamData](https://docs.byteplus.com/en/docs/24/player-android-api-keytype#VeLivePlayerStreamData)。 |

**说明**

在调用 play 之前调用此方法。

### play

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.play()
```

开始或恢复播放。

**说明**

调用此方法后，当播放器完成拉流准备以及首帧渲染时，都会触发 [onPlayerStatusUpdate](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate) 回调。

### stop

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.stop()
```

停止播放。此方法不会销毁播放器。

**说明**

调用此方法后播放停止时，会触发 [onPlayerStatusUpdate](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate) 回调。

### destroy

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.destroy()
```

停止播放并销毁播放器。

### switchResolution

```java
public abstract boolean com.ss.videoarch.liveplayer.VeLivePlayer.switchResolution(VeLivePlayerResolution resolution)
```

更改视频分辨率。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|resolution |VeLivePlayerResolution |视频分辨率。详情请参见 VeLivePlayerResolution。 |

**返回值**

* true：成功；

* false：失败。

**说明**

* 调用此方法之前，调用 [setPlayStreamData](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplaystreamdata) 设置多个分辨率。

* 调用此方法后，播放器切换到新分辨率时，会触发 [onResolutionSwitch](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onresolutionswitch) 回调。

* 为避免切换分辨率时出现黑屏或卡顿，请将 [enableSmoothSwitchResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerStreamData-enablesmoothswitchresolution) 设置为 `true`。

### isPlaying

```java
public abstract boolean com.ss.videoarch.liveplayer.VeLivePlayer.isPlaying()
```

检查播放器是否正在播放。

**返回值**

播放器是否正在播放。

* true：播放器正在播放；

* false：播放器未播放。

### setPlayerVolume

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setPlayerVolume(float volume)
```

设置播放器音量。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|volume |float |音量。默认值为 `1.0`。取值范围为 [0.0, 1.0]。 |

### setMute

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setMute(boolean mute)
```

设置是否静音播放。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|mute |boolean |是否静音播放。默认值为 `false`。<br><br><br>* true：静音；<br><br>* false：不静音。 |

### isMute

```java
public abstract boolean com.ss.videoarch.liveplayer.VeLivePlayer.isMute()
```

检查播放是否已静音。

**返回值**

播放是否已静音。

* true：已静音；

* false：未静音。

### setUrlHostIP

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setUrlHostIP(Map<String, List<String>> hostIpMap)
```

设置域名到服务器 IP 地址的映射。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|hostIpMap |Map<String, List\> |域名到服务器 IP 地址的映射。`Map` 对象以域名作为键，对应的值是与该域名关联的服务器 IP 地址列表。该值为 `List` 类型。 |

**说明**

* 使用 setUrlHostIP 映射域名和 IP 地址时，请在初始配置中将 [enableLiveDNS](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerConfiguration-enablelivedns) 设置为 false，以禁用 DNS 预解析功能。

* 在调用 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 开始播放之前，调用此方法设置域名和 IP 地址的映射。

### setProperty

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setProperty(
    String key,
    Object value
)
```

配置播放器的高级设置，包括离屏渲染、最大缓冲时长和自适应码率（ABR）算法。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|key |String |高级设置的参数名称。 |
|value |Object |高级设置的参数值。 |

### snapshot

```java
public abstract int com.ss.videoarch.liveplayer.VeLivePlayer.snapshot()
```

截取视频画面。

**返回值**

* 0：允许截图。

* [VeLivePlayerErrorRefused](https://docs.byteplus.com/en/docs/24/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorrefused)：不允许截图。

**说明**

* 此方法仅在播放期间生效。

* 调用此方法后，截图完成时会触发 [onSnapshotComplete](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onsnapshotcomplete) 回调，其中包含截图的 Bitmap 对象。

### enableVideoFrameObserver

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.enableVideoFrameObserver(
    boolean enable,
    VeLivePlayerPixelFormat pixelFormat,
    VeLivePlayerVideoBufferType bufferType
)
```

设置视频帧观察者。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|enable |boolean |是否启用视频帧回调。默认值为 `false`。<br><br><br>* true：启用；<br><br>* false：禁用。 |
|pixelFormat |VeLivePlayerPixelFormat |回调中视频帧的像素格式。详情请参见 [VeLivePlayerPixelFormat](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerPixelFormat)。 |
|bufferType |VeLivePlayerVideoBufferType |回调中视频数据的封装格式。详情请参见 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerVideoBufferType)。 |

**说明**

* 你可以调用此方法订阅解码后的视频数据，用于外部渲染。

* 调用此方法后，SDK 收到视频帧时会触发 [onRenderVideoFrame](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onrendervideoframe) 回调。回调包含视频帧的详细信息。

* 如果使用外部渲染，你需要确保视频和音频同步。

### enableAudioFrameObserver

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.enableAudioFrameObserver(
    boolean enable,
    boolean enableRendering,
    VeLivePlayerAudioBufferType bufferType
)
```

设置音频帧观察者。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|enable |boolean |是否启用音频帧回调。默认值为 `false`。<br><br><br>* true：启用；<br><br>* false：禁用。 |
|enableRendering |boolean |是否启用播放器渲染。默认值为 `false`。<br><br><br>* true：启用；<br><br>* false：禁用。 |
|bufferType |VeLivePlayerAudioBufferType |音频缓冲区类型。详情请参见 [VeLivePlayerAudioBufferType](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerAudioBufferType)。 |

**说明**

* 如果你想使用外部渲染，可以调用此方法订阅解码后的音频数据。

* 调用此方法后，SDK 收到音频帧时会触发 [onRenderAudioFrame](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onrenderaudioframe) 回调。回调包含音频帧的详细信息。

* 如果使用外部渲染，你需要确保视频和音频同步。

### setRenderRotation

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setRenderRotation(VeLivePlayerRotation rotation)
```

设置视频的顺时针旋转角度。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|rotation |VeLivePlayerRotation |视频的顺时针旋转角度。默认禁用旋转。详情请参见 [VeLivePlayerRotation](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerRotation)。 |

**说明**

* 你可以在播放前和播放期间更改旋转角度。

* 每次调用此方法时，播放器都会基于原始视频旋转视频。

* 对视频同时应用旋转和镜像时，播放器会先镜像视频，然后旋转视频。

### setRenderMirror

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setRenderMirror(VeLivePlayerMirror mirror)
```

配置镜像设置。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|mirror |VeLivePlayerMirror |镜像设置。默认禁用镜像。详情请参见 [VeLivePlayerMirror](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerMirror)。 |

**说明**

* 你可以在播放前和播放期间更改镜像设置。

* 每次调用此方法时，播放器都会将镜像设置应用到原始视频。

* 对视频同时应用旋转和镜像时，播放器会先镜像视频，然后旋转视频。

### setEnableSuperResolution

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setEnableSuperResolution(boolean enable)
```

启用或禁用超分辨率。使用前必须先联系 BytePlus [技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) 开通该功能。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|enable |boolean |是否启用超分辨率。默认值为 false。<br><br><br>* true：启用；<br><br>* false：禁用。 |

**说明**

* 在收到 [onFirstVideoFrameRender](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onfirstvideoframerender) 回调后，或在播放期间调用此方法。

* 支持在播放期间调用此接口，动态启用和禁用超分辨率。

* 如果 SDK 因设备型号、视频分辨率或帧率而无法启用超分辨率，你会收到 [onStreamFailedOpenSuperResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution) 回调。

### setEnableSharpen

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setEnableSharpen(boolean enable)
```

设置是否启用视频锐化。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|enable |boolean |设置是否启用视频锐化。默认值为 `false`。<br><br><br>* true：启用；<br><br>* false：禁用。 |

### getStreamList

```java
public abstract ArrayList<VeLivePlayerStreamInfo> com.ss.videoarch.liveplayer.VeLivePlayer.getStreamList()
```

获取流信息。

**返回值**

流信息。更多信息请参见 [VeLivePlayerStreamInfo](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype?lang=en#veliveplayerstreaminfo)。

**说明**

* 当 [VeLivePlayerStatus](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerStatus)（播放器状态）为 `VeLivePlayerStatusPrepared` 时调用此方法。

* 此方法目前仅适用于 HLS 格式流。
