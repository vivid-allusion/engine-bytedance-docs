---
title: "iOS Player SDK：回呼"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback-zh-TW"
---

# VeLivePlayerObserver

```objectivec
@protocol VeLivePlayerObserver <NSObject>
```

直播播放器觀察者。

## 成員函式

|傳回值 |名稱 |
|---|---|
|void |[onError:error:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onerror-error) |
|void |[onInfo:info:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-oninfo-info) |
|void |[onFirstVideoFrameRender:isFirstFrame:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onfirstvideoframerender-isfirstframe) |
|void |[onFirstAudioFrameRender:isFirstFrame:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onfirstaudioframerender-isfirstframe) |
|void |[onStallStart:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstallstart) |
|void |[onStallEnd:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstallend) |
|void |[onVideoRenderStall:stallTime:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onvideorenderstall-stalltime) |
|void |[onAudioRenderStall:stallTime:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onaudiorenderstall-stalltime) |
|void |[onResolutionSwitch:resolution:error:reason:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onresolutionswitch-resolution-error-reason) |
|void |[onVideoSizeChanged:width:height:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onvideosizechanged-width-height) |
|void |[onReceiveSeiMessage:message:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onreceiveseimessage-message) |
|void |[onReceiveBinarySeiMessage:message:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onreceivebinaryseimessage-message) |
|void |[onMainBackupSwitch:streamType:error:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onmainbackupswitch-streamtype-error) |
|void |[onStreamFormatSwitch:fromStreamFormat:toStreamFormat:error:extraInfo:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstreamformatswitch-fromstreamformat-tostreamformat-error-extrainfo) |
|void |[onPlayerStatusUpdate:status:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status) |
|void |[onPlayerStatusUpdate:status:extraInfo:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status-extrainfo) |
|void |[onStatistics:statistics:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstatistics-statistics) |
|void |[onSnapshotComplete:image:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onsnapshotcomplete-image) |
|void |[onRenderVideoFrame:videoFrame:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onrendervideoframe-videoframe) |
|void |[onRenderAudioFrame:audioFrame:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onrenderaudioframe-audioframe) |
|void |[onStreamFailedOpenSuperResolution:error:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution-error) |
|nullable NSData\* |[getDrmResourceLoaderCertificateData:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-getdrmresourceloadercertificatedata) |
|nullable NSString\* |[getDrmResourceLoaderLicenseUrl:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-getdrmresourceloaderlicenseurl) |

## 說明

### onError:error:

```objectivec
- (void)onError:(TVLManager *_Nonnull)player error:(VeLivePlayerError *_Nonnull)error;
```

播放器發生錯誤時發生。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |觸發回呼函式的播放器物件。 |
|error |VeLivePlayerError\* |錯誤訊息。如需詳細資訊，請參閱 [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError)。 |

### onInfo:info:

```objectivec
- (void)onInfo:(TVLManager *_Nonnull)player info:(VeLivePlayerError *_Nonnull)info;
```

播放器遇到內部錯誤時觸發。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |觸發回呼的播放器物件。如需詳細資訊，請參閱 [TVLManager](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer))。 |
|info |VeLivePlayerError\* |播放器資訊。如需詳細資訊，請參閱 [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError)。 |

### onFirstVideoFrameRender:isFirstFrame:

```objectivec
- (void)onFirstVideoFrameRender:(TVLManager *_Nonnull)player isFirstFrame:(BOOL)isFirstFrame;
```

播放開始時，或播放期間重試後，算繪第一個視訊畫面時發生。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |觸發回呼函式的播放器物件。 |
|isFirstFrame |BOOL |視訊畫面是否為播放開始時算繪的第一個視訊畫面。<br><br><br>* `YES`：視訊畫面是播放開始時算繪的第一個視訊畫面；<br><br>* `NO`：視訊畫面是播放期間重試後算繪的第一個視訊畫面。 |

### onFirstAudioFrameRender:isFirstFrame:

```objectivec
- (void)onFirstAudioFrameRender:(TVLManager *_Nonnull)player isFirstFrame:(BOOL)isFirstFrame;
```

