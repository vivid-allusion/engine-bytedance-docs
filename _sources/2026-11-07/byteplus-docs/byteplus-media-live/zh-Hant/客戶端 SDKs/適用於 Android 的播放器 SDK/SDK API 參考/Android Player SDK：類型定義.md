---
title: "Android Player SDK：類型定義"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype-zh-TW"
---

# VeLivePlayerResolution

```java
public static class com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution
```

播放器解析度。

## 成員屬性

|類型 |預設值 |名稱 |
|---|---|---|
|String |"origin" |[VeLivePlayerResolutionOrigin](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution-veliveplayerresolutionorigin) |
|String |"uhd" |[VeLivePlayerResolutionUHD](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution-veliveplayerresolutionuhd) |
|String |"hd" |[VeLivePlayerResolutionHD](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution-veliveplayerresolutionhd) |
|String |"sd" |[VeLivePlayerResolutionSD](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution-veliveplayerresolutionsd) |
|String |"ld" |[VeLivePlayerResolutionLD](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution-veliveplayerresolutionld) |
|String |VeLivePlayerResolutionOrigin |[resolutionStr](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution-resolutionstr) |

## 成員函式

|傳回 |名稱 |
|---|---|
|VeLivePlayerResolution |[VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution-veliveplayerresolution) |

## 說明

### VeLivePlayerResolutionOrigin

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin = "origin"
```

原始。

### VeLivePlayerResolutionUHD

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionUHD = "uhd"
```

超高畫質（UHD）。

### VeLivePlayerResolutionHD

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionHD = "hd"
```

高畫質（HD）。

### VeLivePlayerResolutionSD

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionSD = "sd"
```

標準畫質（SD）。

### VeLivePlayerResolutionLD

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionLD = "ld"
```

低畫質（LD）。

### resolutionStr

```java
public String com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution.resolutionStr = VeLivePlayerResolutionOrigin
```

建立物件時傳入的初始解析度等級。

## 說明

### VeLivePlayerResolution

```java
public com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolution(String res)
```

建構函式方法。

**輸入參數**

|名稱 |類型 |說明 |
|---|---|---|
|res |String |解析度等級。 |

# VeLivePlayerConfiguration

```java
public final class com.ss.videoarch.liveplayer.VeLivePlayerConfiguration
```

播放器初始化的組態。

## 成員屬性

|類型 |預設值 |名稱 |
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

## 說明

### enableSei

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.enableSei = false
```

是否啟用字串 SEI 訊息解析。預設值為 `false`。

* true：啟用；

* false：停用。

### enableBinarySei

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.enableBinarySei = false
```

是否啟用二進位 SEI 訊息解析。預設值為 `false`。

* true：啟用；

* false：停用。

**注意事項**

啟用二進位 SEI 後，將不再傳送字串 SEI 的回呼。

### enableHardwareDecode

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.enableHardwareDecode = true
```

是否開啟硬體解碼。預設值為 `true`。啟用硬體解碼後，如果播放器無法啟動硬體解碼，或硬體解碼失敗，播放器會自動切換為軟體解碼。

* true：啟用；

* false：停用。

### networkTimeoutMs

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.networkTimeoutMs = 5_000
```

網路逾時時間，單位為毫秒。預設值為 `5000`。播放器傳送網路請求後，如果逾時時間後仍未收到伺服器回應，則視為網路請求失敗。

### retryIntervalTimeMs

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.retryIntervalTimeMs = 5_000
```

重試間隔，單位為 ms。預設值為 `5000`。若要為每路串流設定單獨的重試間隔，可設定 [retryIntervalTimeMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStream-retryintervaltimems)。

### retryMaxCount

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.retryMaxCount = 5
```

網路連線錯誤時播放器的最大重試次數。預設值為 `5`。如果值為 `0`，播放器不會自動重試。若要為每路串流設定單獨的最大重試次數，可設定 [retryMaxCount](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStream-retrymaxcount)。

### enableLiveDNS

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.enableLiveDNS = false
```

