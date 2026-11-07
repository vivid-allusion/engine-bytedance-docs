---
title: "Player SDK for Android: Type definitions"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype"
---

 &nbsp;

<span id="veliveplayerresolution"></span>
# VeLivePlayerResolution

```java
public static class com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution
```


The player resolution.

 &nbsp;

<span id="member-property"></span>
## Member Property

&nbsp;


|Type |Default Value |Name |
|---|---|---|
|String |"origin" |[VeLivePlayerResolutionOrigin](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution-veliveplayerresolutionorigin) |
|String |"uhd" |[VeLivePlayerResolutionUHD](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution-veliveplayerresolutionuhd) |
|String |"hd" |[VeLivePlayerResolutionHD](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution-veliveplayerresolutionhd) |
|String |"sd" |[VeLivePlayerResolutionSD](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution-veliveplayerresolutionsd) |
|String |"ld" |[VeLivePlayerResolutionLD](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution-veliveplayerresolutionld) |
|String |VeLivePlayerResolutionOrigin |[resolutionStr](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution-resolutionstr) |


 &nbsp;

<span id="member-functions"></span>
## Member Functions

&nbsp;


|Return |Name |
|---|---|
|VeLivePlayerResolution |[VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution-veliveplayerresolution) |


 &nbsp;

<span id="instructions"></span>
## Instructions

 &nbsp;

<span id="veliveplayerresolutionorigin"></span>
### VeLivePlayerResolutionOrigin

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin = "origin"
```


Original.

 &nbsp;

<span id="veliveplayerresolutionuhd"></span>
### VeLivePlayerResolutionUHD

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionUHD = "uhd"
```


Ultra high definition (UHD).

 &nbsp;

<span id="veliveplayerresolutionhd"></span>
### VeLivePlayerResolutionHD

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionHD = "hd"
```


High definition (HD).

 &nbsp;

<span id="veliveplayerresolutionsd"></span>
### VeLivePlayerResolutionSD

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionSD = "sd"
```


Standard definition (SD).

 &nbsp;

<span id="veliveplayerresolutionld"></span>
### VeLivePlayerResolutionLD

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionLD = "ld"
```


Low definition (LD).

 &nbsp;

<span id="resolutionstr"></span>
### resolutionStr

```java
public String com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution.resolutionStr = VeLivePlayerResolutionOrigin
```


The initial resolution level passed in when creating the object.

 &nbsp;

<span id="instructions-1"></span>
## Instructions

 &nbsp;

<span id="veliveplayerresolution-1"></span>
### VeLivePlayerResolution

```java
public com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolution(String res)
```


Constructor method.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|res |String |resolution level. |


 &nbsp;

<span id="veliveplayerconfiguration"></span>
# VeLivePlayerConfiguration

```java
public final class com.ss.videoarch.liveplayer.VeLivePlayerConfiguration
```


The configurations for player initialization.

 &nbsp;

<span id="member-property-1"></span>
## Member Property

&nbsp;


|Type |Default Value |Name |
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


 &nbsp;

<span id="instructions-2"></span>
## Instructions

 &nbsp;

<span id="enablesei"></span>
### enableSei

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.enableSei = false
```


Whether to enable the parsing of string SEI messages. The default value is `false`.


* true: Enable;

* false: Disable.

    &nbsp;


 &nbsp;

<span id="enablebinarysei"></span>
### enableBinarySei

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.enableBinarySei = false
```


Whether to enable the parsing of binary SEI messages. The default value is `false`.


* true: Enable;

* false: Disable.


**Notes**

After binary SEI is enabled, callbacks for string SEI will no longer be sent.

 &nbsp;

<span id="enablehardwaredecode"></span>
### enableHardwareDecode

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.enableHardwareDecode = true
```


Whether to turn on hardware decoding. The default value is `true`. When hardware decoding is enabled, if the player fails to start hardware decoding or if hardware decoding fails, the player automatically switches to software decoding.


* true: Enable;

* false: Disable.

    &nbsp;


 &nbsp;

<span id="networktimeoutms"></span>
### networkTimeoutMs

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.networkTimeoutMs = 5_000
```


Network timeout duration, in milliseconds. The default value is `5000`. Once the player sends a network request, if the player does not receive a response from the server after the timeout duration, the network request is considered failed.

 &nbsp;

<span id="retryintervaltimems"></span>
### retryIntervalTimeMs

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.retryIntervalTimeMs = 5_000
```


The retry interval, in ms. The default value is `5000`. To set a separate retry interval for each stream, you can set [retryIntervalTimeMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStream-retryintervaltimems).

 &nbsp;

<span id="retrymaxcount"></span>
### retryMaxCount

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.retryMaxCount = 5
```


The maximum number of retries by the player in case of network connection errors. The default value is `5`. If the value is `0`, the player will not automatically retry. To set a separate maximum number of retries for each stream, you can set [retryMaxCount](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStream-retrymaxcount).

 &nbsp;

<span id="enablelivedns"></span>
### enableLiveDNS

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.enableLiveDNS = false
```


