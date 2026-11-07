---
title: "Error Code"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-85534"
---

## UserVisibilityChangeError

* **Type**: `enum`

* **Description**: User visibility state change error.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kUserVisibilityChangeErrorOk |`0` |Success. |
   |kUserVisibilityChangeErrorUnknown |`1` |Unknown error. |
   |kUserVisibilityChangeErrorTooManyVisibleUser |`2` |Visible users in the room have reached the upper limit. |

## ForwardStreamError

* **Type**: `enum`

* **Description**: Error codes during the relaying.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kForwardStreamErrorOK |`0` |Normal. |
   |kForwardStreamErrorInvalidArgument |`1201` |Invalid argument. |
   |kForwardStreamErrorInvalidToken |`1202` |Invalid token. |
   |kForwardStreamErrorResponse |`1203` |Error returning from server. |
   |kForwardStreamErrorRemoteKicked |`1204` |Relaying aborts for the reason of that a User with the same user ID as that of the publisher joins. |
   |kForwardStreamErrorNotSupport |`1205` |Server denies. |

## AudioRecordingErrorCode

* **Type**: `enum`

* **Description**: Error code for audio recording.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kAudioRecordingErrorCodeOk |`0` |OK. |
   |kAudioRecordingErrorCodeNoPermission |`-1` |No file write permissions. |
   |kAudioRecordingErrorCodeNotInRoom |`-2` |Not in the room. |
   |kAudioRecordingErrorCodeAlreadyStarted |`-3` |Started. |
   |kAudioRecordingErrorCodeNotStarted |`-4` |Not started. |
   |kAudioRecordingErrorCodeNotSupport |`-5` |Failure. Invalid file format. |
   |kAudioRecordingErrorCodeOther |`-6` |Other error. |

## LocalProxyError

* **Type**: `enum`

* **Description**: The errors of local proxy connection.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kLocalProxyErrorOK |`0` |There are no errors in local proxies. |
   |kLocalProxyErrorSocks5VersionError |`1` |The connection to Socks5 proxy failed because the proxy server replies wrong version numbers which don't accord with the Socks5 document. Please check the proxy server. |
   |kLocalProxyErrorSocks5FormatError |`2` |The connection to Socks5 proxy failed because the format of the proxy's replies doesn't accord with the Socks5 document. Please check the proxy server. |
   |kLocalProxyErrorSocks5InvalidValue |`3` |The connection to Socks5 proxy failed because the proxy replies wrong information which doesn't accord with the Socks5 document. Please check the proxy server. |
   |kLocalProxyErrorSocks5UserPassNotGiven |`4` |The connection to Socks5 proxy failed because the username and password of the local proxy are not provided. Please call [setLocalProxy](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setlocalproxy) and enter your username and password. |
   |kLocalProxyErrorSocks5TcpClosed |`5` |The connection to Socks5 proxy failed because TCP is closed. Please check the proxy server and your network connection status. |
   |kLocalProxyErrorHttpTunnelFailed |`6` |Errors in Http tunnel proxy. Please check Http tunnel proxy and your network connection status. |

## MixedStreamTaskErrorCode

* **Type**: `enum`

* **Description**: Mixed stream task error codes.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kMixedStreamTaskErrorCodeOK |`0` |Success. |
   |kMixedStreamTaskErrorCodeTimeout |`1091` |The task timed out. Check the network status and try again. |
   |kMixedStreamTaskErrorCodeInvalidParamByServer |`1092` |Invalid push parameters detected by the server. |
   |kMixedStreamTaskErrorCodeSubTimeoutByServer |`1093` |Stream subscription timed out. |
   |kMixedStreamTaskErrorCodeInvalidStateByServer |`1094` |Internal mixed\-stream server error. |
   |kMixedStreamTaskErrorCodeAuthenticationByCDN |`1095` |The mixed\-stream server failed to push the stream to CDN. |
   |kMixedStreamTaskErrorCodeUnKnownByServer |`1096` |Unknown server\-side error. |
   |kMixedStreamTaskErrorCodeSignalRequestTimeout |`1097` |The server timed out while receiving signaling. Check the network status and try again. |
   |kMixedStreamTaskErrorCodeMixImageFailed |`1098` |Failed to mix the image. |
   |kMixedStreamTaskErrorCodePushWTNFailed |`1195` |Failed to publish the WTN stream. |

## WarningCode

* **Type**: `enum`

