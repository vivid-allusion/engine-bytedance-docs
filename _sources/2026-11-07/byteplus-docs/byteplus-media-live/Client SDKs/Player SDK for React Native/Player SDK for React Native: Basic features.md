---
title: "Player SDK for React Native: Basic features"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rnplayer-basic-features"
---

This topic introduces how to implement the basic features of Player SDK for React Native.

<span id="e75435da"></span>
## Prerequisites

You have integrated and initialized the Player SDK by following the instructions provided in [Integrating the SDK for React Native](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-rn) and [Initializing the SDK for React Native](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-rn).

<span id="85b33bef"></span>
## Notes

Because the Player SDK uses various audio and video APIs that may not work properly on simulators, we recommend that you use a physical device for testing.

<span id="38d8dfa8"></span>
## Creating a player

To implement the basic features of the Player SDK, you must first create a player.

```JavaScript
import {initPlayer} from '@byteplus/react-native-live-pull';

const mLivePlayer = await initPlayer({
  viewId: 'pull-view', // initial configuration
  enableSei: true, 
  networkTimeoutMs: 10000
});
```


<span id="a0861da8"></span>
## Configuring the player

During the initialization of the player, configure it with the following parameters.


|Name |Type |Description |
|---|---|---|
|enableSei |boolean |Whether to enable the parsing of SEI messages. The default value is `false`. |
|enableHardwareDecode |boolean |Whether to enable hardware decoding. The default value is `true`. When hardware decoding is enabled, if the player fails to start hardware decoding or if hardware decoding fails, the player automatically switches to software decoding. |
|networkTimeoutMs |int |Network timeout duration in milliseconds. The default value is `5000`. If a network request does not receive a response from the server within the timeout period, the player considers the request to have failed. |
|retryIntervalTimeMs |int |The retry interval is in milliseconds. The default value is `5000`. During the live stream, if playback is interrupted by issues such as a network error, the player attempts to retry. |
|retryMaxCount |int |The maximum number of times the player automatically retries after a network connection error. The default value is `5`. If the value is `0`, the player will not automatically retry. |
|enableLiveDNS |boolean |Whether to enable local DNS prefetch. The default value is `false`. Enabling local DNS prefetch can reduce the time required to start playback.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If local DNS prefetch fails, the player may not function properly.</div><br> |
|enableStatisticsCallback |boolean |Whether to enable periodic callbacks for playback information. The default value is `false`. |
|statisticsCallbackInterval |int |The time interval for periodic callbacks that provide playback information, in seconds. The default value is `5`. |


<span id="467aee2b"></span>
## Setting a player observer

You can set a player observer to listen to the live player's events, such as status updates, playback errors, the reception of the first audio and video frames, and periodic statistical data. For details, refer to [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver).

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
## Setting the player view

To display video output, configure a rendering view using the provided NativeViewComponent.

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
## Setting the playback URL

You can set a pull stream address by calling [setPlayUrl](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setplayurl), which supports live streaming protocols such as RTMP, FLV and HLS.

