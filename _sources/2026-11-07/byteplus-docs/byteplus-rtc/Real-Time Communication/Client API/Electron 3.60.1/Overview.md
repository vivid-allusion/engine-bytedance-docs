---
title: "Overview"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-85530"
---

## Engine Management

|Methods |Description |
|---|---|
|[createRTCEngine](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-creatertcengine) |Create an engine instance. |
|[setBusinessId](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setbusinessid) |Sets the business ID. |
|[feedback](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-feedback) |Report the user feedback to RTC. |
|[destroyRTCEngine](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-destroyrtcengine) |Destroy the engine instance created by [createRTCEngine](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-creatertcengine), and release all related resources. |

|Callbacks |Description |
|---|---|
|[onLogReport](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onlogreport) |Terminal monitoring log callback. The callback is triggered when a terminal monitoring event is generated. |
|[onWarning](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onwarning) |This callback informs you of a warning message. |
|[onError](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onerror) |This callback informs you of an error message. |
|[onSysStats](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onsysstats) |Periodically (2s) issue callbacks to report the current CPU and memory usage. |

## Room Management

|Methods |Description |
|---|---|
|[createRTCRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-creatertcroom) |Create a room for the call. |
|[getRoomId](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-getroomid) |Get room ID. |
|[setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setuservisibility) |Set the visibility of the user in the room. The local user is visible to others by default before calling this API. |
|[joinRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-joinroom) |Join the room. |
|[getCallId](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-getcallid) |Get Call ID.<br><br>This method needs to be called after joining a room. |
|[setLiveMode](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setlivemode) |Sets the live\-streaming mode for the room. |
|[setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setroomextrainfo) |Sets extra information about the room the local user joins. |
|[updateToken](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updatetoken) |Update Token. A Token contains the privilege of joining a room, publishing streams, and subscribing to streams. Each privilege has an expiration time. A callback will be triggered 30s before expiration, informing the user to update the Token. In this case, you need to get a new Token and update the Token with this API to ensure the normal call. |
|[leaveRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-leaveroom) |Leave RTC room. |
|[destroy](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-destroy) |Leave and destroy the room. |

|Callbacks |Description |
|---|---|
|[onRoomStreamExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onroomstreamextrainfoupdate) |Callback used to receive the extra information set by other users in the same room with [setStreamExtraInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setstreamextrainfo). |
|[onRoomStats](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onroomstats) |In\-room call statistics callback.<br><br>After the user enters the room and starts the call, he receives this callback every 2s. |
|[onUserJoined](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserjoined) |You will receive this callback in the following cases:<br><br><br>* A remote user joins your room as a visible user.<br><br>* A visible remote user reconnects to your room after a network interruption.<br><br>* An invisible remote user in your room calls [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setuservisibility) and becomes visible.<br><br>* You join a room that already contains visible users. |
|[onLeaveRoom](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onleaveroom) |You receive this callback after leaving the room successfully. |
|[onUserLeave](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserleave) |This callback is triggered when a remote user leaves the room or becomes invisible. |
|[onSetRoomExtraInfoResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onsetroomextrainforesult) |Callback on the result of calling [setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setroomextrainfo) to set extra information about the room. |
|[onRoomExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onroomextrainfoupdate) |Callback used to receive the extra information set by the other users in the same room with [setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setroomextrainfo). |
|[onUserVisibilityChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuservisibilitychanged) |Callback for user to set user visibility by calling [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setuservisibility). |
|[onTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-ontokenwillexpire) |You will be informed 30 sec before the expiration via this callback. |
|[onPublishPrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onpublishprivilegetokenwillexpire) |Callback triggered 30s before the publishing privilege of the Token expires. |
|[onSubscribePrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onsubscribeprivilegetokenwillexpire) |Callback triggered 30s before the subscribing privilege of the Token expires. |

## Audio Management