播放開始時，或播放期間重試後，算繪第一個音訊畫面時發生。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |觸發回呼函式的播放器物件。 |
|isFirstFrame |BOOL |音訊畫面是否為播放開始時算繪的第一個音訊畫面。<br><br><br>* `YES`：音訊畫面是播放開始時算繪的第一個音訊畫面；<br><br>* `NO`：音訊畫面是播放期間重試後算繪的第一個音訊畫面。 |

### onStallStart:

```objectivec
- (void)onStallStart:(TVLManager *_Nonnull)player;
```

播放卡頓開始時發生。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |觸發回呼函式的播放器物件。 |

### onStallEnd:

```objectivec
- (void)onStallEnd:(TVLManager *_Nonnull)player;
```

播放卡頓停止時發生，也就是有足夠音訊緩衝後恢復播放時。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |觸發回呼函式的播放器物件。 |

### onVideoRenderStall:stallTime:

```objectivec
- (void)onVideoRenderStall:(TVLManager *_Nonnull)player stallTime:(int64_t)stallTime;
```

視訊算繪卡頓時發生。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |觸發回呼函式的播放器物件。 |
|stallTime |int64_t |卡頓持續時間，單位為毫秒。 |

### onAudioRenderStall:stallTime:

```objectivec
- (void)onAudioRenderStall:(TVLManager *_Nonnull)player stallTime:(int64_t)stallTime;
```

音訊算繪卡頓時發生。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |觸發回呼函式的播放器物件。 |
|stallTime |int64_t |卡頓持續時間，單位為毫秒。 |

### onResolutionSwitch:resolution:error:reason:

```objectivec
- (void)onResolutionSwitch:(TVLManager *_Nonnull)player resolution:(VeLivePlayerResolution)resolution error:(VeLivePlayerError *)error reason:(VeLivePlayerResolutionSwitchReason)reason;
```

視訊解析度變更時發生。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |觸發回呼函式的播放器物件。 |
|resolution |VeLivePlayerResolution |更新後的解析度。如需詳細資訊，請參閱 [VeLivePlayerResolution](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerResolution)。 |
|error |VeLivePlayerError\* |解析度切換期間是否發生錯誤。如需詳細資訊，請參閱 [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError)。 |
|reason |VeLivePlayerResolutionSwitchReason |解析度切換的原因。如需詳細資訊，請參閱 [VeLivePlayerResolutionSwitchReason](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerResolutionSwitchReason)。 |

### onVideoSizeChanged:width:height:

```objectivec
- (void)onVideoSizeChanged:(TVLManager *_Nonnull)player width:(int)width height:(int)height;
```

視訊大小變更時發生。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |觸發回呼函式的播放器物件。 |
|width |int |更新後的視訊寬度，單位為像素。 |
|height |int |更新後的視訊高度，單位為像素。 |

### onReceiveSeiMessage:message:

```objectivec
- (void)onReceiveSeiMessage:(TVLManager *_Nonnull)player message:(NSString *_Nonnull)message;
```

字串 SEI 訊息回呼。播放器 SDK 收到 SEI 訊息時會觸發此回呼。必須在 `VeLivePlayerConfiguration` 中啟用 `enableSei` 屬性。啟用 `enableBinarySei` 屬性時，將不再傳送字串 SEI 訊息。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |觸發回呼函式的播放器物件。 |
|message |NSString\* |SEI 訊息。 |

### onReceiveBinarySeiMessage:message:

```objectivec
- (void)onReceiveBinarySeiMessage:(TVLManager *_Nonnull)player message:(NSData *_Nonnull)message;
```

二進位 SEI 訊息回呼。播放器 SDK 收到 SEI 訊息時會觸發此回呼。必須在 `VeLivePlayerConfiguration` 中啟用 `enableBinarySei` 屬性。啟用 `enableBinarySei` 屬性時，將不再傳送字串 SEI 訊息。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |觸發回呼函式的播放器物件。 |
|message |NSData\* |SEI 訊息。 |