是否啟用本機 DNS 預取。預設值為 `false`。啟用本機 DNS 預取可縮短開始播放所需時間。如果本機 DNS 預取發生異常，播放器可能無法正常運作。

* true：啟用；

* false：停用。

### enableStatisticsCallback

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.enableStatisticsCallback = false
```

是否啟用播放資訊的定期回呼。預設值為 `false`。如需回呼統計資料的更多資訊，請參閱 [VeLivePlayerStatistics](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics)。如果 `enableStatisticsCallback` 為 `true` 且 [statisticsCallbackInterval](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-statisticscallbackinterval) 大於 `0`，播放器會在指定時間間隔後定期回報播放器狀態資訊。

* true：啟用；

* false：停用。

### statisticsCallbackInterval

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.statisticsCallbackInterval = 5
```

提供播放資訊的定期回呼時間間隔，單位為秒。預設值為 `5`。如果 [enableStatisticsCallback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-enablestatisticscallback) 為 `true` 且 `statisticsCallbackInterval` 大於 `0`，播放器會在指定時間間隔後定期回報播放器狀態資訊。

### stallRetryTimeout

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.stallRetryTimeout = 10_000
```

因卡頓而停止重試的逾時閾值。當卡頓持續時間超過此閾值時，播放器會停止重試。單位為 ms。預設值為 `10000`，等於 10 秒。

# VeLivePlayerFormat

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerFormat
```

直播串流的格式。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerFormatFLV |0 |FLV。 |
|VeLivePlayerFormatHLS |1 |HLS。 |
|VeLivePlayerFormatRTM |2 |即時媒體（RTM）。 |
|VeLivePlayerFormatCMAF |3 |CMAF 格式 |

# VeLivePlayerProtocol

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerProtocol
```

傳輸協定。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerProtocolTCP |0 |TCP。 |
|VeLivePlayerProtocolQUIC |1 |QUIC。 |
|VeLivePlayerProtocolTLS |2 |TLS。 |
|VeLivePlayerProtocolHTTP2 |3 |HTTP/2。 |
|VeLivePlayerProtocolDefault |4 |預設值。播放器會從拉流位址自動識別網路協定。目前僅支援自動識別 TCP 和 TLS 協定。若使用 QUIC 或 HTTP/2 協定，請使用對應值。 |

# VeLivePlayerMirror

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerMirror
```

鏡像選項。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerMirrorNone |0 |不鏡像。 |
|VeLivePlayerMirrorHorizontal |1 |水平鏡像。 |
|VeLivePlayerMirrorVertical |2 |垂直鏡像。 |

# VeLivePlayerVideoBufferType

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerVideoBufferType
```

視訊資料的封裝格式。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerVideoBufferTypeUnknown |0 |未知格式。 |
|VeLivePlayerVideoBufferTypeByteBuffer |1 |ByteBuffer。 |
|VeLivePlayerVideoBufferTypeByteArray |2 |ByteArray。 |
|VeLivePlayerVideoBufferTypeTexture |3 |Texture。 |

# VeLivePlayerStatus

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerStatus
```

直播播放器的狀態。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerStatusStopped |0 |播放已停止。 |
|VeLivePlayerStatusPaused |1 |播放已暫停。 |
|VeLivePlayerStatusPrepared |2 |播放器完成準備，正在等待轉譯視訊。 |
|VeLivePlayerStatusPlaying |3 |播放目前進行中，表示已轉譯首幀，且播放器未發生錯誤。 |
|VeLivePlayerStatusError |4 |播放器發生錯誤。 |
|VeLivePlayerStatusStalled |5 |播放器已卡頓。 |

# VeLivePlayerLogConfig

```java
public class com.ss.videoarch.liveplayer.log.VeLivePlayerLogConfig
```

日誌設定。

