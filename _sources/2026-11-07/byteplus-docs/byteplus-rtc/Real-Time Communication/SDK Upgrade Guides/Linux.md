---
title: "Linux"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-153611"
---

# 3.60.105

## API Changes

|V3.60.104 |V3.60.105 |Change Description |
|---|---|---|
|`setRoomProfile(RoomProfileType room_profile)` |`setLiveMode(RoomLiveMode live_mode)` |Renamed from `setRoomProfile` to `setLiveMode`. The parameter type changed from `RoomProfileType` to `RoomLiveMode`. |
|`sendLivePushSEIMessage`: prerequisite was `kRoomProfileTypeLivePush` set via `joinRoom` |`sendLivePushSEIMessage`: prerequisite is `kRoomLiveModeSoloHost` set via `setLiveMode` |The prerequisite for calling `sendLivePushSEIMessage` changed from setting room profile to `kRoomProfileTypeLivePush` during `joinRoom` to calling `setLiveMode` with `kRoomLiveModeSoloHost`. |

## Type Changes

|Type Name |Change Description |
|---|---|
|`RoomLiveMode` |New enum type. Defines the live streaming mode:<br><br><br>* `kRoomLiveModeCoHost` (value 1): Co\-hosted live streaming mode for multi\-person or interactive live scenarios.<br><br>* `kRoomLiveModeSoloHost` (value 2): Single\-host live streaming mode. |
|`RoomProfileType` |Removed enum values: `kRoomProfileTypeLinkMic` and `kRoomProfileTypeLivePush`. Use the new `RoomLiveMode` enum with `setLiveMode` instead. |
|`RTCRoomConfig` |Added `RoomLiveMode live_mode` field. Default value: `kRoomLiveModeCoHost`. Specifies the live mode when joining a room. Only effective when `room_profile_type` is `kRoomProfileTypeLive`. Can be changed after joining via `setLiveMode`. |
|`VideoEncoderConfig` |Added `int32_t key_frame_interval_ms` field. Default value: `0` (encoder determines automatically). Sets the key frame interval in milliseconds. |
|`VideoSolutionDescription` |Added `int32_t key_frame_interval_ms` field. Default value: `0`. Sets the key frame interval in milliseconds for simulcast stream solutions. |

## New Interfaces

|Class / Module |Interface |Description |
|---|---|---|
|`IRTCRoom` |`setLiveMode` |Sets the live streaming mode (co\-hosted / single\-host). Call after joining a room. |
|`IRTCEngine` |`sendLivePushSEIMessage` |Sends SEI data in Key\-Value (JSON) format through video frames. Requires `kRoomLiveModeSoloHost` mode. |

## Deleted or Deprecated Interfaces

|Interface |Replacement |Description |
|---|---|---|
|`IRTCRoom::setRoomProfile` |`IRTCRoom::setLiveMode` |Replaced by `setLiveMode` with the new `RoomLiveMode` enum. |

# 3.60.104

## API Changes

|Change Details |Interface |Notes |
|---|---|---|
|Added |`setRoomProfile` |Sets room profile before or after joining a room. |
|Added |`sendLivePushSEIMessage` |Sends SEI (Supplemental Enhancement Information) data in Key\-Value format through video frames. |

## Type Changes

|Change Details |Changed Data Type |Notes |
|---|---|---|
|New Enum Value Added |RoomProfileType |New enum values:<br><br><br>* `kRoomProfileTypeLinkMic`: Link mic mode, focuses on high quality, same bitrate as LIVE.<br><br>* `kRoomProfileTypeLivePush`: Live push mode for broadcasting scenarios. |
|New Member Variable Added |VideoEncoderConfig |Added `key_frame_interval_ms` field: Sets key frame interval in milliseconds, default: 0. |
|New Member Variable Added |VideoPreprocessorConfig |Added `action_domain` field: Controls the effective range of your custom video preprocessor. |
|New Enum Added |ProcessorActionDomain |Controls where the custom video preprocessor effects are applied:<br><br><br>* `kProcessorActionDomainPreviewAndEncode`: Effects apply to both preview and transmission.<br><br>* `kProcessorActionDomainPreview`：Effects apply only to local preview.<br><br>* `kProcessorActionDomainEncode`：Effects apply only to outgoing stream. |

# 3.60.103

## API Changes

### Header Files and Base Class Names

|Change Type |V3.58 |V3.60 |
|---|---|---|
|Header file name changes |../bytertc_video.h |../bytertc_engine.h |
||../bytertc_video_event_handler.h |../bytertc_engine_event_handler.h |
|Base class name changes (all modules) |class IRTCVideo class IRTCVideoEventHandler |class IRTCEngine class IRTCEngineEventHandler |
|New header files |None |../IRTSRoom.h<br><br>../IRTSRoomEventHandler.h |

### Engine Management

|Change Type |V3.58 |V3.60 |Change Details |
|---|---|---|---|
|Create engine object |createRTCVideo(const char\* app_id, bytertc::IRTCVideoEventHandler *event_handler, const char* parameters) |createRTCEngine(const EngineConfig& config, IRTCEngineEventHandler\* event_handler) |* **Name change**: `createRTCVideo` changed to `createRTCEngine`<br><br>* **Parameter changes**:<br><br>   * `parameters` and `app_id`: Moved to the new `EngineConfig` class, and `app_id` renamed to `appID`<br><br>   * New field added to `EngineConfig`: `is_game_scene`, used to control game scene switch<br><br>   * `event_handler` parameter type changed from `IRTCVideoEventHandler` to `IRTCEngineEventHandler` |
|Destroy engine |destroyRTCVideo |destroyRTCEngine |**Method name change** |
|Audio and video engine event callback interface |IRTCVideoEventHandler |IRTCEngineEventHandler |**Interface name change** |

### Room Management

|Change Type |V3.58 |V3.60 |Description |
|---|---|---|---|
|Join room |joinRoom(const char\* token, const UserInfo& user_info, const RTCRoomConfig& config) |int joinRoom(const char\* token, const UserInfo& user_info, bool user_visibility, const RTCRoomConfig& config) |* **Parameter changes**:<br><br>   * **New parameter** `user_visibility`: Specifies user visibility.<br><br>      It is recommended to set user visibility to false when joining the room, and then set it to true through setUserVisibility when the user needs to send audio and video streams. The number of invisible users allowed in a room is much higher than that of visible users. To maximize resource utilization, enable user visibility on demand. This prevents new users from being unable to join because the visible user limit has been reached.<br><br>   * The parameter `is_auto_publish` in RTCRoomConfig is split into video is_publish_video and audio is_publish_audio<br><br>   * Values have been added to and removed from the RoomProfileType enum, which is used for the room_profile_type parameter in RTCRoomConfig. For details, see Android below.<br><br>* **Behavior changes**:<br><br>   * V3.58:<br><br>      * By default, the main stream is automatically published when joining the room. Whether to publish audio or video streams when joining the room is determined by publishVideoStream(false) and publishAudioStream(false) before calling the interface<br><br>      * publishVideoStream/publishAudioStream are effective both before and after joining the room<br><br>   * V3.60:<br><br>      * Automatically publish audio and video streams (main stream) when joining the room. Whether the stream is published is determined by isPublishVideo and isPublishAudio in `RTCRoomConfig`.<br><br>      * The scope of the single\-stream version of publishVideoStream/publishAudioStream is limited to after joining the room, and calling before joining the room is invalid |
|Create room instance |createRTCRoom(const char\* room_id) |createRTCRoom(const char\* *room_id*) |**Behavior change**:<br><br>When creating a room instance with an existing roomId, the previously created room instance will be returned, and the error code `kWarningCodeOldRoomBeenReplaced = -2016` will no longer be triggered |
|Room creation failure callback |onCreateRoomStateChanged(const char\* room_id, int error_code) |onRoomStateChanged( const char\* room_id, const char\* uid, int state, const char\* extra_info) |**Interface replacement**: Room creation failure is notified by onRoomStateChanged. No longer through onCreateRoomStateChanged callback. |
|Callback for setting room extra information result |onSetRoomExtraInfoResult(int64_t task_id, SetRoomExtraInfoResult error_code) |onSetRoomExtraInfoResult(int64_t task_id, SetRoomExtraInfoResult result) |**Parameter change**: `error_code` renamed to `result`. |
|Callback for remote visible user joining room, or invisible user in room switching to visible |onUserJoined(const UserInfo &user_info,int elapsed) |onUserJoined(const UserInfo& user_info) |**Parameter change**: Remove invalid parameter `elapsed`. |

### Publish and Subscribe to Simulcast Streams

|Change Type |V3.58 |V3.60 |Description |
|---|---|---|---|
|Enable/disable pushing multiple video streams |enableSimulcastMode(bool enabled) |setLocalSimulcastMode(VideoSimulcastMode mode) |* **Interface renamed**<br><br>* **Function extension and parameter changes**: Remove `bool enabled` from the old method and replace it with `VideoSimulcastMode mode`, allowing you to specify the specific multi\-stream mode type through the parameter `VideoSimulcastMode`.<br><br>* **Default behavior adjustment**:<br><br>   * Old interface: When `enabled` is true, all configured Simulcast streams will be published.<br><br>   * New interface: When the `mode` parameter is set to `kVideoSimulcastModeAlwaysSimulcast = 2`, all configured Simulcast streams will be published.<br><br>* **Calling timing change**: The old method is called before joining the room or after joining the room but before publishing streams, while the new method needs to be called before joining the room. |
|Set the maximum resolution video stream parameters expected to be published |setVideoEncoderConfig(const VideoEncoderConfig& max_solution) |setVideoEncoderConfig(const VideoEncoderConfig& encoder_config) |**Parameter changes**: The parameter name `max_solution` has been changed to `encoder_config` |
|Set multiple video stream parameters |setVideoEncoderConfig(const VideoEncoderConfig\* channel_solutions, int solution_num) |setLocalSimulcastMode(VideoSimulcastMode mode, const VideoEncoderConfig\* stream_config, int num) |**Interface replacement** |
|Set parameters for the expected remote video stream to subscribe to |setRemoteVideoConfig(const char \*user_id,const RemoteVideoConfig &remote_video_config) |setRemoteSimulcastStreamType(const char\* stream_id, SimulcastStreamType stream_type) = 0 |* **Interface renamed**<br><br>* **Parameter removal**:<br><br>   * Change user_id to stream_id, tracking streams instead of users.<br><br>   * Remove `remote_video_config` and replace it with `streamType` (type `SimulcastStreamType`). No need to specify specific values anymore; you can specify subscription preferences by passing enumeration values. |

### Screen Sharing

1. Screen streams and regular video streams cannot coexist in the same engine. When screen streaming is enabled, regular video streaming will be automatically disabled, and when regular video streaming is enabled, screen streaming will be automatically disabled.

2. Screen streams and regular video streams use the same publishing and subscription methods, deprecating a series of interfaces with "screen" in their names.

