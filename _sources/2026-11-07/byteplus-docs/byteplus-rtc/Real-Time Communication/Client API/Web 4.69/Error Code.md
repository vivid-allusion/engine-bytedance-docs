---
title: "Error Code"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104480"
---

<span id="errorcode"></span>
## ErrorCode  

Type: `enum`


* **Member**

   
   |Property |Value |Description |
   |---|---|---|
   |INVALID_ENGINE |`'INVALID_ENGINE'` |Invalid param. Triggered when you call `destroyEngine` with an invalid engine object. |
   |INVALID_PARAMS |`'INVALID_PARAMS'` |Generally used error code. Triggered when you call any API with invalid parameters. Please refer to the API documentation and pass in the correct parameters. |
   |INVALID_TOKEN |`'INVALID_TOKEN'` |Invalid Token. Triggered when you call `joinRoom` with an invalid or expired Token. Please obtain a new Token and call `joinRoom` again. |
   |JOIN_ROOM_FAILED |`'JOIN_ROOM_FAILED'` |Triggered when the user fails to enter the room after `joinRoom` is called. Please check the returned message for the specific reason. |
   |UPDATE_TOKEN_WITH_INVALID_TOKEN |`'UPDATE_TOKEN_WITH_INVALID_TOKEN'` |Invalid Token. Triggered when you call `updateToken` with an invalid Token. |
   |UPDATE_TOKEN_BEFORE_JOIN |`'UPDATE_TOKEN_BEFORE_JOIN'` |The user has not joined a room yet. Triggered When you call `updateToken` before the user enters the room. Please make sure the user is already in the room first. |
   |REPEAT_JOIN |`'REPEAT_JOIN'` |Join the same room repeatedly. Triggered when you call `joinRoom` after the user enters the room. |
   |REPEAT_PUSH |`'REPEAT_PUSH'` |Publish a WTN stream repeatedly. Triggered when you call `startPushPublicStream` after the WTN stream has been published. |
   |REPEAT_PLAY |`'REPEAT_PLAY'` |Subscribe to a WTN stream repeatedly. Triggered when repeatedly calling `startPlayPublicStream` to subscribe to the same WTN stream. |
   |NO_PUBLISH_PERMISSION |`'NO_PUBLISH_PERMISSION'` |No permission to publish streams. Triggered when you call `publishStream` or `publishScreen` to publish streams after setting the user to be invisible to others in the room with `setUserVisibility`. Please switch the user to be visible first. |
   |STREAM_NOT_EXIST |`'STREAM_NOT_EXIST'` |The target stream does not exist. Triggered when you call `subscribeStream`/`unsubscribeStream` to subscribe to or unsubscribe from a stream that does not exist, or `takeRemoteSnapshot` to take a screenshot of a remote stream that does not exist. Please enter the correct ID or make sure that the target stream is in the room. |
   |NOT_CONNECTED_YET |`'NOT_CONNECTED_YET'` |No connection has been built. Triggered when you call the current API while the SDK has not connected to the server yet. Please make sure the user has joined the room when you call the method, or check if the network connection is normal. |
   |KICKED_OUT |`'KICKED_OUT'` |The user has been removed from the room by the administrator via an OpenAPI call. Triggered through the `onError` callback. |
   |ROOM_DISMISS |`'ROOM_DISMISS'` |All the users have been removed from the room because the administrator dismissed the room by calling an OpenAPI. Triggered through the `onError` callback. |
   |TOKEN_EXPIRED |`'TOKEN_EXPIRED'` |The token expires after the user joins the room. Triggered through the `onError` callback. Please obtain a new Token and call `joinRoom` to re\-enter the room with the new Token. |
   |TOKEN_NO_PUBLISH_PERMISSION |`'TOKEN_NO_PUBLISH_PERMISSION'` |Token expired. Call `updateToken` to update publishing permission with the new token. |
   |TOKEN_NO_SUBSCRIBE_PERMISSION |`'TOKEN_NO_SUBSCRIBE_PERMISSION'` |Token expired. Call `updateToken` to update subscription permission with the new token. |
   |DUPLICATE_LOGIN |`'DUPLICATE_LOGIN'` |The user has been removed from the room because the same user joined the room on another client. Triggered through the `onError` callback. |
   |INVOKED_BEFORE_CAPTURE |`'INVOKED_BEFORE_CAPTURE'` |No such stream. Triggered when you call `takeLocalSnapshot` to take a screenshot of a local stream that does not exist. Please make sure that the specified stream has been published. |
   |REPEAT_CAPTURE |`'REPEAT_CAPTURE'` |Capture has started. Triggered when you repeatedly call `startAudioCapture`, `startVideoCapture`, or `startAudioAndVideoCapture` to capture audio/video streams. |
   |GET_VIDEO_TRACK_FAILED |`'GET_VIDEO_TRACK_FAILED'` |Capture failed. Triggered when you fail to start video capture with `startVideoCapture` or `startAudioAndVideoCapture`. Please check if there are available capture devices or if they are being used by other apps. |
   |GET_AUDIO_TRACK_FAILED |`'GET_AUDIO_TRACK_FAILED'` |Capture failed. Triggered when you fail to Start audio capture with `startAudioCapture` or `startAudioAndVideoCapture`. Please check if there are available capture devices or if they are being used by other apps. |
   |GET_SCREEN_TRACK_FAILED |`'GET_SCREEN_TRACK_FAILED'` |Capture failed. Triggered when you fail to start screen capture with `startScreenCapture`. |
   |STREAM_TYPE_NOT_MATCH |`'STREAM_TYPE_NOT_MATCH'` |Wrong stream type. Triggered when you call `startAudioCapture`, `stopAudioCapture`, `startVideoCapture`, `stopVideoCapture`, `startAudioAndVideoCapture` or other APIs related to internal capture after switching to the custom stream source with `setAudioSourceType` or `setVideoSourceType`. |
   |CANT_FIND_DOM |`'CANT_FIND_DOM'` |No DOM. Triggered when passing in a DOM that does not exist by calling `setLocalVideoPlayer` or `setRemoteVideoPlayer`. |
   |INVALID_DEVICE_ID |`'INVALID_DEVICE_ID'` |Invalid device ID. Triggered when setting an invalid ID by calling `setAudioPlaybackDevice`. |
   |NOT_SUPPORTED |`'NOT_SUPPORTED'` |Operation not supported. Triggered when you call `startAudioDeviceRecordTest` or `setAudioPlaybackDevice` if the browser does not support audio device test or audio capture. |
   |ICE_SERVER_WRONG |`'ICE_SERVER_WRONG'` |Triggered when the ICE node request fails after you call `joinRoom`. |
   |LOAD_RESOURCES_FAILED |`'LOAD_RESOURCES_FAILED'` |Loading resource failed. Triggered when resources fail to be loaded after you call `startAudioMixing` or `preloadAudioMixing`. Please pass in the correct resource path. |
   |TIME_OUT |`'TIME_OUT'` |Generally used error code in the majority of features. Triggered if no acknowledgement is received within 60s. |
   |ADD_TRANSCEIVER_FAILED |`'ADD_TRANSCEIVER_FAILED'` |Failure of building a peer\-connection to the signal server for the failure of building transceiver |
   |PUBLISH_FAILED |`'PUBLISH_FAILED'` |Triggered when you fail to publish a stream by calling `publishStream` or `publishScreen`. Please check the returned message for the specific reason. |
   |OPERATION_CANCEL |`'OPERATION_CANCEL'` |Generally used error code. Triggered when leaving room in the middle of operations such as publishing or subscribing to a stream. |
   |START_CLOUD_PROXY_AFTER_JOIN |`'START_CLOUD_PROXY_AFTER_JOIN'` |Wrong API call timing. Triggered when you call `startCloudProxy` after the user has joined the room. Please call `startCloudProxy` when the user is out of the room. |
   |STOP_CLOUD_PROXY_BEFORE_LEAVE |`'STOP_CLOUD_PROXY_BEFORE_LEAVE'` |Wrong API call timing. Triggered when you call `stopCloudProxy` while the user is still in the room. Please call `stopCloudProxy` when the user is out of the room. |
   |UNEXPECTED_ERROR |`'UNEXPECTED_ERROR'` |Generally used error code. Please check the returned message for the specific reason. |
   |REPEAT_DEVICE_TEST |`'REPEAT_DEVICE_TEST'` |The test has started. Triggered when you call `startAudioPlaybackDeviceTest` or `startAudioDeviceRecordTest` to start another device test while the current one is still ongoing. |
   |AUDIO_DEVICE_TEST_FAILED |`'AUDIO_DEVICE_RECORD_FAILED'` |Triggered when you fail to start the audio device test by calling `startAudioDeviceRecordTest`. Please try again. |
   |ALREADY_LOGIN |`'ALREADY_LOGIN'` |The user has already logged in. Triggered when you call `login` with a used userId. Please call `login` with a different userId. |
   |LOGIN_FAILED |`'LOGIN_FAILED'` |Login failed. Triggered when you fail to sign in to the real\-time signaling server by calling `login`. Please check the returned message for the specific reason. |
   |NOT_LOGIN |`'NOT_LOGIN'` |Generally used error code in message\-related features. The user has not logged in. Triggered when you call the message\-related APIs before successfully logging in to the real\-time signaling server by calling `login`. |
   |RTM_DUPLICATE_LOGIN |`'RTM_DUPLICATE_LOGIN'` |The local user is kicked out. Triggered through the `onError` callback when another user logs in with the same userId as the local user. |
   |RTM_TOKEN_ERROR |`'RTM_TOKEN_ERROR'` |The Token is invalid. Triggered in the case of Token verification exception during the process of reconnecting to the real\-time signaling server. Please call `login` with a new Token. |
   |USER_MESSAGE_TIMEOUT |`'USER_MESSAGE_TIMEOUT'` |P2P message failed to be sent due to a timeout. Triggered when a timeout occurs while sending a P2P message by calling methods including `sendUserMessage`, `sendUserBinaryMessage`, `sendUserMessageOutsideRoom`, `sendUserBinaryMessageOutsideRoom`, `sendServerMessage`, and `sendServerBinaryMessage`. |
   |USER_MESSAGE_BROKEN |`'USER_MESSAGE_BROKEN'` |P2P message failed to be sent due to a broken channel. Triggered when you call methods including `sendUserMessage`, `sendUserBinaryMessage`, `sendUserMessageOutsideRoom`, `sendUserBinaryMessageOutsideRoom`, `sendServerMessage`, and `sendServerBinaryMessage` while the signal channel is broken. |
   |USER_MESSAGE_NO_RECEIVER |`'USER_MESSAGE_NO_RECEIVER'` |No receiver. Triggered if no receiver is found after calling `sendUserMessage`, `sendUserBinaryMessage`, `sendUserMessageOutsideRoom`, `sendUserBinaryMessageOutsideRoom`, `sendServerMessage`, and `sendServerBinaryMessage`. Please make sure you pass in the right userId. |
   |USER_MESSAGE_SEND_TO_SERVER_ERROR |`'USER_MESSAGE_SEND_TO_SERVER_ERROR'` |No response from the server. Triggered if Http request fails after calling `sendServerMessage` or `sendServerBinaryMessage` to send messages to the server. |
   |USER_MESSAGE_SERVER_RESPONSE_ERROR |`'USER_MESSAGE_SERVER_RESPONSE_ERROR'` |Failed to send message to the server. Probably triggered after calling `sendServerMessage` or `sendServerBinaryMessage`. Response status code is not 200. |
   |USER_MESSAGE_NOT_JOIN |`'USER_MESSAGE_NOT_JOIN'` |The user has not joined any room. Triggered when you call `sendUserMessage` or `sendUserBinaryMessage` out of a room. Please call `joinRoom` to join a room first. |
   |USER_MESSAGE_NOT_LOGIN |`'USER_MESSAGE_NOT_LOGIN'` |The user has not logged in yet. Triggered when you call `sendUserMessageOutsideRoom`, `sendUserBinaryMessageOutsideRoom`, `sendServerMessage`, and `sendServerBinaryMessage` before logging in to the real\-time signaling server. Please call `login` first. |
   |USER_MESSAGE_SERVER_PARAMS_NOTSET |`'USER_MESSAGE_SERVER_PARAMS_NOTSET'` |The server params have not been set yet. Triggered when you call `sendServerMessage` or `sendServerBinaryMessage` without setting params to the server. Please call `setServerParam` first. |
   |USER_MESSAGE_UNKNOWN |`'USER_MESSAGE_UNKNOWN'` |Unknown error. Triggered when an unknown error occurred after calling `sendUserMessage`, `sendUserBinaryMessage`, `sendUserMessageOutsideRoom`, `sendUserBinaryMessageOutsideRoom`, `sendServerMessage` or `sendServerBinaryMessage`. |
   |RECONNECT_FAILED |`'RECONNECT_FAILED'` |Reconnection failed. Triggered through the `onError` callback if the SDK fails to reconnect to the server. The SDK will no longer automatically retry. Please leave room first and join room again, or contact the technical support. |
   |UNEXPECTED_INVOKE_FORWARD_STREAM |`'UNEXPECTED_INVOKE_FORWARD_STREAM'` |Unexpected operation. Triggered if the timing of API calls related to forwarding media streams across rooms is incorrect. Please refer to the documentation of each API to confirm the correct order of API calls. |
   |ROOM_FORBIDDEN |`'ROOM_FORBIDDEN'` |The room is banned. Triggered when you call `joinRoom` to join a room that has already been banned from the server. |
   |USER_FORBIDDEN |`'USER_FORBIDDEN'` |The user is banned. Triggered when you call `joinRoom` after the local user is banned. |
   |ERR_ELECTRON_IS_NULL |`'ERR_ELECTRON_IS_NULL'` |Failed to get the Electron instance. Ensure the environment meets the requirements for Electron development. Refer to [PC Screen Sharing by Web SDK in Electron](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1340581) for more. |
   |ELECTRON_DESKTOP_CAPTURER_GET_SOURCES_ERROR |`'ELECTRON_DESKTOP_CAPTURER_GET_SOURCES_ERROR'` |Failed to get the screen sharing source in Electron environment. |
   |SET_SIMULCAST_FAILED |`'SET_SIMULCAST_FAILED'` |Failed to change the simulcast settings. Ensure that the timing of calling [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setlocalsimulcastmode) is correct.<br><br>You can change the resolution after publishing, but not the number of streams. |
   |MIXING_OLD_AND_NEW_APIS |`'MIXING_OLD_AND_NEW_APIS'` |Mixing the deprecated methods of the Simulcast feature with the current methods is forbidden. The deprecated methods will no longer be maintained in future versions and are expected to be removed after several updates. It is advised to switch to the current methods as soon as possible.<br><br>+ `setRemoteVideoConfig` is deprecated. Please use [setRemoteSimulcastStreamType](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setremotesimulcaststreamtype) instead.<br><br>+ `enableSimulcastMode` is deprecated. Please use [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setlocalsimulcastmode) instead. |
   |WTN_PUSH_FAILED |`'WTN_PUSH_FAILED'` |Failed to publish the WTN stream via [startPushWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startpushwtn). |
   |WTN_PLAY_FAILED |`'WTN_PLAY_FAILED'` |Failed to subscribe to the WTN stream via [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn). |
   |NOT_ALLOWED_IN_RTS_ROOM |`'NOT_ALLOWED_IN_RTS_ROOM'` |The `RoomMode` is `ROOM_MODE_RTS_ONLY` (indicating that only RTS can be used in the room). Calling the room\-external API is not allowed. |
   |NOT_ALLOWED_IN_RESTRICTED_MODE |`'NOT_ALLOWED_IN_RESTRICTED_MODE'` |Calling the room\-external message class API is not allowed in the RTS restricted mode. |
   


