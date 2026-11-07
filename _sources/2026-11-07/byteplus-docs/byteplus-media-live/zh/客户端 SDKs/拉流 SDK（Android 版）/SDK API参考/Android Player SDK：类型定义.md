---
title: "Android Player SDK：类型定义"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype-zh-CN"
---

# VeLivePlayerResolution

```java
public static class com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution
```

播放器分辨率。

## 成员属性

|类型 |默认值 |名称 |
|---|---|---|
|String |"origin" |[VeLivePlayerResolutionOrigin](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution-veliveplayerresolutionorigin) |
|String |"uhd" |[VeLivePlayerResolutionUHD](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution-veliveplayerresolutionuhd) |
|String |"hd" |[VeLivePlayerResolutionHD](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution-veliveplayerresolutionhd) |
|String |"sd" |[VeLivePlayerResolutionSD](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution-veliveplayerresolutionsd) |
|String |"ld" |[VeLivePlayerResolutionLD](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution-veliveplayerresolutionld) |
|String |VeLivePlayerResolutionOrigin |[resolutionStr](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution-resolutionstr) |

## 成员函数

|返回值 |名称 |
|---|---|
|VeLivePlayerResolution |[VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution-veliveplayerresolution) |

## 说明

### VeLivePlayerResolutionOrigin

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin = "origin"
```

原始分辨率。

### VeLivePlayerResolutionUHD

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionUHD = "uhd"
```

超高清（UHD）。

### VeLivePlayerResolutionHD

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionHD = "hd"
```

高清（HD）。

### VeLivePlayerResolutionSD

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionSD = "sd"
```

标清（SD）。

### VeLivePlayerResolutionLD

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionLD = "ld"
```

低清（LD）。

### resolutionStr

```java
public String com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution.resolutionStr = VeLivePlayerResolutionOrigin
```

创建对象时传入的初始分辨率档位。

## 说明

### VeLivePlayerResolution

```java
public com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolution(String res)
```

构造方法。

**输入参数**

|名称 |类型 |说明 |
|---|---|---|
|res |String |分辨率档位。 |

# VeLivePlayerConfiguration

```java
public final class com.ss.videoarch.liveplayer.VeLivePlayerConfiguration
```

播放器初始化配置。

## 成员属性

|类型 |默认值 |名称 |
|---|---|---|
|boolean |false |[enableSei](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-enablesei) |
|boolean |false |[enableBinarySei](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-enablebinarysei) |
|boolean |true |[enableHardwareDecode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-enablehardwaredecode) |
|int |5_000 |[networkTimeoutMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-networktimeoutms) |
|int |5_000 |[retryIntervalTimeMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-retryintervaltimems) |
|int |5 |[retryMaxCount](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-retrymaxcount) |
|boolean |false |[enableLiveDNS](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-enablelivedns) |
|boolean |false |[enableStatisticsCallback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-enablestatisticscallback) |
|int |5 |[statisticsCallbackInterval](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-statisticscallbackinterval) |
|long |10_000 |[stallRetryTimeout](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-stallretrytimeout) |

## 说明

### enableSei

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.enableSei = false
```

是否开启字符串 SEI 消息解析。默认值为 `false`。

* true：开启；

* false：关闭。

### enableBinarySei

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.enableBinarySei = false
```

是否开启二进制 SEI 消息解析。默认值为 `false`。

* true：开启；

* false：关闭。

**说明**

开启二进制 SEI 后，不再发送字符串 SEI 回调。

### enableHardwareDecode

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.enableHardwareDecode = true
```

是否开启硬件解码。默认值为 `true`。开启硬件解码后，如果播放器启动硬件解码失败或硬件解码失败，播放器会自动切换为软件解码。

* true：开启；

* false：关闭。

### networkTimeoutMs

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.networkTimeoutMs = 5_000
```

网络超时时长，单位为毫秒。默认值为 `5000`。播放器发起网络请求后，如果在超时时长后未收到服务器响应，则认为网络请求失败。

### retryIntervalTimeMs

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.retryIntervalTimeMs = 5_000
```

