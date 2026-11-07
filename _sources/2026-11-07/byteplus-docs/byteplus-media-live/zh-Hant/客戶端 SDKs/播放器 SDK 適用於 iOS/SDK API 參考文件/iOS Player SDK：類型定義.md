---
title: "iOS Player SDK：類型定義"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition-zh-TW"
---

# VeLivePlayerResolutionSwitchReason

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerResolutionSwitchReason
)
```

影片解析度變更的原因。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerResolutionSwitchByAuto |0 |透過自適應位元率 (ABR) 功能自動切換解析度。 |
|VeLivePlayerResolutionSwitchByManual |1 |呼叫 [switchResolution:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-switchresolution) 後變更解析度。 |

# VeLivePlayerConfiguration

```objectivec
@interface VeLivePlayerConfiguration : NSObject
```

播放器初始化的組態。

## 成員屬性

|類型 |名稱 |
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

## 成員函式

|傳回值 |名稱 |
|---|---|
|instancetype |[init](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-init) |

## 說明

### enableSei

```objectivec
@property (nonatomic, assign) BOOL enableSei;
```

是否啟用字串 SEI 訊息解析。預設值為 `NO`。

* `YES`：啟用；

* `NO`：停用。

### enableBinarySei

```objectivec
@property (nonatomic, assign) BOOL enableBinarySei;
```

是否啟用二進位 SEI 訊息解析。預設值為 `NO`。

* `YES`：啟用；

* `NO`：停用。

**注意事項**

啟用二進位 SEI 後，將不再傳送字串 SEI 的回呼。

### enableHardwareDecode

```objectivec
@property (nonatomic, assign) BOOL enableHardwareDecode;
```

是否開啟硬體解碼。預設值為 `YES`。啟用硬體解碼時，如果播放器啟動硬體解碼失敗，或硬體解碼失敗，播放器會自動切換至軟體解碼。

* `YES`：啟用；

* `NO`：停用。

### enableLiveDNS

```objectivec
@property (nonatomic, assign) BOOL enableLiveDNS;
```

是否啟用本機 DNS 預先擷取。預設值為 `NO`。啟用本機 DNS 預先擷取可縮短開始播放所需時間。如果本機 DNS 預先擷取發生異常，播放器可能無法正常運作。

* `YES`：啟用；

* `NO`：停用。

### enableStatisticsCallback

```objectivec
@property (nonatomic, assign) BOOL enableStatisticsCallback;
```

是否啟用播放資訊的週期性回呼。預設值為 `NO`。如需回呼統計資料的詳細資訊，請參閱 [VeLivePlayerStatistics](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics)。如果 `enableStatisticsCallback` 為 `YES`，且 [statisticsCallbackInterval](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-statisticscallbackinterval) 大於 `0`，播放器會在指定時間間隔後定期回報播放器狀態資訊。

* `YES`：啟用；

* `NO`：停用。

### statisticsCallbackInterval

```objectivec
@property (nonatomic, assign) NSInteger statisticsCallbackInterval;
```

提供播放資訊之週期性回呼的時間間隔，單位為秒。預設值為 `5`。如果 enableStatisticsCallback 為 `YES`，且 [enableStatisticsCallback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-enablestatisticscallback) 大於 `0`，播放器會在指定時間間隔後定期回報播放器狀態資訊。

### networkTimeoutMs

```objectivec
@property (nonatomic, assign) NSInteger networkTimeoutMs;
```

網路逾時時間，單位為毫秒。預設值為 `5000`。播放器送出網路請求後，如果逾時時間後仍未收到伺服器回應，則視為網路請求失敗。

### retryIntervalTimeMs

```objectivec
@property (nonatomic, assign) NSInteger retryIntervalTimeMs;
```

重試間隔，單位為 ms。預設值為 `5000`。若要為每個串流設定不同的重試間隔，可設定 [retryIntervalTimeMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-retryintervaltimems)。

### retryMaxCount

```objectivec
@property (nonatomic, assign) NSInteger retryMaxCount;
```

發生網路連線錯誤時，播放器的最大重試次數。預設值為 `5`。如果值為 `0`，播放器將不會自動重試。若要為每個串流設定不同的最大重試次數，可設定 [retryMaxCount](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-retrymaxcount)。

### stallRetryTimeout

```objectivec
@property (nonatomic, assign) NSInteger stallRetryTimeout;
```

因卡頓而停止重試的逾時閾值。當卡頓持續時間超過此閾值時，播放器將停止重試。單位為 ms。預設值為 `10000`，等於 10 秒。

## 說明

### init

```objectivec
- (instancetype _Nonnull)init;
```

初始化組態。

# VeLivePlayerStream

```objectivec
@interface VeLivePlayerStream : NSObject
```

拉流位址的相關資訊。

## 成員屬性

|類型 |名稱 |
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

## 成員函式

|傳回值 |名稱 |
|---|---|
|instancetype |[init](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-init) |

## 說明

### url

```objectivec
@property (nonatomic, copy, nonnull) NSString *url;
```

拉流位址。

### resolution

```objectivec
@property (nonatomic, assign) VeLivePlayerResolution resolution;
```

解析度。詳細資訊請參閱 [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerResolution)。

### bitrate

```objectivec
@property (nonatomic, assign) int bitrate;
```

播放位元率，單位為 bps。

### protocol

```objectivec
@property (nonatomic, assign) VeLivePlayerProtocol protocol;
```

傳輸協定。詳細資訊請參閱 [VeLivePlayerProtocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerProtocol)。

### format

```objectivec
@property (nonatomic, assign) VeLivePlayerFormat format;
```

影片格式。詳細資訊請參閱 [VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerFormat)。

### type

```objectivec
@property (nonatomic, assign) VeLivePlayerStreamType type;
```

串流為主串流或備用串流。詳細資訊請參閱 [VeLivePlayerStreamType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamType)。

### priority

```objectivec
 @property (nonatomic, assign) NSUInteger priority;
