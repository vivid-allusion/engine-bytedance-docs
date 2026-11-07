---
title: "Player SDK for React Native: Type definitions"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition"
---

<span id="licenseconfig"></span>
## LicenseConfig  

Type: `interface`

<span id="appid"></span>
### AppID  

Type: `string`

<span id="appname"></span>
### AppName  

Type: `string`

<span id="appversion"></span>
### AppVersion  

Type: `string`

<span id="appchannel"></span>
### AppChannel  

Type: `string`

<span id="licenseuri"></span>
### LicenseUri  

Type: `{ android: string; ios: string; }`

**Member**


|Name |Type |Description |
|---|---|---|
|android |`string` |The license path for the Android App. |
|ios |`string` |The license path for the iOS App. |


<span id="openlog"></span>
### openLog  

Type：`boolean | undefined`

<span id="useruniqueid"></span>
### UserUniqueID  

Type：`string | undefined`

<span id="packagename"></span>
### PackageName  

Type：`string | undefined`

<span id="bundleid"></span>
### BundleID  

Type：`string | undefined`

<span id="veliveplayerresolution"></span>
## VeLivePlayerResolution  

Type：`enum`

The player resolution.


|Property |Value |Description |
|---|---|---|
|VeLivePlayerResolutionOrigin |`0` |Original. |
|VeLivePlayerResolutionUHD |`1` |Ultra high definition (UHD). |
|VeLivePlayerResolutionHD |`2` |High definition (HD). |
|VeLivePlayerResolutionSD |`3` |Standard definition (SD). |
|VeLivePlayerResolutionLD |`4` |Low definition (LD). |


<span id="veliveplayerconfiguration"></span>
## VeLivePlayerConfiguration  

Type：`class`

The configurations for player initialization.

<span id="enablesei"></span>
### enableSei  

Type：`boolean`

Whether to enable the parsing of SEI messages. The default value is `false`.


* true: Enable;

* false: Disable.


<span id="enablehardwaredecode"></span>
### enableHardwareDecode  

Type：`boolean`

Whether to turn on hardware decoding. The default value is `true`. When hardware decoding is enabled, if the player fails to start hardware decoding or if hardware decoding fails, the player automatically switches to software decoding.


* true: Enable;

* false: Disable.


<span id="networktimeoutms"></span>
### networkTimeoutMs  

Type：`number`

Network timeout duration, in milliseconds. The default value is `5000`. If the player sends a network request and does not receive a response from the server within this duration, the request is considered to have failed.

<span id="retryintervaltimems"></span>
### retryIntervalTimeMs  

Type：`number`

The retry time interval, in milliseconds. The default value is `5000`. This variable takes effect only when there is no backup stream.


* If there is no backup stream and playback is interrupted, the player performs the first three retries immediately. For subsequent retries, the player waits for the specified time interval between each attempt.

* If a backup stream is present, this time interval does not apply, as all retries are immediate.


<span id="retrymaxcount"></span>
### retryMaxCount  

Type：`number`

The maximum number of automatic retries the player will attempt in case of a network connection error. The default value is `5`. If the value is `0`, the player will not automatically retry.


* If there is no backup stream, each retry counts as one attempt.

* In the presence of a backup stream, each switch between the primary stream and the backup stream will count as a retry attempt.


<span id="enablelivedns"></span>
### enableLiveDNS  

Type：`boolean`

Whether to enable local DNS prefetch. The default value is `false`. Enabling local DNS prefetch can reduce the time required to start playback. If an abnormality occurs with local DNS prefetch, the player may not function properly.


* true: Enable;

* false: Disable.


<span id="enablestatisticscallback"></span>
### enableStatisticsCallback  

Type：`boolean`