### onMainBackupSwitch:streamType:error:

```objectivec
- (void)onMainBackupSwitch:(TVLManager *_Nonnull)player streamType:(VeLivePlayerStreamType)streamType error:(VeLivePlayerError *)error;
```

播放器在主串流和備用串流之間切換時發生。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |觸發回呼函式的播放器物件。 |
|streamType |VeLivePlayerStreamType |更新後的串流類型。如需詳細資訊，請參閱 [VeLivePlayerStreamType](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamType)。 |
|error |VeLivePlayerError\* |切換原因。如需詳細資訊，請參閱 [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError)。 |

### onStreamFormatSwitch:fromStreamFormat:toStreamFormat:error:extraInfo:

```objectivec
- (void)onStreamFormatSwitch:(TVLManager *_Nonnull)player fromStreamFormat:(VeLivePlayerFormat)fromStreamType toStreamFormat:(VeLivePlayerFormat)toStreamType error:(VeLivePlayerError *)error extraInfo:(nullable NSDictionary *)extraInfo;
```

播放器切換串流格式時觸發。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |觸發回呼的播放器物件。如需詳細資訊，請參閱 [TVLManager](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer))。 |
|fromStreamType |VeLivePlayerFormat |切換前的串流格式。如需詳細資訊，請參閱 [VeLivePlayerFormat](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerFormat)。 |
|toStreamType |VeLivePlayerFormat |切換後的串流格式。如需詳細資訊，請參閱 [VeLivePlayerFormat](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerFormat)。 |
|error |VeLivePlayerError\* |串流格式切換的原因。如需詳細資訊，請參閱 [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError)。 |
|extraInfo |nullable NSDictionary\* |包含切換相關詳細資料的其他資訊。 |

### onPlayerStatusUpdate:status:

```objectivec
- (void)onPlayerStatusUpdate:(TVLManager *_Nonnull)player status:(VeLivePlayerStatus)status;
```

播放狀態變更時發生。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |播放狀態變更的播放器。 |
|status |VeLivePlayerStatus |更新後的播放器狀態。如需詳細資訊，請參閱 [VeLivePlayerStatus](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatus)。 |

### onPlayerStatusUpdate:status:extraInfo:

```objectivec
- (void)onPlayerStatusUpdate:(TVLManager *_Nonnull)player status:(VeLivePlayerStatus)status extraInfo:(nullable NSDictionary *)extraInfo;
```

播放狀態變更時發生。相較於 [onPlayerStatusUpdate:status:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status)，此回呼會透過 `extraInfo` 傳回目前播放串流的補充資訊。

**輸入參數**

|參數名稱 |類型 |描述 |
|---|---|---|
|player |TVLManager\* |播放狀態變更的播放器。 |
|status |VeLivePlayerStatus |更新後的播放器狀態。如需詳細資訊，請參閱 [VeLivePlayerStatus](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatus)。 |
|extraInfo |nullable NSDictionary\* |目前播放串流補充資訊的字典。字典可能包含以下鍵：<br><br><br>* `url` (NSString)：目前播放串流的 URL。<br><br>* `all_resolution_urls` (NSDictionary<NSString \*, NSString \*\>)：所有解析度的播放位址對應。`Key` 是解析度識別碼，`Value` 是對應的播放 URL。只有目前串流是多解析度串流時，才會存在此鍵。<br><br>* `resolution` (NSString)：目前播放串流的解析度識別碼。只有目前串流是多解析度串流時，才會存在此鍵。<br><br>* `enable_abr` (NSNumber)：是否啟用 Adaptive Bitrate (ABR)。只有目前串流是多解析度串流時，才會存在此鍵。有效值：<br><br>   * `YES`：已啟用。<br><br>   * `NO`：已停用。<br><br>* `enable_smooth_switch_resolution` (NSNumber)：是否啟用平滑解析度切換。只有目前串流是多解析度串流時，才會存在此鍵。有效值：<br><br>   * `YES`：已啟用。<br><br>   * `NO`：已停用。<br><br>* `max_retry_count` (NSNumber, NSInteger)：目前串流的最大重試次數。<br><br>* `retry_interval_time_ms` (NSNumber, NSInteger)：目前串流的重試間隔，單位為毫秒。<br><br>* `priority` (NSNumber, NSInteger)：目前串流在拉流清單中的優先順序。 |