```

串流的優先順序。值必須為 `0`（預設）或正整數。值越大表示優先順序越高。

### retryMaxCount

```objectivec
@property (nonatomic, assign) NSInteger retryMaxCount;
```

串流的最大重試嘗試次數，代表播放嘗試總次數（包括初始嘗試）。例如，值為 `3` 表示播放器在初始失敗後最多重試 2 次。有效值：

* `-1`（預設）：使用 `VeLivePlayerConfiguration` 中的 [retryMaxCount](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-retrymaxcount) 值。

* `0`：不嘗試播放此串流。

* `> 0`：指定的嘗試總次數。

### retryIntervalTimeMs

```objectivec
@property (nonatomic, assign) NSInteger retryIntervalTimeMs;
```

重試間隔，單位為 ms。預設值為 `-1`。如果值為 `-1`，播放器會使用 `VeLivePlayerConfiguration` 中的 [retryIntervalTimeMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-retryintervaltimems) 值。

## 說明

### init

```objectivec
- (instancetype)init;
```

初始化拉流位址。

# VeLivePlayerLogLevel

```objectivec
typedef NS_ENUM(
    NSUInteger,
    VeLivePlayerLogLevel
)
```

播放器的輸出記錄層級。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerLogLevelVerbose |0 |輸出 VERBOSE、DEBUG、INFO、WARNING 和 ERROR 層級的記錄。 |
|VeLivePlayerLogLevelDebug |1 |輸出 DEBUG、INFO、WARNING 和 ERROR 層級的記錄。 |
|VeLivePlayerLogLevelInfo |2 |輸出 INFO、WARNING 和 ERROR 層級的記錄。 |
|VeLivePlayerLogLevelWarn |3 |輸出 WARNING 和 ERROR 層級的記錄。 |
|VeLivePlayerLogLevelError |4 |輸出 ERROR 層級的記錄。 |
|VeLivePlayerLogLevelNone |5 |停用記錄列印。 |

# VeLivePlayerAudioFrame

```objectivec
@interface VeLivePlayerAudioFrame : NSObject
```

音訊影格。

## 成員屬性

|類型 |名稱 |
|---|---|
|VeLivePlayerAudioBufferType |[bufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame-buffertype) |
|int |[sampleRate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame-samplerate) |
|int |[channels](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame-channels) |
|int |[bitDepth](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame-bitdepth) |
|CMTime |[pts](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame-pts) |
|NSData\* |[data](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame-data) |
|int |[samples](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame-samples) |

## 說明

### bufferType

```objectivec
@property (nonatomic, readonly) VeLivePlayerAudioBufferType bufferType;
```

音訊資料的封裝格式。詳細資訊請參閱 [VeLivePlayerAudioBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioBufferType)。

### sampleRate

```objectivec
@property (nonatomic, readonly) int sampleRate;
```

音訊取樣率，單位為 Hz。

### channels

```objectivec
@property (nonatomic, readonly) int channels;
```

音訊聲道數。

* 1：單聲道；

* 2：立體聲。

### bitDepth

```objectivec
@property (nonatomic, readonly) int bitDepth;
```

音訊位元深度。

### pts

```objectivec
@property (nonatomic, readonly) CMTime pts;
```

表示音訊轉譯時間的時間戳記，單位為毫秒。

### data

```objectivec
@property (nonatomic, strong, readonly) NSData* data;
```

PCM 音訊資料。

### samples

```objectivec
@property (nonatomic, readonly) int samples;
```

音訊樣本數。

# VeLivePlayerVideoFrame

```objectivec
@interface VeLivePlayerVideoFrame : NSObject
```

影片影格。

## 成員屬性

|類型 |名稱 |
|---|---|
|VeLivePlayerVideoBufferType |[bufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-buffertype) |
|VeLivePlayerPixelFormat |[pixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-pixelformat) |
|NSInteger |[width](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-width) |
|NSInteger |[height](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-height) |
|int64_t |[pts](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-pts) |
|CVPixelBufferRef |[pixelBuffer](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-pixelbuffer) |
|CMSampleBufferRef |[sampleBuffer](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-samplebuffer) |
|NSData\* |[data](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame-data) |

## 說明

### bufferType

```objectivec
@property (nonatomic, readonly) VeLivePlayerVideoBufferType bufferType;
```

封裝格式。詳細資訊請參閱 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoBufferType)。

### pixelFormat

```objectivec
@property (nonatomic, readonly) VeLivePlayerPixelFormat pixelFormat;
```

像素格式。詳細資訊請參閱 [VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerPixelFormat)。

### width

```objectivec
@property (nonatomic, readonly) NSInteger width;
```

影片寬度，單位為像素。

### height

```objectivec
@property (nonatomic, readonly) NSInteger height;
```

影片高度，單位為像素。

### pts

```objectivec
@property (nonatomic, readonly) int64_t pts;
```

表示影片影格轉譯時間的時間戳記，單位為毫秒。

### pixelBuffer

```objectivec
@property (nonatomic, readonly, nullable) CVPixelBufferRef pixelBuffer;
```

影片資料，當您將 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoBufferType) 設為 `VeLivePlayerVideoBufferTypePixelBuffer` 時使用。

### sampleBuffer

```objectivec
@property (nonatomic, readonly, nullable) CMSampleBufferRef sampleBuffer;
```

影片資料，當您將 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoBufferType) 設為 `VeLivePlayerVideoBufferTypeSampleBuffer` 時使用。

### data

```objectivec
@property (nonatomic, strong, readonly, nullable) NSData* data;
```

影片資料，當您將 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoBufferType) 設為 `VeLivePlayerVideoBufferTypeNSData` 時使用。

# VeLivePlayerSupportResolutionSwitchError

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerSupportResolutionSwitchError
)
```