Whether to enable periodic callbacks for playback information. The default value is `false`. Refer to [VeLivePlayerStatistics](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerstatistics-VeLivePlayerStatistics) for more information on callback statistics. If `enableStatisticsCallback` is `true` and [statisticsCallbackInterval](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#statisticsCallbackInterval) is greater than `0`, the player will periodically report player status information at the specified interval.


* true: Enable;

* false: Disable.


<span id="statisticscallbackinterval"></span>
### statisticsCallbackInterval  

Type：`number`

The time interval for periodic callbacks that provide playback information, in seconds. The default value is `5`. If [enableStatisticsCallback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#enableStatisticsCallback) is `true` and `statisticsCallbackInterval` is greater than `0`, the player will periodically report player status information at the specified interval.

<span id="veliveplayerformat"></span>
## VeLivePlayerFormat  

Type：`enum`

The format of the live stream.


|Property |Value |Description |
|---|---|---|
|VeLivePlayerFormatFLV |`0` |FLV. |
|VeLivePlayerFormatHLS |`1` |HLS. |
|VeLivePlayerFormatRTM |`2` |Real Time Media (RTM). |


<span id="veliveplayerprotocol"></span>
## VeLivePlayerProtocol  

Type：`enum`

The transmission protocol.


|Property |Value |Description |
|---|---|---|
|VeLivePlayerProtocolTCP |`0` |TCP. |
|VeLivePlayerProtocolQUIC |`1` |QUIC. |
|VeLivePlayerProtocolTLS |`2` |TLS. |


<span id="veliveplayermirror"></span>
## VeLivePlayerMirror  

Type：`enum`

The mirroring option.


|Property |Value |Description |
|---|---|---|
|VeLivePlayerMirrorNone |`0` |No mirroring. |
|VeLivePlayerMirrorHorizontal |`1` |Horizontal mirroring. |
|VeLivePlayerMirrorVertical |`2` |Vertical mirroring. |


<span id="veliveplayervideobuffertype"></span>
## VeLivePlayerVideoBufferType  

Type：`enum`

The encapsulation format of the video data.


|Property |Value |Description |
|---|---|---|
|VeLivePlayerVideoBufferTypeUnknown |`0` |Unknown format. |
|VeLivePlayerVideoBufferTypeByteBuffer |`1` |ByteBuffer. |
|VeLivePlayerVideoBufferTypeByteArray |`2` |ByteArray. |
|VeLivePlayerVideoBufferTypeTexture |`3` |Texture. |
|VeLivePlayerVideoBufferTypePixelBuffer |`5` |CVPixelBufferRef. |
|VeLivePlayerVideoBufferTypeSampleBuffer |`6` |CVSampleBufferRef. |
|VeLivePlayerVideoBufferTypeNSData |`7` |NSData. |


<span id="veliveplayerstatus"></span>
## VeLivePlayerStatus  

Type：`enum`

The status of the live player.


|Property |Value |Description |
|---|---|---|
|VeLivePlayerStatusStopped |`3` |The playback is stopped. |
|VeLivePlayerStatusPaused |`2` |The playback is paused. |
|VeLivePlayerStatusPrepared |`0` |The player has finished preparing and is waiting to render the video. |
|VeLivePlayerStatusPlaying |`1` |Playback is currently in progress, meaning that the first frame has been rendered and the player has not encountered any errors. |
|VeLivePlayerStatusError |`4` |The player has encountered an error. |


<span id="veliveplayerstreamdata"></span>
## VeLivePlayerStreamData  

Type：`class`

The configurations for the pull stream addresses.

<span id="enableabr"></span>
### enableABR  

Type：`boolean`

Whether to enable adaptive bitrate (ABR). The default value is `false`.


* true: Enable;

* false: Disable.


<span id="enablemainbackupswitch"></span>
### enableMainBackupSwitch  

Type：`boolean`

Whether to enable switching between primary and backup streams. The default value is `false`.


* true: Enable;

* false: Disable.


<span id="defaultresolution"></span>
### defaultResolution  

Type：[VeLivePlayerResolution](https://docs.byteplus.com/en/docs/24/27549#veliveplayerresolution)

The default resolution. The default value is `VeLivePlayerResolutionOrigin`, which indicates the original resolution. See [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerresolution-VeLivePlayerResolution) for details.

<span id="defaultformat"></span>
### defaultFormat  

Type：[VeLivePlayerFormat](https://docs.byteplus.com/en/docs/24/27549#veliveplayerformat)

The default video format. The default value is `VeLivePlayerFormatFLV`. See [VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerformat-VeLivePlayerFormat) for details.

<span id="defaultprotocol"></span>
### defaultProtocol  

Type：[VeLivePlayerProtocol](https://docs.byteplus.com/en/docs/24/27549#veliveplayerprotocol)

The default transmission protocol. The default value is `VeLivePlayerProtocolTCP`. See [VeLivePlayerProtocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerprotocol-VeLivePlayerProtocol) for details.

<span id="mainstreamlist"></span>
### mainStreamList  

Type：[VeLivePlayerStream](https://docs.byteplus.com/en/docs/24/27549#veliveplayerstream)`[]`

A list of main stream addresses. See [VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerstreamdata-veliveplayerstream) for details.

<span id="backupstreamlist"></span>
### backupStreamList  

Type：[VeLivePlayerStream](https://docs.byteplus.com/en/docs/24/27549#veliveplayerstream)`[]`

A list of backup stream addresses. See [VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerstreamdata-veliveplayerstream) for details.

<span id="veliveplayerstream"></span>
## VeLivePlayerStream  

Type：`class`

The information about a pull stream address.

<span id="url"></span>
### url  

Type：`string`

The pull stream address.

<span id="resolution"></span>
### resolution  

Type：[VeLivePlayerResolution](https://docs.byteplus.com/en/docs/24/27549#veliveplayerresolution)

The playback resolution. For details, see [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerresolution-VeLivePlayerResolution).

<span id="bitrate"></span>
### bitrate  

Type：`number`

The playback bitrate, in Kbps.

<span id="format"></span>
### format  

Type：[VeLivePlayerFormat](https://docs.byteplus.com/en/docs/24/27549#veliveplayerformat)

The format of the live stream. See [VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerformat-VeLivePlayerFormat) for details.

<span id="android-streamtype"></span>
### android_streamType  

Type：`$p_a.VeLivePlayerStreamType`

Whether the stream is a main or backup stream. See [VeLivePlayerStreamType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerstreamtype-VeLivePlayerStreamType) for details.

<span id="veliveplayerresolutionswitchreason"></span>
## VeLivePlayerResolutionSwitchReason  

Type：`enum`

The reason why the video resolution has changed.


|Property |Value |Description |
|---|---|---|
|VeLivePlayerResolutionSwitchByAuto |`0` |The resolution is switched automatically through the adaptive bitrate (ABR) feature. |
|VeLivePlayerResolutionSwitchByManual |`1` |The resolution is changed after [switchResolution](https://docs.byteplus.com/en/docs/24/1317626#veliveplayer-switchResolution) is called. |


<span id="veliveplayerfillmode"></span>
## VeLivePlayerFillMode  

Type：`enum`

The fill mode of the player screen.


|Property |Value |Description |
|---|---|---|
|VeLivePlayerFillModeAspectFit |`0` |Display the full video. The video is uniformly scaled until one dimension of the video reaches the edge of the screen. Any remaining space on the screen will be filled with black. |
|VeLivePlayerFillModeFullFill |`1` |Stretch the video to fill the screen. The aspect ratio of the video might change. |
|VeLivePlayerFillModeAspectFill |`2` |Uniformly scale the video until the screen is completely filled. Part of the video may be cropped. |


<span id="veliveplayerpixelformat"></span>
## VeLivePlayerPixelFormat  

Type：`enum`

The pixel format of the video frame.


|Property |Value |Description |
|---|---|---|
|VeLivePlayerPixelFormatUnknown |`0` |Unknown format. |
|VeLivePlayerPixelFormatRGBA32 |`1` |RGBA8888. |
|VeLivePlayerPixelFormatTexture |`2` |Texture. |
|VeLivePlayerPixelFormatNV12 |`4` |NV12. |
|VeLivePlayerPixelFormatI420 |`5` |YUVI420. |
|VeLivePlayerPixelFormatBGRA32 |`6` |BGRA. |


<span id="veliveplayerstatistics"></span>
## VeLivePlayerStatistics  

Type：`class`

The playback statistics.

<span id="url"></span>
### url  

Type：`string`

`Readonly`, The current pull stream address.

<span id="ishardwaredecode"></span>
### isHardwareDecode  

Type：`boolean`

`Readonly`, Whether hardware decoding is used.


* true: Hardware decoding is used;

* false: Hardware decoding is not used.


<span id="videocodec"></span>
### videoCodec  

Type：`string`

`Readonly`, The encoding format of the video.

<span id="stalltimems"></span>
### stallTimeMs  

Type：`number`

Readonly. The cumulative stutter duration since playback began, in milliseconds.

<span id="bandwidthestimation"></span>
### bandwidthEstimation  

Type：`number`

`Readonly`. The estimated network bandwidth, in Kbps.

<span id="c042a592"></span>
### delayMs

Type：`number`

`Readonly`. The current playback latency, in milliseconds.

<span id="width"></span>
### width  

Type：`number`

`Readonly`, The width of the video, in pixels.

<span id="height"></span>
### height  

Type：`number`

`Readonly`, The height of the video, in pixels.

<span id="fps"></span>
### fps  

Type：`number`

`Readonly`, The frame rate of the video, in fps.

<span id="bitrate"></span>
### bitrate  

Type：`number`

`Readonly`, The downlink bitrate, in Kbps.

<span id="videobufferms"></span>
### videoBufferMs  

Type：`number`

`Readonly`, The video buffer, in milliseconds.

<span id="audiobufferms"></span>
### audioBufferMs  

Type：`number`

`Readonly`, The audio buffer, in milliseconds.

<span id="format"></span>
### format  

Type：[VeLivePlayerFormat](https://docs.byteplus.com/en/docs/24/27549#veliveplayerformat)

`Readonly`, The video format.

<span id="protocol"></span>
### protocol  

Type：[VeLivePlayerProtocol](https://docs.byteplus.com/en/docs/24/27549#veliveplayerprotocol)

`Readonly`, The transmission protocol of the live stream.

<span id="veliveplayervideoframe"></span>
## VeLivePlayerVideoFrame  

Type：`class`

The video frame.

<span id="buffertype"></span>
### bufferType  

Type：[VeLivePlayerVideoBufferType](https://docs.byteplus.com/en/docs/24/27549#veliveplayervideobuffertype)

The encapsulation format. See [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayervideobuffertype-VeLivePlayerVideoBufferType) for details.

<span id="pixelformat"></span>
### pixelFormat  

Type：[VeLivePlayerPixelFormat](https://docs.byteplus.com/en/docs/24/27549#veliveplayerpixelformat)

The pixel format. See [VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerpixelformat-VeLivePlayerPixelFormat) for details.

<span id="width"></span>
### width  

Type：`number`

The video width, in pixels.

<span id="height"></span>
### height  

Type：`number`

The video height, in pixels.

<span id="pts"></span>
### pts  

Type：`number`

The timestamp indicating the time when the video frame is rendered, in milliseconds.

<span id="android-buffer"></span>
### android_buffer  

Type：`ArrayBuffer`

The video data in ByteBuffer format. The SDK returns this video data type if you set [VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerpixelformat-VeLivePlayerPixelFormat) to `VeLivePlayerPixelFormatRGBA32` and set [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayervideobuffertype-VeLivePlayerVideoBufferType) to `VeLivePlayerVideoBufferTypeByteBuffer`.

<span id="data"></span>
### data  

Type：`ArrayBuffer`

The video data in ByteArray format. The SDK returns this video data type if you set [VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerpixelformat-VeLivePlayerPixelFormat) to `VeLivePlayerPixelFormatRGBA32` and set [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayervideobuffertype-VeLivePlayerVideoBufferType) to `VeLivePlayerVideoBufferTypeByteArray`.

<span id="veliveplayerstreamtype"></span>
## VeLivePlayerStreamType  

Type：`enum`

The type of the live stream.


|Property |Value |Description |
|---|---|---|
|VeLivePlayerStreamTypeMain |`0` |The primary stream. |
|VeLivePlayerStreamTypeBackup |`1` |The backup stream. |


<span id="veliveplayerloglevel"></span>
## VeLivePlayerLogLevel  

Type：`enum`

The output log level of the player.


|Property |Value |Description |
|---|---|---|
|VeLivePlayerLogLevelVerbose |`0` |Output logs at the VERBOSE, DEBUG, INFO, WARNING, and ERROR levels. |
|VeLivePlayerLogLevelDebug |`1` |Output logs at the DEBUG, INFO, WARNING, and ERROR levels. |
|VeLivePlayerLogLevelInfo |`2` |Output logs at the INFO, WARNING, and ERROR levels. |
|VeLivePlayerLogLevelWarn |`3` |Output logs at the WARNING and ERROR levels. |
|VeLivePlayerLogLevelError |`4` |Output logs at the ERROR level. |
|VeLivePlayerLogLevelNone |`5` |Disable log printing. |


<span id="veliveplayeraudioframe"></span>
## VeLivePlayerAudioFrame  

Type：`class`

The audio frame.

<span id="buffertype"></span>
### bufferType  

Type：[VeLivePlayerAudioBufferType](https://docs.byteplus.com/en/docs/24/27549#veliveplayeraudiobuffertype)

The encapsulation format of the audio data. See [VeLivePlayerAudioBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayeraudiobuffertype-VeLivePlayerAudioBufferType) for details.

<span id="samplerate"></span>
### sampleRate  

Type：`number`

The audio sample rate, in Hz.

<span id="channels"></span>
### channels  

Type：`number`

The number of audio channels.


* 1: Mono;

* 2: Stereo.


<span id="bitdepth"></span>
### bitDepth  

Type：`number`

The audio bit depth.

<span id="pts"></span>
### pts  

Type：`number`

The timestamp indicating the time when the audio is rendered, in milliseconds.

<span id="android-buffer"></span>
### android_buffer  

Type：`ArrayBuffer`

The PCM audio data.

<span id="samples"></span>
### samples  

Type：`number`

The number of audio samples.

<span id="veliveplayeraudiobuffertype"></span>
## VeLivePlayerAudioBufferType  

Type：`enum`

The encapsulation format of the audio.


|Property |Value |Description |
|---|---|---|
|VeLivePlayerAudioBufferTypeUnknown |`0` |Unknown format. |
|VeLivePlayerAudioBufferTypeByteArray |`1` |ByteArray. |
|VeLivePlayerAudioBufferUnknown |`3` |Unknown format. |
|VeLivePlayerAudioBufferTypeSampleBuffer |`4` |CVSampleBufferRef. The audio data is processed and rendered as sample buffers. |
|VeLivePlayerAudioBufferTypeNSData |`5` |NSData. The audio data is processed and rendered as NSData objects. |


<span id="veliveplayerrotation"></span>
## VeLivePlayerRotation  

Type：`enum`

The clockwise video rotation angle.


|Property |Value |Description |
|---|---|---|
|VeLivePlayerRotation0 |`0` |No rotation. |
|VeLivePlayerRotation90 |`1` |Rotate 90 degrees clockwise. |
|VeLivePlayerRotation180 |`2` |Rotate 180 degrees clockwise. |
|VeLivePlayerRotation270 |`3` |Rotate 270 degrees clockwise. |


<span id="initoptions"></span>
## InitOptions  

Type：`interface`

The configurations for player initialization.

<span id="enablesei"></span>
### enableSei  

Type：`boolean`

Whether to enable the parsing of SEI messages. The default value is `false`.


* true: Enable;

* false: Disable.


<span id="enablehardwaredecode"></span>
### enableHardwareDecode  

Type：`boolean`

Whether to turn on hardware decoding. The default value is `true`. When hardware decoding is enabled, if the player fails to start hardware decoding or if hardware decoding fails, the player automatically switches to software decoding.


* true: Enable;

* false: Disable.


<span id="networktimeoutms"></span>
### networkTimeoutMs  

Type：`number`

Network timeout duration, in milliseconds. The default value is `5000`. If the player sends a network request and does not receive a response from the server within this duration, the request is considered to have failed.

<span id="retryintervaltimems"></span>
### retryIntervalTimeMs  

Type：`number`

The retry time interval, in milliseconds. The default value is `5000`. This variable takes effect only when there is no backup stream.


* If there is no backup stream and playback is interrupted, the player performs the first three retries immediately. For subsequent retries, the player waits for the specified time interval between each attempt.

* If a backup stream is present, this time interval does not apply, as all retries are immediate.


<span id="retrymaxcount"></span>
### retryMaxCount  

Type：`number`

The maximum number of automatic retries the player will attempt in case of a network connection error. The default value is `5`. If the value is `0`, the player will not automatically retry.


* If there is no backup stream, each retry counts as one attempt.

* In the presence of a backup stream, each switch between the primary stream and the backup stream will count as a retry attempt.


<span id="enablelivedns"></span>
### enableLiveDNS  

Type：`boolean`

Whether to enable local DNS prefetch. The default value is `false`. Enabling local DNS prefetch can reduce the time required to start playback. If an abnormality occurs with local DNS prefetch, the player may not function properly.


* true: Enable;

* false: Disable.


<span id="enablestatisticscallback"></span>
### enableStatisticsCallback  

Type：`boolean`

Whether to enable periodic callbacks for playback information. The default value is `false`. Refer to VeLivePlayerStatistics for more information on callback statistics. If `enableStatisticsCallback` is `true` and statisticsCallbackInterval is greater than `0`, the player will periodically report player status information at the specified interval.


* true: Enable;

* false: Disable.


<span id="statisticscallbackinterval"></span>
### statisticsCallbackInterval  

Type：`number`

The time interval for periodic callbacks that provide playback information, in seconds. The default value is `5`. If [enableStatisticsCallback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#enableStatisticsCallback) is `true` and `statisticsCallbackInterval` is greater than `0`, the player will periodically report player status information at the specified interval.

<span id="viewid"></span>
### viewId  

Type：`number`

The ID of the player view