|Function |V3.58 |V3.60 |Change Description |
|---|---|---|---|
|Capture screen video |startScreenVideoCapture(const ScreenCaptureSourceInfo &source_info, const ScreenCaptureParameters &capture_params)=0 |startScreenVideoCapture(const ScreenCaptureSourceInfo& source_info, const ScreenCaptureParameters& capture_params) = 0 |**Behavior changes**:<br><br>Video capture will be stopped when screen capture starts |
|**Capture screen audio** |**startScreenAudioCapture() = 0** |**startScreenAudioCapture(const char device_id[MAX_DEVICE_ID_LENGTH]) = 0** |**Parameter changes**:<br><br>**Added device_id array. On Windows, this parameter is used to capture audio from a specified local process. For example, this parameter can be set to the executable file name of an application (such as QQMusic.exe), and the SDK will only capture the audio of that application. Passing** **`nullptr`** ** or an empty string captures audio from all applications on the system except for the current process. Currently, the application only supports QQ Music, NetEase Cloud Music, and Kugou Music. Capturing other processes may cause unknown behavior.**  |
|Set screen stream encoding parameters |setVideoEncoderConfig(const VideoEncoderConfig &max_solution)=0 |setVideoEncoderConfig(const VideoEncoderConfig& encoder_config) = 0 |**Interface replacement**:<br><br>Screen streams and video streams share the same set of encoding parameters. The parameters set by setVideoEncoderConfig will apply to both screen streams and regular video streams |
|Publish/stop publishing local screen audio and video streams |publishScreen(MediaStreamType type)=0<br><br>unpublishScreen(MediaStreamType type)=0 |publishStreamVideo(bool publish) = 0<br><br>publishStreamAudio(bool publish) = 0 |**Interface replacement**:<br><br>Screen streams and video streams share the same set of publish/unpublish interfaces<br><br>**Interface split**<br><br>Audio and video publish/unpublish interfaces are separated |
|Subscribe/unsubscribe to remote screen audio and video streams |subscribeScreen(const char\* user_id, MediaStreamType type)=0<br><br>unsubscribeScreen(const char\* user_id, MediaStreamType type)=0 |subscribeStreamVideo(const char \*stream_id, bool subscribe) = 0<br><br>subscribeStreamAudio(const char \*stream_id, bool subscribe) = 0 |**Interface replacement**:<br><br>Screen streams and video streams share the same set of subscribe/unsubscribe interfaces<br><br>**Interface split**<br><br>Audio and video subscribe/unsubscribe interfaces are separated<br><br>**Parameter changes**:<br><br>The streamId parameter identifies the stream and indicates if it is a screen stream. |
|Remote user publish or unpublish screen stream callback |onUserPublishScreen(const char\* uid, MediaStreamType type)<br><br>onUserUnpublishScreen(const char\* uid, MediaStreamType type, StreamRemoveReason reason) |onUserPublishStreamVideo(const char\* stream_id, const StreamInfo& stream_info, bool is_publish)<br><br>onUserPublishStreamAudio(const char\* stream_id, const StreamInfo& stream_info, bool is_publish) |**Interface replacement**:<br><br>Screen streams and video streams share the same set of publish/unpublish callback interfaces<br><br>**Interface split**<br><br>Audio and video publish/unpublish callback interfaces are separated<br><br>**Parameter changes**:<br><br>The streamId parameter identifies the stream and indicates if it is a screen stream. |
|Screen sharing stream video first frame send status callback |onScreenVideoFrameSendStateChanged(const char\* room_id, const RtcUser &user, FirstFrameSendState state) |onVideoFrameSendStateChanged(const char\* stream_id, const StreamInfo& stream_info, const RtcUser& user, FirstFrameSendState state) |**Interface replacement**:<br><br>Screen streams and video streams share the same set of video first frame send status callbacks<br><br>**Parameter changes**:<br><br>Use parameter streamId to distinguish which specific stream it is and whether it is a screen stream |
|Screen sharing stream video first frame playback status callback |onScreenVideoFramePlayStateChanged(const char\* room_id, const RtcUser &user, FirstFramePlayState state) |onVideoFramePlayStateChanged(const char\* stream_id, const StreamInfo& stream_info, const RtcUser& user, FirstFramePlayState state) |**Interface replacement**:<br><br>Screen streams and video streams share the same set of video first frame playback status callbacks<br><br>**Parameter changes**:<br><br>Use parameter streamId to distinguish which specific stream it is and whether it is a screen stream |

### RTS

|Function |V3.58 |V3.60 |Change Description |
|---|---|---|---|
|Create RTS room |createRTCRoom(const char\* room_id) = 0 |createRTSRoom(const char\* room_id) = 0 |**Interface split**: If only using RTS\-related capabilities, call createRTSRoom to create RTSRoom instance |
|Set RTS\-related callbacks |setRTCRoomEventHandler(IRTCRoomEventHandler\* room_event_handler) = 0 |setRTSRoomEventHandler(IRTSRoomEventHandler\* room_event_handler) = 0 |**Interface split**: If only using RTS\-related capabilities, call this interface in RTSRoom to set callbacks |
|Callback received when receiving text messages from users outside the room |onUserMessageReceivedOutsideRoom(const char\* uid, const char\* message) |onUserMessageReceivedOutsideRoom(int64_t msgid, const char\* uid, const char\* message) |**Parameter changes**: Added msgid parameter to callback parameters |
|Callback received when receiving binary messages from users outside the room |onUserBinaryMessageReceivedOutsideRoom(const char\* uid, int size, const uint8_t\* message) |onUserBinaryMessageReceivedOutsideRoom(int64_t msgid, const char\* uid, const uint8_t\* message, int size) |**Parameter changes**: Added msgid parameter to callback parameters |
|Callback for receiving broadcast messages in the room |onRoomMessageReceived(const char\* uid, const char\* message) |onRoomMessageReceived(int64_t msgid, const char\* uid, const char\* message) |**Parameter changes**: Added msgid parameter to callback parameters |
|Callback for receiving broadcast binary messages in the room |onRoomBinaryMessageReceived(const char\* uid, int size, const uint8_t\* message) |onRoomBinaryMessageReceived(int64_t msgid, const char\* uid, const uint8_t\* message, int size) |**Parameter changes**: Added msgid parameter to callback parameters |
|Callback received when receiving point\-to\-point text messages from other users in the room |onUserMessageReceived(const char\* uid, const char\* message) |onUserMessageReceived(int64_t msgid, const char\* uid, const char\* message) |**Parameter changes**: Added msgid parameter to callback parameters |
|Callback received when receiving point\-to\-point binary messages from other users in the room |onUserBinaryMessageReceived(const char\* uid, int size, const uint8_t\* message) |onUserBinaryMessageReceived(int64_t msgid, const char\* uid, const uint8_t\* message, int size) |**Parameter changes**: Added msgid parameter to callback parameters |

### Publish and Subscribe Mainstream (Camera/Microphone Captured Streams)

|Function |V3.58 |V3.60 |Change Description |
|---|---|---|---|
|1. **Publish/Unpublish Audio/Video Streams** ||||
|* Publish audio/video streams<br><br>* Unpublish audio/video streams |* publishStream(MediaStreamType type)<br><br>* unpublishStream(MediaStreamType type) |* publishStreamVideo(bool publish)<br><br>* publishStreamAudio(bool publish) |* **Interface split and function extension**:<br><br>   * **Split by audio and video**: 2 new methods for controlling video stream and audio stream publishing respectively<br><br>   * **Merge publish and unpublish**: New interface handles publish and unpublish operations through `bool publish` parameter<br><br>* **Parameter changes**:<br><br>   * Removed `type`, new methods directly distinguish video and audio streams through method names<br><br>   * Added `bool publish`<br><br>* **Behavior changes**:<br><br>   * V3.58: Effective before and after joining room<br><br>   * V3.60: Scope limited to after joining room, calling before joining room is ineffective |
|* Callback for remote camera/microphone captured media streams in the room<br><br>* Callback for removal of remote camera/microphone captured media streams in the room |* onUserPublishStream( const char\* uid, MediaStreamType type )<br><br>* onUserUnpublishStream( const char\* uid, MediaStreamType type, StreamRemoveReason reason) |* onUserPublishStreamAudio(const char\* stream_id, const StreamInfo& stream_info, bool is_publish)<br><br>* onUserPublishStreamVideo(const char\* stream_id, const StreamInfo& stream_info, bool is_publish) |* **Interface split, rename, and function extension**:<br><br>   * **Split by audio and video**: 2 new methods for controlling audio stream and video stream subscription callbacks respectively<br><br>   * **Merge subscribe and unsubscribe status**: New interface handles publish and unpublish callbacks through `is_publish` parameter<br><br>* **Parameter changes**:<br><br>   * Removed `uid`, new methods distinguish streams through `streamId` parameter<br><br>   * Removed `type`, new methods directly distinguish video and audio streams through method names<br><br>   * Added `room_id` parameter to identify room ID<br><br>   * Removed `StreamRemoveReason reason`, no longer provides detailed information about removal reasons |
|Callback when audio/video stream publish status triggers warnings or errors |onStreamStateChanged( const char\* room_id, const char\* uid, int state, const char\* extra_info) |* onVideoPublishStateChanged(const char\* stream_id, const StreamInfo& stream_info, PublishState state, PublishStateChangeReason reason)<br><br>* onAudioPublishStateChanged(const char\* stream_id, const StreamInfo& stream_info, PublishState state, PublishStateChangeReason reason) |* **Interface split and rename**: Split by audio and video, 2 new methods for controlling audio stream and video stream publish status callbacks respectively<br><br>* **Parameter changes**:<br><br>   * **Parameter type changes**: `state` type changed from `int` to `PublishState` enum<br><br>   * **Added parameters**:<br><br>      * Added `streamId` parameter to distinguish streams<br><br>      * Added `reason`, type is `PublishStateChangeReason` enum, used to indicate specific reasons for publish status changes<br><br>   * **Removed parameters**:<br><br>      * Removed `uid`, new methods distinguish streams through `streamId` parameter<br><br>      * Removed invalid parameter `extraInfo` |
|2. **Subscribe/Unsubscribe Audio/Video Streams** ||||
|* Subscribe to audio/video streams<br><br>* Unsubscribe from audio/video streams |* subscribeStream(const char \*user_id, MediaStreamType type)<br><br>* unsubscribeStream(const char \*user_id, MediaStreamType type) |* subscribeStreamVideo(const char \*stream_id, bool subscribe) = 0<br><br>* subscribeStreamAudio(const char \*stream_id, bool subscribe) = 0 |* **Interface split, rename, and function extension**:<br><br>   * **Split by audio and video**: 2 new methods for controlling video stream and audio stream subscription respectively<br><br>   * **Merge subscribe and unsubscribe**: New interface handles subscribe and unsubscribe through `bool subscribe` parameter<br><br>* **Parameter changes**:<br><br>   * Removed `uid`, new methods distinguish streams through `streamId` parameter<br><br>   * Removed `type`, new methods directly distinguish video streams and audio streams through method names<br><br>   * Added `bool subscribe` |
|Audio/video stream subscription status change callback |onStreamSubscribed(SubscribeState state_code, const char\* user_id, const SubscribeConfig& info) |* onVideoSubscribeStateChanged(const char\* stream_id, const StreamInfo& stream_info, SubscribeState state, SubscribeStateChangeReason reason)<br><br>* onAudioSubscribeStateChanged(const char\* stream_id, const StreamInfo& stream_info, SubscribeState state, SubscribeStateChangeReason reason) |* **Interface split and rename**: Split by audio and video, 2 new methods for controlling audio stream and video stream subscription status change callbacks respectively<br><br>* **Parameter changes**<br><br>   * **Added parameters**:<br><br>      * Added `streamId` and `stream_info` parameters to distinguish streams<br><br>      * Added `reason`: Used to describe specific reasons for subscription status changes in more detail<br><br>   * **Parameter rename**:<br><br>      * `state_code`: Renamed to `state`<br><br>   * **Removed parameters**:<br><br>      * Removed `user_id`, new methods distinguish streams through `streamId` and `stream_info` parameters<br><br>      * Removed `info`, no longer returned |
|Callback when audio/video stream subscription status triggers warnings or errors<br><br> **[Originally duplicated with above?]**  |onStreamStateChanged( const char\* room_id, const char\* uid, int state, const char\* extra_info) |* onVideoSubscribeStateChanged(const char\* stream_id, const StreamInfo& stream_info, SubscribeState state, SubscribeStateChangeReason reason)<br><br>* onAudioSubscribeStateChanged(const char\* stream_id, const StreamInfo& stream_info, subscribeState state, SubscribeStateChangeReason reason) |* **Interface split and rename**: Split by audio and video, 2 new methods for controlling audio stream and video stream subscription status change callbacks respectively<br><br>* **Parameter changes**<br><br>   * **Parameter type changes**: `state` type changed from `int` to `SubscribeState` enum<br><br>   * **Added parameters**:<br><br>      * Added `streamId` and `stream_info` parameters to distinguish streams<br><br>      * Added `reason`, type is `SubscribeStateChangeReason` enum, used to indicate specific reasons for publish status changes<br><br>   * **Removed parameters**:<br><br>      * Removed `room_id` and `user_id`, new methods distinguish streams through `streamId` and `stream_info` parameters<br><br>      * Removed invalid parameter `extraInfo` |
|3. **Subscribe/Unsubscribe All Media Streams** ||||
|* Subscribe to all media streams<br><br>* Unsubscribe from all media streams |* subscribeAllStreams(MediaStreamType type)<br><br>* unsubscribeStream(const char \*user_id,MediaStreamType type) |* subscribeAllStreamsVideo(bool subscribe)<br><br>* subscribeAllStreamsAudio(bool subscribe) |* **Interface split, rename, and function extension**:<br><br>   * **Split by audio and video**: 2 new methods for subscribing/unsubscribing all video streams and subscribing/unsubscribing all audio streams respectively<br><br>   * **Merge subscribe and unsubscribe**: New interface handles subscribe and unsubscribe through `bool subscribe` parameter<br><br>* **Parameter changes**:<br><br>   * **Removed parameters**:<br><br>      * Removed `type`, new methods directly distinguish video and audio streams through method names<br><br>      * Removed `user_id`, no need to pass in<br><br>   * **Added parameters**: `bool subscribe` |
|Pause receiving media streams from remote endpoints |pauseAllSubscribedStream(PauseResumeControlMediaType media_type) |* pauseAllSubscribedStreamAudio()<br><br>* pauseAllSubscribedStreamVideo() |* **Interface split**: Split by audio and video, 2 new methods for pausing reception of all remote audio streams and pausing all remote video streams respectively<br><br>* **Parameter changes**: Removed `media_type`, new methods directly distinguish audio and video streams through method names |
|Resume receiving media streams from remote endpoints |resumeAllSubscribedStream(PauseResumeControlMediaType media_type) |* resumeAllSubscribedStreamAudio()<br><br>* resumeAllSubscribedStreamVideo() |* **Interface split**: Split by audio and video, 2 new methods for resuming reception of all remote audio streams and resuming reception of all remote video streams respectively<br><br>* **Parameter changes**: Removed `media_type`, new methods directly distinguish audio and video streams through method names |

