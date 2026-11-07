---
title: "Android"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70019"
---

<span id="cceb5a52"></span>
# 3.60.105

<span id="151f8c11"></span>
## API Changes


|V3.60.104 |V3.60.105 |Change Description |
|---|---|---|
|`RTCRoom.setRoomProfile(ChannelProfile roomProfileType)` |`RTCRoom.setLiveMode(LiveMode liveMode)` |Renamed from `setRoomProfile` to `setLiveMode`. The parameter type changed from `ChannelProfile` to `LiveMode`. |
|`sendLivePushSEIMessage`: prerequisite was `CHANNEL_PROFILE_LIVE_PUSH` set via `joinRoom` |`sendLivePushSEIMessage`: prerequisite is `LIVE_MODE_SOLO_HOST` set via `setLiveMode` |The prerequisite for calling `sendLivePushSEIMessage` changed from setting channel profile to `CHANNEL_PROFILE_LIVE_PUSH` during `joinRoom` to calling `setLiveMode` with `LIVE_MODE_SOLO_HOST`. |


<span id="b08c37e8"></span>
## Type Changes


|Type Name |Change Description |
|---|---|
|`LiveMode` |New enum type. Defines the live streaming mode:<br><br><br>* `LIVE_MODE_CO_HOST` (value 1): Co\-hosted live streaming mode for multi\-person or interactive live scenarios.<br><br>* `LIVE_MODE_SOLO_HOST` (value 2): Single\-host live streaming mode. |
|`ChannelProfile` |Removed enum values: `CHANNEL_PROFILE_LINK_MIC` and `CHANNEL_PROFILE_LIVE_PUSH`. Use the new `LiveMode` enum with `setLiveMode` instead. |
|`RTCRoomConfig` |Added `LiveMode liveMode` field. Default value: `LIVE_MODE_CO_HOST`. Specifies the live mode when joining a room. Only effective when `profile` is `CHANNEL_PROFILE_LIVE`. Can be changed after joining via `setLiveMode`. |
|`VideoEncoderConfig` |Added `int keyFrameIntervalMs` field. Default value: `0` (encoder determines automatically). Sets the key frame interval in milliseconds. |


<span id="63c30a3d"></span>
## New Interfaces


|Class / Module |Interface |Description |
|---|---|---|
|`RTCRoom` |`setLiveMode` |Sets the live streaming mode (co\-hosted / single\-host). Call after joining a room. |
|`RTCEngine` |`sendLivePushSEIMessage` |Sends SEI data in Key\-Value (JSON) format through video frames. Requires `LIVE_MODE_SOLO_HOST` mode. |


<span id="9da0cb73"></span>
## Deleted or Deprecated Interfaces


|Interface |Replacement |Description |
|---|---|---|
|`RTCRoom.setRoomProfile` |`RTCRoom.setLiveMode` |Replaced by `setLiveMode` with the new `LiveMode` enum. |


<span id="72865860"></span>
# 3.60.104

<span id="76f30714"></span>
## API Changes


|Change Details |Interface |Notes |
|---|---|---|
|Added |`setRoomProfile` |Sets room profile before or after joining a room. |
|Added |`sendLivePushSEIMessage` |Sends SEI (Supplemental Enhancement Information) data in Key\-Value format through video frames. |


<span id="a65c115b"></span>
## Type Changes


|Change Details |Changed Data Type |Notes |
|---|---|---|
|New Enum Value Added |ChannelProfile |New enum values:<br><br><br>* `CHANNEL_PROFILE_LINK_MIC`: Link mic mode, focuses on high quality, same bitrate as LIVE.<br><br>* `CHANNEL_PROFILE_LIVE_PUSH`: Live push mode for broadcasting scenarios. |
|New Member Variable Added |VideoEncoderConfig |Added `keyFrameIntervalMs` field: Sets key frame interval in milliseconds, default: 0. |
|New Member Variable Added |VideoPreprocessorConfig |Added `actionDomain` field (default: `PREVIEWANDENCODE`): Controls the effective range of your custom video preprocessor (registerLocalVideoProcessor). |
|New Enum Added |ProcessorActionDomain |Controls where the custom video preprocessor effects are applied:<br><br><br>* `PREVIEWANDENCODE`：Effects apply to both preview and transmission.<br><br>* `PREVIEW`：Effects apply only to local preview.<br><br>* `ENCODE`：Effects apply only to outgoing stream. |


<span id="_3-60"></span>
# 3.60.103

<span id="api-changes"></span>
## API Changes

<span id="header-files-and-base-class-names"></span>
### Header Files and Base Class Names


|Change Type |V3.58 |V3.60 |
|---|---|---|
|Header file name changes |../RTCVideo.java |../RTCEngine.java |
||../IRTCVideoEventHandler.java |../IRTCEngineEventHandler.java |
|Base class name changes (all modules) |public abstract class RTCVideo |public abstract class RTCEngine |
|New header files |None |../RTSRoom.java<br><br>../IRTSRoomEventHandler.java<br><br>../IGameRoom.java |


<span id="a0784eb6"></span>
### Engine Management


|Feature |V3.58 |V3.60 |Description |
|---|---|---|---|
|Create engine object |createRTCVideo(Context context, IRTCVideoEventHandler handler, EngineConfig config) |createRTCEngine(EngineConfig config, IRTCEngineEventHandler handler) |* **Parameter changes**:<br><br>   * `Context` moved into the `EngineConfig` class<br><br>   * New field added to `EngineConfig`: `isGameScene`, used to control game scene switch<br><br>* **Callback name changes**:<br><br><br>Changed from `IRTCVideoEventHandler` to `IRTCEngineEventHandler` |
|Destroy engine |destroyRTCVideo |destroyRTCEngine |**Method name change** |
|Engine event callback |IRTCVideoEventHandler |IRTCEngineEventHandler |**Method name change** |


<span id="3970b45e"></span>
### Room Management


|Feature |V3.58 |V3.60 |Description |
|---|---|---|---|
|Join room | | | |
|Room creation failure callback |onCreateRoomStateChanged(String roomId, int errorCode) |onRoomStateChanged(String roomId, String uid,int state, String extraInfo) |**Interface replacement**:<br><br>Room creation failure is notified by onRoomStateChanged. No longer through the `onCreateRoomStateChanged` callback. |
|Create room instance |createRTCRoom(String roomId) |createRTCRoom(String roomId) |**Behavior change**:<br><br>When creating a room instance with an existing roomId, it will return the previously created room instance and no longer trigger the error code `WARNING_CODE_OLD_ROOM_BEEN_REPLACED = -2016` |
|Callback for remote visible user joining room or invisible user in room switching to visible |onUserJoined(UserInfo userInfo,int elapsed) |onUserJoined(UserInfo userInfo) |**Parameter change**: Remove invalid parameter `elapsed`. |


<span id="1d540e2e"></span>
### Publish and Subscribe to Simulcast Streams


|Change Type |V3.58 |V3.60 |Description |
|---|---|---|---|
|Enable/disable pushing multiple video streams |enableSimulcastMode(boolean enabled) |setLocalSimulcastMode(VideoSimulcastMode mode) |* **Interface rename**<br><br>* **Feature extension and parameter changes**: Remove `boolean enabled` from the old method and replace it with `VideoSimulcastMode mode`, allowing you to specify the specific multi\-stream mode type through the parameter `VideoSimulcastMode`.<br><br>* **Default behavior adjustment**:<br><br>   * Old interface: When `enabled` is true, all configured Simulcast streams will be published<br><br>   * New interface: When the `mode` parameter is set to `VIDEO_SIMULCAST_MODE_ALWAYS_SIMULCAST(2)`, all configured Simulcast streams will be published<br><br>* **Call timing change**: The old method is called before joining the room or after joining the room but before publishing streams, while the new method needs to be called before joining the room |
|Set parameters for expected remote video stream subscription |setRemoteVideoConfig(<br><br>String userId,<br><br>RemoteVideoConfig remoteVideoConfig<br><br>) |setRemoteSimulcastStreamType(String streamId, SimulcastStreamType streamType) |* **Interface rename**<br><br>* **Parameter changes**:<br><br>   * Remove `RemoteVideoConfig remoteVideoConfig` and replace it with `SimulcastStreamType streamType`. No need to specify specific values, you can specify subscription preferences by passing enum values<br><br>   * streamId replaces userId |
|Set or update Simulcast stream encoding parameters |setVideoEncoderConfig(VideoEncoderConfig[] channelSolutions) |setLocalSimulcastMode(VideoSimulcastMode *mode*, VideoEncoderConfig[] *streamConfig*) |**Interface replacement** |
|* Set video stream encoding parameters for single stream<br><br>* Set video stream encoding parameters for the largest stream in multi\-stream scenarios |setVideoEncoderConfig(VideoEncoderConfig maxSolution) |setVideoEncoderConfig(VideoEncoderConfig encoderConfig) |* **Interface merge**<br><br>* **Feature change**: The new method is only used to set large stream encoding parameters<br><br>* **Parameter change**: Formal parameter changed to `encoderConfig` |


<span id="aa64da47"></span>
### Publish and Subscribe to Main Stream (Camera/Microphone Captured Stream)


|Feature |V3.58 |V3.60 |Description |
|---|---|---|---|
|1. **Publish/unpublish audio and video streams** ||||
|API:<br><br><br>* Publish audio and video streams<br><br>* Unpublish audio and video streams |* publishStream(MediaStreamType type)<br><br>* unpublishStream(MediaStreamType type) |* publishStreamVideo(boolean publish)<br><br>* publishStreamAudio(boolean publish) |* **Interface split and feature extension**:<br><br>   * **Split by audio and video**: 2 new methods are used to control video stream and audio stream publishing respectively<br><br>   * **Merge publish and unpublish**: New interface handles publish and unpublish operations through the `boolean publish` parameter<br><br>* **Parameter changes**:<br><br>   * Remove `MediaStreamType type`, new methods directly distinguish video and audio streams through method names<br><br>   * Add `boolean publish`<br><br>* **Behavior changes**:<br><br>   * V3.58: Effective both before and after joining room<br><br>   * V3.60: Scope limited to after joining room, calling before joining room is invalid |
|Callback:<br><br><br>* Callback for remote camera/microphone captured media streams in room<br><br>* Callback for removal of remote camera/microphone captured media streams in room |* onUserPublishStream(String uid,MediaStreamType type)<br><br>* onUserUnpublishStream(String uid,MediaStreamType type, StreamRemoveReason reason) |* onUserPublishStreamAudio(String streamId, StreamInfo streamInfo, boolean isPublish)<br><br>* onUserPublishStreamVideo(String streamId, StreamInfo streamInfo, boolean isPublish) |* **Interface split, rename, and feature extension**:<br><br>   * **Split by audio and video**: 2 new methods are used for audio stream and video stream subscription callbacks respectively<br><br>   * **Merge subscription and unsubscription status**: New interface handles publish and unpublish callbacks through the `isPublish` parameter<br><br>* **Parameter changes**:<br><br>   * Remove `MediaStreamType type`, new methods directly distinguish video and audio streams through method names<br><br>   * Add streamId and streamInfo parameters for stream identification<br><br>   * Remove `StreamRemoveReason reason`, no longer provide detailed information about removal reasons |
|Callback:<br><br>Callback when audio and video stream state triggers warnings or errors |onStreamStateChanged(<br><br>String roomId,<br><br>String uid,<br><br>int state,<br><br>String extraInfo<br><br>) |* onVideoPublishStateChanged(String streamId, StreamInfo streamInfo, PublishState state, PublishStateChangeReason reason)<br><br>* onAudioPublishStateChanged(String streamId, StreamInfo streamInfo, PublishState state, PublishStateChangeReason reason) |* **Interface split and rename**: Split by audio and video, new methods are used for video stream and audio stream publish state callbacks respectively<br><br>* **Parameter changes**:<br><br>   * **Parameter replacement**: roomId and uid replaced with streamId and streamInfo<br><br>   * **Parameter type change**: `state` type changed from `int` to enum type `SubscribeState`<br><br>   * **New parameter**: Add `reason` of type `PublishStateChangeReason` for more detailed description of the specific reason for state change<br><br>   * **Remove parameter**: Remove invalid parameter `extraInfo` |
|2. **Subscribe/unsubscribe to audio and video streams** ||||
|* Subscribe to audio and video streams<br><br>* Unsubscribe from audio and video streams |* subscribeStream(String uid, MediaStreamType type)<br><br>* unsubscribeStream(String uid, MediaStreamType type) |* subscribeStreamVideo(String streamId, boolean subscribe)<br><br>* subscribeStreamAudio(String streamId, boolean subscribe) |* **Interface split, rename, and feature extension**:<br><br>   * **Split by audio and video**: 2 new methods are used to control video stream and audio stream subscription respectively<br><br>   * **Merge subscription and unsubscription**: New interface handles subscription and unsubscription through `boolean subscribe` parameter<br><br>* **Parameter changes**:<br><br>   * Remove `MediaStreamType type`, new methods directly distinguish video streams and audio streams through method names<br><br>   * `uid` replaced by streamId<br><br>   * Add `boolean subscribe` |
|Audio and video stream subscription state change callback |onStreamSubscribed(int stateCode,String userId,SubscribeConfig info) |* onVideoSubscribeStateChanged(String streamId, StreamInfo streamInfo, SubscribeState state, SubscribeStateChangeReason reason)<br><br>* onAudioSubscribeStateChanged(String streamId, StreamInfo streamInfo, SubscribeState state, SubscribeStateChangeReason reason) |* **Interface split and rename**: Split by audio and video, 2 new methods are used for audio stream and video stream subscription state change callbacks respectively<br><br>* **Parameter changes**<br><br>   * `int stateCode`: Replaced with more explicit enum type `SubscribeState state`<br><br>   * userId replaced with streamId and streamInfo<br><br>   * Add parameter `reason`: Used to describe the specific reason for subscription state change in more detail<br><br>   * Remove `SubscribeConfig info` |
|Callback when audio and video stream state triggers warnings or errors |onStreamStateChanged(<br><br>String roomId,<br><br>String uid,<br><br>int state,<br><br>String extraInfo<br><br>) |* onVideoSubscribeStateChanged(String streamId, StreamInfo streamInfo, SubscribeState state, SubscribeStateChangeReason reason)<br><br>* onAudioSubscribeStateChanged(String streamId, StreamInfo streamInfo, SubscribeState state, SubscribeStateChangeReason reason) |* **Interface split and rename**: Split by audio and video, 2 new methods are used for audio stream and video stream subscription state change callbacks respectively<br><br>* **Parameter changes**:<br><br>   * **Parameter type changes**:<br><br>      * `state` type changed from `int` to enum type `SubscribeState`<br><br>      * roomId and uid replaced by streamId and streamInfo<br><br>   * **New parameter**: Add `reason` of type `SubscribeStateChangeReason` for more detailed description of the specific reason for state change<br><br>   * **Remove parameter**: Remove invalid parameter `extraInfo` |
|3. **Subscribe/unsubscribe to all media streams** ||||
|* Subscribe to all media streams<br><br>* Unsubscribe from all media streams |* subscribeAllStreams(MediaStreamType type)<br><br>* unsubscribeAllStreams(MediaStreamType type) |* subscribeAllStreamsVideo(boolean subscribe)<br><br>* subscribeAllStreamsAudio(boolean subscribe) |* **Interface split, rename, and feature extension**:<br><br>   * **Split by audio and video**: 2 new methods are used to subscribe/unsubscribe all video streams and subscribe/unsubscribe all audio streams respectively<br><br>   * **Merge subscription and unsubscription**: New interface handles subscription and unsubscription through `boolean subscribe` parameter<br><br>* **Parameter changes**:<br><br>   * Remove `MediaStreamType type`, new methods directly distinguish video and audio streams through method names<br><br>   * Add `boolean subscribe` |
|Pause receiving media streams from remote |pauseAllSubscribedStream(PauseResumeControlMediaType mediaType) |* pauseAllSubscribedStreamAudio()<br><br>* pauseAllSubscribedStreamVideo() |* **Interface split**: Split by audio and video, 2 new methods are used to pause receiving all remote audio streams and pause all remote video streams respectively<br><br>* **Parameter changes**: Remove `PauseResumeControlMediaType mediaType`, new methods directly distinguish audio and video streams through method names |
|Resume receiving media streams from remote |resumeAllSubscribedStream(PauseResumeControlMediaType mediaType) |* resumeAllSubscribedStreamAudio()<br><br>* resumeAllSubscribedStreamVideo() |* **Interface split**: Split by audio and video, 2 new methods are used to resume receiving all remote audio streams and resume receiving all remote video streams respectively<br><br>* **Parameter changes**: Remove `PauseResumeControlMediaType mediaType`, new methods directly distinguish audio and video streams through method names |


