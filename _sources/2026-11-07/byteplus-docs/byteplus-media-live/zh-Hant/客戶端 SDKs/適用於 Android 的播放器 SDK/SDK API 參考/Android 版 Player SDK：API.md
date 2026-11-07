---
title: "Android 版 Player SDK：API"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference-zh-TW"
---

# VeLivePlayer

```java
public abstract class com.ss.videoarch.liveplayer.VeLivePlayer
```

直播播放器。

## 靜態函式

|傳回值 |名稱 |
|---|---|
|static String |[getVersion](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-getversion) |
|static void |[setLogLevel](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setloglevel) |

## 成員函式

|傳回值 |名稱 |
|---|---|
|abstract void |[setConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setconfig) |
|abstract void |[setObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setobserver) |
|abstract void |[setRenderFillMode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setrenderfillmode) |
|abstract void |[setSurfaceHolder](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurfaceholder) |
|abstract void |[setSurface](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurface) |
|abstract void |[setPlayUrl](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplayurl) |
|abstract void |[setPlayStreamData](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplaystreamdata) |
|abstract void |[play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) |
|abstract void |[stop](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-stop) |
|abstract void |[destroy](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-destroy) |
|abstract boolean |[switchResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-switchresolution) |
|abstract boolean |[isPlaying](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-isplaying) |
|abstract void |[setPlayerVolume](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplayervolume) |
|abstract void |[setMute](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setmute) |
|abstract boolean |[isMute](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-ismute) |
|abstract void |[setUrlHostIP](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-seturlhostip) |
|abstract void |[setProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setproperty) |
|abstract int |[snapshot](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-snapshot) |
|abstract void |[enableVideoFrameObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-enablevideoframeobserver) |
|abstract void |[enableAudioFrameObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-enableaudioframeobserver) |
|abstract void |[setRenderRotation](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setrenderrotation) |
|abstract void |[setRenderMirror](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setrendermirror) |
|abstract void |[setEnableSuperResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setenablesuperresolution) |
|abstract void |[setEnableSharpen](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setenablesharpen) |
|abstract ArrayList |[getStreamList](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-getstreamlist) |

## 說明

### getVersion

```java
public static String com.ss.videoarch.liveplayer.VeLivePlayer.getVersion()
```

取得 Player SDK 的版本號碼。

**傳回值**

Player SDK 的版本號碼。

### setLogLevel

```java
public static void com.ss.videoarch.liveplayer.VeLivePlayer.setLogLevel(VeLivePlayerLogConfig.VeLivePlayerLogLevel logLevel)
```

設定輸出記錄的層級。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|logLevel |VeLivePlayerLogConfig.VeLivePlayerLogLevel |輸出記錄的層級。如需詳細資訊，請參閱 [VeLivePlayerLogLevel](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerLogLevel)。 |

### setConfig

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setConfig(VeLivePlayerConfiguration config)
```

初始化播放器，並設定是否開啟 SEI 訊息、硬體解碼、本機 DNS 預取和其他設定。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|config |VeLivePlayerConfiguration |播放器設定。如需詳細資訊，請參閱 [VeLivePlayerConfiguration](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerConfiguration)。 |

**注意事項**

請在呼叫 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 前，呼叫此方法以初始化播放器。

### setObserver

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setObserver(VeLivePlayerObserver observer)
```

設定播放器觀察器，以監聽直播播放器事件，例如播放錯誤或狀態更新、首個音訊與視訊影格的轉譯，以及解析度切換。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|observer |VeLivePlayerObserver |播放器觀察器。如需詳細資訊，請參閱 [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver)。 |

**注意事項**

請在呼叫 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 前呼叫此方法。

### setRenderFillMode

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setRenderFillMode(VeLivePlayerFillMode fillMode)
```

設定播放器畫面的填滿模式。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|fillMode |VeLivePlayerFillMode |SurfaceView 的填滿模式。預設值為 `VeLivePlayerFillModeAspectFill`。如需詳細資訊，請參閱 [VeLivePlayerFillMode](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerFillMode)。 |

**注意事項**

* 呼叫 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 前，請呼叫此方法以設定播放器的初始填滿模式。

* 您可以在播放期間呼叫此方法，動態調整填滿模式。

### setSurfaceHolder

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setSurfaceHolder(SurfaceHolder surfaceHolder)
```

設定用於視訊轉譯和播放的 `SurfaceHolder` 物件。如果使用 `SurfaceView` 播放，請使用此方法。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|surfaceHolder |SurfaceHolder |`SurfaceHolder` 物件。 |

**注意事項**

如果同時呼叫 setSurfaceHolder 和 [setSurface](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurface) 來設定 `Surface` 物件，播放器會優先使用 `surfaceHolder` 的設定。

