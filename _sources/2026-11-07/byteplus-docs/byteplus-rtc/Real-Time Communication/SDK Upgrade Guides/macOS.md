---
title: "macOS"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70021"
---

<span id="1a0301e4"></span>
# 3.60.105

<span id="abf66ab8"></span>
## API Changes


|V 3.60.104 |V 3.60.105 |Change Description |
|---|---|---|
|`ByteRTCRoom.setRoomProfile:(ByteRTCRoomProfile)profile` |`ByteRTCRoom.setLiveMode:(ByteRTCRoomLiveMode)mode` |Renamed from `setRoomProfile:` to `setLiveMode:`. The parameter type changed from `ByteRTCRoomProfile` to `ByteRTCRoomLiveMode`. |
|`sendLivePushSEIMessage`: prerequisite was `ByteRTCRoomProfileLivePush` set via `joinRoom:userInfo:roomConfig:` |`sendLivePushSEIMessage`: prerequisite is `ByteRTCRoomLiveModeSoloHost` set via `setLiveMode:` |The prerequisite for calling `sendLivePushSEIMessage` changed from setting room profile to `ByteRTCRoomProfileLivePush` during `joinRoom:userInfo:roomConfig:` to calling `setLiveMode:` with `ByteRTCRoomLiveModeSoloHost`. |


<span id="f7cf9fdf"></span>
## Type Changes


|Type Name |Change Description |
|---|---|
|`ByteRTCRoomLiveMode` |New enum type. Defines the live streaming mode:<br><br><br>* `ByteRTCRoomLiveModeCoHost` (value 1): Co\-hosted live streaming mode for multi\-person or interactive live scenarios.<br><br>* `ByteRTCRoomLiveModeSoloHost` (value 2): Single\-host live streaming mode. |
|`ByteRTCRoomProfile` |Removed enum values: `ByteRTCRoomProfileLinkMic` and `ByteRTCRoomProfileLivePush`. Use the new `ByteRTCRoomLiveMode` enum with `setLiveMode:` instead. |
|`ByteRTCRoomConfig` |Added `ByteRTCRoomLiveMode liveMode` property. Default value: `ByteRTCRoomLiveModeCoHost`. Specifies the live mode when joining a room. Only effective when `profile` is `ByteRTCRoomProfileLive`. Can be changed after joining via `setLiveMode:`. |
|`ByteRTCVideoEncoderConfig` |Added `NSInteger keyFrameIntervalMS` property. Default value: `0` (encoder determines automatically). Sets the key frame interval in milliseconds. |


<span id="c1a17b1c"></span>
## New Interfaces


|Class / Module |Interface |Description |
|---|---|---|
|`ByteRTCRoom` |`setLiveMode:` |Sets the live streaming mode (co\-hosted / single\-host). Call after joining a room. |
|`ByteRTCEngine` |`sendLivePushSEIMessage:count:isKeyFrameOnly:allowOverwrite:` |Sends SEI data in Key\-Value (JSON) format through video frames. Requires `ByteRTCRoomLiveModeSoloHost` mode. |


<span id="34ab3d87"></span>
## Deleted or Deprecated Interfaces


|Interface |Replacement |Description |
|---|---|---|
|`ByteRTCRoom.setRoomProfile:` |`ByteRTCRoom.setLiveMode:` |Replaced by `setLiveMode:` with the new `ByteRTCRoomLiveMode` enum. |


<span id="bbd471b0"></span>
# 3.60.104

<span id="ab8cde8a"></span>
## API Changes


|Change Details |Interface |Notes |
|---|---|---|
|Added |`setRoomProfile:` |Sets room profile before or after joining a room. |
|Added |`sendLivePushSEIMessage:count:isKeyFrameOnly:allowOverwrite:` |Sends SEI (Supplemental Enhancement Information) data in Key\-Value format through video frames. |


<span id="d8cdf78f"></span>
## Type Changes


|Change Details |Changed Data Type |Notes |
|---|---|---|
|New Enum Value Added |ByteRTCRoomProfile |New enum values:<br><br><br>* `ByteRTCRoomProfileLinkMic`: Link mic mode, focuses on high quality, same bitrate as LIVE.<br><br>* `ByteRTCRoomProfileLivePush`: Live push mode for broadcasting scenarios. |
|New Member Variable Added |ByteRTCVideoEncoderConfig |Added `keyFrameIntervalMS` field: Sets key frame interval in milliseconds, default: 0. |
|New Member Variable Added |ByteRTCVideoPreprocessorConfig |Added `actionDomain` field: Controls the effective range of your custom video preprocessor. |
|New Enum Added |ByteRTCProcessorActionDomain |Controls where the custom video preprocessor effects are applied:<br><br><br>* `ByteRTCProcessorActionDomainPreviewAndEncode`：Effects apply to both preview and transmission.<br><br>* `ByteRTCProcessorActionDomainPreview`：Effects apply only to local preview.<br><br>* `ByteRTCProcessorActionDomainEncode`：Effects apply only to outgoing stream. |


<span id="_3-60"></span>
# 3.60.103

<span id="api-changes"></span>
## API Changes

<span id="header-files-and-base-class-names"></span>
### Header Files and Base Class Names


|Change Type |V3.58 |V3.60 |
|---|---|---|
|Header file name change |../ByteRTCVideo.h |../ByteRTCEngine.h |
|Base class name change (all modules) |ByteRTCVideo |ByteRTCEngine |
|Base class name change (all modules) |ByteRTCVideoDelegate |ByteRTCEngineDelegate |
|Added header file |None |../ByteRTCRTSRoom.h<br><br>../ByteRTCGameRoom.h |


<span id="a2317f55"></span>
### Engine Management


|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|Create engine object |createRTCVideo:(NSString \* _Nonnull)appId delegate:(id_Nullable)delegate parameters:(NSDictionary \* _Nonnull)parameters; |createRTCEngine:(ByteRTCEngineConfig \* _Nonnull) config delegate:(id_Nullable)delegate |* **Name change**: `createRTCVideo` changed to `createRTCEngine`<br><br>* **Parameter change**:<br><br>   * `parameters` and `appId`: Moved to the new `ByteRTCEngineConfig` class, and `appId` renamed to `appID`<br><br>   * ByteRTCVideoDelegate: Renamed to ByteRTCEngineDelegate |
|Destroy engine |destroyRTCVideo |destroyRTCEngine |**Method name change** |
|Engine event callback |ByteRTCVideoDelegate |ByteRTCEngineDelegate |**Protocol name change** |


<span id="ffb66251"></span>
### Room Management


|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|Join room |joinRoom:(NSString \*_Nullable)token userInfo:(ByteRTCUserInfo \*_Nonnull)userInfo roomConfig:(ByteRTCRoomConfig \*Nonnull)roomConfig NS_SWIFT_NAME(joinRoom(:userInfo:roomConfig:)); |joinRoom:(NSString \*_Nullable)token userInfo:(ByteRTCUserInfo \*_Nonnull)userInfo userVisibility:(BOOL)userVisibility roomConfig:(ByteRTCRoomConfig \*Nonnull)roomConfig NS_SWIFT_NAME(joinRoom(:userInfo:userVisibility:roomConfig:)); |1. **Parameter change**:<br><br>   1. **New parameter userVisibility**: Specifies user visibility.<br><br>      It is recommended to set user visibility to false when joining the room, and then set it to true through setUserVisibility: when users need to send audio and video streams. Since the capacity of invisible users in a single room is much higher than that of visible users, enabling user visibility on demand can maximize the use of RTC call room resources and avoid the situation where subsequent users fail to join the room after the visible users in the RTC room reach the limit.<br><br>   2. Parameters in ByteRTCRoomConfig: `isAutoPublish` is split into video isAutoPublishVideo and audio isAutoPublishAudio.<br><br>   3. The enumeration of parameter `ByteRTCRoomProfile` (room mode) in ByteRTCRoomConfig has additions and deletions. For details, see iOS below.<br><br>2. **Behavior changes**:<br><br>   * V3.58:<br><br>      * By default, the main stream is automatically published when joining the room. Whether to publish audio or video streams when joining the room is determined by calling publishVideoStream(false) and publishAudioStream(false)<br><br>   * publishVideoStream/publishAudioStream are effective before and after joining the room<br><br>   * V3.60:<br><br>      * Audio and video streams (main stream) are automatically published when joining the room. Whether the streams are published is determined by isPublishVideo and isPublishAudio in RTCRoomConfig.<br><br>      * The scope of publishVideoStream/publishAudioStream single\-stream version is limited to after joining the room, and calling before joining the room is invalid |
|Create room instance |createRTCRoom:(NSString \* _Nonnull)roomId |createRTCRoom:(NSString \* _Nonnull)roomId |**Behavior change**:<br><br>When creating a room instance with an existing roomId, it will return the previously created room instance and no longer trigger the error code `ByteRTCWarningCodeOldRoomBeenReplaced = -2016` |
|Create room failure callback |rtcEngine:onCreateRoomStateChanged:errorCode: |rtcRoom:onRoomStateChanged:withUid:state:extraInfo: |**Interface replacement**:<br><br>Room creation failure is notified by rtcRoom:onRoomStateChanged:withUid:state:extraInfo:. No longer through onCreateRoomStateChanged callback. |
|Callback for setting room extra information result |onSetRoomExtraInfoResult:(NSInteger)taskId error:(ByteRTCSetRoomExtraInfoResult)error; |onSetRoomExtraInfoResult:(NSInteger)taskId result:(ByteRTCSetRoomExtraInfoResult)result; |**Replaced parameter**: `error` renamed to `result`. |
|Callback for remote visible user joining room, or invisible user in room switching to visible |onUserJoined:(ByteRTCUserInfo \*_Nonnull)userInfo elapsed:(NSInteger)elapsed; |onUserJoined:(ByteRTCUserInfo\*_Nonnull)userInfo; |**Replaced parameter**: Removed invalid parameter `elapsed`. |


<span id="publish-and-subscribe-to-simulcast-streams"></span>
## Publish and Subscribe to Simulcast Streams


|Change Type |V3.58 |V3.60 |Description |
|---|---|---|---|
|Enable/disable pushing multiple video streams |enableSimulcastMode:(BOOL) enabled<br><br>After enabling, all configured Simulcast streams will be published. |setLocalSimulcastMode:(ByteRTCVideoSimulcastMode)mode |* **Interface rename**<br><br>* **Function extension and parameter change**: Removed `boolean enabled` from the old method and replaced it with `(ByteRTCVideoSimulcastMode)mode`, allowing the parameter `ByteRTCVideoSimulcastMode` to specify the specific simulcast mode type.<br><br>* **Default behavior adjustment**:<br><br>   * Old interface: When `enabled` is `true`, all configured Simulcast streams will be published<br><br>   * New interface: When the `mode` parameter is set to `ByteRTCVideoSimulcastModeAlwaysSimulcast` = `2`, all configured Simulcast streams will be published.<br><br>* **Calling timing change**: The old method is called before joining the room or after joining the room but before publishing streams, while the new method needs to be called before joining the room. |
|Set parameters for expected subscription to remote video streams |setRemoteVideoConfig:(NSString \* _Nonnull) userId remoteVideoConfig:(ByteRTCRemoteVideoConfig \*_Nonnull) remoteVideoConfig |setRemoteSimulcastStreamType:(NSString \* _Nonnull) streamId streamType:(ByteRTCVideoSimulcastStreamType)streamType |* **Interface rename**<br><br>* **Parameter change**:<br><br>   * Changed parameter userId to streamId, tracking streams instead of users.<br><br>   * Replaced parameter `remoteVideoConfig` with `streamType`, no longer need to specify specific values, you can specify subscription preferences by passing enum values. |
|Set or update Simulcast stream encoding parameters |setVideoEncoderConfig:(NSArray <ByteRTCVideoEncoderConfig \*\> \* _Nullable) encoderConfigs |setLocalSimulcastMode:(ByteRTCVideoSimulcastMode)mode config:(NSArray <ByteRTCVideoEncoderConfig \*\> \* _Nullable)streamConfig |* **Interface replacement**<br><br>* **Parameter change**:<br><br>   * Parameter `encoderConfigs` changed to `streamConfig`<br><br>   * Added parameter `mode`, user specifies stream type (main stream or sub stream) |
|* Set single video stream parameters<br><br>* Set multiple video stream parameters |setMaxVideoEncoderConfig:(ByteRTCVideoEncoderConfig \* _Nullable) max_solution; |setVideoEncoderConfig:(ByteRTCVideoEncoderConfig \* _Nullable) encoderConfig; |* **Interface merge**<br><br>* **Function change**: New method is only used to set main stream encoding parameters.<br><br>* **Replaced parameter**: Parameter changed to `encoderConfig` |


<span id="9aeb68fc"></span>
### Publish and Subscribe to Main Stream\*\* (Camera/Microphone Captured Stream)