Whether to enable local DNS prefetch. The default value is `false`. Enabling local DNS prefetch can reduce the time required to start playback. If an abnormality occurs with local DNS prefetch, the player may not function properly.


* true: Enable;

* false: Disable.

    &nbsp;


 &nbsp;

<span id="enablestatisticscallback"></span>
### enableStatisticsCallback

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.enableStatisticsCallback = false
```


Whether to enable periodic callbacks for playback information. The default value is `false`. Refer to [VeLivePlayerStatistics](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics) for more information on callback statistics. If `enableStatisticsCallback` is `true` and [statisticsCallbackInterval](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-statisticscallbackinterval) is greater than `0`, the player will periodically report the player status information after the specified time interval.


* true: Enable;

* false: Disable.

    &nbsp;


 &nbsp;

<span id="statisticscallbackinterval"></span>
### statisticsCallbackInterval

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.statisticsCallbackInterval = 5
```


The time interval for periodic callbacks that provide playback information, in seconds. The default value is `5`. If [enableStatisticsCallback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-enablestatisticscallback) is `true` and `statisticsCallbackInterval` is greater than `0`, the player will periodically report the player status information after the specified time interval.

 &nbsp;

<span id="stallretrytimeout"></span>
### stallRetryTimeout

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerConfiguration.stallRetryTimeout = 10_000
```


The timeout threshold for stopping retries due to stalling. When the stalling duration exceeds this threshold, the player will stop retrying. The unit is ms. The default value is `10000`, which equals 10 seconds.

 &nbsp;

<span id="veliveplayerformat"></span>
# VeLivePlayerFormat

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerFormat
```


The format of the live stream.

 &nbsp;

<span id="enumerated-value"></span>
## Enumerated Value

&nbsp;


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerFormatFLV |0 |FLV. |
|VeLivePlayerFormatHLS |1 |HLS. |
|VeLivePlayerFormatRTM |2 |Real Time Media (RTM). |
|VeLivePlayerFormatCMAF |3 |CMAF format |


 &nbsp;

<span id="veliveplayerprotocol"></span>
# VeLivePlayerProtocol

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerProtocol
```


The transmission protocol.

 &nbsp;

<span id="enumerated-value-1"></span>
## Enumerated Value

&nbsp;


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerProtocolTCP |0 |TCP. |
|VeLivePlayerProtocolQUIC |1 |QUIC. |
|VeLivePlayerProtocolTLS |2 |TLS. |
|VeLivePlayerProtocolHTTP2 |3 |HTTP/2. |
|VeLivePlayerProtocolDefault |4 |The default value. The player will automatically identify the network protocol from the pull stream address. Currently, only TCP and TLS protocols are supported for automatic identification. For QUIC or HTTP/2 protocols, use the corresponding value. |


 &nbsp;

<span id="veliveplayermirror"></span>
# VeLivePlayerMirror

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerMirror
```


The mirroring option.

 &nbsp;

<span id="enumerated-value-2"></span>
## Enumerated Value

&nbsp;


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerMirrorNone |0 |No mirroring. |
|VeLivePlayerMirrorHorizontal |1 |Horizontal mirroring. |
|VeLivePlayerMirrorVertical |2 |Vertical mirroring. |


 &nbsp;

<span id="veliveplayervideobuffertype"></span>
# VeLivePlayerVideoBufferType

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerVideoBufferType
```


The encapsulation format of the video data.

 &nbsp;

<span id="enumerated-value-3"></span>
## Enumerated Value

&nbsp;


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerVideoBufferTypeUnknown |0 |Unknown format. |
|VeLivePlayerVideoBufferTypeByteBuffer |1 |ByteBuffer. |
|VeLivePlayerVideoBufferTypeByteArray |2 |ByteArray. |
|VeLivePlayerVideoBufferTypeTexture |3 |Texture. |


 &nbsp;

<span id="veliveplayerstatus"></span>
# VeLivePlayerStatus

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerStatus
```


The status of the live player.

 &nbsp;

<span id="enumerated-value-4"></span>
## Enumerated Value

&nbsp;


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerStatusStopped |0 |The playback is stopped. |
|VeLivePlayerStatusPaused |1 |The playback is paused. |
|VeLivePlayerStatusPrepared |2 |The player finishes preparing and is waiting to render the video. |
|VeLivePlayerStatusPlaying |3 |Playback is currently in progress, meaning that the first frame has been rendered and no errors have occurred to the player. |
|VeLivePlayerStatusError |4 |An error has occurred to the player. |
|VeLivePlayerStatusStalled |5 |The player has stalled. |


 &nbsp;

<span id="veliveplayerlogconfig"></span>
# VeLivePlayerLogConfig

```java
public class com.ss.videoarch.liveplayer.log.VeLivePlayerLogConfig
```


Log settings.

 &nbsp;

<span id="member-property-2"></span>
## Member Property

&nbsp;