## 成員屬性

|類型 |預設值 |名稱 |
|---|---|---|
|VeLivePlayerLogLevel |VeLivePlayerLogLevel.VeLivePlayerLogLevelVerbose |[logLevel](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerLogConfig-loglevel) |

## 說明

### logLevel

```java
public VeLivePlayerLogLevel com.ss.videoarch.liveplayer.log.VeLivePlayerLogConfig.logLevel = VeLivePlayerLogLevel.VeLivePlayerLogLevelVerbose
```

輸出日誌等級。預設值為 `VeLivePlayerLogLevelDebug`。如需詳細資訊，請參閱 [VeLivePlayerLogLevel](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerLogLevel)。

# VeLivePlayerStreamData

```java
public class com.ss.videoarch.liveplayer.VeLivePlayerStreamData
```

拉流位址的組態。

## 成員屬性

|類型 |預設值 |名稱 |
|---|---|---|
|boolean |false |[enableABR](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-enableabr) |
|boolean |false |[enableMainBackupSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-enablemainbackupswitch) |
|VeLivePlayerResolution |new VeLivePlayerResolution(VeLivePlayerResolution.VeLivePlayerResolutionOrigin) |[defaultResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-defaultresolution) |
|VeLivePlayerFormat |VeLivePlayerFormat.VeLivePlayerFormatFLV |[defaultFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-defaultformat) |
|VeLivePlayerProtocol |VeLivePlayerProtocol.VeLivePlayerProtocolTCP |[defaultProtocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-defaultprotocol) |
|List |null |[mainStreamList](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-mainstreamlist) |
|List |null |[backupStreamList](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-backupstreamlist) |
|boolean |false |[enableSmoothSwitchResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-enablesmoothswitchresolution) |

## 說明

### enableABR

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerStreamData.enableABR = false
```

是否啟用自適應位元率（ABR）。預設值為 `false`。

* true：啟用；

* false：停用。

### enableMainBackupSwitch

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerStreamData.enableMainBackupSwitch = false
```

是否啟用主備串流切換。預設值為 `false`。

* true：啟用；

* false：停用。

### defaultResolution

```java
public VeLivePlayerResolution com.ss.videoarch.liveplayer.VeLivePlayerStreamData.defaultResolution = new VeLivePlayerResolution(VeLivePlayerResolution.VeLivePlayerResolutionOrigin)
```

預設解析度。預設值為 `VeLivePlayerResolutionOrigin`，表示原始解析度。詳情請參閱 [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution)。

### defaultFormat

```java
public VeLivePlayerFormat com.ss.videoarch.liveplayer.VeLivePlayerStreamData.defaultFormat = VeLivePlayerFormat.VeLivePlayerFormatFLV
```

預設視訊格式。預設值為 `VeLivePlayerFormatFLV`。詳情請參閱 [VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerFormat)。

### defaultProtocol

```java
public VeLivePlayerProtocol com.ss.videoarch.liveplayer.VeLivePlayerStreamData.defaultProtocol = VeLivePlayerProtocol.VeLivePlayerProtocolTCP
```

預設傳輸協定。預設值為 `VeLivePlayerProtocolTCP`。詳情請參閱 [VeLivePlayerProtocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProtocol)。

### mainStreamList

```java
public List<VeLivePlayerStream> com.ss.videoarch.liveplayer.VeLivePlayerStreamData.mainStreamList = null
```

主串流位址清單。詳情請參閱 [VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-VeLivePlayerStream)。

### backupStreamList

```java
public List<VeLivePlayerStream> com.ss.videoarch.liveplayer.VeLivePlayerStreamData.backupStreamList = null
```

備用串流位址清單。詳情請參閱 [VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-VeLivePlayerStream)。

