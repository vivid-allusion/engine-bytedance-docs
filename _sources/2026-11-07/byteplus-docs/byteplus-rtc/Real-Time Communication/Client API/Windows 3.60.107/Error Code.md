---
title: "Error Code"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70097"
---

<span id="UserMessageSendResult"></span>
# UserMessageSendResult

```cpp
enum bytertc::UserMessageSendResult
```


Result of sending messages and the reason of failure if it fails.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kUserMessageSendResultSuccess |0 |Message sent successfully. |
|kUserMessageSendResultTimeout |1 |Failure. A timeout occurred. |
|kUserMessageSendResultNetworkDisconnected |2 |Failure. The connection was lost before the message could be sent. |
|kUserMessageSendResultNoReceiver |3 |Failure. The recipient could not be found. |
|kUserMessageSendResultNoRelayPath |4 |Failure. The remote user is not logged in or has not joined a room. |
|kUserMessageSendResultExceedQPS |5 |Failure. Exceeds QPS limit. |
|kUserMessageSendResultE2BSSendFailed |17 |Failure. The app server failed to receive the message sent by the client.<br><br>Triggered by calling `sendServerMessage` or `sendServerBinaryMessage`, and carried by `onServerMessageSendResult` callback. |
|kUserMessageSendResultE2BSReturnFailed |18 |Failure. The app server received the message sent by the client, but failed to respond.<br><br>Triggered by calling `sendServerMessage` or `sendServerBinaryMessage`, and carried by `onServerMessageSendResult` callback. |
|kUserMessageSendResultNotJoin |100 |Failure. The sender has not joined the room. |
|kUserMessageSendResultInit |101 |Failure. The connection has not been initialized. |
|kUserMessageSendResultNoConnection |102 |Failure. No available data transmission channel. |
|kUserMessageSendResultExceedMaxLength |103 |Failure. The message size exceeds the maximum limit. The default maximum length of a message is 1 KB. If you [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode), the maximum length is 64 KB. |
|kUserMessageSendResultEmptyUser |104 |Failure. The ID of the recipient is empty. |
|kUserMessageSendResultNotLogin |105 |Failure. Required parameters for sending to the application server were not set. |
|kUserMessageSendResultServerParamsNotSet |106 |Failure. Required parameters for sending to the application server were not set. |
|kUserMessageSendResultUnknown |1000 |Failure. Unknown error. |


<span id="LocalVideoStreamError"></span>
# LocalVideoStreamError

```cpp
enum bytertc::LocalVideoStreamError
```


Error code when the local video state changes

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kLocalVideoStreamErrorOk |0 |Normal condition |
|kLocalVideoStreamErrorFailure |1 |Local video stream publishing failed |
|kLocalVideoStreamErrorDeviceNoPermission |2 |No access to the local video capture device |
|kLocalVideoStreamErrorDeviceBusy |3 |Local video capture equipment is occupied |
|kLocalVideoStreamErrorDeviceNotFound |4 |Local video capture device does not exist |
|kLocalVideoStreamErrorCaptureFailure |5 |Local video capture failed, it is recommended to check whether the acquisition device is working properly |
|kLocalVideoStreamErrorEncodeFailure |6 |Local video encoding failed |
|kLocalVideoStreamErrorDeviceDisconnected |7 |The local video capture device is disconnected. It is occupied by other programs during the call. |


<span id="MixedStreamTaskErrorCode"></span>
# MixedStreamTaskErrorCode

```cpp
enum bytertc::MixedStreamTaskErrorCode
```


