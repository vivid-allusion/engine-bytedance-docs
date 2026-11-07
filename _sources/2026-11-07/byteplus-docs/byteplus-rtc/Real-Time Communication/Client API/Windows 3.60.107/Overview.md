---
title: "Overview"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70094"
---

<span id="engine-management"></span>
## Engine Management


|Method |Description |
|---|---|
|[createRTCEngine](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-creatertcengine) |Creates an engine instance.<br><br>This is the very first API that you must call if you want to use all the RTC capabilities.<br><br>If there is no engine instance in current process, calling this API will create one. If an engine instance has been created, calling this API again will have the created engine instance returned. |
|[release](https://docs.byteplus.com/en/docs/12/docs-70095#IDeviceCollection-release) |Releases the resources occupied by the current [IDeviceCollection](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceCollection) object. |
|[getDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IDeviceCollection-getdevice) |Get the information of the specific audio device. You can get the device information by index, device name, or device ID. |
|[getCount](https://docs.byteplus.com/en/docs/12/docs-70095#IDeviceCollection-getcount) |Get the number of audio & video devices in the current system |
|[getDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoDeviceCollection-getdevice-2) |Get the information of the specific video device. You can get the device information by index, device info (ID, product ID, etc.). |
|[release](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoDeviceCollection-release) |Releases the resources occupied by the current [IVideoDeviceCollection](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoDeviceCollection) object. |
|[getDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoDeviceCollection-getdevice) |Get the information of the specific video device. You can get the device information by index, device name, or device ID. |
|[getCount](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoDeviceCollection-getcount) |Get the number of video devices in the current system |
|[getDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceCollection-getdevice-2) |Get the information of the specific audio device. You can get the device information by index, device info (ID, product ID, etc.). |
|[release](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceCollection-release) |Releases the resources occupied by the current [IAudioDeviceCollection](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceCollection) object. |
|[getDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceCollection-getdevice) |According to the index number, get device information |
|[getCount](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceCollection-getcount) |Get the number of audio & video devices in the current system |
|[feedback](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-feedback) |Report the user feedback to RTC. |
|[setRuntimeParameters](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setruntimeparameters) |Set runtime parameters |
|[setBusinessId](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setbusinessid) |Sets the business ID<br><br>You can use businessId to distinguish different business scenarios. You can customize your businessId to serve as a sub AppId, which can share and refine the function of the AppId, but it does not need authentication. |
|[setLogConfig](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setlogconfig) |Configures the local log parameters of RTC SDK, including the logging level, directory, the limits for total log file size and the prefix of log. |
|[getSDKVersion](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-getsdkversion) |Get the current SDK version information. |
|[destroyRTCEngine](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-destroyrtcengine) |Destroy the engine instance created by [createRTCEngine](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-creatertcengine), and release all related resources. |



|Callback |Description |
|---|---|
|[onTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-ontokenwillexpire) |The callback is triggered when the SDK detects the joining room privilege from the Token will expires within 30s.<br><br>After receiving this callback, you must call [updateToken](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-updatetoken) to update the joining room privilege Token. |
|[onSysStats](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onsysstats) |You will periodically(2s) receive the callbacks of the current CPU and memory information. |
|[onLogReport](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onlogreport) |Terminal monitoring log callback. The callback is triggered when a terminal monitoring event is generated. |
|[onError](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onerror) |Error callback occurred. This callback is triggered when a network or media\-related error occurs during the<br><br>SDK runtime and cannot be automatically recovered and you may need to intervene. |
|[onWarning](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onwarning) |A warning occurred during the SDK runtime. The SDK usually recovers automatically and warnings can be ignored. |
|[onSubscribePrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onsubscribeprivilegetokenwillexpire) |Callback triggered 30s before the subscribing privilege of the Token expires.<br><br>After receiving this callback, you must call [updateToken](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-updatetoken) to update the subscribing privilege Token. |
|[onPublishPrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onpublishprivilegetokenwillexpire) |Callback triggered 30s before the publishing privilege of the Token expires.<br><br>After receiving this callback, you must call [updateToken](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-updatetoken) to update the publishing privilege Token. |


<span id="room-management"></span>
## Room Management


|Method |Description |
|---|---|
|[createRTCRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-creatertcroom) |Create a RTC room instance.<br><br>This API only returns a RTCroom instance. You still need to call [joinRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-joinroom) to actually create/join the room.<br><br>Each call of this API creates one [IRTCRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom) instance. Call this API as many times as the number of rooms you need, and then call [joinRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-joinroom) of each IRTCRoom instance to join multiple rooms at the same time.<br><br>In multi\-room mode, a user can subscribe to media streams in the joined rooms at the same time. |
|[setLiveMode](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-setlivemode) |Sets room live mode.<br><br>Call this method after joining a room. |
|[getCallId](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-getcallid) |Gets call ID.<br><br>Call this method after joining a room. After creating a room, a call ID is generated to identify the call for this room. |
|[getRoomId](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-getroomid) |Get room ID. |
|[setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-setroomextrainfo) |Sets extra information about the room the local user joins. |
|[joinRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-joinroom) |Join an RTC room.<br><br>After creating a room by calling [createRTCRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-creatertcroom), call this API to join the room and make audio & video calls with other users in the room. |
|[setRTCRoomEventHandler](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-setrtcroomeventhandler) |Listens for event callbacks related to the [IRTCRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom) instance by setting the event handler of this instance. |
|[setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-setuservisibility) |Set the visibility of the user in the room. The local user is visible to others by default before calling this API.<br><br>An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Room Capacity](https://docs.byteplus.com/en/byteplus-rtc/docs/257549). |
|[destroy](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-destroy) |Leave and destroy the RTC room instance created by calling [createRTCRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-creatertcroom). |
|[updateToken](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-updatetoken) |Update Token.<br><br>You must call this API to update token to ensure the RTC call to continue when you receive [onTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-ontokenwillexpire), [onPublishPrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onpublishprivilegetokenwillexpire), or [onSubscribePrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onsubscribeprivilegetokenwillexpire). |
|[joinRTSRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-joinrtsroom) |Joins an RTS room.<br><br>Users in the same room can talk to each other.<br><br>Repeated calls after entering the room are invalid. The user must call `leaveRoom` to exit the current room before joining the next room. |
|[setRTSRoomEventHandler](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-setrtsroomeventhandler) |Set the event handle of the [IRTSRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom) object.<br><br>You can listen for callback events for the room corresponding to this [IRTSRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom) object by setting the event handle. |
|[leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-leaveroom) |Leave the RTC or RTS room.<br><br>The user calls this method to leave the room, end the call process, and release all call\-related resources. |
|[destroy](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-destroy) |Leave and destroy the RTS room instance created by calling [createRTSRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-creatertsroom). |
|[createRTSRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-creatertsroom) |Create an RTS room instance.<br><br>This API only returns an RTS room instance. You still need to call [joinRTSRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-joinrtsroom) to actually create/join the room.<br><br>Each call of this API creates one [IRTSRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom) instance. Call this API as many times as the number of rooms you need, and then call [joinRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-joinroom) of each IRTCRoom instance to join multiple rooms at the same time.<br><br>In multi\-room mode, a user can send and receive rts message in the joined rooms at the same time. |



|Callback |Description |
|---|---|
|[onRoomStats](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onroomstats) |In\-room call statistics callback.<br><br>After the user enters the room and starts the call, he receives this callback every 2s. |
|[onUserLeave](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onuserleave) |This callback is triggered when a remote user is disconnected. |
|[onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onuserjoined) |Callback about remote users joining the room. |
|[onLeaveRoom](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onleaveroom) |Leave the room callback.<br><br>After the user calls the [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-leaveroom) method, the SDK stops all publishing subscription streams and notifies the user to leave the room successfully through this callback after releasing all audio & video resources related to the call. |
|[onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) |Callback on room state changes. Via this callback you get notified of room relating warnings, errors and events. For example, the user joins the room, the user is removed from the room, and so on. |
|[onUserVisibilityChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuservisibilitychanged) |Callback for user to set user visibility by calling [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-setuservisibility). |
|[onRoomStreamExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onroomstreamextrainfoupdate) |Callback used to receive the extra information set by the other users in the same room with [setStreamExtraInfo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-setstreamextrainfo). |
|[onRoomExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onroomextrainfoupdate) |Callback used to receive the extra information set by the other users in the same room with [setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-setroomextrainfo). |
|[onSetRoomExtraInfoResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onsetroomextrainforesult) |Callback on the result of calling [setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-setroomextrainfo) to set extra information about the room. |
|[onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserjoined) |Callback for when a remote visible user joins the room, or when an invisible user in the room switches to being visible.<br><br><br>&nbsp;<br><br>1. When a remote user sets themselves to be visible by calling the setUserVisibility method and then joins the room, other users in the room will receive this event.<br><br>2. When a remote visible user who has been disconnected re\-enters the room, other users in the room will receive this event.<br><br>3. When a hidden remote user in the room switches to being visible by calling the setUserVisibility method, other users in the room will receive this event.<br><br>4. A new user entering the room will receive an entry callback notification for visible users who were already in the room before they entered. |


<span id="audio-management"></span>
## Audio Management


|Method |Description |
|---|---|
|[muteAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-muteaudiocapture) |Set whether to mute the recording signal (without changing the local hardware). |
|[stopAudioDevicePlayTest](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-stopaudiodeviceplaytest) |Stop the capture and playback test for local audio devices which is started by calling [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-startaudiodevicerecordtest).<br><br>Before the test ends by itself, you can call this API to stop the recording or playing. |
|[stopAudioDeviceRecordAndPlayTest](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-stopaudiodevicerecordandplaytest) |Call this API to stop recording in the test and start to play the recording in 30 s after calling [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-startaudiodevicerecordtest). |
|[startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-startaudiodevicerecordtest) |Start the capture and playback test for local audio devices. |
|[stopAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-stopaudioplaybackdevicetest) |Stop the playback test for the local audio device. |
|[startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-startaudioplaybackdevicetest) |Start the playback test for the local audio device. RTC will start playing the audio file specified. And RTC will notify the audio volume via the `onAudioPlaybackDeviceTestVolume` periodically. |
|[initAudioCaptureDeviceForTest](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-initaudiocapturedevicefortest) |Try to initialize the audio capture device, which can detect abnormal problems such as the device does not exist, permissions are denied/disabled, etc. |
|[initAudioPlaybackDeviceForTest](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-initaudioplaybackdevicefortest) |Try to initialize the audio playback device, and you can detect abnormal problems such as the device does not exist, permissions are denied/disabled, etc. |
|[getAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-getaudiocapturedevice) |Gets the current audio capture device ID. |
|[getAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-getaudioplaybackdevice) |Gets the current audio playback device ID. |
|[getAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-getaudiocapturedevicemute) |Get state of the audio capture device. |
|[setAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-setaudiocapturedevicemute) |Mute or Unmute the current audio capture device. The default state is speaking. |
|[getAudioPlaybackDeviceMute](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-getaudioplaybackdevicemute) |Get the mute state of the current audio playback device. |
|[setAudioPlaybackDeviceMute](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-setaudioplaybackdevicemute) |Mute or Unmute the current audio playback device. The default state is speaking. |
|[getAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-getaudiocapturedevicevolume) |Get the current audio capture volume. |
|[setAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-setaudiocapturedevicevolume) |Set the current audio capture volume |
|[getAudioPlaybackDeviceVolume](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-getaudioplaybackdevicevolume) |Get the current audio playback device volume. |
|[setAudioPlaybackDeviceVolume](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-setaudioplaybackdevicevolume) |Set the current audio playback device volume |
|[setAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-setaudiocapturedevice) |Set up audio capture devices. |
|[setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-setaudioplaybackdevice) |Sets the audio playback device. |
|[followSystemCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-followsystemcapturedevice) |Set the audio capture device to follow the OS setting or not. |
|[followSystemPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-followsystemplaybackdevice) |Set the audio playback device to follow the OS setting or not. |
|[enumerateAudioCaptureDevices](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-enumerateaudiocapturedevices) |Get a list of audio acquisition devices in the current system. If there are subsequent device changes, you need to call this interface again to get a new device list. |
|[enumerateAudioPlaybackDevices](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioDeviceManager-enumerateaudioplaybackdevices) |Get a list of the audio playback device. When the audio playback device changes, you will receive `onAudioMediaDeviceStateChanged` and you need to call this API again to get the new device list. |
|[buildAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70095#buildaudioframe) |Create IAudioFrame |
|[setAudioSelectionConfig](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-setaudioselectionconfig) |Set the priority of the local audio stream to be published. |
|[setRemoteRoomAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-setremoteroomaudioplaybackvolume) |Adjusts the audio playback volume from all the remote users in a room. |
|[stopHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-stophardwareechodetection) |Stop the echo detection before joining a room. |
|[startHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-starthardwareechodetection) |Start echo detection before joining a room. |
|[enablePlaybackDucking](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-enableplaybackducking) |Enables/disables the playback ducking function. This function is usually used in scenarios where short videos or music will be played simultaneously during RTC calls.<br><br>With the function on, if remote voice is detected, the local media volume of RTC will be lowered to ensure the clarity of the remote voice. If remote voice disappears, the local media volume of RTC restores. |
|[enableVocalInstrumentBalance](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-enablevocalinstrumentbalance) |Enables/disables the loudness equalization function.<br><br>If you call this API with the parameter set to True, the loudness of user's voice will be adjusted to \-16lufs. If then you also call setAudioMixingLoudness and import the original loudness of the audio data used in audio mixing, the loudness will be adjusted to \-20lufs when the audio data starts to play. |
|[setRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setremoteaudioplaybackvolume) |Set the audio volume of playing the received remote stream. You must join the room before calling the API. The validity of the setting is not associated with the publishing status of the stream. |
|[enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-enableaudiopropertiesreport) |Enable audio information prompts. After that, you will receive [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onlocalaudiopropertiesreport), [onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onremoteaudiopropertiesreport), and [onActiveSpeaker](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onactivespeaker). |
|[enableExternalSoundCard](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-enableexternalsoundcard) |Enable the audio process mode for external sound card. |
|[getAudioDeviceManager](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-getaudiodevicemanager) |Device audio management interface creation |
|[enableAGC](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-enableagc) |Turns on/ off AAGC（Analog Automatic Gain Control）.<br><br>After AAGC is enabled, SDK can automatically adjust microphone pickup volume to keep the output volume at a steady level. |
|[setAudioProfile](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setaudioprofile) |Sets the sound quality. Call this API to change the sound quality if the audio settings in the current [RoomProfileType](https://docs.byteplus.com/en/docs/12/docs-70098#RoomProfileType) can not meet your requirements. |
|[stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-stopaudiocapture) |Stop internal audio capture. The default is off.<br><br>Internal audio capture refers to: capturing audio using the built\-in module.<br><br>The local client will be informed via [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onaudiodevicestatechanged) after stopping audio capture by calling this API.<br><br>.<br><br>The remote clients in the room will be informed of the state change via [onUserStopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onuserstopaudiocapture) after the visible client stops audio capture by calling this API.<br><br>. |
|[setPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setplaybackvolume) |Adjust the playback volume of the mixed remote audios. You can call this API before or during the playback. |
|[setCaptureVolume](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setcapturevolume) |Adjust the audio capture volume |
|[startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startaudiocapture) |Start internal audio capture. The default is off.<br><br>Internal audio capture refers to: capturing audio using the built\-in module.<br><br>The local client will be informed via [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onaudiodevicestatechanged) after starting audio capture by calling this API.<br><br>The remote clients in the room will be informed of the state change via [onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onuserstartaudiocapture) after the visible user starts audio capture by calling this API.. |



|Callback |Description |
|---|---|
|[onAudioStreamBanned](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onaudiostreambanned) |All the users in the room will get informed via this callback when a user is banned or the ban of the user has been lifted by calling BanUserStream/UnbanUserStream on the server side. |
|[onHardwareEchoDetectionResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onhardwareechodetectionresult) |Callback that notifies you the result of the echo detection before a call |
|[onStreamSyncInfoReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onstreamsyncinforeceived) |Audio stream synchronization information callback. You can use this callback to receive audio stream synchronization information sent remotely after the remote user calls [sendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-sendstreamsyncinfo) to send an audio stream synchronization message. |
|[onActiveSpeaker](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onactivespeaker) |After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-enableaudiopropertiesreport), you will periodically receive this callback for the active speaker information. |
|[onUserStopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onuserstopaudiocapture) |When a user in the room calls [stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-stopaudiocapture) to turn off audio capture, other users in the room will receive this callback. |
|[onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onuserstartaudiocapture) |Users in the room call [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startaudiocapture) When audio capture is turned on, other users in the room will receive this callback. |
|[onLocalAudioStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onlocalaudiostatechanged) |When the state of the local audio changes, the callback notifies the current local audio state. |
|[onAudioDeviceVolumeChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onaudiodevicevolumechanged) |Callback to notify you the volume of the audio device has been changed or when the device has been muted or unmuted. No need to activate the notification beforehand. |
|[onAudioPlaybackDeviceTestVolume](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onaudioplaybackdevicetestvolume) |Notification on the playing volume during the test for the local audio devices |
|[onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onremoteaudiopropertiesreport) |After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-enableaudiopropertiesreport), you will periodically receive this callback for the instantaneous information about the subscribed remote audio streams.<br><br>The remote audio streams includes the microphone audio and screen audio collected using the RTC SDK internal mechanism/custom mechanism. |
|[onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onlocalaudiopropertiesreport) |After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-enableaudiopropertiesreport), you will periodically receive this callback for the instantaneous information about local audio.<br><br>Local audio includes the microphone audio, the screen audio captured using RTC SDK internal mechanisms, and locally mixing audio. |
|[onAudioDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onaudiodevicewarning) |Audio device warning callback. The audio devices include audio capture devices and audio rendering devices. |
|[onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onaudiodevicestatechanged) |Callback of audio device state. Audio devices include audio capture devices and audio playback devices. |


<span id="video-management"></span>
## Video Management


|Method |Description |
|---|---|
|[startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startvideocapture) |Enable internal video capture immediately. The default is off.<br><br>Internal video capture refers to: use the RTC SDK built\-in video capture module to capture.<br><br>The local client will be informed via [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onvideodevicestatechanged) after starting video capture by calling this API.<br><br>The remote clients in the room will be informed of the state change via [onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onuserstartvideocapture) after the visible client starts video capture by calling this API. |
|[getVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoDeviceManager-getvideocapturedevice) |Get the video capture device information currently used by the SDK |
|[setVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoDeviceManager-setvideocapturedevice) |Set the current video capture device |
|[enumerateVideoCaptureDevices](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoDeviceManager-enumeratevideocapturedevices) |Get a list of video capture devices in the current system. |
|[buildEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70095#buildencodedvideoframe) |Create IEncodedVideoFrame |
|[setRemoteVideoConfig](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-setremotevideoconfig) |Sets your expected configuration of the remote video stream that you want to subscribe to or have subscribed to. |
|[setRemoteSimulcastStreamType](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-setremotesimulcaststreamtype) |Sets the type of the remote video stream to subscribe to. |
|[updateRemoteStreamVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-updateremotestreamvideocanvas) |Modifies remote video frame rendering settings, including render mode and background color. |
|[getVideoDeviceManager](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-getvideodevicemanager) |Create a video Facility Management instance |
|[updateRemoteStreamVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-updateremotestreamvideocanvas-2) |Modifies remote video frame rendering settings, including render mode, background color, and rotation angle, while using the internal rendering of the SDK. |
|[setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setremotevideocanvas) |Set the view and mode for rendering the specific video stream.<br><br>If you need to unbind the canvas for the video stream, set the canvas to `Null`. |
|[updateLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-updatelocalvideocanvas) |Update the render mode and background color of local video rendering |
|[setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setlocalvideocanvas) |Sets the view to be used for local video rendering and the rendering mode. |
|[disableAlphaChannelVideoEncode](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-disablealphachannelvideoencode) |Disables the Alpha channel encoding feature for custom captured video frames. |
|[enableAlphaChannelVideoEncode](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-enablealphachannelvideoencode) |Enables the Alpha channel encoding feature for custom capture video frames.<br><br>Suitable for scenarios where the video subject needs to be separated from the background at the push\-streaming end, and the background can be custom rendered at the receive\-streaming end. |
|[setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setvideoencoderconfig) |Sets the expected quality of the video stream by specifying the resolution, frame rate, bitrate, and the fallback strategy when the network is poor. |
|[setVideoCaptureConfig](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setvideocaptureconfig) |Set the video capture parameters for internal capture of the RTC SDK.<br><br>If your project uses the SDK internal capture module, you can specify the video capture parameters including preference, resolution and frame rate through this interface. |
|[stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-stopvideocapture) |Disable internal video capture immediately. The default is off.<br><br>Internal video capture refers to: use the RTC SDK built\-in video capture module to capture.<br><br>The local client will be informed via [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onvideodevicestatechanged) after stopping video capture by calling this API.<br><br>The remote clients in the room will be informed of the state change via [onUserStopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onuserstopvideocapture) after the visible client stops video capture by calling this API. |



|Callback |Description |
|---|---|
|[onP2PLocalExternalEncoderStop](https://docs.byteplus.com/en/docs/12/docs-70096#IStreamingRTCEventHandler-onp2plocalexternalencoderstop) |You will get informed of the stopping of the external video encoder.<br><br>For information on setting encoding configuration refer to [setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-setvideosourcetype). |
|[onLocalVideoStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onlocalvideostatechanged) |Receive this event when the state of the local video stream changes. |
|[onUserStopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onuserstopvideocapture) |The remote clients in the room will be informed of the state change via this callback after the visible user stops video capture by calling [stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-stopvideocapture).<br><br>If you don't start video capture before you publish video data, all visible user will receive this callback. |
|[onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onuserstartvideocapture) |The remote clients in the room will be informed of the state change via this callback after the visible user starts video capture by calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startvideocapture). |
|[onVideoDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onvideodevicewarning) |Video device warning callback. The video devices include video capture devices. |
|[onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onvideodevicestatechanged) |Callback of video device state. Video devices include cameras and screen sharing video capture devices. |
|[onFaceDetectResult](https://docs.byteplus.com/en/docs/12/docs-70096#IFaceDetectionObserver-onfacedetectresult) |Callback of the result of face detection with Effect SDK.<br><br>After calling [enableFaceDetection](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoEffect-enablefacedetection) and using the Effect SDK integrated in the RTC SDK, you will receive this callback. |
|[onP2PLocalExternalEncoderActiveVideoLayer](https://docs.byteplus.com/en/docs/12/docs-70096#IStreamingRTCEventHandler-onp2plocalexternalencoderactivevideolayer) |As the sender of a external encoded video stream, you will receive this callback at certain moments.<br><br>Based on the hints of this callback, you can selectively encode the video stream that is ready for transmission, in order to reduce the performance impact of video encoding on the local device. This callback is triggered based on a combination of factors, including the performance of the local device, the local network, and whether the stream is subscribed by the remote user. |
|[onP2PRequestLocalExternalEncoderKeyFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IStreamingRTCEventHandler-onp2prequestlocalexternalencoderkeyframe) |You will get informed of the request of the external video encoder for key frames.<br><br>For information on setting encoding configuration refer to [setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-setvideosourcetype). |
|[onP2PSuggestLocalExternalEncoderRateUpdate](https://docs.byteplus.com/en/docs/12/docs-70096#IStreamingRTCEventHandler-onp2psuggestlocalexternalencoderrateupdate) |You will get informed of the encoding\-bitrate change of the external video encoder.<br><br>For information on setting encoding configuration refer to [setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-setvideosourcetype). |


<span id="audio-video-transport"></span>
## Audio & Video Transport


|Method |Description |
|---|---|
|[requestRemoteVideoKeyFrame](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-requestremotevideokeyframe) |After subscribing to the remote video stream, request the key frame to the remote |
|[resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-resumeforwardstreamtoallrooms) |Call this method to resume relaying to all rooms from the pause by calling [pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-pauseforwardstreamtoallrooms). |
|[pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-pauseforwardstreamtoallrooms) |Call this method to pause relaying media stream to all rooms after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-startforwardstreamtorooms).<br><br>After that, call [resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-resumeforwardstreamtoallrooms) to resume. |
|[stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-stopforwardstreamtorooms) |Call to this method to stop relaying media stream to all rooms after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-startforwardstreamtorooms). |
|[updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-updateforwardstreamtorooms) |Update information of the rooms where you want to relay the media stream to after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-startforwardstreamtorooms).<br><br>Adding and removing rooms by calling this method will trigger [onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onforwardstreamstatechanged) on the local. |
|[startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-startforwardstreamtorooms) |Start relaying media stream across rooms.<br><br>After calling [joinRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-joinroom), you can call this method to publish the media stream to multiple rooms that applies to scenarios such as anOnline talent contest and so on. |
|[setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-setmultideviceavsync) |Synchronizes published audio and video.<br><br>When the same user simultaneously uses separate devices to capture and publish audio and video, there is a possibility that the streams are out of sync due to the network disparity. In this case, you can call this API on the video publisher side and the SDK will automatically line the video stream up according to the timestamp of the audio stream, ensuring that the audio the receiver hears corresponds to the video the receiver watches. |
|[resumeAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-resumeallsubscribedstreamaudio) |Resumes receiving all the audio streams of all remote users. |
|[resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-resumeallsubscribedstreamvideo) |Resumes receiving all the video streams of all remote users. |
|[pauseAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-pauseallsubscribedstreamaudio) |Pauses receiving the audio streams of all remote users. |
|[pauseAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-pauseallsubscribedstreamvideo) |Pauses receiving all the video streams of all remote users. |
|[subscribeAllStreamsAudio](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-subscribeallstreamsaudio) |Subscribes to or unsubscribes from all remote audio streams (by the microphone). |
|[subscribeAllStreamsVideo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-subscribeallstreamsvideo) |Subscribes to or unsubscribes from all remote video streams (by the camera). |
|[setStreamExtraInfo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-setstreamextrainfo) |Sets the stream extra info. |
|[subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-subscribestreamaudio) |Subscribes to or unsubscribes from the specific remote audio streams. |
|[subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-subscribestreamvideo) |Subscribes to or unsubscribes from the specific remote video stream. |
|[publishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-publishstreamaudio) |Publishes or stops publishing audio streams in the current room. |
|[publishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-publishstreamvideo) |Publishes or stops publishing video streams. |
|[setDummyCaptureImagePath](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setdummycaptureimagepath) |Set an alternative image when the local internal video capture is not enabled.<br><br>When you call `stopVideoCapture`, an alternative image will be pushed. You can set the path to null or open the camera to stop publishing the image.<br><br>You can repeatedly call this API to update the image. |



|Callback |Description |
|---|---|
|[onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onvideopublishstatechanged) |Callback on video\-stream state changes. |
|[onFirstLocalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onfirstlocalaudioframe) |Receive the callback when publishing local audio stream. |
|[onVideoFramePlayStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onvideoframeplaystatechanged) |Remote video stream first frame playback state change callback |
|[onAudioFramePlayStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onaudioframeplaystatechanged) |Audio first frame playback state change callback |
|[onFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onfirstremotevideoframedecoded) |The subscriber will receive this callback when the first frame of the receiving video stream begins to decode. The following situations are included:<br><br><br>&nbsp;<br><br>1. The publisher publishes video, including the initial publication and restart after cancellation. The publisher can cancel the video streaming proactively. Video streaming can also be cancelled by the publisher to stop publishing, leave the room or go offline.<br><br>2. After the publisher stops video capture, they restart it. When using an external source, this involves stopping the stream and then streaming again.<br><br>3. After the publisher publishes video, the subscriber cancels the subscription to video and then re\-subscribes to it. |
|[onFirstRemoteVideoFrameRendered](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onfirstremotevideoframerendered) |The subscriber will receive this callback when the first frame of the receiving video stream begins to render. The following situations are included:<br><br><br>&nbsp;<br><br>1. The publisher publishes video for the first time.<br><br>2. In 1, the publisher cancels the video streaming after publishing and publishes it again.<br><br>3. In 1, the publisher stops video capture after publishing and restarts it. (Or when using an external source, the stream is stopped and restarted again.)<br><br>4. In 1, the subscriber cancels the video streaming and subscribes to it again. (The interface includes [subscribeAllStreamsVideo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-subscribeallstreamsvideo), [pauseAllSubscribedStream](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-pauseallsubscribedstreamvideo)/[resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-resumeallsubscribedstreamvideo)) |
|[onVideoFrameSendStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onvideoframesendstatechanged) |Triggered when the local video stream first frame sending status changes. |
|[onAudioFrameSendStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onaudioframesendstatechanged) |Audio first frame sending status change callback |
|[onRemoteVideoStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onremotevideostatechanged) |When the state of a remote video stream changes, users in the room who subscribe to this stream receive the event. |
|[onRemoteAudioStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onremoteaudiostatechanged) |When the state of the audio stream from the remote user subscribes to changes, this callback will be received to understand the current state of the remote audio stream. |
|[onFirstRemoteAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onfirstremoteaudioframe) |The subscriber will receive this callback when the first frame of the receiving audio stream begins to decode. The following situations are included:<br><br><br>&nbsp;<br><br>1. The publisher publishes audio, including the initial publication and restart after cancellation.The publisher can cancel the audio streaming proactively. Audio streaming can also be cancelled by the publisher to stop publishing, leave the room or go offline.<br><br>2. After the publisher stops audio capture, they restart it. When using an external source, this involves stopping the stream and then streaming again.<br><br>3. After the publisher publishes audio, the subscriber cancels the subscription to audio and then re\-subscribes to it. |
|[onFirstLocalVideoFrameCaptured](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onfirstlocalvideoframecaptured) |RTC SDK receives this callback when the first video frame or screen video frame capture is completed locally. |
|[onRemoteVideoSizeChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onremotevideosizechanged) |Users in the room who subscribe to this video stream receive this callback when the remote video size or rotation configuration changes. |
|[onLocalVideoSizeChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onlocalvideosizechanged) |Receive this callback when the local video size or rotation configuration changes. |
|[onAVSyncEvent](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onavsyncevent) |Stream publisher will receive this callback when the A/V synchronization error occurs after [setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-setmultideviceavsync) is called. |
|[onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onnetworkquality) |Report the network quality of the users every 2s after the local user joins the room and starts publishing or subscribing to a stream. |
|[onForwardStreamEvent](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onforwardstreamevent) |Callback returning the events during relaying the media stream to each room |
|[onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onforwardstreamstatechanged) |Callback returning the state and errors during relaying the media stream to each of the rooms |
|[onAVSyncStateChange](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onavsyncstatechange) |Stream publisher will receive this callback when the A/V synchronization state changes after [setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-setmultideviceavsync) is called. |
|[onVideoStreamBanned](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onvideostreambanned) |All the users in the room will get informed via this callback when a user is banned or the ban of the user has been lifted by calling BanUserStream/UnbanUserStream on the server side. |
|[onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserpublishstreamaudio) |Callback on a remote user publishing or stopping publishing remote audio streams in the room. |
|[onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserpublishstreamvideo) |Callback on a remote user publishing or stopping publishing video streams in the room. |
|[onRemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onremotestreamstats) |Remote audio/video stream statistics and network quality callbacks for local subscriptions.<br><br>After the local user subscribes to the stream successfully, the SDK will periodically (2s) notify the user through this callback event of the quality statistics of the subscribed stream during this reference period, including: sending audio & video bit rate, sending frame rate, encoded frame rate, network quality, etc. |
|[onLocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onlocalstreamstats) |Local stream data statistics and network quality callback.<br><br>After the local user publishes the flow successfully, the SDK will periodically (2s) notify the user through this callback event of the quality statistics of the published flow during this reference period.<br><br>Statistics are passed to the user through the callback parameters of the [LocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-70098#LocalStreamStats) type, including the sent audio & video bit rate, sent frame rate, encoded frame rate, network quality, etc. |
|[onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onaudiosubscribestatechanged) |Callback on state changes of the subscription to microphone\-audio streams. |
|[onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onvideosubscribestatechanged) |Callback on state changes of the subscription to camera\-video streams. |
|[onAudioPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onaudiopublishstatechanged) |Triggered when local audio stream publishing status changes, or the local user joins the room. |


<span id="audio-processing"></span>
## Audio Processing


|Method |Description |
|---|---|
|[setVoiceChangerType](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setvoicechangertype) |Set the sound change effect type |
|[setLocalVoicePitch](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setlocalvoicepitch) |Change local voice to a different key, mostly used in Karaoke scenarios.<br><br>You can adjust the pitch of local voice such as ascending or descending with this method. |
|[enableLocalVoiceReverb](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-enablelocalvoicereverb) |Enable the reverb effect for the local captured voice. |
|[setLocalVoiceReverbParam](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setlocalvoicereverbparam) |Set the reverb effect for the local captured audio. The audio includes both internal captured audio and external captured voice, but not the mixing audio file. |
|[setLocalVoiceEqualization](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setlocalvoiceequalization) |Set the equalization effect for the local captured audio. The audio includes both internal captured audio and external captured voice, but not the mixing audio file. |
|[setVoiceReverbType](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setvoicereverbtype) |Set the reverb effect type |


<span id="video-processing"></span>
## Video Processing


|Method |Description |
|---|---|
|[initCVResource](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoEffect-initcvresource) |Checks video effect license, sets the video effect resource model path, and initializes video effect. |
|[setLowLightAdjusted](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setlowlightadjusted) |Sets the video lowlight enhancement mode.<br><br>It can significantly improve image quality in scenarios with insufficient light, contrast lighting, or backlit situations. |
|[clearVideoWatermark](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-clearvideowatermark) |Removes video watermark from designated video stream. |
|[setVideoWatermark](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setvideowatermark) |Adds watermark to designated video stream. |
|[stopVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-stopvideodigitalzoomcontrol) |Stop the ongoing digital zoom control instantly. |
|[startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startvideodigitalzoomcontrol) |Continuous and repeatedly digital zoom control. This action effect both the video preview locally and the stream published. |
|[setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setvideodigitalzoomcontrol) |Digital zoom or move the local video image once. This action affects both the video preview locally and the stream published. |
|[setVideoDigitalZoomConfig](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setvideodigitalzoomconfig) |Set the step size for each digital zooming control to the local videos. |
|[setBeautyIntensity](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setbeautyintensity) |Sets the beauty effect intensity. |
|[enableEffectBeauty](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-enableeffectbeauty) |Enables/Disables basic beauty effects. |
|[getVideoEffectInterface](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-getvideoeffectinterface) |Gets video effect interfaces. |
|[setRemoteVideoMirrorType](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setremotevideomirrortype) |When using internal rendering, enable mirroring for the remote stream. |
|[setLocalVideoMirrorType](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setlocalvideomirrortype) |Sets the mirror mode for the captured video stream. |
|[setVideoCaptureRotation](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setvideocapturerotation) |Set the rotation of the video images captured from the local device.<br><br>Call this API to rotate the videos when the camera is fixed upside down or tilted. |
|[disableFaceDetection](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoEffect-disablefacedetection) |Stops face detection. |
|[enableFaceDetection](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoEffect-enablefacedetection) |Starts face detection and registers the observer for the result.<br><br>With this observer, you will receive [onFaceDetectResult](https://docs.byteplus.com/en/docs/12/docs-70096#IFaceDetectionObserver-onfacedetectresult) periodically. |
|[disableVirtualBackground](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoEffect-disablevirtualbackground) |Turns off the virtual background. |
|[enableVirtualBackground](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoEffect-enablevirtualbackground) |Sets the original background to a specified image or a solid color. |
|[setColorFilterIntensity](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoEffect-setcolorfilterintensity) |Sets the intensity of the color filter enabled. |
|[setColorFilter](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoEffect-setcolorfilter) |Sets the color filter. |
|[updateEffectNode](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoEffect-updateeffectnode) |Sets the intensity of video effects. |
|[setEffectNodes](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoEffect-seteffectnodes) |Sets the video effects material package. |
|[disableVideoEffect](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoEffect-disablevideoeffect) |Disables video effects. |
|[enableVideoEffect](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoEffect-enablevideoeffect) |Enables video effects including beauty and color filters. |
|[freeAuthMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoEffect-freeauthmessage) |After using the authorization message string, free the memory. |
|[getAuthMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoEffect-getauthmessage) |Get authorization messages from the Effect SDK to obtain online licenses. |


<span id="custom-stream-processing"></span>
## Custom Stream Processing


|Method |Description |
|---|---|
|[setAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setaudiosourcetype) |Switch the audio capture type. |
|[processVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoProcessor-processvideoframe) |Get RTC SDK acquired video frames obtained, according to the video pre\-processor [registerLocalVideoProcessor](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-registerlocalvideoprocessor) set, video pre\-processing, the final processed video frames to the RTC SDK for encoding transmission. |
|[setRemoteVideoSink](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setremotevideosink) |Binds the remote video stream to a custom renderer. |
|[setLocalVideoSink](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setlocalvideosink) |Binds the local video stream to a custom renderer. |
|[setVideoDecoderConfig](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setvideodecoderconfig) |Before subscribing to the remote video stream, set the remote video data decoding method |
|[pushExternalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-pushexternalencodedvideoframe) |Push custom encoded video stream |
|[setExternalVideoEncoderEventHandler](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setexternalvideoencodereventhandler) |Register custom encoded frame push event callback |
|[registerRemoteEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-registerremoteencodedvideoframeobserver) |Video data callback after registering remote encoding.<br><br>After registration, when the SDK detects a remote encoded video frame, it will trigger the [onRemoteEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IRemoteEncodedVideoFrameObserver-onremoteencodedvideoframe) callback |
|[registerLocalEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-registerlocalencodedvideoframeobserver) |Register a local video frame observer.<br><br>This method applys to both internal capturing and custom capturing.<br><br>After calling this API, SDK triggers [onLocalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70096#ILocalEncodedVideoFrameObserver-onlocalencodedvideoframe) whenever a video frame is captured. |
|[registerLocalVideoProcessor](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-registerlocalvideoprocessor) |Set up a custom video preprocessor.<br><br>Using this video preprocessor, you can call [processVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoProcessor-processvideoframe) to preprocess the video frames collected by the RTC SDK, and use the processed video frames for RTC audio & video communication. |
|[disableAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-disableaudioprocessor) |Disable custom audio processing. |
|[enableAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-enableaudioprocessor) |Enable audio frames callback for custom processing and set the format for the specified type of audio frames. |
|[registerAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-registeraudioprocessor) |Register a custom audio preprocessor.<br><br>After that, you can call [enableAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-enableaudioprocessor) to process the audio streams that either captured locally or received from the remote side. RTC SDK then encodes or renders the processed data. |
|[registerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-registeraudioframeobserver) |Register an audio frame observer. |
|[disableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-disableaudioframecallback) |Disables audio data callback. |
|[enableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-enableaudioframecallback) |Enable audio frames callback and set the format for the specified type of audio frames. |
|[pushExternalVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-pushexternalvideoframe) |Pushes external video frames. |
|[setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setvideosourcetype) |Set the video source, including the screen recordings.<br><br>The internal video capture is the default, which refers to capturing video using the built\-in module. |
|[pushReferenceAudioPCMData](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-pushreferenceaudiopcmdata) |Push custom aec reference audio data to the RTC SDK. |
|[setRemoteVideoSink](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setremotevideosink-2) |Binds the remote video stream to a custom renderer.You can get video frame data at specified positions and formats through parameter settings. |
|[setLocalVideoSink](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setlocalvideosink-2) |Binds the local video stream to a custom renderer.You can get video frame data at specified positions and formats through parameter settings. |
|[pullExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-pullexternalaudioframe) |Pull remote audio data. You can use the data for audio processing or custom rendering.<br><br>After calling this method, the SDK will actively pull the audio data that is ready to be played, including the decoded and mixed audio data from remote end for external playback. |
|[pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-pushexternalaudioframe) |Push custom captured audio data to the RTC SDK. |
|[setAudioRenderType](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setaudiorendertype) |Switch the audio render type. |



|Callback |Description |
|---|---|
|[onRemoteEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IRemoteEncodedVideoFrameObserver-onremoteencodedvideoframe) |Call [registerRemoteEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-registerremoteencodedvideoframeobserver), the callback is triggered when the SDK detects the remote encoded video data |
|[onLocalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70096#ILocalEncodedVideoFrameObserver-onlocalencodedvideoframe) |After calling [registerLocalEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-registerlocalencodedvideoframeobserver), SDK will trigger this callback when it receives local video frames. |
|[onProcessRemoteUserAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioFrameProcessor-onprocessremoteuseraudioframe) |Returns the address of the locally captured audio frame for custom processing. |
|[onProcessPlayBackAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioFrameProcessor-onprocessplaybackaudioframe) |Returns the address of the locally captured audio frame for custom processing. |
|[onProcessRecordAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioFrameProcessor-onprocessrecordaudioframe) |Returns the address of the locally captured audio frame for custom processing. |
|[onAudioFileFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioFileFrameObserver-onaudiofileframe) |The callback for the audio frames during local audio file mixing. |
|[onCaptureMixedAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioFrameObserver-oncapturemixedaudioframe) |Return the mixed audio data of the data recorded by local microphone and the audio data of `MediaPlayer` and `EffectPlayer`. |
|[onRecordScreenAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioFrameObserver-onrecordscreenaudioframe) |Returns the audio data played locally |
|[onMixedAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioFrameObserver-onmixedaudioframe) |Returns mixed audio data including both data recorded by the local microphone and data from all subscribed remote users |
|[onRemoteUserAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioFrameObserver-onremoteuseraudioframe) |Returns the audio data of one remote user. |
|[onPlaybackAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioFrameObserver-onplaybackaudioframe) |Returns the mixed audio data of all subscribed remote users |
|[onRecordAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioFrameObserver-onrecordaudioframe) |Returns audio data recorded by microphone |
|[onActiveVideoLayer](https://docs.byteplus.com/en/docs/12/docs-70096#IExternalVideoEncoderEventHandler-onactivevideolayer) |As the sender of a external encoded video stream, you will receive this callback at certain moments.<br><br>Based on the hints of this callback, you can selectively encode the video stream that is ready for transmission, in order to reduce the performance impact of video encoding on the local device. This callback is triggered based on a combination of factors, including the performance of the local device, the local network, and whether the stream is subscribed by the remote user. |
|[onRequestKeyFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IExternalVideoEncoderEventHandler-onrequestkeyframe) |This callback is used to inform the stream publisher that a keyframe needs to be regenerated. |
|[onRateUpdate](https://docs.byteplus.com/en/docs/12/docs-70096#IExternalVideoEncoderEventHandler-onrateupdate) |When the frame rate or bit rate of a custom encoded stream changes, the callback is triggered |
|[onStop](https://docs.byteplus.com/en/docs/12/docs-70096#IExternalVideoEncoderEventHandler-onstop) |When you receive the callback, you need to stop pushing custom encoded video frames to the SDK |
|[onStart](https://docs.byteplus.com/en/docs/12/docs-70096#IExternalVideoEncoderEventHandler-onstart) |Prompt custom encoded frames to start pushing callbacks.<br><br>After receiving this callback, you can call [pushExternalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-pushexternalencodedvideoframe) to push a custom encoded video frame to the SDK |


<span id="network-processing"></span>
## Network Processing


|Method |Description |
|---|---|
|[setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setlocalsimulcastmode) |Enable the Simulcast feature and configure the lower\-quality video streams settings. |
|[getNetworkTimeInfo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-getnetworktimeinfo) |Obtain the synchronization network time information. |
|[stopEchoTest](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-stopechotest) |Stop the current call test.<br><br>After calling [startEchoTest](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startechotest), you must call this API to stop the test. |
|[startEchoTest](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startechotest) |Starts a call test.<br><br>Before entering the room, you can call this API to test whether your local audio/video equipment as well as the upstream and downstream networks are working correctly.<br><br>Once the test starts, SDK will record your sound or video. If you receive the playback within the delay range you set, the test is considered normal. |
|[stopNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-stopnetworkdetection) |Stop pre\-call network probe |
|[startNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startnetworkdetection) |Pre\-call network detection |
|[setRemoteUserPriority](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setremoteuserpriority) |Set user priority |
|[setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setsubscribefallbackoption) |Sets the fallback option for subscribed RTC streams.<br><br>You can call this API to set whether to lower the resolution of currently subscribed stream under limited network conditions. |
|[setPublishFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setpublishfallbackoption) |Sets the fallback option for published audio & video streams.<br><br>You can call this API to set whether to automatically lower the resolution you set of the published streams under limited network conditions. |
|[setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setlocalsimulcastmode-2) |Enable the Simulcast feature. |



|Callback |Description |
|---|---|
|[onConnectionStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onconnectionstatechanged) |SDK connection state change callback with signaling server. Triggered when the connection state changes. |
|[onNetworkTimeSynchronized](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onnetworktimesynchronized) |After calling [getNetworkTimeInfo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-getnetworktimeinfo) for the first time, the SDK starts network time synchronization internally. This callback will be triggered when the synchronization is completed. |
|[onEchoTestResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onechotestresult) |Callback about the call test result. |
|[onNetworkDetectionStopped](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onnetworkdetectionstopped) |Pre\-call network probing ends<br><br>The following will stop detection and receive this primary callback:<br><br><br>&nbsp;<br><br>1. This callback is received once when the [stopNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-stopnetworkdetection) interface is called to stop probing;<br><br>2. Stop detection when the first frame of remote/local audio is received;<br><br>3. Stop detecting when the detection exceeds 3 minutes;<br><br>4. When the probe link is disconnected for a certain period of time, the probe is stopped. |
|[onNetworkDetectionResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onnetworkdetectionresult) |Pre\-call network detection result.<br><br>After successfully calling [startNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startnetworkdetection), you will receive this callback for the first time in 3s and every 2s thereafter. |
|[onSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onseimessagereceived) |Receive this callback when you receive a video frame with a SEI message sent via [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-sendseimessage) |
|[onPerformanceAlarms](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onperformancealarms) |When the publish performance fallback [setPublishFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setpublishfallbackoption) is not turned on locally, and when insufficient device performance is detected, this callback is received.<br><br>When the publish performance fallback [setPublishFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setpublishfallbackoption) is locally turned on, and when the publish performance fallback/recovery is caused due to device performance/network reasons, this callback is received. |
|[onSimulcastSubscribeFallback](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onsimulcastsubscribefallback) |This callback is triggered when media streams start to fall back or restore from a fallback. |
|[onNetworkTypeChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onnetworktypechanged) |SDK Current network connection type change callback. Callbacks the event when the current network connection type of the SDK changes. |


<span id="messaging"></span>
## Messaging


|Method |Description |
|---|---|
|[sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-sendseimessage) |<span id="IRTCEngine\-sendseimessage\-2"\></span\> Sends SEI data.<br><br>In a video call scenario, SEI is sent with the video frame, while in a voice call scenario, SDK will automatically publish a black frame with a resolution of 16 × 16 pixels to carry SEI data.<br><br>&nbsp;<br><br>In a voice call, you should set this parameter to `kStreamIndexMain`, otherwise the SEI data is discarded and cannot be sent to the remote user. |
|[sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-senduserbinarymessage) |Sends a binary message (P2P) to the specified user in the room |
|[sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-sendusermessage) |Send a text message (P2P) to the specified user in the room |
|[sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-sendroombinarymessage) |Send broadcast messages to all other users in the room. |
|[sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-sendroommessage) |Send broadcast messages to all other users in the room. |
|[sendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-sendstreamsyncinfo) |Send audio stream synchronization information. The message is sent to the remote end through the audio stream and synchronized with the audio stream. After the interface is successfully called, the remote user will receive a [onStreamSyncInfoReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onstreamsyncinforeceived) callback. |
|[sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-sendserverbinarymessage) |Client side sends binary messages to the application server (P2Server) |
|[sendServerMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-sendservermessage) |The client side sends a text message to the application server (P2Server) |
|[sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-senduserbinarymessageoutsideroom) |Send binary messages (P2P) to a specified user outside the room |
|[sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-sendusermessageoutsideroom) |Send a text message (P2P) to a specified user outside the room |
|[getPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-getpeeronlinestatus) |Query the login status of the opposite or local user |
|[setServerParams](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setserverparams) |Set application server parameters<br><br>Client side calls [sendServerMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-sendservermessage) or [sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-sendserverbinarymessage) Before sending a message to the application server, a valid signature and application server address must be set. |
|[updateLoginToken](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-updatelogintoken) |Update the Token<br><br>Token used by the user to log in has a certain valid period. When the Token expires, you need to call this method to update the login Token information.<br><br>When calling the [login](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-login) method to log in, if an expired token is used, the login will fail and you will receive an [onLoginResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onloginresult) callback notification with an error code of kLoginErrorCodeInvalidToken. You need to reacquire the token and call this method to update the token. |
|[logout](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-logout) |Log out of RTS server.<br><br>Calls this interface to log out, it is impossible to call methods related to out\-of\-room messages and end\-to\-server messages or receive related callbacks. |
|[login](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-login) |Log in to RTS server.<br><br>Log in to call [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-sendusermessageoutsideroom) and [sendServerMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-sendservermessage) to send P2P messages or send messages to a server without joining the RTC room.<br><br>To log out, call [logout](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-logout). |
|[sendLivePushSEIMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-sendlivepushseimessage) |Sends SEI data in Key\-Value format through video frames.<br><br>Before calling this API, you must call [setLiveMode](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-setlivemode) and set the room live mode to `kRoomLiveModeSoloHost`. |



|Callback |Description |
|---|---|
|[onP2PMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70096#IStreamingRTCEventHandler-onp2pmessagesendresult) |Callback of message\-sending result. You will get informed after calling [sendP2PMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-sendp2pmessage) or [sendP2PBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-sendp2pbinarymessage). |
|[onSEIStreamUpdate](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onseistreamupdate) |Callback about publishing status of the black frame video stream .<br><br>In a voice call scenario, when the local user calls [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-sendseimessage) to send SEI data with a black frame, the sending status of the stream is notified to the remote user through this callback.<br><br>You can tell from this callback that the video frame carrying SEI data is a black frame and thus not render that video frame. |
|[onServerMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onservermessagesendresult) |Receives the callback after sending the message to the application server successfully. |
|[onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom-2) |This callback is triggered when a binary message is received from a user outside the room who calls [sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-senduserbinarymessageoutsideroom). |
|[onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onusermessagereceivedoutsideroom-2) |Triggered when you receive a text message from a user outside the room by calling [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-sendusermessageoutsideroom). |
|[onUserMessageSendResultOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onusermessagesendresultoutsideroom) |Callback for the result of sending a message to a user outside the room.<br><br>Triggered after sending a message to a user outside the room via [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-sendusermessageoutsideroom) or [sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-senduserbinarymessageoutsideroom). |
|[onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom) |\> This callback will be deprecated in version 3.64. Please use [onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom-2) instead.<br><br>Triggered when a binary message is received from a user outside the room who called [sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-senduserbinarymessageoutsideroom). |
|[onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onusermessagereceivedoutsideroom) |\> This interface will be deprecated in version 3.64. Please use [onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onusermessagereceivedoutsideroom-2) instead.<br><br>Triggered when a text message is received from a user outside the room who called [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-sendusermessageoutsideroom). |
|[onGetPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-ongetpeeronlinestatus) |The return result of querying the login status of the peer or local user |
|[onServerParamsSetResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onserverparamssetresult) |Set the return result of the application server parameter |
|[onLogout](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onlogout) |Callback of logout result |
|[onLoginResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onloginresult) |login result callback |
|[onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onuserbinarymessagereceived-2) |A single user receives a callback (P2P) of binary messages from other uid\-owned users in the same room. |
|[onUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onusermessagereceived-2) |Receive this callback when you receive a text message (P2P) from another user in the room. |
|[onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroombinarymessagereceived-2) |Receives a callback to a binary broadcast message in the room. |
|[onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroommessagereceived-2) |Callback for receiving room messages.<br><br>Other users in the same room will receive this callback when they call [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-sendusermessage) to send a broadcast message. |
|[onUserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onusermessagesendresult) |After sending a text or binary message (P2P) to a single user in the room, the message sender receives a callback with the result of the message. |
|[onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onuserbinarymessagereceived) |A single user receives a callback (P2P) of binary messages from other uid\-owned users in the same room.<br><br>\> The callback will be deprecated in version 3.64. Please use [onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onuserbinarymessagereceived-2) instead. |
|[onUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onusermessagereceived) |\> The interface will be deprecated in version 3.64. Please use [onUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onusermessagereceived-2) instead.<br><br>Receive this callback when you receive a text message (P2P) from another user in the room. |
|[onRoomMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroommessagesendresult) |When the [sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-sendroommessage) function is called to send a message, the sending result of this message (feedback) is called back. |
|[onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroombinarymessagereceived) |Receives a callback to a binary broadcast message in the room. |
|[onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroommessagereceived) |Receives a callback for broadcast messages in the room. |
|[onP2PBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IStreamingRTCEventHandler-onp2pbinarymessagereceived) |Callback of point\-to\-point binary message. You will get informed of the message contents via this callback when you receive a P2P binary message. |
|[onP2PMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IStreamingRTCEventHandler-onp2pmessagereceived) |Callback of point\-to\-point text message. You will get informed of the message contents via this callback when you receive a P2P text message. |


<span id="push-to-cdn-wtn"></span>
## Push to CDN/WTN


|Method |Description |
|---|---|
|[stopPushSingleStream](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-stoppushsinglestream) |Stops the task started via [startPushSingleStream](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startpushsinglestream).<br><br>This method stops pushing a single stream to CDN. |
|[startPushSingleStream](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startpushsinglestream) |Pushes a single media stream to CDN or RTC room. |
|[stopPushMixedStream](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-stoppushmixedstream) |Stops the task started via [startPushMixedStream](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startpushmixedstream). |
|[updatePushMixedStream](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-updatepushmixedstream) |Update the task configuration during the task started via [startPushMixedStream](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startpushmixedstream). You will be informed of the change via the [onMixedStreamEvent](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onmixedstreamevent) callback. |
|[startPushMixedStream](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startpushmixedstream) |Specify the streams to be mixed and initiates the task to push the mixed stream to CDN or WTN. |
|[subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-70095#IWTNStream-subscribewtnvideostream) |Subscribe/ unsubscribe WTN video stream<br><br>A user can call this method to subscribe or unsubscribe a WTN stream whether he/she has joined the room or not. |
|[getWTNStream](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-getwtnstream) |Gets the WTN stream object.<br><br>You can use this method to get the WTN stream object to implement custom video rendering and processing.<br><br>You must call enableWTNStream to enable the WTN stream before calling this method. |
|[subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-70095#IWTNStream-subscribewtnaudiostream) |Subscribe/unsubscribe the WTN audio stream<br><br>A user can call this method to subscribe a WTN stream whether he/she has joined the room or not. |
|[setWTNRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70095#IWTNStream-setwtnremotevideocanvas) |Assign a internal render view to the WTN stream |
|[setWTNRemoteVideoSink](https://docs.byteplus.com/en/docs/12/docs-70095#IWTNStream-setwtnremotevideosink) |Assign a custom renderer to the WTN stream. See [Custom Video Rendering](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-81201) |
|[setWTNRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-70095#IWTNStream-setwtnremoteaudioplaybackvolume) |Set the audio playback volume of the WTN stream. |
|[setWTNStreamEventHandler](https://docs.byteplus.com/en/docs/12/docs-70095#IWTNStream-setwtnstreameventhandler) |Set the WTN event handler. |



|Callback |Description |
|---|---|
|[onMixedStreamEvent](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onmixedstreamevent) |Reports events during pushing a mixed stream to CDN or a WTN stream. |
|[onSingleStreamEvent](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onsinglestreamevent) |Reports events during pushing a single stream to CDN |
|[onWTNRemoteVideoStats](https://docs.byteplus.com/en/docs/12/docs-70096#IWTNStreamEventHandler-onwtnremotevideostats) |Remote WTN video stream ID and statistics. |
|[onWTNRemoteAudioStats](https://docs.byteplus.com/en/docs/12/docs-70096#IWTNStreamEventHandler-onwtnremoteaudiostats) |Remote WTN audio stream ID and statistics. |
|[onWTNVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IWTNStreamEventHandler-onwtnvideosubscribestatechanged) |Callback for the change of WTN video stream's subscription status<br><br>You will be informed of the result of subscribing to the WTN video stream by this callback after calling [subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-70095#IWTNStream-subscribewtnvideostream). |
|[onWTNAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IWTNStreamEventHandler-onwtnaudiosubscribestatechanged) |Callback for the change of WTN audio stream's subscription status<br><br>You will be informed of the result of subscribing to the WTN audio stream by this callback after calling [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-70095#IWTNStream-subscribewtnaudiostream). |
|[onWTNFirstRemoteAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IWTNStreamEventHandler-onwtnfirstremoteaudioframe) |Callback of successfully decoding of the first audio frame of the WTN stream.<br><br>Refer to [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-70095#IWTNStream-subscribewtnaudiostream) for details about subscribing to a WTN audio stream. |
|[onWTNFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-70096#IWTNStreamEventHandler-onwtnfirstremotevideoframedecoded) |Callback of successfully decoding of the first video frame of the WTN stream<br><br>Refer to [subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-70095#IWTNStream-subscribewtnvideostream) for details about subscribing to a WTN video stream. |
|[onWTNSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IWTNStreamEventHandler-onwtnseimessagereceived) |Callback on receiving the SEI message carried by the WTN stream.<br><br>After calling [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-70095#IWTNStream-subscribewtnaudiostream)/[subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-70095#IWTNStream-subscribewtnvideostream), you will receive this callback if the WTN stream has an SEI message. |
|[onWTNDataMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IWTNStreamEventHandler-onwtndatamessagereceived) |The data information contained in the callback of WTN stream..<br><br>After calling [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-70095#IWTNStream-subscribewtnaudiostream)/[subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-70095#IWTNStream-subscribewtnvideostream), you can listen to this callback and retrieve SEI messages inserted by Open API calls or audio volume. |


<span id="audio-mixing"></span>
## Audio Mixing


|Method |Description |
|---|---|
|[getAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-getaudioeffectplayer) |Create an instance for audio effect player. |
|[setEventHandler](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioEffectPlayer-seteventhandler) |Set the event handler. |
|[getDuration](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioEffectPlayer-getduration) |Get the duration of the audio effect file. |
|[getVolume](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioEffectPlayer-getvolume) |Gets the current volume. |
|[setVolumeAll](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioEffectPlayer-setvolumeall) |Sets the volume of all audio effect, including audio effect files and PCM effects. |
|[setVolume](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioEffectPlayer-setvolume) |Adjusts the volume level of a specified audio effect, including audio effect file and PCM effect. |
|[getPosition](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioEffectPlayer-getposition) |Gets the current position of audio effect file playback. |
|[setPosition](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioEffectPlayer-setposition) |Sets the start position of the audio effect file. |
|[resumeAll](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioEffectPlayer-resumeall) |Resumes the playback of all audio effect files. |
|[resume](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioEffectPlayer-resume) |Resumes the playback of audio effect files. |
|[pauseAll](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioEffectPlayer-pauseall) |Pauses the Playback of all audio effect files. |
|[pause](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioEffectPlayer-pause) |Pauses the playback of audio effect files. |
|[unloadAll](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioEffectPlayer-unloadall) |Unloads all audio effect files. |
|[unload](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioEffectPlayer-unload) |Unloads the specified audio effect file. |
|[preload](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioEffectPlayer-preload) |Preloads specified music files into memory to avoid repeated loading when playing the same file frequently and reduce CPU usage. |
|[stopAll](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioEffectPlayer-stopall) |Stops playback of all audio effect files. |
|[stop](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioEffectPlayer-stop) |Stops the playback of audio effect files. |
|[start](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioEffectPlayer-start) |Starts to play the audio effect file.<br><br>This API can be called multiple times with different IDs and filepaths for multiple effects at the same time. |
|[setEventHandler](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-seteventhandler) |Set the event handler. |
|[pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-pushexternalaudioframe) |Push PCM audio frame data for mixing. |
|[registerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-registeraudioframeobserver) |Register an observer to receive related callbacks when the local media file is mixing. |
|[setLoudness](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-setloudness) |To call [enableVocalInstrumentBalance](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-enablevocalinstrumentbalance) to adjust the volume of the mixed media file or the PCM audio data, you must pass in its original loudness through this API. |
|[setProgressInterval](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-setprogressinterval) |Set the interval of the periodic callback [onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-70096#IMediaPlayerEventHandler-onmediaplayerplayingprogress) during audio mixing. |
|[setPlaybackSpeed](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-setplaybackspeed) |Set the playback speed of the audio file. |
|[selectAudioTrack](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-selectaudiotrack) |Specifies the playback track of the current media file. |
|[getAudioTrackCount](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-getaudiotrackcount) |Gets the track count of the current media file. |
|[setAudioDualMonoMode](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-setaudiodualmonomode) |Sets the channel mode of the mixing of the media file. |
|[setPosition](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-setposition) |Sets the starting playback position of the media file. |
|[setAudioPitch](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-setaudiopitch) |Set the pitch of the local audio file mixing. Usually used in karaoke scenes. |
|[getState](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-getstate) |Get the state of the media player. |
|[getPosition](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-getposition) |Gets the playback progress of the media file. |
|[getPlaybackDuration](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-getplaybackduration) |Gets the actual playback duration of the mixed media file, in milliseconds. |
|[getTotalDuration](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-gettotalduration) |Gets the duration of the media file. |
|[getVolume](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-getvolume) |Gets the current volume. |
|[setVolume](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-setvolume) |Adjusts the volume of the specified audio mixing, including media file mixing and PCM mixing. |
|[resume](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-resume) |After calling [pause](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-pause) to pause audio mixing, call this API to resume audio mixing. |
|[pause](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-pause) |After calling [open](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-open), or [start](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-start) to start audio mixing, call this API to pause audio mixing. |
|[stop](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-stop) |After calling [open](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-open), [start](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-start), or [openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-openwithcustomsource) to start audio mixing, call this method to stop audio mixing. |
|[openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-openwithcustomsource) |Enable audio mixing with audio raw data.<br><br>To open the audio file, see [open](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-open). `open` and this API are mutually exclusive. |
|[start](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-start) |Start playing the audio. Call this API when you call [open](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-open) and set `AutoPlay=False`. |
|[open](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-open) |Open the audio file.<br><br>You can only open one audio file with one player instance at the same time. For multiple audio files at the same time, create multiple player instances.<br><br>For audio file in PCM format, see [openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-openwithcustomsource). `openWithCustomSource` and this API are mutually exclusive. |
|[getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-getmediaplayer) |Create a media player instance. |



|Callback |Description |
|---|---|
|[onAudioEffectPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioEffectPlayerEventHandler-onaudioeffectplayerstatechanged) |Callback for audio mixing status change. |
|[onAudioMixingPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onaudiomixingplayingprogress) |Callback for playback progress of mixed audio files |
|[onMediaPlayerEvent](https://docs.byteplus.com/en/docs/12/docs-70096#IMediaPlayerEventHandler-onmediaplayerevent) |Callback for media player events. You would receive the notification after calling [selectAudioTrack](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-selectaudiotrack) and [setPosition](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-setposition). |
|[onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-70096#IMediaPlayerEventHandler-onmediaplayerplayingprogress) |Periodic callback for audio mixing progress. The period is set by [setProgressInterval](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-setprogressinterval). |
|[onMediaPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IMediaPlayerEventHandler-onmediaplayerstatechanged) |Callback for audio mixing status change. |
|[onSeek](https://docs.byteplus.com/en/docs/12/docs-70096#IMediaPlayerCustomSourceProvider-onseek) |Seeking the audio data based on the set starting position and offset to help SDK read and analyze data.<br><br>When you call [openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-openwithcustomsource) API to play the in\-memory audio data you input, or when you call [setPosition](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-setposition) to set the starting position of audio playing, this callback will be trigerred and you need to seek the audio data accorring to the value of offset and whence. |
|[onReadData](https://docs.byteplus.com/en/docs/12/docs-70096#IMediaPlayerCustomSourceProvider-onreaddata) |Callback of getting the path and size of the audio data you input.<br><br>When you call [openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-70095#IMediaPlayer-openwithcustomsource) API to play the in\-memory audio data you input, this callback will be triggered and you need to enter the path and size of the audio data. |
|[onFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IMediaPlayerAudioFrameObserver-onframe) |The callback for the audio frames during local audio file mixing. |


<span id="screen-sharing"></span>
## Screen Sharing


|Method |Description |
|---|---|
|[muteScreenAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-mutescreenaudiocapture) |Mutes/unmutes the audio captured when screen sharing.<br><br>Calling this method will send muted data instead of the screen audio data, and it does not affect the local audio device capture status and the SDK audio stream publishing status. |
|[release](https://docs.byteplus.com/en/docs/12/docs-70095#IScreenCaptureSourceList-release) |If you are finished with the [IScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/docs-70095#IScreenCaptureSourceList), call this API to destruct it and release the memory. |
|[getSourceInfo](https://docs.byteplus.com/en/docs/12/docs-70095#IScreenCaptureSourceList-getsourceinfo) |According to the index, get the elements in the screen share list |
|[getCount](https://docs.byteplus.com/en/docs/12/docs-70095#IScreenCaptureSourceList-getcount) |Get the length of the list |
|[pushScreenAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-pushscreenaudioframe) |Using a custom capture method, when capturing screen audio during screen sharing, push the audio frame to the RTC SDK for encoding and other processing. |
|[stopScreenAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-stopscreenaudiocapture) |Stop RTC SDK's device audio recorder. |
|[startScreenAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startscreenaudiocapture-2) |When sharing the screen, start using RTC SDK internal collection method to collect screen audio. |
|[setScreenAudioChannel](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setscreenaudiochannel) |Set the audio channel of the screen\-sharing audio stream |
|[setScreenAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setscreenaudiosourcetype) |Set the screen audio acquisition method (internal acquisition/custom acquisition) |
|[getWindowAppIcon](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-getwindowappicon) |Get application window preview thumbnail for screen sharing. |
|[getThumbnail](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-getthumbnail) |Get the preview thumbnail of the screen\-sharing object |
|[getScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-getscreencapturesourcelist) |Get the item list for screen sharing. |
|[updateScreenCaptureFilterConfig](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-updatescreencapturefilterconfig) |When capturing screen video streams through the capture module provided by the RTC SDK, set the window that needs to be filtered. |
|[updateScreenCaptureMouseCursor](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-updatescreencapturemousecursor) |Update the processing settings for the mouse when capturing screen video streams through the capture module provided by the RTC SDK. Default acquisition mouse. |
|[updateScreenCaptureHighlightConfig](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-updatescreencapturehighlightconfig) |Update border highlighting settings when capturing screen video streams through the capture module provided by the RTC SDK. The default display table box. |
|[stopScreenVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-stopscreenvideocapture) |Stop screen video streaming. |
|[startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startscreenvideocapture) |Capture screen video stream for sharing. Screen video stream includes: content displayed on the screen, in the application window, or in the virtual screen.<br><br>Displaying contents in virtual screens is only available on Windows. |
|[updateScreenCaptureRegion](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-updatescreencaptureregion) |Update the capture area when capturing screen video streams through the capture module provided by the RTC SDK. Only used when the capture source is the monitor screen. |
|[setScreenCaptureVolume](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setscreencapturevolume) |Adjusts the volume of audio captured during screen sharing.<br><br>This method only changes the volume of audio data and does not affect the hardware volume of the local device. |



|Callback |Description |
|---|---|
|[onProcessScreenAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioFrameProcessor-onprocessscreenaudioframe) |Returns the address of the shared\-screen audio frames for custom processing. |


<span id="security-and-encryption"></span>
## Security and Encryption


|Method |Description |
|---|---|
|[setEncryptInfo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setencryptinfo) |Sets the way to use built\-in encryption when transmitting. |
|[setLocalProxy](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setlocalproxy) |Sets local proxy. |
|[stopCloudProxy](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-stopcloudproxy) |Stop cloud proxy |
|[startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startcloudproxy) |Start cloud proxy |
|[setCustomizeEncryptHandler](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setcustomizeencrypthandler) |Sets custom encryption and decryption methods. |



|Callback |Description |
|---|---|
|[onEncryptData](https://docs.byteplus.com/en/docs/12/docs-70096#IEncryptHandler-onencryptdata) |Custom encryption.<br><br>Encrypts audio & video frame data before transmission using the custom encryption method set.<br><br>Encryption of the original audio and video frames is currently not available. |
|[onLocalProxyStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onlocalproxystatechanged) |Callback on local proxy connection. After calling [setLocalProxy](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setlocalproxy) to set local proxies, you will receive this callback that informs you of the states of local proxy connection. |
|[onCloudProxyConnected](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-oncloudproxyconnected) |Receives the callback when you call [startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startcloudproxy) to start cloud proxy, and the SDK connects the proxy server successfully. |
|[onDecryptData](https://docs.byteplus.com/en/docs/12/docs-70096#IEncryptHandler-ondecryptdata) |Custom decryption.<br><br>Decrypts custom encrypted audio & video frame data. For custom encryption, see [onEncryptData](https://docs.byteplus.com/en/docs/12/docs-70096#IEncryptHandler-onencryptdata). |


<span id="advanced-features"></span>
## Advanced Features


|Method |Description |
|---|---|
|[enableRangeAudio](https://docs.byteplus.com/en/docs/12/docs-70095#IRangeAudio-enablerangeaudio) |Enable/disable the range audio function.<br><br>Range audio means that within a certain range in a same RTC room, the audio volume of the remote user received by the local user will be amplified/attenuated as the remote user moves closer/away. The audio coming from out of the range cannot be heard. See [updateReceiveRange](https://docs.byteplus.com/en/docs/12/docs-70095#IRangeAudio-updatereceiverange) to set audio receiving range. |
|[setReportExtraInfo](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-setreportextrainfo) |Set extra_info of trace. |
|[requestRemoteVideoKeyFrame](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-requestremotevideokeyframe) |After subscribing to the remote video stream, request the key frame to the remote |
|[pushEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-pushencodedvideoframe) |Push video stream encoded with the external encoder. |
|[pushVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-pushvideoframe) |Send external\-source video data |
|[setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-setvideosourcetype) |Set the video source of the StreamingEngine.<br><br>The internal video capture is the default video source, which refers to capturing video using the built\-in module. |
|[setVideoSourceHWDeviceContext](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-setvideosourcehwdevicecontext) |Set the device context information of the video source |
|[setVideoDecoderConfig](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-setvideodecoderconfig) |Set decoding options for remote video data<br><br>Call this API before calling [startup](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-startup). |
|[setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-setvideoencoderconfig) |Sets the video encoder configuration of each individual stream for simulcasting, including resolution, frame rate, bitrate, scale mode, fallback strategy under poor network conditions, etc. |
|[pushAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-pushaudioframe) |Send Audio data |
|[pullAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-pullaudioframe) |Pull Audio data |
|[sendP2PBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-sendp2pbinarymessage) |Send point\-to\-point binary messages |
|[sendP2PMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-sendp2pmessage) |Send point\-to\-point text messages |
|[shutdown](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-shutdown) |Shutdown StreamingRTCEngine |
|[startup](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-startup) |startup StreamingRTCEngine<br><br>Set types and ports of the engine instance in [EngineConfig](https://docs.byteplus.com/en/docs/12/docs-70098#EngineConfig). |
|[destroyStreamingRTCEngine](https://docs.byteplus.com/en/docs/12/docs-70095#destroystreamingrtcengine) |Destroy the engine instance created by calling [createStreamingRTCEngine](https://docs.byteplus.com/en/docs/12/docs-70095#createstreamingrtcengine), and release all related resources. |
|[createStreamingRTCEngine](https://docs.byteplus.com/en/docs/12/docs-70095#createstreamingrtcengine) |Create an IStreamingRTCEngine instance.<br><br>This is the first API you must call if you want to use all the RTC capabilities.<br><br>If the current thread does not have an engine instance, calling this API will create one. If an engine instance has been created, calling this API again will create another instance. |
|[getSpatialAudio](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-getspatialaudio) |Gets spatial audio instance. |
|[getRangeAudio](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-getrangeaudio) |Gets range audio instance. |
|[removeAllRemotePosition](https://docs.byteplus.com/en/docs/12/docs-70095#ISpatialAudio-removeallremoteposition) |Disables all spatial audio effects set by calling [updateRemotePosition](https://docs.byteplus.com/en/docs/12/docs-70095#ISpatialAudio-updateremoteposition) for all remote users. |
|[removeRemotePosition](https://docs.byteplus.com/en/docs/12/docs-70095#ISpatialAudio-removeremoteposition) |Disables all spatial audio effects set by calling [updateRemotePosition](https://docs.byteplus.com/en/docs/12/docs-70095#ISpatialAudio-updateremoteposition) for a certain remote user. |
|[updateRemotePosition](https://docs.byteplus.com/en/docs/12/docs-70095#ISpatialAudio-updateremoteposition) |Sets the coordinate and orientation of the remote user as a speaker in the rectangular coordinate system of the local user. In this case, the local user hears from the remote user with the expected spatial audio effects. |
|[updateSelfPosition](https://docs.byteplus.com/en/docs/12/docs-70095#ISpatialAudio-updateselfposition) |Sets the coordinate and orientation of the local user as a listener in the rectangular coordinate system the local user built to achieve expected spatial audio effects. |
|[disableRemoteOrientation](https://docs.byteplus.com/en/docs/12/docs-70095#ISpatialAudio-disableremoteorientation) |Turn off the effect of the orientation of the local user as the sound source.<br><br>After the effect is off, all the other users in the room listen to the local user as if the local user is in right front of each of them. |
|[enableSpatialAudio](https://docs.byteplus.com/en/docs/12/docs-70095#ISpatialAudio-enablespatialaudio) |Enable/disable spatial audio function. |
|[takeLocalSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-takelocalsnapshottofile) |Takes a snapshot of the local video stream and save it as a JPG file at the specified local path.<br><br>After calling this method, the SDK triggers [onLocalSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onlocalsnapshottakentofile) to report whether the snapshot is taken successfully and provide details of the snapshot image. |
|[takeRemoteSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-takeremotesnapshottofile) |Takes a snapshot of the remote video stream and save it as a JPG file at the specified local path.<br><br>After calling this method, the SDK triggers [onRemoteSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onremotesnapshottakentofile) to report whether the snapshot is taken successfully and provide details of the snapshot image. |
|[takeRemoteSnapshot](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-takeremotesnapshot) |Take a snapshot of the remote video. |
|[takeLocalSnapshot](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-takelocalsnapshot) |Take a snapshot of the local video. |
|[stopAudioRecording](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-stopaudiorecording) |Stop audio recording. |
|[startAudioRecording](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startaudiorecording) |Starts recording audio communication, and generate the local file.<br><br>If you call this API before or after joining the room without internal audio capture, then the recording task can still begin but the data will not be recorded in the local files. Only when you call [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startaudiocapture) to enable internal audio capture, the data will be recorded in the local files. |
|[stopFileRecording](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-stopfilerecording) |Stop local recording |
|[startFileRecording](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startfilerecording) |This method records the audio & video data during the call to a local file. |
|[setAnsMode](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setansmode) |Set the Active Noise Cancellation(ANC) mode during audio and video communications. |
|[setEarMonitorVolume](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setearmonitorvolume) |Set the volume of the earphone monitor |
|[setEarMonitorMode](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setearmonitormode-2) |Enables/disables in\-ear monitoring and controls whether to apply local audio processing to the in\-ear monitoring audio. |
|[setEarMonitorMode](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-setearmonitormode) |Turn on/off the earphone monitor function |
|[setNoAttenuationFlags](https://docs.byteplus.com/en/docs/12/docs-70095#IRangeAudio-setnoattenuationflags) |Set the flags to mark the user groups, within which the users talk without attenuation.<br><br>In the RTC room, if the flags of the users intersects with each other, the users talk without attenuation.<br><br>For example, the user is a member of multiple teams, and teammates of the same team talks without attentuation. You can set the flag for each team, and includes the flags of the user's teams in the user's flags. |
|[setAttenuationModel](https://docs.byteplus.com/en/docs/12/docs-70095#IRangeAudio-setattenuationmodel) |Set the volume roll\-off mode that a 3D sound has in an audio source when using the Range Audio feature. |
|[updatePosition](https://docs.byteplus.com/en/docs/12/docs-70095#IRangeAudio-updateposition) |Updates the coordinate of the local user's position in the rectangular coordinate system in the current room. |
|[updateReceiveRange](https://docs.byteplus.com/en/docs/12/docs-70095#IRangeAudio-updatereceiverange) |Updates the audio receiving range for the local user. |



|Callback |Description |
|---|---|
|[onTakeLocalSnapshotResult](https://docs.byteplus.com/en/docs/12/docs-70096#ISnapshotResultCallback-ontakelocalsnapshotresult) |Receives the callback after calling [takeLocalSnapshot](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-takelocalsnapshot). |
|[onRemoteSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onremotesnapshottakentofile) |Triggered after calling [takeRemoteSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-takeremotesnapshottofile) to report whether the snapshot is taken successfully and provide details of the snapshot image. |
|[onLocalSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onlocalsnapshottakentofile) |Triggered after calling [takeLocalSnapshotToFile](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-takelocalsnapshottofile) to report whether the snapshot is taken successfully and provide details of the snapshot image. |
|[onAudioRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onaudiorecordingstateupdate) |When calling [startAudioRecording](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startaudiorecording) or [stopAudioRecording](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-stopaudiorecording) to change the recording status, receive the callback. |
|[onRecordingProgressUpdate](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onrecordingprogressupdate) |Local recording progress callback.<br><br>This callback is triggered by [startFileRecording](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startfilerecording). When the recording state is normal, the system will prompt the recording progress through this callback every second. |
|[onRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onrecordingstateupdate) |Get a callback of the local recording status.<br><br>The callback is triggered by [startFileRecording](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startfilerecording) or [stopFileRecording](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-stopfilerecording). |
|[onExtensionAccessError](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onextensionaccesserror) |Failed to access the extension.<br><br>RTC SDK provides some features with extensions. Without implementing the extension, you cannot use the corresponding feature. |
|[onP2PLocalExternalEncoderStart](https://docs.byteplus.com/en/docs/12/docs-70096#IStreamingRTCEventHandler-onp2plocalexternalencoderstart) |You will get informed of the startup of the external video encoder.<br><br>For information on setting encoding configuration refer to [setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-setvideosourcetype). |
|[onP2PRemoteEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IStreamingRTCEventHandler-onp2premoteencodedvideoframe) |You can get encoded video frames sent from the remote client via this callback. And pass the data into your own decoder.<br><br>For information on pushing video frames refer to [pushVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-pushvideoframe)<br><br>For information on pushing encoded video streams refer to [pushEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-pushencodedvideoframe)<br><br>For information on setting encoding configuration refer to [setVideoDecoderConfig](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-setvideodecoderconfig) |
|[onP2PRemoteVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IStreamingRTCEventHandler-onp2premotevideoframe) |You can get video frames sent from the remote client via this callback.<br><br>For information on pushing video frames refer to [pushVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-pushvideoframe)<br><br>For information on pushing encoded video streams refer to [pushEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-pushencodedvideoframe)<br><br>For information on setting encoding configuration refer to [setVideoDecoderConfig](https://docs.byteplus.com/en/docs/12/docs-70095#IStreamingRTCEngine-setvideodecoderconfig) |
|[onP2PRemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-70096#IStreamingRTCEventHandler-onp2premotestreamstats) |Callback of statistics of the remote stream. You will get informed of the data every 2 s after the engine starts up. |
|[onP2PLocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-70096#IStreamingRTCEventHandler-onp2plocalstreamstats) |Callback of statistics of the local stream. You will get informed of the data every 2 s after the engine starts up. |
|[onP2PConnectionStats](https://docs.byteplus.com/en/docs/12/docs-70096#IStreamingRTCEventHandler-onp2pconnectionstats) |Callback of statistics of the RTC call. You will get informed of the data every 2 s after the engine starts up. |
|[onP2PConnectionStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IStreamingRTCEventHandler-onp2pconnectionstatechanged) |Callback of change of the connection state. You will get informed when the connection state of the engine changes. |
|[onExtensionAccessError](https://docs.byteplus.com/en/docs/12/docs-70096#IStreamingRTCEventHandler-onextensionaccesserror) |Failed to access the extension.<br><br>RTC SDK provides some features with extensions. Without implementing the extension, you cannot use the corresponding feature. |
|[onError](https://docs.byteplus.com/en/docs/12/docs-70096#IStreamingRTCEventHandler-onerror) |Callback for informing an error that cannot be recovered by the SDK. You will get informed of the error message via the callback. |
|[onWarning](https://docs.byteplus.com/en/docs/12/docs-70096#IStreamingRTCEventHandler-onwarning) |Callback for warning. You will get the warning message via the callback. |
|[onLogReport](https://docs.byteplus.com/en/docs/12/docs-70096#IStreamingRTCEventHandler-onlogreport) |Callback of logging. You will get notified via the callback when SDK logs an event. |
|[onTakeRemoteSnapshotResult](https://docs.byteplus.com/en/docs/12/docs-70096#ISnapshotResultCallback-ontakeremotesnapshotresult) |Receives the callback after calling [takeRemoteSnapshot](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-takeremotesnapshot). |