重试间隔，单位为 ms。默认值为 `5000`。如需为每路流单独设置重试间隔，可以设置 [retryIntervalTimeMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStream-retryintervaltimems)。

### retryMaxCount

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.retryMaxCount = 5
```

播放器在网络连接错误时的最大重试次数。默认值为 `5`。如果取值为 `0`，播放器不会自动重试。如需为每路流单独设置最大重试次数，可以设置 [retryMaxCount](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStream-retrymaxcount)。

### enableLiveDNS

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.enableLiveDNS = false
```

是否开启本地 DNS 预解析。默认值为 `false`。开启本地 DNS 预解析可以减少起播所需时间。如果本地 DNS 预解析出现异常，播放器可能无法正常工作。

* true：开启；

* false：关闭。

### enableStatisticsCallback

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.enableStatisticsCallback = false
```

是否开启播放信息的周期性回调。默认值为 `false`。有关回调统计信息的更多信息，请参见 [VeLivePlayerStatistics](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics)。如果 `enableStatisticsCallback` 为 `true`，且 [statisticsCallbackInterval](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-statisticscallbackinterval) 大于 `0`，播放器会在指定时间间隔后周期性上报播放器状态信息。

* true：开启；

* false：关闭。

### statisticsCallbackInterval

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.statisticsCallbackInterval = 5
```

提供播放信息的周期性回调时间间隔，单位为秒。默认值为 `5`。如果 [enableStatisticsCallback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-enablestatisticscallback) 为 `true`，且 `statisticsCallbackInterval` 大于 `0`，播放器会在指定时间间隔后周期性上报播放器状态信息。

### stallRetryTimeout

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.stallRetryTimeout = 10_000
```

因卡顿停止重试的超时阈值。当卡顿时长超过此阈值时，播放器将停止重试。单位为 ms。默认值为 `10000`，即 10 秒。

# VeLivePlayerFormat

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerFormat
```

直播流的格式。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerFormatFLV |0 |FLV。 |
|VeLivePlayerFormatHLS |1 |HLS。 |
|VeLivePlayerFormatRTM |2 |实时媒体（RTM）。 |
|VeLivePlayerFormatCMAF |3 |CMAF 格式 |

# VeLivePlayerProtocol

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerProtocol
```

传输协议。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerProtocolTCP |0 |TCP。 |
|VeLivePlayerProtocolQUIC |1 |QUIC。 |
|VeLivePlayerProtocolTLS |2 |TLS。 |
|VeLivePlayerProtocolHTTP2 |3 |HTTP/2。 |
|VeLivePlayerProtocolDefault |4 |默认值。播放器会从拉流地址中自动识别网络协议。目前，仅支持自动识别 TCP 和 TLS 协议。对于 QUIC 或 HTTP/2 协议，请使用对应的值。 |

# VeLivePlayerMirror

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerMirror
```

镜像选项。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerMirrorNone |0 |不镜像。 |
|VeLivePlayerMirrorHorizontal |1 |水平镜像。 |
|VeLivePlayerMirrorVertical |2 |垂直镜像。 |

# VeLivePlayerVideoBufferType

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerVideoBufferType
```

视频数据的封装格式。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerVideoBufferTypeUnknown |0 |未知格式。 |
|VeLivePlayerVideoBufferTypeByteBuffer |1 |ByteBuffer。 |
|VeLivePlayerVideoBufferTypeByteArray |2 |ByteArray。 |
|VeLivePlayerVideoBufferTypeTexture |3 |Texture。 |

# VeLivePlayerStatus

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerStatus
```

直播播放器的状态。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerStatusStopped |0 |播放已停止。 |
|VeLivePlayerStatusPaused |1 |播放已暂停。 |
|VeLivePlayerStatusPrepared |2 |播放器已完成准备，正在等待渲染视频。 |
|VeLivePlayerStatusPlaying |3 |正在播放，表示首帧已渲染且播放器未发生错误。 |
|VeLivePlayerStatusError |4 |播放器发生错误。 |
|VeLivePlayerStatusStalled |5 |播放器已卡顿。 |

# VeLivePlayerLogConfig

```java
public class com.ss.videoarch.liveplayer.log.VeLivePlayerLogConfig
```