|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|1. **Publish/unpublish audio and video streams** ||| |
|API:<br><br><br>* Publish audio and video streams<br><br>* Unpublish audio and video streams |* publishStream:(ByteRTCMediaStreamType)type<br><br>* unpublishStream:(ByteRTCMediaStreamType)type |* publishStreamVideo:(BOOL)publish<br><br>* publishStreamAudio:(BOOL)publish |* **Interface split and function extension**:<br><br>   * **Split by audio and video**: 2 new methods are used to control the publishing of video streams and audio streams respectively<br><br>   * **Merge publish and unpublish**: New interface handles publish and unpublish operations through `(BOOL)publish` parameter<br><br>* **Parameter change**:<br><br>   * Removed `(ByteRTCMediaStreamType)type`, new methods directly distinguish video and audio streams through method names<br><br>   * Added `(BOOL)publish`<br><br>* **Behavior change**:<br><br>   * V3.58: Effective before and after joining the room<br><br>   * V3.60: Scope is limited to after joining the room, calling before joining the room is invalid |
|Audio and video stream publish state change callback |* rtcRoom:( ByteRTCRoom \* _Nonnull)rtcRoom onUserPublishStream:(NSString \*_Nonnull)userId type:(ByteRTCMediaStreamType)type;<br><br>* rtcRoom:( ByteRTCRoom \* _Nonnull)rtcRoom onUserUnpublishStream:(NSString \*_Nonnull)userId type:(ByteRTCMediaStreamType)type reason:(ByteRTCStreamRemoveReason)reason; |* rtcRoom:(ByteRTCRoom\* _Nonnull)rtcRoom onUserPublishStreamAudio:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info isPublish:(BOOL)isPublish<br><br>* rtcRoom:(ByteRTCRoom\* _Nonnull)rtcRoom onUserPublishStreamVideo:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info isPublish:(BOOL)isPublish |* **Interface split, rename and function extension**:<br><br>   * **Split by audio and video**: 2 new methods are used for audio stream and video stream subscription callbacks respectively<br><br>   * **Merge subscribe and unsubscribe states**: New interface uses `isPublish` parameter to represent publish and unpublish<br><br>* **Parameter change**:<br><br>   * **Removed parameter**<br><br>      * Removed `userId`, new method identifies through `streamId` parameter.<br><br>      * Removed `type`, new method directly distinguishes video and audio streams through method names.<br><br>      * Removed `reason`, no longer provides detailed information about removal reasons.<br><br>   * **Added parameter**: Added `streamId` parameter to distinguish streams. |
|Callback when audio and video stream publish state triggers warning or error |rtcRoom:(ByteRTCRoom \*_Nonnull)rtcRoom onStreamStateChanged:(NSString \*_Nonnull)roomId withUid:(nonnull NSString \*)uid state:(NSInteger)state extraInfo:(NSString \*_Nonnull)extraInfo; |* rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onVideoPublishStateChanged:(NSString  *_Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info state:(ByteRTCPublishState)state reason:(ByteRTCPublishStateChangeReason)reason<br><br>* rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onAudioPublishStateChanged:(NSString  *_Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info state:(ByteRTCPublishState)state reason:(ByteRTCPublishStateChangeReason)reason |* **Interface split and rename**: Split by audio and video, new methods are used for video stream and audio stream publish state callbacks respectively<br><br>* **Replaced parameter**:<br><br>   * **Removed parameter**:<br><br>      * Removed parameters `roomId` and `uid`;<br><br>      * Removed invalid parameter `extraInfo`.<br><br>   * **Added parameter**:<br><br>      * Added `streamId` and `info` parameters to identify stream unique identifier and stream information;<br><br>      * Added `reason` parameter to describe the specific reason for state changes in more detail.<br><br>   * **Parameter type change**: `state` parameter type changed from `NSInteger` to `ByteRTCPublishState` enumeration type to provide clearer state definitions |
|2. **Subscribe/unsubscribe to audio and video streams** ||| |
|* Subscribe to audio and video streams<br><br>* Unsubscribe from audio and video streams |* subscribeStream:(NSString \*_Nonnull)userId mediaStreamType:(ByteRTCMediaStreamType)mediaStreamType<br><br>* unsubscribeStream:(NSString \*_Nonnull)userId mediaStreamType:(ByteRTCMediaStreamType)mediaStreamType; |* subscribeStreamAudio:(NSString \*_Nonnull)streamId subscribe:(BOOL)subscribe<br><br>* subscribeStreamVideo:(NSString \*_Nonnull)streamId subscribe:(BOOL)subscribe |* **Interface split, rename and function extension**:<br><br>   * **Split by audio and video**: 2 new methods are used to control video stream and audio stream subscription respectively<br><br>   * **Merge subscribe and unsubscribe**: New interface uses `subscribe` parameter to represent subscribe and unsubscribe<br><br>* **Parameter change**:<br><br>   * **Removed parameter**:<br><br>      * Removed `userId`, use `streamId` to identify streams.<br><br>      * Removed `type`, new methods directly distinguish video and audio streams through method names<br><br>   * **Added parameter**:<br><br>      * `streamId` used to identify streams;<br><br>      * `subscribe`, used to identify whether to subscribe. |
|Audio and video stream subscription state change callback |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onStreamSubscribed:(ByteRTCSubscribeState)state userId:(NSString \*_Nonnull)userId subscribeConfig:(ByteRTCSubscribeConfig \*_Nonnull)info |* rtcRoom:(ByteRTCRoom\* _Nonnull)rtcRoom onUserPublishStreamAudio:(NSString\* _Nonnull)roomId uid:(NSString\* _Nonnull)uid isPublish:(BOOL)isPublish<br><br>* rtcRoom:(ByteRTCRoom\* _Nonnull)rtcRoom onUserPublishScreenVideo:(NSString\* _Nonnull)roomId uid:(NSString\* _Nonnull)uid isPublish:(BOOL)isPublish |* **Interface split, rename and function extension**:<br><br>   * **Split by audio and video**: 2 new methods are used for audio stream and video stream subscription callbacks respectively<br><br>   * **Merge subscribe and unsubscribe states**: New interface uses `(BOOL)isPublish` parameter to represent publish and unpublish<br><br>* **Parameter change**:<br><br>   * **Added parameter**: `roomId`: Room ID<br><br>   * **Parameter rename**: `userId` renamed to `uid`<br><br>   * **Removed parameter**:<br><br>      * Removed `subscribeConfig:(ByteRTCSubscribeConfig *_Nonnull)info`, no longer provides subscription configuration information.<br><br>      * Removed `state` parameter, replaced by `isPublish` parameter to clearly distinguish between publish and unpublish states |
|Audio and video stream subscription state change callback |rtcRoom:(ByteRTCRoom \*_Nonnull)rtcRoom onStreamStateChanged:(NSString \*_Nonnull)roomId withUid:(nonnull NSString \*)uid state:(NSInteger)state extraInfo:(NSString \*_Nonnull)extraInfo; |* rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onVideoSubscribeStateChanged:(NSString  *_Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info state:(ByteRTCSubscribeState)state reason:(ByteRTCSubscribeStateChangeReason)reason<br><br>* rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onAudioSubscribeStateChanged:(NSString  *_Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info state:(ByteRTCSubscribeState)state reason:(ByteRTCSubscribeStateChangeReason)reason |* **Interface split and rename**: Split by audio and video, new methods are used for video stream and audio stream publish state callbacks respectively<br><br>* **Parameter change**:<br><br>   * **Added parameter**:<br><br>      * Added `streamId` and `info` parameters to identify stream information for subscription state changes.<br><br>      * Added `reason` parameter to identify the specific reason for subscription state changes<br><br>   * **Parameter type change**: `state` parameter type changed from `NSInteger` to `ByteRTCSubscribeState` enumeration type to provide clearer state definitions.<br><br>   * **Removed parameter**:<br><br>      * Removed parameters `roomId` and `uid`;<br><br>      * Removed invalid parameter `extraInfo`. |
|3. **Subscribe/unsubscribe to all media streams** ||||
|* Subscribe to all media streams<br><br>* Unsubscribe from all media streams |* subscribeAllStreamsWithMediaStreamType:(ByteRTCMediaStreamType)mediaStreamType<br><br>* unsubscribeAllStreamsWithMediaStreamType:(ByteRTCMediaStreamType)mediaStreamType |* subscribeAllStreamsVideo:(BOOL)subscribe<br><br>* subscribeAllStreamsAudio:(BOOL)subscribe |* **Interface split, rename, and feature expansion**:<br><br>   * **Split by audio and video**: 2 new methods are used to control video stream and audio stream subscription respectively<br><br>   * **Merge subscribe and unsubscribe**: New interface handles subscription and unsubscription through `subscribe` parameter<br><br>* **Replaced parameter**: Removed `mediaStreamType`, new methods directly distinguish video streams and audio streams through method names |
|Pause receiving media streams from remote |pauseAllSubscribedStream:(ByteRTCPauseResumControlMediaType) mediaType |* pauseAllSubscribedStreamAudio<br><br>* pauseAllSubscribedStreamVideo |* **Interface split**: Split by audio and video, 2 new methods are used to pause receiving all remote audio streams and pause all remote video streams respectively<br><br>* **Replaced parameter**: Removed `mediaType` parameter, new methods directly distinguish audio and video streams through method names |
|Resume receiving media streams from remote |resumeAllSubscribedStream:(ByteRTCPauseResumControlMediaType) mediaType |* resumeAllSubscribedStreamAudio<br><br>* resumeAllSubscribedStreamVideo |* **Interface split**: Split by audio and video, 2 new methods are used to resume receiving all remote audio streams and resume receiving all remote video streams respectively<br><br>* **Replaced parameter**: Removed `mediaType` parameter, new methods directly distinguish audio and video streams through method names |


<span id="98e49606"></span>
### Screen Sharing


1. Screen streams and normal video streams cannot coexist in the same engine. Starting a screen stream will automatically stop the normal video stream, and starting a normal video stream will automatically stop the screen stream.

2. Screen streams and normal video streams use the same publish and subscribe methods. A series of interfaces with "screen" have been deprecated.



|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|Capture screen video |startScreenVideoCapture:(ByteRTCScreenCaptureSourceInfo  *_Nonnull)sourceInfo captureParameters:(ByteRTCScreenCaptureParam \*\*Nonnull)captureParameters NS_SWIFT_NAME(startScreenVideoCapture(* :captureParameters:)) |startScreenVideoCapture:(ByteRTCScreenCaptureSourceInfo  *_Nonnull)sourceInfo captureParameters:(ByteRTCScreenCaptureParam \*\*Nonnull)captureParameters NS_SWIFT_NAME(startScreenVideoCapture(* :captureParameters:)) |**Behavior change**:<br><br>When starting screen capture, video capture functionality will be stopped |
|Set screen stream encoding parameters |setScreenVideoEncoderConfig:(ByteRTCScreenVideoEncoderConfig \* _Nullable) encoderConfig |setVideoEncoderConfig:(ByteRTCVideoEncoderConfig \* _Nullable) encoderConfig |**Interface replacement**:<br><br>Screen streams and video streams share the same encoding parameters. Parameters set by setVideoEncoderConfig will apply to both screen streams and normal video streams |
|Publish/stop publishing local screen audio and video streams |publishScreen:(ByteRTCMediaStreamType)type<br><br>unpublishScreen:(ByteRTCMediaStreamType)type |publishStreamVideo:(BOOL)publish<br><br>publishStreamAudio:(BOOL)publish |**Interface replacement**:<br><br>Screen stream and video stream share the same publish/unpublish interface<br><br>**API split**<br><br>Audio and video publish/unpublish interfaces are separated |
|Subscribe/unsubscribe to remote screen audio and video streams |subscribeScreen:(NSString \*_Nonnull)userId mediaStreamType:(ByteRTCMediaStreamType)mediaStreamType<br><br>unsubscribeScreen:(NSString \*_Nonnull)userId mediaStreamType:(ByteRTCMediaStreamType)mediaStreamType |subscribeStreamVideo:(NSString \*_Nonnull)streamId subscribe:(BOOL)subscribe<br><br>subscribeStreamAudio:(NSString \*_Nonnull)streamId subscribe:(BOOL)subscribe |**Interface replacement**:<br><br>Screen streams and video streams share the same subscribe/unsubscribe interface<br><br>**Interface split**<br><br>Audio and video subscribe/unsubscribe interfaces are separated<br><br>**Replaced parameter**:<br><br>Use parameter streamId to distinguish which stream it is and whether it is a screen stream |
|Remote user publish or unpublish screen stream callback |rtcRoom:( ByteRTCRoom \* _Nonnull)rtcRoom onUserPublishScreen:(NSString \*_Nonnull)userId type:(ByteRTCMediaStreamType)type<br><br>rtcRoom:( ByteRTCRoom \* _Nonnull)rtcRoom onUserUnpublishScreen:(NSString \*_Nonnull)userId type:(ByteRTCMediaStreamType)type reason:(ByteRTCStreamRemoveReason)reason |rtcRoom:(ByteRTCRoom\* _Nonnull)rtcRoom onUserPublishStreamVideo:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info isPublish:(BOOL)isPublish;<br><br>rtcRoom:(ByteRTCRoom\* _Nonnull)rtcRoom onUserPublishStreamAudio:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info isPublish:(BOOL)isPublish; |**Interface replacement**:<br><br>Screen streams and video streams share the same publish/unpublish callback interface<br><br>**Interface split**<br><br>Audio and video publish/unpublish callback interfaces are separated<br><br>**Replaced parameter**:<br><br>Use parameter streamId to distinguish which stream it is and whether it is a screen stream |
|Screen sharing stream video first frame send state callback |rtcEngine:(ByteRTCVideo \*_Nonnull)engine onScreenVideoFrameSendStateChanged:(NSString \* _Nonnull)roomId rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFrameSendState)state; |rtcEngine:(ByteRTCEngine  *_Nonnull)engine onVideoFrameSendStateChanged:(NSString \* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFrameSendState)state |**Interface replacement**:<br><br>Screen stream and video stream share the same video first frame send state callback<br><br>**Replaced parameter**:<br><br>Use parameter streamId to distinguish which stream it is and whether it is a screen stream |
|Screen sharing stream video first frame playback state callback |rtcEngine:(ByteRTCVideo \*_Nonnull)engine onScreenVideoFramePlayStateChanged:(NSString \* _Nonnull)roomId rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFramePlayState)state; |rtcEngine:(ByteRTCEngine  *_Nonnull)engine onVideoFramePlayStateChanged:(NSString \* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFramePlayState)state |**Interface replacement**:<br><br>Screen stream and video stream share the same video first frame playback state callback<br><br>**Replaced parameter**:<br><br>Use parameter streamId to distinguish which stream it is and whether it is a screen stream |


<span id="5b8c6ce7"></span>
### RTS

RTC includes RTS capabilities. In the current version, RTS\-related interfaces are further split. If only using RTS\-related capabilities, call createRTSRoom to create an RTSRoom instance and use ByteRTCRTSRoomDelegate callbacks. If using both audio/video capabilities and RTS capabilities, call createRTCRoom from RTCEngine to create an RTCRoom instance and use ByteRTCRoomDelegate callbacks.

<span id="49c35885"></span>
#### ByteRTCRoom


|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|Create RTS room |createRTCRoom:(NSString \* _Nonnull)roomId; |createRTSRoom:(NSString \* _Nonnull)roomId; |**Interface split**: If only using RTS\-related capabilities, call createRTSRoom to create RTSRoom instance |
|Set RTS\-related callback |setRTCRoomDelegate:(id_Nullable)roomDelegate; |setRTSRoomDelegate:(id_Nullable)roomDelegate; |**Interface split**: If only using RTS\-related capabilities, call this interface in RTSRoom to set callback |
|Callback received when receiving binary message from user outside the room |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserBinaryMessageReceivedOutsideRoom:(NSString \* _Nonnull)uid message:(NSData \* _Nonnull)message |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserBinaryMessageReceivedOutsideRoom:(NSInteger)msgid uid:(NSString \* _Nonnull)uid message:(NSData \* _Nonnull)message |**Replaced parameter**: Callback parameter adds msgid parameter |
|Callback for receiving broadcast message in room |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onRoomMessageReceived:(NSString \*_Nonnull)uid message:(NSString \*_Nonnull)message |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onRoomMessageReceived:(NSInteger)msgid uid:(NSString \*_Nonnull)uid message:(NSString \*_Nonnull)message |**Replaced parameter**: Callback parameter adds msgid parameter |
|Callback for receiving broadcast binary message in room |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onRoomBinaryMessageReceived:(NSString \*_Nonnull)uid message:(NSData \*_Nonnull)message |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onRoomBinaryMessageReceived:(NSInteger)msgid uid:(NSString \*_Nonnull)uid message:(NSData \*_Nonnull)message |**Replaced parameter**: Callback parameter adds msgid parameter |
|Callback received when receiving point\-to\-point text message from other users in the room |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onUserMessageReceived:(NSString \*_Nonnull)uid message:(NSString \*_Nonnull)message |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onUserMessageReceived:(NSInteger)msgid uid:(NSString \*_Nonnull)uid message:(NSString \*_Nonnull)message |**Replaced parameter**: Callback parameter adds msgid parameter |
|Callback received when receiving point\-to\-point binary message from other users in the room |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onUserBinaryMessageReceived:(NSString \*_Nonnull)uid message:(NSData \*_Nonnull)message |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onUserBinaryMessageReceived:(NSInteger)msgid uid:(NSString \*_Nonnull)uid message:(NSData \*_Nonnull)message |**Replaced parameter**: Callback parameter adds msgid parameter |


<span id="dcdcb654"></span>
#### ByteRTCRTSRoom


|**Function** |**V3.58** |**V3.60** |Description |
|---|---|---|---|
|Callback for receiving broadcast message in room |rtsRoom:(ByteRTCRTSRoom \* _Nonnull)rtsRoom onRoomMessageReceived:(NSString \* _Nonnull)uid message:(NSString \* _Nonnull)message; |rtsRoom:( ByteRTCRTSRoom \*_Nonnull)rtsRoom onRoomMessageReceived:(NSInteger)msgid uid:(NSString \*_Nonnull)uid message:(NSString \*_Nonnull)message; |**Replaced parameter**: Callback parameter adds msgid parameter |
|Callback for receiving broadcast binary message in room |rtsRoom:(ByteRTCRTSRoom \* _Nonnull)rtsRoom onRoomBinaryMessageReceived:(NSString \* _Nonnull)uid message:(NSData \* _Nonnull)message; |rtsRoom:( ByteRTCRTSRoom \*_Nonnull)rtsRoom onRoomBinaryMessageReceived:(NSInteger)msgid uid:(NSString \*_Nonnull)uid message:(NSData \*_Nonnull)message; |**Replaced parameter**: Callback parameter adds msgid parameter |
|Callback received when receiving point\-to\-point text message from other users in the room |rtsRoom:( ByteRTCRTSRoom \*_Nonnull)rtsRoom onUserMessageReceived:(NSString \*_Nonnull)uid message:(NSString \*_Nonnull)message; |rtsRoom:( ByteRTCRTSRoom \*_Nonnull)rtsRoom onUserMessageReceived:(NSInteger)msgid uid:(NSString \*_Nonnull)uid message:(NSString \*_Nonnull)message; |**Replaced parameter**: Callback parameter adds msgid parameter |
|Callback received when receiving point\-to\-point binary message from other users in the room |rtsRoom:( ByteRTCRTSRoom \*_Nonnull)rtsRoom onUserBinaryMessageReceived:(NSString \*_Nonnull)uid message:(NSData \*_Nonnull)message; |rtsRoom:( ByteRTCRTSRoom \*_Nonnull)rtsRoom onUserBinaryMessageReceived:(NSInteger)msgid uid:(NSString \*_Nonnull)uid message:(NSData \*_Nonnull)message; |**Replaced parameter**: Callback parameter adds msgid parameter |


<span id="94248c78"></span>
### WTN stream (formerly public stream)


* Interface relocation:

   * WTN stream subscription interfaces moved to the new `ByteRTCWTNStream` class.

   * WTN stream subscriber callbacks moved to the new `ByteRTCWTNStreamDelegate` callback class. You need to call setWTNStreamDelegate: first to set the callback handle.

* Share MixedStreamConfig with mixed stream push interfaces to improve usability.

* Added onWTNRemoteVideoStats:videoStats: and onWTNRemoteAudioStats:audioStats: for obtaining WTN stream information and detecting stream quality.

* Interface split, rename, and replacement, specific changes as follows:



|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|Publish WTN stream |startPushPublicStream:(NSString \* _Nonnull)publicStreamId withLayout:(ByteRTCPublicStreaming \*_Nullable)publicStream |startPushMixedStream:(NSString \* _Nonnull)taskId withPushTargetConfig:(ByteRTCMixedStreamPushTargetConfig\*)pushTargetConfig withMixedConfig:(ByteRTCMixedStreamConfig \*_Nullable)config |* **Interface rename**<br><br>* **Interface merge and feature expansion**: startPushPublicStream and startPushMixedStreamToCDN are merged into startPushMixedStream, the new interface can be used for both mixed stream push to CDN or push to WTN (formerly public stream)<br><br>* **Parameter change**:<br><br>   * **Added parameter**: Added `taskId`: Set push task ID to identify the push task<br><br>   * **Replaced parameter**:<br><br>      * Removed `publicStreamId`: The new parameter `pushTargetConfig` specifies the WTN stream ID (that is, public stream ID)<br><br>      * Removed `publicStream`, the new parameter `mixedConfig` specifies the configuration of WTN stream (for example, video transcoding, layout, and more) |
|Update WTN stream |updatePublicStreamParam:(NSString \* _Nonnull)publicStreamId withLayout:(ByteRTCPublicStreaming \*_Nullable)publicStream |updatePushMixedStream:(NSString _Nonnull)taskId withPushTargetConfig:(ByteRTCMixedStreamPushTargetConfig)pushTargetConfig withMixedConfig:(ByteRTCMixedStreamConfig \*_Nonnull)config |* **Interface rename**<br><br>* **Interface merge and feature expansion**: updatePublicStreamParam and updatePushMixedStreamToCDN are merged into updatePushMixedStream, the new interface can be used for both updating mixed stream push to CDN and push to WTN (formerly public stream) tasks<br><br>* **Parameter change**:<br><br>   * **Added parameter**: Added `taskId`, the ID of the mixed stream task<br><br>   * **Replaced parameter**:<br><br>      * Removed `publicStreamId`: The new parameter `pushTargetConfig` specifies the WTN stream ID (that is, public stream ID)<br><br>      * Removed `publicStream`, the new parameter `mixedConfig` specifies the configuration of WTN stream (for example, video transcoding, layout, and more) |
|Stop publishing WTN stream |stopPushPublicStream:(NSString \* _Nonnull)publicStreamId; |stopPushMixedStream:(NSString \*_Nonnull)taskId withPushTargetType:(ByteRTCMixedStreamPushTargetType)pushTargetType |* **Interface rename**<br><br>* **Interface merge and feature expansion**: stopPushPublicStream and stopPushStreamToCDN are merged into stopPushMixedStream, the new interface can be used for both stopping WTN stream (formerly public stream) publishing and stopping mixed stream push<br><br>* **Parameter change**:<br><br>   * **Added parameter**: Added `taskId`, the ID of the mixed stream task<br><br>   * **Replaced parameter**: Removed `publicStreamId`, the new parameter `pushTargetType` specifies the stream to stop |
|* Subscribe to WTN stream<br><br>* Unsubscribe from WTN stream |* startPlayPublicStream:(NSString \* _Nonnull)publicStreamId<br><br>* stopPlayPublicStream:(NSString \* _Nonnull)publicStreamId |* subscribeWTNVideoStream:(NSString \* _Nonnull)streamId subscribe:(bool)subscribe<br><br>* subscribeWTNAudioStream:(NSString \* _Nonnull)streamId subscribe:(bool)subscribe |* **Interface split, rename, and feature expansion**:<br><br>   * **Split by audio and video**: 2 new methods are used for subscribing/unsubscribing to WTN audio streams and subscribing/unsubscribing to video streams respectively<br><br>   * **Merge subscribe and unsubscribe**: New interface handles subscription and unsubscription through `(bool)subscribe` parameter<br><br>* **Parameter change**:<br><br>   * `publicStreamId`: Renamed to streamId<br><br>   * Added `boolean subscribe` |
|Bind WTN stream canvas |setPublicStreamVideoCanvas:(NSString \*_Nonnull)publicStreamId withCanvas:(ByteRTCVideoCanvas \* Nullable)canvas NS_SWIFT_NAME(setPublicStreamVideoCanvas(:withCanvas:)) |setWTNRemoteVideoCanvas:(NSString \*_Nonnull)streamId withCanvas:(ByteRTCVideoCanvas \* Nullable)canvas NS_SWIFT_NAME(setWTNRemoteVideoCanvas(:withCanvas:)) |* **Interface rename**<br><br>* **Replaced parameter**: `publicStreamId` renamed to `streamId` |
|Specify external renderer for WTN stream |setPublicStreamVideoSink:(NSString \*_Nonnull)publicStreamId withSink:(id_Nullable)videoSink withPixelFormat:(ByteRTCVideoSinkPixelFormat)requiredFormat NS_SWIFT_NAME(setPublicStreamVideoSink(:withSink:withPixelFormat:)) |setWTNRemoteVideoSink:(NSString  *_Nonnull)streamId withSink:(id_Nullable)videoSink withConfig:(ByteRTCRemoteVideoSinkConfig*)config NS_SWIFT_NAME(setWTNRemoteVideoSink(_:withSink:withConfig:)) |* **Interface rename**<br><br>* **Parameter change**:<br><br>   * **Parameter rename**: `publicStreamId` renamed to `streamId`<br><br>   * **Added parameter**: `config` (`ByteRTCRemoteVideoSinkConfig` type), used to configure remote video frames (for example position, format, whether to mirror video frames, and more)<br><br>   * **Replacement and relocation**:<br><br>      Remove `requiredFormat`, moved to `ByteRTCRemoteVideoSinkConfig`, default is 0 (original format) |
|Adjust WTN stream playback volume |setPublicStreamAudioPlaybackVolume:(NSString \*_Nonnull)publicStreamId volume:(NSInteger)volume |setWTNRemoteAudioPlaybackVolume:(NSString \*_Nonnull)streamId volume:(NSInteger)volume |* **Interface rename**<br><br>* **Replaced parameter**: `publicStreamId` renamed to `streamId` |
|WTN stream task callback |rtcEngine:(ByteRTCVideo \*_Nonnull)engine onPushPublicStreamResult:(NSString \*_Nonnull)roomId publicStreamId:(NSString \*_Nonnull)streamId errorCode:(ByteRTCPublicStreamErrorCode)errorCode |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onMixedStreamEvent:(ByteRTCMixedStreamTaskEvent)event withMixedStreamInfo:(ByteRTCMixedStreamTaskInfo\*)info withErrorCode:(ByteRTCMixedStreamTaskErrorCode)errorCode |* **Interface rename**<br><br>* **Interface merge and functionality extension**: onMixingEvent, onStreamMixingEvent and onPushPublicStreamResult are merged into onMixedStreamEvent, the new interface can be used simultaneously for callbacks of mixed stream push to CDN / WTN stream status<br><br>* **Parameter change**:<br><br>   * **Parameter type change**:<br><br>      The type of `errorCode` is changed from `ByteRTCPublicStreamErrorCode` to `ByteRTCMixedStreamTaskErrorCode`, sharing the same enumeration class with mixed stream push tasks. For change details, refer to iOS<br><br>   * **Removed parameter**:<br><br>      * Remove `roomId`: No longer needs to be passed in<br><br>      * Remove `publicStreamId`: Replaced by `taskId` in the newly added `MixedStreamTaskInfo info`<br><br>   * **Added parameter**: Added `event` (mixed stream task event) of `ByteRTCMixedStreamTaskEvent` type, for details refer to iOS |
|Play WTN stream task callback |rtcEngine:(ByteRTCVideo \*_Nonnull)engine onPlayPublicStreamResult:(NSString \*_Nonnull)publicStreamId errorCode:(ByteRTCPublicStreamErrorCode)errorCode |* onWTNVideoSubscribeStateChanged:(NSString \*_Nonnull)streamId state:(ByteRTCWTNSubscribeState)state reason:(ByteRTCWTNSubscribeStateChangeReason)reason<br><br>* onWTNAudioSubscribeStateChanged:(NSString \*_Nonnull)streamId state:(ByteRTCWTNSubscribeState)state reason:(ByteRTCWTNSubscribeStateChangeReason)reason |* **Interface split and rename**: Split into 2 independent interfaces, used respectively for callbacks of WTN audio/video stream subscription status changes<br><br>* **Replaced parameter**:<br><br>   * **Parameter rename**: `publicStreamId` renamed to `streamId`<br><br>   * **Removed parameter**: Remove `errorCode`, replaced by `state` (subscription status code) and `reason` (subscription status change reason).<br><br>* **Location move**: Moved to `ByteRTCWTNStreamDelegate` class |
|Receive SEI callback in WTN stream |rtcEngine:(ByteRTCVideo \* _Nonnull)engine onPublicStreamSEIMessageReceived:(NSString\* _Nonnull)publicStreamId andMessage:(NSData\* _Nonnull)message andSourceType:(ByteRTCDataMessageSourceType)sourceType |onWTNSEIMessageReceived:(NSString\* _Nonnull)streamId andChannelId:(int)channelId andMessage:(NSData\* _Nonnull)message |* **Interface rename**<br><br>* **Parameter change**:<br><br>   * **Parameter rename**: `publicStreamId` renamed to `streamId`<br><br>   * **Added parameter**: Added `channelId`, set different ChannelID for different receivers, receivers can select SEI information to focus on based on ChannelID in callback<br><br>   * **Removed parameter**: Remove `DataMessageSourceType sourceType`, no longer needs to be passed in<br><br>* **Location move**: Moved to `ByteRTCWTNStreamDelegate` class |
|Receive Data Message callback in WTN stream |rtcEngine:(ByteRTCVideo \* _Nonnull)engine onPublicStreamDataMessageReceived:(NSString\* _Nonnull)publicStreamId andMessage:(NSData\* _Nonnull)message andSourceType:(ByteRTCDataMessageSourceType)sourceType |onWTNDataMessageReceived:(NSString\* _Nonnull)streamId andMessage:(NSData\* _Nonnull)message andSourceType:(ByteRTCDataMessageSourceType)sourceType |* **Interface rename**<br><br>* **Replaced parameter**: `publicStreamId` renamed to `streamId`<br><br>* **Location move**: Moved to `ByteRTCWTNStreamDelegate` class |
|WTN video stream first frame decode success callback |rtcEngine:(ByteRTCVideo \* _Nonnull)engine onFirstPublicStreamVideoFrameDecoded:(NSString \* _Nonnull)publicStreamId withFrameInfo:(ByteRTCVideoFrameInfo \* Nonnull)frameInfo NS_SWIFT_NAME(rtcEngine(:onFirstPublicStreamVideoFrameDecoded:withFrameInfo:)) |onWTNFirstRemoteVideoFrameDecoded:(NSString \* _Nonnull)streamId withFrameInfo:(ByteRTCVideoFrameInfo \* _Nonnull)frameInfo NS_SWIFT_NAME(onWTNFirstRemoteVideoFrameDecoded(streamId:withFrameInfo:)) |* **Interface rename**<br><br>* **Parameter rename**: `publicStreamId` renamed to `streamId`<br><br>* **Location move**: Moved to `ByteRTCWTNStreamDelegate` class |
|WTN audio stream first frame decode success callback |rtcEngine:(ByteRTCVideo \* _Nonnull)engine onFirstPublicStreamAudioFrame:(NSString \* _Nonnull)publicStreamId |onWTNFirstRemoteAudioFrame:(NSString \* _Nonnull)streamId |* **Interface rename**<br><br>* **Replaced parameter**: `publicStreamId` renamed to `streamId`<br><br>* **Location move**: Moved to `ByteRTCWTNStreamDelegate` class |


<span id="5cdb1028"></span>
### Push to CDN

Optimized the usability of push to live streaming interfaces. Share MixedStreamConfig with WTN interfaces to improve usability. If you have already implemented push to live streaming functionality, refer to the following table to replace interfaces.


|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|Mixed stream push |startPushMixedStreamToCDN:(NSString \* _Nonnull)taskID mixedConfig:(ByteRTCMixedStreamConfig \*_Nullable)config observer:(id_Nullable)observer |startPushMixedStream:(NSString \* _Nonnull)taskId withPushTargetConfig:(ByteRTCMixedStreamPushTargetConfig\*)pushTargetConfig withMixedConfig:(ByteRTCMixedStreamConfig \*_Nullable)config |* **Interface rename**<br><br>* **Interface merge and functionality change**: startPushPublicStream and startPushMixedStreamToCDN are merged into startPushMixedStream, the new interface can be used simultaneously for mixed stream push to CDN and push to WTN (formerly public stream)<br><br>* **Parameter change**:<br><br>   * **Parameter rename**: `taskID` renamed to `taskId`<br><br>   * **Remove and delete**: `observer`<br><br>   * **Added parameter**: Added `pushTargetConfig`, type is `ByteRTCMixedStreamPushTargetConfig`, used to configure push target. |
|Update mixed stream push task |updatePushMixedStreamToCDN:(NSString \*_Nonnull)taskID mixedConfig:(ByteRTCMixedStreamConfig \*_Nonnull)config |updatePushMixedStream:(NSString  *_Nonnull)taskId withPushTargetConfig:(ByteRTCMixedStreamPushTargetConfig*)pushTargetConfig withMixedConfig:(ByteRTCMixedStreamConfig \*_Nonnull)config |* **Interface rename**<br><br>* **Interface merge**: updatePublicStreamParam and updatePushMixedStreamToCDN are merged into updatePushMixedStream, the new interface can be used simultaneously for updating mixed stream push to CDN and push to WTN (formerly public stream) tasks<br><br>* **Parameter change**:<br><br>   * **Parameter rename**: `taskID` renamed to `taskId`<br><br>   * **Added parameter**: Added `pushTargetConfig`, type is `ByteRTCMixedStreamPushTargetConfig`, used to set target push address |
|Single stream push |startPushSingleStreamToCDN:(NSString \*_Nonnull)taskID singleStream:(ByteRTCPushSingleStreamParam \*_Nonnull)singleStream observer:(idNullable)observer NS_SWIFT_NAME(startPushSingleStreamToCDN(:singleStream:observer:)) |startPushSingleStream:(NSString \*_Nonnull)taskId singleStream:(ByteRTCPushSingleStreamParam \*_Nonnull)singleStream |* **Interface rename**<br><br>* **Parameter change**:<br><br>   * **Removed parameter**: Remove `observer`, no longer needs to be passed in<br><br>   * **Parameter rename**: `taskID` renamed to `taskId` |
|Stop push task |stopPushStreamToCDN:(NSString \*Nonnull)taskID NS_SWIFT_NAME(stopPushStreamToCDN(:)) |* startPushSingleStream:(NSString \*_Nonnull)taskId singleStream:(ByteRTCPushSingleStreamParam \*_Nonnull)singleStream<br><br>* stopPushMixedStream:(NSString \*_Nonnull)taskId withPushTargetType:(ByteRTCMixedStreamPushTargetType)pushTargetType |* **Interface split and rename**: Split by single stream and mixed stream<br><br>* **Among them, stop mixed stream push interface (stopPushMixedStream):** <br><br>   * **Functionality extension**: Can be used to stop push to CDN and also to stop push to WTN stream<br><br>   * **Added parameter**: Added `pushTargetType`, type is `ByteRTCMixedStreamPushTargetType` enumeration, used to specify the target stream to stop<br><br>   * **Parameter rename**: `taskID` renamed to `taskId` |
|Push task callback |onMixingEvent:(ByteRTCStreamMixingEvent)event taskId:(NSString \*_Nonnull)taskId error:(ByteRTCStreamMixingErrorCode)errorCode mixType:(ByteRTCMixedStreamType)mixType |* rtcEngine:(ByteRTCEngine \* _Nonnull)engine onMixedStreamEvent:(ByteRTCMixedStreamTaskEvent)event withMixedStreamInfo:(ByteRTCMixedStreamTaskInfo\*)info withErrorCode:(ByteRTCMixedStreamTaskErrorCode)errorCode<br><br>* rtcEngine:(ByteRTCEngine \* _Nonnull)engine onSingleStreamEvent:(ByteRTCSingleStreamTaskEvent)event withTaskId:(NSString\*)taskId withErrorCode:(ByteRTCSingleStreamTaskErrorCode)errorCode |* **Interface split and rename**: Split by mixed stream task event callback and single stream task event callback<br><br>   **Among them, mixed stream push callback (onMixedStreamEvent):** <br><br>   * **Interface merge and functionality extension**: onMixingEvent, onStreamMixingEvent and onPushPublicStreamResult are merged into onMixedStreamEvent, the new interface can be used simultaneously for callback of mixed stream push to CDN / WTN stream status<br><br>* **Parameter change**:<br><br>   * **Type change**:<br><br>      * `event` (event): Type changed from `ByteRTCStreamMixingEvent` to `ByteRTCMixedStreamTaskEvent`, for details please refer to iOS<br><br>      * `errorCode`: Type changed from `ByteRTCStreamMixingErrorCode` to `ByteRTCMixedStreamTaskErrorCode`, for details please refer to iOS<br><br>   * **Removed parameter**: Remove `MixedStreamType mixType`: No replacement<br><br>   * **Added parameter**: Added `info`, type is `ByteRTCMixedStreamTaskInfo`, used to provide detailed information of mixed stream task<br><br>* **Location move**: Moved to ByteRTCEngineDelegate |


<span id="809c10ff"></span>
### Audio & Video Transport


|Function |Interface Name |Description |
|---|---|---|
|Callback when receiving the first frame from a remote audio stream |rtcEngine:onFirstRemoteAudioFrame:info: |**Parameter change:** <br><br>RemoteStreamKey parameter replaced with streamId and streamInfo<br><br>**Added applicable scenarios:** <br><br>This callback will also be received after a remote user cancels publishing audio and republishes audio.<br><br>Cancel publishing includes active cancellation by the publisher, active room exit, disconnection, and stopping capture. |
|* Callback after SDK successfully renders the first frame of remote video stream<br><br>* Callback after SDK receives and decodes the first frame of remote video stream |* rtcEngine:onFirstRemoteVideoFrameRendered:info:withFrameInfo:<br><br>* rtcEngine:onFirstRemoteVideoFrameDecoded:info:withFrameInfo: |**Parameter change:** <br><br>RemoteStreamKey parameter replaced with streamId and streamInfo<br><br>**Added applicable scenarios:** <br><br>These two callbacks will also be received after a remote user cancels publishing video and republishes video.<br><br>Cancel publishing includes active cancellation by the publisher, active room exit, disconnection, and stopping capture. |
|Push external audio reference frame to SDK |pushReferenceAudioPCMData:(ByteRTCAudioFrame \* _Nonnull) audioFrame; |**Added API**: Custom audio echo cancellation reference signal |


<span id="f7678b73"></span>
### Audio\-Video Synchronization


|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|Audio\-video synchronization state change callback |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onAVSyncStateChange:(ByteRTCAVSyncState)state |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onAVSyncEvent:(NSString \*_Nonnull)roomId userId:(NSString \*_Nonnull)userId eventCode:(ByteRTCAVSyncEvent)eventCode |After the audio\-video synchronization function is enabled, the synchronization result will be notified through this callback. The new callback adds roomId and userId. At the same time, the synchronization state AVSyncState is replaced by the synchronization failure event ByteRTCAVSyncEvent. When you receive this notification, you can call setMultiDeviceAVSync: with empty parameters to unbind the synchronization relationship, and then call this interface again to bind.<br><br><br>* **Interface rename**<br><br>* **Replaced parameter**:<br><br>   * **Added parameter**: Added `roomId` and `uid`<br><br>   * **Parameter replacement**: Removed `state` parameter, replaced with `eventCode` (synchronization failure event). When you receive this notification, you can call setMultiDeviceAVSync with empty parameters to unbind the synchronization relationship, and then call this interface again to bind.<br><br>* **Behavior change**: Audio\-video synchronization failure<br><br>   * 3.58: Returned by the following error code: `ByteRTCErrorCodInvalidAudioSyncUidRepeated = -1083`<br><br>   * 3.60: Returned through rtcRoom:onAVSyncEvent:userId:eventCode: `ByteRTCAVSyncEventInvalidUidRepeated = 0` |


<span id="a4229420"></span>
### Volume, audio playback route, and audio scenario


|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|Adjust the playback volume of audio streams from specified remote users on local device |setRemoteAudioPlaybackVolume:(NSString \*_Nonnull)roomID remoteUid:(NSString \*_Nonnull)userID playVolume:(NSInteger)volume |setRemoteAudioPlaybackVolume:(NSString\* _Nonnull)streamId volume:(int)volume |* **Parameter change**:<br><br>   Parameters `roomId` and `uid` for specifying audio streams changed to `streamId`.<br><br>* **Feature expansion**:<br><br>   Upgraded from only supporting adjustment of media stream volume from specified users to supporting separate adjustment of local capture media stream volume, screen stream volume, and specific process volume. |
|Force switch current audio playback route |setAudioRoute: |setAudioRoute: |**Restriction change**:<br><br>Force switch current audio playback route, no longer restricted to use only under `AUDIO_SCENARIO_COMMUNICATION` audio scenario, can be used as long as the current state is call mode. |
|Set audio scenario type |setAudioScenario: |setAudioScenario: |The volume mode used by audio devices has changed, refer to media volume and call volume:<br><br><br>* Already set audio scenario through setAudioScenario:: Need to refer to the above documentation, replace with updated audio scenario, and pay attention to changes in volume mode.<br><br>* Never set audio scenario through setAudioScenario:: Also need to pay attention to volume mode changes of the same audio device under default audio scenario. |


<span id="eb0eac32"></span>
### Push External Video Frame


|V3.58 |V3.60 |Description |
|---|---|---|
|pushExternalVideoFrame:(ByteRTCVideoFrame \* _Nonnull)frame |pushExternalVideoFrame:(ByteRTCVideoFrameData \* _Nonnull)frame |Parameter `frame` type replaced with `ByteRTCVideoFrameData`. Compared to the original parameter type, both the included parameters and whether they are required have changed. |


<span id="60e1e6e8"></span>
### Get Song List for Each Chart Based on Hot Charts


|V3.58 |V3.60 |Description |
|---|---|---|
|getHotMusic:(ByteRTCMusicHotType)hotType filterType:(ByteRTCMusicFilterType)filterType |getHotMusic:(NSArray <NSString \*\> \*_Nullable)customHotlistId filterType:(ByteRTCMusicFilterType)filterType |**Parameter replacement**: Remove `hotType` and replace with `customHotlistId`. The type is also changed from enum to `NSArray <NSString *> *` to provide custom hotlist IDs. Property value mappings are as follows:<br><br><br>* `ByteRTCMusicHotTypeContentCenter` → `ContentCenter`<br><br>* `ByteRTCMusicHotTypeProject` → `Project` |


<span id="5a2374ab"></span>
### StreamId Unique Stream Identification

The current version uses StreamId to uniquely identify a stream. Therefore, the StreamIndex / RemoteStreamKey parameters from previous versions in various APIs are replaced by StreamId or related information. The affected APIs are as follows:


|Class |V3.58 |V3.60 |Description |
|---|---|---|---|
|ByteRTCEngine |muteAudioCapture:(ByteRTCStreamIndex)index mute:(bool)mute |muteAudioCapture: (bool)mute |Parameter change: Remove StreamIndex parameter |
|ByteRTCEngine |setCaptureVolume:(ByteRTCStreamIndex)index volume:(int)volume |setCaptureVolume: (int)volume |Parameter change: Remove StreamIndex parameter |
|ByteRTCEngine |setLocalVideoCanvas:(ByteRTCStreamIndex)streamIndex withCanvas:(ByteRTCVideoCanvas \* *Nullable)canvas NS_SWIFT_NAME(setLocalVideoCanvas(* :withCanvas:)) |setLocalVideoCanvas:(ByteRTCVideoCanvas \* _Nullable)canvas NS_SWIFT_NAME(setLocalVideoCanvas(withCanvas:)) |Parameter change: Remove StreamIndex parameter |
|ByteRTCEngine |updateLocalVideoCanvas:(ByteRTCStreamIndex)streamIndex withRenderMode:(ByteRTCRenderMode)renderMode withBackgroundColor:(NSUInteger)backgroundColor NS_SWIFT_NAME(updateLocalVideoCanvas(_:withRenderMode:withBackgroundColor:)) |updateLocalVideoCanvas:(ByteRTCRenderMode)renderMode withBackgroundColor:(NSUInteger)backgroundColor NS_SWIFT_NAME(updateLocalVideoCanvas(withBackgroundColor:)) |Parameter change: Remove StreamIndex parameter |
|ByteRTCEngine |setRemoteVideoCanvas:(ByteRTCRemoteStreamKey \* _Nonnull)key withCanvas:(ByteRTCVideoCanvas \* *Nullable)canvas NS_SWIFT_NAME(setRemoteVideoCanvas(* :withCanvas:)) |setRemoteVideoCanvas:(NSString\* _Nonnull)streamId withCanvas:(ByteRTCVideoCanvas \* *Nullable)canvas NS_SWIFT_NAME(setRemoteVideoCanvas(* :withCanvas:)) |Parameter change: Replace RemoteStreamKey with streamId |
|ByteRTCEngine |updateRemoteStreamVideoCanvas:(ByteRTCRemoteStreamKey \* _Nonnull)key withRemoteVideoRenderConfig:(ByteRTCRemoteVideoRenderConfig \* *Nonnull)remoteVideoRenderConfig NS_SWIFT_NAME(updateRemoteStreamVideoCanvas(* :withRemoteVideoRenderConfig:)); |updateRemoteStreamVideoCanvas:(NSString\* _Nonnull)streamId withRemoteVideoRenderConfig:(ByteRTCRemoteVideoRenderConfig \* *Nonnull)remoteVideoRenderConfig NS_SWIFT_NAME(updateRemoteStreamVideoCanvas(* :withRemoteVideoRenderConfig:)); |Parameter change: Replace RemoteStreamKey with streamId |
|ByteRTCEngine |setRemoteVideoSink:(ByteRTCRemoteStreamKey\* _Nonnull)streamKey withSink:(id*Nullable)videoSink withRemoteRenderConfig:(ByteRTCRemoteVideoSinkConfig*)config NS_SWIFT_NAME(setRemoteVideoSink(\*:withSink:withRemoteRenderConfig:)); |setRemoteVideoSink:(NSString\* _Nonnull)streamId withSink:(id*Nullable)videoSink withRemoteRenderConfig:(ByteRTCRemoteVideoSinkConfig*)config NS_SWIFT_NAME(setRemoteVideoSink(\*:withSink:withRemoteRenderConfig:)); |Parameter change: Replace RemoteStreamKey with streamId |
|ByteRTCEngine |setVideoSourceType:(ByteRTCVideoSourceType)type WithStreamIndex:(ByteRTCStreamIndex)streamIndex NS_SWIFT_NAME(setVideoSourceType(_:WithStreamIndex:)) |setVideoSourceType:(ByteRTCVideoSourceType)type NS_SWIFT_NAME(setVideoSourceType(_:)) |Parameter change: Remove StreamIndex parameter |
|ByteRTCEngine |setRemoteVideoMirrorType:(ByteRTCRemoteStreamKey\*)key withMirrorType:(ByteRTCRemoteMirrorType)mirrorType |setRemoteVideoMirrorType:(NSString\* _Nonnull)streamId withMirrorType:(ByteRTCRemoteMirrorType)mirrorType |Parameter change: Replace RemoteStreamKey with streamId |
|ByteRTCEngine |sendSEIMessage:(ByteRTCStreamIndex)streamIndex andMessage:(NSData\* _Nonnull)message andRepeatCount:(int)repeatCount andCountPerFrame:(ByteRTCSEICountPerFrame) mode |sendSEIMessage: (NSData\* _Nonnull)message andRepeatCount:(int)repeatCount andCountPerFrame:(ByteRTCSEICountPerFrame) mode |Parameter change: Remove StreamIndex parameter |
|ByteRTCEngine |startFileRecording:(ByteRTCStreamIndex)streamIndex withRecordingConfig:(ByteRTCRecordingConfig\* *Nonnull)recordingConfig type:(ByteRTCRecordingType)recordingType NS_SWIFT_NAME(startFileRecording(* :withRecordingConfig:type:)) |startFileRecording: (ByteRTCRecordingConfig\* _Nonnull)recordingConfig type:(ByteRTCRecordingType)recordingType NS_SWIFT_NAME(startFileRecording(withRecordingConfig:type:)) |Parameter change: Remove StreamIndex parameter |
|ByteRTCEngine |stopFileRecording:(ByteRTCStreamIndex)streamIndex |stopFileRecording |Parameter change: Remove StreamIndex parameter |
|ByteRTCEngine |setRemoteAudioPlaybackVolume:(ByteRTCRemoteStreamKey\* _Nonnull)streamKey volume:(int)volume; |setRemoteAudioPlaybackVolume:(NSString\* _Nonnull)streamId volume:(int)volume |Parameter change: Replace RemoteStreamKey with streamId |
|ByteRTCEngine |pushExternalEncodedVideoFrame:(ByteRTCStreamIndex)streamIndex withVideoIndex:(NSInteger)videoIndex withEncodedVideoFrame:(ByteRTCEncodedVideoFrame\* *Nonnull)videoFrame NS_SWIFT_NAME(pushExternalEncodedVideoFrame(* :withVideoIndex:withEncodedVideoFrame:)) |pushExternalEncodedVideoFrame: (NSInteger)videoIndex withEncodedVideoFrame:(ByteRTCEncodedVideoFrame\* _Nonnull)videoFrame NS_SWIFT_NAME(pushExternalEncodedVideoFrame(withVideoIndex:withEncodedVideoFrame:)) |Parameter change: Replace StreamIndex with videoIndex |
|ByteRTCEngine |setVideoDecoderConfig:(ByteRTCRemoteStreamKey \* *Nonnull)key withVideoDecoderConfig:(ByteRTCVideoDecoderConfig)config NS_SWIFT_NAME(setVideoDecoderConfig(* :withVideoDecoderConfig:)) |setVideoDecoderConfig:(NSString\* *Nonnull)streamId withVideoDecoderConfig:(ByteRTCVideoDecoderConfig)config NS_SWIFT_NAME(setVideoDecoderConfig(* :withVideoDecoderConfig:)) |Parameter change: Replace RemoteStreamKey with streamId |
|ByteRTCEngine |requestRemoteVideoKeyFrame:(ByteRTCRemoteStreamKey \* _Nonnull)key |requestRemoteVideoKeyFrame:(NSString\* _Nonnull)streamId |Parameter change: Replace RemoteStreamKey with streamId |
|ByteRTCEngine |setVideoWatermark:(ByteRTCStreamIndex)streamIndex withImagePath:(NSString \* _Nullable)imagePath withRtcWatermarkConfig:(ByteRTCVideoWatermarkConfig\* _Nonnull)rtcWatermarkConfig |setVideoWatermark: (NSString \* _Nullable)imagePath withRtcWatermarkConfig:(ByteRTCVideoWatermarkConfig\* _Nonnull)rtcWatermarkConfig |Parameter change: Remove StreamIndex parameter |
|ByteRTCEngine |clearVideoWatermark:(ByteRTCStreamIndex)streamIndex NS_SWIFT_NAME(clearVideoWatermark(_:)) |clearVideoWatermark |Parameter change: Remove StreamIndex parameter |
|ByteRTCEngine |takeLocalSnapshot:(ByteRTCStreamIndex)streamIndex callback:(id_Nullable)callback |takeLocalSnapshot:(id_Nullable)callback |Parameter change: Remove StreamIndex parameter |
|ByteRTCEngine |takeRemoteSnapshot:(ByteRTCRemoteStreamKey\* _Nonnull)streamKey callback:(id_Nullable)callback |takeRemoteSnapshot:(NSString\* _Nonnull)streamId callback:(id_Nullable)callback |Parameter change: Replace RemoteStreamKey with streamId |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserStartVideoCapture:(NSString \* _Nonnull)roomId uid:(NSString \* _Nonnull)uid |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserStartVideoCapture:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info |Parameter change: Replace roomId and userId with streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserStopVideoCapture:(NSString \* _Nonnull)roomId uid:(NSString \* _Nonnull)uid |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserStopVideoCapture:(NSString \* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info |Parameter change: Replace roomId and userId with streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserStartAudioCapture:(NSString\* _Nonnull)roomId uid:(NSString \*_Nonnull)userId |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserStartAudioCapture:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info |Parameter change: Replace roomId and userId with streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserStopAudioCapture:(NSString\* _Nonnull)roomId uid:(NSString \*_Nonnull)userId |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onUserStopAudioCapture:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info· |Parameter change: Replace roomId and userId with streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onLocalAudioStateChanged:(ByteRTCLocalAudioStreamState)state error:(ByteRTCLocalAudioStreamError)error |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onLocalAudioStateChanged:(NSString \*_Nonnull)streamId info:(ByteRTCStreamInfo \*_Nonnull)info state:(ByteRTCLocalAudioStreamState)state error:(ByteRTCLocalAudioStreamError)error |Parameter change: Add streamId and streamInfo parameters |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \*\*Nonnull)engine onLocalVideoStateChanged:(ByteRTCStreamIndex)streamIndex withStreamState:(ByteRTCLocalVideoStreamState)state withStreamError:(ByteRTCLocalVideoStreamError)error NS_SWIFT_NAME(rtcEngine(\*:onLocalVideoStateChanged:withStreamState:withStreamError:)) |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onLocalVideoStateChanged:(NSString  *_Nonnull)streamId info:(ByteRTCStreamInfo \*\*Nonnull)info withStreamState:(ByteRTCLocalVideoStreamState)state withStreamError:(ByteRTCLocalVideoStreamError)error NS_SWIFT_NAME(rtcEngine(* :onLocalVideoStateChanged:info:withStreamState:withStreamError:)) |Parameter change: Replace streamIndex with streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onRemoteAudioStateChanged:(ByteRTCRemoteStreamKey \* _Nonnull)key state:(ByteRTCRemoteAudioState)state reason:(ByteRTCRemoteAudioStateChangeReason)reason |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onRemoteAudioStateChanged:(NSString \*_Nonnull)streamId info:(ByteRTCStreamInfo \*_Nonnull)info state:(ByteRTCRemoteAudioState)state reason:(ByteRTCRemoteAudioStateChangeReason)reason |Parameter change: Replace RemoteStreamKey with streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine  *_Nonnull)engine onRemoteVideoStateChanged:(ByteRTCRemoteStreamKeyNonnull)streamKey withVideoState:(ByteRTCRemoteVideoState)state withVideoStateReason:(ByteRTCRemoteVideoStateChangeReason)reason NS_SWIFT_NAME(rtcEngine(* :onRemoteVideoStateChanged:withVideoState:withVideoStateReason:)) |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onRemoteVideoStateChanged:(NSString  *_Nonnull)streamId info:(ByteRTCStreamInfo \*\*Nonnull)info withVideoState:(ByteRTCRemoteVideoState)state withVideoStateReason:(ByteRTCRemoteVideoStateChangeReason)reason NS_SWIFT_NAME(rtcEngine(* :onRemoteVideoStateChanged:withVideoState:withVideoStateReason:)) |Parameter change: Replace RemoteStreamKey with streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onFirstLocalVideoFrameCaptured:(ByteRTCStreamIndex)streamIndex withFrameInfo:(ByteRTCVideoFrameInfo \* *Nonnull)frameInfo NS_SWIFT_NAME(rtcEngine(* :onFirstLocalVideoFrameCaptured:withFrameInfo:)) |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onFirstLocalVideoFrameCaptured:(ByteRTCVideoSource\* _Nullable)videoSource withFrameInfo:(ByteRTCVideoFrameInfo \* *Nonnull)frameInfo NS_SWIFT_NAME(rtcEngine(* :onFirstLocalVideoFrameCaptured:withFrameInfo:)) |Parameter change: Replace streamIndex with VideoSource |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine  *_Nonnull)engine onLocalVideoSizeChanged:(ByteRTCStreamIndex)streamIndex withFrameInfo:(ByteRTCVideoFrameInfo \*\*Nonnull)frameInfo NS_SWIFT_NAME(rtcEngine(* :onLocalVideoSizeChanged:withFrameInfo:)) |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onLocalVideoSizeChanged:(ByteRTCVideoSource  *_Nullable)videoSource withFrameInfo:(ByteRTCVideoFrameInfo \*\*Nonnull)frameInfo NS_SWIFT_NAME(rtcEngine(* :onLocalVideoSizeChanged:withFrameInfo:)) |Parameter change: Replace streamIndex with VideoSource |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onRemoteVideoSizeChanged:(ByteRTCRemoteStreamKey  *_Nonnull)streamKey withFrameInfo:(ByteRTCVideoFrameInfo \*\*Nonnull)frameInfo NS_SWIFT_NAME(rtcEngine(* :onRemoteVideoSizeChanged:withFrameInfo:)) |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onRemoteVideoSizeChanged:(NSString \*_Nonnull)streamId info:(ByteRTCStreamInfo  *_Nonnull)info withFrameInfo:(ByteRTCVideoFrameInfo \*\*Nonnull)frameInfo NS_SWIFT_NAME(rtcEngine(* :onRemoteVideoSizeChanged:withFrameInfo:)) |Parameter change: Replace RemoteStreamKey with streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onFirstLocalAudioFrame:(ByteRTCStreamIndex) streamIndex |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onFirstLocalAudioFrame:(ByteRTCAudioSource\* _Nullable)audioSource |Parameter change: Replace streamIndex with AudioSource |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onSEIMessageReceived:(ByteRTCRemoteStreamKey\* _Nonnull)remoteStreamKey andMessage:(NSData\* _Nonnull)message |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onSEIMessageReceived:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info andMessage:(NSData\* _Nonnull)message |Parameter change: Replace RemoteStreamKey with streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onSEIStreamUpdate:(ByteRTCRemoteStreamKey\* _Nonnull)remoteStreamKey eventType:(ByteRTCSEIStreamEventType)eventType |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onSEIStreamUpdate:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info eventType:(ByteRTCSEIStreamEventType)eventType |Parameter change: Replace RemoteStreamKey with streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine\* _Nonnull)engine onRecordingStateUpdate:(ByteRTCStreamIndex)type state:(ByteRTCRecordingState)state error_code:(ByteRTCRecordingErrorCode)errorCode recording_info:(ByteRTCRecordingInfo\* _Nonnull)recordingInfo |rtcEngine:(ByteRTCEngine\* _Nonnull)engine onRecordingStateUpdate:(ByteRTCVideoSource\* _Nullable)videoSource state:(ByteRTCRecordingState)state error_code:(ByteRTCRecordingErrorCode)errorCode recording_info:(ByteRTCRecordingInfo\* _Nonnull)recordingInfo |Parameter change: Replace streamIndex with VideoSource |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine\* _Nonnull)engine onRecordingProgressUpdate:(ByteRTCStreamIndex)type process:(ByteRTCRecordingProgress\* _Nonnull)process recording_info:(ByteRTCRecordingInfo\* _Nonnull)recordingInfo |rtcEngine:(ByteRTCEngine\* _Nonnull)engine onRecordingProgressUpdate:(ByteRTCVideoSource\* _Nullable)videoSource process:(ByteRTCRecordingProgress\* _Nonnull)process recording_info:(ByteRTCRecordingInfo\* _Nonnull)recordingInfo |Parameter change: Replace streamIndex with VideoSource |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onStreamSyncInfoReceived:(ByteRTCRemoteStreamKey\* _Nonnull)remoteStreamKey streamType:(ByteRTCSyncInfoStreamType)streamType data:(NSData\* _Nonnull)data |rtcEngine:(ByteRTCEngine \* _Nonnull)engine onStreamSyncInfoReceived:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info streamType:(ByteRTCSyncInfoStreamType)streamType data:(NSData\* _Nonnull)data |Parameter change: Replace RemoteStreamKey with streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onAudioFrameSendStateChanged:(NSString \* _Nonnull)roomId rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFrameSendState)state |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onAudioFrameSendStateChanged:(NSString \* _Nonnull)streamId info:(ByteRTCStreamInfo \*_Nonnull)info rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFrameSendState)state |Parameter change: Replace roomId with streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onVideoFrameSendStateChanged:(NSString \* _Nonnull)roomId rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFrameSendState)state |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onVideoFrameSendStateChanged:(NSString \* _Nonnull)streamId info:(ByteRTCStreamInfo \*_Nonnull)info rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFrameSendState)state; |Parameter change: Replace roomId with streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onAudioFramePlayStateChanged:(NSString \* _Nonnull)roomId rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFramePlayState)state |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onAudioFramePlayStateChanged:(NSString \* _Nonnull)streamId info:(ByteRTCStreamInfo \*_Nonnull)info rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFramePlayState)state |Parameter change: Replace roomId with streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onVideoFramePlayStateChanged:(NSString \* _Nonnull)roomId rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFramePlayState)state |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onVideoFramePlayStateChanged:(NSString \* _Nonnull)streamId info:(ByteRTCStreamInfo \*_Nonnull)info rtcUser:(ByteRTCUser \*_Nonnull)user state:(ByteRTCFirstFramePlayState)state |Parameter change: Replace roomId with streamId and streamInfo |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onSimulcastSubscribeFallback:(ByteRTCRemoteStreamSwitchEvent \*_Nonnull)event |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onSimulcastSubscribeFallback:(NSString  *_Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info event:(ByteRTCRemoteStreamSwitchEvent \*_Nonnull)event |Parameter change: Add streamId and streamInfo parameters |
|ByteRTCEngineDelegate |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onPerformanceAlarms:(ByteRTCPerformanceAlarmMode)mode roomId:(NSString \*_Nonnull)roomId reason:(ByteRTCPerformanceAlarmReason)reason sourceWantedData:(ByteRTCSourceWantedData \*_Nonnull)data |rtcEngine:(ByteRTCEngine \*_Nonnull)engine onPerformanceAlarms:(NSString  *_Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info mode:(ByteRTCPerformanceAlarmMode)mode reason:(ByteRTCPerformanceAlarmReason)reason sourceWantedData:(ByteRTCSourceWantedData \*_Nonnull)data |Parameter change: Add streamId and streamInfo parameters |
|ByteRTCRoomDelegate |rtcRoom:( ByteRTCRoom  *_Nonnull)rtcRoom onLocalStreamStats:(ByteRTCLocalStreamStats \*\*Nonnull)stats NS_SWIFT_NAME(rtcRoom(* :onLocalStreamStats:)) |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onLocalStreamStats:(NSString \*_Nonnull)streamId info:(ByteRTCStreamInfo  *_Nonnull)info stats:(ByteRTCLocalStreamStats \*\*Nonnull)stats NS_SWIFT_NAME(rtcRoom(* :onLocalStreamStats:)) |Parameter change: Add streamId and streamInfo parameters |
|ByteRTCRoomDelegate |rtcRoom:( ByteRTCRoom  *_Nonnull)rtcRoom onRemoteStreamStats:(ByteRTCRemoteStreamStats \*\*Nonnull)stats NS_SWIFT_NAME(rtcRoom(* :onRemoteStreamStats:)) |rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onRemoteStreamStats:(NSString \*_Nonnull)streamId info:(ByteRTCStreamInfo  *_Nonnull)info stats:(ByteRTCRemoteStreamStats \*\*Nonnull)stats NS_SWIFT_NAME(rtcRoom(* :onRemoteStreamStats:)) |Parameter change: Add streamId and streamInfo parameters |
|LocalEncodedVideoFrameObserverObjC : ILocalEncodedVideoFrameObserver |onLocalEncodedVideoFrame:(ByteRTCStreamIndex) streamIndex Frame:(ByteRTCEncodedVideoFrame \* _Null_unspecified)frame |onLocalEncodedVideoFrame:(ByteRTCVideoSource\* _Nullable)videoSource Frame:(ByteRTCEncodedVideoFrame \* _Null_unspecified)frame |Parameter change: Replace streamIndex with VideoSource |
|RemoteEncodedVideoFrameObserverObjC : IRemoteEncodedVideoFrameObserver |onRemoteEncodedVideoFrame:(ByteRTCRemoteStreamKey \* _Nonnull)streamKey withEncodedVideoFrame:(ByteRTCEncodedVideoFrame\* _Nonnull)videoFrame |onRemoteEncodedVideoFrame:(NSString\*)streamId info:(ByteRTCStreamInfo \* _Nonnull)info withEncodedVideoFrame:(ByteRTCEncodedVideoFrame\* _Nonnull)videoFrame |Parameter change: Replace RemoteStreamKey with streamId and streamInfo |
|SnapshotResultObjC : ISnapshotResultCallback |onTakeLocalSnapshotResult:(NSInteger) taskId streamIndex:(ByteRTCStreamIndex)streamIndex image:(ByteRTCImage \* _Nullable)image errorCode:(NSInteger)errorCode |onTakeLocalSnapshotResult:(NSInteger) taskId videoSource:(ByteRTCVideoSource \* _Nullable)videoSource image:(ByteRTCImage \* _Nullable)image errorCode:(NSInteger)errorCode |Parameter change: Replace streamIndex with VideoSource |
|SnapshotResultObjC : ISnapshotResultCallback |onTakeRemoteSnapshotResult:(NSInteger)taskId streamKey:(ByteRTCRemoteStreamKey \* _Nonnull)streamKey image:(ByteRTCImage \* _Nullable)image errorCode:(NSInteger)errorCode |onTakeRemoteSnapshotResult:(NSInteger)taskId streamId:(NSString\*)streamId info:(ByteRTCStreamInfo \* _Nonnull)info image:(ByteRTCImage \* _Nullable)image errorCode:(NSInteger)errorCode |Parameter change: Replace RemoteStreamKey with streamId and streamInfo |
|ByteRTCAudioFrameObserver : IAudioFrameObserver |onRemoteUserAudioFrame:(ByteRTCRemoteStreamKey \* _Nonnull)streamKey audioFrame:(ByteRTCAudioFrame \* _Nonnull)audioFrame |onRemoteUserAudioFrame:(NSString \* _Nonnull)streamId info:(ByteRTCStreamInfo \* _Nonnull)info audioFrame:(ByteRTCAudioFrame \* _Nonnull)audioFrame |Parameter change: Replace RemoteStreamKey with streamId and streamInfo |
|ByteRtcAudioFrameProcessorOCC : IAudioFrameProcessor |onProcessRemoteUserAudioFrame:(ByteRTCRemoteStreamKey \* _Nonnull)streamKey audioFrame:(ByteRTCAudioFrame \* _Nonnull)audioFrame |onProcessRemoteUserAudioFrame:(NSString \* _Nonnull)streamId info:(ByteRTCStreamInfo \* _Nonnull)info audioFrame:(ByteRTCAudioFrame \* _Nonnull)audioFrame |Parameter change: Replace RemoteStreamKey with streamId and streamInfo |
|ExternalVideoEncoderEventHandlerObjC : IExternalVideoEncoderEventHandler |onStart:(ByteRTCStreamIndex)streamIndex |onStart:(NSString\*)streamId info:(ByteRTCStreamInfo \* _Nonnull)info |Parameter change: Replace streamIndex with streamId and streamInfo |
|ExternalVideoEncoderEventHandlerObjC : IExternalVideoEncoderEventHandler |onStop:(ByteRTCStreamIndex)streamIndex |onStop:(NSString\*)streamId info:(ByteRTCStreamInfo \* _Nonnull)info |Parameter change: Replace streamIndex with streamId and streamInfo |
|ExternalVideoEncoderEventHandlerObjC : IExternalVideoEncoderEventHandler |onRateUpdate:(ByteRTCStreamIndex)streamIndex withVideoIndex:(NSInteger)videoIndex withFps:(NSInteger)fps withBitRate:(NSInteger)bitRateKps |onRateUpdate:(NSString\*)streamId info:(ByteRTCStreamInfo \* _Nonnull)info withVideoIndex:(NSInteger)videoIndex withFps:(NSInteger)fps withBitRate:(NSInteger)bitRateKps |Parameter change: Replace streamIndex with streamId and streamInfo |
|ExternalVideoEncoderEventHandlerObjC : IExternalVideoEncoderEventHandler |onRequestKeyFrame:(ByteRTCStreamIndex)streamIndex withVideoIndex:(NSInteger)videoIndex |onRequestKeyFrame:(NSString\*)streamId info:(ByteRTCStreamInfo \* _Nonnull)info withVideoIndex:(NSInteger)videoIndex |Parameter change: Replace streamIndex with streamId and streamInfo |
|ExternalVideoEncoderEventHandlerObjC : IExternalVideoEncoderEventHandler |onActiveVideoLayer:(ByteRTCStreamIndex)streamIndex withVideoIndex:(NSInteger)videoIndex withActive:(BOOL)active |onActiveVideoLayer:(NSString\*)streamId info:(ByteRTCStreamInfo \* _Nonnull)info withVideoIndex:(NSInteger)videoIndex withActive:(BOOL)active |Parameter change: Replace streamIndex with streamId and streamInfo |


<span id="c36f017a"></span>
## Type Changes

<span id="faf266df"></span>
### Room Profile


|Changed Data Type |V3.58 |V3.60 |Description |
|---|---|---|---|
|ByteRTCRoomProfile |* ByteRTCRoomProfileChat = 5<br><br>* ByteRTCRoomProfileLwTogether = 7 |ByteRTCRoomProfileCall = 19 |Prioritizes smoothness with relatively low default video bitrate, low audio quality requirements, and high smoothness requirements. |
||* ByteRTCRoomProfileGameHD = 8<br><br>* ByteRTCRoomProfileCoHost = 9<br><br>* ByteRTCRoomProfileKTV = 11<br><br>* ByteRTCRoomProfileVRChat = 13<br><br>* ByteRTCRoomProfileLanLiveStreaming = 15<br><br>* ByteRTCRoomProfileLiveBroadcasting = 1 |ByteRTCRoomProfileLive = 20 |Prioritizes video quality with relatively high default video bitrate and high audio quality requirements. |


<span id="caad93cb"></span>
### Video Frame Related


|Function |V3.58 |V3.60 |Description |
|---|---|---|---|
|Video frame data |ByteRTCVideoFrame |ByteRTCVideoFrameData |1. **Type rename**<br><br>2. **Parameter change**:<br><br>* Remove supplementaryInfo<br><br>* Remove colorSpace<br><br>* time changed to timestamp<br><br>* planeDatas changed to planeDataArray<br><br>* planeStrides changed to planeStrideArray<br><br>* extendedData changed to seiData<br><br>* Add bufferType<br><br>* Add format<br><br>* Add addRef<br><br>* Add releaseRef |
|*Remote video frame callback position* |ByteRTCRemoteVideoRenderPosition |ByteRTCRemoteVideoSinkPosition |Type rename |
|*Whether to mirror video frame* |ByteRTCVideoRenderMirrorType |ByteRTCVideoSinkMirrorType |Type rename |


<span id="20427bdc"></span>
### Mixed Stream Push Events


* Name replacement: `ByteRTCStreamMixingEvent` changed to `ByteRTCMixedStreamTaskEvent`, sharing the same event enumeration class with WTN stream tasks.

* Enumeration value changes as follows:



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
|Mixed stream with image |ByteRTCStreamMixingEventMixImage = 16 |ByteRTCMixedStreamTaskEventWarning = 7 |
|Warning event |None |ByteRTCMixedStreamTaskEventWarning = 7 |
|Others |ByteRTCStreamMixingEventChangeMixType = 10<br><br>ByteRTCStreamMixingEventFirstAudioFrameByClientMixer = 11<br><br>ByteRTCStreamMixingEventFirstVideoFrameByClientMixer = 12 |Removed |


<span id="6cd67708"></span>
### Single Stream Push Task Events


* Name change: Changed from `ByteRTCSingleStreamPushEvent` to `ByteRTCSingleStreamTaskEvent`.

* Specific enumeration value changes as follows



|Description |V3.58 |V3.60 |
|---|---|---|
|Start push stream |ByteRTCSingleStreamPushEventStart = 1 |ByteRTCSingleStreamTaskEventStartSuccess = 1 |
|Push stream success |ByteRTCSingleStreamPushEventStartSuccess = 2 |ByteRTCSingleStreamTaskEventStartSuccess = 1 |
|Push stream failed |ByteRTCSingleStreamPushEventStartFailed = 3 |ByteRTCSingleStreamTaskEventStartFailed = 2 |
|Stop push stream |ByteRTCSingleStreamPushEventStop = 4 |ByteRTCSingleStreamTaskEventStopSuccess = 3 |
|Single stream push live task processing timeout, check network status and retry |ByteRTCSingleStreamPushEventTimeout = 5 |ByteRTCSingleStreamTaskEventWarning = 5, for specific error information see ByteRTCSingleStreamTaskErrorCode. |
|Parameter error |ByteRTCSingleStreamPushEventParamError = 6 |Returns ByteRTCReturnStatusParameterErr = \-2 when calling startPushSingleStream:singleStream:. |
|Stop push stream failed |None |ByteRTCSingleStreamTaskEventStopFailed = 4 |


<span id="1f5af844"></span>
### Audio and Video Stream Statistics


|Function |Modified data type |Description |
|---|---|---|
|Local audio stream statistics |ByteRTCLocalAudioStats |Add fields audioDeviceLoopDelay (audio capture and playback delay), encodeFrameRate (audio encoding frame rate) |
|Remote audio stream statistics |ByteRTCRemoteAudioStats |Add field decodeFrameRate (audio decoding frame rate) |
|Remote video stream statistics |ByteRTCRemoteVideoStats |Add fields capToRenderDelay (delay from sender capture start to receiver rendering completion), avSyncDiffMs (audio\-video synchronization difference), codecElapsePerFrame (average video decoding time) |


<span id="c7a739a5"></span>
### Others


|Function |Name |Description |
|---|---|---|
|Publish state change reason |ByteRTCPublishStateChangeReason |**New class** |
|Screenshot error code |ByteRTCSnapshotErrorCode |**New enumeration**<br><br>Screenshot success (0, ByteRTCSnapshotErrorCodeOk)<br><br>Screenshot error. Failed to generate image data or RGBA encoding failed (\-1, ByteRTCSnapshotErrorCodeCreateFail)<br><br>Screenshot error. Stream invalid (\-2, ByteRTCSnapshotErrorCodeStreamInvalid)<br><br>Screenshot error. Screenshot timeout, timeout duration 1 second (\-3, ByteRTCSnapshotErrorCodeTimeout)<br><br>Screenshot error. Image save failed (\-4, ByteRTCSnapshotErrorCodeFileSaveError) |
|Audio scenario type |ByteRTCAudioScenarioType |**Enumeration value added**<br><br>Education scenario. Suitable for high\-quality scenarios mainly focused on voice teaching content (4, ByteRTCAudioScenarioTypeEducation)<br><br>AI conversation scenario (5, ByteRTCAudioScenarioTypeAiClient) |
|Ear monitor Audio Filter type |ByteRTCEarMonitorAudioFilter |**New enumeration**<br><br>No Audio Filter (default setting) (0x0001, ByteRTCEarMonitorAudioFilterNone)<br><br>Ear monitor reuses 3A processing (0x8000, ByteRTCEarMonitorAudioFilterReuseAudioProcessing) |
|Single stream push live error code |ByteRTCSingleStreamTaskErrorCode |**Enumeration value added**<br><br>Server detects invalid task parameters (1093, ByteRTCSingleStreamTaskErrorCodeInvalidParamByServer)<br><br>Push task user ID in target room was kicked out of target room (1094, ByteRTCSingleStreamTaskErrorCodeRemoteKicked)<br><br>Push task failed to join target room (1095, ByteRTCSingleStreamTaskErrorCodeJoinDestRoomFailed)<br><br>Push task pull stream timeout in source room (1096, ByteRTCSingleStreamTaskErrorCodeReceiveSrcStreamTimeout)<br><br>Audio and video encoding push task not supported (1097, ByteRTCSingleStreamTaskErrorCodeNotSurportCodec) |
|Single stream push configuration target room information |DestInfo |**New class** |
|Single stream push type |ByteRTCSingleStreamPushType |**Enumeration added**<br><br>Single stream push to CDN (1, ByteRTCSingleStreamPushToCDN)<br><br>Single stream push to RTC room (2, ByteRTCSingleStreamPushToRTC) |
|Single stream push live configuration parameters |ByteRTCPushSingleStreamParam |**Member added**<br><br>Added to single stream push live configuration parameters: target room information list for single stream push configuration (destInfo), push type (pushType) two members |
|Mirror type |ByteRTCMirrorType |**Enumeration value added**<br><br>No mirror effect during local preview, mirror effect only during encoding transmission (2, ByteRTCMirrorTypeEncoder) |


<span id="65f4c413"></span>
## Error Code Changes

<span id="3593d5f4"></span>
### Callback Warning \- WarningCode


|V3.58 |V3.60 |
|---|---|
|ByteRTCWarningCodeOldRoomBeenReplaced = \-2016 |**Removed**:<br><br>When creating a room again with the same roomId, the previously created room instance will be returned, and this error code will no longer be triggered. |


<span id="53943359"></span>
### WTN stream (formerly public stream)


* Error code name change: `ByteRTCPublicStreamErrorCode` changed to `ByteRTCMixedStreamTaskErrorCode`, sharing the same enumeration class with mixed stream push tasks.

* Specific error code change details as follows:



|Description |V3.58 |V3.60 |
|---|---|---|
|Success |ByteRTCPublicStreamErrorCodeSuccess = 0 |ByteRTCMixedStreamTaskErrorCodeOK = 0 |
|Server parameter validation failed |ByteRTCPublicStreamErrorCodePushParamError = 1191 |Deleted, this type of error will not be called back. |
|Server internal error |ByteRTCPublicStreamErrorCodePushStatusError = 1192 Deleted, this type of error will not be called back. |ByteRTCMixedStreamTaskErrorCodeInvalidStateByServer = 1094 |
|Server unknown error |ByteRTCPublicStreamErrorCodePushInternalError = 1193 Deleted, this type of error will not be called back. |ByteRTCMixedStreamTaskErrorCodeUnKnownErrorByServer = 1096 |
|Task failed |ByteRTCPublicStreamErrorCodePushError = 1195 |ByteRTCMixedStreamTaskErrorCodePushWTNFailed = 1195 |
|Task timeout |ByteRTCPublicStreamErrorCodePushTimeOut = 1196 |ByteRTCMixedStreamTaskErrorCodeTimeOut = 1091 |
|Stream subscription timeout |ByteRTCPublicStreamErrorCodePullNoPushStream = 1300 |ByteRTCWTNSubscribeStateChangeReason.ByteRTCWTNSubscribeStateChangeReasonUnsubscribe = 1300, returned through onWTNVideoSubscribeStateChanged:state:reason: or onWTNAudioSubscribeStateChanged:state:reason:. |


<span id="ccd1a68b"></span>
### Mixed Stream Push Error Codes


* Error code name change: `ByteRtcTranscoderErrorCode` changed to `ByteRTCMixedStreamTaskErrorCode`, sharing the same enumeration class with WTN stream tasks.

* Specific error code change details as follows:



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
|Server receiving signaling timeout, check network status and retry |ByteRtcTranscoderErrorCodeTimeoutBySignaling = 1099 |ByteRTCMixedStreamTaskErrorCodeSignalRequestTimeout = 1097 |
|Image mixed stream failed |ByteRtcTranscoderErrorCodeMixImageFail = 1100 |ByteRTCMixedStreamTaskErrorCodeMixImageFailed = 1098 |
|Server unknown error |ByteRtcTranscoderErrorCodeUnKnownErrorByServer = 1101 |ByteRTCMixedStreamTaskErrorCodeUnKnownErrorByServer = 1096 |


<span id="8715857c"></span>
### Single Stream Push Error Codes


* Error code replacement: Replaced `ByteRTCTranscoderErrorCode` with `ByteRTCSingleStreamTaskErrorCode`.

* Specific error code changes and corresponding details as follows:



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
|Server receiving signaling timeout, check network status and retry |TRANSCODER_ERROR_TIMEOUT_BY_SIGNALING = 1099 |ByteRTCSingleStreamTaskErrorCodeSignalRequestTimeout = 1092 |
|Image mixed stream failed |TRANSCODER_ERROR_MIX_IMAGE_FAIL = 1100 |None, single stream tasks will not trigger this error code. |
|Server unknown error |TRANSCODER_ERROR_UNKNOW_ERROR_BY_SERVER = 1101 |ByteRTCSingleStreamTaskErrorCodeUnknownByServer = 1091 |


<span id="20b69dfe"></span>
### Other Error Codes

Removed some error codes that have been deprecated for multiple versions


|Description |Error code |
|---|---|
|This warning is triggered when attempting to publish a stream after setting self visibility to false. |ByteRTCWarningCodePublishStreamForbiden = \-2010 |
|This warning is triggered when attempting to enable manual subscription mode while automatic subscription mode is not turned off. |ByteRTCWarningCodeGetRoomFailed = \-2000 |


<span id="75b5ebca"></span>
## New Interfaces


|**Interface** |**Function Description** |
|---|---|
|createRTSRoom: |Create RTS room |
|pushReferenceAudioPCMData: |Push external audio reference frame to SDK |
|getCallId |Get call ID. This method needs to be called after joining the room |
|onRemoteEncodedAudioFrame:info:audioFrame: |After calling RegisterRemoteEncodedAudioFrameObserver, this event is called back when the SDK receives remote audio frame information |
|takeLocalSnapshotToFile: |Capture local video stream screen, generate JPG file, and save to specified local path. |
|takeRemoteSnapshotToFile:filePath: |Capture remote video stream screen, generate JPG file, and save to specified local path. |
|rtcEngine:onLocalSnapshotTakenToFile:filePath:width:height:errorCode:taskId: |When capturing video screen with takeSnapshotToFile:filePath:, this callback is received to report whether the screenshot is successful and the captured image information. |
|rtcEngine:onRemoteSnapshotTakenToFile:info:filePath:width:height:errorCode:taskId: |When capturing video screen with takeSnapshotToFile:filePath:, this callback is received to report whether the screenshot is successful and the captured image information. |
|setEarMonitorMode:filter: |Ear monitor supports reusing locally captured audio after custom processing |
|setWTNStreamDelegate: |Set WTN stream callback interface |
|rtcRoom:onRoomEvent:uid:state:info: |Room event callback, with new enum ByteRTCRoomEventInfo |
|setStreamExtraInfo: |Set stream additional information for current push stream |
|rtcRoom:onRoomStreamExtraInfoUpdate:info:extraInfo: |Callback for receiving stream additional information set by other users calling setStreamExtraInfo in the same room. |
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


<span id="c3615e06"></span>
## Deleted/Deprecated Interfaces

Removed deprecated or not recommended methods, as follows:


|**Function** |**Deleted/Deprecated Interface** |**Alternative Interface** |
|---|---|---|
|Deprecated |* (int)setLocalVideoSink:(ByteRTCStreamIndex)index withSink:(id*Nullable)videoSink withPixelFormat:(ByteRTCVideoSinkPixelFormat)requiredFormat NS_SWIFT_NAME(setLocalVideoSink(* :withSink:withPixelFormat:)); |* (int)setLocalVideoSink:(id_Nullable)videoSink withPixelFormat:(ByteRTCVideoSinkPixelFormat)requiredFormat NS_SWIFT_NAME(setLocalVideoSink(withSink:withPixelFormat:)) |
|Deprecated |* (int)setRemoteVideoSink:(ByteRTCRemoteStreamKey\* _Nonnull)streamKey withSink:(id*Nullable)videoSink withPixelFormat:(ByteRTCVideoSinkPixelFormat)requiredFormat NS_SWIFT_NAME(setRemoteVideoSink(* :withSink:withPixelFormat:)) |* (int)setRemoteVideoSink:(NSString\* _Nonnull)streamId withSink:(id*Nullable)videoSink withPixelFormat:(ByteRTCVideoSinkPixelFormat)requiredFormat NS_SWIFT_NAME(setRemoteVideoSink(* :withSink:withPixelFormat:)) |
|Deleted |(RTCVideo \* _Nullable) createRTCVideo:(NSString \* _Nonnull)appId delegate:(id_Nullable)delegate parameters:(NSDictionary \* _Nonnull)parameters |(ByteRTCEngine \* _Nullable) createRTCEngine:(ByteRTCEngineConfig \* _Nonnull) config delegate:(id_Nullable)delegate |
|Deleted |getErrorDescription: |No alternative interface |
|Deleted |startASR:handler:<br><br>stopASR |No alternative interface<br><br>To use ASR functionality, it can be implemented through real\-time subtitle related interfaces: startSubtitle:, stopSubtitle |
|Deleted |onSuccessonMessage:rtcEngine:<br><br>onError: |To use ASR functionality, it can be implemented through real\-time subtitle related interfaces: rtcRoom:onSubtitleStateChanged:errorCode:errorMessage:<br><br>rtcRoom:onSubtitleMessageReceived: |
|Deleted |* (void)setDeviceId:(NSString\* _Nonnull) deviceID |No alternative interface |
|Deleted |\-(int)setAudioPlaybackDevice:(ByteRTCAudioPlaybackDevice)audioPlaybackDevice __deprecated_msg("Will be removed in new version") |* (int)setDefaultAudioRoute:(ByteRTCAudioRoute)audioRoute |
|Deleted |(void)rtcRoom:( ByteRTCRoom \*_Nonnull)rtcRoom onRoomError:(ByteRTCErrorCode)errorCode __deprecated_msg("Will be removed in new version") |* (void)rtcRoom:(ByteRTCRoom \*_Nonnull)rtcRoom onRoomStateChanged:(NSString \*_Nonnull)roomId withUid:(nonnull NSString \*)uid state:(NSInteger)state extraInfo:(NSString \*_Nonnull)extraInfo;<br><br>* (void)rtcRoom:(ByteRTCRoom \*_Nonnull)rtcRoom onStreamStateChanged:(NSString \*_Nonnull)roomId withUid:(nonnull NSString \*)uid state:(NSInteger)state extraInfo:(NSString \*_Nonnull)extraInfo |
|Deleted |(int)subscribeUserStream:(NSString \*_Nonnull)userId streamType:(ByteRTCStreamIndex)streamType mediaType:(ByteRTCSubscribeMediaType)mediaType videoConfig:(ByteRTCSubscribeVideoConfig \*_Nonnull)videoConfig __deprecated_msg("Will be removed in new version") |* (int)subscribeStreamVideo:(NSString \*_Nonnull)streamId subscribe:(BOOL)subscribe<br><br>* (int)subscribeStreamAudio:(NSString \*_Nonnull)streamId subscribe:(BOOL)subscribe |
|Deleted |1. \-(void)rtcEngine:(ByteRTCVideo \* _Nonnull)engine onUserMuteAudio:(NSString \* _Nonnull)roomId uid:(NSString \* _Nonnull)uid muteState:(ByteRTCMuteState)muteState __deprecated_msg("Will be removed in new version")<br><br>2. \-(void)rtcEngine:(ByteRTCVideo \* _Nonnull)engine onUserMuteVideo:(NSString \* _Nonnull)roomId uid:(NSString \* Nonnull)uid withMuteState:(ByteRTCMuteState)muteState NS_SWIFT_NAME(rtcEngine(:onUserMuteVideo:uid:withMuteState:)) __deprecated_msg("Will be removed in new version")<br><br>3. \-(void)rtcEngine:(ByteRTCVideo \* _Nonnull)engine onMediaDeviceStateChanged:(NSString\*_Nonnull)deviceID device_type:(ByteRTCMediaDeviceType)deviceType device_state:(ByteRTCMediaDeviceState)deviceState device_error:(ByteRTCMediaDeviceError)deviceError __attribute((deprecated("Will be removed in new version")))<br><br>4. \-(void)rtcEngine:(ByteRTCVideo \* _Nonnull)engine onMediaDeviceWarning:(NSString\*_Nonnull)deviceId deviceType:(ByteRTCMediaDeviceType)deviceType deviceWarning:(ByteRTCMediaDeviceWarning)deviceWarning __deprecated_msg("Will be removed in new version")<br><br>5. \-(void)rtcEngine:(ByteRTCVideo \* _Nonnull)engine onAudioPlaybackDeviceChanged:(ByteRTCAudioPlaybackDevice)device __deprecated_msg("Will be removed in new version")<br><br>6. \-(void)rtcEngine:(ByteRTCVideo \* _Nonnull)engine onAudioMixingStateChanged:(NSInteger)mixId state:(ByteRTCAudioMixingState)state error:(ByteRTCAudioMixingError)error<br><br>7. \-(void)rtcEngine:(ByteRTCVideo \*_Nonnull)engine onHttpProxyState:(NSInteger)state<br><br>8. \-(void)rtcEngine:(ByteRTCVideo \*_Nonnull)engine onSocks5ProxyState:(NSInteger)state cmd:(NSString \*_Nonnull)cmd proxy_address:(NSString \*_Nonnull)proxyAddress local_address:(NSString \*_Nonnull)localAddress remote_address:(NSString \*_Nonnull)remoteAddress |1. (void)rtcRoom:(ByteRTCRoom\* _Nonnull)rtcRoom onUserPublishStreamAudio:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info isPublish:(BOOL)isPublish<br><br>2. (void)rtcRoom:(ByteRTCRoom\* _Nonnull)rtcRoom onUserPublishStreamVideo:(NSString\* _Nonnull)streamId info:(ByteRTCStreamInfo\* _Nonnull)info isPublish:(BOOL)isPublish<br><br>3. (void)rtcEngine:(ByteRTCEngine \* _Nonnull)engine onAudioDeviceStateChanged:(NSString\*_Nonnull)deviceID device_type:(ByteRTCAudioDeviceType)deviceType device_state:(ByteRTCMediaDeviceState)deviceState device_error:(ByteRTCMediaDeviceError)deviceError<br><br>   * (void)rtcEngine:(ByteRTCEngine \* _Nonnull)engine onVideoDeviceStateChanged: (NSString\*_Nonnull)deviceID device_type: (ByteRTCVideoDeviceType)deviceType device_state:(ByteRTCMediaDeviceState)deviceState device_error:(ByteRTCMediaDeviceError)deviceError<br><br>4. (void)rtcEngine:(ByteRTCEngine \* _Nonnull)engine onAudioDeviceWarning:(NSString\*_Nonnull)deviceId deviceType:(ByteRTCAudioDeviceType)deviceType deviceWarning:(ByteRTCMediaDeviceWarning)deviceWarning<br><br>   * (void)rtcEngine:(ByteRTCEngine \* _Nonnull)engine onVideoDeviceWarning (NSString\*_Nonnull)deviceId deviceType:(ByteRTCVideoDeviceType)deviceType deviceWarning:(ByteRTCMediaDeviceWarning)deviceWarning<br><br>5. (void)rtcEngine:(ByteRTCEngine \*_Nonnull)engine onAudioRouteChanged:(ByteRTCAudioRoute)device<br><br>6. \-(void)onAudioEffectPlayerStateChanged:(int)effectId state:(ByteRTCPlayerState)state error:(ByteRTCPlayerError)error<br><br>   \-(void)onMediaPlayerStateChanged:(int)playerId state:(ByteRTCPlayerState)state error:(ByteRTCPlayerError)error<br><br>7. (void)rtcEngine:(ByteRTCVideo \* _Nonnull)engine onLocalProxyStateChanged:(ByteRTCLocalProxyType)type withProxyState:(ByteRTCLocalProxyState)state withProxyError:(ByteRTCLocalProxyError)error<br><br>8. (void)rtcEngine:(ByteRTCVideo \* _Nonnull)engine onLocalProxyStateChanged:(ByteRTCLocalProxyType)type withProxyState:(ByteRTCLocalProxyState)state withProxyError:(ByteRTCLocalProxyError)error |
|Deleted |1. \-(int)checkVideoEffectLicense:(NSString \* Nonnull)licenseFile NS_SWIFT_NAME(checkVideoEffectLicense(:)) __deprecated_msg("Will be removed in new version")<br><br>2. \-(void)setVideoEffectAlgoModelPath:(NSString \* _Nonnull)modelPath __deprecated_msg("Will be removed in new version")<br><br>3. \-(int)enableVideoEffect:(BOOL)enabled NS_SWIFT_NAME(enableVideoEffect(_:)) __deprecated_msg("Will be removed in new version")<br><br>4. (int) setVideoEffectNodes:(NSArray <NSString \*\> \*_Nonnull)effectNodePaths __deprecated_msg("Will be removed in new version")<br><br>5. \-(int) updateVideoEffectNode:(NSString \* _Nonnull)nodePath nodeKey:(NSString \* Nonnull)nodeKey nodeValue:(float) nodeValue NS_SWIFT_NAME(updateVideoEffectNode(:nodeKey:nodeValue:)) __deprecated_msg("Will be removed in new version")<br><br>6. \-(int) setVideoEffectColorFilter:(NSString \* _Nonnull)resPath __deprecated_msg("Will be removed in new version")<br><br>7. \-(int) setVideoEffectColorFilterIntensity:(float) intensity __deprecated_msg("Will be removed in new version")<br><br>8. \-(int) setBackgroundSticker:(NSString\* _Nullable)modelPath source:(ByteRTCVirtualBackgroundSource\* _Nonnull)source __deprecated_msg("Will be removed in new version")<br><br>9. \-(int) registerFaceDetectionObserver:(Nullable id)faceDetectionObserver withInterval:(NSInteger)interval NS_SWIFT_NAME(registerFaceDetectionObserver(:withInterval:)) __deprecated_msg("Will be removed in new version") |Beauty\-related APIs moved from ByteRTCEngine (formerly ByteRTCVideo) to ByteRTCVideoEffect:<br><br><br>1. (int) initCVResource:(NSString\* _Nonnull)licenseFile withAlgoModelDir: (NSString\* _Nonnull)algoModelDir<br><br>2. (int) initCVResource:(NSString\* _Nonnull)licenseFile withAlgoModelDir: (NSString\* _Nonnull)algoModelDir<br><br>3. (int) enableVideoEffect<br><br>4. (int) setEffectNodes:(NSArray<NSString\*\>\*_Nonnull)effect_nodes<br><br>5. (int) updateEffectNode:(NSString\* _Nonnull)node_path key:(NSString\* _Nonnull)key value:(float) value<br><br>6. (int) setColorFilter:(NSString\* _Nonnull)filter_res<br><br>7. (int) setColorFilterIntensity:(float) intensity<br><br>8. (int) enableVirtualBackground:(NSString\* _Nonnull)bg_sticker_res withSource:(ByteRTCVirtualBackgroundSource\* _Nonnull)source<br><br>9. (int) enableFaceDetection:(id)observer withInterval:(NSUInteger)interval withModelPath:(NSString \*)path |
|Deleted |1. \-(int)startLiveTranscoding:(NSString \* _Nonnull)taskID transcoding:(ByteRTCLiveTranscoding \*_Nullable)<br><br>2. \-(int)stopLiveTranscoding:(NSString \*_Nonnull)taskID __deprecated_msg("deprecated since 352, will be deleted in 358, use stopPushStreamToCDN instead")<br><br>3. \-(int)updateLiveTranscoding:(NSString \*_Nonnull)taskID transcoding:(ByteRTCLiveTranscoding \*_Nonnull)transcoding __deprecated_msg("deprecated since 352, will be deleted in 358, use updatePushMixedStreamToCDN instead") |1. (int)startPushMixedStream:(NSString \* _Nonnull)taskId withPushTargetConfig:(ByteRTCMixedStreamPushTargetConfig\*)pushTargetConfig withMixedConfig:(ByteRTCMixedStreamConfig \*_Nullable)config<br><br>2. (int)stopPushMixedStream:(NSString \*_Nonnull)taskId withPushTargetType:(ByteRTCMixedStreamPushTargetType)pushTargetType<br><br>3. (int)updatePushMixedStream:(NSString  *_Nonnull)taskId withPushTargetConfig:(ByteRTCMixedStreamPushTargetConfig*)pushTargetConfig withMixedConfig:(ByteRTCMixedStreamConfig \*_Nonnull)config |
|Deleted |ByteRTCAudioMixingManager |ByteRTCMediaPlayer<br><br>ByteRTCAudioEffectPlayer |
|Deleted |\-(int)muteAudioPlayback:(ByteRTCMuteState)muteState __deprecated_msg("Will be removed in new version") |* (int)setPlaybackVolume:(NSInteger)volume |
| |1. \-(int)updatePosition:(ByteRTCPosition\* _Nonnull) pos __deprecated_msg("deprecated since 352, use updateSelfPosition instead");<br><br>2. \-(int)updateSelfOrientation:(ByteRTCHumanOrientation\* _Nonnull) orientation __deprecated_msg("deprecated since 352, use updateSelfPosition instead");<br><br>3. \-(int)updateListenerPosition:(ByteRTCPosition\* _Nonnull) pos __deprecated_msg("deprecated since 352, use updateRemotePosition instead");<br><br>4. \-(int)updateListenerOrientation:(ByteRTCHumanOrientation\* _Nonnull)orientation __deprecated_msg("deprecated since 352, use updateRemotePosition instead") |1. \-(int)updateSelfPosition:(ByteRTCPositionInfo\* _Nonnull)positionInfo<br><br>2. \-(int)updateSelfPosition:(ByteRTCPositionInfo\* _Nonnull)positionInfo<br><br>3. \-(int)updateRemotePosition:(NSString \* _Nonnull)uid positionInfo:(ByteRTCPositionInfo\* _Nonnull)positionInfo<br><br>4. \-(int)updateRemotePosition:(NSString \* _Nonnull)uid positionInfo:(ByteRTCPositionInfo\* _Nonnull)positionInfo |
|Deleted |* The following methods defined by ByteRTCEngine (formerly ByteRTCVideo) class:<br><br>   * (int)pushScreenVideoFrame:(CVPixelBufferRef _Nonnull )frame time:(CMTime)pts rotation:(int)rotation<br><br>   * (int)setScreenAudioStreamIndex:(ByteRTCStreamIndex) index |Screen sharing functionality partially removed, no replacement available |


<span id="_3-58"></span>
# 3.58

<span id="important-notes"></span>
## Important Notes

This version has unified all non\-standard API namings to improve code standardization and usability. The following are examples of changes; please refer to the [Key Types](https://docs.byteplus.com/en/docs/12/docs-70089) page for specific modifications to the types used.


|Change Object |Change Details |Old Version Example |New Version Example |
|---|---|---|---|
|Enum Values |Unify with the prefix "ByteRTC", changed to "ClassName+ValueName" |For example, `ByteRTCSEICountPerFrame`:<br><br><br>* kSingleSEIPerFrame = 0,<br><br>* kMultiSEIPerFrame = 1, |For example, `ByteRTCSEICountPerFrame`:<br><br><br>* ByteRTCSEICountPerFrameSingle = 0,<br><br>* ByteRTCSEICountPerFrameMulti = 1, |
|Struct Members |Changed to lowercase initial letter, camel case notation |For example, `ByteRTCLocalStreamStats`:<br><br><br>* audio_stats<br><br>* video_stats<br><br>* tx_quality<br><br>* rx_quality<br><br>* is_screen |For example, `ByteRTCLocalStreamStats`:<br><br><br>* audioStats<br><br>* videoStats<br><br>* txQuality<br><br>* rxQuality<br><br>* isScreen |


<span id="method-changes"></span>
## Method Changes


|Change Details |Functional Module |Deprecated Class/Interface |Replacement Class/Interface |Notes |
|---|---|---|---|---|
|Removed |Main Class |`ByteRTCEngineKit` |`ByteRTCVideo` | |
|Removed |Engine Management |`ByteRTCVideo.setEnv` |`RTCVideo.createRTCVideo:delegate:parameters:` |For more information, please consult technical support. |
|Expanded Usage Range |Video Processing |`setVideoDecoderConfig` |`setVideoDecoderConfig` |The old interface was only supported for manual subscription; the new one also supports automatic subscription. |
|Removed |Audio Processing |`ByteRTCAudioProcessor` |`ByteRTCAudioFrameProcessor` |`ByteRTCAudioProcessor` was deprecated in version 3.42 and has been removed in this version. |
|New Member Variable in Parameter Data Structure |Audio Management |`enableAudioPropertiesReport` |`enableAudioPropertiesReport` |A new parameter `enableVoicePitch` has been added to control whether to callback the fundamental frequency of the local user's voice. |
|Deprecated |Video Processing |`ByteRTCVideo.getAuthMessage` |`ByteRTCVideoEffect.getAuthMessage` |Replace the method in `ByteRTCVideo` with the one in the `ByteRTCVideoEffect` class. |


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
|Member Variable Change |CDN Live Streaming |`ByteRTCMixedStreamLayoutRegionConfig` |The setting for the individual user image in live streaming has changed from a normalized ratio relative to the overall image to an absolute pixel value setting. |
|Enum Value Renamed |Video Management |`ByteRTCVideoSourceType` |`ByteRTCVideoSourceTypeEncodedManualSimulcast = 2` changed to `ByteRTCVideoSourceTypeEncodedAutoSimulcast = 2`<br><br>`ByteRTCVideoSourceTypeEncodedAutoSimulcast = 3` changed to `ByteRTCVideoSourceTypeEncodedManualSimulcast = 3`<br><br>The renamed enum values are now consistent with those on other platforms. |


<span id="error-code-changes"></span>
## Error Code Changes


|Change Details |Error Code |Notes |
|---|---|---|
|Enum Value Addition/Removal |`ByteRTCUserMessageSendResult` |New error codes for client message sending failures to the business server have been added:<br><br>`ByteRTCUserMessageSendResultE2BSSendFailed = 17`<br><br>`ByteRTCUserMessageSendResultE2BSReturnFailed = 18` |


<span id="_3-56"></span>
# 3.56

<span id="important-notes"></span>
## Important Notes

Since V3.56, the RTC SDK for macOS requires macOS 10.13 or later.

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
|Modified |Audio management |* `enumerateAudioCaptureDevices`<br><br>* `enumerateAudioPlaybackDevices` |* `enumerateAudioCaptureDevices`<br><br>* `enumerateAudioPlaybackDevices` |Behavior change. A time\-out mechanism has been added to the API to handle waiting times. If a time\-out occurs, it returns an empty list. By default, the time\-out duration is set to 10 seconds. |
|Modified |Video management |`enumerateVideoCaptureDevices` |`enumerateVideoCaptureDevices` |Behavior change. A time\-out mechanism has been added to the API to handle waiting times. If a time\-out occurs, it returns an empty list. By default, the time\-out duration is set to 10 seconds. |
|Deprecated |Video Management |`- (int)updateRemoteStreamVideoCanvas:(ByteRTCRemoteStreamKey * _Nonnull)key withRenderMode:(ByteRTCRenderMode)renderMode withBackgroundColor:(NSUInteger)backgroundColor NS_SWIFT_NAME(updateRemoteStreamVideoCanvas(_:withRenderMode:withBackgroundColor:));` |`- (int)updateRemoteStreamVideoCanvas:(ByteRTCRemoteStreamKey * _Nonnull)key withRemoteVideoRenderConfig:(ByteRTCRemoteVideoRenderConfig * _Nonnull)remoteVideoRenderConfig NS_SWIFT_NAME(updateRemoteStreamVideoCanvas(_:withRemoteVideoRenderConfig:));` |With the new API, you can set both the render mode and the background color through the "remoteVideoRenderConfig" parameter. In addition, another parameter "renderRotation" is added allowing you to set the rotation angle of the remote video frame. |
|Deprecated |Video Processing |`ByteRTCVideo.getAuthMessage` |`ByteRTCVideoEffect.getAuthMessage` |`getAuthMessage` has been moved from the ByteRTCVideo class to the ByteRTCVideoEffect class, and the original method has been deprecated. |


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


|Type |Class |Previous |Current |Notes |
|---|---|---|---|---|
|Replaced |Top level class used in APIs for pushing mixed streams to CDN |`ByteRTCLiveTranscoding` |`ByteRTCMixedStreamConfig` |Some variable names/API names in the class are also changed. For specific changes, click the new class. |
|Replaced |Observer used in APIs for pushing mixed streams to CDN |`LiveTranscodingDelegate` |`ByteRTCMixedStreamObserver` ||
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

This version included two new dependencies `libAGFX.dylib` and `libbytenn.dylib` which you should import into you project. See SDK configuration for how to add dependencies.

<span id="header-file"></span>
## Header File

The original `ByteRTCCommonDefines.h` header file has been split into `ByteRTCMediaDefines.h` and `ByteRTCRtsDefines.h`, both of which you should import into your project if needed.

<span id="api"></span>
## API


|Type |Function Module |Previous |Current |Notes |
|---|---|---|---|---|
|Return value change |Room management |`joinRoom:userInfo:roomConfig:` returns:<br><br><br>* `-1`: Invalid parameters.<br><br>* `-2`: Already in a room. |`joinRoom:userInfo:roomConfig:` returns:<br><br><br>* `-1`: Failure.<br><br>* `-2`: Invalid parameters.<br><br>* `-4`: Already in a room. |`0` continues to represent success. |
||Engine management |`setBusinessId:` returns:<br><br><br>* `< 0`: Failure. Refer to `BusinessCheckCode`。<br><br>* `-6001`: Already in a room.<br><br>* `-6002`: Invalid parameters. |`setBusinessId:` returns:<br><br><br>* `< 0`: Failure. Refer to `ReturnStatus`<br><br>* `-2`: Invalid parameters. ||
|Modified |Message |`(int64_t)sendUserMessage:(NSString *_Nonnull)userId message:(NSString *_Nonnull)message config:(ByteRTCMessageConfig)config;` |`(NSInteger)sendUserMessage:(NSString *_Nonnull)userId message:(NSString *_Nonnull)message config:(ByteRTCMessageConfig)config;` |The data type of the parameter changed from `int64_t` to `NSInteger`. |
|Modified |Message |`(int64_t)sendUserBinaryMessage:(NSString * _Nonnull)uid message:(NSData * _Nonnull)message config:(ByteRTCMessageConfig)config;` |`(NSInteger)sendUserBinaryMessage:(NSString * _Nonnull)uid message:(NSData * _Nonnull)message config:(ByteRTCMessageConfig)config;` |The data type of the parameter changed from `int64_t` to `NSInteger`. |
|Modified |Message |`(int64_t)sendRoomMessage:(NSString *_Nonnull)message NS_SWIFT_NAME(sendRoomMessage(_:));` |`(NSInteger)sendRoomMessage:(NSString *_Nonnull)message NS_SWIFT_NAME(sendRoomMessage(_:));` |The data type of the parameter changed from `int64_t` to `NSInteger`. |
|Modified |Message |`(int64_t)sendRoomBinaryMessage:(NSData * _Nonnull)message NS_SWIFT_NAME(sendRoomBinaryMessage(_:));` |`(NSInteger)sendRoomBinaryMessage:(NSData * _Nonnull)message NS_SWIFT_NAME(sendRoomBinaryMessage(_:));` |The data type of the parameter changed from `int64_t` to `NSInteger`. |
|Modified |Message |`(int64_t)sendUserMessageOutsideRoom:(NSString * _Nonnull)userId message:(NSString * _Nonnull)messageStr config:(ByteRTCMessageConfig)config;` |`(NSInteger)sendUserMessageOutsideRoom:(NSString * _Nonnull)userId message:(NSString * _Nonnull)messageStr config:(ByteRTCMessageConfig)config;` |The data type of the parameter changed from `int64_t` to `NSInteger`. |
|Modified |Message |`(int64_t)sendUserBinaryMessageOutsideRoom:(NSString * _Nonnull)userId message:(NSData * _Nonnull)messageStr config:(ByteRTCMessageConfig)config;` |`(NSInteger)sendUserBinaryMessageOutsideRoom:(NSString * _Nonnull)userId message:(NSData * _Nonnull)messageStr config:(ByteRTCMessageConfig)config;` |The data type of the parameter changed from `int64_t` to `NSInteger`. |
|Modified |Message |`(int64_t)sendServerMessage:(NSString * _Nonnull)messageStr;` |`(NSInteger)sendServerMessage:(NSString * _Nonnull)messageStr;` |The data type of the parameter changed from `int64_t` to `NSInteger`. |
|Modified |Message |`(int64_t)sendServerBinaryMessage:(NSData * _Nonnull)messageStr;` |`(NSInteger)sendServerBinaryMessage:(NSData * _Nonnull)messageStr;` |The data type of the parameter changed from `int64_t` to `NSInteger`. |
|Modified |Screen sharing |`(int)setScreenVideoEncoderConfig:(ByteRTCVideoEncoderConfig * _Nullable) screen_solution;` |`(int)setScreenVideoEncoderConfig:(ByteRTCScreenVideoEncoderConfig * _Nullable) screen_solution;` |The data type of the parameter changed to `ByteRTCScreenVideoEncoderConfig`. |
|Modified |Screen sharing |* `setVideoSourceType:WithStreamIndex:` The screen video source defaults to external.<br><br>* `setScreenAudioSourceType:` When the current setting is an internal source, and the capture is enabled, calling the API to switch to external source does not affect the internal capture.<br><br>* `startScreenAudioCapture:` When the current setting is an external source, calling the API enables the internal source, and starts capturing.<br><br>* `stopScreenCapture` When the current setting is an external source, calling the API disables the external capturing. |* `setVideoSourceType:WithStreamIndex:` The screen video source defaults to internal.<br><br>* `setScreenAudioSourceType:` When the current setting is an internal source, and the capture is enabled, calling the API to switch to external source stops the internal capture as well.<br><br>* `startScreenAudioCapture:`/`startScreenVideoCapture:captureParameters:` When the current setting is an external source, calling the API to enable the internal source will fail and receive `rtcEngine:onVideoDeviceWarning:deviceType:deviceWarning:` or `rtcEngine:onAudioDeviceWarning:deviceType:deviceWarning:`.<br><br>* `stopScreenAudioCapture`/ `stopScreenVideoCapture` When the current setting is an external source, calling the API to enable the internal source will fail and receive `rtcEngine:onVideoDeviceWarning:deviceType:deviceWarning:` or `rtcEngine:onAudioDeviceWarning:deviceType:deviceWarning:`. |Align the behaviors of the screen\-sharing APIs with the video stream APIs. |
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
|Modified |Multiple modules |`leaveRoom`<br><br>`publishStream`<br><br>`unpublishStream`<br><br>`publishScreen`<br><br>`unpublishScreen`<br><br>`enableSimulcastMode`<br><br>`updateLocalVideoCanvas`<br><br>`setLocalVideoMirrorType`<br><br>`setVideoRotationMode`<br><br>`startLiveTranscoding`<br><br>`stopLiveTranscoding`<br><br>`setPublishFallbackOption`<br><br>`setSubscribeFallbackOption` |`leaveRoom`<br><br>`publishStream`<br><br>`unpublishStream`<br><br>`publishScreen`<br><br>`unpublishScreen`<br><br>`enableSimulcastMode`<br><br>`updateLocalVideoCanvas`<br><br>`setLocalVideoMirrorType`<br><br>`setVideoRotationMode`<br><br>`startLiveTranscoding`<br><br>`stopLiveTranscoding`<br><br>`setPublishFallbackOption`<br><br>`setSubscribeFallbackOption` |The return type changed from `int` to `void`. |
|Modified |Video Management |`(int)setRemoteVideoCanvas:(NSString * _Nonnull)uid withIndex:(ByteRTCStreamIndex)streamIndex withCanvas:(ByteRTCVideoCanvas * _Nullable)canvas;` |`(void)setRemoteVideoCanvas:(ByteRTCRemoteStreamKey * _Nonnull)key withCanvas:(ByteRTCVideoCanvas * _Nullable)canvas;` |* The return type changes form `int` to `void`.<br><br>* Set `uid` and `streamIndex` in `key`. |
|Modified |Video Management |`(int)updateRemoteStreamVideoCanvas:(NSString * _Nonnull)roomid withUserId:(NSString * _Nonnull)uid withIndex:(ByteRTCStreamIndex)streamIndex withRenderMode:(ByteRTCRenderMode)renderMode withBackgroundColor:(NSUInteger)backgroundColor;` |`(void)updateRemoteStreamVideoCanvas:(ByteRTCRemoteStreamKey * _Nonnull)key withRenderMode:(ByteRTCRenderMode)renderMode withBackgroundColor:(NSUInteger)backgroundColor;` |* The return type changes form `int` to `void`.<br><br>* Set `roomid`, `uid` and `streamIndex` in `key`. |
|Modified |Advanced Features |`UpdateScreenCaptureMouseCursor` |`updateScreenCaptureMouseCursor` | |
|Modified |Advanced Features |`UpdateScreenCaptureFilterConfig` |`updateScreenCaptureFilterConfig` | |
|Modified |Advanced Features |`getScreenCaptureSourceThumbnail` |`getThumbnail` | |
|Modified |Room Management |`setRtcRoomDelegate` |`setRTCRoomDelegate` | |
|Modified |Room Management |`joinRoomByToken` |`joinRoom` | |
|Modified |Room Management |`renewToken` |`updateToken` | |
|Modified |Engine Management |`getSdkVersion` |`getSDKVersion` | |
|Modified |Security and Encryption |`setEncryptType` |`setEncryptInfo` | |
|Modified |Audio Management |`startPlaybackDeviceTest` |`startAudioPlaybackDeviceTest` | |
|Modified |Audio Management |`stopPlaybackDeviceTest` |`stopAudioPlaybackDeviceTest` | |
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
|Modified |Push to CDN |`onMixingAudioFrame` |`onMixingAudioFrame` |Added a new parameter: `timeStamp` |
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
|New member in API parameter |`enableAudioPropertiesReport:` |Adds `ByteRTCAudioPropertiesMode` member in "ByteRTCAudioPropertiesConfig". |


<span id="keytype"></span>
## Keytype


|Type |API |Notes |
|---|---|---|
|Member change |`ByteRTCAudioFrameMethod` |Adds "ByteRTCAudioFrameProcessorScreen = 4" member. |