Mixing stream errors.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kMixedStreamTaskErrorCodeOK |0 |Everything is OK. |
|kMixedStreamTaskErrorCodeTimeout |1091 |Request timed out. Please check network status and retry. |
|kMixedStreamTaskErrorCodeInvalidParamByServer |1092 |Invalid parameters were detected by the server. |
|kMixedStreamTaskErrorCodeSubTimeoutByServer |1093 |Subscription to the stream has expired. |
|kMixedStreamTaskErrorCodeInvalidStateByServer |1094 |Internal server error. |
|kMixedStreamTaskErrorCodeAuthenticationByCDN |1095 |The server failed to push the mixing streams to CDN. |
|kMixedStreamTaskErrorCodeUnKnownByServer |1096 |Unknown error from server. |
|kMixedStreamTaskErrorCodeSignalRequestTimeout |1097 |Signaling connection timeout error. Please check network status and retry. |
|kMixedStreamTaskErrorCodeMixImageFailed |1098 |Failed to mix images. |
|kMixedStreamTaskErrorCodePushWTNFailed |1195 |Failed to push the WTN stream. |


<span id="WarningCode"></span>
# WarningCode

```cpp
enum bytertc::WarningCode
```


Callback warning code. The warning code indicates that there is a problem within the SDK and is trying to recover. Warning codes only serve as notifications.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kWarningCodeJoinRoomFailed |\-2001 |Failed to enter the room. Receive message from [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) callback.<br><br>When you call the first time to join the room or disconnect and reconnect due to poor network conditions, the room entry fails due to a server error. The SDK automatically retries joining the room. |
|kWarningCodePublishStreamFailed |\-2002 |Failed to publish audio & video streams. Receive message from [onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onvideopublishstatechanged), onAudioPublishStateChanged{@link #IRTCRoomEventHandler#onAudioPublishStateChanged.<br><br>When you publish audio & video streams in your room, the publication fails due to a server error. The SDK automatically retries the release. |
|kWarningCodeSubscribeStreamFailed404 |\-2003 |Subscription to audio & video stream failed. Receive message from [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onvideosubscribestatechanged), [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onaudiosubscribestatechanged) callback.<br><br>The subscription failed because the audio & video stream for the subscription could not be found in the current room. The SDK will automatically retry the subscription. If the subscription fails, it is recommended that you exit the retry. |
|kWarningCodeSubscribeStreamFailed5xx |\-2004 |Subscription to audio & video stream failed. Receive message from [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onvideosubscribestatechanged), [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onaudiosubscribestatechanged) callback.<br><br>When you subscribe to audio & video streams in your room, the subscription fails due to a server error. The SDK automatically retries the subscription. |
|kWarningCodePublishStreamForbidden |\-2009 |This warning is triggered when you call `setUserVisibility` to set yourself invisible to others and then try to publish the stream. Receive message from [onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onvideopublishstatechanged), onAudioPublishStateChanged{@link #IRTCRoomEventHandler#onAudioPublishStateChanged. |
|kWarningCodeSendCustomMessage |\-2011 |Sending a custom broadcast message failed, you are not currently in the room. |
|kWarningCodeUserNotifyStop |\-2013 |When the number of people in the room exceeds 500, stop sending `onUserJoined` and `onUserLeave` callbacks to existing users in the room, and prompt all users in the room via broadcast. Receive message from [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) callback. |
|kWarningCodeUserInPublish |\-2014 |The user has published in another room. Receive message from [onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onvideopublishstatechanged), onAudioPublishStateChanged{@link #IRTCRoomEventHandler#onAudioPublishStateChanged. |
|kWarningCodeInEchoTestMode |\-2017 |This interface has been disabled because the engine is in echo testing mode. |
|kWarningCodeNoCameraPermission |\-5001 |The camera permission is abnormal, and the current application does not obtain the camera permission. |
|kWarningCodeNoMicrophonePermission |\-5002 |Deprecated since 3.45. Please use [MediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70098#MediaDeviceError).kMediaDeviceErrorDeviceNoPermission instead.<br><br>The microphone permission is abnormal, and the current application does not obtain microphone permission. |
|kWarningCodeRecodingDeviceStartFailed |\-5003 |Deprecated since 3.45. Please use [MediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70098#MediaDeviceError).kMediaDeviceErrorDeviceFailure instead.<br><br>The audio capture device failed to start, and the current device may be occupied by other applications. |
|kWarningCodePlayoutDeviceStartFailed |\-5004 |Deprecated since 3.45. Please use [MediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70098#MediaDeviceError).kMediaDeviceErrorDeviceFailure instead.<br><br>The audio playback device failed to start, which may be due to insufficient system resources or wrong parameters. |
|kWarningCodeNoRecordingDevice |\-5005 |Deprecated since 3.45. Please use [MediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70098#MediaDeviceError).kMediaDeviceErrorDeviceNotFound instead.<br><br>No audio acquisition device is available, please insert the available audio acquisition device. |
|kWarningCodeNoPlayoutDevice |\-5006 |Deprecated since 3.45. Please use [MediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70098#MediaDeviceError).kMediaDeviceErrorDeviceNotFound instead.<br><br>No audio playback device is available, please insert an available audio playback device. |
|kWarningCodeRecordingSilence |\-5007 |Deprecated since 3.45. Please use [MediaDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70098#MediaDeviceWarning).kMediaDeviceWarningCaptureSilence instead.<br><br>The current audio equipment has not collected valid sound data, please check and replace the audio capture device. |
|kWarningCodeMediaDeviceOperationDenied |\-5008 |Deprecated since 3.45. Please use [MediaDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70098#MediaDeviceWarning).kMediaDeviceWarningOperationDenied instead.<br><br>Warning on mishandling media devices.<br><br>When using custom acquisition, the internal acquisition switch cannot be called, and this warning will be triggered when called. |
|kWarningCodeSetScreenAudioSourceTypeFailed |\-5009 |You must call `setScreenAudioSourceType` before calling publishStreamAudio. |
|kWarningCodeSetScreenAudioStreamIndexFailed |\-5010 |Setting the audio capture method for screen sharing via `setScreenAudioStreamIndex` after calling publishStreamAudio is not supported. |
|kWarningCodeInvalidVoicePitch |\-5011 |Invalid pitch value setting |
|kWarningCodeInvalidAudioFormat |\-5012 |Invalid audio format setting |
|kWarningCodeInvalidCallForExtAudio |\-5013 |Mixed use of old and new APIs for external audio sources |
|kWarningCodeInvalidRemoteStreamKey |\-5014 |Invalid remote streamKey |
|kWarningCodeInvalidCanvasHandle |\-6001 |The specified internal rendering canvas handle is invalid.<br><br>This callback is triggered when you specify an invalid canvas handle when you call [setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setlocalvideocanvas). |
|kWarningLicenseFileExpired |\-7001 |The authentication file is invalid. When checking the status of the authentication file, if the local file is inconsistent with the remote file, a second warning will be triggered. Receive message from [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) callback. |
|kWarningInvaildSamiAppkeyORToken |\-7002 |Authorization failure for [BytePlus Audio SDK](https://go.byteplus.com/audio-sdk). Contact the technical support. |
|kWarningInvaildSamiResourcePath |\-7003 |Failure to get the resource for [BytePlus Audio SDK](https://go.byteplus.com/audio-sdk). Input the right DAT path or contact the technical support. |
|kWarningLoadSamiLibraryFailed |\-7004 |Failure to load the library for [BytePlus Audio SDK](https://go.byteplus.com/audio-sdk). Use the right library or contact the technical support. |
|kWarningInvaildSamiEffectType |\-7005 |The audio effect is not supported by [BytePlus Audio SDK](https://go.byteplus.com/audio-sdk). Contact the technical support. |


<span id="LoginErrorCode"></span>
# LoginErrorCode

```cpp
enum bytertc::LoginErrorCode
```


login result

The result of calling `login` will notify the user through the `onLoginResult` callback.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kLoginErrorCodeSuccess |0 |Call the `login` method to sign in successfully |
|kLoginErrorCodeInvalidToken |\-1000 |The Token used when calling the `login` method is invalid or expired, requiring the user to reacquire the Token. |
|kLoginErrorCodeLoginFailed |\-1001 |login error<br><br>An unknown error occurred when calling the `login` method, which caused the login to fail and requires re\-login. |
|kLoginErrorCodeInvalidUserId |\-1002 |There was a problem with the user ID passed in when the `login` method was called. |
|kLoginErrorCodeServerError |\-1003 |An error occurred at the server level when calling `login` to sign in. |
|kLoginErrorCodeLimitedMode |\-1004 |An error occurred when calling `login` to sign in, try to apply for unlimited rts mode. |


<span id="RtsWarningCode"></span>
# RtsWarningCode

```cpp
enum bytertc::RtsWarningCode
```


Callback warning code. The warning code indicates that there is a problem within the SDK and is trying to recover. Warning codes only serve as notifications.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRtsWarningCodeJoinRoomFailed |\-2001 |Failed to enter the room.<br><br>When you call the first time to join the room or disconnect and reconnect due to poor network conditions, the room entry fails due to a server error. The SDK automatically retries joining the room. |
|kRtsWarningCodePublishStreamFailed |\-2002 |Failed to publish audio & video streams.<br><br>When you publish audio & video streams in your room, the publication fails due to a server error. The SDK automatically retries the release. |
|kRtsWarningCodeSendCustomMessage |\-2011 |Sending a custom broadcast message failed, you are not currently in the room. |
|kRtsWarningCodeUserNotifyStop |\-2013 |When the number of people in the room exceeds 500, stop sending `onUserJoined` and `onUserLeave` callbacks to existing users in the room, and prompt all users in the room via broadcast. |
|kRtsWarningCodeOldRoomBeenReplaced |\-2016 |The old room has been replaced by a new room with the same roomId |


<span id="NetworkDetectionStartReturn"></span>
# NetworkDetectionStartReturn

```cpp
enum bytertc::NetworkDetectionStartReturn
```


Return value to start probing

`startNetworkDetection` Return object type

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kNetworkDetectionStartReturnSuccess |0 |Network probing enabled successfully. |
|kNetworkDetectionStartReturnParamErr |1 |Failed to start probing. Parameter error, both uplink and downlink probes are 'false ', or the expected bandwidth exceeds the range [100,10000] |
|kNetworkDetectionStartReturnStreaming |2 |Failed to start probing. The reason for the failure is that stream publishing and subscribing have started |
|kNetworkDetectionStartReturnStarted |3 |Detection has started, no need to open it again |
|kNetworkDetectionStartReturnNotSupport |4 |Do not support this function |


<span id="ErrorCode"></span>
# ErrorCode

```cpp
enum bytertc::ErrorCode
```


Callback error code.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kErrorCodeInvalidToken |\-1000 |Token is invalid. Receive message from [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) callback.<br><br>The Token used when calling [joinRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-joinroom) is invalid or expired. The user is required to retrieve the token and call the [updateToken](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-updatetoken) to update the token. |
|kErrorCodeJoinRoom |\-1001 |Join room error. Receive message from [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) callback.<br><br>An unknown error occurred while joining the room, which caused the joining room to fail. Users are required to rejoin the room. |
|kErrorCodeNoPublishPermission |\-1002 |No permission to publish audio & video streams. Receive message from [onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onvideopublishstatechanged), onAudioPublishStateChanged{@link #IRTCRoomEventHandler#onAudioPublishStateChanged.<br><br>The user failed to publish the audio & video stream in the room. The reason for the failure is that the user does not have permission to publish the stream. |
|kErrorCodeNoSubscribePermission |\-1003 |No subscription permissions for audio & video streams. Receive message from [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onvideosubscribestatechanged), [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onaudiosubscribestatechanged) callback.<br><br>The user failed to subscribe to the audio & video stream in the room where the user is located. The reason for the failure is that the user does not have permission to subscribe to the stream. |
|kErrorCodeDuplicateLogin |\-1004 |The user has been removed from the room because the same user joined the room on another client. Receive message from [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) callback. |
|kErrorCodeKickedOut |\-1006 |The user has been removed from the room by the administrator via an OpenAPI call. Receive message from [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) callback. |
|kRoomErrorTokenExpired |\-1009 |Token expired. This error code is returned when the user's token expires in the room. Receive message from [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) callback.<br><br>Call [joinRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-joinroom) to rejoin the room with a new required Token. |
|kRoomErrorUpdateTokenWithInvalidToken |\-1010 |The Token you provided when calling `updateToken` is invalid. Receive message from [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) callback. |
|kErrorCodeRoomDismiss |\-1011 |Users have been removed from the room because the administrator dismissed the room by calling OpenAPI. Receive message from [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) callback. |
|kErrorCodeRoomAlreadyExist |\-1013 |There is a room with the same roomId, whose room id is the same as echo test. Receive message from [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) callback. |
|kErrorCodeUserIDDifferent |\-1014 |The local user joins multiple rooms with different uids. Receive message from [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) callback.<br><br>In the same engine instance, users need to use the same uid to join different rooms. |
|kErrorCodeJoinRoomRoomForbidden |\-1025 |The room has been banned before the user calls `joinRoom`. Receive message from [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) callback. |
|kErrorCodeJoinRoomUserForbidden |\-1026 |The user has been banned before calling `joinRoom`. Receive message from [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) callback. |
|kErrorCodeOverStreamSubscribeLimit |\-1070 |Subscription to audio & video stream failed, the total number of subscribed audio & video streams exceeded the upper limit. Receive message from [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onvideosubscribestatechanged), [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onaudiosubscribestatechanged) callback.<br><br>In the game scenario, in order to ensure the performance and quality of audio & video calls, the server will limit the total number of audio & video streams subscribed by the user. When the total number of audio & video streams subscribed by the user has reached the maximum, continuing to subscribe to more streams will fail, and the user will receive this error notification. |
|kErrorCodeOverStreamPublishLimit |\-1080 |Publishing flow failed, the total number of publishing flows exceeds the upper limit. Receive message from [onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onvideopublishstatechanged), onAudioPublishStateChanged{@link #IRTCRoomEventHandler#onAudioPublishStateChanged.<br><br>RTC system limits the total number of streams published in a single room, including video streams, audio streams, and screen streams. Local users will fail to publish streams to the room when the maximum number of published streams in the room has been reached, and will receive this error notification. |
|kErrorCodeAbnormalServerStatus |\-1084 |The user has been removed from the room due to the abnormal server status. Receive message from [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) callback.<br><br>SDK is disconnected from the signaling server. It will not reconnect automatically. Please contact technical support. |
|[deprecated] kErrorCodeOverVideoPublishLimit |\-1082 |Deprecated since 3.52, use kErrorCodeOverStreamPublishLimit（\-1080）instead<br><br>The total number of published video streams exceeds the upper limit. Receive message from [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) callback.<br><br>The RTC system limits the number of video streams posted in a single room. If the maximum number of video streams posted in the room has been reached, local users will fail to post video streams to the room again and will receive this error notification. |
|[deprecated] kErrorCodeInvalidAudioSyncUidRepeated |\-1083 |Deprecated since 3.60, use kAVSyncEventInvalidUidRepeated carried by [onAVSyncEvent](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onavsyncevent) instead.<br><br>A/V synchronization failed. Receive message from onStreamStateChanged callback.<br><br>Current source audio ID has been set by other video publishers in the same room.<br><br>One single audio source cannot be synchronized with multiple video sources at the same time. |


<span id="SingleStreamTaskErrorCode"></span>
# SingleStreamTaskErrorCode

```cpp
enum bytertc::SingleStreamTaskErrorCode
```


Single stream errors.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kSingleStreamTaskErrorCodeOK |0 |Everything is OK. |
|kSingleStreamTaskErrorCodeUnKnownByServer |1091 |Unknown error from server. |
|kSingleStreamTaskErrorCodeSignalRequestTimeout |1092 |Request timed out. Please check network status and retry. |
|kSingleStreamTaskErrorCodeInvalidParamByServer |1093 |The server detects that the task parameters are invalid |
|kSingleStreamTaskErrorRemoteKicked |1094 |In the relay task, the user ID in the target room has been kicked out of the target room. |
|kSingleStreamTaskErrorCodeJoinDestRoomFailed |1095 |The relay task failed to join the target room. |
|kSingleStreamTaskErrorCodeReceiveSrcStreamTimeout |1096 |The stream pulling for the relay task in the source room timed out. |
|kSingleStreamTaskErrorCodeNotSurportCodec |1097 |Audio and video encoding relay tasks are not supported |
|kSingleStreamTaskErrorCodePushToCDN |1098 |Failed to push the single stream to CDN. |
|kSingleStreamTaskErrorCodeCountOverLimit |1099 |The number of concurrent single\-stream push tasks for the host exceeds the limit of 20. |


<span id="AudioRecordingErrorCode"></span>
# AudioRecordingErrorCode

```cpp
enum bytertc::AudioRecordingErrorCode
```


Error code for audio recording.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioRecordingErrorCodeOk |0 |OK |
|kAudioRecordingErrorCodeNoPermission |\-1 |No file write permissions. |
|kAudioRecordingErrorCodeNotInRoom |\-2 |Not in the room. |
|kAudioRecordingErrorCodeAlreadyStarted |\-3 |Started. |
|kAudioRecordingErrorCodeNotStarted |\-4 |Not started. |
|kAudioRecordingErrorCodeNotSupport |\-5 |Failure. Invalid file format. |
|kAudioRecordingErrorCodeOther |\-6 |Other error. |


<span id="RtsErrorCode"></span>
# RtsErrorCode

```cpp
enum bytertc::RtsErrorCode
```


Callback error code.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kRtsErrorCodeInvalidToken |\-1000 |Token is invalid.<br><br>The Token used when joining the room is invalid or expired. The user is required to retrieve the token and call the `updateToken` to update the token. |
|kRtsErrorCodeJoinRoom |\-1001 |Join room error.<br><br>An unknown error occurred while joining the room, which caused the joining room to fail. Users are required to rejoin the room. |
|kRtsErrorCodeDuplicateLogin |\-1004 |The user has been removed from the room because the same user joined the room on another client. |
|kRtsErrorCodeKickedOut |\-1006 |The user has been removed from the room by the administrator via an OpenAPI call. |
|kRtsRoomErrorCodeRoomIdIllegal |\-1007 |When calling `createRTCRoom`, if the roomid is illegal, it will return null and throw the error |
|kRtsRoomErrorTokenExpired |\-1009 |Token expired. Call `joinRoom` to rejoin with a valid Token. |
|kRtsRoomErrorUpdateTokenWithInvalidToken |\-1010 |The Token you provided when calling `updateToken` is invalid. |
|kRtsErrorCodeRoomDismiss |\-1011 |Users have been removed from the room because the administrator dismissed the room by calling OpenAPI. |
|kRtsErrorCodeRoomAlreadyExist |\-1013 |There is a room with the same roomId, whose room id is the same as echo test |
|kRtsErrorCodeUserIDDifferent |\-1014 |The user name set by the same engine instance when entering multiple rooms must be the same |
|kRtsErrorCodeAbnormalServerStatus |\-1084 |The user has been removed from the room due to the abnormal server status.<br><br>SDK is disconnected from the signaling server. It will not reconnect automatically. Please contact technical support. |
|kRtsErrorCodeJoinRoomLimitedMode |\-1013 |Join room error. |


<span id="SingleStreamTaskEvent"></span>
# SingleStreamTaskEvent

```cpp
enum bytertc::SingleStreamTaskEvent
```


Event of pushing a single stream to CDN.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kSingleStreamTaskEventStartSuccess |1 |The task initiated successfully. |
|kSingleStreamTaskEventStartFailed |2 |Failed to initiate the task. |
|kSingleStreamTaskEventStopSuccess |3 |The task stopped. |
|kSingleStreamTaskEventStopFailed |4 |Failed to stop the task. |
|kSingleStreamTaskEventWarning |5 |Warnings |
