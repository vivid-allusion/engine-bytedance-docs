---
title: "React Native 拉流 SDK：基础功能"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rnplayer-basic-features-zh-CN"
---

本主题介绍如何实现 React Native 拉流 SDK 的基础功能。

<span id="e75435da"></span>
## 前提条件

你已按照 [集成 React Native 的拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/106185) 和 [初始化 React Native 拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/106178) 提供的说明集成并初始化拉流 SDK。

<span id="85b33bef"></span>
## 说明

由于拉流 SDK 使用了多种音视频 API，这些 API 在模拟器上可能无法正常工作，建议使用真实设备进行测试。

<span id="38d8dfa8"></span>
## 创建播放器

要实现拉流 SDK 的基础功能，需先创建一个播放器。

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

在播放器初始化过程中，请使用以下参数进行配置。


|名称 |类型 |接口行为 |
|---|---|---|
|enableSei |boolean |是否开启 SEI 消息解析。默认值为 `false`。 |
|enableHardwareDecode |boolean |是否开启硬解。默认值为 `true`。开启硬解后，若播放器无法启动硬解或硬解失败，则会自动切换为软解。 |
|networkTimeoutMs |int |网络超时时长（毫秒）。默认值为 `5000`。若网络请求在超时时间内未收到服务器返回调用结果，则播放器认为请求失败。 |
|retryIntervalTimeMs |int |重试间隔时长（毫秒）。默认值为`5000`。在直播流过程中，如果回放因网络错误等问题中断，播放器会尝试重新拉流。 |
|retryMaxCount |int |播放器在网络连接错误后自动重试的最大次数。默认值为`5`。若取值为`0`，播放器不会自动重试。 |
|enableLiveDNS |boolean |是否启用本地 DNS 预取。默认值为`false`。启用本地 DNS 预取可减少启动回放所需时间。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若本地 DNS 预取失败，播放器可能无法正常工作。</div><br> |
|enableStatisticsCallback |boolean |是否启用回放信息的周期性回调。默认值为`false`。 |
|statisticsCallbackInterval |int |提供回放信息的周期性回调时间间隔，单位为秒。默认值为`5`。 |


<span id="467aee2b"></span>
## 设置播放器观察者

你可以设置播放器观察者，监听直播流播放器的事件，例如状态更新、回放错误、收到首帧音视频、以及周期性统计数据。详情请参见 [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver)。

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
## 设置播放器视图

要显示视频输出，请使用提供的 NativeViewComponent 配置渲染视图。

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
## 设置播放地址

你可以通过调用 [setPlayUrl](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setplayurl) 设置拉流地址，支持 RTMP、FLV、HLS 等直播流协议。

