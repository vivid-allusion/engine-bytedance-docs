---
title: "Callback"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-85533"
---

## RTCVIDEOCALLBACK

Type: `interface`

* **Callbacks**

|Callback |Description |
|---|---|
|[onLogReport](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onlogreport) |Terminal monitoring log callback. The callback is triggered when a terminal monitoring event is generated. |
|[onTakeLocalSnapshotResult](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-ontakelocalsnapshotresult) |Receives the callback after calling [takeLocalSnapshot](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-takelocalsnapshot). |
|[onTakeRemoteSnapshotResult](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-ontakeremotesnapshotresult) |Receives the callback after calling [takeRemoteSnapshot](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-takeremotesnapshot). |
|[onStreamSyncInfoReceived](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onstreamsyncinforeceived) |Audio stream synchronization information callback. You can use this callback to receive audio stream synchronization information sent remotely after the remote user calls [sendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-sendstreamsyncinfo) to send an audio stream synchronization message. |
|[onCloudProxyConnected](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-oncloudproxyconnected) |Receives the callback when you call [startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startcloudproxy) to start cloud proxy, and the SDK connects the proxy server successfully. |
|[onNetworkTimeSynchronized](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onnetworktimesynchronized) |After calling [getNetworkTimeInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getnetworktimeinfo) for the first time, the SDK starts network time synchronization internally. This callback will be triggered when the synchronization is completed. |
|[onFaceDetectResult](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onfacedetectresult) |Callback of the result of face detection with Effect SDK.<br><br>After calling [enableFaceDetection](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enablefacedetection) and using the Effect SDK integrated in the RTC SDK, you will receive this callback. |
|[onAudioDeviceVolumeChanged](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onaudiodevicevolumechanged) |Callback to notify you the volume of the audio device has been changed or when the device has been muted or unmuted. No need to activate the notification beforehand. |
|[onAudioRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onaudiorecordingstateupdate) |When calling [startAudioRecording](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudiorecording) or [stopAudioRecording](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopaudiorecording) to change the recording status, receive the callback. |
|[onExtensionAccessError](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onextensionaccesserror) |Failed to access the extension.<br><br>RTC SDK provides some features with extensions. Without implementing the extension, you cannot use the corresponding feature. |
|[onHardwareEchoDetectionResult](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onhardwareechodetectionresult) |Callback that notifies you of the result of the echo detection before a call. |
|[onLocalProxyStateChanged](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onlocalproxystatechanged) |Callback on local proxy connection. After calling [setLocalProxy](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setlocalproxy) to set local proxies, you will receive this callback that informs you of the states of local proxy connection. |
|[onMixedStreamEvent](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onmixedstreamevent) |Reports events for a server\-side mixed\-stream push task. |
|[onLocalVideoFrame](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onlocalvideoframe) |Receives successfully captured local camera frames for custom processing or rendering. |
|[onRemoteVideoFrame](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onremotevideoframe) |Receives successfully captured remote camera frames for custom processing or rendering. |
|[onWarning](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onwarning) |This callback informs you of a warning message. |
|[onError](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onerror) |This callback informs you of an error message. |
|[onConnectionStateChanged](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onconnectionstatechanged) |SDK connection state change callback with signaling server. Triggered when the connection state changes. |
|[onNetworkTypeChanged](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onnetworktypechanged) |SDK Current network connection type change callback. Triggers the event when the current network connection type of the SDK changes. |
|[onPerformanceAlarms](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onperformancealarms) |Publish performance fallback is not turned on locally. When insufficient device performance is detected, this callback is received. Locally turn on the publish performance fallback. When the publish performance fallback/recovery is caused due to device performance/network reasons, this callback is received. |
|[onSysStats](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onsysstats) |Periodically (2s) issue callbacks to report the current CPU and memory usage. |
|[onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onuserstartaudiocapture) |The remote clients in the room will be informed of the state change via this callback after the visible user starts audio capture by calling [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudiocapture). |
|[onUserStopAudioCapture](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onuserstopaudiocapture) |The remote clients in the room will be informed of the state change via this callback after the visible user stops audio capture by calling [stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopaudiocapture). |
|[onFirstLocalAudioFrame](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onfirstlocalaudioframe) |Receive the callback when the first audio frame is locally collected. |
|[onFirstRemoteAudioFrame](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onfirstremoteaudioframe) |This callback informs you when the first frame of every remote audio is received. |
|[onSimulcastSubscribeFallback](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onsimulcastsubscribefallback) |Once the Fallback option is set, Fallback or reverting from a Fallback of a media stream will trigger this callback. |
|[onFirstLocalVideoFrameCaptured](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onfirstlocalvideoframecaptured) |RTC SDK receives this callback when the first video frame or screen video frame capture is completed locally. |
|[onLocalVideoSizeChanged](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onlocalvideosizechanged) |Receive this callback when the local video size or rotation configuration changes. |
|[onRemoteVideoSizeChanged](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onremotevideosizechanged) |Users in the room who subscribe to this video stream receive this callback when the remote video size or rotation configuration changes. |
|[onFirstRemoteVideoFrameRendered](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onfirstremotevideoframerendered) |Receive this callback after the first frame of remote video stream is locally rendered by SDK. |
|[onFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onfirstremotevideoframedecoded) |Receive this callback after the first frame of remote video stream is received and decoded by SDK. |
|[onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onuserstartvideocapture) |The remote clients in the room will be informed of the state change via this callback after the visible user starts video capture by calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startvideocapture). |
|[onUserStopVideoCapture](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onuserstopvideocapture) |The remote clients in the room will be informed of the state change via this callback after the visible user stops video capture by calling [stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopvideocapture). |
|[onLocalAudioStateChanged](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onlocalaudiostatechanged) |When the state of the local audio changes, the callback notifies the current local audio state. |
|[onRemoteAudioStateChanged](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onremoteaudiostatechanged) |When the state of the subscribed remote audio stream changes, you will receive this callback to get the current state of the remote audio stream. |
|[onActiveSpeaker](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onactivespeaker) |After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableaudiopropertiesreport), you will periodically receive this callback for the active speaker information. |
|[onLocalVideoStateChanged](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onlocalvideostatechanged) |Receive this event when the state of the local video stream changes. |
|[onRemoteVideoStateChanged](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onremotevideostatechanged) |When the state of a remote video stream changes, users in the room who subscribe to this stream receive the event. |
|[onAudioFrameSendStateChanged](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onaudioframesendstatechanged) |Audio first frame sending status change callback. |
|[onVideoFrameSendStateChanged](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onvideoframesendstatechanged) |Video first frame sending status change callback. |
|[onAudioFramePlayStateChanged](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onaudioframeplaystatechanged) |Audio first frame playback state change callback. |
|[onVideoFramePlayStateChanged](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onvideoframeplaystatechanged) |Video first frame playback state change callback. |
|[onUserMessageSendResult](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onusermessagesendresult) |After sending a text or binary message (P2P) to a single user in the room, the message sender receives a callback with the result of the message. |
|[onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onuserbinarymessagereceived) |Receive this callback when you receive a binary message from an out\-of\-room user calling [sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-senduserbinarymessage). |
|[onSEIMessageReceived](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onseimessagereceived) |Receive this callback when you receive a video frame with a SEI message sent via sendSEIMessage. |
|[onSingleStreamEvent](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onsinglestreamevent) |Used for reporting events during pushing a single stream to CDN. |
|[onRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onrecordingstateupdate) |Callback of the local recording status. |
|[onRecordingProgressUpdate](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onrecordingprogressupdate) |Local recording progress callback. |
|[onLoginResult](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onloginresult) |login result callback. |
|[onLogout](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onlogout) |logout result callback. |
|[onServerParamsSetResult](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onserverparamssetresult) |Returns the result of setting the application server parameters. |
|[onGetPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-ongetpeeronlinestatus) |Callback to tell the login state of a user. |
|[onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onusermessagereceivedoutsideroom) |Receive this callback when you receive a text message from an out\-of\-room user calling sendUserMessageOutsideRoom. |
|[onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onuserbinarymessagereceivedoutsideroom) |Receive this callback when you receive a binary message from an out\-of\-room user calling [sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-senduserbinarymessageoutsideroom). |
|[onUserMessageSendResultOutsideRoom](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onusermessagesendresultoutsideroom) |Callback triggered when a message is sent to a specified user outside the room. |
|[onServerMessageSendResult](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onservermessagesendresult) |Callback to send a message to the application server. |
|[onRecordAudioFrame](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onrecordaudioframe) |Returns audio data recorded by microphone. |
|[onPlaybackAudioFrame](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onplaybackaudioframe) |Returns the mixed audio data of all subscribed remote users. |
|[onMixedAudioFrame](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onmixedaudioframe) |Returns mixed audio data including both data recorded by the local microphone and data from all subscribed remote users. |
|[onASRSuccess](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onasrsuccess) |Speech recognition service started successfully. |
|[onMessage](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onmessage) |The voice\-to\-text callback is successful, and the callback returns the full amount of messages after recognition. |
|[onASRError](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onasrerror) |This callback is triggered when an error event occurs within the speech recognition service. |
|[onNetworkDetectionResult](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onnetworkdetectionresult) |Pre\-call network detection result. |
|[onNetworkDetectionStopped](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onnetworkdetectionstopped) |Pre\-call network probing ends. |
|[onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onlocalaudiopropertiesreport) |After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableaudiopropertiesreport), you will periodically receive this callback for the information about local audio. |
|[onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onremoteaudiopropertiesreport) |After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableaudiopropertiesreport), you will periodically receive this callback with information about subscribed remote audio streams. |
|[onEchoTestResult](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onechotestresult) |Callback about the call test result. |
|[onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onvideodevicestatechanged) |Callback of video device state. Video devices include cameras and screen sharing video capture devices. |
|[onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onaudiodevicestatechanged) |Callback for audio device state changes. Audio devices include capture and playback devices. |
|[onAudioPlaybackDeviceTestVolume](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onaudioplaybackdevicetestvolume) |Notification on the playing volume during the test for the local audio devices. |
|[onLocalSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onlocalsnapshottakentofile) |Triggered after calling [takeLocalSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-takelocalsnapshottofile) to report whether the snapshot is taken successfully and provide details of the snapshot image. |
|[onRemoteSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onremotesnapshottakentofile) |Triggered after calling [takeRemoteSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-takeremotesnapshottofile) to report whether the snapshot is taken successfully and provide details of the snapshot image. |
|[onRemoteUserAudioFrame](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onremoteuseraudioframe) |Returns the audio data of one remote user. |
|[onRecordScreenAudioFrame](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onrecordscreenaudioframe) |Returns the audio data played locally. |
|[onCaptureMixedAudioFrame](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-oncapturemixedaudioframe) |Returns audio data recorded by microphone and the audio mixing data from MediaPlayer, KTVPlayer, EffectPlayer. |
|[onAudioDeviceWarning](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onaudiodevicewarning) |Audio device warning callback. The audio devices include audio capture devices and audio rendering devices. |
|[onVideoDeviceWarning](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onvideodevicewarning) |Video device warning callback. The video devices include video capture devices. |
|[onSEIStreamUpdate](https://docs.byteplus.com/en/docs/12/14197#rtcvideocallback-onseistreamupdate) |Callback about publishing status of the black frame video stream. |

### onLogReport

Terminal monitoring log callback. The callback is triggered when a terminal monitoring event is generated.

* **Signature**

   ```ts
   (
     log_type: string,
     log_content: string
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |log_type |string |Event type. For now, "live_webrtc_monitor_log" is the only one available value. |
   |log_content |string |Terminal monitoring log content. |

### onTakeLocalSnapshotResult

Receives the callback after calling [takeLocalSnapshot](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-takelocalsnapshot).

* **Signature**

   ```ts
   (
     task_id: number,
     stream_index: number,
     image: string,
     error_code: number
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |task_id |number |The index for the snapshot, the same as the return value of [takeLocalSnapshot](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-takelocalsnapshot). |
   |stream_index |number |Stream properties, mainstream or screen streams. |
   |image |string |The snapshot image. If the snapshot task fails, the value is `null`. |
   |error_code |number |Error code:<br><br><br>* `0`: Success.<br><br>* `-1`: Failure. Fails to generate the image.<br><br>* `-2`: Failure. The stream is invalid. |

### onTakeRemoteSnapshotResult

Receives the callback after calling [takeRemoteSnapshot](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-takeremotesnapshot).

* **Signature**

   ```ts
   (
     task_id: number,
     stream_id: string,
     stream_info: StreamInfo,
     image: string,
     error_code: number
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |task_id |number |The index for the remote snapshot, the same as the return value of [takeRemoteSnapshot](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-takeremotesnapshot). |
   |stream_id |string |Remote stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Remote stream information. |
   |image |string |The snapshot image. If the snapshot task fails, the value is `null`. |
   |error_code |number |Error code:<br><br><br>* `0`: Success.<br><br>* `-1`: Failure. Fails to generate the image.<br><br>* `-2`: Failure. The stream is invalid. |

### onStreamSyncInfoReceived

Audio stream synchronization information callback. You can use this callback to receive audio stream synchronization information sent remotely after the remote user calls [sendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-sendstreamsyncinfo) to send an audio stream synchronization message.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     stream_type: SyncInfoStreamType,
     data: string
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Remote stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Remote stream information. |
   |stream_type |SyncInfoStreamType |Media stream type. See [SyncInfoStreamType](https://docs.byteplus.com/en/docs/12/docs-85535#syncinfostreamtype). |
   |data |string |Message content. |

### onCloudProxyConnected

Receives the callback when you call [startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startcloudproxy) to start cloud proxy, and the SDK connects the proxy server successfully.

* **Signature**

   ```ts
   (interval: number) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |interval |number |The interval in ms between starting cloud proxy and connects the cloud proxy server successfully. |

### onNetworkTimeSynchronized

After calling [getNetworkTimeInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getnetworktimeinfo) for the first time, the SDK starts network time synchronization internally. This callback will be triggered when the synchronization is completed.

* **Signature**

   ```ts
   () => void
   ```

### onFaceDetectResult

Callback of the result of face detection with Effect SDK.

After calling [enableFaceDetection](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enablefacedetection) and using the Effect SDK integrated in the RTC SDK, you will receive this callback.

* **Signature**

   ```ts
   (
     detect_result: FaceDetectResult["detect_result"],
     face_count: FaceDetectResult["face_count"],
     rect: FaceDetectResult["rect"],
     image_width: FaceDetectResult["image_width"],
     image_height: FaceDetectResult["image_height"],
     frame_timestamp_us: FaceDetectResult["frame_timestamp_us"]
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |detect_result |number |Face detection result code. |
   |face_count |number |Number of detected faces. |
   |rect |Rectangle[] |Bounding rectangles of the detected faces. The array length equals `face_count`. |
   |image_width |number |Width of the source image in pixels. |
   |image_height |number |Height of the source image in pixels. |
   |frame_timestamp_us |number |Timestamp of the video frame used for face detection, in microseconds. |

### onAudioDeviceVolumeChanged

Callback to notify you the volume of the audio device has been changed or when the device has been muted or unmuted. No need to activate the notification beforehand.

* **Signature**

   ```ts
   (
     device_type: RTCAudioDeviceType,
     volume: number,
     muted: boolean
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |device_type |[RTCAudioDeviceType](https://docs.byteplus.com/en/docs/12/docs-85535#rtcaudiodevicetype) |Includes microphones and speakers. |
   |volume |number |Volume ranging [0, 255]. When the volume turns to 0, muted turns to true. Note that on Windows, when the volume of a microphone turns to 0, muted remains unchanged. |
   |muted |boolean |Whether the device is muted. When a speaker is muted, muted turns true but volume remains unchanged. |

### onAudioRecordingStateUpdate

When calling [startAudioRecording](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudiorecording) or [stopAudioRecording](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopaudiorecording) to change the recording status, receive the callback.

* **Signature**

   ```ts
   (
     state: AudioRecordingState,
     error_code: AudioRecordingErrorCode
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |state |[AudioRecordingState](https://docs.byteplus.com/en/docs/12/docs-85535#audiorecordingstate) |Recording state. |
   |error_code |[AudioRecordingErrorCode](https://docs.byteplus.com/en/docs/12/docs-85534#audiorecordingerrorcode) |Error code. |

### onExtensionAccessError

Failed to access the extension.

RTC SDK provides some features with extensions. Without implementing the extension, you cannot use the corresponding feature.

* **Signature**

   ```ts
   (
     extensionName: string,
     msg: string
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |extensionName |string |The name of extension. |
   |msg |string |Error message. |

### onHardwareEchoDetectionResult

Callback that notifies you the result of the echo detection before a call.

* **Signature**

   ```ts
   (hardware_echo_detection_result: HardwareEchoDetectionResult) => void
   ```

* **Notes**

   * This callback notifies you the result of the echo detection by calling [startHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-starthardwareechodetection).

   * We recommend to call [stopHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stophardwareechodetection) to stop the detection.

   * Listen to `kMediaDeviceWarningLeakEchoDetected` in the callback of [onAudioDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onaudiodevicewarning) for the echo issue during a call.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |hardware_echo_detection_result |[HardwareEchoDetectionResult](https://docs.byteplus.com/en/docs/12/docs-85535#hardwareechodetectionresult) |The result of the echo detection. |

### onLocalProxyStateChanged

Callback on local proxy connection. After calling [setLocalProxy](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setlocalproxy) to set local proxies, you will receive this callback that informs you of the states of local proxy connection.

* **Signature**

   ```ts
   (
     local_proxy_type: LocalProxyType,
     local_proxy_state: LocalProxyState,
     local_proxy_error: LocalProxyError
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |local_proxy_type |[LocalProxyType](https://docs.byteplus.com/en/docs/12/docs-85535#localproxytype) |The types of local proxies. |
   |local_proxy_state |[LocalProxyState](https://docs.byteplus.com/en/docs/12/docs-85535#localproxystate) |The states of local proxy connection. |
   |local_proxy_error |[LocalProxyError](https://docs.byteplus.com/en/docs/12/docs-85534#localproxyerror) |The errors of local proxy connection. |

### onMixedStreamEvent

Reports events for a server\-side mixed\-stream push task.

* **Signature**

   ```ts
   (
     info: MixedStreamTaskInfo,
     event: MixedStreamTaskEvent,
     error_code: MixedStreamTaskErrorCode
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |info |[MixedStreamTaskInfo](https://docs.byteplus.com/en/docs/12/docs-85535#mixedstreamtaskinfo) |Mixed\-stream push task information, including the task ID and push target type. |
   |event |[MixedStreamTaskEvent](https://docs.byteplus.com/en/docs/12/docs-85535#mixedstreamtaskevent) |Mixed\-stream push task event. |
   |error_code |[MixedStreamTaskErrorCode](https://docs.byteplus.com/en/docs/12/docs-85534#mixedstreamtaskerrorcode) |Mixed\-stream push task error code. |

### onLocalVideoFrame

Receives successfully captured local camera frames for custom processing or rendering.

* **Signature**

   ```ts
   (frame: IVideoFrame) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |frame |[IVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85535#ivideoframe) |Video frame. |

### onRemoteVideoFrame

Receives successfully captured remote camera frames for custom processing or rendering.

* **Signature**

   ```ts
   (frame: IVideoFrame) => void
   ```

* **Notes**

   The pixel format of the video frame varies by platform.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |frame |[IVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85535#ivideoframe) |Video frame. |

### onWarning

This callback informs you of a warning message.

* **Signature**

   ```ts
   (warn: WarningCode) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |warn |[WarningCode](https://docs.byteplus.com/en/docs/12/docs-85534#warningcode) |Warning code. |

### onError

This callback informs you of an error message.

* **Signature**

   ```ts
   (err: ErrorCode) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |err |[ErrorCode](https://docs.byteplus.com/en/docs/12/docs-85534#errorcode) |Error code. |

### onConnectionStateChanged

SDK connection state change callback with signaling server. Triggered when the connection state changes.

* **Signature**

   ```ts
   (state: ConnectionState) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |state |[ConnectionState](https://docs.byteplus.com/en/docs/12/docs-85535#connectionstate) |The current connection status between the SDK and the signaling server. |

### onNetworkTypeChanged

SDK Current network connection type change callback. Callbacks the event when the current network connection type of the SDK changes.

* **Signature**

   ```ts
   (type: NetworkType) => void
   ```

* **Notes**

   Refer to [Getting Connection Status](https://docs.byteplus.com/byteplus-rtc/docs/95376) for more details.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |type |[NetworkType](https://docs.byteplus.com/en/docs/12/docs-85535#networktype) |The current network connection type. |

### onPerformanceAlarms

publish performance fallback is not turned on locally. When insufficient device performance is detected, this callback is received. Locally turn on the release performance fallback. When the release performance fallback/recovery is caused due to device performance/network reasons, this callback is received.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     mode: PerformanceAlarmMode,
     reason: PerformanceAlarmReason,
     data: SourceWantedData
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Stream ID affected by the alarm. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Stream information affected by the alarm. |
   |mode |[PerformanceAlarmMode](https://docs.byteplus.com/en/docs/12/docs-85535#performancealarmmode) |Indicates whether the release fallback function is turned on locally.<br><br><br>* When the publisher does not enable publish fallback, the mode is `kPerformanceAlarmModeNormal`.<br><br>* When the publisher enables publish fallback, the mode is `kPerformanceAlarmModeSimulcast`. |
   |reason |[PerformanceAlarmReason](https://docs.byteplus.com/en/docs/12/docs-85535#performancealarmreason) |Reason for the alarm. |
   |data |[SourceWantedData](https://docs.byteplus.com/en/docs/12/docs-85535#sourcewanteddata) |Performance rollback related data. |

### onSysStats

Periodically (2s) issue callbacks to report the current CPU and memory usage.

* **Signature**

   ```ts
   (stats: SysStats) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stats |[SysStats](https://docs.byteplus.com/en/docs/12/docs-85535#sysstats) |Return the current system state information. |

### onUserStartAudioCapture

The remote clients in the room will be informed of the state change via this callback after the visible user starts audio capture by calling [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudiocapture).

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Remote stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Remote stream information. |

### onUserStopAudioCapture

The remote clients in the room will be informed of the state change via this callback after the visible user stops audio capture by calling [stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopaudiocapture).

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Remote stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Remote stream information. |

### onFirstLocalAudioFrame

Receive the callback when the first audio frame is locally collected.

* **Signature**

   ```ts
   () => void
   ```

### onFirstRemoteAudioFrame

This callback informs you when the first frame of every remote audio is received.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Remote stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Remote stream information. |

### onSimulcastSubscribeFallback

Once the Fallback option is set, Fallback or reverting from a Fallback of a media stream will trigger this callback.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     event: RemoteStreamSwitch
   ) => void
   ```

* **Notes**

   Call setSubscribeFallbackOption or configure Fallback options on the server side to register this callback.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Remote stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Remote stream information. |
   |event |[RemoteStreamSwitch](https://docs.byteplus.com/en/docs/12/docs-85535#remotestreamswitch) |Information of stream switching. |

### onFirstLocalVideoFrameCaptured

RTC SDK receives this callback when the first video frame or screen video frame capture is completed locally.

* **Signature**

   ```ts
   (info: VideoFrameInfo) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |info |[VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-85535#videoframeinfo) |Video information. |

### onLocalVideoSizeChanged

Receive this callback when the local video size or rotation configuration changes.

* **Signature**

   ```ts
   (info: VideoFrameInfo) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |info |[VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-85535#videoframeinfo) |Video frame information. |

### onRemoteVideoSizeChanged

Users in the room who subscribe to this video stream receive this callback when the remote video size or rotation configuration changes.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     stream: VideoFrameInfo
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Remote stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Remote stream information. |
   |stream |[VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-85535#videoframeinfo) |Video frame information. |

### onFirstRemoteVideoFrameRendered

Receive this callback after the first frame of remote video stream is locally rendered by SDK.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     info: VideoFrameInfo
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Remote stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Remote stream information. |
   |info |[VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-85535#videoframeinfo) |Video frame information. |

### onFirstRemoteVideoFrameDecoded

Receive this callback after the first frame of remote video stream is received and decoded by SDK.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     info: VideoFrameInfo
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Remote stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Remote stream information. |
   |info |[VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-85535#videoframeinfo) |Video frame information. |

### onUserStartVideoCapture

The remote clients in the room will be informed of the state change via this callback after the visible user starts video capture by calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startvideocapture).

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Stream information. |

### onUserStopVideoCapture

The remote clients in the room will be informed of the state change via this callback after the visible user stops video capture by calling [stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopvideocapture).

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Stream information. |

### onLocalAudioStateChanged

When the state of the local audio changes, the callback notifies the current local audio state.

* **Deprecated**

   since 3.50. Use [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onaudiodevicestatechanged) instead.

* **Signature**

   ```ts
   (
     state: LocalAudioStreamState,
     error: LocalAudioStreamError
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |state |[LocalAudioStreamState](https://docs.byteplus.com/en/docs/12/docs-85535#localaudiostreamstate) |State of the local audio device. |
   |error |[LocalAudioStreamError](https://docs.byteplus.com/en/docs/12/docs-85534#localaudiostreamerror) |Error code when the local audio state changes. |

### onRemoteAudioStateChanged

When the state of the audio stream from the remote user subscribes to changes, this callback will be received to understand the current state of the remote audio stream.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     state: RemoteAudioState,
     reason: RemoteAudioStateChangeReason
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Remote stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Remote stream information. |
   |state |[RemoteAudioState](https://docs.byteplus.com/en/docs/12/docs-85535#remoteaudiostate) |Remote audio stream state. |
   |reason |[RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-85535#remoteaudiostatechangereason) |Reason for remote audio stream state change. |

### onActiveSpeaker

After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableaudiopropertiesreport), you will periodically receive this callback for the active speaker information.

* **Signature**

   ```ts
   (
     room_id: string,
     uid: string
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |room_id |string |Room ID. |
   |uid |string |The user ID of the active speaker. |

### onLocalVideoStateChanged

Receive this event when the state of the local video stream changes.

* **Deprecated**

   since 3.50. Use [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onvideodevicestatechanged) instead.

* **Signature**

   ```ts
   (
     state: LocalVideoStreamState,
     error: LocalVideoStreamError
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |state |[LocalVideoStreamState](https://docs.byteplus.com/en/docs/12/docs-85535#localvideostreamstate) |Local video stream status. |
   |error |[LocalVideoStreamError](https://docs.byteplus.com/en/docs/12/docs-85534#localvideostreamerror) |Error code when local video status changes. |

### onRemoteVideoStateChanged

When the state of a remote video stream changes, users in the room who subscribe to this stream receive the event.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     state: RemoteVideoState,
     reason: RemoteVideoStateChangeReason
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Remote stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Remote stream information. |
   |state |[RemoteVideoState](https://docs.byteplus.com/en/docs/12/docs-85535#remotevideostate) |Remote video stream state. |
   |reason |[RemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-85535#remotevideostatechangereason) |Reason for the remote video stream state change. |

### onAudioFrameSendStateChanged

Audio first frame sending status change callback.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     user: RtcUser,
     state: FirstFrameSendState
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Stream information. |
   |user |[RtcUser](https://docs.byteplus.com/en/docs/12/docs-85535#rtcuser) |Local user information. |
   |state |[FirstFrameSendState](https://docs.byteplus.com/en/docs/12/docs-85535#firstframesendstate) |First frame sending state. |

### onVideoFrameSendStateChanged

Video first frame sending status change callback.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     user: RtcUser,
     state: FirstFrameSendState
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Stream information. |
   |user |[RtcUser](https://docs.byteplus.com/en/docs/12/docs-85535#rtcuser) |Local user information. |
   |state |[FirstFrameSendState](https://docs.byteplus.com/en/docs/12/docs-85535#firstframesendstate) |First frame sending state. |

### onAudioFramePlayStateChanged

Audio first frame playback state change callback.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     user: RtcUser,
     state: FirstFramePlayState
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Remote stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Remote stream information. |
   |user |[RtcUser](https://docs.byteplus.com/en/docs/12/docs-85535#rtcuser) |Remote user information. |
   |state |[FirstFramePlayState](https://docs.byteplus.com/en/docs/12/docs-85535#firstframeplaystate) |First frame playback state. |

### onVideoFramePlayStateChanged

Video first frame playback state change callback.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     user: RtcUser,
     state: FirstFramePlayState
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Remote stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Remote stream information. |
   |user |[RtcUser](https://docs.byteplus.com/en/docs/12/docs-85535#rtcuser) |Remote user information. |
   |state |[FirstFramePlayState](https://docs.byteplus.com/en/docs/12/docs-85535#firstframeplaystate) |First frame playback state. |

### onUserMessageSendResult

After sending a text or binary message (P2P) to a single user in the room, the message sender receives a callback with the result of the message.

* **Signature**

   ```ts
   (
     msgid: number,
     error: MessageSendResultCode
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |msgid |number |ID of this message. |
   |error |[MessageSendResultCode](https://docs.byteplus.com/en/docs/12/docs-85534#messagesendresultcode) |Message sending result. `0` indicates success. |

### onUserBinaryMessageReceived

Receive this callback when you receive a binary message from an out\-of\-room user calling [sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-senduserbinarymessage).

* **Signature**

   ```ts
   (
     uid: string,
     message: Buffer
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |uid |string |User ID of the message sender. |
   |message |Buffer |Content of the message. |

### onSEIMessageReceived

Receive this callback when you receive a video frame with a SEI message sent via sendSEIMessage.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     message: string
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Remote stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Remote stream information. |
   |message |string |Received SEI message. |

### onSingleStreamEvent

Used for reporting events during pushing a single stream to CDN.

* **Signature**

   ```ts
   (
     task_id: string,
     event: SingleStreamTaskEvent,
     error_code: SingleStreamTaskErrorCode
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |task_id |string |Task ID. |
   |event |[SingleStreamTaskEvent](https://docs.byteplus.com/en/docs/12/docs-85535#singlestreamtaskevent) |Task event. |
   |error_code |[SingleStreamTaskErrorCode](https://docs.byteplus.com/en/docs/12/docs-85534#singlestreamtaskerrorcode) |Task error code.<br><br><br>* `0`: Success.<br><br>* `1091`: Unknown server error.<br><br>* `1092`: Signaling request timed out.<br><br>* `1093`: Invalid parameters detected by the server.<br><br>* `1094`: The user ID of the task was kicked out of the destination room.<br><br>* `1095`: Failed to join the destination room.<br><br>* `1096`: Timed out while receiving the source stream.<br><br>* `1097`: The audio or video codec is not supported.<br><br>* `1098`: Failed to push the stream to CDN.<br><br>* `1099`: The number of single\-stream forwarding tasks exceeds the limit. |

### onRecordingStateUpdate

Callback of the local recording status.

* **Signature**

   ```ts
   (
     state: number,
     error_code: number,
     info: RecordingInfo
   ) => void
   ```

* **Notes**

   The callback is triggered by [startFileRecording](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startfilerecording) or [stopFileRecording](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopfilerecording).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |state |number |Recording state. |
   |error_code |number |Recording error code. |
   |info |[RecordingInfo](https://docs.byteplus.com/en/docs/12/docs-85535#recordinginfo) |For more information about the recorded file. |

### onRecordingProgressUpdate

Local recording progress callback.

* **Signature**

   ```ts
   (
     process: RecordingProgress,
     info: RecordingInfo
   ) => void
   ```

* **Notes**

   This callback is triggered by [startFileRecording](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startfilerecording). When the recording state is normal, the system will prompt the recording progress through this callback every second.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |process |[RecordingProgress](https://docs.byteplus.com/en/docs/12/docs-85535#recordingprogress) |Recording progress. |
   |info |[RecordingInfo](https://docs.byteplus.com/en/docs/12/docs-85535#recordinginfo) |More information about the recorded file. |

### onLoginResult

login result callback.

* **Signature**

   ```ts
   (
     uid: string,
     error_code: number,
     elapsed: number
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |uid |string |Login user ID. |
   |error_code |number |Login result. |
   |elapsed |number |The time taken from the call to [login](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-login) to the receipt of the result. Measured by ms. |

### onLogout

logout result callback.

* **Signature**

   ```ts
   (reason: LogoutReason) => void
   ```

* **Notes**

   After calling [logout](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-logout), you will receive this callback.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |reason |[LogoutReason](https://docs.byteplus.com/en/docs/12/docs-85535#logoutreason) |Logout reason. |

### onServerParamsSetResult

Set the return result of the application server parameter.

* **Signature**

   ```ts
   (error: number) => void
   ```

* **Notes**

   Receive this callback after calling [setServerParams](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setserverparams).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |error |number |Result code.<br><br><br>* 200, set successfully<br><br>* != 200: Failure. |

### onGetPeerOnlineStatus

Callback to tell the login state of a user.

* **Signature**

   ```ts
   (
     peer_user_id: string,
     status: number
   ) => void
   ```

* **Notes**

   Call [getPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getpeeronlinestatus) before you can get this callback.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |peer_user_id |string |User ID. |
   |status |number |Login status of the user. |

### onUserMessageReceivedOutsideRoom

Receive this callback when you receive a text message from an out\-of\-room user calling sendUserMessageOutsideRoom.

* **Signature**

   ```ts
   (
     uid: string,
     message: string
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |uid |string |User ID of the message sender. |
   |message |string |Received text message content. |

### onUserBinaryMessageReceivedOutsideRoom

Receive this callback when you receive a binary message from an out\-of\-room user calling [sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-senduserbinarymessageoutsideroom).

* **Signature**

   ```ts
   (
     uid: string,
     message: Buffer
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |uid |string |User ID of the message sender. |
   |message |Buffer |Binary message content received. |

### onUserMessageSendResultOutsideRoom

A callback that sends a message to a specified user outside the room.

* **Signature**

   ```ts
   (
     msgid: number,
     error: number
   ) => void
   ```

* **Notes**

   Receive this callback when a message is sent by calling [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-sendusermessageoutsideroom) or [sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-senduserbinarymessageoutsideroom).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |msgid |number |The ID of this message. All P2P and P2Server messages share a single ID sequence. |
   |error |number |Message sending result. |

### onServerMessageSendResult

Callback to send a message to the application server.

* **Signature**

   ```ts
   (
     msgid: number,
     error: number,
     msg: string
   ) => void
   ```

* **Notes**

   Receive this callback after calling [sendServerMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-sendservermessage) or [sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-sendserverbinarymessage).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |msgid |number |The ID of this message<br><br>All P2P and P2Server messages share a single ID sequence. |
   |error |number |Message Sending Results. |
   |msg |string |ACK message returned by the application server. The message must not exceed 64 KB. |

### onRecordAudioFrame

Returns audio data recorded by microphone.

* **Signature**

   ```ts
   (audio_frame: IAudioFrame) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |audio_frame |[IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85535#iaudioframe) |Audio data. |

### onPlaybackAudioFrame

Returns the mixed audio data of all subscribed remote users.

* **Signature**

   ```ts
   (audio_frame: IAudioFrame) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |audio_frame |[IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85535#iaudioframe) |Audio data. |

### onMixedAudioFrame

Returns mixed audio data including both data recorded by the local microphone and data from all subscribed remote users.

* **Signature**

   ```ts
   (audio_frame: IAudioFrame) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |audio_frame |[IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85535#iaudioframe) |Audio data. |

### onASRSuccess

Speech recognition service started successfully.

* **Signature**

   ```ts
   () => void
   ```

### onMessage

The voice\-to\-text callback is successful, and the callback returns the full amount of messages after recognition.

* **Signature**

   ```ts
   (message: string) => void
   ```

* **Notes**

   If the network connection is interrupted during the recognition process, the callback information after the reconnection contains only the text message recognized after the reconnection, and no longer contains the previously recognized messages.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |message |string |Text message obtained after the completion of the recognition. |

### onASRError

This callback is triggered when an error event occurs within the speech recognition service.

* **Signature**

   ```ts
   (
     error_code: number,
     error_message: string
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |error_code |number |Error code<br><br><br>* < 0: parameter error or API call order error.<br><br>* `-1`: Disconnected. SDK will keep retrying.<br><br>* `-2`: Call startASR repeatedly. Call stopASR when you intend to start ASR service again.<br><br>* `-3`: Token of ASR service is required.<br><br>* `-4`: secret_key is required in the Signature mode.<br><br>* `-5`: User ID is required.<br><br>* `-6`: App ID is required.<br><br>* `-7`: cluster is required.<br><br>* `-8`: Connection building error. Please contact our technical specialist for the correct SDK version with ASR service. |
   |error_message |string |Detailed error message. |

### onNetworkDetectionResult

Pre\-call network detection result.

* **Signature**

   ```ts
   (
     type: number,
     quality: number,
     rtt: number,
     lost_rate: number,
     bit_rate: number,
     jitter: number
   ) => void
   ```

* **Notes**

   After successfully calling [startNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startnetworkdetection), you will receive this callback for the first time in 3s and every 2s thereafter.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |type |number |Identifies the network type as uplink/downlink. |
   |quality |number |Network quality. |
   |rtt |number |Network RTT in ms. |
   |lost_rate |number |Packet loss rate. |
   |bit_rate |number |Network bandwidth in kbps. |
   |jitter |number |Network jitter in ms. |

### onNetworkDetectionStopped

Pre\-call network probing ends.

* **Signature**

   ```ts
   (reason: number) => void
   ```

* **Notes**

   The following will stop detection and receive this primary callback:

   1. This callback is received once when the [stopNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopnetworkdetection) interface is called to stop probing;

   2. Stop detection when the first frame of remote/local audio is received;

   3. Stop detecting when the detection exceeds 3 minutes;

   4. When the probe link is disconnected for a certain period of time, the probe is stopped.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |reason |number |Reason of stopping probing. |

### onLocalAudioPropertiesReport

After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableaudiopropertiesreport), you will periodically receive this callback for the information about local audio.

* **Signature**

   ```ts
   (
     audio_properties_infos: LocalAudioPropertiesInfo[],
     audio_properties_info_number: number
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |audio_properties_infos |[LocalAudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/docs-85535#localaudiopropertiesinfo)[] |Local audio which includes the microphone audio and the screen audio captured using RTC SDK internal mechanisms. |
   |audio_properties_info_number |number |length of the array which you can ignore. |

### onRemoteAudioPropertiesReport

After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableaudiopropertiesreport), you will periodically receive this callback with information about subscribed remote audio streams.

* **Signature**

   ```ts
   (
     audio_properties_infos: RemoteAudioPropertiesInfo[],
     audio_properties_info_number: number,
     total_remote_volume: number
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |audio_properties_infos |[RemoteAudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/docs-85535#remoteaudiopropertiesinfo)[] |Remote audio information, including stream IDs, stream information, and audio properties. |
   |audio_properties_info_number |number |Length of `audio_properties_infos`. You can ignore this parameter. |
   |total_remote_volume |number |Combined volume of all subscribed remote streams. The range is `[0, 255]`. |

### onEchoTestResult

Callback about the call test result.

* **Signature**

   ```ts
   (result: EchoTestResult) => void
   ```

* **Notes**

   The timing when this callback will be triggered is as follows:

   * A device\-related error occured during the test；

   * After a successful test；

   * After stopping the test, provided that the audio/video playback was not received during the test due to non\-device reasons.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |result |[EchoTestResult](https://docs.byteplus.com/en/docs/12/docs-85535#echotestresult) |* kTestSuccess    0:    Success<br><br>* kTestTimeout 1:    Abort after a 60 sec timeout<br><br>* kTestIntervalShort 2:    The next test must start 5 sec after the end of the previous test.<br><br>* kAudioDeviceError    3:    Error in audio capture<br><br>* kVideoDeviceError    4:    Error in video capture<br><br>* kAudioReceiveError    5:    Error in receiving audio<br><br>* kVideoReceiveError    6:    Error in receiving video<br><br>* kInternalError    7:    Unrecoverable error. |

### onVideoDeviceStateChanged

Callback of video device state. Video devices include cameras and screen sharing video capture devices.

* **Signature**

   ```ts
   (
     device_id: string,
     device_type: number,
     device_state: number,
     device_error: number
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |device_id |string |Device ID. |
   |device_type |number |Device type.<br><br><br>* `-1`: Unknown.<br><br>* `0`: Video rendering device.<br><br>* `1`: Video capture device.<br><br>* `2`: Screen recorder. |
   |device_state |number |Device state.<br><br><br>* `1`: On<br><br>* `2`: Off<br><br>* `3`: Runtime error, for example, when the media device is expected to be working but no data is received.<br><br>* `4`: Device paused. Including:<br><br>* During screen capturing, the target application window is minimized in the taskbar.<br><br>* Before or during screen capturing, the target application window is hidden.<br><br>* During screen capturing, the target application window is being stretched.<br><br>* During screen capturing, the target application window is being dragged.<br><br>* `5`: Resumed.<br><br>* `10`: Added.<br><br>* `11`: Removed.<br><br>* `12`: Closing the laptop interrupted the RTC call. RTC call will resume once the laptop is opened.<br><br>* `13`: RTC call resumed from the interruption caused by Closing the laptop.<br><br>* `14`: The device just became the default device.<br><br>* `15`: The device is no longer the default device.<br><br>* `16`: Notification of receiving the device list after time\-out. Call enumerate\-device api to update the device list when you get this notification. |
   |device_error |number |Device error<br><br><br>* `0`: Media equipment is normal.<br><br>* `1`: No permission to start media device<br><br>* `2`: Media devices are already in use<br><br>* `3`: Media device error<br><br>* `4`: The specified media device was not found.<br><br>* `5`: Media device, window or monitor removed.<br><br>* `6`: Device has no data callback.<br><br>* `7`: Device sample rate not supported. |

### onAudioDeviceStateChanged

Callback for audio device state changes. Audio devices include capture and playback devices.

* **Signature**

   ```ts
   (
     device_id: string,
     device_type: number,
     device_state: number,
     device_error: number
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |device_id |string |Device ID. |
   |device_type |number |Device type.<br><br><br>* `-1`: Unknown device.<br><br>* `0`: Audio playback device.<br><br>* `1`: Audio capture device.<br><br>* `2`: Screen audio capture device. |
   |device_state |number |Device state.<br><br><br>* `1`: Started.<br><br>* `2`: Stopped.<br><br>* `3`: Runtime error.<br><br>* `4`: Paused.<br><br>* `5`: Resumed.<br><br>* `10`: Added.<br><br>* `11`: Removed.<br><br>* `12`: The RTC call was interrupted when the laptop lid was closed.<br><br>* `13`: The RTC call resumed after the laptop lid was opened.<br><br>* `14`: The device became the system default.<br><br>* `15`: The device is no longer the system default. |
   |device_error |number |Device error.<br><br><br>* `0`: The device is operating normally.<br><br>* `1`: Permission to start the device was not granted.<br><br>* `2`: The device is already in use.<br><br>* `3`: Device error.<br><br>* `4`: The specified device was not found.<br><br>* `5`: The device was removed.<br><br>* `6`: The device produced no data callback.<br><br>* `7`: The device sample rate is not supported. |

### onAudioPlaybackDeviceTestVolume

Notification on the playing volume during the test for the local audio devices.

* **Signature**

   ```ts
   (volume: number) => void
   ```

* **Notes**

   Start an audio\-device test by calling [startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudioplaybackdevicetest) will register this callback for regular notification on playing volume. You can set the time interval between each callback by passing a proper value when calling the API above.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |volume |number |Playing volume during the test for the local audio devices. The range is `[0, 255]`. |

### onLocalSnapshotTakenToFile

Triggered after calling [takeLocalSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-takelocalsnapshottofile) to report whether the snapshot is taken successfully and provide details of the snapshot image.

* **Signature**

   ```ts
   (
     file_path: string,
     width: number,
     height: number,
     error_code: number,
     task_id: number
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |file_path |string |The path where the snapshot file is saved. |
   |width |number |The width (px) of the snapshot image. |
   |height |number |The height (px) of the snapshot image. |
   |error_code |number |The error code for the snapshot task. See `SnapshotErrorCode` for specific indications. |
   |task_id |number |The index of the snapshot task, which matches the return value of [takeLocalSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-takelocalsnapshottofile). |

### onRemoteSnapshotTakenToFile

Triggered after calling [takeRemoteSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-takeremotesnapshottofile) to report whether the snapshot is taken successfully and provide details of the snapshot image.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     file_path: string,
     width: number,
     height: number,
     error_code: number,
     task_id: number
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |ID of the snapshotted video stream. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Information of the snapshotted video stream. |
   |file_path |string |The path where the snapshot file is saved. |
   |width |number |The width (px) of the snapshot image. |
   |height |number |The height (px) of the snapshot image. |
   |error_code |number |The error code for the snapshot task. See `SnapshotErrorCode` for specific indications. |
   |task_id |number |The index of the snapshot task, which matches the return value of [takeRemoteSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-takeremotesnapshottofile). |

### onRemoteUserAudioFrame

Returns the audio data of one remote user.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     audio_frame: IAudioFrame
   ) => void
   ```

* **Notes**

   This callback works on the playback thread. Don't do anything time\-consuming in this callback, or it may affect the entire audio playback chain.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Remote stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Remote stream information. |
   |audio_frame |[IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85535#iaudioframe) |Audio data. |

### onRecordScreenAudioFrame

Returns the audio data played locally.

* **Signature**

   ```ts
   (audio_frame: IAudioFrame) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |audio_frame |[IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85535#iaudioframe) |Audio data. |

### onCaptureMixedAudioFrame

Returns audio data recorded by microphone and the audio mixing data from MediaPlayer, KTVPlayer, EffectPlayer.

* **Signature**

   ```ts
   (audio_frame: IAudioFrame) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |audio_frame |[IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85535#iaudioframe) |Audio data. |

### onAudioDeviceWarning

Audio device warning callback. The audio devices include audio capture devices and audio rendering devices.

* **Signature**

   ```ts
   (
     device_id: string,
     device_type: RTCAudioDeviceType,
     device_warning: MediaDeviceWarning
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |device_id |string |Device ID. |
   |device_type |[RTCAudioDeviceType](https://docs.byteplus.com/en/docs/12/docs-85535#rtcaudiodevicetype) |Device type. |
   |device_warning |[MediaDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-85535#mediadevicewarning) |Device error type. |

### onVideoDeviceWarning

Video device warning callback. The video devices include video capture devices.

* **Signature**

   ```ts
   (
     device_id: string,
     device_type: RTCAudioDeviceType,
     device_warning: MediaDeviceWarning
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |device_id |string |Device ID. |
   |device_type |[RTCAudioDeviceType](https://docs.byteplus.com/en/docs/12/docs-85535#rtcaudiodevicetype) |Device type. |
   |device_warning |[MediaDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-85535#mediadevicewarning) |Device error type. |

### onSEIStreamUpdate

Callback about publishing status of the black frame video stream.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     type: SEIStreamEventType
   ) => void
   ```

* **Notes**

   * In a voice call scenario, when the local user calls [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-sendseimessage) to send SEI data with a black frame, the sending status of the stream is notified to the remote user through this callback.

   * You can tell from this callback that the video frame carrying SEI data is a black frame and thus not render that video frame.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Remote stream information. |
   |type |[SEIStreamEventType](https://docs.byteplus.com/en/docs/12/docs-85535#seistreameventtype) |State of the black frame video stream. |

## RTCROOMCALLBACK

Type: `interface`

* **Callbacks**

|Callback |Description |
|---|---|
|[onUserVisibilityChanged](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onuservisibilitychanged) |Callback for user to set user visibility by calling [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setuservisibility). |
|[onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onvideopublishstatechanged) |Callback on video\-stream state changes. |
|[onAudioPublishStateChanged](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onaudiopublishstatechanged) |Callback on audio\-stream state changes. |
|[onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onvideosubscribestatechanged) |Callback on state changes of the subscription to video streams. |
|[onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onaudiosubscribestatechanged) |Callback on state changes of the subscription to audio streams. |
|[onLeaveRoom](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onleaveroom) |After leaving the room successfully, receives the callback. |
|[onUserJoined](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onuserjoined) |You will receive this callback in the following cases:<br><br><br>* A remote user joins your room as a visible user.<br><br>* A visible remote user reconnects to your room after a network interruption.<br><br>* An invisible remote user in your room calls [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setuservisibility) and becomes visible.<br><br>* You join a room that already contains visible users. |
|[onUserLeave](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onuserleave) |This callback is triggered when a remote user leaves the room or becomes invisible. |
|[onTokenWillExpire](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-ontokenwillexpire) |You will be informed 30 sec before the expiration via this callback. |
|[onAVSyncStateChange](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onavsyncstatechange) |Stream publisher will receive this callback when the A/V synchronization state changes after [setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setmultideviceavsync) is called. |
|[onRoomStats](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onroomstats) |In\-room call statistics callback.<br><br>After the user enters the room and starts the call, he receives this callback every 2s. |
|[onLocalStreamStats](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onlocalstreamstats) |After the stream is successfully published, you receive this callback every 2s to understand the network quality information of the published stream during this cycle. |
|[onRemoteStreamStats](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onremotestreamstats) |Receive this callback every 2s to learn the network quality information of the stream published by the subscribed remote user during this cycle. |
|[onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onuserpublishstreamvideo) |Callback on remote camera\-video streams in the room. |
|[onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onuserpublishstreamaudio) |Callback on remote microphone\-audio streams in the room. |
|[onAVSyncEvent](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onavsyncevent) |Stream publisher will receive this callback when the A/V synchronization error occurs after [setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setmultideviceavsync) is called. |
|[onVideoStreamBanned](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onvideostreambanned) |All users in the room are notified when video stream sending for a user is disabled or re\-enabled by calling BanUserStream/UnbanUserStream on the server. |
|[onAudioStreamBanned](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onaudiostreambanned) |All users in the room are notified when audio stream sending for a user is disabled or re\-enabled by calling BanUserStream/UnbanUserStream on the server. |
|[onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onroommessagereceived) |Receives a callback for broadcast messages in the room. |
|[onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onroombinarymessagereceived) |Receives a callback to a binary broadcast message in the room. |
|[onUserMessageReceived](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onusermessagereceived) |Receive this callback when you receive a text message (P2P) from another user in the room. |
|[onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onuserbinarymessagereceived) |A single user receives a callback (P2P) of binary messages from other specified users in the same room. |
|[onUserMessageSendResult](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onusermessagesendresult) |After sending a text or binary message (P2P) to a single user in the room, the message sender receives a callback with the result of the message. |
|[onRoomMessageSendResult](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onroommessagesendresult) |You receive this callback with the result of calling [sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-sendroommessage) or [sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-sendroombinarymessage). |
|[onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onforwardstreamstatechanged) |Callback returning the state and errors during relaying the audio stream to each of the rooms. |
|[onForwardStreamEvent](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onforwardstreamevent) |Callback returning the events during relaying the audio stream to each room. |
|[onNetworkQuality](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onnetworkquality) |Report the network quality of the users every 2s after the local user joins the room. |
|[onPublishPrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onpublishprivilegetokenwillexpire) |Callback triggered 30s before the publishing privilege of the Token expires. |
|[onSubscribePrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onsubscribeprivilegetokenwillexpire) |Callback triggered 30s before the subscribing privilege of the Token expires. |
|[onSetRoomExtraInfoResult](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onsetroomextrainforesult) |Callback on the result of calling [setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setroomextrainfo) to set extra information about the room. |
|[onRoomExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onroomextrainfoupdate) |Callback used to receive the extra information set by the other users in the same room with [setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setroomextrainfo). |
|[onRoomStreamExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/14197#rtcroomcallback-onroomstreamextrainfoupdate) |Callback used to receive the extra information set by other users in the same room with [setStreamExtraInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setstreamextrainfo). |

### onUserVisibilityChanged

Callback for user to set user visibility by calling [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setuservisibility).

* **Signature**

   ```ts
   (
     current_user_visibility: boolean,
     error_code: UserVisibilityChangeError
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |current_user_visibility |boolean |Visibility of the current user.<br><br><br>* true: Visible. The user can publish media streams. The other users in the room get informed of the behaviors of the user, such as joining room, starting video capture, and leaving room.<br><br>* false: Invisible. The user cannot publish media streams. The other users in the room do not get informed of the behaviors of the user, such as joining room, starting video capture, or leaving room. |
   |error_code |[UserVisibilityChangeError](https://docs.byteplus.com/en/docs/12/docs-85534#uservisibilitychangeerror) |Error code for setting user visibility. |

### onVideoPublishStateChanged

Callback on video\-stream state changes.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     state: number,
     reason: number
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Stream information. |
   |state |number |State code. See `PublishState` for more. |
   |reason |number |See `PublishStateChangeReason` for more. |

### onAudioPublishStateChanged

Callback on audio\-stream state changes.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     state: number,
     reason: number
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Stream information. |
   |state |number |State code. See `PublishState` for more. |
   |reason |number |See `PublishStateChangeReason` for more. |

### onVideoSubscribeStateChanged

Callback on state changes of the subscription to video streams.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     state: number,
     reason: number
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Stream information. |
   |state |number |State code. See `SubscribeState` for more. |
   |reason |number |See `SubscribeStateChangeReason` for more. |

### onAudioSubscribeStateChanged

Callback on state changes of the subscription to audio streams.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     state: number,
     reason: number
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Stream information. |
   |state |number |State code. See `SubscribeState` for more. |
   |reason |number |The reason why room state changes. See `SubscribeStateChangeReason` for more. |

### onLeaveRoom

After leaving the room successfully, receives the callback.

* **Signature**

   ```ts
   (stats: RtcRoomStats) => void
   ```

* **Notes**

   * When the user calls the [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-leaveroom), the SDK will stop all publishing subscription streams and release all call\-related media resources. After that, the user receives this callback.

   * If calling [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-leaveroom) and then [destroy](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-destroy) immediately after, the user will not receive this callback.

   * If the app needs to use the media resources of the device for purposes other than RTC, you should init the resources after receiving this callback. Receiving this callback ensures that the resources are not occupied by RTC SDK.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stats |[RtcRoomStats](https://docs.byteplus.com/en/docs/12/docs-85535#rtcroomstats) |Statistics for this call. |

### onUserJoined

You will receive this callback in the following cases:

* A remote user joins your room as a visible user.

* A visible remote user reconnects to your room after a network interruption.

* An invisible remote user in your room calls [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setuservisibility) and becomes visible.

* You join a room that already contains visible users.

* **Signature**

   ```ts
   (user_info: UserInfo) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |user_info |[UserInfo](https://docs.byteplus.com/en/docs/12/docs-85535#userinfo) |User ID. |

### onUserLeave

This callback is triggered when a remote user leaves the room or becomes invisible.

* **Signature**

   ```ts
   (
     uid: string,
     reason: UserOfflineReasonType
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |uid |string |ID of the user who leaves the room, or switches to invisible. |
   |reason |[UserOfflineReasonType](https://docs.byteplus.com/en/docs/12/docs-85535#userofflinereasontype) |Reason to leave the room. |

### onTokenWillExpire

You will be informed 30 sec before the expiration via this callback.

* **Signature**

   ```ts
   () => void
   ```

* **Notes**

   Call [updateToken](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updatetoken) to renew the Token. If the Token expired, the user would be removed from the room and not be able to continue the call.

### onAVSyncStateChange

Stream publisher will receive this callback when the A/V synchronization state changes after [setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setmultideviceavsync) is called.

* **Signature**

   ```ts
   (state: AVSyncState) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |state |[AVSyncState](https://docs.byteplus.com/en/docs/12/docs-85535#avsyncstate) |A/V synchronization state. |

### onRoomStats

In\-room call statistics callback.

After the user enters the room and starts the call, he receives this callback every 2s.

* **Signature**

   ```ts
   (stats: RtcRoomStats) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stats |[RtcRoomStats](https://docs.byteplus.com/en/docs/12/docs-85535#rtcroomstats) |Current RtcEngine statistics. |

### onLocalStreamStats

After the published stream is successful, you receive this callback every 2s to understand the network quality information of the published stream during this cycle.

* **Signature**

   ```ts
   (stats: LocalStreamStats) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stats |[LocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-85535#localstreamstats) |Current RtcEngine statistics. |

### onRemoteStreamStats

Receive this callback every 2s to learn the network quality information of the stream published by the subscribed remote user during this cycle.

* **Signature**

   ```ts
   (stats: RemoteStreamStats) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stats |[RemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-85535#remotestreamstats) |Current RtcEngine statistics. |

### onUserPublishStreamVideo

Callback on remote camera\-video streams in the room.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     is_publish: boolean
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Stream information. |
   |is_publish |boolean |Whether the stream is published.<br><br><br>* `true`: Published<br><br>* `false`: Removed. |

### onUserPublishStreamAudio

Callback on remote microphone\-audio streams in the room.

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     is_publish: boolean
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Stream information. |
   |is_publish |boolean |Whether the stream is published.<br><br><br>* `true`: Published<br><br>* `false`: Removed. |

### onAVSyncEvent

Stream publisher will receive this callback when the A/V synchronization error occurs after [setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setmultideviceavsync) is called.

* **Signature**

   ```ts
   (
     room_id: string,
     uid: string,
     av_sync_event: number
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |room_id |string |Room ID. |
   |uid |string |User ID. |
   |av_sync_event |number |A/V synchronization error. See [AVSyncEvent](https://docs.byteplus.com/en/docs/12/docs-85535#avsyncevent). |

### onVideoStreamBanned

All users in the room are notified when video stream sending for a user is disabled or re\-enabled by calling BanUserStream/UnbanUserStream on the server.

* **Signature**

   ```ts
   (
     uid: string,
     banned: boolean
   ) => void
   ```

* **Notes**

   * When the specified user in the room is disabled/unbanned Video stream sending, all users in the room will receive the callback.

   * If the banned user leaves or disconnects and then rejoins the room, the user is still banned from publishing audio stream, and all users in the room will be informed via the callback.

   * After the specified user is banned, other users in the room will check out and enter the room again, and will receive the callback again.

   * If the conference mode is enabled in the console, only the user whose stream is banned will receive this callback.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |uid |string |User ID of the video stream that was disabled/unbanned. |
   |banned |boolean |Video stream sending status<br><br><br>* true: Video stream sending was disabled<br><br>* false: Video stream sending was unbanned. |

### onAudioStreamBanned

All users in the room are notified when audio stream sending for a user is disabled or re\-enabled by calling BanUserStream/UnbanUserStream on the server.

* **Signature**

   ```ts
   (
     uid: string,
     banned: boolean
   ) => void
   ```

* **Notes**

   * All users in the room will receive this callback when audio stream sending for a specified user is disabled or re\-enabled.

   * If the banned user leaves and then re\-enters the room, the user will still be in the banned status, and everyone in the room will receive the callback again.

   * If the banned user is disconnected and reconnected to the room, it will still be banned status, and only the person will receive the callback again.

   * After the specified user is banned, other users in the room will check out and enter the room again, and will receive the callback again.

   * The same room is created again after dissolution, and the state in the room is empty.

   * If the conference mode is enabled in the console, only the user whose stream is banned will receive this callback.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |uid |string |Disabled/unbanned audio stream user ID. |
   |banned |boolean |Audio stream sending status<br><br><br>* true: audio stream sending is disabled<br><br>* false: audio stream sending is unbanned. |

### onRoomMessageReceived

Receives a callback for broadcast messages in the room.

* **Signature**

   ```ts
   (
     uid: string,
     message: string
   ) => void
   ```

* **Notes**

   When other users in the same room call [sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-sendroommessage) to send a text broadcast message, you receive this callback.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |uid |string |Message sender ID. |
   |message |string |Received message content. |

### onRoomBinaryMessageReceived

Receives a callback to a binary broadcast message in the room.

* **Signature**

   ```ts
   (
     uid: string,
     message: Buffer
   ) => void
   ```

* **Notes**

   When other users in the same room call [sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-sendroombinarymessage) to send a binary broadcast message, you receive this callback.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |uid |string |Message sender ID. |
   |message |Buffer |Binary message content received. |

### onUserMessageReceived

Receive this callback when you receive a text message (P2P) from another user in the room.

* **Signature**

   ```ts
   (
     uid: string,
     message: string
   ) => void
   ```

* **Notes**

   When another user in the same room calls [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-sendusermessage) to send a P2P text message to you, you receive this callback.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |uid |string |Message sender ID. |
   |message |string |The content of the received text message. |

### onUserBinaryMessageReceived

A single user receives a callback (P2P) of binary messages from other uid\-owned users in the same room.

* **Signature**

   ```ts
   (
     uid: string,
     message: Buffer
   ) => void
   ```

* **Notes**

   When other users in the same room call [sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-senduserbinarymessage) to send binary messages to local users, local users will receive the callback.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |uid |string |Message sender ID. |
   |message |Buffer |The content of the received binary message. |

### onUserMessageSendResult

After sending a text or binary message (P2P) to a single user in the room, the message sender receives a callback with the result of the message.

* **Signature**

   ```ts
   (
     msgid: number,
     error: number
   ) => void
   ```

* **Notes**

   You must first call the [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-sendusermessage) or [sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-senduserbinarymessage) interface to receive this callback.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |msgid |number |The ID of this message. |
   |error |number |Message sending result. `0` indicates success. See `MessageSendResultCode`. |

### onRoomMessageSendResult

You receive this callback with the result of calling [sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-sendroommessage) or [sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-sendroombinarymessage).

* **Signature**

   ```ts
   (
     msgid: number,
     error: number
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |msgid |number |ID of this message. |
   |error |number |Message sending result. `200` indicates success. See `MessageSendResultCode`. |

### onForwardStreamStateChanged

Callback returning the state and errors during relaying the audio stream to each of the rooms.

* **Signature**

   ```ts
   (
     infos: ForwardStreamStateInfo[],
     info_count: number
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |infos |[ForwardStreamStateInfo](https://docs.byteplus.com/en/docs/12/docs-85535#forwardstreamstateinfo)[] |Array of the state and errors of each designated room. |
   |info_count |number |Count. |

### onForwardStreamEvent

Callback returning the events during relaying the audio stream to each room.

* **Signature**

   ```ts
   (
     infos: ForwardStreamEventInfo[],
     info_count: number
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |infos |[ForwardStreamEventInfo](https://docs.byteplus.com/en/docs/12/docs-85535#forwardstreameventinfo)[] |Array of the event of each designated room. |
   |info_count |number |Count. |

### onNetworkQuality

Report the network quality of the users every 2s after the local user joins the room.

* **Signature**

   ```ts
   (
     localQuality: NetworkQualityStats,
     remoteQualities: NetworkQualityStats[]
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |localQuality |[NetworkQualityStats](https://docs.byteplus.com/en/docs/12/docs-85535#networkqualitystats) |Local network quality. |
   |remoteQualities |[NetworkQualityStats](https://docs.byteplus.com/en/docs/12/docs-85535#networkqualitystats)[] |Network quality of the subscribed users. |

### onPublishPrivilegeTokenWillExpire

Callback triggered 30s before the publishing privilege of the Token expires.

* **Signature**

   ```ts
   () => void
   ```

* **Notes**

   After receiving this callback, you must call [updateToken](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updatetoken) to update the publishing privilege Token.After a user's publishing privilege expires:

   * When attempting to publish a stream, the user will receive the corresponding publish\-state callback, such as [onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onvideopublishstatechanged) or [onAudioPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onaudiopublishstatechanged), indicating no permission to publish streams.

   * The published streams of the user will be removed, and the publisher will receive the corresponding publish\-state callback. Remote users in the room will receive [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserpublishstreamvideo) / [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserpublishstreamaudio) with `is_publish` set to `false`.

### onSubscribePrivilegeTokenWillExpire

Callback triggered 30s before the subscribing privilege of the Token expires.

* **Signature**

   ```ts
   () => void
   ```

* **Notes**

   After receiving this callback, you must call [updateToken](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updatetoken) to update the subscribing privilege Token. After a user's subscribing privilege expires, the user will fail to subscribe to new streams, or the subscribed streams will be removed, and he/she will receive the corresponding subscribe\-state callback, such as [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onvideosubscribestatechanged) or [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onaudiosubscribestatechanged), indicating no permission to subscribe to streams.

### onSetRoomExtraInfoResult

Callback on the result of calling [setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setroomextrainfo) to set extra information about the room.

* **Signature**

   ```ts
   (
     task_id: number,
     error_code: SetRoomExtraInfoResult
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |task_id |number |The task ID of the API call. |
   |error_code |[SetRoomExtraInfoResult](https://docs.byteplus.com/en/docs/12/docs-85535#setroomextrainforesult) |Setting results and reasons. |

### onRoomExtraInfoUpdate

Callback used to receive the extra information set by the other users in the same room with [setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setroomextrainfo).

* **Signature**

   ```ts
   (
     key: string,
     value: string,
     last_update_user_id: string,
     last_update_time_ms: number
   ) => void
   ```

* **Notes**

   A user joining the room receives all room extra information that was set before they joined.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |key |string |Key of the extra information. |
   |value |string |Content of the extra information. |
   |last_update_user_id |string |The ID of the last user who updated this information. |
   |last_update_time_ms |number |The Unix time in ms when this information was last updated. |

### onRoomStreamExtraInfoUpdate

Callback used to receive the extra information set by other users in the same room with [setStreamExtraInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setstreamextrainfo).

* **Signature**

   ```ts
   (
     stream_id: string,
     stream_info: StreamInfo,
     extra_info: string
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Stream ID. |
   |stream_info |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) |Stream information. |
   |extra_info |string |Content of the extra information of the stream. |

## RTCAUDIOEFFECTPLAYERCALLBACK

Type: `interface`

* **Callbacks**

|Callback |Description |
|---|---|
|[onAudioEffectPlayerStateChanged](https://docs.byteplus.com/en/docs/12/14197#rtcaudioeffectplayercallback-onaudioeffectplayerstatechanged) |Callback for audio mixing status change. |

### onAudioEffectPlayerStateChanged

Callback for audio mixing status change.

* **Signature**

   ```ts
   (
     effect_id: number,
     state: PlayerState,
     error: PlayerError
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |effect_id |number |The ID of veRTCAudioEffectPlayer. Set by [getAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getaudioeffectplayer). |
   |state |[PlayerState](https://docs.byteplus.com/en/docs/12/docs-85535#playerstate) |Player state. |
   |error |[PlayerError](https://docs.byteplus.com/en/docs/12/docs-85534#playererror) |Player error code. |

## RTCMediaPlayerCALLBACK

Type: `interface`

* **Callbacks**

|Callback |Description |
|---|---|
|[onMediaPlayerStateChanged](https://docs.byteplus.com/en/docs/12/14197#rtcmediaplayercallback-onmediaplayerstatechanged) |Callback for audio mixing status change. |
|[onMediaPlayerEvent](https://docs.byteplus.com/en/docs/12/14197#rtcmediaplayercallback-onmediaplayerevent) |Callback for media player events. |
|[onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/14197#rtcmediaplayercallback-onmediaplayerplayingprogress) |Periodic callback for playing progress. The period is set by `MediaPlayerConfig.callback_on_progress_interval`. |

### onMediaPlayerStateChanged

Callback for audio mixing status change.

* **Signature**

   ```ts
   (
     player_id: number,
     state: PlayerState,
     error: PlayerError
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |player_id |number |The ID of veRTCMediaPlayer. Set by [getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getmediaplayer). |
   |state |[PlayerState](https://docs.byteplus.com/en/docs/12/docs-85535#playerstate) |Player state. |
   |error |[PlayerError](https://docs.byteplus.com/en/docs/12/docs-85534#playererror) |Player error code. |

### onMediaPlayerEvent

Callback for media player events.

* **Signature**

   ```ts
   (
     player_id: number,
     event: number,
     message: string
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |player_id |number |The ID of veRTCMediaPlayer. Set by [getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getmediaplayer). |
   |event |number |Player event. See `PlayerEvent`. |
   |message |string |Additional event message, which may be empty. |

### onMediaPlayerPlayingProgress

Periodic callback for playing progress. The period is set by `MediaPlayerConfig.callback_on_progress_interval`.

* **Signature**

   ```ts
   (
     player_id: number,
     progress: string
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |player_id |number |The ID of veRTCMediaPlayer. Set by [getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getmediaplayer). |
   |progress |string |Mixing progress in ms. |

## RTCWTNSTREAMCALLBACK

Type: `interface`

WTN stream event callbacks.

* **Callbacks**

|Callback |Description |
|---|---|
|[onWTNVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/14197#rtcwtnstreamcallback-onwtnvideosubscribestatechanged) |Callback for WTN video subscription state changes. |
|[onWTNAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/14197#rtcwtnstreamcallback-onwtnaudiosubscribestatechanged) |Callback for WTN audio subscription state changes. |
|[onWTNFirstRemoteAudioFrame](https://docs.byteplus.com/en/docs/12/14197#rtcwtnstreamcallback-onwtnfirstremoteaudioframe) |Callback when the first remote WTN audio frame is decoded successfully. |
|[onWTNFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/14197#rtcwtnstreamcallback-onwtnfirstremotevideoframedecoded) |Callback when the first remote WTN video frame is decoded successfully. |
|[onWTNSEIMessageReceived](https://docs.byteplus.com/en/docs/12/14197#rtcwtnstreamcallback-onwtnseimessagereceived) |Callback for SEI messages carried in a WTN stream. |
|[onWTNDataMessageReceived](https://docs.byteplus.com/en/docs/12/14197#rtcwtnstreamcallback-onwtndatamessagereceived) |Callback for data messages carried in a WTN stream. |
|[onWTNVideoFrame](https://docs.byteplus.com/en/docs/12/14197#rtcwtnstreamcallback-onwtnvideoframe) |Callback for custom\-rendered WTN video frames. |

### onWTNVideoSubscribeStateChanged

Callback for WTN video subscription state changes.

* **Signature**

   ```ts
   (
     stream_id: string,
     state_code: WTNSubscribeState,
     reason: WTNSubscribeStateChangeReason
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |WTN video stream ID. |
   |state_code |[WTNSubscribeState](https://docs.byteplus.com/en/docs/12/docs-85535#wtnsubscribestate) |Subscription state. |
   |reason |[WTNSubscribeStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-85535#wtnsubscribestatechangereason) |Reason for the state change. |

### onWTNAudioSubscribeStateChanged

Callback for WTN audio subscription state changes.

* **Signature**

   ```ts
   (
     stream_id: string,
     state_code: WTNSubscribeState,
     reason: WTNSubscribeStateChangeReason
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |WTN audio stream ID. |
   |state_code |[WTNSubscribeState](https://docs.byteplus.com/en/docs/12/docs-85535#wtnsubscribestate) |Subscription state. |
   |reason |[WTNSubscribeStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-85535#wtnsubscribestatechangereason) |Reason for the state change. |

### onWTNFirstRemoteAudioFrame

Callback when the first remote WTN audio frame is decoded successfully.

* **Signature**

   ```ts
   (stream_id: string) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |WTN stream ID. |

### onWTNFirstRemoteVideoFrameDecoded

Callback when the first remote WTN video frame is decoded successfully.

* **Signature**

   ```ts
   (
     stream_id: string,
     info: VideoFrameInfo
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |WTN stream ID. |
   |info |[VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-85535#videoframeinfo) |Video frame information. |

### onWTNSEIMessageReceived

Callback for SEI messages carried in a WTN stream.

* **Signature**

   ```ts
   (
     stream_id: string,
     channel_id: number,
     message: Uint8Array,
     message_length: number
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |WTN stream ID. |
   |channel_id |number |SEI transmission channel ID in the range `[0, 255]`. |
   |message |Uint8Array |SEI payload inserted through the client API. |
   |message_length |number |Length of the SEI payload. |

### onWTNDataMessageReceived

Callback for data messages carried in a WTN stream.

* **Signature**

   ```ts
   (
     stream_id: string,
     message: Uint8Array,
     source_type: DataMessageSourceType
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |WTN stream ID. |
   |message |Uint8Array |Data payload, such as OpenAPI custom messages or volume indication data. |
   |source_type |[DataMessageSourceType](https://docs.byteplus.com/en/docs/12/docs-85535#datamessagesourcetype) |Data source type. |

### onWTNVideoFrame

Callback for custom\-rendered WTN video frames.

* **Signature**

   ```ts
   (frame: IVideoFrame) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |frame |[IVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85535#ivideoframe) |Video frame data. |
