---
title: "Player SDK for iOS：类型定义"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition-zh-CN"
---

# VeLivePlayerResolutionSwitchReason

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerResolutionSwitchReason
)
```

视频分辨率发生变化的原因。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerResolutionSwitchByAuto |0 |通过自适应码率（ABR）功能自动切换分辨率。 |
|VeLivePlayerResolutionSwitchByManual |1 |调用 [switchResolution:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-switchresolution) 后切换分辨率。 |

# VeLivePlayerConfiguration

```objectivec
@interface VeLivePlayerConfiguration : NSObject
```

播放器初始化配置。

## 成员属性

|类型 |名称 |
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

## 成员函数

|返回值 |名称 |
|---|---|
|instancetype |[init](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-init) |

## 说明

### enableSei

```objectivec
@property (nonatomic, assign) BOOL enableSei;
```

是否启用字符串 SEI 消息解析。默认值为 `NO`。

* `YES`：启用；

* `NO`：禁用。

### enableBinarySei

```objectivec
@property (nonatomic, assign) BOOL enableBinarySei;
```

是否启用二进制 SEI 消息解析。默认值为 `NO`。

* `YES`：启用；

* `NO`：禁用。

**说明**

启用二进制 SEI 后，将不再发送字符串 SEI 的回调。

### enableHardwareDecode

```objectivec
@property (nonatomic, assign) BOOL enableHardwareDecode;
```

是否开启硬件解码。默认值为 `YES`。启用硬件解码后，如果播放器启动硬件解码失败，或硬件解码失败，播放器会自动切换为软件解码。

* `YES`：启用；

* `NO`：禁用。

### enableLiveDNS

```objectivec
@property (nonatomic, assign) BOOL enableLiveDNS;
```

是否启用本地 DNS 预取。默认值为 `NO`。启用本地 DNS 预取可减少起播所需时间。如果本地 DNS 预取发生异常，播放器可能无法正常工作。

* `YES`：启用；

* `NO`：禁用。

### enableStatisticsCallback

```objectivec
@property (nonatomic, assign) BOOL enableStatisticsCallback;
```

是否启用播放信息的周期性回调。默认值为 `NO`。有关回调统计信息的更多信息，请参阅 [VeLivePlayerStatistics](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics)。如果 `enableStatisticsCallback` 为 `YES` 且 [statisticsCallbackInterval](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-statisticscallbackinterval) 大于 `0`，播放器将在指定时间间隔后周期性上报播放器状态信息。

* `YES`：启用；

* `NO`：禁用。

### statisticsCallbackInterval

```objectivec
@property (nonatomic, assign) NSInteger statisticsCallbackInterval;
```

提供播放信息的周期性回调时间间隔，单位为秒。默认值为 `5`。如果 enableStatisticsCallback 为 `YES` 且 [enableStatisticsCallback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-enablestatisticscallback) 大于 `0`，播放器将在指定时间间隔后周期性上报播放器状态信息。

### networkTimeoutMs

```objectivec
@property (nonatomic, assign) NSInteger networkTimeoutMs;
```

网络超时时长，单位为毫秒。默认值为 `5000`。播放器发送网络请求后，如果在超时时长后未收到服务器响应，则认为网络请求失败。

### retryIntervalTimeMs

```objectivec
@property (nonatomic, assign) NSInteger retryIntervalTimeMs;
```

重试间隔，单位为 ms。默认值为 `5000`。如需为每个流设置单独的重试间隔，可以设置 [retryIntervalTimeMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-retryintervaltimems)。

### retryMaxCount

```objectivec
@property (nonatomic, assign) NSInteger retryMaxCount;
```

发生网络连接错误时，播放器的最大重试次数。默认值为 `5`。如果值为 `0`，播放器不会自动重试。如需为每个流设置单独的最大重试次数，可以设置 [retryMaxCount](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-retrymaxcount)。

### stallRetryTimeout

```objectivec
@property (nonatomic, assign) NSInteger stallRetryTimeout;
```

因卡顿而停止重试的超时阈值。当卡顿时长超过此阈值时，播放器将停止重试。单位为 ms。默认值为 `10000`，即 10 秒。

## 说明

### init

```objectivec
- (instancetype _Nonnull)init;
```

初始化配置。

# VeLivePlayerStream

```objectivec
@interface VeLivePlayerStream : NSObject
```

拉流地址的信息。

## 成员属性

|类型 |名称 |
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

## 成员函数

|返回值 |名称 |
|---|---|
|instancetype |[init](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-init) |

## 说明

### url

```objectivec
@property (nonatomic, copy, nonnull) NSString *url;
```

拉流地址。

### resolution

```objectivec
@property (nonatomic, assign) VeLivePlayerResolution resolution;
```

分辨率。详情请参阅 [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerResolution)。

### bitrate

```objectivec
@property (nonatomic, assign) int bitrate;
```

播放码率，单位为 bps。

### protocol

```objectivec
@property (nonatomic, assign) VeLivePlayerProtocol protocol;
```

传输协议。详情请参阅 [VeLivePlayerProtocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerProtocol)。

### format

```objectivec
@property (nonatomic, assign) VeLivePlayerFormat format;
```

视频格式。详情请参阅 [VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerFormat)。

### type

```objectivec
@property (nonatomic, assign) VeLivePlayerStreamType type;
```

该流是主流还是备流。详情请参阅 [VeLivePlayerStreamType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamType)。

### priority

```objectivec
 @property (nonatomic, assign) NSUInteger priority;