|Methods |Description |
|---|---|
|[enumerateAudioPlaybackDevices](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enumerateaudioplaybackdevices) |Get a list of the audio playback devices. When the audio playback device changes, you will receive the [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onaudiodevicestatechanged), and you need to call this API again to get the new device list. |
|[setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setaudioplaybackdevice) |Sets the audio playback device. |
|[getAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getaudioplaybackdevice) |Gets the current audio playback device ID. |
|[followSystemPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-followsystemplaybackdevice) |Set the audio playback device to follow the OS setting or not. |
|[enumerateAudioCaptureDevices](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enumerateaudiocapturedevices) |Get a list of audio acquisition devices in the current system. If there are subsequent device changes, you need to call this interface again to get a new device list. |
|[setAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setaudiocapturedevice) |Set up audio capture devices. |
|[getAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getaudiocapturedevice) |Gets the current audio capture device ID. |
|[followSystemCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-followsystemcapturedevice) |Set the audio capture device to follow the OS setting or not. |
|[setAudioProfile](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setaudioprofile) |Sets the sound quality. |
|[enableExternalSoundCard](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableexternalsoundcard) |Enable the audio process mode for external sound card. |
|[enableAGC](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableagc) |Enable or disable automatic gain control to adjust microphone pickup volume. |
|[enableVocalInstrumentBalance](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enablevocalinstrumentbalance) |Enables/disables the loudness equalization function. |
|[startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudiocapture) |Start internal audio capture. The default is off. |
|[muteAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-muteaudiocapture) |Set whether to mute the recording signal (without changing the local hardware). |
|[setCaptureVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setcapturevolume) |Adjust the audio capture volume. |
|[setAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setaudiocapturedevicevolume) |Set the current audio capture volume. |
|[getAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getaudiocapturedevicevolume) |Get the current audio capture volume. |
|[setAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setaudiocapturedevicemute) |Mute or Unmute the current audio capture device. The default state is speaking. |
|[getAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getaudiocapturedevicemute) |Get state of the audio capture device. |
|[stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopaudiocapture) |Stop internal audio capture. The default is off. |
|[setAudioPlaybackDeviceVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setaudioplaybackdevicevolume) |Set the current audio playback device volume. |
|[getAudioPlaybackDeviceVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getaudioplaybackdevicevolume) |Get the current audio playback device volume. |
|[setAudioPlaybackDeviceMute](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setaudioplaybackdevicemute) |Mute or Unmute the current audio playback device. The default state is speaking. |
|[getAudioPlaybackDeviceMute](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getaudioplaybackdevicemute) |Get state of the audio playback device. |
|[setScreenCaptureVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setscreencapturevolume) |Adjust the volume of the audio captured during screen sharing.<br><br>This only changes the volume property of the audio data, without affecting the microphone capture volume or the local device volume. |
|[setPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setplaybackvolume) |Adjust the playback volume of the mixed remote audio streams. You can call this API before or during the playback. |
|[setRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setremoteaudioplaybackvolume) |Adjust the audio playback volume of the remote user. |
|[setRemoteRoomAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setremoteroomaudioplaybackvolume) |Adjusts the audio playback volume from all the remote users in a room. |
|[enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableaudiopropertiesreport) |Enable audio information prompts. |
|[setAudioSelectionConfig](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setaudioselectionconfig) |Set the priority of the local audio stream to be published. |
|[initAudioPlaybackDeviceForTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-initaudioplaybackdevicefortest) |Try to initialize the audio playback device for device test. |
|[startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudioplaybackdevicetest) |Start the playback test for the local audio device. RTC will start playing the audio file specified. And RTC will notify the audio volume via the [onAudioPlaybackDeviceTestVolume](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onaudioplaybackdevicetestvolume) periodically. |
|[stopAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopaudioplaybackdevicetest) |Stop the playback test for the local audio device. |
|[initAudioCaptureDeviceForTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-initaudiocapturedevicefortest) |Try to initialize the audio capture device for device test. |
|[startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudiodevicerecordtest) |Start the capture and playback test for local audio devices. |
|[stopAudioDeviceRecordAndPlayTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopaudiodevicerecordandplaytest) |Call this API to stop recording in the test and start to play the recording in 30 s after calling [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudiodevicerecordtest). |
|[stopAudioDevicePlayTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopaudiodeviceplaytest) |Stop the capture and playback test for local audio devices which is started by calling [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudiodevicerecordtest).<br><br>Before the test ends by itself, you can call this API to stop the recording or playing. |
|[startHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-starthardwareechodetection) |Start echo detection before joining a room. |
|[stopHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stophardwareechodetection) |Stop the echo detection before joining a room. |

|Callbacks |Description |
|---|---|
|[onAudioDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onaudiodevicewarning) |Audio device warning callback. The audio devices include audio capture devices and audio rendering devices. |
|[onAudioStreamBanned](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onaudiostreambanned) |All users in the room are notified when audio stream sending for a user is disabled or re\-enabled by calling BanUserStream/UnbanUserStream on the server. |
|[onAudioDeviceVolumeChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onaudiodevicevolumechanged) |Callback to notify you the volume of the audio device has been changed or when the device has been muted or unmuted. No need to activate the notification beforehand. |
|[onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onaudiodevicestatechanged) |Callback for audio device state changes. Audio devices include capture and playback devices. |
|[onStreamSyncInfoReceived](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onstreamsyncinforeceived) |Audio stream synchronization information callback. You can use this callback to receive audio stream synchronization information sent remotely after the remote user calls [sendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-sendstreamsyncinfo) to send an audio stream synchronization message. |
|[onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onlocalaudiopropertiesreport) |After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableaudiopropertiesreport), you will periodically receive this callback for the information about local audio. |
|[onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onremoteaudiopropertiesreport) |After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableaudiopropertiesreport), you will periodically receive this callback with information about subscribed remote audio streams. |
|[onActiveSpeaker](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onactivespeaker) |After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableaudiopropertiesreport), you will periodically receive this callback for the active speaker information. |
|[onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onuserstartaudiocapture) |The remote clients in the room will be informed of the state change via this callback after the visible user starts audio capture by calling [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudiocapture). |
|[onUserStopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onuserstopaudiocapture) |The remote clients in the room will be informed of the state change via this callback after the visible user stops audio capture by calling [stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopaudiocapture). |
|[onAudioPlaybackDeviceTestVolume](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onaudioplaybackdevicetestvolume) |Notification on the playing volume during the test for the local audio devices. |
|[onHardwareEchoDetectionResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onhardwareechodetectionresult) |Callback that notifies you the result of the echo detection before a call. |

## Video Management

|Methods |Description |
|---|---|
|[enumerateVideoCaptureDevices](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enumeratevideocapturedevices) |Get a list of video capture devices in the current system. |
|[setVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvideocapturedevice) |Set the current video capture device. |
|[getVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getvideocapturedevice) |Get the video capture device information currently used by the SDK. |
|[setVideoCaptureConfig](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvideocaptureconfig) |Set the video capture parameters for internal capture of the RTC SDK. |
|[setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvideoencoderconfig) |Sets the expected maximum published video stream configuration. |
|[setupLocalVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setuplocalvideo) |Set the view for the local video. |
|[startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startvideocapture) |Enable internal video capture immediately. The default is off. |
|[setupRemoteVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setupremotevideo) |Bind the remote video stream to the view. |
|[requestRemoteVideoKeyFrame](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-requestremotevideokeyframe) |Requests a key video frame from a subscribed remote video stream. |
|[removeRemoteVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-removeremotevideo) |Unbind the remote video from the view. |
|[removeAllRemoteVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-removeallremotevideo) |Unbind all remote videos from the views. |
|[removeLocalVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-removelocalvideo) |Unbind the local video stream from its rendering view. |
|[stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopvideocapture) |Disable internal video capture immediately. The default is off. |