### enableSmoothSwitchResolution

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerStreamData.enableSmoothSwitchResolution = false
```

是否啟用平滑解析度切換。預設值為 `false`。若啟用，當您呼叫 [switchResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-switchresolution) 方法手動切換解析度時，SDK 會嘗試執行平滑轉換，避免黑屏或延遲。有效值：

* `true`：啟用。

* `false`：停用。

# VeLivePlayerResolutionSwitchReason

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolutionSwitchReason
```

視訊解析度變更的原因。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLiveplayerResolutionSwitchByAuto |0 |解析度透過自適應位元率（ABR）功能自動切換。 |
|VeLiveplayerResolutionSwitchByManual |1 |呼叫 [switchResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-switchresolution) 後變更解析度。 |

# VeLivePlayerSupportResolutionSwitchError

```java
public static class com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError
```

畫質等級切換的錯誤。

## 成員屬性

|類型 |預設值 |名稱 |
|---|---|---|
|int |0 |[VeLivePlayerNoError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerSupportResolutionSwitchError-veliveplayernoerror) |
|int |\-1 |[VeLivePlayerErrorInvalidRes](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerSupportResolutionSwitchError-veliveplayererrorinvalidres) |
|int |\-2 |[VeLivePlayerErrorSameRes](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerSupportResolutionSwitchError-veliveplayererrorsameres) |
|int |\-3 |[VeLivePlayerErrorStatusInvalid](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerSupportResolutionSwitchError-veliveplayererrorstatusinvalid) |
|int |\-4 |[VeLivePlayerErrorResNotFound](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerSupportResolutionSwitchError-veliveplayererrorresnotfound) |
|int |\-5 |[VeLivePlayerErrorFormatNotSupport](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerSupportResolutionSwitchError-veliveplayererrorformatnotsupport) |
|int |\-6 |[VeLivePlayerErrorConfigNotSupport](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerSupportResolutionSwitchError-veliveplayererrorconfignotsupport) |

## 說明

### VeLivePlayerNoError

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError.VeLivePlayerNoError = 0
```

沒有錯誤。

### VeLivePlayerErrorInvalidRes

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError.VeLivePlayerErrorInvalidRes = -1
```

無效的畫質等級。

### VeLivePlayerErrorSameRes

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError.VeLivePlayerErrorSameRes = -2
```

與目前畫質等級相同。

### VeLivePlayerErrorStatusInvalid

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError.VeLivePlayerErrorStatusInvalid = -3
```

播放器狀態不是 `prepare`。

### VeLivePlayerErrorResNotFound

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError.VeLivePlayerErrorResNotFound = -4
```

找不到對應的畫質等級。

### VeLivePlayerErrorFormatNotSupport

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError.VeLivePlayerErrorFormatNotSupport = -5
```

目前播放格式不支援此畫質等級。

### VeLivePlayerErrorConfigNotSupport

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError.VeLivePlayerErrorConfigNotSupport = -6
```

目前播放組態不支援此畫質等級。

# VeLivePlayerStream

```java
public static class com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream
```

拉流位址的資訊。

## 成員屬性

|類型 |預設值 |名稱 |
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

## 說明

### url

```java
public String com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.url = null
```

拉流位址。

### resolution

```java
public VeLivePlayerResolution com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.resolution = new VeLivePlayerResolution(VeLivePlayerResolution.VeLivePlayerResolutionOrigin)
```

播放解析度。詳情請參閱 [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution)。

### bitrate

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.bitrate
```

播放位元率，單位為 Kbps。

### format

```java
public VeLivePlayerFormat com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.format = VeLivePlayerFormat.VeLivePlayerFormatFLV
```

直播串流的格式。詳情請參閱 [VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerFormat)。

### streamType

```java
public VeLivePlayerStreamType com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain
```

串流是主串流或備用串流。詳情請參閱 [VeLivePlayerStreamType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamType)。

### priority

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.priority = 0
```

串流的優先順序。值必須為 `0`（預設）或正整數。值越大表示優先順序越高。

### retryMaxCount

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.retryMaxCount = -1
```