### setSurface

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setSurface(Surface surface)
```

設定用於視訊轉譯和播放的 `Surface` 物件。如果使用 `SurfaceView` 或 `TextureView` 播放，請使用此方法。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|surface |Surface |`Surface` 物件。 |

**注意事項**

如果同時呼叫 [setSurfaceHolder](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurfaceholder) 和 `setSurface` 來設定 `Surface` 物件，播放器會優先使用 `surfaceHolder` 的設定。

### setPlayUrl

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setPlayUrl(String url)
```

設定拉流位址。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|url |String |拉流位址。 |

**注意事項**

請在呼叫 play 前呼叫此方法。

### setPlayStreamData

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setPlayStreamData(VeLivePlayerStreamData streamData)
```

設定多個直播流。如果您需要啟用需要多個直播流的功能，例如自適應位元率 (ABR)、手動解析度切換，以及主備流，請呼叫此方法。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|streamData |VeLivePlayerStreamData |多個拉流位址的設定。如需詳細資訊，請參閱 [VeLivePlayerStreamData](https://docs.byteplus.com/en/docs/24/player-android-api-keytype#VeLivePlayerStreamData)。 |

**注意事項**

請在呼叫 play 前呼叫此方法。

### play

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.play()
```

開始或繼續播放。

**注意事項**

呼叫此方法後，播放器完成拉流準備時，以及轉譯第一個影格時，都會觸發 [onPlayerStatusUpdate](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate) 回呼。

### stop

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.stop()
```

停止播放。此方法不會銷毀播放器。

**注意事項**

呼叫此方法後播放停止時，會觸發 [onPlayerStatusUpdate](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate) 回呼。

### destroy

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.destroy()
```

停止播放並銷毀播放器。

### switchResolution

```java
public abstract boolean com.ss.videoarch.liveplayer.VeLivePlayer.switchResolution(VeLivePlayerResolution resolution)
```

變更視訊解析度。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|resolution |VeLivePlayerResolution |視訊解析度。如需詳細資訊，請參閱 VeLivePlayerResolution。 |

**傳回值**

* true：成功；

* false：失敗。

**注意事項**

* 呼叫此方法前，請呼叫 [setPlayStreamData](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplaystreamdata) 以設定多個解析度。

* 呼叫此方法後，播放器切換至新解析度時，會觸發 [onResolutionSwitch](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onresolutionswitch) 回呼。

* 若要避免切換解析度時出現黑畫面或延遲，請將 [enableSmoothSwitchResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerStreamData-enablesmoothswitchresolution) 設為 `true`。

### isPlaying

```java
public abstract boolean com.ss.videoarch.liveplayer.VeLivePlayer.isPlaying()
```

檢查播放器是否正在播放。

**傳回值**

播放器是否正在播放。

* true：播放器正在播放；

* false：播放器未播放。

### setPlayerVolume

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setPlayerVolume(float volume)
```

設定播放器音量。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|volume |float |音量。預設值為 `1.0`。值範圍為 [0.0, 1.0]。 |

### setMute

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setMute(boolean mute)
```

設定是否將播放靜音。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|mute |boolean |是否將播放靜音。預設值為 `false`。<br><br><br>* true：靜音；<br><br>* false：不靜音。 |

### isMute

```java
public abstract boolean com.ss.videoarch.liveplayer.VeLivePlayer.isMute()
```

檢查播放是否已靜音。

**傳回值**

播放是否已靜音。

* true：已靜音；

* false：未靜音。

### setUrlHostIP

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setUrlHostIP(Map<String, List<String>> hostIpMap)
```

設定網域名稱與伺服器 IP 位址的對應。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|hostIpMap |Map<String, List\> |網域名稱與伺服器 IP 位址的對應。`Map` 物件使用網域名稱作為索引鍵，對應的值是與該網域關聯的伺服器 IP 位址清單。值為 `List` 類型。 |

**注意事項**

* 使用 setUrlHostIP 對應網域名稱和 IP 位址時，請在初始設定中將 [enableLiveDNS](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerConfiguration-enablelivedns) 設為 false，以停用 DNS 預解析功能。

* 呼叫 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 開始播放前，請呼叫此方法設定網域名稱和 IP 位址的對應。

### setProperty

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setProperty(
    String key,
    Object value
)
```

設定播放器的進階設定，包括離屏轉譯、最大緩衝時間，以及自適應位元率 (ABR) 演算法。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|key |String |進階設定的參數名稱。 |
|value |Object |進階設定的參數值。 |

### snapshot

```java
public abstract int com.ss.videoarch.liveplayer.VeLivePlayer.snapshot()
```

擷取視訊畫面。

**傳回值**

* 0：允許擷取螢幕截圖。

