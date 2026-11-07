---
title: "Android 播放器 SDK：回调"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback-zh-CN"
---

# VeLivePlayerObserver

```java
public interface com.ss.videoarch.liveplayer.VeLivePlayerObserver
```

直播播放器观察者。

## 成员函数

|返回值 |名称 |
|---|---|
|default void |[onError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onerror) |
|default void |[onInfo](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-oninfo) |
|default void |[onFirstVideoFrameRender](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onfirstvideoframerender) |
|default void |[onFirstAudioFrameRender](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onfirstaudioframerender) |
|default void |[onStallStart](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstallstart) |
|default void |[onStallEnd](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstallend) |
|default void |[onVideoRenderStall](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onvideorenderstall) |
|default void |[onAudioRenderStall](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onaudiorenderstall) |
|default void |[onResolutionSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onresolutionswitch) |
|default void |[onVideoSizeChanged](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onvideosizechanged) |
|default void |[onReceiveSeiMessage](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onreceiveseimessage) |
|default void |[onReceiveBinarySeiMessage](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onreceivebinaryseimessage) |
|default void |[onMainBackupSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onmainbackupswitch) |
|default void |[onStreamFormatSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstreamformatswitch) |
|default void |[onPlayerStatusUpdate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate) |
|default void |[onPlayerStatusUpdate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate-2) |
|default void |[onStatistics](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstatistics) |
|default void |[onSnapshotComplete](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onsnapshotcomplete) |
|default void |[onRenderVideoFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onrendervideoframe) |
|default void |[onRenderAudioFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onrenderaudioframe) |
|default void |[onStreamFailedOpenSuperResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution) |
|default void |[onStreamFailedOpenSharpen](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstreamfailedopensharpen) |

## 说明

### onError

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onError(
    VeLivePlayer player,
    VeLivePlayerError error
)
```

当播放器发生错误时发生。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |VeLivePlayer |触发回调函数的播放器对象。 |
|error |VeLivePlayerError |错误消息。详情请参见 [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-android-api-errorcode#VeLivePlayerError)。 |

### onInfo

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onInfo(
    VeLivePlayer player,
    VeLivePlayerError error
)
```