|Type |Default Value |Name |
|---|---|---|
|VeLivePlayerLogLevel |VeLivePlayerLogLevel.VeLivePlayerLogLevelVerbose |[logLevel](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerLogConfig-loglevel) |


 &nbsp;

<span id="instructions-3"></span>
## Instructions

 &nbsp;

<span id="loglevel"></span>
### logLevel

```java
public VeLivePlayerLogLevel com.ss.videoarch.liveplayer.log.VeLivePlayerLogConfig.logLevel = VeLivePlayerLogLevel.VeLivePlayerLogLevelVerbose
```


The output log level. The default value is `VeLivePlayerLogLevelDebug`. For details, see [VeLivePlayerLogLevel](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerLogLevel).

 &nbsp;

<span id="veliveplayerstreamdata"></span>
# VeLivePlayerStreamData

```java
public class com.ss.videoarch.liveplayer.VeLivePlayerStreamData
```


The configurations for the pull stream addresses.

 &nbsp;

<span id="member-property-3"></span>
## Member Property

&nbsp;


|Type |Default Value |Name |
|---|---|---|
|boolean |false |[enableABR](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-enableabr) |
|boolean |false |[enableMainBackupSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-enablemainbackupswitch) |
|VeLivePlayerResolution |new VeLivePlayerResolution(VeLivePlayerResolution.VeLivePlayerResolutionOrigin) |[defaultResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-defaultresolution) |
|VeLivePlayerFormat |VeLivePlayerFormat.VeLivePlayerFormatFLV |[defaultFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-defaultformat) |
|VeLivePlayerProtocol |VeLivePlayerProtocol.VeLivePlayerProtocolTCP |[defaultProtocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-defaultprotocol) |
|List |null |[mainStreamList](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-mainstreamlist) |
|List |null |[backupStreamList](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-backupstreamlist) |
|boolean |false |[enableSmoothSwitchResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-enablesmoothswitchresolution) |


 &nbsp;

<span id="instructions-4"></span>
## Instructions

 &nbsp;

<span id="enableabr"></span>
### enableABR

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerStreamData.enableABR = false
```


Whether to enable adaptive bitrate (ABR). The default value is `false`.


* true: Enable;

* false: Disable.

    &nbsp;


 &nbsp;

<span id="enablemainbackupswitch"></span>
### enableMainBackupSwitch

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerStreamData.enableMainBackupSwitch = false
```


Whether to enable switching between primary and backup streams. The default value is `false`.


* true: Enable;

* false: Disable.

    &nbsp;


 &nbsp;

<span id="defaultresolution"></span>
### defaultResolution

```java
public VeLivePlayerResolution com.ss.videoarch.liveplayer.VeLivePlayerStreamData.defaultResolution = new VeLivePlayerResolution(VeLivePlayerResolution.VeLivePlayerResolutionOrigin)
```


The default resolution. The default value is `VeLivePlayerResolutionOrigin`, which indicates the original resolution. See [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution) for details.

 &nbsp;

<span id="defaultformat"></span>
### defaultFormat

```java
public VeLivePlayerFormat com.ss.videoarch.liveplayer.VeLivePlayerStreamData.defaultFormat = VeLivePlayerFormat.VeLivePlayerFormatFLV
```


The default video format. The default value is `VeLivePlayerFormatFLV`. See [VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerFormat) for details.

 &nbsp;

<span id="defaultprotocol"></span>
### defaultProtocol

```java
public VeLivePlayerProtocol com.ss.videoarch.liveplayer.VeLivePlayerStreamData.defaultProtocol = VeLivePlayerProtocol.VeLivePlayerProtocolTCP
```


The default transmission protocol. The default value is `VeLivePlayerProtocolTCP`. See [VeLivePlayerProtocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProtocol) for details.

 &nbsp;

<span id="mainstreamlist"></span>
### mainStreamList

```java
public List<VeLivePlayerStream> com.ss.videoarch.liveplayer.VeLivePlayerStreamData.mainStreamList = null
```


A list of main stream addresses. See [VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-VeLivePlayerStream) for details.

 &nbsp;

<span id="backupstreamlist"></span>
### backupStreamList

```java
public List<VeLivePlayerStream> com.ss.videoarch.liveplayer.VeLivePlayerStreamData.backupStreamList = null
```


A list of backup stream addresses. See [VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-VeLivePlayerStream) for details.

 &nbsp;

<span id="enablesmoothswitchresolution"></span>
### enableSmoothSwitchResolution

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerStreamData.enableSmoothSwitchResolution = false
```


Whether to enable smooth resolution switching. The default value is `false`. If enabled, the SDK will attempt to perform a smooth transition when you call the [switchResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-switchresolution) method to manually switch the resolution, avoiding black screens or lag. Valid values:


* `true`: Enable.

* `false`: Disable.

    &nbsp;


 &nbsp;

<span id="veliveplayerresolutionswitchreason"></span>
# VeLivePlayerResolutionSwitchReason

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerResolutionSwitchReason
```


The reason why the video resolution has changed.

 &nbsp;

<span id="enumerated-value-5"></span>
## Enumerated Value

