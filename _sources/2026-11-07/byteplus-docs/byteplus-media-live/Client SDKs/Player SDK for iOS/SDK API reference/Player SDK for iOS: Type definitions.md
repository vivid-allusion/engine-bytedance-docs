---
title: "Player SDK for iOS: Type definitions"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition"
---

<span id="VeLivePlayerResolutionSwitchReason"></span>
# VeLivePlayerResolutionSwitchReason

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerResolutionSwitchReason
)
```


The reason why the video resolution has changed.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerResolutionSwitchByAuto |0 |The resolution is switched automatically through the adaptive bitrate (ABR) feature. |
|VeLivePlayerResolutionSwitchByManual |1 |The resolution is changed after [switchResolution:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-switchresolution) is called. |


<span id="VeLivePlayerConfiguration"></span>
# VeLivePlayerConfiguration

```objectivec
@interface VeLivePlayerConfiguration : NSObject
```


The configurations for player initialization.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[enableSei](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-enablesei) |
|BOOL |[enableBinarySei](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-enablebinarysei) |
|BOOL |[enableHardwareDecode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-enablehardwaredecode) |
|BOOL |[enableLiveDNS](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-enablelivedns) |
|BOOL |[enableStatisticsCallback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-enablestatisticscallback) |
|NSInteger |[statisticsCallbackInterval](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-statisticscallbackinterval) |
|NSInteger |[networkTimeoutMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-networktimeoutms) |
|NSInteger |[retryIntervalTimeMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-retryintervaltimems) |
|NSInteger |[retryMaxCount](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-retrymaxcount) |
|NSInteger |[stallRetryTimeout](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-stallretrytimeout) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[init](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-init) |


<span id="instructions"></span>
## Instructions

<span id="VeLivePlayerConfiguration-enablesei"></span>
### enableSei

```objectivec
@property (nonatomic, assign) BOOL enableSei;
```


Whether to enable the parsing of string SEI messages. The default value is `NO`.


* `YES`: Enable;

* `NO`: Disable.

    &nbsp;


<span id="enablebinarysei"></span>
### enableBinarySei

```objectivec
@property (nonatomic, assign) BOOL enableBinarySei;
```


Whether to enable the parsing of binary SEI messages. The default value is `NO`.


* `YES`: Enable;

* `NO`: Disable.


**Notes**

After binary SEI is enabled, callbacks for string SEI will no longer be sent.

<span id="VeLivePlayerConfiguration-enablehardwaredecode"></span>
### enableHardwareDecode

```objectivec
@property (nonatomic, assign) BOOL enableHardwareDecode;
```


Whether to turn on hardware decoding. The default value is `YES`. When hardware decoding is enabled, if the player fails to start hardware decoding or if hardware decoding fails, the player automatically switches to software decoding.


* `YES`: Enable;

* `NO`: Disable.

    &nbsp;


<span id="enablelivedns"></span>
### enableLiveDNS

```objectivec
@property (nonatomic, assign) BOOL enableLiveDNS;
```


Whether to enable local DNS prefetch. The default value is `NO`. Enabling local DNS prefetch can reduce the time required to start playback. If an abnormality occurs with local DNS prefetch, the player may not function properly.


* `YES`: Enable;

* `NO`: Disable.

    &nbsp;


<span id="enablestatisticscallback"></span>
### enableStatisticsCallback

```objectivec
@property (nonatomic, assign) BOOL enableStatisticsCallback;
```


Whether to enable periodic callbacks for playback information. The default value is `NO`. Refer to [VeLivePlayerStatistics](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics) for more information on callback statistics. If `enableStatisticsCallback` is `YES` and [statisticsCallbackInterval](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-statisticscallbackinterval) is greater than `0`, the player will periodically report the player status information after the specified time interval.


* `YES`: Enable;

* `NO`: Disable.

    &nbsp;


<span id="statisticscallbackinterval"></span>
### statisticsCallbackInterval

```objectivec
@property (nonatomic, assign) NSInteger statisticsCallbackInterval;
```


The time interval for periodic callbacks that provide playback information, in seconds. The default value is `5`. If enableStatisticsCallback is `YES` and [enableStatisticsCallback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-enablestatisticscallback) is greater than `0`, the player will periodically report the player status information after the specified time interval.

<span id="VeLivePlayerConfiguration-networktimeoutms"></span>
### networkTimeoutMs

```objectivec
@property (nonatomic, assign) NSInteger networkTimeoutMs;
```


Network timeout duration in milliseconds. The default value is `5000`. Once the player sends a network request, if the player does not receive a response from the server after the timeout duration, the network request is considered to have failed.

<span id="VeLivePlayerConfiguration-retryintervaltimems"></span>
### retryIntervalTimeMs

```objectivec
@property (nonatomic, assign) NSInteger retryIntervalTimeMs;
```


The retry interval, in ms. The default value is `5000`. To set a separate retry interval for each stream, you can set [retryIntervalTimeMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-retryintervaltimems).

<span id="VeLivePlayerConfiguration-retrymaxcount"></span>
### retryMaxCount

```objectivec
@property (nonatomic, assign) NSInteger retryMaxCount;
```


The maximum number of retries by the player in case of network connection errors. The default value is `5`. If the value is `0`, the player will not automatically retry. To set a separate maximum number of retries for each stream, you can set [retryMaxCount](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-retrymaxcount).

<span id="VeLivePlayerConfiguration-stallretrytimeout"></span>
### stallRetryTimeout

```objectivec
@property (nonatomic, assign) NSInteger stallRetryTimeout;
```


The timeout threshold for stopping retries due to stalling. When the stalling duration exceeds this threshold, the player will stop retrying. The unit is ms. The default value is `10000`, which equals 10 seconds.

<span id="instructions"></span>
## Instructions

<span id="VeLivePlayerConfiguration-init"></span>
### init

```objectivec
- (instancetype _Nonnull)init;
```


Initializes the configurations.

<span id="VeLivePlayerStream"></span>
# VeLivePlayerStream

```objectivec
@interface VeLivePlayerStream : NSObject
```


The information about a pull stream address.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSString\* |[url](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-url) |
|VeLivePlayerResolution |[resolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-resolution) |
|int |[bitrate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-bitrate) |
|VeLivePlayerProtocol |[protocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-protocol) |
|VeLivePlayerFormat |[format](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-format) |
|VeLivePlayerStreamType |[type](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-type) |
|NSUInteger |[priority](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-priority) |
|NSInteger |[retryMaxCount](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-retrymaxcount) |
|NSInteger |[retryIntervalTimeMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-retryintervaltimems) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[init](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-init) |


<span id="instructions"></span>
## Instructions

<span id="VeLivePlayerStream-url"></span>
### url

```objectivec
@property (nonatomic, copy, nonnull) NSString *url;
```


The pull stream address.

<span id="VeLivePlayerStream-resolution"></span>
### resolution

```objectivec
@property (nonatomic, assign) VeLivePlayerResolution resolution;
```


The resolution. See [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerResolution) for details.

<span id="VeLivePlayerStream-bitrate"></span>
### bitrate

```objectivec
@property (nonatomic, assign) int bitrate;
```


The playback bitrate, in bps.

<span id="VeLivePlayerStream-protocol"></span>
### protocol

```objectivec
@property (nonatomic, assign) VeLivePlayerProtocol protocol;
```


The transmission protocol. See [VeLivePlayerProtocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerProtocol) for details.

<span id="VeLivePlayerStream-format"></span>
### format

```objectivec
@property (nonatomic, assign) VeLivePlayerFormat format;
```


The video format. See [VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerFormat) for details.

<span id="VeLivePlayerStream-type"></span>
### type

```objectivec
@property (nonatomic, assign) VeLivePlayerStreamType type;
```


Whether the stream is a primary or a backup stream. See [VeLivePlayerStreamType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamType) for details.

<span id="VeLivePlayerStream-priority"></span>
### priority

```objectivec
 @property (nonatomic, assign) NSUInteger priority;