串流的最大重試嘗試次數，表示播放嘗試總次數（包括初始嘗試）。例如，值為 `3` 表示播放器在初始失敗後最多重試 2 次。有效值：

* `-1`（預設）：使用 `VeLivePlayerConfiguration` 中的 [retryMaxCount](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-retrymaxcount) 值。

* `0`：不嘗試播放此串流。

* `> 0`：特定的總嘗試次數。

### retryIntervalTimeMs

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.retryIntervalTimeMs = -1
```

重試間隔，單位為 ms。預設值為 `-1`。如果值為 `-1`，播放器會使用 `VeLivePlayerConfiguration` 中的 [retryIntervalTimeMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-retryintervaltimems) 值。

### protocol

```java
public VeLivePlayerProtocol com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.protocol = VeLivePlayerProtocol.VeLivePlayerProtocolDefault
```

傳輸協定。詳情請參閱 [VeLivePlayerProtocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProtocol)。

# VeLivePlayerFillMode

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerFillMode
```

播放器畫面的填充模式。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerFillModeAspectFit |0 |顯示完整視訊。視訊會等比例縮放，直到視訊的其中一個維度到達畫面邊界。畫面上的剩餘空間會以黑色填滿。 |
|VeLivePlayerFillModeFullFill |1 |拉伸視訊以填滿畫面。視訊的寬高比可能會變更。 |
|VeLivePlayerFillModeAspectFill |2 |等比例縮放視訊，直到完全填滿畫面。部分視訊可能會被裁切。 |

# VeLivePlayerPixelFormat

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerPixelFormat
```

視訊影格的像素格式。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerPixelFormatUnknown |0 |未知格式。 |
|VeLivePlayerPixelFormatRGBA32 |1 |RGBA8888。 |
|VeLivePlayerPixelFormatTexture |2 |Texture。 |
|VeLivePlayerPixelFormatI420 |3 |YUV420P 格式。 |

# VeLivePlayerStatistics

```java
public class com.ss.videoarch.liveplayer.VeLivePlayerStatistics
```

播放統計資料。

## 成員屬性

|類型 |預設值 |名稱 |
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

## 說明

### url

```java
public String com.ss.videoarch.liveplayer.VeLivePlayerStatistics.url
```

目前拉流位址。

### isHardwareDecode

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerStatistics.isHardwareDecode
```

是否使用硬體解碼。

* true：使用硬體解碼；

* false：未使用硬體解碼。

### videoCodec

```java
public String com.ss.videoarch.liveplayer.VeLivePlayerStatistics.videoCodec
```

視訊的編碼格式。

### stallTimeMs

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.stallTimeMs
```

自播放開始以來發生卡頓的累計持續時間，單位為毫秒。

### bandwidthEstimation

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.bandwidthEstimation
```

頻寬估計，單位為 kbps。

### delayMs

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.delayMs
```

目前播放延遲，單位為毫秒。

### delayS2sMs

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.delayS2sMs = -1
```

伺服器到伺服器延遲，單位為毫秒。表示串流從 MediaLive 推流側邊緣節點傳輸到 MediaLive 拉流側邊緣節點所需時間。當 SEI 訊息不包含串流到達推流側邊緣節點和拉流側邊緣節點時的伺服器時間戳記時，值為 `-1`。

### delayE2eMs

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.delayE2eMs = -1
```

端到端延遲，單位為毫秒。表示從 Broadcast SDK 將時間戳記寫入 SEI 訊息，到 Player SDK 在本機解析 SEI 訊息所需時間。精確計算取決於基於 NTP 的時鐘同步。當 SEI 訊息不包含 Broadcast SDK 寫入的時間戳記時，值為 `-1`。

### delayS2eMs

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.delayS2eMs = -1
```