```

流的优先级。取值必须为 `0`（默认值）或正整数。值越大，优先级越高。

### retryMaxCount

```objectivec
@property (nonatomic, assign) NSInteger retryMaxCount;
```

该流的最大尝试播放次数，表示播放尝试总次数（包括首次尝试）。例如，值为 `3` 表示首次失败后，播放器最多重试 2 次。有效值：

* `-1`（默认）：使用 `VeLivePlayerConfiguration` 中的 [retryMaxCount](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-retrymaxcount) 值。

* `0`：不尝试播放此流。

* `> 0`：指定的总尝试次数。

### retryIntervalTimeMs

```objectivec
@property (nonatomic, assign) NSInteger retryIntervalTimeMs;
```

重试间隔，单位为 ms。默认值为 `-1`。如果值为 `-1`，播放器使用 `VeLivePlayerConfiguration` 中的 [retryIntervalTimeMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-retryintervaltimems) 值。

## 说明

### init

```objectivec
- (instancetype)init;
```

初始化拉流地址。

# VeLivePlayerLogLevel

```objectivec
typedef NS_ENUM(
    NSUInteger,
    VeLivePlayerLogLevel
)
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

```objectivec
@interface VeLivePlayerAudioFrame : NSObject
```

音频帧。

## 成员属性

|类型 |名称 |
|---|---|
|VeLivePlayerAudioBufferType |[bufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame-buffertype) |
|int |[sampleRate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame-samplerate) |
|int |[channels](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame-channels) |
|int |[bitDepth](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame-bitdepth) |
|CMTime |[pts](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame-pts) |
|NSData\* |[data](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame-data) |
|int |[samples](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame-samples) |

## 说明

### bufferType

```objectivec
@property (nonatomic, readonly) VeLivePlayerAudioBufferType bufferType;
```

音频数据的封装格式。详情请参阅 [VeLivePlayerAudioBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioBufferType)。

### sampleRate

```objectivec
@property (nonatomic, readonly) int sampleRate;
```

音频采样率，单位为 Hz。

### channels

```objectivec
@property (nonatomic, readonly) int channels;
```

音频声道数。

* 1：单声道；

* 2：立体声。

### bitDepth

```objectivec
@property (nonatomic, readonly) int bitDepth;
```

音频位深。

### pts

```objectivec
@property (nonatomic, readonly) CMTime pts;
```

指示音频渲染时间的时间戳，单位为毫秒。

### data

```objectivec
@property (nonatomic, strong, readonly) NSData* data;
```

PCM 音频数据。

### samples

```objectivec
@property (nonatomic, readonly) int samples;
```

