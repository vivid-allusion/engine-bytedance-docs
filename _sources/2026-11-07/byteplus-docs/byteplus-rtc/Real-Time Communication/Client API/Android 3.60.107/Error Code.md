---
title: "Error Code"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70082"
---

<span id="SingleStreamTaskErrorCode"></span>
# SingleStreamTaskErrorCode

```java
public enum com.ss.bytertc.engine.live.SingleStreamTaskErrorCode
```


Single stream errors.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|OK |0 |Successfully pushed streams to target CDN. |
|UNKNOWN_BY_SERVER |1091 |Error from the server. |
|SIGNAL_REQUEST_TIMEOUT |1092 |Request timed out. Please check network status and retry. |
|INVALID_PARAM_BY_SERVER |1093 |The server detects that the task parameters are invalid |
|REMOTE_KICKED |1094 |In the relay task, the user ID in the target room has been kicked out of the target room. |
|JOIN_DEST_ROOM_FAIED |1095 |The relay task failed to join the target room. |
|RECEIVE_SRC_STREAM_TIMEOUT |1096 |The stream pulling for the relay task in the source room timed out. |
|NOT_SURPORT_CODEC |1097 |Audio and video encoding relay tasks are not supported |
|ERROR_PUSH_TO_CDN |1098 |Failed to push the single stream to CDN. |
|ERROR_TASK_COUNT_OVER_LIMIT |1099 |The number of concurrent single\-stream push tasks for the host exceeds the limit of 20. |


<span id="UserMessageSendResult"></span>
# UserMessageSendResult

```java
public class com.ss.bytertc.engine.type.UserMessageSendResult
```


