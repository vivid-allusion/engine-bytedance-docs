---
title: "Android 版 Player SDK：回呼"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback-zh-TW"
---

# VeLivePlayerObserver

```java
public interface com.ss.videoarch.liveplayer.VeLivePlayerObserver
```

直播播放器觀察者。

## 成員函式

|傳回 |名稱 |
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

## 說明

### onError

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onError(
    VeLivePlayer player,
    VeLivePlayerError error
)
```

當播放器發生錯誤時觸發。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |VeLivePlayer |觸發回呼函式的播放器物件。 |
|error |VeLivePlayerError |錯誤訊息。如需詳細資訊，請參閱 [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-android-api-errorcode#VeLivePlayerError)。 |

### onInfo

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onInfo(
    VeLivePlayer player,
    VeLivePlayerError error
)
```

當播放器遇到內部錯誤時觸發。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |VeLivePlayer |觸發回呼的播放器物件。如需詳細資訊，請參閱 [VeLivePlayer](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer)。 |
|error |VeLivePlayerError |播放器資訊。如需詳細資訊，請參閱 [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-android-api-errorcode#VeLivePlayerError)。 |

### onFirstVideoFrameRender

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onFirstVideoFrameRender(
    VeLivePlayer player,
    boolean isFirstFrame
)
```

在開始播放時或播放期間重試後，轉譯第一個視訊影格時觸發。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |VeLivePlayer |觸發回呼函式的播放器物件。 |
|isFirstFrame |boolean |視訊影格是否為開始播放時轉譯的第一個視訊影格。<br><br><br>* true：視訊影格是開始播放時轉譯的第一個視訊影格；<br><br>* false：視訊影格是播放期間重試後轉譯的第一個視訊影格。 |

### onFirstAudioFrameRender

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onFirstAudioFrameRender(
    VeLivePlayer player,
    boolean isFirstFrame
)
```

在開始播放時或播放期間重試後，轉譯第一個音訊影格時觸發。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |VeLivePlayer |觸發回呼函式的播放器物件。 |
|isFirstFrame |boolean |音訊影格是否為開始播放時轉譯的第一個音訊影格。<br><br><br>* true：音訊影格是開始播放時轉譯的第一個音訊影格；<br><br>* false：音訊影格是播放期間重試後轉譯的第一個音訊影格。 |

### onStallStart

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onStallStart(VeLivePlayer player)
```

播放卡頓開始時觸發。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |VeLivePlayer |觸發回呼函式的播放器物件。 |

### onStallEnd

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onStallEnd(VeLivePlayer player)
```

播放卡頓停止時觸發，也就是有足夠的音訊緩衝後恢復播放時。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |VeLivePlayer |觸發回呼函式的播放器物件。 |

### onVideoRenderStall

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onVideoRenderStall(
    VeLivePlayer player,
    long stallTime
)
```

視訊轉譯卡頓時觸發。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |VeLivePlayer |觸發回呼函式的播放器物件。 |
|stallTime |long |卡頓持續時間，單位為毫秒。 |

### onAudioRenderStall

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onAudioRenderStall(
    VeLivePlayer player,
    long stallTime
)
```

音訊轉譯卡頓時觸發。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |VeLivePlayer |觸發回呼函式的播放器物件。 |
|stallTime |long |卡頓持續時間，單位為毫秒。 |

### onResolutionSwitch

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onResolutionSwitch(
    VeLivePlayer player,
    VeLivePlayerResolution resolution,
    VeLivePlayerError error,
    VeLivePlayerResolutionSwitchReason reason
)
```

視訊解析度變更時觸發。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |VeLivePlayer |觸發回呼函式的播放器物件。 |
|resolution |VeLivePlayerResolution |更新後的解析度。如需詳細資訊，請參閱 [VeLivePlayerResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerResolution)。 |
|error |VeLivePlayerError |解析度切換期間是否發生錯誤。如需詳細資訊，請參閱 [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-android-api-errorcode#VeLivePlayerError)。 |
|reason |VeLivePlayerResolutionSwitchReason |解析度切換的原因。如需詳細資訊，請參閱 [VeLivePlayerResolutionSwitchReason](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerResolutionSwitchReason)。 |

### onVideoSizeChanged

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onVideoSizeChanged(
    VeLivePlayer player,
    int width,
    int height
)
```

視訊大小變更時觸發。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |VeLivePlayer |觸發回呼函式的播放器物件。 |
|width |int |更新後的視訊寬度，單位為像素。 |
|height |int |更新後的視訊高度，單位為像素。 |

### onReceiveSeiMessage

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onReceiveSeiMessage(
    VeLivePlayer player,
    String message
)
```

字串 SEI 訊息回呼。當播放器 SDK 收到 SEI 訊息時會觸發此回呼。必須在 `VeLivePlayerConfiguration` 中啟用 `enableSei` 屬性。啟用 `enableBinarySei` 屬性時，將不再傳送字串 SEI 訊息。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |VeLivePlayer |觸發回呼函式的播放器物件。 |
|message |String |SEI 訊息。 |

### onReceiveBinarySeiMessage

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onReceiveBinarySeiMessage(
    VeLivePlayer player,
    byte[] message
)
```

二進位 SEI 訊息回呼。當播放器 SDK 收到 SEI 訊息時會觸發此回呼。必須在 `VeLivePlayerConfiguration` 中啟用 `enableBinarySei` 屬性。啟用 `enableBinarySei` 屬性時，將不再傳送字串 SEI 訊息。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |VeLivePlayer |觸發回呼函式的播放器物件。 |
|message |byte[] |SEI 訊息。 |

### onMainBackupSwitch

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onMainBackupSwitch(
    VeLivePlayer player,
    VeLivePlayerStreamType streamType,
    VeLivePlayerError error
)
```

播放器在主串流和備用串流之間切換時觸發。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |VeLivePlayer |觸發回呼函式的播放器物件。 |
|streamType |VeLivePlayerStreamType |更新後串流的類型。如需詳細資訊，請參閱 [VeLivePlayerStreamType](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerStreamType)。 |
|error |VeLivePlayerError |切換原因。如需詳細資訊，請參閱 [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-android-api-errorcode#VeLivePlayerError)。 |

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

播放器切換串流格式時觸發。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |VeLivePlayer |觸發回呼的播放器物件。如需詳細資訊，請參閱 [VeLivePlayer](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer)。 |
|fromStreamFormat |VeLivePlayerFormat |切換前的串流格式。如需詳細資訊，請參閱 [VeLivePlayerFormat](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerFormat)。 |
|toStreamFormat |VeLivePlayerFormat |切換後的串流格式。如需詳細資訊，請參閱 [VeLivePlayerFormat](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerFormat)。 |
|error |VeLivePlayerError |串流格式切換的原因。如需詳細資訊，請參閱 [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-android-api-errorcode#VeLivePlayerError)。 |
|extraInfo |Bundle |包含切換相關詳細資料的其他資訊。 |

### onPlayerStatusUpdate

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onPlayerStatusUpdate(
    VeLivePlayer player,
    VeLivePlayerStatus status
)
```

播放狀態變更時觸發。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |VeLivePlayer |播放狀態發生變更的播放器。 |
|status |VeLivePlayerStatus |播放器更新後的狀態。如需詳細資訊，請參閱 [VeLivePlayerStatus](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerStatus)。 |

### onPlayerStatusUpdate

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onPlayerStatusUpdate(
    VeLivePlayer player,
    VeLivePlayerStatus status,
    Bundle extraInfo
)
```

播放狀態變更時觸發。相較於 [onPlayerStatusUpdate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate)，此回呼會透過 `extraInfo` 傳回目前播放串流的補充資訊。

**輸入參數**

|Parameter Name |Type |Description |
|---|---|---|
|player |VeLivePlayer |播放狀態發生變更的播放器。 |
|status |VeLivePlayerStatus |播放器更新後的狀態。如需詳細資訊，請參閱 [VeLivePlayerStatus](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerStatus)。 |
|extraInfo |Bundle |目前播放串流補充資訊的 Bundle。Bundle 可能包含下列鍵：<br><br><br>* `url` (String)：目前正在播放的串流 URL。<br><br>* `all_resolution_urls` (Bundle)：所有解析度的播放位址對應。`Key` 是解析度識別碼，`Value` 是對應的播放 URL。僅在目前串流為多解析度串流時，才會存在此鍵。<br><br>* `resolution` (String)：目前播放串流的解析度識別碼。僅在目前串流為多解析度串流時，才會存在此鍵。<br><br>* `enable_abr` (boolean)：是否啟用 Adaptive Bitrate (ABR)。僅在目前串流為多解析度串流時，才會存在此鍵。有效值：<br><br>   * `true`：已啟用。<br><br>   * `false`：已停用。<br><br>* `enable_smooth_switch_resolution` (boolean)：是否啟用平滑解析度切換。僅在目前串流為多解析度串流時，才會存在此鍵。有效值：<br><br>   * `true`：已啟用。<br><br>   * `false`：已停用。<br><br>* `max_retry_count` (int)：目前串流的最大重試次數。<br><br>* `retry_interval_time_ms` (int)：目前串流的重試間隔，單位為毫秒。<br><br>* `priority` (int)：目前串流在拉流清單中的優先順序。 |

### onStatistics

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onStatistics(
    VeLivePlayer player,
    VeLivePlayerStatistics statistics
)
```

定期觸發，用於回報目前拉流位址、位元率和影格率等資訊。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |VeLivePlayer |觸發回呼函式的播放器物件。 |
|statistics |VeLivePlayerStatistics |播放統計資訊。如需詳細資訊，請參閱 [VeLivePlayerStatistics](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerStatistics)。 |

### onSnapshotComplete

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onSnapshotComplete(
    VeLivePlayer player,
    Bitmap bitmap
)
```

呼叫 [snapshot](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-snapshot) 後擷取螢幕擷取畫面時觸發。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |VeLivePlayer |觸發回呼函式的播放器物件。 |
|bitmap |Bitmap |螢幕擷取畫面的 Bitmap 物件。 |

### onRenderVideoFrame

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onRenderVideoFrame(
    VeLivePlayer player,
    VeLivePlayerVideoFrame videoFrame
)
```

播放器解碼視訊影格時觸發。呼叫 [enableVideoFrameObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-enablevideoframeobserver) 以啟用視訊影格回呼。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |VeLivePlayer |觸發回呼函式的播放器物件。 |
|videoFrame |VeLivePlayerVideoFrame |視訊影格，包含像素格式、封裝格式、視訊寬度和高度，以及其他資訊。如需詳細資訊，請參閱 [VeLivePlayerVideoFrame](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerVideoFrame)。 |

**注意事項**

如果您使用紋理格式進行外部轉譯，建議您在回呼執行緒中轉譯視訊。

### onRenderAudioFrame

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onRenderAudioFrame(
    VeLivePlayer player,
    VeLivePlayerAudioFrame audioFrame
)
```

播放器解碼音訊影格時觸發。呼叫 [enableAudioFrameObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-enableaudioframeobserver) 以啟用音訊影格回呼。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |VeLivePlayer |觸發回呼函式的播放器物件。 |
|audioFrame |VeLivePlayerAudioFrame |音訊影格。如需詳細資訊，請參閱 [VeLivePlayerAudioFrame](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerAudioFrame)。 |

**注意事項**

回呼傳回的音訊資料類型為 Float32，並採用大端位元組序。

### onStreamFailedOpenSuperResolution

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onStreamFailedOpenSuperResolution(
    VeLivePlayer player,
    VeLivePlayerError error
)
```

呼叫 [setEnableSuperResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setenablesuperresolution) 後，SDK 無法啟用超解析度時觸發。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |VeLivePlayer |觸發回呼函式的播放器物件。 |
|error |VeLivePlayerError |失敗原因。如需詳細資訊，請參閱 [VeLivePlayerErrorCode](https://docs.byteplus.com/en/docs/24/docs-player-android-api-errorcode#VeLivePlayerErrorCode)。 |

### onStreamFailedOpenSharpen

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onStreamFailedOpenSharpen(
    VeLivePlayer player,
    VeLivePlayerError error
)
```

呼叫 [setEnableSharpen](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setenablesharpen) 後，SDK 無法啟用銳化時觸發。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|player |VeLivePlayer |觸發回呼函式的播放器物件。 |
|error |VeLivePlayerError |失敗原因。如需詳細資訊，請參閱 VeLivePlayerErrorCode。 |