当播放器遇到内部错误时触发。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |VeLivePlayer |触发回调的播放器对象。详情请参见 [VeLivePlayer](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer)。 |
|error |VeLivePlayerError |播放器信息。详情请参见 [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-android-api-errorcode#VeLivePlayerError)。 |

### onFirstVideoFrameRender

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onFirstVideoFrameRender(
    VeLivePlayer player,
    boolean isFirstFrame
)
```

在播放开始时，或播放期间重试后，渲染首个视频帧时发生。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |VeLivePlayer |触发回调函数的播放器对象。 |
|isFirstFrame |boolean |该视频帧是否为播放开始时渲染的首个视频帧。<br><br><br>* true：该视频帧是播放开始时渲染的首个视频帧；<br><br>* false：该视频帧是播放期间重试后渲染的首个视频帧。 |

### onFirstAudioFrameRender

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onFirstAudioFrameRender(
    VeLivePlayer player,
    boolean isFirstFrame
)
```

在播放开始时，或播放期间重试后，渲染首个音频帧时发生。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |VeLivePlayer |触发回调函数的播放器对象。 |
|isFirstFrame |boolean |该音频帧是否为播放开始时渲染的首个音频帧。<br><br><br>* true：该音频帧是播放开始时渲染的首个音频帧；<br><br>* false：该音频帧是播放期间重试后渲染的首个音频帧。 |

### onStallStart

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onStallStart(VeLivePlayer player)
```

播放卡顿开始时发生。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |VeLivePlayer |触发回调函数的播放器对象。 |

### onStallEnd

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onStallEnd(VeLivePlayer player)
```

播放卡顿停止时发生，即音频缓冲充足后恢复播放时。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |VeLivePlayer |触发回调函数的播放器对象。 |

### onVideoRenderStall

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onVideoRenderStall(
    VeLivePlayer player,
    long stallTime
)
```

视频渲染卡顿时发生。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |VeLivePlayer |触发回调函数的播放器对象。 |
|stallTime |long |卡顿时长，单位为毫秒。 |

### onAudioRenderStall

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onAudioRenderStall(
    VeLivePlayer player,
    long stallTime
)
```

音频渲染卡顿时发生。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |VeLivePlayer |触发回调函数的播放器对象。 |
|stallTime |long |卡顿时长，单位为毫秒。 |

### onResolutionSwitch

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onResolutionSwitch(
    VeLivePlayer player,
    VeLivePlayerResolution resolution,
    VeLivePlayerError error,
    VeLivePlayerResolutionSwitchReason reason
)
```

视频分辨率变化时发生。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |VeLivePlayer |触发回调函数的播放器对象。 |
|resolution |VeLivePlayerResolution |更新后的分辨率。详情请参见 [VeLivePlayerResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerResolution)。 |
|error |VeLivePlayerError |分辨率切换期间是否发生错误。详情请参见 [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-android-api-errorcode#VeLivePlayerError)。 |
|reason |VeLivePlayerResolutionSwitchReason |分辨率切换原因。详情请参见 [VeLivePlayerResolutionSwitchReason](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerResolutionSwitchReason)。 |

### onVideoSizeChanged

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onVideoSizeChanged(
    VeLivePlayer player,
    int width,
    int height
)
```

视频尺寸变化时发生。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |VeLivePlayer |触发回调函数的播放器对象。 |
|width |int |更新后的视频宽度，单位为像素。 |
|height |int |更新后的视频高度，单位为像素。 |

### onReceiveSeiMessage

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onReceiveSeiMessage(
    VeLivePlayer player,
    String message
)
```

字符串 SEI 消息回调。当播放器 SDK 收到 SEI 消息时，会触发此回调。需要在 `VeLivePlayerConfiguration` 中开启 `enableSei` 属性。开启 `enableBinarySei` 属性后，将不再发送字符串 SEI 消息。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |VeLivePlayer |触发回调函数的播放器对象。 |
|message |String |SEI 消息。 |

### onReceiveBinarySeiMessage

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onReceiveBinarySeiMessage(
    VeLivePlayer player,
    byte[] message
)
```

二进制 SEI 消息回调。当播放器 SDK 收到 SEI 消息时，会触发此回调。需要在 `VeLivePlayerConfiguration` 中开启 `enableBinarySei` 属性。开启 `enableBinarySei` 属性后，将不再发送字符串 SEI 消息。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |VeLivePlayer |触发回调函数的播放器对象。 |
|message |byte[] |SEI 消息。 |

### onMainBackupSwitch

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onMainBackupSwitch(
    VeLivePlayer player,
    VeLivePlayerStreamType streamType,
    VeLivePlayerError error
)
```

播放器在主流和备流之间切换时发生。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |VeLivePlayer |触发回调函数的播放器对象。 |
|streamType |VeLivePlayerStreamType |更新后的流类型。详情请参见 [VeLivePlayerStreamType](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerStreamType)。 |
|error |VeLivePlayerError |切换原因。详情请参见 [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-android-api-errorcode#VeLivePlayerError)。 |

### onStreamFormatSwitch

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onStreamFormatSwitch(
    VeLivePlayer player,
    VeLivePlayerFormat fromStreamFormat,
    VeLivePlayerFormat toStreamFormat,
    VeLivePlayerError error,
    Bundle extraInfo
)
```

播放器切换流格式时触发。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |VeLivePlayer |触发回调的播放器对象。详情请参见 [VeLivePlayer](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer)。 |
|fromStreamFormat |VeLivePlayerFormat |切换前的流格式。详情请参见 [VeLivePlayerFormat](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerFormat)。 |
|toStreamFormat |VeLivePlayerFormat |切换后的流格式。详情请参见 [VeLivePlayerFormat](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerFormat)。 |
|error |VeLivePlayerError |流格式切换原因。详情请参见 [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-android-api-errorcode#VeLivePlayerError)。 |
|extraInfo |Bundle |包含切换相关详细数据的附加信息。 |

### onPlayerStatusUpdate

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onPlayerStatusUpdate(
    VeLivePlayer player,
    VeLivePlayerStatus status
)
```

播放状态变化时发生。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |VeLivePlayer |播放状态发生变化的播放器。 |
|status |VeLivePlayerStatus |播放器更新后的状态。详情请参见 [VeLivePlayerStatus](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerStatus)。 |

### onPlayerStatusUpdate

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onPlayerStatusUpdate(
    VeLivePlayer player,
    VeLivePlayerStatus status,
    Bundle extraInfo
)
```

播放状态变化时发生。与 [onPlayerStatusUpdate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate) 相比，此回调通过 `extraInfo` 返回当前播放流的补充信息。

**输入参数**

|参数名称 |类型 |描述 |
|---|---|---|
|player |VeLivePlayer |播放状态发生变化的播放器。 |
|status |VeLivePlayerStatus |播放器更新后的状态。详情请参见 [VeLivePlayerStatus](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerStatus)。 |
|extraInfo |Bundle |当前播放流的补充信息 Bundle。该 Bundle 可能包含以下键：<br><br><br>* `url` (String)：当前正在播放的流的 URL。<br><br>* `all_resolution_urls` (Bundle)：所有分辨率的播放地址映射。`Key` 是分辨率标识，`Value` 是对应的播放 URL。仅当当前流是多分辨率流时，才存在此键。<br><br>* `resolution` (String)：当前正在播放的流的分辨率标识。仅当当前流是多分辨率流时，才存在此键。<br><br>* `enable_abr` (boolean)：是否启用自适应码率（ABR）。仅当当前流是多分辨率流时，才存在此键。有效值：<br><br>   * `true`：已启用。<br><br>   * `false`：已禁用。<br><br>* `enable_smooth_switch_resolution` (boolean)：是否启用平滑分辨率切换。仅当当前流是多分辨率流时，才存在此键。有效值：<br><br>   * `true`：已启用。<br><br>   * `false`：已禁用。<br><br>* `max_retry_count` (int)：当前流的最大重试次数。<br><br>* `retry_interval_time_ms` (int)：当前流的重试间隔，单位为毫秒。<br><br>* `priority` (int)：当前流在拉流列表中的优先级。 |

### onStatistics

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onStatistics(
    VeLivePlayer player,
    VeLivePlayerStatistics statistics
)
```

定期发生，用于上报当前拉流地址、码率和帧率等信息。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |VeLivePlayer |触发回调函数的播放器对象。 |
|statistics |VeLivePlayerStatistics |播放统计信息。详情请参见 [VeLivePlayerStatistics](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerStatistics)。 |

### onSnapshotComplete

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onSnapshotComplete(
    VeLivePlayer player,
    Bitmap bitmap
)
```

调用 [snapshot](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-snapshot) 后完成截图时发生。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |VeLivePlayer |触发回调函数的播放器对象。 |
|bitmap |Bitmap |截图的 Bitmap 对象。 |

### onRenderVideoFrame

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onRenderVideoFrame(
    VeLivePlayer player,
    VeLivePlayerVideoFrame videoFrame
)
```

播放器解码视频帧时发生。调用 [enableVideoFrameObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-enablevideoframeobserver) 可启用视频帧回调。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |VeLivePlayer |触发回调函数的播放器对象。 |
|videoFrame |VeLivePlayerVideoFrame |视频帧，包括像素格式、封装格式、视频宽高以及其他信息。详情请参见 [VeLivePlayerVideoFrame](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerVideoFrame)。 |

**注意事项**

如果使用纹理格式进行外部渲染，建议在回调线程中渲染视频。

### onRenderAudioFrame

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onRenderAudioFrame(
    VeLivePlayer player,
    VeLivePlayerAudioFrame audioFrame
)
```

播放器解码音频帧时发生。调用 [enableAudioFrameObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-enableaudioframeobserver) 可启用音频帧回调。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |VeLivePlayer |触发回调函数的播放器对象。 |
|audioFrame |VeLivePlayerAudioFrame |音频帧。详情请参见 [VeLivePlayerAudioFrame](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerAudioFrame)。 |

**注意事项**

回调返回的音频数据类型为 Float32，字节序为大端序。

### onStreamFailedOpenSuperResolution

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onStreamFailedOpenSuperResolution(
    VeLivePlayer player,
    VeLivePlayerError error
)
```

调用 [setEnableSuperResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setenablesuperresolution) 后，SDK 启用超分失败时发生。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |VeLivePlayer |触发回调函数的播放器对象。 |
|error |VeLivePlayerError |失败原因。详情请参见 [VeLivePlayerErrorCode](https://docs.byteplus.com/en/docs/24/docs-player-android-api-errorcode#VeLivePlayerErrorCode)。 |

### onStreamFailedOpenSharpen

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onStreamFailedOpenSharpen(
    VeLivePlayer player,
    VeLivePlayerError error
)
```

调用 [setEnableSharpen](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setenablesharpen) 后，SDK 启用锐化失败时发生。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|player |VeLivePlayer |触发回调函数的播放器对象。 |
|error |VeLivePlayerError |失败原因。详情请参见 VeLivePlayerErrorCode。 |