音频采样数。

# VeLivePlayerVideoFrame

```objectivec
@interface VeLivePlayerVideoFrame : NSObject
```

视频帧。

## 成员属性

|类型 |名称 |
|---|---|
|VeLivePlayerVideoBufferType |[bufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-buffertype) |
|VeLivePlayerPixelFormat |[pixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-pixelformat) |
|NSInteger |[width](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-width) |
|NSInteger |[height](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-height) |
|int64_t |[pts](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-pts) |
|CVPixelBufferRef |[pixelBuffer](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-pixelbuffer) |
|CMSampleBufferRef |[sampleBuffer](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-samplebuffer) |
|NSData\* |[data](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-data) |

## 说明

### bufferType

```objectivec
@property (nonatomic, readonly) VeLivePlayerVideoBufferType bufferType;
```

封装格式。详情请参阅 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoBufferType)。

### pixelFormat

```objectivec
@property (nonatomic, readonly) VeLivePlayerPixelFormat pixelFormat;
```

像素格式。详情请参阅 [VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerPixelFormat)。

### width

```objectivec
@property (nonatomic, readonly) NSInteger width;
```

视频宽度，单位为像素。

### height

```objectivec
@property (nonatomic, readonly) NSInteger height;
```

视频高度，单位为像素。

### pts

```objectivec
@property (nonatomic, readonly) int64_t pts;
```

指示视频帧渲染时间的时间戳，单位为毫秒。

### pixelBuffer

```objectivec
@property (nonatomic, readonly, nullable) CVPixelBufferRef pixelBuffer;
```

视频数据，前提是将 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoBufferType) 设置为 `VeLivePlayerVideoBufferTypePixelBuffer`。

### sampleBuffer

```objectivec
@property (nonatomic, readonly, nullable) CMSampleBufferRef sampleBuffer;
```

视频数据，前提是将 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoBufferType) 设置为 `VeLivePlayerVideoBufferTypeSampleBuffer`。

### data

```objectivec
@property (nonatomic, strong, readonly, nullable) NSData* data;
```

视频数据，前提是将 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoBufferType) 设置为 `VeLivePlayerVideoBufferTypeNSData`。

# VeLivePlayerSupportResolutionSwitchError

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerSupportResolutionSwitchError
)
```

分辨率档位切换的错误消息。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerErrorResNotFound |\-1 |未找到对应的分辨率档位。 |
|VeLivePlayerErrorSameRes |\-2 |与当前分辨率档位相同。 |
|VeLivePlayerErrorStatusInvalid |\-3 |播放器状态不处于 prepare 状态。 |
|VeLivePlayerErrorInvalidRes |\-4 |分辨率档位错误。 |
|VeLivePlayerErrorConfigNotSupport |\-5 |不支持该配置。 |
|VeLivePlayerErrorFormatNotSupport |\-6 |不支持该格式。 |

# VeLivePlayerStreamData

```objectivec
@interface VeLivePlayerStreamData : NSObject
```

拉流地址配置。

## 成员属性

|类型 |名称 |
|---|---|
|BOOL |[enableABR](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-enableabr) |
|BOOL |[enableMainBackupSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-enablemainbackupswitch) |
|BOOL |[enableSmoothSwitchResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-enablesmoothswitchresolution) |
|VeLivePlayerResolution |[defaultResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-defaultresolution) |
|VeLivePlayerFormat |[defaultFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-defaultformat) |
|VeLivePlayerProtocol |[defaultProtocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-defaultprotocol) |
|NSArray<VeLivePlayerStream\*\>\* |[mainStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-mainstream) |
|NSArray<VeLivePlayerStream\*\>\* |[backupStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-backupstream) |

## 说明

### enableABR

```objectivec
@property (nonatomic, assign) BOOL enableABR;
```

是否启用自适应码率（ABR）。默认值为 `NO`。

* `YES`：启用；

* `NO`：禁用。

### enableMainBackupSwitch

```objectivec
@property (nonatomic, assign) BOOL enableMainBackupSwitch;
```

是否启用主流和备流之间的切换。默认值为 `NO`。

* `YES`：启用；

* `NO`：禁用。

### enableSmoothSwitchResolution

```objectivec
@property (nonatomic, assign) BOOL enableSmoothSwitchResolution;
```

是否启用平滑分辨率切换。默认值为 `NO`。如果启用，当您调用 [switchResolution:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-switchresolution:) 方法手动切换分辨率时，SDK 将尝试执行平滑过渡，以避免黑屏或卡顿。有效值：

* `YES`：启用。

* `NO`：禁用。

### defaultResolution

```objectivec
@property (nonatomic, assign) VeLivePlayerResolution defaultResolution;
```

默认分辨率。默认值为 `VeLivePlayerResolutionOrigin`，表示原始分辨率。详情请参阅 [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerResolution)。

### defaultFormat

```objectivec
@property (nonatomic, assign) VeLivePlayerFormat defaultFormat;
```

默认视频格式。默认值为 `VeLivePlayerFormatFLV`。详情请参阅 [VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerFormat)。

### defaultProtocol

```objectivec
@property (nonatomic, assign) VeLivePlayerProtocol defaultProtocol;
```

默认传输协议。默认值为 `VeLivePlayerProtocolTCP`。详情请参阅 [VeLivePlayerProtocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerProtocol)。

### mainStream

```objectivec
@property (nonatomic, copy, nullable) NSArray<VeLivePlayerStream *> * mainStream;
```

主流地址列表。详情请参阅 [VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream)。

### backupStream

```objectivec
@property (nonatomic, copy, nullable) NSArray<VeLivePlayerStream *> * backupStream;
```

备流地址列表。详情请参阅 [VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream)。

# VeLivePlayerAudioBufferType

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerAudioBufferType
)
```