&nbsp;


|Type |Value |Instructions |
|---|---|---|
|VeLiveplayerResolutionSwitchByAuto |0 |The resolution is switched automatically through the adaptive bitrate (ABR) feature. |
|VeLiveplayerResolutionSwitchByManual |1 |The resolution is changed after [switchResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-switchresolution) is called. |


 &nbsp;

<span id="veliveplayersupportresolutionswitcherror"></span>
# VeLivePlayerSupportResolutionSwitchError

```java
public static class com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError
```


Error for quality level switching.

 &nbsp;

<span id="member-property-4"></span>
## Member Property

&nbsp;


|Type |Default Value |Name |
|---|---|---|
|int |0 |[VeLivePlayerNoError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerSupportResolutionSwitchError-veliveplayernoerror) |
|int |\-1 |[VeLivePlayerErrorInvalidRes](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerSupportResolutionSwitchError-veliveplayererrorinvalidres) |
|int |\-2 |[VeLivePlayerErrorSameRes](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerSupportResolutionSwitchError-veliveplayererrorsameres) |
|int |\-3 |[VeLivePlayerErrorStatusInvalid](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerSupportResolutionSwitchError-veliveplayererrorstatusinvalid) |
|int |\-4 |[VeLivePlayerErrorResNotFound](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerSupportResolutionSwitchError-veliveplayererrorresnotfound) |
|int |\-5 |[VeLivePlayerErrorFormatNotSupport](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerSupportResolutionSwitchError-veliveplayererrorformatnotsupport) |
|int |\-6 |[VeLivePlayerErrorConfigNotSupport](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerSupportResolutionSwitchError-veliveplayererrorconfignotsupport) |


 &nbsp;

<span id="instructions-5"></span>
## Instructions

 &nbsp;

<span id="veliveplayernoerror"></span>
### VeLivePlayerNoError

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError.VeLivePlayerNoError = 0
```


No error.

 &nbsp;

<span id="veliveplayererrorinvalidres"></span>
### VeLivePlayerErrorInvalidRes

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError.VeLivePlayerErrorInvalidRes = -1
```


Invalid quality level.

 &nbsp;

<span id="veliveplayererrorsameres"></span>
### VeLivePlayerErrorSameRes

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError.VeLivePlayerErrorSameRes = -2
```


The same as the current quality level.

 &nbsp;

<span id="veliveplayererrorstatusinvalid"></span>
### VeLivePlayerErrorStatusInvalid

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError.VeLivePlayerErrorStatusInvalid = -3
```


The player status is not `prepare`.

 &nbsp;

<span id="veliveplayererrorresnotfound"></span>
### VeLivePlayerErrorResNotFound

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError.VeLivePlayerErrorResNotFound = -4
```


The corresponding quality level is not found.

 &nbsp;

<span id="veliveplayererrorformatnotsupport"></span>
### VeLivePlayerErrorFormatNotSupport

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError.VeLivePlayerErrorFormatNotSupport = -5
```


The current playback format does not support this quality level.

 &nbsp;

<span id="veliveplayererrorconfignotsupport"></span>
### VeLivePlayerErrorConfigNotSupport

```java
public static final int com.ss.videoarch.liveplayer.VeLivePlayerError.VeLivePlayerSupportResolutionSwitchError.VeLivePlayerErrorConfigNotSupport = -6
```


The current playback configuration does not support this quality level.

 &nbsp;

<span id="veliveplayerstream"></span>
# VeLivePlayerStream

```java
public static class com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream
```


The information about a pull stream address.

 &nbsp;

<span id="member-property-5"></span>
## Member Property

&nbsp;


|Type |Default Value |Name |
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


 &nbsp;

<span id="instructions-6"></span>
## Instructions

 &nbsp;

<span id="url"></span>
### url

```java
public String com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.url = null
```


The pull stream address.

 &nbsp;

<span id="resolution"></span>
### resolution

```java
public VeLivePlayerResolution com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.resolution = new VeLivePlayerResolution(VeLivePlayerResolution.VeLivePlayerResolutionOrigin)
```


The playback resolution. For details, see [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerResolution).

 &nbsp;

<span id="bitrate"></span>
### bitrate

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.bitrate
```


The playback bitrate, in Kbps.

 &nbsp;

<span id="format"></span>
### format

```java
public VeLivePlayerFormat com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.format = VeLivePlayerFormat.VeLivePlayerFormatFLV
```


The format of the live stream. See [VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerFormat) for details.

 &nbsp;

<span id="streamtype"></span>
### streamType

```java
public VeLivePlayerStreamType com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain
```


Whether the stream is a main or backup stream. See [VeLivePlayerStreamType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamType) for details.

 &nbsp;

<span id="priority"></span>
### priority

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.priority = 0
```


The priority of the stream. The value must be `0` (default) or a positive integer. A larger value indicates a higher priority.

 &nbsp;

