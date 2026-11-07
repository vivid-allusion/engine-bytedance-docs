---
title: "Android 版 Player SDK：概觀"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-overview-zh-TW"
---

# 方法

|方法 |說明 |
|---|---|
|[setConfig](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setconfig) |初始化播放器，並設定是否開啟 SEI 訊息、硬體解碼、本機 DNS 預先擷取和其他設定。 |
|[getStreamList](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-getstreamlist) |取得串流資訊。 |
|[setEnableSharpen](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setenablesharpen) |設定是否啟用影片銳化。 |
|[setObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setobserver) |設定播放器觀察者，以監聽直播播放器的事件，例如播放錯誤或狀態更新、第一個音訊和視訊影格的算繪，以及解析度切換。 |
|[setRenderFillMode](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setrenderfillmode) |設定播放器畫面的填滿模式。 |
|[getVersion](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-getversion) |取得 Player SDK 的版本號碼。 |
|[setLogLevel](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setloglevel) |設定輸出日誌的層級。 |
|[setSurfaceHolder](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setsurfaceholder) |設定用於影片算繪和播放的 `SurfaceHolder` 物件。如果使用 `SurfaceView` 播放，請使用此方法。 |
|[setSurface](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setsurface) |設定用於影片算繪和播放的 `Surface` 物件。如果使用 `SurfaceView` 或 `TextureView` 播放，請使用此方法。 |
|[setPlayUrl](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setplayurl) |設定拉流位址。 |
|[setPlayerVolume](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setplayervolume) |設定播放器音量。 |
|[setMute](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setmute) |設定是否將播放靜音。 |
|[isMute](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-ismute) |檢查播放是否已靜音。 |
|[setUrlHostIP](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-seturlhostip) |設定網域名稱到伺服器 IP 位址的對應。 |
|[setProperty](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setproperty) |設定播放器的進階設定，包括離屏算繪、最大緩衝區持續時間和自適應位元率 (ABR) 演算法。 |
|[snapshot](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-snapshot) |擷取影片螢幕截圖。 |
|[enableVideoFrameObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-enablevideoframeobserver) |設定視訊影格觀察者。 |
|[enableAudioFrameObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-enableaudioframeobserver) |設定音訊影格觀察者。 |
|[setRenderRotation](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setrenderrotation) |設定影片的順時針旋轉角度。 |
|[setRenderMirror](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setrendermirror) |設定鏡像設定。 |
|[setEnableSuperResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setenablesuperresolution) |啟用或停用超解析度。使用此功能前，您必須先聯絡 BytePlus [技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)以啟用此功能。 |
|[isPlaying](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-isplaying) |檢查播放器是否正在播放。 |
|[switchResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-switchresolution) |變更影片解析度。 |
|[destroy](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-destroy) |停止播放並銷毀播放器。 |
|[stop](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-stop) |停止播放。此方法不會銷毀播放器。 |
|[play](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-play) |開始或繼續播放。 |
|[setPlayStreamData](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setplaystreamdata) |設定多個直播串流。如果需要啟用需要多個直播串流的功能，請呼叫此方法，例如自適應位元率 (ABR)、手動解析度切換，以及主要和備用串流。 |

# 回呼

|方法 |說明 |
|---|---|
|[onError](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onerror) |當播放器發生錯誤時發生。 |
|[onFirstVideoFrameRender](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onfirstvideoframerender) |在播放開始時，或播放期間重試後算繪第一個視訊影格時發生。 |
|[onFirstAudioFrameRender](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onfirstaudioframerender) |在播放開始時，或播放期間重試後算繪第一個音訊影格時發生。 |
|[onStallStart](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onstallstart) |當播放卡頓開始時發生。 |
|[onStallEnd](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onstallend) |當播放卡頓停止時發生，也就是有足夠音訊緩衝區後播放恢復時。 |
|[onVideoRenderStall](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onvideorenderstall) |當視訊算繪卡頓時發生。 |
|[onAudioRenderStall](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onaudiorenderstall) |當音訊算繪卡頓時發生。 |
|[onResolutionSwitch](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onresolutionswitch) |當影片解析度變更時發生。 |
|[onVideoSizeChanged](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onvideosizechanged) |當影片大小變更時發生。 |
|[onReceiveSeiMessage](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onreceiveseimessage) |字串 SEI 訊息回呼。當播放器 SDK 收到 SEI 訊息時，會觸發此回呼。必須在 `VeLivePlayerConfiguration` 中啟用 `enableSei` 屬性。啟用 `enableBinarySei` 屬性時，將不再傳送字串 SEI 訊息。 |
|[onReceiveBinarySeiMessage](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onreceivebinaryseimessage) |二進位 SEI 訊息回呼。當播放器 SDK 收到 SEI 訊息時，會觸發此回呼。必須在 `VeLivePlayerConfiguration` 中啟用 `enableBinarySei` 屬性。啟用 `enableBinarySei` 屬性時，將不再傳送字串 SEI 訊息。 |
|[onMainBackupSwitch](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onmainbackupswitch) |當播放器在主要串流和備用串流之間切換時發生。 |
|[onPlayerStatusUpdate](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate) |當播放狀態變更時發生。 |
|[onPlayerStatusUpdate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate-2) |當播放狀態變更時發生。與 [onPlayerStatusUpdate](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate) 相比，此回呼會透過 `extraInfo` 傳回目前播放串流的補充資訊。 |
|[onStatistics](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onstatistics) |定期發生，以回報目前拉流位址、位元率和影格率等資訊。 |
|[onSnapshotComplete](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onsnapshotcomplete) |呼叫 [snapshot](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-snapshot) 後擷取螢幕截圖時發生。 |
|[onRenderVideoFrame](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onrendervideoframe) |當播放器解碼視訊影格時發生。呼叫 [enableVideoFrameObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-enablevideoframeobserver) 以啟用視訊影格回呼。 |
|[onRenderAudioFrame](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onrenderaudioframe) |當播放器解碼音訊影格時發生。呼叫 [enableAudioFrameObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-enableaudioframeobserver) 以啟用音訊影格回呼。 |
|[onStreamFailedOpenSuperResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution) |呼叫 [setEnableSuperResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setenablesuperresolution) 後，SDK 無法啟用超解析度時發生。 |
|[onStreamFailedOpenSharpen](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onstreamfailedopensharpen) |呼叫 [setEnableSharpen](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setenablesharpen) 後，SDK 無法啟用銳化時發生。 |
|[onInfo](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-oninfo) |當播放器遇到內部錯誤時觸發。 |
|[onStreamFormatSwitch](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onstreamformatswitch) |當播放器切換串流格式時觸發。 |