```


The priority of the stream. The value must be `0` (default) or a positive integer. A larger value indicates a higher priority.

<span id="VeLivePlayerStream-retrymaxcount"></span>
### retryMaxCount

```objectivec
@property (nonatomic, assign) NSInteger retryMaxCount;
```


The maximum number of retry attempts for the stream, representing the total number of playback attempts (including the initial attempt). For example, a value of `3` means the player will retry at most 2 times after the initial failure. Valid values:


* `-1` (Default): Use the [retryMaxCount](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-retrymaxcount) value in `VeLivePlayerConfiguration`.

* `0`: Do not attempt to play this stream.

* `> 0`: The specific total number of attempts.

    &nbsp;


<span id="retryintervaltimems"></span>
### retryIntervalTimeMs

```objectivec
@property (nonatomic, assign) NSInteger retryIntervalTimeMs;
```


The retry interval, in ms. The default value is `-1`. If the value is `-1`, the player uses the [retryIntervalTimeMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-retryintervaltimems) value in `VeLivePlayerConfiguration`.

<span id="instructions"></span>
## Instructions

<span id="VeLivePlayerStream-init"></span>
### init

```objectivec
- (instancetype)init;
```


Initializes a pull stream address.

<span id="VeLivePlayerLogLevel"></span>
# VeLivePlayerLogLevel

```objectivec
typedef NS_ENUM(
    NSUInteger,
    VeLivePlayerLogLevel
)
```


The output log level of the player.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerLogLevelVerbose |0 |Output logs at the VERBOSE, DEBUG, INFO, WARNING, and ERROR levels. |
|VeLivePlayerLogLevelDebug |1 |Output logs at the DEBUG, INFO, WARNING, and ERROR levels. |
|VeLivePlayerLogLevelInfo |2 |Output logs at the INFO, WARNING, and ERROR levels. |
|VeLivePlayerLogLevelWarn |3 |Output logs at the WARNING and ERROR levels. |
|VeLivePlayerLogLevelError |4 |Output logs at the ERROR level. |
|VeLivePlayerLogLevelNone |5 |Disable log printing. |


<span id="VeLivePlayerAudioFrame"></span>
# VeLivePlayerAudioFrame

```objectivec
@interface VeLivePlayerAudioFrame : NSObject
```


The audio frame.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|VeLivePlayerAudioBufferType |[bufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame-buffertype) |
|int |[sampleRate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame-samplerate) |
|int |[channels](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame-channels) |
|int |[bitDepth](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame-bitdepth) |
|CMTime |[pts](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame-pts) |
|NSData\* |[data](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame-data) |
|int |[samples](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame-samples) |


<span id="instructions"></span>
## Instructions

<span id="VeLivePlayerAudioFrame-buffertype"></span>
### bufferType

```objectivec
@property (nonatomic, readonly) VeLivePlayerAudioBufferType bufferType;
```


The encapsulation format of the audio data. See [VeLivePlayerAudioBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioBufferType) for details.

<span id="VeLivePlayerAudioFrame-samplerate"></span>
### sampleRate

```objectivec
@property (nonatomic, readonly) int sampleRate;
```


The audio sample rate, in Hz.

<span id="VeLivePlayerAudioFrame-channels"></span>
### channels

```objectivec
@property (nonatomic, readonly) int channels;
```


The number of audio channels.


* 1: Mono;

* 2: Stereo.

    &nbsp;


<span id="bitdepth"></span>
### bitDepth

```objectivec
@property (nonatomic, readonly) int bitDepth;
```


The audio bit depth.

<span id="VeLivePlayerAudioFrame-pts"></span>
### pts

```objectivec
@property (nonatomic, readonly) CMTime pts;
```


The timestamp indicating the time when the audio is rendered, in milliseconds.

<span id="VeLivePlayerAudioFrame-data"></span>
### data

```objectivec
@property (nonatomic, strong, readonly) NSData* data;
```


The PCM audio data.

<span id="VeLivePlayerAudioFrame-samples"></span>
### samples

```objectivec
@property (nonatomic, readonly) int samples;
```


The number of audio samples.

<span id="VeLivePlayerVideoFrame"></span>
# VeLivePlayerVideoFrame

```objectivec
@interface VeLivePlayerVideoFrame : NSObject
```


The video frame.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|VeLivePlayerVideoBufferType |[bufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-buffertype) |
|VeLivePlayerPixelFormat |[pixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-pixelformat) |
|NSInteger |[width](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-width) |
|NSInteger |[height](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-height) |
|int64_t |[pts](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-pts) |
|CVPixelBufferRef |[pixelBuffer](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-pixelbuffer) |
|CMSampleBufferRef |[sampleBuffer](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-samplebuffer) |
|NSData\* |[data](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-data) |


<span id="instructions"></span>
## Instructions

<span id="VeLivePlayerVideoFrame-buffertype"></span>
### bufferType

```objectivec
@property (nonatomic, readonly) VeLivePlayerVideoBufferType bufferType;
```


The encapsulation format. See [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoBufferType) for details.

<span id="VeLivePlayerVideoFrame-pixelformat"></span>
### pixelFormat

```objectivec
@property (nonatomic, readonly) VeLivePlayerPixelFormat pixelFormat;
```


The pixel format. See [VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerPixelFormat) for details.

<span id="VeLivePlayerVideoFrame-width"></span>
### width

```objectivec
@property (nonatomic, readonly) NSInteger width;
```


The video width, in pixels.

<span id="VeLivePlayerVideoFrame-height"></span>
### height

```objectivec
@property (nonatomic, readonly) NSInteger height;
```


The video height, in pixels.

<span id="VeLivePlayerVideoFrame-pts"></span>
### pts

```objectivec
@property (nonatomic, readonly) int64_t pts;
```


The timestamp indicating the time when the video frame is rendered, in milliseconds.

<span id="VeLivePlayerVideoFrame-pixelbuffer"></span>
### pixelBuffer

```objectivec
@property (nonatomic, readonly, nullable) CVPixelBufferRef pixelBuffer;
```


The video data, if you set [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoBufferType) to `VeLivePlayerVideoBufferTypePixelBuffer`.

<span id="VeLivePlayerVideoFrame-samplebuffer"></span>
### sampleBuffer

```objectivec
@property (nonatomic, readonly, nullable) CMSampleBufferRef sampleBuffer;
```


The video data, if you set [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoBufferType) to `VeLivePlayerVideoBufferTypeSampleBuffer`.

<span id="VeLivePlayerVideoFrame-data"></span>
### data

```objectivec
@property (nonatomic, strong, readonly, nullable) NSData* data;
```


The video data, if you set [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoBufferType) to `VeLivePlayerVideoBufferTypeNSData`.

<span id="VeLivePlayerSupportResolutionSwitchError"></span>
# VeLivePlayerSupportResolutionSwitchError

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerSupportResolutionSwitchError
)
```


