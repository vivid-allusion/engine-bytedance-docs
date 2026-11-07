---
title: "Error Code"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70091"
---

<span id="ByteRTCNetworkDetectionStartReturn"></span>
# ByteRTCNetworkDetectionStartReturn

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCNetworkDetectionStartReturn
)
```


Return value to start probing

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCNetworkDetectionStartReturnSuccess |0 |Successfully initiated detection. |
|ByteRTCNetworkDetectionStartReturnParamErr |1 |Failed to start probing. Parameter error, both uplink and downlink probes are false, or the expected bandwidth exceeds the range [100,10000] |
|ByteRTCNetworkDetectionStartReturnStreaming |2 |Failed to start probing. Stream publishing and subscribing has begun |
|ByteRTCNetworkDetectionStartReturnStarted |3 |Has begun to detect |
|ByteRTCNNetworkDetectionStartReturnNotSupport |4 |Not supported |


<span id="ByteRTCAudioRecordingErrorCode"></span>
# ByteRTCAudioRecordingErrorCode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCAudioRecordingErrorCode
)
```


Error code for audio recording.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCAudioRecordingErrorCodeOk |0 |OK |
|ByteRTCAudioRecordingErrorCodeNoPermission |\-1 |No file write permissions. |
|ByteRTCAudioRecordingErrorNotInRoom |\-2 |Not in the room. |
|ByteRTCAudioRecordingAlreadyStarted |\-3 |Started. |
|ByteRTCAudioRecordingNotStarted |\-4 |Not started. |
|ByteRTCAudioRecordingErrorCodeNotSupport |\-5 |Failure. Invalid file format. |
|ByteRTCAudioRecordingErrorCodeOther |\-6 |Other error. |


<span id="ByteRTCRoomMessageSendResult"></span>
# ByteRTCRoomMessageSendResult

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCRoomMessageSendResult
)
```


Result of broadcasting messages in the room

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCRoomMessageSendResultSuccess |200 |The message was sent successfully. |
|ByteRTCRoomMessageSendResultTimeout |1 |Failure. Sending timeout. |
|ByteRTCRoomMessageSendResultNetworkDisconnected |2 |Failure. Channel disconnected. |
|ByteRTCRoomMessageSendResultExceedQPS |5 |Failure. Exceeds QPS limit. |
|ByteRTCRoomMessageSendResultNotJoin |100 |Failure. The sender has not joined a room. |
|ByteRTCRoomMessageSendResultInit |101 |Failure. The connection has not completed initialization. |
|ByteRTCRoomMessageSendResultNoConnection |102 |Failure. No connection available. |
|ByteRTCRoomMessageSendResultExceedMaxLength |103 |Failure. The message size exceeds the maximum limit. The default maximum length of a message is 1 KB. If you [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode), the maximum length is 64 KB. |
|ByteRTCRoomMessageSendResultUnknown |1000 |Failure. Unknown error. |


<span id="ByteRTCWarningCode"></span>
# ByteRTCWarningCode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCWarningCode
)
```