### WTN Streams (Formerly Public Streams)

* Interface location changes:

   * WTN stream subscription interfaces moved to the newly added `IWTNStream` class.

   * WTN stream subscription callbacks moved to the newly added `IWTNStreamEventHandler` callback class. You need to call setWTNStreamEventHandler first to set the callback handler.

* Shares IMixedStreamConfig with mixed stream push interfaces to improve usability.

* Added onWTNRemoteVideoStats and onWTNRemoteAudioStats to obtain WTN stream information and detect stream quality.

* Interface split, rename, and replacement, specific changes as follows:

|Function |V3.58 |V3.60 |Details |
|---|---|---|---|
|Publish WTN streams<br><br>Support composing media streams published by multiple users in a specified room into one WTN stream |startPushPublicStream(const char\* public_stream_id, IPublicStreamParam\* param) |startPushMixedStream(const char\* task_id, MixedStreamPushTargetConfig push_target_config, IMixedStreamConfig\* config) |* **Interface rename**<br><br>* **Interface merge and function extension**: startPushPublicStream and startPushMixedStreamToCDN merged into startPushMixedStream, new interface can be used simultaneously for mixed stream push to CDN or push WTN (formerly public streams)<br><br>* **Parameter changes**:<br><br>   * **Added parameters**: Added `task_id`: Set push task ID to identify push tasks<br><br>   * **Parameter replacement**:<br><br>      * Removed `public_stream_id`: WTN stream ID (i.e., public stream ID) specified by newly added parameter `push_target_config`<br><br>      * Removed `param`: Replaced with newly added parameter `config` for configuring WTN streams |
|Update WTN Stream |updatePublicStreamParam(const char\* public_stream_id, IPublicStreamParam\* param) |updatePushMixedStream(const char\* task_id, MixedStreamPushTargetConfig push_target_config, IMixedStreamConfig\* config) |* **Interface rename**<br><br>* **Interface merge and functional extension**: updatePublicStreamParam and updatePushMixedStreamToCDN merged into updatePushMixedStream, the new interface can be used for both updating mixed stream push to CDN and push to WTN (formerly public stream) tasks<br><br>* **Parameter changes**:<br><br>   * **Added parameters**: Added `task_id`: Set push task ID to identify push tasks<br><br>   * **Parameter replacement**:<br><br>      * Removed `public_stream_id`: WTN stream ID (i.e., public stream ID) specified by newly added parameter `push_target_config`<br><br>      * Removed `param`: Replaced with newly added parameter `config` for configuring WTN streams |
|Stop Publishing WTN Stream |stopPushPublicStream(const char\* public_stream_id) |stopPushMixedStream(const char\* *task_id*, MixedStreamPushTargetType *target_type*) |* **Interface rename**<br><br>* **Interface merge and functional extension**: stopPushPublicStream and stopPushStreamToCDN merged into stopPushMixedStream, the new interface can be used for both stopping WTN stream (formerly public stream) publishing and stopping mixed stream push<br><br>* **Parameter changes**:<br><br>   * **Added parameters**: `taskId`, ID of the mixed stream task<br><br>   * **Removed parameters**: Removed `public_stream_idString publicStreamId`, WTN stream ID (i.e., public stream ID) to be stopped specified by `push_target_config` |
|Subscribe/Unsubscribe WTN Stream |* startPlayPublicStream(const char\* public_stream_id)<br><br>* stopPlayPublicStream(const char\* public_stream_id) |* subscribeWTNVideoStream(const char\* stream_id, bool subscribe)<br><br>* subscribeWTNAudioStream(const char\* stream_id, bool subscribe) |* **Interface split, rename, and functional extension**:<br><br>   * **Split by audio and video**: 2 new methods for subscribing/unsubscribing WTN audio streams and subscribing/unsubscribing video streams respectively<br><br>   * **Merge subscribe and unsubscribe**: New interface handles subscription and unsubscription through `bool subscribe` parameter<br><br>* **Parameter changes**:<br><br>   * `public_stream_id`: Renamed to `stream_id`<br><br>   * Added `bool subscribe` |
|Bind WTN Stream Canvas |setPublicStreamVideoCanvas(const char\* public_stream_id, const VideoCanvas& canvas) |setWTNRemoteVideoCanvas(const char\* stream_id, const VideoCanvas& canvas) |* **Interface rename**<br><br>* **Parameter changes**: `public_stream_id`: Renamed to `stream_id` |
|Specify External Renderer for WTN Stream |setPublicStreamVideoSink(const char\* public_stream_id, IVideoSink\* video_sink, IVideoSink::PixelFormat format) |setWTNRemoteVideoSink(const char\* stream_id, IVideoSink\* video_sink, RemoteVideoSinkConfig& config) |* **Interface rename**<br><br>* **Parameter changes**:<br><br>   * **Parameter rename**: `public_stream_id` renamed to `stream_id`<br><br>   * **Added parameters**: Added `config` for configuring remote video frames (such as position, format, whether to mirror video frames, etc.)<br><br>   * **Parameter replacement**: Original `format` implemented by field `pixel_format` in `RemoteVideoSinkConfig`, defaults to 0 (original format) |
|Set WTN Stream Playback Volume |setPublicStreamAudioPlaybackVolume(const char\* public_stream_id, int volume) |setWTNRemoteAudioPlaybackVolume(const char\* stream_id, int volume) |* **Interface rename**<br><br>* **Parameter changes**: `public_stream_id` renamed to `stream_id` |
|WTN Stream Playback Task Callback |onPlayPublicStreamResult(const char\* public_stream_id, PublicStreamErrorCode error_code) |* onWTNVideoSubscribeStateChanged(const char\* stream_id, WTNSubscribeState state_code, WTNSubscribeStateChangeReason reason)<br><br>* onWTNAudioSubscribeStateChanged(const char\* stream_id, WTNSubscribeState state_code, WTNSubscribeStateChangeReason reason) |* **Interface split and rename**: Split into 2 independent interfaces for callbacks on WTN audio/video stream subscription state changes respectively<br><br>* **Parameter changes**<br><br>   * **Parameter rename**: `public_stream_id` renamed to `stream_id`<br><br>   * **Parameter replacement**: Removed `error_code`: Replaced with `state_code` (subscription state code) and `reason` (subscription state change reason) |
|Receive SEI Callback in WTN Stream |onPublicStreamSEIMessageReceived(const char\* public_stream_id,<br><br>const uint8_t\* message,<br><br>int message_length,<br><br>DataMessageSourceType source_type) |onWTNSEIMessageReceived(const char\* stream_id, int channel_id, const uint8_t\* message, int length) |* **Interface rename**<br><br>* **Location move**: Moved to IWTNStream class<br><br>* **Parameter changes**:<br><br>   * **Parameter rename**:<br><br>      * `public_stream_id` renamed to `stream_id`<br><br>      * `message_length` renamed to `length`<br><br>   * **Added parameters**: Added `channel_id`: Set different `channel_id` for different receivers, receivers can select SEI information to focus on based on `channel_id` in the callback<br><br>   * **Removed parameters**: Removed `source_type` parameter, no longer needed |
|Receive Data Message Callback in WTN Stream |onPublicStreamDataMessageReceived(const char\* public_stream_id,<br><br>const uint8_t\* message,<br><br>int message_length,<br><br>DataMessageSourceType source_type) |onWTNDataMessageReceived(const char\* stream_id, const uint8_t\* message, int message_length, DataMessageSourceType source_type) |* **Interface rename**<br><br>* **Location move**: Moved to IWTNStream class<br><br>* **Parameter changes**: `public_stream_id` renamed to `stream_id` |
|WTN Video Stream First Frame Decode Success Callback |onFirstPublicStreamVideoFrameDecoded(const char\* public_stream_id, const VideoFrameInfo& info) |onWTNFirstRemoteVideoFrameDecoded(const char\* stream_id, const VideoFrameInfo& info) |* **Interface rename**<br><br>* **Location move**: Moved to IWTNStream class<br><br>* **Parameter changes**: `public_stream_id` renamed to `stream_id` |
|WTN Audio Stream First Frame Decode Success Callback |onFirstPublicStreamAudioFrame(const char\* public_stream_id) |onWTNFirstRemoteAudioFrame(const char\* stream_id) |* **Interface rename**<br><br>* **Location move**: Moved to IWTNStream class<br><br>* **Parameter changes**: `public_stream_id` renamed to `stream_id` |
|WTN Stream Publishing Result Callback |onPushPublicStreamResult(<br><br>const char\* room_id,<br><br>const char\* public_streamid,<br><br>PublicStreamErrorCode error_code<br><br>) |onMixedStreamEvent(MixedStreamTaskInfo info, MixedStreamTaskEvent event, MixedStreamTaskErrorCode error_code) |* **Interface rename**<br><br>* **Interface merge**: onMixingEvent, onStreamMixingEvent and onPushPublicStreamResult merged into onMixedStreamEvent, the new interface can be used for callbacks on mixed stream push to CDN / WTN stream status<br><br>* **Parameter changes**:<br><br>   * **Parameter type change**: Parameter `error_code` type changed from `PublicStreamErrorCode` to `MixedStreamTaskErrorCode`, sharing the same enumeration class with mixed stream push tasks. For change details, see Windows<br><br>   * `room_id`: No longer needed<br><br>   * `public_streamid`: Replaced with `task_id` in newly added `MixedStreamTaskInfo info`<br><br>   * Added `MixedStreamTaskEvent event`, for details see Windows |

