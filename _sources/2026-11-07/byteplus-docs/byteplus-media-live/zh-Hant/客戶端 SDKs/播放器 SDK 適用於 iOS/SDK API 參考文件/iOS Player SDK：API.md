---
title: "iOS Player SDK：API"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api-zh-TW"
---

# TVLManager(VeLivePlayer)

```objectivec
@interface TVLManager (VeLivePlayer)
```

直播播放器。

## 成員屬性

|類型 |名稱 |
|---|---|
|id |[observer](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-observer) |
|UIView\* |[playerView](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-playerview) |
|float |[volume](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-volume) |
|BOOL |[isPlaying](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-isplaying) |

## 靜態函式

|傳回 |名稱 |
|---|---|
|void |[setLogLevel:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setloglevel) |
|NSString\* |[getVersion](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-getversion) |

## 成員函式

|傳回 |名稱 |
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

## 說明

### observer

```objectivec
@property (nonatomic, weak, readonly, nullable) id<VeLivePlayerObserver> observer;
```

播放器觀察者。

### playerView

```objectivec
@property (nonatomic, strong, readonly) UIView *playerView;
```

播放器用於算繪影片的檢視。將 `playerView` 新增至應用程式的檢視階層，以顯示影片內容。

### volume

```objectivec
@property (nonatomic, assign) float volume;
```

播放器音量。預設值為 `1.0`。取值範圍為 [0.0, 1.0]。

### isPlaying

```objectivec
@property (nonatomic, assign, readonly) BOOL isPlaying;
```

檢查播放器是否正在播放。

## 說明

### setLogLevel:

```objectivec
+ (void)setLogLevel:(VeLivePlayerLogLevel)logLevel;
```

設定輸出日誌層級。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|logLevel |VeLivePlayerLogLevel |輸出日誌層級。如需詳細資訊，請參閱 [VeLivePlayerLogLevel](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerLogLevel)。 |

### getVersion

```objectivec
+ (NSString *_Nonnull )getVersion;
```

取得 Player SDK 的版本號碼。

**傳回值**

Player SDK 的版本號碼。

### init

```objectivec
- (instancetype)init;
```

初始化播放器。

### initWithType:

```objectivec
- (instancetype)initWithType:(VeLivePlayerType)type;
```

初始化指定類型的播放器。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|type |VeLivePlayerType |播放器類型。如需詳細資訊，請參閱 [VeLivePlayerType](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerType)。 |

### setConfig:

```objectivec
- (void)setConfig:(VeLivePlayerConfiguration *_Nonnull)config;
```

設定播放器設定，包括是否開啟 SEI 訊息、硬體解碼和本機 DNS 預先擷取。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|config |VeLivePlayerConfiguration\* |播放器設定。如需詳細資訊，請參閱 [VeLivePlayerConfiguration](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration)。 |

**注意事項**

請在呼叫 play 前呼叫此方法。

### setObserver:

```objectivec
- (void)setObserver:(id<VeLivePlayerObserver> _Nullable)observer;
```

設定播放器觀察者，以監聽 VeLivePlayer 的事件，例如播放錯誤或狀態更新、第一個音訊和影片影格的算繪，以及解析度切換。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|observer |id |播放器觀察者。如需詳細資訊，請參閱 [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver)。 |

**注意事項**

請在呼叫 play 前呼叫此方法。

### setRenderFillMode:

```objectivec
- (void)setRenderFillMode:(VeLivePlayerFillMode)fillMode;
```

設定播放器畫面的填滿模式。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|fillMode |VeLivePlayerFillMode |SurfaceView 的填滿模式。預設值為 `VeLivePlayerFillModeAspectFill`。如需詳細資訊，請參閱 [VeLivePlayerFillMode](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerFillMode)。 |

**注意事項**

* 請在呼叫 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-play) 前呼叫此方法，以設定播放器的初始填滿模式。

* 您可以在播放期間呼叫此方法，以動態調整填滿模式。

### setPlayUrl:

```objectivec
- (void)setPlayUrl:(NSString *_Nonnull)url;
```

設定拉流位址。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|url |NSString\* |拉流位址。 |

**注意事項**

請在呼叫 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-play) 前呼叫此方法。

### setUrlHostIP:

```objectivec
- (void)setUrlHostIP:(NSDictionary *_Nonnull)hostIpMap;
```

設定網域名稱到伺服器 IP 位址的對應。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|hostIpMap |NSDictionary\* |網域名稱到伺服器 IP 位址的對應。`Map` 物件以網域名稱作為鍵，對應值為與該網域關聯的伺服器 IP 位址清單。值為 `List` 類型。 |

### setProperty:value:

```objectivec
- (void)setProperty:(NSString *_Nonnull)key value:(id _Nonnull)value;
```