Error message for resolution level switching.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerErrorResNotFound |\-1 |The corresponding resolution gear is not found. |
|VeLivePlayerErrorSameRes |\-2 |The same as the current resolution level. |
|VeLivePlayerErrorStatusInvalid |\-3 |The player status is not in the prepare state. |
|VeLivePlayerErrorInvalidRes |\-4 |Resolution level error. |
|VeLivePlayerErrorConfigNotSupport |\-5 |Configuration not supported. |
|VeLivePlayerErrorFormatNotSupport |\-6 |Format not supported. |


<span id="VeLivePlayerStreamData"></span>
# VeLivePlayerStreamData

```objectivec
@interface VeLivePlayerStreamData : NSObject
```


The configurations for the pull stream addresses.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|BOOL |[enableABR](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-enableabr) |
|BOOL |[enableMainBackupSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-enablemainbackupswitch) |
|BOOL |[enableSmoothSwitchResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-enablesmoothswitchresolution) |
|VeLivePlayerResolution |[defaultResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-defaultresolution) |
|VeLivePlayerFormat |[defaultFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-defaultformat) |
|VeLivePlayerProtocol |[defaultProtocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-defaultprotocol) |
|NSArray<VeLivePlayerStream\*\>\* |[mainStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-mainstream) |
|NSArray<VeLivePlayerStream\*\>\* |[backupStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-backupstream) |