<span id="retrymaxcount-1"></span>
### retryMaxCount

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.retryMaxCount = -1
```


The maximum number of retry attempts for the stream, representing the total number of playback attempts (including the initial attempt). For example, a value of `3` means the player will retry at most 2 times after the initial failure. Valid values:


* `-1` (Default): Use the [retryMaxCount](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-retrymaxcount) value in `VeLivePlayerConfiguration`.

* `0`: Do not attempt to play this stream.

* `> 0`: The specific total number of attempts.

    &nbsp;


 &nbsp;

<span id="retryintervaltimems-1"></span>
### retryIntervalTimeMs

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.retryIntervalTimeMs = -1
```


The retry interval, in ms. The default value is `-1`. If the value is `-1`, the player uses the [retryIntervalTimeMs](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-retryintervaltimems) value in `VeLivePlayerConfiguration`.

 &nbsp;

<span id="protocol"></span>
### protocol

```java
public VeLivePlayerProtocol com.ss.videoarch.liveplayer.VeLivePlayerStreamData.VeLivePlayerStream.protocol = VeLivePlayerProtocol.VeLivePlayerProtocolDefault
```


The transmission protocol. See [VeLivePlayerProtocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProtocol) for details.

 &nbsp;

<span id="veliveplayerfillmode"></span>
# VeLivePlayerFillMode

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerFillMode
```


The fill mode of the player screen.

 &nbsp;

<span id="enumerated-value-6"></span>
## Enumerated Value

&nbsp;


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerFillModeAspectFit |0 |Display the full video. The video is uniformly scaled until one dimension of the video hits the boundary of the screen. Any remaining space on the screen will be filled with black. |
|VeLivePlayerFillModeFullFill |1 |Stretch the video to fill the screen. The aspect ratio of the video might change. |
|VeLivePlayerFillModeAspectFill |2 |Uniformly scale the video until the screen is completely filled. Part of the video may be cropped. |


 &nbsp;

<span id="veliveplayerpixelformat"></span>
# VeLivePlayerPixelFormat

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerPixelFormat
```


The pixel format of the video frame.

 &nbsp;

<span id="enumerated-value-7"></span>
## Enumerated Value

&nbsp;


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerPixelFormatUnknown |0 |Unknown format. |
|VeLivePlayerPixelFormatRGBA32 |1 |RGBA8888. |
|VeLivePlayerPixelFormatTexture |2 |Texture. |
|VeLivePlayerPixelFormatI420 |3 |YUV420P format. |


 &nbsp;

<span id="veliveplayerstatistics"></span>
# VeLivePlayerStatistics

```java
public class com.ss.videoarch.liveplayer.VeLivePlayerStatistics
```


The playback statistics.

 &nbsp;

<span id="member-property-6"></span>
## Member Property

&nbsp;


|Type |Default Value |Name |
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


 &nbsp;

<span id="instructions-7"></span>
## Instructions

 &nbsp;

<span id="url-1"></span>
### url

```java
public String com.ss.videoarch.liveplayer.VeLivePlayerStatistics.url
```


The current pull stream address.

 &nbsp;

<span id="ishardwaredecode"></span>
### isHardwareDecode

```java
public boolean com.ss.videoarch.liveplayer.VeLivePlayerStatistics.isHardwareDecode
```


Whether hardware decoding is used.


* true: Hardware decoding is used;

* false: Hardware decoding is not used.

    &nbsp;


 &nbsp;

<span id="videocodec"></span>
### videoCodec

```java
public String com.ss.videoarch.liveplayer.VeLivePlayerStatistics.videoCodec
```


The encoding format of the video.

 &nbsp;

<span id="stalltimems"></span>
### stallTimeMs

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.stallTimeMs
```


The cumulative duration of stutters that occurred since the beginning of playback, in milliseconds.

 &nbsp;

<span id="bandwidthestimation"></span>
### bandwidthEstimation

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.bandwidthEstimation
```


Bandwidth estimation, unit is kbps.

 &nbsp;

<span id="delayms"></span>
### delayMs

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.delayMs
```


The current playback latency, in milliseconds.

 &nbsp;

<span id="delays2sms"></span>
### delayS2sMs

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.delayS2sMs = -1
```


Server\-to\-server delay, in milliseconds. Indicates the time taken for the stream to travel from the MediaLive push\-side edge node to the MediaLive pull\-side edge node. The value is `-1` when the SEI message does not contain the server timestamps for when the stream reaches the push\-side edge node and the pull\-side edge node.

 &nbsp;

<span id="delaye2ems"></span>
### delayE2eMs

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.delayE2eMs = -1
```


End\-to\-end delay, in milliseconds. Indicates the time taken from when the Broadcast SDK writes the timestamp into the SEI message to when the Player SDK parses the SEI message locally. Accurate calculation depends on NTP\-based clock synchronization. The value is `-1` when the SEI message does not contain the timestamp written by the Broadcast SDK.

 &nbsp;

<span id="delays2ems"></span>
### delayS2eMs

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.delayS2eMs = -1
```