Callback warning code. The warning code indicates that there is a problem within the SDK and the SDK is trying to recover. Warning codes are for notification only.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCWarningCodePublishStreamFailed |\-2002 |Failed to publish audio & video streams.<br><br>&nbsp;<br><br>When you publish audio & video streams in your room, publishing fails due to a server error. The SDK automatically retries publishing. |
|ByteRTCWarningCodeSubscribeStreamFailed404 |\-2003 |Subscription to audio & video stream failed. Receive message from [rtcRoom:onVideoSubscribeStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onvideosubscribestatechanged-info-state-reason), [rtcRoom:onAudioSubscribeStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onaudiosubscribestatechanged-info-state-reason).<br><br>&nbsp;<br><br>The subscription failed because the audio & video stream for the subscription was not found in the current room. The SDK will automatically retry the subscription. If the subscription fails, it is recommended that you exit the retry. |
|ByteRTCWarningCodeSubscribeStreamFailed5xx |\-2004 |Subscription to audio & video stream failed. Receive message from [rtcRoom:onVideoSubscribeStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onvideosubscribestatechanged-info-state-reason), [rtcRoom:onAudioSubscribeStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onaudiosubscribestatechanged-info-state-reason).<br><br>&nbsp;<br><br>When you subscribe to audio & video streams in your room, the subscription fails due to a server error. The SDK automatically retries the subscription. |
|ByteRTCWarningCodePublishStreamForbidden |\-2009 |This warning is triggered when you call `setUserVisibility:` to set yourself invisible to others before attempting to publish the stream. Receive message via [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish), [rtcRoom:onUserPublishStreamAudio:info:isPublish:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamaudio-info-ispublish). |
|ByteRTCWarningCodeSendCustomMessage |\-2011 |Sending a custom broadcast message failed, you are not currently in the room. |
|ByteRTCWarningCodeCodeUserNotifyStop |\-2013 |When the number of people in the room exceeds 500, stop sending `rtcEngine:onUserJoined:elapsed:` and `rtcEngine:onUserLeave:reason:` callbacks to existing users in the room, and prompt all users in the room via broadcast. Receive message from [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo). |
|ByteRTCWarningCodeUserInPublish |\-2014 |The user has published in another room. Receive message via [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish), [rtcRoom:onUserPublishStreamAudio:info:isPublish:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamaudio-info-ispublish). |
|ByteRTCWarningCodeInEchoTestMode |\-2017 |This interface has been disabled because the engine is in echo testing mode. |
|ByteRTCWarningCodeNoCameraPermission |\-5001 |The camera permission is abnormal, the current application does not get the camera permission |
|ByteRTCWarningSetScreenAudioSourceTypeFailed |\-5009 |Setting the screen audio capture type via `setScreenAudioSourceType` after publishScreenAudio: is not supported |
|ByteRTCWarningSetScreenAudioStreamIndexFailed |\-5010 |Setting the screen audio mix type via `setScreenAudioStreamIndex` after publishScreenAudio: is not supported |
|ByteRTCWarningInvalidVoicePitch |\-5011 |Invalid pitch value setting |
|ByteRTCWarningInvalidCallForExtAudio |\-5013 |Mixed use of old and new APIs for external audio sources |
|ByteRTCWarningCodeInvalidCanvasHandle |\-6001 |The specified internal rendering canvas handle is invalid.<br><br>&nbsp;<br><br>An invalid canvas handle is specified when you call [setLocalVideoCanvas:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-setlocalvideocanvas) or [setRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-setremotevideocanvas-withcanvas), triggering this callback. |
|ByteRTCWarningCodeInvaildSamiAppkeyORToken |\-7002 |Authorization failure for [BytePlus Audio SDK](https://go.byteplus.com/audio-sdk). Contact the technical support. |
|ByteRTCWarningCodeInvaildSamiResourcePath |\-7003 |Failure to get the resource for [BytePlus Audio SDK](https://go.byteplus.com/audio-sdk). Input the right DAT path or contact the technical support. |
|ByteRTCWarningCodeLoadSamiLibraryFailed |\-7004 |Failure to load the library for [BytePlus Audio SDK](https://go.byteplus.com/audio-sdk). Use the right library or contact the technical support. |
|ByteRTCWarningCodeInvaildSamiEffectType |\-7005 |The audio effect is not supported by [BytePlus Audio SDK](https://go.byteplus.com/audio-sdk). Contact the technical support. |
|[deprecated] ByteRTCWarningCodeRoomAlreadyExist |\-2015 |Deprecated since 3.45 and will be deleted in 3.51.<br><br>There is a room with the same roomId |
|[deprecated] ByteRTCWarningCodeNoMicrophonePermission |\-5002 |Deprecated since 3.45 and will be deleted in 3.51, use [ByteRTCMediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70089#ByteRTCMediaDeviceError).ByteRTCMediaDeviceErrorDeviceNoPermission instead.<br><br>Deprecated since 3.45. Please use [ByteRTCMediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70089#ByteRTCMediaDeviceError).ByteRTCMediaDeviceErrorDeviceNoPermission instead.<br><br>&nbsp;<br><br>The microphone permission is abnormal, the current application does not get microphone permission. |
|[deprecated] ByteRTCWarningCodeAudioDeviceManagerRecordingStartFail |\-5003 |Deprecated since 3.45 and will be deleted in 3.51, use [ByteRTCMediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70089#ByteRTCMediaDeviceError).ByteRTCMediaDeviceErrorDeviceFailure instead.<br><br>Deprecated since 3.45. Please use [ByteRTCMediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70089#ByteRTCMediaDeviceError).ByteRTCMediaDeviceErrorDeviceFailure instead.<br><br>&nbsp;<br><br>The audio capture device failed to start.<br><br>&nbsp;<br><br>Failed to start the audio capture device, the current device may be occupied by other applications. |
|[deprecated] ByteRTCWarningCodeAudioDeviceManagerPlayoutStartFail |\-5004 |Deprecated since 3.45 and will be deleted in 3.51, use [ByteRTCMediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70089#ByteRTCMediaDeviceError).ByteRTCMediaDeviceErrorDeviceFailure instead.<br><br>Deprecated since 3.45. Please use [ByteRTCMediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70089#ByteRTCMediaDeviceError).ByteRTCMediaDeviceErrorDeviceFailure instead.<br><br>&nbsp;<br><br>Audio playback device startup failure warning.<br><br>&nbsp;<br><br>It may be due to insufficient system resources or wrong parameters. |
|[deprecated] ByteRTCWarningCodeNoRecordingDevice |\-5005 |Deprecated since 3.45 and will be deleted in 3.51, use [ByteRTCMediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70089#ByteRTCMediaDeviceError).ByteRTCMediaDeviceErrorDeviceNotFound instead.<br><br>Deprecated since 3.45. Please use [ByteRTCMediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70089#ByteRTCMediaDeviceError).ByteRTCMediaDeviceErrorDeviceNotFound instead.<br><br>&nbsp;<br><br>No audio capture device available.<br><br>&nbsp;<br><br>Failed to start the audio capture device, please insert the available audio capture device. |
|[deprecated] ByteRTCWarningCodeNoPlayoutDevice |\-5006 |Deprecated since 3.45 and will be deleted in 3.51, use [ByteRTCMediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70089#ByteRTCMediaDeviceError).ByteRTCMediaDeviceErrorDeviceNotFound instead.<br><br>Deprecated since 3.45. Please use [ByteRTCMediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70089#ByteRTCMediaDeviceError).ByteRTCMediaDeviceErrorDeviceNotFound instead.<br><br>&nbsp;<br><br>No audio playback device available.<br><br>&nbsp;<br><br>Failed to start the audio playback device, please insert the available audio playback device. |
|[deprecated] ByteRTCWarningCodeRecordingSilence |\-5007 |Deprecated since 3.45 and will be deleted in 3.51, use [ByteRTCMediaDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70089#ByteRTCMediaDeviceWarning).ByteRTCMediaDeviceWarningCaptureSilence instead.<br><br>Deprecated since 3.45. Please use [ByteRTCMediaDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70089#ByteRTCMediaDeviceWarning).ByteRTCMediaDeviceWarningCaptureSilence instead.<br><br>&nbsp;<br><br>The current audio equipment has not collected valid sound data, please check and replace the audio capture device. |
|[deprecated] ByteRTCWarningCodeMediaDeviceOperationDennied |\-5008 |Deprecated since 3.45 and will be deleted in 3.51, use [ByteRTCMediaDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70089#ByteRTCMediaDeviceWarning).ByteRTCMediaDeviceWarningOperationDenied instead.<br><br>Deprecated since 3.45. Please use [ByteRTCMediaDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70089#ByteRTCMediaDeviceWarning).ByteRTCMediaDeviceWarningOperationDenied instead.<br><br>&nbsp;<br><br>Warning on mishandling media devices.<br><br>&nbsp;<br><br>When using custom acquisition, the internal acquisition switch cannot be called, and this warning is triggered when called. |


<span id="ByteRTCErrorCode"></span>
# ByteRTCErrorCode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCErrorCode
)
```


Callback error code. When an unrecoverable error is encountered internally in the

SDK, the user is notified via an `rtcEngine:onError:` callback.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCErrorCodeInvalidToken |\-1000 |Token is invalid. Receive message from [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo).<br><br>The Token used when calling [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig) is invalid or expired. The user is required to retrieve the token and call the [updateToken:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCRTSRoom-updatetoken) to update the token. |
|ByteRTCErrorCodeJoinRoom |\-1001 |Join room error. Receive message from [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo).<br><br>An unknown error occurred when joining the room, which caused the user to fail to join the room. Users are required to rejoin the room. |
|ByteRTCErrorCodeNoPublishPermission |\-1002 |No permission to publish audio & video streams. Receive message from [rtcRoom:onVideoPublishStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onvideopublishstatechanged-info-state-reason), [rtcRoom:onAudioPublishStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onaudiopublishstatechanged-info-state-reason).<br><br>&nbsp;<br><br>The user failed to publish the audio & video stream in the room. The reason for the failure is that the user does not have permission to publish the stream. |
|ByteRTCErrorCodeNoSubscribePermission |\-1003 |No subscription permissions for audio & video streams. Receive message from [rtcRoom:onVideoSubscribeStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onvideosubscribestatechanged-info-state-reason), [rtcRoom:onAudioSubscribeStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onaudiosubscribestatechanged-info-state-reason).<br><br>&nbsp;<br><br>The user failed to subscribe to the audio & video stream in the room where the user is located. The reason for the failure is that the user does not have permission to subscribe to the stream. |
|ByteRTCErrorCodeDuplicateLogin |\-1004 |The user has been removed from the room because another user with the same user ID joins the room. Receive message from [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo). |
|ByteRTCErrorCodeKickedOut |\-1006 |The user has been removed from the room by the administrator via an OpenAPI call. Receive message from [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo). |
|ByteRTCErrorCodeRoomIdIllegal |\-1007 |When calling `createRtcRoom:`, if the roomId is illegal, it will return null and throw the error. Receive message from [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo). |
|ByteRTCErrorCodeTokenExpired |\-1009 |Token expired. This error code is returned when the user's token expires in the room. Receive message from [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo).<br><br>Call [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig) to rejoin the room with a new required Token. |
|ByteRTCErrorCodeUpdateTokenWithInvalidToken |\-1010 |The Token you provided when calling `updateToken:` is invalid. Receive message from [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo). |
|ByteRTCErrorCodeRoomDismiss |\-1011 |Users have been removed from the room because the administrator dismissed the room by calling OpenAPI. Receive message from [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo). |
|ByteRTCRoomAlreadyExist |\-1013 |There is a room with the same roomId, whose room id is the same as echo test. Receive message from [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo). |
|ByteRTCUserIDDifferent |\-1014 |The local user joins multiple rooms with different uids. Receive message from [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo).<br><br>In the same engine instance, users need to use the same uid to join different rooms. |
|ByteRTCErrorCodeJoinRoomRoomForbidden |\-1025 |The room has been banned before the user calls `joinRoom`. Receive message from [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo). |
|ByteRTCErrorCodeJoinRoomUserForbidden |\-1026 |The user has been banned before calling `joinRoom`. Receive message from [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo). |
|ByteRTCErrorCodeOverStreamSubscribeLimit |\-1070 |Subscription to audio & video stream failed, the total number of subscribed audio & video streams exceeded the upper limit. Receive message from [rtcRoom:onVideoSubscribeStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onvideosubscribestatechanged-info-state-reason), [rtcRoom:onAudioSubscribeStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onaudiosubscribestatechanged-info-state-reason).<br><br>&nbsp;<br><br>In the game scenario, in order to ensure the performance and quality of audio & video calls, the server will limit the total number of audio & video streams subscribed by the user. When the total number of audio & video streams subscribed by the user has reached the maximum, continuing to subscribe to more streams will fail, and the user will receive this error notification. |
|ByteRTCErrorCodeOverStreamPublishLimit |\-1080 |Publishing stream failed because the total number of publishing streams exceeds the upper limit. Receive message from [rtcRoom:onVideoPublishStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onvideopublishstatechanged-info-state-reason), [rtcRoom:onAudioPublishStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onaudiopublishstatechanged-info-state-reason).<br><br>&nbsp;<br><br>RTC system limits the total number of streams published in a single room, including video streams, audio streams, and screen streams. Local users will fail to publish streams to the room when the maximum number of published streams in the room has been reached, and will receive this error notification. |
|ByteRTCErrorCodeAbnormalServerStatus |\-1084 |The user has been removed from the room due to the abnormal server status. Receive message from [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo).<br><br>SDK is disconnected from the signaling server. It will not reconnect automatically. Please contact technical support. |
|[deprecated] ByteRTCErrorCodeOverVideoPublishLimit |\-1082 |Deprecated since 3.52, use ByteRTCErrorCodeOverStreamPublishLimit\-1080 instead<br><br>The total number of published video streams exceeds the upper limit.<br><br>&nbsp;<br><br>The RTC system limits the number of video streams posted in a single room. If the maximum number of video streams posted in the room has been reached, local users will fail to post video streams to the room again and will receive this error notification. |
|[deprecated] ByteRTCErrorCodInvalidAudioSyncUidRepeated |\-1083 |Deprecated since 3.60, use ByteRTCAVSyncEventInvalidUidRepeated = 0 carried by [rtcRoom:onAVSyncEvent:userId:eventCode:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCRoomDelegate-rtcroom-onavsyncevent-userid-eventcode) instead.<br><br>A/V synchronization failed. Receive message from tcRoom:onStreamStateChanged:withUid:state:extraInfo:.<br><br>Current source audio ID has been set by other video publishers in the same room.<br><br>&nbsp;<br><br>One single audio source cannot be synchronized with multiple video sources at the same time. |


<span id="ByteRTCUserMessageSendResult"></span>
# ByteRTCUserMessageSendResult

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCUserMessageSendResult
)
```


Result of sending messages and the reason of failure if it fails.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCUserMessageSendResultSuccess |0 |Message sent successfully. |
|ByteRTCUserMessageSendResultTimeout |1 |Failure. A timeout occurred. |
|ByteRTCUserMessageSendResultNetworkDisconnected |2 |Failure. The connection was lost before the message could be sent. |
|ByteRTCUserMessageSendResultNoReceiver |3 |Failure. The recipient could not be found. |
|ByteRTCUserMessageSendResultNoRelayPath |4 |Failure. The remote user is not logged in or has not joined a room. |
|ByteRTCUserMessageSendResultExceedQPS |5 |Failure. Exceeds QPS limit. |
|ByteRTCUserMessageSendResultE2BSSendFailed |17 |Failure. The app server failed to receive the message sent by the client.<br><br>&nbsp;<br><br>Triggered by calling `sendServerMessage` or `sendServerBinaryMessage`, and carried by `onServerMessageSendResult` callback. |
|ByteRTCUserMessageSendResultE2BSReturnFailed |18 |Failure. The app server received the message sent by the client, but failed to respond.<br><br>&nbsp;<br><br>Triggered by calling `sendServerMessage` or `sendServerBinaryMessage`, and carried by `onServerMessageSendResult` callback. |
|ByteRTCUserMessageSendResultNotJoin |100 |Failure. The sender has not joined the room. |
|ByteRTCUserMessageSendResultInit |101 |Failure. The connection has not been initialized. |
|ByteRTCUserMessageSendResultNoConnection |102 |Failure. No available data transmission channel. |
|ByteRTCUserMessageSendResultExceedMaxLength |103 |Failure. The message size exceeds the maximum limit. The default maximum length of a message is 1 KB. If you [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode), the maximum length is 64 KB. |
|ByteRTCUserMessageSendResultEmptyUser |104 |Failure. The ID of the recipient is empty. |
|ByteRTCUserMessageSendResultNotLogin |105 |Failure. The sender is not signed in. |
|ByteRTCUserMessageSendResultServerParamsNotSet |106 |Failure. Required parameters for sending to the application server were not set. |
|ByteRTCUserMessageSendResultUnknown |1000 |Failure. Unknown error. |


<span id="ByteRTCLoginErrorCode"></span>
# ByteRTCLoginErrorCode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCLoginErrorCode
)
```


Login result

The result of calling [login:uid:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-login-uid) will notify the user through [rtcEngine:onLoginResult:errorCode:elapsed:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCEngineDelegate-rtcengine-onloginresult-errorcode-elapsed) callback.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCLoginErrorCodeSuccess |0 |Call the [login:uid:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-login-uid) method to sign in successfully. |
|ByteRTCLoginErrorCodeInvalidToken |\-1000 |The token used when calling the [login:uid:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-login-uid) method is invalid or expired. The user is required to re\-acquire the token. |
|ByteRTCLoginErrorCodeLoginFailed |\-1001 |Login error<br><br>&nbsp;<br><br>An unknown error occurred when calling the [login:uid:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-login-uid) method, which caused the login to fail. The user is required to sign in again. |
|ByteRTCLoginErrorCodeInvalidUserId |\-1002 |There was a problem with the incoming user ID when the [login:uid:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-login-uid) method was called. |
|ByteRTCLoginErrorCodeServerError |\-1003 |A server error occurred while calling [login:uid:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-login-uid) during login. |


<span id="ByteRTCSingleStreamTaskErrorCode"></span>
# ByteRTCSingleStreamTaskErrorCode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCSingleStreamTaskErrorCode
)
```


Errors occurring during pushing a single stream to CDN

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCSingleStreamTaskErrorCodeOK |0 |Everything is OK. |
|ByteRTCSingleStreamTaskErrorCodeUnknownByServer |1091 |Error from the server. |
|ByteRTCSingleStreamTaskErrorCodeSignalRequestTimeout |1092 |Request timed out. Please check network status and retry. |
|ByteRTCSingleStreamTaskErrorCodeInvalidParamByServer |1093 |The server detects that the task parameters are invalid |
|ByteRTCSingleStreamTaskErrorCodeRemoteKicked |1094 |In the relay task, the user ID in the target room has been kicked out of the target room. |
|ByteRTCSingleStreamTaskErrorCodeJoinDestRoomFailed |1095 |The relay task failed to join the target room. |
|ByteRTCSingleStreamTaskErrorCodeReceiveSrcStreamTimeout |1096 |The stream pulling for the relay task in the source room timed out. |
|ByteRTCSingleStreamTaskErrorCodeNotSurportCodec |1097 |Audio and video encoding relay tasks are not supported |
|ByteRTCSingleStreamTaskErrorCodePushToCDN |1098 |Failed to push the single stream to CDN. |
|ByteRTCSingleStreamTaskErrorCodeTaskCountOverLimit |1099 |The number of concurrent single\-stream push tasks for the host exceeds the limit of 20. |


<span id="ByteRTCMixedStreamTaskErrorCode"></span>
# ByteRTCMixedStreamTaskErrorCode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTCMixedStreamTaskErrorCode
)
```


Mixing stream errors.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCMixedStreamTaskErrorCodeOK |0 |Successfully pushed streams to target CDN. |
|ByteRTCMixedStreamTaskErrorCodeTimeOut |1091 |Request timed out. Please check network status and retry. |
|ByteRTCMixedStreamTaskErrorCodeInvalidParamByServer |1092 |Invalid parameters detected by the server. |
|ByteRTCMixedStreamTaskErrorCodeSubTimeoutByServer |1093 |Subscription to the stream has expired. |
|ByteRTCMixedStreamTaskErrorCodeInvalidStateByServer |1094 |Internal server error. |
|ByteRTCMixedStreamTaskErrorCodeAuthenticationByCDN |1095 |The server failed to push streams to CDN. |
|ByteRTCMixedStreamTaskErrorCodeUnKnownErrorByServer |1096 |Unknown error from server. |
|ByteRTCMixedStreamTaskErrorCodeSignalRequestTimeout |1097 |Signaling connection timeout error. Please check network status and retry. |
|ByteRTCMixedStreamTaskErrorCodeMixImageFailed |1098 |Failed to mix image. |
|ByteRTCMixedStreamTaskErrorCodePushWTNFailed |1195 |Failed to push WTN stream. |


<span id="ByteRTCSingleStreamTaskEvent"></span>
# ByteRTCSingleStreamTaskEvent

```objectivec
typedef NS_ENUM(
    NSUInteger,
    ByteRTCSingleStreamTaskEvent
)
```


Event of pushing a single stream to CDN.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTCSingleStreamTaskEventStartSuccess |1 |The task initiated successfully. |
|ByteRTCSingleStreamTaskEventStartFailed |2 |Failed to initiate the task. |
|ByteRTCSingleStreamTaskEventStopSuccess |3 |The task stopped. |
|ByteRTCSingleStreamTaskEventStopFailed |4 |Failed to stop the task. |
|ByteRTCSingleStreamTaskEventWarning |5 |Warnings |


<span id="ByteRTSWarningCode"></span>
# ByteRTSWarningCode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTSWarningCode
)
```


Callback warning code. The warning code indicates that there is a problem within the SDK and the SDK is trying to recover. Warning codes are for notification only.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTSWarningCodeJoinRoomFailed |\-2001 |Failed to enter the room.<br><br>&nbsp;<br><br>When entering the room for the first time or when the network is disconnected and reconnected due to poor network conditions, entering the room failed due to a server error. The SDK automatically retries joining the room. |
|ByteRTSWarningCodePublishStreamFailed |\-2002 |Failed to publish audio & video streams.<br><br>&nbsp;<br><br>When you publish audio & video streams in your room, publishing fails due to a server error. The SDK automatically retries publishing. |
|ByteRTSWarningCodeSendCustomMessage |\-2011 |Sending a custom broadcast message failed, you are not currently in the room. |
|ByteRTSWarningCodeOldRoomBeenReplaced |\-2016 |The old room has been replaced by a new room with the same roomId |


<span id="ByteRTSErrorCode"></span>
# ByteRTSErrorCode

```objectivec
typedef NS_ENUM(
    NSInteger,
    ByteRTSErrorCode
)
```


Callback error code. When an unrecoverable error is encountered internally in the

SDK, the user is notified via an `rtcEngine:onError:` callback.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|ByteRTSErrorCodeInvalidToken |\-1000 |Token is invalid.<br><br>&nbsp;<br><br>The token used when joining the room is invalid or expired. The user is required to retrieve the token and update it by calling `updateToken:`. |
|ByteRTSErrorCodeJoinRoom |\-1001 |Join room error.<br><br>&nbsp;<br><br>An unknown error occurred when joining the room, which caused the user to fail to join the room. Users are required to rejoin the room. |
|ByteRTSErrorCodeDuplicateLogin |\-1004 |The user has been removed from the room because the same user joined the room on another client. |
|ByteRTSErrorCodeKickedOut |\-1006 |The user has been removed from the room by the administrator via an OpenAPI call. |
|ByteRTSErrorCodeRoomIdIllegal |\-1007 |When calling `createRtcRoom:`, if the roomId is illegal, it will return null and throw the error |
|ByteRTSErrorCodeTokenExpired |\-1009 |Token expired. Call `joinRoomByKey:roomId:userInfo:rtcRoomConfig:` to rejoin with a valid Token. |
|ByteRTSErrorCodeUpdateTokenWithInvalidToken |\-1010 |The Token you provided when calling `updateToken:` is invalid. |
|ByteRTSErrorCodeRoomDismiss |\-1011 |Users have been removed from the room because the administrator dismissed the room by calling OpenAPI. |
|ByteRTSErrorRoomAlreadyExist |\-1013 |There is a room with the same roomId, whose room id is the same as echo test |
|ByteRTSErrorUserIDDifferent |\-1014 |The local user joins multiple rooms with different uids.<br><br>&nbsp;<br><br>In the same engine instance, users need to use the same uid to join different rooms. |
|ByteRTSErrorCodeAbnormalServerStatus |\-1084 |The user has been removed from the room due to the abnormal server status.<br><br>&nbsp;<br><br>SDK is disconnected from the signaling server. It will not reconnect automatically. Please contact technical support. |