<span id="instructions"></span>
## Instructions

<span id="VeLivePlayerStreamData-enableabr"></span>
### enableABR

```objectivec
@property (nonatomic, assign) BOOL enableABR;
```


Whether to enable adaptive bitrate (ABR). The default value is `NO`.


* `YES`: Enable;

* `NO`: Disable.

    &nbsp;


<span id="enablemainbackupswitch"></span>
### enableMainBackupSwitch

```objectivec
@property (nonatomic, assign) BOOL enableMainBackupSwitch;
```


Whether to enable switching between the primary and the backup stream. The default value is `NO`.


* `YES`: Enable;

* `NO`: Disable.

    &nbsp;


<span id="enablesmoothswitchresolution"></span>
### enableSmoothSwitchResolution

```objectivec
@property (nonatomic, assign) BOOL enableSmoothSwitchResolution;
```


Whether to enable smooth resolution switching. The default value is `NO`. If enabled, the SDK will attempt to perform a smooth transition when you call the [switchResolution:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-switchresolution:) method to manually switch the resolution, avoiding black screens or lag. Valid values:


* `YES`: Enable.

* `NO`: Disable.

    &nbsp;


<span id="defaultresolution"></span>
### defaultResolution

```objectivec
@property (nonatomic, assign) VeLivePlayerResolution defaultResolution;
```