伺服器到終端延遲，單位為毫秒。表示從串流到達 MediaLive 推流側邊緣節點，到 Player SDK 在本機解析 SEI 訊息所需時間。精確計算取決於基於 NTP 的時鐘同步。當 SEI 訊息不包含串流到達 MediaLive 推流側邊緣節點時的伺服器時間戳記時，值為 `-1`。

### width

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerStatistics.width
```

視訊寬度，單位為像素。

### height

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerStatistics.height
```

視訊高度，單位為像素。

### fps

```java
public float com.ss.videoarch.liveplayer.VeLivePlayerStatistics.fps
```

視訊影格率，單位為 fps。

### bitrate

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.bitrate
```

下行位元率，單位為 Kbps。

### videoBufferMs

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.videoBufferMs
```

視訊緩衝，單位為毫秒。

### audioBufferMs

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.audioBufferMs
```

音訊緩衝，單位為毫秒。

### format

```java
public VeLivePlayerFormat com.ss.videoarch.liveplayer.VeLivePlayerStatistics.format
```

視訊格式。如需更多資訊，請參閱 [VeLivePlayerFormat](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#veliveplayerformat)。

### protocol

```java
public VeLivePlayerProtocol com.ss.videoarch.liveplayer.VeLivePlayerStatistics.protocol
```

直播串流的傳輸協定。如需更多資訊，請參閱 [VeLivePlayerProtocol](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#veliveplayerprotocol)。

# VeLivePlayerVideoFrame

```java
public class com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame
```

視訊影格。

## 成員屬性

|類型 |預設值 |名稱 |
|---|---|---|
|VeLivePlayerVideoBufferType |`-` |[bufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-buffertype) |
|VeLivePlayerPixelFormat |`-` |[pixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-pixelformat) |
|int |`-` |[width](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-width) |
|int |`-` |[height](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-height) |
|long |`-` |[pts](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-pts) |
|VeLivePlayerVideoTexture |null |[texture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-texture) |
|ByteBuffer |null |[buffer](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-buffer) |
|byte[] |null |[data](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-data) |

## 說明

### bufferType

```java
public VeLivePlayerVideoBufferType com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.bufferType
```

封裝格式。詳情請參閱 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoBufferType)。

### pixelFormat

```java
public VeLivePlayerPixelFormat com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.pixelFormat
```

像素格式。詳情請參閱 [VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerPixelFormat)。

### width

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.width
```

視訊寬度，單位為像素。

### height

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.height
```

視訊高度，單位為像素。

### pts

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.pts
```

表示視訊影格轉譯時間的時間戳記，單位為毫秒。

### texture

```java
public VeLivePlayerVideoTexture com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.texture = null
```

用於 OpenGL 轉譯的紋理資料。如果您將 [VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerPixelFormat) 設為 `VeLivePlayerPixelFormatTexture`，並將 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoBufferType) 設為 `VeLivePlayerVideoBufferTypeTexture`，SDK 會傳回此視訊資料類型。詳情請參閱 [VeLivePlayerVideoTexture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoTexture)。

### buffer

```java
public ByteBuffer com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.buffer = null
```

ByteBuffer 格式的視訊資料。如果您將 [VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerPixelFormat) 設為 `VeLivePlayerPixelFormatRGBA32`，並將 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoBufferType) 設為 `VeLivePlayerVideoBufferTypeByteBuffer`，SDK 會傳回此視訊資料類型。

### data

```java
public byte [] com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.data = null
```

ByteArray 格式的視訊資料。如果您將 [VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerPixelFormat) 設為 `VeLivePlayerPixelFormatRGBA32`，並將 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoBufferType) 設為 `VeLivePlayerVideoBufferTypeByteArray`，SDK 會傳回此視訊資料類型。

# VeLivePlayerVideoTexture

```java
public class com.ss.videoarch.liveplayer.VeLivePlayerVideoTexture
```

視訊紋理。

## 成員屬性

|類型 |預設值 |名稱 |
|---|---|---|
|int |`-` |[texId](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoTexture-texid) |
|EGLContext |`-` |[eglContext](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoTexture-eglcontext) |