Server\-to\-end delay, in milliseconds. Indicates the time taken from when the stream reaches the MediaLive push\-side edge node to when the Player SDK parses the SEI message locally. Accurate calculation depends on NTP\-based clock synchronization. The value is `-1` when the SEI message does not contain the server timestamp for when the stream reaches the MediaLive push\-side edge node.

 &nbsp;

<span id="width"></span>
### width

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerStatistics.width
```


The width of the video, in pixels.

 &nbsp;

<span id="height"></span>
### height

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerStatistics.height
```


The height of the video, in pixels.

 &nbsp;

<span id="fps"></span>
### fps

```java
public float com.ss.videoarch.liveplayer.VeLivePlayerStatistics.fps
```


The frame rate of the video, in fps.

 &nbsp;

<span id="bitrate-1"></span>
### bitrate

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.bitrate
```


The downlink bitrate, in Kbps.

 &nbsp;

<span id="videobufferms"></span>
### videoBufferMs

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.videoBufferMs
```


The video buffer, in milliseconds.

 &nbsp;

<span id="audiobufferms"></span>
### audioBufferMs

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerStatistics.audioBufferMs
```


The audio buffer, in milliseconds.

 &nbsp;

<span id="format-1"></span>
### format

```java
public VeLivePlayerFormat com.ss.videoarch.liveplayer.VeLivePlayerStatistics.format
```


The video format. For more information, see [VeLivePlayerFormat](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#veliveplayerformat).

 &nbsp;

<span id="protocol-1"></span>
### protocol

```java
public VeLivePlayerProtocol com.ss.videoarch.liveplayer.VeLivePlayerStatistics.protocol
```


The transmission protocol of the live stream. For more information, see [VeLivePlayerProtocol](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#veliveplayerprotocol).

 &nbsp;

<span id="veliveplayervideoframe"></span>
# VeLivePlayerVideoFrame

```java
public class com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame
```


The video frame.

 &nbsp;

<span id="member-property-7"></span>
## Member Property

&nbsp;


|Type |Default Value |Name |
|---|---|---|
|VeLivePlayerVideoBufferType |`-` |[bufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-buffertype) |
|VeLivePlayerPixelFormat |`-` |[pixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-pixelformat) |
|int |`-` |[width](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-width) |
|int |`-` |[height](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-height) |
|long |`-` |[pts](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-pts) |
|VeLivePlayerVideoTexture |null |[texture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-texture) |
|ByteBuffer |null |[buffer](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-buffer) |
|byte[] |null |[data](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame-data) |


 &nbsp;

<span id="instructions-8"></span>
## Instructions

 &nbsp;

<span id="buffertype"></span>
### bufferType

```java
public VeLivePlayerVideoBufferType com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.bufferType
```


The encapsulation format. See [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoBufferType) for details.

 &nbsp;

<span id="pixelformat"></span>
### pixelFormat

```java
public VeLivePlayerPixelFormat com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.pixelFormat
```


The pixel format. See [VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerPixelFormat) for details.

 &nbsp;

<span id="width-1"></span>
### width

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.width
```


The video width, in pixels.

 &nbsp;

<span id="height-1"></span>
### height

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.height
```


The video height, in pixels.

 &nbsp;

<span id="pts"></span>
### pts

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.pts
```


The timestamp indicating the time when the video frame is rendered, in milliseconds.

 &nbsp;

<span id="texture"></span>
### texture

```java
public VeLivePlayerVideoTexture com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.texture = null
```


The texture data for OpenGL rendering. The SDK returns this video data type if you set [VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerPixelFormat) to `VeLivePlayerPixelFormatTexture` and set [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoBufferType) to `VeLivePlayerVideoBufferTypeTexture`. See [VeLivePlayerVideoTexture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoTexture) for details.

 &nbsp;

<span id="buffer"></span>
### buffer

```java
public ByteBuffer com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.buffer = null
```


The video data in ByteBuffer format. The SDK returns this video data type if you set [VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerPixelFormat) to `VeLivePlayerPixelFormatRGBA32` and set [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoBufferType) to `VeLivePlayerVideoBufferTypeByteBuffer`.

 &nbsp;

<span id="data"></span>
### data

```java
public byte [] com.ss.videoarch.liveplayer.VeLivePlayerVideoFrame.data = null
```


The video data in ByteArray format. The SDK returns this video data type if you set [VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerPixelFormat) to `VeLivePlayerPixelFormatRGBA32` and set [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoBufferType) to `VeLivePlayerVideoBufferTypeByteArray`.

 &nbsp;

<span id="veliveplayervideotexture"></span>
# VeLivePlayerVideoTexture

```java
public class com.ss.videoarch.liveplayer.VeLivePlayerVideoTexture
```


The video texture.

 &nbsp;

<span id="member-property-8"></span>
## Member Property

&nbsp;


|Type |Default Value |Name |
|---|---|---|
|int |`-` |[texId](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoTexture-texid) |
|EGLContext |`-` |[eglContext](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoTexture-eglcontext) |


 &nbsp;

<span id="instructions-9"></span>
## Instructions

 &nbsp;

