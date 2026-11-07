---
title: "React Native 用 Player SDK：總覽"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-overview-zh-TW"
---

<span id="methods"></span>
## 方法


|方法 |說明 |
|---|---|
|[setConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setconfig) |初始化播放器，並設定是否啟用 SEI 訊息、硬體解碼、本地 DNS 預取，以及其他配置。 |
|[setObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setobserver) |設置播放器觀察者，以監聽直播播放器的事件，例如播放錯誤或狀態更新、首個音訊和視訊畫面渲染，以及解析度切換。 |
|[setRenderFillMode](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setrenderfillmode) |設定播放器畫面的填充模式。 |
|[setPlayerVolume](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setplayervolume) |設定播放器音量。 |
|[isPlaying](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-isplaying) |檢查播放器是否正在播放。 |
|[switchResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-switchresolution) |切換視訊解析度。 |
|[destroy](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-destroy) |停止播放並銷毀播放器。 |
|[stop](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-stop) |停止播放。此方法不會銷毀播放器。 |
|[pause](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-pause) |暫停播放。 |
|[play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-play) |開始或恢復播放。 |
|[setPlayStreamData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setplaystreamdata) |設定多路直播流。若需啟用多路直播流相關功能，例如自適應碼率（ABR）、手動解析度切換，以及主備流，請呼叫此方法。 |
|[setPlayUrl](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setplayurl) |設定拉流地址。 |
|[setMute](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setmute) |設定是否靜音播放。 |
|[isMute](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-ismute) |檢查播放是否為靜音狀態。 |
|[setProperty](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setproperty) |配置播放器進階設定，包括離屏渲染、最大緩衝時長，以及自適應碼率（ABR）演算法。如需進一步資訊，請聯絡 BytePlus 技術支援。 |
|[setRenderRotation](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setrenderrotation) |設定視訊順時針旋轉角度。 |
|[setRenderMirror](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setrendermirror) |配置鏡像設定。 |
|[setEnableSuperResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setenablesuperresolution) |啟用或停用超解析度。使用此功能前，必須先聯絡 BytePlus [技術支援](https://www.byteplus.com/en/support)啟用該功能。 |
|[startPictureInPicture()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#3bbd9dbc) |啟動子母畫面（PiP）模式，並將播放器顯示於浮動視窗。 |
|[stopPictureInPicture()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#fb3447d5) |退出子母畫面（PiP）模式。 |
|[isPictureInPictureSupported()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#4b3e1343) |檢查目前環境是否支援子母畫面（PiP）模式。 |
|[setPictureInPictureListener()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#9727b950) |設定 PiP 相關事件的監聽器，例如 PiP 啟動、停止或錯誤。 |
|[enablePictureInPicture()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#a1f76572) |（僅限 iOS）當應用程式進入背景時，啟用自動 PiP 模式。 |
|[disablePictureInPicture()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#1b8b5910) |（僅限 iOS）停用自動 PiP 模式。 |


<span id="80a2effe"></span>
## 回調


|方法 |說明 |
|---|---|
|[onError](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onerror) |當播放器發生錯誤時觸發。 |
|[onFirstVideoFrameRender](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onfirstvideoframerender) |於播放開始或重試後，首個視訊畫面渲染時觸發。 |
|[onFirstAudioFrameRender](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onfirstaudioframerender) |於播放開始或重試後，首個音訊畫面渲染時觸發。 |
|[onStallStart](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onstallstart) |當播放卡頓開始時觸發。 |
|[onStallEnd](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onstallend) |當播放卡頓結束時觸發，即音訊緩衝足夠後恢復播放。 |
|[onVideoRenderStall](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onvideorenderstall) |當視訊渲染卡頓時觸發。 |
|[onAudioRenderStall](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onaudiorenderstall) |當音訊渲染卡頓時觸發。 |
|[onResolutionSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onresolutionswitch) |當視訊解析度變更時觸發。 |
|[onVideoSizeChanged](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onvideosizechanged) |當視訊尺寸變更時觸發。 |
|[onReceiveSeiMessage](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onreceiveseimessage) |當 Player SDK 接收到 SEI 訊息時觸發。 |
|[onMainBackupSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onmainbackupswitch) |當播放器在主流與備流間切換時觸發。 |
|[onPlayerStatusUpdate](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onplayerstatusupdate) |當播放狀態變更時觸發。 |
|[onStatistics](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onstatistics) |定期觸發，回報目前拉流地址、碼率、幀率等資訊。 |
|[onSnapshotComplete](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onsnapshotcomplete) |呼叫快照後，截圖完成時觸發。 |
|[onRenderVideoFrame](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onrendervideoframe) |當播放器解碼視訊畫面時觸發。 |
|[onRenderAudioFrame](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onrenderaudioframe) |當播放器解碼音訊畫面時觸發。請呼叫 enableAudioFrameObserver 以啟用音訊畫面回調。 |
|[onStreamFailedOpenSuperResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onstreamfailedopensuperresolution) |呼叫 setEnableSuperResolution 後，SDK 啟用超解析度失敗時觸發。 |
|[onStartPictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#5c6ba1f3) |啟動子母畫面模式時觸發。你可以使用此回呼來更新 UI 狀態或新增分析追蹤。 |
|[onStopPictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#b33d5937) |當畫中畫模式被退出時（無論是使用者操作或程式控制），會觸發此事件。 |
|[onClickPictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#a2f98e10) |當畫中畫視窗被點擊時，會觸發此事件。使用此回呼來回應使用者對 PiP 視窗的互動。 |
|[onError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#a9a4d317) |當發生與畫中畫模式相關的錯誤時，會觸發此事件。使用此回呼進行錯誤回報或備援處理。 |
