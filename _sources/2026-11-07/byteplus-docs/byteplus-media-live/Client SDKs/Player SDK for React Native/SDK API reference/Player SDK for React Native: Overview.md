---
title: "Player SDK for React Native: Overview"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-overview"
---

<span id="methods"></span>
## Methods


|Method |Description |
|---|---|
|[setConfig](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-api#veliveplayer-setconfig) |Initializes the player and configures whether to turn on SEI messaging, hardware decoding, local DNS prefetch, and other configurations. |
|[setObserver](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-api#veliveplayer-setobserver) |Sets the player observer to listen to the live player's events, such as playback errors or status updates, rendering of the first audio and video frame, and resolution switching. |
|[setRenderFillMode](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-api#veliveplayer-setrenderfillmode) |Sets the fill mode of the player screen. |
|[setPlayerVolume](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-api#veliveplayer-setplayervolume) |Sets the player volume. |
|[isPlaying](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-api#veliveplayer-isplaying) |Checks whether the player is playing. |
|[switchResolution](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-api#veliveplayer-switchresolution) |Changes the video resolution. |
|[destroy](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-api#veliveplayer-destroy) |Stops playback and destroys the player. |
|[stop](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-api#veliveplayer-stop) |Stops playback. This method does not destroy the player. |
|[pause](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-api#veliveplayer-pause) |Pauses playback. |
|[play](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-api#veliveplayer-play) |Starts or resumes playback. |
|[setPlayStreamData](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-api#veliveplayer-setplaystreamdata) |Sets multiple live streams. Call this method if you need to enable features requiring multiple live streams, such as adaptive bitrate (ABR), manual resolution switching, and primary and backup streams. |
|[setPlayUrl](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-api#veliveplayer-setplayurl) |Sets a pull stream address. |
|[setMute](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-api#veliveplayer-setmute) |Sets whether to mute playback. |
|[isMute](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-api#veliveplayer-ismute) |Checks whether playback is muted. |
|[setProperty](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-api#veliveplayer-setproperty) |Configures advanced settings for the player, including offscreen rendering, maximum buffer duration, and adaptive bitrate (ABR) algorithms. Contact BytePlus technical support if you need further information. |
|[setRenderRotation](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-api#veliveplayer-setrenderrotation) |Sets the clockwise rotation angle of the video. |
|[setRenderMirror](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-api#veliveplayer-setrendermirror) |Configures mirroring settings. |
|[setEnableSuperResolution](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-api#veliveplayer-setenablesuperresolution) |Enables or disables super resolution. You must first contact the BytePlus [technical support](https://www.byteplus.com/en/support) to activate the feature before using it. |
|[startPictureInPicture()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#3bbd9dbc) |Starts picture\-in\-picture (PiP) mode and displays the player in a floating window. |
|[stopPictureInPicture()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#fb3447d5) |Exits picture\-in\-picture (PiP) mode. |
|[isPictureInPictureSupported()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#4b3e1343) |Checks whether the current environment supports picture\-in\-picture (PiP) mode. |
|[setPictureInPictureListener()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#9727b950) |Sets the listener for PiP\-related events, such as PiP started, stopped, or errors. |
|[enablePictureInPicture()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#a1f76572) |(iOS only) Enables automatic PiP mode when the app goes into the background. |
|[disablePictureInPicture()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#1b8b5910) |(iOS only) Disables automatic PiP mode. |


<span id="callbacks"></span>
## Callbacks


|Method |Description |
|---|---|
|[onError](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-callback#veliveplayerobserver-onerror) |Occurs when a player error occurs. |
|[onFirstVideoFrameRender](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-callback#veliveplayerobserver-onfirstvideoframerender) |Occurs when the first video frame is rendered at the beginning of playback or after a retry during playback. |
|[onFirstAudioFrameRender](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-callback#veliveplayerobserver-onfirstaudioframerender) |Occurs when the first audio frame is rendered at the beginning of playback or after a retry during playback. |
|[onStallStart](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-callback#veliveplayerobserver-onstallstart) |Occurs when a playback stutter starts. |
|[onStallEnd](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-callback#veliveplayerobserver-onstallend) |Occurs when a playback stutter stops, that is, when playback resumes after there is enough audio buffer. |
|[onVideoRenderStall](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-callback#veliveplayerobserver-onvideorenderstall) |Occurs when video rendering stutters. |
|[onAudioRenderStall](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-callback#veliveplayerobserver-onaudiorenderstall) |Occurs when audio rendering stutters. |
|[onResolutionSwitch](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-callback#veliveplayerobserver-onresolutionswitch) |Occurs when the video resolution changes. |
|[onVideoSizeChanged](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-callback#veliveplayerobserver-onvideosizechanged) |Occurs when the video size changes. |
|[onReceiveSeiMessage](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-callback#veliveplayerobserver-onreceiveseimessage) |Occurs when the Player SDK receives an SEI message. |
|[onMainBackupSwitch](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-callback#veliveplayerobserver-onmainbackupswitch) |Occurs when the player switches between the primary stream and the backup stream. |
|[onPlayerStatusUpdate](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-callback#veliveplayerobserver-onplayerstatusupdate) |Occurs when the playback status changes. |
|[onStatistics](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-callback#veliveplayerobserver-onstatistics) |Occurs periodically to report information such as the current pull stream address, bitrate, and frame rate. |
|[onSnapshotComplete](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-callback#veliveplayerobserver-onsnapshotcomplete) |Occurs when a screenshot is taken after snapshot is called. |
|[onRenderVideoFrame](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-callback#veliveplayerobserver-onrendervideoframe) |Occurs when the player decodes a video frame. Call [enableVideoFrameObserver](https://docs.byteplus.com/en/docs/24/player-android-api-reference#veliveplayer-enablevideoframeobserver) to enable video frame callback. |
|[onRenderAudioFrame](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-callback#veliveplayerobserver-onrenderaudioframe) |Occurs when the player decodes an audio frame. Call enableAudioFrameObserver to enable audio frame callback. |
|[onStreamFailedOpenSuperResolution](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-rn-callback#veliveplayerobserver-onstreamfailedopensuperresolution) |Occurs when the SDK fails to enable super resolution after setEnableSuperResolution is called. |
|[onStartPictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#5c6ba1f3) |Occurs when picture\-in\-picture mode is started. You can use this callback to update UI status or add analytics tracking. |
|[onStopPictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#b33d5937) |Occurs when picture\-in\-picture mode is exited, either by user action or programmatically. |
|[onClickPictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#a2f98e10) |Occurs when the picture\-in\-picture window is clicked. Use this callback to respond to user interaction with the PiP window. |
|[onError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#a9a4d317) |Occurs when an error related to picture\-in\-picture mode occurs. Use this callback for error reporting or fallback handling. |