* **Description**: Callback warning code. The warning code indicates that there is a problem within the SDK and is trying to recover. Warning codes only serve as notifications.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kWarningCodeJoinRoomFailed |`-2001` |Failed to enter the room.<br><br>When you call the first time to join the room or disconnect and reconnect due to poor network conditions, the room entry fails due to a server error. The SDK automatically retries the room. |
   |kWarningCodePublishStreamFailed |`-2002` |Release audio & video stream failed.<br><br>When you publish audio & video streams in your room, the publication fails due to a server error. The SDK automatically retries the release. |
   |kWarningCodeSubscribeStreamFailed404 |`-2003` |Subscription to audio & video stream failed.<br><br>The subscription failed because the audio & video stream for the subscription could not be found in the current room. The SDK will automatically retry the subscription. If the subscription fails, it is recommended that you exit the retry. |
   |kWarningCodeSubscribeStreamFailed5xx |`-2004` |Subscription to audio & video stream failed.<br><br>When you subscribe to audio & video streams in your room, the subscription fails due to a server error. The SDK automatically retries the subscription. |
   |kWarningCodePublishStreamForbidden |`-2009` |This warning is triggered when you call [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setuservisibility) to set yourself unvisible to others and then try to publish the flow. |
   |kWarningCodeSubscribeStreamForbidden |`-2010` |When automatic subscription mode is not turned off, trying to turn on manual subscription mode will trigger this warning.<br><br>You need to turn off the automatic subscription mode before entering the room, and then call the [subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-subscribestreamvideo) / [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-subscribestreamaudio) method to manually subscribe to the audio & video stream. |
   |kWarningCodeSendCustomMessage |`-2011` |Sending a custom broadcast message failed, you are not currently in the room. |
   |kWarningCodeUserNotifyStop |`-2013` |When the number of people in the room exceeds 500, stop sending [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserjoined) and [onUserLeave](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserleave) callbacks to existing users in the room, and prompt all users in the room via broadcast. |
   |kWarningCodeUserInPublish |`-2014` |user had published in other room or had published public stream. |
   |kWarningCodeOldRoomBeenReplaced |`-2016` |A newly created room replaced the old room with the same room ID. |
   |kWarningCodeInEchoTestMode |`-2017` |This API cannot be called while an echo test is running. |
   |kWarningCodeNoCameraPermission |`-5001` |The camera permission is abnormal, and the current application does not obtain the camera permission. |
   |kWarningCodeSetScreenAudioSourceTypeFailed |`-5009` |Setting the screen audio capture type with `setScreenAudioSourceType` after screen audio is published is not supported, please set before it. |
   |kWarningCodeSetScreenAudioStreamIndexFailed |`-5010` |Setting the screen\-sharing audio capture mode after screen audio is published is not supported. |
   |kWarningCodeInvalidVoicePitch |`-5011` |Invalid pitch value setting. |
   |kWarningCodeInvalidAudioFormat |`-5012` |Invalid audio format setting. |
   |kWarningCodeInvalidCallForExtAudio |`-5013` |Mixed use of old and new interfaces for external audio sources. |
   |kWarningCodeInvalidCanvasHandle |`-6001` |The specified internal rendering canvas handle is invalid.<br><br>This callback is triggered when you specify an invalid canvas handle when you call [setupLocalVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setuplocalvideo) or [setupRemoteVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setupremotevideo). |
   |kWarningLicenseFileExpired |`-7001` |The authentication file is invalid. When checking the status of the authentication file, if the local file is inconsistent with the remote file, a<br><br>second warning will be triggered. |
   |kWarningInvaildSamiAppkeyORToken |`-7002` |Authorization failure for [BytePlus Audio SDK](https://go.byteplus.com/audio-sdk). Contact the technical supporters. |
   |kWarningInvaildSamiResourcePath |`-7003` |Failure to get the resource for [BytePlus Audio SDK](https://go.byteplus.com/audio-sdk). Input the right DAT path or contact the technical supporters. |
   |kWarningLoadSamiLibraryFailed |`-7004` |Failure to load the library for [BytePlus Audio SDK](https://go.byteplus.com/audio-sdk). Use right library or contact the technical supporters. |
   |kWarningInvaildSamiEffectType |`-7005` |The audio effect is not supported by [BytePlus Audio SDK](https://go.byteplus.com/audio-sdk). Contact the technical supporters. |

## ErrorCode

* **Type**: `enum`

* **Description**: Callback error code.

   When an unrecoverable error is encountered inside the SDK, the user is notified via the [onError](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onerror) callback.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kErrorCodeInvalidToken |`-1000` |Token is invalid.<br><br>The Token used when joining the room is invalid or expired. The user is required to retrieve the token and call the [updateToken](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updatetoken) to update the token. |
   |kErrorCodeJoinRoom |`-1001` |Join room error.<br><br>An unknown error occurred while joining the room, which caused the joining room to fail. Users are required to rejoin the room. |
   |kErrorCodeNoPublishPermission |`-1002` |No permission to publish audio & video streams.<br><br>The user failed to publish the audio & video stream in the room. The reason for the failure is that the user does not have permission to publish the stream. |
   |kErrorCodeNoSubscribePermission |`-1003` |No subscription permissions for audio & video streams.<br><br>The user failed to subscribe to the audio & video stream in the room where the user is located. The reason for the failure is that the user does not have permission to subscribe to the stream. |
   |kErrorCodeDuplicateLogin |`-1004` |The user has been removed from the room because the same user joined the room on the other client. |
   |kErrorCodeKickedOut |`-1006` |The user has been removed from the room by the administrator via a OpenAPI call. |
   |kRoomErrorCodeRoomIdIllegal |`-1007` |When calling [createRTCRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-creatertcroom), if the roomid is illegal, it will return null and throw the error. |
   |kRoomErrorTokenExpired |`-1009` |Token expired. Call [joinRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-joinroom) to rejoin with a valid Token. |
   |kRoomErrorUpdateTokenWithInvalidToken |`-1010` |The Token you provided when calling [updateToken](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updatetoken) is invalid. |
   |kErrorCodeRoomDismiss |`-1011` |Users have been removed from the room because the administrator dismissed the room by calling OpenAPI. |
   |kErrorCodeRoomAlreadyExist |`-1013` |there is a room with the same roomId，whose room id is the same with echo test. |
   |kErrorCodeOverStreamSubscribeLimit |`-1070` |Subscription to audio & video stream failed, the total number of subscribed audio & video streams exceeded the upper limit.<br><br>In the game scenario, in order to ensure the performance and quality of audio & video calls, the server will limit the total number of audio & video streams subscribed by the user. When the total number of audio & video streams subscribed by the user has reached the maximum, continuing to subscribe to more streams will fail, and the user will receive this error notification. |
   |kErrorCodeOverStreamPublishLimit |`-1080` |Publishing flow failed, the total number of publishing flows exceeds the upper limit. The<br><br>RTC system limits the total number of streams published in a single room, including video streams, audio streams, and screen streams. Local users will fail to publish streams to the room when the maximum number of published streams in the room has been reached, and will receive this error notification. |
   |[Deprecated] kErrorCodeOverVideoPublishLimit |`-1082` |Deprecated since 3.52. Use `kErrorCodeOverStreamPublishLimit` (`-1080`) instead.<br><br>The number of published video streams exceeds the limit. |
   |kErrorCodeInvalidAudioSyncUidRepeated |`-1083` |A/V synchronization failed.<br><br>Current source audio ID has been set by other video publishers in the same room.<br><br>One single audio source cannot be synchronized with multiple video sources at the same time. |
   |kErrorCodeAbnormalServerStatus |`-1084` |The user has been removed from the room due to the abnormal status of server.<br><br>SDK is disconnected with the signaling server. It will not reconnect automatically. Please contact technical support. |
   |kErrorCodeJoinRoomRoomForbidden |`-1025` |The room has banned before the user calls [joinRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-joinroom). |
   |kErrorCodeJoinRoomUserForbidden |`-1026` |The user has banned before calling [joinRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-joinroom). |

## LocalAudioStreamError

* **Type**: `enum`

* **Description**: Error code when the local audio state changes.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kLocalAudioStreamErrorOk |`0` |Local audio status is normal. |
   |kLocalAudioStreamErrorFailure |`1` |Local audio error cause unknown. |
   |kLocalAudioStreamErrorDeviceNoPermission |`2` |No permission to start local audio recording device. |
   |kLocalAudioStreamErrorRecordFailure |`4` |Local audio recording failed, it is recommended that you check whether the recording device is working properly. |
   |kLocalAudioStreamErrorEncodeFailure |`5` |Local audio encoding failed. |
   |kLocalAudioStreamErrorNoRecordingDevice |`6` |No audio recording equipment available. |

## LocalVideoStreamError

* **Type**: `enum`

* **Description**: Error Codes for the local video state changed.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kLocalVideoStreamErrorOk |`0` |Normal. |
   |kLocalVideoStreamErrorFailure |`1` |Local video stream publishing failed. |
   |kLocalVideoStreamErrorDeviceNoPermission |`2` |No access to the local video capture device. |
   |kLocalVideoStreamErrorDeviceBusy |`3` |Local video capture equipment is occupied. |
   |kLocalVideoStreamErrorDeviceNotFound |`4` |Local video capture device does not exist. |
   |kLocalVideoStreamErrorCaptureFailure |`5` |Local video capture failed, it is recommended to check whether the acquisition device is working properly. |
   |kLocalVideoStreamErrorEncodeFailure |`6` |Local video encoding failed. |
   |kLocalVideoStreamErrorDeviceDisconnected |`7` |The local video capture device is disconnected. It is occupied by other programs during the call. |

## MessageSendResultCode

* **Type**: `enum`

* **Description**: Result of sending messages and the reason for failure. For P2P messages, `0` indicates success. For room broadcast messages, `200` indicates success.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |MESSAGE_CODE_SUCCESS |`0` |The P2P message has been sent successfully. |
   |MESSAGE_CODE_ROOM_SUCCESS |`200` |The room\-wide broadcasting message has been sent successfully. |
   |MESSAGE_CODE_ERROR_TIMEOUT |`1` |Failure. Sending timeout. |
   |MESSAGE_CODE_ERROR_BROKEN |`2` |Failure. Channel disconnected. |
   |MESSAGE_CODE_ERROR_NOT_RECEIVER |`3` |Failure. Recipient not found. |
   |MESSAGE_CODE_ERROR_NOT_JOIN |`100` |Failure. The sender of the message did not join the room. |
   |MESSAGE_CODE_ERROR_NO_CONNECTION |`102` |Failure. No data transmission channel connection available. |
   |MESSAGE_CODE_ERROR_EXCEED_MAX_LENGTH |`103` |Failure. The message exceeds the maximum size. By default, the maximum size of a single message is 1 KB. After the advanced RTS feature is enabled, the maximum size is 64 KB. |
   |MESSAGE_CODE_ERROR_EMPTY_USER |`104` |Failure. The id of the recipient is empty. |
   |MESSAGE_CODE_ERROR_UNKNOWN |`1000` |Failure. Unknown error. |

## SingleStreamTaskErrorCode

* **Type**: `enum`

* **Description**: Single stream push task error codes.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kSingleStreamTaskErrorCodeOK |`0` |Success. |
   |kSingleStreamTaskErrorCodeUnKnownByServer |`1091` |Unknown server error. |
   |kSingleStreamTaskErrorCodeSignalRequestTimeout |`1092` |Task processing timed out. Check the network status and try again. |
   |kSingleStreamTaskErrorCodeInvalidParamByServer |`1093` |Invalid parameter detected by the server. |
   |kSingleStreamTaskErrorRemoteKicked |`1094` |The user ID of the task in the destination room is kicked out. |
   |kSingleStreamTaskErrorCodeJoinDestRoomFailed |`1095` |Failed to join the destination room. |
   |kSingleStreamTaskErrorCodeReceiveSrcStreamTimeout |`1096` |Timeout while receiving source stream in the source room. |
   |kSingleStreamTaskErrorCodeNotSurportCodec |`1097` |Audio and video codec task is not supported. |
   |kSingleStreamTaskErrorCodePushToCDN |`1098` |Failed to push the stream to CDN. |
   |kSingleStreamTaskErrorCodeCountOverLimit |`1099` |The number of single\-stream forwarding tasks exceeds the limit. One host can run no more than 20 tasks at the same time. |

## PlayerError

* **Type**: `enum`

* **Description**: Error code for audio playout.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kPlayerErrorOK |`0` |OK. |
   |kPlayerErrorFormatNotSupport |`1` |Format not supported. |
   |kPlayerErrorInvalidPath |`2` |Invalid file path. |
   |kPlayerErrorInvalidState |`3` |The prerequisite is not met. Check the specific API doc. |
   |kPlayerErrorInvalidPosition |`4` |Invalid position. |
   |kPlayerErrorInvalidVolume |`5` |Invalid volume. |
   |kPlayerErrorInvalidPitch |`6` |Invalid pitch value. |
   |kPlayerErrorInvalidAudioTrackIndex |`7` |Invalid audio track. |
   |kPlayerErrorInvalidPlaybackSpeed |`8` |Invalid playback speed. |
   |kPlayerErrorInvalidEffectId |`9` |Invalid effect ID. Receive this error code when you call other APIs before the audio file is preloaded or opened. |

## SnapshotErrorCode

* **Type**: `enum`

* **Description**: Snapshot error codes.

* **Member**

   |Property |Value |Description |
   |---|---|---|
   |kSnapshotErrorCodeOk |`0` |Success. |
   |kSnapshotErrorCodeCreateFail |`-1` |Failure. Fails to generate the image data or encode RGBA. |
   |kSnapshotErrorCodeStreamInvalid |`-2` |Failure. The stream is invalid. |
   |kSnapshotErrorCodeTimeout |`-3` |Failure. Snapshot timeout, with a default timeout of 1 second. |
   |kSnapshotErrorCodeFileSaveError |`-4` |Failure. Failed to save the image. |