解析度檔位切換的錯誤訊息。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerErrorResNotFound |\-1 |找不到對應的解析度檔位。 |
|VeLivePlayerErrorSameRes |\-2 |與目前解析度檔位相同。 |
|VeLivePlayerErrorStatusInvalid |\-3 |播放器狀態不在準備狀態。 |
|VeLivePlayerErrorInvalidRes |\-4 |解析度檔位錯誤。 |
|VeLivePlayerErrorConfigNotSupport |\-5 |不支援組態。 |
|VeLivePlayerErrorFormatNotSupport |\-6 |不支援格式。 |

# VeLivePlayerStreamData

```objectivec
@interface VeLivePlayerStreamData : NSObject
```

拉流位址的組態。

## 成員屬性

|類型 |名稱 |
|---|---|
|BOOL |[enableABR](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-enableabr) |
|BOOL |[enableMainBackupSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-enablemainbackupswitch) |
|BOOL |[enableSmoothSwitchResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-enablesmoothswitchresolution) |
|VeLivePlayerResolution |[defaultResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-defaultresolution) |
|VeLivePlayerFormat |[defaultFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-defaultformat) |
|VeLivePlayerProtocol |[defaultProtocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-defaultprotocol) |
|NSArray<VeLivePlayerStream\*\>\* |[mainStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-mainstream) |
|NSArray<VeLivePlayerStream\*\>\* |[backupStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-backupstream) |

