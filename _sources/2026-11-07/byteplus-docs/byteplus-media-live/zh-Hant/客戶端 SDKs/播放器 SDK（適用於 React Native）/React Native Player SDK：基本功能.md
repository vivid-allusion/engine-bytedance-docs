---
title: "React Native Player SDK：基本功能"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rnplayer-basic-features-zh-TW"
---

本主題介紹如何實現 React Native Player SDK 的基本功能。

<span id="e75435da"></span>
## 先決條件

您已根據 [整合 Player SDK 至 React Native](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-rn-zh-TW) 和 [初始化 React Native 的 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-rn-zh-TW) 中提供的指引完成 Player SDK 的集成與初始化。

<span id="85b33bef"></span>
## Note

由於 Player SDK 使用多種音訊與視訊 API，這些 API 在模擬器上可能無法正常運作，建議您使用實體裝置進行測試。

<span id="38d8dfa8"></span>
## 建立播放器

要實現 Player SDK 的基本功能，必須先建立播放器。

```JavaScript
import {initPlayer} from '@byteplus/react-native-live-pull';

const mLivePlayer = await initPlayer({
  viewId: 'pull-view', // initial configuration
  enableSei: true, 
  networkTimeoutMs: 10000
});
```


<span id="a0861da8"></span>
## 配置播放器

在初始化播放器時，請使用以下參數進行配置。


|名稱 |類型 |說明 |
|---|---|---|
|enableSei |boolean |是否啟用 SEI 訊息解析。預設值為 `false`。 |
|enableHardwareDecode |boolean |是否啟用硬體解碼。預設值為 `true`。啟用硬體解碼時，若播放器無法啟動硬體解碼或硬體解碼失敗，播放器會自動切換至軟體解碼。 |
|networkTimeoutMs |int |網路逾時時間（毫秒）。預設值為 `5000`。若網路請求在逾時期間未收到伺服器回應，播放器會判定請求失敗。 |
|retryIntervalTimeMs |int |重試間隔時間（毫秒）。預設值為`5000`。在直播過程中，若因網路錯誤等問題導致播放中斷，播放器會嘗試重新連線。 |
|retryMaxCount |int |播放器在網路連線錯誤後自動重試的最大次數。預設值為`5`。若設為`0`，播放器將不會自動重試。 |
|enableLiveDNS |boolean |是否啟用本地 DNS 預取。預設值為`false`。啟用本地 DNS 預取可減少啟動播放所需的時間。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若本地 DNS 預取失敗，播放器可能無法正常運作。</div><br> |
|enableStatisticsCallback |boolean |是否啟用播放資訊的定期回調。預設值為`false`。 |
|statisticsCallbackInterval |int |提供播放資訊的定期回調時間間隔，單位為秒。預設值為`5`。 |


<span id="467aee2b"></span>
## 設置播放器監聽器

您可以設置播放器監聽器來監聽直播播放器的事件，例如狀態更新、播放錯誤、收到首個音訊與視訊幀，以及定期統計數據。詳細資訊請參考 [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver)。

```JavaScript
mLivePlayer.setObserver({
  onFirstVideoFrameRender() {
    addLog('First video frame render');
  },
  onFirstAudioFrameRender() {
    addLog('First audio frame render');
  },
  onVideoRenderStall() {
    addLog('Video rendering is stall');
  },
  onAudioRenderStall() {
    addLog('Audio rendering is Stall');
  },
  onResolutionSwitch(_player, resolution) {
    if (resolution !== playerConfig.resolution) {
      playerConfig.resolution = resolution;
    }
    addLog(`Resolution switch: ${VeLivePlayerResolution[resolution]}`);
  },
  onVideoSizeChanged(_player, width, height) {
    addLog(`Video size change: ${width} * ${height}`);
  },
  onReceiveSeiMessage(_player, message) {
    if (message.includes('[RTS]')) {
      return;
    }
    addLog(`Receive an SEI  message: ${message}`);
  },
  onMainBackupSwitch(_player, _streamType, _error) {
    addLog('Switch between the primary stream and the backup stream');
  },
  onPlayerStatusUpdate(_player, status) {
    addLog('Playback status changes' + VeLivePlayerStatus[status]);
  },
  onSnapshotComplete(_player, _bitmap) {
    addLog('Screenshot is taken');
  },
  onStreamFailedOpenSuperResolution(_player, err) {
    addLog(`Super resolution failed to open. (${err.errorCode || ''}) ${err.errorMsg || ''}`);
  },
  onStatistics(_player, info) {
    playerConfig.info = `url: ${info.url}
Current playback delay: ${info.delayMs}
Download bitrate: ${info.bitrate}
Current playback format: ${VeLivePlayerFormat[info.format]}
Current fps: ${info.fps}
Resolution: ${info.width} * ${info.height}
Decoding method: ${info.isHardwareDecode? 'Hardware decoding' : 'Software decoding'}
Transmission Protocol: ${VeLivePlayerProtocol[info.protocol]}
Playback stutter duration: ${info.stallTimeMs}
Audio buffer size: ${info.audioBufferMs}
Video buffer size: ${info.videoBufferMs}
Video codec types: ${info.videoCodec}`;
  },
  onError(_player, error) {
    addLog(`Play error: (${error.errorCode}) ${error.errorMsg}`);
  },
});
```


<span id="d9f8c0fe"></span>
## 設置播放器視圖

若要顯示視訊輸出，請使用提供的 NativeViewComponent 配置渲染視圖。