## 說明

### texId

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerVideoTexture.texId
```

視訊紋理 ID。

### eglContext

```java
public EGLContext com.ss.videoarch.liveplayer.VeLivePlayerVideoTexture.eglContext
```

自訂轉譯的 OpenGL ES 內容。將 EGLContext 繫結至 GLSurfaceView 或 TextureView 後，您可以在繫結的 View 上執行自訂 OpenGL ES 轉譯。

# VeLivePlayerStreamType

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerStreamType
```

直播串流的類型。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerStreamTypeMain |0 |主串流。 |
|VeLivePlayerStreamTypeBackup |1 |備用串流。 |

# VeLivePlayerProperty

```java
public class com.ss.videoarch.liveplayer.VeLivePlayerProperty
```

進階組態。

## 成員屬性

|類型 |預設值 |名稱 |
|---|---|---|
|String |"VeLivePlayerKeySetParamsLowLatencyFLV" |[VeLivePlayerKeySetParamsLowLatencyFLV](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProperty-veliveplayerkeysetparamslowlatencyflv) |
|String |"VeLivePlayerKeySetParamsHttpHeaders" |[VeLivePlayerKeySetParamsHttpHeaders](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProperty-veliveplayerkeysetparamshttpheaders) |
|String |`"VeLivePlayerKeySetParamsRemoveQueryParams"` |[VeLivePlayerKeySetParamsRemoveQueryParams](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProperty-veliveplayerkeysetparamsremovequeryparams) |

## 說明

### VeLivePlayerKeySetParamsLowLatencyFLV

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerProperty.VeLivePlayerKeySetParamsLowLatencyFLV = "VeLivePlayerKeySetParamsLowLatencyFLV"
```

設定 FLV 低延遲設定（2–3 秒延遲）。如需詳細用法，請參閱[播放低延遲 FLV 串流](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-2#playing-low-latency-flv-streams)。

### VeLivePlayerKeySetParamsHttpHeaders

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerProperty.VeLivePlayerKeySetParamsHttpHeaders = "VeLivePlayerKeySetParamsHttpHeaders"
```