<span id="2cd9a97d"></span>
### Screen Sharing


1. Screen streams and regular video streams cannot coexist in the same engine. When screen stream is enabled, regular video stream will be automatically disabled, and when regular video stream is enabled, screen stream will be automatically disabled.

2. Screen streams and regular video streams have the same publish and subscribe methods, deprecating a series of interfaces with "screen".



|Feature |V3.58 |V3.60 |Description |
|---|---|---|---|
|Capture screen video |startScreenCapture(ScreenMediaType type, Intent mediaProjectionResultData) |startScreenCapture(ScreenMediaType type, Intent mediaProjectionResultData) |**Behavior change**:<br><br>Video capture will be stopped when screen capture starts |
|Set screen stream encoding parameters |setScreenVideoEncoderConfig(ScreenVideoEncoderConfig screenSolution) |setVideoEncoderConfig(VideoEncoderConfig encoderConfig) |**Interface replacement**:<br><br>Screen streams and video streams share the same set of encoding parameters, parameters set by setVideoEncoderConfig will apply to both screen streams and regular video streams |
|Publish/unpublish local screen audio and video streams |publishScreen(MediaStreamType type)<br><br>unpublishScreen(MediaStreamType type) |publishStreamVideo(boolean publish)<br><br>publishStreamAudio(boolean publish) |**Interface replacement**:<br><br>Screen streams and video streams share the same publish/unpublish interface<br><br>**Interface split**<br><br>Audio and video publish/unpublish interfaces are separated |
|Subscribe/unsubscribe to remote screen audio and video streams |subscribeScreen(String uid,MediaStreamType type)<br><br>unsubscribeScreen( String uid,MediaStreamType type) |subscribeStreamVideo(String streamId, boolean subscribe)<br><br>subscribeStreamAudio(String streamId, boolean subscribe) |**Interface replacement**:<br><br>Screen streams and video streams share the same subscribe/unsubscribe interface<br><br>**Interface split**<br><br>Audio and video subscribe/unsubscribe interfaces are separated<br><br>**Parameter changes**:<br><br>Use parameter streamId to distinguish which specific stream it is and whether it is a screen stream |
|Remote user publish or unpublish screen stream callback |onUserPublishScreen( String uid,MediaStreamType type)<br><br>onUserUnpublishScreen(String uid,MediaStreamType type,StreamRemoveReason reason) |onUserPublishStreamVideo(String streamId, StreamInfo streamInfo, boolean isPublish)<br><br>onUserPublishStreamAudio(String streamId, StreamInfo streamInfo, boolean isPublish) |**Interface replacement**:<br><br>Screen streams and video streams share the same publish/unpublish callback interface<br><br>**Interface split**<br><br>Audio and video publish/unpublish callback interfaces are separated<br><br>**Parameter changes**:<br><br>Use parameter streamId to distinguish which specific stream it is and whether it is a screen stream |
|Screen sharing stream video first frame send state callback |onScreenVideoFrameSendStateChanged(String roomId，RtcUser user，FirstFrameSendState state) |onVideoFrameSendStateChanged(String streamId, StreamInfo streamInfo, RtcUser user, FirstFrameSendState state) |**Interface replacement**:<br><br>Screen streams and video streams share the same video first frame send state callback<br><br>**Parameter changes**:<br><br>Use parameter streamId to distinguish which specific stream it is and whether it is a screen stream |
|Screen sharing stream video first frame play state callback |onScreenVideoFramePlayStateChanged(String roomId，RtcUser user，FirstFramePlayState state) |onVideoFramePlayStateChanged(String streamId, StreamInfo streamInfo, RtcUser user, FirstFramePlayState state) |**Interface replacement**:<br><br>Screen streams and video streams share the same video first frame play state callback<br><br>**Parameter changes**:<br><br>Use parameter streamId to distinguish which specific stream it is and whether it is a screen stream |


<span id="e891509a"></span>
### RTS

RTC includes RTS capabilities. The current version further splits RTS\-related interfaces. If only using RTS\-related capabilities, call createRTSRoom to create RTSRoom instance and use RTSRoomEventHandler callback. If using both audio/video capabilities and RTS capabilities, call createRTCRoom from RTCEngine to create RTCRoom instance and use RTCRoomEventHandler callback.


|Feature |V3.58 |V3.60 |Description |
|---|---|---|---|
|Create RTS room |createRTCRoom(String roomId) |createRTSRoom(String roomId) |* **Interface split**: If only using RTS\-related capabilities, call createRTSRoom to create RTSRoom instance |
|Set RTS related callback |setRTCRoomEventHandler(IRTCRoomEventHandler rtcRoomEventHandler); |setRTSRoomEventHandler(IRTSRoomEventHandler rtcRoomEventHandler) |* **Interface split**: If only using RTS\-related capabilities, call this interface in RTSRoom to set callback |
|Callback when receiving text message from user outside room |onUserMessageReceivedOutsideRoom(String uid,String message) |onUserMessageReceivedOutsideRoom(long msgid, String uid, String message) |* **Parameter changes**: Add msgid parameter to callback parameters |
|Callback when receiving binary message from user outside room |onUserBinaryMessageReceivedOutsideRoom(String uid, ByteBuffer message)jiu |onUserBinaryMessageReceivedOutsideRoom(long msgid, String uid, ByteBuffer message) |* **Parameter changes**: Add msgid parameter to callback parameters |
|Callback for receiving broadcast message in room |onRoomMessageReceived(String uid,String message) |onRoomMessageReceived(long msgid, String uid, String message) |* **Parameter changes**: Add msgid parameter to callback parameters |
|Callback for receiving broadcast binary message in room |onRoomBinaryMessageReceived(String uid,ByteBuffer message) |onRoomBinaryMessageReceived(long msgid, String uid, ByteBuffer message) |* **Parameter changes**: Add msgid parameter to callback parameters |
|Callback when receiving point\-to\-point text message from other users in room |onUserMessageReceived(String uid,String message) |onUserMessageReceived(long msgid, String uid, String message) |* **Parameter changes**: Add msgid parameter to callback parameters |
|Callback when receiving point\-to\-point binary message from other users in room |onUserBinaryMessageReceived( String uid,ByteBuffer message) |onUserBinaryMessageReceived(long msgid, String uid, ByteBuffer message) |* **Parameter changes**: Add msgid parameter to callback parameters |


<span id="e08eb4b7"></span>
### WTN Streams (Formerly Public Streams)


* Interface location changes:

   * Interfaces for subscribing to WTN streams are moved to the newly added `IWTNStream` class.

   * WTN stream subscriber callbacks are moved to the newly added `IWTNStreamEventHandler` callback class. You need to call setWTNStreamEventHandler first to set the callback handler.

* Share MixedStreamConfig with mixed stream push interfaces to improve usability.

* Add onWTNRemoteVideoStats and onWTNRemoteAudioStats: Used to get WTN stream information and detect stream quality.

* Interfaces undergo split, rename, replacement, parameter changes, etc. Specific changes are as follows:



|Feature |V3.58 |V3.60 |Description |
|---|---|---|---|
|Publish WTN stream<br><br>Support composing media streams published by multiple users in a specified room into one WTN stream |startPushPublicStream(<br><br>String publicStreamId,<br><br>PublicStreaming publicStream<br><br>) |startPushMixedStream(String taskId, MixedStreamPushTargetConfig pushTargetConfig, MixedStreamConfig mixedConfig) |* **Interface rename**<br><br>* **Interface merge and feature extension**: startPushPublicStream and startPushMixedStreamToCDN are merged into startPushMixedStream, the new interface can be used for both mixed stream push to CDN or push WTN (formerly public stream)<br><br>* **Parameter changes**:<br><br>   * Add `taskId`: Set push task ID to identify the push task<br><br>   * Add `MixedStreamConfig mixedConfig` type for configuring mixed stream push, such as video and audio transcoding parameters, layout, etc.<br><br>   * Remove `String publicStreamId`: Specify WTN stream ID (i.e., public stream ID) through the new parameter `MixedStreamPushTargetConfig pushTargetConfig`<br><br>   * Remove `PublicStreaming publicStream`, use the new parameter `MixedStreamConfig mixedConfig` to specify WTN stream configuration (such as video transcoding, layout, etc.) |
|Update WTN stream |updatePublicStreamParam(<br><br>String publicStreamId,<br><br>PublicStreaming transcoding<br><br>) |updatePushMixedStream(String taskId, MixedStreamPushTargetConfig pushTargetConfig, MixedStreamConfig mixedConfig) |* **Interface rename**<br><br>* **Interface merge and feature extension**: updatePublicStreamParam and updatePushMixedStreamToCDN are merged into updatePushMixedStream, the new interface can be used for both updating mixed stream push to CDN and push WTN (formerly public stream) tasks<br><br>* **Parameter changes**:<br><br>   * Add `taskId`: ID of the mixed stream task<br><br>   * Remove `String publicStreamId`: Specify WTN stream ID (i.e., public stream ID) through the new parameter `MixedStreamPushTargetConfig pushTargetConfig`<br><br>   * Remove `PublicStreaming transcoding`, use the new parameter `MixedStreamConfig mixedConfig` to configure WTN stream (such as video and audio transcoding parameters, layout, etc.) |
|Stop publishing WTN stream |stopPushPublicStream(String publicStreamId) |stopPushMixedStream(String taskId, MixedStreamPushTargetType targetType) |* **Interface rename**<br><br>* **Interface merge and feature extension**: stopPushPublicStream and stopPushStreamToCDN are merged into stopPushMixedStream, the new interface can be used for both stopping WTN stream (formerly public stream) publishing and stopping mixed stream push<br><br>* **Parameter changes**:<br><br>   * Add `taskId`: ID of the mixed stream task<br><br>   * Remove `String publicStreamId`, use `MixedStreamPushTargetType targetType` to specify the type of stream to stop |
|Subscribe/unsubscribe WTN stream |* startPlayPublicStream(String publicStreamId)<br><br>* stopPlayPublicStream(String publicStreamId) |* subscribeWTNVideoStream(String streamId, boolean subscribe)<br><br>* subscribeWTNAudioStream(String streamId, boolean subscribe) |* **Interface split, rename, and feature extension**:<br><br>   * **Split by audio and video**: 2 new methods are used for subscribing/unsubscribing WTN audio stream and subscribing/unsubscribing video stream respectively<br><br>   * **Merge subscription and unsubscription**: New interface handles subscription and unsubscription through `boolean subscribe` parameter<br><br>* **Parameter changes**:<br><br>   * `publicStreamId`: Renamed to `streamId`<br><br>   * Add `boolean subscribe` |
|Bind WTN stream canvas |setPublicStreamVideoCanvas(<br><br>String publicStreamId,<br><br>VideoCanvas canvas<br><br>) |setWTNRemoteVideoCanvas(String streamId, VideoCanvas canvas) |* **Interface rename**<br><br>* **Parameter changes**: `publicStreamId` renamed to `streamId` |
|Specify external renderer for WTN stream |setPublicStreamVideoSink(<br><br>String publicStreamId,<br><br>IVideoSink videoSink,<br><br>@IVideoSink.PixelFormat int requiredFormat<br><br>) |setWTNRemoteVideoSink(String streamId, IVideoSink videoSink, RemoteVideoSinkConfig config) |* **Interface rename**<br><br>* **Parameter changes**:<br><br>   * `publicStreamId` renamed to `streamId`<br><br>   * Add field `RemoteVideoSinkConfig config` for configuring remote video frames (such as position, format, whether to mirror video frames, etc.)<br><br>   * Original `@IVideoSink.PixelFormat int requiredFormat` is implemented by the `pixelFormat` field in `RemoteVideoSinkConfig`, default is 0 (original format) |
|Set WTN stream playback volume |setPublicStreamAudioPlaybackVolume(<br><br>String publicStreamId,<br><br>int volume<br><br>) |setWTNRemoteAudioPlaybackVolume(String streamId, int volume) |* **Interface rename**<br><br>* **Parameter changes**: `publicStreamId` renamed to `streamId` |
|WTN stream publish result callback |onPushPublicStreamResult(<br><br>String roomId,<br><br>String publicStreamId,<br><br>PublicStreamErrorCode error<br><br>) |onMixedStreamEvent(MixedStreamTaskInfo info, MixedStreamTaskEvent event, MixedStreamTaskErrorCode error) |* **Interface rename**<br><br>* **Interface merge**: onMixingEvent, onStreamMixingEvent and onPushPublicStreamResult are merged into onMixedStreamEvent, the new interface can be used for both mixed stream push to CDN / WTN stream status callbacks<br><br>* **Parameter changes**:<br><br>   * `PublicStreamErrorCode` changed to `MixedStreamTaskErrorCode`, sharing the same enumeration class with mixed stream push tasks. For change details, see Android<br><br>   * `roomId`: No longer needs to be passed in<br><br>   * `publicStreamId`: Replaced by `taskId` in the new `MixedStreamTaskInfo info`<br><br>   * Add `MixedStreamTaskEvent event`, for details see Android |
|WTN stream playback task callback |onPlayPublicStreamResult(<br><br>String publicStreamId,<br><br>PublicStreamErrorCode error<br><br>) |* onWTNVideoSubscribeStateChanged(String streamId, WTNSubscribeState stateCode, WTNSubscribeStateChangeReason reason)<br><br>* onWTNAudioSubscribeStateChanged(String streamId, WTNSubscribeState stateCode, WTNSubscribeStateChangeReason reason) |* **Interface split and rename**: Split into 2 independent interfaces for WTN audio/video stream subscription state change callbacks respectively<br><br>* **Parameter changes**<br><br>   * `publicStreamId` renamed to `streamId`<br><br>   * Remove `PublicStreamErrorCode error`: Replaced by `WTNSubscribeState stateCode` (subscription state code) and `WTNSubscribeStateChangeReason reason` (subscription state change reason). |
|Receive SEI callback in WTN stream |onPublicStreamSEIMessageReceived(<br><br>String publicStreamId,<br><br>ByteBuffer message,<br><br>DataMessageSourceType sourceType<br><br>) |onWTNSEIMessageReceived(String streamId, int channelId, ByteBuffer message) |* **Interface rename**<br><br>* **Location change**: Moved to IWTNStream class<br><br>* **Parameter changes**:<br><br>   * `publicStreamId` renamed to `streamId`<br><br>   * Add `channelId`: Set different ChannelID for different receivers, receivers can select SEI information to focus on based on ChannelID in callback<br><br>   * Remove `DataMessageSourceType sourceType`, no longer needs to be passed in |
|Receive Data Message callback in WTN stream |onPublicStreamDataMessageReceived(<br><br>String publicStreamId,<br><br>ByteBuffer message,<br><br>DataMessageSourceType sourceType<br><br>) |onWTNDataMessageReceived(String streamId, ByteBuffer message, DataMessageSourceType sourceType) |* **Interface rename**<br><br>* **Location change**: Moved to IWTNStream class<br><br>* **Parameter changes**: `publicStreamId` renamed to `streamId` |
|WTN video stream first frame decode success callback |onFirstPublicStreamVideoFrameDecoded(<br><br>String publicStreamId,<br><br>VideoFrameInfo videoFrameInfo<br><br>) |onWTNFirstRemoteVideoFrameDecoded(String streamId, VideoFrameInfo info) |* **Interface rename**<br><br>* **Location change**: Moved to IWTNStream class<br><br>* **Parameter changes**:<br><br>   * `publicStreamId` renamed to `streamId`<br><br>   * `videoFrameInfo` renamed to `info` |
|WTN audio stream first frame decode success callback |onFirstPublicStreamAudioFrame(String publicStreamId) |onWTNFirstRemoteAudioFrame(String streamId) |* **Interface rename**<br><br>* **Location change**: Moved to IWTNStream class<br><br>* **Parameter changes**: `publicStreamId` renamed to `streamId` |