The default resolution. The default value is `VeLivePlayerResolutionOrigin`, which indicates the original resolution. See [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerResolution) for details.

<span id="VeLivePlayerStreamData-defaultformat"></span>
### defaultFormat

```objectivec
@property (nonatomic, assign) VeLivePlayerFormat defaultFormat;
```


The default video format. The default value is `VeLivePlayerFormatFLV`. See [VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerFormat) for details.

<span id="VeLivePlayerStreamData-defaultprotocol"></span>
### defaultProtocol

```objectivec
@property (nonatomic, assign) VeLivePlayerProtocol defaultProtocol;
```


The default transmission protocol. The default value is `VeLivePlayerProtocolTCP`. See [VeLivePlayerProtocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerProtocol) for details.

<span id="VeLivePlayerStreamData-mainstream"></span>
### mainStream

```objectivec
@property (nonatomic, copy, nullable) NSArray<VeLivePlayerStream *> * mainStream;
```


A list of main stream addresses. See [VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream) for details.

<span id="VeLivePlayerStreamData-backupstream"></span>
### backupStream

```objectivec
@property (nonatomic, copy, nullable) NSArray<VeLivePlayerStream *> * backupStream;
```


A list of backup stream addresses. See [VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream) for details.

<span id="VeLivePlayerAudioBufferType"></span>
# VeLivePlayerAudioBufferType

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerAudioBufferType
)
```


The encapsulation format of the audio.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerAudioBufferUnknown |0 |Unknown format. |
|VeLivePlayerAudioBufferTypeSampleBuffer |1 |CVSampleBufferRef. The audio data is processed and rendered as sample buffers. |
|VeLivePlayerAudioBufferTypeNSData |2 |NSData. The audio data is processed and rendered as NSData objects. |


<span id="VeLivePlayerVideoBufferType"></span>
# VeLivePlayerVideoBufferType

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerVideoBufferType
)
```


The encapsulation format of the video data.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerVideoBufferTypeUnknown |0 |Unknown format. |
|VeLivePlayerVideoBufferTypePixelBuffer |1 |CVPixelBufferRef. |
|VeLivePlayerVideoBufferTypeSampleBuffer |2 |CVSampleBufferRef. |
|VeLivePlayerVideoBufferTypeNSData |3 |NSData. |


<span id="VeLivePlayerProtocol"></span>
# VeLivePlayerProtocol

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerProtocol
)
```


The transmission protocol.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerProtocolTCP |0 |TCP. |
|VeLivePlayerProtocolQUIC |1 |QUIC. |
|VeLivePlayerProtocolTLS |2 |TLS. |
|VeLivePlayerProtocolHTTP2 |3 |HTTP/2. |
|VeLivePlayerProtocolDefault |4 |The default value. The player will automatically identify the network protocol from the pull stream address. Currently, only TCP and TLS protocols are supported for automatic identification. For QUIC or HTTP/2 protocols, use the corresponding value. |


<span id="VeLivePlayerFillMode"></span>
# VeLivePlayerFillMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerFillMode
)
```