|Callbacks |Description |
|---|---|
|[onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onuserstartvideocapture) |The remote clients in the room will be informed of the state change via this callback after the visible user starts video capture by calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startvideocapture). |
|[onUserStopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onuserstopvideocapture) |The remote clients in the room will be informed of the state change via this callback after the visible user stops video capture by calling [stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopvideocapture). |
|[onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onvideodevicestatechanged) |Callback of video device state. Video devices include cameras and screen sharing video capture devices. |
|[onVideoDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onvideodevicewarning) |Video device warning callback. The video devices include video capture devices. |
|[onFirstLocalVideoFrameCaptured](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onfirstlocalvideoframecaptured) |RTC SDK receives this callback when the first video frame or screen video frame capture is completed locally. |
|[onLocalVideoStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onlocalvideostatechanged) |Receive this event when the state of the local video stream changes. |

## Audio & Video Transport

|Methods |Description |
|---|---|
|[setDummyCaptureImagePath](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setdummycaptureimagepath) |Set an alternative image when the local internal video capture is not enabled. You can repeatedly call this API to update the image. You can set the path to null or open the camera to stop publishing the image. |
|[publishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-publishstreamaudio) |Start or stop publishing media streams captured by the local microphone in the current room. |
|[publishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-publishstreamvideo) |Start or stop publishing video streams captured by camera in the current room. |
|[subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-subscribestreamaudio) |Subscribes to specific remote media streams captured by the remote microphone. Or update the subscribe options of the subscribed user. |
|[subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-subscribestreamvideo) |Subscribes to specific remote media streams captured by the remote camera. Or update the subscribe options of the subscribed user. |
|[subscribeAllStreamsAudio](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-subscribeallstreamsaudio) |Subscribes to all remote audio streams captured by microphone. |
|[unsubscribeAllStreamsAudio](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-unsubscribeallstreamsaudio) |Unsubscribes from all remote audio streams captured by microphone. |
|[subscribeAllStreamsVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-subscribeallstreamsvideo) |Subscribes to all remote video streams captured by camera. |
|[unsubscribeAllStreamsVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-unsubscribeallstreamsvideo) |Unsubscribes from all remote video streams captured by camera. |
|[setStreamExtraInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setstreamextrainfo) |Sets extra information for the currently published stream. |
|[setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setmultideviceavsync) |Synchronizes published audio and video. |
|[pauseAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-pauseallsubscribedstreamaudio) |Pause receiving remote audio streams. |
|[resumeAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-resumeallsubscribedstreamaudio) |Resume receiving remote audio streams. |
|[pauseAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-pauseallsubscribedstreamvideo) |Pause receiving remote video streams. |
|[resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-resumeallsubscribedstreamvideo) |Resume receiving remote video streams. |
|[startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-startforwardstreamtorooms) |Start relaying media stream across rooms. |
|[updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updateforwardstreamtorooms) |Update information of the rooms where you want to relay the media stream to. |
|[pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-pauseforwardstreamtoallrooms) |Pause relaying media streams to all rooms. |
|[resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-resumeforwardstreamtoallrooms) |Resume relaying media streams to all rooms. |
|[stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-stopforwardstreamtorooms) |Stop relaying media streams to all rooms. |

|Callbacks |Description |
|---|---|
|[onRemoteAudioStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onremoteaudiostatechanged) |When the state of the audio stream from the remote user you subscribe to changes, this callback will be received to understand the current state of the remote audio stream. |
|[onFirstLocalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onfirstlocalaudioframe) |Receive the callback when the first audio frame is locally collected. |
|[onFirstRemoteAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onfirstremoteaudioframe) |This callback informs you when the first frame of every remote audio is received. |
|[onAudioFrameSendStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onaudioframesendstatechanged) |Audio first frame sending status change callback. |
|[onVideoFrameSendStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onvideoframesendstatechanged) |Video first frame sending status change callback. |
|[onAudioFramePlayStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onaudioframeplaystatechanged) |Audio first frame playback state change callback. |
|[onVideoFramePlayStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onvideoframeplaystatechanged) |Video first frame playback state change callback. |
|[onLocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onlocalstreamstats) |After the published stream is successful, you receive this callback every 2s to understand the network quality information of the published stream during this cycle. |
|[onRemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onremotestreamstats) |Receive this callback every 2s to learn the network quality information of the stream published by the subscribed remote user during this cycle. |
|[onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onnetworkquality) |Report the network quality of the users every 2s after the local user joins the room. |
|[onLocalVideoSizeChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onlocalvideosizechanged) |Receive this callback when the local video size or rotation configuration changes. |
|[onRemoteVideoSizeChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onremotevideosizechanged) |Users in the room who subscribe to this video stream receive this callback when the remote video size or rotation configuration changes. |
|[onRemoteVideoStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onremotevideostatechanged) |When the state of a remote video stream changes, users in the room who subscribe to this stream receive the event. |
|[onFirstRemoteVideoFrameRendered](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onfirstremotevideoframerendered) |Receive this callback after the first frame of remote video stream is locally rendered by SDK. |
|[onVideoStreamBanned](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onvideostreambanned) |All users in the room are notified when video stream sending for a user is disabled or re\-enabled by calling BanUserStream/UnbanUserStream on the server. |
|[onFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onfirstremotevideoframedecoded) |Receive this callback after the first frame of remote video stream is received and decoded by SDK. |
|[onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onforwardstreamstatechanged) |Callback returning the state and errors during relaying the audio stream to each of the rooms. |
|[onForwardStreamEvent](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onforwardstreamevent) |Callback returning the events during relaying the audio stream to each room. |
|[onAVSyncStateChange](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onavsyncstatechange) |Stream publisher will receive this callback when the A/V synchronization state changes after [setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setmultideviceavsync) is called. |