設定播放器 HTTP 請求的自訂 HTTP 標頭。這通常用於傳遞其他資訊，例如驗證 Token、Cookie 或業務追蹤識別碼。如需詳細用法，請參閱[自訂 HTTP 請求標頭](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-2#customizing-http-request-headers)。

### VeLivePlayerKeySetParamsRemoveQueryParams

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerProperty.VeLivePlayerKeySetParamsRemoveQueryParams = "VeLivePlayerKeySetParamsRemoveQueryParams"
```

設定是否移除 SDK 自動附加至拉流位址的查詢參數。預設值為 `false`。若啟用，拉流請求會移除 SDK 自動附加的查詢參數，並保留原始拉流位址中已存在的查詢參數。如需詳細用法，請參閱[移除 SDK 自動附加的查詢參數](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-2?lang=en#removing-query-parameters-automatically-appended-by-the-sdk)。

* `true`：移除 SDK 自動附加的查詢參數。

* `false`：保留 SDK 自動附加的查詢參數。

# VeLivePlayerLogLevel

```java
public enum com.ss.videoarch.liveplayer.log.VeLivePlayerLogConfig.VeLivePlayerLogLevel
```

播放器的輸出日誌等級。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerLogLevelVerbose |0 |輸出 VERBOSE、DEBUG、INFO、WARNING 和 ERROR 等級的日誌。 |
|VeLivePlayerLogLevelDebug |1 |輸出 DEBUG、INFO、WARNING 和 ERROR 等級的日誌。 |
|VeLivePlayerLogLevelInfo |2 |輸出 INFO、WARNING 和 ERROR 等級的日誌。 |
|VeLivePlayerLogLevelWarn |3 |輸出 WARNING 和 ERROR 等級的日誌。 |
|VeLivePlayerLogLevelError |4 |輸出 ERROR 等級的日誌。 |
|VeLivePlayerLogLevelNone |5 |停用日誌列印。 |

# VeLivePlayerAudioFrame

```java
public class com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame
```

音訊影格。

## 成員屬性

|類型 |預設值 |名稱 |
|---|---|---|
|VeLivePlayerAudioBufferType |`-` |[bufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-buffertype) |
|int |`-` |[sampleRate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-samplerate) |
|int |`-` |[channels](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-channels) |
|int |`-` |[bitDepth](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-bitdepth) |
|long |`-` |[pts](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-pts) |
|byte[] |null |[bufferArray](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-bufferarray) |
|ByteBuffer[] |null |[buffer](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-buffer) |
|int |`-` |[samples](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-samples) |

## 說明

### bufferType

```java
public VeLivePlayerAudioBufferType com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.bufferType
```

音訊資料的封裝格式。詳情請參閱 [VeLivePlayerAudioBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioBufferType)。

### sampleRate

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.sampleRate
```

音訊取樣率，單位為 Hz。

### channels

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.channels
```

音訊聲道數。

* 1：單聲道；

* 2：立體聲。

### bitDepth

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.bitDepth
```

音訊位元深度。

### pts

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.pts
```

表示音訊轉譯時間的時間戳記，單位為毫秒。

### bufferArray

```java
public byte [] com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.bufferArray = null
```

PCM 音訊資料。byte[] 類型。

### buffer

```java
public ByteBuffer [] com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.buffer = null
```

PCM 音訊資料。ByteBuffer[] 類型。

### samples

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.samples
```

音訊取樣數。

# VeLivePlayerAudioBufferType

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerAudioBufferType
```

音訊的封裝格式。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerAudioBufferTypeUnknown |0 |未知格式。 |
|VeLivePlayerAudioBufferTypeByteArray |1 |ByteArray。 |

# VeLivePlayerRotation

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerRotation
```

視訊順時針旋轉角度。

## 列舉值

|類型 |值 |說明 |
|---|---|---|
|VeLivePlayerRotation0 |0 |不旋轉。 |
|VeLivePlayerRotation90 |1 |順時針旋轉 90 度。 |
|VeLivePlayerRotation180 |2 |順時針旋轉 180 度。 |
|VeLivePlayerRotation270 |3 |順時針旋轉 270 度。 |

# VeLivePlayerStreamInfo

```java
public class com.ss.videoarch.liveplayer.hls.VeLivePlayerStreamInfo
```

HLS 串流資訊。

## 成員變數

|名稱 |類型 |預設 |
|---|---|---|
|[width](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamInfo-width) |int |\- |
|[height](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamInfo-height) |int |\- |
|[bandwidth](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamInfo-bandwidth) |int |\- |
|[url](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamInfo-url) |String |\- |

## 成員函式

|名稱 |傳回 |
|---|---|
|[toString](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamInfo-tostring) |String |

## 變數說明

### width

```java
public int com.ss.videoarch.liveplayer.hls.VeLivePlayerStreamInfo.width
```

視訊寬度，單位為像素。

### height

```java
public int com.ss.videoarch.liveplayer.hls.VeLivePlayerStreamInfo.height
```

視訊高度，單位為像素。

### bandwidth

```java
public int com.ss.videoarch.liveplayer.hls.VeLivePlayerStreamInfo.bandwidth
```

串流頻寬，單位為位元/秒（bps）。

### url

```java
public String com.ss.videoarch.liveplayer.hls.VeLivePlayerStreamInfo.url
```

HLS 串流的播放 URL。

## 函式說明

### toString

```java
public String com.ss.videoarch.liveplayer.hls.VeLivePlayerStreamInfo.toString()
```

將 HLS 串流資訊轉換為字串。

**傳回值**

包含 HLS 串流視訊寬度、視訊高度、頻寬和播放 URL 的字串。