<span id="2179e567"></span>
### Push to CDN

Optimized the usability of live streaming push interfaces. Share MixedStreamConfig with WTN interfaces to improve usability. If you have already implemented live streaming push functionality, refer to the following table to replace interfaces.


|Feature |V3.58 |V3.60 |Description |
|---|---|---|---|
|1. **Mixed stream push** ||||
|API: Mixed stream push |startPushMixedStreamToCDN(<br><br>String taskId,<br><br>MixedStreamConfig mixedConfig,<br><br>IMixedStreamObserver observer<br><br>) |startPushMixedStream(String taskId, MixedStreamPushTargetConfig pushTargetConfig, MixedStreamConfig mixedConfig) |* **Interface rename**<br><br>* **Interface merge and feature change**: startPushPublicStream and startPushMixedStreamToCDN are merged into startPushMixedStream, the new interface can be used for both mixed stream push to CDN and push WTN (formerly public stream)<br><br>* **Parameter changes**:<br><br>   * Remove: `observer`, no longer needs to be passed in<br><br>   * Add: `pushTargetConfig`, used to specify push stream address (such as CDN address, WTN stream ID) |
|Callback:<br><br>Mixed stream push live streaming status callback |* onMixingEvent(ByteRTCStreamMixingEvent eventType,String taskId,ByteRTCTranscoderErrorCode error,MixedStreamType mixType)<br><br>* onStreamMixingEvent(ByteRTCStreamMixingEvent eventType,String taskId,ByteRTCTranscoderErrorCode error,MixedStreamType mixType) |onMixedStreamEvent(MixedStreamTaskInfo info, MixedStreamTaskEvent event, MixedStreamTaskErrorCode error) |* **Interface split and rename**: Split by mixed stream task event callback and single stream task event callback.<br><br>* **Interface merge**: onMixingEvent, onStreamMixingEvent and onPushPublicStreamResult are merged into onMixedStreamEvent, the new interface can be used for both mixed stream push to CDN / WTN stream status callbacks<br><br>* **Parameter changes**:<br><br>   * **Event change**: `ByteRTCStreamMixingEvent eventType` replaced by `MixedStreamTaskEvent event`, for details see Android<br><br>   * **Error code change**: `ByteRTCTranscoderErrorCode` replaced by `MixedStreamTaskErrorCode`, for details see Android<br><br>   * **Remove** **`MixedStreamType mixType`**: No replacement<br><br>   * **Add parameter** **`MixedStreamTaskInfo info`**: Contains information related to mixed stream tasks, such as stream type, etc.<br><br>* **Location change**: Moved to IRTCEngineEventHandler |
|Update mixed stream push task |updatePushMixedStreamToCDN(<br><br>String taskId,<br><br>MixedStreamConfig mixedConfig<br><br>) |updatePushMixedStream(String taskId, MixedStreamPushTargetConfig pushTargetConfig, MixedStreamConfig mixedConfig) |* **Interface rename**<br><br>* **Interface merge**: updatePublicStreamParam and updatePushMixedStreamToCDN are merged into updatePushMixedStream, the new interface can be used for both updating mixed stream push to CDN and push WTN (formerly public stream) tasks<br><br>* **Parameter changes**: Add parameter `MixedStreamPushTargetConfig pushTargetConfig` for setting target push stream address |
|2. **Single stream push** ||||
|API: Start single stream push |startPushSingleStreamToCDN(<br><br>String taskId,<br><br>PushSingleStreamParam param,<br><br>IPushSingleStreamToCDNObserver observer<br><br>) |startPushSingleStream(String taskId, PushSingleStreamParam param) |* **Interface rename**<br><br>* **Remove parameter**: `IPushSingleStreamToCDNObserver observer`<br><br>* **API feature extension**:<br><br>   * This upgrade allows the interface to not only push RTC streams to CDN, but also supports pushing RTC streams to RTC rooms |
|Callback:<br><br>Single stream push live streaming status callback |onStreamPushEvent(<br><br>ByteRTCStreamSinglePushEvent eventType,<br><br>String taskId,<br><br>int error<br><br>) |onSingleStreamEvent(String taskId, SingleStreamTaskEvent event, SingleStreamTaskErrorCode error) |* **Interface rename**<br><br>* **Parameter changes**:<br><br>   * **Event change**: `ByteRTCStreamSinglePushEvent eventType` replaced by `SingleStreamTaskEvent event`, for details see Android<br><br>   * `int error`: Replaced by `SingleStreamTaskErrorCode error`, the new enumeration provides more specific error code definitions, for details see Android |
|3. **Stop push** ||||
|Stop single stream/mixed stream push |stopPushStreamToCDN(String *taskId*) |* stopPushSingleStream(String taskId)<br><br>* stopPushMixedStream(String taskId, MixedStreamPushTargetType targetType) |* **Interface split and rename**: Split by single stream and mixed stream<br><br>* **Among them, the stop mixed stream push interface (stopPushMixedStream)** :<br><br>   * Functionality: Can be used to stop pushing to CDN and also to stop pushing WTN streams<br><br>   * Add parameter: `MixedStreamPushTargetType targetType`, used to specify the stream type to stop |


<span id="d5dbec2c"></span>
### Audio & Video Transport


|Feature |Interface name |Description | |
|---|---|---|---|
|Callback when receiving the first frame from a remote audio stream | | | |
|* Callback after SDK successfully renders the first frame of remote video stream<br><br>* Callback after SDK receives and decodes the first frame of remote video stream |* onFirstRemoteVideoFrameRendered(String streamId, StreamInfo streamInfo, VideoFrameInfo frameInfo)<br><br>* onFirstRemoteVideoFrameDecoded(String streamId, StreamInfo streamInfo, VideoFrameInfo frameInfo) |**Parameter changes**:<br><br>RemoteStreamKey replaced by streamId, streamInfo<br><br>**New applicable scenarios**:<br><br>These two callbacks will also be received after a remote user cancels publishing video and republishes video.<br><br>Canceling publishing includes active cancellation by the publisher, active room exit, disconnection, and stopping capture. |^^ |
|Push external audio reference frame to SDK |pushReferenceAudioPCMData |**New API**: Custom audio echo cancellation reference signal | |


<span id="61c96f60"></span>
### Audio\-Video Synchronization


|Feature |V3.58 |V3.60 |Description |
|---|---|---|---|
|When audio and video synchronization state changes |onAVSyncStateChange(AVSyncState state) |onAVSyncEvent(String roomId, String uid, AVSyncEvent eventCode) |* **Interface rename**<br><br>* **Parameter changes**<br><br>   * Added `roomId` and `uid`<br><br>   * `AVSyncState state` (synchronization state): Type replaced by `AVSyncEvent` (synchronization failure event), you can call setMultiDeviceAVSync with empty parameters to unbind the synchronization relationship when receiving this notification, and call the interface again for binding.<br><br>* **Behavior change**: Audio and video synchronization failure<br><br>   * 3.58: Returned by the following error code: ErrorCode.ERROR_CODE_INVALID_AUDIO_SYNC_USERID_REPEATED = \-1083<br><br>   * 3.60: Returned through onAVSyncEvent `AVSyncEvent.INVALID_UID_REPEATED(0)` |


<span id="85085024"></span>
### Volume, audio playback routing, and audio scenario


|Feature |V3.58 |V3.60 |Description |
|---|---|---|---|
|Force switch current audio playback route |setAudioRoute |setAudioRoute |**Restriction changes**:<br><br>Force switching the current audio playback route is no longer limited to use only in the `AUDIO_SCENARIO_COMMUNICATION` audio scenario, it can be used as long as the current state is call mode. |
|Set audio scenario type |setAudioScenario |setAudioScenario |* **Parameter changes**:<br><br>   * The volume mode used by audio devices has changed, see media volume and call volume:<br><br>      * Audio scenario has been set through setAudioScenario: Need to refer to the above documentation, replace with the updated audio scenario, and pay attention to the changes in volume mode.<br><br>      * Audio scenario has never been set through setAudioScenario: Also need to pay attention to the volume mode changes of the same audio device under the default audio scenario.<br><br>* **API behavior changes**:<br><br>   * This upgrade causes this interface to adopt different audio 3A algorithms according to different AudioScenarioType parameters.<br><br>* **Specific upgrade guide**: https://bytedance.larkoffice.com/docx/V8dTdJasdoLJiDxtxRvc8yzwnHb |


<span id="b58d56b3"></span>
### Push External Video Frame


|V3.58 |V3.60 |Description |
|---|---|---|
|pushExternalVideoFrame(VideoFrame frame) |pushExternalVideoFrame(VideoFrameData frame) |**Parameter changes**:<br><br>The type of parameter `videoFrame` is replaced from `VideoFrame` to `VideoFrameData`. Compared to the original type, both the included parameters and whether they are required have changed. For details, see Android. |


<span id="bcaaab94"></span>
### Get Song List for Each Chart Based on Hot Charts


|V3.58 |V3.60 |Description |
|---|---|---|
|getHotMusic(@NonNull MusicHotType[] hotTypes,@NonNull MusicFilterType[] filters) |getHotMusic(@NonNull ListcustomHotlistId, @NonNull MusicFilterType[] filters) |**Parameter replacement**: Remove `hotType`, replace with `customHotlistId`, the type is also changed from enumeration to `List<String>` (chart ID list), used to provide custom hot music list IDs. Property value correspondence is as follows:<br><br><br>* `CONTENT_CENTER` → `ContentCenter`<br><br>* `PROJECT` → `Project` |


<span id="7e8a731b"></span>
### StreamId Unique Stream Identification

The current version uses streamId to uniquely identify a stream, so the streamIndex parameters in previous versions of various APIs are replaced by streamId or related information. The involved APIs are as follows:


|V3.58 |V3.60 |Description |
|---|---|---|
|muteAudioCapture(StreamIndex index, boolean mute) |muteAudioCapture(boolean mute) |**Parameter changes**:<br><br>Remove StreamIndex parameter |
|setCaptureVolume(StreamIndex index, int volume) |setCaptureVolume(int volume) |**Parameter changes**:<br><br>Remove StreamIndex parameter |
|enableAlphaChannelVideoEncode(StreamIndex streamIndex, AlphaLayout alphaLayout) |enableAlphaChannelVideoEncode(AlphaLayout alphaLayout) |**Parameter changes**:<br><br>Remove StreamIndex parameter |
|disableAlphaChannelVideoEncode(StreamIndex streamIndex) |disableAlphaChannelVideoEncode() |**Parameter changes**:<br><br>Remove StreamIndex parameter |
|setLocalVideoCanvas(StreamIndex streamIndex, VideoCanvas videoCanvas) |setLocalVideoCanvas(VideoCanvas videoCanvas) |**Parameter changes**:<br><br>Remove StreamIndex parameter |
|updateLocalVideoCanvas(StreamIndex streamIndex, int renderMode, int backgroundColor) |updateLocalVideoCanvas(int renderMode, int backgroundColor) |**Parameter changes**:<br><br>Remove StreamIndex parameter |
|setRemoteVideoCanvas(RemoteStreamKey streamKey, VideoCanvas videoCanvas) |setRemoteVideoCanvas(String streamId, VideoCanvas videoCanvas) |**Parameter changes**:<br><br>Replace RemoteStreamKey parameter with streamId |
|int updateRemoteStreamVideoCanvas(RemoteStreamKey streamKey, RemoteVideoRenderConfig remoteVideoRenderConfig) |updateRemoteStreamVideoCanvas(String streamId, RemoteVideoRenderConfig remoteVideoRenderConfig) |**Parameter changes**:<br><br>Replace RemoteStreamKey parameter with streamId |
|setLocalVideoSink(StreamIndex index, IVideoSink videoSink, LocalVideoSinkConfig config) |setLocalVideoSink(IVideoSink videoSink, LocalVideoSinkConfig config) |**Parameter changes**:<br><br>Remove StreamIndex parameter |
|setRemoteVideoSink(RemoteStreamKey streamKey, IVideoSink videoSink, RemoteVideoSinkConfig config) |setRemoteVideoSink(String streamId, IVideoSink videoSink, RemoteVideoSinkConfig config) |**Parameter changes**:<br><br>Replace RemoteStreamKey parameter with streamId |
|setVideoSourceType(StreamIndex index, VideoSourceType type) |setVideoSourceType(VideoSourceType type) |**Parameter changes**:<br><br>Remove StreamIndex parameter |
|setRemoteVideoMirrorType(RemoteStreamKey remoteStreamKey, RemoteMirrorType mirrorType) |setRemoteVideoMirrorType(String streamId, RemoteMirrorType mirrorType) |**Parameter changes**:<br><br>Replace RemoteStreamKey parameter with streamId |
|sendSEIMessage(StreamIndex streamIndex, byte[] message, int repeatCount, SEICountPerFrame mode) |sendSEIMessage(byte[] message, int repeatCount, SEICountPerFrame mode) |**Parameter changes**:<br><br>Remove StreamIndex parameter |
|startFileRecording(StreamIndex type, RecordingConfig config, RecordingType recordingType) |startFileRecording(RecordingConfig config, RecordingType recordingType) |**Parameter changes**:<br><br>Remove StreamIndex parameter |
|stopFileRecording(StreamIndex type) |stopFileRecording() |**Parameter changes**:<br><br>Remove StreamIndex parameter |
|setRemoteAudioPlaybackVolume(String roomId, String uid, int *volume*) |setRemoteAudioPlaybackVolume(String streamId, int volume) |* **Parameter changes**:<br><br><br>Replace roomid, uid parameters with streamId<br><br><br>* **Feature extension**:<br><br><br>Only supports adjusting media stream volume from specified users, upgraded to support separately adjusting local capture media stream volume, screen stream volume, and specified process volume. |
|pushExternalEncodedVideoFrame(StreamIndex streamIndex, int videoIndex, RTCEncodedVideoFrame encodedVideoFrame) |pushExternalEncodedVideoFrame(int videoIndex, RTCEncodedVideoFrame encodedVideoFrame) |**Parameter changes**:<br><br>Remove StreamIndex parameter |
|setVideoDecoderConfig(RemoteStreamKey key, VideoDecoderConfig config) |setVideoDecoderConfig(String streamId, VideoDecoderConfig config) |**Parameter changes**:<br><br>Replace RemoteStreamKey parameter with streamId |
|requestRemoteVideoKeyFrame(RemoteStreamKey streamKey) |requestRemoteVideoKeyFrame(String streamId) |**Parameter changes**:<br><br>Replace RemoteStreamKey parameter with streamId |
|setVideoWatermark(StreamIndex streamIndex, String imagePath, RTCWatermarkConfig watermarkConfig) |setVideoWatermark(String imagePath, RTCWatermarkConfig watermarkConfig) |**Parameter changes**:<br><br>Remove StreamIndex parameter |
|clearVideoWatermark(StreamIndex streamIndex) |clearVideoWatermark() |**Parameter changes**:<br><br>Remove StreamIndex parameter |
|takeLocalSnapshot(StreamIndex streamIndex, ISnapshotResultCallback callback) |takeLocalSnapshot(ISnapshotResultCallback callback) |**Parameter changes**:<br><br>Replace StreamIndex parameter with streamId |
|takeRemoteSnapshot(StreamIndex streamIndex, ISnapshotResultCallback callback) |takeRemoteSnapshot(String streamId, ISnapshotResultCallback callback) |**Parameter changes**:<br><br>Replace StreamIndex parameter with streamId |
|onUserStartVideoCapture(String roomId,String uid) |onUserStartVideoCapture(String streamId, StreamInfo streamInfo) |**Parameter changes**:<br><br>roomId, uid replaced by streamId, streamInfo |
|onUserStopVideoCapture(String roomId, String uid) |onUserStopVideoCapture(String streamId, StreamInfo streamInfo) |**Parameter changes**:<br><br>roomId, uid replaced by streamId, streamInfo |
|onUserStartAudioCapture(String roomId, String uid) |onUserStartAudioCapture(String streamId, StreamInfo streamInfo) |**Parameter changes**:<br><br>roomId, uid replaced by streamId, streamInfo |
|onUserStopAudioCapture(String roomId, String uid) |onUserStopAudioCapture(String streamId, StreamInfo streamInfo) |**Parameter changes**:<br><br>roomId, uid replaced by streamId, streamInfo |
|onLocalAudioStateChanged(LocalAudioStreamState state, LocalAudioStreamError error) |onLocalAudioStateChanged(String streamId, StreamInfo streamInfo, LocalAudioStreamState state, LocalAudioStreamError error) |**Parameter changes**:<br><br>Add parameters streamId, streamInfo |
|onLocalVideoStateChanged(StreamIndex streamIndex, LocalVideoStreamState state, LocalVideoStreamError error) |onLocalVideoStateChanged(String streamId, StreamInfo streamInfo, LocalVideoStreamState state, LocalVideoStreamError error) |**Parameter changes**:<br><br>StreamIndex replaced by streamId, streamInfo |
|onRemoteAudioStateChanged(RemoteStreamKey key, RemoteAudioState state ,RemoteAudioStateChangeReason reason) |onRemoteAudioStateChanged(String streamId, StreamInfo streamInfo, RemoteAudioState state, RemoteAudioStateChangeReason reason) |**Parameter changes**:<br><br>RemoteStreamKey replaced by streamId, streamInfo |
|onRemoteVideoStateChanged(RemoteStreamKey streamKey, RemoteVideoState videoState, RemoteVideoStateChangeReason videoStateReason) |onRemoteVideoStateChanged(String streamId, StreamInfo streamInfo, RemoteVideoState videoState, RemoteVideoStateChangeReason videoStateReason) |**Parameter changes**:<br><br>RemoteStreamKey replaced by streamId, streamInfo |
|onFirstLocalVideoFrameCaptured(StreamIndex streamIndex, VideoFrameInfo frameInfo) |onFirstLocalVideoFrameCaptured(IVideoSource videoSource, VideoFrameInfo frameInfo) |**Parameter changes**:<br><br>StreamIndex replaced by IVideoSource |
|onLocalVideoSizeChanged(StreamIndex streamIndex, VideoFrameInfo frameInfo) |onLocalVideoSizeChanged(IVideoSource videoSource, VideoFrameInfo frameInfo) |**Parameter changes**:<br><br>StreamIndex replaced by IVideoSource |
|onRemoteVideoSizeChanged(RemoteStreamKey remoteStreamKey, VideoFrameInfo frameInfo) |onRemoteVideoSizeChanged(String streamId, StreamInfo streamInfo, VideoFrameInfo frameInfo) |**Parameter changes**:<br><br>RemoteStreamKey replaced by streamId, streamInfo |
|onFirstLocalAudioFrame(StreamIndex streamIndex) |onFirstLocalAudioFrame(IAudioSource audioSource) |**Parameter changes**:<br><br>StreamIndex replaced by IAudioSource |
|onSEIMessageReceived(RemoteStreamKey remoteStreamKey,ByteBuffer message) |onSEIMessageReceived(String streamId, StreamInfo streamInfo, ByteBuffer message) |**Parameter changes**:<br><br>RemoteStreamKey replaced by streamId, streamInfo |
|onSEIStreamUpdate(RemoteStreamKey remoteStreamKey, SEIStreamUpdateEvent event) |onSEIStreamUpdate(String streamId, StreamInfo streamInfo, SEIStreamUpdateEvent event) |**Parameter changes**:<br><br>RemoteStreamKey replaced by streamId, streamInfo |
|onRecordingStateUpdate(StreamIndex index, RecordingState state, RecordingErrorCode errorCode, RecordingInfo info) |onRecordingStateUpdate(IVideoSource videoSource, RecordingState state, RecordingErrorCode errorCode, RecordingInfo info) |**Parameter changes**:<br><br>StreamIndex replaced by IVideoSource |
|onRecordingProgressUpdate(StreamIndex index, RecordingProgress progress, RecordingInfo info) |onRecordingProgressUpdate(IVideoSource videoSource, RecordingProgress progress, RecordingInfo info) |**Parameter changes**:<br><br>StreamIndex replaced by IVideoSource |
|onStreamSyncInfoReceived(RemoteStreamKey streamKey, StreamSyncInfoConfig.SyncInfoStreamType streamType, ByteBuffer data) |onStreamSyncInfoReceived(String streamId, StreamInfo streamInfo, StreamSyncInfoConfig.SyncInfoStreamType streamType, ByteBuffer data) |**Parameter changes**:<br><br>RemoteStreamKey replaced by streamId, streamInfo |
|onAudioFrameSendStateChanged(String roomId, RtcUser user, FirstFrameSendState state) |onAudioFrameSendStateChanged(String streamId, StreamInfo streamInfo, RtcUser user, FirstFrameSendState state) |**Parameter changes**:<br><br>roomId replaced by streamId, streamInfo |
|onVideoFrameSendStateChanged(String roomId, RtcUser user, FirstFrameSendState state) |onVideoFrameSendStateChanged(String streamId, StreamInfo streamInfo, RtcUser user, FirstFrameSendState state) |**Parameter changes**:<br><br>roomId replaced by streamId, streamInfo |
|onAudioFramePlayStateChanged(String roomId, RtcUser user, FirstFramePlayState state) |onAudioFramePlayStateChanged(String streamId, StreamInfo streamInfo, RtcUser user, FirstFramePlayState state) |**Parameter changes**:<br><br>roomId replaced by streamId, streamInfo |
|onVideoFramePlayStateChanged(String roomId, RtcUser user, FirstFramePlayState state) |onVideoFramePlayStateChanged(String streamId, StreamInfo streamInfo, RtcUser user, FirstFramePlayState state) |**Parameter changes**:<br><br>roomId replaced by streamId, streamInfo |
|onSimulcastSubscribeFallback(RemoteStreamSwitch event) |onSimulcastSubscribeFallback(String streamId, StreamInfo streamInfo, RemoteStreamSwitch event) |**Parameter changes**:<br><br>Added streamId, streamInfo parameters |
|onPerformanceAlarms(PerformanceAlarmMode mode, String roomId, PerformanceAlarmReason reason, SourceWantedData data) |onPerformanceAlarms(String streamId, StreamInfo streamInfo, PerformanceAlarmMode mode, PerformanceAlarmReason reason, SourceWantedData data) |**Parameter changes**:<br><br>roomId replaced by streamId, streamInfo |
|onLocalStreamStats(LocalStreamStats stats) |onLocalStreamStats(String streamId, StreamInfo streamInfo, LocalStreamStats stats) |**Parameter changes**:<br><br>Added streamId, streamInfo parameters |
|onRemoteStreamStats(RemoteStreamStats stats) |onRemoteStreamStats(String streamId, StreamInfo streamInfo, RemoteStreamStats stats) |**Parameter changes**:<br><br>Added streamId, streamInfo parameters |
|onLocalEncodedVideoFrame(StreamIndex streamIndex, RTCEncodedVideoFrame encodedVideoFrame) |onLocalEncodedVideoFrame(IVideoSource videoSource, RTCEncodedVideoFrame encodedVideoFrame) |**Parameter changes**:<br><br>StreamIndex replaced by IVideoSource |
|onRemoteEncodedVideoFrame(RemoteStreamKey streamKey, RTCEncodedVideoFrame encodedVideoFrame) |onRemoteEncodedVideoFrame(String streamId, StreamInfo streamInfo, RTCEncodedVideoFrame encodedVideoFrame) |**Parameter changes**:<br><br>RemoteStreamKey replaced by streamId, streamInfo |
|onTakeLocalSnapshotResult(long taskId, StreamIndex streamIndex, Bitmap image, int errorCode) |onTakeLocalSnapshotResult(long taskId, IVideoSource videoSource, Bitmap image, int errorCode) |**Parameter changes**:<br><br>StreamIndex replaced by IVideoSource |
|onTakeRemoteSnapshotResult(long taskId, RemoteStreamKey streamKey, Bitmap image, int errorCode) |onTakeRemoteSnapshotResult(long taskId, String streamId, StreamInfo streamInfo, Bitmap image, int errorCode) |**Parameter changes**:<br><br>RemoteStreamKey replaced by streamId, streamInfo |
|onRemoteUserAudioFrame(RemoteStreamKey streamKey, IAudioFrame audioFrame) |onRemoteUserAudioFrame(String streamId, StreamInfo streamInfo, IAudioFrame audioFrame) |**Parameter changes**:<br><br>RemoteStreamKey replaced by streamId, streamInfo |
|onProcessRemoteUserAudioFrame(RemoteStreamKey streamKey, IAudioFrame audioFrame) |onProcessRemoteUserAudioFrame(String streamId, StreamInfo streamInfo, IAudioFrame audioFrame) |**Parameter changes**:<br><br>RemoteStreamKey replaced by streamId, streamInfo |
|onStart(StreamIndex index) |onStart(String streamId, StreamInfo streamInfo) |**Parameter changes**:<br><br>StreamIndex replaced by streamId, streamInfo |
|onStop(StreamIndex index) |onStop(String streamId, StreamInfo streamInfo) |**Parameter changes**:<br><br>StreamIndex replaced by streamId, streamInfo |
|onRateUpdate(StreamIndex streamIndex, int videoIndex, int fps, int bitrateKbps) |onRateUpdate(String streamId, StreamInfo streamInfo, int videoIndex, int fps, int bitrateKbps) |**Parameter changes**:<br><br>StreamIndex replaced by streamId, streamInfo |
|onRequestKeyFrame(StreamIndex streamIndex, int videoIndex) |onRequestKeyFrame(String streamId, StreamInfo streamInfo, int videoIndex) |**Parameter changes**:<br><br>StreamIndex replaced by streamId, streamInfo |
|onActiveVideoLayer(StreamIndex streamIndex, int videoIndex, boolean active) |onActiveVideoLayer(String streamId, StreamInfo streamInfo, int videoIndex, boolean active) |**Parameter changes**:<br><br>StreamIndex replaced by streamId, streamInfo |


<span id="2be9cfb2"></span>
## Type Changes

<span id="59d2a267"></span>
### Room Mode \- ChannelProfile


