---
title: "React Native 拉流 SDK：类型详情"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition-zh-CN"
---

<span id="licenseconfig"></span>
## LicenseConfig

类型：`interface`

<span id="22268e4d"></span>
### AppID

类型：`string`

<span id="a1b8862f"></span>
### AppName

类型：`string`

<span id="8e59eca9"></span>
### AppVersion

类型：`string`

<span id="2a5c2766"></span>
### AppChannel

类型：`string`

<span id="fd1837d7"></span>
### LicenseUri

类型：`{ android: string; ios: string; }`

**成员**


|名称 |类型 |接口行为 |
|---|---|---|
|android |`string` |Android 应用的 license 路径。 |
|ios |`string` |iOS 应用的 license 路径。 |


<span id="1e652764"></span>
### openLog

类型：`boolean | undefined`

<span id="b69a6b68"></span>
### UserUniqueID

类型：`string | undefined`

<span id="e0a44dd3"></span>
### PackageName

类型：`string | undefined`

<span id="59e43c39"></span>
### BundleID

类型：`string | undefined`

<span id="65235c62"></span>
## VeLivePlayerResolution

类型：`enum`

播放器分辨率。


|属性 |值 |接口行为 |
|---|---|---|
|VeLivePlayerResolutionOrigin |`0` |原始。 |
|VeLivePlayerResolutionUHD |`1` |超高清（UHD）。 |
|VeLivePlayerResolutionHD |`2` |高清（HD）。 |
|VeLivePlayerResolutionSD |`3` |标清（SD）。 |
|VeLivePlayerResolutionLD |`4` |低清（LD）。 |


<span id="f6547cab"></span>
## VeLivePlayerConfiguration

类型：`class`

播放器初始化配置。

<span id="fe0901c6"></span>
### enableSei

类型：`boolean`

是否启用 SEI 消息解析。默认值为 `false`。


* true：启用；

* false：禁用。


<span id="df72ece1"></span>
### enableHardwareDecode

类型：`boolean`

是否开启硬解。默认值为 `true`。启用硬解后，若播放器无法启动硬解或硬解失败，将自动切换为软解。


* true：启用；

* false：禁用。


<span id="290f3c15"></span>
### networkTimeoutMs

类型：`number`

网络超时时长，单位为毫秒。默认值为 `5000`。若播放器发送网络请求，在该时长内未收到服务器返回调用结果，则认为请求失败。

<span id="3a98bfb1"></span>
### retryIntervalTimeMs

类型：`number`

重试时间间隔，单位为毫秒。默认值为 `5000`。该变量仅在无备流时生效。


* 若无备流且回放中断，播放器会立即执行前三次重试。后续重试时，播放器会在每次尝试之间等待指定的时间间隔。

* 若存在备流，则该时间间隔不生效，所有重试均为即时执行。


<span id="408e6d5e"></span>
### retryMaxCount

类型：`number`

播放器在网络连接错误时自动重试的最大次数。默认值为 `5`。若值为 `0`，播放器不会自动重试。


* 若无备流，每次重试计为一次尝试。

* 存在备流时，每次主流与备流切换均计为一次重试。


<span id="3dd01afc"></span>
### enableLiveDNS

类型：`boolean`

是否启用本地 DNS 预取。默认值为 `false`。启用本地 DNS 预取可减少启动回放所需时间。若本地 DNS 预取异常，播放器可能无法正常工作。


* true：启用；

* false：禁用。


<span id="3722a3b3"></span>
### enableStatisticsCallback

类型：`boolean`