日志设置。

## 成员属性

|类型 |默认值 |名称 |
|---|---|---|
|VeLivePlayerLogLevel |VeLivePlayerLogLevel.VeLivePlayerLogLevelVerbose |[logLevel](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerLogConfig-loglevel) |

## 说明

### logLevel

```java
public VeLivePlayerLogLevel com.ss.videoarch.liveplayer.log.VeLivePlayerLogConfig.logLevel = VeLivePlayerLogLevel.VeLivePlayerLogLevelVerbose
```

输出日志级别。默认值为 `VeLivePlayerLogLevelDebug`。详情请参见 [VeLivePlayerLogLevel](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerLogLevel)。

# VeLivePlayerStreamData

```java
public class com.ss.videoarch.liveplayer.VeLivePlayerStreamData
```

拉流地址配置。

## 成员属性

|类型 |默认值 |名称 |
|---|---|---|
|boolean |false |[enableABR](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-enableabr) |
|boolean |false |[enableMainBackupSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-enablemainbackupswitch) |
|VeLivePlayerResolution |new VeLivePlayerResolution(VeLivePlayerResolution.VeLivePlayerResolutionOrigin) |[defaultResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-defaultresolution) |
|VeLivePlayerFormat |VeLivePlayerFormat.VeLivePlayerFormatFLV |[defaultFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-defaultformat) |
|VeLivePlayerProtocol |VeLivePlayerProtocol.VeLivePlayerProtocolTCP |[defaultProtocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-defaultprotocol) |
|List |null |[mainStreamList](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-mainstreamlist) |
|List |null |[backupStreamList](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-backupstreamlist) |
|boolean |false |[enableSmoothSwitchResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-enablesmoothswitchresolution) |

## 说明

### enableABR

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerStreamData.enableABR = false
```

是否开启自适应码率（ABR）。默认值为 `false`。

* true：开启；

* false：关闭。

### enableMainBackupSwitch

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerStreamData.enableMainBackupSwitch = false
```

是否开启主备流切换。默认值为 `false`。

* true：开启；

* false：关闭。

### defaultResolution

```java
public VeLivePlayerResolution com.ss.videoarch.liveplayer.VeLivePlayerStreamData.defaultResolution = new VeLivePlayerResolution(VeLivePlayerResolution.VeLivePlayerResolutionOrigin)
```

默认分辨率。默认值为 `VeLivePlayerResolutionOrigin`，表示原始分辨率。详情请参见 [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution)。

### defaultFormat

```java
public VeLivePlayerFormat com.ss.videoarch.liveplayer.VeLivePlayerStreamData.defaultFormat = VeLivePlayerFormat.VeLivePlayerFormatFLV
```

默认视频格式。默认值为 `VeLivePlayerFormatFLV`。详情请参见 [VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerFormat)。

### defaultProtocol

```java
public VeLivePlayerProtocol com.ss.videoarch.liveplayer.VeLivePlayerStreamData.defaultProtocol = VeLivePlayerProtocol.VeLivePlayerProtocolTCP
```

默认传输协议。默认值为 `VeLivePlayerProtocolTCP`。详情请参见 [VeLivePlayerProtocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProtocol)。

### mainStreamList

```java
public List<VeLivePlayerStream> com.ss.videoarch.liveplayer.VeLivePlayerStreamData.mainStreamList = null
```

主流地址列表。详情请参见 [VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-VeLivePlayerStream)。

### backupStreamList

```java
public List<VeLivePlayerStream> com.ss.videoarch.liveplayer.VeLivePlayerStreamData.backupStreamList = null
```

备流地址列表。详情请参见 [VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-VeLivePlayerStream)。

### enableSmoothSwitchResolution

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerStreamData.enableSmoothSwitchResolution = false
```

是否开启分辨率平滑切换。默认值为 `false`。开启后，当你调用 [switchResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-switchresolution) 方法手动切换分辨率时，SDK 会尝试平滑过渡，避免黑屏或卡顿。有效值：

* `true`：开启。

* `false`：关闭。

# VeLivePlayerResolutionSwitchReason

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolutionSwitchReason
```

