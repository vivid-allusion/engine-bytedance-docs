---
title: "Player SDK for iOS: Overview"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api-overview"
---

<span id="methods"></span>
# Methods


|Method |Description |
|---|---|
|[init](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-init) |Initializes the player. |
|[initWithType:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-initwithtype) |Initializes the specified type of player. |
|[getStreamList](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-getstreamlist) |Gets the stream information. |
|[setEnableSharpen:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setenablesharpen) |Sets whether to enable video sharpening. If enabled, the edges and details in the video become more pronounced, making the visuals appear clearer and more vivid. |
|[isSupportResolutionSwitch:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-issupportresolutionswitch) |Check whether the player currently supports the specified resolution level. |
|[setConfig:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setconfig) |Configures player settings, including whether to turn on SEI messaging, hardware decoding, and local DNS prefetch. |
|[setObserver:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setobserver) |Sets the player observer to listen to the VeLivePlayer's events, such as playback errors or status updates, rendering of the first audio and video frame, and resolution switching. |
|[setRenderFillMode:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setrenderfillmode) |Sets the fill mode of the player screen. |
|[setPlayUrl:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setplayurl) |Sets a pull stream address. |
|[getVersion](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-getversion) |Gets the version number of the Player SDK. |
|[setPlayStreamData:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setplaystreamdata) |Sets multiple live streams. Call this method if you need to enable features requiring multiple live streams, such as adaptive bitrate (ABR), manual resolution switching, and primary and backup streams. |
|[setLogLevel:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setloglevel) |Sets the level of the output log. |
|[play](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-play) |Starts or resumes playback. |
|[stop](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-stop) |Stops playback. This method does not destroy the player. |
|[switchResolution:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-switchresolution) |Changes the video resolution. |
|[setMute:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setmute) |Sets whether to mute playback. |
|[isMute](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-ismute) |Checks whether playback is muted. |
|[destroy](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-destroy) |Stops playback and destroys the player. |
|[snapshot](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-snapshot) |Takes a screenshot of the video. |
|[enableVideoFrameObserver:pixelFormat:bufferType:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enablevideoframeobserver-pixelformat-buffertype) |Sets the video frame observer. |
|[enableAudioFrameObserver:enableRendering:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enableaudioframeobserver-enablerendering) |Sets the audio frame observer. |
|[setEnableSuperResolution:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setenablesuperresolution) |Enables or disables super resolution. |
|[setUrlHostIP:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-seturlhostip) |Sets the mapping of domain names to server IP addresses. |
|[setRenderRotation:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setrenderrotation) |Sets the clockwise rotation angle of the video. |
|[setRenderMirror:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setrendermirror) |Configures mirroring settings. |
|[setProperty:value:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setproperty-value) |Configures advanced settings for the player, including offscreen rendering, maximum buffer duration, and adaptive bitrate (ABR) algorithms. |
|[isPictureInPictureSupported](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-ispictureinpicturesupported) |Whether PiP is supported on the current device. |
|[isPictureInPictureStarted](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-ispictureinpicturestarted) |Whether PiP has started successfully. |
|[startPictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-startpictureinpicture) |Manually start PiP. |
|[stopPictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-stoppictureinpicture) |Manually stop PiP and close the PiP window. |
|[invalidatePictureInPicturePlaybackState](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-invalidatepictureinpictureplaybackstate) |Manually update the play/pause button state and progress display in the PiP window. |


<span id="callbacks"></span>
# Callbacks


|Method |Description |
|---|---|
|[onError:error:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onerror-error) |Occurs when a player error occurs. |
|[onAudioRenderStall:stallTime:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onaudiorenderstall-stalltime) |Occurs when audio rendering stutters. |
|[onVideoRenderStall:stallTime:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onvideorenderstall-stalltime) |Occurs when video rendering stutters. |
|[onFirstAudioFrameRender:isFirstFrame:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onfirstaudioframerender-isfirstframe) |Occurs when the first audio frame is rendered at the beginning of playback or after a retry during playback. |
|[onInfo:info:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-oninfo-info) |Triggered when the player encounters an internal error. |
|[onResolutionSwitch:resolution:error:reason:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onresolutionswitch-resolution-error-reason) |Occurs when the video resolution changes. |
|[onVideoSizeChanged:width:height:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onvideosizechanged-width-height) |Occurs when the video size changes. |
|[onReceiveBinarySeiMessage:message:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onreceivebinaryseimessage-message) |Binary SEI message callback. This callback is triggered when the player SDK receives an SEI message. It is necessary to enable the `enableBinarySei` property in `VeLivePlayerConfiguration`. When the `enableBinarySei` property is enabled, the string SEI message will no longer be sent. |
|[onMainBackupSwitch:streamType:error:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onmainbackupswitch-streamtype-error) |Occurs when the player switches between the primary stream and the backup stream. |
|[onPlayerStatusUpdate:status:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status) |Occurs when the playback status changes. |
|[onPlayerStatusUpdate:status:extraInfo:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status-extrainfo) |Occurs when the playback status changes. Compared with [onPlayerStatusUpdate:status:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status), this callback returns supplemental information about the current playback stream through `extraInfo`. |
|[onStatistics:statistics:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstatistics-statistics) |Occurs periodically to report information such as the current pull stream address, bitrate, and frame rate. |
|[onSnapshotComplete:image:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onsnapshotcomplete-image) |Occurs when a screenshot is taken after snapshot is called. |
|[onRenderVideoFrame:videoFrame:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onrendervideoframe-videoframe) |Occurs when the player decodes a video frame. Call [enableVideoFrameObserver:pixelFormat:bufferType:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enablevideoframeobserver-pixelformat-buffertype) to enable video frame callback. |
|[onRenderAudioFrame:audioFrame:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onrenderaudioframe-audioframe) |Occurs when the player decodes an audio frame. Call [enableAudioFrameObserver:enableRendering:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enableaudioframeobserver-enablerendering) to enable audio frame callback. |
|[onStreamFailedOpenSuperResolution:error:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution-error) |Occurs when the SDK fails to enable super resolution after [setEnableSuperResolution:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setenablesuperresolution) is called. |
|[getDrmResourceLoaderCertificateData:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-getdrmresourceloadercertificatedata) |You need to return the FairPlay certificate in NSData format in this callback. |
|[getDrmResourceLoaderLicenseUrl:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-getdrmresourceloaderlicenseurl) |You need to return the URL of the DRM license in this callback. |
|[onReceiveSeiMessage:message:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onreceiveseimessage-message) |String SEI message callback. This callback is triggered when the player SDK receives an SEI message. It is necessary to enable the `enableSei` property in `VeLivePlayerConfiguration`. When the `enableBinarySei` property is enabled, the string SEI message will no longer be sent. |
|[onStallStart:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstallstart) |Occurs when a playback stutter starts. |
|[onStallEnd:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstallend) |Occurs when a playback stutter stops, that is, when playback resumes after there is enough audio buffer. |
|[onFirstVideoFrameRender:isFirstFrame:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onfirstvideoframerender-isfirstframe) |Occurs when the first video frame is rendered at the beginning of playback or after a retry during playback. |
|[onStreamFormatSwitch:fromStreamFormat:toStreamFormat:error:extraInfo:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstreamformatswitch-fromstreamformat-tostreamformat-error-extrainfo) |Triggered when the player switches the stream format. |