|**Modified Data Type** |V3.58 |V3.60 |Description |
|---|---|---|---|
|ChannelProfile |CHANNEL_PROFILE_CHAT(5)<br><br>CHANNEL_PROFILE_LW_TOGETHER(7) |CHANNEL_PROFILE_CALL(19) |Focuses on smoothness with relatively low default video bitrate, low audio quality requirements, and high smoothness requirements. |
||CHANNEL_PROFILE_GAME_HD(8)<br><br>CHANNEL_PROFILE_CO_HOST(9)<br><br>CHANNEL_PROFILE_KTV(11)<br><br>CHANNEL_PROFIEL_VR_CHAT(13)<br><br>CHANNEL_PROFILE_LAN_LIVE_STREAMING(15)<br><br>CHANNEL_PROFILE_LIVE_BROADCASTING(1) |CHANNEL_PROFILE_LIVE(20) |Focuses more on video quality with relatively high default video bitrate and high audio quality requirements. |


<span id="0fcb5161"></span>
### Video Frame Related


|Feature |V3.58 |V3.60 |Description |
|---|---|---|---|
|Video Frame Data |VideoFrame |VideoFrameData |1. **Type Rename**<br><br>2. **Parameter Changes**:<br><br>* **Parameter Renames**<br><br>   * getFrameType() changed to bufferType()<br><br>   * getTimeStampUS() changed to timestampUs()<br><br>   * getTextureID() changed to getTextureId<br><br>   * getExternalDataInfo() changed to getSeIData()<br><br>* **Parameter Deletions**<br><br>   * Removed getSupplementaryInfo()<br><br>   * Removed getColorSpace()<br><br>* **New Parameters**:<br><br>   * Added addRef()<br><br>   * Added releaseRef() |
|Local Video Frame Callback Configuration |LocalVideoRenderPosition |LocalVideoSinkPosition |* **Type Rename**<br><br>* **Default Value Change**: Changed from LocalVideoRenderPosition.AFTER_CAPTURE (before preprocessing) to LocalVideoSinkPosition.AFTER_PREPROCESS (after preprocessing). |
|*Remote Video Frame Callback Position* |RemoteVideoRenderPosition |RemoteVideoSinkPosition |Type rename |
|*Whether to Mirror Video Frames* |VideoRenderMirrorType |VideoSinkMirrorType |Enum rename |
|Build Texture Format Video Data Return Frame |GLTextureVideoFrameBuilder |/ |Removed, no replacement |
|Build CpuBuffer Video Frame |CpuBufferVideoFrameBuilder |/ |Removed, no replacement |


<span id="6605b0c1"></span>
### Mixed Stream Events


* Name replacement: `ByteRTCStreamMixingEvent` changed to `MixedStreamTaskEvent`, sharing the same event enum class with WTN stream tasks.

* Enum value changes are as follows:



|Description |V3.58 |V3.60 |
|---|---|---|
|Request to start task<br><br>Stream push success |STREAM_MIXING_START(1)<br><br>STREAM_MIXING_START_SUCCESS(2) |START_SUCCESS(1) |
|Task start failed |STREAM_MIXING_START_FAILED(3) |START_FAILED(2)<br><br>See MixedStreamTaskErrorCode for specific failure reasons |
|Request update<br><br>Task update success |STREAM_MIXING_UPDATE(4)<br><br>STREAM_MIXING_UPDATE_SUCCESS(5) |UPDATE_SUCCESS(3) |
|Task update failed |STREAM_MIXING_UPDATE_FAILED(6) |UPDATE_FAILED(4)<br><br>See MixedStreamTaskErrorCode for specific failure reasons |
|Request to end task<br><br>Task end success |STREAM_MIXING_STOP(7)<br><br>STREAM_MIXING_STOP_SUCCESS(8) |STOP_SUCCESS(5) |
|Task end failed |STREAM_MIXING_STOP_FAILED(9) |STOP_FAILED(6)<br><br>See MixedStreamTaskErrorCode for specific failure reasons |
|Parameter error |STREAM_MIXING_REQUEST_PARAM_ERROR(15) |Returns RETURN_STATUS_PARAMETER_ERR = \-2 when calling startPushMixedStream or updatePushMixedStream |
|Task processing timeout, check network status and retry |STREAM_MIXING_UPDATE_TIMEOUT(13)<br><br>STREAM_MIXING_START_TIMEOUT(14) |Returns TIMEOUT(1091) when calling startPushMixedStream or updatePushMixedStream |
|Mixed stream add image |STREAM_MIXING_MIX_IMAGE_EVENT(16) |WARNING(7)<br><br>See MixedStreamTaskErrorCode for specific failure reasons |
|Warning event |None |WARNING(7) |
|Others |STREAM_MIXING_FIRST_AUDIO_FRAME_BY_CLIENT_MIX(11)<br><br>STREAM_MIXING_FIRST_VIDEO_FRAME_BY_CLIENT_MIX(12)<br><br>STREAM_MIXING_CHANGE_MIX_TYPE(10) |Removed |


<span id="98395edd"></span>
### Single Stream Push Events


* Name change: Changed from `ByteRTCStreamSinglePushEvent` to `SingleStreamTaskEvent`.

* Specific enum value changes are as follows:



|Description |V3.58 |V3.60 |
|---|---|---|
|Start stream push |SINGLE_STREAM_PUSH_START = 1 |START_SUCCESS = 1 |
|Stream push success |SINGLE_STREAM_PUSH_SUCCESS = 2 |START_SUCCESS = 1 |
|Stream push failed |SINGLE_STREAM_PUSH_FAILED = 3 |START_FAILED = 2 |
|Stop stream push |SINGLE_STREAM_PUSH_STOP = 4 |STOP_SUCCESS = 3 |
|Single stream transcoding live task processing timeout, check network status and retry |SINGLE_STREAM_PUSH_TIMEOUT = 5 |WARNING = 5, see SingleStreamTaskErrorCode for specific error information. |
|Parameter error |SINGLE_STREAM_PUSH_PARAM_ERROR = 6 |Returns RETURN_STATUS_PARAMETER_ERR = \-2 when calling startPushSingleStream. |
|Stop stream push failed |None |STOP_FAILED = 4 |


<span id="23487877"></span>
### Audio and Video Stream Statistics


|Feature |Modified Data Type |Description |
|---|---|---|
|Local Audio Stream Statistics |LocalAudioStats |Added fields:<br><br><br>* `audioDeviceLoopDelay`: Audio capture and playback delay<br><br>* `encodeFrameRate`: Audio encoding frame rate |
|Remote Audio Stream Statistics |RemoteAudioStats |Added field:<br><br>`decodeFrameRate`: Audio decoding frame rate |
|Remote Video Stream Statistics |RemoteVideoStats |Added fields:<br><br><br>* `capToRenderDelay`: Delay from sender capture start to receiver rendering completion<br><br>* `avSyncDiffMs`: Audio\-video synchronization difference<br><br>* `codecElapsePerFrame`: Average video decoding time per frame |


<span id="830fae3d"></span>
### Others


|Feature |Modified Data Type |Description |
|---|---|---|
|Screenshot Error Code |SnapshotErrorCode |**New class** |
|Audio Scenario Type |AudioScenarioType |**Added enum values:** <br><br>EDUCATION (4, Education scenario. Suitable for high\-quality scenarios mainly focused on voice teaching content.)<br><br>AICLIENT (5, AI conversation scenario. Suitable for scenarios where real people interact with AI agents.) |
|Voice Reverb Type |VoiceReverbType |**Added enum values:** <br><br>The following four reverb effects:<br><br>Enhance Original (VOICE_REVERB_ENHANCE_ORIGINAL),<br><br>Bathroom (VOICE_REVERB_BATHROOM),<br><br>Natural (VOICE_REVERB_NATURAL),<br><br>Hallway (VOICE_REVERB_HALLWAY) |
|Login Error Code |LoginErrorCode |**Added error code:** <br><br>Added login error code \-1004, representing current restricted mode<br><br>Using RTS capabilities in restricted mode has the following limitations:<br><br>Supports in\-room broadcast and point\-to\-point;<br><br>Message sending rate does not exceed 30KB/second;<br><br>Message sending frequency does not exceed 60 packets/second;<br><br>Message packet length does not exceed 1KB;<br><br>Switching between restricted/unrestricted modes requires configuration in the Volcano console. |
|Single Stream Task Error Code |SingleStreamTaskErrorCode |**Added enum values:** <br><br>Added the following error codes:<br><br>Server detects invalid task parameters (1093, INVALID_PARAM_BY_SERVER)<br><br>Transcoding task user ID kicked out of target room (1094, REMOTE_KICKED)<br><br>Transcoding task failed to join target room (1095, JOIN_DEST_ROOM_FAIED)<br><br>Transcoding task stream pulling timeout in source room (1096, RECEIVE_SRC_STREAM_TIMEOUT)<br><br>Audio/video encoding transcoding task not supported (1097, NOT_SURPORT_CODEC) |
|Single Stream Push Target Room Configuration |DestInfo |**New class** |
|Single Stream Push Type |SingleStreamPushType |**New class** |
|Single Stream Push Live Configuration Parameters |PushSingleStreamParam |**Added members:** <br><br>Added to single stream push live configuration parameters: target room information list (destInfos), push type (pushType) |
|Mirror Type Enum |MirrorType |**Added enum value:** <br><br>No mirror effect during local preview, mirror effect only during encoding transmission (2, kMirrorTypeEncoder) |
|Publish State Change Reason |PublishStateChangeReason |**New class** |


<span id="fc298036"></span>
## Error Code Changes

<span id="8ad4399f"></span>
### Callback Warning \- WarningCode


|V3.58 |V3.60 |
|---|---|
|WARNING_CODE_OLD_ROOM_BEEN_REPLACED = \-2016<br><br>Room with the same roomId already exists, newly created room instance has replaced the old room instance |**Removed**:<br><br>When creating a room again with the same roomId, the previously created room instance will be returned, and this error code will no longer be triggered. |


<span id="1ea79d29"></span>
### WTN Stream Error Codes (formerly Public Stream)


* Error code name change: `PublicStreamErrorCode` changed to `MixedStreamTaskErrorCode`, sharing the same enum class with mixed stream transcoding tasks.

* Specific error code change details are as follows:



|Description |V3.58 |V3.60 |
|---|---|---|
|Success |ERROR_CODE_SUCCESS = 0 |OK = 0 |
|Server parameter validation failed |ERROR_CODE_PUSH_PARAM_ERROR = 1191 |Deleted, this type of error will not be called back. |
|Server internal error |ERROR_CODE_PUSH_STATE_ERROR = 1192 |Deleted, this type of error will not be called back. |
|Server unknown error |ERROR_CODE_PUSH_INTERNAL_ERROR = 1193 |Deleted, this type of error will not be called back. |
|Task failed |ERROR_CODE_PUSH_ERROR = 1195 |PUSH_WTN_FAILED = 1105 |
|Task timeout |ERROR_CODE_PUSH_TIMEOUT = 1196 |TIMEOUT = 1091 |
|Stream subscription timeout |ERROR_CODE_PULL_NO_PUSH_STREAM = 1300 |WTNSubscribeStateChangeReason.UNSUBSCRIBE(1300), returned through onWTNVideoSubscribeStateChanged or onWTNAudioSubscribeStateChanged. |


<span id="2fc44f2b"></span>
### Mixed Stream Transcoding Error Codes


* Error code name change: `ByteRTCTranscoderErrorCode` changed to `MixedStreamTaskErrorCode`, sharing the same enum class with WTN stream tasks.

* Specific error code change details are as follows:



|Description |V3.58 |V3.60 |
|---|---|---|
|Push stream success |TRANSCODER_ERROR_OK = 0 |OK = 0 |
|Undefined mixed stream error |TRANSCODER_ERROR_BASE = 1090 |None, this error code is not enabled. |
|Client SDK detected invalid push stream parameters |TRANSCODER_ERROR_INVALID_PARAM = 1091 |Returns RETURN_STATUS_PARAMETER_ERR = \-2 when calling startPushMixedStream or updatePushMixedStream. |
|State error, operation needs to be initiated under normal state machine conditions |TRANSCODER_ERROR_INVALID_STATE = 1092 |INVALID_STATE_BY_SERVER = 1094 |
|Invalid operation |TRANSCODER_ERROR_INVALID_OPERATOR = 1093 |INVALID_STATE_BY_SERVER = 1094 |
|Transcoding live task processing timeout, check network status and retry |TRANSCODER_ERROR_TIMEOUT = 1094 |TIMEOUT = 1091 |
|Server detected incorrect push stream parameters |TRANSCODER_ERROR_INVALID_PARAM_BY_SERVER = 1095 |INVALID_PARAM_BY_SERVER = 1092 |
|Stream subscription timeout |TRANSCODER_ERROR_SUB_TIMEOUT_BY_SERVER = 1096 |SUB_TIMEOUT_BY_SERVER = 1093 |
|Mixed stream server internal error |TRANSCODER_ERROR_INVALID_STATE_BY_SERVER = 1097 |INVALID_STATE_BY_SERVER = 1094 |
|Mixed stream server push to CDN failed |TRANSCODER_ERROR_AUTHENTICATION_BY_CDN = 1098 |AUTHENTICATION_BY_CDN = 1095 |
|Server received signaling timeout, check network status and retry |TRANSCODER_ERROR_TIMEOUT_BY_SIGNALING = 1099 |SIGNAL_REQUEST_TIMEOUT = 1097 |
|Image mixed stream failed |TRANSCODER_ERROR_MIX_IMAGE_FAIL = 1100 |MIX_IMAGE_FAIL = 1098 |
|Server unknown error |TRANSCODER_ERROR_UNKNOW_ERROR_BY_SERVER = 1101 |UNKNOWN_BY_SERVER = 1096 |


<span id="d651888d"></span>
### Single Stream Push Error Codes


* Error code replacement: Replaced `StreamMixingErrorCode` with `SingleStreamTaskErrorCode`.

* Specific error code changes and corresponding details are as follows:



|Description |V3.58 |V3.60 |
|---|---|---|
|Push stream success |TRANSCODER_ERROR_OK = 0 |OK = 0 |
|Undefined mixed stream error |TRANSCODER_ERROR_BASE = 1090 |None, this error code is not enabled. |
|Client SDK detected invalid push stream parameters |TRANSCODER_ERROR_INVALID_PARAM = 1091 |Returns RETURN_STATUS_PARAMETER_ERR = \-2 when calling startPushSingleStream. |
|State error, operation needs to be initiated under normal state machine conditions |TRANSCODER_ERROR_INVALID_STATE = 1092 |None, single stream tasks will not trigger this error code. |
|Invalid operation |TRANSCODER_ERROR_INVALID_OPERATOR = 1093 |None, single stream tasks will not trigger this error code. |
|Transcoding live task processing timeout, check network status and retry |TRANSCODER_ERROR_TIMEOUT = 1094 |None, single stream tasks will not trigger this error code. |
|Server detected incorrect push stream parameters |TRANSCODER_ERROR_INVALID_PARAM_BY_SERVER = 1095 |None, single stream tasks will not trigger this error code. |
|Stream subscription timeout |TRANSCODER_ERROR_SUB_TIMEOUT_BY_SERVER = 1096 |None, single stream tasks will not trigger this error code. |
|Mixed stream server internal error |TRANSCODER_ERROR_INVALID_STATE_BY_SERVER = 1097 |None, single stream tasks will not trigger this error code. |
|Mixed stream server push to CDN failed |TRANSCODER_ERROR_AUTHENTICATION_BY_CDN = 1098 |None, single stream tasks will not trigger this error code. |
|Server received signaling timeout, check network status and retry |TRANSCODER_ERROR_TIMEOUT_BY_SIGNALING = 1099 |SIGNAL_REQUEST_TIMEOUT = 1092 |
|Image mixed stream failed |TRANSCODER_ERROR_MIX_IMAGE_FAIL = 1100 |None, single stream tasks will not trigger this error code. |
|Server unknown error |TRANSCODER_ERROR_UNKNOW_ERROR_BY_SERVER = 1101 |UNKNOWN_BY_SERVER = 1091 |


<span id="96e39988"></span>
### Other Error Codes

Removed some error codes that have been deprecated for multiple versions


|Description |Error Code |
|---|---|
|This warning is triggered when attempting to publish a stream after setting self visibility to false. |*WARNING_CODE_SUBSCRIBE_STREAM_FORBIDEN =*  \-2010 |
|This warning is triggered when attempting to enable manual subscription mode while automatic subscription mode is not turned off. |WARNING_CODE_GET_ROOM_FAILED = \-2000 |


<span id="26a5b5b2"></span>
## New Interfaces


|Interface |Feature Description |
|---|---|
|setEarMonitorMode |Ear monitoring supports reusing locally captured audio after custom processing.<br><br>> If hardware ear monitoring is enabled, the filter parameter of this interface is invalid. |
|setStreamExtraInfo |Set additional information for the current push stream |
|getCallId |Get call ID, the ID obtained after each room entry is brand new |
|setWTNStreamEventHandler |Set WTN stream callback interface |
|takeLocalSnapshotToFile |Capture local video stream frame, generate JPG file, and save to specified local path |
|takeRemoteSnapshotToFile |Capture remote video stream frame, generate JPG file, and save to specified local path |
|onLocalSnapshotTakenToFile |Local video stream frame capture callback |
|onRemoteSnapshotTakenToFile |Remote video stream frame capture callback |
|onRoomEvent |Room event callback, with new enum RoomEventInfo added |
|onRemoteEncodedAudioFrame(String streamId, StreamInfo streamInfo, EncodedAudioFrameData audioStream) |After calling registerRemoteEncodedAudioFrameObserver, this event is called back when the SDK receives remote audio frame information |
|onRoomStreamExtraInfoUpdate(String streamId, StreamInfo streamInfo, String extraInfo) |Callback for set stream additional information |
|createGameRTCRoom |Create game room |
|GameRTCRoom.destroy |Destroy game room |
|GameRTCRoom.setRTCRoomEventHandler |Set the event handler for the GameRTCRoom object to listen for callback events corresponding to this object |
|GameRTCRoom.joinRoom |Join game room |
|GameRTCRoom.leaveRoom |Leave game room |
|GameRTCRoom.getRangeAudio |Return IRangeAudioIRangeAudio instance |
|GameRTCRoom.updateToken |Update Token |
|GameRTCRoom.enableMicrophone |Enable or disable microphone |
|GameRTCRoom.enableSpeakerphone |Enable or disable speakerphone |
|GameRTCRoom.enableAudioSend |Send or cancel sending audio stream |
|GameRTCRoom.enableAudioReceive |Whether to receive audio stream from specified user |
|GameRTCRoom.setRemoteRoomAudioPlaybackVolume |Adjust the audio playback volume of all remote users in a room |


<span id="1ffbe145"></span>
## Deleted/Deprecated Interfaces

Removed deprecated or not recommended methods, as follows:


|Change Details |Deleted/Deprecated Interface |Alternative Interface |
|---|---|---|
|Deprecated |setLocalVideoSink(StreamIndex index, IVideoSink videoSink, @IVideoSink.PixelFormat int requiredFormat) |setLocalVideoSink(IVideoSink videoSink, LocalVideoSinkConfig config) |
|Deprecated |setRemoteVideoSink(RemoteStreamKey streamKey, IVideoSink videoSink, @IVideoSink.PixelFormat int requiredFormat) |setRemoteVideoSink(String streamId, IVideoSink videoSink, @IVideoSink.PixelFormat int requiredFormat) |
|Deleted |createRTCVideo(Context context, String appId, IRTCVideoEventHandler handler, Object eglContext, JSONObject parameters) |createRTCEngine(EngineConfig config, IRTCEngineEventHandler handler) |
|Deleted |getErrorDescription |No alternative interface |
|Deleted |* startASR<br><br>* stopASR |No alternative interface<br><br>If you need to use ASR functionality, you can implement it through real\-time subtitle related interfaces: startSubtitle, stopSubtitle |
|Deleted |* onSuccessonMessage(String message)<br><br>* onError(int errorCode, String errorMessage) |If you need to use ASR functionality, you can implement it through real\-time subtitle related interfaces: onSubtitleStateChanged, onSubtitleMessageReceived |
|Deleted |onGLEnvInitiated |No alternative interface<br><br>You need to control initialization operations based on video frame callbacks |
|Deleted |onGLEnvRelease |No alternative interface<br><br>You need to control destruction operations based on video frame callbacks |
|Deleted |subscribeUserStream(String uid, StreamIndex streamType, SubscribeMediaType mediaType, SubscribeVideoConfig subscribeVideoConfig); |subscribeStreamVideo(String streamId, boolean subscribe)<br><br>subscribeStreamAudio(String streamId, boolean subscribe) |
|Deleted |setDeviceId(String deviceId) |No alternative interface |
|Deleted |replaceBackground(BackgroundMode mode, DivideModel divideModel) |No alternative interface |
|Deleted |setAudioPlaybackDevice(AudioPlaybackDevice audioPlaybackDevice) |setDefaultAudioRoute(AudioRoute route) |
|Deleted |pushExternalVideoFrame(VideoFrame frame, boolean isDirectEncode) |No alternative interface |
|Deleted |1. startLiveTranscoding(String taskId, LiveTranscoding liveTranscode, ILiveTranscodingObserver observer)<br><br>2. stopLiveTranscoding(String taskId)<br><br>3. updateLiveTranscoding(String taskId, LiveTranscoding transcoding) |1. startPushMixedStream(String taskId, MixedStreamPushTargetConfig pushTargetConfig, MixedStreamConfig mixedConfig)<br><br>2. stopPushMixedStream(String taskId, MixedStreamPushTargetType targetType)<br><br>3. updatePushMixedStream(String taskId, MixedStreamPushTargetConfig pushTargetConfig, MixedStreamConfig mixedConfig) |
|Deleted |setOnDestroyCompletedCallback(Runnable callback) |No alternative interface |
|Deleted |1. checkVideoEffectLicense(Context context , String licenseFile)<br><br>2. setVideoEffectAlgoModelPath(String modelPath)<br><br>3. enableVideoEffect(boolean enable)<br><br>4. setVideoEffectNodes(ListeffectNodes)<br><br>5. updateVideoEffectNode(String effectNode, String key, float value)<br><br>6. setBackgroundSticker(String modelPath, VirtualBackgroundSource source)<br><br>7. setVideoEffectColorFilter(String resFile)<br><br>8. setVideoEffectColorFilterIntensity(float intensity)<br><br>9. registerFaceDetectionObserver(IFaceDetectionObserver observer, int interval) |1. IVideoEffect.initCVResource(String licenseFile, String algoModelDir)<br><br>2. IVideoEffect.initCVResource(String licenseFile, String algoModelDir)<br><br>3. IVideoEffect.enableVideoEffect()<br><br>4. IVideoEffect.setEffectNodes(ListeffectNodes)<br><br>5. IVideoEffect.updateEffectNode(String effectNode, String key, float value)<br><br>6. IVideoEffect.enableVirtualBackground(String backgroundStickerRes, VirtualBackgroundSource source)<br><br>7. IVideoEffect.setColorFilter(String filterRes)<br><br>8. IVideoEffect.setColorFilterIntensity(float intensity)<br><br>9. IVideoEffect.enableFaceDetection(IFaceDetectionObserver observer, int interval_ms, String face_model_path) |
|Deleted |IAudioMixingManager |IMediaPlayer<br><br>IAudioEffectPlayer |
|Deleted |muteAudioPlayback(MuteState muteState) |setPlaybackVolume(int volume) |
|Deleted |1. ISpatialAudio.updatePosition(Position pos)<br><br>2. ISpatialAudio.updateSelfOrientation(HumanOrientation orientation)<br><br>3. ISpatialAudio.updateListenerPosition(Position pos)<br><br>4. ISpatialAudio.updateListenerOrientation(HumanOrientation orientation) |1. ISpatialAudio.updateSelfPosition(PositionInfo positionInfo)<br><br>2. ISpatialAudio.updateSelfPosition(PositionInfo positionInfo)<br><br>3. ISpatialAudio.updateRemotePosition(String uid,PositionInfo positionInfo)<br><br>4. ISpatialAudio.updateRemotePosition(String uid,PositionInfo positionInfo) |
|Deleted |IRTCRoomEventHandler.onRoomError(int err) |* IRTCRoomEventHandler.onRoomStateChanged(String roomId, String uid, int state, String extraInfo)<br><br>* IRTCRoomEventHandler.onStreamStateChanged(String roomId, String uid, int state, String extraInfo) |
|Deleted |1. onUserMuteAudio(String roomId, String uid, MuteState muteState)<br><br>2. onUserMuteVideo(String roomId, String uid, MuteState muteState)<br><br>3. onAudioPlaybackDeviceChanged(AudioPlaybackDevice device)<br><br>4. onMediaDeviceStateChanged(String deviceID, int deviceType, int deviceState, int deviceError)<br><br>5. onMediaDeviceWarning(String deviceID, int deviceType, int deviceWarning)<br><br>6. onHttpProxyState(int state)<br><br>7. onSocks5ProxyState(int state, String cmd, String proxyAddress, String localAddress, String remoteAddress)<br><br>8. onAudioMixingStateChanged(int mixId, AudioMixingState state, AudioMixingError error) |1. onUserPublishStreamAudio(String streamId, StreamInfo streamInfo, boolean isPublish)<br><br>2. onUserPublishStreamVideo(String streamId, StreamInfo streamInfo, boolean isPublish)<br><br>3. onAudioRouteChanged(AudioRoute route)<br><br>4. onAudioDeviceStateChanged(String deviceID, AudioDeviceType deviceType, int deviceState, int deviceError)<br><br>   onVideoDeviceStateChanged(String deviceID, VideoDeviceType deviceType, int deviceState, int deviceError)<br><br>5. onAudioDeviceWarning(String deviceID, AudioDeviceType deviceType, int deviceWarning)<br><br>   onVideoDeviceWarning(String deviceID, VideoDeviceType deviceType, int deviceWarning)<br><br>6. onLocalProxyStateChanged(LocalProxyType localProxyType, LocalProxyState localProxyState, LocalProxyError localProxyError)<br><br>7. onLocalProxyStateChanged(LocalProxyType localProxyType, LocalProxyState localProxyState, LocalProxyError localProxyError)<br><br>8. IMediaPlayerEventHandler.onMediaPlayerStateChanged(int playerId, PlayerState state, PlayerError error)<br><br>   IAudioEffectPlayerEventHandler.onAudioEffectPlayerStateChanged(int effectId, PlayerState state, PlayerError error) |
|Deleted |1. ILiveTranscodingObserver interface and all methods defined by it<br><br>2. LiveTranscoding class and all variables, constants, and methods defined by it |1. IMixedStreamObserver interface and all methods defined by it<br><br>2. MixedStreamConfig class and all variables, constants, and methods defined by it |
|Deleted |* The following methods defined by RTCEngine (formerly RTCVideo) class:<br><br>   * setScreenAudioSourceType(AudioSourceType sourceType)<br><br>   * pushScreenVideoFrame(VideoFrame videoFrame)<br><br>* The following callbacks defined by IRTCRoomEventHandler class:<br><br>   * onExternalScreenFrameUpdate(FrameUpdateInfo info) |No alternative interface, screen streaming in this version does not support setting external source data |


<span id="_3-58"></span>
# 3.58

<span id="important-notes"></span>
## Important Notes