视频分辨率发生变化的原因。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLiveplayerResolutionSwitchByAuto |0 |通过自适应码率（ABR）功能自动切换分辨率。 |
|VeLiveplayerResolutionSwitchByManual |1 |调用 [switchResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-switchresolution) 后更改分辨率。 |

# VeLivePlayerSupportResolutionSwitchError

```java
public static class com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError
```

清晰度档位切换错误。

## 成员属性

|类型 |默认值 |名称 |
|---|---|---|
|int |0 |[VeLivePlayerNoError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerSupportResolutionSwitchError-veliveplayernoerror) |
|int |\-1 |[VeLivePlayerErrorInvalidRes](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerSupportResolutionSwitchError-veliveplayererrorinvalidres) |
|int |\-2 |[VeLivePlayerErrorSameRes](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerSupportResolutionSwitchError-veliveplayererrorsameres) |
|int |\-3 |[VeLivePlayerErrorStatusInvalid](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerSupportResolutionSwitchError-veliveplayererrorstatusinvalid) |
|int |\-4 |[VeLivePlayerErrorResNotFound](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerSupportResolutionSwitchError-veliveplayererrorresnotfound) |
|int |\-5 |[VeLivePlayerErrorFormatNotSupport](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerSupportResolutionSwitchError-veliveplayererrorformatnotsupport) |
|int |\-6 |[VeLivePlayerErrorConfigNotSupport](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerSupportResolutionSwitchError-veliveplayererrorconfignotsupport) |

## 说明

### VeLivePlayerNoError

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError.VeLivePlayerNoError = 0
```

无错误。

### VeLivePlayerErrorInvalidRes

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError.VeLivePlayerErrorInvalidRes = -1
```

无效的清晰度档位。

### VeLivePlayerErrorSameRes

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError.VeLivePlayerErrorSameRes = -2
```

与当前清晰度档位相同。

### VeLivePlayerErrorStatusInvalid

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError.VeLivePlayerErrorStatusInvalid = -3
```

播放器状态不是 `prepare`。

### VeLivePlayerErrorResNotFound

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError.VeLivePlayerErrorResNotFound = -4
```

未找到对应的清晰度档位。

### VeLivePlayerErrorFormatNotSupport

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError.VeLivePlayerErrorFormatNotSupport = -5
```

当前播放格式不支持此清晰度档位。

### VeLivePlayerErrorConfigNotSupport

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError.VeLivePlayerErrorConfigNotSupport = -6
```

当前播放配置不支持此清晰度档位。

# VeLivePlayerStream

```java
public static class com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream
```

拉流地址的信息。

## 成员属性

|类型 |默认值 |名称 |
|---|---|---|
|String |null |[url](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStream-url) |
|VeLivePlayerResolution |new VeLivePlayerResolution(VeLivePlayerResolution.VeLivePlayerResolutionOrigin) |[resolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStream-resolution) |
|long |`-` |[bitrate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStream-bitrate) |
|VeLivePlayerFormat |VeLivePlayerFormat.VeLivePlayerFormatFLV |[format](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStream-format) |
|VeLivePlayerStreamType |VeLivePlayerStreamType.VeLivePlayerStreamTypeMain |[streamType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStream-streamtype) |
|int |0 |[priority](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStream-priority) |
|int |\-1 |[retryMaxCount](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStream-retrymaxcount) |
|int |\-1 |[retryIntervalTimeMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStream-retryintervaltimems) |
|VeLivePlayerProtocol |VeLivePlayerProtocol.VeLivePlayerProtocolDefault |[protocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStream-protocol) |

## 说明

### url

```java
public String com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.url = null
```

拉流地址。

### resolution

```java
public VeLivePlayerResolution com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.resolution = new VeLivePlayerResolution(VeLivePlayerResolution.VeLivePlayerResolutionOrigin)
```

播放分辨率。详情请参见 [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution)。

### bitrate

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.bitrate
```

播放码率，单位为 Kbps。

### format

```java
public VeLivePlayerFormat com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.format = VeLivePlayerFormat.VeLivePlayerFormatFLV
```

