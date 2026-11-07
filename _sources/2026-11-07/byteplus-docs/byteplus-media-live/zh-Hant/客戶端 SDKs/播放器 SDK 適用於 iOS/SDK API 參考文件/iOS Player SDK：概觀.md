---
title: "iOS Player SDK：概觀"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api-overview-zh-TW"
---

# 方法

|方法 |描述 |
|---|---|
|[init](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-init) |初始化播放器。 |
|[initWithType:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-initwithtype) |初始化指定類型的播放器。 |
|[getStreamList](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-getstreamlist) |取得串流資訊。 |
|[setEnableSharpen:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setenablesharpen) |設定是否啟用影片銳化。啟用後，影片中的邊緣和細節會更明顯，使畫面看起來更清晰生動。 |
|[isSupportResolutionSwitch:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-issupportresolutionswitch) |檢查播放器目前是否支援指定的解析度等級。 |
|[setConfig:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setconfig) |設定播放器組態，包括是否開啟 SEI 訊息、硬體解碼和本機 DNS 預先擷取。 |
|[setObserver:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setobserver) |設定播放器觀察者，以監聽 VeLivePlayer 的事件，例如播放錯誤或狀態更新、首個音訊和視訊影格的轉譯，以及解析度切換。 |
|[setRenderFillMode:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setrenderfillmode) |設定播放器畫面的填滿模式。 |
|[setPlayUrl:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setplayurl) |設定拉流位址。 |
|[getVersion](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-getversion) |取得 Player SDK 的版本號。 |
|[setPlayStreamData:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setplaystreamdata) |設定多個直播串流。如果需要啟用需要多個直播串流的功能，請呼叫此方法，例如自適應位元率 (ABR)、手動解析度切換，以及主串流和備用串流。 |
|[setLogLevel:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setloglevel) |設定輸出日誌的層級。 |
|[play](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-play) |開始或繼續播放。 |
|[stop](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-stop) |停止播放。此方法不會銷毀播放器。 |
|[switchResolution:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-switchresolution) |變更影片解析度。 |
|[setMute:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setmute) |設定是否將播放靜音。 |
|[isMute](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-ismute) |檢查播放是否已靜音。 |
|[destroy](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-destroy) |停止播放並銷毀播放器。 |
|[snapshot](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-snapshot) |擷取影片螢幕截圖。 |
|[enableVideoFrameObserver:pixelFormat:bufferType:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enablevideoframeobserver-pixelformat-buffertype) |設定視訊影格觀察者。 |
|[enableAudioFrameObserver:enableRendering:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enableaudioframeobserver-enablerendering) |設定音訊影格觀察者。 |
|[setEnableSuperResolution:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setenablesuperresolution) |啟用或停用超解析度。 |
|[setUrlHostIP:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-seturlhostip) |設定網域名稱到伺服器 IP 位址的對應。 |
|[setRenderRotation:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setrenderrotation) |設定影片的順時針旋轉角度。 |
|[setRenderMirror:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setrendermirror) |設定鏡像組態。 |
|[setProperty:value:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setproperty-value) |設定播放器進階組態，包括離屏轉譯、最大緩衝區持續時間和自適應位元率 (ABR) 演算法。 |
|[isPictureInPictureSupported](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-ispictureinpicturesupported) |目前裝置是否支援 PiP。 |
|[isPictureInPictureStarted](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-ispictureinpicturestarted) |PiP 是否已成功啟動。 |
|[startPictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-startpictureinpicture) |手動啟動 PiP。 |
|[stopPictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-stoppictureinpicture) |手動停止 PiP 並關閉 PiP 視窗。 |
|[invalidatePictureInPicturePlaybackState](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-invalidatepictureinpictureplaybackstate) |手動更新 PiP 視窗中的播放/暫停按鈕狀態和進度顯示。 |

# 回呼

