---
title: "iOS"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70020"
---

<span id="390dcf8d"></span>
# 3.60.105

<span id="89ee0ddb"></span>
## API Changes


|V3.60.104 |V3.60.105 |Change Description |
|---|---|---|
|`ByteRTCRoom.setRoomProfile:(ByteRTCRoomProfile)profile` |`ByteRTCRoom.setLiveMode:(ByteRTCRoomLiveMode)mode` |Renamed from `setRoomProfile:` to `setLiveMode:`. The parameter type changed from `ByteRTCRoomProfile` to `ByteRTCRoomLiveMode`. |
|`sendLivePushSEIMessage`: prerequisite was `ByteRTCRoomProfileLivePush` set via `joinRoom:userInfo:roomConfig:` |`sendLivePushSEIMessage`: prerequisite is `ByteRTCRoomLiveModeSoloHost` set via `setLiveMode:` |The prerequisite for calling `sendLivePushSEIMessage` changed from setting room profile to `ByteRTCRoomProfileLivePush` during `joinRoom:userInfo:roomConfig:` to calling `setLiveMode:` with `ByteRTCRoomLiveModeSoloHost`. |


<span id="bb253ae5"></span>
## Type Changes


|Type Name |Change Description |
|---|---|
|`ByteRTCRoomLiveMode` |New enum type. Defines the live streaming mode:<br><br><br>* `ByteRTCRoomLiveModeCoHost` (value 1): Co\-hosted live streaming mode for multi\-person or interactive live scenarios.<br><br>* `ByteRTCRoomLiveModeSoloHost` (value 2): Single\-host live streaming mode. |
|`ByteRTCRoomProfile` |Removed enum values: `ByteRTCRoomProfileLinkMic` and `ByteRTCRoomProfileLivePush`. Use the new `ByteRTCRoomLiveMode` enum with `setLiveMode:` instead. |
|`ByteRTCRoomConfig` |Added `ByteRTCRoomLiveMode liveMode` property. Default value: `ByteRTCRoomLiveModeCoHost`. Specifies the live mode when joining a room. Only effective when `profile` is `ByteRTCRoomProfileLive`. Can be changed after joining via `setLiveMode:`. |
|`ByteRTCVideoEncoderConfig` |Added `NSInteger keyFrameIntervalMS` property. Default value: `0` (encoder determines automatically). Sets the key frame interval in milliseconds. |


<span id="7bb7fc4c"></span>
## New Interfaces


|Class / Module |Interface |Description |
|---|---|---|
|`ByteRTCRoom` |`setLiveMode:` |Sets the live streaming mode (co\-hosted / single\-host). Call after joining a room. |
|`ByteRTCEngine` |`sendLivePushSEIMessage:count:isKeyFrameOnly:allowOverwrite:` |Sends SEI data in Key\-Value (JSON) format through video frames. Requires `ByteRTCRoomLiveModeSoloHost` mode. |


<span id="d66057d4"></span>
## Deleted or Deprecated Interfaces


|Interface |Replacement |Description |
|---|---|---|
|`ByteRTCRoom.setRoomProfile:` |`ByteRTCRoom.setLiveMode:` |Replaced by `setLiveMode:` with the new `ByteRTCRoomLiveMode` enum. |


<span id="_3-60-104"></span>
# 3.60.104

<span id="api-changes"></span>
## API Changes


|Change Details |Interface |Notes |
|---|---|---|
|Added |`setRoomProfile:` |Sets room profile before or after joining a room. |
|Added |`sendLivePushSEIMessage:count:isKeyFrameOnly:allowOverwrite:` |Sends SEI (Supplemental Enhancement Information) data in Key\-Value format through video frames. |


<span id="type-changes"></span>
## Type Changes


|Change Details |Changed Data Type |Notes |
|---|---|---|
|New Enum Value Added |ByteRTCRoomProfile |New enum values:<br><br><br>* `ByteRTCRoomProfileLinkMic`: Link mic mode, focuses on high quality, same bitrate as LIVE.<br><br>* `ByteRTCRoomProfileLivePush`: Live push mode for broadcasting scenarios. |
|New Member Variable Added |ByteRTCVideoEncoderConfig |Added `keyFrameIntervalMS` field: Sets key frame interval in milliseconds, default: 0. |
|New Member Variable Added |ByteRTCVideoPreprocessorConfig |Added `actionDomain` field: Controls the effective range of your custom video preprocessor. |
|New Enum Added |ByteRTCProcessorActionDomain |Controls where the custom video preprocessor effects are applied:<br><br><br>* `ByteRTCProcessorActionDomainPreviewAndEncode`：Effects apply to both preview and transmission.<br><br>* `ByteRTCProcessorActionDomainPreview`：Effects apply only to local preview.<br><br>* `ByteRTCProcessorActionDomainEncode`：Effects apply only to outgoing stream. |


<span id="_3-60-103"></span>
# 3.60.103

<span id="api-changes"></span>
## API Changes

<span id="dependency-changes"></span>
### Dependency Changes

This version adds a required dependency `RTCFFmpeg.xcframework`.

<span id="header-files-and-base-class-names"></span>
### Header Files and Base Class Names


|Change Type |V3.58 |V3.60 |
|---|---|---|
|Header file name changes |../ByteRTCVideo.h |../ByteRTCEngine.h |
|Base class name changes (all modules) |ByteRTCVideo |ByteRTCEngine |
|Base class name changes (all modules) |ByteRTCVideoDelegate |ByteRTCEngineDelegate |
|New header files |None |../ByteRTCRTSRoom.h<br><br>../ByteRTCGameRoom.h |


<span id="engine-management"></span>
### Engine Management


|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|Create engine object |createRTCVideo:(NSString \* _Nonnull)appId delegate:(id_Nullable)delegate parameters:(NSDictionary \* _Nonnull)parameters; |createRTCEngine:(ByteRTCEngineConfig \* _Nonnull) config delegate:(id_Nullable)delegate |* **Name change**: `createRTCVideo` changed to `createRTCEngine`<br><br>* **Parameter change**:<br><br>* `parameters`, `appId`: moved into the new `ByteRTCEngineConfig` class, and `appId` name changed to `appID`<br><br>* ByteRTCVideoDelegate: renamed to ByteRTCEngineDelegate |
|Destroy engine |destroyRTCVideo |destroyRTCEngine |**Method name change** |
|Engine event callback |ByteRTCVideoDelegate |ByteRTCEngineDelegate |**Protocol name change** |


<span id="room-management"></span>
### Room Management


|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|Join room |joinRoom:(NSString \*_Nullable)token userInfo:(ByteRTCUserInfo \*_Nonnull)userInfo roomConfig:(ByteRTCRoomConfig \*Nonnull)roomConfig NS_SWIFT_NAME(joinRoom(:userInfo:roomConfig:)); |joinRoom:(NSString \*_Nullable)token userInfo:(ByteRTCUserInfo \*_Nonnull)userInfo userVisibility:(BOOL)userVisibility roomConfig:(ByteRTCRoomConfig *Nonnull)roomConfig NS_SWIFT_NAME(joinRoom(* :userInfo:userVisibility:roomConfig:)); |1. **Parameter change**:<br><br>2. **New parameter userVisibility**: specifies user visibility.<br><br>   It is recommended to set user visibility to false when joining the room, and then set it to true through setUserVisibility: when the user needs to send audio and video streams. Since the capacity of invisible users in a single room is much higher than that of visible users, enabling user visibility on demand can maximize the use of RTC call room resources and avoid the situation where subsequent users fail to join the room after the visible users in the RTC room reach the limit.<br><br>3. Parameters in ByteRTCRoomConfig: `isAutoPublish` is split into video isAutoPublishVideo and audio isAutoPublishAudio.<br><br>4. The enumeration of parameter `ByteRTCRoomProfile` (room mode) in ByteRTCRoomConfig has additions and deletions, please refer to the iOS section below for details.<br><br>5. **Behavior change**:<br><br>* V3.58:<br><br>* Join room defaults to automatically publish main stream, whether to publish audio stream or video stream when joining room is determined by calling publishVideoStream(false) and publishAudioStream(false)<br><br>* publishVideoStream/publishAudioStream are effective before and after joining room<br><br>* V3.60:<br><br>* Join room automatically publishes audio and video streams (main stream), whether the stream is published is determined by isPublishVideo and isPublishAudio in RTCRoomConfig.<br><br>* publishVideoStream/publishAudioStream single stream version scope is limited to after joining room, calling before joining room is invalid |
|Create room instance |createRTCRoom:(NSString \* _Nonnull)roomId |createRTCRoom:(NSString \* _Nonnull)roomId |**Behavior change**:<br><br>When creating a room instance with an existing roomId, it will return the previously created room instance and no longer trigger error code `ByteRTCWarningCodeOldRoomBeenReplaced = -2016` |
|Create room failure callback |rtcEngine:onCreateRoomStateChanged:errorCode: |rtcRoom:onRoomStateChanged:withUid:state:extraInfo: |**Interface replacement**:<br><br>Room creation failure is notified by rtcRoom:onRoomStateChanged:withUid:state:extraInfo:. No longer through onCreateRoomStateChanged callback. |
|Callback for setting room additional information result |onSetRoomExtraInfoResult:(NSInteger)taskId error:(ByteRTCSetRoomExtraInfoResult)error; |onSetRoomExtraInfoResult:(NSInteger)taskId result:(ByteRTCSetRoomExtraInfoResult)result; |**Parameter change**: `error` renamed to `result`. |
|Callback when remote visible user joins room, or invisible user in room switches to visible |onUserJoined:(ByteRTCUserInfo \*_Nonnull)userInfo elapsed:(NSInteger)elapsed; |onUserJoined:(ByteRTCUserInfo\*_Nonnull)userInfo; |**Parameter change**: removed invalid parameter `elapsed`. |


<span id="publish-and-subscribe-to-simulcast-streams"></span>
### Publish and Subscribe to Simulcast Streams


|Change Type |V3.58 |V3.60 |Description |
|---|---|---|---|
|Enable/disable pushing multiple video streams |enableSimulcastMode:(BOOL) enabled<br><br>After enabling, all set Simulcast streams will be published. |setLocalSimulcastMode:(ByteRTCVideoSimulcastMode)mode |* **Interface rename**<br><br>* **Function extension, parameter change**: removed `boolean enabled` from the old method, replaced with `(ByteRTCVideoSimulcastMode)mode`, allowing to specify the specific multi\-stream mode type through parameter `ByteRTCVideoSimulcastMode`.<br><br>* **Default behavior adjustment**:<br><br>* Old interface: when `enabled` is `true`, all set Simulcast streams will be published<br><br>* New interface: when `mode` parameter is set to `ByteRTCVideoSimulcastModeAlwaysSimulcast` = `2`, all set Simulcast streams will be published.<br><br>* **Call timing change**: the old method is called before joining room or after joining room but before publishing stream, the new method needs to be called before joining room. |
|Set parameters for expected subscription to remote video stream |setRemoteVideoConfig:(NSString \* _Nonnull) userId remoteVideoConfig:(ByteRTCRemoteVideoConfig \*_Nonnull) remoteVideoConfig |setRemoteSimulcastStreamType:(NSString \* _Nonnull) streamId streamType:(ByteRTCVideoSimulcastStreamType)streamType |* **Interface rename**<br><br>* **Parameter change**:<br><br>* Changed parameter userId to streamId, tracking stream instead of user.<br><br>* Replaced parameter `remoteVideoConfig` with `streamType`, no longer need to specify specific values, you can specify subscription preference by passing enumeration values. |
|Set or update encoding parameters for Simulcast stream |setVideoEncoderConfig:(NSArray <ByteRTCVideoEncoderConfig \*\> \* _Nullable) encoderConfigs |setLocalSimulcastMode:(ByteRTCVideoSimulcastMode)mode config:(NSArray <ByteRTCVideoEncoderConfig \*\> \* _Nullable)streamConfig |* **Interface replacement**<br><br>* **Parameter change**:<br><br>* Formal parameter `encoderConfigs` changed to `streamConfig`<br><br>* Added parameter `mode`, user specifies stream type (main stream or sub stream) |
|* Set single video stream parameters<br><br>* Set multiple video stream parameters |setMaxVideoEncoderConfig:(ByteRTCVideoEncoderConfig \* _Nullable) max_solution; |setVideoEncoderConfig:(ByteRTCVideoEncoderConfig \* _Nullable) encoderConfig; |* **Interface merge**<br><br>* **Function change**: new method is only used to set main stream encoding parameters.<br><br>* **Parameter change**: formal parameter changed to `encoderConfig` |


<span id="publish-and-subscribe-main-stream-camera-microphone-captured-stream"></span>
### Publish and Subscribe Main Stream (Camera/Microphone Captured Stream)