<span id="audiomixingerror"></span>
## AudioMixingError  

Type: `enum`

Audio mixing error codes. Returned through the [onAudioMixingStateChanged](https://docs.byteplus.com/en/docs/12/docs-104479#onaudiomixingstatechanged) callback.


* **Member**

   
   |Property |Value |Description |
   |---|---|---|
   |AUDIO_MIXING_ERROR_OK |`0` |Normal |
   |AUDIO_MIXING_ERROR_PRELOAD_FAILED |`1` |Pre\-load fails because of missing audio file or the length of the audio file exceeding 20s. |
   |AUDIO_MIXING_ERROR_START_FAILED |`2` |Audio mixing fails to start because of missing audio file or failure of reading the audio file. |
   |AUDIO_MIXING_ERROR_ID_NOT_FOUND |`3` |Invalid audio mixing ID |
   |AUDIO_MIXING_ERROR_SET_POSITION_FAILED |`4` |Invalid start position |
   |AUDIO_MIXING_ERROR_INVALID_VOLUME |`5` |Invalid volume argument. The volume value ranges [0, 400]. |
   |AUDIO_MIXING_ERROR_LOAD_CONFLICT |`6` |The audio file to be played does not match the preload one. Call `unloadAudioMixing` to unload file and proceed. |
   |AUDIO_MIXING_ERROR_ID_TYPE_NOT_MATCH |`7` |Type of the audio file to be played is not supported. |
   |AUDIO_MIXING_ERROR_ID_TYPE_INVALID_PITCH |`8` |Invalid audio pitch |
   |AUDIO_MIXING_ERROR_INVALID_AUDIO_TRACK |`9` |Invalid audio track |
   


<span id="streammixingeventerrorcode"></span>
## StreamMixingEventErrorCode  

Type: `enum`

The error codes of pushing a mixed stream to CDN events. Returned through the [onStreamMixingEvent](https://docs.byteplus.com/en/docs/12/docs-104479#onstreammixingevent) callback.


* **Member**

   
   |Property |Value |Description |
   |---|---|---|
   |ERR_OK |`0` |Success. |
   |ERR_PARAM_INVALID |`1` |Failure. Invalid configuration parameters. |
   |ERR_FRAME_TIMEOUT |`2` |RTC connection failure. The RTC server will be auto\-reconnected. |
   |ERR_POSTPROCESS |`3` |Errors occur during stream mixing. Please retry your request. |
   |ERR_PUSH_CDN |`4` |Failure. Please wait for a re\-push. |
   |ERR_UNKNOWN |`9999` |Other unknown errors. |
   


<span id="forwardstreamerror"></span>
## ForwardStreamError  

Type: `enum`

Forward stream error code. Returned through the [onForwardStreamError](https://docs.byteplus.com/en/docs/12/docs-104479#onforwardstreamerror) callback.


* **Member**

   
   |Property |Value |Description |
   |---|---|---|
   |FORWARD_STREAM_ERROR_OK |`0` |Success. |
   |FORWARD_STREAM_ERROR_INVALID_TOKEN |`1202` |Target room's token is invalid. |
   |FORWARD_STREAM_ERROR_RESPONSE |`1203` |Server side error. |
   |FORWARD_STREAM_ERROR_REMOTE_KICKED |`1204` |The source room is set as the target room. |