1. Starting from version 3.57, the RTC SDK supports dynamic loading of `.so` files other than the main library. The structure of the SDK offline package has changed. Please refer to the updated [Manual SDK Integration](https://docs.byteplus.com/en/docs/12/docs-70134) guide.

   The SDK provides a `nativeLoadPath` property in the `EngineConfig` class, which supports dynamically loading the required `.so` files from a specified private directory during App runtime, thereby reducing the size of the App's installation package. For dynamic loading of `.so` files, see [Integrate Plugins on Demand to Reduce the Size of the Application](https://docs.byteplus.com/docs/byteplus-rtc/1108726).

2. This version provides the SAMI audio technology dynamic library plugin. For details, see [Integrate Plugins on Demand to Reduce the Size of the Application](https://docs.byteplus.com/docs/byteplus-rtc/1108726).

3. This version has unified all non\-standard API namings to improve code standardization and usability. The following are just examples of changes. Please refer to [Type Details](https://docs.byteplus.com/en/docs/12/docs-70083) for specific modifications to the types used.

   
   |Change Object |Change Details |Old Version Example |New Version Example |
   |---|---|---|---|
   |Enum Values |* Remove prefixes/suffixes<br><br>* Change to all uppercase letters, separated by underscores |For example, `SubscribeMediaType`:<br><br><br>* RTC_SUBSCRIBE_MEDIA_TYPE_NONE(0),<br><br>* RTC_SUBSCRIBE_MEDIA_TYPE_AUDIO_ONLY(1),<br><br>* RTC_SUBSCRIBE_MEDIA_TYPE_VIDEO_ONLY(2),<br><br>* RTC_SUBSCRIBE_MEDIA_TYPE_AUDIO_AND_VIDEO(3); |For example, `SubscribeMediaType`:<br><br><br>* NONE(0),<br><br>* AUDIO_ONLY(1),<br><br>* VIDEO_ONLY(2),<br><br>* AUDIO_AND_VIDEO(3); |
   |Struct Members |Change to lowercase initial letter, camel case identification |For example, `AudioPropertiesConfig`:<br><br><br>* interval;<br><br>* enable_spectrum;<br><br>* enable_vad;<br><br>* local_main_report_mode;<br><br>* audio_report_mode;<br><br>* smooth; |For example, `AudioPropertiesConfig`:<br><br><br>* interval;<br><br>* enableSpectrum;<br><br>* enableVad;<br><br>* localMainReportMode;<br><br>* audioReportMode;<br><br>* smooth; |
   


<span id="api-changes"></span>
## API Changes


|Change Details |Functional Module |Deprecated Class/Interface |Replacement Class/Interface |Notes |
|---|---|---|---|---|
|Removed |Main Class |`RTCEngine` |`RTCVideo` | |
|Removed |Engine Management |`RTCVideo.setEnv` |`RTCVideo.setRuntimeParameters` |For more information, please contact technical support. |
|Expanded Usage Range |Video Processing |`setVideoDecoderConfig` |`setVideoDecoderConfig` |The old interface only supported manual subscription, and the new one also supports automatic subscription. |
|Deprecated |Video Management |`public abstract int updateRemoteStreamVideoCanvas(RemoteStreamKey streamKey, int renderMode, int backgroundColor);` |`public abstract int updateRemoteStreamVideoCanvas(RemoteStreamKey streamKey, RemoteVideoRenderConfig remoteVideoRenderConfig);` |The new interface unifies the rendering mode and background color settings through the `remoteVideoRenderConfig` parameter. Additionally, a new parameter `renderRotation` is added to support setting the rotation angle of the video frame. |
|Removed |Audio Processing |`IAudioProcessor` |`IAudioFrameProcessor` |`IAudioProcessor` was deprecated in version 3.42 and has been removed in this version. |
|New Member Variable in Parameter Data Structure |Audio Management |`enableAudioPropertiesReport` |`enableAudioPropertiesReport` |A new parameter `enableVoicePitch` is added to control whether to callback the fundamental frequency of the local user's voice. |


<span id="callback-changes"></span>
## Callback Changes


|Change Details |Functional Module |Deprecated Class/Interface |Replacement Class/Interface |Notes |
|---|---|---|---|---|
|Removed |Main Callback Class |`IRTCEngineEventHandler` |`IRTCVideoEventHandler` | |
|Parameter Change |Message |`virtual void onLogout()` |`virtual void onLogout(int reason)` |A new `reason` parameter has been added to the `onLogout` callback to distinguish between voluntary and involuntary logouts by the user. For specific parameter types, refer to `LogoutReason`. |
|New Member Variable in Parameter Data Structure |Audio Management |`onLocalAudioPropertiesReport` |`onLocalAudioPropertiesReport` |A new parameter `voicePitch` has been added to return the fundamental frequency of the local user's voice. |


<span id="type-changes"></span>
## Type Changes


|Change Details |Functional Module |Changed Data Type |Notes |
|---|---|---|---|
|New Enum Value Added |Audio Effects |`PlayerState` | |
|New Member Variable Added |Subtitle Translation Service |`SubtitleMessage` |New member variables `language` and `mode` have been added to the `SubtitleMessage` parameter in the subtitle content callback `onSubtitleMessageReceived`, which can be used to receive both the original and translated subtitle text simultaneously. |
|Member Variable Change |CDN Live Streaming |`MixedStreamLayoutRegionConfig` |The live streaming of individual user images in the push stream has changed from setting a normalized ratio relative to the overall image to setting an absolute pixel value. |


<span id="_3-56"></span>
# 3.56

<span id="sdk-integration"></span>
## SDK Integration

A new plugin named `libbytertc_ffmpeg_audio_extension.so` is added into `BytePlusRTC-Release.aar` in this version, which supports functionality of playback from memory and enables decoding of audio files in various formats including mp3, mp4, aac, m4a, 3gp, wav, ogg, ts, and wma. After integrating this plugin, the app's size will increase by 1.3MB for the arm64\-v8a architecture and 1.1MB for the armeabi\-v7a architecture. This plugin is optional, and if there is no need for its use, it can be removed after integrating the `BytePlusRTC-Release.aar`. Refer to Integrate the Android SDK using Maven for specific instructions.

<span id="api"></span>
## API

This version adds a return value for all APIs, through which the failed API call can be clearly identified and the cause of the failure can be located. For the meaning of the specific return value, refer to each API comment.

Other API changes:


|Type |Function Module |Previous |Current |Notes |
|---|---|---|---|---|
|Deprecated and replaced |Audio Mixing |* `getAudioMixingManager`<br><br>* `IAudioMixingManager` |* `getAudioEffectPlayer`<br><br>* `IAudioEffectPlayer`<br><br>* `getMediaPlayer`<br><br>* `IMediaPlayer` |This version splits the audio mixing class into audio effect management class and music management class.<br><br>Generally, for audio effect less than 20 seconds, use audio effect class; for audio files longer than 20 seconds or PCM data, use music management class.<br><br>See the comparison table for the API mapping between deprecated API and new API. |
|Deleted |Audio Processing |`IAudioProcessor` |`IAudioFrameProcessor` |`IAudioProcessor` was deprecated in 3.45, and is deleted in 3.56. |
|Modified |Audio Management |`enableAudioPropertiesReport` |`enableAudioPropertiesReport` |Adds `enableVoicePitch` to control whether to return the vocal pitch of local users. |
|Modified |Video Processing |`setVideoDecoderConfig` |`setVideoDecoderConfig` |Previously, it was only supported with manual subscription, but now it is also supported with automatic subscription. |
|Deprecated |Video Management |`public abstract int updateRemoteStreamVideoCanvas(RemoteStreamKey streamKey, int renderMode, int backgroundColor);` |`public abstract int updateRemoteStreamVideoCanvas(RemoteStreamKey streamKey, RemoteVideoRenderConfig remoteVideoRenderConfig);` |With the new API, you can set both the render mode and the background color through the "remoteVideoRenderConfig" parameter. In addition, another parameter "renderRotation" is added allowing you to set the rotation angle of the remote video frame. |


 &nbsp;

API mapping in audio mixing module:


|Categories |Use |Deprecated APIs, callbacks, classes |New APIs, callbacks, classes (Audio Effect) |New APIs, callbacks, classes (Media) |Notes |
|---|---|---|---|---|---|
|Get instance |Get player instances |getAudioMixingManager |getAudioEffectPlayer |getAudioMediaManager | |
|Class | |IAudioMixingManager |IAudioEffectPlayer |IMediaPlayer | |
|API |Load music files to memory |* preloadAudioMixing<br><br>* unloadAudioMixing |* preload<br><br>* unload<br><br>* unloadAll |* open<br><br>* openWithCustomSource | |
|API |Start, Stop, Pause, Resume |* startAudioMixing<br><br>* stopAudioMixing<br><br>* stopAllAudioMixing<br><br>* pauseAudioMixing<br><br>* pauseAllAudioMixing<br><br>* resumeAudioMixing<br><br>* resumeAllAudioMixing |* start<br><br>* stop<br><br>* stopAll<br><br>* pause<br><br>* pauseAll<br><br>* resume<br><br>* resumeAll |* start<br><br>* stop<br><br>* stopAll<br><br>* pause<br><br>* resume | |
|API |Get / Set position |* setAudioMixingPosition<br><br>* getAudioMixingCurrentPosition<br><br>* getAudioMixingDuration |* setPosition<br><br>* getPosition<br><br>* getDuration |* setPosition<br><br>* getTotalDuration<br><br>* getPlaybackDuration | |
|API |Get / Set volume |* setAudioMixingVolume<br><br>* NA |* setVolume<br><br>* getVolume |* setVolume<br><br>* getVolume | |
|API |Adjust pitch |setAudioMixingPitch |NA |setAudioPitch | |
|API |Set mono mode |setAudioMixingDualMonoMode |NA |setAudioDualMonoMode | |
|API |Get / Set audio tracks |* getAudioTrackCount<br><br>* selectAudioTrack |NA |* getAudioTrackCount<br><br>* selectAudioTrack |The index in the new API starts from 0 instead of 1. |
|API |Set playback speed |setAudioMixingPlaybackSpeed |NA |setPlaybackSpeed | |
|API |Set playback callback progress callback |setAudioMixingProgressInterval |NA |setProgressInterval | |
|API |Set loudness |setAudioMixingLoudness |NA |setLoudness | |
|API |Use external audio source |* enableAudioMixingFrame<br><br>* disableAudioMixingFrame<br><br>* pushAudioMixingFrame |NA |* openWithCustomSource<br><br>* pushExternalAudioFrame | |
|Callback |Progress callback |onAudioMixingStateChanged |* setEventHandler<br><br>* onAudioEffectPlayerStateChanged |* setEventHandler<br><br>* onMediaPlayerStateChanged<br><br>* onMediaPlayerPlayingProgress | |
|Callback |Audio data callback |* registerAudioFileFrameObserver<br><br>* onAudioFileFrame |NA |* IMediaPlayerAudioFrameObserver<br><br>* onFrame | |


<span id="callback"></span>
## Callback


|Type |Function Module |Previous |Current |Notes |
|---|---|---|---|---|
|Modified |Audio Management |`onLocalAudioPropertiesReport` |`onLocalAudioPropertiesReport` |Adds `voicePitch` to return the vocal pitch of local users. |
|Modified |Message |`virtual void onLogout()` |`virtual void onLogout(int reason)` |Adds a new parameter `reason` on `onLogout` to describe the reason why the user logs out. See `LogoutReason` for the details. |


<span id="_3-52"></span>
# 3.52

<span id="api"></span>
## API


|Type |Function Module |Previous |Current |Notes |
|---|---|---|---|---|
|Modified |Engine Management |`public abstract int feedback(List<ProblemFeedback> types, String problemDesc)` |`public abstract int feedback(List<ProblemFeedbackOption> types, ProblemFeedbackInfo info);` |The data types of the parameters are changed. |
|Modified |Advanced Features |`public abstract int startAudioRecording(AudioRecordingConfig config);` |`public abstract int startAudioRecording(AudioRecordingConfig config);` |In previous versions, this API only supports calling after joining a room. Since this version, this API can be called before and after entering the room. If you call it before joining the room, and the recording task will not stop automatically after checking out; if you call it after entering the room, and the recording task will stop automatically after checking out. |
|Replaced |Advanced Features |`int updatePosition(Position pos);`<br><br>`int updateSelfOrientation(HumanOrientation orientation);` |`int updateSelfPosition(PositionInfo positionInfo);` |The APIs used in the the spatial audio feature are replaced and the new API allows local users to set their own position and orientation in the rectangular coordinate system. |
|Replaced |Advanced Features |`int updateListenerPosition(Position pos);`<br><br>`int updateListenerOrientation(HumanOrientation orientation);` |`-int updateRemotePosition(String uid,PositionInfo positionInfo);` |The APIs used in the the spatial audio feature are replaced and the new API allows local users to set the position and orientation of remote users in the rectangular coordinate system. |
|Replaced |Push to CDN |`public abstract int startLiveTranscoding(String taskId, LiveTranscoding liveTranscode, ILiveTranscodingObserver observer);startLiveTranscoding` |`public abstract int startPushMixedStreamToCDN(String taskId, MixedStreamConfig mixedConfig, IMixedStreamObserver observer);` |The APIs used in the function of pushing mixed streams to CDN are renamed with the behavior logic remaining unchanged. See Keytype change for the correspondence between the old and new versions of the class name. |
|Replaced |Push to CDN |`public abstract int stopLiveTranscoding(String taskId);` |`public abstract int stopPushStreamToCDN(String taskId);` |The APIs used in the function of pushing mixed streams to CDN are renamed with the behavior logic remaining unchanged. See Keytype change for the correspondence between the old and new versions of the class name. |
|Replaced |Push to CDN |`public abstract int updateLiveTranscoding(String taskId, LiveTranscoding transcoding);` |`public abstract int updatePushMixedStreamToCDN(String taskId, MixedStreamConfig mixedConfig);` |The APIs used in the function of pushing mixed streams to CDN are renamed with the behavior logic remaining unchanged. See Keytype change for the correspondence between the old and new versions of the class name. |


<span id="keytype"></span>
## Keytype


|Type |Class |Previous |Current |Notes |
|---|---|---|---|---|
|Replaced |Top level class used in APIs for pushing mixed streams to CDN |`LiveTranscoding` |`MixedStreamConfig` |Some variable names/API names in the class are also changed. For specific changes, click the new class. |
|Replaced |Observer used in APIs for pushing mixed streams to CDN |`ILiveTranscodingObserver` |`IMixedStreamObserver` |To upgrade this version, you need to import com.ss.bytertc.engine.video.VideoFrame instead of org.webrtc.VideoFrame. |
|Replaced |The nested classes used in APIs for pushing mixed streams to CDN |`VideoConfig` |`MixedStreamVideoConfig` |Some variable names/API names in the class are also changed. For specific changes, click the new class. |
|Replaced |The nested classes used in APIs for pushing mixed streams to CDN |`AudioConfig` |`MixedStreamAudioConfig` |Some variable names/API names in the class are also changed. For specific changes, click the new class. |
|Replaced |The nested classes used in APIs for pushing mixed streams to CDN |`SpatialConfig` |`MixedStreamSpatialConfig` |Some variable names/API names in the class are also changed. For specific changes, click the new class. |
|Replaced |The nested classes used in APIs for pushing mixed streams to CDN |`ClientMixParam` |`MixedStreamClientMixConfig` |Some variable names/API names in the class are also changed. For specific changes, click the new class. |
|Replaced |The nested classes used in APIs for pushing mixed streams to CDN |`Region` |`MixedStreamLayoutRegionConfig` |Some variable names/API names in the class are also changed. For specific changes, click the new class. |
|Replaced |The nested classes used in APIs for pushing mixed streams to CDN |`Layout` |`MixedStreamLayoutConfig` |Some variable names/API names in the class are also changed. For specific changes, click the new class. |
|Replaced |Enum classes used in APIs for pushing mixed streams to CDN |`TranscoderClientMixVideoFormat` |`MixedStreamClientMixVideoFormat` |The names of values in each enumeration class are also changed. For specific changes, click the new class. |
|Replaced |Enum classes used in APIs for pushing mixed streams to CDN |`TranscoderContentControlType` |`MixedStreamMediaType` |The names of values in each enumeration class are also changed. For specific changes, click the new class. |
|Replaced |Enum classes used in APIs for pushing mixed streams to CDN |`TranscoderRenderMode` |`MixedStreamRenderMode` |The names of values in each enumeration class are also changed. For specific changes, click the new class. |
|Replaced |Enum classes used in APIs for pushing mixed streams to CDN |`TranscoderLayoutRegionType` |`MixedStreamLayoutRegionType` |The names of values in each enumeration class are also changed. For specific changes, click the new class. |
|Replaced |Enum classes used in APIs for pushing mixed streams to CDN |`AACProfile` |`MixedStreamAudioProfile` |The names of values in each enumeration class are also changed. For specific changes, click the new class. |
|Replaced |Enum classes used in APIs for pushing mixed streams to CDN |`VideoCodecType` |`MixedStreamVideoCodecType` |The names of values in each enumeration class are also changed. For specific changes, click the new class. |
|Replaced |Enum classes used in APIs for pushing mixed streams to CDN |`AudioCodecType` |`MixedStreamAudioCodecType` |The names of values in each enumeration class are also changed. For specific changes, click the new class. |
|Replaced |Enum classes used in APIs for pushing mixed streams to CDN |`ByteRTCStreamMixingType` |`MixedStreamType` |The names of values in each enumeration class are also changed. For specific changes, click the new class. |


<span id="error-code"></span>
## Error Code


1. Add new error codes: `ERROR_CODE_JOIN_ROOM_ROOM_FORBIDDEN=-1025` and `ERROR_CODE_JOIN_ROOM_USER_FORBIDDEN=-1026`. The client SDK receives the error code when the user is banned in a specific room by the RTC server and fails to join the room or is removed from the room.

2. `ERROR_CODE_OVER_SCREEN_PUBLISH_LIMIT=-1081` is deprecated and replaced by `ERROR_CODE_OVER_STREAM_PUBLISH_LIMIT=-1080`.


<span id="_3-50"></span>
# 3.50

<span id="api"></span>
## API


|Type |Function Module |Previous |Current |Notes |
|---|---|---|---|---|
|Return value change |Room management |`joinRoom` returns:<br><br><br>* `-1`: Invalid parameters.<br><br>* `-2`: Already in a room. |`joinRoom` returns:<br><br><br>* `-1`: Failure.<br><br>* `-2`: Invalid parameters.<br><br>* `-4`: Already in a room. |`0` continues to represent success. |
||Network management |`stopEchoTest` returns `-1` denoting failure due to no echo test is in progress. |`stopEchoTest` returns `-3` denoting failure due to no echo test is in progress. ||
||Engine management |`setBusinessId` returns:<br><br><br>* `< 0`: Failure. Refer to `BusinessCheckCode`。<br><br>* `-6001`: Already in a room.<br><br>* `-6002`: Invalid parameters. |`setBusinessId` returns:<br><br><br>* `< 0`: Failure. Refer to `ReturnStatus`<br><br>* `-2`: Invalid parameters. ||
|Modified |Screen sharing |`public abstract int setScreenVideoEncoderConfig(VideoEncoderConfig screen_solution);` |`public abstract int setScreenVideoEncoderConfig(ScreenVideoEncoderConfig screen_solution);` |The data type of the parameter changed to `ScreenVideoEncoderConfig`. |
|Modified |Screen sharing |* `setVideoSourceType` The screen video source defaults to external.<br><br>* `setScreenAudioSourceType` When the current setting is an internal source, and the capture is enabled, calling the API to switch to external source does not affect the internal capture.<br><br>* `startScreenCapture` When the current setting is an external source, calling the API enables the internal source, and starts capturing.<br><br>* `stopScreenCapture` When the current setting is an external source, calling the API disables the external capturing. |* `setVideoSourceType` The screen video source defaults to internal.<br><br>* `setScreenAudioSourceType` When the current setting is an internal source, and the capture is enabled, calling the API to switch to external source stops the internal capture as well.<br><br>* `startScreenCapture` When the current setting is an external source, calling the API to enable the internal source will fail and receive `onAudioDeviceWarning` or `onVideoDeviceWarning`.<br><br>* `stopScreenCapture` When the current setting is an external source, calling the API to enable the internal source will fail and receive `onAudioDeviceWarning` or `onVideoDeviceWarning`. |Align the behaviors of the screen\-sharing APIs with the video stream APIs. |
|Replaced |Custom Stream Processing |`registerVideoFrameObserver` |`setLocalVideoSink` | |
|Replaced |Video Processing |* `public abstract int checkVideoEffectLicense(Context context , String licenseFile);`<br><br>* `public abstract void setVideoEffectAlgoModelPath(String modelPath);` |`public abstract int initCVResource(String license_file, String algo_model_dir);` |* Moved from `RTCVideo` class to `IVideoEffect` class.<br><br>* Unified the return values. |
|Replaced |Video Processing |`public abstract int enableVideoEffect(boolean enable);` |* `public abstract int enableVideoEffect();`<br><br>* `public abstract int disableVideoEffect();` |* Moved from `RTCVideo` class to `IVideoEffect` class.<br><br>* Unified the return values. |
|Replaced |Video Processing |`public abstract int setVideoEffectNodes(List<String> effectNodes);` |`public abstract int setEffectNodes(List<String> effect_nodes);` |* Moved from `RTCVideo` class to `IVideoEffect` class.<br><br>* Unified the return values. |
|Replaced |Video Processing |`public abstract int updateVideoEffectNode(String effectNode, String key, float value);` |`public abstract int updateEffectNode(String effect_node, String key, float value);` |* Moved from `RTCVideo` class to `IVideoEffect` class.<br><br>* Unified the return values. |
|Replaced |Video Processing |`public abstract int setBackgroundSticker(String modelPath, VirtualBackgroundSource source);` |* `public abstract int enableVirtualBackground(String bg_sticker_res, VirtualBackgroundSource source);`<br><br>* `public abstract int disableVirtualBackground();` |* Moved from `RTCVideo` class to `IVideoEffect` class.<br><br>* Unified the return values. |
|Replaced |Video Processing |`public abstract int setVideoEffectColorFilter(String resFile);` |`public abstract int setColorFilter(String filter_res);` |* Moved from `RTCVideo` class to `IVideoEffect` class.<br><br>* Unified the return values. |
|Replaced |Video Processing |`public abstract int setVideoEffectColorFilterIntensity(float intensity);` |`public abstract int setColorFilterIntensity(float intensity);` |* Moved from `RTCVideo` class to `IVideoEffect` class.<br><br>* Unified the return values. |
|Replaced |Video Management |`public abstract int registerFaceDetectionObserver(IFaceDetectionObserver observer, int interval);` |* `public abstract int enableFaceDetection( IFaceDetectionObserver observer, int interval_ms, String face_model_path);`<br><br>* `public abstract int disableFaceDetection();` |* Moved from `RTCVideo` class to `IVideoEffect` class.<br><br>* Decoupled face detection and video effects to improve usability.<br><br>* Unified the return values. |
|Modified |Message |`public abstract int sendSEIMessage(StreamIndex streamIndex, byte[] message, int repeatCount);` |`public abstract int sendSEIMessage(StreamIndex streamIndex, byte[] message, int repeatCount, SEICountPerFrame mode);` |Added Multi\-SEI mode. When you send multiple SEI messages in 1 frame, they will be sent together in the next frame. |
|Modified |Multiple modules |`updateToken`<br><br>`setRemoteVideoConfig`<br><br>`subscribeStream`<br><br>`unsubscribeStream`<br><br>`subscribeScreen`<br><br>`unsubscribeScreen`<br><br>`setVoiceChangerType`<br><br>`setRemoteAudioPlaybackVolume` |`updateToken`<br><br>`setRemoteVideoConfig`<br><br>`subscribeStream`<br><br>`unsubscribeStream`<br><br>`subscribeScreen`<br><br>`unsubscribeScreen`<br><br>`setVoiceChangerType`<br><br>`setRemoteAudioPlaybackVolume` |The return type changed from `void` to `int`. See `ReturnStatus` for the description of the return value. |
|Modified |Multiple modules |`setVoiceReverbType`<br><br>`pushExternalVideoFrame`<br><br>`pushExternalEncodedVideoFrame` |`setVoiceReverbType`<br><br>`pushExternalVideoFrame`<br><br>`pushExternalEncodedVideoFrame` |The return type changed from `boolean` to `int`. See `ReturnStatus` for the description of the return value. |
|Modified |Multiple modules |`setMultiDeviceAVSync`<br><br>`setLocalVideoMirrorType`<br><br>`setVideoRotationMode`<br><br>`setAudioRoute`<br><br>`registerAudioFrameObserver`<br><br>`registerAudioProcessor`<br><br>`enableSimulcastMode`<br><br>`setPublishFallbackOption`<br><br>`setSubscribeFallbackOption`<br><br>`updateLocalVideoCanvas`<br><br>`setRemoteVideoCanvas` |`setMultiDeviceAVSync`<br><br>`setLocalVideoMirrorType`<br><br>`setVideoRotationMode`<br><br>`setAudioRoute`<br><br>`registerAudioFrameObserver`<br><br>`registerAudioProcessor`<br><br>`enableSimulcastMode`<br><br>`setPublishFallbackOption`<br><br>`setSubscribeFallbackOption`<br><br>`updateLocalVideoCanvas`<br><br>`setRemoteVideoCanvas` |The return type changed from `int` to `void`. |
|Modified |Video Management |`public abstract void updateRemoteStreamVideoCanvas(String roomId, String userId, StreamIndex streamIndex, int renderMode, int background_color);` |`public abstract void updateRemoteStreamVideoCanvas(RemoteStreamKey stream_key, int renderMode, int background_color);` |Set `roomId`, `userId` and `streamIndex` in `stream_key`. |
|Modified |Video Management |`public abstract int setRemoteVideoCanvas(String userId, StreamIndex streamIndex, VideoCanvas videoCanvas);` |`public abstract void setRemoteVideoCanvas(RemoteStreamKey stream_key, VideoCanvas videoCanvas);` |Set `userId` and `streamIndex` in `stream_key`. |
|Modified |Engine Management |`getSdkVersion` |`getSDKVersion` | |
|Modified |Screen Sharing |`public abstract boolean pushScreenFrame(VideoFrame videoFrame);` |`public abstract int pushScreenVideoFrame(VideoFrame videoFrame);` |* The return type changes from `boolean` to `int`.<br><br>* The name changes from `pushScreenFrame` to `pushScreenVideoFrame`. |


<span id="callback"></span>
## Callback


|Type |Function Module |Previous |Current |Notes |
|---|---|---|---|---|
|Modified |Push to CDN |`void onMixingAudioFrame(String taskId, byte[] audioFrame, int frameNum);` |`void onMixingAudioFrame(String taskId, byte[] audioFrame, int frameNum, long timeStampMs);` |Added a new parameter: `timeStampMs` |
|Modified |Custom Stream Processing |`OnStart`<br><br>`OnStop`<br><br>`OnRateUpdate`<br><br>`OnRequestKeyFrame`<br><br>`OnRemoteEncodedVideoFrame` |`onStart`<br><br>`onStop`<br><br>`onRateUpdate`<br><br>`onRequestKeyFrame`<br><br>`onRemoteEncodedVideoFrame` |The name changed from UpperCamelCase to LowerCamelCase. |
|Modified |Push to CDN |`onDataFrame` |`onMixingDataFrame` | |
|Replaced |Range Audio |When you use range audio with manual audio subscription, you must set the attenuation index based on the return value of `IRangeAudioObserver`. |Set the attenuation model by calling `setAttenuationModel`. | |
|Modified |Custom Stream Processing |`onProcessRecordAudioFrame` |`onProcessRecordAudioFrame` |In earlier versions, any modification to the audio frames returned by the callback affects the audio data sent to the remote user and the audio data sent to the local ear monitoring device.<br><br>In this version or higher, the modification affects the audio data sent to the remote user only. If you need to modify the audio data sent to the local ear monitoring device, see `onProcessEarMonitorAudioFrame`. |


<span id="keytype"></span>
## Keytype


|Type |Keytype |Notes |
|---|---|---|
|New |`FaceDetectionResult` |Added new member: `frameTimestampUs` |
|Modified |`VideoCanvas` |* Deleted the following members:<br><br>   `roomId`<br><br>   `uid`<br><br>   `streamId`<br><br>   `isScreen`<br><br>* `RENDER_MODE_Fill` changed to `RENDER_MODE_FILL` |
|New |`AudioProcessorMethod` |Added `AUDIO_FRAME_PROCESSOR_EAR_MONITOR(3)` |
|New |`UserMessageSendResult` |Added `USER_MESSAGE_SEND_RESULT_EXCEED_QPS = 5` |
|New |`RoomMessageSendResult` |Added `ROOM_MESSAGE_SEND_RESULT_EXCEED_QPS = 5` |
|Modified |`position` |The data type of `x`, `y`, `z` of `position` used in spatial audio is changed from `int` to `float`. |
|Modified |`ChannelProfile` |The default value of `CHANNEL_PROFILE_COMMUNICATION(0)` is changed from `CHANNEL_PROFILE_CHAT_ROOM(6)` to `CHANNEL_PROFIEL_MEETING(16)`. |
|New |`LiveTranscoding` |Added member `ClientMixParam` |
|Modified |`Region.size` |The range of parameter `width` and `height` extended from `(0.0, 1.0]` to `[0.0, 1.0]`. |
|Modified |`AudioRoute` |`AUDIO_ROUTE_UNKNOWN` is replaced by `AUDIO_ROUTE_DEFAULT` |
|Modified |`AudioScenarioType` |The mapping from audio routing and publishing and subscribing status to audio type has changed, see the latest documentation. |


<span id="error-code"></span>
## Error Code


|Type |Error Code |Notes |
|---|---|---|
|New |`ErrorCode` |Added `ERROR_CODE_USER_ID_DIFFERENT = -1014` |


<span id="_3-45-6"></span>
# 3.45.6

<span id="api"></span>
## API


|Type |API |Notes |
|---|---|---|
|New |`enableAudioPropertiesReport` |Adds `AudioPropertiesMode` member in `AudioPropertiesConfig`. |
|Modified |`setEarMonitorMode` |Enables hardware\-level in\-ear monitoring self\-adaptively. |


<span id="keytype"></span>
## Keytype


|Type |Keytype |Notes |
|---|---|---|
|New |`AudioScenarioType` |Added `AUDIO_SCENARIO_HIGHQUALITY_CHAT` member. |
|New |`AudioProcessorMethod` |Added `AUDIO_FRAME_PROCESSOR_EAR_MONITOR(3)` member for acquiring SDK\-level in\-ear monitoring audio. |
|New |`AudioProcessorMethod` |Added `AUDIO_FRAME_PROCESSOR_SCREEN(4)` member. |