設定播放器的進階設定，包括離屏算繪、最大緩衝區持續時間和自適應位元率（ABR）演算法。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|key |NSString\* |進階設定的參數名稱。 |
|value |id |進階設定的參數值。 |

### setPlayStreamData:

```objectivec
- (void)setPlayStreamData:(VeLivePlayerStreamData *_Nonnull)streamData;
```

設定多個直播串流。如果需要啟用需要多個直播串流的功能，請呼叫此方法，例如自適應位元率（ABR）、手動解析度切換，以及主備串流。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|streamData |VeLivePlayerStreamData\* |多個拉流位址的設定。如需詳細資訊，請參閱 [VeLivePlayerStreamData](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData)。 |

**注意事項**

請在呼叫 play 前呼叫此方法。

### play

```objectivec
- (void)play;
```

開始或繼續播放。

**注意事項**

呼叫此方法後，播放器完成拉流準備，以及算繪第一個影格時，都會觸發 [onPlayerStatusUpdate:status:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status) 回呼。

### stop

```objectivec
- (void)stop;
```

停止播放。此方法不會銷毀播放器。

**注意事項**

呼叫此方法後播放停止時，會觸發 [onPlayerStatusUpdate:status:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status) 回呼。

### destroy

```objectivec
- (void)destroy;
```

停止播放並銷毀播放器。

### isSupportResolutionSwitch:

```objectivec
- (int)isSupportResolutionSwitch:(VeLivePlayerResolution)resolution;
```

檢查播放器目前是否支援指定的解析度層級。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|resolution |VeLivePlayerResolution |解析度層級。如需詳細資訊，請參閱 [VeLivePlayerResolution](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerResolution)。 |

**傳回值**

* 0：支援；

* 其他：不支援。如需其他傳回值的詳細資訊，請參閱 [VeLivePlayerSupportResolutionSwitchError](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerSupportResolutionSwitchError)。

### switchResolution:

```objectivec
- (void)switchResolution:(VeLivePlayerResolution)resolution;
```

變更影片解析度。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|resolution |VeLivePlayerResolution |影片解析度。如需詳細資訊，請參閱 [VeLivePlayerResolution](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerResolution)。 |

**傳回值**

* `YES`：成功；

* `NO`：失敗。

**注意事項**

* 呼叫此方法前，請呼叫 [setPlayStreamData:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setplaystreamdata) 以設定多個解析度。

* 呼叫此方法後，一旦播放器切換至新解析度，會觸發 [onResolutionSwitch:resolution:error:reason:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onresolutionswitch-resolution-error-reason) 回呼。

* 為避免切換解析度時出現黑畫面或延遲，請將 [enableSmoothSwitchResolution](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-enablesmoothswitchresolution) 設定為 `YES`。

### setMute:

```objectivec
- (void)setMute:(BOOL)mute;
```

設定是否將播放靜音。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|mute |BOOL |是否將播放靜音。預設值為 `NO`。<br><br><br>* `YES`：靜音；<br><br>* `NO`：不靜音。 |

### isMute

```objectivec
- (BOOL)isMute;
```

檢查播放是否已靜音。

**傳回值**

播放是否已靜音。

* `YES`：已靜音；

* `NO`：未靜音。

### setRenderRotation:

```objectivec
- (void)setRenderRotation:(VeLivePlayerRotation)rotation;
```

設定影片順時針旋轉角度。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|rotation |VeLivePlayerRotation |影片順時針旋轉角度。預設停用旋轉。如需詳細資訊，請參閱 [VeLivePlayerRotation](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerRotation)。 |

**注意事項**

* 您可以在播放前和播放期間變更旋轉角度。

* 每次呼叫此方法時，播放器都會根據原始影片旋轉影片。

* 對影片同時套用旋轉和鏡像時，播放器會先鏡像影片，再旋轉影片。

### setRenderMirror:

```objectivec
- (void)setRenderMirror:(VeLivePlayerMirror)mirror;
```

設定鏡像設定。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|mirror |VeLivePlayerMirror |鏡像設定。預設停用鏡像。如需詳細資訊，請參閱 [VeLivePlayerMirror](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerMirror)。 |

**注意事項**

* 您可以在播放前和播放期間變更鏡像設定。

* 每次呼叫此方法時，播放器都會將鏡像設定套用至原始影片。

* 對影片同時套用旋轉和鏡像時，播放器會先鏡像影片，再旋轉影片。

### snapshot

```objectivec
- (int)snapshot;
```

擷取影片螢幕截圖。

**傳回值**

* 0：允許擷取螢幕截圖；

* VeLivePlayerErrorRefused：不允許擷取螢幕截圖。

**注意事項**

* 此方法僅在播放期間生效。