The fill mode of the player screen.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerFillModeAspectFill |0 |Uniformly scale the video until the screen is completely filled. Part of the video may be cropped. |
|VeLivePlayerFillModeAspectFit |1 |Display the full video. The video is uniformly scaled until one dimension of the video hits the boundary of the screen. Any remaining space on the screen will be filled with black. |
|VeLivePlayerFillModeFullFill |2 |Stretch the video to fill the screen. The aspect ratio of the video might change. |


<span id="VeLivePlayerRotation"></span>
# VeLivePlayerRotation

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerRotation
)
```


The clockwise video rotation angle.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerRotation0 |0 |No rotation. |
|VeLivePlayerRotation90 |90 |Rotate 90 degrees clockwise. |
|VeLivePlayerRotation180 |180 |Rotate 180 degrees clockwise. |
|VeLivePlayerRotation270 |270 |Rotate 270 degrees clockwise. |


<span id="VeLivePlayerMirror"></span>
# VeLivePlayerMirror

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerMirror
)
```


The mirroring option.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerMirrorNone |0 |No mirroring. |
|VeLivePlayerMirrorHorizontal |1 |Horizontal mirroring. |
|VeLivePlayerMirrorVertical |2 |Vertical mirroring. |


<span id="VeLivePlayerPixelFormat"></span>
# VeLivePlayerPixelFormat

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerPixelFormat
)
```


The pixel format of the video frame.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerPixelFormatUnknown |0 |Unknown format. |
|VeLivePlayerPixelFormatI420 |2 |YUVI420. |


<span id="VeLivePlayerStatus"></span>
# VeLivePlayerStatus

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerStatus
)
```


The status of the live player.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerStatusPrepared |0 |The player finishes preparing and is waiting to render the video. |
|VeLivePlayerStatusPlaying |1 |Playback is currently in progress, meaning that the first frame has been rendered and no errors have occurred to the player. |
|VeLivePlayerStatusPaused |2 |The playback is paused. |
|VeLivePlayerStatusStopped |3 |The playback is stopped. |
|VeLivePlayerStatusError |4 |An error has occurred to the player. |
|VeLivePlayerStatusStalled |5 |The player has stalled. |


<span id="VeLivePlayerStatistics"></span>
# VeLivePlayerStatistics

```objectivec
@interface VeLivePlayerStatistics : NSObject
```


The playback statistics.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|NSURL\* |[url](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics-url) |
|BOOL |[isHardWareDecode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics-ishardwaredecode) |
|int |[delayMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics-delayms) |
|int |[delayS2sMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics-delays2sms) |
|int |[delayE2eMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics-delaye2ems) |
|int |[delayS2eMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics-delays2ems) |
|int |[stallTimeMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics-stalltimems) |
|long |[bandwidthEstimation](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics-bandwidthestimation) |
|NSString\* |[videoCodec](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics-videocodec) |
|int |[width](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics-width) |
|int |[height](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics-height) |
|float |[fps](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics-fps) |
|long |[bitrate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics-bitrate) |
|long |[videoBufferMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics-videobufferms) |
|long |[audioBufferMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics-audiobufferms) |
|VeLivePlayerFormat |[format](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics-format) |
|VeLivePlayerProtocol |[protocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics-protocol) |


<span id="instructions"></span>
## Instructions

<span id="VeLivePlayerStatistics-url"></span>
### url

```objectivec
@property (nonatomic, strong, readonly, nullable) NSURL* url;
```


The current pull stream address.

<span id="VeLivePlayerStatistics-ishardwaredecode"></span>
### isHardWareDecode

```objectivec
@property (nonatomic, readonly) BOOL isHardWareDecode;
```


Whether hardware decoding is used.