## Video Processing

|Methods |Description |
|---|---|
|[setLocalVideoMirrorType](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setlocalvideomirrortype) |Sets the mirror mode for the captured video stream. |
|[setVideoCaptureRotation](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvideocapturerotation) |Set the rotation of the local video images. Call this API to rotate the videos when the camera is fixed upside down or tilted. |
|[setLowLightAdjusted](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setlowlightadjusted) |Sets the low\-light video enhancement mode. Enable this feature in low\-light, unevenly lit, or backlit environments to improve video quality. |
|[setVideoWatermark](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvideowatermark) |Adds watermark to the local video stream. |
|[clearVideoWatermark](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-clearvideowatermark) |Removes video watermark from the local video stream. |
|[enableEffectBeauty](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableeffectbeauty) |Enables/Disables basic beauty effects. |
|[setBeautyIntensity](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setbeautyintensity) |Sets the beauty effect intensity. |
|[initCVResource](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-initcvresource) |Video effects license check. |
|[getAuthMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getauthmessage) |Get authorization messages from the Effect SDK to obtain online licenses. |
|[enableVideoEffect](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enablevideoeffect) |Enables video effects including beauty and color filters. |
|[setEffectNodes](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-seteffectnodes) |Set video effects material package. |
|[updateEffectNode](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-updateeffectnode) |Set the effect intensity. |
|[setColorFilter](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setcolorfilter) |Set the color filter. |
|[setColorFilterIntensity](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setcolorfilterintensity) |Set the intensity of the color filter enabled. |
|[disableVideoEffect](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-disablevideoeffect) |Disables video effects. |
|[enableVirtualBackground](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enablevirtualbackground) |Set the original background to a specified image or a solid color. To disable this effect, set the modelPath parameter to null. |
|[disableVirtualBackground](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-disablevirtualbackground) |Turns off the virtual background. |
|[enableFaceDetection](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enablefacedetection) |Starts face detection and registers the observer for the result. |
|[disableFaceDetection](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-disablefacedetection) |Stops face detection. |
|[setVideoDigitalZoomConfig](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvideodigitalzoomconfig) |Set the step size for each digital zooming control to the local videos. |
|[setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvideodigitalzoomcontrol) |Digital zoom or move the local video image once. This action affects both the video preview locally and the stream published. |
|[startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startvideodigitalzoomcontrol) |Continuous and repeatedly digital zoom control. This action affects both the video preview locally and the stream published. |
|[stopVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopvideodigitalzoomcontrol) |Stop the ongoing digital zoom control instantly. |

|Callbacks |Description |
|---|---|
|[onFaceDetectResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onfacedetectresult) |Callback of the result of face detection with Effect SDK.<br><br>After calling [enableFaceDetection](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enablefacedetection) and using the Effect SDK integrated in the RTC SDK, you will receive this callback. |

## Audio Processing

|Methods |Description |
|---|---|
|[setVoiceChangerType](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvoicechangertype) |Set the sound effect type. |
|[setVoiceReverbType](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvoicereverbtype) |Set the reverb effect type. |
|[setLocalVoicePitch](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setlocalvoicepitch) |Change local voice to a different key, mostly used in Karaoke scenarios. You can adjust the pitch of local voice such as ascending or descending with this method. |
|[setLocalVoiceReverbParam](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setlocalvoicereverbparam) |Set the equalization effect for the local captured audio. The audio includes both internal captured audio and external captured voice, but not the mixing audio file. |
|[enableLocalVoiceReverb](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enablelocalvoicereverb) |Enable the reverb effect for the local captured voice. |
|[setLocalVoiceEqualization](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setlocalvoiceequalization) |Set the equalization effect for the local captured audio. The audio includes both internal captured audio and external captured voice, but not the mixing audio file. |
|[enablePlaybackDucking](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableplaybackducking) |Enables/disables the playback ducking function. This function is usually used in scenarios where short videos or music will be played simultaneously during RTC calls. |

## Custom Stream Processing

|Methods |Description |
|---|---|
|[setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvideosourcetype) |Sets the input video source for the SDK, including screen streams. Internal capture is used by default. |
|[pushExternalVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-pushexternalvideoframe) |Pushes an external video frame. |
|[enableAlphaChannelVideoEncode](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enablealphachannelvideoencode) |Enables encoding of video frames with an alpha channel. |
|[disableAlphaChannelVideoEncode](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-disablealphachannelvideoencode) |Disables encoding of video frames with an alpha channel. |
|[setAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setaudiosourcetype) |Switches the audio capture source type. |
|[pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-pushexternalaudioframe) |Pushes custom audio data to the RTC SDK. |
|[setLocalVideoSink](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setlocalvideosink) |Get local video stream. |
|[unsetLocalVideoSink](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-unsetlocalvideosink) |Stop getting local video stream. |
|[setRemoteVideoSink](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setremotevideosink) |Get remote video stream. |
|[unsetRemoteVideoSink](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-unsetremotevideosink) |Stop get remote video stream. |
|[enableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableaudioframecallback) |Enable audio frames callback and set the format for the specified type of audio frames. |
|[disableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-disableaudioframecallback) |Disables audio data callback. |

