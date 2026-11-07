---
title: "Error Code"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-191861"
---

<span id="LocalAudioStreamError"></span>
# LocalAudioStreamError

```c#
enum class bytertc.LocalAudioStreamError
```


Error code when the state of the local audio stream changes. The SDK calls back the error code via `OnLocalAudioStateChangedEventHandler`.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kLocalAudioStreamErrorOk |0 |Local audio status is normal |
|kLocalAudioStreamErrorFailure |1 |Local audio error cause unknown |
|kLocalAudioStreamErrorDeviceNoPermission |2 |No permission to start local audio recording device |
|kLocalAudioStreamErrorDeviceBusy |3 |The local audio recording device is already in use |
|kLocalAudioStreamErrorRecordFailure |4 |Local audio recording failed, it is recommended that you check whether the recording device is working properly |
|kLocalAudioStreamErrorEncodeFailure |5 |Local audio encoding failed |
|kLocalAudioStreamErrorNoRecordingDevice |6 |No audio recording equipment available |


<span id="ErrorCode"></span>
# ErrorCode

```c#
class bytertc::ErrorCode
```


Callback error code. When an unrecoverable error is encountered inside the SDK, the user is notified via the `onError` callback.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[ERROR_CODE_INVALID_TOKEN](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_invalid_token) |
|int |[ERROR_CODE_JOIN_ROOM](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_join_room) |
|int |[ERROR_CODE_NO_PUBLISH_PERMISSION](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_no_publish_permission) |
|int |[ERROR_CODE_NO_SUBSCRIBE_PERMISSION](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_no_subscribe_permission) |
|int |[ERROR_CODE_DUPLICATE_LOGIN](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_duplicate_login) |
|int |[ERROR_CODE_APP_ID_NULL](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_app_id_null) |
|int |[ERROR_CODE_KICKED_OUT](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_kicked_out) |
|int |[ERROR_CODE_ROOM_ID_ILLEGAL](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_room_id_illegal) |
|int |[ERROR_CODE_TOKEN_EXPIRED](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_token_expired) |
|int |[ERROR_CODE_UPDATE_TOKEN_WITH_INVALID_TOKEN](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_update_token_with_invalid_token) |
|int |[ERROR_CODE_ROOM_DISMISS](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_room_dismiss) |
|int |[ERROR_CODE_JOIN_ROOM_WITHOUT_LICENSE_AUTHENTICATE_SDK](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_join_room_without_license_authenticate_sdk) |
|int |[ERROR_CODE_ROOM_ALREADY_EXIST](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_room_already_exist) |
|int |[ERROR_CODE_USER_ID_DIFFERENT](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_user_id_different) |
|int |[ERROR_CODE_SERVER_LICENSE_EXPIRE](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_server_license_expire) |
|int |[ERROR_CODE_EXCEEDS_THE_UPPER_LIMIT](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_exceeds_the_upper_limit) |
|int |[ERROR_CODE_LICENSE_PARAMETER_ERROR](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_license_parameter_error) |
|int |[ERROR_CODE_LICENSE_FILE_PATH_ERROR](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_license_file_path_error) |
|int |[ERROR_CODE_LICENSE_ILLEGAL](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_license_illegal) |
|int |[ERROR_CODE_LICENSE_EXPIRED](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_license_expired) |
|int |[ERROR_CODE_LICENSE_INFORMATION_NOT_MATCH](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_license_information_not_match) |
|int |[ERROR_CODE_LICENSE_NOT_MATCH_WITH_CACHE](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_license_not_match_with_cache) |
|int |[ERROR_CODE_OVER_SUBSCRIBE_LIMIT](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_over_subscribe_limit) |
|int |[ERROR_CODE_LOAD_SO_LIB](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_load_so_lib) |
|int |[ERROR_CODE_OVER_STREAM_PUBLISH_LIMIT](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_over_stream_publish_limit) |
|int |[ERROR_CODE_OVER_SCREEN_PUBLISH_LIMIT](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_over_screen_publish_limit) |
|int |[ERROR_CODE_OVER_VIDEO_PUBLISH_LIMIT](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_over_video_publish_limit) |
|int |[ERROR_CODE_INVALID_AUDIO_SYNC_USERID_REPEATED](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_invalid_audio_sync_userid_repeated) |
|int |[ERROR_CODE_ABNORMAL_SERVER_STATUS](https://docs.byteplus.com/en/docs/12/35816#ErrorCode-error_code_abnormal_server_status) |


<span id="instructions"></span>
## Instructions

<span id="ErrorCode-error_code_invalid_token"></span>
### ERROR_CODE_INVALID_TOKEN

```c#
int bytertc.ErrorCode.ERROR_CODE_INVALID_TOKEN = -1000
```


Token is invalid. The token used when entering the room is invalid or expired. The user is required to retrieve the token and call the `updateToken` method to update the token.

<span id="ErrorCode-error_code_join_room"></span>
### ERROR_CODE_JOIN_ROOM

```c#
int bytertc.ErrorCode.ERROR_CODE_JOIN_ROOM = -1001
```


Join room error. An unknown error occurred while entering the room, which caused the joining room to fail. Users are required to rejoin the room.

<span id="ErrorCode-error_code_no_publish_permission"></span>
### ERROR_CODE_NO_PUBLISH_PERMISSION

```c#
int bytertc.ErrorCode.ERROR_CODE_NO_PUBLISH_PERMISSION = -1002
```


No permission to publish audio & video streams. The user failed to publish the audio & video stream in the room. The reason for the failure is that the user does not have permission to publish the stream.

<span id="ErrorCode-error_code_no_subscribe_permission"></span>
### ERROR_CODE_NO_SUBSCRIBE_PERMISSION

```c#
int bytertc.ErrorCode.ERROR_CODE_NO_SUBSCRIBE_PERMISSION = -1003
```


No subscription permissions for audio & video streams. The user failed to subscribe to the audio & video stream in the room where the user is located. The reason for the failure is that the user does not have permission to subscribe to the stream.

<span id="ErrorCode-error_code_duplicate_login"></span>
### ERROR_CODE_DUPLICATE_LOGIN

```c#
int bytertc.ErrorCode.ERROR_CODE_DUPLICATE_LOGIN = -1004
```


The user has been removed from the room because the same user joined the room on the other client.

<span id="ErrorCode-error_code_app_id_null"></span>
### ERROR_CODE_APP_ID_NULL

```c#
int bytertc.ErrorCode.ERROR_CODE_APP_ID_NULL = -1005
```


The App ID parameter is abnormal. The App ID parameter passed in when the engine was created is empty.

<span id="ErrorCode-error_code_kicked_out"></span>
### ERROR_CODE_KICKED_OUT

```c#
int bytertc.ErrorCode.ERROR_CODE_KICKED_OUT = -1006
```


The user has been remove from the room by the administrator via a OpenAPI call.

<span id="ErrorCode-error_code_room_id_illegal"></span>
### ERROR_CODE_ROOM_ID_ILLEGAL

```c#
int bytertc.ErrorCode.ERROR_CODE_ROOM_ID_ILLEGAL = -1007
```


When calling `createRoom`, if the roomId is illegal, it will return null and throw the error

<span id="ErrorCode-error_code_token_expired"></span>
### ERROR_CODE_TOKEN_EXPIRED

```c#
int bytertc.ErrorCode.ERROR_CODE_TOKEN_EXPIRED = -1009
```


Token expired. Call `joinRoom` to rejoin with a valid Token.

<span id="ErrorCode-error_code_update_token_with_invalid_token"></span>
### ERROR_CODE_UPDATE_TOKEN_WITH_INVALID_TOKEN

```c#
int bytertc.ErrorCode.ERROR_CODE_UPDATE_TOKEN_WITH_INVALID_TOKEN = -1010
```


The Token you provided when calling `updateToken` is invalid.

<span id="ErrorCode-error_code_room_dismiss"></span>
### ERROR_CODE_ROOM_DISMISS

```c#
int bytertc.ErrorCode.ERROR_CODE_ROOM_DISMISS = -1011
```


Users have been removed from the room because the administrator dismissed the room by calling OpenAPI.

<span id="ErrorCode-error_code_join_room_without_license_authenticate_sdk"></span>
### ERROR_CODE_JOIN_ROOM_WITHOUT_LICENSE_AUTHENTICATE_SDK

```c#
int bytertc.ErrorCode.ERROR_CODE_JOIN_ROOM_WITHOUT_LICENSE_AUTHENTICATE_SDK = -1012
```


Join room error.

The LICENSE billing account does not use the LICENSE_AUTHENTICATE SDK while calling `joinRoom`, which caused the joining room to fail.

<span id="ErrorCode-error_code_room_already_exist"></span>
### ERROR_CODE_ROOM_ALREADY_EXIST

```c#
int bytertc.ErrorCode.ERROR_CODE_ROOM_ALREADY_EXIST = -1013
```


A room with the same roomId already exists during the call echo test.

<span id="ErrorCode-error_code_user_id_different"></span>
### ERROR_CODE_USER_ID_DIFFERENT

```c#
int bytertc.ErrorCode.ERROR_CODE_USER_ID_DIFFERENT = -1014
```


The local user joins multiple rooms with different uid.

In the same engine instance, users need to use the same uid to join different rooms.

<span id="ErrorCode-error_code_server_license_expire"></span>
### ERROR_CODE_SERVER_LICENSE_EXPIRE

```c#
int bytertc.ErrorCode.ERROR_CODE_SERVER_LICENSE_EXPIRE = -1017
```


Server license expired, refused to enter the room.

<span id="ErrorCode-error_code_exceeds_the_upper_limit"></span>
### ERROR_CODE_EXCEEDS_THE_UPPER_LIMIT

```c#
int bytertc.ErrorCode.ERROR_CODE_EXCEEDS_THE_UPPER_LIMIT = -1018
```


Exceeds the upper limit of the concurrency allowed by the server license, and refuses to enter the room.

<span id="ErrorCode-error_code_license_parameter_error"></span>
### ERROR_CODE_LICENSE_PARAMETER_ERROR

```c#
int bytertc.ErrorCode.ERROR_CODE_LICENSE_PARAMETER_ERROR = -1019
```


The license parameter is wrong and refuses to enter the room.

<span id="ErrorCode-error_code_license_file_path_error"></span>
### ERROR_CODE_LICENSE_FILE_PATH_ERROR

```c#
int bytertc.ErrorCode.ERROR_CODE_LICENSE_FILE_PATH_ERROR = -1020
```


wrong license certificate path.

<span id="ErrorCode-error_code_license_illegal"></span>
### ERROR_CODE_LICENSE_ILLEGAL

```c#
int bytertc.ErrorCode.ERROR_CODE_LICENSE_ILLEGAL = -1021
```


The license certificate is illegal, refuse to enter the room.

<span id="ErrorCode-error_code_license_expired"></span>
### ERROR_CODE_LICENSE_EXPIRED

```c#
int bytertc.ErrorCode.ERROR_CODE_LICENSE_EXPIRED = -1022
```


License certificate has expired, refused to enter the room.

<span id="ErrorCode-error_code_license_information_not_match"></span>
### ERROR_CODE_LICENSE_INFORMATION_NOT_MATCH

```c#
int bytertc.ErrorCode.ERROR_CODE_LICENSE_INFORMATION_NOT_MATCH = -1023
```


The content of the license certificate does not match.

<span id="ErrorCode-error_code_license_not_match_with_cache"></span>
### ERROR_CODE_LICENSE_NOT_MATCH_WITH_CACHE

```c#
int bytertc.ErrorCode.ERROR_CODE_LICENSE_NOT_MATCH_WITH_CACHE = -1024
```


licenseThe current certificate does not match the cached certificate.

<span id="ErrorCode-error_code_over_subscribe_limit"></span>
### ERROR_CODE_OVER_SUBSCRIBE_LIMIT

```c#
int bytertc.ErrorCode.ERROR_CODE_OVER_SUBSCRIBE_LIMIT = -1070
```


Failed to subscribe to streams because the total number of subscribed streams has exceeded the upper limit. In order to ensure the performance and quality of audio & video calls in the game scenario, the server will limit the total number of audio & video streams subscribed by the user. When the total number of audio & video streams subscribed by the user has reached the maximum, continuing to subscribe to more streams will fail, and the user will receive this error notification.

<span id="ErrorCode-error_code_load_so_lib"></span>
### ERROR_CODE_LOAD_SO_LIB

```c#
int bytertc.ErrorCode.ERROR_CODE_LOAD_SO_LIB = -1072
```


<span id="ErrorCode-error_code_over_stream_publish_limit"></span>
### ERROR_CODE_OVER_STREAM_PUBLISH_LIMIT

```c#
int bytertc.ErrorCode.ERROR_CODE_OVER_STREAM_PUBLISH_LIMIT = -1080
```


Failed to publish video stream because the total number of published streams has exceeded the upper limit. RTC will limit the total number of streams published in a single room, including video, audio, and screen streams. Local users will fail to publish streams to the room when the maximum number of published streams in the room has been reached, and will receive this error notification.

<span id="ErrorCode-error_code_over_screen_publish_limit"></span>
### ERROR_CODE_OVER_SCREEN_PUBLISH_LIMIT

```c#
int bytertc.ErrorCode.ERROR_CODE_OVER_SCREEN_PUBLISH_LIMIT = -1081
```


Publishing the screen stream failed, and the total number of publishing streams exceeded the upper limit. The RTC will limit the total number of streams published in a single room, including video, audio, and screen streams.

Local users will fail to publish streams to the room when the maximum number of published streams in the room has been reached, and will receive this error notification.

<span id="ErrorCode-error_code_over_video_publish_limit"></span>
### ERROR_CODE_OVER_VIDEO_PUBLISH_LIMIT

```c#
int bytertc.ErrorCode.ERROR_CODE_OVER_VIDEO_PUBLISH_LIMIT = -1082
```


The total number of published video streams exceeds the upper limit. The RTC system limits the number of video streams posted in a single room. If the maximum number of video streams posted in the room has been reached, local users will fail to post video streams to the room again and will receive this error notification.

<span id="ErrorCode-error_code_invalid_audio_sync_userid_repeated"></span>
### ERROR_CODE_INVALID_AUDIO_SYNC_USERID_REPEATED

```c#
int bytertc.ErrorCode.ERROR_CODE_INVALID_AUDIO_SYNC_USERID_REPEATED = -1083
```


A/V synchronization failed.

Current source audio ID has been set by other video publishers in the same room.

One single audio source cannot be synchronized with multiple video sources at the same time.

<span id="ErrorCode-error_code_abnormal_server_status"></span>
### ERROR_CODE_ABNORMAL_SERVER_STATUS

```c#
int bytertc.ErrorCode.ERROR_CODE_ABNORMAL_SERVER_STATUS = -1084
```


The user has been removed from the room due to the abnormal status of server.

SDK is disconnected with the signaling server. It will not reconnect automatically. Please contact technical support.

<span id="WarningCode"></span>
# WarningCode

```c#
class bytertc::WarningCode
```


Callback warning code. The warning code indicates that there is a problem within the SDK and is trying to recover. Warning codes are for notification only.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|int |[WARNING_CODE_JOIN_ROOM_FAILED](https://docs.byteplus.com/en/docs/12/35816#WarningCode-warning_code_join_room_failed) |
|int |[WARNING_CODE_PUBLISH_STREAM_FAILED](https://docs.byteplus.com/en/docs/12/35816#WarningCode-warning_code_publish_stream_failed) |
|int |[WARNING_CODE_SUBSCRIBE_STREAM_FAILED404](https://docs.byteplus.com/en/docs/12/35816#WarningCode-warning_code_subscribe_stream_failed404) |
|int |[WARNING_CODE_SUBSCRIBE_STREAM_FAILED5XX](https://docs.byteplus.com/en/docs/12/35816#WarningCode-warning_code_subscribe_stream_failed5xx) |
|int |[WARNING_CODE_PUBLISH_STREAM_FORBIDEN](https://docs.byteplus.com/en/docs/12/35816#WarningCode-warning_code_publish_stream_forbiden) |
|int |[WARNING_CODE_SEND_CUSTOM_MESSAGE](https://docs.byteplus.com/en/docs/12/35816#WarningCode-warning_code_send_custom_message) |
|int |[WARNING_CODE_RECEIVE_USER_NOTIFY_STOP](https://docs.byteplus.com/en/docs/12/35816#WarningCode-warning_code_receive_user_notify_stop) |
|int |[WARNING_CODE_USER_IN_PUBLISH](https://docs.byteplus.com/en/docs/12/35816#WarningCode-warning_code_user_in_publish) |
|int |[WARNING_CODE_OLD_ROOM_BEEN_REPLACED](https://docs.byteplus.com/en/docs/12/35816#WarningCode-warning_code_old_room_been_replaced) |
|int |[WARNING_CODE_IN_ECHO_TEST_MODE](https://docs.byteplus.com/en/docs/12/35816#WarningCode-warning_code_in_echo_test_mode) |
|int |[WARNING_CODE_NO_CAMERA_PERMISSION](https://docs.byteplus.com/en/docs/12/35816#WarningCode-warning_code_no_camera_permission) |
|int |[WARNING_CODE_SET_SCREEN_AUDIO_SOURCE_TYPE_FAILED](https://docs.byteplus.com/en/docs/12/35816#WarningCode-warning_code_set_screen_audio_source_type_failed) |
|int |[WARNING_CODE_SET_SCREEN_STREAM_INDEX_FAILED](https://docs.byteplus.com/en/docs/12/35816#WarningCode-warning_code_set_screen_stream_index_failed) |
|int |[WARNING_CODE_SET_SCREEN_STREAM_INVALID_VOICE_PITCH](https://docs.byteplus.com/en/docs/12/35816#WarningCode-warning_code_set_screen_stream_invalid_voice_pitch) |
|int |[WARNING_CODE_INVALID_CALL_FOR_EXT_AUDIO](https://docs.byteplus.com/en/docs/12/35816#WarningCode-warning_code_invalid_call_for_ext_audio) |
|int |[WARNING_CODE_INVALID_REMOTE_STREAM_KEY](https://docs.byteplus.com/en/docs/12/35816#WarningCode-warning_code_invalid_remote_stream_key) |


<span id="instructions"></span>
## Instructions

<span id="WarningCode-warning_code_join_room_failed"></span>
### WARNING_CODE_JOIN_ROOM_FAILED

```c#
int bytertc.WarningCode.WARNING_CODE_JOIN_ROOM_FAILED = -2001
```


Failed to enter the room.

When you enter the room for the first time or disconnect and reconnect due to poor network condition, the room entry failed due to a server error. The SDK automatically retries to join the room.

<span id="WarningCode-warning_code_publish_stream_failed"></span>
### WARNING_CODE_PUBLISH_STREAM_FAILED

```c#
int bytertc.WarningCode.WARNING_CODE_PUBLISH_STREAM_FAILED = -2002
```


Release audio & video stream failed.

When you publish audio & video streams in your room, the publication fails due to a server error. The SDK automatically retries the release.

<span id="WarningCode-warning_code_subscribe_stream_failed404"></span>
### WARNING_CODE_SUBSCRIBE_STREAM_FAILED404

```c#
int bytertc.WarningCode.WARNING_CODE_SUBSCRIBE_STREAM_FAILED404 = -2003
```


Subscription to audio & video stream failed.

The subscription failed because the audio & video stream for the subscription could not be found in the current room. The SDK will automatically retry the subscription. If the subscription fails, it is recommended that you exit the retry.

<span id="WarningCode-warning_code_subscribe_stream_failed5xx"></span>
### WARNING_CODE_SUBSCRIBE_STREAM_FAILED5XX

```c#
int bytertc.WarningCode.WARNING_CODE_SUBSCRIBE_STREAM_FAILED5XX = -2004
```


Subscription to audio & video stream failed.

When you subscribe to audio & video streams in your room, the subscription fails due to a server error. The SDK automatically retries the subscription.

<span id="WarningCode-warning_code_publish_stream_forbiden"></span>
### WARNING_CODE_PUBLISH_STREAM_FORBIDEN

```c#
int bytertc.WarningCode.WARNING_CODE_PUBLISH_STREAM_FORBIDEN = -2009
```


This warning is triggered when a call to `setUserVisibility` sets its own visibility to false and then attempts to publish the flow.

<span id="WarningCode-warning_code_send_custom_message"></span>
### WARNING_CODE_SEND_CUSTOM_MESSAGE

```c#
int bytertc.WarningCode.WARNING_CODE_SEND_CUSTOM_MESSAGE = -2011
```


Sending a custom broadcast message failed, you are not currently in the room.

<span id="WarningCode-warning_code_receive_user_notify_stop"></span>
### WARNING_CODE_RECEIVE_USER_NOTIFY_STOP

```c#
int bytertc.WarningCode.WARNING_CODE_RECEIVE_USER_NOTIFY_STOP = -2013
```


When the number of people in the room exceeds 500, stop sending `onUserJoined` and `onUserLeave` callbacks to existing users in the room, and prompt all users in the room via broadcast.

<span id="WarningCode-warning_code_user_in_publish"></span>
### WARNING_CODE_USER_IN_PUBLISH

```c#
int bytertc.WarningCode.WARNING_CODE_USER_IN_PUBLISH = -2014
```


User had published in other room.

<span id="WarningCode-warning_code_old_room_been_replaced"></span>
### WARNING_CODE_OLD_ROOM_BEEN_REPLACED

```c#
int bytertc.WarningCode.WARNING_CODE_OLD_ROOM_BEEN_REPLACED = -2016
```


A room with the same roomId already exists. The newly created room instance has replaced the old one.

<span id="WarningCode-warning_code_in_echo_test_mode"></span>
### WARNING_CODE_IN_ECHO_TEST_MODE

```c#
int bytertc.WarningCode.WARNING_CODE_IN_ECHO_TEST_MODE = -2017
```


this inteface has been banned for the engine is in echo testing mode

<span id="WarningCode-warning_code_no_camera_permission"></span>
### WARNING_CODE_NO_CAMERA_PERMISSION

```c#
int bytertc.WarningCode.WARNING_CODE_NO_CAMERA_PERMISSION = -5001
```


The camera permission is abnormal, and the current application does not obtain the camera permission.

<span id="WarningCode-warning_code_set_screen_audio_source_type_failed"></span>
### WARNING_CODE_SET_SCREEN_AUDIO_SOURCE_TYPE_FAILED

```c#
int bytertc.WarningCode.WARNING_CODE_SET_SCREEN_AUDIO_SOURCE_TYPE_FAILED = -5009
```


Setting the screen audio capture type by calling [SetScreenAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setscreenaudiosourcetype) after [PublishScreen](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-publishscreen) is not supported

<span id="WarningCode-warning_code_set_screen_stream_index_failed"></span>
### WARNING_CODE_SET_SCREEN_STREAM_INDEX_FAILED

```c#
int bytertc.WarningCode.WARNING_CODE_SET_SCREEN_STREAM_INDEX_FAILED = -5010
```


After [PublishScreen](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-publishscreen), calling [SetScreenAudioStreamIndex](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setscreenaudiostreamindex) to set the screen audio share publication type is not supported

<span id="WarningCode-warning_code_set_screen_stream_invalid_voice_pitch"></span>
### WARNING_CODE_SET_SCREEN_STREAM_INVALID_VOICE_PITCH

```c#
int bytertc.WarningCode.WARNING_CODE_SET_SCREEN_STREAM_INVALID_VOICE_PITCH = -5011
```


Invalid pitch value setting

<span id="WarningCode-warning_code_invalid_call_for_ext_audio"></span>
### WARNING_CODE_INVALID_CALL_FOR_EXT_AUDIO

```c#
int bytertc.WarningCode.WARNING_CODE_INVALID_CALL_FOR_EXT_AUDIO = -5013
```


Mixed use of old and new interfaces for external audio sources

<span id="WarningCode-warning_code_invalid_remote_stream_key"></span>
### WARNING_CODE_INVALID_REMOTE_STREAM_KEY

```c#
int bytertc.WarningCode.WARNING_CODE_INVALID_REMOTE_STREAM_KEY = -5014
```


Invalid remote streamKey

<span id="LocalVideoStreamError"></span>
# LocalVideoStreamError

```c#
enum class bytertc.LocalVideoStreamError
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
|kLocalVideoStreamErrorDeviceDisconnected |7 |Local video capture device removed |


<span id="AudioRecordingErrorCode"></span>
# AudioRecordingErrorCode

```c#
enum class bytertc.AudioRecordingErrorCode
```


Error code for audio recording.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|kAudioRecordingErrorCodeOk |0 |OK |
|kAudioRecordingErrorCodeNoPermission |\-1 |No file write permissions. |
|kAudioRecordingErrorNotInRoom |\-2 |Not in the room. |
|kAudioRecordingAlreadyStarted |\-3 |Started. |
|kAudioRecordingNotStarted |\-4 |Not started. |
|kAudioRecordingErrorCodeNotSupport |\-5 |Failure. Invalid file format. |
|kAudioRecordingErrorCodeOther |\-6 |Other error. |