* `YES`: Hardware decoding is used;

* `NO`: Hardware decoding is not used.

    &nbsp;


<span id="delayms"></span>
### delayMs

```objectivec
@property (nonatomic, readonly) int delayMs;
```


The current playback latency, in milliseconds.

<span id="VeLivePlayerStatistics-delays2sms"></span>
### delayS2sMs

```objectivec
@property (nonatomic, readonly) int delayS2sMs;
```


Server\-to\-server delay, in milliseconds. Indicates the time taken for the stream to travel from the MediaLive push\-side edge node to the MediaLive pull\-side edge node. The value is `-1` when the SEI message does not contain the server timestamps for when the stream reaches the push\-side edge node and the pull\-side edge node.

<span id="VeLivePlayerStatistics-delaye2ems"></span>
### delayE2eMs

```objectivec
@property (nonatomic, readonly) int delayE2eMs;
```


End\-to\-end delay, in milliseconds. Indicates the time taken from when the Broadcast SDK writes the timestamp into the SEI message to when the Player SDK parses the SEI message locally. Accurate calculation depends on NTP\-based clock synchronization. The value is `-1` when the SEI message does not contain the timestamp written by the Broadcast SDK.

<span id="VeLivePlayerStatistics-delays2ems"></span>
### delayS2eMs

```objectivec
@property (nonatomic, readonly) int delayS2eMs;
```


Server\-to\-end delay, in milliseconds. Indicates the time taken from when the stream reaches the MediaLive push\-side edge node to when the Player SDK parses the SEI message locally. Accurate calculation depends on NTP\-based clock synchronization. The value is `-1` when the SEI message does not contain the server timestamp for when the stream reaches the MediaLive push\-side edge node.

<span id="VeLivePlayerStatistics-stalltimems"></span>
### stallTimeMs

```objectivec
@property (nonatomic, readonly) int stallTimeMs;
```


The cumulative duration of stutters that occurred since the beginning of playback, in milliseconds.

<span id="VeLivePlayerStatistics-bandwidthestimation"></span>
### bandwidthEstimation

```objectivec
@property (nonatomic, readonly) long bandwidthEstimation;
```


The estimated bandwidth, in kbps.

<span id="VeLivePlayerStatistics-videocodec"></span>
### videoCodec

```objectivec
@property (nonatomic, copy, readonly, nullable) NSString* videoCodec;
```


The encoding format of the video.

<span id="VeLivePlayerStatistics-width"></span>
### width

```objectivec
@property (nonatomic, readonly) int width;
```


The width of the video, in pixels.

<span id="VeLivePlayerStatistics-height"></span>
### height

```objectivec
@property (nonatomic, readonly) int height;
```


The height of the video, in pixels.

<span id="VeLivePlayerStatistics-fps"></span>
### fps

```objectivec
@property (nonatomic, readonly) float fps;
```


The frame rate of the video, in fps.

<span id="VeLivePlayerStatistics-bitrate"></span>
### bitrate

```objectivec
@property (nonatomic, readonly) long bitrate;
```


The downlink bitrate, in Kbps.

<span id="VeLivePlayerStatistics-videobufferms"></span>
### videoBufferMs

```objectivec
@property (nonatomic, readonly) long videoBufferMs;
```


The video buffer, in milliseconds.

<span id="VeLivePlayerStatistics-audiobufferms"></span>
### audioBufferMs

```objectivec
@property (nonatomic, readonly) long audioBufferMs;
```


The audio buffer, in milliseconds.

<span id="VeLivePlayerStatistics-format"></span>
### format

```objectivec
@property (nonatomic, readonly) VeLivePlayerFormat format;
```


The video format.

<span id="VeLivePlayerStatistics-protocol"></span>
### protocol

```objectivec
@property (nonatomic, readonly) VeLivePlayerProtocol protocol;
```


The transmission protocol of the live stream.

<span id="VeLivePlayerStreamInfo"></span>
# VeLivePlayerStreamInfo

```objectivec
@interface VeLivePlayerStreamInfo : NSObject
```