是否启用回放信息周期性回调。默认值为 `false`。更多回调统计信息请参见 [VeLivePlayerStatistics](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerstatistics-VeLivePlayerStatistics)。若 `enableStatisticsCallback` 为 `true` 且 [statisticsCallbackInterval](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#statisticsCallbackInterval) 大于 `0`，播放器会按指定间隔周期性上报播放器状态信息。


* true：启用；

* false：禁用。


<span id="42c645fb"></span>
### statisticsCallbackInterval

类型：`number`

周期性回调回放信息的时间间隔，单位为秒。默认值为 `5`。若 [enableStatisticsCallback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#enableStatisticsCallback) 为 `true` 且 `statisticsCallbackInterval` 大于 `0`，播放器会按指定间隔周期性上报播放器状态信息。

<span id="d1a34194"></span>
## VeLivePlayerFormat

类型：`enum`

直播流格式。


|属性 |值 |接口行为 |
|---|---|---|
|VeLivePlayerFormatFLV |`0` |FLV。 |
|VeLivePlayerFormatHLS |`1` |HLS。 |
|VeLivePlayerFormatRTM |`2` |实时媒体（RTM）。 |


<span id="09205021"></span>
## VeLivePlayerProtocol

类型：`enum`

传输协议。


|属性 |值 |接口行为 |
|---|---|---|
|VeLivePlayerProtocolTCP |`0` |TCP。 |
|VeLivePlayerProtocolQUIC |`1` |QUIC。 |
|VeLivePlayerProtocolTLS |`2` |TLS。 |


<span id="1697047e"></span>
## VeLivePlayerMirror

类型：`enum`

镜像选项。


|属性 |值 |接口行为 |
|---|---|---|
|VeLivePlayerMirrorNone |`0` |无镜像。 |
|VeLivePlayerMirrorHorizontal |`1` |水平镜像。 |
|VeLivePlayerMirrorVertical |`2` |垂直镜像。 |


<span id="f920d758"></span>
## VeLivePlayerVideoBufferType

类型：`enum`

视频数据封装格式。


|属性 |数值 |接口行为 |
|---|---|---|
|VeLivePlayerVideoBufferTypeUnknown |`0` |未知格式。 |
|VeLivePlayerVideoBufferTypeByteBuffer |`1` |ByteBuffer。 |
|VeLivePlayerVideoBufferTypeByteArray |`2` |ByteArray。 |
|VeLivePlayerVideoBufferTypeTexture |`3` |Texture。 |
|VeLivePlayerVideoBufferTypePixelBuffer |`5` |CVPixelBufferRef。 |
|VeLivePlayerVideoBufferTypeSampleBuffer |`6` |CVSampleBufferRef。 |
|VeLivePlayerVideoBufferTypeNSData |`7` |NSData。 |


<span id="01afecd2"></span>
## VeLivePlayerStatus

类型：`enum`

拉流播放器状态。


|属性 |数值 |接口行为 |
|---|---|---|
|VeLivePlayerStatusStopped |`3` |回放已停止。 |
|VeLivePlayerStatusPaused |`2` |回放已暂停。 |
|VeLivePlayerStatusPrepared |`0` |播放器已完成准备，正在等待渲染视频。 |
|VeLivePlayerStatusPlaying |`1` |回放正在进行中，表示首帧已渲染且播放器未遇到任何错误。 |
|VeLivePlayerStatusError |`4` |播放器遇到错误。 |


<span id="5c0fa055"></span>
## VeLivePlayerStreamData

类型：`class`

拉流地址配置。

<span id="5504a465"></span>
### enableABR

类型：`boolean`

是否启用自适应码率（ABR）。默认值为 `false`。


* true：启用；

* false：禁用。


<span id="44dc7c26"></span>
### enableMainBackupSwitch

类型：`boolean`

是否启用主流与备流切换。默认值为`false`。


* true：启用；

* false：禁用。


<span id="faaef3c9"></span>
### defaultResolution

类型：[VeLivePlayerResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerresolution)

默认分辨率。默认值为`VeLivePlayerResolutionOrigin`，表示原画。详情请参见[VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerresolution-VeLivePlayerResolution)。

<span id="e2f2349a"></span>
### defaultFormat

类型：[VeLivePlayerFormat](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerformat)

默认视频格式。默认值为`VeLivePlayerFormatFLV`。详情请参见[VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerformat-VeLivePlayerFormat)。

<span id="fbb7f54a"></span>
### defaultProtocol

类型：[VeLivePlayerProtocol](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerprotocol)

默认传输协议。默认值为`VeLivePlayerProtocolTCP`。详情请参见[VeLivePlayerProtocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerprotocol-VeLivePlayerProtocol)。

<span id="ac4718ec"></span>
### mainStreamList

类型：[VeLivePlayerStream](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerstream)`[]`

主流地址列表。详情请参见[VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerstreamdata-veliveplayerstream)。

<span id="2665c9ff"></span>
### backupStreamList

类型：[VeLivePlayerStream](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerstream)`[]`

备流地址列表。详情请参见[VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerstreamdata-veliveplayerstream)。

<span id="a39ca559"></span>
## VeLivePlayerStream

类型：`class`

拉流地址信息。

<span id="9246292c"></span>
### url

类型：`string`

拉流地址。

<span id="891004c9"></span>
### resolution

类型：[VeLivePlayerResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerresolution)

回放分辨率。详情请参见[VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerresolution-VeLivePlayerResolution)。

<span id="c51a333d"></span>
### bitrate

类型：`number`

回放码率，单位为 Kbps。

<span id="f3412c31"></span>
### format

类型：[VeLivePlayerFormat](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerformat)

直播流格式。详情请参见[VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerformat-VeLivePlayerFormat)。

<span id="e555376b"></span>
### android_streamType

类型：`$p_a.VeLivePlayerStreamType`

该流为主流还是备流。详情请参见[VeLivePlayerStreamType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerstreamtype-VeLivePlayerStreamType)。

<span id="cc5a63ce"></span>
## VeLivePlayerResolutionSwitchReason

类型：`enum`

视频分辨率变化原因。


|属性 |数值 |接口行为 |
|---|---|---|
|VeLivePlayerResolutionSwitchByAuto |`0` |分辨率通过自适应码率功能自动切换。 |
|VeLivePlayerResolutionSwitchByManual |`1` |调用[switchResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/1317626#veliveplayer-switchResolution)后分辨率发生变化。 |


<span id="d4e1b91a"></span>
## VeLivePlayerFillMode

类型：`enum`

播放器屏幕填充模式。


|属性 |数值 |接口行为 |
|---|---|---|
|VeLivePlayerFillModeAspectFit |`0` |显示完整视频。视频将均匀缩放，直到某一维度达到屏幕边缘。屏幕上剩余的空间将以黑色填充。 |
|VeLivePlayerFillModeFullFill |`1` |拉伸视频以填满屏幕。视频长宽比可能发生变化。 |
|VeLivePlayerFillModeAspectFill |`2` |均匀缩放视频直到屏幕被完全填满。视频部分内容可能会被裁剪。 |


<span id="14681414"></span>
## VeLivePlayerPixelFormat

类型：`enum`

视频帧像素格式。


|属性 |数值 |接口行为 |
|---|---|---|
|VeLivePlayerPixelFormatUnknown |`0` |未知格式。 |
|VeLivePlayerPixelFormatRGBA32 |`1` |RGBA8888。 |
|VeLivePlayerPixelFormatTexture |`2` |Texture。 |
|VeLivePlayerPixelFormatNV12 |`4` |NV12。 |
|VeLivePlayerPixelFormatI420 |`5` |YUVI420。 |
|VeLivePlayerPixelFormatBGRA32 |`6` |BGRA。 |


<span id="42dab9d5"></span>
## VeLivePlayerStatistics

类型：`class`

回放统计信息。

<span id="61826fbb"></span>
### url

类型：`string`

`Readonly`，当前拉流地址。

<span id="b7665147"></span>
### isHardwareDecode

类型：`boolean`

`Readonly`，是否使用硬解。


* true：使用硬解；

* false：未使用硬解。


<span id="b1a67af1"></span>
### videoCodec

类型：`string`

`Readonly`，视频编码格式。

<span id="ff1c2c2b"></span>
### stallTimeMs

类型：`number`

只读。自回放开始累计卡顿时长，单位为毫秒。

<span id="52ab55f5"></span>
### bandwidthEstimation

类型：`number`

`Readonly`。估算网络带宽，单位为 Kbps。

<span id="91cbeb50"></span>
### delayMs

类型：`number`

`Readonly`。当前回放延迟，单位为毫秒。

<span id="5b2b1e4d"></span>
### width

类型：`number`

`Readonly`，视频宽度，单位为像素。

<span id="82f859ce"></span>
### height

类型：`number`

`Readonly`，视频高度，单位为像素。

<span id="c17e971b"></span>
### fps

类型：`number`

`Readonly`，视频帧率，单位为 fps。

<span id="4b750f0d"></span>
### bitrate

类型：`number`

`Readonly`，下行码率，单位为 Kbps。

<span id="81991728"></span>
### videoBufferMs

类型：`number`

`Readonly`，视频缓冲区，单位为毫秒。

<span id="49e1695c"></span>
### audioBufferMs

类型：`number`

`Readonly`，音频缓冲区，单位为毫秒。

<span id="0cdc5e51"></span>
### format

类型：[VeLivePlayerFormat](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerformat)

`Readonly`，视频格式。

<span id="3499bbac"></span>
### protocol

类型：[VeLivePlayerProtocol](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerprotocol)

`Readonly`，直播流传输协议。

<span id="fece7704"></span>
## VeLivePlayerVideoFrame

类型：`class`

视频帧。

<span id="4dbce073"></span>
### bufferType

类型：[VeLivePlayerVideoBufferType](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayervideobuffertype)

封装格式。详情请参见[VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayervideobuffertype-VeLivePlayerVideoBufferType)。

<span id="50fa9b75"></span>
### pixelFormat

类型：[VeLivePlayerPixelFormat](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerpixelformat)

像素格式。详情请参见[VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerpixelformat-VeLivePlayerPixelFormat)。

<span id="ce5a457e"></span>
### width

类型：`number`

视频宽度，单位为像素。

<span id="b344efd5"></span>
### height

类型：`number`

视频高度，单位为像素。

<span id="ce308637"></span>
### pts

类型：`number`

视频帧渲染时间戳，单位为毫秒。

<span id="82d59e1c"></span>
### android_buffer

类型：`ArrayBuffer`

ByteBuffer 格式的视频数据。当设置[VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerpixelformat-VeLivePlayerPixelFormat)为`VeLivePlayerPixelFormatRGBA32`且[VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayervideobuffertype-VeLivePlayerVideoBufferType)为`VeLivePlayerVideoBufferTypeByteBuffer`时，SDK 返回此视频数据类型。

<span id="38e94a83"></span>
### data

类型：`ArrayBuffer`

ByteArray 格式的视频数据。当设置[VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerpixelformat-VeLivePlayerPixelFormat)为`VeLivePlayerPixelFormatRGBA32`且[VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayervideobuffertype-VeLivePlayerVideoBufferType)为`VeLivePlayerVideoBufferTypeByteArray`时，SDK 返回此视频数据类型。

<span id="9a3421e5"></span>
## VeLivePlayerStreamType

类型：`enum`

直播流类型。


|属性 |数值 |接口行为 |
|---|---|---|
|VeLivePlayerStreamTypeMain |`0` |主流。 |
|VeLivePlayerStreamTypeBackup |`1` |备流。 |


<span id="ebd2a745"></span>
## VeLivePlayerLogLevel

类型：`enum`

播放器输出日志级别。


|属性 |数值 |接口行为 |
|---|---|---|
|VeLivePlayerLogLevelVerbose |`0` |输出 VERBOSE、DEBUG、INFO、WARNING 和 ERROR 级别的日志。 |
|VeLivePlayerLogLevelDebug |`1` |输出 DEBUG、INFO、WARNING 和 ERROR 级别的日志。 |
|VeLivePlayerLogLevelInfo |`2` |输出 INFO、WARNING 和 ERROR 级别的日志。 |
|VeLivePlayerLogLevelWarn |`3` |输出 WARNING 和 ERROR 级别的日志。 |
|VeLivePlayerLogLevelError |`4` |输出 ERROR 级别的日志。 |
|VeLivePlayerLogLevelNone |`5` |禁用日志打印。 |


<span id="e9e49d32"></span>
## VeLivePlayerAudioFrame

类型：`class`

音频帧。

<span id="036d4e51"></span>
### bufferType

类型：[VeLivePlayerAudioBufferType](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayeraudiobuffertype)

音频数据封装格式。详情请参见[VeLivePlayerAudioBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayeraudiobuffertype-VeLivePlayerAudioBufferType)。

<span id="391ed2fc"></span>
### sampleRate

类型：`number`

音频采样率，单位为 Hz。

<span id="4edbca80"></span>
### channels

类型：`number`

音频通道数。


* 1：单声道；

* 2：立体声。


<span id="72e1439e"></span>
### bitDepth

类型：`number`

音频位深度。

<span id="9193b964"></span>
### pts

类型：`number`

音频渲染时间戳，单位为毫秒。

<span id="c89d0e21"></span>
### android_buffer

类型：`ArrayBuffer`

PCM 音频数据。

<span id="e9a450c4"></span>
### 采样数

类型：`number`

音频采样的数量。

<span id="a6083ccc"></span>
## VeLivePlayerAudioBufferType

类型：`enum`

音频的封装格式。


|属性 |数值 |接口行为 |
|---|---|---|
|VeLivePlayerAudioBufferTypeUnknown |`0` |未知格式。 |
|VeLivePlayerAudioBufferTypeByteArray |`1` |ByteArray。 |
|VeLivePlayerAudioBufferUnknown |`3` |未知格式。 |
|VeLivePlayerAudioBufferTypeSampleBuffer |`4` |CVSampleBufferRef。音频数据以 sample buffer 形式处理并渲染。 |
|VeLivePlayerAudioBufferTypeNSData |`5` |NSData。音频数据以 NSData 对象形式处理并渲染。 |


<span id="7877b1de"></span>
## VeLivePlayerRotation

类型：`enum`

视频顺时针旋转角度。


|属性 |数值 |接口行为 |
|---|---|---|
|VeLivePlayerRotation0 |`0` |无旋转。 |
|VeLivePlayerRotation90 |`1` |顺时针旋转 90 度。 |
|VeLivePlayerRotation180 |`2` |顺时针旋转 180 度。 |
|VeLivePlayerRotation270 |`3` |顺时针旋转 270 度。 |


<span id="8c318281"></span>
## InitOptions

类型：`interface`

播放器初始化的配置项。

<span id="97db5320"></span>
### enableSei

类型：`boolean`

是否已开启 SEI 消息解析。默认值为 `false`。


* true：已开启；

* false：未开启。


<span id="4028f347"></span>
### enableHardwareDecode

类型：`boolean`

是否已开启硬解。默认值为 `true`。当硬解已开启时，如果播放器无法启动硬解或硬解失败，播放器会自动切换为软解。


* true：已开启；

* false：未开启。


<span id="ab9aff33"></span>
### networkTimeoutMs

类型：`number`

网络超时时长，单位为毫秒。默认值为 `5000`。如果播放器发送网络请求，在该时长内未收到服务器的返回调用结果，则请求视为失败。

<span id="41b9ab3e"></span>
### retryIntervalTimeMs

类型：`number`

重试时间间隔，单位为毫秒。默认值为 `5000`。该变量仅在没有备流时生效。


* 若无备流且回放中断，播放器会立即进行前三次重试。后续重试时，播放器会在每次尝试之间等待指定的时间间隔。

* 若存在备流，则该时间间隔不生效，所有重试均为即时重试。


<span id="41b89fbd"></span>
### retryMaxCount

类型：`number`

播放器在网络连接错误时自动重试的最大次数。默认值为 `5`。若值为 `0`，播放器不会自动重试。


* 若无备流，每次重试计为一次尝试。

* 存在备流时，每次主流与备流切换均计为一次重试。


<span id="ba175414"></span>
### enableLiveDNS

类型：`boolean`

是否已开启本地 DNS 预解析。默认值为 `false`。已开启本地 DNS 预解析可减少启动回放所需时间。若本地 DNS 预解析出现异常，播放器可能无法正常工作。


* true：已开启；

* false：未开启。


<span id="bf2254dc"></span>
### enableStatisticsCallback

类型：`boolean`

是否已开启回放信息的周期性回调。默认值为 `false`。有关回调统计信息，参见 VeLivePlayerStatistics。若 `enableStatisticsCallback` 为 `true` 且 statisticsCallbackInterval 大于 `0`，播放器会按指定间隔周期性上报播放器状态信息。


* true：已开启；

* false：未开启。


<span id="ac0baf49"></span>
### statisticsCallbackInterval

类型：`number`

周期性回调回放信息的时间间隔，单位为秒。默认值为 `5`。若 [enableStatisticsCallback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#enableStatisticsCallback) 为 `true` 且 `statisticsCallbackInterval` 大于 `0`，播放器会按指定间隔周期性上报播放器状态信息。

<span id="dae2ea8d"></span>
### viewId

类型：`number`

播放器视图的 ID