<span id="texid"></span>
### texId

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerVideoTexture.texId
```


The video texture ID.

 &nbsp;

<span id="eglcontext"></span>
### eglContext

```java
public EGLContext com.ss.videoarch.liveplayer.VeLivePlayerVideoTexture.eglContext
```


OpenGL ES context for custom rendering. After you bind EGLContext to GLSurfaceView or TextureView, you can perform custom OpenGL ES rendering on the bound View.

 &nbsp;

<span id="veliveplayerstreamtype"></span>
# VeLivePlayerStreamType

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerStreamType
```


The type of the live stream.

 &nbsp;

<span id="enumerated-value-8"></span>
## Enumerated Value

&nbsp;


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerStreamTypeMain |0 |The primary stream. |
|VeLivePlayerStreamTypeBackup |1 |The backup stream. |


 &nbsp;

<span id="veliveplayerproperty"></span>
# VeLivePlayerProperty

```java
public class com.ss.videoarch.liveplayer.VeLivePlayerProperty
```


Advanced configurations.

 &nbsp;

<span id="member-property-9"></span>
## Member Property

&nbsp;


|Type |Default Value |Name |
|---|---|---|
|String |"VeLivePlayerKeySetParamsLowLatencyFLV" |[VeLivePlayerKeySetParamsLowLatencyFLV](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProperty-veliveplayerkeysetparamslowlatencyflv) |
|String |"VeLivePlayerKeySetParamsHttpHeaders" |[VeLivePlayerKeySetParamsHttpHeaders](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProperty-veliveplayerkeysetparamshttpheaders) |
|String |`"VeLivePlayerKeySetParamsRemoveQueryParams"` |[VeLivePlayerKeySetParamsRemoveQueryParams](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProperty-veliveplayerkeysetparamsremovequeryparams) |


 &nbsp;

<span id="instructions-10"></span>
## Instructions

 &nbsp;

<span id="veliveplayerkeysetparamslowlatencyflv"></span>
### VeLivePlayerKeySetParamsLowLatencyFLV

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerProperty.VeLivePlayerKeySetParamsLowLatencyFLV = "VeLivePlayerKeySetParamsLowLatencyFLV"
```


Configures FLV low\-latency settings (2–3 seconds latency). For detailed usage, see [Playing low-latency FLV streams](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-2#playing-low-latency-flv-streams).

 &nbsp;

<span id="veliveplayerkeysetparamshttpheaders"></span>
### VeLivePlayerKeySetParamsHttpHeaders

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerProperty.VeLivePlayerKeySetParamsHttpHeaders = "VeLivePlayerKeySetParamsHttpHeaders"
```


Sets custom HTTP headers for the player's HTTP requests. This is commonly used to pass additional information such as authentication tokens, cookies, or business tracking identifiers. For detailed usage, see [Customizing HTTP request headers](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-2#customizing-http-request-headers).

 &nbsp;

<span id="veliveplayerkeysetparamsremovequeryparams"></span>
### VeLivePlayerKeySetParamsRemoveQueryParams

```java
public static final String com.ss.videoarch.liveplayer.VeLivePlayerProperty.VeLivePlayerKeySetParamsRemoveQueryParams = "VeLivePlayerKeySetParamsRemoveQueryParams"
```


