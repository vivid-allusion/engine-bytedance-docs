---
title: "Web SDK"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-115174"
---

<span id="_4-69-1"></span>
## 4.69.1

Release date: August 31, 2026.

<span id="new-features-4-69-1"></span>
### New features

**Added AEC and AGC audio preprocessing extensions for Web**


* Added the `@byteplus/rtc/extension-aec` acoustic echo cancellation extension for preprocessing locally captured audio. By default, the extension processes internally captured audio in the main stream and takes effect only when a remote reference audio stream is available.

* Added the `@byteplus/rtc/extension-agc` automatic gain control extension. It automatically adjusts the capture gain to improve volume stability. By default, the extension processes internally captured audio in the main stream.

* When the AEC, AINR, and AGC extensions are enabled together, the recommended processing order is `AEC -> AINR -> AGC`. Web SDK 4.69.1 or later guarantees this order. Earlier versions do not.

* Register the AEC and AGC extensions before starting audio capture. For subsequent capture, the SDK sets `echoCancellation` to `false` when AEC is registered and sets `autoGainControl` to `false` when AGC is registered. If an extension is registered after capture starts, the corresponding constraint cannot be changed for the active capture pipeline, and the SDK reports a console warning and telemetry event. This behavior is not guaranteed if the extensions are used with an earlier SDK version.


<span id="393f14f4"></span>
## 4.68.5

Release date: June 11, 2026.

Fixed some known bugs.

<span id="_4-68-1"></span>
## 4.68.1

Release date: January 20, 2026.

<span id="new-features"></span>
### New features

Supports Alpha channel video rendering (only supported when the sender is on Linux).

<span id="_4-68-0"></span>
## 4.68.0

Release date: December 5, 2025.

<span id="new-features"></span>
### New Features


* The Web SDK now supports use in an Electron environment.

* The Web SDK now supports the 360 Extreme Browser in the macOS environment.


<span id="_4-67-2"></span>
## 4.67.2

Release date: August 6, 2025

<span id="new-features"></span>
### New Features

