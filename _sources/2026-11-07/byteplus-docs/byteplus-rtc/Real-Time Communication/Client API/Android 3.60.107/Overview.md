---
title: "Overview"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70079"
---

<span id="engine-management"></span>
## Engine Management


|Method |Description |
|---|---|
|[createRTCEngine](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-creatertcengine) |Creates an engine instance.<br><br>This is the very first API that you must call if you want to use all the RTC capabilities.<br><br>If there is no engine instance in current process, calling this API will create one. If an engine instance has been created, calling this API again will have the created engine instance returned. |
|[setVideoCaptureRotation](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setvideocapturerotation) |Set the rotation of the video images captured from the local device.<br><br>Call this API to rotate the videos when the camera is fixed upside down or tilted. For rotating videos on a phone, we recommend to use [setVideoRotationMode](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setvideorotationmode). |
|[getNativeHandle](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-getnativehandle) |Get [IRTCEngine](https://docs.byteplus.com/byteplus-rtc/docs/70095#irtcengine) in C++ layer. |
|[feedback](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-feedback) |Report the user feedback to RTC. |
|[setRuntimeParameters](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setruntimeparameters) |Setting runtime parameters |
|[setBusinessId](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setbusinessid) |Sets the business ID<br><br>You can use businessId to distinguish different business scenarios. You can customize your businessId to serve as a sub AppId, which can share and refine the function of the AppId, but it does not need authentication. |
|[setLogConfig](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setlogconfig) |Configures the local log parameters of RTC SDK, including the logging level, directory, the limits for total log file size, and the prefix to the log file. |
|[getSDKVersion](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-getsdkversion) |Get the current version number of the SDK. |
|[destroyRTCEngine](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-destroyrtcengine) |Destroy the engine instance created by [createRTCEngine](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-creatertcengine), and release all related resources. |



|Callback |Description |
|---|---|
|[onPublishPrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onpublishprivilegetokenwillexpire) |Callback triggered 30s before the publishing privilege of the Token expires.<br><br>After receiving this callback, you must call [updateToken](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-updatetoken) to update the publishing privilege Token. |
|[onExperimentalCallback](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onexperimentalcallback) |callback for experimental api |
|[onLogReport](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onlogreport) |Callback this event when logging is reported. |
|[onSysStats](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onsysstats) |Callbacks occur every 2 seconds to inform the current CPU and memory usage information. |
|[onError](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onerror) |Error callback occurred. |
|[onWarning](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onwarning) |A warning occurred during the SDK runtime. The SDK usually recovers automatically and warnings can be ignored. |
|[onSubscribePrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onsubscribeprivilegetokenwillexpire) |Callback triggered 30s before the subscribing privilege of the Token expires.<br><br>After receiving this callback, you must call [updateToken](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-updatetoken) to update the subscribing privilege Token. |
|[onTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-ontokenwillexpire) |The callback is triggered when the SDK detects the joining room privilege from the Token will expires within 30s.<br><br>After receiving this callback, you must call [updateToken](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-updatetoken) to update the joining room privilege Token. |


<span id="room-management"></span>
## Room Management


|Method |Description |
|---|---|
|[destroy](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-destroy) |Leave and destroy the room instance created by calling [createRTCRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-creatertcroom). |
|[createRTSRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-creatertsroom) |Create a [RTSRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom) instance.<br><br>This API only returns a room instance. You still need to call [joinRTSRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-joinrtsroom) to actually create/join the room.<br><br>Each call of this API creates one [RTSRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom) instance. Call this API as many times as the number of rooms you need, and then call [joinRTSRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-joinrtsroom) of each RTSRoom instance to join multiple rooms at the same time. |
|[createRTCRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-creatertcroom) |Create a RTCroom instance.<br><br>This API only returns a room instance. You still need to call [joinRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-joinroom) to actually create/join the room.<br><br>Each call of this API creates one [RTCRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom) instance. Call this API as many times as the number of rooms you need, and then call [joinRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-joinroom) of each RTCRoom instance to join multiple rooms at the same time.<br><br>In multi\-room mode, a user can subscribe to media streams in the joined rooms at the same time. |
|[setRTSRoomEventHandler](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-setrtsroomeventhandler) |Listens for event callbacks related to the [RTCRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom) instance by setting the event handler of this instance. |
|[leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-leaveroom) |Leave the RTS room.<br><br>The user calls this method to leave the room, end the call process, and release all call\-related resources. |
|[updateToken](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-updatetoken) |Updates the room token.<br><br>You must call this API to update token to ensure the RTC call to continue when you receive [onTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-ontokenwillexpire), [onPublishPrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onpublishprivilegetokenwillexpire), or . |
|[joinRTSRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-joinrtsroom) |Joins the RTS room.<br><br>After creating a room by calling [createRTSRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-creatertsroom), call this API to join the room and make audio & video calls with other users in the room. |
|[destroy](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-destroy) |Leave and destroy the room instance created by calling [createRTSRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-creatertsroom). |
|[getCallId](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-getcallid) |Gets call ID.<br><br>Call this method after joining an RTC room. After creating a room, a call ID is generated to identify the call for this room. |
|[getRoomId](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-getroomid) |Get RTC room ID. |
|[setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setroomextrainfo) |Sets extra information about the RTC room the local user joins. |
|[setLiveMode](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setlivemode) |Sets live mode.<br><br>Call this method after joining a room. |
|[setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setuservisibility) |Set the visibility of the user in the room. The local user is visible to others by default before calling this API.<br><br>An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Room Capacity](https://docs.byteplus.com/en/byteplus-rtc/docs/257549). |
|[setRTCRoomEventHandler](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setrtcroomeventhandler) |Listens for event callbacks related to the [RTCRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom) instance by setting the event handler of this instance. |
|[joinRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-joinroom) |Join the RTC room.<br><br>After creating a room by calling [createRTCRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-creatertcroom), call this API to join the room and make audio & video calls with other users in the room. |



|Callback |Description |
|---|---|
|[onLeaveRoom](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onleaveroom) |Leave the room successfully callback.<br><br>After the user calls the [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-leaveroom) method, the SDK will stop all publishing subscription streams, and after releasing all call\-related audio & video resources, this callback will notify the user to leave the room successfully. |
|[onUserLeave](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onuserleave) |This callback is triggered when a remote user is disconnected or turns invisible. |
|[onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onuserjoined) |You will receive this callback in following cases:<br><br><br>&nbsp;<br><br>* The remote user calls [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setuservisibility) turns visible and joins your room.<br><br>* The remote visible user is disconnected and then reconnected to your room.<br><br>* The invisible remote user in your room calls [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setuservisibility) and turns visible.<br><br>* You join the room when there are visible users in the room. |
|[onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onroomstatechanged) |Callback on room state changes. Via this callback you get notified of room relating warnings, errors and events. For example, the user joins the room, the user is removed from the room, and so on. |
|[onLeaveRoom](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onleaveroom) |Leave the room successfully callback.<br><br>After the user calls the [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-leaveroom) method, the SDK will stop all publishing subscription streams, and after releasing all call\-related audio & video resources, this callback will notify the user to leave the room successfully. |
|[onUserVisibilityChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuservisibilitychanged) |Callback for user to set user visibility by calling [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setuservisibility). |
|[onRoomStreamExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstreamextrainfoupdate) |Callback used to receive the extra information set by the other users in the same room with [setStreamExtraInfo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setstreamextrainfo). |
|[onRoomExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomextrainfoupdate) |Callback used to receive the extra information set by the other users in the same room with [setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setroomextrainfo). |
|[onSetRoomExtraInfoResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onsetroomextrainforesult) |Callback on the result of calling [setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setroomextrainfo) to set extra information about the room. |
|[onUserLeave](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserleave) |This callback is triggered when a remote user is disconnected or turns invisible. |
|[onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserjoined) |You will receive this callback in following cases:<br><br><br>&nbsp;<br><br>* The remote user calls [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setuservisibility) turns visible and joins your room.<br><br>* The remote visible user is disconnected and then reconnected to your room.<br><br>* The invisible remote user in your room calls [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setuservisibility) and turns visible.<br><br>* You join the room when there are visible users in the room. |
|[onRoomStats](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstats) |Room call statistics callback.<br><br>After the user enters the room and starts the call, he receives this callback every 2s. |
|[onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged) |Callback on room state changes. Via this callback you get notified of room relating warnings, errors and events. For example, the user joins the room, the user is removed from the room, and so on. |


<span id="audio-management"></span>
## Audio Management


|Method |Description |
|---|---|
|[startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/docs-70080#IRTCAudioDeviceManager-startaudioplaybackdevicetest) |Start the playback test for the local audio device. RTC will start playing the audio file specified. And RTC will notify the audio volume via the `onAudioPlaybackDeviceTestVolume` periodically. |
|[stopHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stophardwareechodetection) |Stop the echo detection before joining a room. |
|[startHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-starthardwareechodetection) |Start echo detection before joining a room. |
|[setRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setremoteaudioplaybackvolume) |Set the audio volume of playing the received remote stream. You must join the room before calling the API. The validity of the setting is not associated with the publishing status of the stream. |
|[enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enableaudiopropertiesreport) |Enable audio information prompts. After that, you will receive [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onlocalaudiopropertiesreport), [onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onremoteaudiopropertiesreport), and [onActiveSpeaker](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onactivespeaker). |
|[enablePlaybackDucking](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enableplaybackducking) |Enables/disables the playback ducking function. This function is usually used in scenarios where short videos or music will be played simultaneously during RTC calls.<br><br>With the function on, if remote voice is detected, the local media volume of RTC will be lowered to ensure the clarity of the remote voice. If remote voice disappears, the local media volume of RTC restores. |
|[enableVocalInstrumentBalance](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enablevocalinstrumentbalance) |Enables/disables the loudness equalization function.<br><br>If you call this API with the parameter set to True, the loudness of user's voice will be adjusted to \-16lufs. If then you also call setAudioMixingLoudness and import the original loudness of the audio data used in audio mixing, the loudness will be adjusted to \-20lufs when the audio data starts to play. |
|[setPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setplaybackvolume) |Adjusts the locally playing volume after mixing sounds of all remote users. You can call this API before or during the playback. |
|[setScreenCaptureVolume](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setscreencapturevolume) |Adjusts the volume of audio captured during screen sharing.<br><br>This method only changes the volume of audio data and does not affect the hardware volume of the local device. |
|[setCaptureVolume](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setcapturevolume) |Adjust the volume of the audio capture |
|[muteScreenAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-mutescreenaudiocapture) |Mutes/unmutes the audio captured when screen sharing.<br><br>Calling this method will send muted data instead of the screen audio data, and it does not affect the local audio device capture status and the SDK audio stream publishing status. |
|[muteAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-muteaudiocapture) |Set whether to mute the recording signal (without changing the local hardware). |
|[enableExternalSoundCard](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enableexternalsoundcard) |Enable the audio process mode for external sound card. |
|[setDefaultAudioRoute](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setdefaultaudioroute) |Set the speaker or earpiece as the default audio playback device. |
|[getAudioRoute](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-getaudioroute) |Get the information of currently\-using playback route. |
|[setAudioRoute](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setaudioroute) |Set the current audio playback route. The default device is set via [setDefaultAudioRoute](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setdefaultaudioroute).<br><br>When the audio playback route changes, you will receive [onAudioRouteChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onaudioroutechanged). |
|[setAudioProfile](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setaudioprofile) |Sets the sound quality. Call this API to change the sound quality if the audio settings in the current [ChannelProfile](https://docs.byteplus.com/en/docs/12/docs-70083#ChannelProfile) can not meet your requirements. |
|[setAudioScenario](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setaudioscenario) |Sets the audio scenarios.<br><br>After selecting the audio scenario, SDK will automatically switch to the proper volume modes (the call/media volume) according to the scenarios and the best audio configurations under such scenarios.<br><br>This API should not be used at the same time with the old one. |
|[stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stopaudiocapture) |Stop internal audio capture. The default is off.<br><br>Internal audio capture refers to: capturing audio using the built\-in module.<br><br>The local client will be informed via [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onaudiodevicestatechanged) after stopping audio capture by calling this API.<br><br>The remote clients in the room will be informed of the state change via [onUserStopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onuserstopaudiocapture) after the visible client stops audio capture by calling this API. |
|[startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startaudiocapture) |Start internal audio capture. The default is off.<br><br>Internal audio capture refers to: capturing audio using the built\-in module.<br><br>The local client will be informed via [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onaudiodevicestatechanged) after starting audio capture by calling this API.<br><br>The remote clients in the room will be informed of the state change via [onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onuserstartaudiocapture) after the visible user starts audio capture by calling this API. |
|[getAudioDeviceManager](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-getaudiodevicemanager) |Gets audio device management API class. |
|[setAudioSelectionConfig](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setaudioselectionconfig) |Set the priority of the local audio stream to be published. |
|[setRemoteRoomAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setremoteroomaudioplaybackvolume) |Adjusts the audio playback volume from all the remote users in a room. |
|[stopAudioDevicePlayTest](https://docs.byteplus.com/en/docs/12/docs-70080#IRTCAudioDeviceManager-stopaudiodeviceplaytest) |Stop the capture and playback test for local audio devices which is started by calling [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-70080#IRTCAudioDeviceManager-startaudiodevicerecordtest).<br><br>Before the test ends by itself, you can call this API to stop the recording or playing. |
|[stopAudioDeviceRecordAndPlayTest](https://docs.byteplus.com/en/docs/12/docs-70080#IRTCAudioDeviceManager-stopaudiodevicerecordandplaytest) |Call this API to stop recording in the test and start to play the recording in 30 s after calling [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-70080#IRTCAudioDeviceManager-startaudiodevicerecordtest). |
|[startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-70080#IRTCAudioDeviceManager-startaudiodevicerecordtest) |Start the capture and playback test for local audio devices. |
|[stopAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/docs-70080#IRTCAudioDeviceManager-stopaudioplaybackdevicetest) |Stop the playback test for the local audio device. |



|Callback |Description |
|---|---|
|[onAudioStreamBanned](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onaudiostreambanned) |All the users in the room will get informed via this callback when a user is banned or the ban of the user has been lifted by calling BanUserStream/UnbanUserStream on the server side. |
|[onStreamSyncInfoReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onstreamsyncinforeceived) |Audio stream synchronization information callback. You can use this callback to receive audio stream synchronization information sent remotely after the remote user calls [sendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendstreamsyncinfo) to send an audio stream synchronization message. |
|[onHardwareEchoDetectionResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onhardwareechodetectionresult) |Callback that notifies you the result of the echo detection before a call |
|[onActiveSpeaker](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onactivespeaker) |After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enableaudiopropertiesreport), you will periodically receive this callback for the active speaker information. |
|[onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onremoteaudiopropertiesreport) |After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enableaudiopropertiesreport), you will periodically receive this callback for the instantaneous information about the subscribed remote audio streams.<br><br>The remote audio streams includes the microphone audio and screen audio collected using the RTC SDK internal mechanism/custom mechanism. |
|[onAudioPlaybackDeviceTestVolume](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onaudioplaybackdevicetestvolume) |Notification on the playing volume during the test for the local audio devices |
|[onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onlocalaudiopropertiesreport) |After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enableaudiopropertiesreport), you will periodically receive this callback for the instantaneous information about local audio.<br><br>Local audio includes the microphone audio, the screen audio captured using RTC SDK internal mechanisms, and locally mixing audio. |
|[onAudioDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onaudiodevicewarning) |Audio device warning callback. The audio devices includes audio capture devices and audio rendering devices. |
|[onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onaudiodevicestatechanged) |Audio device state callback, returns the state of audio capture and audio playback devices. |
|[onAudioRouteChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onaudioroutechanged) |Receive the callback when the audio route changes. |
|[onLocalAudioStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onlocalaudiostatechanged) |When the state of the local audio stream changes, the callback notifies the current local audio stream state. |
|[onUserStopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onuserstopaudiocapture) |Users in the room call [stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stopaudiocapture) when audio capture is turned off, other users in the room will receive this callback. |
|[onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onuserstartaudiocapture) |Users in the room will receive this callback when they call [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startaudiocapture) to turn on audio capture. |


<span id="video-management"></span>
## Video Management


|Method |Description |
|---|---|
|[enumerateVideoCaptureDevices](https://docs.byteplus.com/en/docs/12/docs-70080#IVideoDeviceManager-enumeratevideocapturedevices) |Get a list of video capture devices in the current system. |
|[updateRemoteStreamVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-updateremotestreamvideocanvas) |Modifies remote video frame rendering settings, including render mode and background color. |
|[getVideoDeviceManager](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-getvideodevicemanager) |Create a video Facility Management instance |
|[setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setremotevideocanvas) |Sets the view to be used for remote video rendering and the rendering mode.<br><br>To unbind the canvas, set `videoCanvas` to Null. |
|[updateRemoteStreamVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-updateremotestreamvideocanvas-2) |Modifies remote video frame rendering settings, including render mode, background color, and rotation angle, while using the internal rendering of the SDK. |
|[disableAlphaChannelVideoEncode](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-disablealphachannelvideoencode) |Disables the Alpha channel encoding feature for externally captured video frames. |
|[enableAlphaChannelVideoEncode](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enablealphachannelvideoencode) |Enables the Alpha channel encoding feature for custom captured video frames.<br><br>Suitable for scenarios where the video subject and background need to be separated at the push stream end, and the background can be custom rendered at the pull stream end. |
|[setCameraAdaptiveMinimumFrameRate](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setcameraadaptiveminimumframerate) |Set the minimum frame rate of of the dynamic framerate mode during internal video capture. |
|[enableCameraAutoExposureFaceMode](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enablecameraautoexposurefacemode) |Enable or disable face auto exposure mode during internal video capture. This mode fixes the problem that the face is too dark under strong backlight; but it will also cause the problem of too bright/too dark in the area outside the ROI region. |
|[setCameraExposureCompensation](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setcameraexposurecompensation) |Sets the exposure compensation for the currently used camera. |
|[setCameraExposurePosition](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setcameraexposureposition) |Sets the manual exposure position for the currently used camera. |
|[isCameraExposurePositionSupported](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-iscameraexposurepositionsupported) |Checks if manual exposure setting is available for the currently used camera. |
|[setCameraFocusPosition](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setcamerafocusposition) |Sets the manual focus position for the currently used camera. |
|[isCameraFocusPositionSupported](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-iscamerafocuspositionsupported) |Checks if manual focus is available for the currently used camera. |
|[setCameraTorch](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setcameratorch) |Turn on/off the flash state of the currently used camera (front/postcondition) |
|[getCameraZoomMaxRatio](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-getcamerazoommaxratio) |Get the maximum zoom factor of the currently used camera (front/postcondition) |
|[setCameraZoomRatio](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setcamerazoomratio) |Change the optical zoom magnification. |
|[isCameraZoomSupported](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-iscamerazoomsupported) |Detect whether the currently used camera (front/postcondition) supports zoom (digital/optical zoom). |
|[isCameraTorchSupported](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-iscameratorchsupported) |Detect the currently used camera (front/postcondition), whether flash is supported. |
|[setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setvideoencoderconfig) |Sets the expected quality of the video stream by specifying the resolution, frame rate, bitrate, and the fallback strategy when the network is poor. |
|[setVideoCaptureConfig](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setvideocaptureconfig) |Set the video capture parameters for internal capture of the RTC SDK.<br><br>If your project uses the SDK internal capture module, you can specify the video capture parameters including preference, resolution and frame rate through this interface. |
|[switchCamera](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-switchcamera) |Switch to the front\-facing/back\-facing camera used in the internal video capture<br><br>The local client will be informed via [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onvideodevicestatechanged) after calling this API. |
|[setVideoRotationMode](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setvideorotationmode) |Set the orientation of the video capture. By default, the App direction is used as the orientation reference.<br><br>During rendering, the receiving client rotates the video in the same way as the sending client did. |
|[updateLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-updatelocalvideocanvas) |Update the render mode and background color of local video rendering |
|[setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setlocalvideocanvas) |Sets the view to be used for local video rendering and the rendering mode. |
|[stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stopvideocapture) |Disable internal video capture immediately. The default is off.<br><br>Internal video capture refers to: capturing video using the built\-in module.<br><br>The local client will be informed via [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onvideodevicestatechanged) after stopping video capture by calling this API.<br><br>The remote clients in the room will be informed of the state change via [onUserStopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onuserstopvideocapture) after the visible client stops video capture by calling this API. |
|[startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startvideocapture) |Enable internal video capture immediately. The default setting is off.<br><br>Internal video capture refers to: capturing video using the built\-in module.<br><br>The local client will be informed via [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onvideodevicestatechanged) after starting video capture by calling this API.<br><br>The remote clients in the room will be informed of the state change via [onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onuserstartvideocapture) after the visible client starts video capture by calling this API. |
|[setRemoteVideoConfig](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setremotevideoconfig) |Sets your expected configuration of the remote video stream that you want to subscribe to or have subscribed to. |
|[setRemoteSimulcastStreamType](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setremotesimulcaststreamtype) |Sets the type of the remote video stream to subscribe to. |
|[setVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-70080#IVideoDeviceManager-setvideocapturedevice) |Set the current video capture device |



|Callback |Description |
|---|---|
|[onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onuserstartvideocapture) |The remote clients in the room will be informed of the state change via this callback after the visible user starts video capture by calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startvideocapture). |
|[onFaceDetectResult](https://docs.byteplus.com/en/docs/12/docs-70081#IFaceDetectionObserver-onfacedetectresult) |Callback of the result of face detection with Effect SDK.<br><br>After calling [enableFaceDetection](https://docs.byteplus.com/en/docs/12/docs-70080#IVideoEffect-enablefacedetection) and using the Effect SDK integrated in the RTC SDK, you will receive this callback. |
|[onVideoDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onvideodevicewarning) |Video device warning callback, including video capture devices. |
|[onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onvideodevicestatechanged) |Video device state callback, returns the state of video capture and screen capture devices. |
|[onLocalVideoStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onlocalvideostatechanged) |Receive this event when the state of the local video stream changes. |
|[onUserStopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onuserstopvideocapture) |The remote clients in the room will be informed of the state change via this callback after the visible user stops video capture by calling [stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stopvideocapture).<br><br>If you don't start video capture before you publish video data, all visible user will receive this callback. |


<span id="audio-video-transport"></span>
## Audio & Video Transport


|Method |Description |
|---|---|
|[setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setmultideviceavsync) |Synchronizes published audio and video.<br><br>When the same user simultaneously uses separate devices to capture and publish audio and video, there is a possibility that the streams are out of sync due to the network disparity. In this case, you can call this API on the video publisher side and the SDK will automatically line the video stream up according to the timestamp of the audio stream, ensuring that the audio the receiver hears corresponds to the video the receiver watches. |
|[requestRemoteVideoKeyFrame](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-requestremotevideokeyframe) |After subscribing to the remote video stream, request the keyframe |
|[setDummyCaptureImagePath](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setdummycaptureimagepath) |Set an alternative image when the local internal video capture is not enabled.<br><br>When you call `stopVideoCapture`, an alternative image will be pushed. You can set the path to null or open the camera to stop publishing the image.<br><br>You can repeatedly call this API to update the image. |
|[setStreamExtraInfo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setstreamextrainfo) |Sets extra information about the stream the local user publishes. |
|[resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-resumeforwardstreamtoallrooms) |Call this method to resume relaying to all rooms from the pause by calling [pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-pauseforwardstreamtoallrooms). |
|[pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-pauseforwardstreamtoallrooms) |Call this method to pause relaying media stream to all rooms after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-startforwardstreamtorooms).<br><br>After that, call [resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-resumeforwardstreamtoallrooms) to resume. |
|[stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-stopforwardstreamtorooms) |Call to this method to stop relaying media stream to all rooms after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-startforwardstreamtorooms). |
|[updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-updateforwardstreamtorooms) |Update information of the rooms where you want to relay the media stream to after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-startforwardstreamtorooms).<br><br>Adding and removing rooms by calling this method will trigger [onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onforwardstreamstatechanged) on the local. |
|[startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-startforwardstreamtorooms) |Start relaying media stream across rooms.<br><br>After calling [joinRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-joinroom), you can call this method to publish the media stream to multiple rooms that applies to scenarios such as an online talent contest and so on. |
|[resumeAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-resumeallsubscribedstreamaudio) |Resumes receiving all remote audio streams. |
|[resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-resumeallsubscribedstreamvideo) |Resumes receiving all remote video streams. |
|[pauseAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-pauseallsubscribedstreamaudio) |Pauses receiving all remote audio streams. |
|[pauseAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-pauseallsubscribedstreamvideo) |Pauses receiving all remote video streams. |
|[subscribeAllStreamsAudio](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-subscribeallstreamsaudio) |Subscribes to or unsubscribes from all remote audio streams. |
|[subscribeAllStreamsVideo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-subscribeallstreamsvideo) |Subscribes to or unsubscribes from all remote video streams (by the camera). |
|[subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-subscribestreamaudio) |Subscribes to or unsubscribes from the specific remote audio streams captured by the microphone. |
|[subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-subscribestreamvideo) |Subscribes to or unsubscribes from the specific remote video streams captured by the camera. |
|[publishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-publishstreamaudio) |Publishes or stops publishing audio streams in the current room. |
|[publishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-publishstreamvideo) |Publishes or stops publishing video streams. |



|Callback |Description |
|---|---|
|[onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onvideopublishstatechanged) |Callback on video publishing state change. |
|[onAudioPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onaudiopublishstatechanged) |Callback on audio publishing state change. |
|[onSimulcastSubscribeFallback](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onsimulcastsubscribefallback) |When the simulcast subscribe fallback occurs, this callback is received. |
|[onVideoFramePlayStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onvideoframeplaystatechanged) |Triggered when the remote video stream first frame play state changes. |
|[onAudioFramePlayStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onaudioframeplaystatechanged) |Triggered when the audio first frame play state changes. |
|[onVideoFrameSendStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onvideoframesendstatechanged) |Triggered when the local video first frame send state changes. |
|[onAudioFrameSendStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onaudioframesendstatechanged) |Triggered when the local audio first frame send state changes. |
|[onFirstRemoteAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onfirstremoteaudioframe) |The subscriber will receive this callback when the first frame of the receiving audio stream begins to decode. The following situations are included:<br><br><br>&nbsp;<br><br>1. The publisher publishes audio, including the initial publication and restart after cancellation.<br><br>2. After the publisher stops audio capture, they restart it. When using an external source, this involves stopping the stream and then streaming again.<br><br>3. After the publisher publishes audio, the subscriber cancels the subscription to audio and then re\-subscribes to it. |
|[onFirstLocalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onfirstlocalaudioframe) |Receive the callback when publishing local audio stream. |
|[onRemoteVideoSizeChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onremotevideosizechanged) |Users in the room who subscribe to this video stream receive this callback when the remote video size or rotation information changes. |
|[onLocalVideoSizeChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onlocalvideosizechanged) |Callback triggered when the local preview video size or rotation information has changed. |
|[onFirstLocalVideoFrameCaptured](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onfirstlocalvideoframecaptured) |RTC SDK receives this callback when the first video frame or screen video frame capture is completed locally. |
|[onFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onfirstremotevideoframedecoded) |The subscriber will receive this callback when the first frame of the receiving video stream begins to decode. The following situations are included:<br><br><br>&nbsp;<br><br>1. The publisher publishes video, including the initial publication and restart after cancellation.<br><br>2. After the publisher stops video capture, they restart it. When using an external source, this involves stopping the stream and then streaming again.<br><br>3. After the publisher publishes video, the subscriber cancels the subscription to video and then re\-subscribes to it. |
|[onFirstRemoteVideoFrameRendered](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onfirstremotevideoframerendered) |The subscriber will receive this callback when the first frame of the receiving video stream begins to render. The following situations are included:<br><br><br>&nbsp;<br><br>1. The publisher publishes video for the first time.<br><br>2. In 1, the publisher cancels the video stream after publishing and publishes it again.<br><br>3. In 1, the publisher stops video capture after publishing and restarts it. (Or when using an external source, the stream is stopped and restarted again.)<br><br>4. In 1, the subscriber cancels the video stream and subscribes to it again. (The interface includes [subscribeAllStreamsVideo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-subscribeallstreamsvideo), [pauseAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-pauseallsubscribedstreamvideo). |
|[onRemoteVideoStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onremotevideostatechanged) |When the state of a remote video stream changes, users in the room who subscribe to this stream receive the event. |
|[onRemoteAudioStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onremoteaudiostatechanged) |When the state of the audio stream from the remote user subscribes to changes, this callback will be received to understand the current state of the remote audio stream. |
|[onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onnetworkquality) |Report the network quality of the users every 2s after the local user joins the room and starts publishing or subscribing to a stream. |
|[onForwardStreamEvent](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onforwardstreamevent) |Callback returning the events during relaying the media stream to each room |
|[onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onforwardstreamstatechanged) |Callback returning the state and errors during relaying the media stream to each of the rooms |
|[onVideoStreamBanned](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onvideostreambanned) |All the users in the room will get informed via this callback when a user is banned or the ban of the user has been lifted by calling BanUserStream/UnbanUserStream on the server side. |
|[onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamaudio) |Callback on a remote user publishing or stopping publishing remote microphone\-audio streams in the room. |
|[onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo) |Callback on a remote user publishing or stopping publishing video streams in the room. |
|[onAVSyncEvent](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onavsyncevent) |Stream publisher will receive this callback when the A/V synchronization error occurs after [setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setmultideviceavsync) is called. |
|[onStreamSubscribed](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onstreamsubscribed) |Callback on subscription status of media streams |
|[onRemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onremotestreamstats) |Remote audio/video stream statistics and network quality callbacks for local subscriptions.<br><br>After the local user subscribes to the stream successfully, the SDK will periodically (2s) notify the user through this callback event of the quality statistics of the subscribed stream during this reference period, including: sending audio & video bit rate, sending frame rate, encoded frame rate, network quality, etc. |
|[onLocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onlocalstreamstats) |Local stream data statistics and network quality callback.<br><br>After the local user publishes the flow successfully, the SDK will periodically (2s) notify the user through this callback event of the quality statistics of the published flow during this reference period.<br><br>Statistics are passed to the user through the callback parameters of the [LocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-70083#LocalStreamStats) type, including the sent audio & video bit rate, sent frame rate, encoded frame rate, network quality, etc. |
|[onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onaudiosubscribestatechanged) |Callback on state changes of the subscription to microphone\-audio streams. |
|[onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onvideosubscribestatechanged) |Callback on state changes of the subscription to camera\-video streams. |
|[onStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onstreamstatechanged) |Callback on stream state changes. You will receive this callback when you receive stream relating warnings and errors. |
|[onAVSyncStateChange](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onavsyncstatechange) |Stream publisher will receive this callback when the A/V synchronization state changes after [setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setmultideviceavsync) is called. |


<span id="audio-processing"></span>
## Audio Processing


|Method |Description |
|---|---|
|[setVoiceChangerType](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setvoicechangertype) |Set the sound change effect type |
|[setLocalVoicePitch](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setlocalvoicepitch) |Change local voice to a different key, mostly used in Karaoke scenarios.<br><br>You can adjust the pitch of local voice such as ascending or descending with this method. |
|[enableLocalVoiceReverb](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enablelocalvoicereverb) |Enable the reverb effect for the local captured voice. |
|[setLocalVoiceReverbParam](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setlocalvoicereverbparam) |Set the reverb effect for the local captured audio. The audio includes both internal captured audio and external captured voice, but not the mixing audio file. |
|[setLocalVoiceEqualization](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setlocalvoiceequalization) |Set the equalization effect for the local captured audio. The audio includes both internal captured audio and external captured voice, but not the mixing audio file. |
|[setVoiceReverbType](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setvoicereverbtype) |Set the reverb effect type |


<span id="video-processing"></span>
## Video Processing


|Method |Description |
|---|---|
|[initCVResource](https://docs.byteplus.com/en/docs/12/docs-70080#IVideoEffect-initcvresource) |Checks video effect license, sets the video effect resource model path, and initializes video effect. |
|[clearVideoWatermark](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-clearvideowatermark) |Removes video watermark from designated video stream. |
|[setVideoWatermark](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setvideowatermark) |Adds watermark to designated video stream. |
|[setVideoOrientation](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setvideoorientation) |Sets the orientation of the video frame before custom video processing and encoding. The default value is `Adaptive`.<br><br>You should set the orientation to `Portrait` when using video effects or custom processing.<br><br>You should set the orientation to `Portrait` or `Landscape` when pushing a single stream to the CDN. |
|[setBeautyIntensity](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setbeautyintensity) |Sets the beauty effect intensity. |
|[enableEffectBeauty](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enableeffectbeauty) |Enables/Disables basic beauty effects. |
|[getVideoEffectInterface](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-getvideoeffectinterface) |Gets video effect interfaces. |
|[stopVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stopvideodigitalzoomcontrol) |Stop the ongoing digital zoom control instantly. |
|[startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startvideodigitalzoomcontrol) |Continuous and repeatedly digital zoom control. This action effect both the video preview locally and the stream published. |
|[setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setvideodigitalzoomcontrol) |Digital zoom or move the local video image once. This action affects both the video preview locally and the stream published. |
|[setVideoDigitalZoomConfig](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setvideodigitalzoomconfig) |Set the step size for each digital zooming control to the local videos. |
|[setRemoteVideoMirrorType](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setremotevideomirrortype) |When using internal rendering, enable mirroring for the remote stream. |
|[setLocalVideoMirrorType](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setlocalvideomirrortype) |Sets the mirror mode for the captured video stream. |
|[disableFaceDetection](https://docs.byteplus.com/en/docs/12/docs-70080#IVideoEffect-disablefacedetection) |Stops face detection. |
|[enableFaceDetection](https://docs.byteplus.com/en/docs/12/docs-70080#IVideoEffect-enablefacedetection) |Starts face detection and registers the observer for the result.<br><br>With this observer, you will receive [onFaceDetectResult](https://docs.byteplus.com/en/docs/12/docs-70081#IFaceDetectionObserver-onfacedetectresult) periodically. |
|[disableVirtualBackground](https://docs.byteplus.com/en/docs/12/docs-70080#IVideoEffect-disablevirtualbackground) |Turns off the virtual background. |
|[enableVirtualBackground](https://docs.byteplus.com/en/docs/12/docs-70080#IVideoEffect-enablevirtualbackground) |Sets the original background to a specified image or a solid color. |
|[setColorFilterIntensity](https://docs.byteplus.com/en/docs/12/docs-70080#IVideoEffect-setcolorfilterintensity) |Sets the intensity of the color filter enabled. |
|[setColorFilter](https://docs.byteplus.com/en/docs/12/docs-70080#IVideoEffect-setcolorfilter) |Sets the color filter. |
|[updateEffectNode](https://docs.byteplus.com/en/docs/12/docs-70080#IVideoEffect-updateeffectnode) |Sets the intensity of video effects. |
|[setEffectNodes](https://docs.byteplus.com/en/docs/12/docs-70080#IVideoEffect-seteffectnodes) |Sets the video effects material package. |
|[disableVideoEffect](https://docs.byteplus.com/en/docs/12/docs-70080#IVideoEffect-disablevideoeffect) |Disables video effects. |
|[enableVideoEffect](https://docs.byteplus.com/en/docs/12/docs-70080#IVideoEffect-enablevideoeffect) |Enables video effects including beauty and color filters. |
|[getAuthMessage](https://docs.byteplus.com/en/docs/12/docs-70080#IVideoEffect-getauthmessage) |Get authorization messages from the Effect SDK for the online license. |


<span id="custom-stream-processing"></span>
## Custom Stream Processing


|Method |Description |
|---|---|
|[processVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70080#IVideoProcessor-processvideoframe) |Get RTC SDK acquired video frame, according to the video pre\-processor [registerLocalVideoProcessor](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-registerlocalvideoprocessor) set, video pre\-processing, the final processed video frame to the RTC SDK for encoding transmission. |
|[setRemoteVideoSink](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setremotevideosink) | |
|[setLocalVideoSink](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setlocalvideosink) |Binds the local video stream to a custom renderer. |
|[setVideoDecoderConfig](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setvideodecoderconfig) |Before subscribing to the remote video stream, set the remote video data decoding method |
|[pushExternalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-pushexternalencodedvideoframe) |Push a custom encoded video stream |
|[setRemoteVideoSink](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setremotevideosink-2) |Binds the remote video stream to a custom renderer.You can get video frame data at specified positions and formats through parameter settings. |
|[setExternalVideoEncoderEventHandler](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setexternalvideoencodereventhandler) |Register custom coded frame push event callback |
|[pushReferenceAudioPCMData](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-pushreferenceaudiopcmdata) |Push custom aec reference audio data to the RTC SDK. |
|[pullExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-pullexternalaudioframe) |Pulls audio data for external playback.<br><br>After calling this method, the SDK will actively fetch the audio data to play, including the decoded and mixed audio data from the remote source, for external playback. |
|[pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-pushexternalaudioframe) |Push custom captured audio data to the RTC SDK. |
|[setAudioRenderType](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setaudiorendertype) |Switch the audio render type. |
|[setAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setaudiosourcetype) |Switch the audio capture type. |
|[pushExternalVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-pushexternalvideoframe) |Pushes external video frames. |
|[setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setvideosourcetype) |Set the video source, including the screen recordings.<br><br>The internal video capture is the default, which refers to capturing video using the built\-in module. |
|[registerRemoteEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-registerremoteencodedvideoframeobserver) |Video data callback after registering remote encoding.<br><br>After registration, when the SDK detects a remote encoded video frame, it will trigger the [onRemoteEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IRemoteEncodedVideoFrameObserver-onremoteencodedvideoframe) callback |
|[registerLocalEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-registerlocalencodedvideoframeobserver) |Register a local video frame observer.<br><br>This method applys to both internal capturing and custom capturing.<br><br>After calling this API, SDK triggers [onLocalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70081#ILocalEncodedVideoFrameObserver-onlocalencodedvideoframe) whenever a video frame is captured. |
|[registerLocalVideoProcessor](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-registerlocalvideoprocessor) |Set up a custom video preprocessor.<br><br>Using this video preprocessor, you can call [processVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70080#IVideoProcessor-processvideoframe) to preprocess the video frames collected by the RTC SDK, and use the processed video frames for RTC audio & video communication. |
|[disableAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-disableaudioprocessor) |Disable custom audio processing. |
|[enableAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enableaudioprocessor) |Enable audio frames callback for custom processing and set the format for the specified type of audio frames. |
|[registerAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-registeraudioprocessor) |Register a custom audio preprocessor.<br><br>After that, you can call [enableAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enableaudioprocessor) to process the audio streams that either captured locally or received from the remote side. RTC SDK then encodes or renders the processed data. |
|[registerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-registeraudioframeobserver) |Register an audio frame observer. |
|[disableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-disableaudioframecallback) |Disables audio data callback. |
|[enableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enableaudioframecallback) |Enable audio frames callback and set the format for the specified type of audio frames. |
|[setLocalVideoSink](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setlocalvideosink-2) |Binds the local video stream to a custom renderer.You can get video frame data at specified positions and formats through parameter settings. |



|Callback |Description |
|---|---|
|[onRemoteEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IRemoteEncodedVideoFrameObserver-onremoteencodedvideoframe) |Call [registerRemoteEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-registerremoteencodedvideoframeobserver), the callback is triggered when the SDK detects the remote encoded video data |
|[onProcessScreenAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioFrameProcessor-onprocessscreenaudioframe) |Returns the address of the shared\-screen audio frames for custom processing. |
|[onProcessEarMonitorAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioFrameProcessor-onprocessearmonitoraudioframe) |You will receive the address of SDK\-level in\-ear monitoring audio frames for custom processing.<br><br>The audio effects set by `setVoiceReverbType` and `setVoiceChangerType` are included. |
|[onProcessRemoteUserAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioFrameProcessor-onprocessremoteuseraudioframe) |Returns the address of the locally captured audio frame for custom processing. |
|[onProcessPlayBackAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioFrameProcessor-onprocessplaybackaudioframe) |Returns the address of the locally captured audio frame for custom processing. |
|[onProcessRecordAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioFrameProcessor-onprocessrecordaudioframe) |Returns the address of the locally captured audio frame for custom processing. |
|[onCaptureMixedAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioFrameObserver-oncapturemixedaudioframe) |Return the mixed audio data of the data recorded by local microphone and the audio data of `MediaPlayer` and `EffectPlayer`. |
|[onMixedAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioFrameObserver-onmixedaudioframe) |Returns the mixed audio data including the data recorded by local microphone and that of all remote users subscribed by the local user. |
|[onRemoteUserAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioFrameObserver-onremoteuseraudioframe) |Returns the audio data of one remote user. |
|[onPlaybackAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioFrameObserver-onplaybackaudioframe) |Returns the mixed audio data of all remote users subscribed by the local user. |
|[onRecordAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioFrameObserver-onrecordaudioframe) |Returns the audio data recorded by local microphone. |
|[onActiveVideoLayer](https://docs.byteplus.com/en/docs/12/docs-70081#IExternalVideoEncoderEventHandler-onactivevideolayer) |As the sender of a external encoded video stream, you will receive this callback at certain moments.<br><br>Based on the hints of this callback, you can selectively encode the video stream that is ready for transmission, in order to reduce the performance impact of video encoding on the local device. This callback is triggered based on a combination of factors, including the performance of the local device, the local network, and whether the stream is subscribed by the remote user. |
|[onRequestKeyFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IExternalVideoEncoderEventHandler-onrequestkeyframe) |This callback is used to inform the stream publisher that a keyframe needs to be regenerated. |
|[onRateUpdate](https://docs.byteplus.com/en/docs/12/docs-70081#IExternalVideoEncoderEventHandler-onrateupdate) |When the frame rate or bit rate of a custom encoded stream changes, the callback is triggered |
|[onStop](https://docs.byteplus.com/en/docs/12/docs-70081#IExternalVideoEncoderEventHandler-onstop) |When receiving the callback, you need to stop pushing custom encoded video frames to the SDK |
|[onStart](https://docs.byteplus.com/en/docs/12/docs-70081#IExternalVideoEncoderEventHandler-onstart) |Prompt custom encoded frames to start pushing callbacks.<br><br>After receiving this callback, you can call [pushExternalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-pushexternalencodedvideoframe) to push a custom encoded video frame to the SDK |
|[onLocalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70081#ILocalEncodedVideoFrameObserver-onlocalencodedvideoframe) |After calling [registerLocalEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-registerlocalencodedvideoframeobserver), SDK will trigger this callback when it receives local video frames. |
|[onAudioFileFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioFileFrameObserver-onaudiofileframe) |The callback for the audio frames during local audio file mixing. |


<span id="network-processing"></span>
## Network Processing


|Method |Description |
|---|---|
|[startNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startnetworkdetection) |Enable pre\-call network detection |
|[setCellularEnhancement](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setcellularenhancement) |Enable cellular network assisted communication to improve call quality. |
|[getNetworkTimeInfo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-getnetworktimeinfo) |Obtain the synchronization network time information. |
|[stopEchoTest](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stopechotest) |Stop the current call test.<br><br>After calling [startEchoTest](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startechotest), you must call this API to stop the test. |
|[startEchoTest](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startechotest) |Starts a call test.<br><br>Before entering the room, you can call this API to test whether your local audio/video equipment as well as the upstream and downstream networks are working correctly.<br><br>Once the test starts, SDK will record your sound or video. If you receive the playback within the delay range you set, the test is considered normal. |
|[setRemoteUserPriority](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setremoteuserpriority) |Set user priority. |
|[setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setsubscribefallbackoption) |Sets the fallback option for subscribed RTC streams.<br><br>You can call this API to set whether to lower the resolution of currently subscribed stream under limited network conditions. |
|[setPublishFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setpublishfallbackoption) |Sets the fallback option for published audio & video streams.<br><br>You can call this API to set whether to automatically lower the resolution you set of the published streams under limited network conditions. |
|[setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setlocalsimulcastmode-2) |Enable the Simulcast feature. |
|[setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setlocalsimulcastmode) |Enable the Simulcast feature and configure the lower\-quality video streams settings. |
|[stopNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stopnetworkdetection) |Stop pre\-call network probe |



|Callback |Description |
|---|---|
|[onNetworkTypeChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onnetworktypechanged) |SDK Current network connection type change callback. Callbacks the event when the current network connection type of the SDK changes. |
|[onPerformanceAlarms](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onperformancealarms) |When the publish performance fallback [setPublishFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setpublishfallbackoption) is not turned on locally, and when insufficient device performance is detected, this callback is received.<br><br>When the [setPublishFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setpublishfallbackoption) is locally turned on, ans when the publish performance fallback/recovery is caused due to device performance/network reasons, this callback is received. |
|[onNetworkTimeSynchronized](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onnetworktimesynchronized) |After calling [getNetworkTimeInfo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-getnetworktimeinfo) for the first time, the SDK starts network time synchronization internally. This callback will be triggered when the synchronization is completed. |
|[onEchoTestResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onechotestresult) |Callback about the call test result. |
|[onNetworkDetectionStopped](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onnetworkdetectionstopped) |Network detection before the call ends<br><br>The following conditions will stop the detection and receive this callback:<br><br><br>&nbsp;<br><br>1. The callback is received once after the [stopNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stopnetworkdetection) interface is called to stop probing;<br><br>2. Upon receipt of the distal/local audio first frame, stop the probe; When the detection exceeds 3 minutes, stop detection;<br><br>3. When the detection link is disconnected for a certain time, stop detection.<br><br>   Reason |
|[onNetworkDetectionResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onnetworkdetectionresult) |Pre\-call network detection result.<br><br>After successfully calling [startNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startnetworkdetection), you will receive this callback for the first time in 3s and every 2s thereafter. |
|[onSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onseimessagereceived) |Receive this callback when you receive a video frame with a SEI message sent by calling [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendseimessage) |
|[onConnectionStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onconnectionstatechanged) |Callback SDK and signaling server connection status related events. Callbacks the event when the network connection state of the SDK to the signaling server changes. |


<span id="messaging"></span>
## Messaging


|Method |Description |
|---|---|
|[sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendusermessage) |Send a point\-to\-point text message to the specified user in the room |
|[sendLivePushSEIMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendlivepushseimessage) |Sends SEI data in Key\-Value format through video frames.<br><br>Before calling this API, you must call [setLiveMode](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setlivemode) and set the room live mode to `LIVE_MODE_SOLO_HOST`. |
|[sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendseimessage) |<span id="RTCEngine\-sendseimessage\-2"\></span\>Sends SEI data.<br><br>In a video call scenario, SEI is sent with the video frame, while in a voice call scenario, SDK will automatically publish a black frame with a resolution of 16 × 16 pixels to carry SEI data. |
|[sendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendstreamsyncinfo) |Send audio stream synchronization information. The message is sent to the remote end through the audio stream and synchronized with the audio stream. After the interface is successfully called, the remote user will receive a [onStreamSyncInfoReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onstreamsyncinforeceived) callback. |
|[sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendserverbinarymessage) |Client side sends binary messages to the application server (P2Server) |
|[sendServerMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendservermessage) |The client side sends a text message to the application server (P2Server) |
|[sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-senduserbinarymessageoutsideroom) |Send binary messages (P2P) to the specified user outside the room |
|[sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendusermessageoutsideroom) |Send a text message (P2P) to a specified user outside the room |
|[getPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-getpeeronlinestatus) |Query the login status of the opposite or local user |
|[setServerParams](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setserverparams) |Set application server parameters<br><br>Client side calls [sendServerMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendservermessage) or [sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendserverbinarymessage) Before sending a message to the application server, you must set a valid signature and application server address. |
|[updateLoginToken](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-updatelogintoken) |Update the Token<br><br>Token used by the user for login has a certain valid period. When the Token expires, you need to call this method to update the login Token information.<br><br>When calling the [login](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-login) method to log in, if an expired token is used, the login will fail and you will receive an [onLoginResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onloginresult) callback notification with an error code of 'LOGIN_ERROR_CODE_INVALID_TOKEN'. You need to reacquire the token and call this method to update the token. |
|[logout](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-logout) |Call this method to log out, it is impossible to call methods related to out\-of\-room messages and end\-to\-server messages or receive related callbacks. |
|[login](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-login) |Log in to call [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendusermessageoutsideroom) and [sendServerMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendservermessage) to send P2P messages or send messages to a server without joining the RTC room.<br><br>To log out, call [logout](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-logout). |
|[sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroombinarymessage) |Group binary messages to all other users in the room. |
|[sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroommessage) |Mass text messages to all other users in the room. |
|[sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-senduserbinarymessage) |Sends a point\-to\-point binary message to the specified user in the room. |



|Callback |Description |
|---|---|
|[onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroommessagereceived) |\> This callback will be deprecated since version 3.64. Use [onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroommessagereceived-2) instead.<br><br>Receive a callback for broadcast messages in the room.<br><br>This callback is received when other users in the room call [sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroommessage) to send a broadcast message. |
|[onRoomMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onroommessagesendresult) |Receives this callback after sending a text message or a binary message to a room with [sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroommessage) or [sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroombinarymessage). |
|[onUserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onusermessagesendresult) |After sending a point\-to\-point text or point\-to\-point binary message to a single user in the room, the message sender will receive a callback with the result of the message. |
|[onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onuserbinarymessagereceived-2) |Receive this callback when you receive a peer\-to\-peer binary message from another user in the room via [sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-senduserbinarymessage). |
|[onUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onusermessagereceived-2) |Receive this callback when you receive a peer\-to\-peer text message from another user in the room via [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendusermessage). |
|[onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onroombinarymessagereceived-2) |Receives a callback for broadcast binary messages in the room.<br><br>This callback is received when other users in the room call [sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroombinarymessage) to send a broadcast binary message. |
|[onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onroommessagereceived-2) |Receive a callback for broadcast messages in the room.<br><br>This callback is received when other users in the room call [sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroommessage) to send a broadcast message. |
|[onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onuserbinarymessagereceived) |Receive this callback when you receive a peer\-to\-peer binary message from another user in the room via [sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-senduserbinarymessage). |
|[onUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onusermessagereceived) |Receive this callback when you receive a peer\-to\-peer text message from another user in the room via [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendusermessage). |
|[onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onroombinarymessagereceived) |Receives a callback for broadcast binary messages in the room.<br><br>This callback is received when other users in the room call [sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroombinarymessage) to send a broadcast binary message. |
|[onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onroommessagereceived) |Receive a callback for broadcast messages in the room.<br><br>This callback is received when other users in the room call [sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroommessage) to send a broadcast message. |
|[onServerMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onservermessagesendresult) |Receives the callback after sending the message to the application server successfully. |
|[onUserMessageSendResultOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onusermessagesendresultoutsideroom) |Callback for the result of sending a message to a user outside the room.<br><br>Triggered after you call [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendusermessageoutsideroom) or [sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-senduserbinarymessageoutsideroom). |
|[onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom-2) |This is triggered when a binary message is received from an out\-of\-room user calling [sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-senduserbinarymessageoutsideroom). |
|[onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onusermessagereceivedoutsideroom-2) |Receive this callback when you receive a text message from an out\-of\-room user calling [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendusermessageoutsideroom) |
|[onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom) |\> This callback will be deprecated in version 3.64. Please use [onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom-2) instead.<br><br>Receive this callback when you receive a binary message from an out\-of\-room user calling [sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-senduserbinarymessageoutsideroom) |
|[onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onusermessagereceivedoutsideroom) |\> This callback will be deprecated in version 3.64. Please use [onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onusermessagereceivedoutsideroom-2) instead.<br><br>Receive this callback when you receive a text message from an out\-of\-room user calling [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendusermessageoutsideroom) |
|[onGetPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-ongetpeeronlinestatus) |The return result of querying the login status of the peer or local user |
|[onServerParamsSetResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onserverparamssetresult) |Set the return result of the application server parameter |
|[onLogout](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onlogout) |Callback of logout result |
|[onLoginResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onloginresult) |Login result callback |
|[onSEIStreamUpdate](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onseistreamupdate) |Callback about publishing status of the black frame video stream .<br><br>In a voice call scenario, when the local user calls [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendseimessage) to send SEI data with a black frame, the sending status of the stream is notified to the remote user through this callback.<br><br>You can tell from this callback that the video frame carrying SEI data is a black frame and thus not render that video frame. |
|[onRoomMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroommessagesendresult) |Receives this callback after sending a text message or a binary message to a room with [sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroommessage) or [sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroombinarymessage). |
|[onUserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onusermessagesendresult) |After sending a point\-to\-point text or point\-to\-point binary message to a single user in the room, the message sender will receive a callback with the result of the message. |
|[onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserbinarymessagereceived-2) |Receive this callback when you receive a peer\-to\-peer binary message from another user in the room via [sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-senduserbinarymessage). |
|[onUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onusermessagereceived-2) |Receive this callback when you receive a peer\-to\-peer text message from another user in the room via [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendusermessage). |
|[onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroombinarymessagereceived-2) |Receives a callback for broadcast binary messages in the room.<br><br>This callback is received when other users in the room call [sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroombinarymessage) to send a broadcast binary message. |
|[onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroommessagereceived-2) |Receive a callback for broadcast messages in the room.<br><br>This callback is received when other users in the room call [sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroommessage) to send a broadcast message. |
|[onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserbinarymessagereceived) |\> This callback will be deprecated since version 3.64. Use [onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserbinarymessagereceived-2) instead.<br><br>Receive this callback when you receive a peer\-to\-peer binary message from another user in the room via [sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-senduserbinarymessage). |
|[onUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onusermessagereceived) |\> This callback will be deprecated since version 3.64. Use [onUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onusermessagereceived-2) instead.<br><br>Receive this callback when you receive a peer\-to\-peer text message from another user in the room via [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendusermessage). |
|[onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroombinarymessagereceived) |\> This callback will be deprecated since version 3.64. Use [onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroombinarymessagereceived-2) instead.<br><br>Receives a callback for broadcast binary messages in the room.<br><br>This callback is received when other users in the room call [sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroombinarymessage) to send a broadcast binary message. |


<span id="push-to-cdn-wtn"></span>
## Push to CDN/WTN


|Method |Description |
|---|---|
|[startPushMixedStream](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startpushmixedstream) |Specify the streams to be mixed and initiates the task to push the mixed stream to CDN or WTN. |
|[stopPushSingleStream](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stoppushsinglestream) |Stops the task of pushing a single media stream to CDN started via [startPushSingleStream](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startpushsinglestream). |
|[startPushSingleStream](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startpushsinglestream) |Pushes a single media stream to CDN or RTC room. |
|[stopPushMixedStream](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stoppushmixedstream) |Stops the task started via [startPushMixedStream](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startpushmixedstream). |
|[updatePushMixedStream](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-updatepushmixedstream) |Update the task configuration during the task started via [startPushMixedStream](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startpushmixedstream). You will be informed of the change via the [onMixedStreamEvent](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onmixedstreamevent) callback. |
|[subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-subscribewtnvideostream) |Subscribe/ unsubscribe WTN video stream<br><br>A user can call this method to subscribe or unsubscribe a WTN stream whether he/she has joined the room or not. |
|[subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-subscribewtnaudiostream) |Subscribe/unsubscribe the WTN audio stream<br><br>A user can call this method to subscribe a WTN stream whether he/she has joined the room or not. |
|[getWTNStream](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-getwtnstream) |Get the WTN stream interfaces. |
|[setWTNRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-setwtnremotevideocanvas) |Assign a internal render view to the WTN stream |
|[setWTNRemoteVideoSink](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-setwtnremotevideosink) |Assign a custom renderer to the WTN stream. See [Custom Video Rendering](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-81201) |
|[setWTNRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-setwtnremoteaudioplaybackvolume) |Set the audio playback volume of the WTN stream. |
|[setWTNStreamEventHandler](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-setwtnstreameventhandler) |Set the WTN event handler. |



|Callback |Description |
|---|---|
|[onMixedStreamEvent](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onmixedstreamevent) |Reports events during pushing a mixed stream to CDN or a WTN stream. |
|[onSingleStreamEvent](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onsinglestreamevent) |Reports events during pushing a single stream to CDN |
|[onWTNRemoteVideoStats](https://docs.byteplus.com/en/docs/12/docs-70081#IWTNStreamEventHandler-onwtnremotevideostats) |Remote WTN video stream ID and statistics. |
|[onWTNRemoteAudioStats](https://docs.byteplus.com/en/docs/12/docs-70081#IWTNStreamEventHandler-onwtnremoteaudiostats) |Remote WTN audio stream ID and statistics. |
|[onWTNVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IWTNStreamEventHandler-onwtnvideosubscribestatechanged) |Callback for the change of WTN video stream's subscription status<br><br>You will be informed of the result of subscribing to the WTN video stream by this callback after calling [subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-subscribewtnvideostream). |
|[onWTNAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IWTNStreamEventHandler-onwtnaudiosubscribestatechanged) |Callback for the change of WTN audio stream's subscription status<br><br>You will be informed of the result of subscribing to the WTN audio stream by this callback after calling [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-subscribewtnaudiostream). |
|[onWTNFirstRemoteAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IWTNStreamEventHandler-onwtnfirstremoteaudioframe) |Callback of successfully decoding of the first audio frame of the WTN stream<br><br>Refer to [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-subscribewtnaudiostream) for details about subscribing to a WTN audio stream. |
|[onWTNFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-70081#IWTNStreamEventHandler-onwtnfirstremotevideoframedecoded) |Callback of successfully decoding of the first video frame of the WTN stream<br><br>Refer to [subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-subscribewtnvideostream) for details about subscribing to a WTN video stream. |
|[onWTNSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IWTNStreamEventHandler-onwtnseimessagereceived) |Callback on receiving the SEI message carried by the WTN stream.<br><br>After calling [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-subscribewtnaudiostream)/[subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-subscribewtnvideostream), you will receive this callback if the WTN stream has an SEI message. |
|[onWTNDataMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IWTNStreamEventHandler-onwtndatamessagereceived) |The data information contained in the callback of WTN stream..<br><br>After calling [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-subscribewtnaudiostream)/[subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-70080#IWTNStream-subscribewtnvideostream), you can listen to this callback and retrieve SEI messages inserted by Open API calls or audio volume. |


<span id="audio-mixing"></span>
## Audio Mixing


|Method |Description |
|---|---|
|[getAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-getaudioeffectplayer) |Create an instance for audio effect player. |
|[setEventHandler](https://docs.byteplus.com/en/docs/12/docs-70080#IAudioEffectPlayer-seteventhandler) |Set the event handler. |
|[getDuration](https://docs.byteplus.com/en/docs/12/docs-70080#IAudioEffectPlayer-getduration) |Get the duration of the audio effect file. |
|[getVolume](https://docs.byteplus.com/en/docs/12/docs-70080#IAudioEffectPlayer-getvolume) |Gets the current volume. |
|[setVolumeAll](https://docs.byteplus.com/en/docs/12/docs-70080#IAudioEffectPlayer-setvolumeall) |Sets the volume of all audio effect, including audio effect files and PCM effects. |
|[setVolume](https://docs.byteplus.com/en/docs/12/docs-70080#IAudioEffectPlayer-setvolume) |Adjusts the volume level of a specified audio effect, including audio effect file and PCM effect. |
|[getPosition](https://docs.byteplus.com/en/docs/12/docs-70080#IAudioEffectPlayer-getposition) |Gets the current position of audio effect file playback. |
|[setPosition](https://docs.byteplus.com/en/docs/12/docs-70080#IAudioEffectPlayer-setposition) |Sets the start position of the audio effect file. |
|[resumeAll](https://docs.byteplus.com/en/docs/12/docs-70080#IAudioEffectPlayer-resumeall) |Resumes the playback of all audio effect files. |
|[resume](https://docs.byteplus.com/en/docs/12/docs-70080#IAudioEffectPlayer-resume) |Resumes the playback of audio effect files. |
|[pauseAll](https://docs.byteplus.com/en/docs/12/docs-70080#IAudioEffectPlayer-pauseall) |Pauses the Playback of all audio effect files. |
|[pause](https://docs.byteplus.com/en/docs/12/docs-70080#IAudioEffectPlayer-pause) |Pauses the playback of audio effect files. |
|[unloadAll](https://docs.byteplus.com/en/docs/12/docs-70080#IAudioEffectPlayer-unloadall) |Unloads all audio effect files. |
|[unload](https://docs.byteplus.com/en/docs/12/docs-70080#IAudioEffectPlayer-unload) |Unloads the specified audio effect file. |
|[preload](https://docs.byteplus.com/en/docs/12/docs-70080#IAudioEffectPlayer-preload) |Preloads specified music files into memory to avoid repeated loading when playing the same file frequently and reduce CPU usage. |
|[stopAll](https://docs.byteplus.com/en/docs/12/docs-70080#IAudioEffectPlayer-stopall) |Stops playback of all audio effect files. |
|[stop](https://docs.byteplus.com/en/docs/12/docs-70080#IAudioEffectPlayer-stop) |Stops the playback of audio effect files. |
|[start](https://docs.byteplus.com/en/docs/12/docs-70080#IAudioEffectPlayer-start) |Starts to play the audio effect file.<br><br>This API can be called multiple times with different IDs and filepaths for multiple effects at the same time. |
|[setEventHandler](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-seteventhandler) |Set the event handler. |
|[pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-pushexternalaudioframe) |Push PCM audio frame data for mixing. |
|[registerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-registeraudioframeobserver) |Register an observer to receive related callbacks when the local media file is mixing. |
|[setLoudness](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-setloudness) |To call [enableVocalInstrumentBalance](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-enablevocalinstrumentbalance) to adjust the volume of the mixed media file or the PCM audio data, you must pass in its original loudness through this API. |
|[setProgressInterval](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-setprogressinterval) |Set the interval of the periodic callback [onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-70081#IMediaPlayerEventHandler-onmediaplayerplayingprogress) during audio mixing. |
|[setPlaybackSpeed](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-setplaybackspeed) |Set the playback speed of the audio file. |
|[selectAudioTrack](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-selectaudiotrack) |Specifies the playback track of the current media file. |
|[getAudioTrackCount](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-getaudiotrackcount) |Gets the track count of the current media file. |
|[setAudioDualMonoMode](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-setaudiodualmonomode) |Sets the channel mode of the mixing of the media file. |
|[setPosition](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-setposition) |Sets the starting playback position of the media file. |
|[setAudioPitch](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-setaudiopitch) |Set the pitch of the local audio file mixing. Usually used in karaoke scenes. |
|[getState](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-getstate) |Get the state of the media player. |
|[getPosition](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-getposition) |Gets the playback progress of the media file. |
|[getPlaybackDuration](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-getplaybackduration) |Gets the actual playback duration of the mixed media file, in milliseconds. |
|[getTotalDuration](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-gettotalduration) |Gets the duration of the media file. |
|[getVolume](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-getvolume) |Gets the current volume. |
|[setVolume](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-setvolume) |Adjusts the volume of the specified audio mixing, including media file mixing and PCM mixing. |
|[resume](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-resume) |After calling [pause](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-pause) to pause audio mixing, call this API to resume audio mixing. |
|[pause](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-pause) |After calling [open](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-open), or [start](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-start) to start audio mixing, call this API to pause audio mixing. |
|[stop](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-stop) |After calling [open](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-open), [start](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-start), or [openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-openwithcustomsource) to start audio mixing, call this method to stop audio mixing. |
|[openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-openwithcustomsource) |Enable audio mixing with audio raw data.<br><br>To open the audio file, see [open](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-open). `open` and this API are mutually exclusive. |
|[start](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-start) |Start playing the audio. Call this API when you call [open](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-open) and set `AutoPlay=False`. |
|[open](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-open) |Open the audio file.<br><br>You can only open one audio file with one player instance at the same time. For multiple audio files at the same time, create multiple player instances.<br><br>For audio file in PCM format, see [openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-openwithcustomsource). `openWithCustomSource` and this API are mutually exclusive. |
|[getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-getmediaplayer) |Create a media player instance. |



|Callback |Description |
|---|---|
|[onAudioEffectPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioEffectPlayerEventHandler-onaudioeffectplayerstatechanged) |Callback for audio mixing status change. |
|[onSeek](https://docs.byteplus.com/en/docs/12/docs-70081#IMediaPlayerCustomSourceProvider-onseek) |Seeking the audio data based on the set starting position and offset to help SDK read and analyze data.<br><br>When you call [openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-openwithcustomsource) API to play the in\-memory audio data you input, or when you call [setPosition](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-setposition) to set the starting position of audio playing, this callback will be trigerred and you need to seek the audio data accorring to the value of offset and whence. |
|[onReadData](https://docs.byteplus.com/en/docs/12/docs-70081#IMediaPlayerCustomSourceProvider-onreaddata) |Callback of getting the path and size of the audio data you input.<br><br>When you call [openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-openwithcustomsource) API to play the in\-memory audio data you input, this callback will be triggered and you need to enter the path and size of the audio data. |
|[onMediaPlayerEvent](https://docs.byteplus.com/en/docs/12/docs-70081#IMediaPlayerEventHandler-onmediaplayerevent) |Callback for audio mixing player events. This callback is triggered after you call [selectAudioTrack](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-selectaudiotrack) and [setPosition](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-setposition). |
|[onFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IMediaPlayerAudioFrameObserver-onframe) |The callback for the audio frames during local audio file mixing. |
|[onMediaPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IMediaPlayerEventHandler-onmediaplayerstatechanged) |Callback for audio mixing status change. |
|[onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-70081#IMediaPlayerEventHandler-onmediaplayerplayingprogress) |Periodic callback for audio mixing progress. The period is set by [setProgressInterval](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-setprogressinterval). |
|[onAudioMixingPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onaudiomixingplayingprogress) |Callback for playback progress of mixed audio files |


<span id="screen-sharing"></span>
## Screen Sharing


|Method |Description |
|---|---|
|[startScreenCapture](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startscreencapture) |The RTC SDK start capturing the screen audio and/or video stream internally. |
|[updateScreenCapture](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-updatescreencapture) |Updates the media type of the internal screen capture. |
|[setScreenAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setscreenaudiosourcetype) |Sets the screen audio source type. (internal capture/custom capture) |
|[pushScreenAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-pushscreenaudioframe) |Using a custom capture method, when capturing screen audio during screen sharing, push the audio frame to the RTC SDK for encoding and other processing. |


<span id="security-and-encryption"></span>
## Security and Encryption


|Method |Description |
|---|---|
|[setEncryptInfo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setencryptinfo) |Sets the way to use built\-in encryption when transmitting. |
|[setLocalProxy](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setlocalproxy) |Sets local proxy. |
|[stopCloudProxy](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stopcloudproxy) |Stop cloud proxy |
|[startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startcloudproxy) |Start cloud proxy |
|[setCustomizeEncryptHandler](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setcustomizeencrypthandler) |Sets custom encryption and decryption methods. |



|Callback |Description |
|---|---|
|[onCloudProxyConnected](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-oncloudproxyconnected) |Receives the callback when you call [startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startcloudproxy) to start cloud proxy, and the SDK connects the proxy server successfully. |
|[onDecryptData](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEncryptionHandler-ondecryptdata) |Custom decryption.<br><br>Decrypts custom encrypted audio & video frame data. For custom encryption, see [onEncryptData](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEncryptionHandler-onencryptdata). |
|[onEncryptData](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEncryptionHandler-onencryptdata) |Custom encryption.<br><br>Encrypts audio & video frame data before transmission using the custom encryption method set.<br><br>Encryption of the original audio and video frames is currently not available. |
|[onLocalProxyStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onlocalproxystatechanged) |Callback on local proxy connection. After calling [setLocalProxy](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setlocalproxy) to set local proxies, you will receive this callback that informs you of the states of local proxy connection. |


<span id="advanced-features"></span>
## Advanced Features


|Method |Description |
|---|---|
|[enableSpatialAudio](https://docs.byteplus.com/en/docs/12/docs-70080#ISpatialAudio-enablespatialaudio) |Enable/disable spatial audio function. |
|[takeLocalSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-takelocalsnapshottofile) |Takes a snapshot of the local/remote video stream and save it as a JPG file at the specified local path.<br><br>After calling this method, the SDK triggers [onLocalSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onlocalsnapshottakentofile) to report whether the snapshot is taken successfully and provide details of the snapshot image. |
|[takeRemoteSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-takeremotesnapshottofile) |Takes snapshot of the remote video stream and save it as a JPG file at the specified local path.<br><br>After calling this method, the SDK triggers [onRemoteSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onremotesnapshottakentofile) to report whether the snapshot is taken successfully and provide details of the snapshot image. |
|[takeRemoteSnapshot](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-takeremotesnapshot) |Takes a snapshot of the local video. |
|[takeLocalSnapshot](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-takelocalsnapshot) |Take a snapshot of the local video. |
|[stopFileRecording](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stopfilerecording) |Stop local recording |
|[startFileRecording](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startfilerecording) |This method records the audio & video data during the call to a local file. |
|[setEarMonitorVolume](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setearmonitorvolume) |Set the monitoring volume. |
|[setEarMonitorMode](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setearmonitormode-2) |Enables/disables in\-ear monitoring and controls whether to apply local audio processing to the in\-ear monitoring audio. |
|[setEarMonitorMode](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setearmonitormode) |Enables/disables in\-ear monitoring. |
|[stopAudioRecording](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stopaudiorecording) |Stop audio recording. |
|[startAudioRecording](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startaudiorecording) |Starts recording audio communication, and generate the local file.<br><br>If you call this API before or after joining the room without internal audio capture, then the recording task can still begin but the data will not be recorded in the local files. Only when you call [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startaudiocapture) to enable internal audio capture, the data will be recorded in the local files. |
|[setAnsMode](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-setansmode) |Set the Active Noise Cancellation(ANC) mode during audio and video communications. |
|[setNoAttenuationFlags](https://docs.byteplus.com/en/docs/12/docs-70080#IRangeAudio-setnoattenuationflags) |Set the flags to mark the user groups, within which the users talk without attenuation.<br><br>In the RTC room, if the flags of the users intersects with each other, the users talk without attenuation.<br><br>For example, the user is a member of multiple teams, and teammates of the same team talks without attentuation. You can set the flag for each team, and includes the flags of the user's teams in the user's flags. |
|[setAttenuationModel](https://docs.byteplus.com/en/docs/12/docs-70080#IRangeAudio-setattenuationmodel) |Set the volume roll\-off mode that a 3D sound has in an audio source when using the Range Audio feature. |
|[updateReceiveRange](https://docs.byteplus.com/en/docs/12/docs-70080#IRangeAudio-updatereceiverange) |Updates the audio receiving range for the local user. |
|[updatePosition](https://docs.byteplus.com/en/docs/12/docs-70080#IRangeAudio-updateposition) |Updates the coordinate of the local user's position in the rectangular coordinate system in the current room. |
|[enableRangeAudio](https://docs.byteplus.com/en/docs/12/docs-70080#IRangeAudio-enablerangeaudio) |Enable/disable the range audio function.<br><br>Range audio means that within a certain range in a same RTC room, the audio volume of the remote user received by the local user will be amplified/attenuated as the remote user moves closer/away. The audio coming from out of the range cannot be heard. See [updateReceiveRange](https://docs.byteplus.com/en/docs/12/docs-70080#IRangeAudio-updatereceiverange) to set audio receiving range. |
|[getSpatialAudio](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-getspatialaudio) |Get location audio interface instances. |
|[getRangeAudio](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-getrangeaudio) |Gets range audio instance. |
|[removeAllRemotePosition](https://docs.byteplus.com/en/docs/12/docs-70080#ISpatialAudio-removeallremoteposition) |Disables all spatial audio effects set by calling [updateRemotePosition](https://docs.byteplus.com/en/docs/12/docs-70080#ISpatialAudio-updateremoteposition) for all remote users. |
|[removeRemotePosition](https://docs.byteplus.com/en/docs/12/docs-70080#ISpatialAudio-removeremoteposition) |Disables all spatial audio effects set by calling [updateRemotePosition](https://docs.byteplus.com/en/docs/12/docs-70080#ISpatialAudio-updateremoteposition) for a certain remote user. |
|[updateRemotePosition](https://docs.byteplus.com/en/docs/12/docs-70080#ISpatialAudio-updateremoteposition) |Sets the coordinate and orientation of the remote user as a speaker in the rectangular coordinate system of the local user. In this case, the local user hears from the remote user with the expected spatial audio effects. |
|[updateSelfPosition](https://docs.byteplus.com/en/docs/12/docs-70080#ISpatialAudio-updateselfposition) |Sets the coordinate and orientation of the local user as a listener in the rectangular coordinate system the local user built to achieve expected spatial audio effects. |
|[disableRemoteOrientation](https://docs.byteplus.com/en/docs/12/docs-70080#ISpatialAudio-disableremoteorientation) |Turn off the effect of the orientation of the local user as the sound source.<br><br>After the effect is off, all the other users in the room listen to the local user as if the local user is in right front of each of them. |



|Callback |Description |
|---|---|
|[onExtensionAccessError](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onextensionaccesserror) |Failed to access the extension.<br><br>RTC SDK provides some features with extensions. Without implementing the extension, you cannot use the corresponding feature. |
|[onTakeRemoteSnapshotResult](https://docs.byteplus.com/en/docs/12/docs-70081#ISnapshotResultCallback-ontakeremotesnapshotresult) |Receives the callback after calling [takeRemoteSnapshot](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-takeremotesnapshot). |
|[onTakeLocalSnapshotResult](https://docs.byteplus.com/en/docs/12/docs-70081#ISnapshotResultCallback-ontakelocalsnapshotresult) |Receives the callback after calling [takeLocalSnapshot](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-takelocalsnapshot). |
|[onLocalSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onlocalsnapshottakentofile) |Triggered after calling [takeLocalSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-takelocalsnapshottofile) to report whether the snapshot is taken successfully and provide details of the snapshot image. |
|[onRemoteSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onremotesnapshottakentofile) |Triggered after calling [takeRemoteSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-takeremotesnapshottofile) to report whether the snapshot is taken successfully and provide details of the snapshot image. |
|[onAudioRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onaudiorecordingstateupdate) |When calling [startAudioRecording](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startaudiorecording) or [stopAudioRecording](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stopaudiorecording) to change the recording status, receive the callback. |
|[onRecordingProgressUpdate](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onrecordingprogressupdate) |Local recording progress callback.<br><br>This callback is triggered by [startFileRecording](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startfilerecording). When the recording state is normal, the system will prompt the recording progress through this callback every second. |
|[onRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onrecordingstateupdate) |Get a callback of the local recording status.<br><br>The callback is triggered by either [startFileRecording](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startfilerecording) or [stopFileRecording](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-stopfilerecording). |