```JavaScript
import {NativeViewComponent} from '@byteplus/react-native-velive-pull';

const PullView = () => {
  return (
    <NativeViewComponent
      id="pull-view"
      kind={
        Platform.select({
          android: 'SurfaceView',
          ios: 'UIView',
        })!
      }
      onViewLoad={initPlayer}
      style={{width: '100%', height: '100%'}}
    />
  );
};
```


<span id="920f81ab"></span>
## 設置播放 URL

您可以呼叫 [setPlayUrl](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setplayurl) 設置拉流地址，支援 RTMP、FLV、HLS 等直播協議。

```Java
const playUrl = "http://pull.example.com/live/stream.flv";
mLivePlayer.setPlayUrl(playUrl);
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">若需設定多個播放 URL，可呼叫<a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setplaystreamdata">setPlayStreamData</a>，其支援以下功能：</div>



* <div data-tips="true" data-tips-type="tip">使用 RTM 協定拉流，</div>


* <div data-tips="true" data-tips-type="tip">使用 QUIC 協定拉流，</div>


* <div data-tips="true" data-tips-type="tip">設定主備串流地址，</div>


* <div data-tips="true" data-tips-type="tip">切換解析度，</div>


* <div data-tips="true" data-tips-type="tip">自適應碼率（ABR）。</div>



<div data-tips="true" data-tips-type="tip">更多資訊請參見<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-rnplayer-advanced-features-zh-TW">React Native Player SDK：進階功能</a>。</div>


<span id="3ccadb15"></span>
## 調整播放畫面

您可以配置填充模式、鏡像設置與旋轉角度，以提升播放體驗。

<span id="2d849b2f"></span>
### 設置填充模式

呼叫 [setRenderFillMode](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setrenderfillmode) 設置播放畫面的填充模式。


|類型 |說明 |
|---|---|
|VeLivePlayerFillModeAspectFit |保持影片原始寬高比，直到影片完整顯示於播放器內。若影片寬高比與播放器不同，未被影片填滿的區域將顯示為黑色。 |
|VeLivePlayerFillModeFullFill |影片會完全填滿播放器，但影片的寬高比可能會改變。 |
|VeLivePlayerFillModeAspectFill |保持影片原始寬高比並填滿播放器。若影片寬高比與播放器不同，超出播放器範圍的影片區域將被裁切，可能導致畫面不完整。 |


```JavaScript
// Set the fill mode to aspect fill.
mLivePlayer.setRenderFillMode(
  VeLivePlayerFillMode.VeLivePlayerFillModeAspectFill,
);
```


<span id="1e5ee328"></span>
### 設置鏡像

呼叫 [setRenderMirror](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setrendermirror) 配置播放畫面的鏡像設置。


|類型 |說明 |
|---|---|
|VeLivePlayerMirrorNone |無鏡像。 |
|VeLivePlayerMirrorHorizontal |水平鏡像。 |
|VeLivePlayerMirrorVertical |垂直鏡像。 |


```JavaScript
// Configure the mirroring setting to horizontal.
mLivePlayer.setRenderMirror(VeLivePlayerMirror.VeLivePlayerMirrorHorizontal);
```


<span id="f20e2918"></span>
### 設置旋轉角度

呼叫 [setRenderRotation](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setrenderrotation) 設置播放畫面的旋轉角度。


|類型 |說明 |
|---|---|
|VeLivePlayerRotation0 |無旋轉。 |
|VeLivePlayerRotation90 |順時針旋轉 90 度。 |
|VeLivePlayerRotation180 |順時針旋轉 180 度。 |
|VeLivePlayerRotation270 |順時針旋轉 270 度。 |


```JavaScript
// Rotate the video 90 degrees clockwise.
mLivePlayer.setRenderRotation(VeLivePlayerRotation.VeLivePlayerRotation90);
```


<span id="c7385922"></span>
## 開始播放

呼叫 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#play) 開始播放。

```JavaScript
mLivePlayer.play();
```


您可以呼叫 [isPlaying](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#isplaying) 取得目前播放狀態。

```JavaScript
const isPlaying = mLivePlayer.isPlaying();
```


<span id="b4c01274"></span>
## 暫停播放

呼叫 [pause](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#pause) 暫停播放。

```JavaScript
mLivePlayer.pause();
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在直播場景下，暫停與停止播放效果相同。若在暫停播放後呼叫 <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#play">play</a>，播放器將重新拉流。</div>


<span id="8ac7ea54"></span>
## 停止播放

呼叫 [stop](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#stop) 停止播放。此方法不會銷毀播放器。

```JavaScript
mLivePlayer.stop();
```


<span id="fbbab700"></span>
## 銷毀播放器

播放停止後，請呼叫此方法銷毀播放器並釋放其相關記憶體。

```Java
mLivePlayer.destroy();
```


<span id="48bc1b40"></span>
## 設置背景模式

預設情況下，當應用程式在背景執行時，播放器會持續播放音訊。若要暫停音訊播放，請新增以下程式碼：

```JavaScript
AppState.addEventListener('change', state => {
  state === 'active' && mLivePlayer.play();
  state === 'background' && mLivePlayer.pause();
});
```


<span id="1e716940"></span>
## 靜音播放

呼叫 [setMute](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setmute) 以靜音或取消靜音音訊。

```JavaScript
mLivePlayer.setMute(true);
```


您可以呼叫 [isMute](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#ismute) 查詢音訊是否處於靜音狀態。

```JavaScript
boolean isMute = mLivePlayer.isMute();
```


<span id="2ad709e8"></span>
## 設置播放器音量

您可以呼叫 [setPlayerVolume](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setplayervolume) 控制播放音量。該參數代表音量等級，預設值為 1.0，取值範圍為 0.0 到 1.0。

```JavaScript
mLivePlayer.setPlayerVolume(0.5);
```