### Push to CDN

Optimized the usability of live streaming push interfaces. Shares IMixedStreamConfig with WTN interfaces to improve usability. If you have already implemented live streaming push functionality, refer to the following table to replace interfaces.

|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|Mixed Stream Push |startPushMixedStreamToCDN(const char\* task_id, IMixedStreamConfig\* config, IMixedStreamObserver\* observer) |startPushMixedStream(const char\* task_id, MixedStreamPushTargetConfig push_target_config, IMixedStreamConfig\* config) |* **Interface rename**<br><br>* **Interface merge and functional change**: startPushPublicStream and startPushMixedStreamToCDN merged into startPushMixedStream, the new interface can be used for both mixed stream push to CDN and push to WTN (formerly public stream)<br><br>* **Parameter changes**:<br><br>   * Removed `observer`, no longer needed<br><br>   * Added: `push_target_config`, used to specify push stream address (such as CDN address, WTN stream ID) |
|Update Mixed Stream Push Task |updatePushMixedStreamToCDN(const char\* task_id, IMixedStreamConfig\* config) |updatePushMixedStream(const char\* task_id, MixedStreamPushTargetConfig push_target_config, IMixedStreamConfig\* config) |* **Interface rename**<br><br>* **Interface merge**: updatePublicStreamParam and updatePushMixedStreamToCDN merged into updatePushMixedStream, the new interface can be used for both updating mixed stream push to CDN and push to WTN (formerly public stream) tasks<br><br>* **Parameter changes**: Added `push_target_config`, used to specify push stream address (such as CDN address, WTN stream ID) |
|Mixed Stream Push Callback |* onMixingEvent( StreamMixingEvent event, const char\* task_id, StreamMixingErrorCode error, MixedStreamType mix_type)<br><br>* onStreamMixingEvent( StreamMixingEvent event, const char\* task_id, StreamMixingErrorCode error, StreamMixingType mix_type) |onMixedStreamEvent(MixedStreamTaskInfo info, MixedStreamTaskEvent event, MixedStreamTaskErrorCode error_code) |* **Interface split and rename**: Split by mixed stream task event callbacks and single stream task event callbacks<br><br>* **Interface merge**: onMixingEvent, onStreamMixingEvent and onPushPublicStreamResult merged into onMixedStreamEvent, the new interface can be used for callbacks on mixed stream push to CDN / WTN stream status<br><br>* **Parameter changes**:<br><br>   * **Type changes**:<br><br>      * `event` (event): Type replaced with `MixedStreamTaskEvent`, for details see Windows<br><br>      * `error` (error code): Renamed to `error_code`, type replaced with `MixedStreamTaskErrorCode`, for details see Windows<br><br>   * **Removed parameters**: Removed `mix_type`, no replacement<br><br>   * **Added parameters**: Added `info`, contains related information of mixed stream tasks, such as stream type, etc.<br><br>* **Location move**: Moved to IRTCEngineEventHandler |
|Single Stream Push |startPushSingleStreamToCDN(const char\* task_id, PushSingleStreamParam& param, IPushSingleStreamToCDNObserver\* observer) |startPushSingleStream(const char\* task_id, PushSingleStreamParam& param) |* **Interface rename**<br><br>* **Removed parameters**: `observer`, no longer needed |
|Stop Push Task |stopPushStreamToCDN(const char\* task_id) |* stopPushSingleStream(const char\* task_id)<br><br>* stopPushMixedStream(const char\* task_id, MixedStreamPushTargetType target_type) |* **Interface split and rename**: Split by single stream and mixed stream<br><br>* **Among them, the stop mixed stream push interface (stopPushMixedStream)** :<br><br>   * Functionally: Can be used for both stopping push to CDN and stopping push to WTN stream<br><br>   * Added parameters: `target_type`, used to specify the stream type to stop pushing |
|Single Stream Push Callback |onStreamPushEvent(<br><br>SingleStreamPushEvent event,<br><br>const char\* task_id,<br><br>int error<br><br>) |onSingleStreamEvent(const char \*task_id, SingleStreamTaskEvent event, SingleStreamTaskErrorCode error_code) |* **Interface rename**<br><br>* **Parameter changes**:<br><br>   * **Type changes**:<br><br>      * `event` (event): Type replaced with `SingleStreamTaskEvent`, for details see Windows<br><br>      * `error` (error code): Renamed to `error_code`, type replaced with `SingleStreamTaskErrorCode`, for details see Windows |

### Audio & Video Transport

|Function |Interface Name |Description |
|---|---|---|
|Callback when receiving the first frame from a remote audio stream |onFirstRemoteAudioFrame(const char\* stream_id, const StreamInfo& stream_info) |Added applicable scenario: after a remote user cancels publishing audio and then publishes audio again, this callback will also be received. Canceling publishing includes active cancellation by the publisher, active room exit, disconnection, and stopping capture. |
|* Callback after SDK successfully renders the first frame of remote video stream<br><br>* Callback after SDK receives and decodes the first frame of remote video stream |* onFirstRemoteVideoFrameRendered(const char\* stream_id, const StreamInfo& stream_info, const VideoFrameInfo& info)<br><br>* onFirstRemoteVideoFrameDecoded(const char\* stream_id, const StreamInfo& stream_info, const VideoFrameInfo& info) |Added applicable scenario: after a remote user cancels publishing video and then publishes video again, these two callbacks will also be received.<br><br>Canceling publishing includes active cancellation by the publisher, active room exit, disconnection, and stopping capture. |

### Audio\-Video Synchronization

|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|When audio\-video synchronization state changes |onAVSyncStateChange(AVSyncState state) |onAVSyncEvent(const char\* room_id, const char\* uid, AVSyncEvent event) |* **Interface rename**<br><br>* **Parameter changes**<br><br>   * Added `room_id` and `uid`<br><br>   * `state` (synchronization state): Type replaced with `AVSyncEvent` (synchronization failure event), you can call `setMultiDeviceAVSync` with empty parameters to unbind the synchronization relationship when receiving this notification, and call this interface again to bind.<br><br>* **Behavior change**: Audio\-video synchronization failure<br><br>   * 3.58: Returned by the following error code: `kErrorCodeInvalidAudioSyncUidRepeated`<br><br>   * 3.60: Returned through onAVSyncEvent `kAVSyncEventInvalidUidRepeated` |

### Playback Volume

**setAudioRoute and setAudioScenario are not supported on Windows and Linux.**

|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|Adjust the playback volume of audio stream from specified remote user on local device |setRemoteAudioPlaybackVolume(const char\* room_id,const char\* user_id, int volume) |*setRemoteAudioPlaybackVolume(const char stream_id, int volume)* \* |* **Parameter changes**:<br><br>   The `room_id` and `user_id` used to specify audio stream are moved to the newly added `stream_key` parameter structure.<br><br>* **Feature expansion**:<br><br>   Only supports adjusting media stream volume from specified users, upgraded to support separately adjusting local capture media stream volume, screen stream volume, and specified process volume. |

### Push External Video Frame

|V3.58 |V3.60 |Description |
|---|---|---|
|pushExternalVideoFrame(StreamIndex stream_index, IVideoFrame\* frame) |pushExternalVideoFrame(const VideoFrameData & frame) |**Parameter changes**:<br><br>The type of parameter `frame` is replaced from `IVideoFrame*` to `VideoFrameData`. Compared to the original parameter type, both the contained parameters and whether they are required have changed. For details, see Windows |

### Get Song List for Each Chart Based on Hot Charts

|3.58 |V3.60 |Description |
|---|---|---|
|getHotMusic(int hot_types, int filters) |getHotMusic(const char\*\* custom_hotlist_id, int id_num, int filters) |**Parameter changes**:<br><br><br>* **Parameter replacement**: Removed `hot_types`, replaced with `custom_hotlist_id`, type changed from enum to `const char**`, used to provide custom hot music list ID. Property value correspondence is as follows:<br><br>   * `kMusicHotTypeContentCenter` → `ContentCenter`<br><br>   * `kMusicHotTypeProject` → `Project`<br><br>* **Added parameters**: Added `id_num`, used to specify the number of chart IDs |

### StreamId Unique Stream Identification

The current version uses StreamId to uniquely identify a stream, so the StreamIndex / RemoteStreamKey parameters from previous versions in various APIs are replaced by StreamId or related information. The involved APIs are as follows:

|Class |V3.58 |V3.60 |Description |
|---|---|---|---|
|IRTCEngine |muteAudioCapture(StreamIndex index, bool mute) |muteAudioCapture(bool mute) |Parameter change: Removed StreamIndex parameter |
|IRTCEngine |setCaptureVolume(StreamIndex index, int volume) |setCaptureVolume(int volume) |Parameter change: Removed StreamIndex parameter |
|IRTCEngine |enableAlphaChannelVideoEncode(StreamIndex stream_index, AlphaLayout alpha_layout) |enableAlphaChannelVideoEncode(AlphaLayout alpha_layout) |Parameter change: Removed StreamIndex parameter |
|IRTCEngine |disableAlphaChannelVideoEncode(StreamIndex stream_index) |disableAlphaChannelVideoEncode() |Parameter change: Removed StreamIndex parameter |
|IRTCEngine |setLocalVideoCanvas(StreamIndex index, const VideoCanvas& canvas) |setLocalVideoCanvas(const VideoCanvas& canvas) |Parameter change: Removed StreamIndex parameter |
|IRTCEngine |updateLocalVideoCanvas(StreamIndex index, const enum RenderMode render_mode, const uint32_t background_color) |updateLocalVideoCanvas(const enum RenderMode render_mode, const uint32_t background_color) |Parameter change: Removed StreamIndex parameter |
|IRTCEngine |setRemoteVideoCanvas(RemoteStreamKey stream_key, const VideoCanvas& canvas) |setRemoteVideoCanvas(const char\* stream_id, const VideoCanvas& canvas) |Parameter change: Changed RemoteStreamKey to stream_id |
|IRTCEngine |updateRemoteStreamVideoCanvas(RemoteStreamKey stream_key, const RemoteVideoRenderConfig& remote_video_render_config) |updateRemoteStreamVideoCanvas(const char\* stream_id, const RemoteVideoRenderConfig& remote_video_render_config) |Parameter change: Changed RemoteStreamKey to stream_id |
|IRTCEngine |setLocalVideoSink(StreamIndex index, IVideoSink\* video_sink, LocalVideoSinkConfig& config) |setLocalVideoSink(IVideoSink\* video_sink, LocalVideoSinkConfig& config) |Parameter change: Removed StreamIndex parameter |
|IRTCEngine |setRemoteVideoSink(RemoteStreamKey stream_key, IVideoSink\* video_sink, RemoteVideoSinkConfig& config) |setRemoteVideoSink(const char\* stream_id, IVideoSink\* video_sink, RemoteVideoSinkConfig& config) |Parameter change: Changed RemoteStreamKey to stream_id |
|IRTCEngine |setVideoSourceType(StreamIndex stream_index, VideoSourceType type) |setVideoSourceType(VideoSourceType type) |Parameter change: Removed StreamIndex parameter |
|IRTCEngine |setRemoteVideoMirrorType(RemoteStreamKey stream_key, RemoteMirrorType mirror_type) |setRemoteVideoMirrorType(const char\* stream_id, RemoteMirrorType mirror_type) |Parameter change: Changed RemoteStreamKey to stream_id |
|IRTCEngine |sendSEIMessage(StreamIndex stream_index, const uint8_t\* message, int length, int repeat_count, SEICountPerFrame mode) |sendSEIMessage(const uint8_t\* message, int length, int repeat_count, SEICountPerFrame mode) |Parameter change: Removed StreamIndex parameter |
|IRTCEngine |startFileRecording(StreamIndex type, RecordingConfig config, RecordingType recording_type) |startFileRecording(RecordingConfig config, RecordingType recording_type) |Parameter change: Removed StreamIndex parameter |
|IRTCEngine |stopFileRecording(StreamIndex type) |stopFileRecording() |Parameter change: Removed StreamIndex parameter |
|IRTCEngine |setRemoteAudioPlaybackVolume(const RemoteStreamKey& stream_key, int volume) |setRemoteAudioPlaybackVolume(const char\* stream_id, int volume) |Parameter change: Changed RemoteStreamKey to stream_id |
|IRTCEngine |pushExternalEncodedVideoFrame(StreamIndex index, int video_index, IEncodedVideoFrame\* video_stream) |pushExternalEncodedVideoFrame(int video_index, IEncodedVideoFrame\* video_stream) |Parameter change: Removed StreamIndex parameter |
|IRTCEngine |setVideoDecoderConfig(RemoteStreamKey key, VideoDecoderConfig config) |setVideoDecoderConfig(const char\* stream_id, VideoDecoderConfig config) |Parameter change: Changed RemoteStreamKey to stream_id |
|IRTCEngine |requestRemoteVideoKeyFrame(const RemoteStreamKey& stream_info) |requestRemoteVideoKeyFrame(const char\* stream_id) |Parameter change: Changed RemoteStreamKey to stream_id |
|IRTCEngine |setVideoWatermark(StreamIndex stream_index, const char\* image_path, RTCWatermarkConfig config) |setVideoWatermark(const char\* image_path, RTCWatermarkConfig config) |Parameter change: Removed StreamIndex parameter |
|IRTCEngine |clearVideoWatermark(StreamIndex stream_index) |clearVideoWatermark() |Parameter change: Removed StreamIndex parameter |
|IRTCEngine |takeLocalSnapshot(const StreamIndex stream_index, ISnapshotResultCallback\* callback) |takeLocalSnapshot(ISnapshotResultCallback\* callback) |Parameter change: Removed StreamIndex parameter |
|IRTCEngine |takeRemoteSnapshot(const RemoteStreamKey stream_key, ISnapshotResultCallback\* callback) |takeRemoteSnapshot(const char\* stream_id, ISnapshotResultCallback\* callback) |Parameter change: Changed RemoteStreamKey to stream_id |
|IRTCEngineEventHandler |onUserStartVideoCapture(const char\* room_id, const char\* user_id) |onUserStartVideoCapture(const char\* stream_id, const StreamInfo& stream_info) |Parameter change: Changed roomId and userId to streamId and streamInfo |
|IRTCEngineEventHandler |onUserStopVideoCapture(const char\* room_id, const char\* user_id) |onUserStopVideoCapture(const char\* stream_id, const StreamInfo& stream_info) |Parameter change: Changed roomId and userId to streamId and streamInfo |
|IRTCEngineEventHandler |onUserStartAudioCapture(const char\* room_id, const char\* user_id) |onUserStartAudioCapture(const char\* stream_id, const StreamInfo& stream_info) |Parameter change: Changed roomId and userId to streamId and streamInfo |
|IRTCEngineEventHandler |onUserStopAudioCapture(const char\* room_id, const char\* user_id) |onUserStopAudioCapture(const char\* stream_id, const StreamInfo& stream_info) |Parameter change: Changed roomId and userId to streamId and streamInfo |
|IRTCEngineEventHandler |onLocalAudioStateChanged(LocalAudioStreamState state, LocalAudioStreamError error) |onLocalAudioStateChanged(const char\* stream_id, const StreamInfo& stream_info, LocalAudioStreamState state, LocalAudioStreamError error) |Parameter change: Added streamId and streamInfo parameters |
|IRTCEngineEventHandler |onLocalVideoStateChanged(StreamIndex index, LocalVideoStreamState state, LocalVideoStreamError error) |onLocalVideoStateChanged(const char\* stream_id, const StreamInfo& stream_info, LocalVideoStreamState state, LocalVideoStreamError error) |Parameter change: Changed streamIndex to streamId and streamInfo |
|IRTCEngineEventHandler |onRemoteAudioStateChanged(const RemoteStreamKey& key, RemoteAudioState state, RemoteAudioStateChangeReason reason) |onRemoteAudioStateChanged(const char\* stream_id, const StreamInfo& stream_info, RemoteAudioState state, RemoteAudioStateChangeReason reason) |Parameter change: Changed RemoteStreamKey to streamId and streamInfo |
|IRTCEngineEventHandler |onRemoteVideoStateChanged(RemoteStreamKey key, RemoteVideoState state, RemoteVideoStateChangeReason reason) |onRemoteVideoStateChanged(const char\* stream_id, const StreamInfo& stream_info, RemoteVideoState state, RemoteVideoStateChangeReason reason) |Parameter change: Changed RemoteStreamKey to streamId and streamInfo |
|IRTCEngineEventHandler |onFirstRemoteVideoFrameRendered(const RemoteStreamKey key, const VideoFrameInfo& info) |onFirstRemoteVideoFrameRendered(const char\* stream_id, const StreamInfo& stream_info, const VideoFrameInfo& info) |Parameter change: Changed RemoteStreamKey to streamId and streamInfo |
|IRTCEngineEventHandler |onFirstRemoteVideoFrameDecoded(const RemoteStreamKey key, const VideoFrameInfo& info) |onFirstRemoteVideoFrameDecoded(const char\* stream_id, const StreamInfo& stream_info, const VideoFrameInfo& info) |Parameter change: Changed RemoteStreamKey to streamId and streamInfo |
|IRTCEngineEventHandler |onFirstLocalVideoFrameCaptured(StreamIndex index, VideoFrameInfo info) |onFirstLocalVideoFrameCaptured(IVideoSource\* video_source, VideoFrameInfo info) |Parameter change: Changed streamIndex to VideoSource |
|IRTCEngineEventHandler |onLocalVideoSizeChanged(StreamIndex index, const VideoFrameInfo& info) |onLocalVideoSizeChanged(IVideoSource\* video_source, const VideoFrameInfo& info) |Parameter change: Changed streamIndex to VideoSource |
|IRTCEngineEventHandler |onRemoteVideoSizeChanged(RemoteStreamKey key, const VideoFrameInfo& info) |onRemoteVideoSizeChanged(const char\* stream_id, const StreamInfo& stream_info, const VideoFrameInfo& info) |Parameter change: Changed RemoteStreamKey to streamId and streamInfo |
|IRTCEngineEventHandler |onFirstLocalAudioFrame(StreamIndex index) |onFirstLocalAudioFrame(IAudioSource\* audio_source) |Parameter change: Changed streamIndex to AudioSource |
|IRTCEngineEventHandler |onFirstRemoteAudioFrame(const RemoteStreamKey& key) |onFirstRemoteAudioFrame(const char\* stream_id, const StreamInfo& stream_info) |Parameter change: Changed RemoteStreamKey to streamId and streamInfo |
|IRTCEngineEventHandler |onSEIMessageReceived(RemoteStreamKey stream_key, const uint8_t\* message, int length) |onSEIMessageReceived(const char\* stream_id, const StreamInfo& stream_info, const uint8_t\* message, int length) |Parameter change: Changed RemoteStreamKey to streamId and streamInfo |
|IRTCEngineEventHandler |onSEIStreamUpdate(const RemoteStreamKey& key, SEIStreamEventType type) |onSEIStreamUpdate(const char\* stream_id, const StreamInfo& stream_info, SEIStreamEventType type) |Parameter change: Changed RemoteStreamKey to streamId and streamInfo |
|IRTCEngineEventHandler |onRecordingStateUpdate(StreamIndex type, RecordingState state, RecordingErrorCode error_code, RecordingInfo info) |onRecordingStateUpdate(IVideoSource\* video_source, RecordingState state, RecordingErrorCode error_code, RecordingInfo info) |Parameter change: Changed streamIndex to VideoSource |
|IRTCEngineEventHandler |onRecordingProgressUpdate(StreamIndex type, RecordingProgress process, RecordingInfo info) |onRecordingProgressUpdate(IVideoSource\* video_source, RecordingProgress process, RecordingInfo info) |Parameter change: Changed streamIndex to VideoSource |
|IRTCEngineEventHandler |onStreamSyncInfoReceived(RemoteStreamKey stream_key, SyncInfoStreamType stream_type, const uint8_t\* data, int32_t length) |onStreamSyncInfoReceived(const char\* stream_id, const StreamInfo& stream_info, SyncInfoStreamType stream_type, const uint8_t\* data, int32_t length) |Parameter change: Changed RemoteStreamKey to streamId and streamInfo |
|IRTCEngineEventHandler |onAudioFrameSendStateChanged(const char\* room_id, const RtcUser& user, FirstFrameSendState state) |onAudioFrameSendStateChanged(const char\* stream_id, const StreamInfo& stream_info, const RtcUser& user, FirstFrameSendState state) |Parameter change: Changed roomId to streamId and streamInfo |
|IRTCEngineEventHandler |onVideoFrameSendStateChanged(const char\* room_id, const RtcUser& user, FirstFrameSendState state) |onVideoFrameSendStateChanged(const char\* stream_id, const StreamInfo& stream_info, const RtcUser& user, FirstFrameSendState state) |Parameter change: Changed roomId to streamId and streamInfo |
|IRTCEngineEventHandler |onAudioFramePlayStateChanged(const char\* room_id, const RtcUser& user, FirstFramePlayState state) |onAudioFramePlayStateChanged(const char\* stream_id, const StreamInfo& stream_info, const RtcUser& user, FirstFramePlayState state) |Parameter change: Changed roomId to streamId and streamInfo |
|IRTCEngineEventHandler |onVideoFramePlayStateChanged(const char\* room_id, const RtcUser& user, FirstFramePlayState state) |onVideoFramePlayStateChanged(const char\* stream_id, const StreamInfo& stream_info, const RtcUser& user, FirstFramePlayState state) |Parameter change: Changed roomId to streamId and streamInfo |
|IRTCEngineEventHandler |onSimulcastSubscribeFallback(const RemoteStreamSwitch& event) |onSimulcastSubscribeFallback(const char\* stream_id, const StreamInfo& stream_info, const bytertc::RemoteStreamSwitch& event) |Parameter change: Added streamId and streamInfo parameters |
|IRTCEngineEventHandler |onPerformanceAlarms(bytertc::PerformanceAlarmMode mode, const char\* room_id, bytertc::PerformanceAlarmReason reason, const bytertc::SourceWantedData& data) |onPerformanceAlarms(const char\* stream_id, const StreamInfo& stream_info, bytertc::PerformanceAlarmMode mode, bytertc::PerformanceAlarmReason reason, const bytertc::SourceWantedData& data) |Parameter change: Added streamId and streamInfo parameters |
|IRTCRoomEventHandler |onLocalStreamStats(const LocalStreamStats& stats) |onLocalStreamStats(const char\* stream_id, const bytertc::StreamInfo& stream_info, const LocalStreamStats& stats) |Parameter change: Added streamId and streamInfo parameters |
|IRTCRoomEventHandler |onRemoteStreamStats(const char\* stream_id, const bytertc::StreamInfo& stream_info, const RemoteStreamStats& stats) |onRemoteStreamStats(const RemoteStreamStats& stats) |Parameter change: Added streamId and streamInfo parameters |
|ILocalEncodedVideoFrameObserver |onLocalEncodedVideoFrame(StreamIndex type, const IEncodedVideoFrame& video_stream)) |onLocalEncodedVideoFrame(IVideoSource \*video_source, const IEncodedVideoFrame& video_stream) |Parameter change: Changed streamIndex to VideoSource |
|IRemoteEncodedVideoFrameObserver |onRemoteEncodedVideoFrame(const RemoteStreamKey& stream_info, const IEncodedVideoFrame& video_stream) |onRemoteEncodedVideoFrame(const char\* stream_id, const StreamInfo& stream_info, const IEncodedVideoFrame& video_stream) |Parameter change: Changed RemoteStreamKey to streamId and streamInfo |
|ISnapshotResultCallback |onTakeLocalSnapshotResult(long task_id, StreamIndex stream_index, IVideoFrame\* image, int error_code) |onTakeLocalSnapshotResult(long task_id, IVideoSource\* video_source, IVideoFrame\* image, int error_code) |Parameter change: Changed streamIndex to VideoSource |
|ISnapshotResultCallback |onTakeRemoteSnapshotResult(long task_id, RemoteStreamKey stream_key, IVideoFrame\* image, int error_code) |onTakeRemoteSnapshotResult(long task_id, const char\* stream_id, const StreamInfo& stream_info, IVideoFrame\* image, int error_code) |Parameter change: Changed RemoteStreamKey to streamId and streamInfo |
|IAudioFrameObserver |onRemoteUserAudioFrame(const RemoteStreamKey& stream_info, const IAudioFrame& audio_frame) |onRemoteUserAudioFrame(const char\* stream_id, const StreamInfo& stream_info, const IAudioFrame& audio_frame) |Parameter change: Changed RemoteStreamKey to streamId and streamInfo |
|IAudioFrameProcessor |onProcessRemoteUserAudioFrame(const RemoteStreamKey& stream_info, IAudioFrame& audio_frame) |onProcessRemoteUserAudioFrame(const char\* stream_id, const StreamInfo& stream_info, IAudioFrame& audio_frame) |Parameter change: Changed RemoteStreamKey to streamId and streamInfo |
|IExternalVideoEncoderEventHandler |onStart(StreamIndex index) |onStart(const char\* stream_id, const StreamInfo& stream_info) |Parameter change: Changed streamIndex to streamId and streamInfo |
|IExternalVideoEncoderEventHandler |onStop(StreamIndex index) |onStop(const char\* stream_id, const StreamInfo& stream_info) |Parameter change: Changed streamIndex to streamId and streamInfo |
|IExternalVideoEncoderEventHandler |onRateUpdate(StreamIndex index, int32_t video_index, VideoRateInfo info) |onRateUpdate(const char\* stream_id, const StreamInfo& stream_info, int32_t video_index, VideoRateInfo info) |Parameter change: Changed streamIndex to streamId and streamInfo |
|IExternalVideoEncoderEventHandler |onRequestKeyFrame(StreamIndex index, int32_t video_index) |onRequestKeyFrame(const char\* stream_id, const StreamInfo& stream_info, int32_t video_index) |Parameter change: Changed streamIndex to streamId and streamInfo |
|IExternalVideoEncoderEventHandler |onActiveVideoLayer(StreamIndex index, int32_t video_index, bool active) |onActiveVideoLayer(const char\* stream_id, const StreamInfo& stream_info, int32_t video_index, bool active) |Parameter change: Changed streamIndex to streamId and streamInfo |
|ILocalEncodedAudioFrameObserver |onLocalEncodedAudioFrame(StreamIndex type, const EncodedAudioFrameData& audio_stream) |onLocalEncodedAudioFrame(IAudioSource\* audio_source, const EncodedAudioFrameData& audio_stream) |Parameter change: Changed streamIndex to AudioSource |