|Callbacks |Description |
|---|---|
|[onLocalVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onlocalvideoframe) |Receives successfully captured local camera frames for custom processing or rendering. |
|[onRemoteVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onremotevideoframe) |Receives successfully captured remote camera frames for custom processing or rendering. |
|[onRecordAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onrecordaudioframe) |Returns audio data recorded by microphone. |
|[onPlaybackAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onplaybackaudioframe) |Returns the mixed audio data of all subscribed remote users. |
|[onRemoteUserAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onremoteuseraudioframe) |Returns the audio data of one remote user. |
|[onMixedAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onmixedaudioframe) |Returns mixed audio data including both data recorded by the local microphone and data from all subscribed remote users. |
|[onRecordScreenAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onrecordscreenaudioframe) |Returns the audio data played locally. |

## Network Management

|Methods |Description |
|---|---|
|[setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setlocalsimulcastmode) |Sets the local simulcast mode and optional substream configurations. |
|[setRemoteVideoConfig](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setremotevideoconfig) |Sets your expected configuration of the remote video stream that you want to subscribe to or have subscribed to. |
|[setPublishFallbackOption](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setpublishfallbackoption) |Sets the fallback option for published audio & video streams. You can call this API to set whether to automatically lower the resolution you set of the published streams under limited network conditions. |
|[setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setsubscribefallbackoption) |Sets the fallback option for subscribed RTC streams. You can call this API to set whether to lower the resolution of currently subscribed stream under limited network conditions. |
|[setRemoteUserPriority](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setremoteuserpriority) |Set user priority. |
|[startNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startnetworkdetection) |Pre\-call network detection. |
|[stopNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopnetworkdetection) |Stop pre\-call network probe. |
|[startEchoTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startechotest) |Audio/video loopback testing is unavailable in the single\-stream version. |
|[stopEchoTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopechotest) |Stopping an audio/video loopback test is unavailable in the single\-stream version. |
|[getNetworkTimeInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getnetworktimeinfo) |Obtain the synchronization network time information. |

|Callbacks |Description |
|---|---|
|[onSimulcastSubscribeFallback](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onsimulcastsubscribefallback) |Once the Fallback option is set, Fallback or reverting from a Fallback of a media stream will trigger this callback. |
|[onPerformanceAlarms](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onperformancealarms) |publish performance fallback is not turned on locally. When insufficient device performance is detected, this callback is received. If the publish performance fallback is enabled locally, this callback is received when the publish performance fallback/recovery is caused due to device performance/network reasons. |
|[onConnectionStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onconnectionstatechanged) |SDK connection state change callback with signaling server. Triggered when the connection state changes. |
|[onNetworkTypeChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onnetworktypechanged) |SDK Current network connection type change callback. Triggers the event when the current network connection type of the SDK changes. |
|[onNetworkDetectionResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onnetworkdetectionresult) |Pre\-call network detection result. |
|[onNetworkDetectionStopped](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onnetworkdetectionstopped) |Pre\-call network probing ends. |
|[onEchoTestResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onechotestresult) |Callback about the call test result. |
|[onNetworkTimeSynchronized](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onnetworktimesynchronized) |After calling [getNetworkTimeInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getnetworktimeinfo) for the first time, the SDK starts network time synchronization internally. This callback will be triggered when the synchronization is completed. |

## Message

|Methods |Description |
|---|---|
|[login](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-login) |Log in to send P2P messages or send messages to a server without joining the RTC room. |
|[updateLoginToken](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-updatelogintoken) |Update the Token. |
|[getPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getpeeronlinestatus) |Query the login status of the opposite or local user. |
|[sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-sendroommessage) |Send broadcast messages to all other users in the room. |
|[sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-sendroombinarymessage) |Send broadcast messages to all other users in the room. |
|[sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-sendusermessage) |Send a text message (P2P) to the specified user in the room. |
|[sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-senduserbinarymessage) |Sends a binary message (P2P) to the specified user in the room. |
|[sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-sendusermessageoutsideroom) |Send a text message (P2P) to a specified user outside the room. |
|[sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-senduserbinarymessageoutsideroom) |Send binary messages (P2P) to a specified user outside the room. |
|[setServerParams](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setserverparams) |Set application server parameters. |
|[sendServerMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-sendservermessage) |The client side sends a text message to the application server (P2Server). |
|[sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-sendserverbinarymessage) |Client side sends binary messages to the application server (P2Server). |
|[sendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-sendstreamsyncinfo) |Send audio stream synchronization information. The message is sent to the remote end through the audio stream and synchronized with the audio stream. |
|[sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-sendseimessage) |Sends SEI data. |
|[sendLivePushSEIMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-sendlivepushseimessage) |Sends SEI data in key\-value format through video frames. |
|[logout](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-logout) |After calling this interface to log out, it is impossible to call methods related to out\-of\-room messages and end\-to\-server messages or receive related callbacks. |

|Callbacks |Description |
|---|---|
|[onLoginResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onloginresult) |login result callback. |
|[onLogout](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onlogout) |logout result callback. |
|[onRoomMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onroommessagesendresult) |You receive this callback with the result of calling [sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-sendroommessage) or [sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-sendroombinarymessage). |
|[onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onroommessagereceived) |Receives a callback for broadcast messages in the room. |
|[onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onroombinarymessagereceived) |Receives a callback to a binary broadcast message in the room. |
|[onGetPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-ongetpeeronlinestatus) |Callback to tell the login state of a user. |
|[onUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onusermessagereceived) |Receive this callback when you receive a text message (P2P) from another user in the room. |
|[onUserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onusermessagesendresult) |After sending a text or binary message (P2P) to a single user in the room, the message sender receives a callback with the result of the message. |
|[onUserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onusermessagesendresult) |After sending a text or binary message (P2P) to a single user in the room, the message sender receives a callback with the result of the message. |
|[onServerParamsSetResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onserverparamssetresult) |Set the return result of the application server parameter. |
|[onServerMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onservermessagesendresult) |Callback to send a message to the application server. |
|[onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserbinarymessagereceived) |A single user receives a callback (P2P) of binary messages from other uid\-owned users in the same room. |
|[onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onuserbinarymessagereceived) |Receive this callback when you receive a binary message from an out\-of\-room user calling [sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-senduserbinarymessage). |
|[onUserMessageSendResultOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onusermessagesendresultoutsideroom) |A callback that sends a message to a specified user outside the room. |
|[onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onusermessagereceivedoutsideroom) |Receive this callback when you receive a text message from an out\-of\-room user calling sendUserMessageOutsideRoom. |
|[onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onuserbinarymessagereceivedoutsideroom) |Receive this callback when you receive a binary message from an out\-of\-room user calling [sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-senduserbinarymessageoutsideroom). |
|[onSEIStreamUpdate](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onseistreamupdate) |Callback about publishing status of the black frame video stream. |
|[onSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onseimessagereceived) |Receive this callback when you receive a video frame with a SEI message sent via sendSEIMessage. |