直播流的格式。详情请参见 [VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerFormat)。

### streamType

```java
public VeLivePlayerStreamType com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain
```

该流是主流还是备流。详情请参见 [VeLivePlayerStreamType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamType)。

### priority

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.priority = 0
```

流的优先级。取值必须为 `0`（默认）或正整数。值越大，优先级越高。

### retryMaxCount

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.retryMaxCount = -1
```

该流的最大重试尝试次数，表示播放尝试总次数（包括首次尝试）。例如，取值为 `3` 表示播放器在首次失败后最多重试 2 次。有效值：

* `-1`（默认）：使用 `VeLivePlayerConfiguration` 中的 [retryMaxCount](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-retrymaxcount) 值。

* `0`：不尝试播放此流。

* `> 0`：指定的总尝试次数。

### retryIntervalTimeMs

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.retryIntervalTimeMs = -1
```

重试间隔，单位为 ms。默认值为 `-1`。如果取值为 `-1`，播放器使用 `VeLivePlayerConfiguration` 中的 [retryIntervalTimeMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-retryintervaltimems) 值。

### protocol

```java
public VeLivePlayerProtocol com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.protocol = VeLivePlayerProtocol.VeLivePlayerProtocolDefault
```

传输协议。详情请参见 [VeLivePlayerProtocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProtocol)。

# VeLivePlayerFillMode

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerFillMode
```

播放器画面的填充模式。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerFillModeAspectFit |0 |显示完整视频。视频会等比缩放，直到视频的一个维度触达屏幕边界。屏幕上的剩余空间将以黑色填充。 |
|VeLivePlayerFillModeFullFill |1 |拉伸视频以填满屏幕。视频的宽高比可能会变化。 |
|VeLivePlayerFillModeAspectFill |2 |等比缩放视频，直到屏幕被完全填满。视频的一部分可能会被裁剪。 |

# VeLivePlayerPixelFormat

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerPixelFormat
```

视频帧的像素格式。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerPixelFormatUnknown |0 |未知格式。 |
|VeLivePlayerPixelFormatRGBA32 |1 |RGBA8888。 |
|VeLivePlayerPixelFormatTexture |2 |Texture。 |
|VeLivePlayerPixelFormatI420 |3 |YUV420P 格式。 |

# VeLivePlayerStatistics

```java
public class com.ss.videoarch.liveplayer.VeLivePlayerStatistics
```

播放统计信息。

## 成员属性

|类型 |默认值 |名称 |
|---|---|---|
|String |`-` |[url](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics-url) |
|boolean |`-` |[isHardwareDecode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics-ishardwaredecode) |
|String |`-` |[videoCodec](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics-videocodec) |
|long |`-` |[stallTimeMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics-stalltimems) |
|long |`-` |[bandwidthEstimation](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics-bandwidthestimation) |
|long |`-` |[delayMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics-delayms) |
|long |`-1` |[delayS2sMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics-delays2sms) |
|long |`-1` |[delayE2eMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics-delaye2ems) |
|long |`-1` |[delayS2eMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics-delays2ems) |
|int |`-` |[width](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics-width) |
|int |`-` |[height](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics-height) |
|float |`-` |[fps](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics-fps) |
|long |`-` |[bitrate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics-bitrate) |
|long |`-` |[videoBufferMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics-videobufferms) |
|long |`-` |[audioBufferMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics-audiobufferms) |
|VeLivePlayerFormat |`-` |[format](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics-format) |
|VeLivePlayerProtocol |`-` |[protocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics-protocol) |

## 说明

### url

```java
public String com.ss.videoarch.liveplayer.VeLivePlayerStatistics.url
```

当前拉流地址。

### isHardwareDecode

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerStatistics.isHardwareDecode
```

是否使用硬件解码。

* true：使用硬件解码；

* false：不使用硬件解码。

### videoCodec

```java
public String com.ss.videoarch.liveplayer.VeLivePlayerStatistics.videoCodec
```

视频的编码格式。

### stallTimeMs

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.stallTimeMs
```

自播放开始以来发生的卡顿累计时长，单位为毫秒。

### bandwidthEstimation

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.bandwidthEstimation
```