## Type Changes

### Room Mode

|Type Name |V3.58 |V3.60 |Description |
|---|---|---|---|
|RoomProfileType |kRoomProfileTypeChat = 5<br><br>kRoomProfileTypeLwTogether = 7 |kRoomProfileTypeCall = 19 |Focuses on smoothness, with relatively low default video bitrate, low audio quality requirements, and high smoothness requirements. |
||kRoomProfileTypeGameHD = 8<br><br>kRoomProfileTypeCoHost = 9<br><br>kRoomProfileTypeKTV = 11<br><br>kRoomProfileTypeVRChat = 13<br><br>kRoomProfileTypeLanLiveStreaming = 15<br><br>kRoomProfileTypeLiveBroadcasting = 1 |kRoomProfileTypeLive = 20 |Focuses more on video quality, with relatively high default video bitrate and high audio quality requirements. |

### Custom Stream Processing

|Change Type |V3.58 |V3.60 |
|---|---|---|
|Name change, default value change |LocalVideoRenderPosition |Name changed to: LocalVideoSinkPosition. Default value changed: from kLocalVideoRenderPositionAfterCapture (before preprocessing) to kLocalVideoSinkPositionAfterPreProcess (after preprocessing). |
|Name change |RemoteVideoRenderPosition |RemoteVideoSinkPosition |
|Name change |VideoRenderMirrorType |VideoSinkMirrorType |

### Video Frame Related

|Change Type |V3.58 |V3.60 |Description |
|---|---|---|---|
|Parameter change |IVideoFrame |VideoFrameData |Specific changes as follows:<br><br><br>* **Changed parameters**:<br><br>   * frameType() changed to bufferType()<br><br>   * videoContentType() changed to contentType()<br><br>   * getPlaneData(int plane_index) changed to planeData(int plane_index)<br><br>   * getPlaneStride(int plane_index) changed to planeStride(int plane_index)<br><br>   * getExtraDataInfo(int& size) changed to seiData(int& size)<br><br>   * getTexMatrix(float matrix[16]) changed to textureMatrix(float matrix[16])<br><br>   * getTextureId() changed to textureId(), getCameraId() changed to cameraId()<br><br>   * getHwaccelContext() changed to hwContext()<br><br>   * getHwaccelBuffer() changed to hwBuffer()<br><br>* **Removed parameters**:<br><br>   * Removed colorSpace()<br><br>   * Removed flip()<br><br>   * Removed getSupplementaryInfo(int& size)<br><br>   * Removed release()<br><br>   * Removed toI420()<br><br>   * Removed shadowCopy()<br><br>   * Removed getAndroidHwaccelContext()<br><br>* **Added parameters**:<br><br>   * Added addRef()<br><br>   * Added releaseRef() |

### Mixed Stream Push Events

* Name replacement: `StreamMixingEvent` changed to `MixedStreamTaskEvent`, sharing the same event enumeration class with WTN stream tasks.

* Enumeration value changes as follows:

|**Description** |**V3.58** |**V3.60** |
|---|---|---|
|Request to start task<br><br>Push stream success |kStreamMixingEventStart = 1<br><br>kStreamMixingEventStartSuccess = 2 |kMixedStreamTaskEventStartSuccess = 1 |
|Task start failed |kStreamMixingEventStartFailed= 3 |kMixedStreamTaskEventStartFailed = 2<br><br>See MixedStreamTaskErrorCode for specific failure reasons |
|Request update<br><br>Task update success |kStreamMixingEventUpdate = 4<br><br>kStreamMixingEventUpdateSuccess = 5 |kMixedStreamTaskEventUpdateSuccess = 3 |
|Task update failed |kStreamMixingEventUpdateFailed = 6 |kMixedStreamTaskEventUpdateFailed = 4<br><br>See MixedStreamTaskErrorCode for specific failure reasons |
|Request to end task<br><br>Task end success |kStreamMixingEventStop = 7<br><br>kStreamMixingEventStopSuccess = 8 |kMixedStreamTaskEventStopSuccess = 5 |
|Task end failed |kStreamMixingEventStopFailed = 9 |kMixedStreamTaskEventStopFailed = 6<br><br>See MixedStreamTaskErrorCode for specific failure reasons |
|Parameter error |kStreamMixingEventRequestParamError = 15 |Calling startPushMixedStream or updatePushMixedStream returns kReturnStatusParameterErr = \-2 |
|Task processing timeout, please check network status and retry |kStreamMixingEventUpdateTimeout = 13<br><br>kStreamMixingEventStartTimeout = 14 |Calling startPushMixedStream or updatePushMixedStream returns kMixedStreamTaskErrorCodeTimeout = 1091 |
|Add image to mixed stream |kStreamMixingEventMixImageEvent = 16 |kMixedStreamTaskEventWarning = 7<br><br>See MixedStreamTaskErrorCode for specific failure reasons |
|Warning event |None |kMixedStreamTaskEventWarning = 7 |
|Others |kStreamMixingEventFirstAudioFrameByClientMix = 11<br><br>kStreamMixingEventFirstVideoFrameByClientMix = 12<br><br>kStreamMixingEventChangeMixType = 10 |Removed |

### Single Stream Push Events

* Name change: Changed from `SingleStreamPushEvent` to `SingleStreamTaskEvent`.

* Specific enumeration value changes as follows

|Description |V3.58 |V3.60 |
|---|---|---|
|Start push stream |kSingleStreamPushEventStart = 1 |kSingleStreamTaskEventStartSuccess = 1 |
|Push stream success |kSingleStreamPushEventStartSuccess = 2 |kSingleStreamTaskEventStartSuccess = 1 |
|Push stream failed |kSingleStreamPushEventStartFailed = 3 |kSingleStreamTaskEventStartFailed = 2 |
|Stop push stream |kSingleStreamPushEventStop = 4 |kSingleStreamTaskEventStopSuccess = 3 |
|Single stream push live task processing timeout, please check network status and retry |kSingleStreamPushEventTimeout = 5 |kSingleStreamTaskEventWarning = 5, see SingleStreamTaskErrorCode for specific error information. |
|Parameter error |kSingleStreamPushEventParamError = 6 |Calling startPushSingleStream returns kReturnStatusParameterErr = \-2. |
|Stop push stream failed |None |kSingleStreamTaskEventStopFailed = 4 |

### Audio and Video Stream Statistics

|Function |Changed Data Type |Description |
|---|---|---|
|Local audio stream statistics |LocalAudioStats |Added fields audio_device_loop_delay (audio capture playback delay), encode_frame_rate (audio encoding frame rate) |
|Remote audio stream statistics |RemoteAudioStats |Added field decode_frame_rate (audio decoding frame rate) |
|Remote video stream statistics |RemoteVideoStats |Added fields cap_to_render_delay (delay from sender capture start to receiver rendering completion), av_sync_diff_ms (audio\-video sync difference), codec_elapse_per_frame (average video decoding time) |