### onStatistics:statistics:

```objectivec
- (void)onStatistics:(TVLManager *_Nonnull)player statistics:(VeLivePlayerStatistics *_Nonnull)statistics;
```

定期發生，用於報告目前拉流位址、位元率和影格率等資訊。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |觸發回呼函式的播放器物件。 |
|statistics |VeLivePlayerStatistics\* |播放統計資料。如需詳細資訊，請參閱 [VeLivePlayerStatistics](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics)。 |

### onSnapshotComplete:image:

```objectivec
- (void)onSnapshotComplete:(TVLManager *_Nonnull)player image:(UIImage *_Nonnull)image;
```

呼叫 snapshot 後完成螢幕擷取畫面時發生。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |觸發回呼函式的播放器物件。 |
|image |UIImage\* |螢幕擷取畫面的 UIImage 物件。 |

### onRenderVideoFrame:videoFrame:

```objectivec
- (void)onRenderVideoFrame:(TVLManager *_Nonnull)player videoFrame:(VeLivePlayerVideoFrame *_Nonnull)videoFrame;
```

播放器解碼視訊畫面時發生。呼叫 [enableVideoFrameObserver:pixelFormat:bufferType:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enablevideoframeobserver-pixelformat-buffertype) 以啟用視訊畫面回呼。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |觸發回呼函式的播放器物件。 |
|videoFrame |VeLivePlayerVideoFrame\* |視訊畫面，包含像素格式、封裝格式、視訊寬度和高度，以及其他資訊。如需詳細資訊，請參閱 [VeLivePlayerVideoFrame](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame)。 |

**注意事項**

如果您使用紋理格式進行外部算繪，建議在回呼執行緒中算繪視訊。

### onRenderAudioFrame:audioFrame:

```objectivec
- (void)onRenderAudioFrame:(TVLManager *_Nonnull)player audioFrame:(VeLivePlayerAudioFrame *_Nonnull)audioFrame;
```

播放器解碼音訊畫面時發生。呼叫 [enableAudioFrameObserver:enableRendering:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enableaudioframeobserver-enablerendering) 以啟用音訊畫面回呼。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |觸發回呼函式的播放器物件。 |
|audioFrame |VeLivePlayerAudioFrame\* |音訊畫面。如需詳細資訊，請參閱 [VeLivePlayerAudioFrame](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame)。 |

**注意事項**

回呼傳回的音訊資料類型為 Float32，且採用大端位元組順序。

### onStreamFailedOpenSuperResolution:error:

```objectivec
- (void)onStreamFailedOpenSuperResolution:(TVLManager *_Nonnull)player error:(VeLivePlayerError *_Nullable)error;
```

呼叫 [setEnableSuperResolution:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setenablesuperresolution) 後，SDK 無法啟用超解析度時發生。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |觸發回呼函式的播放器物件。 |
|error |VeLivePlayerError\* |失敗原因。如需詳細資訊，請參閱 [VeLivePlayerErrorCode](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api-error-code#VeLivePlayerErrorCode)。 |

### getDrmResourceLoaderCertificateData:

```objectivec
- (nullable NSData *)getDrmResourceLoaderCertificateData:(nonnull TVLManager *_Nonnull)player;
```

您需要在此回呼中傳回 NSData 格式的 FairPlay 憑證。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |觸發回呼的播放器執行個體。 |

### getDrmResourceLoaderLicenseUrl:

```objectivec
- (nullable NSString *)getDrmResourceLoaderLicenseUrl:(nonnull TVLManager *_Nonnull)player;
```

您需要在此回呼中傳回 DRM 授權的 URL。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |TVLManager\* |觸發回呼的播放器執行個體。 |