带宽估计，单位为 kbps。

### delayMs

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.delayMs
```

当前播放延迟，单位为毫秒。

### delayS2sMs

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.delayS2sMs = -1
```

服务器到服务器延迟，单位为毫秒。表示流从 MediaLive 推流侧边缘节点传输到 MediaLive 拉流侧边缘节点所用时间。当 SEI 消息不包含流到达推流侧边缘节点和拉流侧边缘节点时的服务器时间戳时，该值为 `-1`。

### delayE2eMs

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.delayE2eMs = -1
```

端到端延迟，单位为毫秒。表示从 Broadcast SDK 将时间戳写入 SEI 消息，到 Player SDK 在本地解析该 SEI 消息所用时间。精确计算依赖基于 NTP 的时钟同步。当 SEI 消息不包含 Broadcast SDK 写入的时间戳时，该值为 `-1`。

### delayS2eMs

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.delayS2eMs = -1
```

服务器到端延迟，单位为毫秒。表示从流到达 MediaLive 推流侧边缘节点，到 Player SDK 在本地解析 SEI 消息所用时间。精确计算依赖基于 NTP 的时钟同步。当 SEI 消息不包含流到达 MediaLive 推流侧边缘节点时的服务器时间戳时，该值为 `-1`。

### width

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerStatistics.width
```

视频宽度，单位为像素。

### height

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerStatistics.height
```

视频高度，单位为像素。

### fps

```java
public float com.ss.videoarch.liveplayer.VeLivePlayerStatistics.fps
```

视频帧率，单位为 fps。

### bitrate

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.bitrate
```

下行码率，单位为 Kbps。

### videoBufferMs

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.videoBufferMs
```

视频缓冲区，单位为毫秒。

### audioBufferMs

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.audioBufferMs
```

音频缓冲区，单位为毫秒。

### format

```java
public VeLivePlayerFormat com.ss.videoarch.liveplayer.VeLivePlayerStatistics.format
```

视频格式。更多信息，请参见 [VeLivePlayerFormat](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#veliveplayerformat)。

### protocol

```java
public VeLivePlayerProtocol com.ss.videoarch.liveplayer.VeLivePlayerStatistics.protocol
```

直播流的传输协议。更多信息，请参见 [VeLivePlayerProtocol](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#veliveplayerprotocol)。

# VeLivePlayerVideoFrame

```java
public class com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame
```

视频帧。

## 成员属性

|类型 |默认值 |名称 |
|---|---|---|
|VeLivePlayerVideoBufferType |`-` |[bufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-buffertype) |
|VeLivePlayerPixelFormat |`-` |[pixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-pixelformat) |
|int |`-` |[width](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-width) |
|int |`-` |[height](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-height) |
|long |`-` |[pts](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-pts) |
|VeLivePlayerVideoTexture |null |[texture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-texture) |
|ByteBuffer |null |[buffer](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-buffer) |
|byte[] |null |[data](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-data) |

## 说明

### bufferType

```java
public VeLivePlayerVideoBufferType com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.bufferType
```

封装格式。详情请参见 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoBufferType)。

### pixelFormat

```java
public VeLivePlayerPixelFormat com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.pixelFormat
```

像素格式。详情请参见 [VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerPixelFormat)。

### width

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.width
```

视频宽度，单位为像素。

### height

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.height
```

视频高度，单位为像素。

### pts

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.pts
```

表示视频帧渲染时间的时间戳，单位为毫秒。

### texture

```java
public VeLivePlayerVideoTexture com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.texture = null
```

用于 OpenGL 渲染的纹理数据。如果你将 [VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerPixelFormat) 设置为 `VeLivePlayerPixelFormatTexture`，并将 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoBufferType) 设置为 `VeLivePlayerVideoBufferTypeTexture`，SDK 将返回此视频数据类型。详情请参见 [VeLivePlayerVideoTexture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoTexture)。

### buffer

```java
public ByteBuffer com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.buffer = null
```