```Java
const playUrl = "http://pull.example.com/live/stream.flv";
mLivePlayer.setPlayUrl(playUrl);
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需设置多个播放地址，可调用<a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setplaystreamdata">setPlayStreamData</a>，支持以下功能：</div>



* <div data-tips="true" data-tips-type="tip">使用 RTM 协议拉流，</div>


* <div data-tips="true" data-tips-type="tip">使用 QUIC 协议拉流，</div>


* <div data-tips="true" data-tips-type="tip">设置主流和备流地址，</div>


* <div data-tips="true" data-tips-type="tip">分辨率切换，</div>


* <div data-tips="true" data-tips-type="tip">自适应码率（ABR）。</div>



<div data-tips="true" data-tips-type="tip">更多信息请参见<a href="https://docs.byteplus.com/docs/byteplus-media-live/106193">React Native 拉流 SDK：高级功能</a>。</div>


<span id="3ccadb15"></span>
## 调整回放画面

你可以配置填充模式、镜像设置和旋转角度，以获得更好的回放体验。

<span id="2d849b2f"></span>
### 设置填充模式

调用 [setRenderFillMode](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setrenderfillmode) 设置回放画面的填充模式。


|Type |接口行为 |
|---|---|
|VeLivePlayerFillModeAspectFit |保持视频原始视频长宽比，直至视频完整显示在播放器内。若视频长宽比与播放器不同，未被视频填充的区域将显示为黑色。 |
|VeLivePlayerFillModeFullFill |视频完全填充播放器，但视频长宽比可能发生变化。 |
|VeLivePlayerFillModeAspectFill |保持视频原始视频长宽比并填充播放器。若视频长宽比与播放器不同，超出播放器边界的视频区域将被裁剪，可能导致画面不完整。 |


```JavaScript
// Set the fill mode to aspect fill.
mLivePlayer.setRenderFillMode(
  VeLivePlayerFillMode.VeLivePlayerFillModeAspectFill,
);
```


<span id="1e5ee328"></span>
### 设置镜像

调用 [setRenderMirror](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setrendermirror) 配置回放画面的镜像设置。


|Type |接口行为 |
|---|---|
|VeLivePlayerMirrorNone |无镜像。 |
|VeLivePlayerMirrorHorizontal |水平镜像。 |
|VeLivePlayerMirrorVertical |垂直镜像。 |


```JavaScript
// Configure the mirroring setting to horizontal.
mLivePlayer.setRenderMirror(VeLivePlayerMirror.VeLivePlayerMirrorHorizontal);
```


<span id="f20e2918"></span>
### 设置旋转角度

调用 [setRenderRotation](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setrenderrotation) 设置回放画面的旋转角度。


|Type |Instruction |
|---|---|
|VeLivePlayerRotation0 |无旋转。 |
|VeLivePlayerRotation90 |顺时针旋转 90 度。 |
|VeLivePlayerRotation180 |顺时针旋转 180 度。 |
|VeLivePlayerRotation270 |顺时针旋转 270 度。 |


```JavaScript
// Rotate the video 90 degrees clockwise.
mLivePlayer.setRenderRotation(VeLivePlayerRotation.VeLivePlayerRotation90);
```


<span id="c7385922"></span>
## 开始回放

调用 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#play) 开始回放。

```JavaScript
mLivePlayer.play();
```


你可以调用 [isPlaying](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#isplaying) 获取当前回放状态。

```JavaScript
const isPlaying = mLivePlayer.isPlaying();
```


<span id="b4c01274"></span>
## 暂停回放

调用 [pause](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#pause) 暂停回放。

```JavaScript
mLivePlayer.pause();
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在直播流中，暂停和停止回放效果相同。若在暂停回放后调用 <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#play">play</a>，播放器将重新拉流。</div>


<span id="8ac7ea54"></span>
## 停止回放

调用 [stop](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#stop) 停止回放。此方法不会销毁播放器。

```JavaScript
mLivePlayer.stop();
```


<span id="fbbab700"></span>
## 销毁播放器

回放停止后，调用此方法销毁播放器并释放相关内存。

```Java
mLivePlayer.destroy();
```


<span id="48bc1b40"></span>
## 设置后台模式

默认情况下，应用在后台运行时，播放器会继续播放音频。如需暂停音频回放，请添加如下代码：

```JavaScript
AppState.addEventListener('change', state => {
  state === 'active' && mLivePlayer.play();
  state === 'background' && mLivePlayer.pause();
});
```


<span id="1e716940"></span>
## 静音回放

调用 [setMute](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setmute) 实现音频静音或取消静音。

```JavaScript
mLivePlayer.setMute(true);
```


你可以通过调用 [isMute](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#ismute) 查询音频是否已静音。

```JavaScript
boolean isMute = mLivePlayer.isMute();
```


<span id="2ad709e8"></span>
## 设置播放器音量

你可以通过调用 [setPlayerVolume](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setplayervolume) 控制回放音量。该参数表示音量等级，默认值为 1.0，取值范围为 0.0 到 1.0。

```JavaScript
mLivePlayer.setPlayerVolume(0.5);
```