[AI noise-canceling extension](https://docs.byteplus.com/en/docs/12/docs-148647) now supports Firefox 80+ and Safari 14.1+.

<span id="_4-67-1"></span>
## 4.67.1

<span id="new-features"></span>
### New Features


1. **Added support for getting the visibility state of local, remote, or WTN video players**

   
   |API |Description |
   |---|---|
   |[getLocalVideoPlayerVisibility](https://docs.byteplus.com/en/docs/12/docs-104478#getlocalvideoplayervisibility) |Gets the visibility state of the local video player and the reasons for its invisibility. |
   |[getRemotePlayerVisibility](https://docs.byteplus.com/en/docs/12/docs-104478#getremoteplayervisibility) |Gets the visibility state of remote video player and reasons for invisibility. |
   |[getWTNVideoPlayerVisibility](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-getwtnvideoplayervisibility) |Gets the visibility status of the specified WTN stream's video player. |
   |[onPlayerVisibility](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onplayervisibility) |A callback that is triggered every 30 seconds to report changes in the player's visibility status. |
   

2. **Added media stream exception event callbacks**

   
   |API |Description |
   |---|---|
   |[onRemoteStatsException](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onremotestatsexception) |SDK detects an abnormal event, which is usually caused by external factors such as network or capture/playback devices. The abnormal event is not an error, but it usually degrades call quality. If the problem is resolved, you will also receive this callback. |
   |[onLocalStatsException](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onlocalstatsexception) |SDK detects an abnormal event, which is usually caused by external factors such as network or capture/playback devices. The abnormal event is not an error, but it usually degrades call quality. If the problem is resolved, you will also receive this callback. |
   |[onWTNLocalStatsException](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnlocalstatsexception) |Exception event callback of local WTN media stream. |
   |[onWTNRemoteStatsException](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnremotestatsexception) |Exception event callback of remote WTN media stream. |
   

3. **Added support for publishing videos in ByteVC1 format**

   When setting the publishing parameters for a video stream via [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-104478#setvideoencoderconfig), you can now specify the video encoding format as H.264, VP8, or ByteVC1.


<span id="web-sdk-4-66-0"></span>
## Web SDK 4.66.0

Release date: March 11, 2025

<span id="new"></span>
### New


1. Support for creating RTS\-only rooms

   When creating a room via [joinRoom](https://docs.byteplus.com/en/docs/12/docs-104478#joinroom), you can set the room creation mode using the newly added field `roomMode?: RoomMode` in [RoomConfig](https://docs.byteplus.com/en/docs/12/docs-104481#roomconfig):

* `ROOM_MODE_RTC = 0` (default): Both RTC and RTS features are available in the room.

* `ROOM_MODE_RTS_ONLY = 1`: Only RTS features are available in the room. Only RTS\-related interfaces can be used, while RTC\-related features (such as publishStream, subscribeStream, etc.) are not available.

2. **Get the Call ID of a room**

   New method [getCallId](https://docs.byteplus.com/en/docs/12/docs-104478#getcallid): After joining a room, you can call this method to get the room's call ID, which uniquely identifies the call session.

3. **SEI function supports Firefox 117+ and Safari 15.4+** 

   When sending SEI data via [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-104478#sendseimessage), in addition to Chromium 86+, it now also supports Firefox 117+ and Safari 15.4+.


<span id="web-sdk-4-65-0"></span>
## Web SDK 4.65.0

Release date: December 23, 2024

<span id="new"></span>
### New


1. **New options on the AI noise\-canceling extension**

   * Before using the AI noise\-canceling extension, check if the current browser supports the feature via `isSupported`.

   * The AI noise\-cancelling level can be adjusted by `setAnsMode(ansMode: AnsMode)`.

   * The target stream can be specified by `streamIndex` and `sourceType` when calling `enable` to enable AI noise\-cancelling. The default stream is the microphone audio stream captured by the SDK.

2. **Multiple cloud proxy server addresses**

   When calling [startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-104478#startcloudproxy), you can pass an array of server addresses to use multiple cloud proxies.

3. **Publish and subscribe media streams without joining a room (WTN streams)** 

   We recommend using this API if the user does not need to interact with audio and video in the RTC room. Compared to the existing method `startPushPublicStream`, the `startPushWtn` does not require the publishing user to join the room. If the user does not need to interact with the audio&video in the RTC room, it is recommended to use this interface.

   
   |API |Notes |
   |---|---|
   |[getWTNStreamManager](https://docs.byteplus.com/en/docs/12/docs-104478#getwtnstreammanager) |Creates a WTN stream manager object. |
   |[startPushWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startpushwtn) |Starts publishing a WTN stream without joining a room. |
   |[stopPushWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-stoppushwtn) |Stops publishing the WTN stream which was published via [startPushWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startpushwtn). |
   |[muteWTNLocalVideo](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-mutewtnlocalvideo) |Pauses/Resumes to publish the video of a WTN stream. |
   |[muteWTNLocalAudio](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-mutewtnlocalaudio) |Pauses/Resumes to publish the audio of a WTN stream. |
   |[onWTNPushStateChanged](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnpushstatechanged) |Callback of the result of publishing the WTN stream.<br><br>After calling [startPushWTN] |
   |[sendWTNSEIMessage](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-sendwtnseimessage) |Sends SEI via a WTN stream. |
   |[onWTNSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnseimessagereceived) |Callback of the SEI carried by the public video stream.<br><br>You will receive SEI by this callback if the WTN stream you subscribed to by calling [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn) is carrying SEI. |
   

   The subscriber can get stream status and media statistics from the following new callbacks. You can receive the statistics callbacks every 2 seconds after subscribing to the audio of a WTN stream via [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn).

   
   |API |Notes |
   |---|---|
   |[onWTNPlayStateChanged](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnplaystatechanged) |Callback of the result of subscribing to the WTN stream. |
   |[onWTNRemoteAudioStateChanged](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnremoteaudiostatechanged) |Callback for the subscription state of the WTN audio stream. |
   |[onWTNRemoteVideoStateChanged](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnremotevideostatechanged) |Callback for the subscription state of the WTN video stream. |
   |[onWTNRemoteVideoStats](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnremotevideostats) |Callback carrying the video statistics of the WTN stream. |
   |[onWTNRemoteAudioStats](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnremoteaudiostats) |Callback carrying the audio statistics of the WTN stream. |
   

   Methods of subscribing to WTN streams have been changed. See the following **Incompatible changes** section for details.


<span id="breaking-changes"></span>
### Breaking changes

If you have used WTN streams (referred to as public stream in previous versions) in your project, replace the following methods and callbacks with the new ones.

Starting from this version, to access methods and callbacks associated with WTN stream subscriptions, you need to obtain an IWTNStream instance via [getWTNStreamManager](https://docs.byteplus.com/en/docs/12/docs-104478#getwtnstreammanager).


|Before |After |Details |
|---|---|---|
|`startPlayPublicStream` |[startPlayWTN: (token: string \| null, streamId: string, videoMute: boolean, audioMute: boolean) => Promise;](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn) |Subscribes to a WTN stream. Note that the new method requires three more parameters: `token`, `videoMute`, and `audioMute`. |
|`stopPlayPublicStream` |[stopPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-stopplaywtn) |Unsubscribes from a designated WTN stream. |
|`setPublicStreamVideoPlayer` |[setWTNRemoteVideoPlayer](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-setwtnremotevideoplayer) |Sets the player information and rendering mode for the WTN stream. |
|`setPublicStreamVolume` |[setWTNRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-setwtnremoteaudioplaybackvolume) |Adjusts audio playback volume of a WTN stream. |
|`onPublicStreamStats` |[onWTNRemoteVideoStats](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnremotevideostats), [onWTNRemoteAudioStats](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnremoteaudiostats) |Callback carrying the video statistics of the WTN stream. |
|`onFirstPublicStreamAudioFrameDecoded` |None |Callback of the successful decoding of the first audio frame of the WTN stream. You can monitor the state of a WTN stream by [onWTNRemoteAudioStateChanged](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnremoteaudiostatechanged). |
|`onFirstPublicStreamVideoFrameDecoded` |[onWTNFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnfirstremotevideoframedecoded) |Callback of the successful decoding of the first video frame of the WTN stream. |
|`onFirstPublicStreamVideoFrameRendered` |None |Callback for the successful rendering of the first video frame of the WTN stream. |


<span id="web-sdk-4-63-2"></span>
## Web SDK 4.63.2

Release date: December 19, 2024

Fixed a couple of known issues related to the beauty effect extension.

<span id="web-sdk-4-63-0"></span>
## Web SDK 4.63.0

Release date: October 24, 2024

<span id="new"></span>
### New


1. **In\-ear monitors (IEMs)** 

   In music interaction scenarios, such as online karaoke and chorus singing, the performers may need to listen to the monitor audio. Since V4.63, you can now enable the in\-ear monitors via `setEarMonitorMode`. You can adjust the volume of the in\-ear monitor via`setEarMonitorVolume`.

2. **Screen sharing**

   Starting from V4.63, the Web SDK also supports screen sharing when used in Electron. You can obtain screen sharing sources, including the sourceId, name, and thumbnail of screens and application windows, by `getElectronScreenSources`. Then, when you invoke `startScreenCapture`, you can pass in the `sourceId` to specify the screen sharing source. However, if you don't specify the `sourceId` in the call of `startScreenCapture`, the SDK will prompt the user to select the screen sharing source.

3. **Video streaming statistics**

   You can detect the codec type of the remote video stream by the codecType parameter in the `RemoteStreamStats.RemoteVideoStats.codecType` object, which is obtained through `onRemoteStreamStats`.

4. **Messages**

   We optimized the experience of the [message interface](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104477#message). When the sending frequency exceeds the limit, messages will be automatically discarded, and an error code `USER_MESSAGE_EXCEED_QPS` will be returned.


<span id="enhanced"></span>
### Enhanced

Web SDK has been tested and works as expected on Huawei's browsers that run on the HarmonyOS Next. For details on support and known issues, refer to [Supported Browsers of WebRTC SDK](https://docs.byteplus.com/en/docs/12/docs-111854).

<span id="breaking-changes"></span>
### Breaking changes

The rules for video stream fallback on the sender side have changed. The video streaming will now fall back to each provided encoding parameter in descending order, rather than falling back to the predefined resolution streams set by the SDK. For example, this applies if the sender has set up 1080P (high), 360P (medium), and 180P (low).


* In the previous versions, the downgrade path was 1080P (high) \-\> 720P (high) \-\> 630P (high) \-\> 540P (high) \-\> 450P (high) \-\> 360P (medium) \-\> 270P (medium) \-\> 180P (low) \-\> 144P (low).

* In the current version, the downgrade path is 1080P (high) \-\> 360P (medium) \-\> 180P (low).


Additionally, changes to the methods for publishing and subscribing to Simulcast streams are shown in the table below.

> The old interfaces have been deprecated in this version. Although you can still use them, we will no longer maintain them. We recommend that you migrate to the new interfaces as soon as possible.



|Change |Before |After |Description |
|---|---|---|---|
|API replacement |`enableSimulcastMode`<br><br>enables the Simulcast feature that the SDK will send the video stream in every resolution you provide. |[setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-104478#setlocalsimulcastmode)<br><br>with the `mode` set to `VIDEO_ALWAYS_SIMULCAST`=`2`, enables the Simulcast feature that the SDK will send the video stream in every resolution you provide. |A new Simulcast mode has been added that allows the sender to send a stream only at the quality required by subscribers. |
|Behavior changes |`setVideoEncoderConfig` |[setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-104478#setlocalsimulcastmode) |You can specify or update the encoding parameters for each Simulcast stream via `setLocalSimulcastMode` instead of `setVideoEncoderConfig`, which is now for the high\-quality stream only. |
|API replacement |`setRemoteVideoConfig` |[setRemoteSimulcastStreamType](https://docs.byteplus.com/en/docs/12/docs-104478#setremotesimulcaststreamtype) |You can set the subscription preference to the Simulcast stream via [setRemoteSimulcastStreamType](https://docs.byteplus.com/en/docs/12/docs-104478#setremotesimulcaststreamtype) instead of `setRemoteVideoConfig`. By simply passing an enum value, you no longer need to specify values for resolution, frame rate, or bitrate. |


<span id="web-sdk-4-62-1"></span>
## Web SDK 4.62.1

Release date: September 14, 2024

Fixed a couple of known issues.

<span id="web-sdk-4-62-0"></span>
## Web SDK 4.62.0

Release date: August 28, 2024

<span id="new"></span>
### New


1. Starting from v4.62, in addition to [onLocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onlocalstreamstats) and [onRemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onremotestreamstats), you can get statistics for remote streams by calling the following methods.

   * `getRemoteVideoStats`

   * `getRemoteAudioStats`

   * `getLocalVideoStats`

   * `getLocalAudioStats`

2. To add more audio features to your application, such as audio recording, audio audit, and so on, you may need to get the audio raw data. Since V4.62, you can enable the audio frame callback and designate the callback function to receive the PCM audio data using [IRTCEngine.setAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-104478#setaudioframecallback) to obtain both local and remote audio frames. For the raw data of mixed\-audio, use [IAudioMixingManager.setAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-104478#audiomixingmanager-setaudioframecallback).

3. You can now mirror the remote video stream by calling [setRemoteVideoMirrorType](https://docs.byteplus.com/en/docs/12/docs-104478#setremotevideomirrortype). Upon successful setup, the specified mode will take effect in the player that has been or will be added, meaning that the mirror effect can be set either before or after calling [setRemoteVideoPlayer](https://docs.byteplus.com/en/docs/12/docs-104478#setremotevideoplayer).


<span id="web-sdk-4-61-3"></span>
## Web SDK 4.61.3

Release date: August 19, 2024

We have resolved three known issues, one of which involved subscription failures during network downtime.

<span id="web-sdk-4-61-1"></span>
## Web SDK 4.61.1

Release date: July 15, 2024

With the imminent release of Google Chrome 128, scheduled for mid\-August, a significant breaking change is anticipated that may disrupt the publishing and subscribing processes of media streams, affecting the functionality of the RTC Web SDK. To ensure the stability of your application, we strongly recommend upgrading to this version or a newer version of the RTC Web SDK.

<span id="web-sdk-4-61-0"></span>
## Web SDK 4.61.0

Release date: June 28, 2024

<span id="breaking-changes"></span>
### Breaking changes

Since V4.61.0, the mirror setting of the video stream will not be reflected in the snapshot captured using [takeLocalSnapshot](https://docs.byteplus.com/en/docs/12/docs-104478#takelocalsnapshot) or `takeRemoteSnapshot`.

<span id="new"></span>
### New


1. You can now pause a media stream without cancelling the subscription to a stream. This is useful when you want to resume the media stream shortly after the pause. Refer to [stop](https://docs.byteplus.com/en/docs/12/docs-104478#stop).

2. In addition to [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104479#onlocalaudiopropertiesreport) or [onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onremoteaudiopropertiesreport), you can now get the audio volume of the remote user by calling [getAudioVolume](https://docs.byteplus.com/en/docs/12/docs-104478#getaudiovolume) since V4.61.

3. You can now assign a media stream to multiple players at the same time. This is useful in the online meetings, where the video is rendered in both the main screen and the sidebar.

   * [setLocalVideoPlayer](https://docs.byteplus.com/en/docs/12/docs-104478#setlocalvideoplayer)

   * [setRemoteVideoPlayer](https://docs.byteplus.com/en/docs/12/docs-104478#setremotevideoplayer)

   * [setPublicStreamVideoPlayer](https://docs.byteplus.com/en/docs/12/docs-104478#setpublicstreamvideoplayer)

4. To accommodate changes to the screen\-sharing feature in Chrome 107 and Edge 107, new properties `displaySurface`, `selfBrowserSurface`, `surfaceSwitching`, and `systemAudio` were added to the [ScreenConfig](https://docs.byteplus.com/en/docs/12/docs-104481#screenconfig), which is a key type for [startScreenCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startscreencapture). Refer to [Chrome documentation](https://developer.chrome.com/docs/web-platform/screen-sharing-controls/).

5. You can use the new parameter `publishState` of [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserjoined), which indicates the audio and video publishing state of the remote user, to show the corresponding UI components. For example, load the mute/unmute icon depending on the audio publish state when the local user enters the room or the remote user enters the room.


<span id="web-sdk-4-60-2"></span>
## Web SDK 4.60.2

Release date: January 17, 2024

<span id="breaking-changes"></span>
### Breaking changes


* Browser compatibility changed for both the [Beauty Effects Extension](https://docs.byteplus.com/en/docs/12/docs-148646) and [Virtual Background](https://docs.byteplus.com/en/docs/12/docs-697417).

* When creating an instance of the [Beauty Effects Extension](https://docs.byteplus.com/en/docs/12/docs-148646), the authentication file is required.

* Some literal values in the enumeration types have been modified for the [Virtual Background](https://docs.byteplus.com/en/docs/12/docs-697417).


<span id="new"></span>
### New

New options for setting the [Virtual Background](https://docs.byteplus.com/en/docs/12/docs-697417), including choosing a video or a solid color.

You can now customize the level of blurriness for the background with `setBackgroundBlurRadius` when using the blur background.

<span id="web-sdk-4-60"></span>
## Web SDK 4.60

Release date: January 4, 2024

<span id="new"></span>
### New


1. Added callbacks triggered when the publishing or subscription permission of your token is about to expire and has expired. After receiving the callback, you should update the corresponding token.



|API |Description |
|---|---|
|[onTokenPublishPrivilegeWillExpire](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-ontokenpublishprivilegewillexpire) |This callback will be triggered 30 seconds before the token publishing permission expires. |
|[onTokenPublishPrivilegeDidExpired](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-ontokenpublishprivilegedidexpired) |This callback will be triggered when the token publishing permission expires. |
|[onTokenSubscribePrivilegeWillExpire](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-ontokensubscribeprivilegewillexpire) |This callback will be triggered 30 seconds before the token subscription permission expires. |
|[onTokenSubscribePrivilegeDidExpired](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-ontokensubscribeprivilegedidexpired) |This callback will be triggered when the token subscription permission expires. |



2. Supports sending supplemental enhancement information (SEI) in voice call scenarios. After calling the [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-104478#sendseimessage) interface, the SDK internally generates a black frame video for sending SEI, and notifies the publishing status of the black frame video stream to remote users through the [onSEIStreamUpdate](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onseistreamupdate) event.


<span id="enhanced"></span>
### Enhanced


1. Enhances the functionality of Audio Selection. It now allows you to adjust settings so that the local audio stream may opt\-out of Audio Selection. This feature is highly useful in situations where the voice of specific users, such as a host during an online meeting, should always be audible. Refer to [setAudioSelectionConfig](https://docs.byteplus.com/en/docs/12/docs-104478#setaudioselectionconfig) for more information.


<span id="web-sdk-4-58"></span>
## Web SDK 4.58

Release date: November 8, 2023

This update improves the accuracy of data reporting and provides bug fixes to some known issues.

<span id="web-sdk-4-56"></span>
## Web SDK 4.56

Release date: September 7, 2023

<span id="new"></span>
### New


1. Support simultaneous activation of audio and video capture functions. When calling this method, the browser will request microphone and camera permissions simultaneously, and the user only needs to grant permission once. See [StartAudioAndVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startaudioandvideocapture).

2. Support configuring the callback mode and data range (controlling whether the callback includes mixed audio) for local main stream audio. The new feature affects the callback [onActiveSpeaker](https://docs.byteplus.com/en/docs/12/docs-104479#onactivespeaker). Please refer to the newly added parameters [LocalMainReportMode](https://docs.byteplus.com/en/docs/12/docs-104481#localmainreportmode) and [AudioReportMode](https://docs.byteplus.com/en/docs/12/docs-104481#audioreportmode) in the [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104478#enableaudiopropertiesreport) interface.

3. The [onError](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onerror) callback provides more detailed error codes for events such as room dissolution, being kicked out of a room, and being banned. If a room or user is banned, attempting to join the room with the [joinRoom](https://docs.byteplus.com/en/docs/12/docs-104478#joinroom) method returns ErrorCode.ROOM_FORBIDDEN or ErrorCode.USER_FORBIDDEN.

4. Support setting [VideoEncoderConfig.contentHint](https://docs.byteplus.com/en/docs/12/docs-104481#videoencoderconfig-contenthint) for the main stream.

5. When rendering remote video streams, you can set the rotation angle of the video using [setRemoteVideoPlayer.videoPlayerOption](https://docs.byteplus.com/en/docs/12/docs-104478#setremotevideoplayer).


<span id="web-sdk-4-55"></span>
## Web SDK 4.55

Release date: August 11, 2023

<span id="new"></span>
### New


1. Added a new enumerator value `DOWN = 6` for [NetworkQuality](https://docs.byteplus.com/en/docs/12/docs-104481#networkquality). You can now detect network disconnections through [onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onnetworkquality).

2. [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startaudiocapture) now returns the current audio capture parameters through [MediaTrackSettings](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackSettings).


<span id="web-sdk-4-54"></span>
## Web SDK 4.54

Release date: July 13, 2023

<span id="new"></span>
### New


1. Supports forwarding media streams across rooms. Cross\-room media stream forwarding refers to simultaneously forwarding visible users' media streams to multiple rooms. The audience can receive media streams from hosts in other rooms. For interfaces and sample code, refer to [Forward media streams across rooms](https://docs.byteplus.com/en/docs/12/docs-104398).


<span id="web-sdk-4-53"></span>
## Web SDK 4.53

Release date: June 15, 2023

<span id="new"></span>
### New


1. Added totalRtt to [RemoteAudioStats](https://docs.byteplus.com/en/docs/12/docs-104481#remoteaudiostats) and [RemoteVideoStats](https://docs.byteplus.com/en/docs/12/docs-104481#remotevideostats). You can get the round\-trip transmission time delay through [onRemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-104479#onremotestreamstats).

2. Added RENDER_MODE_FILL to [VideoRenderMode](https://docs.byteplus.com/en/docs/12/docs-104481#videorendermode) for internal video rendering. The video frame will be non\-uniformly scaled until it fills the window.

3. Added GPU mode to the virtual background extension. See [Virtual Background](https://docs.byteplus.com/en/docs/12/docs-697417).


<span id="web-sdk-4-52"></span>
## Web SDK 4.52

Release date: May 18, 2023

<span id="new"></span>
### New


1. Support adjusting audio capture and playback volume.



|API |Description |
|---|---|
|[setCaptureVolume](https://docs.byteplus.com/en/docs/12/docs-104478#setcapturevolume) |Adjust audio capture volume. |
|[setPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-104478#setplaybackvolume) |Adjust audio playback volume of a specified remote user. |
|[setPublicStreamVolume](https://docs.byteplus.com/en/docs/12/docs-104478#setpublicstreamvolume) |Adjust audio playback volume of a public stream. |



2. Added the Virtual Background Extension, which allows you to separate the user portrait from the background and use custom images or a blurred background. This feature is provided at an additional charge. See [Virtual Background](https://docs.byteplus.com/en/docs/12/docs-697417).


<span id="web-sdk-4-51"></span>
## Web SDK 4.51

Release date: April 13, 2023

<span id="new"></span>
### New


1. Support for synchronous rendering of remote audio and video streams. See [setRemoteStreamRenderSync](https://docs.byteplus.com/en/docs/12/docs-104478#setremotestreamrendersync).


<span id="web-sdk-4-49"></span>
## Web SDK 4.49

Release date: February 23, 2023

<span id="new"></span>
### New


1. Supports setting the logging level of local cache, and the maximum cache space that can be used. See [setLogConfig](https://docs.byteplus.com/en/docs/12/docs-104478#setlogconfig) and [downloadLog](https://docs.byteplus.com/en/docs/12/docs-104478#downloadlog).


<span id="enhanced"></span>
### Enhanced


1. Simplified the process of pushing media streams to a CDN. Unified the configuration limits, restrictions, and default values of RTC SDK and OpenAPI, and the configurations will be verified by RTC SDK. Some illegal parameters will be automatically corrected to default values. See [LiveTranscodeConfig](https://docs.byteplus.com/en/docs/12/docs-104481#livetranscodeconfig).


<span id="web-sdk-4-47"></span>
## Web SDK 4.47

Release date: December 30, 2022

<span id="new"></span>
### New


1. Supports taking screenshots of local/remote video streams on the client side. See [takeLocalSnapshot](https://docs.byteplus.com/en/docs/12/docs-104478#takelocalsnapshot) and [takeRemoteSnapshot](https://docs.byteplus.com/en/docs/12/docs-104478#takeremotesnapshot).

2. Support for controlling media and getting media information from [MediaStreamTrack](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack), which is one of the Web APIs.

3. Adds Beauty Effects Extension, by which you can apply brightening, skin\-smoothing, and sharpening effects to your video stream. See [Beauty Effects Extension](https://docs.byteplus.com/en/docs/12/docs-148646).

4. Adds AI Noise\-Canceling Extension, by which you can reduce the noise in different scenarios. See [AI Noise-Cancelling Extension](https://docs.byteplus.com/en/docs/12/docs-148647).


<span id="web-sdk-4-46"></span>
## Web SDK 4.46

Release date: September 21, 2022

<span id="new"></span>
### New


1. After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104478#enableaudiopropertiesreport), you will periodically receive the callback of [onActiveSpeaker](https://docs.byteplus.com/en/docs/12/docs-104479#onactivespeaker) for active speaker information.

2. When the audio stream/video stream of a specified user is banned/unbanned, all users in the room will receive the [onAudioStreamBanned](https://docs.byteplus.com/en/docs/12/docs-104479#onaudiostreambanned)/[onVideoStreamBanned](https://docs.byteplus.com/en/docs/12/docs-104479#onvideostreambanned) callbacks.

3. Supports setting [ScreenEncoderConfig.contentHint](https://docs.byteplus.com/en/docs/12/docs-104481#screenencoderconfig), the content type parameter when sharing screen, which improves the quality of the shared content in different scenarios.


<span id="fixed"></span>
### Fixed


1. Removed two RTM\-related error codes from the header file and the API Reference: USER_MESSAGE_EXCEED_MAX_LENGTH and USER_MESSAGE_EMPTY_USER. The SDK will emit these errors with the code [INVALID_PARAMS](https://docs.byteplus.com/en/docs/12/docs-104480) and detailed message, for example: SDKError('INVALID_PARAMS', 'The message length must be less than 64K').


<span id="web-sdk-4-45"></span>
## Web SDK 4.45

Release date: August 31, 2022

<span id="new"></span>
### New


1. Supports Auto\-play policy settings when calling [createEngine](https://docs.byteplus.com/en/docs/12/docs-104478#createengine). Enhanced the functionality of [play](https://docs.byteplus.com/en/docs/12/docs-104478#play) and [onAutoPlayFailed](https://docs.byteplus.com/en/docs/12/docs-104479#onautoplayfailed). You can call [play](https://docs.byteplus.com/en/docs/12/docs-104478#play) to start audio and/or video after auto\-play fails. You will also get notified when the local media fails to play automatically via an [onAutoPlayFailed](https://docs.byteplus.com/en/docs/12/docs-104479#onautoplayfailed) callback without an argument.

2. Sets the encoding configuration of the screen\-sharing stream, which is also applied in video capture. If the configuration is not supported by your browser, the video will be captured based on the supported configuration. You will also receive the callback [onLocalVideoSizeChanged](https://docs.byteplus.com/en/docs/12/docs-104479#onlocalvideosizechanged).


<span id="web-sdk-4-44"></span>
## Web SDK 4.44

Release date: July 29, 2022

This version marks the first official release of the BytePlus RTC SDK for Web.