ByteBuffer 格式的视频数据。如果你将 [VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerPixelFormat) 设置为 `VeLivePlayerPixelFormatRGBA32`，并将 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoBufferType) 设置为 `VeLivePlayerVideoBufferTypeByteBuffer`，SDK 将返回此视频数据类型。

### data

```java
public byte [] com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.data = null
```

ByteArray 格式的视频数据。如果你将 [VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerPixelFormat) 设置为 `VeLivePlayerPixelFormatRGBA32`，并将 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoBufferType) 设置为 `VeLivePlayerVideoBufferTypeByteArray`，SDK 将返回此视频数据类型。

# VeLivePlayerVideoTexture

```java
public class com.ss.videoarch.liveplayer.VeLivePlayerVideoTexture
```

视频纹理。

## 成员属性

|类型 |默认值 |名称 |
|---|---|---|
|int |`-` |[texId](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoTexture-texid) |
|EGLContext |`-` |[eglContext](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoTexture-eglcontext) |

## 说明

### texId

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerVideoTexture.texId
```

视频纹理 ID。

### eglContext

```java
public EGLContext com.ss.videoarch.liveplayer.VeLivePlayerVideoTexture.eglContext
```

用于自定义渲染的 OpenGL ES 上下文。将 EGLContext 绑定到 GLSurfaceView 或 TextureView 后，可以在绑定的 View 上执行自定义 OpenGL ES 渲染。

# VeLivePlayerStreamType

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerStreamType
```

直播流的类型。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerStreamTypeMain |0 |主流。 |
|VeLivePlayerStreamTypeBackup |1 |备流。 |

# VeLivePlayerProperty

```java
public class com.ss.videoarch.liveplayer.VeLivePlayerProperty
```

高级配置。

## 成员属性

|类型 |默认值 |名称 |
|---|---|---|
|String |"VeLivePlayerKeySetParamsLowLatencyFLV" |[VeLivePlayerKeySetParamsLowLatencyFLV](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProperty-veliveplayerkeysetparamslowlatencyflv) |
|String |"VeLivePlayerKeySetParamsHttpHeaders" |[VeLivePlayerKeySetParamsHttpHeaders](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProperty-veliveplayerkeysetparamshttpheaders) |
|String |`"VeLivePlayerKeySetParamsRemoveQueryParams"` |[VeLivePlayerKeySetParamsRemoveQueryParams](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProperty-veliveplayerkeysetparamsremovequeryparams) |

## 说明

### VeLivePlayerKeySetParamsLowLatencyFLV

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerProperty.VeLivePlayerKeySetParamsLowLatencyFLV = "VeLivePlayerKeySetParamsLowLatencyFLV"
```

配置 FLV 低延迟设置（2–3 秒延迟）。详细用法请参见[播放低延迟 FLV 流](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-2#playing-low-latency-flv-streams)。

### VeLivePlayerKeySetParamsHttpHeaders

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerProperty.VeLivePlayerKeySetParamsHttpHeaders = "VeLivePlayerKeySetParamsHttpHeaders"
```

