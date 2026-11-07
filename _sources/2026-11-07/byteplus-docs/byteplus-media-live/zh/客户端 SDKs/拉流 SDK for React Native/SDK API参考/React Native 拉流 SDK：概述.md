---
title: "React Native 拉流 SDK：概述"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-overview-zh-CN"
---

<span id="methods"></span>
## 方法


|方法 |接口行为 |
|---|---|
|[setConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setconfig) |初始化播放器，并配置是否开启 SEI 消息、硬解、本地 DNS 预取等其他配置项。 |
|[setObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setobserver) |设置播放器监听器，用于监听播放器的事件，例如回放错误或状态更新、首帧音视频渲染、分辨率切换等。 |
|[setRenderFillMode](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setrenderfillmode) |设置播放器画面填充模式。 |
|[setPlayerVolume](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setplayervolume) |设置播放器音量。 |
|[isPlaying](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-isplaying) |检查播放器是否正在播放。 |
|[switchResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-switchresolution) |切换视频分辨率。 |
|[destroy](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-destroy) |停止回放并销毁播放器。 |
|[stop](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-stop) |停止回放。此方法不会销毁播放器。 |
|[pause](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-pause) |暂停回放。 |
|[play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-play) |开始或恢复回放。 |
|[setPlayStreamData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setplaystreamdata) |设置多个在线流。如需启用需要多个在线流的功能，例如自适应码率（ABR）、手动分辨率切换、主流与备流，请调用此方法。 |
|[setPlayUrl](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setplayurl) |设置拉流地址。 |
|[setMute](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setmute) |设置是否静音回放。 |
|[isMute](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-ismute) |检查回放是否为静音状态。 |
|[setProperty](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setproperty) |配置播放器高级设置，包括离屏渲染、最大缓冲时长、自适应码率算法等。如需进一步信息，请联系 BytePlus 技术支持。 |
|[setRenderRotation](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setrenderrotation) |设置视频顺时针旋转角度。 |
|[setRenderMirror](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setrendermirror) |配置镜像设置。 |
|[setEnableSuperResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setenablesuperresolution) |开启或关闭超分。使用前必须先联系 BytePlus [technical support](https://www.byteplus.com/en/support) 激活该功能。 |
|[startPictureInPicture()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#3bbd9dbc) |开启画中画（PiP）模式，并将播放器显示为悬浮窗。 |
|[stopPictureInPicture()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#fb3447d5) |退出画中画（PiP）模式。 |
|[isPictureInPictureSupported()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#4b3e1343) |检查当前环境是否支持画中画（PiP）模式。 |
|[setPictureInPictureListener()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#9727b950) |设置画中画相关事件的监听器，例如画中画启动、停止或错误。 |
|[enablePictureInPicture()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#a1f76572) |（仅限 iOS）应用进入后台时自动开启画中画模式。 |
|[disablePictureInPicture()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#1b8b5910) |（仅限 iOS）禁用自动画中画模式。 |


<span id="80a2effe"></span>
## 回调


|方法 |接口行为 |
|---|---|
|[onError](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onerror) |播放器发生错误时触发。 |
|[onFirstVideoFrameRender](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onfirstvideoframerender) |回放开始或回放重试后，首个视频帧渲染时触发。 |
|[onFirstAudioFrameRender](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onfirstaudioframerender) |回放开始或回放重试后，首个音频帧渲染时触发。 |
|[onStallStart](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onstallstart) |回放卡顿开始时触发。 |
|[onStallEnd](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onstallend) |回放卡顿结束时触发，即音频缓冲充足后回放恢复。 |
|[onVideoRenderStall](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onvideorenderstall) |视频渲染卡顿时触发。 |
|[onAudioRenderStall](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onaudiorenderstall) |音频渲染卡顿时触发。 |
|[onResolutionSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onresolutionswitch) |视频分辨率切换时触发。 |
|[onVideoSizeChanged](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onvideosizechanged) |视频尺寸变化时触发。 |
|[onReceiveSeiMessage](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onreceiveseimessage) |拉流 SDK 收到 SEI 消息时触发。 |
|[onMainBackupSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onmainbackupswitch) |播放器在主流与备流切换时触发。 |
|[onPlayerStatusUpdate](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onplayerstatusupdate) |回放状态变化时触发。 |
|[onStatistics](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onstatistics) |定期触发，报告当前拉流地址、码率、帧率等信息。 |
|[onSnapshotComplete](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onsnapshotcomplete) |调用截图后，截图完成时触发。 |
|[onRenderVideoFrame](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onrendervideoframe) |播放器解码视频帧时触发。调用 [enableVideoFrameObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/player-android-api-reference#veliveplayer-enablevideoframeobserver) 以开启视频帧回调。 |
|[onRenderAudioFrame](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onrenderaudioframe) |播放器解码音频帧时触发。调用 enableAudioFrameObserver 以开启音频帧回调。 |
|[onStreamFailedOpenSuperResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#veliveplayerobserver-onstreamfailedopensuperresolution) |调用 setEnableSuperResolution 后，SDK 启用超分失败时触发。 |
|[onStartPictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#5c6ba1f3) |画中画模式启动时触发。你可以使用此回调来更新 UI 状态或添加分析跟踪。 |
|[onStopPictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#b33d5937) |当画中画模式被用户操作或程序方式退出时触发。 |
|[onClickPictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#a2f98e10) |当画中画窗口被点击时触发。使用此回调来响应用户对 PiP 窗口的交互。 |
|[onError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#a9a4d317) |当发生与画中画模式相关的错误时触发。使用此回调进行错误报告或降级处理。 |