音频的封装格式。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerAudioBufferUnknown |0 |未知格式。 |
|VeLivePlayerAudioBufferTypeSampleBuffer |1 |CVSampleBufferRef。音频数据作为 sample buffers 进行处理和渲染。 |
|VeLivePlayerAudioBufferTypeNSData |2 |NSData。音频数据作为 NSData 对象进行处理和渲染。 |

# VeLivePlayerVideoBufferType

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerVideoBufferType
)
```

视频数据的封装格式。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerVideoBufferTypeUnknown |0 |未知格式。 |
|VeLivePlayerVideoBufferTypePixelBuffer |1 |CVPixelBufferRef。 |
|VeLivePlayerVideoBufferTypeSampleBuffer |2 |CVSampleBufferRef。 |
|VeLivePlayerVideoBufferTypeNSData |3 |NSData。 |

# VeLivePlayerProtocol

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerProtocol
)
```

传输协议。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerProtocolTCP |0 |TCP。 |
|VeLivePlayerProtocolQUIC |1 |QUIC。 |
|VeLivePlayerProtocolTLS |2 |TLS。 |
|VeLivePlayerProtocolHTTP2 |3 |HTTP/2。 |
|VeLivePlayerProtocolDefault |4 |默认值。播放器将从拉流地址中自动识别网络协议。目前，仅支持自动识别 TCP 和 TLS 协议。对于 QUIC 或 HTTP/2 协议，请使用对应值。 |

# VeLivePlayerFillMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerFillMode
)
```

播放器画面的填充模式。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerFillModeAspectFill |0 |等比缩放视频，直到屏幕被完全填满。部分视频可能被裁剪。 |
|VeLivePlayerFillModeAspectFit |1 |显示完整视频。视频会等比缩放，直到视频的某一维度到达屏幕边界。屏幕上的剩余空间将填充为黑色。 |
|VeLivePlayerFillModeFullFill |2 |拉伸视频以填满屏幕。视频宽高比可能发生变化。 |

# VeLivePlayerRotation

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerRotation
)
```

视频顺时针旋转角度。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerRotation0 |0 |不旋转。 |
|VeLivePlayerRotation90 |90 |顺时针旋转 90 度。 |
|VeLivePlayerRotation180 |180 |顺时针旋转 180 度。 |
|VeLivePlayerRotation270 |270 |顺时针旋转 270 度。 |