* 呼叫此方法後擷取螢幕截圖時，會觸發 [onSnapshotComplete:image:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onsnapshotcomplete-image) 回呼，其中包含螢幕截圖的 `UIImage` 物件。

### enableVideoFrameObserver:pixelFormat:bufferType:

```objectivec
- (void)enableVideoFrameObserver:(BOOL)enable pixelFormat:(VeLivePlayerPixelFormat)pixelFormat bufferType:(VeLivePlayerVideoBufferType)bufferType;
```

設定影片影格觀察者。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|enable |BOOL |是否啟用影片影格回呼。預設值為 `NO`。<br><br><br>* `YES`：啟用；<br><br>* `NO`：停用。 |
|pixelFormat |VeLivePlayerPixelFormat |回呼中影片影格的像素格式。如需詳細資訊，請參閱 [VeLivePlayerPixelFormat](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerPixelFormat)。 |
|bufferType |VeLivePlayerVideoBufferType |回呼中影片資料的封裝格式。如需詳細資訊，請參閱 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoBufferType)。 |

**注意事項**

* 您可以呼叫此方法，以訂閱解碼後的影片資料並用於外部算繪。

* 呼叫此方法後，SDK 收到影片影格時會觸發 onRenderVideoFrame:videoFrame:is。回呼包含影片影格的詳細資訊。

* 如果使用外部算繪，您需要確保影片與音訊同步。

### enableAudioFrameObserver:enableRendering:

```objectivec
- (void)enableAudioFrameObserver:(BOOL)enable enableRendering:(BOOL)enableRendering;
```

設定音訊影格觀察者。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|enable |BOOL |是否啟用音訊影格回呼。預設值為 `NO`。<br><br><br>* `YES`：啟用；<br><br>* `NO`：停用。 |
|enableRendering |BOOL |是否啟用播放器算繪。預設值為 `NO`。<br><br><br>* `YES`：啟用；<br><br>* `NO`：停用。 |

**注意事項**

* 您可以呼叫此方法，以訂閱解碼後的音訊資料並用於外部算繪。

* 呼叫此方法後，SDK 收到音訊影格時會觸發 [onRenderAudioFrame:audioFrame:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onrenderaudioframe-audioframe) 回呼。回呼包含音訊影格的詳細資訊。

* 如果使用外部算繪，您需要確保影片與音訊同步。

### setEnableSuperResolution:

```objectivec
- (void)setEnableSuperResolution:(BOOL)enable;
```

啟用或停用超解析度。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|enable |BOOL |是否啟用超解析度。預設值為 `NO`。<br><br><br>* `YES`：開啟；<br><br>* `NO`：關閉。 |

**注意事項**

* 請在收到 onFirstVideoFrameRender:isFirstFrame:callback 後，或在播放期間呼叫此方法。

* 支援在播放期間呼叫此方法，以開啟或關閉超解析度。

* 如果 SDK 因裝置型號、影片解析度或影格率而無法啟用超解析度，您將收到 [onStreamFailedOpenSuperResolution:error:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution-error)。

### setEnableSharpen:

```objectivec
- (void)setEnableSharpen:(BOOL)enable;
```

設定是否啟用影片銳化。啟用後，影片中的邊緣和細節會更明顯，使視覺效果更清晰鮮明。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|enable |BOOL |是否啟用影片銳化。預設值為 `NO`。有效值：<br><br><br>* `YES`：啟用。<br><br>* `NO`：停用。 |

### getStreamList

```objectivec
- (NSArray<VeLivePlayerStreamInfo *> *)getStreamList;
```

取得串流資訊。

**傳回值**

串流資訊。

**注意事項**

* 當 [VeLivePlayerStatus](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatus)（播放器狀態）為 `VeLivePlayerStatusPrepared` 時，呼叫此方法。

* 此方法目前僅適用於 HLS 格式串流。

# TVLManager(PictureInPicture)

```objective-c
@interface TVLManager (PictureInPicture)
```

直播播放器的子母畫面（PiP）功能。

## 成員變數

|名稱 |類型 |
|---|---|
|[enablePictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-enablepictureinpicture) |BOOL |
|[pictureInPictureRequiresLinearPlayback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-pictureinpicturerequireslinearplayback) |BOOL |
|[canStartPictureInPictureAutomaticallyFromInline](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-canstartpictureinpictureautomaticallyfrominline) |BOOL |
|[avPictureInPictureController](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-avpictureinpicturecontroller) |AVPictureInPictureController \* |
|[pictureInPictureDelegate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-pictureinpicturedelegate) |id |
|[pictureInPicturePlaybackDelegate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-pictureinpictureplaybackdelegate) |id |

## 靜態函式

|名稱 |傳回 |
|---|---|
|[isPictureInPictureSupported](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-ispictureinpicturesupported) |BOOL |
|[isPictureInPictureStarted](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-ispictureinpicturestarted) |BOOL |