### Custom Encryption Type

|Function |Changed Data Type |Description |
|---|---|---|
|Parameter change |EncryptType |kEncryptTypeCustomize = 0 changed to kEncryptTypeNone = 0, to disable built\-in encryption. If setCustomizeEncryptHandler has been called to set custom encryption, calling setEncryptInfo with 0 will disable custom encryption. To enable custom encryption, you need to call setCustomizeEncryptHandler to reset it. (Before the change, custom encryption would not be disabled) |

### Others

|Function |Name |Description |
|---|---|---|
|Publish state change reason |PublishStateChangeReason |**New class** |
|Screenshot error code |SnapshotErrorCode |**New enumeration**<br><br>Screenshot success (0, kSnapshotErrorCodeOk)<br><br>Screenshot error. Failed to generate image data or RGBA encoding failed (\-1, kSnapshotErrorCodeCreateFail)<br><br>Screenshot error. Stream invalid (\-2, kSnapshotErrorCodeStreamInvalid)<br><br>Screenshot error. Screenshot timeout, timeout duration 1 second (\-3, kSnapshotErrorCodeTimeout)<br><br>Screenshot error. Image save failed (\-4, kSnapshotErrorCodeFileSaveError) |
|Audio scenario type |AudioScenarioType |**Enumeration value added**<br><br>Education scenario. Suitable for high\-quality scenarios mainly focused on voice teaching content (4, kAudioScenarioTypeEducation)<br><br>AI conversation scenario (5, kAudioScenarioTypeAiClient) |
|Ear monitor Audio Filter type |EarMonitorAudioFilter |**New enumeration**<br><br>No Audio Filter (default setting) (0x0001, kEarMonitorAudioFilterNone)<br><br>Ear monitor reuses 3A processing (0x8000, kEarMonitorAudioFilterReuseAudioProcessing) |
|Login error code |LoginErrorCode |**Error code added:** <br><br>Added login error code \-1004, representing current restricted mode<br><br>Using RTS capabilities in restricted mode has the following limitations:<br><br>Supports in\-room broadcast and point\-to\-point;<br><br>Message sending rate does not exceed 30KB/second;<br><br>Message sending frequency does not exceed 60 packets/second;<br><br>Message packet length does not exceed 1KB;<br><br>Switching between restricted/unrestricted modes needs to be set in the Volcano console. |
|Single stream push live error code |SingleStreamTaskErrorCode |**Enumeration value added**<br><br>Server detects invalid task parameters (1093, kSingleStreamTaskErrorCodeInvalidParamByServer)<br><br>Push task user ID in target room is kicked out of target room (1094, kSingleStreamTaskErrorRemoteKicked)<br><br>Push task failed to join target room (1095, kSingleStreamTaskErrorCodeJoinDestRoomFailed)<br><br>Push task pull stream timeout in source room (1096, kSingleStreamTaskErrorCodeReceiveSrcStreamTimeout)<br><br>Audio and video encoding push task not supported (1097, kSingleStreamTaskErrorCodeNotSurportCodec) |
|Single stream push configuration target room information |DestInfo |**New class** |
|Single stream push type |SingleStreamPushType |**Enumeration added**<br><br>Single stream push to CDN (1, kPushToCDN)<br><br>Single stream push to RTC room (2, kPushToRTC) |
|Single stream push live configuration parameters |PushSingleStreamParam |**Member added**<br><br>Added to single stream push live configuration parameters: single stream push configuration target room information list (dest_info), number of push target rooms, array length of `dest_info` (dest_info_size), push type (push_type) three members |
|Mirror type |MirrorType |**Enumeration value added**<br><br>No mirror effect during local preview, mirror effect only during encoding transmission (2, ByteRTCMirrorTypeEncoder) |

## Error Code Changes

### Callback Warning \- WarningCode

|V3.58 |V3.60 |
|---|---|
|kWarningCodeOldRoomBeenReplaced = \-2016 |**Removed**:<br><br>When creating a room again with the same roomId, the previously created room instance will be returned, and this error code will no longer be triggered. |

### WTN Stream Error Code (Formerly Public Stream)

* Error code name change: `PublicStreamErrorCode` changed to `MixedStreamTaskErrorCode`, sharing the same enumeration class with mixed stream push tasks.

* Specific error code change details as follows:

|Description |V3.58 |V3.60 |
|---|---|---|
|Success |kPublicStreamErrorCodeOK = 0 |kMixedStreamTaskErrorCodeOK = 0 |
|Server parameter validation failed |kPublicStreamErrorCodePushInvalidParam = 1191 |Deleted, this type of error will not be called back. |
|Server internal error |kPublicStreamErrorCodePushInvalidStatus = 1192 |Deleted, this type of error will not be called back. |
|Server unknown error |kPublicStreamErrorCodePushInternalError = 1193 |Deleted, this type of error will not be called back. |
|Task failed |kPublicStreamErrorCodePushFailed = 1195 |kMixedStreamTaskErrorCodePushWTNFailed = 1195 |
|Task timeout |kPublicStreamErrorCodePushTimeout = 1196 |kMixedStreamTaskErrorCodeTimeout = 1091 |
|Stream subscription timeout |kPublicStreamErrorCodePullNoPushStream = 1300 |WTNSubscribeStateChangeReason.kWTNSubscribeStateChangeReasonUnsubscribe = 1300, returned through onWTNVideoSubscribeStateChanged or onWTNAudioSubscribeStateChanged. |

### Mixed Stream Push Error Code

* Error code name change: `StreamMixingErrorCode` changed to `MixedStreamTaskErrorCode`, sharing the same enumeration class with WTN stream tasks.

* Specific error code change details as follows:

|Description |V3.58 |V3.60 |
|---|---|---|
|Push stream success |kStreamMixingErrorCodeCodeOK = 0 |kMixedStreamTaskErrorCodeOK = 0 |
|Undefined mixed stream error |kStreamMixingErrorCodeCodeBase = 1090 |None, this error code is not enabled. |
|Client SDK detected invalid push stream parameters |kStreamMixingErrorCodeCodeInvalidParam = 1091 |Calling startPushMixedStream or updatePushMixedStream returns kReturnStatusParameterErr = \-2. |
|State error, operation needs to be initiated under normal state machine state |kStreamMixingErrorCodeCodeInvalidState = 1092 |kMixedStreamTaskErrorCodeInvalidStateByServer = 1094 |
|Invalid operation |kStreamMixingErrorCodeCodeInvalidOperator = 1093 |kMixedStreamTaskErrorCodeInvalidStateByServer = 1094 |
|Push live task processing timeout, please check network status and retry |kStreamMixingErrorCodeCodeTimeOut = 1094 |kMixedStreamTaskErrorCodeTimeOut = 1091 |
|Server detected incorrect push stream parameters |kStreamMixingErrorCodeCodeInvalidParamByServer = 1095 |kMixedStreamTaskErrorCodeInvalidParamByServer = 1092 |
|Stream subscription timeout |kStreamMixingErrorCodeCodeSubTimeoutByServer = 1096 |kMixedStreamTaskErrorCodeSubTimeoutByServer = 1093 |
|Mixed stream server internal error |kStreamMixingErrorCodeCodeInvalidStateByServer = 1097 |kMixedStreamTaskErrorCodeInvalidStateByServer = 1094 |
|Mixed stream server push CDN failed |kStreamMixingErrorCodeCodeAuthenticationByCDN = 1098 |kMixedStreamTaskErrorCodeAuthenticationByCDN = 1095 |
|Server signaling reception timed out. Please check your network status and try again. |kStreamMixingErrorCodeCodeTimeoutBySignaling = 1099 |kMixedStreamTaskErrorCodeSignalRequestTimeout = 1097 |
|Image mixing failed |kStreamMixingErrorCodeCodeMixImageFail = 1100 |kMixedStreamTaskErrorCodeMixImageFailed = 1098 |
|Server unknown error |kStreamMixingErrorCodeCodeUnKnownErrorByServer = 1101 |kMixedStreamTaskErrorCodeUnKnownErrorByServer = 1096 |

### Single Stream Push Error Code

* Error code replacement: replaced by `SingleStreamTaskErrorCode` from `StreamMixingErrorCode`.

* Specific error code changes and corresponding details as follows:

|Description |V3.58 |V3.60 |
|---|---|---|
|Push stream success |TRANSCODER_ERROR_OK = 0 |kSingleStreamTaskErrorCodeOK = 0 |
|Undefined mixed stream error |TRANSCODER_ERROR_BASE = 1090 |None, this error code is not enabled. |
|Client SDK detected invalid push stream parameters |TRANSCODER_ERROR_INVALID_PARAM = 1091 |Calling startPushSingleStream returns kReturnStatusParameterErr = \-2. |
|State error, operation needs to be initiated under normal state machine state |TRANSCODER_ERROR_INVALID_STATE = 1092 |None, single stream task will not trigger this error code. |
|Invalid operation |TRANSCODER_ERROR_INVALID_OPERATOR = 1093 |None, single stream task will not trigger this error code. |
|Push live task processing timeout, please check network status and retry |TRANSCODER_ERROR_TIMEOUT = 1094 |None, single stream task will not trigger this error code. |
|Server detected incorrect push stream parameters |TRANSCODER_ERROR_INVALID_PARAM_BY_SERVER = 1095 |None, single stream task will not trigger this error code. |
|Stream subscription timeout |TRANSCODER_ERROR_SUB_TIMEOUT_BY_SERVER = 1096 |None, single stream task will not trigger this error code. |
|Mixed stream server internal error |TRANSCODER_ERROR_INVALID_STATE_BY_SERVER = 1097 |None, single stream task will not trigger this error code. |
|Mixed stream server push CDN failed |TRANSCODER_ERROR_AUTHENTICATION_BY_CDN = 1098 |None, single stream task will not trigger this error code. |
|Server receiving signaling timeout, please check network status and retry |TRANSCODER_ERROR_TIMEOUT_BY_SIGNALING = 1099 |kSingleStreamTaskErrorCodeSignalRequestTimeout = 1092 |
|Image mixing failed |TRANSCODER_ERROR_MIX_IMAGE_FAIL = 1100 |None, single stream task will not trigger this error code. |
|Server unknown error |TRANSCODER_ERROR_UNKNOW_ERROR_BY_SERVER = 1101 |kSingleStreamTaskErrorCodeUnKnownByServer = 1091 |

### Other Error Codes

Removed some error codes that have been deprecated for multiple versions:

|Description |Error Code |
|---|---|
|The room ID passed to createRTCRoom is invalid. The method will return null and trigger this error. |kRoomErrorCodeRoomIdIllegal = \-1007 |
|A room with the same roomId already exists in call loop detection. |kErrorCodeRoomAlreadyExist = \-1013 |
|Get room information failed warning. |kWarningCodeGetRoomFailed = \-2000 |
|When auto\-subscribe mode is not turned off, attempting to enable manual subscribe mode will trigger this warning. |kWarningCodeSubscribeStreamForbiden = \-2010 |
|Total number of published streams exceeds the limit. |kErrorCodeOverScreenPublishLimit = \-1081 |
|Public stream parameter exception, please modify parameters and retry. |kPublicStreamErrorCodePushInvalidParam = 1191 |
|Server status exception, will automatically retry. |kPublicStreamErrorCodePushInvalidStatus = 1192 |
|Internal error, unrecoverable, please retry. |kPublicStreamErrorCodePushInternalError = 1193 |
|Publish failed. The system will automatically retry. Pay attention to the retry results. |kPublicStreamErrorCodePushFailed = 1195 |
|Publish failed. The system will retry after 10 seconds and automatically stop after 3 retries. |kPublicStreamErrorCodePushTimeout = 1196 |