Sets whether to remove query parameters automatically appended by the SDK to the pull stream address. The default value is `false`. If enabled, stream pulling requests remove query parameters automatically appended by the SDK and retain query parameters already present in the original pull stream address. For detailed usage, see [Removing query parameters automatically appended by the SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-2?lang=en#removing-query-parameters-automatically-appended-by-the-sdk).


* `true`: Remove query parameters automatically appended by the SDK.

* `false`: Keep query parameters automatically appended by the SDK.


 &nbsp;

<span id="veliveplayerloglevel"></span>
# VeLivePlayerLogLevel

```java
public enum com.ss.videoarch.liveplayer.log.VeLivePlayerLogConfig.VeLivePlayerLogLevel
```


The output log level of the player.

 &nbsp;

<span id="enumerated-value-9"></span>
## Enumerated Value

&nbsp;


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerLogLevelVerbose |0 |Output logs at the VERBOSE, DEBUG, INFO, WARNING, and ERROR levels. |
|VeLivePlayerLogLevelDebug |1 |Output logs at the DEBUG, INFO, WARNING, and ERROR levels. |
|VeLivePlayerLogLevelInfo |2 |Output logs at the INFO, WARNING, and ERROR levels. |
|VeLivePlayerLogLevelWarn |3 |Output logs at the WARNING and ERROR levels. |
|VeLivePlayerLogLevelError |4 |Output logs at the ERROR level. |
|VeLivePlayerLogLevelNone |5 |Disable log printing. |


 &nbsp;

<span id="veliveplayeraudioframe"></span>
# VeLivePlayerAudioFrame

```java
public class com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame
```


The audio frame.

 &nbsp;

<span id="member-property-10"></span>
## Member Property

&nbsp;


|Type |Default Value |Name |
|---|---|---|
|VeLivePlayerAudioBufferType |`-` |[bufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-buffertype) |
|int |`-` |[sampleRate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-samplerate) |
|int |`-` |[channels](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-channels) |
|int |`-` |[bitDepth](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-bitdepth) |
|long |`-` |[pts](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-pts) |
|byte[] |null |[bufferArray](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-bufferarray) |
|ByteBuffer[] |null |[buffer](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-buffer) |
|int |`-` |[samples](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame-samples) |


 &nbsp;

<span id="instructions-11"></span>
## Instructions

 &nbsp;

<span id="buffertype-1"></span>
### bufferType

```java
public VeLivePlayerAudioBufferType com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.bufferType
```


The encapsulation format of the audio data. See [VeLivePlayerAudioBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioBufferType) for details.

 &nbsp;

<span id="samplerate"></span>
### sampleRate

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.sampleRate
```


The audio sample rate, in Hz.

 &nbsp;

<span id="channels"></span>
### channels

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.channels
```


The number of audio channels.


* 1: Mono;

* 2: Stereo.

    &nbsp;


 &nbsp;

<span id="bitdepth"></span>
### bitDepth

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.bitDepth
```


The audio bit depth.

 &nbsp;

<span id="pts-1"></span>
### pts

```java
public long com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.pts
```


The timestamp indicating the time when the audio is rendered, in milliseconds.

 &nbsp;

<span id="bufferarray"></span>
### bufferArray

```java
public byte [] com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.bufferArray = null
```


The PCM audio data. byte[] type.

 &nbsp;

<span id="buffer-1"></span>
### buffer

```java
public ByteBuffer [] com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.buffer = null
```


The PCM audio data. ByteBuffer[] type.

 &nbsp;

<span id="samples"></span>
### samples

```java
public int com.ss.videoarch.liveplayer.VeLivePlayerAudioFrame.samples
```


The number of audio samples.

 &nbsp;

<span id="veliveplayeraudiobuffertype"></span>
# VeLivePlayerAudioBufferType

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerAudioBufferType
```


The encapsulation format of the audio.

 &nbsp;

<span id="enumerated-value-10"></span>
## Enumerated Value

&nbsp;


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerAudioBufferTypeUnknown |0 |Unknown format. |
|VeLivePlayerAudioBufferTypeByteArray |1 |ByteArray. |


 &nbsp;

<span id="veliveplayerrotation"></span>
# VeLivePlayerRotation

```java
public enum com.ss.videoarch.liveplayer.VeLivePlayerDef.VeLivePlayerRotation
```


The clockwise video rotation angle.

 &nbsp;

<span id="enumerated-value-11"></span>
## Enumerated Value

&nbsp;


|Type |Value |Instructions |
|---|---|---|
|VeLivePlayerRotation0 |0 |No rotation. |
|VeLivePlayerRotation90 |1 |Rotate 90 degrees clockwise. |
|VeLivePlayerRotation180 |2 |Rotate 180 degrees clockwise. |
|VeLivePlayerRotation270 |3 |Rotate 270 degrees clockwise. |


 &nbsp;

<span id="veliveplayerstreaminfo"></span>
# VeLivePlayerStreamInfo

```java
public class com.ss.videoarch.liveplayer.hls.VeLivePlayerStreamInfo
```


HLS stream information.

 &nbsp;

<span id="member-variables"></span>
## Member Variables

&nbsp;


|Name |Type |Default |
|---|---|---|
|[width](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamInfo-width) |int |\- |
|[height](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamInfo-height) |int |\- |
|[bandwidth](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamInfo-bandwidth) |int |\- |
|[url](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamInfo-url) |String |\- |


 &nbsp;

<span id="member-functions-1"></span>
## Member Functions

&nbsp;


|Name |Return |
|---|---|
|[toString](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamInfo-tostring) |String |


 &nbsp;

<span id="variable-description"></span>
## Variable Description

 &nbsp;

<span id="width-2"></span>
### width

```java
public int com.ss.videoarch.liveplayer.hls.VeLivePlayerStreamInfo.width
```


The video width, in pixels.

 &nbsp;

<span id="height-2"></span>
### height

```java
public int com.ss.videoarch.liveplayer.hls.VeLivePlayerStreamInfo.height
```


The video height, in pixels.

 &nbsp;

<span id="bandwidth"></span>
### bandwidth

```java
public int com.ss.videoarch.liveplayer.hls.VeLivePlayerStreamInfo.bandwidth
```


The stream bandwidth, in bits per second (bps).

 &nbsp;

<span id="url-2"></span>
### url

```java
public String com.ss.videoarch.liveplayer.hls.VeLivePlayerStreamInfo.url
```


The playback URL of the HLS stream.

 &nbsp;

<span id="function-description"></span>
## Function Description

 &nbsp;

<span id="tostring"></span>
### toString

```java
public String com.ss.videoarch.liveplayer.hls.VeLivePlayerStreamInfo.toString()
```


Converts the HLS stream information to a string.

**Return Value**

A string that contains the video width, video height, bandwidth, and playback URL of the HLS stream.