stream info..

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[width](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamInfo-width) |
|int |[height](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamInfo-height) |
|int |[bandwidth](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamInfo-bandwidth) |
|NSString\* |[url](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamInfo-url) |


<span id="instructions"></span>
## Instructions

<span id="VeLivePlayerStreamInfo-width"></span>
### width

```objectivec
@property (nonatomic, assign) int width;
```


The width of the video, in pixels.

<span id="VeLivePlayerStreamInfo-height"></span>
### height

```objectivec
@property (nonatomic, assign) int height;
```


The height of the video, in pixels.

<span id="VeLivePlayerStreamInfo-bandwidth"></span>
### bandwidth

```objectivec
@property (nonatomic, assign) int bandwidth;
```


The bandwidth of the video,in Bps

<span id="VeLivePlayerStreamInfo-url"></span>
### url

```objectivec
@property (nonatomic, copy) NSString *url;
```


The url of the video.

<span id="VeLivePlayerType"></span>
# VeLivePlayerType

```objectivec
typedef NS_ENUM(
    NSUInteger,
    VeLivePlayerType
)
```


Player Type.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerTypeOwn |0 |Custom player. |
|VeLivePlayerTypeSystem |1 |System player. |


<span id="VeLivePlayerStreamType"></span>
# VeLivePlayerStreamType

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerStreamType
)
```


The type of the live stream.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerStreamTypeMain |0 |The primary stream. |
|VeLivePlayerStreamTypeBackup |1 |The backup stream. |


<span id="VeLivePlayerFormat"></span>
# VeLivePlayerFormat

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerFormat
)
```


The format of the live stream.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerFormatFLV |0 |FLV. |
|VeLivePlayerFormatHLS |1 |HLS. |
|VeLivePlayerFormatRTM |2 |Real Time Media (RTM). |


<span id="VeLivePlayerResolution"></span>
# VeLivePlayerResolution

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerResolution
)
```


The player resolution.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerResolutionOrigin |0 |Original. |
|VeLivePlayerResolutionUHD |1 |Ultra high definition (UHD). |
|VeLivePlayerResolutionFHD |2 |Full High definition (FHD). |
|VeLivePlayerResolutionHD |3 |High definition (HD). |
|VeLivePlayerResolutionSD |4 |Standard definition (SD). |
|VeLivePlayerResolutionLD |5 |Low definition (LD). |
|VeLivePlayerResolutionAUTO |8 |Auto. |


<span id="VeLivePlayerProperty"></span>
# VeLivePlayerProperty

```objectivec
typedef NSString * VeLivePlayerProperty;
```


Advanced configurations.

<span id="Member Variables"></span>
## Member Variables


|Name |Type |
|---|---|
|[VeLivePlayerKeySetParamsHttpHeaders](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerProperty-veliveplayerkeysetparamshttpheaders) |[VeLivePlayerProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerProperty) |
|[VeLivePlayerKeySetParamsLowLatencyFlv](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerProperty-veliveplayerkeysetparamslowlatencyflv) |[VeLivePlayerProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerProperty) |


<span id="Variable Description"></span>
## Variable Description

<span id="VeLivePlayerProperty-veliveplayerkeysetparamshttpheaders"></span>
### VeLivePlayerKeySetParamsHttpHeaders

```objectivec
OBJC_EXTERN const VeLivePlayerProperty VeLivePlayerKeySetParamsHttpHeaders;
```


Sets custom HTTP headers for the player's HTTP requests. This is commonly used to pass additional information such as authentication tokens, cookies, or business tracking identifiers. For detailed usage, see [Customizing HTTP request headers](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-3?lang=en#customizing-http-request-headers).

<span id="VeLivePlayerProperty-veliveplayerkeysetparamslowlatencyflv"></span>
### VeLivePlayerKeySetParamsLowLatencyFlv

```objectivec
OBJC_EXTERN const VeLivePlayerProperty VeLivePlayerKeySetParamsLowLatencyFlv;
```


Configures FLV low\-latency settings (2–3 seconds latency). For detailed usage, see [Playing low-latency FLV streams](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-3?lang=en#playing-low-latency-flv-streams).