|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|1. **Publish/Unpublish Audio and Video Streams** | | | |
|API:<br><br><br>* Publish audio and video stream<br><br>* Unpublish audio and video stream |* publishStream:(ByteRTCMediaStreamType)type<br><br>* unpublishStream:(ByteRTCMediaStreamType)type |* publishStreamVideo:(BOOL)publish<br><br>* publishStreamAudio:(BOOL)publish |* **Interface split, function extension**:<br><br>* **Split by audio and video**: 2 new methods are used to control video stream and audio stream publishing respectively<br><br>* **Merge publish and unpublish**: new interface handles publish and unpublish operations through `(BOOL)publish` parameter<br><br>* **Parameter change**:<br><br>* Removed `(ByteRTCMediaStreamType)type`, new methods directly distinguish video and audio streams through method names<br><br>* Added `(BOOL)publish`<br><br>* **Behavior change**:<br><br>* V3.58: effective before and after joining room<br><br>* V3.60: scope is limited to after joining room, calling before joining room is invalid |
|Audio and video stream publish status change callback |* rtcRoom:( ByteRTCRoom \* _Nonnull)rtcRoom onUserPublishStream:(NSString \*_Nonnull)userId type:(ByteRTCMediaStreamType)type;<br><br>* rtcRoom:( ByteRTCRoom \* _Nonnull)rtcRoom onUserUnpublishStream:(NSString \*_Nonnull)userId type:(ByteRTCMediaStreamType)type reason:(ByteRTCStreamRemoveReason)reason; |* rtcRoom:(ByteRTCRoom\* _Nonnull)rtcRoom onUserPublishStreamAudio:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info isPublish:(BOOL)isPublish<br><br>* rtcRoom:(ByteRTCRoom\* _Nonnull)rtcRoom onUserPublishStreamVideo:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info isPublish:(BOOL)isPublish |* **Interface split rename, function extension**:<br><br>* **Split by audio and video**: 2 new methods are used for audio stream and video stream subscription callbacks respectively<br><br>* **Merge subscribe and unsubscribe status**: new interface uses `isPublish` parameter to represent publish and unpublish<br><br>* **Parameter change**:<br><br>* **Removed parameters**<br><br>* Removed `userId`, new method identifies through `streamId` parameter.<br><br>* Removed `type`, new method directly distinguishes video and audio streams through method names.<br><br>* Removed `reason`, no longer provides detailed information about removal reason.<br><br>* **Added parameter**: added `streamId` parameter to distinguish streams. |
|Callback when audio and video stream publish status triggers warning or error |rtcRoom:(ByteRTCRoom \*_Nonnull)rtcRoom onStreamStateChanged:(NSString \*_Nonnull)roomId withUid:(nonnull NSString \*)uid state:(NSInteger)state extraInfo:(NSString \*_Nonnull)extraInfo; |* rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onVideoPublishStateChanged:(NSString  *_Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info state:(ByteRTCPublishState)state reason:(ByteRTCPublishStateChangeReason)reason<br><br>* rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onAudioPublishStateChanged:(NSString  *_Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info state:(ByteRTCPublishState)state reason:(ByteRTCPublishStateChangeReason)reason |* **Interface split rename**: split by audio and video, new methods are used for video stream and audio stream publish status callbacks respectively<br><br>* **Parameter change**<br><br>* **Removed parameters**:<br><br>* Removed parameters `roomId` and `uid`;<br><br>* Removed invalid parameter `extraInfo`.<br><br>* **Added parameters**:<br><br>* Added `streamId` and `info` parameters to identify stream unique identifier and stream information;<br><br>* Added `reason` parameter to describe the specific reason for status change in more detail.<br><br>* **Parameter type change**: `state` parameter type changed from `NSInteger` to `ByteRTCPublishState` enumeration type to provide clearer status definition |
|2. **Subscribe/Unsubscribe Audio and Video Streams** | | | |
|* Subscribe to audio and video stream<br><br>* Unsubscribe from audio and video stream |* subscribeStream:(NSString \*_Nonnull)userId mediaStreamType:(ByteRTCMediaStreamType)mediaStreamType<br><br>* unsubscribeStream:(NSString \*_Nonnull)userId mediaStreamType:(ByteRTCMediaStreamType)mediaStreamType; |* subscribeStreamAudio:(NSString \*_Nonnull)streamId subscribe:(BOOL)subscribe<br><br>* subscribeStreamVideo:(NSString \*_Nonnull)streamId subscribe:(BOOL)subscribe |* **Interface split rename, function extension**:<br><br>* **Split by audio and video**: 2 new methods are used to control video stream and audio stream subscription respectively<br><br>* **Merge subscribe and unsubscribe**: new interface uses `subscribe` parameter to represent subscribe and unsubscribe<br><br>* **Parameter change**:<br><br>* **Removed parameters**:<br><br>* Removed `userId`, use `streamId` to identify stream.<br><br>* Removed `type`, new methods directly distinguish video and audio streams through method names<br><br>* **Added parameters**:<br><br>* `streamId` is used to identify stream;<br><br>* `subscribe` is used to identify whether to subscribe. |
|Audio and video stream subscription status change callback |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onStreamSubscribed:(ByteRTCSubscribeState)state userId:(NSString \*_Nonnull)userId subscribeConfig:(ByteRTCSubscribeConfig \*_Nonnull)info |* rtcRoom:(ByteRTCRoom\* _Nonnull)rtcRoom onUserPublishStreamAudio:(NSString\* _Nonnull)roomId uid:(NSString\* _Nonnull)uid isPublish:(BOOL)isPublish<br><br>* rtcRoom:(ByteRTCRoom\* _Nonnull)rtcRoom onUserPublishScreenVideo:(NSString\* _Nonnull)roomId uid:(NSString\* _Nonnull)uid isPublish:(BOOL)isPublish |* **Interface split rename, function extension**:<br><br>* **Split by audio and video**: 2 new methods are used for audio stream and video stream subscription callbacks respectively<br><br>* **Merge subscribe and unsubscribe status**: new interface uses `(BOOL)isPublish` parameter to represent publish and unpublish<br><br>* **Parameter change**:<br><br>* **Added parameter**: `roomId`: room ID<br><br>* **Parameter rename**: `userId` is renamed to `uid`<br><br>* **Removed parameters**:<br><br>* Removed `subscribeConfig:(ByteRTCSubscribeConfig *_Nonnull)info`, no longer provides subscription configuration information.<br><br>* Removed `state` parameter, replaced by `isPublish` parameter to clearly distinguish publish and unpublish status |
|Audio and video stream subscription status change callback |rtcRoom:(ByteRTCRoom \*_Nonnull)rtcRoom onStreamStateChanged:(NSString \*_Nonnull)roomId withUid:(nonnull NSString \*)uid state:(NSInteger)state extraInfo:(NSString \*_Nonnull)extraInfo; |* rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onVideoSubscribeStateChanged:(NSString  *_Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info state:(ByteRTCSubscribeState)state reason:(ByteRTCSubscribeStateChangeReason)reason<br><br>* rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onAudioSubscribeStateChanged:(NSString  *_Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info state:(ByteRTCSubscribeState)state reason:(ByteRTCSubscribeStateChangeReason)reason |* **Interface split rename**: split by audio and video, new methods are used for video stream and audio stream publish status callbacks respectively<br><br>* **Parameter change**:<br><br>* **Added parameters**:<br><br>* Added `streamId` and `info` parameters to identify stream information for subscription status changes.<br><br>* Added `reason` parameter: used to identify the specific reason for subscription status changes<br><br>* **Parameter type change**: `state` parameter type changed from `NSInteger` to `ByteRTCSubscribeState` enumeration type to provide clearer status definition.<br><br>* **Removed parameters**:<br><br>* Removed parameters `roomId` and `uid`;<br><br>* Removed invalid parameter `extraInfo`. |
|3. **Subscribe/Unsubscribe All Media Streams** | | | |
|* Subscribe to all media streams<br><br>* Unsubscribe from all media streams |* subscribeAllStreamsWithMediaStreamType:(ByteRTCMediaStreamType)mediaStreamType<br><br>* unsubscribeAllStreamsWithMediaStreamType:(ByteRTCMediaStreamType)mediaStreamType |* subscribeAllStreamsVideo:(BOOL)subscribe<br><br>* subscribeAllStreamsAudio:(BOOL)subscribe |* **Interface split rename, function extension**:<br><br>* **Split by audio and video**: 2 new methods are used to control video stream and audio stream subscription respectively<br><br>* **Merge subscribe and unsubscribe**: new interface handles subscribe and unsubscribe through `subscribe` parameter<br><br>* **Parameter change**: removed `mediaStreamType`, new methods directly distinguish video stream and audio stream through method names |
|Pause receiving media streams from remote |pauseAllSubscribedStream:(ByteRTCPauseResumControlMediaType) mediaType |* pauseAllSubscribedStreamAudio<br><br>* pauseAllSubscribedStreamVideo |* **Interface split**: split by audio and video, 2 new methods are used to pause receiving all remote audio streams and pause all remote video streams respectively<br><br>* **Parameter change**: removed `mediaType` parameter, new methods directly distinguish audio and video streams through method names |
|Resume receiving media streams from remote |resumeAllSubscribedStream:(ByteRTCPauseResumControlMediaType) mediaType |* resumeAllSubscribedStreamAudio<br><br>* resumeAllSubscribedStreamVideo |* **Interface split**: split by audio and video, 2 new methods are used to resume receiving all remote audio streams and resume receiving all remote video streams respectively<br><br>* **Parameter change**: removed `mediaType` parameter, new methods directly distinguish audio and video streams through method names |


<span id="screen-sharing"></span>
### Screen Sharing


1. Screen stream and normal video stream cannot coexist in the same engine. When screen stream is enabled, normal video stream will be automatically disabled, and when normal video stream is enabled, screen stream will be automatically disabled.

2. Screen stream and normal video stream have the same publish and subscribe methods, deprecating a series of interfaces with "screen".



|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|Capture screen video |startScreenCapture:(ByteRTCScreenMediaType) type bundleId:(NSString \*_Nullable)bundleId |startScreenCapture:(ByteRTCScreenMediaType) type bundleId:(NSString \*_Nullable)bundleId |**Behavior change**:<br><br>When starting screen capture, video capture function will be stopped |
|Set screen stream encoding parameters |setScreenVideoEncoderConfig:(ByteRTCScreenVideoEncoderConfig \* _Nullable) encoderConfig |setVideoEncoderConfig:(ByteRTCVideoEncoderConfig \* _Nullable) encoderConfig |**Interface replacement**:<br><br>Screen stream and video stream share the same set of encoding parameters, parameters set by setVideoEncoderConfig will apply to both screen stream and general video stream |
|Publish/stop publishing local screen audio and video stream |publishScreen:(ByteRTCMediaStreamType)type<br><br>unpublishScreen:(ByteRTCMediaStreamType)type |publishStreamVideo:(BOOL)publish<br><br>publishStreamAudio:(BOOL)publish |**Interface replacement**:<br><br>Screen stream and video stream share the same set of publish/unpublish interfaces<br><br>**Interface split**<br><br>Audio and video publish/unpublish interfaces are separated |
|Subscribe/unsubscribe remote screen audio and video stream |subscribeScreen:(NSString \*_Nonnull)userId mediaStreamType:(ByteRTCMediaStreamType)mediaStreamType<br><br>unsubscribeScreen:(NSString \*_Nonnull)userId mediaStreamType:(ByteRTCMediaStreamType)mediaStreamType |subscribeStreamVideo:(NSString \*_Nonnull)streamId subscribe:(BOOL)subscribe<br><br>subscribeStreamAudio:(NSString \*_Nonnull)streamId subscribe:(BOOL)subscribe |**Interface replacement**:<br><br>Screen stream and video stream share the same set of subscribe/unsubscribe interfaces<br><br>**Interface split**<br><br>Audio and video subscribe/unsubscribe interfaces are separated<br><br>**Parameter change**:<br><br>Use parameter streamId to distinguish which specific stream it is, whether it is a screen stream |
|Remote user publish or unpublish screen stream callback |rtcRoom:( ByteRTCRoom \* _Nonnull)rtcRoom onUserPublishScreen:(NSString \*_Nonnull)userId type:(ByteRTCMediaStreamType)type<br><br>rtcRoom:( ByteRTCRoom \* _Nonnull)rtcRoom onUserUnpublishScreen:(NSString \*_Nonnull)userId type:(ByteRTCMediaStreamType)type reason:(ByteRTCStreamRemoveReason)reason |rtcRoom:(ByteRTCRoom\* _Nonnull)rtcRoom onUserPublishStreamVideo:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info isPublish:(BOOL)isPublish;<br><br>rtcRoom:(ByteRTCRoom\* _Nonnull)rtcRoom onUserPublishStreamAudio:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info isPublish:(BOOL)isPublish; |**Interface replacement**:<br><br>Screen stream and video stream share the same set of publish/unpublish callback interfaces<br><br>**Interface split**<br><br>Audio and video publish/unpublish callback interfaces are separated<br><br>**Parameter change**:<br><br>Use parameter streamId to distinguish which specific stream it is, whether it is a screen stream |
|Screen sharing stream video first frame send status callback |rtcEngine:(ByteRTCVideo \*_Nonnull)engine onScreenVideoFrameSendStateChanged:(NSString \* _Nonnull)roomId rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFrameSendState)state; |rtcEngine:(ByteRTCEngine  *_Nonnull)engine onVideoFrameSendStateChanged:(NSString \* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFrameSendState)state |**Interface replacement**:<br><br>Screen stream and video stream share the same set of video first frame send status callbacks<br><br>**Parameter change**:<br><br>Use parameter streamId to distinguish which specific stream it is, whether it is a screen stream |
|Screen sharing stream video first frame play status callback |rtcEngine:(ByteRTCVideo \*_Nonnull)engine onScreenVideoFramePlayStateChanged:(NSString \* _Nonnull)roomId rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFramePlayState)state; |rtcEngine:(ByteRTCEngine  *_Nonnull)engine onVideoFramePlayStateChanged:(NSString \* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFramePlayState)state |**Interface replacement**:<br><br>Screen stream and video stream share the same set of video first frame play status callbacks<br><br>**Parameter change**:<br><br>Use parameter streamId to distinguish which specific stream it is, whether it is a screen stream |


<span id="rts"></span>
### RTS

RTC includes RTS capability. The current version further splits RTS\-related interfaces. If only using RTS\-related capabilities, call createRTSRoom to create RTSRoom instance and use ByteRTCRTSRoomDelegate callback. If using both audio/video capabilities and RTS capabilities, call createRTCRoom from RTCEngine to create RTCRoom instance and use ByteRTCRoomDelegate callback.

<span id="bytertcroom-section"></span>
#### ByteRTCRoom Section


|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|Create RTS room |createRTCRoom:(NSString \* _Nonnull)roomId; |createRTSRoom:(NSString \* _Nonnull)roomId; |**Interface split**: if only using RTS\-related capabilities, call createRTSRoom to create RTSRoom instance |
|Set RTS\-related callback |setRTCRoomDelegate:(id_Nullable)roomDelegate; |setRTSRoomDelegate:(id_Nullable)roomDelegate; |**Interface split**: if only using RTS\-related capabilities, call this interface in RTSRoom to set callback |
|Callback when receiving text message from user outside room |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserMessageReceivedOutsideRoom:(NSString \* _Nonnull)uid message:(NSString \* _Nonnull)message |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserMessageReceivedOutsideRoom:(NSInteger)msgid uid:(NSString \* _Nonnull)uid message:(NSString \* _Nonnull)message |**Parameter change**: callback parameter adds msgid parameter |
|Callback when receiving binary message from user outside room |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserBinaryMessageReceivedOutsideRoom:(NSString \* _Nonnull)uid message:(NSData \* _Nonnull)message |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserBinaryMessageReceivedOutsideRoom:(NSInteger)msgid uid:(NSString \* _Nonnull)uid message:(NSData \* _Nonnull)message |**Parameter change**: callback parameter adds msgid parameter |
|Callback for receiving broadcast message in room |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onRoomMessageReceived:(NSString \*_Nonnull)uid message:(NSString \*_Nonnull)message |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onRoomMessageReceived:(NSInteger)msgid uid:(NSString \*_Nonnull)uid message:(NSString \*_Nonnull)message |**Parameter change**: callback parameter adds msgid parameter |
|Callback for receiving broadcast binary message in room |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onRoomBinaryMessageReceived:(NSString \*_Nonnull)uid message:(NSData \*_Nonnull)message |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onRoomBinaryMessageReceived:(NSInteger)msgid uid:(NSString \*_Nonnull)uid message:(NSData \*_Nonnull)message |**Parameter change**: callback parameter adds msgid parameter |
|Callback when receiving point\-to\-point text message from other users in room |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onUserMessageReceived:(NSString \*_Nonnull)uid message:(NSString \*_Nonnull)message |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onUserMessageReceived:(NSInteger)msgid uid:(NSString \*_Nonnull)uid message:(NSString \*_Nonnull)message |**Parameter change**: callback parameter adds msgid parameter |
|Callback when receiving point\-to\-point binary message from other users in room |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onUserBinaryMessageReceived:(NSString \*_Nonnull)uid message:(NSData \*_Nonnull)message |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onUserBinaryMessageReceived:(NSInteger)msgid uid:(NSString \*_Nonnull)uid message:(NSData \*_Nonnull)message |**Parameter change**: callback parameter adds msgid parameter |


<span id="bytertcrtsroom-section"></span>
#### ByteRTCRTSRoom Section


|**Function** |**V3.58** |**V3.60** |Description |
|---|---|---|---|
|Callback for receiving broadcast message in room |rtsRoom:(ByteRTCRTSRoom \* _Nonnull)rtsRoom onRoomMessageReceived:(NSString \* _Nonnull)uid message:(NSString \* _Nonnull)message; |rtsRoom:( ByteRTCRTSRoom \*_Nonnull)rtsRoom onRoomMessageReceived:(NSInteger)msgid uid:(NSString \*_Nonnull)uid message:(NSString \*_Nonnull)message; |**Parameter change**: callback parameter adds msgid parameter |
|Callback for receiving broadcast binary message in room |rtsRoom:(ByteRTCRTSRoom \* _Nonnull)rtsRoom onRoomBinaryMessageReceived:(NSString \* _Nonnull)uid message:(NSData \* _Nonnull)message; |rtsRoom:( ByteRTCRTSRoom \*_Nonnull)rtsRoom onRoomBinaryMessageReceived:(NSInteger)msgid uid:(NSString \*_Nonnull)uid message:(NSData \*_Nonnull)message; |**Parameter change**: callback parameter adds msgid parameter |
|Callback when receiving point\-to\-point text message from other users in room |rtsRoom:( ByteRTCRTSRoom \*_Nonnull)rtsRoom onUserMessageReceived:(NSString \*_Nonnull)uid message:(NSString \*_Nonnull)message; |rtsRoom:( ByteRTCRTSRoom \*_Nonnull)rtsRoom onUserMessageReceived:(NSInteger)msgid uid:(NSString \*_Nonnull)uid message:(NSString \*_Nonnull)message; |**Parameter change**: callback parameter adds msgid parameter |
|Callback when receiving point\-to\-point binary message from other users in room |rtsRoom:( ByteRTCRTSRoom \*_Nonnull)rtsRoom onUserBinaryMessageReceived:(NSString \*_Nonnull)uid message:(NSData \*_Nonnull)message; |rtsRoom:( ByteRTCRTSRoom \*_Nonnull)rtsRoom onUserBinaryMessageReceived:(NSInteger)msgid uid:(NSString \*_Nonnull)uid message:(NSData \*_Nonnull)message; |**Parameter change**: callback parameter adds msgid parameter |


<span id="wtn-stream-formerly-public-stream"></span>
### WTN Stream (formerly Public Stream)


* Interface location changes:

   * WTN stream subscription interfaces are moved to the newly added `ByteRTCWTNStream` class.

   * WTN stream subscription callbacks are moved to the newly added `ByteRTCWTNStreamDelegate` callback class. You need to call setWTNStreamDelegate: first to set the callback handle.

* Shares MixedStreamConfig with mixed stream push interfaces to improve usability.

* Added onWTNRemoteVideoStats:videoStats: and onWTNRemoteAudioStats:audioStats: for obtaining WTN stream information and monitoring stream quality.

* Interface splitting, renaming, and replacement, specific changes are as follows:



|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|Publish WTN stream |startPushPublicStream:(NSString \* _Nonnull)publicStreamId withLayout:(ByteRTCPublicStreaming \*_Nullable)publicStream |startPushMixedStream:(NSString \* _Nonnull)taskId withPushTargetConfig:(ByteRTCMixedStreamPushTargetConfig\*)pushTargetConfig withMixedConfig:(ByteRTCMixedStreamConfig \*_Nullable)config |* **Interface rename**<br><br>* **Interface merge and feature expansion**: startPushPublicStream and startPushMixedStreamToCDN are merged into startPushMixedStream, the new interface can be used for both mixed stream push to CDN or push WTN (formerly public stream)<br><br>* **Parameter change**:<br><br>* **Added parameter**: added `taskId`: set push task ID to identify push task<br><br>* **Replaced parameter**:<br><br>* Removed `publicStreamId`: specified by the newly added parameter `pushTargetConfig` to specify WTN stream ID (i.e., public stream ID)<br><br>* Removed `publicStream`, replaced by newly added parameter `mixedConfig` to configure WTN stream (such as video transcoding, layout, etc.) |
|Update WTN stream |updatePublicStreamParam:(NSString \* _Nonnull)publicStreamId withLayout:(ByteRTCPublicStreaming \*_Nullable)publicStream |updatePushMixedStream:(NSString _Nonnull)taskId withPushTargetConfig:(ByteRTCMixedStreamPushTargetConfig)pushTargetConfig withMixedConfig:(ByteRTCMixedStreamConfig \*_Nonnull)config |* **Interface rename**<br><br>* **Interface merge and feature expansion**: updatePublicStreamParam and updatePushMixedStreamToCDN are merged into updatePushMixedStream, the new interface can be used for both updating mixed stream push to CDN and push WTN (formerly public stream) tasks<br><br>* **Parameter change**:<br><br>* **Added parameter**: added `taskId`, ID of the mixed stream task<br><br>* **Replaced parameter**:<br><br>* Removed `publicStreamId`: specified by the newly added parameter `pushTargetConfig` to specify WTN stream ID (i.e., public stream ID)<br><br>* Removed `publicStream`, replaced by newly added parameter `mixedConfig` to configure WTN stream (such as video transcoding, layout, etc.) |
|Stop publishing WTN stream |stopPushPublicStream:(NSString \* _Nonnull)publicStreamId; |stopPushMixedStream:(NSString \*_Nonnull)taskId withPushTargetType:(ByteRTCMixedStreamPushTargetType)pushTargetType |* **Interface rename**<br><br>* **Interface merge and feature expansion**: stopPushPublicStream and stopPushStreamToCDN are merged into stopPushMixedStream, the new interface can be used for both stopping WTN stream (formerly public stream) publishing and stopping mixed stream push<br><br>* **Parameter change**:<br><br>* **Added parameter**: added `taskId`, ID of the mixed stream task<br><br>* **Replaced parameter**: removed `publicStreamId`, replaced by newly added parameter `pushTargetType` to specify the stream to stop |
|* Subscribe to WTN stream<br><br>* Unsubscribe from WTN stream |* startPlayPublicStream:(NSString \* _Nonnull)publicStreamId<br><br>* stopPlayPublicStream:(NSString \* _Nonnull)publicStreamId |* subscribeWTNVideoStream:(NSString \* _Nonnull)streamId subscribe:(bool)subscribe<br><br>* subscribeWTNAudioStream:(NSString \* _Nonnull)streamId subscribe:(bool)subscribe |* **Interface split, rename, and feature expansion**:<br><br>* **Split by audio and video**: 2 new methods are used for subscribing/unsubscribing to WTN audio stream and subscribing/unsubscribing to video stream<br><br>* **Merge subscribe and unsubscribe**: new interface handles subscribe and unsubscribe through `(bool )subscribe` parameter<br><br>* **Parameter change**:<br><br>* `publicStreamId`: renamed to streamId<br><br>* Added `boolean subscribe` |
|Bind WTN stream canvas |setPublicStreamVideoCanvas:(NSString \*_Nonnull)publicStreamId withCanvas:(ByteRTCVideoCanvas \* Nullable)canvas NS_SWIFT_NAME(setPublicStreamVideoCanvas(:withCanvas:)) |setWTNRemoteVideoCanvas:(NSString \*_Nonnull)streamId withCanvas:(ByteRTCVideoCanvas \* Nullable)canvas NS_SWIFT_NAME(setWTNRemoteVideoCanvas(:withCanvas:)) |* **Interface rename**<br><br>* **Parameter change**: `publicStreamId` renamed to `streamId` |
|Specify external renderer for WTN stream |setPublicStreamVideoSink:(NSString \*_Nonnull)publicStreamId withSink:(id_Nullable)videoSink withPixelFormat:(ByteRTCVideoSinkPixelFormat)requiredFormat NS_SWIFT_NAME(setPublicStreamVideoSink(:withSink:withPixelFormat:)) |setWTNRemoteVideoSink:(NSString  *_Nonnull)streamId withSink:(id _Nullable)videoSink withConfig:(ByteRTCRemoteVideoSinkConfig*)config NS_SWIFT_NAME(setWTNRemoteVideoSink(_:withSink:withConfig:)) |* **Interface rename**<br><br>* **Parameter change**:<br><br>* **Parameter rename**: `publicStreamId` renamed to `streamId`<br><br>* **Added parameter**: `config` (`ByteRTCRemoteVideoSinkConfig` type), used to configure remote video frames (such as position, format, whether to mirror video frames, etc.)<br><br>* **Replace and move**:<br><br>   Removed `requiredFormat`, moved to `ByteRTCRemoteVideoSinkConfig`, default is 0 (original format) |
|Adjust WTN stream playback volume |setPublicStreamAudioPlaybackVolume:(NSString \*_Nonnull)publicStreamId volume:(NSInteger)volume |setWTNRemoteAudioPlaybackVolume:(NSString \*_Nonnull)streamId volume:(NSInteger)volume |* **Interface rename**<br><br>* **Parameter change**: `publicStreamId` renamed to `streamId` |
|WTN stream task callback |rtcEngine:(ByteRTCVideo \*_Nonnull)engine onPushPublicStreamResult:(NSString \*_Nonnull)roomId publicStreamId:(NSString \*_Nonnull)streamId errorCode:(ByteRTCPublicStreamErrorCode)errorCode |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onMixedStreamEvent:(ByteRTCMixedStreamTaskEvent)event withMixedStreamInfo:(ByteRTCMixedStreamTaskInfo\*)info withErrorCode:(ByteRTCMixedStreamTaskErrorCode)errorCode |* **Interface rename**<br><br>* **Interface merge and feature expansion**: onMixingEvent, onStreamMixingEvent and onPushPublicStreamResult are merged into onMixedStreamEvent, the new interface can be used for both mixed stream push to CDN / WTN stream status callbacks<br><br>* **Parameter change**:<br><br>* **Parameter type change**:<br><br>   `errorCode` type changed from `ByteRTCPublicStreamErrorCode` to `ByteRTCMixedStreamTaskErrorCode`, sharing the same enumeration class with mixed stream push tasks. For change details, see iOS<br><br>* **Removed parameter**:<br><br>* Removed `roomId`: no longer needed<br><br>* Removed `publicStreamId`: replaced by `taskId` in the newly added `MixedStreamTaskInfo info`<br><br>* **Added parameter**: added `event` (mixed stream task event) `ByteRTCMixedStreamTaskEvent` type, see iOS for details |
|Play WTN stream task callback |rtcEngine:(ByteRTCVideo \*_Nonnull)engine onPlayPublicStreamResult:(NSString \*_Nonnull)publicStreamId errorCode:(ByteRTCPublicStreamErrorCode)errorCode |* onWTNVideoSubscribeStateChanged:(NSString \*_Nonnull)streamId state:(ByteRTCWTNSubscribeState)state reason:(ByteRTCWTNSubscribeStateChangeReason)reason<br><br>* onWTNAudioSubscribeStateChanged:(NSString \*_Nonnull)streamId state:(ByteRTCWTNSubscribeState)state reason:(ByteRTCWTNSubscribeStateChangeReason)reason |* **Interface split and rename**: split into 2 independent interfaces, used for WTN audio/video stream subscription status change callbacks respectively<br><br>* **Parameter change**<br><br>* **Parameter rename**: `publicStreamId` renamed to `streamId`<br><br>* **Removed parameter**: removed `errorCode`, replaced by `state` (subscription status code) and `reason` (subscription status change reason)<br><br>* **Location move**: moved to `ByteRTCWTNStreamDelegate` class |
|Receive SEI callback in WTN stream |rtcEngine:(ByteRTCVideo \* _Nonnull)engine onPublicStreamSEIMessageReceived:(NSString\* _Nonnull)publicStreamId andMessage:(NSData\* _Nonnull)message andSourceType:(ByteRTCDataMessageSourceType)sourceType |onWTNSEIMessageReceived:(NSString\* _Nonnull)streamId andChannelId:(int)channelId andMessage:(NSData\* _Nonnull)message |* **Interface rename**<br><br>* **Parameter change**:<br><br>* **Parameter rename**: `publicStreamId` renamed to `streamId`<br><br>* **Added parameter**: added `channelId`, set different ChannelID for different receivers, receivers can select SEI information to focus on based on ChannelID in callback<br><br>* **Removed parameter**: removed `DataMessageSourceType sourceType`, no longer needed<br><br>* **Location move**: moved to `ByteRTCWTNStreamDelegate` class |
|Receive Data Message callback in WTN stream |rtcEngine:(ByteRTCVideo \* _Nonnull)engine onPublicStreamDataMessageReceived:(NSString\* _Nonnull)publicStreamId andMessage:(NSData\* _Nonnull)message andSourceType:(ByteRTCDataMessageSourceType)sourceType |onWTNDataMessageReceived:(NSString\* _Nonnull)streamId andMessage:(NSData\* _Nonnull)message andSourceType:(ByteRTCDataMessageSourceType)sourceType |* **Interface rename**<br><br>* **Parameter change**: `publicStreamId` renamed to `streamId`<br><br>* **Location move**: moved to `ByteRTCWTNStreamDelegate` class |
|WTN video stream first frame decode success callback |rtcEngine:(ByteRTCVideo \* _Nonnull)engine onFirstPublicStreamVideoFrameDecoded:(NSString \* _Nonnull)publicStreamId withFrameInfo:(ByteRTCVideoFrameInfo \* Nonnull)frameInfo NS_SWIFT_NAME(rtcEngine(:onFirstPublicStreamVideoFrameDecoded:withFrameInfo:)) |onWTNFirstRemoteVideoFrameDecoded:(NSString \* _Nonnull)streamId withFrameInfo:(ByteRTCVideoFrameInfo \* _Nonnull)frameInfo NS_SWIFT_NAME(onWTNFirstRemoteVideoFrameDecoded(streamId:withFrameInfo:)) |* **Interface rename**<br><br>* **Parameter rename**: `publicStreamId` renamed to `streamId`<br><br>* **Location move**: moved to `ByteRTCWTNStreamDelegate` class |
|WTN audio stream first frame decode success callback |rtcEngine:(ByteRTCVideo \* _Nonnull)engine onFirstPublicStreamAudioFrame:(NSString \* _Nonnull)publicStreamId |onWTNFirstRemoteAudioFrame:(NSString \* _Nonnull)streamId |* **Interface rename**<br><br>* **Parameter change**: `publicStreamId` renamed to `streamId`<br><br>* **Location move**: moved to `ByteRTCWTNStreamDelegate` class |


<span id="push-to-cdn"></span>
### Push to CDN

The usability of push\-to\-live streaming interfaces has been optimized. They now share `MixedStreamConfig` with WTN interfaces to improve usability. If you have already implemented push\-to\-live streaming functionality, refer to the following table to replace the interfaces.


|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|Mixed stream push |startPushMixedStreamToCDN:(NSString \* _Nonnull)taskID mixedConfig:(ByteRTCMixedStreamConfig \*_Nullable)config observer:(id_Nullable)observer |startPushMixedStream:(NSString \* _Nonnull)taskId withPushTargetConfig:(ByteRTCMixedStreamPushTargetConfig\*)pushTargetConfig withMixedConfig:(ByteRTCMixedStreamConfig \*_Nullable)config |* **Interface renamed**<br><br>* **Interface merged and functionality changed**: `startPushPublicStream` and `startPushMixedStreamToCDN` are merged into `startPushMixedStream`. The new interface can be used for both mixed stream push to CDN and push to WTN (formerly public streams)<br><br>* **Parameter changes**:<br><br>* **Parameter renamed**: `taskID` is renamed to `taskId`<br><br>* **Parameter removed**: `observer`<br><br>* **Parameter added**: Added `pushTargetConfig` of type `ByteRTCMixedStreamPushTargetConfig` to configure push targets |
|Update mixed stream push task |updatePushMixedStreamToCDN:(NSString \*_Nonnull)taskID mixedConfig:(ByteRTCMixedStreamConfig \*_Nonnull)config |updatePushMixedStream:(NSString  *_Nonnull)taskId withPushTargetConfig:(ByteRTCMixedStreamPushTargetConfig*)pushTargetConfig withMixedConfig:(ByteRTCMixedStreamConfig \*_Nonnull)config |* **Interface renamed**<br><br>* **Interface merged**: `updatePublicStreamParam` and `updatePushMixedStreamToCDN` are merged into `updatePushMixedStream`. The new interface can be used for updating both mixed stream push to CDN and push to WTN (formerly public streams) tasks<br><br>* **Parameter changes**:<br><br>* **Parameter renamed**: `taskID` is renamed to `taskId`<br><br>* **Parameter added**: Added `pushTargetConfig` of type `ByteRTCMixedStreamPushTargetConfig` to set target push addresses |
|Single stream push |startPushSingleStreamToCDN:(NSString \*_Nonnull)taskID singleStream:(ByteRTCPushSingleStreamParam \*_Nonnull)singleStream observer:(idNullable)observer NS_SWIFT_NAME(startPushSingleStreamToCDN(:singleStream:observer:)) |startPushSingleStream:(NSString \*_Nonnull)taskId singleStream:(ByteRTCPushSingleStreamParam \*_Nonnull)singleStream |* **Interface renamed**<br><br>* **Parameter changes**:<br><br>* **Parameter removed**: Removed `observer`, no longer required<br><br>* **Parameter renamed**: `taskID` is renamed to `taskId` |
|Stop push task |stopPushStreamToCDN:(NSString \*Nonnull)taskID NS_SWIFT_NAME(stopPushStreamToCDN(:)) |* startPushSingleStream:(NSString \*_Nonnull)taskId singleStream:(ByteRTCPushSingleStreamParam \*_Nonnull)singleStream<br><br>* stopPushMixedStream:(NSString \*_Nonnull)taskId withPushTargetType:(ByteRTCMixedStreamPushTargetType)pushTargetType |* **Interface split and renamed**: Split by single stream and mixed stream<br><br>* **For the stop mixed stream push interface (stopPushMixedStream)** :<br><br>* **Functionality extended**: Can be used to stop both CDN push and WTN stream push<br><br>* **Parameter added**: Added `pushTargetType` of type `ByteRTCMixedStreamPushTargetType` enum to specify the target stream to stop<br><br>* **Parameter renamed**: `taskID` is renamed to `taskId` |
|Push task callbacks |onMixingEvent:(ByteRTCStreamMixingEvent)event taskId:(NSString \*_Nonnull)taskId error:(ByteRTCStreamMixingErrorCode)errorCode mixType:(ByteRTCMixedStreamType)mixType |* rtcEngine:(ByteRTCEngine \* _Nonnull)engine onMixedStreamEvent:(ByteRTCMixedStreamTaskEvent)event withMixedStreamInfo:(ByteRTCMixedStreamTaskInfo\*)info withErrorCode:(ByteRTCMixedStreamTaskErrorCode)errorCode<br><br>* rtcEngine:(ByteRTCEngine \* _Nonnull)engine onSingleStreamEvent:(ByteRTCSingleStreamTaskEvent)event withTaskId:(NSString\*)taskId withErrorCode:(ByteRTCSingleStreamTaskErrorCode)errorCode |* **Interface split and renamed**: Split by mixed stream task event callbacks and single stream task event callbacks<br><br>   **For mixed stream push callbacks (onMixedStreamEvent)** :<br><br>* **Interface merged and functionality extended**: `onMixingEvent`, `onStreamMixingEvent`, and `onPushPublicStreamResult` are merged into `onMixedStreamEvent`. The new interface can be used for callbacks of both mixed stream push to CDN and WTN stream status<br><br>* **Parameter changes**:<br><br>* **Type changes**:<br><br>* `event`: Type changed from `ByteRTCStreamMixingEvent` to `ByteRTCMixedStreamTaskEvent`, see iOS for details<br><br>* `errorCode`: Type changed from `ByteRTCStreamMixingErrorCode` to `ByteRTCMixedStreamTaskErrorCode`, see iOS for details<br><br>* **Parameter removed**: Removed `MixedStreamType mixType` with no replacement<br><br>* **Parameter added**: Added `info` of type `ByteRTCMixedStreamTaskInfo` to provide detailed information about mixed stream tasks<br><br>* **Location moved**: Moved to `ByteRTCEngineDelegate` |


<span id="audio-video-transport"></span>
### Audio & Video Transport


|Function |Interface Name |Description |
|---|---|---|
|Callback when receiving the first frame from a remote audio stream |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onFirstRemoteAudioFrame:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info; |**Parameter changes**:<br><br>`RemoteStreamKey` parameter is replaced with `streamId` and `streamInfo`<br><br>**New applicable scenarios**:<br><br>This callback is also triggered when a remote user stops publishing audio and then republishes audio<br><br>Stopping publishing includes active cancellation by the publisher, actively leaving the room, disconnection, and stopping capture |
|* Callback after SDK successfully renders the first frame of remote video stream<br><br>* Callback after SDK receives and decodes the first frame of remote video stream |* rtcEngine:onFirstRemoteVideoFrameRendered:info:withFrameInfo:<br><br>* rtcEngine:onFirstRemoteVideoFrameDecoded:info:withFrameInfo: |**Parameter changes**:<br><br>`RemoteStreamKey` parameter is replaced with `streamId` and `streamInfo`<br><br>**New applicable scenarios**:<br><br>These two callbacks are also triggered when a remote user stops publishing video and then republishes video<br><br>Stopping publishing includes active cancellation by the publisher, actively leaving the room, disconnection, and stopping capture |
|Push external audio reference frames to the SDK |pushReferenceAudioPCMData:(ByteRTCAudioFrame \* _Nonnull) audioFrame; |**New API**: Custom audio echo cancellation reference signal |


<span id="audio-video-synchronization"></span>
### Audio\-Video Synchronization


|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|Audio\-video synchronization state change callback |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onAVSyncStateChange:(ByteRTCAVSyncState)state |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onAVSyncEvent:(NSString \*_Nonnull)roomId userId:(NSString \*_Nonnull)userId eventCode:(ByteRTCAVSyncEvent)eventCode |After the audio\-video synchronization feature is enabled, synchronization results will be notified through this callback. The new callback adds `roomId` and `userId`. Additionally, the synchronization state `AVSyncState` is replaced with synchronization failure event `ByteRTCAVSyncEvent`. When you receive this notification, you can call `setMultiDeviceAVSync:` with empty parameters to unbind the synchronization relationship and call the interface again to rebind<br><br><br>* **Interface renamed**<br><br>* **Parameter changes**<br><br>* **Parameters added**: Added `roomId` and `uid`<br><br>* **Parameter replaced**: Removed `state` parameter, replaced with `eventCode` (synchronization failure event). When you receive this notification, you can call `setMultiDeviceAVSync` with empty parameters to unbind the synchronization relationship and call the interface again to rebind<br><br>* **Behavior change**: Audio\-video synchronization failure<br><br>* 3.58: Returned by the following error code: `ByteRTCErrorCodInvalidAudioSyncUidRepeated = -1083`<br><br>* 3.60: Returned through `rtcRoom:onAVSyncEvent:userId:eventCode:` as `ByteRTCAVSyncEventInvalidUidRepeated = 0` |


<span id="volume-audio-playback-route-and-audio-scenario"></span>
### Volume, Audio Playback Route, and Audio Scenario


|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|Adjust the playback volume of a specified remote user's audio stream on the local device |setRemoteAudioPlaybackVolume:(NSString \*_Nonnull)roomID remoteUid:(NSString \*_Nonnull)userID playVolume:(NSInteger)volume |setRemoteAudioPlaybackVolume:(NSString\* _Nonnull)streamId volume:(int)volume |* **Parameter changes**:<br><br>   Parameters `roomId` and `uid` for specifying audio streams are changed to `streamId`<br><br>* **Functionality extended**:<br><br>   Upgraded from supporting only adjustment of media stream volume from specified users to supporting separate adjustment of local capture media stream volume, screen stream volume, and specified process volume |
|Force switch the current audio playback route |setAudioRoute: |setAudioRoute: |**Restriction changes**:<br><br>Force switching the current audio playback route is no longer limited to use only in the `AUDIO_SCENARIO_COMMUNICATION` audio scenario. It can be used as long as the current state is call mode |
|Set audio scenario type |setAudioScenario: |setAudioScenario: |The volume mode used by audio devices has changed, see media volume and call volume:<br><br><br>* If you have already set an audio scenario through `setAudioScenario:`: You need to refer to the above documentation, replace it with the updated audio scenario, and pay attention to changes in volume mode<br><br>* If you have never set an audio scenario through `setAudioScenario:`: You also need to pay attention to changes in volume mode for the same audio device under the default audio scenario |


<span id="push-external-video-frame"></span>
### Push External Video Frame


|V3.58 |V3.60 |Description |
|---|---|---|
|pushExternalVideoFrame:(ByteRTCVideoFrame \* _Nonnull)frame |pushExternalVideoFrame:(ByteRTCVideoFrameData \* _Nonnull)frame |The `frame` parameter type is replaced with `ByteRTCVideoFrameData`. Compared to the original parameter type, both the included parameters and whether they are required have changed |


<span id="get-song-list-for-each-chart-based-on-hot-charts"></span>
### Get Song List for Each Chart Based on Hot Charts


|V3.58 |V3.60 |Description |
|---|---|---|
|getHotMusic:(ByteRTCMusicHotType)hotType filterType:(ByteRTCMusicFilterType)filterType |getHotMusic:(NSArray <NSString \*\> \*_Nullable)customHotlistId filterType:(ByteRTCMusicFilterType)filterType |**Parameter replacement**: Removed `hotType`, replaced with `customHotlistId`. The type is also changed from enum to `NSArray <NSString *> *` to provide custom hot music list IDs. Property value mappings are as follows:<br><br><br>* `ByteRTCMusicHotTypeContentCenter` → `ContentCenter`<br><br>* `ByteRTCMusicHotTypeProject` → `Project` |


<span id="streamid-unique-stream-identification"></span>
### StreamId Unique Stream Identification

The current version uses StreamId to uniquely identify a stream. Therefore, the StreamIndex / RemoteStreamKey parameters in various APIs from previous versions are replaced with StreamId or related information. The affected APIs are as follows:


|Class |V3.58 |V3.60 |Description |
|---|---|---|---|
|ByteRTCEngine |muteAudioCapture:(ByteRTCStreamIndex)index mute:(bool)mute |muteAudioCapture: (bool)mute |Parameter change: Removed StreamIndex parameter |
|ByteRTCEngine |setCaptureVolume:(ByteRTCStreamIndex)index volume:(int)volume |setCaptureVolume: (int)volume |Parameter change: Removed StreamIndex parameter |
|ByteRTCEngine |enableAlphaChannelVideoEncode:(ByteRTCStreamIndex)streamIndex withAlphaLayout:(ByteRTCAlphaLayout)alphaLayout |enableAlphaChannelVideoEncode:(ByteRTCAlphaLayout)alphaLayout; |Parameter change: Removed StreamIndex parameter |
|ByteRTCEngine |disableAlphaChannelVideoEncode:(ByteRTCStreamIndex)streamIndex |disableAlphaChannelVideoEncode |Parameter change: Removed StreamIndex parameter |
|ByteRTCEngine |setLocalVideoCanvas:(ByteRTCStreamIndex)streamIndex withCanvas:(ByteRTCVideoCanvas \* *Nullable)canvas NS_SWIFT_NAME(setLocalVideoCanvas(* :withCanvas:)) |setLocalVideoCanvas:(ByteRTCVideoCanvas \* _Nullable)canvas NS_SWIFT_NAME(setLocalVideoCanvas(withCanvas:)) |Parameter change: Removed StreamIndex parameter |
|ByteRTCEngine |updateLocalVideoCanvas:(ByteRTCStreamIndex)streamIndex withRenderMode:(ByteRTCRenderMode)renderMode withBackgroundColor:(NSUInteger)backgroundColor NS_SWIFT_NAME(updateLocalVideoCanvas(_:withRenderMode:withBackgroundColor:)) |updateLocalVideoCanvas:(ByteRTCRenderMode)renderMode withBackgroundColor:(NSUInteger)backgroundColor NS_SWIFT_NAME(updateLocalVideoCanvas(withBackgroundColor:)) |Parameter change: Removed StreamIndex parameter |
|ByteRTCEngine |setRemoteVideoCanvas:(ByteRTCRemoteStreamKey \* _Nonnull)key withCanvas:(ByteRTCVideoCanvas \* *Nullable)canvas NS_SWIFT_NAME(setRemoteVideoCanvas(* :withCanvas:)) |setRemoteVideoCanvas:(NSString\* _Nonnull)streamId withCanvas:(ByteRTCVideoCanvas \* *Nullable)canvas NS_SWIFT_NAME(setRemoteVideoCanvas(* :withCanvas:)) |Parameter change: Changed RemoteStreamKey to streamId |
|ByteRTCEngine |updateRemoteStreamVideoCanvas:(ByteRTCRemoteStreamKey \* _Nonnull)key withRemoteVideoRenderConfig:(ByteRTCRemoteVideoRenderConfig \* *Nonnull)remoteVideoRenderConfig NS_SWIFT_NAME(updateRemoteStreamVideoCanvas(* :withRemoteVideoRenderConfig:)); |updateRemoteStreamVideoCanvas:(NSString\* _Nonnull)streamId withRemoteVideoRenderConfig:(ByteRTCRemoteVideoRenderConfig \* *Nonnull)remoteVideoRenderConfig NS_SWIFT_NAME(updateRemoteStreamVideoCanvas(* :withRemoteVideoRenderConfig:)); |Parameter change: Changed RemoteStreamKey to streamId |
|ByteRTCEngine |setLocalVideoSink:(ByteRTCStreamIndex)index withSink:(id*Nullable)videoSink withLocalRenderConfig:(ByteRTCLocalVideoSinkConfig*)config NS_SWIFT_NAME(setLocalVideoSink(\*:withSink:withLocalRenderConfig:)); |setLocalVideoSink:(id_Nullable)videoSink withLocalRenderConfig:(ByteRTCLocalVideoSinkConfig\*)config NS_SWIFT_NAME(setLocalVideoSink(withSink:withLocalRenderConfig:)); |Parameter change: Changed StreamIndex to videoSink |
|ByteRTCEngine |setRemoteVideoSink:(ByteRTCRemoteStreamKey\* _Nonnull)streamKey withSink:(id*Nullable)videoSink withRemoteRenderConfig:(ByteRTCRemoteVideoSinkConfig*)config NS_SWIFT_NAME(setRemoteVideoSink(\*:withSink:withRemoteRenderConfig:)); |setRemoteVideoSink:(NSString\* _Nonnull)streamId withSink:(id*Nullable)videoSink withRemoteRenderConfig:(ByteRTCRemoteVideoSinkConfig*)config NS_SWIFT_NAME(setRemoteVideoSink(\*:withSink:withRemoteRenderConfig:)); |Parameter change: Changed RemoteStreamKey to streamId |
|ByteRTCEngine |setVideoSourceType:(ByteRTCVideoSourceType)type WithStreamIndex:(ByteRTCStreamIndex)streamIndex NS_SWIFT_NAME(setVideoSourceType(_:WithStreamIndex:)) |setVideoSourceType:(ByteRTCVideoSourceType)type NS_SWIFT_NAME(setVideoSourceType(_:)) |Parameter change: Removed StreamIndex parameter |
|ByteRTCEngine |setRemoteVideoMirrorType:(ByteRTCRemoteStreamKey\*)key withMirrorType:(ByteRTCRemoteMirrorType)mirrorType |setRemoteVideoMirrorType:(NSString\* _Nonnull)streamId withMirrorType:(ByteRTCRemoteMirrorType)mirrorType |Parameter change: Changed RemoteStreamKey to streamId |
|ByteRTCEngine |sendSEIMessage:(ByteRTCStreamIndex)streamIndex andMessage:(NSData\* _Nonnull)message andRepeatCount:(int)repeatCount andCountPerFrame:(ByteRTCSEICountPerFrame) mode |sendSEIMessage: (NSData\* _Nonnull)message andRepeatCount:(int)repeatCount andCountPerFrame:(ByteRTCSEICountPerFrame) mode |Parameter change: Removed StreamIndex parameter |
|ByteRTCEngine |startFileRecording:(ByteRTCStreamIndex)streamIndex withRecordingConfig:(ByteRTCRecordingConfig\* *Nonnull)recordingConfig type:(ByteRTCRecordingType)recordingType NS_SWIFT_NAME(startFileRecording(* :withRecordingConfig:type:)) |startFileRecording: (ByteRTCRecordingConfig\* _Nonnull)recordingConfig type:(ByteRTCRecordingType)recordingType NS_SWIFT_NAME(startFileRecording(withRecordingConfig:type:)) |Parameter change: Removed StreamIndex parameter |
|ByteRTCEngine |stopFileRecording:(ByteRTCStreamIndex)streamIndex |stopFileRecording |Parameter change: Removed StreamIndex parameter |
|ByteRTCEngine |setRemoteAudioPlaybackVolume:(ByteRTCRemoteStreamKey\* _Nonnull)streamKey volume:(int)volume; |setRemoteAudioPlaybackVolume:(NSString\* _Nonnull)streamId volume:(int)volume |Parameter change: Changed RemoteStreamKey to streamId |
|ByteRTCEngine |pushExternalEncodedVideoFrame:(ByteRTCStreamIndex)streamIndex withVideoIndex:(NSInteger)videoIndex withEncodedVideoFrame:(ByteRTCEncodedVideoFrame\* *Nonnull)videoFrame NS_SWIFT_NAME(pushExternalEncodedVideoFrame(* :withVideoIndex:withEncodedVideoFrame:)) |pushExternalEncodedVideoFrame: (NSInteger)videoIndex withEncodedVideoFrame:(ByteRTCEncodedVideoFrame\* _Nonnull)videoFrame NS_SWIFT_NAME(pushExternalEncodedVideoFrame(withVideoIndex:withEncodedVideoFrame:)) |Parameter change: Changed StreamIndex to videoIndex |
|ByteRTCEngine |setVideoDecoderConfig:(ByteRTCRemoteStreamKey \* *Nonnull)key withVideoDecoderConfig:(ByteRTCVideoDecoderConfig)config NS_SWIFT_NAME(setVideoDecoderConfig(* :withVideoDecoderConfig:)) |setVideoDecoderConfig:(NSString\* *Nonnull)streamId withVideoDecoderConfig:(ByteRTCVideoDecoderConfig)config NS_SWIFT_NAME(setVideoDecoderConfig(* :withVideoDecoderConfig:)) |Parameter change: Changed RemoteStreamKey to streamId |
|ByteRTCEngine |requestRemoteVideoKeyFrame:(ByteRTCRemoteStreamKey \* _Nonnull)key |requestRemoteVideoKeyFrame:(NSString\* _Nonnull)streamId |Parameter change: Changed RemoteStreamKey to streamId |
|ByteRTCEngine |setVideoWatermark:(ByteRTCStreamIndex)streamIndex withImagePath:(NSString \* _Nullable)imagePath withRtcWatermarkConfig:(ByteRTCVideoWatermarkConfig\* _Nonnull)rtcWatermarkConfig |setVideoWatermark: (NSString \* _Nullable)imagePath withRtcWatermarkConfig:(ByteRTCVideoWatermarkConfig\* _Nonnull)rtcWatermarkConfig |Parameter change: Removed StreamIndex parameter |
|ByteRTCEngine |clearVideoWatermark:(ByteRTCStreamIndex)streamIndex NS_SWIFT_NAME(clearVideoWatermark(_:)) |clearVideoWatermark |Parameter change: Removed StreamIndex parameter |
|ByteRTCEngine |takeLocalSnapshot:(ByteRTCStreamIndex)streamIndex callback:(id_Nullable)callback |takeLocalSnapshot:(id_Nullable)callback |Parameter change: Removed StreamIndex parameter |
|ByteRTCEngine |takeRemoteSnapshot:(ByteRTCRemoteStreamKey\* _Nonnull)streamKey callback:(id_Nullable)callback |takeRemoteSnapshot:(NSString\* _Nonnull)streamId callback:(id_Nullable)callback |Parameter change: Changed RemoteStreamKey to streamId |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserStartVideoCapture:(NSString \* _Nonnull)roomId uid:(NSString \* _Nonnull)uid |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserStartVideoCapture:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info |Parameter change: Changed roomId and userId to streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserStopVideoCapture:(NSString \* _Nonnull)roomId uid:(NSString \* _Nonnull)uid |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserStopVideoCapture:(NSString \* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info |Parameter change: Changed roomId and userId to streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserStartAudioCapture:(NSString\* _Nonnull)roomId uid:(NSString \*_Nonnull)userId |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserStartAudioCapture:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info |Parameter change: Changed roomId and userId to streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserStopAudioCapture:(NSString\* _Nonnull)roomId uid:(NSString \*_Nonnull)userId |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserStopAudioCapture:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info· |Parameter change: Changed roomId and userId to streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onLocalAudioStateChanged:(ByteRTCLocalAudioStreamState)state error:(ByteRTCLocalAudioStreamError)error |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onLocalAudioStateChanged:(NSString \*_Nonnull)streamId info:(ByteRTCStreamInfo \*_Nonnull)info state:(ByteRTCLocalAudioStreamState)state error:(ByteRTCLocalAudioStreamError)error |Parameter change: Added streamId and streamInfo parameters |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \*\*Nonnull)engine onLocalVideoStateChanged:(ByteRTCStreamIndex)streamIndex withStreamState:(ByteRTCLocalVideoStreamState)state withStreamError:(ByteRTCLocalVideoStreamError)error NS_SWIFT_NAME(rtcEngine(\*:onLocalVideoStateChanged:withStreamState:withStreamError:)) |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onLocalVideoStateChanged:(NSString  *_Nonnull)streamId info:(ByteRTCStreamInfo \*\*Nonnull)info withStreamState:(ByteRTCLocalVideoStreamState)state withStreamError:(ByteRTCLocalVideoStreamError)error NS_SWIFT_NAME(rtcEngine(* :onLocalVideoStateChanged:info:withStreamState:withStreamError:)) |Parameter change: Changed streamIndex to streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onRemoteAudioStateChanged:(ByteRTCRemoteStreamKey \* _Nonnull)key state:(ByteRTCRemoteAudioState)state reason:(ByteRTCRemoteAudioStateChangeReason)reason |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onRemoteAudioStateChanged:(NSString \*_Nonnull)streamId info:(ByteRTCStreamInfo \*_Nonnull)info state:(ByteRTCRemoteAudioState)state reason:(ByteRTCRemoteAudioStateChangeReason)reason |Parameter change: Changed RemoteStreamKey to streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine  *_Nonnull)engine onRemoteVideoStateChanged:(ByteRTCRemoteStreamKeyNonnull)streamKey withVideoState:(ByteRTCRemoteVideoState)state withVideoStateReason:(ByteRTCRemoteVideoStateChangeReason)reason NS_SWIFT_NAME(rtcEngine(* :onRemoteVideoStateChanged:withVideoState:withVideoStateReason:)) |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onRemoteVideoStateChanged:(NSString  *_Nonnull)streamId info:(ByteRTCStreamInfo \*\*Nonnull)info withVideoState:(ByteRTCRemoteVideoState)state withVideoStateReason:(ByteRTCRemoteVideoStateChangeReason)reason NS_SWIFT_NAME(rtcEngine(* :onRemoteVideoStateChanged:withVideoState:withVideoStateReason:)) |Parameter change: Changed RemoteStreamKey to streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onFirstLocalVideoFrameCaptured:(ByteRTCStreamIndex)streamIndex withFrameInfo:(ByteRTCVideoFrameInfo \* *Nonnull)frameInfo NS_SWIFT_NAME(rtcEngine(* :onFirstLocalVideoFrameCaptured:withFrameInfo:)) |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onFirstLocalVideoFrameCaptured:(ByteRTCVideoSource\* _Nullable)videoSource withFrameInfo:(ByteRTCVideoFrameInfo \* *Nonnull)frameInfo NS_SWIFT_NAME(rtcEngine(* :onFirstLocalVideoFrameCaptured:withFrameInfo:)) |Parameter change: Changed streamIndex to VideoSource |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine  *_Nonnull)engine onLocalVideoSizeChanged:(ByteRTCStreamIndex)streamIndex withFrameInfo:(ByteRTCVideoFrameInfo \*\*Nonnull)frameInfo NS_SWIFT_NAME(rtcEngine(* :onLocalVideoSizeChanged:withFrameInfo:)) |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onLocalVideoSizeChanged:(ByteRTCVideoSource  *_Nullable)videoSource withFrameInfo:(ByteRTCVideoFrameInfo \*\*Nonnull)frameInfo NS_SWIFT_NAME(rtcEngine(* :onLocalVideoSizeChanged:withFrameInfo:)) |Parameter change: Changed streamIndex to VideoSource |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onRemoteVideoSizeChanged:(ByteRTCRemoteStreamKey  *_Nonnull)streamKey withFrameInfo:(ByteRTCVideoFrameInfo \*\*Nonnull)frameInfo NS_SWIFT_NAME(rtcEngine(* :onRemoteVideoSizeChanged:withFrameInfo:)) |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onRemoteVideoSizeChanged:(NSString \*_Nonnull)streamId info:(ByteRTCStreamInfo  *_Nonnull)info withFrameInfo:(ByteRTCVideoFrameInfo \*\*Nonnull)frameInfo NS_SWIFT_NAME(rtcEngine(* :onRemoteVideoSizeChanged:withFrameInfo:)) |Parameter change: Changed RemoteStreamKey to streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onFirstLocalAudioFrame:(ByteRTCStreamIndex) streamIndex |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onFirstLocalAudioFrame:(ByteRTCAudioSource\* _Nullable)audioSource |Parameter change: 将streamIndex变为AudioSource |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onSEIMessageReceived:(ByteRTCRemoteStreamKey\* _Nonnull)remoteStreamKey andMessage:(NSData\* _Nonnull)message |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onSEIMessageReceived:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info andMessage:(NSData\* _Nonnull)message |Parameter change: 将RemoteStreamKey变为streamId和streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onSEIStreamUpdate:(ByteRTCRemoteStreamKey\* _Nonnull)remoteStreamKey eventType:(ByteRTCSEIStreamEventType)eventType |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onSEIStreamUpdate:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info eventType:(ByteRTCSEIStreamEventType)eventType |Parameter change: 将RemoteStreamKey变为streamId和streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine\* _Nonnull)engine onRecordingStateUpdate:(ByteRTCStreamIndex)type state:(ByteRTCRecordingState)state error_code:(ByteRTCRecordingErrorCode)errorCode recording_info:(ByteRTCRecordingInfo\* _Nonnull)recordingInfo |rtcEngine:(ByteRTCEngine\* _Nonnull)engine onRecordingStateUpdate:(ByteRTCVideoSource\* _Nullable)videoSource state:(ByteRTCRecordingState)state error_code:(ByteRTCRecordingErrorCode)errorCode recording_info:(ByteRTCRecordingInfo\* _Nonnull)recordingInfo |Parameter change: 将streamIndex变为VideoSource |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine\* _Nonnull)engine onRecordingProgressUpdate:(ByteRTCStreamIndex)type process:(ByteRTCRecordingProgress\* _Nonnull)process recording_info:(ByteRTCRecordingInfo\* _Nonnull)recordingInfo |rtcEngine:(ByteRTCEngine\* _Nonnull)engine onRecordingProgressUpdate:(ByteRTCVideoSource\* _Nullable)videoSource process:(ByteRTCRecordingProgress\* _Nonnull)process recording_info:(ByteRTCRecordingInfo\* _Nonnull)recordingInfo |Parameter change: 将streamIndex变为VideoSource |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onStreamSyncInfoReceived:(ByteRTCRemoteStreamKey\* _Nonnull)remoteStreamKey streamType:(ByteRTCSyncInfoStreamType)streamType data:(NSData\* _Nonnull)data |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onStreamSyncInfoReceived:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info streamType:(ByteRTCSyncInfoStreamType)streamType data:(NSData\* _Nonnull)data |Parameter change: 将RemoteStreamKey变为streamId和streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onAudioFrameSendStateChanged:(NSString \* _Nonnull)roomId rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFrameSendState)state |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onAudioFrameSendStateChanged:(NSString \* _Nonnull)streamId info:(ByteRTCStreamInfo \*_Nonnull)info rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFrameSendState)state |Parameter change: 将roomId改为streamId和streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onVideoFrameSendStateChanged:(NSString \* _Nonnull)roomId rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFrameSendState)state |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onVideoFrameSendStateChanged:(NSString \* _Nonnull)streamId info:(ByteRTCStreamInfo \*_Nonnull)info rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFrameSendState)state; |Parameter change: 将roomId改为streamId和streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onAudioFramePlayStateChanged:(NSString \* _Nonnull)roomId rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFramePlayState)state |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onAudioFramePlayStateChanged:(NSString \* _Nonnull)streamId info:(ByteRTCStreamInfo \*_Nonnull)info rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFramePlayState)state |Parameter change: 将roomId改为streamId和streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onVideoFramePlayStateChanged:(NSString \* _Nonnull)roomId rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFramePlayState)state |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onVideoFramePlayStateChanged:(NSString \* _Nonnull)streamId info:(ByteRTCStreamInfo \*_Nonnull)info rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFramePlayState)state |Parameter change: 将roomId改为streamId和streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onSimulcastSubscribeFallback:(ByteRTCRemoteStreamSwitchEvent \*_Nonnull)event |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onSimulcastSubscribeFallback:(NSString  *_Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info event:(ByteRTCRemoteStreamSwitchEvent \*_Nonnull)event |Parameter change: 添加参数streamId和streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onPerformanceAlarms:(ByteRTCPerformanceAlarmMode)mode roomId:(NSString \*_Nonnull)roomId reason:(ByteRTCPerformanceAlarmReason)reason sourceWantedData:(ByteRTCSourceWantedData \*_Nonnull)data |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onPerformanceAlarms:(NSString  *_Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info mode:(ByteRTCPerformanceAlarmMode)mode reason:(ByteRTCPerformanceAlarmReason)reason sourceWantedData:(ByteRTCSourceWantedData \*_Nonnull)data |Parameter change: 添加参数streamId和streamInfo |
|ByteRTCRoomDelegate |rtcRoom:( ByteRTCRoom  *_Nonnull)rtcRoom onLocalStreamStats:(ByteRTCLocalStreamStats \*\*Nonnull)stats NS_SWIFT_NAME(rtcRoom(* :onLocalStreamStats:)) |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onLocalStreamStats:(NSString \*_Nonnull)streamId info:(ByteRTCStreamInfo  *_Nonnull)info stats:(ByteRTCLocalStreamStats \*\*Nonnull)stats NS_SWIFT_NAME(rtcRoom(* :onLocalStreamStats:)) |Parameter change: 添加参数streamId和streamInfo |
|ByteRTCRoomDelegate |rtcRoom:( ByteRTCRoom  *_Nonnull)rtcRoom onRemoteStreamStats:(ByteRTCRemoteStreamStats \*\*Nonnull)stats NS_SWIFT_NAME(rtcRoom(* :onRemoteStreamStats:)) |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onRemoteStreamStats:(NSString \*_Nonnull)streamId info:(ByteRTCStreamInfo  *_Nonnull)info stats:(ByteRTCRemoteStreamStats \*\*Nonnull)stats NS_SWIFT_NAME(rtcRoom(* :onRemoteStreamStats:)) |Parameter change: 添加参数streamId和streamInfo |
|LocalEncodedVideoFrameObserverObjC : ILocalEncodedVideoFrameObserver |onLocalEncodedVideoFrame:(ByteRTCStreamIndex) streamIndex Frame:(ByteRTCEncodedVideoFrame \* _Null_unspecified)frame |onLocalEncodedVideoFrame:(ByteRTCVideoSource\* _Nullable)videoSource Frame:(ByteRTCEncodedVideoFrame \* _Null_unspecified)frame |Parameter change: 将streamIndex变为VideoSource |
|RemoteEncodedVideoFrameObserverObjC : IRemoteEncodedVideoFrameObserver |onRemoteEncodedVideoFrame:(ByteRTCRemoteStreamKey \* _Nonnull)streamKey withEncodedVideoFrame:(ByteRTCEncodedVideoFrame\* _Nonnull)videoFrame |onRemoteEncodedVideoFrame:(NSString\*)streamId info:(ByteRTCStreamInfo \* _Nonnull)info withEncodedVideoFrame:(ByteRTCEncodedVideoFrame\* _Nonnull)videoFrame |Parameter change: 将RemoteStreamKey变为streamId和streamInfo |
|SnapshotResultObjC : ISnapshotResultCallback |onTakeLocalSnapshotResult:(NSInteger) taskId streamIndex:(ByteRTCStreamIndex)streamIndex image:(ByteRTCImage \* _Nullable)image errorCode:(NSInteger)errorCode |onTakeLocalSnapshotResult:(NSInteger) taskId videoSource:(ByteRTCVideoSource \* _Nullable)videoSource image:(ByteRTCImage \* _Nullable)image errorCode:(NSInteger)errorCode |Parameter change: 将streamIndex变为VideoSource |
|SnapshotResultObjC : ISnapshotResultCallback |onTakeRemoteSnapshotResult:(NSInteger)taskId streamKey:(ByteRTCRemoteStreamKey \* _Nonnull)streamKey image:(ByteRTCImage \* _Nullable)image errorCode:(NSInteger)errorCode |onTakeRemoteSnapshotResult:(NSInteger)taskId streamId:(NSString\*)streamId info:(ByteRTCStreamInfo \* _Nonnull)info image:(ByteRTCImage \* _Nullable)image errorCode:(NSInteger)errorCode |Parameter change: 将RemoteStreamKey变为streamId和streamInfo |
|ByteRTCAudioFrameObserver : IAudioFrameObserver |onRemoteUserAudioFrame:(ByteRTCRemoteStreamKey \* _Nonnull)streamKey audioFrame:(ByteRTCAudioFrame \* _Nonnull)audioFrame |onRemoteUserAudioFrame:(NSString \* _Nonnull)streamId info:(ByteRTCStreamInfo \* _Nonnull)info audioFrame:(ByteRTCAudioFrame \* _Nonnull)audioFrame |Parameter change: 将RemoteStreamKey变为streamId和streamInfo |
|ByteRtcAudioFrameProcessorOCC : IAudioFrameProcessor |onProcessRemoteUserAudioFrame:(ByteRTCRemoteStreamKey \* _Nonnull)streamKey audioFrame:(ByteRTCAudioFrame \* _Nonnull)audioFrame |onProcessRemoteUserAudioFrame:(NSString \* _Nonnull)streamId info:(ByteRTCStreamInfo \* _Nonnull)info audioFrame:(ByteRTCAudioFrame \* _Nonnull)audioFrame |Parameter change: 将RemoteStreamKey变为streamId和streamInfo |
|ExternalVideoEncoderEventHandlerObjC : IExternalVideoEncoderEventHandler |onStart:(ByteRTCStreamIndex)streamIndex |onStart:(NSString\*)streamId info:(ByteRTCStreamInfo \* _Nonnull)info |Parameter change: 将streamIndex变为streamId和streamInfo |
|ExternalVideoEncoderEventHandlerObjC : IExternalVideoEncoderEventHandler |onStop:(ByteRTCStreamIndex)streamIndex |onStop:(NSString\*)streamId info:(ByteRTCStreamInfo \* _Nonnull)info |Parameter change: 将streamIndex变为streamId和streamInfo |
|ExternalVideoEncoderEventHandlerObjC : IExternalVideoEncoderEventHandler |onRateUpdate:(ByteRTCStreamIndex)streamIndex withVideoIndex:(NSInteger)videoIndex withFps:(NSInteger)fps withBitRate:(NSInteger)bitRateKps |onRateUpdate:(NSString\*)streamId info:(ByteRTCStreamInfo \* _Nonnull)info withVideoIndex:(NSInteger)videoIndex withFps:(NSInteger)fps withBitRate:(NSInteger)bitRateKps |Parameter change: 将streamIndex变为streamId和streamInfo |
|ExternalVideoEncoderEventHandlerObjC : IExternalVideoEncoderEventHandler |onRequestKeyFrame:(ByteRTCStreamIndex)streamIndex withVideoIndex:(NSInteger)videoIndex |onRequestKeyFrame:(NSString\*)streamId info:(ByteRTCStreamInfo \* _Nonnull)info withVideoIndex:(NSInteger)videoIndex |Parameter change: 将streamIndex变为streamId和streamInfo |
|ExternalVideoEncoderEventHandlerObjC : IExternalVideoEncoderEventHandler |onActiveVideoLayer:(ByteRTCStreamIndex)streamIndex withVideoIndex:(NSInteger)videoIndex withActive:(BOOL)active |onActiveVideoLayer:(NSString\*)streamId info:(ByteRTCStreamInfo \* _Nonnull)info withVideoIndex:(NSInteger)videoIndex withActive:(BOOL)active |Parameter change: 将streamIndex变为streamId和streamInfo |


<span id="type-changes"></span>
## Type Changes

<span id="room-mode"></span>
### Room Mode


|Changed data type |V3.58 |V3.60 |Description |
|---|---|---|---|
|ByteRTCRoomProfile |* ByteRTCRoomProfileChat = 5<br><br>* ByteRTCRoomProfileLwTogether = 7 |ByteRTCRoomProfileCall = 19 |Focuses more on fluency, with relatively low default video bitrate, low audio quality requirements, and high fluency requirements. |
| |* ByteRTCRoomProfileGameHD = 8<br><br>* ByteRTCRoomProfileCoHost = 9<br><br>* ByteRTCRoomProfileKTV = 11<br><br>* ByteRTCRoomProfileVRChat = 13<br><br>* ByteRTCRoomProfileLanLiveStreaming = 15<br><br>* ByteRTCRoomProfileLiveBroadcasting = 1 |ByteRTCRoomProfileLive = 20 |Focuses more on image quality, with relatively high default video bitrate and high audio quality requirements. |


<span id="video-frame-related"></span>
### Video frame related


|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|Video frame data |ByteRTCVideoFrame |ByteRTCVideoFrameData |1. **Type renamed**<br><br>2. **Parameter changes**:<br><br>* Removed supplementaryInfo<br><br>* Removed colorSpace<br><br>* time changed to timestamp<br><br>* planeDatas changed to planeDataArray<br><br>* planeStrides changed to planeStrideArray<br><br>* extendedData changed to seiData<br><br>* Added bufferType<br><br>* Added format<br><br>* Added addRef<br><br>* Added releaseRef |
|*Remote video frame callback position* |ByteRTCRemoteVideoRenderPosition |ByteRTCRemoteVideoSinkPosition |Type renamed |
|*Whether to mirror video frames* |ByteRTCVideoRenderMirrorType |ByteRTCVideoSinkMirrorType |Type renamed |


<span id="mixed-stream-push-events"></span>
### Mixed stream push events


* Name replacement: `ByteRTCStreamMixingEvent` changed to `ByteRTCMixedStreamTaskEvent`, sharing the same event enumeration class with WTN stream tasks.

* Enumeration value changes are as follows:



|Description |V3.58 |V3.60 |
|---|---|---|
|Request to start task<br><br>Push stream success |ByteRTCStreamMixingEventStart = 1<br><br>ByteRTCStreamMixingEventStartSuccess = 2 |ByteRTCMixedStreamTaskEventStartSuccess = 1 |
|Task start failed |ByteRTCStreamMixingEventStartFailed= 3 |ByteRTCMixedStreamTaskEventStartFailed = 2<br><br>For specific failure reasons, see ByteRTCMixedStreamTaskErrorCode |
|Request update<br><br>Task update success |ByteRTCStreamMixingEventUpdate = 4<br><br>ByteRTCStreamMixingEventUpdateSuccess = 5 |ByteRTCMixedStreamTaskEventUpdateSuccess = 3 |
|Task update failed |ByteRTCStreamMixingEventUpdateFailed = 6 |ByteRTCMixedStreamTaskEventUpdateFailed = 4<br><br>For specific failure reasons, see ByteRTCMixedStreamTaskErrorCode |
|Request to end task<br><br>Task end success |ByteRTCStreamMixingEventStop = 7<br><br>ByteRTCStreamMixingEventStopSuccess = 8 |ByteRTCMixedStreamTaskEventStopSuccess = 5 |
|Task end failed |ByteRTCStreamMixingEventStopFailed = 9 |ByteRTCMixedStreamTaskEventStopFailed = 6<br><br>For specific failure reasons, see ByteRTCMixedStreamTaskErrorCode |
|Parameter error |ByteRTCStreamMixingEventRequestParamError = 15 |Returns ByteRTCReturnStatusParameterErr = \-2 when calling startPushMixedStream:withPushTargetConfig:withMixedConfig: or updatePushMixedStream:withPushTargetConfig:withMixedConfig: |
|Task processing timeout, check network status and retry |ByteRTCStreamMixingEventUpdateTimeout = 13<br><br>ByteRTCStreamMixingEventStartTimeout = 14 |Returns ByteRTCMixedStreamTaskErrorCodeTimeout = 1091 when calling startPushMixedStream:withPushTargetConfig:withMixedConfig: or updatePushMixedStream:withPushTargetConfig:withMixedConfig: |
|Mixed stream add image |ByteRTCStreamMixingEventMixImage = 16 |ByteRTCMixedStreamTaskEventWarning = 7 |
|Warning event |None |ByteRTCMixedStreamTaskEventWarning = 7 |
|Others |ByteRTCStreamMixingEventChangeMixType = 10<br><br>ByteRTCStreamMixingEventFirstAudioFrameByClientMixer = 11<br><br>ByteRTCStreamMixingEventFirstVideoFrameByClientMixer = 12 |Removed |


<span id="single-stream-push-task-events"></span>
### Single stream push task events


* Name change: Changed from `ByteRTCSingleStreamPushEvent` to `ByteRTCSingleStreamTaskEvent`.

* Specific enumeration value changes are as follows:



|Description |V3.58 |V3.60 |
|---|---|---|
|Start push stream |ByteRTCSingleStreamPushEventStart = 1 |ByteRTCSingleStreamTaskEventStartSuccess = 1 |
|Push stream success |ByteRTCSingleStreamPushEventStartSuccess = 2 |ByteRTCSingleStreamTaskEventStartSuccess = 1 |
|Push stream failed |ByteRTCSingleStreamPushEventStartFailed = 3 |ByteRTCSingleStreamTaskEventStartFailed = 2 |
|Stop push stream |ByteRTCSingleStreamPushEventStop = 4 |ByteRTCSingleStreamTaskEventStopSuccess = 3 |
|Single stream push live task processing timeout, check network status and retry |ByteRTCSingleStreamPushEventTimeout = 5 |ByteRTCSingleStreamTaskEventWarning = 5, for specific error information see ByteRTCSingleStreamTaskErrorCode. |
|Parameter error |ByteRTCSingleStreamPushEventParamError = 6 |Returns ByteRTCReturnStatusParameterErr = \-2 when calling startPushSingleStream:singleStream:. |
|Stop push stream failed |None |ByteRTCSingleStreamTaskEventStopFailed = 4 |


<span id="audio-and-video-stream-statistics"></span>
### Audio and video stream statistics


|Function |Changed data type |Description |
|---|---|---|
|Local audio stream statistics |ByteRTCLocalAudioStats |Added fields audioDeviceLoopDelay (audio capture playback delay), encodeFrameRate (audio encoding frame rate) |
|Remote audio stream statistics |ByteRTCRemoteAudioStats |Added field decodeFrameRate (audio decoding frame rate) |
|Remote video stream statistics |ByteRTCRemoteVideoStats |Added fields capToRenderDelay (delay from sender capture start to receiver rendering completion), avSyncDiffMs (audio\-video synchronization difference), codecElapsePerFrame (average video decoding time) |


<span id="others"></span>
### Others


|Function |Name |Description |
|---|---|---|
|Publish state change reason |ByteRTCPublishStateChangeReason |**New class** |
|Screenshot error code |ByteRTCSnapshotErrorCode |**New enumeration**<br><br>Screenshot success (0, ByteRTCSnapshotErrorCodeOk)<br><br>Screenshot error. Failed to generate image data or RGBA encoding failed (\-1, ByteRTCSnapshotErrorCodeCreateFail)<br><br>Screenshot error. Invalid stream (\-2, ByteRTCSnapshotErrorCodeStreamInvalid)<br><br>Screenshot error. Screenshot timeout, timeout is 1 second (\-3, ByteRTCSnapshotErrorCodeTimeout)<br><br>Screenshot error. Image save failed (\-4, ByteRTCSnapshotErrorCodeFileSaveError) |
|Audio scenario type |ByteRTCAudioScenarioType |**Enumeration value added**<br><br>Education scenario. Suitable for high\-quality scenarios mainly focused on voice teaching content (4, ByteRTCAudioScenarioTypeEducation)<br><br>AI conversation scenario (5, ByteRTCAudioScenarioTypeAiClient) |
|Ear monitor Audio Filter type |ByteRTCEarMonitorAudioFilter |**New enumeration**<br><br>No Audio Filter (default setting) (0x0001, ByteRTCEarMonitorAudioFilterNone)<br><br>Ear monitor reuses 3A processing (0x8000, ByteRTCEarMonitorAudioFilterReuseAudioProcessing) |
|Single stream push live error code |ByteRTCSingleStreamTaskErrorCode |**Enumeration value added**<br><br>Server detects invalid task parameters (1093, ByteRTCSingleStreamTaskErrorCodeInvalidParamByServer)<br><br>Push task user ID kicked out of target room (1094, ByteRTCSingleStreamTaskErrorCodeRemoteKicked)<br><br>Push task failed to join target room (1095, ByteRTCSingleStreamTaskErrorCodeJoinDestRoomFailed)<br><br>Push task pull stream timeout in source room (1096, ByteRTCSingleStreamTaskErrorCodeReceiveSrcStreamTimeout)<br><br>Audio and video encoding push task not supported (1097, ByteRTCSingleStreamTaskErrorCodeNotSurportCodec) |
|Single stream push configuration target room information |DestInfo |**New class** |
|Single stream push type |ByteRTCSingleStreamPushType |**Enumeration added**<br><br>Single stream push to CDN (1, ByteRTCSingleStreamPushToCDN)<br><br>Single stream push to RTC room (2, ByteRTCSingleStreamPushToRTC) |
|Single stream push live configuration parameters |ByteRTCPushSingleStreamParam |**Member added**<br><br>Added to single stream push live configuration parameters: single stream push configuration target room information list (destInfo), push type (pushType) two members |
|Mirror type |ByteRTCMirrorType |**Enumeration value added**<br><br>No mirror effect during local preview, only mirror effect during encoding transmission (2, ByteRTCMirrorTypeEncoder) |


<span id="error-code-changes"></span>
## Error Code Changes

<span id="callback-warning-warningcode"></span>
### Callback warning \- WarningCode


|V3.58 |V3.60 |
|---|---|
|ByteRTCWarningCodeOldRoomBeenReplaced = \-2016 |**Removed**:<br><br>When creating a room again with the same roomId, the previously created room instance will be returned, and this error code will no longer be triggered. |


<span id="wtn-stream-formerly-public-stream"></span>
### WTN stream (formerly public stream)


* Error code name change: `ByteRTCPublicStreamErrorCode` changed to `ByteRTCMixedStreamTaskErrorCode`, sharing the same enumeration class with mixed stream push tasks.

* Specific error code change details are as follows:



|Description |V3.58 |V3.60 |
|---|---|---|
|Success |ByteRTCPublicStreamErrorCodeSuccess = 0 |ByteRTCMixedStreamTaskErrorCodeOK = 0 |
|Server parameter validation failed |ByteRTCPublicStreamErrorCodePushParamError = 1191 |Deleted, this type of error will not be called back. |
|Server internal error |ByteRTCPublicStreamErrorCodePushStatusError = 1192 Deleted, this type of error will not be called back. |ByteRTCMixedStreamTaskErrorCodeInvalidStateByServer = 1094 |
|Server unknown error |ByteRTCPublicStreamErrorCodePushInternalError = 1193 Deleted, this type of error will not be called back. |ByteRTCMixedStreamTaskErrorCodeUnKnownErrorByServer = 1096 |
|Task failed |ByteRTCPublicStreamErrorCodePushError = 1195 |ByteRTCMixedStreamTaskErrorCodePushWTNFailed = 1195 |
|Task timeout |ByteRTCPublicStreamErrorCodePushTimeOut = 1196 |ByteRTCMixedStreamTaskErrorCodeTimeOut = 1091 |
|Stream subscription timeout |ByteRTCPublicStreamErrorCodePullNoPushStream = 1300 |ByteRTCWTNSubscribeStateChangeReason.ByteRTCWTNSubscribeStateChangeReasonUnsubscribe = 1300, returned through onWTNVideoSubscribeStateChanged:state:reason: or onWTNAudioSubscribeStateChanged:state:reason:. |


<span id="mixed-stream-push-error-codes"></span>
### Mixed stream push error codes


* Error code name change: `ByteRtcTranscoderErrorCode` changed to `ByteRTCMixedStreamTaskErrorCode`, sharing the same enumeration class with WTN stream tasks.

* Specific error code change details are as follows:



|Description |V3.58 |V3.60 |
|---|---|---|
|Push stream success |ByteRtcTranscoderErrorCodeOK = 0 |ByteRTCMixedStreamTaskErrorCodeOK = 0 |
|Undefined mixed stream error |ByteRtcTranscoderErrorCodeBase = 1090 |None, this error code is not enabled. |
|Client SDK detected invalid push stream parameters |ByteRtcTranscoderErrorCodeInvalidParam = 1091 |Returns ByteRTCReturnStatusParameterErr = \-2 when calling startPushMixedStream:withPushTargetConfig:withMixedConfig: or updatePushMixedStream:withPushTargetConfig:withMixedConfig:. |
|State error, operation needs to be initiated under normal state machine state |ByteRtcTranscoderErrorCodeInvalidState = 1092 |ByteRTCMixedStreamTaskErrorCodeInvalidStateByServer = 1094 |
|Invalid operation |ByteRtcTranscoderErrorCodeInvalidOperator = 1093 |ByteRTCMixedStreamTaskErrorCodeInvalidStateByServer = 1094 |
|Push live task processing timeout, check network status and retry |ByteRtcTranscoderErrorCodeTimeOut = 1094 |ByteRTCMixedStreamTaskErrorCodeTimeOut = 1091 |
|Server detected incorrect push stream parameters |ByteRtcTranscoderErrorCodeInvalidParamByServer = 1095 |ByteRTCMixedStreamTaskErrorCodeInvalidParamByServer = 1092 |
|Stream subscription timeout |ByteRtcTranscoderErrorCodeSubTimeoutByServer = 1096 |ByteRTCMixedStreamTaskErrorCodeSubTimeoutByServer = 1093 |
|Mixed stream server internal error |ByteRtcTranscoderErrorCodeInvalidStateByServer = 1097 |ByteRTCMixedStreamTaskErrorCodeInvalidStateByServer = 1094 |
|Mixed stream server push CDN failed |ByteRtcTranscoderErrorCodeAuthenticationByCDN = 1098 |ByteRTCMixedStreamTaskErrorCodeAuthenticationByCDN = 1095 |
|Server received signaling timeout, check network status and retry. |ByteRtcTranscoderErrorCodeTimeoutBySignaling = 1099 |ByteRTCMixedStreamTaskErrorCodeSignalRequestTimeout = 1097 |
|Image mixed stream failed |ByteRtcTranscoderErrorCodeMixImageFail = 1100 |ByteRTCMixedStreamTaskErrorCodeMixImageFailed = 1098 |
|Server unknown error |ByteRtcTranscoderErrorCodeUnKnownErrorByServer = 1101 |ByteRTCMixedStreamTaskErrorCodeUnKnownErrorByServer = 1096 |


<span id="single-stream-push-error-codes"></span>
### Single stream push error codes


* Error code replacement: Replaced `ByteRTCTranscoderErrorCode` with `ByteRTCSingleStreamTaskErrorCode`.

* Specific error code changes and corresponding details are as follows:



|Description |V3.58 |V3.60 |
|---|---|---|
|Push stream success |TRANSCODER_ERROR_OK = 0 |ByteRTCMixedStreamTaskErrorCodeOK = 0 |
|Undefined mixed stream error |TRANSCODER_ERROR_BASE = 1090 |None, this error code is not enabled. |
|Client SDK detected invalid push stream parameters |TRANSCODER_ERROR_INVALID_PARAM = 1091 |Returns ByteRTCReturnStatusParameterErr = \-2 when calling startPushSingleStream:singleStream:. |
|State error, operation needs to be initiated under normal state machine state |TRANSCODER_ERROR_INVALID_STATE = 1092 |None, single stream tasks will not trigger this error code. |
|Invalid operation |TRANSCODER_ERROR_INVALID_OPERATOR = 1093 |None, single stream tasks will not trigger this error code. |
|Push live task processing timeout, check network status and retry |TRANSCODER_ERROR_TIMEOUT = 1094 |None, single stream tasks will not trigger this error code. |
|Server detected incorrect push stream parameters |TRANSCODER_ERROR_INVALID_PARAM_BY_SERVER = 1095 |None, single stream tasks will not trigger this error code. |
|Stream subscription timeout |TRANSCODER_ERROR_SUB_TIMEOUT_BY_SERVER = 1096 |None, single stream tasks will not trigger this error code. |
|Mixed stream server internal error |TRANSCODER_ERROR_INVALID_STATE_BY_SERVER = 1097 |None, single stream tasks will not trigger this error code. |
|Mixed stream server push CDN failed |TRANSCODER_ERROR_AUTHENTICATION_BY_CDN = 1098 |None, single stream tasks will not trigger this error code. |
|Server received signaling timeout, check network status and retry |TRANSCODER_ERROR_TIMEOUT_BY_SIGNALING = 1099 |ByteRTCSingleStreamTaskErrorCodeSignalRequestTimeout = 1092 |
|Image mixed stream failed |TRANSCODER_ERROR_MIX_IMAGE_FAIL = 1100 |None, single stream tasks will not trigger this error code. |
|Server unknown error |TRANSCODER_ERROR_UNKNOW_ERROR_BY_SERVER = 1101 |ByteRTCSingleStreamTaskErrorCodeUnknownByServer = 1091 |


<span id="other-error-codes"></span>
### Other error codes

Removed some error codes that have been deprecated for multiple versions


|Description |Error code |
|---|---|
|After setting own visibility to false, attempting to publish stream will trigger this warning. |ByteRTCWarningCodePublishStreamForbiden = \-2010 |
|When automatic subscription mode is not turned off, attempting to enable manual subscription mode will trigger this warning. |ByteRTCWarningCodeGetRoomFailed = \-2000 |


<span id="new-interfaces"></span>
## New Interfaces


|**Interface** |**Function description** |
|---|---|
|createRTSRoom: |Create RTS room |
|pushReferenceAudioPCMData: |Push external audio reference frames to SDK |
|getCallId |Get call ID. This method needs to be called after joining the room |
|takeLocalSnapshotToFile: |Capture local video stream frame, generate JPG file, and save to specified local path. |
|takeRemoteSnapshotToFile:filePath: |Capture remote video stream frame, generate JPG file, and save to specified local path. |
|rtcEngine:onLocalSnapshotTakenToFile:filePath:width:height:errorCode:taskId: |When using takeSnapshotToFile:filePath: to capture video frame, this callback will be received to report whether the screenshot was successful and the captured image information. |
|rtcEngine:onRemoteSnapshotTakenToFile:info:filePath:width:height:errorCode:taskId: |When using takeSnapshotToFile:filePath: to capture video frame, this callback will be received to report whether the screenshot was successful and the captured image information. |
|setEarMonitorMode:filter: |Ear monitor supports reusing locally captured audio after custom processing |
|setWTNStreamDelegate: |Set WTN stream callback interface |
|rtcRoom:onRoomEvent:uid:state:info: |Room event callback, with new enum ByteRTCRoomEventInfo |
|setStreamExtraInfo: |Set additional information for current push stream |
|rtcRoom:onRoomStreamExtraInfoUpdate:info:extraInfo: |Callback to receive additional stream information set by other users calling setStreamExtraInfo in the same room. |
|createGameRoom |Create game room |
|ByteRTCGameRoom.destroy |Destroy game room |
|ByteRTCGameRoom.setRTCGameRoomDelegate: |Set delegate object for GameRTCRoom events<br><br>Handle of ByteRTCGameRoomDelegate, listen to callback events corresponding to this object. |
|ByteRTCGameRoom.joinRoom: |Join game room |
|ByteRTCGameRoom.leaveRoom |Leave game room |
|ByteRTCGameRoom.getRangeAudio |New addition |
|ByteRTCGameRoom.updateToken: |Update Token |
|ByteRTCGameRoom.enableMicrophone: |Enable or disable microphone |
|ByteRTCGameRoom.enableSpeakerphone: |Enable or disable speakerphone |
|ByteRTCGameRoom.enableAudioSend: |Send or cancel sending audio stream |
|ByteRTCGameRoom.enableAudioReceive: |Whether to receive audio stream from specified user |
|ByteRTCGameRoom.setRemoteRoomAudioPlaybackVolume: |Adjust audio playback volume of all remote users in a certain room. |


<span id="deleted-deprecated-interfaces"></span>
## Deleted/Deprecated Interfaces

Removed deprecated or not recommended methods, as follows:


|**Function** |**Deleted/deprecated interface** |**Alternative interface** |
|---|---|---|
|Deprecated |* (int)setLocalVideoSink:(ByteRTCStreamIndex)index withSink:(id*Nullable)videoSink withPixelFormat:(ByteRTCVideoSinkPixelFormat)requiredFormat NS_SWIFT_NAME(setLocalVideoSink(* :withSink:withPixelFormat:)); |* (int)setLocalVideoSink:(id_Nullable)videoSink withPixelFormat:(ByteRTCVideoSinkPixelFormat)requiredFormat NS_SWIFT_NAME(setLocalVideoSink(withSink:withPixelFormat:)) |
|Deprecated |* (int)setRemoteVideoSink:(ByteRTCRemoteStreamKey\* _Nonnull)streamKey withSink:(id*Nullable)videoSink withPixelFormat:(ByteRTCVideoSinkPixelFormat)requiredFormat NS_SWIFT_NAME(setRemoteVideoSink(* :withSink:withPixelFormat:)) |* (int)setRemoteVideoSink:(NSString\* _Nonnull)streamId withSink:(id*Nullable)videoSink withPixelFormat:(ByteRTCVideoSinkPixelFormat)requiredFormat NS_SWIFT_NAME(setRemoteVideoSink(* :withSink:withPixelFormat:)) |
|Deleted |(RTCVideo \* _Nullable) createRTCVideo:(NSString \* _Nonnull)appId delegate:(id_Nullable)delegate parameters:(NSDictionary \* _Nonnull)parameters |(ByteRTCEngine \* _Nullable) createRTCEngine:(ByteRTCEngineConfig \* _Nonnull) config delegate:(id_Nullable)delegate |
|Deleted |getErrorDescription: |无替代接口 |
|Deleted |startASR:handler:<br><br>stopASR |无替代接口<br><br>如果需要使用 ASR 功能，可以通过实时字幕功能相关接口实现：startSubtitle:、stopSubtitle |
|Deleted |onSuccessonMessage:rtcEngine:<br><br>onError: |如果需要使用 ASR 功能，可以通过实时字幕功能相关接口实现。rtcRoom:onSubtitleStateChanged:errorCode:errorMessage:<br><br>rtcRoom:onSubtitleMessageReceived: |
|Deleted |* (void)setDeviceId:(NSString\* _Nonnull) deviceID |无替代接口 |
|Deleted |\-(int)setAudioPlaybackDevice:(ByteRTCAudioPlaybackDevice)audioPlaybackDevice __deprecated_msg("Will be removed in new version") |* (int)setDefaultAudioRoute:(ByteRTCAudioRoute)audioRoute |
|Deleted |(void)rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onRoomError:(ByteRTCErrorCode)errorCode __deprecated_msg("Will be removed in new version") |* (void)rtcRoom:(ByteRTCRoom \*_Nonnull)rtcRoom onRoomStateChanged:(NSString \*_Nonnull)roomId withUid:(nonnull NSString \*)uid state:(NSInteger)state extraInfo:(NSString \*_Nonnull)extraInfo;<br><br>* (void)rtcRoom:(ByteRTCRoom \*_Nonnull)rtcRoom onStreamStateChanged:(NSString \*_Nonnull)roomId withUid:(nonnull NSString \*)uid state:(NSInteger)state extraInfo:(NSString \*_Nonnull)extraInfo |
|Deleted |(int)subscribeUserStream:(NSString \*_Nonnull)userId streamType:(ByteRTCStreamIndex)streamType mediaType:(ByteRTCSubscribeMediaType)mediaType videoConfig:(ByteRTCSubscribeVideoConfig \*_Nonnull)videoConfig __deprecated_msg("Will be removed in new version") |* (int)subscribeStreamVideo:(NSString \*_Nonnull)streamId subscribe:(BOOL)subscribe<br><br>* (int)subscribeStreamAudio:(NSString \*_Nonnull)streamId subscribe:(BOOL)subscribe |
|Deleted |1. \-(void)rtcEngine:(ByteRTCVideo \* _Nonnull)engine onUserMuteAudio:(NSString \* _Nonnull)roomId uid:(NSString \* _Nonnull)uid muteState:(ByteRTCMuteState)muteState __deprecated_msg("Will be removed in new version")<br><br>2. \-(void)rtcEngine:(ByteRTCVideo \* _Nonnull)engine onUserMuteVideo:(NSString \* _Nonnull)roomId uid:(NSString \* Nonnull)uid withMuteState:(ByteRTCMuteState)muteState NS_SWIFT_NAME(rtcEngine(:onUserMuteVideo:uid:withMuteState:)) __deprecated_msg("Will be removed in new version")<br><br>3. \-(void)rtcEngine:(ByteRTCVideo \* _Nonnull)engine onMediaDeviceStateChanged:(NSString\*_Nonnull)deviceID device_type:(ByteRTCMediaDeviceType)deviceType device_state:(ByteRTCMediaDeviceState)deviceState device_error:(ByteRTCMediaDeviceError)deviceError __attribute((deprecated("Will be removed in new version")))<br><br>4. \-(void)rtcEngine:(ByteRTCVideo \* _Nonnull)engine onMediaDeviceWarning:(NSString\*_Nonnull)deviceId deviceType:(ByteRTCMediaDeviceType)deviceType deviceWarning:(ByteRTCMediaDeviceWarning)deviceWarning __deprecated_msg("Will be removed in new version")<br><br>5. \-(void)rtcEngine:(ByteRTCVideo \* _Nonnull)engine onAudioPlaybackDeviceChanged:(ByteRTCAudioPlaybackDevice)device __deprecated_msg("Will be removed in new version")<br><br>6. \-(void)rtcEngine:(ByteRTCVideo \* _Nonnull)engine onAudioMixingStateChanged:(NSInteger)mixId state:(ByteRTCAudioMixingState)state error:(ByteRTCAudioMixingError)error<br><br>7. \-(void)rtcEngine:(ByteRTCVideo \*_Nonnull)engine onHttpProxyState:(NSInteger)state<br><br>8. \-(void)rtcEngine:(ByteRTCVideo \*_Nonnull)engine onSocks5ProxyState:(NSInteger)state cmd:(NSString \*_Nonnull)cmd proxy_address:(NSString \*_Nonnull)proxyAddress local_address:(NSString \*_Nonnull)localAddress remote_address:(NSString \*_Nonnull)remoteAddress |1. (void)rtcRoom:(ByteRTCRoom\* _Nonnull)rtcRoom onUserPublishStreamAudio:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info isPublish:(BOOL)isPublish<br><br>2. (void)rtcRoom:(ByteRTCRoom\* _Nonnull)rtcRoom onUserPublishStreamVideo:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info isPublish:(BOOL)isPublish<br><br>3. (void)rtcEngine:(ByteRTCEngine \* _Nonnull)engine onAudioDeviceStateChanged:(NSString\*_Nonnull)deviceID device_type:(ByteRTCAudioDeviceType)deviceType device_state:(ByteRTCMediaDeviceState)deviceState device_error:(ByteRTCMediaDeviceError)deviceError<br><br>* (void)rtcEngine:(ByteRTCEngine \* _Nonnull)engine onVideoDeviceStateChanged: (NSString\*_Nonnull)deviceID device_type: (ByteRTCVideoDeviceType)deviceType device_state:(ByteRTCMediaDeviceState)deviceState device_error:(ByteRTCMediaDeviceError)deviceError<br><br>4. (void)rtcEngine:(ByteRTCEngine \* _Nonnull)engine onAudioDeviceWarning:(NSString\*_Nonnull)deviceId deviceType:(ByteRTCAudioDeviceType)deviceType deviceWarning:(ByteRTCMediaDeviceWarning)deviceWarning<br><br>* (void)rtcEngine:(ByteRTCEngine \* _Nonnull)engine onVideoDeviceWarning (NSString\*_Nonnull)deviceId deviceType:(ByteRTCVideoDeviceType)deviceType deviceWarning:(ByteRTCMediaDeviceWarning)deviceWarning<br><br>5. (void)rtcEngine:(ByteRTCEngine \*_Nonnull)engine onAudioRouteChanged:(ByteRTCAudioRoute)device<br><br>6. \-(void)onAudioEffectPlayerStateChanged:(int)effectId state:(ByteRTCPlayerState)state error:(ByteRTCPlayerError)error<br><br>   \-(void)onMediaPlayerStateChanged:(int)playerId state:(ByteRTCPlayerState)state error:(ByteRTCPlayerError)error<br><br>7. (void)rtcEngine:(ByteRTCVideo \* _Nonnull)engine onLocalProxyStateChanged:(ByteRTCLocalProxyType)type withProxyState:(ByteRTCLocalProxyState)state withProxyError:(ByteRTCLocalProxyError)error<br><br>8. (void)rtcEngine:(ByteRTCVideo \* _Nonnull)engine onLocalProxyStateChanged:(ByteRTCLocalProxyType)type withProxyState:(ByteRTCLocalProxyState)state withProxyError:(ByteRTCLocalProxyError)error |
|Deleted |1. \-(int)checkVideoEffectLicense:(NSString \* Nonnull)licenseFile NS_SWIFT_NAME(checkVideoEffectLicense(:)) __deprecated_msg("Will be removed in new version")<br><br>2. \-(void)setVideoEffectAlgoModelPath:(NSString \* *Nonnull)modelPath __deprecated_msg("Will be removed in new version")* <br><br>   *3. \-(int)enableVideoEffect:(BOOL)enabled NS_SWIFT_NAME(enableVideoEffect(* :)) __deprecated_msg("Will be removed in new version")<br><br>3. (int) :(NSArray <NSString  *\> _Nonnull)effectNodePaths __deprecated_msg("Will be removed in new version")* <br><br>   *5. \-(int) updateVideoEffectNode:(NSString \* _Nonnull)nodePath nodeKey:(NSString \* Nonnull)nodeKey nodeValue:(float) nodeValue NS_SWIFT_NAME(updateVideoEffectNode(:nodeKey:nodeValue:)) __deprecated_msg("Will be removed in new version")* <br><br>   *6. \-(int) setVideoEffectColorFilter:(NSString \* _Nonnull)resPath __deprecated_msg("Will be removed in new version")* <br><br>   *7. \-(int) setVideoEffectColorFilterIntensity:(float) intensity __deprecated_msg("Will be removed in new version")* <br><br>   *8. \-(int) setBackgroundSticker:(NSString _Nullable)modelPath source:(ByteRTCVirtualBackgroundSource* _Nonnull)source __deprecated_msg("Will be removed in new version")<br><br>4. \-(int) registerFaceDetectionObserver:(Nullable id)faceDetectionObserver withInterval:(NSInteger)interval NS_SWIFT_NAME(registerFaceDetectionObserver(:withInterval:)) __deprecated_msg("Will be removed in new version") |美颜相关API从ByteRTCEngine（原ByteRTCVideo）移到了ByteRTCVideoEffect中：<br><br><br>1. (int) initCVResource:(NSString\* _Nonnull)licenseFile withAlgoModelDir: (NSString\* _Nonnull)algoModelDir<br><br>2. (int) initCVResource:(NSString\* _Nonnull)licenseFile withAlgoModelDir: (NSString\* _Nonnull)algoModelDir<br><br>3. (int) enableVideoEffect<br><br>4. (int) setEffectNodes:(NSArray<NSString\*\> *_Nonnull)effect_nodes*<br><br>   *5. (int) updateEffectNode:(NSString* _Nonnull)node_path key:(NSString\* _Nonnull)key value:(float) value<br><br>5. (int) setColorFilter:(NSString\* _Nonnull)filter_res<br><br>6. (int) setColorFilterIntensity:(float) intensity<br><br>7. (int) enableVirtualBackground:(NSString\* _Nonnull)bg_sticker_res withSource:(ByteRTCVirtualBackgroundSource\* _Nonnull)source<br><br>8. (int) enableFaceDetection:(id)observer withInterval:(NSUInteger)interval withModelPath:(NSString \*)path |
|Deleted |1. \-(int)startLiveTranscoding:(NSString \* _Nonnull)taskID transcoding:(ByteRTCLiveTranscoding \*_Nullable)<br><br>2. \-(int)stopLiveTranscoding:(NSString \*_Nonnull)taskID __deprecated_msg("deprecated since 352, will be deleted in 358, use stopPushStreamToCDN instead")<br><br>3. \-(int)updateLiveTranscoding:(NSString \*_Nonnull)taskID transcoding:(ByteRTCLiveTranscoding \*_Nonnull)transcoding __deprecated_msg("deprecated since 352, will be deleted in 358, use updatePushMixedStreamToCDN instead") |1. (int)startPushMixedStream:(NSString \* _Nonnull)taskId withPushTargetConfig:(ByteRTCMixedStreamPushTargetConfig\*)pushTargetConfig withMixedConfig:(ByteRTCMixedStreamConfig \*_Nullable)config<br><br>2. (int)stopPushMixedStream:(NSString \*_Nonnull)taskId withPushTargetType:(ByteRTCMixedStreamPushTargetType)pushTargetType<br><br>3. (int)updatePushMixedStream:(NSString  *_Nonnull)taskId withPushTargetConfig:(ByteRTCMixedStreamPushTargetConfig*)pushTargetConfig withMixedConfig:(ByteRTCMixedStreamConfig \*_Nonnull)config |
|Deleted |ByteRTCAudioMixingManager |ByteRTCMediaPlayer<br><br>ByteRTCAudioEffectPlayer |
|Deleted |\-(int)muteAudioPlayback:(ByteRTCMuteState)muteState __deprecated_msg("Will be removed in new version") |* (int)setPlaybackVolume:(NSInteger)volume |
| |1. \-(int)updatePosition:(ByteRTCPosition\* _Nonnull) pos __deprecated_msg("deprecated since 352, use updateSelfPosition instead");<br><br>2. \-(int)updateSelfOrientation:(ByteRTCHumanOrientation\* _Nonnull) orientation __deprecated_msg("deprecated since 352, use updateSelfPosition instead");<br><br>3. \-(int)updateListenerPosition:(ByteRTCPosition\* _Nonnull) pos __deprecated_msg("deprecated since 352, use updateRemotePosition instead");<br><br>4. \-(int)updateListenerOrientation:(ByteRTCHumanOrientation\* _Nonnull)orientation __deprecated_msg("deprecated since 352, use updateRemotePosition instead") |1. \-(int)updateSelfPosition:(ByteRTCPositionInfo\* _Nonnull)positionInfo<br><br>2. \-(int)updateSelfPosition:(ByteRTCPositionInfo\* _Nonnull)positionInfo<br><br>3. \-(int)updateRemotePosition:(NSString \* _Nonnull)uid positionInfo:(ByteRTCPositionInfo\* _Nonnull)positionInfo<br><br>4. \-(int)updateRemotePosition:(NSString \* _Nonnull)uid positionInfo:(ByteRTCPositionInfo\* _Nonnull)positionInfo |
|Deleted |* ByteRTCEngine（原ByteRTCVideo）类定义的以下方法：<br><br>* (int)pushScreenVideoFrame:(CVPixelBufferRef _Nonnull )frame time:(CMTime)pts rotation:(int)rotation<br><br>* (int)setScreenAudioStreamIndex:(ByteRTCStreamIndex) index |屏幕分享功能部分删除，暂无替换 |


<span id="_3-58"></span>
# 3.58

<span id="important-notes"></span>
## Important Notes


1. This version separates the required library `RealXBase.xcframework` from the main library `VolcEngineRTC.xcframework`. If you have only integrated the main library or integrated the main library with some optional plugins, you will need to adjust the integration method. Versions before 3.57 required the inclusion of one mandatory main library `VolcEngineRTC.xcframework`. Versions 3.57 and later require the inclusion of two mandatory main libraries `VolcEngineRTC.xcframework` and `RealXBase.xcframework`. Please refer to the updates in the [Integrate Plugins on Demand to Reduce the Size of the Application](https://docs.byteplus.com/6uofwzl3/25046).

2. A SAMI audio technology dynamic library plugin is provided. For details, see [Integrate Plugins on Demand to Reduce the Size of the Application](https://docs.byteplus.com/6uofwzl3/25046).

3. This version has unified all non\-standard API namings to improve code standardization and usability. The following are examples of changes; please refer to the [Type Details](https://docs.byteplus.com/en/docs/12/docs-70088) page for specific modifications to the types used.

   
   |Change Object |Change Details |Old Version Example |New Version Example |
   |---|---|---|---|
   |Enum Values |Unified with the prefix "ByteRTC", changed to "ClassName+ValueName" |For example, `ByteRTCSEICountPerFrame`:<br><br><br>* kSingleSEIPerFrame = 0,<br><br>* kMultiSEIPerFrame = 1, |For example, `ByteRTCSEICountPerFrame`:<br><br><br>* ByteRTCSEICountPerFrameSingle = 0,<br><br>* ByteRTCSEICountPerFrameMulti = 1, |
   |Struct Members |Changed to lowercase initial letter, camel case notation |For example, `ByteRTCLocalStreamStats`:<br><br><br>* audio_stats<br><br>* video_stats<br><br>* tx_quality<br><br>* rx_quality<br><br>* is_screen |For example, `ByteRTCLocalStreamStats`:<br><br><br>* audioStats<br><br>* videoStats<br><br>* txQuality<br><br>* rxQuality<br><br>* isScreen |
   


<span id="api-changes"></span>
## API Changes


|Change Details |Functional Module |Deprecated Class/Interface |Replacement Class/Interface |Notes |
|---|---|---|---|---|
|Removed |Main Class |`ByteRTCEngineKit` |`ByteRTCVideo` | |
|Removed |Engine Management |`ByteRTCVideo.setEnv` |`RTCVideo.createRTCVideo:delegate:parameters:` |For more details, please consult technical support. |
|Expanded Usage Range |Video Processing |`setVideoDecoderConfig` |`setVideoDecoderConfig` |The old interface only supported manual subscription, and the new one also supports automatic subscription. |
|Deprecated |Video Management |`- (int)updateRemoteStreamVideoCanvas:(ByteRTCRemoteStreamKey * _Nonnull)key withRenderMode:(ByteRTCRenderMode)renderMode withBackgroundColor:(NSUInteger)backgroundColor NS_SWIFT_NAME(updateRemoteStreamVideoCanvas(_:withRenderMode:withBackgroundColor:));` |`- (int)updateRemoteStreamVideoCanvas:(ByteRTCRemoteStreamKey * _Nonnull)key withRemoteVideoRenderConfig:(ByteRTCRemoteVideoRenderConfig * _Nonnull)remoteVideoRenderConfig NS_SWIFT_NAME(updateRemoteStreamVideoCanvas(_:withRemoteVideoRenderConfig:));` |The new interface unifies the rendering mode and background color settings through the `remoteVideoRenderConfig` parameter. Additionally, a new parameter `renderRotation` is added to support setting the rotation angle of the video frame. |
|Removed |Audio Processing |`ByteRTCAudioProcessor` |`ByteRTCAudioFrameProcessor` |`ByteRTCAudioProcessor` was deprecated in version 3.42 and has been removed in this version. |
|New Member Variable in Parameter Data Structure |Audio Management |`enableAudioPropertiesReport` |`enableAudioPropertiesReport` |A new parameter `enableVoicePitch` is added to control whether to callback the fundamental frequency of the local user's voice. |


<span id="callback-changes"></span>
## Callback Changes


|Change Details |Functional Module |Deprecated Class/Interface |Replacement Class/Interface |Notes |
|---|---|---|---|---|
|Removed |Main Callback Class |`ByteRTCEngineDelegate` |`ByteRTCVideoDelegate` | |
|Parameter Change |Message |`(void)rtcEngineOnLogout:(ByteRTCVideo * _Nonnull)engine NS_SWIFT_NAME(rtcEngineOnLogout(_:))` |`(void)rtcEngine:(ByteRTCVideo * _Nonnull)engine onLogout:(ByteRTCLogoutReason)reason` |A new `reason` parameter has been added to the `onLogout` callback to differentiate between voluntary and involuntary logouts by the user. |
|New Member Variable in Parameter Data Structure |Audio Management |`onLocalAudioPropertiesReport` |`onLocalAudioPropertiesReport` |A new parameter `voicePitch` has been added to return the fundamental frequency of the local user's voice. |


<span id="type-changes"></span>
## Type Changes


|Change Details |Functional Module |Changed Data Type |Notes |
|---|---|---|---|
|New Enum Value Added |Audio Effects |`ByteRTCPlayerState` | |
|Member Variable Change |CDN Live Streaming |`ByteRTCMixedStreamLayoutRegionConfig` |The setting for the live streaming of individual user images has changed from a normalized ratio relative to the overall image to an absolute pixel value setting. |


<span id="error-code-changes"></span>
## Error Code Changes


|Change Details |Error Code |Notes |
|---|---|---|
|Enum Value Addition/Removal |`ByteRTCUserMessageSendResult` |New error codes for client message sending failures to the business server have been added:<br><br>`ByteRTCUserMessageSendResultE2BSSendFailed = 17`<br><br>`ByteRTCUserMessageSendResultE2BSReturnFailed = 18` |


<span id="_3-56"></span>
# 3.56

<span id="important-notes"></span>
## Important Notes

Since V3.56, the RTC SDK for iOS requires iOS 11.0 or later.

<span id="sdk-integration"></span>
## SDK Integration

A new plugin named `ByteRTCFFmpegAudioExtension.xcframework` is added in this version, which supports functionality of playback from memory and enables decoding of audio files in various formats including mp3, mp4, aac, m4a, 3gp, wav, ogg, ts, and wma. After integrating this plugin, the app's size will increase by 807KB for the arm64 architecture. This plugin is optional, and can be excluded from the main project if it is not needed.

<span id="api"></span>
## API

This version adds a return value for all APIs, through which the failed API call can be clearly identified and the cause of the failure can be located. For the meaning of the specific return value, refer to each API comment.

Other API changes:


|Type |Function Module |Previous |Current |Notes |
|---|---|---|---|---|
|Deprecated and replaced |Audio Mixing |* `getAudioMixingManager`<br><br>* `ByteRTCAudioMixingManager` |* `getAudioEffectPlayer`<br><br>* `ByteRTCAudioEffectPlayer`<br><br>* `getMediaPlayer`<br><br>* `ByteRTCMediaPlayer` |This version splits the audio mixing class into audio effect management class and music management class.<br><br>Generally, for audio effect less than 20 seconds, use audio effect class; for audio files longer than 20 seconds or PCM data, use music management class.<br><br>See the comparison table for the API mapping between deprecated API and new API. |
|Deleted |Audio Processing |`ByteRTCAudioProcessor` |`ByteRTCAudioFrameProcessor` |`ByteRTCAudioProcessor` was deprecated in 3.45, and is deleted in 3.56. |
|Modified |Audio Management |`enableAudioPropertiesReport` |`enableAudioPropertiesReport` |Adds `enableVoicePitch` to control whether to return the vocal pitch of local users. |
|Modified |Video Processing |`setVideoDecoderConfig` |`setVideoDecoderConfig` |Previously, it was only supported with manual subscription, but now it is also supported with automatic subscription. |
|Deprecated |Video Management |`- (int)updateRemoteStreamVideoCanvas:(ByteRTCRemoteStreamKey * _Nonnull)key withRenderMode:(ByteRTCRenderMode)renderMode withBackgroundColor:(NSUInteger)backgroundColor NS_SWIFT_NAME(updateRemoteStreamVideoCanvas(_:withRenderMode:withBackgroundColor:));` |`- (int)updateRemoteStreamVideoCanvas:(ByteRTCRemoteStreamKey * _Nonnull)key withRemoteVideoRenderConfig:(ByteRTCRemoteVideoRenderConfig * _Nonnull)remoteVideoRenderConfig NS_SWIFT_NAME(updateRemoteStreamVideoCanvas(_:withRemoteVideoRenderConfig:));` |With the new API, you can set both the render mode and the background color through the "remoteVideoRenderConfig" parameter. In addition, another parameter "renderRotation" is added allowing you to set the rotation angle of the remote video frame. |


 &nbsp;

API mapping in audio mixing module:


|Categories |Use |Deprecated APIs, callbacks, classes |New APIs, callbacks, classes (Audio Effect) |New APIs, callbacks, classes (Media) |Notes |
|---|---|---|---|---|---|
|Get instance |Get player instances |getAudioMixingManager |getAudioEffectPlayer |getMediaPlayer | |
|Class | |ByteRTCAudioMixingManager |ByteRTCAudioEffectPlayer |ByteRTCMediaPlayer | |
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
|Callback |Audio data callback |* registerAudioFileFrameObserver<br><br>* onAudioFileFrame |NA |* ByteRTCMediaPlayerAudioFrameObserver<br><br>* onFrame | |


<span id="callback"></span>
## Callback


|Type |Function Module |Previous |Current |Notes |
|---|---|---|---|---|
|Modified |Audio Management |`onLocalAudioPropertiesReport` |`onLocalAudioPropertiesReport` |Adds `voicePitch` to return the vocal pitch of local users. |
|Modified |Message |`(void)rtcEngineOnLogout:(ByteRTCVideo * _Nonnull)engine NS_SWIFT_NAME(rtcEngineOnLogout(_:))` |`(void)rtcEngine:(ByteRTCVideo * _Nonnull)engine onLogout:(ByteRTCLogoutReason)reason` |Adds a new parameter `reason` on `onLogout` to describe the reason why the user logs out. |


<span id="keytype"></span>
## Keytype


|Change |Class |Previous |Current |Notes |
|---|---|---|---|---|
|Modified |`ByteRTCRoomStats` |`tx_cellular_kbitrate` |`txCellularKBitrate` |<br>---<br><br> |
|Modified |`ByteRTCRoomStats` |`rx_cellular_kbitrate` |`rxCellularKBitrate` |<br>---<br><br> |
|Modified |`ByteRTCVideoSourceType` |* ByteRTCVideoSourceTypeEncodedManualSimulcast = 2<br><br>* ByteRTCVideoSourceTypeEncodedAutoSimulcast = 3 |* ByteRTCVideoSourceTypeEncodedAutoSimulcast = 2<br><br>* ByteRTCVideoSourceTypeEncodedManualSimulcast = 3 |The modified enumeration member and its corresponding value now match with those of the SDK for the other platforms. |


<span id="error-code"></span>
## Error Code


|Type |Error Code |Notes |
|---|---|---|
|New |`ByteRTCUserMessageSendResult` |Adds new error codes for message sending failure from the client to the app server:<br><br><br>* ByteRTCUserMessageSendResultE2BSSendFailed = 17<br><br>* ByteRTCUserMessageSendResultE2BSReturnFailed = 18 |


<span id="_3-52"></span>
# 3.52

<span id="api"></span>
## API


|Type |Function Module |Previous |Current |Notes |
|---|---|---|---|---|
|Modified |Engine Management |`- (int)feedback:(NSArray<ByteRTCProblemOption *> * _Nullable)types desc:(NSString* _Nullable)desc;` |`- (int)feedback:(ByteRTCProblemFeedbackOption)types info:(ByteRTCProblemFeedbackInfo* _Nullable)info;` |The data types of the parameters are changed. |
|Modified |Advanced Features |`- (int)startAudioRecording:(ByteRTCAudioRecordingConfig* _Nonnull) recordingConfig;` |`- (int)startAudioRecording:(ByteRTCAudioRecordingConfig* _Nonnull) recordingConfig;` |In previous versions, this API only supports calling after joining a room. Since this version, this API can be called before and after entering the room. If you call it before joining the room, and the recording task will not stop automatically after checking out; if you call it after entering the room, and the recording task will stop automatically after checking out. |
|Replaced |Advanced Features |`-(int)updatePosition:(Position* _Nonnull) pos`<br><br>`-(int)updateSelfOrientation:(HumanOrientation* _Nonnull) orientation` |`-(int)updateSelfPosition:(ByteRTCPositionInfo* _Nonnull)positionInfo;` |The APIs used in the the spatial audio feature are replaced and the new API allows local users to set their own position and orientation in the rectangular coordinate system. |
|Replaced |Advanced Features |`-(int)updateListenerPosition:(Position* _Nonnull) pos`<br><br>`-(int)updateListenerOrientation:(HumanOrientation* _Nonnull)orientation` |`-(int)updateRemotePosition:(NSString * _Nonnull)uid positionInfo:(ByteRTCPositionInfo* _Nonnull)positionInfo;` |The APIs used in the the spatial audio feature are replaced and the new API allows local users to set the position and orientation of remote users in the rectangular coordinate system. |
|Replaced |Push to CDN |`- (int)startLiveTranscoding:(NSString * _Nonnull)taskID transcoding:(ByteRTCLiveTranscoding *_Nullable)transcoding observer:(id<LiveTranscodingDelegate> _Nullable)observer;` |`- (int)startPushMixedStreamToCDN:(NSString * _Nonnull)taskID mixedConfig:(ByteRTCMixedStreamConfig *_Nullable)config observer:(id<ByteRTCMixedStreamObserver> _Nullable)observer;` |The APIs used in the function of pushing mixed streams to CDN are renamed with the behavior logic remaining unchanged. See Keytype change for the correspondence between the old and new versions of the class name. |
|Replaced |Push to CDN |`- (int)stopLiveTranscoding:(NSString *_Nonnull)taskID;` |`- (int)stopPushStreamToCDN:(NSString *_Nonnull)taskID NS_SWIFT_NAME(stopPushStreamToCDN(_:));` |The APIs used in the function of pushing mixed streams to CDN are renamed with the behavior logic remaining unchanged. See Keytype change for the correspondence between the old and new versions of the class name. |
|Replaced |Push to CDN |`- (int)updateLiveTranscoding:(NSString *_Nonnull)taskID transcoding:(ByteRTCLiveTranscoding *_Nonnull)transcoding;` |`- (int)updatePushMixedStreamToCDN:(NSString *_Nonnull)taskID mixedConfig:(ByteRTCMixedStreamConfig *_Nonnull)config;` |The APIs used in the function of pushing mixed streams to CDN are renamed with the behavior logic remaining unchanged. See Keytype change for the correspondence between the old and new versions of the class name. |


<span id="keytype"></span>
## Keytype


|Change |Class |Previous |Current |Notes |
|---|---|---|---|---|
|Replaced |Top level class used in APIs for pushing mixed streams to CDN |`ByteRTCLiveTranscoding` |`ByteRTCMixedStreamConfig` |Some variable names/API names in the class are also changed. For specific changes, click the new class. |
|Replaced |Observer used in APIs for pushing mixed streams to CDN |`LiveTranscodingDelegate` |`ByteRTCMixedStreamObserver` | |
|Replaced |The nested classes used in APIs for pushing mixed streams to CDN |`ByteRTCTranscodingVideoConfig` |`ByteRTCMixedStreamVideoConfig` |Some variable names/API names in the class are also changed. For specific changes, click the new class. |
|Replaced |The nested classes used in APIs for pushing mixed streams to CDN |`ByteRTCTranscodingAudioConfig` |`ByteRTCMixedStreamAudioConfig` |Some variable names/API names in the class are also changed. For specific changes, click the new class. |
|Replaced |The nested classes used in APIs for pushing mixed streams to CDN |`ByteRTCTranscodingSpatialConfig` |`ByteRTCMixedStreamSpatialAudioConfig` |Some variable names/API names in the class are also changed. For specific changes, click the new class. |
|Replaced |The nested classes used in APIs for pushing mixed streams to CDN |`ByteRTCTranscodingClientMixParam` |`ByteRTCMixedStreamClientMixConfig` |Some variable names/API names in the class are also changed. For specific changes, click the new class. |
|Replaced |The nested classes used in APIs for pushing mixed streams to CDN |`ByteRTCVideoCompositingRegion` |`ByteRTCMixedStreamLayoutRegionConfig` |Some variable names/API names in the class are also changed. For specific changes, click the new class. |
|Replaced |The nested classes used in APIs for pushing mixed streams to CDN |`ByteRTCVideoCompositingLayout` |`ByteRTCMixedStreamLayoutConfig` |Some variable names/API names in the class are also changed. For specific changes, click the new class. |
|Replaced |Enum classes used in APIs for pushing mixed streams to CDN |`ByteRTCClientMixVideoFormat` |`ByteRTCMixedStreamClientMixVideoFormat` |The names of values in each enumeration class are also changed. For specific changes, click the new class. |
|Replaced |Enum classes used in APIs for pushing mixed streams to CDN |`ByteRTCTranscoderContentControlType` |`ByteRTCMixedStreamMediaType` |The names of values in each enumeration class are also changed. For specific changes, click the new class. |
|Replaced |Enum classes used in APIs for pushing mixed streams to CDN |`ByteRTCRenderMode` |`ByteRTCMixedStreamRenderMode` |The names of values in each enumeration class are also changed. For specific changes, click the new class. |
|Replaced |Enum classes used in APIs for pushing mixed streams to CDN |`ByteRTCTranscoderLayoutRegionType` |`ByteRTCMixedStreamLayoutRegionType` |The names of values in each enumeration class are also changed. For specific changes, click the new class. |
|Replaced |Enum classes used in APIs for pushing mixed streams to CDN |`ByteRTCAACProfile` |`ByteRTCMixedStreamAudioProfile` |The names of values in each enumeration class are also changed. For specific changes, click the new class. |
|Replaced |Enum classes used in APIs for pushing mixed streams to CDN |`ByteRTCTranscodingVideoCodec` |`ByteRTCMixedStreamVideoCodecType` |The names of values in each enumeration class are also changed. For specific changes, click the new class. |
|Replaced |Enum classes used in APIs for pushing mixed streams to CDN |`ByteRTCTranscodingAudioCodec` |`ByteRTCMixedStreamAudioCodecType` |The names of values in each enumeration class are also changed. For specific changes, click the new class. |
|Replaced |Enum classes used in APIs for pushing mixed streams to CDN |`ByteRTCStreamMixingType` |`ByteRTCMixedStreamType` |The names of values in each enumeration class are also changed. For specific changes, click the new class. |


<span id="error-code"></span>
## Error Code


1. Add new error codes: `kErrorCodeJoinRoomRoomForbidden=-1025` and `kErrorCodeJoinRoomUserForbidden =-1026`. The client SDK receives the error code when the user is banned in a specific room by the RTC server and fails to join the room or is removed from the room.

2. `ByteRTCErrorCodeOverScreenPublishLimit=-1081` is deprecated and replaced by `ByteRTCErrorCodeOverStreamPublishLimit=-1080`.


<span id="_3-50"></span>
# 3.50

<span id="sdk-integration"></span>
## SDK Integration

A new plugin named `RTCFFmpeg.xcframework` is added in this version, which can be used for iOS software decoding (fallback when hardware decoding fails), local video recording, and image decoding. After integrating this plugin, the app's size will increase by 1.3MB for the arm64 architecture. To ensure the proper functioning of the RTC SDK, it is necessary to integrate this plugin into your project.

<span id="header-file"></span>
## Header File

The original `ByteRTCCommonDefines.h` header file has been split into `ByteRTCMediaDefines.h` and `ByteRTCRtsDefines.h`, both of which you should import into your project if needed.

<span id="api"></span>
## API


|Type |Function Module |Previous |Current |Notes |
|---|---|---|---|---|
|Return value change |Room management |`joinRoom:userInfo:roomConfig:` returns:<br><br><br>* `-1`: Invalid parameters.<br><br>* `-2`: Already in a room. |`joinRoom:userInfo:roomConfig:` returns:<br><br><br>* `-1`: Failure.<br><br>* `-2`: Invalid parameters.<br><br>* `-4`: Already in a room. |`0` continues to represent success. |
| |Network management |`stopEchoTest` returns `-1` denoting failure due to no echo test is in progress. |`stopEchoTest` returns `-3` denoting failure due to no echo test is in progress. | |
| |Engine management |`setBusinessId:` returns:<br><br><br>* `< 0`: Failure. Refer to `BusinessCheckCode`。<br><br>* `-6001`: Already in a room.<br><br>* `-6002`: Invalid parameters. |`setBusinessId:` returns:<br><br><br>* `< 0`: Failure. Refer to `ReturnStatus`<br><br>* `-2`: Invalid parameters. | |
|Modified |Message |`(int64_t)sendUserMessage:(NSString *_Nonnull)userId message:(NSString *_Nonnull)message config:(ByteRTCMessageConfig)config;` |`(NSInteger)sendUserMessage:(NSString *_Nonnull)userId message:(NSString *_Nonnull)message config:(ByteRTCMessageConfig)config;` |The data type of the parameter changed from `int64_t` to `NSInteger`. |
|Modified |Message |`(int64_t)sendUserBinaryMessage:(NSString * _Nonnull)uid message:(NSData * _Nonnull)message config:(ByteRTCMessageConfig)config;` |`(NSInteger)sendUserBinaryMessage:(NSString * _Nonnull)uid message:(NSData * _Nonnull)message config:(ByteRTCMessageConfig)config;` |The data type of the parameter changed from `int64_t` to `NSInteger`. |
|Modified |Message |`(int64_t)sendRoomMessage:(NSString *_Nonnull)message NS_SWIFT_NAME(sendRoomMessage(_:));` |`(NSInteger)sendRoomMessage:(NSString *_Nonnull)message NS_SWIFT_NAME(sendRoomMessage(_:));` |The data type of the parameter changed from `int64_t` to `NSInteger`. |
|Modified |Message |`(int64_t)sendRoomBinaryMessage:(NSData * _Nonnull)message NS_SWIFT_NAME(sendRoomBinaryMessage(_:));` |`(NSInteger)sendRoomBinaryMessage:(NSData * _Nonnull)message NS_SWIFT_NAME(sendRoomBinaryMessage(_:));` |The data type of the parameter changed from `int64_t` to `NSInteger`. |
|Modified |Message |`(int64_t)sendUserMessageOutsideRoom:(NSString * _Nonnull)userId message:(NSString * _Nonnull)messageStr config:(ByteRTCMessageConfig)config;` |`(NSInteger)sendUserMessageOutsideRoom:(NSString * _Nonnull)userId message:(NSString * _Nonnull)messageStr config:(ByteRTCMessageConfig)config;` |The data type of the parameter changed from `int64_t` to `NSInteger`. |
|Modified |Message |`(int64_t)sendUserBinaryMessageOutsideRoom:(NSString * _Nonnull)userId message:(NSData * _Nonnull)messageStr config:(ByteRTCMessageConfig)config;` |`(NSInteger)sendUserBinaryMessageOutsideRoom:(NSString * _Nonnull)userId message:(NSData * _Nonnull)messageStr config:(ByteRTCMessageConfig)config;` |The data type of the parameter changed from `int64_t` to `NSInteger`. |
|Modified |Message |`(int64_t)sendServerMessage:(NSString * _Nonnull)messageStr;` |`(NSInteger)sendServerMessage:(NSString * _Nonnull)messageStr;` |The data type of the parameter changed from `int64_t` to `NSInteger`. |
|Modified |Message |`(int64_t)sendServerBinaryMessage:(NSData * _Nonnull)messageStr;` |`(NSInteger)sendServerBinaryMessage:(NSData * _Nonnull)messageStr;` |The data type of the parameter changed from `int64_t` to `NSInteger`. |
|Modified |Screen sharing |`(int)setScreenVideoEncoderConfig:(ByteRTCVideoEncoderConfig * _Nullable) screen_solution;` |`(int)setScreenVideoEncoderConfig:(ByteRTCScreenVideoEncoderConfig * _Nullable) screen_solution;` |The data type of the parameter changed to `ByteRTCScreenVideoEncoderConfig`. |
|Modified |Screen sharing |* `setVideoSourceType:WithStreamIndex:` The screen video source defaults to external.<br><br>* `setScreenAudioSourceType:` When the current setting is an internal source, and the capture is enabled, calling the API to switch to external source does not affect the internal capture.<br><br>* `startScreenCapture:bundleId:` When the current setting is an external source, calling the API enables the internal source, and starts capturing.<br><br>* `stopScreenCapture` When the current setting is an external source, calling the API disables the external capturing. |* `setVideoSourceType:WithStreamIndex:` The screen video source defaults to internal.<br><br>* `setScreenAudioSourceType:` When the current setting is an internal source, and the capture is enabled, calling the API to switch to external source stops the internal capture as well.<br><br>* `startScreenCapture:bundleId:` When the current setting is an external source, calling the API to enable the internal source will fail and receive `rtcEngine:onVideoDeviceWarning:deviceType:deviceWarning:` or `rtcEngine:onAudioDeviceWarning:deviceType:deviceWarning:`.<br><br>* `stopScreenCapture` When the current setting is an external source, calling the API to enable the internal source will fail and receive `rtcEngine:onVideoDeviceWarning:deviceType:deviceWarning:` or `rtcEngine:onAudioDeviceWarning:deviceType:deviceWarning:`. |Align the behaviors of the screen\-sharing APIs with the video stream APIs. |
|Replaced |Video Processing |* `(int)checkVideoEffectLicense:(NSString * _Nonnull)licenseFile;`<br><br>* `(void)setVideoEffectAlgoModelPath:(NSString * _Nonnull)modelPath;` |`(int) initCVResource:(NSString* _Nonnull)license_file withAlgoModelDir: (NSString* _Nonnull)algo_model_dir;` |* Moved from `ByteRTCVideo` class to `ByteRTCVideoEffect` class.<br><br>* Unified the return values. |
|Replaced |Video Processing |`(int)enableVideoEffect:(BOOL)enabled;` |* `(int) enableVideoEffect;`<br><br>* `(int) disableVideoEffect;` |* Moved from `ByteRTCVideo` class to `ByteRTCVideoEffect` class.<br><br>* Unified the return values. |
|Replaced |Video Processing |`(int) setVideoEffectNodes:(NSArray <NSString *> *_Nonnull)effectNodePaths;` |`(int) setEffectNodes:(NSArray<NSString*>*_Nonnull)effect_nodes;` |* Moved from `ByteRTCVideo` class to `ByteRTCVideoEffect` class.<br><br>* Unified the return values. |
|Replaced |Video Processing |`(int) updateVideoEffectNode:(NSString * _Nonnull)nodePath nodeKey:(NSString * _Nonnull)nodeKey nodeValue:(float) nodeValue;` |`(int) updateEffectNode:(NSString* _Nonnull)node key:(NSString* _Nonnull)key value:(float) value;` |* Moved from `ByteRTCVideo` class to `ByteRTCVideoEffect` class.<br><br>* Unified the return values. |
|Replaced |Video Processing |`(int) setBackgroundSticker:(NSString* _Nullable)modelPath source:(ByteRTCVirtualBackgroundSource* _Nonnull)source;` |* `(int) enableVirtualBackground:(NSString* _Nonnull)bg_sticker_path withSource:(ByteRTCVirtualBackgroundSource* _Nonnull)source;`<br><br>* `(int) disableVirtualBackground;` |* Moved from `ByteRTCVideo` class to `ByteRTCVideoEffect` class.<br><br>* Unified the return values. |
|Replaced |Video Processing |`(int) setVideoEffectColorFilter:(NSString * _Nonnull)resPath;` |`(int) setColorFilter:(NSString* _Nonnull)filter_res;` |* Moved from `ByteRTCVideo` class to `ByteRTCVideoEffect` class.<br><br>* Unified the return values. |
|Replaced |Video Processing |`(int) setVideoEffectColorFilterIntensity:(float) intensity;` |`(int) setColorFilterIntensity:(float) intensity;` |* Moved from `ByteRTCVideo` class to `ByteRTCVideoEffect` class.<br><br>* Unified the return values. |
|Replaced |Video Management |`(int) registerFaceDetectionObserver:(_Nullable id<ByteRTCFaceDetectionObserver>)faceDetectionObserver withInterval:(NSInteger)interval;` |* `(int) enableFaceDetection:(_Nullable id<ByteRTCFaceDetectionObserver>) observer withInterval:(NSUInteger)interval withModelPath:(NSString* _Nonnull)path;`<br><br>* `(int) disableFaceDetection;` |* Moved from `ByteRTCVideo` class to `ByteRTCVideoEffect` class.<br><br>* Decoupled face detection and video effects to improve usability.<br><br>* Unified the return values. |
|Modified |Message |`(int)sendSEIMessage:(ByteRTCStreamIndex)streamIndex andMessage:(NSData* _Nonnull)message andRepeatCount:(int)repeatCount;` |`(int)sendSEIMessage:(ByteRTCStreamIndex)streamIndex andMessage:(NSData* _Nonnull)message andRepeatCount:(int)repeatCount andCountPerFrame:(ByteRTCSEICountPerFrame) mode;` |Added Multi\-SEI mode. When you send multiple SEI messages in 1 frame, they will be sent together in the next frame. |
|Modified |Multiple modules |`subscribeStream`<br><br>`subscribeScreen`<br><br>`setVoiceChangerType`<br><br>`setVoiceReverbType`<br><br>`login` |`subscribeStream`<br><br>`subscribeScreen`<br><br>`setVoiceChangerType`<br><br>`setVoiceReverbType`<br><br>`login` |The return type changed from `void` to `int`. See `ByteRTCReturnStatus` for the description of the return value. |
|Modified |Multiple modules |`pushExternalEncodedVideoFrame` |`pushExternalEncodedVideoFrame` |The return type changed from `BOOL` to `int`. See `ByteRTCReturnStatus` for the description of the return value. |
|Modified |Multiple modules |`setUserVisibility`<br><br>`setMultiDeviceAVSync`<br><br>`registerAudioProcessor` |`setUserVisibility`<br><br>`setMultiDeviceAVSync`<br><br>`registerAudioProcessor` |The return type changed from `BOOL` to `void`. |
|Modified |Multiple modules |`leaveRoom`<br><br>`publishStream`<br><br>`unpublishStream`<br><br>`publishScreen`<br><br>`unpublishScreen`<br><br>`enableSimulcastMode`<br><br>`updateLocalVideoCanvas`<br><br>`setLocalVideoMirrorType`<br><br>`setVideoRotationMode`<br><br>`switchCamera`<br><br>`setAudioRoute`<br><br>`startLiveTranscoding`<br><br>`stopLiveTranscoding`<br><br>`setPublishFallbackOption`<br><br>`setSubscribeFallbackOption` |`leaveRoom`<br><br>`publishStream`<br><br>`unpublishStream`<br><br>`publishScreen`<br><br>`unpublishScreen`<br><br>`enableSimulcastMode`<br><br>`updateLocalVideoCanvas`<br><br>`setLocalVideoMirrorType`<br><br>`setVideoRotationMode`<br><br>`switchCamera`<br><br>`setAudioRoute`<br><br>`startLiveTranscoding`<br><br>`stopLiveTranscoding`<br><br>`setPublishFallbackOption`<br><br>`setSubscribeFallbackOption` |The return type changed from `int` to `void`. |
|Modified |Video Management |`(int)setRemoteVideoCanvas:(NSString * _Nonnull)uid withIndex:(ByteRTCStreamIndex)streamIndex withCanvas:(ByteRTCVideoCanvas * _Nullable)canvas;` |`(void)setRemoteVideoCanvas:(ByteRTCRemoteStreamKey * _Nonnull)key withCanvas:(ByteRTCVideoCanvas * _Nullable)canvas;` |* The return type changes form `int` to `void`.<br><br>* Set `uid` and `streamIndex` in `key`. |
|Modified |Video Management |`(int)updateRemoteStreamVideoCanvas:(NSString * _Nonnull)roomid withUserId:(NSString * _Nonnull)uid withIndex:(ByteRTCStreamIndex)streamIndex withRenderMode:(ByteRTCRenderMode)renderMode withBackgroundColor:(NSUInteger)backgroundColor;` |`(void)updateRemoteStreamVideoCanvas:(ByteRTCRemoteStreamKey * _Nonnull)key withRenderMode:(ByteRTCRenderMode)renderMode withBackgroundColor:(NSUInteger)backgroundColor;` |* The return type changes form `int` to `void`.<br><br>* Set `roomid`, `uid` and `streamIndex` in `key`. |
|Modified |Room Management |`setRtcRoomDelegate` |`setRTCRoomDelegate` | |
|Modified |Room Management |`joinRoomByToken` |`joinRoom` | |
|Modified |Room Management |`renewToken` |`updateToken` | |
|Modified |Engine Management |`getSdkVersion` |`getSDKVersion` | |
|Modified |Security and Encryption |`setEncryptType` |`setEncryptInfo` | |
|Modified |Video Processing |`SetVideoWatermark` |`setVideoWatermark` |The name changed from UpperCamelCase to LowerCamelCase. |
|Modified |Video Processing |`ClearVideoWatermark` |`clearVideoWatermark` |The name changed from UpperCamelCase to LowerCamelCase. |
|Modified |Screen Sharing |`SetScreenVideoEncoderConfig` |`setScreenVideoEncoderConfig` |The name changed from UpperCamelCase to LowerCamelCase. |
|Modified |Video Management |`SetVideoEncoderConfig` |`setVideoEncoderConfig` |The name changed from UpperCamelCase to LowerCamelCase. |
|Modified |Video Management |`SetMaxVideoEncoderConfig` |`setMaxVideoEncoderConfig` |The name changed from UpperCamelCase to LowerCamelCase. |
|Modified |Audio & Video Transport |`(void)unSubscribeStream:(NSString *_Nonnull)userId mediaStreamType:(ByteRTCMediaStreamType)mediaStreamType;` |`(int)unsubscribeStream:(NSString *_Nonnull)userId mediaStreamType:(ByteRTCMediaStreamType)mediaStreamType;` |* The return type changed from `void` to `int`.<br><br>* Fixed incorrect letter case in the name. |
|Modified |Audio & Video Transport |`(void)unSubscribeScreen:(NSString *_Nonnull)userId mediaStreamType:(ByteRTCMediaStreamType)mediaStreamType;` |`(int)unsubscribeScreen:(NSString *_Nonnull)userId mediaStreamType:(ByteRTCMediaStreamType)mediaStreamType;` |* The return type changed from `void` to `int`.<br><br>* Fixed incorrect letter case in the name. |
|Modified |Screen Sharing |`(void)pushScreenCaptureFrame:(CVPixelBufferRef _Nonnull )frame time:(CMTime)pts rotation:(int)rotation;` |`(int)pushScreenVideoFrame:(CVPixelBufferRef _Nonnull )frame time:(CMTime)pts rotation:(int)rotation;` |* The return type changes from `void` to `int`.<br><br>* The name changes from `pushScreenCaptureFrame` to `pushScreenVideoFrame`. |
|Modified |Custom Stream Processing |`(BOOL)pushExternalByteVideoFrame:(ByteRTCVideoFrame * _Nonnull)frame;` |`(int)pushExternalVideoFrame:(ByteRTCVideoFrame * _Nonnull)frame;` |* The return type changes from `BOOL` to `int`.<br><br>* The name changes from `pushExternalByteVideoFrame` to `pushExternalVideoFrame`. |
|Modified |Custom Stream Processing |`(BOOL)setAudioFrameObserver:(_Nullable id<ByteRTCAudioFrameObserver>) audioFrameObserver;` |`(void)registerAudioFrameObserver:(_Nullable id<ByteRTCAudioFrameObserver>) audioFrameObserver;` |* The return type changes from `BOOL` to `void`.<br><br>* The name changes from `setAudioFrameObserver` to `registerAudioFrameObserver`. |
|Replaced |Custom Stream Processing |* `(BOOL)pushExternalVideoFrame:(CVPixelBufferRef _Nonnull )frame time:(CMTime)pts;`<br><br>* `(BOOL)pushExternalVideoFrame:(CVPixelBufferRef _Nonnull )frame time:(CMTime)pts rotation:(ByteRTCVideoRotation)rotation;`<br><br>* `(BOOL)pushExternalVideoFrame:(CVPixelBufferRef _Nonnull )frame time:(CMTime)pts rotation:(ByteRTCVideoRotation)rotation extendedData:(NSData* _Nullable)extendedData supplementaryInfo:(NSData* _Nullable)supplementoryInfo;` |`(int)pushExternalVideoFrame:(ByteRTCVideoFrame * _Nonnull)frame;` | |


<span id="callback"></span>
## Callback


|Type |Function Module |Previous |Current |Notes |
|---|---|---|---|---|
|Modified |Message |`(void)rtcRoom:( ByteRTCRoom *_Nonnull)rtcRoom onUserMessageSendResult:(int64_t)msgid error:(ByteRTCUserMessageSendResult)error;` |`(void)rtcRoom:( ByteRTCRoom *_Nonnull)rtcRoom onUserMessageSendResult:(NSInteger)msgid error:(ByteRTCUserMessageSendResult)error;` |The type of the parameter `msgid` changes from `int64_t` to `NSInteger`. |
|Modified |Message |`(void)rtcRoom:( ByteRTCRoom *_Nonnull)rtcRoom onRoomMessageSendResult:(int64_t)msgid error:(ByteRTCRoomMessageSendResult)error;` |`(void)rtcRoom:( ByteRTCRoom *_Nonnull)rtcRoom onRoomMessageSendResult:(NSInteger)msgid error:(ByteRTCRoomMessageSendResult)error;` |The type of the parameter `msgid` changes from `int64_t` to `NSInteger`. |
|Modified |Message |`(void)rtcEngine:(ByteRTCVideo * _Nonnull)engine onUserMessageSendResultOutsideRoom:(int64_t)msgid error:(ByteRTCUserMessageSendResult)error;` |`(void)rtcEngine:(ByteRTCVideo * _Nonnull)engine onUserMessageSendResultOutsideRoom:(NSInteger)msgid error:(ByteRTCUserMessageSendResult)error;` |The type of the parameter `msgid` changes from `int64_t` to `NSInteger`. |
|Modified |Push to CDN |`(void)onMixingAudioFrame:(ByteRTCAudioFrame *_Nonnull)audioFrame taskId:(NSString *_Nonnull)taskId;` |`onMixingAudioFrame:(ByteRTCAudioFrame *_Nonnull)audioFrame timestamp:(int64_t)timeStamp taskId:(NSString *_Nonnull)taskId;` |Added a new parameter: `timeStamp` |
|Modified |Room Management |`onLeaveRoomWithStats` |`onLeaveRoom` | |
|Modified |Audio & Video Transport |`connectionChangedToState` |`onConnectionStateChanged` | |
|Modified |Audio & Video Transport |`networkTypeChangedToType` |`onNetworkTypeChanged` | |
|Modified |Audio & Video Transport |`reportSysStats` |`onSysStats` | |
|Modified |Network Management |`onPerformanceAlarmsWithMode` |`onPerformanceAlarms` | |
|Modified |Network Management |`OnSimulcastSubscribeFallback` |`onSimulcastSubscribeFallback` | |
|Modified |Security and Encryption |`ByteRTCEncryptRawData` |`onEncryptData` | |
|Modified |Security and Encryption |`ByteRTCDecryptRawData` |`onDecryptData` | |
|Modified |Video Management |`onFaceDetectionResult` |`onFaceDetectResult` | |
|Replaced |Range Audio |When you use range audio with manual audio subscription, you must set the attenuation index based on the return value of `ByteRTCRangeAudioObserver`. |Set the attenuation model by calling `setAttenuationModel:coefficient:`. | |
|Deprecated |Audio & Video Transport |`(void)rtcEngine:(ByteRTCVideo * _Nonnull)engine remoteVideoStateChangedOfUid:(NSString * _Nonnull)uid state:(ByteRTCRemoteVideoState)state;` |/ | |
|Modified |Custom Stream Processing |`onProcessRecordAudioFrame:` |`onProcessRecordAudioFrame:` |In earlier versions, any modification to the audio frames returned by the callback affects the audio data sent to the remote user and the audio data sent to the local ear monitoring device.<br><br>In this version or higher, the modification affects the audio data sent to the remote user only. If you need to modify the audio data sent to the local ear monitoring device, see `onProcessEarMonitorAudioFrame`. |


<span id="keytype"></span>
## Keytype


|Type |Keytype |Notes |
|---|---|---|
|New |`ByteRTCUserMessageSendResult` |Added `ByteRTCUserMessageSendResultExceedQPS = 5` |
|New |`ByteRTCRoomMessageSendResult` |Added `ByteRTCRoomMessageSendResultExceedQPS = 5` |
|New |`ByteRTCAudioFrameMethod` |Added `ByteRTCAudioFrameProcessorEarMonitor = 3` |
|New |`ByteRTCFaceDetectionResult` |Added member `frameTimestamp` |
|Modified |`ByteRTCVideoCanvas` |Deleted `roomId` and `uid`. |
|Modified |`ByteRTCVideoFrame` |* The type of member `extendedData` changes from `ByteRTCFrameExtendedData` to `NSData`<br><br>* Added member `supplementaryInfo` |
|New |`ByteRTCLiveTranscoding` |Added member `ByteRTCTranscodingClientMixParam` |
|Modified |`position` |The data type of `x`, `y`, `z` of `position` used in spatial audio is changed from `int` to `float`. |
|Modified |`ByteRTCRoomProfile` |The default value of `ByteRTCRoomProfileCommunication = 0` is changed from `ByteRTCRoomProfileChatRoom = 6` to `ByteRTCRoomProfileMeeting = 16`. |
|Modified |`ByteRTCVideoFrame` |The following data types are removed:<br><br>`cropLeft`<br><br>`cropTop`<br><br>`cropRight`<br><br>`cropBottom` |
|Modified |`ByteRTCVideoCompositingRegion` |The range of parameter `width` and `height` extended from `(0.0, 1.0]` to `[0.0, 1.0]`. |
|Modified |`ByteRTCAudioRoute` |`ByteRTCAudioRouteUnknown` is replaced by `ByteRTCAudioRouteDefault` |
|Modified |`ByteRTCAudioScenarioType` |The mapping from audio routing and publishing and subscribing status to audio type has changed, see the latest documentation. |


<span id="error-code"></span>
## Error Code


|Type |Error Code |Notes |
|---|---|---|
|New |`ByteRTCErrorCode` |Added `ByteRTCUserIDDifferent = -1014` |


<span id="_3-45-6"></span>
# 3.45.6

<span id="api"></span>
## API


|Type |API |Notes |
|---|---|---|
|New member in API parameter |`enableAudioPropertiesReport:` |Adds \- `ByteRTCAudioPropertiesMode` member in "ByteRTCAudioPropertiesConfig". |


<span id="keytype"></span>
## Keytype


|Type |API |Notes |
|---|---|---|
|Member change |`ByteRTCAudioScenarioType` |Adds "ByteRTCAudioScenarioHighqualityChat" member. |
|Member change |`ByteRTCAudioFrameMethod` |Adds "ByteRTCAudioFrameProcessorEarMonitor = 3" member for acquiring SDK\-level in\-ear monitoring audio. |
|Member change |`ByteRTCAudioFrameMethod` |Adds "ByteRTCAudioFrameProcessorScreen = 4" member. |