* [VeLivePlayerErrorRefused](https://docs.byteplus.com/en/docs/24/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorrefused)：不允許擷取螢幕截圖。

**注意事項**

* 此方法僅在播放期間生效。

* 呼叫此方法後擷取螢幕截圖時，會觸發 [onSnapshotComplete](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onsnapshotcomplete) 回呼，其中包含螢幕截圖的 Bitmap 物件。

### enableVideoFrameObserver

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.enableVideoFrameObserver(
    boolean enable,
    VeLivePlayerPixelFormat pixelFormat,
    VeLivePlayerVideoBufferType bufferType
)
```

設定視訊影格觀察器。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|enable |boolean |是否啟用視訊影格回呼。預設值為 `false`。<br><br><br>* true：啟用；<br><br>* false：停用。 |
|pixelFormat |VeLivePlayerPixelFormat |回呼中視訊影格的像素格式。如需詳細資訊，請參閱 [VeLivePlayerPixelFormat](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerPixelFormat)。 |
|bufferType |VeLivePlayerVideoBufferType |回呼中視訊資料的封裝格式。如需詳細資訊，請參閱 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerVideoBufferType)。 |

**注意事項**

* 您可以呼叫此方法，訂閱已解碼的視訊資料以進行外部轉譯。

* 呼叫此方法後，SDK 收到視訊影格時，會觸發 [onRenderVideoFrame](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onrendervideoframe) 回呼。此回呼包含視訊影格的詳細資訊。

* 如果使用外部轉譯，您需要確保視訊與音訊同步。

### enableAudioFrameObserver

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.enableAudioFrameObserver(
    boolean enable,
    boolean enableRendering,
    VeLivePlayerAudioBufferType bufferType
)
```

設定音訊影格觀察器。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|enable |boolean |是否啟用音訊影格回呼。預設值為 `false`。<br><br><br>* true：啟用；<br><br>* false：停用。 |
|enableRendering |boolean |是否啟用播放器轉譯。預設值為 `false`。<br><br><br>* true：啟用；<br><br>* false：停用。 |
|bufferType |VeLivePlayerAudioBufferType |音訊緩衝區類型。如需詳細資訊，請參閱 [VeLivePlayerAudioBufferType](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerAudioBufferType)。 |

**注意事項**

* 如果想使用外部轉譯，您可以呼叫此方法訂閱已解碼的音訊資料。

* 呼叫此方法後，SDK 收到音訊影格時，會觸發 [onRenderAudioFrame](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onrenderaudioframe) 回呼。此回呼包含音訊影格的詳細資訊。

* 如果使用外部轉譯，您需要確保視訊與音訊同步。

### setRenderRotation

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setRenderRotation(VeLivePlayerRotation rotation)
```

設定視訊的順時針旋轉角度。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|rotation |VeLivePlayerRotation |視訊的順時針旋轉角度。預設停用旋轉。如需詳細資訊，請參閱 [VeLivePlayerRotation](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerRotation)。 |

**注意事項**

* 您可以在播放前和播放期間變更旋轉角度。

* 每次呼叫此方法時，播放器都會根據原始視訊旋轉視訊。

* 對視訊同時套用旋轉和鏡像時，播放器會先鏡像視訊，然後再旋轉。

### setRenderMirror

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setRenderMirror(VeLivePlayerMirror mirror)
```

設定鏡像設定。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|mirror |VeLivePlayerMirror |鏡像設定。預設停用鏡像。如需詳細資訊，請參閱 [VeLivePlayerMirror](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerMirror)。 |

**注意事項**

* 您可以在播放前和播放期間變更鏡像設定。

* 每次呼叫此方法時，播放器都會將鏡像設定套用至原始視訊。

* 對視訊同時套用旋轉和鏡像時，播放器會先鏡像視訊，然後再旋轉。

### setEnableSuperResolution

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setEnableSuperResolution(boolean enable)
```

啟用或停用超解析度。使用前，您必須先聯絡 BytePlus [技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) 以啟用此功能。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|enable |boolean |是否啟用超解析度。預設值為 false。<br><br><br>* true：啟用；<br><br>* false：停用。 |

**注意事項**

* 請在收到 [onFirstVideoFrameRender](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onfirstvideoframerender) 回呼後，或在播放期間呼叫此方法。

* 支援在播放期間呼叫此介面，動態啟用和停用超解析度。

* 如果 SDK 因裝置型號、視訊解析度或影格率而無法啟用超解析度，您會收到 [onStreamFailedOpenSuperResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution) 回呼。

### setEnableSharpen

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setEnableSharpen(boolean enable)
```

設定是否啟用視訊銳化。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|enable |boolean |設定是否啟用視訊銳化。預設值為 `false`。<br><br><br>* true：啟用；<br><br>* false：停用。 |

### getStreamList

```java
public abstract ArrayList<VeLivePlayerStreamInfo> com.ss.videoarch.liveplayer.VeLivePlayer.getStreamList()
```

取得串流資訊。

**傳回值**

串流資訊。如需詳細資訊，請參閱 [VeLivePlayerStreamInfo](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype?lang=en#veliveplayerstreaminfo)。

**注意事項**

* 當 [VeLivePlayerStatus](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerStatus)（播放器狀態）為 `VeLivePlayerStatusPrepared` 時，呼叫此方法。

* 此方法目前僅適用於 HLS 格式串流。