为播放器的 HTTP 请求设置自定义 HTTP 请求头。通常用于传递认证令牌、Cookie 或业务跟踪标识符等附加信息。详细用法请参见[自定义 HTTP 请求头](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-2#customizing-http-request-headers)。

### VeLivePlayerKeySetParamsRemoveQueryParams

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerProperty.VeLivePlayerKeySetParamsRemoveQueryParams = "VeLivePlayerKeySetParamsRemoveQueryParams"
```

设置是否移除 SDK 自动追加到拉流地址的查询参数。默认值为 `false`。开启后，拉流请求会移除 SDK 自动追加的查询参数，并保留原始拉流地址中已有的查询参数。详细用法请参见[移除 SDK 自动追加的查询参数](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-2?lang=en#removing-query-parameters-automatically-appended-by-the-sdk)。

* `true`：移除 SDK 自动追加的查询参数。

* `false`：保留 SDK 自动追加的查询参数。

# VeLivePlayerLogLevel

```java
public enum com.ss.videoarch.liveplayer.log.VeLivePlayerLogConfig.VeLivePlayerLogLevel
```

播放器的输出日志级别。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerLogLevelVerbose |0 |输出 VERBOSE、DEBUG、INFO、WARNING 和 ERROR 级别的日志。 |
|VeLivePlayerLogLevelDebug |1 |输出 DEBUG、INFO、WARNING 和 ERROR 级别的日志。 |
|VeLivePlayerLogLevelInfo |2 |输出 INFO、WARNING 和 ERROR 级别的日志。 |
|VeLivePlayerLogLevelWarn |3 |输出 WARNING 和 ERROR 级别的日志。 |
|VeLivePlayerLogLevelError |4 |输出 ERROR 级别的日志。 |
|VeLivePlayerLogLevelNone |5 |禁用日志打印。 |

# VeLivePlayerAudioFrame

```java
public class com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame
```

音频帧。

## 成员属性

|类型 |默认值 |名称 |
|---|---|---|
|VeLivePlayerAudioBufferType |`-` |[bufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-buffertype) |
|int |`-` |[sampleRate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-samplerate) |
|int |`-` |[channels](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-channels) |
|int |`-` |[bitDepth](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-bitdepth) |
|long |`-` |[pts](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-pts) |
|byte[] |null |[bufferArray](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-bufferarray) |
|ByteBuffer[] |null |[buffer](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-buffer) |
|int |`-` |[samples](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-samples) |

## 说明

### bufferType

```java
public VeLivePlayerAudioBufferType com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.bufferType
```

音频数据的封装格式。详情请参见 [VeLivePlayerAudioBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioBufferType)。

### sampleRate

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.sampleRate
```

音频采样率，单位为 Hz。

### channels

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.channels
```

音频声道数。

* 1：单声道；

* 2：立体声。

### bitDepth

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.bitDepth
```

音频位深。

### pts

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.pts
```

表示音频渲染时间的时间戳，单位为毫秒。

### bufferArray

```java
public byte [] com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.bufferArray = null
```

PCM 音频数据。byte[] 类型。

### buffer

```java
public ByteBuffer [] com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.buffer = null
```

PCM 音频数据。ByteBuffer[] 类型。

### samples

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.samples
```

音频采样数。

# VeLivePlayerAudioBufferType

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerAudioBufferType
```

音频的封装格式。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerAudioBufferTypeUnknown |0 |未知格式。 |
|VeLivePlayerAudioBufferTypeByteArray |1 |ByteArray。 |

# VeLivePlayerRotation

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerRotation
```

视频顺时针旋转角度。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerRotation0 |0 |不旋转。 |
|VeLivePlayerRotation90 |1 |顺时针旋转 90 度。 |
|VeLivePlayerRotation180 |2 |顺时针旋转 180 度。 |
|VeLivePlayerRotation270 |3 |顺时针旋转 270 度。 |

# VeLivePlayerStreamInfo

```java
public class com.ss.videoarch.liveplayer.hls.VeLivePlayerStreamInfo
```

HLS 流信息。

## 成员变量

|名称 |类型 |默认值 |
|---|---|---|
|[width](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamInfo-width) |int |\- |
|[height](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamInfo-height) |int |\- |
|[bandwidth](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamInfo-bandwidth) |int |\- |
|[url](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamInfo-url) |String |\- |

## 成员函数

|名称 |返回值 |
|---|---|
|[toString](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamInfo-tostring) |String |

## 变量说明

### width

```java
public int com.ss.videoarch.liveplayer.hls.VeLivePlayerStreamInfo.width
```

视频宽度，单位为像素。

### height

```java
public int com.ss.videoarch.liveplayer.hls.VeLivePlayerStreamInfo.height
```

视频高度，单位为像素。

### bandwidth

```java
public int com.ss.videoarch.liveplayer.hls.VeLivePlayerStreamInfo.bandwidth
```

流带宽，单位为比特每秒（bps）。

### url

```java
public String com.ss.videoarch.liveplayer.hls.VeLivePlayerStreamInfo.url
```

HLS 流的播放 URL。

## 函数说明

### toString

```java
public String com.ss.videoarch.liveplayer.hls.VeLivePlayerStreamInfo.toString()
```

将 HLS 流信息转换为字符串。

**返回值**

包含 HLS 流的视频宽度、视频高度、带宽和播放 URL 的字符串。