Message sending result and the reason of failure if it fails.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |0 |[USER_MESSAGE_SEND_RESULT_SUCCESS](https://docs.byteplus.com/en/docs/12/14168#UserMessageSendResult-user_message_send_result_success) |
|int |1 |[USER_MESSAGE_SEND_RESULT_TIMEOUT](https://docs.byteplus.com/en/docs/12/14168#UserMessageSendResult-user_message_send_result_timeout) |
|int |2 |[USER_MESSAGE_SEND_RESULT_BROKEN](https://docs.byteplus.com/en/docs/12/14168#UserMessageSendResult-user_message_send_result_broken) |
|int |3 |[USER_MESSAGE_SEND_RESULT_NO_RECEIVER](https://docs.byteplus.com/en/docs/12/14168#UserMessageSendResult-user_message_send_result_no_receiver) |
|int |4 |[USER_MESSAGE_SEND_RESULT_NO_RELAY_PATH](https://docs.byteplus.com/en/docs/12/14168#UserMessageSendResult-user_message_send_result_no_relay_path) |
|int |5 |[USER_MESSAGE_SEND_RESULT_EXCEED_QPS](https://docs.byteplus.com/en/docs/12/14168#UserMessageSendResult-user_message_send_result_exceed_qps) |
|int |100 |[USER_MESSAGE_SEND_RESULT_NOT_JOIN](https://docs.byteplus.com/en/docs/12/14168#UserMessageSendResult-user_message_send_result_not_join) |
|int |101 |[USER_MESSAGE_SEND_RESULT_INIT](https://docs.byteplus.com/en/docs/12/14168#UserMessageSendResult-user_message_send_result_init) |
|int |102 |[USER_MESSAGE_SEND_RESULT_NO_CONNECTION](https://docs.byteplus.com/en/docs/12/14168#UserMessageSendResult-user_message_send_result_no_connection) |
|int |103 |[USER_MESSAGE_SEND_RESULT_EXCEED_MAX_LENGTH](https://docs.byteplus.com/en/docs/12/14168#UserMessageSendResult-user_message_send_result_exceed_max_length) |
|int |104 |[USER_MESSAGE_SEND_RESULT_EMPTY_USER](https://docs.byteplus.com/en/docs/12/14168#UserMessageSendResult-user_message_send_result_empty_user) |
|int |105 |[USER_MESSAGE_SEND_RESULT_NOT_LOGIN](https://docs.byteplus.com/en/docs/12/14168#UserMessageSendResult-user_message_send_result_not_login) |
|int |106 |[USER_MESSAGE_SEND_RESULT_SERVER_PARAMS_NOT_SET](https://docs.byteplus.com/en/docs/12/14168#UserMessageSendResult-user_message_send_result_server_params_not_set) |
|int |1000 |[USER_MESSAGE_SEND_RESULT_UNKNOWN](https://docs.byteplus.com/en/docs/12/14168#UserMessageSendResult-user_message_send_result_unknown) |


<span id="instructions"></span>
## Instructions

<span id="UserMessageSendResult-user_message_send_result_success"></span>
### USER_MESSAGE_SEND_RESULT_SUCCESS

```java
public static final int com.ss.bytertc.engine.type.UserMessageSendResult.USER_MESSAGE_SEND_RESULT_SUCCESS = 0
```


Message sent successfully.

<span id="UserMessageSendResult-user_message_send_result_timeout"></span>
### USER_MESSAGE_SEND_RESULT_TIMEOUT

```java
public static final int com.ss.bytertc.engine.type.UserMessageSendResult.USER_MESSAGE_SEND_RESULT_TIMEOUT = 1
```


Failure. A timeout occurred.

<span id="UserMessageSendResult-user_message_send_result_broken"></span>
### USER_MESSAGE_SEND_RESULT_BROKEN

```java
public static final int com.ss.bytertc.engine.type.UserMessageSendResult.USER_MESSAGE_SEND_RESULT_BROKEN = 2
```


Failure. The connection was lost before the message could be sent.

<span id="UserMessageSendResult-user_message_send_result_no_receiver"></span>
### USER_MESSAGE_SEND_RESULT_NO_RECEIVER

```java
public static final int com.ss.bytertc.engine.type.UserMessageSendResult.USER_MESSAGE_SEND_RESULT_NO_RECEIVER = 3
```


Failure. The recipient could not be found.

<span id="UserMessageSendResult-user_message_send_result_no_relay_path"></span>
### USER_MESSAGE_SEND_RESULT_NO_RELAY_PATH

```java
public static final int com.ss.bytertc.engine.type.UserMessageSendResult.USER_MESSAGE_SEND_RESULT_NO_RELAY_PATH = 4
```


Failure. The remote user is not logged in or has not joined a room.

<span id="UserMessageSendResult-user_message_send_result_exceed_qps"></span>
### USER_MESSAGE_SEND_RESULT_EXCEED_QPS

```java
public static final int com.ss.bytertc.engine.type.UserMessageSendResult.USER_MESSAGE_SEND_RESULT_EXCEED_QPS = 5
```


Failure. Exceeds QPS limit.

<span id="UserMessageSendResult-user_message_send_result_not_join"></span>
### USER_MESSAGE_SEND_RESULT_NOT_JOIN

```java
public static final int com.ss.bytertc.engine.type.UserMessageSendResult.USER_MESSAGE_SEND_RESULT_NOT_JOIN = 100
```


Failure. The sender has not joined the room.

<span id="UserMessageSendResult-user_message_send_result_init"></span>
### USER_MESSAGE_SEND_RESULT_INIT

```java
public static final int com.ss.bytertc.engine.type.UserMessageSendResult.USER_MESSAGE_SEND_RESULT_INIT = 101
```


Failure. The connection has not been initialized.

<span id="UserMessageSendResult-user_message_send_result_no_connection"></span>
### USER_MESSAGE_SEND_RESULT_NO_CONNECTION

```java
public static final int com.ss.bytertc.engine.type.UserMessageSendResult.USER_MESSAGE_SEND_RESULT_NO_CONNECTION = 102
```


Failure. No available data transmission channel.

<span id="UserMessageSendResult-user_message_send_result_exceed_max_length"></span>
### USER_MESSAGE_SEND_RESULT_EXCEED_MAX_LENGTH

```java
public static final int com.ss.bytertc.engine.type.UserMessageSendResult.USER_MESSAGE_SEND_RESULT_EXCEED_MAX_LENGTH = 103
```


Failure. The message size exceeds the maximum limit. The default maximum length of a message is 1 KB. If you [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode), the maximum length is 64 KB.

<span id="UserMessageSendResult-user_message_send_result_empty_user"></span>
### USER_MESSAGE_SEND_RESULT_EMPTY_USER

```java
public static final int com.ss.bytertc.engine.type.UserMessageSendResult.USER_MESSAGE_SEND_RESULT_EMPTY_USER = 104
```


Failure. The ID of the recipient is empty.

<span id="UserMessageSendResult-user_message_send_result_not_login"></span>
### USER_MESSAGE_SEND_RESULT_NOT_LOGIN

```java
public static final int com.ss.bytertc.engine.type.UserMessageSendResult.USER_MESSAGE_SEND_RESULT_NOT_LOGIN = 105
```


Failure. The sender is not signed in.

<span id="UserMessageSendResult-user_message_send_result_server_params_not_set"></span>
### USER_MESSAGE_SEND_RESULT_SERVER_PARAMS_NOT_SET

```java
public static final int com.ss.bytertc.engine.type.UserMessageSendResult.USER_MESSAGE_SEND_RESULT_SERVER_PARAMS_NOT_SET = 106
```


Failure. Required parameters for sending to the application server were not set.

<span id="UserMessageSendResult-user_message_send_result_unknown"></span>
### USER_MESSAGE_SEND_RESULT_UNKNOWN

```java
public static final int com.ss.bytertc.engine.type.UserMessageSendResult.USER_MESSAGE_SEND_RESULT_UNKNOWN = 1000
```


Failure. Unknown error.

<span id="MixedStreamTaskErrorCode"></span>
# MixedStreamTaskErrorCode

```java
public enum com.ss.bytertc.engine.live.MixedStreamTaskErrorCode
```


Mixing stream errors.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|OK |0 |Successfully pushed streams to target CDN. |
|TIMEOUT |1091 |Request timed out. Please check network status and retry. |
|INVALID_PARAM_BY_SERVER |1092 |Invalid parameters were detected by the server. |
|SUB_TIMEOUT_BY_SERVER |1093 |Subscription to the stream has expired. |
|INVALID_STATE_BY_SERVER |1094 |Internal server error. |
|AUTHENTICATION_BY_CDN |1095 |The server failed to push the mixing streams to CDN. |
|UNKNOWN_BY_SERVER |1096 |Unknown error from server. |
|SIGNAL_REQUEST_TIMEOUT |1097 |Signaling connection timeout error. Please check network status and retry. |
|MIX_IMAGE_FAIL |1098 |Failed to mix images. |
|PUSH_WTN_FAILED |1195 |Failed to push the WTN stream. |


<span id="AudioRecordingErrorCode"></span>
# AudioRecordingErrorCode

```java
public enum com.ss.bytertc.engine.type.AudioRecordingErrorCode
```


Error code for audio recording.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|AUDIO_RECORDING_ERROR_CODE_OK |0 |OK |
|AUDIO_RECORDING_ERROR_CODE_NO_PERMISSION |\-1 |No file write permissions. |
|AUDIO_RECORDING_ERROR_CODE_NOT_IN_ROOM |\-2 |Not in the room. |
|AUDIO_RECORDING_ERROR_CODE_ALREADY_STARTED |\-3 |Started. |
|AUDIO_RECORDING_ERROR_CODE_NOT_STARTED |\-4 |Not started. |
|AUDIO_RECORDING_ERROR_CODE_NOT_SUPPORT |\-5 |Failure. Invalid file format. |
|AUDIO_RECORDING_ERROR_CODE_OTHER |\-6 |Other error. |


<span id="SingleStreamTaskEvent"></span>
# SingleStreamTaskEvent

```java
public enum com.ss.bytertc.engine.live.SingleStreamTaskEvent
```


Event of pushing a single stream to CDN.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|START_SUCCESS |1 |The task initiated successfully. |
|START_FAILED |2 |Failed to initiate the task. |
|STOP_SUCCESS |3 |The task stopped. |
|STOP_FAILED |4 |Failed to stop the task. |
|WARNING |5 |Warnings. |


<span id="ErrorCode"></span>
# ErrorCode

```java
public class com.ss.bytertc.engine.type.ErrorCode
```


Callback error code. When an unrecoverable error is encountered inside the

SDK, the user is notified via an `onError` callback.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |\-1000 |[ERROR_CODE_INVALID_TOKEN](https://docs.byteplus.com/en/docs/12/14168#ErrorCode-error_code_invalid_token) |
|int |\-1001 |[ERROR_CODE_JOIN_ROOM](https://docs.byteplus.com/en/docs/12/14168#ErrorCode-error_code_join_room) |
|int |\-1002 |[ERROR_CODE_NO_PUBLISH_PERMISSION](https://docs.byteplus.com/en/docs/12/14168#ErrorCode-error_code_no_publish_permission) |
|int |\-1003 |[ERROR_CODE_NO_SUBSCRIBE_PERMISSION](https://docs.byteplus.com/en/docs/12/14168#ErrorCode-error_code_no_subscribe_permission) |
|int |\-1004 |[ERROR_CODE_DUPLICATE_LOGIN](https://docs.byteplus.com/en/docs/12/14168#ErrorCode-error_code_duplicate_login) |
|int |\-1005 |[ERROR_CODE_APP_ID_NULL](https://docs.byteplus.com/en/docs/12/14168#ErrorCode-error_code_app_id_null) |
|int |\-1006 |[ERROR_CODE_KICKED_OUT](https://docs.byteplus.com/en/docs/12/14168#ErrorCode-error_code_kicked_out) |
|int |\-1007 |[ERROR_CODE_ROOM_ID_ILLEGAL](https://docs.byteplus.com/en/docs/12/14168#ErrorCode-error_code_room_id_illegal) |
|int |\-1009 |[ERROR_CODE_TOKEN_EXPIRED](https://docs.byteplus.com/en/docs/12/14168#ErrorCode-error_code_token_expired) |
|int |\-1010 |[ERROR_CODE_UPDATE_TOKEN_WITH_INVALID_TOKEN](https://docs.byteplus.com/en/docs/12/14168#ErrorCode-error_code_update_token_with_invalid_token) |
|int |\-1011 |[ERROR_CODE_ROOM_DISMISS](https://docs.byteplus.com/en/docs/12/14168#ErrorCode-error_code_room_dismiss) |
|int |\-1013 |[ERROR_CODE_ROOM_ALREADY_EXIST](https://docs.byteplus.com/en/docs/12/14168#ErrorCode-error_code_room_already_exist) |
|int |\-1014 |[ERROR_CODE_USER_ID_DIFFERENT](https://docs.byteplus.com/en/docs/12/14168#ErrorCode-error_code_user_id_different) |
|int |\-1025 |[ERROR_CODE_JOIN_ROOM_ROOM_FORBIDDEN](https://docs.byteplus.com/en/docs/12/14168#ErrorCode-error_code_join_room_room_forbidden) |
|int |\-1026 |[ERROR_CODE_JOIN_ROOM_USER_FORBIDDEN](https://docs.byteplus.com/en/docs/12/14168#ErrorCode-error_code_join_room_user_forbidden) |
|int |\-1070 |[ERROR_CODE_OVER_SUBSCRIBE_LIMIT](https://docs.byteplus.com/en/docs/12/14168#ErrorCode-error_code_over_subscribe_limit) |
|int |\-1080 |[ERROR_CODE_OVER_STREAM_PUBLISH_LIMIT](https://docs.byteplus.com/en/docs/12/14168#ErrorCode-error_code_over_stream_publish_limit) |
|int |\-1084 |[ERROR_CODE_ABNORMAL_SERVER_STATUS](https://docs.byteplus.com/en/docs/12/14168#ErrorCode-error_code_abnormal_server_status) |
|int |\-1081 |[deprecated] [ERROR_CODE_OVER_SCREEN_PUBLISH_LIMIT](https://docs.byteplus.com/en/docs/12/14168#ErrorCode-error_code_over_screen_publish_limit) |
|int |\-1082 |[deprecated] [ERROR_CODE_OVER_VIDEO_PUBLISH_LIMIT](https://docs.byteplus.com/en/docs/12/14168#ErrorCode-error_code_over_video_publish_limit) |
|int |\-1083 |[deprecated] [ERROR_CODE_INVALID_AUDIO_SYNC_USERID_REPEATED](https://docs.byteplus.com/en/docs/12/14168#ErrorCode-error_code_invalid_audio_sync_userid_repeated) |


<span id="instructions"></span>
## Instructions

<span id="ErrorCode-error_code_invalid_token"></span>
### ERROR_CODE_INVALID_TOKEN

```java
public static final int com.ss.bytertc.engine.type.ErrorCode.ERROR_CODE_INVALID_TOKEN = -1000
```


The token is invalid. Returned by [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged).

The token used when entering the room is invalid or expired. The user is required to retrieve the token and call the `updateToken` method to update the token.

<span id="ErrorCode-error_code_join_room"></span>
### ERROR_CODE_JOIN_ROOM

```java
public static final int com.ss.bytertc.engine.type.ErrorCode.ERROR_CODE_JOIN_ROOM = -1001
```


Join room error. Returned by [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged).

An unknown error occurred while entering the room, which caused the joining room to fail. Users are required to rejoin the room.

<span id="ErrorCode-error_code_no_publish_permission"></span>
### ERROR_CODE_NO_PUBLISH_PERMISSION

```java
public static final int com.ss.bytertc.engine.type.ErrorCode.ERROR_CODE_NO_PUBLISH_PERMISSION = -1002
```


No permission to publish audio & video streams. Returned by [onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onvideopublishstatechanged), [onAudioPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onaudiopublishstatechanged).

The user failed to publish the audio & video stream in the room. The reason for the failure is that the user does not have permission to publish the stream.

<span id="ErrorCode-error_code_no_subscribe_permission"></span>
### ERROR_CODE_NO_SUBSCRIBE_PERMISSION

```java
public static final int com.ss.bytertc.engine.type.ErrorCode.ERROR_CODE_NO_SUBSCRIBE_PERMISSION = -1003
```


No subscription permissions for audio & video streams. Returned by [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onvideosubscribestatechanged), [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onaudiosubscribestatechanged).

The user failed to subscribe to the audio & video stream in the room where the user is located. The reason for the failure is that the user does not have permission to subscribe to the stream.

<span id="ErrorCode-error_code_duplicate_login"></span>
### ERROR_CODE_DUPLICATE_LOGIN

```java
public static final int com.ss.bytertc.engine.type.ErrorCode.ERROR_CODE_DUPLICATE_LOGIN = -1004
```


The user has been removed from the room because the same user joined the room on another client. Returned by [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged).

<span id="ErrorCode-error_code_app_id_null"></span>
### ERROR_CODE_APP_ID_NULL

```java
public static final int com.ss.bytertc.engine.type.ErrorCode.ERROR_CODE_APP_ID_NULL = -1005
```


The App ID parameter is abnormal.

The App ID parameter passed in when the engine was created is empty.

<span id="ErrorCode-error_code_kicked_out"></span>
### ERROR_CODE_KICKED_OUT

```java
public static final int com.ss.bytertc.engine.type.ErrorCode.ERROR_CODE_KICKED_OUT = -1006
```


The user has been removed from the room by the administrator via an OpenAPI call. Returned by [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged).

<span id="ErrorCode-error_code_room_id_illegal"></span>
### ERROR_CODE_ROOM_ID_ILLEGAL

```java
public static final int com.ss.bytertc.engine.type.ErrorCode.ERROR_CODE_ROOM_ID_ILLEGAL = -1007
```


When calling `createRoom`, if the roomId is illegal, it will return null and throw the error. Returned by [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged).

<span id="ErrorCode-error_code_token_expired"></span>
### ERROR_CODE_TOKEN_EXPIRED

```java
public static final int com.ss.bytertc.engine.type.ErrorCode.ERROR_CODE_TOKEN_EXPIRED = -1009
```


The token has expired. Call `joinRoom` to rejoin with a valid Token. Returned by [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged).

<span id="ErrorCode-error_code_update_token_with_invalid_token"></span>
### ERROR_CODE_UPDATE_TOKEN_WITH_INVALID_TOKEN

```java
public static final int com.ss.bytertc.engine.type.ErrorCode.ERROR_CODE_UPDATE_TOKEN_WITH_INVALID_TOKEN = -1010
```


The Token you provided when calling `updateToken` is invalid. Returned by [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged).

<span id="ErrorCode-error_code_room_dismiss"></span>
### ERROR_CODE_ROOM_DISMISS

```java
public static final int com.ss.bytertc.engine.type.ErrorCode.ERROR_CODE_ROOM_DISMISS = -1011
```


Users have been removed from the room because the administrator dismissed the room by calling OpenAPI. Returned by [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged).

<span id="ErrorCode-error_code_room_already_exist"></span>
### ERROR_CODE_ROOM_ALREADY_EXIST

```java
public static final int com.ss.bytertc.engine.type.ErrorCode.ERROR_CODE_ROOM_ALREADY_EXIST = -1013
```


A room with the same roomId already exists during the call echo test. Returned by [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged).

<span id="ErrorCode-error_code_user_id_different"></span>
### ERROR_CODE_USER_ID_DIFFERENT

```java
public static final int com.ss.bytertc.engine.type.ErrorCode.ERROR_CODE_USER_ID_DIFFERENT = -1014
```


The local user joins multiple rooms with different uids. Returned by [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged).

In the same engine instance, users need to use the same uid to join different rooms.

<span id="ErrorCode-error_code_join_room_room_forbidden"></span>
### ERROR_CODE_JOIN_ROOM_ROOM_FORBIDDEN

```java
public static final int com.ss.bytertc.engine.type.ErrorCode.ERROR_CODE_JOIN_ROOM_ROOM_FORBIDDEN = -1025
```


The room has been banned before the user calls `joinRoom`. Returned by [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged).

<span id="ErrorCode-error_code_join_room_user_forbidden"></span>
### ERROR_CODE_JOIN_ROOM_USER_FORBIDDEN

```java
public static final int com.ss.bytertc.engine.type.ErrorCode.ERROR_CODE_JOIN_ROOM_USER_FORBIDDEN = -1026
```


The user has been banned before calling `joinRoom`. Returned by [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged).

<span id="ErrorCode-error_code_over_subscribe_limit"></span>
### ERROR_CODE_OVER_SUBSCRIBE_LIMIT

```java
public static final int com.ss.bytertc.engine.type.ErrorCode.ERROR_CODE_OVER_SUBSCRIBE_LIMIT = -1070
```


Failed to subscribe to streams because the total number of subscribed streams has exceeded the upper limit. Returned by [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onvideosubscribestatechanged), [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onaudiosubscribestatechanged).

In order to ensure the performance and quality of audio & video calls in the game scenario, the server will limit the total number of audio & video streams subscribed by the user. When the total number of audio & video streams subscribed by the user has reached the maximum, continuing to subscribe to more streams will fail, and the user will receive this error notification.

<span id="ErrorCode-error_code_over_stream_publish_limit"></span>
### ERROR_CODE_OVER_STREAM_PUBLISH_LIMIT

```java
public static final int com.ss.bytertc.engine.type.ErrorCode.ERROR_CODE_OVER_STREAM_PUBLISH_LIMIT = -1080
```


Failed to publish video stream because the total number of published streams has exceeded the upper limit. Returned by [onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onvideopublishstatechanged), [onAudioPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onaudiopublishstatechanged).

RTC will limit the total number of streams published in a single room, including video, audio, and screen streams. Local users will fail to publish streams to the room when the maximum number of published streams in the room has been reached, and will receive this error notification.

<span id="ErrorCode-error_code_abnormal_server_status"></span>
### ERROR_CODE_ABNORMAL_SERVER_STATUS

```java
public static final int com.ss.bytertc.engine.type.ErrorCode.ERROR_CODE_ABNORMAL_SERVER_STATUS = -1084
```


The user has been removed from the room due to the abnormal status of the server. This code will be received via [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged).

The SDK is disconnected from the signaling server. It will not reconnect automatically. Please contact technical support.

<span id="ErrorCode-error_code_over_screen_publish_limit"></span>
### ERROR_CODE_OVER_SCREEN_PUBLISH_LIMIT

```java
public static final int com.ss.bytertc.engine.type.ErrorCode.ERROR_CODE_OVER_SCREEN_PUBLISH_LIMIT = -1081
```


> Deprecated since 3.52, use ERROR_CODE_OVER_STREAM_PUBLISH_LIMIT(\-1080) instead


Publishing the screen stream failed, and the total number of publishing streams exceeded the upper limit. The

RTC will limit the total number of streams published in a single room, including video, audio, and screen streams.

Local users will fail to publish streams to the room when the maximum number of published streams in the room has been reached, and will receive this error notification.

<span id="ErrorCode-error_code_over_video_publish_limit"></span>
### ERROR_CODE_OVER_VIDEO_PUBLISH_LIMIT

```java
public static final int com.ss.bytertc.engine.type.ErrorCode.ERROR_CODE_OVER_VIDEO_PUBLISH_LIMIT = -1082
```


> Deprecated since 3.52, use ERROR_CODE_OVER_STREAM_PUBLISH_LIMIT(\-1080) instead


The total number of published video streams exceeds the upper limit.

The RTC system limits the number of video streams posted in a single room. If the maximum number of video streams posted in the room has been reached, local users will fail to post video streams to the room again and will receive this error notification.

<span id="ErrorCode-error_code_invalid_audio_sync_userid_repeated"></span>
### ERROR_CODE_INVALID_AUDIO_SYNC_USERID_REPEATED

```java
public static final int com.ss.bytertc.engine.type.ErrorCode.ERROR_CODE_INVALID_AUDIO_SYNC_USERID_REPEATED = -1083
```


> Deprecated since 3.60, use INVALID_UID_REPEATED(0) carried by [onAVSyncEvent](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onavsyncevent) instead.


A/V synchronization failed.

Current source audio ID has been set by other video publishers in the same room.

One single audio source cannot be synchronized with multiple video sources at the same time.

Returned by onStreamStateChanged.

<span id="WarningCode"></span>
# WarningCode

```java
public class com.ss.bytertc.engine.type.WarningCode
```


Callback warning code. The warning code indicates that there is a problem within the SDK and is trying to recover. Warning codes are for notification only.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |\-2002 |[WARNING_CODE_PUBLISH_STREAM_FAILED](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_publish_stream_failed) |
|int |\-2003 |[WARNING_CODE_SUBSCRIBE_STREAM_FAILED404](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_subscribe_stream_failed404) |
|int |\-2004 |[WARNING_CODE_SUBSCRIBE_STREAM_FAILED5XX](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_subscribe_stream_failed5xx) |
|int |\-2009 |[WARNING_CODE_PUBLISH_STREAM_FORBIDEN](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_publish_stream_forbiden) |
|int |\-2011 |[WARNING_CODE_SEND_CUSTOM_MESSAGE](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_send_custom_message) |
|int |\-2013 |[WARNING_CODE_RECEIVE_USER_NOTIFY_STOP](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_receive_user_notify_stop) |
|int |\-2014 |[WARNING_CODE_USER_IN_PUBLISH](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_user_in_publish) |
|int |\-2017 |[WARNING_CODE_IN_ECHO_TEST_MODE](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_in_echo_test_mode) |
|int |\-5001 |[WARNING_CODE_NO_CAMERA_PERMISSION](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_no_camera_permission) |
|int |\-5009 |[WARNING_CODE_SET_SCREEN_AUDIO_SOURCE_TYPE_FAILED](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_set_screen_audio_source_type_failed) |
|int |\-5010 |[WARNING_CODE_SET_SCREEN_STREAM_INDEX_FAILED](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_set_screen_stream_index_failed) |
|int |\-5011 |[WARNING_CODE_SET_SCREEN_STREAM_INVALID_VOICE_PITCH](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_set_screen_stream_invalid_voice_pitch) |
|int |\-5013 |[WARNING_CODE_INVALID_CALL_FOR_EXT_AUDIO](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_invalid_call_for_ext_audio) |
|int |\-7002 |[WARNING_CODE_INVALID_SAMI_APPKEY_OR_TOKEN](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_invalid_sami_appkey_or_token) |
|int |\-7003 |[WARNING_CODE_INVALID_RESOURCE_PATH](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_invalid_resource_path) |
|int |\-7004 |[WARNING_CODE_LOAD_SAMI_LIBRARY_FAILED](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_load_sami_library_failed) |
|int |\-7005 |[WARNING_CODE_INVALID_SAMI_EFFECT_TYPE](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_invalid_sami_effect_type) |
|int |\-2000 |[deprecated] [WARNING_CODE_GET_ROOM_FAILED](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_get_room_failed) |
|int |\-2010 |[deprecated] [WARNING_CODE_SUBSCRIBE_STREAM_FORBIDEN](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_subscribe_stream_forbiden) |
|int |\-2015 |[deprecated] [WARNING_CODE_ROOM_ID_ALREADY_EXIST](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_room_id_already_exist) |
|int |\-5002 |[deprecated] [WARNING_CODE_NO_MICROPHONE_PERMISSION](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_no_microphone_permission) |
|int |\-5003 |[deprecated] [WARNING_CODE_RECODING_DEVICE_START_FAILED](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_recoding_device_start_failed) |
|int |\-5004 |[deprecated] [WARNING_CODE_PLAYOUT_DEVICE_START_FAILED](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_playout_device_start_failed) |
|int |\-5005 |[deprecated] [WARNING_CODE_NO_RECORDING_DEVICE](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_no_recording_device) |
|int |\-5006 |[deprecated] [WARNING_CODE_NO_PLAYOUT_DEVICE](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_no_playout_device) |
|int |\-5007 |[deprecated] [WARNING_CODE_RECORDING_SILENCE](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_recording_silence) |
|int |\-5008 |[deprecated] [WARNING_CODE_MEDIA_DEVICE_OPERATION_DENIED](https://docs.byteplus.com/en/docs/12/14168#WarningCode-warning_code_media_device_operation_denied) |


<span id="instructions"></span>
## Instructions

<span id="WarningCode-warning_code_publish_stream_failed"></span>
### WARNING_CODE_PUBLISH_STREAM_FAILED

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_PUBLISH_STREAM_FAILED = -2002
```


Failed to publish audio & video streams. Returned by [onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onvideopublishstatechanged), [onAudioPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onaudiopublishstatechanged).

When you publish audio & video streams in your room, the publication fails due to a server error. The SDK automatically retries publishing.

<span id="WarningCode-warning_code_subscribe_stream_failed404"></span>
### WARNING_CODE_SUBSCRIBE_STREAM_FAILED404

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_SUBSCRIBE_STREAM_FAILED404 = -2003
```


Subscription to audio & video stream failed. Returned by [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onvideosubscribestatechanged), [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onaudiosubscribestatechanged).

The subscription failed because the audio & video stream for the subscription could not be found in the current room. The SDK will automatically retry the subscription. If the subscription fails, it is recommended that you stop retrying.

<span id="WarningCode-warning_code_subscribe_stream_failed5xx"></span>
### WARNING_CODE_SUBSCRIBE_STREAM_FAILED5XX

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_SUBSCRIBE_STREAM_FAILED5XX = -2004
```


Subscription to audio & video stream failed. Returned by [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onvideosubscribestatechanged), [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onaudiosubscribestatechanged).

When you subscribe to audio & video streams in your room, the subscription fails due to a server error. The SDK automatically retries the subscription.

<span id="WarningCode-warning_code_publish_stream_forbiden"></span>
### WARNING_CODE_PUBLISH_STREAM_FORBIDEN

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_PUBLISH_STREAM_FORBIDEN = -2009
```


This warning is triggered when a call to `setUserVisibility` sets its own visibility to false and then attempts to publish the stream. Returned by [onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onvideopublishstatechanged), [onAudioPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onaudiopublishstatechanged).

<span id="WarningCode-warning_code_send_custom_message"></span>
### WARNING_CODE_SEND_CUSTOM_MESSAGE

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_SEND_CUSTOM_MESSAGE = -2011
```


Sending a custom broadcast message failed because you are not currently in the room.

<span id="WarningCode-warning_code_receive_user_notify_stop"></span>
### WARNING_CODE_RECEIVE_USER_NOTIFY_STOP

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_RECEIVE_USER_NOTIFY_STOP = -2013
```


When the number of people in the room exceeds 500, stop sending `onUserJoined` and `onUserLeave` callbacks to existing users in the room, and prompt all users in the room via broadcast. Returned by [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged).

<span id="WarningCode-warning_code_user_in_publish"></span>
### WARNING_CODE_USER_IN_PUBLISH

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_USER_IN_PUBLISH = -2014
```


The user has published in another room. Returned by [onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onvideopublishstatechanged), [onAudioPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onaudiopublishstatechanged).

<span id="WarningCode-warning_code_in_echo_test_mode"></span>
### WARNING_CODE_IN_ECHO_TEST_MODE

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_IN_ECHO_TEST_MODE = -2017
```


This API has been disabled because the engine is in echo testing mode.

<span id="WarningCode-warning_code_no_camera_permission"></span>
### WARNING_CODE_NO_CAMERA_PERMISSION

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_NO_CAMERA_PERMISSION = -5001
```


The camera permission is abnormal, and the current application has not obtained the camera permission.

<span id="WarningCode-warning_code_set_screen_audio_source_type_failed"></span>
### WARNING_CODE_SET_SCREEN_AUDIO_SOURCE_TYPE_FAILED

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_SET_SCREEN_AUDIO_SOURCE_TYPE_FAILED = -5009
```


Setting the screen audio capture type by calling [setScreenAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setscreenaudiosourcetype) after publishScreenAudio is not supported

<span id="WarningCode-warning_code_set_screen_stream_index_failed"></span>
### WARNING_CODE_SET_SCREEN_STREAM_INDEX_FAILED

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_SET_SCREEN_STREAM_INDEX_FAILED = -5010
```


After publishScreenAudio, calling setScreenAudioStreamIndex to set the screen audio share publication type is not supported

<span id="WarningCode-warning_code_set_screen_stream_invalid_voice_pitch"></span>
### WARNING_CODE_SET_SCREEN_STREAM_INVALID_VOICE_PITCH

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_SET_SCREEN_STREAM_INVALID_VOICE_PITCH = -5011
```


Invalid pitch value setting

<span id="WarningCode-warning_code_invalid_call_for_ext_audio"></span>
### WARNING_CODE_INVALID_CALL_FOR_EXT_AUDIO

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_INVALID_CALL_FOR_EXT_AUDIO = -5013
```


Mixed use of old and new APIs for external audio sources

<span id="WarningCode-warning_code_invalid_sami_appkey_or_token"></span>
### WARNING_CODE_INVALID_SAMI_APPKEY_OR_TOKEN

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_INVALID_SAMI_APPKEY_OR_TOKEN = -7002
```


Authorization failure for [BytePlus Audio SDK](https://go.byteplus.com/audio-sdk). Contact technical support.

<span id="WarningCode-warning_code_invalid_resource_path"></span>
### WARNING_CODE_INVALID_RESOURCE_PATH

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_INVALID_RESOURCE_PATH = -7003
```


Failure to get the resource for [BytePlus Audio SDK](https://go.byteplus.com/audio-sdk). Input the right DAT path or contact the technical support.

<span id="WarningCode-warning_code_load_sami_library_failed"></span>
### WARNING_CODE_LOAD_SAMI_LIBRARY_FAILED

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_LOAD_SAMI_LIBRARY_FAILED = -7004
```


Failure to load the library for [BytePlus Audio SDK](https://go.byteplus.com/audio-sdk). Use the right library or contact the technical support.

<span id="WarningCode-warning_code_invalid_sami_effect_type"></span>
### WARNING_CODE_INVALID_SAMI_EFFECT_TYPE

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_INVALID_SAMI_EFFECT_TYPE = -7005
```


The audio effect is not supported by [BytePlus Audio SDK](https://go.byteplus.com/audio-sdk). Contact the technical support.

<span id="WarningCode-warning_code_get_room_failed"></span>
### WARNING_CODE_GET_ROOM_FAILED

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_GET_ROOM_FAILED = -2000
```


> Deprecated since 3.45 and will be deleted in 3.51.


Failed to get room information Warning

**Notes**

SDK Failed to get room information (including timeout, returning an error code other than 200), try again every two seconds.

After 5 consecutive failures, report the warning and continue to try again.

We suggest prompting the user: Failed to enter the room, please try again later.

<span id="WarningCode-warning_code_subscribe_stream_forbiden"></span>
### WARNING_CODE_SUBSCRIBE_STREAM_FORBIDEN

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_SUBSCRIBE_STREAM_FORBIDEN = -2010
```


> Deprecated since 3.45 and will be deleted in 3.51.


When automatic subscription mode is not turned off, trying to turn on manual subscription mode will trigger this warning.

You need to turn off the automatic subscription mode before entering the room, and then manually subscribe to the audio & video stream.

<span id="WarningCode-warning_code_room_id_already_exist"></span>
### WARNING_CODE_ROOM_ID_ALREADY_EXIST

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_ROOM_ID_ALREADY_EXIST = -2015
```


> Deprecated since 3.45 and will be deleted in 3.51.


There is a room with the same roomId

<span id="WarningCode-warning_code_no_microphone_permission"></span>
### WARNING_CODE_NO_MICROPHONE_PERMISSION

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_NO_MICROPHONE_PERMISSION = -5002
```


> Deprecated since 3.45 and will be deleted in 3.51, use [MediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70083#MediaDeviceError).MEDIA_DEVICE_ERROR_NOPERMISSION instead.


The microphone permission is abnormal, and the current application does not obtain microphone permission.

<span id="WarningCode-warning_code_recoding_device_start_failed"></span>
### WARNING_CODE_RECODING_DEVICE_START_FAILED

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_RECODING_DEVICE_START_FAILED = -5003
```


> Deprecated since 3.45 and will be deleted in 3.51, use [MediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70083#MediaDeviceError).MEDIA_DEVICE_ERROR_DEVICEFAILURE instead.


The audio capture device failed to start.

Failed to start the audio capture device; the current device may be occupied by other applications.

<span id="WarningCode-warning_code_playout_device_start_failed"></span>
### WARNING_CODE_PLAYOUT_DEVICE_START_FAILED

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_PLAYOUT_DEVICE_START_FAILED = -5004
```


> Deprecated since 3.45 and will be deleted in 3.51, use [MediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70083#MediaDeviceError).MEDIA_DEVICE_ERROR_DEVICEFAILURE instead.


Audio playback device startup failure warning.

It may be due to insufficient system resources or wrong parameters.

<span id="WarningCode-warning_code_no_recording_device"></span>
### WARNING_CODE_NO_RECORDING_DEVICE

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_NO_RECORDING_DEVICE = -5005
```


> Deprecated since 3.45 and will be deleted in 3.51, use [MediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70083#MediaDeviceError).MEDIA_DEVICE_ERROR_DEVICENOTFOUND instead.


No audio capture device available.

Failed to start the audio capture device, please insert the available audio capture device.

<span id="WarningCode-warning_code_no_playout_device"></span>
### WARNING_CODE_NO_PLAYOUT_DEVICE

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_NO_PLAYOUT_DEVICE = -5006
```


> Deprecated since 3.45 and will be deleted in 3.51, use [MediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70083#MediaDeviceError).MEDIA_DEVICE_ERROR_DEVICENOTFOUND instead.


No audio playback device available.

Failed to start the audio playback device, please insert the available audio playback device.

<span id="WarningCode-warning_code_recording_silence"></span>
### WARNING_CODE_RECORDING_SILENCE

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_RECORDING_SILENCE = -5007
```


> Deprecated since 3.45 and will be deleted in 3.51, use [MediaDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70083#MediaDeviceWarning).MEDIA_DEVICE_WARNING_CAPTURE_SILENCE instead.


The current audio equipment has not collected valid sound data, please check and replace the audio capture device.

<span id="WarningCode-warning_code_media_device_operation_denied"></span>
### WARNING_CODE_MEDIA_DEVICE_OPERATION_DENIED

```java
public static final int com.ss.bytertc.engine.type.WarningCode.WARNING_CODE_MEDIA_DEVICE_OPERATION_DENIED = -5008
```


> Deprecated since 3.45 and will be deleted in 3.51, use [MediaDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70083#MediaDeviceWarning).MEDIA_DEVICE_WARNING_OPERATION_DENIED instead.


Warning on mishandling media devices.

When using custom acquisition, the internal acquisition switch cannot be called, and this warning will be triggered when called.

<span id="RoomMessageSendResult"></span>
# RoomMessageSendResult

```java
public class com.ss.bytertc.engine.type.RoomMessageSendResult
```


The result of sending room broadcast message

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |200 |[ROOM_MESSAGE_SEND_RESULT_SUCCESS](https://docs.byteplus.com/en/docs/12/14168#RoomMessageSendResult-room_message_send_result_success) |
|int |5 |[ROOM_MESSAGE_SEND_RESULT_EXCEED_QPS](https://docs.byteplus.com/en/docs/12/14168#RoomMessageSendResult-room_message_send_result_exceed_qps) |
|int |100 |[ROOM_MESSAGE_SEND_RESULT_NOT_JOIN](https://docs.byteplus.com/en/docs/12/14168#RoomMessageSendResult-room_message_send_result_not_join) |
|int |101 |[ROOM_MESSAGE_SEND_RESULT_INIT](https://docs.byteplus.com/en/docs/12/14168#RoomMessageSendResult-room_message_send_result_init) |
|int |102 |[ROOM_MESSAGE_SEND_RESULT_NO_CONNECTION](https://docs.byteplus.com/en/docs/12/14168#RoomMessageSendResult-room_message_send_result_no_connection) |
|int |103 |[ROOM_MESSAGE_SEND_RESULT_EXCEED_MAX_LENGTH](https://docs.byteplus.com/en/docs/12/14168#RoomMessageSendResult-room_message_send_result_exceed_max_length) |
|int |1000 |[ROOM_MESSAGE_SEND_RESULT_UNKNOWN](https://docs.byteplus.com/en/docs/12/14168#RoomMessageSendResult-room_message_send_result_unknown) |


<span id="instructions"></span>
## Instructions

<span id="RoomMessageSendResult-room_message_send_result_success"></span>
### ROOM_MESSAGE_SEND_RESULT_SUCCESS

```java
public static final int com.ss.bytertc.engine.type.RoomMessageSendResult.ROOM_MESSAGE_SEND_RESULT_SUCCESS = 200
```


Success

<span id="RoomMessageSendResult-room_message_send_result_exceed_qps"></span>
### ROOM_MESSAGE_SEND_RESULT_EXCEED_QPS

```java
public static final int com.ss.bytertc.engine.type.RoomMessageSendResult.ROOM_MESSAGE_SEND_RESULT_EXCEED_QPS = 5
```


Failure. Exceeds QPS limit.

<span id="RoomMessageSendResult-room_message_send_result_not_join"></span>
### ROOM_MESSAGE_SEND_RESULT_NOT_JOIN

```java
public static final int com.ss.bytertc.engine.type.RoomMessageSendResult.ROOM_MESSAGE_SEND_RESULT_NOT_JOIN = 100
```


Failure. The sender of the message is not in the room.

<span id="RoomMessageSendResult-room_message_send_result_init"></span>
### ROOM_MESSAGE_SEND_RESULT_INIT

```java
public static final int com.ss.bytertc.engine.type.RoomMessageSendResult.ROOM_MESSAGE_SEND_RESULT_INIT = 101
```


Failure. The connection is not initialized.

<span id="RoomMessageSendResult-room_message_send_result_no_connection"></span>
### ROOM_MESSAGE_SEND_RESULT_NO_CONNECTION

```java
public static final int com.ss.bytertc.engine.type.RoomMessageSendResult.ROOM_MESSAGE_SEND_RESULT_NO_CONNECTION = 102
```


Failure. No data transmission channel connection available.

<span id="RoomMessageSendResult-room_message_send_result_exceed_max_length"></span>
### ROOM_MESSAGE_SEND_RESULT_EXCEED_MAX_LENGTH

```java
public static final int com.ss.bytertc.engine.type.RoomMessageSendResult.ROOM_MESSAGE_SEND_RESULT_EXCEED_MAX_LENGTH = 103
```


Failure. The default maximum length of a message is 1 KB. If you [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode), the maximum length is 64 KB.

<span id="RoomMessageSendResult-room_message_send_result_unknown"></span>
### ROOM_MESSAGE_SEND_RESULT_UNKNOWN

```java
public static final int com.ss.bytertc.engine.type.RoomMessageSendResult.ROOM_MESSAGE_SEND_RESULT_UNKNOWN = 1000
```


Failure. Unknown error.

<span id="LoginErrorCode"></span>
# LoginErrorCode

```java
public class com.ss.bytertc.engine.type.LoginErrorCode
```


Login result

The user is notified of the result of calling `login` via an `onLoginResult` callback.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |0 |[LOGIN_ERROR_CODE_SUCCESS](https://docs.byteplus.com/en/docs/12/14168#LoginErrorCode-login_error_code_success) |
|int |\-1000 |[LOGIN_ERROR_CODE_INVALID_TOKEN](https://docs.byteplus.com/en/docs/12/14168#LoginErrorCode-login_error_code_invalid_token) |
|int |\-1001 |[LOGIN_ERROR_CODE_LOGIN_FAILED](https://docs.byteplus.com/en/docs/12/14168#LoginErrorCode-login_error_code_login_failed) |
|int |\-1002 |[LOGIN_ERROR_CODE_INVALID_USER_ID](https://docs.byteplus.com/en/docs/12/14168#LoginErrorCode-login_error_code_invalid_user_id) |
|int |\-1003 |[LOGIN_ERROR_CODE_SERVER_ERROR](https://docs.byteplus.com/en/docs/12/14168#LoginErrorCode-login_error_code_server_error) |


<span id="instructions"></span>
## Instructions

<span id="LoginErrorCode-login_error_code_success"></span>
### LOGIN_ERROR_CODE_SUCCESS

```java
public static final int com.ss.bytertc.engine.type.LoginErrorCode.LOGIN_ERROR_CODE_SUCCESS = 0
```


Call the `login` method to sign in successfully.

<span id="LoginErrorCode-login_error_code_invalid_token"></span>
### LOGIN_ERROR_CODE_INVALID_TOKEN

```java
public static final int com.ss.bytertc.engine.type.LoginErrorCode.LOGIN_ERROR_CODE_INVALID_TOKEN = -1000
```


The Token used when calling the `login` method is invalid or expired. The user is required to re\-acquire the token.

<span id="LoginErrorCode-login_error_code_login_failed"></span>
### LOGIN_ERROR_CODE_LOGIN_FAILED

```java
public static final int com.ss.bytertc.engine.type.LoginErrorCode.LOGIN_ERROR_CODE_LOGIN_FAILED = -1001
```


Login error.

An unknown error occurred when calling the `login` method, which caused the login to fail and requires re\-login.

<span id="LoginErrorCode-login_error_code_invalid_user_id"></span>
### LOGIN_ERROR_CODE_INVALID_USER_ID

```java
public static final int com.ss.bytertc.engine.type.LoginErrorCode.LOGIN_ERROR_CODE_INVALID_USER_ID = -1002
```


There was a problem with the user ID passed in when the `login` method was called.

<span id="LoginErrorCode-login_error_code_server_error"></span>
### LOGIN_ERROR_CODE_SERVER_ERROR

```java
public static final int com.ss.bytertc.engine.type.LoginErrorCode.LOGIN_ERROR_CODE_SERVER_ERROR = -1003
```


Server error when calling `login` to sign in.

<span id="TranscodingError"></span>
# TranscodingError

```java
public class com.ss.bytertc.engine.type.TranscodingError
```


Errors that may occur during pushing streams to CDN.

<span id="member-property"></span>
## Member Property


|Type |Default Value |Name |
|---|---|---|
|int |0 |[TRANSCODING_ERROR_OK](https://docs.byteplus.com/en/docs/12/14168#TranscodingError-transcoding_error_ok) |
|int |1 |[TRANSCODING_ERROR_INVALID_ARGUMENT](https://docs.byteplus.com/en/docs/12/14168#TranscodingError-transcoding_error_invalid_argument) |
|int |2 |[TRANSCODING_ERROR_SUBSCRIBE](https://docs.byteplus.com/en/docs/12/14168#TranscodingError-transcoding_error_subscribe) |
|int |3 |[TRANSCODING_ERROR_PROCESSING](https://docs.byteplus.com/en/docs/12/14168#TranscodingError-transcoding_error_processing) |
|int |4 |[TRANSCODING_ERROR_PUBLISH](https://docs.byteplus.com/en/docs/12/14168#TranscodingError-transcoding_error_publish) |


<span id="instructions"></span>
## Instructions

<span id="TranscodingError-transcoding_error_ok"></span>
### TRANSCODING_ERROR_OK

```java
public static final int com.ss.bytertc.engine.type.TranscodingError.TRANSCODING_ERROR_OK = 0
```


Successfully pushed streams to target CDN.

<span id="TranscodingError-transcoding_error_invalid_argument"></span>
### TRANSCODING_ERROR_INVALID_ARGUMENT

```java
public static final int com.ss.bytertc.engine.type.TranscodingError.TRANSCODING_ERROR_INVALID_ARGUMENT = 1
```


Parameter error. You should reset stream pushing parameters and try again.

<span id="TranscodingError-transcoding_error_subscribe"></span>
### TRANSCODING_ERROR_SUBSCRIBE

```java
public static final int com.ss.bytertc.engine.type.TranscodingError.TRANSCODING_ERROR_SUBSCRIBE = 2
```


Failed to establish a connection with the RTC server. SDK will automatically retry.

<span id="TranscodingError-transcoding_error_processing"></span>
### TRANSCODING_ERROR_PROCESSING

```java
public static final int com.ss.bytertc.engine.type.TranscodingError.TRANSCODING_ERROR_PROCESSING = 3
```


There is an error in the process of stream mixing. We suggest that you try again.

<span id="TranscodingError-transcoding_error_publish"></span>
### TRANSCODING_ERROR_PUBLISH

```java
public static final int com.ss.bytertc.engine.type.TranscodingError.TRANSCODING_ERROR_PUBLISH = 4
```


Pushing the stream failed. You can wait for the server to push again.