## 說明

### enableABR

```objectivec
@property (nonatomic, assign) BOOL enableABR;
```

是否啟用自適應位元率 (ABR)。預設值為 `NO`。

* `YES`：啟用；

* `NO`：停用。

### enableMainBackupSwitch

```objectivec
@property (nonatomic, assign) BOOL enableMainBackupSwitch;
```

是否啟用主串流與備用串流之間的切換。預設值為 `NO`。

* `YES`：啟用；

* `NO`：停用。

### enableSmoothSwitchResolution

```objectivec
@property (nonatomic, assign) BOOL enableSmoothSwitchResolution;
```

是否啟用平滑解析度切換。預設值為 `NO`。如果啟用，當您呼叫 [switchResolution:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-switchresolution:) 方法手動切換解析度時，SDK 會嘗試執行平滑轉換，避免黑畫面或延遲。有效值：

* `YES`：啟用。

* `NO`：停用。

### defaultResolution

```objectivec
@property (nonatomic, assign) VeLivePlayerResolution defaultResolution;
```

預設解析度。預設值為 `VeLivePlayerResolutionOrigin`，表示原始解析度。詳細資訊請參閱 [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerResolution)。

### defaultFormat

```objectivec
@property (nonatomic, assign) VeLivePlayerFormat defaultFormat;
```

預設影片格式。預設值為 `VeLivePlayerFormatFLV`。詳細資訊請參閱 [VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerFormat)。

### defaultProtocol

```objectivec
@property (nonatomic, assign) VeLivePlayerProtocol defaultProtocol;
```

預設傳輸協定。預設值為 `VeLivePlayerProtocolTCP`。詳細資訊請參閱 [VeLivePlayerProtocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerProtocol)。

### mainStream

```objectivec
@property (nonatomic, copy, nullable) NSArray<VeLivePlayerStream *> * mainStream;
```

主串流位址清單。詳細資訊請參閱 [VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream)。

### backupStream

```objectivec
@property (nonatomic, copy, nullable) NSArray<VeLivePlayerStream *> * backupStream;
```

備用串流位址清單。詳細資訊請參閱 [VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream)。

# VeLivePlayerAudioBufferType

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerAudioBufferType
)
```

音訊的封裝格式。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerAudioBufferUnknown |0 |未知格式。 |
|VeLivePlayerAudioBufferTypeSampleBuffer |1 |CVSampleBufferRef。音訊資料會以 sample buffer 進行處理與轉譯。 |
|VeLivePlayerAudioBufferTypeNSData |2 |NSData。音訊資料會以 NSData 物件進行處理與轉譯。 |

# VeLivePlayerVideoBufferType

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerVideoBufferType
)
```

影片資料的封裝格式。

## 列舉值

|類型 |值 |說明 |
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

傳輸協定。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerProtocolTCP |0 |TCP。 |
|VeLivePlayerProtocolQUIC |1 |QUIC。 |
|VeLivePlayerProtocolTLS |2 |TLS。 |
|VeLivePlayerProtocolHTTP2 |3 |HTTP/2。 |
|VeLivePlayerProtocolDefault |4 |預設值。播放器會從拉流位址自動識別網路協定。目前僅支援自動識別 TCP 和 TLS 協定。對於 QUIC 或 HTTP/2 協定，請使用對應值。 |

# VeLivePlayerFillMode

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerFillMode
)
```

播放器畫面的填滿模式。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerFillModeAspectFill |0 |等比例縮放影片，直到畫面完全填滿。影片部分內容可能會被裁切。 |
|VeLivePlayerFillModeAspectFit |1 |顯示完整影片。影片會等比例縮放，直到影片某一邊達到畫面邊界。畫面上剩餘空間將以黑色填滿。 |
|VeLivePlayerFillModeFullFill |2 |拉伸影片以填滿畫面。影片的寬高比可能會改變。 |

# VeLivePlayerRotation

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerRotation
)
```

