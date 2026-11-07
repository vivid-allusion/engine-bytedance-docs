---
title: "Player SDK for Android: Overview"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-overview"
---

 &nbsp;

<span id="methods"></span>
# Methods

&nbsp;


|Method |Description |
|---|---|
|[setConfig](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setconfig) |Initializes the player and configures whether to turn on SEI messaging, hardware decoding, local DNS prefetch, and other configurations. |
|[getStreamList](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-getstreamlist) |Gets the stream information. |
|[setEnableSharpen](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setenablesharpen) |Set whether to enable video sharpening. |
|[setObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setobserver) |Sets the player observer to listen to the live player's events, such as playback errors or status updates, rendering of the first audio and video frame, and resolution switching. |
|[setRenderFillMode](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setrenderfillmode) |Sets the fill mode of the player screen. |
|[getVersion](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-getversion) |Gets the version number of the Player SDK. |
|[setLogLevel](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setloglevel) |Sets the level of the output log. |
|[setSurfaceHolder](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setsurfaceholder) |Sets the `SurfaceHolder` object for video rendering and playback. Use this method if you use `SurfaceView` for playback. |
|[setSurface](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setsurface) |Sets the `Surface` object for video rendering and playback. Use this method if you use `SurfaceView` or `TextureView` for playback. |
|[setPlayUrl](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setplayurl) |Sets a pull stream address. |
|[setPlayerVolume](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setplayervolume) |Sets the player volume. |
|[setMute](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setmute) |Sets whether to mute playback. |
|[isMute](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-ismute) |Checks whether playback is muted. |
|[setUrlHostIP](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-seturlhostip) |Sets the mapping of domain names to server IP addresses. |
|[setProperty](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setproperty) |Configures advanced settings for the player, including offscreen rendering, maximum buffer duration, and adaptive bitrate (ABR) algorithms. |
|[snapshot](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-snapshot) |Takes a screenshot of the video. |
|[enableVideoFrameObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-enablevideoframeobserver) |Sets the video frame observer. |
|[enableAudioFrameObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-enableaudioframeobserver) |Sets the audio frame observer. |
|[setRenderRotation](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setrenderrotation) |Sets the clockwise rotation angle of the video. |
|[setRenderMirror](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setrendermirror) |Configures mirroring settings. |
|[setEnableSuperResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setenablesuperresolution) |Enables or disables super resolution. You must first contact BytePlus [technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) to activate the feature before using it. |
|[isPlaying](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-isplaying) |Checks whether the player is playing. |
|[switchResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-switchresolution) |Changes the video resolution. |
|[destroy](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-destroy) |Stops playback and destroys the player. |
|[stop](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-stop) |Stops playback. This method does not destroy the player. |
|[play](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-play) |Starts or resumes playback. |
|[setPlayStreamData](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setplaystreamdata) |Sets multiple live streams. Call this method if you need to enable features requiring multiple live streams, such as adaptive bitrate (ABR), manual resolution switching, and primary and backup streams. |


 &nbsp;

<span id="callbacks"></span>
# Callbacks

&nbsp;


|Method |Description |
|---|---|
|[onError](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onerror) |Occurs when a player error occurs. |
|[onFirstVideoFrameRender](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onfirstvideoframerender) |Occurs when the first video frame is rendered at the beginning of playback or after a retry during playback. |
|[onFirstAudioFrameRender](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onfirstaudioframerender) |Occurs when the first audio frame is rendered at the beginning of playback or after a retry during playback. |
|[onStallStart](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onstallstart) |Occurs when a playback stutter starts. |
|[onStallEnd](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onstallend) |Occurs when a playback stutter stops, that is, when playback resumes after there is enough audio buffer. |
|[onVideoRenderStall](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onvideorenderstall) |Occurs when video rendering stutters. |
|[onAudioRenderStall](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onaudiorenderstall) |Occurs when audio rendering stutters. |
|[onResolutionSwitch](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onresolutionswitch) |Occurs when the video resolution changes. |
|[onVideoSizeChanged](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onvideosizechanged) |Occurs when the video size changes. |
|[onReceiveSeiMessage](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onreceiveseimessage) |String SEI message callback. This callback is triggered when the player SDK receives an SEI message. It is necessary to enable the `enableSei` property in `VeLivePlayerConfiguration`. When the `enableBinarySei` property is enabled, the string SEI message will no longer be sent. |
|[onReceiveBinarySeiMessage](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onreceivebinaryseimessage) |Binary SEI message callback. This callback is triggered when the player SDK receives an SEI message. It is necessary to enable the `enableBinarySei` property in `VeLivePlayerConfiguration`. When the `enableBinarySei` property is enabled, the string SEI message will no longer be sent. |
|[onMainBackupSwitch](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onmainbackupswitch) |Occurs when the player switches between the primary stream and the backup stream. |
|[onPlayerStatusUpdate](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate) |Occurs when the playback status changes. |
|[onPlayerStatusUpdate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate-2) |Occurs when the playback status changes. Compared with [onPlayerStatusUpdate](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate), this callback returns supplemental information about the current playback stream through `extraInfo`. |
|[onStatistics](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onstatistics) |Occurs periodically to report information such as the current pull stream address, bitrate, and frame rate. |
|[onSnapshotComplete](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onsnapshotcomplete) |Occurs when a screenshot is taken after [snapshot](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-snapshot) is called. |
|[onRenderVideoFrame](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onrendervideoframe) |Occurs when the player decodes a video frame. Call [enableVideoFrameObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-enablevideoframeobserver) to enable video frame callback. |
|[onRenderAudioFrame](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onrenderaudioframe) |Occurs when the player decodes an audio frame. Call [enableAudioFrameObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-enableaudioframeobserver) to enable audio frame callback. |
|[onStreamFailedOpenSuperResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution) |Occurs when the SDK fails to enable super resolution after [setEnableSuperResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setenablesuperresolution) is called. |
|[onStreamFailedOpenSharpen](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onstreamfailedopensharpen) |Occurs when the SDK fails to enable sharpen after [setEnableSharpen](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setenablesharpen) is called. |
|[onInfo](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-oninfo) |Triggered when the player encounters an internal error. |
|[onStreamFormatSwitch](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onstreamformatswitch) |Triggered when the player switches the stream format. |