```Java
const playUrl = "http://pull.example.com/live/stream.flv";
mLivePlayer.setPlayUrl(playUrl);
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you need to set multiple playback URLs, you can call <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setplaystreamdata">setPlayStreamData</a> which supports features including:</div>



* <div data-tips="true" data-tips-type="tip">Pulling streams using the RTM protocol,</div>


* <div data-tips="true" data-tips-type="tip">Pulling streams using the QUIC protocol,</div>


* <div data-tips="true" data-tips-type="tip">Setting a primary and a backup stream address,</div>


* <div data-tips="true" data-tips-type="tip">Resolution switching,</div>


* <div data-tips="true" data-tips-type="tip">Adaptive bitrate (ABR).</div>



<div data-tips="true" data-tips-type="tip">For more information, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-rnplayer-advanced-features">Player SDK for React Native: Advanced features</a>.</div>


<span id="3ccadb15"></span>
## Adjusting the playback screen

You can configure the fill mode, mirroring setting, and rotation for a better playback experience.

<span id="2d849b2f"></span>
### Setting the fill mode

Call [setRenderFillMode](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setrenderfillmode) to set the fill mode of the playback screen.


|Type |Description |
|---|---|
|VeLivePlayerFillModeAspectFit |Maintain the video's original aspect ratio until the video is fully displayed within the player. If the video's aspect ratio differs from that of the player, areas not filled by the video will appear black. |
|VeLivePlayerFillModeFullFill |The video completely fills the player, but the video's aspect ratio may change. |
|VeLivePlayerFillModeAspectFill |Maintain the video's original aspect ratio and fill the player. If the video's aspect ratio differs from that of the player, areas of the video that extend beyond the player's boundaries will be cropped, which may result in an incomplete view. |


```JavaScript
// Set the fill mode to aspect fill.
mLivePlayer.setRenderFillMode(
  VeLivePlayerFillMode.VeLivePlayerFillModeAspectFill,
);
```


<span id="1e5ee328"></span>
### Setting the mirroring

Call [setRenderMirror](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setrendermirror) to configure the mirroring setting of the playback screen.


|Type |Description |
|---|---|
|VeLivePlayerMirrorNone |No mirroring. |
|VeLivePlayerMirrorHorizontal |Horizontal mirroring. |
|VeLivePlayerMirrorVertical |Vertical mirroring. |


```JavaScript
// Configure the mirroring setting to horizontal.
mLivePlayer.setRenderMirror(VeLivePlayerMirror.VeLivePlayerMirrorHorizontal);
```


<span id="f20e2918"></span>
### Setting the rotation angle

Call [setRenderRotation](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setrenderrotation) to set the rotation angle of the playback screen.


|Type |Instruction |
|---|---|
|VeLivePlayerRotation0 |No rotation. |
|VeLivePlayerRotation90 |Rotate 90 degrees clockwise. |
|VeLivePlayerRotation180 |Rotate 180 degrees clockwise. |
|VeLivePlayerRotation270 |Rotate 270 degrees clockwise. |


```JavaScript
// Rotate the video 90 degrees clockwise.
mLivePlayer.setRenderRotation(VeLivePlayerRotation.VeLivePlayerRotation90);
```


<span id="c7385922"></span>
## Starting playback

Call [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#play) to start playback.

```JavaScript
mLivePlayer.play();
```


You can call [isPlaying](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#isplaying) to get the current playback status.

```JavaScript
const isPlaying = mLivePlayer.isPlaying();
```


<span id="b4c01274"></span>
## Pausing playback

Call [pause](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#pause) to pause playback.

```JavaScript
mLivePlayer.pause();
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In live streaming, pausing and stopping playback have the same effect. If you call <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#play">play</a> after pausing playback, the player will restart pulling the stream.</div>


<span id="8ac7ea54"></span>
## Stopping playback

Call [stop](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#stop) to stop playback. This method does not destroy the player.

```JavaScript
mLivePlayer.stop();
```


<span id="fbbab700"></span>
## Destroying the player

After playback has stopped, call this method to destroy the player and release its associated memory.

```Java
mLivePlayer.destroy();
```


<span id="48bc1b40"></span>
## Setting the background mode

By default, the player continues playing the audio when the application is running in the background. To pause audio playback, add the following code:

```JavaScript
AppState.addEventListener('change', state => {
  state === 'active' && mLivePlayer.play();
  state === 'background' && mLivePlayer.pause();
});
```


<span id="1e716940"></span>
## Muting playback

Call [setMute](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setmute) to mute or unmute the audio.

```JavaScript
mLivePlayer.setMute(true);
```


You can query whether the audio is muted by calling [isMute](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#ismute).

```JavaScript
boolean isMute = mLivePlayer.isMute();
```


<span id="2ad709e8"></span>
## Setting the player volume

You can control the playback volume by calling [setPlayerVolume](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setplayervolume). The parameter represents the volume level, with a default value of 1.0. The value ranges from 0.0 to 1.0.

```JavaScript
mLivePlayer.setPlayerVolume(0.5);
```