影片順時針旋轉角度。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerRotation0 |0 |不旋轉。 |
|VeLivePlayerRotation90 |90 |順時針旋轉 90 度。 |
|VeLivePlayerRotation180 |180 |順時針旋轉 180 度。 |
|VeLivePlayerRotation270 |270 |順時針旋轉 270 度。 |

# VeLivePlayerMirror

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerMirror
)
```

鏡像選項。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerMirrorNone |0 |不鏡像。 |
|VeLivePlayerMirrorHorizontal |1 |水平鏡像。 |
|VeLivePlayerMirrorVertical |2 |垂直鏡像。 |

# VeLivePlayerPixelFormat

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerPixelFormat
)
```

影片影格的像素格式。

## 列舉值

|類型 |值 |說明 |
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

直播播放器的狀態。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerStatusPrepared |0 |播放器完成準備，正在等待轉譯影片。 |
|VeLivePlayerStatusPlaying |1 |目前正在播放，表示第一個影格已轉譯，且播放器未發生錯誤。 |
|VeLivePlayerStatusPaused |2 |播放已暫停。 |
|VeLivePlayerStatusStopped |3 |播放已停止。 |
|VeLivePlayerStatusError |4 |播放器發生錯誤。 |
|VeLivePlayerStatusStalled |5 |播放器發生卡頓。 |

# VeLivePlayerStatistics

```objectivec
@interface VeLivePlayerStatistics : NSObject
```

播放統計資料。

## 成員屬性

|類型 |名稱 |
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

## 說明

### url

```objectivec
@property (nonatomic, strong, readonly, nullable) NSURL* url;
```

目前的拉流位址。

### isHardWareDecode

```objectivec
@property (nonatomic, readonly) BOOL isHardWareDecode;
```

是否使用硬體解碼。

* `YES`：使用硬體解碼；

* `NO`：不使用硬體解碼。

### delayMs

```objectivec
@property (nonatomic, readonly) int delayMs;
```

目前播放延遲，單位為毫秒。

### delayS2sMs

```objectivec
@property (nonatomic, readonly) int delayS2sMs;
```

伺服器到伺服器延遲，單位為毫秒。表示串流從 MediaLive 推流側邊緣節點傳輸至 MediaLive 拉流側邊緣節點所需的時間。當 SEI 訊息未包含串流到達推流側邊緣節點和拉流側邊緣節點時的伺服器時間戳記時，值為 `-1`。

### delayE2eMs

```objectivec
@property (nonatomic, readonly) int delayE2eMs;
```

端到端延遲，單位為毫秒。表示從 Broadcast SDK 將時間戳記寫入 SEI 訊息，到 Player SDK 在本機解析 SEI 訊息所需的時間。準確計算取決於基於 NTP 的時鐘同步。當 SEI 訊息未包含 Broadcast SDK 寫入的時間戳記時，值為 `-1`。

### delayS2eMs

```objectivec
@property (nonatomic, readonly) int delayS2eMs;
```

伺服器到端延遲，單位為毫秒。表示從串流到達 MediaLive 推流側邊緣節點，到 Player SDK 在本機解析 SEI 訊息所需的時間。準確計算取決於基於 NTP 的時鐘同步。當 SEI 訊息未包含串流到達 MediaLive 推流側邊緣節點時的伺服器時間戳記時，值為 `-1`。

### stallTimeMs

```objectivec
@property (nonatomic, readonly) int stallTimeMs;
```

自播放開始以來發生的卡頓累計時長，單位為毫秒。

### bandwidthEstimation

```objectivec
@property (nonatomic, readonly) long bandwidthEstimation;
```

預估頻寬，單位為 kbps。

### videoCodec

```objectivec
@property (nonatomic, copy, readonly, nullable) NSString* videoCodec;
```

影片的編碼格式。

### width

```objectivec
@property (nonatomic, readonly) int width;
```

影片寬度，單位為像素。

### height

```objectivec
@property (nonatomic, readonly) int height;
```

影片高度，單位為像素。

### fps

```objectivec
@property (nonatomic, readonly) float fps;
```

影片影格率，單位為 fps。

### bitrate

```objectivec
@property (nonatomic, readonly) long bitrate;
```

下行位元率，單位為 Kbps。