## New Interfaces

|Interface |Function Description |
|---|---|
|IRTCEngine::createRTSRoom |Create RTS room |
|IRTCRoom::getCallId |Get call ID. This method needs to be called after joining the room |
|IRemoteEncodedAudioFrameObserver::onRemoteEncodedAudioFrame |After calling RegisterRemoteEncodedAudioFrameObserver, when SDK receives remote audio frame information, this event is called back |
|IRTCEngine::muteScreenAudioCapture |Set whether to mute the recording signal of screen audio source (does not change local hardware). |
|IRTCRoom::setStreamExtraInfo |Set additional information for the current push stream. |
|IRTCRoomEventHandler::onRoomStreamExtraInfoUpdate |Receive callback for stream additional information set by other users calling setStreamExtraInfo in the same room. |
|IRTCEngine::takeLocalSnapshotToFile |Capture local video stream frame, generate JPG file, and save to specified local path. |
|IRTCEngine::takeRemoteSnapshotToFile |Capture remote video stream frame, generate JPG file, and save to specified local path. |
|IRTCEngineEventHandler::onLocalSnapshotTakenToFile |When capturing video frame with takeSnapshotToFile:filePath:, this callback reports whether the screenshot was successful and the captured image information. |
|IRTCEngineEventHandler::onRemoteSnapshotTakenToFile |When capturing video frame with takeSnapshotToFile:filePath:, this callback reports whether the screenshot was successful and the captured image information. |
|setEarMonitorMode |New interface ear monitor supports reusing locally captured audio after custom processing |
|setWTNStreamEventHandler |Set WTN stream callback interface |
|onRoomEvent |Room event callback, and added enumeration RoomEventInfo |
|createGameRoom |Create game room instance |
|IGameRoom.joinRoom |Join game room |
|IGameRoom.updateToken |Game room update token |
|IGameRoom.setRTCRoomEventHandler |Set event callback object for game room, monitor corresponding callback events |
|IGameRoom.getRangeAudio |Get range audio interface instance |
|IGameRoom.enableMicrophone |Start or stop audio capture |
|IGameRoom.enableSpeakerphone |Turn on/off speaker |
|IGameRoom.enableAudioSend |Start or stop audio sending |
|IGameRoom.enableAudioReceive |Whether to listen to a certain user's voice |
|IGameRoom.setRemoteRoomAudioPlaybackVolume |Adjust audio playback volume of all remote users in a certain room |

## Deleted/Deprecated Interfaces

Removed deprecated or not recommended methods, specifically as follows:

|Change Details |Removed/Deprecated Interface |Alternative Interface |
|---|---|---|
|Deprecated |setLocalVideoSink(IVideoSink\* video_sink, IVideoSink::PixelFormat required_format) |setLocalVideoSink(IVideoSink\* video_sink, LocalVideoSinkConfig& config) = 0 |
|Deprecated |setRemoteVideoSink(RemoteStreamKey stream_key, IVideoSink\* video_sink, IVideoSink::PixelFormat required_format) |setRemoteVideoSink(const char\* stream_id, IVideoSink\* video_sink, RemoteVideoSinkConfig& config) |
|Deleted |createRTCVideo(const char\* app_id, bytertc::IRTCVideoEventHandler *event_handler, const char* parameters) |createRTCEngine(const EngineConfig& config, IRTCEngineEventHandler\* event_handler) |
|Deprecated |startScreenAudioCapture() |startScreenAudioCapture(const char device_id[MAX_DEVICE_ID_LENGTH]) = 0;<br><br>New interface supports controlling whether to capture audio from specific processes for screen sharing through parameters. The new interface can replace the old interface functionality by passing nullptr or leaving empty, that is, capturing audio from the entire system. |
|Deleted |IAudioDeviceManager::enableFilterSilentDevice(bool enable) |If you need to use the filter silent device functionality, please contact technical support. |
|Deleted |IVideoFrame.buildVideoFrame |Use VideoFrameData as replacement. |
|Deleted |getErrorDescription |No alternative interface |
|Deleted |* startASR(const RTCASRConfig& asr_config, IRTCASREngineEventHandler\* handler)<br><br>* stopASR() |If you need to use ASR functionality, it can be implemented through real\-time subtitle functionality related interfaces: startSubtitle, stopSubtitle |
|Deleted |onError(int err) |If you need to use ASR functionality, it can be implemented through real\-time subtitle functionality related interfaces: onSubtitleStateChanged, onSubtitleMessageReceived |
|Deleted |subscribeUserStream(const char\* user_id, StreamIndex stream_type, SubscribeMediaType media_type, const SubscribeVideoConfig& video_config) |* subscribeStreamVideo(const char \*stream_id, bool subscribe)<br><br>* subscribeStreamAudio(const char \*stream_id, bool subscribe) |
|Deleted |onRoomError(int err) |onRoomStateChanged(const char\* room_id, const char\* uid, int state, const char\* extra_info) |
|Deleted |IAudioMixingManager |IMediaPlayer<br><br>IAudioEffectPlayer |
|Deleted |onAudioMixingStateChanged(int mix_id, bytertc::AudioMixingState state, bytertc::AudioMixingError error) |onMediaPlayerStateChanged( int player_id, PlayerState state, PlayerError error)<br><br>onAudioEffectPlayerStateChanged(int effect_id, PlayerState state, PlayerError error) |
|Deleted |1. startLiveTranscoding(const char\* task_id, ITranscoderParam\* param, ITranscoderObserver\* observer)<br><br>2. stopLiveTranscoding(const char\* task_id)<br><br>3. updateLiveTranscoding(const char\* task_id, ITranscoderParam\* param) |1. startPushMixedStream(const char\* task_id, MixedStreamPushTargetConfig push_target_config, IMixedStreamConfig\* config)<br><br>2. stopPushMixedStream(const char\* task_id, MixedStreamPushTargetType target_type)<br><br>3. updatePushMixedStream(const char\* task_id, MixedStreamPushTargetConfig push_target_config, IMixedStreamConfig\* config) |
|Deleted |muteAudioPlayback(MuteState mute_state) |setPlaybackVolume(const int volume) |
|Deleted |1. onMediaDeviceStateChanged(const char\* device_id, bytertc::MediaDeviceType device_type, bytertc::MediaDeviceState device_state, bytertc::MediaDeviceError device_error)<br><br>2. onMediaDeviceWarning(const char\* device_id, bytertc::MediaDeviceType device_type, bytertc::MediaDeviceWarning device_warning)<br><br>3. onHttpProxyState(int state)<br><br>4. onHttpsProxyState(int state)<br><br>5. onSocks5ProxyState(int state, const char\* cmd, const char\* proxy_address, const char\* local_address, const char\* remote_address)<br><br>6. onUserMuteAudio(const char\* room_id, const char\* user_id, MuteState mute_state)<br><br>7. onUserMuteVideo(const char\* room_id, const char\* uid, MuteState mute) |1. onAudioDeviceStateChanged(const char\* device_id, bytertc::RTCAudioDeviceType device_type, bytertc::MediaDeviceState device_state, bytertc::MediaDeviceError device_error)<br><br>   onVideoDeviceStateChanged(const char\* device_id, bytertc::RTCVideoDeviceType device_type, bytertc::MediaDeviceState device_state, bytertc::MediaDeviceError device_error)<br><br>2. onAudioDeviceWarning(const char\* device_id, bytertc::RTCAudioDeviceType device_type, bytertc::MediaDeviceWarning device_warning)<br><br>   onVideoDeviceWarning(const char\* device_id, bytertc::RTCVideoDeviceType device_type, bytertc::MediaDeviceWarning device_warning)<br><br>3. onLocalProxyStateChanged(LocalProxyType local_proxy_type, LocalProxyState local_proxy_state, LocalProxyError local_proxy_error)<br><br>4. onLocalProxyStateChanged(LocalProxyType local_proxy_type, LocalProxyState local_proxy_state, LocalProxyError local_proxy_error)<br><br>5. onLocalProxyStateChanged(LocalProxyType local_proxy_type, LocalProxyState local_proxy_state, LocalProxyError local_proxy_error)<br><br>6. onUserPublishStreamAudio(const char\* stream_id, const StreamInfo& stream_info, bool is_publish)<br><br>7. onUserPublishStreamVideo(const char\* stream_id, const StreamInfo& stream_info, bool is_publish) |
|Deleted |1. ISpatialAudio.updatePosition(const Position& pos)<br><br>2. ISpatialAudio.updateSelfOrientation(const HumanOrientation& orientation)<br><br>3. ISpatialAudio.updateListenerPosition(const Position &pos)<br><br>4. ISpatialAudio.updateListenerOrientation(const HumanOrientation& orientation) |1. ISpatialAudio.updateSelfPosition(const PositionInfo& position_info)<br><br>2. ISpatialAudio.updateSelfPosition(const PositionInfo& position_info)<br><br>3. ISpatialAudio.updateRemotePosition(const char\* uid, const PositionInfo& position_info)<br><br>4. ISpatialAudio.updateRemotePosition(const char\* uid, const PositionInfo& position_info) |
|Deleted |1. IVideoEffect.checkLicense(void\* android_context, void\* jnienv, const char\* license_path)<br><br>2. IVideoEffect.setAlgoModelPath(const char\* model_path)<br><br>3. IVideoEffect.enableEffect(bool enabled)<br><br>4. IVideoEffect.updateNode(const char\* node_path, const char\* node_key, float node_value)<br><br>5. IVideoEffect.registerFaceDetectionObserver(IFaceDetectionObserver\* observer, int interval_ms)<br><br>6. IVideoEffect.setBackgroundSticker(const char\* model_path, const VirtualBackgroundSource& source) |1. IVideoEffect.initCVResource(const char\* license_file_path, const char\* algo_model_dir)<br><br>2. IVideoEffect.initCVResource(const char\* license_file_path, const char\* algo_model_dir)<br><br>3. IVideoEffect.enableVideoEffect()<br><br>4. IVideoEffect.updateEffectNode(const char\* effect_node_path, const char\* node_key, float node_value)<br><br>5. IVideoEffect.enableFaceDetection(IFaceDetectionObserver\* observer, unsigned int interval_ms, const char\* face_model_path)<br><br>6. IVideoEffect.enableVirtualBackground(const char\* background_sticker_path, const VirtualBackgroundSource& source) |
|Deleted |1. onScreenAudioFrameSendStateChanged(const char\* room_id, const RtcUser& user, FirstFrameSendState state)<br><br>2. onScreenVideoFramePlayStateChanged(const char\* room_id, const RtcUser& user, FirstFramePlayState state) |1. onAudioFrameSendStateChanged(String streamId, StreamInfo streamInfo, InternalRTCUser user, int state)<br><br>2. onVideoFrameSendStateChanged(String streamId, StreamInfo streamInfo, InternalRTCUser user, int state) |
|Deleted |RTCEngine (formerly RTCVideo) class defined the following methods:<br><br><br>* setOriginalScreenVideoInfo(int original_capture_width, int original_capture_height)<br><br>* setScreenAudioStreamIndex(StreamIndex index)<br><br>* pushScreenVideoFrame(const VideoFrameData& frame) |No alternative interface |

# 3.58

RTC SDK for Linux 3.58 is released.