## 成員函式

|名稱 |傳回 |
|---|---|
|[startPictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-startpictureinpicture) |void |
|[stopPictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-stoppictureinpicture) |void |
|[invalidatePictureInPicturePlaybackState](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-invalidatepictureinpictureplaybackstate) |void |

## 變數說明

### enablePictureInPicture

```objective-c
@property (nonatomic, assign) BOOL enablePictureInPicture;
```

是否啟用 PiP 功能。預設值為 `NO`。

* `YES`：啟用 PiP 功能。之後，您可以呼叫 PiP 相關方法或設定 PiP 相關屬性。

* `NO`：停用 PiP 功能。

**注意**

將此屬性設定為 `YES` 前，請確保符合以下條件：

* 系統執行 iOS 15.0 或更新版本。

* 應用程式已在 **Background Modes** 中啟用 **Audio, AirPlay, and Picture in Picture**。

### pictureInPictureRequiresLinearPlayback

```objective-c
@property (nonatomic, assign) BOOL pictureInPictureRequiresLinearPlayback;
```

PiP 視窗中是否隱藏快轉和倒轉按鈕。預設值為 `YES`。有效值：

* `YES`：隱藏快轉和倒轉按鈕。

* `NO`：顯示快轉和倒轉按鈕。

### canStartPictureInPictureAutomaticallyFromInline

```objective-c
@property (nonatomic, assign) BOOL canStartPictureInPictureAutomaticallyFromInline;
```

應用程式移至背景時，PiP 是否可以自動啟動。預設值為 `YES`。有效值：

* `YES`：允許系統在應用程式移至背景時嘗試自動啟動 PiP。

* `NO`：防止系統在應用程式移至背景時自動啟動 PiP。

### avPictureInPictureController

```objective-c
@property (nonatomic, strong, readonly, nullable) AVPictureInPictureController *avPictureInPictureController;
```

與目前播放器關聯的 [AVPictureInPictureController](https://developer.apple.com/documentation/AVKit/AVPictureInPictureController) 執行個體，可用於讀取系統層級的 PiP 狀態和相關資訊。

### pictureInPictureDelegate

```objective-c
@property (nonatomic, weak, nullable) id<AVPictureInPictureControllerDelegate> pictureInPictureDelegate API_AVAILABLE(ios(15.0));
```

實作 [AVPictureInPictureControllerDelegate](https://developer.apple.com/documentation/avkit/avpictureinpicturecontrollerdelegate) 的委派物件，用於接收 PiP 生命週期回呼，例如開始、停止和失敗事件。

**注意**

SDK 提供基本 PiP 功能。若要自訂相關委派回呼的處理方式，請將此屬性設定為您的委派物件。此屬性僅在同時符合以下條件時生效：

* 系統執行 iOS 15.0 或更新版本。

* [enablePictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-enablepictureinpicture) 屬性設定為 `YES`。

### pictureInPicturePlaybackDelegate

```objective-c
@property (nonatomic, weak, nullable) id<AVPictureInPictureSampleBufferPlaybackDelegate> pictureInPicturePlaybackDelegate API_AVAILABLE(ios(15.0));
```

實作 [AVPictureInPictureSampleBufferPlaybackDelegate](https://developer.apple.com/documentation/avkit/avpictureinpicturesamplebufferplaybackdelegate) 的委派物件，用於處理 PiP 中的播放和暫停要求，判斷 PiP 視窗中的播放控制項應顯示播放或暫停，並提供可播放時間範圍。

**注意**

SDK 提供基本 PiP 功能。若要自訂相關委派回呼的處理方式，請將此屬性設定為您的委派物件。此屬性僅在同時符合以下條件時生效：

* 系統執行 iOS 15.0 或更新版本。

* [enablePictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-enablepictureinpicture) 屬性設定為 `YES`。

## 函式說明

### isPictureInPictureSupported

```objective-c
+ (BOOL) isPictureInPictureSupported;
```

目前裝置是否支援 PiP。

**傳回值**

* `YES`：支援。

* `NO`：不支援。

### isPictureInPictureStarted

```objective-c
+ (BOOL) isPictureInPictureStarted;
```

PiP 是否已成功啟動。

**傳回值**

* `YES`：PiP 已成功啟動。

* `NO`：PiP 尚未啟動。

### startPictureInPicture

```objective-c
- (void) startPictureInPicture;
```

手動啟動 PiP。

### stopPictureInPicture

```objective-c
- (void) stopPictureInPicture;
```

手動停止 PiP 並關閉 PiP 視窗。

### invalidatePictureInPicturePlaybackState

```objective-c
- (void) invalidatePictureInPicturePlaybackState;
```

手動更新 PiP 視窗中的播放/暫停按鈕狀態和進度顯示。