## Push to CDN/WTN

|Methods |Description |
|---|---|
|[setAudioAlignmentProperty](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setaudioalignmentproperty) |On the listener side, set all subscribed audio streams precisely timely aligned. |
|[startPushMixedStream](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startpushmixedstream) |Starts a task that publishes a mixed stream to CDN or publishes a WTN stream. |
|[updatePushMixedStream](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-updatepushmixedstream) |Updates parameters of a task started by [startPushMixedStream](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startpushmixedstream). |
|[stopPushMixedStream](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stoppushmixedstream) |Stop pushing a mixed stream to its target. |
|[startPushSingleStream](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startpushsinglestream) |Start forwarding a single media stream to a specified RTC room or CDN address. |
|[stopPushSingleStream](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stoppushsinglestream) |Stop a single\-stream forwarding task. |
|[getWTNStream](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getwtnstream) |Gets the WTN stream instance. |
|[subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-85532#rtcwtnstream-subscribewtnaudiostream) |Subscribes to or unsubscribes from a specified WTN audio stream. |
|[subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-85532#rtcwtnstream-subscribewtnvideostream) |Subscribes to or unsubscribes from a specified WTN video stream. |
|[setupWTNRemoteVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcwtnstream-setupwtnremotevideo) |Binds an internal render view for a specified WTN remote video stream. |
|[setWTNRemoteVideoSink](https://docs.byteplus.com/en/docs/12/docs-85532#rtcwtnstream-setwtnremotevideosink) |Binds a custom video sink for a specified WTN remote video stream. |
|[setWTNRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcwtnstream-setwtnremoteaudioplaybackvolume) |Adjusts the playback volume of a specified WTN remote audio stream. |
|[unsetWTNRemoteVideoSink](https://docs.byteplus.com/en/docs/12/docs-85532#rtcwtnstream-unsetwtnremotevideosink) |Unbinds the custom video sink of a specified WTN remote video stream. |
|[removeWTNRemoteVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcwtnstream-removewtnremotevideo) |Removes the internal render view bound to a specified WTN remote video stream. |
|[dispose](https://docs.byteplus.com/en/docs/12/docs-85532#rtcwtnstream-dispose) |Releases the WTN stream instance. |

|Callbacks |Description |
|---|---|
|[onMixedStreamEvent](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onmixedstreamevent) |Reports events for a server\-side mixed\-stream push task. |
|[onSingleStreamEvent](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onsinglestreamevent) |Used for reporting events during pushing a single stream to CDN. |
|[onWTNAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcwtnstreamcallback-onwtnaudiosubscribestatechanged) |Callback for WTN audio subscription state changes. |
|[onWTNVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcwtnstreamcallback-onwtnvideosubscribestatechanged) |Callback for WTN video subscription state changes. |
|[onWTNFirstRemoteAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85533#rtcwtnstreamcallback-onwtnfirstremoteaudioframe) |Callback when the first remote WTN audio frame is decoded successfully. |
|[onWTNFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-85533#rtcwtnstreamcallback-onwtnfirstremotevideoframedecoded) |Callback when the first remote WTN video frame is decoded successfully. |
|[onWTNSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85533#rtcwtnstreamcallback-onwtnseimessagereceived) |Callback for SEI messages carried in a WTN stream. |
|[onWTNDataMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85533#rtcwtnstreamcallback-onwtndatamessagereceived) |Callback for data messages carried in a WTN stream. |
|[onWTNVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85533#rtcwtnstreamcallback-onwtnvideoframe) |Callback for custom\-rendered WTN video frames. |

## Audio Effect Player

|Methods |Description |
|---|---|
|[getAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getaudioeffectplayer) |Create an instance for audio effect player. |
|[setEventHandler](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-seteventhandler) |Set the event handler. |
|[preload](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-preload) |Preloads specified music files into memory to avoid repeated loading when playing the same file frequently and reduce CPU usage. |
|[start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-start) |Starts to play the audio effect file.<br><br>This API can be called multiple times with different IDs and filepaths for multiple effects at the same time. |
|[setPosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-setposition) |Sets the start position of the audio effect file. |
|[getPosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-getposition) |Gets the current position of audio effect file playback. |
|[getDuration](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-getduration) |Get the duration of the audio effect file. |
|[setVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-setvolume) |Adjusts the volume level of a specified audio effect, including audio effect file and PCM effect. |
|[setVolumeAll](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-setvolumeall) |Sets the volume of all audio effects, including audio effect files and PCM effects. |
|[getVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-getvolume) |Gets the current volume. |
|[pause](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-pause) |Pauses the playback of audio effect files. |
|[resume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-resume) |Resumes the playback of audio effect files. |
|[pauseAll](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-pauseall) |Pauses the Playback of all audio effect files. |
|[resumeAll](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-resumeall) |Resumes the playback of all audio effect files. |
|[stop](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-stop) |Stops the playback of audio effect files. |
|[stopAll](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-stopall) |Stops playback of all audio effect files. |
|[unload](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-unload) |Unloads the specified audio effect file. |
|[unloadAll](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-unloadall) |Unloads all audio effect files. |

|Callbacks |Description |
|---|---|
|[onAudioEffectPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcaudioeffectplayercallback-onaudioeffectplayerstatechanged) |Callback for audio mixing status change. |

## Media Player

|Methods |Description |
|---|---|
|[getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getmediaplayer) |Create a media player instance. |
|[setEventHandler](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-seteventhandler) |Register an observer to receive related callbacks when the local media file is mixing. |
|[open](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-open) |Open the audio file.<br><br>You can only open one audio file with one player instance at the same time. For multiple audio files at the same time, create multiple player instances. |
|[openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-openwithcustomsource) |Starts mixing PCM audio data from a custom source. |
|[pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-pushexternalaudioframe) |Pushes PCM audio frames for mixing. |
|[start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-start) |Start playing the audio. Call this API when you call [open](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-open) and set `AutoPlay=false`. |
|[setVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-setvolume) |Adjusts the volume of the specified audio mixing, including media file mixing and PCM mixing. |
|[getVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-getvolume) |Gets the current volume. |
|[setPosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-setposition) |Sets the starting playback position of the media file. |
|[getPosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-getposition) |Gets the playback progress of the media file. |
|[getTotalDuration](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-gettotalduration) |Gets the duration of the media file. |
|[getPlaybackDuration](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-getplaybackduration) |Gets the actual playback duration of the mixed media file, in milliseconds. |
|[setAudioPitch](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-setaudiopitch) |Set the pitch of the local audio file mixing. Usually used in karaoke scenes. |
|[setAudioDualMonoMode](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-setaudiodualmonomode) |Sets the channel mode of the mixing of the media file. |
|[getAudioTrackCount](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-getaudiotrackcount) |Gets the track count of the current media file. |
|[selectAudioTrack](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-selectaudiotrack) |Specifies the playback track of the current media file. |
|[setPlaybackSpeed](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-setplaybackspeed) |Sets the playback speed of the audio file. |
|[setProgressInterval](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-setprogressinterval) |Set the interval of the periodic callback [onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-85533#rtcmediaplayercallback-onmediaplayerplayingprogress) during audio mixing. |
|[setLoudness](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-setloudness) |To call [enableVocalInstrumentBalance](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enablevocalinstrumentbalance) to adjust the volume of the mixed media file or the PCM audio data, you must pass in its original loudness through this API. |
|[pause](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-pause) |After calling [open](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-open), or [start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-start) to start audio mixing, call this API to pause audio mixing. |
|[resume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-resume) |After calling [pause](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-pause) to pause audio mixing, call this API to resume audio mixing. |
|[stop](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-stop) |After calling [open](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-open) or [start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-start) to start audio mixing, call this method to stop audio mixing. |

|Callbacks |Description |
|---|---|
|[onMediaPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcmediaplayercallback-onmediaplayerstatechanged) |Callback for audio mixing status change. |
|[onMediaPlayerEvent](https://docs.byteplus.com/en/docs/12/docs-85533#rtcmediaplayercallback-onmediaplayerevent) |Callback for media player events. |
|[onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-85533#rtcmediaplayercallback-onmediaplayerplayingprogress) |Periodic callback for playing progress. The period is set by `MediaPlayerConfig.callback_on_progress_interval`. |

## Screen Sharing

|Methods |Description |
|---|---|
|[getScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getscreencapturesourcelist) |Get the item list for screen sharing. |
|[getThumbnail](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getthumbnail) |Get the preview thumbnail of the screen\-sharing object. |
|[getWindowAppIcon](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getwindowappicon) |Get application window preview thumbnail for screen sharing. |
|[startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startscreenvideocapture) |Capture screen video stream for sharing. Screen video stream includes: content displayed on the screen, in the application window, or in the virtual screen. |
|[updateScreenCaptureMouseCursor](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-updatescreencapturemousecursor) |Update the processing settings for the mouse when capturing screen video streams through the capture module provided by the RTC SDK. The mouse is captured by default. |
|[updateScreenCaptureRegion](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-updatescreencaptureregion) |Update the capture area when capturing screen video streams through the capture module provided by the RTC SDK. |
|[updateScreenCaptureHighlightConfig](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-updatescreencapturehighlightconfig) |Update border highlighting settings when capturing screen video streams through the capture module provided by the RTC SDK. A border is displayed by default. |
|[updateScreenCaptureFilterConfig](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-updatescreencapturefilterconfig) |When capturing screen video streams through the capture module provided by the RTC SDK, set the window that needs to be filtered. |
|[startScreenAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startscreenaudiocapture) |When sharing the screen, start using RTC SDK internal collection method to collect screen audio. |
|[muteScreenAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-mutescreenaudiocapture) |Mute/Unmute the screen audio. |
|[setScreenAudioChannel](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setscreenaudiochannel) |Set the audio channel of the screen\-sharing audio stream. |
|[stopScreenAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopscreenaudiocapture) |Stop recording device audio. |
|[stopScreenVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopscreenvideocapture) |Stop screen video streaming. |

## Security and Encryption

|Methods |Description |
|---|---|
|[setEncryptInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setencryptinfo) |Set the way to use built\-in encryption when transmitting. |
|[setLocalProxy](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setlocalproxy) |Sets local proxy. |
|[startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startcloudproxy) |Start cloud proxy. |
|[stopCloudProxy](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopcloudproxy) |Stop cloud proxy. |

|Callbacks |Description |
|---|---|
|[onCloudProxyConnected](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-oncloudproxyconnected) |Receives the callback when you call [startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startcloudproxy) to start cloud proxy, and the SDK connects the proxy server successfully. |
|[onLocalProxyStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onlocalproxystatechanged) |Callback on local proxy connection. After calling [setLocalProxy](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setlocalproxy) to set local proxies, you will receive this callback that informs you of the states of local proxy connection. |

## Recording

|Methods |Description |
|---|---|
|[startFileRecording](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startfilerecording) |This method records the audio & video data during the call to a local file. |
|[stopFileRecording](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopfilerecording) |Stop local recording. |
|[startAudioRecording](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudiorecording) |Start recording audio communication, and generate the local file. |
|[stopAudioRecording](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopaudiorecording) |Stops local audio recording. |

|Callbacks |Description |
|---|---|
|[onRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onrecordingstateupdate) |Callback of the local recording status. |
|[onRecordingProgressUpdate](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onrecordingprogressupdate) |Local recording progress callback. |
|[onAudioRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onaudiorecordingstateupdate) |When calling [startAudioRecording](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudiorecording) or [stopAudioRecording](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopaudiorecording) to change the recording status, receive the callback. |

## Spatial Audio

|Methods |Description |
|---|---|
|[enableSpatialAudio](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-enablespatialaudio) |Enable/disable spatial audio function. |
|[disableRemoteOrientation](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-disableremoteorientation) |Call this API in each client to neglect the orientation of the remote speakers. From the local user's perspective, all the remote users will be facing him/her. |
|[updateSelfPosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updateselfposition) |Sets the coordinate and orientation of the local user as a listener in the rectangular coordinate system the local user built to achieve expected spatial audio effects. |
|[updateRemotePosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updateremoteposition) |Sets the coordinate and orientation of the remote user as a speaker in the rectangular coordinate system of the local user. In this case, the local user hears from the remote user with the expected spatial audio effects. |
|[removeRemotePosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-removeremoteposition) |Disables all spatial audio effects set by calling [updateRemotePosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updateremoteposition) for a certain remote user. |
|[removeAllRemotePosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-removeallremoteposition) |Disables all spatial audio effects set by calling [updateRemotePosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updateremoteposition) for all remote users. |

## Range Audio

|Methods |Description |
|---|---|
|[updateRangePosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updaterangeposition) |Updates the coordinate of the local user's position in the rectangular coordinate system in the current room. |
|[updateReceiveRange](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updatereceiverange) |Updates the audio receiving range for the local user. |
|[setAttenuationModel](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setattenuationmodel) |Set the volume roll\-off mode that a 3D sound has in an audio source when using the Range Audio feature. |
|[setNoAttenuationFlags](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setnoattenuationflags) |Set the flags to mark the user groups, within which the users talk without attenuation.<br><br>In the RTC room, if the flags of the users intersect with each other, the users talk without attenuation.<br><br>For example, the user is a member of multiple teams, and teammates of the same team talk without attenuation. You can set the flag for each team, and include the flags of the user's teams in the user's flags. |
|[enableRangeAudio](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-enablerangeaudio) |Enable/disable the range audio function. |

## Video Snapshot

|Methods |Description |
|---|---|
|[takeLocalSnapshot](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-takelocalsnapshot) |Take a snapshot of the local video. |
|[takeLocalSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-takelocalsnapshottofile) |Take a snapshot of the local video stream and save it as a JPG file at the specified local path.<br><br>After calling this method, the SDK triggers [onLocalSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onlocalsnapshottakentofile) to report whether the snapshot is taken successfully and provide details of the snapshot image. |
|[takeRemoteSnapshot](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-takeremotesnapshot) |Take a snapshot of the remote video. |
|[takeRemoteSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-takeremotesnapshottofile) |Take a snapshot of the local/remote video stream and save it as a JPG file at the specified local path.<br><br>After calling this method, the SDK triggers [onRemoteSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onremotesnapshottakentofile) to report whether the snapshot is taken successfully and provide details of the snapshot image. |

|Callbacks |Description |
|---|---|
|[onTakeLocalSnapshotResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-ontakelocalsnapshotresult) |Receives the callback after calling [takeLocalSnapshot](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-takelocalsnapshot). |
|[onLocalSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onlocalsnapshottakentofile) |Triggered after calling [takeLocalSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-takelocalsnapshottofile) to report whether the snapshot is taken successfully and provide details of the snapshot image. |
|[onTakeRemoteSnapshotResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-ontakeremotesnapshotresult) |Receives the callback after calling [takeRemoteSnapshot](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-takeremotesnapshot). |
|[onRemoteSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onremotesnapshottakentofile) |Triggered after calling [takeRemoteSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-takeremotesnapshottofile) to report whether the snapshot is taken successfully and provide details of the snapshot image. |

## Plugin Manager

|Methods |Description |
|---|---|
|[initializePluginManager](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-initializepluginmanager) |Initialize the plugin manager. |
|[registerPlugin](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-registerplugin) |Registers a plugin library. |
|[getPlugin](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getplugin) |Gets the control interface for a registered plugin. |
|[unregisterPlugin](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-unregisterplugin) |Uninstall plugin. |
|[releasePluginManager](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-releasepluginmanager) |Release plugin manager. |

## Advanced Features

|Methods |Description |
|---|---|
|[setAnsMode](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setansmode) |Set the Active Noise Cancellation(ANC) mode during audio and video communications. |
|[setEarMonitorMode](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setearmonitormode) |Turn on/off the earphone monitor function. |
|[setEarMonitorVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setearmonitorvolume) |Set the volume of the earphone monitor. |

|Callbacks |Description |
|---|---|
|[onExtensionAccessError](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onextensionaccesserror) |Failed to access the extension.<br><br>RTC SDK provides some features with extensions. Without implementing the extension, you cannot use the corresponding feature. |
