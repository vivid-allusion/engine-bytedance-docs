---
title: "Android 播放器 SDK：概览"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-overview-zh-CN"
---

# 方法

|方法 |描述 |
|---|---|
|[setConfig](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setconfig) |初始化播放器，并配置是否开启 SEI 消息、硬件解码、本地 DNS 预取及其他配置。 |
|[getStreamList](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-getstreamlist) |获取流信息。 |
|[setEnableSharpen](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setenablesharpen) |设置是否启用视频锐化。 |
|[setObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setobserver) |设置播放器观察者，用于监听直播播放器事件，例如播放错误或状态更新、首个音视频帧渲染、分辨率切换。 |
|[setRenderFillMode](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setrenderfillmode) |设置播放器画面的填充模式。 |
|[getVersion](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-getversion) |获取播放器 SDK 的版本号。 |
|[setLogLevel](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setloglevel) |设置输出日志级别。 |
|[setSurfaceHolder](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setsurfaceholder) |设置用于视频渲染和播放的 `SurfaceHolder` 对象。如果使用 `SurfaceView` 播放，请使用此方法。 |
|[setSurface](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setsurface) |设置用于视频渲染和播放的 `Surface` 对象。如果使用 `SurfaceView` 或 `TextureView` 播放，请使用此方法。 |
|[setPlayUrl](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setplayurl) |设置拉流地址。 |
|[setPlayerVolume](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setplayervolume) |设置播放器音量。 |
|[setMute](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setmute) |设置播放是否静音。 |
|[isMute](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-ismute) |检查播放是否静音。 |
|[setUrlHostIP](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-seturlhostip) |设置域名到服务器 IP 地址的映射。 |
|[setProperty](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setproperty) |配置播放器高级设置，包括离屏渲染、最大缓冲时长和自适应码率（ABR）算法。 |
|[snapshot](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-snapshot) |对视频截图。 |
|[enableVideoFrameObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-enablevideoframeobserver) |设置视频帧观察者。 |
|[enableAudioFrameObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-enableaudioframeobserver) |设置音频帧观察者。 |
|[setRenderRotation](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setrenderrotation) |设置视频的顺时针旋转角度。 |
|[setRenderMirror](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setrendermirror) |配置镜像设置。 |
|[setEnableSuperResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setenablesuperresolution) |启用或禁用超分辨率。使用前，必须先联系 BytePlus [技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) 开通该功能。 |
|[isPlaying](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-isplaying) |检查播放器是否正在播放。 |
|[switchResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-switchresolution) |更改视频分辨率。 |
|[destroy](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-destroy) |停止播放并销毁播放器。 |
|[stop](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-stop) |停止播放。此方法不会销毁播放器。 |
|[play](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-play) |开始或恢复播放。 |
|[setPlayStreamData](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setplaystreamdata) |设置多路直播流。如果需要启用依赖多路直播流的功能，请调用此方法。例如自适应码率（ABR）、手动分辨率切换、主备流。 |

# 回调

|方法 |描述 |
|---|---|
|[onError](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onerror) |播放器发生错误时触发。 |
|[onFirstVideoFrameRender](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onfirstvideoframerender) |播放开始时，或播放中重试后渲染首个视频帧时触发。 |
|[onFirstAudioFrameRender](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onfirstaudioframerender) |播放开始时，或播放中重试后渲染首个音频帧时触发。 |
|[onStallStart](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onstallstart) |播放卡顿开始时触发。 |
|[onStallEnd](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onstallend) |播放卡顿停止时触发，即有足够音频缓冲后恢复播放时触发。 |
|[onVideoRenderStall](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onvideorenderstall) |视频渲染卡顿时触发。 |
|[onAudioRenderStall](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onaudiorenderstall) |音频渲染卡顿时触发。 |
|[onResolutionSwitch](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onresolutionswitch) |视频分辨率变化时触发。 |
|[onVideoSizeChanged](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onvideosizechanged) |视频尺寸变化时触发。 |
|[onReceiveSeiMessage](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onreceiveseimessage) |字符串 SEI 消息回调。播放器 SDK 接收到 SEI 消息时触发此回调。需要在 `VeLivePlayerConfiguration` 中启用 `enableSei` 属性。启用 `enableBinarySei` 属性后，将不再发送字符串 SEI 消息。 |
|[onReceiveBinarySeiMessage](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onreceivebinaryseimessage) |二进制 SEI 消息回调。播放器 SDK 接收到 SEI 消息时触发此回调。需要在 `VeLivePlayerConfiguration` 中启用 `enableBinarySei` 属性。启用 `enableBinarySei` 属性后，将不再发送字符串 SEI 消息。 |
|[onMainBackupSwitch](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onmainbackupswitch) |播放器在主流和备流之间切换时触发。 |
|[onPlayerStatusUpdate](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate) |播放状态变化时触发。 |
|[onPlayerStatusUpdate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate-2) |播放状态变化时触发。与 [onPlayerStatusUpdate](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate) 相比，此回调通过 `extraInfo` 返回当前播放流的补充信息。 |
|[onStatistics](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onstatistics) |定期触发，用于上报当前拉流地址、码率和帧率等信息。 |
|[onSnapshotComplete](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onsnapshotcomplete) |调用 [snapshot](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-snapshot) 后完成截图时触发。 |
|[onRenderVideoFrame](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onrendervideoframe) |播放器解码视频帧时触发。调用 [enableVideoFrameObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-enablevideoframeobserver) 可启用视频帧回调。 |
|[onRenderAudioFrame](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onrenderaudioframe) |播放器解码音频帧时触发。调用 [enableAudioFrameObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-enableaudioframeobserver) 可启用音频帧回调。 |
|[onStreamFailedOpenSuperResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution) |调用 [setEnableSuperResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setenablesuperresolution) 后，SDK 未能启用超分辨率时触发。 |
|[onStreamFailedOpenSharpen](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onstreamfailedopensharpen) |调用 [setEnableSharpen](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setenablesharpen) 后，SDK 未能启用锐化时触发。 |
|[onInfo](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-oninfo) |播放器遇到内部错误时触发。 |
|[onStreamFormatSwitch](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onstreamformatswitch) |播放器切换流格式时触发。 |