### videoBufferMs

```objectivec
@property (nonatomic, readonly) long videoBufferMs;
```

影片緩衝，單位為毫秒。

### audioBufferMs

```objectivec
@property (nonatomic, readonly) long audioBufferMs;
```

音訊緩衝，單位為毫秒。

### format

```objectivec
@property (nonatomic, readonly) VeLivePlayerFormat format;
```

影片格式。

### protocol

```objectivec
@property (nonatomic, readonly) VeLivePlayerProtocol protocol;
```

直播串流的傳輸協定。

# VeLivePlayerStreamInfo

```objectivec
@interface VeLivePlayerStreamInfo : NSObject
```

串流資訊。

## 成員屬性

|類型 |名稱 |
|---|---|
|int |[width](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamInfo-width) |
|int |[height](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamInfo-height) |
|int |[bandwidth](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamInfo-bandwidth) |
|NSString\* |[url](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamInfo-url) |

## 說明

### width

```objectivec
@property (nonatomic, assign) int width;
```

影片寬度，單位為像素。

### height

```objectivec
@property (nonatomic, assign) int height;
```

影片高度，單位為像素。

### bandwidth

```objectivec
@property (nonatomic, assign) int bandwidth;
```

影片頻寬，單位為 Bps

### url

```objectivec
@property (nonatomic, copy) NSString *url;
```

影片的 url。

# VeLivePlayerType

```objectivec
typedef NS_ENUM(
    NSUInteger,
    VeLivePlayerType
)
```

播放器類型。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerTypeOwn |0 |自訂播放器。 |
|VeLivePlayerTypeSystem |1 |系統播放器。 |

# VeLivePlayerStreamType

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerStreamType
)
```

直播串流的類型。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerStreamTypeMain |0 |主串流。 |
|VeLivePlayerStreamTypeBackup |1 |備用串流。 |

# VeLivePlayerFormat

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerFormat
)
```

直播串流的格式。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerFormatFLV |0 |FLV。 |
|VeLivePlayerFormatHLS |1 |HLS。 |
|VeLivePlayerFormatRTM |2 |Real Time Media (RTM)。 |

# VeLivePlayerResolution

```objectivec
typedef NS_ENUM(
    NSInteger,
    VeLivePlayerResolution
)
```

播放器解析度。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerResolutionOrigin |0 |原始。 |
|VeLivePlayerResolutionUHD |1 |超高畫質 (UHD)。 |
|VeLivePlayerResolutionFHD |2 |全高畫質 (FHD)。 |
|VeLivePlayerResolutionHD |3 |高畫質 (HD)。 |
|VeLivePlayerResolutionSD |4 |標準畫質 (SD)。 |
|VeLivePlayerResolutionLD |5 |低畫質 (LD)。 |
|VeLivePlayerResolutionAUTO |8 |自動。 |

# VeLivePlayerProperty

```objectivec
typedef NSString * VeLivePlayerProperty;
```

進階組態。

## 成員變數

|名稱 |類型 |
|---|---|
|[VeLivePlayerKeySetParamsHttpHeaders](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerProperty-veliveplayerkeysetparamshttpheaders) |[VeLivePlayerProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerProperty) |
|[VeLivePlayerKeySetParamsLowLatencyFlv](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerProperty-veliveplayerkeysetparamslowlatencyflv) |[VeLivePlayerProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerProperty) |

## 變數說明

### VeLivePlayerKeySetParamsHttpHeaders

```objectivec
OBJC_EXTERN const VeLivePlayerProperty VeLivePlayerKeySetParamsHttpHeaders;
```

為播放器的 HTTP 請求設定自訂 HTTP 標頭。這通常用於傳遞其他資訊，例如驗證權杖、Cookie 或業務追蹤識別碼。如需詳細用法，請參閱[自訂 HTTP 請求標頭](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-3?lang=en#customizing-http-request-headers)。

### VeLivePlayerKeySetParamsLowLatencyFlv

```objectivec
OBJC_EXTERN const VeLivePlayerProperty VeLivePlayerKeySetParamsLowLatencyFlv;
```

設定 FLV 低延遲設定（2–3 秒延遲）。如需詳細用法，請參閱[播放低延遲 FLV 串流](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-3?lang=en#playing-low-latency-flv-streams)。