# VeLivePlayerMirror

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerMirror
)
```

镜像选项。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerMirrorNone |0 |不镜像。 |
|VeLivePlayerMirrorHorizontal |1 |水平镜像。 |
|VeLivePlayerMirrorVertical |2 |垂直镜像。 |

# VeLivePlayerPixelFormat

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerPixelFormat
)
```

视频帧的像素格式。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerPixelFormatUnknown |0 |未知格式。 |
|VeLivePlayerPixelFormatI420 |2 |YUVI420。 |

# VeLivePlayerStatus

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerStatus
)
```

直播播放器的状态。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerStatusPrepared |0 |播放器完成准备，正在等待渲染视频。 |
|VeLivePlayerStatusPlaying |1 |正在播放，表示首帧已渲染且播放器未发生错误。 |
|VeLivePlayerStatusPaused |2 |播放已暂停。 |
|VeLivePlayerStatusStopped |3 |播放已停止。 |
|VeLivePlayerStatusError |4 |播放器发生错误。 |
|VeLivePlayerStatusStalled |5 |播放器发生卡顿。 |

# VeLivePlayerStatistics

```objectivec
@interface VeLivePlayerStatistics : NSObject
```

播放统计信息。

## 成员属性

|类型 |名称 |
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

## 说明

### url

```objectivec
@property (nonatomic, strong, readonly, nullable) NSURL* url;
```

当前拉流地址。

### isHardWareDecode

```objectivec
@property (nonatomic, readonly) BOOL isHardWareDecode;
```

是否使用硬件解码。

* `YES`：使用硬件解码；

* `NO`：未使用硬件解码。

### delayMs

```objectivec
@property (nonatomic, readonly) int delayMs;
```

当前播放延迟，单位为毫秒。

### delayS2sMs

```objectivec
@property (nonatomic, readonly) int delayS2sMs;
```

服务器到服务器延迟，单位为毫秒。表示流从 MediaLive 推流侧边缘节点传输到 MediaLive 拉流侧边缘节点所需的时间。当 SEI 消息不包含流到达推流侧边缘节点和拉流侧边缘节点时的服务器时间戳时，该值为 `-1`。

### delayE2eMs

```objectivec
@property (nonatomic, readonly) int delayE2eMs;
```

端到端延迟，单位为毫秒。表示从 Broadcast SDK 将时间戳写入 SEI 消息，到 Player SDK 在本地解析 SEI 消息所需的时间。准确计算依赖基于 NTP 的时钟同步。当 SEI 消息不包含 Broadcast SDK 写入的时间戳时，该值为 `-1`。

### delayS2eMs

```objectivec
@property (nonatomic, readonly) int delayS2eMs;
```

服务器到终端延迟，单位为毫秒。表示从流到达 MediaLive 推流侧边缘节点，到 Player SDK 在本地解析 SEI 消息所需的时间。准确计算依赖基于 NTP 的时钟同步。当 SEI 消息不包含流到达 MediaLive 推流侧边缘节点时的服务器时间戳时，该值为 `-1`。

### stallTimeMs

```objectivec
@property (nonatomic, readonly) int stallTimeMs;
```

自播放开始以来发生的卡顿累计时长，单位为毫秒。

### bandwidthEstimation

```objectivec
@property (nonatomic, readonly) long bandwidthEstimation;
```

估算带宽，单位为 kbps。

### videoCodec

```objectivec
@property (nonatomic, copy, readonly, nullable) NSString* videoCodec;
```

视频的编码格式。

### width

```objectivec
@property (nonatomic, readonly) int width;
```

视频宽度，单位为像素。

### height

```objectivec
@property (nonatomic, readonly) int height;
```

视频高度，单位为像素。

### fps

```objectivec
@property (nonatomic, readonly) float fps;
```

视频帧率，单位为 fps。

### bitrate

```objectivec
@property (nonatomic, readonly) long bitrate;
```

下行码率，单位为 Kbps。

### videoBufferMs

```objectivec
@property (nonatomic, readonly) long videoBufferMs;
```

视频缓冲区，单位为毫秒。

### audioBufferMs

```objectivec
@property (nonatomic, readonly) long audioBufferMs;
```

音频缓冲区，单位为毫秒。

### format

```objectivec
@property (nonatomic, readonly) VeLivePlayerFormat format;
```

视频格式。

### protocol

```objectivec
@property (nonatomic, readonly) VeLivePlayerProtocol protocol;
```

直播流的传输协议。

# VeLivePlayerStreamInfo

```objectivec
@interface VeLivePlayerStreamInfo : NSObject
```

流信息。

## 成员属性

|类型 |名称 |
|---|---|
|int |[width](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamInfo-width) |
|int |[height](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamInfo-height) |
|int |[bandwidth](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamInfo-bandwidth) |
|NSString\* |[url](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamInfo-url) |

## 说明

### width

```objectivec
@property (nonatomic, assign) int width;
```

视频宽度，单位为像素。

### height

```objectivec
@property (nonatomic, assign) int height;
```

视频高度，单位为像素。

### bandwidth

```objectivec
@property (nonatomic, assign) int bandwidth;
```

视频带宽，单位为 Bps

### url

```objectivec
@property (nonatomic, copy) NSString *url;
```

视频的 url。

# VeLivePlayerType

```objectivec
typedef NS_ENUM(
    NSUInteger,
    VeLivePlayerType
)
```

播放器类型。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerTypeOwn |0 |自定义播放器。 |
|VeLivePlayerTypeSystem |1 |系统播放器。 |

# VeLivePlayerStreamType

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerStreamType
)
```

