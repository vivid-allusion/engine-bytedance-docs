---
title: "iOS 播放器 SDK：概述"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api-overview-zh-CN"
---

# 方法

|方法 |描述 |
|---|---|
|[init](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-init) |初始化播放器。 |
|[initWithType:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-initwithtype) |初始化指定类型的播放器。 |
|[getStreamList](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-getstreamlist) |获取流信息。 |
|[setEnableSharpen:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setenablesharpen) |设置是否启用视频锐化。启用后，视频中的边缘和细节更加明显，画面更清晰、更生动。 |
|[isSupportResolutionSwitch:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-issupportresolutionswitch) |检查播放器当前是否支持指定的分辨率档位。 |
|[setConfig:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setconfig) |配置播放器设置，包括是否开启 SEI 消息、硬件解码和本地 DNS 预取。 |
|[setObserver:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setobserver) |设置播放器观察者，用于监听 VeLivePlayer 的事件，例如播放错误或状态更新、首个音频和视频帧渲染以及分辨率切换。 |
|[setRenderFillMode:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setrenderfillmode) |设置播放器画面的填充模式。 |
|[setPlayUrl:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setplayurl) |设置拉流地址。 |
|[getVersion](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-getversion) |获取 Player SDK 的版本号。 |
|[setPlayStreamData:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setplaystreamdata) |设置多个直播流。如果需要启用依赖多个直播流的功能，请调用此方法，例如自适应码率（ABR）、手动分辨率切换以及主备流。 |
|[setLogLevel:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setloglevel) |设置输出日志的级别。 |
|[play](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-play) |开始或恢复播放。 |
|[stop](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-stop) |停止播放。此方法不会销毁播放器。 |
|[switchResolution:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-switchresolution) |更改视频分辨率。 |
|[setMute:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setmute) |设置是否静音播放。 |
|[isMute](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-ismute) |检查播放是否已静音。 |
|[destroy](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-destroy) |停止播放并销毁播放器。 |
|[snapshot](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-snapshot) |截取视频画面。 |
|[enableVideoFrameObserver:pixelFormat:bufferType:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enablevideoframeobserver-pixelformat-buffertype) |设置视频帧观察者。 |
|[enableAudioFrameObserver:enableRendering:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enableaudioframeobserver-enablerendering) |设置音频帧观察者。 |
|[setEnableSuperResolution:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setenablesuperresolution) |启用或禁用超分辨率。 |
|[setUrlHostIP:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-seturlhostip) |设置域名到服务器 IP 地址的映射。 |
|[setRenderRotation:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setrenderrotation) |设置视频的顺时针旋转角度。 |
|[setRenderMirror:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setrendermirror) |配置镜像设置。 |
|[setProperty:value:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setproperty-value) |配置播放器的高级设置，包括离屏渲染、最大缓冲时长和自适应码率（ABR）算法。 |
|[isPictureInPictureSupported](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-ispictureinpicturesupported) |当前设备是否支持画中画（PiP）。 |
|[isPictureInPictureStarted](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-ispictureinpicturestarted) |PiP 是否已成功启动。 |
|[startPictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-startpictureinpicture) |手动启动 PiP。 |
|[stopPictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-stoppictureinpicture) |手动停止 PiP 并关闭 PiP 窗口。 |
|[invalidatePictureInPicturePlaybackState](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-invalidatepictureinpictureplaybackstate) |手动更新 PiP 窗口中的播放/暂停按钮状态和进度显示。 |

# 回调

|方法 |描述 |
|---|---|
|[onError:error:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onerror-error) |播放器发生错误时触发。 |
|[onAudioRenderStall:stallTime:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onaudiorenderstall-stalltime) |音频渲染卡顿时触发。 |
|[onVideoRenderStall:stallTime:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onvideorenderstall-stalltime) |视频渲染卡顿时触发。 |
|[onFirstAudioFrameRender:isFirstFrame:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onfirstaudioframerender-isfirstframe) |播放开始时或播放期间重试后，首个音频帧完成渲染时触发。 |
|[onInfo:info:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-oninfo-info) |播放器遇到内部错误时触发。 |
|[onResolutionSwitch:resolution:error:reason:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onresolutionswitch-resolution-error-reason) |视频分辨率变化时触发。 |
|[onVideoSizeChanged:width:height:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onvideosizechanged-width-height) |视频尺寸变化时触发。 |
|[onReceiveBinarySeiMessage:message:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onreceivebinaryseimessage-message) |二进制 SEI 消息回调。播放器 SDK 收到 SEI 消息时触发此回调。需要在 `VeLivePlayerConfiguration` 中启用 `enableBinarySei` 属性。启用 `enableBinarySei` 属性后，将不再发送字符串 SEI 消息。 |
|[onMainBackupSwitch:streamType:error:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onmainbackupswitch-streamtype-error) |播放器在主流和备流之间切换时触发。 |
|[onPlayerStatusUpdate:status:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status) |播放状态变化时触发。 |
|[onPlayerStatusUpdate:status:extraInfo:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status-extrainfo) |播放状态变化时触发。与 [onPlayerStatusUpdate:status:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status) 相比，此回调会通过 `extraInfo` 返回当前播放流的补充信息。 |
|[onStatistics:statistics:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstatistics-statistics) |定期触发，用于上报当前拉流地址、码率和帧率等信息。 |
|[onSnapshotComplete:image:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onsnapshotcomplete-image) |调用 snapshot 后截图完成时触发。 |
|[onRenderVideoFrame:videoFrame:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onrendervideoframe-videoframe) |播放器解码视频帧时触发。调用 [enableVideoFrameObserver:pixelFormat:bufferType:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enablevideoframeobserver-pixelformat-buffertype) 启用视频帧回调。 |
|[onRenderAudioFrame:audioFrame:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onrenderaudioframe-audioframe) |播放器解码音频帧时触发。调用 [enableAudioFrameObserver:enableRendering:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enableaudioframeobserver-enablerendering) 启用音频帧回调。 |
|[onStreamFailedOpenSuperResolution:error:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution-error) |调用 [setEnableSuperResolution:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setenablesuperresolution) 后，SDK 未能启用超分辨率时触发。 |
|[getDrmResourceLoaderCertificateData:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-getdrmresourceloadercertificatedata) |你需要在此回调中返回 NSData 格式的 FairPlay 证书。 |
|[getDrmResourceLoaderLicenseUrl:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-getdrmresourceloaderlicenseurl) |你需要在此回调中返回 DRM 许可证的 URL。 |
|[onReceiveSeiMessage:message:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onreceiveseimessage-message) |字符串 SEI 消息回调。播放器 SDK 收到 SEI 消息时触发此回调。需要在 `VeLivePlayerConfiguration` 中启用 `enableSei` 属性。启用 `enableBinarySei` 属性后，将不再发送字符串 SEI 消息。 |
|[onStallStart:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstallstart) |播放卡顿开始时触发。 |
|[onStallEnd:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstallend) |播放卡顿停止时触发，即有足够的音频缓冲后恢复播放时触发。 |
|[onFirstVideoFrameRender:isFirstFrame:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onfirstvideoframerender-isfirstframe) |播放开始时或播放期间重试后，首个视频帧完成渲染时触发。 |
|[onStreamFormatSwitch:fromStreamFormat:toStreamFormat:error:extraInfo:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstreamformatswitch-fromstreamformat-tostreamformat-error-extrainfo) |播放器切换流格式时触发。 |