|方法 |描述 |
|---|---|
|[onError:error:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onerror-error) |播放器發生錯誤時發生。 |
|[onAudioRenderStall:stallTime:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onaudiorenderstall-stalltime) |音訊轉譯發生卡頓時發生。 |
|[onVideoRenderStall:stallTime:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onvideorenderstall-stalltime) |視訊轉譯發生卡頓時發生。 |
|[onFirstAudioFrameRender:isFirstFrame:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onfirstaudioframerender-isfirstframe) |播放開始時或播放期間重試後，轉譯首個音訊影格時發生。 |
|[onInfo:info:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-oninfo-info) |播放器遇到內部錯誤時觸發。 |
|[onResolutionSwitch:resolution:error:reason:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onresolutionswitch-resolution-error-reason) |影片解析度變更時發生。 |
|[onVideoSizeChanged:width:height:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onvideosizechanged-width-height) |影片尺寸變更時發生。 |
|[onReceiveBinarySeiMessage:message:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onreceivebinaryseimessage-message) |二進位 SEI 訊息回呼。當 Player SDK 接收到 SEI 訊息時，會觸發此回呼。必須在 `VeLivePlayerConfiguration` 中啟用 `enableBinarySei` 屬性。啟用 `enableBinarySei` 屬性後，將不再傳送字串 SEI 訊息。 |
|[onMainBackupSwitch:streamType:error:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onmainbackupswitch-streamtype-error) |播放器在主串流和備用串流之間切換時發生。 |
|[onPlayerStatusUpdate:status:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status) |播放狀態變更時發生。 |
|[onPlayerStatusUpdate:status:extraInfo:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status-extrainfo) |播放狀態變更時發生。與 [onPlayerStatusUpdate:status:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status) 相比，此回呼會透過 `extraInfo` 傳回目前播放串流的補充資訊。 |
|[onStatistics:statistics:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstatistics-statistics) |定期發生，以回報目前拉流位址、位元率和影格率等資訊。 |
|[onSnapshotComplete:image:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onsnapshotcomplete-image) |呼叫 snapshot 後完成螢幕截圖時發生。 |
|[onRenderVideoFrame:videoFrame:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onrendervideoframe-videoframe) |播放器解碼視訊影格時發生。呼叫 [enableVideoFrameObserver:pixelFormat:bufferType:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enablevideoframeobserver-pixelformat-buffertype) 以啟用視訊影格回呼。 |
|[onRenderAudioFrame:audioFrame:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onrenderaudioframe-audioframe) |播放器解碼音訊影格時發生。呼叫 [enableAudioFrameObserver:enableRendering:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enableaudioframeobserver-enablerendering) 以啟用音訊影格回呼。 |
|[onStreamFailedOpenSuperResolution:error:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution-error) |呼叫 [setEnableSuperResolution:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setenablesuperresolution) 後，SDK 無法啟用超解析度時發生。 |
|[getDrmResourceLoaderCertificateData:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-getdrmresourceloadercertificatedata) |您需要在此回呼中傳回 NSData 格式的 FairPlay 憑證。 |
|[getDrmResourceLoaderLicenseUrl:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-getdrmresourceloaderlicenseurl) |您需要在此回呼中傳回 DRM 授權的 URL。 |
|[onReceiveSeiMessage:message:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onreceiveseimessage-message) |字串 SEI 訊息回呼。當 Player SDK 接收到 SEI 訊息時，會觸發此回呼。必須在 `VeLivePlayerConfiguration` 中啟用 `enableSei` 屬性。啟用 `enableBinarySei` 屬性後，將不再傳送字串 SEI 訊息。 |
|[onStallStart:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstallstart) |播放卡頓開始時發生。 |
|[onStallEnd:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstallend) |播放卡頓停止時發生，也就是有足夠音訊緩衝區後恢復播放時。 |
|[onFirstVideoFrameRender:isFirstFrame:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onfirstvideoframerender-isfirstframe) |播放開始時或播放期間重試後，轉譯首個視訊影格時發生。 |
|[onStreamFormatSwitch:fromStreamFormat:toStreamFormat:error:extraInfo:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstreamformatswitch-fromstreamformat-tostreamformat-error-extrainfo) |播放器切換串流格式時觸發。 |