直播流的类型。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerStreamTypeMain |0 |主流。 |
|VeLivePlayerStreamTypeBackup |1 |备流。 |

# VeLivePlayerFormat

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerFormat
)
```

直播流的格式。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerFormatFLV |0 |FLV。 |
|VeLivePlayerFormatHLS |1 |HLS。 |
|VeLivePlayerFormatRTM |2 |实时媒体（RTM）。 |

# VeLivePlayerResolution

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerResolution
)
```

播放器分辨率。

## 枚举值

|类型 |值 |说明 |
|---|---|---|
|VeLivePlayerResolutionOrigin |0 |原始。 |
|VeLivePlayerResolutionUHD |1 |超高清（UHD）。 |
|VeLivePlayerResolutionFHD |2 |全高清（FHD）。 |
|VeLivePlayerResolutionHD |3 |高清（HD）。 |
|VeLivePlayerResolutionSD |4 |标清（SD）。 |
|VeLivePlayerResolutionLD |5 |低清（LD）。 |
|VeLivePlayerResolutionAUTO |8 |自动。 |

# VeLivePlayerProperty

```objectivec
typedef NSString * VeLivePlayerProperty;
```

高级配置。

## 成员变量

|名称 |类型 |
|---|---|
|[VeLivePlayerKeySetParamsHttpHeaders](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerProperty-veliveplayerkeysetparamshttpheaders) |[VeLivePlayerProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerProperty) |
|[VeLivePlayerKeySetParamsLowLatencyFlv](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerProperty-veliveplayerkeysetparamslowlatencyflv) |[VeLivePlayerProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerProperty) |

## 变量说明

### VeLivePlayerKeySetParamsHttpHeaders

```objectivec
OBJC_EXTERN const VeLivePlayerProperty VeLivePlayerKeySetParamsHttpHeaders;
```

为播放器的 HTTP 请求设置自定义 HTTP 头。通常用于传递身份验证令牌、Cookie 或业务跟踪标识符等附加信息。详细用法请参阅[自定义 HTTP 请求头](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-3?lang=en#customizing-http-request-headers)。

### VeLivePlayerKeySetParamsLowLatencyFlv

```objectivec
OBJC_EXTERN const VeLivePlayerProperty VeLivePlayerKeySetParamsLowLatencyFlv;
```

配置 FLV 低延迟设置（2–3 秒延迟）。详细用法请参阅[播放低延迟 FLV 流](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-3?lang=en#playing-low-latency-flv-streams)。
