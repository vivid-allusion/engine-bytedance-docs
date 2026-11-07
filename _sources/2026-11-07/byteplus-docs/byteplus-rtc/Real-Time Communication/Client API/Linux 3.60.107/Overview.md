---
title: "Overview"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-85515"
---

<span id="engine-management"></span>
## Engine Management


|Method |Description |
|---|---|
|[createRTCEngine](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-creatertcengine) |Creates an engine instance.<br><br>This is the very first API that you must call if you want to use all the RTC capabilities.<br><br>If there is no engine instance in current process, calling this API will create one. If an engine instance has been created, calling this API again will have the created engine instance returned. |
|[release](https://docs.byteplus.com/en/docs/12/docs-85516#IDeviceCollection-release) |Releases the resources occupied by the current [IDeviceCollection](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceCollection) object. |
|[getDevice](https://docs.byteplus.com/en/docs/12/docs-85516#IDeviceCollection-getdevice) |Get the information of the specific audio device. You can get the device information by index, device name, or device ID. |
|[getCount](https://docs.byteplus.com/en/docs/12/docs-85516#IDeviceCollection-getcount) |Get the number of audio & video devices in the current system |
|[getDevice](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoDeviceCollection-getdevice-2) |Get the information of the specific video device. You can get the device information by index, device info (ID, product ID, etc.). |
|[release](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoDeviceCollection-release) |Releases the resources occupied by the current [IVideoDeviceCollection](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoDeviceCollection) object. |
|[getDevice](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoDeviceCollection-getdevice) |Get the information of the specific video device. You can get the device information by index, device name, or device ID. |
|[getCount](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoDeviceCollection-getcount) |Get the number of video devices in the current system |
|[getDevice](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceCollection-getdevice-2) |Get the information of the specific audio device. You can get the device information by index, device info (ID, product ID, etc.). |
|[release](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceCollection-release) |Releases the resources occupied by the current [IAudioDeviceCollection](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceCollection) object. |
|[getDevice](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceCollection-getdevice) |According to the index number, get device information |
|[getCount](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceCollection-getcount) |Get the number of audio & video devices in the current system |
|[feedback](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-feedback) |Report the user feedback to RTC. |
|[setRuntimeParameters](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setruntimeparameters) |Set runtime parameters |
|[setBusinessId](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setbusinessid) |Sets the business ID<br><br>You can use businessId to distinguish different business scenarios. You can customize your businessId to serve as a sub AppId, which can share and refine the function of the AppId, but it does not need authentication. |
|[setLogConfig](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setlogconfig) |Configures the local log parameters of RTC SDK, including the logging level, directory, the limits for total log file size and the prefix of log. |
|[getSDKVersion](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-getsdkversion) |Get the current SDK version information. |
|[destroyRTCEngine](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-destroyrtcengine) |Destroy the engine instance created by [createRTCEngine](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-creatertcengine), and release all related resources. |



|Callback |Description |
|---|---|
|[onTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-ontokenwillexpire) |The callback is triggered when the SDK detects the joining room privilege from the Token will expires within 30s.<br><br>After receiving this callback, you must call [updateToken](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-updatetoken) to update the joining room privilege Token. |
|[onSysStats](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onsysstats) |You will periodically(2s) receive the callbacks of the current CPU and memory information. |
|[onLogReport](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onlogreport) |Terminal monitoring log callback. The callback is triggered when a terminal monitoring event is generated. |
|[onError](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onerror) |Error callback occurred. This callback is triggered when a network or media\-related error occurs during the<br><br>SDK runtime and cannot be automatically recovered and you may need to intervene. |
|[onWarning](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onwarning) |A warning occurred during the SDK runtime. The SDK usually recovers automatically and warnings can be ignored. |
|[onSubscribePrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onsubscribeprivilegetokenwillexpire) |Callback triggered 30s before the subscribing privilege of the Token expires.<br><br>After receiving this callback, you must call [updateToken](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-updatetoken) to update the subscribing privilege Token. |
|[onPublishPrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onpublishprivilegetokenwillexpire) |Callback triggered 30s before the publishing privilege of the Token expires.<br><br>After receiving this callback, you must call [updateToken](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-updatetoken) to update the publishing privilege Token. |


<span id="room-management"></span>
## Room Management


|Method |Description |
|---|---|
|[createRTCRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-creatertcroom) |Create a RTC room instance.<br><br>This API only returns a RTCroom instance. You still need to call [joinRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-joinroom) to actually create/join the room.<br><br>Each call of this API creates one [IRTCRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom) instance. Call this API as many times as the number of rooms you need, and then call [joinRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-joinroom) of each IRTCRoom instance to join multiple rooms at the same time.<br><br>In multi\-room mode, a user can subscribe to media streams in the joined rooms at the same time. |
|[setLiveMode](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setlivemode) |Sets room live mode.<br><br>Call this method after joining a room. |
|[getCallId](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-getcallid) |Gets call ID.<br><br>Call this method after joining a room. After creating a room, a call ID is generated to identify the call for this room. |
|[getRoomId](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-getroomid) |Get room ID. |
|[setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setroomextrainfo) |Sets extra information about the room the local user joins. |
|[joinRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-joinroom) |Join an RTC room.<br><br>After creating a room by calling [createRTCRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-creatertcroom), call this API to join the room and make audio & video calls with other users in the room. |
|[setRTCRoomEventHandler](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setrtcroomeventhandler) |Listens for event callbacks related to the [IRTCRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom) instance by setting the event handler of this instance. |
|[setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setuservisibility) |Set the visibility of the user in the room. The local user is visible to others by default before calling this API.<br><br>An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Room Capacity](https://docs.byteplus.com/en/byteplus-rtc/docs/257549). |
|[destroy](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-destroy) |Leave and destroy the RTC room instance created by calling [createRTCRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-creatertcroom). |
|[updateToken](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-updatetoken) |Update Token.<br><br>You must call this API to update token to ensure the RTC call to continue when you receive [onTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-ontokenwillexpire), [onPublishPrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onpublishprivilegetokenwillexpire), or [onSubscribePrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onsubscribeprivilegetokenwillexpire). |
|[joinRTSRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-joinrtsroom) |Joins an RTS room.<br><br>Users in the same room can talk to each other.<br><br>Repeated calls after entering the room are invalid. The user must call `leaveRoom` to exit the current room before joining the next room. |
|[setRTSRoomEventHandler](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-setrtsroomeventhandler) |Set the event handle of the [IRTSRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom) object.<br><br>You can listen for callback events for the room corresponding to this [IRTSRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom) object by setting the event handle. |
|[leaveRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-leaveroom) |Leave the RTC or RTS room.<br><br>The user calls this method to leave the room, end the call process, and release all call\-related resources. |
|[destroy](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-destroy) |Leave and destroy the RTS room instance created by calling [createRTSRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-creatertsroom). |
|[createRTSRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-creatertsroom) |Create an RTS room instance.<br><br>This API only returns an RTS room instance. You still need to call [joinRTSRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-joinrtsroom) to actually create/join the room.<br><br>Each call of this API creates one [IRTSRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom) instance. Call this API as many times as the number of rooms you need, and then call [joinRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-joinroom) of each IRTCRoom instance to join multiple rooms at the same time.<br><br>In multi\-room mode, a user can send and receive rts message in the joined rooms at the same time. |



|Callback |Description |
|---|---|
|[onRoomStats](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onroomstats) |In\-room call statistics callback.<br><br>After the user enters the room and starts the call, he receives this callback every 2s. |
|[onUserLeave](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onuserleave) |This callback is triggered when a remote user is disconnected. |
|[onUserJoined](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onuserjoined) |Callback about remote users joining the room. |
|[onLeaveRoom](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onleaveroom) |Leave the room callback.<br><br>After the user calls the [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-leaveroom) method, the SDK stops all publishing subscription streams and notifies the user to leave the room successfully through this callback after releasing all audio & video resources related to the call. |
|[onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onroomstatechanged) |Callback on room state changes. Via this callback you get notified of room relating warnings, errors and events. For example, the user joins the room, the user is removed from the room, and so on. |
|[onUserVisibilityChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuservisibilitychanged) |Callback for user to set user visibility by calling [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setuservisibility). |
|[onRoomStreamExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onroomstreamextrainfoupdate) |Callback used to receive the extra information set by the other users in the same room with [setStreamExtraInfo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setstreamextrainfo). |
|[onRoomExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onroomextrainfoupdate) |Callback used to receive the extra information set by the other users in the same room with [setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setroomextrainfo). |
|[onSetRoomExtraInfoResult](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onsetroomextrainforesult) |Callback on the result of calling [setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setroomextrainfo) to set extra information about the room. |
|[onUserJoined](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserjoined) |Callback for when a remote visible user joins the room, or when an invisible user in the room switches to being visible.<br><br><br>&nbsp;<br><br>1. When a remote user sets themselves to be visible by calling the setUserVisibility method and then joins the room, other users in the room will receive this event.<br><br>2. When a remote visible user who has been disconnected re\-enters the room, other users in the room will receive this event.<br><br>3. When a hidden remote user in the room switches to being visible by calling the setUserVisibility method, other users in the room will receive this event.<br><br>4. A new user entering the room will receive an entry callback notification for visible users who were already in the room before they entered. |


<span id="audio-management"></span>
## Audio Management


|Method |Description |
|---|---|
|[muteAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-muteaudiocapture) |Set whether to mute the recording signal (without changing the local hardware). |
|[stopAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-stopaudioplaybackdevicetest) |Stop the playback test for the local audio device. |
|[startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-startaudioplaybackdevicetest) |Start the playback test for the local audio device. RTC will start playing the audio file specified. And RTC will notify the audio volume via the `onAudioPlaybackDeviceTestVolume` periodically. |
|[initAudioCaptureDeviceForTest](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-initaudiocapturedevicefortest) |Try to initialize the audio capture device, which can detect abnormal problems such as the device does not exist, permissions are denied/disabled, etc. |
|[initAudioPlaybackDeviceForTest](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-initaudioplaybackdevicefortest) |Try to initialize the audio playback device, and you can detect abnormal problems such as the device does not exist, permissions are denied/disabled, etc. |
|[getAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-getaudiocapturedevice) |Gets the current audio capture device ID. |
|[getAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-getaudioplaybackdevice) |Gets the current audio playback device ID. |
|[getAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-getaudiocapturedevicemute) |Get state of the audio capture device. |
|[setAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-setaudiocapturedevicemute) |Mute or Unmute the current audio capture device. The default state is speaking. |
|[getAudioPlaybackDeviceMute](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-getaudioplaybackdevicemute) |Get the mute state of the current audio playback device. |
|[setAudioPlaybackDeviceMute](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-setaudioplaybackdevicemute) |Mute or Unmute the current audio playback device. The default state is speaking. |
|[getAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-getaudiocapturedevicevolume) |Get the current audio capture volume. |
|[setAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-setaudiocapturedevicevolume) |Set the current audio capture volume |
|[getAudioPlaybackDeviceVolume](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-getaudioplaybackdevicevolume) |Get the current audio playback device volume. |
|[setAudioPlaybackDeviceVolume](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-setaudioplaybackdevicevolume) |Set the current audio playback device volume |
|[setAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-setaudiocapturedevice) |Set up audio capture devices. |
|[setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-setaudioplaybackdevice) |Sets the audio playback device. |
|[followSystemCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-followsystemcapturedevice) |Set the audio capture device to follow the OS setting or not. |
|[followSystemPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-followsystemplaybackdevice) |Set the audio playback device to follow the OS setting or not. |
|[enumerateAudioCaptureDevices](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-enumerateaudiocapturedevices) |Get a list of audio acquisition devices in the current system. If there are subsequent device changes, you need to call this interface again to get a new device list. |
|[enumerateAudioPlaybackDevices](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioDeviceManager-enumerateaudioplaybackdevices) |Get a list of the audio playback device. When the audio playback device changes, you will receive `onAudioMediaDeviceStateChanged` and you need to call this API again to get the new device list. |
|[buildAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85516#buildaudioframe) |Create IAudioFrame |
|[setAudioSelectionConfig](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setaudioselectionconfig) |Set the priority of the local audio stream to be published. |
|[setRemoteRoomAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setremoteroomaudioplaybackvolume) |Adjusts the audio playback volume from all the remote users in a room. |
|[enablePlaybackDucking](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-enableplaybackducking) |Enables/disables the playback ducking function. This function is usually used in scenarios where short videos or music will be played simultaneously during RTC calls.<br><br>With the function on, if remote voice is detected, the local media volume of RTC will be lowered to ensure the clarity of the remote voice. If remote voice disappears, the local media volume of RTC restores. |
|[enableVocalInstrumentBalance](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-enablevocalinstrumentbalance) |Enables/disables the loudness equalization function.<br><br>If you call this API with the parameter set to True, the loudness of user's voice will be adjusted to \-16lufs. If then you also call setAudioMixingLoudness and import the original loudness of the audio data used in audio mixing, the loudness will be adjusted to \-20lufs when the audio data starts to play. |
|[setRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setremoteaudioplaybackvolume) |Set the audio volume of playing the received remote stream. You must join the room before calling the API. The validity of the setting is not associated with the publishing status of the stream. |
|[enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-enableaudiopropertiesreport) |Enable audio information prompts. After that, you will receive [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onlocalaudiopropertiesreport), [onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onremoteaudiopropertiesreport), and [onActiveSpeaker](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onactivespeaker). |
|[enableExternalSoundCard](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-enableexternalsoundcard) |Enable the audio process mode for external sound card. |
|[getAudioDeviceManager](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-getaudiodevicemanager) |Device audio management interface creation |
|[enableAGC](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-enableagc) |Turns on/ off AAGC（Analog Automatic Gain Control）.<br><br>After AAGC is enabled, SDK can automatically adjust microphone pickup volume to keep the output volume at a steady level. |
|[setAudioProfile](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setaudioprofile) |Sets the sound quality. Call this API to change the sound quality if the audio settings in the current [RoomProfileType](https://docs.byteplus.com/en/docs/12/docs-85519#RoomProfileType) can not meet your requirements. |
|[stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-stopaudiocapture) |Stop internal audio capture. The default is off.<br><br>Internal audio capture refers to: capturing audio using the built\-in module.<br><br>The local client will be informed via [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onaudiodevicestatechanged) after stopping audio capture by calling this API.<br><br>.<br><br>The remote clients in the room will be informed of the state change via [onUserStopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onuserstopaudiocapture) after the visible client stops audio capture by calling this API.<br><br>. |
|[setPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setplaybackvolume) |Adjust the playback volume of the mixed remote audios. You can call this API before or during the playback. |
|[setCaptureVolume](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setcapturevolume) |Adjust the audio capture volume |
|[startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startaudiocapture) |Start internal audio capture. The default is off.<br><br>Internal audio capture refers to: capturing audio using the built\-in module.<br><br>The local client will be informed via [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onaudiodevicestatechanged) after starting audio capture by calling this API.<br><br>The remote clients in the room will be informed of the state change via [onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onuserstartaudiocapture) after the visible user starts audio capture by calling this API.. |



|Callback |Description |
|---|---|
|[onAudioStreamBanned](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onaudiostreambanned) |All the users in the room will get informed via this callback when a user is banned or the ban of the user has been lifted by calling BanUserStream/UnbanUserStream on the server side. |
|[onStreamSyncInfoReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onstreamsyncinforeceived) |Audio stream synchronization information callback. You can use this callback to receive audio stream synchronization information sent remotely after the remote user calls [sendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendstreamsyncinfo) to send an audio stream synchronization message. |
|[onActiveSpeaker](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onactivespeaker) |After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-enableaudiopropertiesreport), you will periodically receive this callback for the active speaker information. |
|[onUserStopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onuserstopaudiocapture) |When a user in the room calls [stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-stopaudiocapture) to turn off audio capture, other users in the room will receive this callback. |
|[onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onuserstartaudiocapture) |Users in the room call [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startaudiocapture) When audio capture is turned on, other users in the room will receive this callback. |
|[onLocalAudioStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onlocalaudiostatechanged) |When the state of the local audio changes, the callback notifies the current local audio state. |
|[onAudioDeviceVolumeChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onaudiodevicevolumechanged) |Callback to notify you the volume of the audio device has been changed or when the device has been muted or unmuted. No need to activate the notification beforehand. |
|[onAudioPlaybackDeviceTestVolume](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onaudioplaybackdevicetestvolume) |Notification on the playing volume during the test for the local audio devices |
|[onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onremoteaudiopropertiesreport) |After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-enableaudiopropertiesreport), you will periodically receive this callback for the instantaneous information about the subscribed remote audio streams.<br><br>The remote audio streams includes the microphone audio and screen audio collected using the RTC SDK internal mechanism/custom mechanism. |
|[onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onlocalaudiopropertiesreport) |After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-enableaudiopropertiesreport), you will periodically receive this callback for the instantaneous information about local audio.<br><br>Local audio includes the microphone audio, the screen audio captured using RTC SDK internal mechanisms, and locally mixing audio. |
|[onAudioDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onaudiodevicewarning) |Audio device warning callback. The audio devices include audio capture devices and audio rendering devices. |
|[onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onaudiodevicestatechanged) |Callback of audio device state. Audio devices include audio capture devices and audio playback devices. |


<span id="video-management"></span>
## Video Management


|Method |Description |
|---|---|
|[startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startvideocapture) |Enable internal video capture immediately. The default is off.<br><br>Internal video capture refers to: use the RTC SDK built\-in video capture module to capture.<br><br>The local client will be informed via [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onvideodevicestatechanged) after starting video capture by calling this API.<br><br>The remote clients in the room will be informed of the state change via [onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onuserstartvideocapture) after the visible client starts video capture by calling this API. |
|[getVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoDeviceManager-getvideocapturedevice) |Get the video capture device information currently used by the SDK |
|[setVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoDeviceManager-setvideocapturedevice) |Set the current video capture device |
|[enumerateVideoCaptureDevices](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoDeviceManager-enumeratevideocapturedevices) |Get a list of video capture devices in the current system. |
|[buildEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85516#buildencodedvideoframe) |Create IEncodedVideoFrame |
|[setRemoteVideoConfig](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setremotevideoconfig) |Sets your expected configuration of the remote video stream that you want to subscribe to or have subscribed to. |
|[setRemoteSimulcastStreamType](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setremotesimulcaststreamtype) |Sets the type of the remote video stream to subscribe to. |
|[updateRemoteStreamVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-updateremotestreamvideocanvas) |Modifies remote video frame rendering settings, including render mode and background color. |
|[getVideoDeviceManager](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-getvideodevicemanager) |Create a video Facility Management instance |
|[updateRemoteStreamVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-updateremotestreamvideocanvas-2) |Modifies remote video frame rendering settings, including render mode, background color, and rotation angle, while using the internal rendering of the SDK. |
|[setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setremotevideocanvas) |Set the view and mode for rendering the specific video stream.<br><br>If you need to unbind the canvas for the video stream, set the canvas to `Null`. |
|[updateLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-updatelocalvideocanvas) |Update the render mode and background color of local video rendering |
|[setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setlocalvideocanvas) |Sets the view to be used for local video rendering and the rendering mode. |
|[setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setvideoencoderconfig) |Sets the expected quality of the video stream by specifying the resolution, frame rate, bitrate, and the fallback strategy when the network is poor. |
|[setVideoCaptureConfig](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setvideocaptureconfig) |Set the video capture parameters for internal capture of the RTC SDK.<br><br>If your project uses the SDK internal capture module, you can specify the video capture parameters including preference, resolution and frame rate through this interface. |
|[stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-stopvideocapture) |Disable internal video capture immediately. The default is off.<br><br>Internal video capture refers to: use the RTC SDK built\-in video capture module to capture.<br><br>The local client will be informed via [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onvideodevicestatechanged) after stopping video capture by calling this API.<br><br>The remote clients in the room will be informed of the state change via [onUserStopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onuserstopvideocapture) after the visible client stops video capture by calling this API. |



|Callback |Description |
|---|---|
|[onFaceDetectResult](https://docs.byteplus.com/en/docs/12/docs-85517#IFaceDetectionObserver-onfacedetectresult) |Callback of the result of face detection with Effect SDK.<br><br>After calling [enableFaceDetection](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoEffect-enablefacedetection) and using the Effect SDK integrated in the RTC SDK, you will receive this callback. |
|[onLocalVideoStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onlocalvideostatechanged) |Receive this event when the state of the local video stream changes. |
|[onUserStopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onuserstopvideocapture) |The remote clients in the room will be informed of the state change via this callback after the visible user stops video capture by calling [stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-stopvideocapture).<br><br>If you don't start video capture before you publish video data, all visible user will receive this callback. |
|[onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onuserstartvideocapture) |The remote clients in the room will be informed of the state change via this callback after the visible user starts video capture by calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startvideocapture). |
|[onVideoDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onvideodevicewarning) |Video device warning callback. The video devices include video capture devices. |
|[onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onvideodevicestatechanged) |Callback of video device state. Video devices include cameras and screen sharing video capture devices. |


<span id="audio-video-transport"></span>
## Audio & Video Transport


|Method |Description |
|---|---|
|[requestRemoteVideoKeyFrame](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-requestremotevideokeyframe) |After subscribing to the remote video stream, request the key frame to the remote |
|[resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-resumeforwardstreamtoallrooms) |Call this method to resume relaying to all rooms from the pause by calling [pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-pauseforwardstreamtoallrooms). |
|[pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-pauseforwardstreamtoallrooms) |Call this method to pause relaying media stream to all rooms after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-startforwardstreamtorooms).<br><br>After that, call [resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-resumeforwardstreamtoallrooms) to resume. |
|[stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-stopforwardstreamtorooms) |Call to this method to stop relaying media stream to all rooms after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-startforwardstreamtorooms). |
|[updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-updateforwardstreamtorooms) |Update information of the rooms where you want to relay the media stream to after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-startforwardstreamtorooms).<br><br>Adding and removing rooms by calling this method will trigger [onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onforwardstreamstatechanged) on the local. |
|[startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-startforwardstreamtorooms) |Start relaying media stream across rooms.<br><br>After calling [joinRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-joinroom), you can call this method to publish the media stream to multiple rooms that applies to scenarios such as anOnline talent contest and so on. |
|[setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setmultideviceavsync) |Synchronizes published audio and video.<br><br>When the same user simultaneously uses separate devices to capture and publish audio and video, there is a possibility that the streams are out of sync due to the network disparity. In this case, you can call this API on the video publisher side and the SDK will automatically line the video stream up according to the timestamp of the audio stream, ensuring that the audio the receiver hears corresponds to the video the receiver watches. |
|[resumeAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-resumeallsubscribedstreamaudio) |Resumes receiving all the audio streams of all remote users. |
|[resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-resumeallsubscribedstreamvideo) |Resumes receiving all the video streams of all remote users. |
|[pauseAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-pauseallsubscribedstreamaudio) |Pauses receiving the audio streams of all remote users. |
|[pauseAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-pauseallsubscribedstreamvideo) |Pauses receiving all the video streams of all remote users. |
|[subscribeAllStreamsAudio](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-subscribeallstreamsaudio) |Subscribes to or unsubscribes from all remote audio streams (by the microphone). |
|[subscribeAllStreamsVideo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-subscribeallstreamsvideo) |Subscribes to or unsubscribes from all remote video streams (by the camera). |
|[setStreamExtraInfo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setstreamextrainfo) |Sets the stream extra info. |
|[subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-subscribestreamaudio) |Subscribes to or unsubscribes from the specific remote audio streams. |
|[subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-subscribestreamvideo) |Subscribes to or unsubscribes from the specific remote video stream. |
|[publishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-publishstreamaudio) |Publishes or stops publishing audio streams in the current room. |
|[publishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-publishstreamvideo) |Publishes or stops publishing video streams. |
|[setDummyCaptureImagePath](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setdummycaptureimagepath) |Set an alternative image when the local internal video capture is not enabled.<br><br>When you call `stopVideoCapture`, an alternative image will be pushed. You can set the path to null or open the camera to stop publishing the image.<br><br>You can repeatedly call this API to update the image. |



|Callback |Description |
|---|---|
|[onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onvideopublishstatechanged) |Callback on video\-stream state changes. |
|[onFirstLocalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onfirstlocalaudioframe) |Receive the callback when publishing local audio stream. |
|[onVideoFramePlayStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onvideoframeplaystatechanged) |Remote video stream first frame playback state change callback |
|[onAudioFramePlayStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onaudioframeplaystatechanged) |Audio first frame playback state change callback |
|[onFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onfirstremotevideoframedecoded) |The subscriber will receive this callback when the first frame of the receiving video stream begins to decode. The following situations are included:<br><br><br>&nbsp;<br><br>1. The publisher publishes video, including the initial publication and restart after cancellation. The publisher can cancel the video streaming proactively. Video streaming can also be cancelled by the publisher to stop publishing, leave the room or go offline.<br><br>2. After the publisher stops video capture, they restart it. When using an external source, this involves stopping the stream and then streaming again.<br><br>3. After the publisher publishes video, the subscriber cancels the subscription to video and then re\-subscribes to it. |
|[onFirstRemoteVideoFrameRendered](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onfirstremotevideoframerendered) |The subscriber will receive this callback when the first frame of the receiving video stream begins to render. The following situations are included:<br><br><br>&nbsp;<br><br>1. The publisher publishes video for the first time.<br><br>2. In 1, the publisher cancels the video streaming after publishing and publishes it again.<br><br>3. In 1, the publisher stops video capture after publishing and restarts it. (Or when using an external source, the stream is stopped and restarted again.)<br><br>4. In 1, the subscriber cancels the video streaming and subscribes to it again. (The interface includes [subscribeAllStreamsVideo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-subscribeallstreamsvideo), [pauseAllSubscribedStream](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-pauseallsubscribedstreamvideo)/[resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-resumeallsubscribedstreamvideo)) |
|[onVideoFrameSendStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onvideoframesendstatechanged) |Triggered when the local video stream first frame sending status changes. |
|[onAudioFrameSendStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onaudioframesendstatechanged) |Audio first frame sending status change callback |
|[onRemoteVideoStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onremotevideostatechanged) |When the state of a remote video stream changes, users in the room who subscribe to this stream receive the event. |
|[onRemoteAudioStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onremoteaudiostatechanged) |When the state of the audio stream from the remote user subscribes to changes, this callback will be received to understand the current state of the remote audio stream. |
|[onFirstRemoteAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onfirstremoteaudioframe) |The subscriber will receive this callback when the first frame of the receiving audio stream begins to decode. The following situations are included:<br><br><br>&nbsp;<br><br>1. The publisher publishes audio, including the initial publication and restart after cancellation.The publisher can cancel the audio streaming proactively. Audio streaming can also be cancelled by the publisher to stop publishing, leave the room or go offline.<br><br>2. After the publisher stops audio capture, they restart it. When using an external source, this involves stopping the stream and then streaming again.<br><br>3. After the publisher publishes audio, the subscriber cancels the subscription to audio and then re\-subscribes to it. |
|[onFirstLocalVideoFrameCaptured](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onfirstlocalvideoframecaptured) |RTC SDK receives this callback when the first video frame or screen video frame capture is completed locally. |
|[onRemoteVideoSizeChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onremotevideosizechanged) |Users in the room who subscribe to this video stream receive this callback when the remote video size or rotation configuration changes. |
|[onLocalVideoSizeChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onlocalvideosizechanged) |Receive this callback when the local video size or rotation configuration changes. |
|[onAVSyncEvent](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onavsyncevent) |Stream publisher will receive this callback when the A/V synchronization error occurs after [setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setmultideviceavsync) is called. |
|[onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onnetworkquality) |Report the network quality of the users every 2s after the local user joins the room and starts publishing or subscribing to a stream. |
|[onForwardStreamEvent](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onforwardstreamevent) |Callback returning the events during relaying the media stream to each room |
|[onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onforwardstreamstatechanged) |Callback returning the state and errors during relaying the media stream to each of the rooms |
|[onAVSyncStateChange](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onavsyncstatechange) |Stream publisher will receive this callback when the A/V synchronization state changes after [setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setmultideviceavsync) is called. |
|[onVideoStreamBanned](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onvideostreambanned) |All the users in the room will get informed via this callback when a user is banned or the ban of the user has been lifted by calling BanUserStream/UnbanUserStream on the server side. |
|[onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserpublishstreamaudio) |Callback on a remote user publishing or stopping publishing remote audio streams in the room. |
|[onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserpublishstreamvideo) |Callback on a remote user publishing or stopping publishing video streams in the room. |
|[onRemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onremotestreamstats) |Remote audio/video stream statistics and network quality callbacks for local subscriptions.<br><br>After the local user subscribes to the stream successfully, the SDK will periodically (2s) notify the user through this callback event of the quality statistics of the subscribed stream during this reference period, including: sending audio & video bit rate, sending frame rate, encoded frame rate, network quality, etc. |
|[onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onaudiosubscribestatechanged) |Callback on state changes of the subscription to microphone\-audio streams. |
|[onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onvideosubscribestatechanged) |Callback on state changes of the subscription to camera\-video streams. |
|[onAudioPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onaudiopublishstatechanged) |Triggered when local audio stream publishing status changes, or the local user joins the room. |


<span id="audio-processing"></span>
## Audio Processing


|Method |Description |
|---|---|
|[setLocalVoicePitch](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setlocalvoicepitch) |Change local voice to a different key, mostly used in Karaoke scenarios.<br><br>You can adjust the pitch of local voice such as ascending or descending with this method. |


<span id="video-processing"></span>
## Video Processing


|Method |Description |
|---|---|
|[initCVResource](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoEffect-initcvresource) |Checks video effect license, sets the video effect resource model path, and initializes video effect. |
|[setLowLightAdjusted](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setlowlightadjusted) |Sets the video lowlight enhancement mode.<br><br>It can significantly improve image quality in scenarios with insufficient light, contrast lighting, or backlit situations. |
|[clearVideoWatermark](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-clearvideowatermark) |Removes video watermark from designated video stream. |
|[setVideoWatermark](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setvideowatermark) |Adds watermark to designated video stream. |
|[stopVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-stopvideodigitalzoomcontrol) |Stop the ongoing digital zoom control instantly. |
|[startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startvideodigitalzoomcontrol) |Continuous and repeatedly digital zoom control. This action effect both the video preview locally and the stream published. |
|[setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setvideodigitalzoomcontrol) |Digital zoom or move the local video image once. This action affects both the video preview locally and the stream published. |
|[setVideoDigitalZoomConfig](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setvideodigitalzoomconfig) |Set the step size for each digital zooming control to the local videos. |
|[getVideoEffectInterface](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-getvideoeffectinterface) |Gets video effect interfaces. |
|[setRemoteVideoMirrorType](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setremotevideomirrortype) |When using internal rendering, enable mirroring for the remote stream. |
|[setVideoCaptureRotation](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setvideocapturerotation) |Set the rotation of the video images captured from the local device.<br><br>Call this API to rotate the videos when the camera is fixed upside down or tilted. |
|[disableFaceDetection](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoEffect-disablefacedetection) |Stops face detection. |
|[enableFaceDetection](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoEffect-enablefacedetection) |Starts face detection and registers the observer for the result.<br><br>With this observer, you will receive [onFaceDetectResult](https://docs.byteplus.com/en/docs/12/docs-85517#IFaceDetectionObserver-onfacedetectresult) periodically. |
|[setColorFilterIntensity](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoEffect-setcolorfilterintensity) |Sets the intensity of the color filter enabled. |
|[setColorFilter](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoEffect-setcolorfilter) |Sets the color filter. |
|[updateEffectNode](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoEffect-updateeffectnode) |Sets the intensity of video effects. |
|[setEffectNodes](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoEffect-seteffectnodes) |Sets the video effects material package. |
|[disableVideoEffect](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoEffect-disablevideoeffect) |Disables video effects. |
|[enableVideoEffect](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoEffect-enablevideoeffect) |Enables video effects including beauty and color filters. |
|[freeAuthMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoEffect-freeauthmessage) |After using the authorization message string, free the memory. |
|[getAuthMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoEffect-getauthmessage) |Get authorization messages from the Effect SDK to obtain online licenses. |


<span id="custom-stream-processing"></span>
## Custom Stream Processing


|Method |Description |
|---|---|
|[setAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setaudiosourcetype) |Switch the audio capture type. |
|[processVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoProcessor-processvideoframe) |Get RTC SDK acquired video frames obtained, according to the video pre\-processor [registerLocalVideoProcessor](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-registerlocalvideoprocessor) set, video pre\-processing, the final processed video frames to the RTC SDK for encoding transmission. |
|[setRemoteVideoSink](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setremotevideosink) |Binds the remote video stream to a custom renderer. |
|[setLocalVideoSink](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setlocalvideosink) |Binds the local video stream to a custom renderer. |
|[setVideoDecoderConfig](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setvideodecoderconfig) |Before subscribing to the remote video stream, set the remote video data decoding method |
|[pushExternalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-pushexternalencodedvideoframe) |Push custom encoded video stream |
|[setExternalVideoEncoderEventHandler](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setexternalvideoencodereventhandler) |Register custom encoded frame push event callback |
|[registerRemoteEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-registerremoteencodedvideoframeobserver) |Video data callback after registering remote encoding.<br><br>After registration, when the SDK detects a remote encoded video frame, it will trigger the [onRemoteEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IRemoteEncodedVideoFrameObserver-onremoteencodedvideoframe) callback |
|[registerLocalEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-registerlocalencodedvideoframeobserver) |Register a local video frame observer.<br><br>This method applys to both internal capturing and custom capturing.<br><br>After calling this API, SDK triggers [onLocalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85517#ILocalEncodedVideoFrameObserver-onlocalencodedvideoframe) whenever a video frame is captured. |
|[registerLocalVideoProcessor](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-registerlocalvideoprocessor) |Set up a custom video preprocessor.<br><br>Using this video preprocessor, you can call [processVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85516#IVideoProcessor-processvideoframe) to preprocess the video frames collected by the RTC SDK, and use the processed video frames for RTC audio & video communication. |
|[disableAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-disableaudioprocessor) |Disable custom audio processing. |
|[enableAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-enableaudioprocessor) |Enable audio frames callback for custom processing and set the format for the specified type of audio frames. |
|[registerAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-registeraudioprocessor) |Register a custom audio preprocessor.<br><br>After that, you can call [enableAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-enableaudioprocessor) to process the audio streams that either captured locally or received from the remote side. RTC SDK then encodes or renders the processed data. |
|[registerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-registeraudioframeobserver) |Register an audio frame observer. |
|[disableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-disableaudioframecallback) |Disables audio data callback. |
|[enableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-enableaudioframecallback) |Enable audio frames callback and set the format for the specified type of audio frames. |
|[pushExternalVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-pushexternalvideoframe) |Pushes external video frames. |
|[setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setvideosourcetype) |Set the video source, including the screen recordings.<br><br>The internal video capture is the default, which refers to capturing video using the built\-in module. |
|[pullExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-pullexternalaudioframe) |Pull remote audio data. You can use the data for audio processing or custom rendering.<br><br>After calling this method, the SDK will actively pull the audio data that is ready to be played, including the decoded and mixed audio data from remote end for external playback. |
|[setRemoteVideoSink](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setremotevideosink-2) |Binds the remote video stream to a custom renderer.You can get video frame data at specified positions and formats through parameter settings. |
|[setLocalVideoSink](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setlocalvideosink-2) |Binds the local video stream to a custom renderer.You can get video frame data at specified positions and formats through parameter settings. |
|[pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-pushexternalaudioframe) |Push custom captured audio data to the RTC SDK. |
|[setAudioRenderType](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setaudiorendertype) |Switch the audio render type. |



|Callback |Description |
|---|---|
|[onRemoteEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IRemoteEncodedVideoFrameObserver-onremoteencodedvideoframe) |Call [registerRemoteEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-registerremoteencodedvideoframeobserver), the callback is triggered when the SDK detects the remote encoded video data |
|[onLocalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85517#ILocalEncodedVideoFrameObserver-onlocalencodedvideoframe) |After calling [registerLocalEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-registerlocalencodedvideoframeobserver), SDK will trigger this callback when it receives local video frames. |
|[onProcessRemoteUserAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IAudioFrameProcessor-onprocessremoteuseraudioframe) |Returns the address of the locally captured audio frame for custom processing. |
|[onProcessPlayBackAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IAudioFrameProcessor-onprocessplaybackaudioframe) |Returns the address of the locally captured audio frame for custom processing. |
|[onProcessRecordAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IAudioFrameProcessor-onprocessrecordaudioframe) |Returns the address of the locally captured audio frame for custom processing. |
|[onCaptureMixedAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IAudioFrameObserver-oncapturemixedaudioframe) |Return the mixed audio data of the data recorded by local microphone and the audio data of `MediaPlayer` and `EffectPlayer`. |
|[onRecordScreenAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IAudioFrameObserver-onrecordscreenaudioframe) |Returns the audio data played locally |
|[onMixedAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IAudioFrameObserver-onmixedaudioframe) |Returns mixed audio data including both data recorded by the local microphone and data from all subscribed remote users |
|[onRemoteUserAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IAudioFrameObserver-onremoteuseraudioframe) |Returns the audio data of one remote user. |
|[onPlaybackAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IAudioFrameObserver-onplaybackaudioframe) |Returns the mixed audio data of all subscribed remote users |
|[onRecordAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IAudioFrameObserver-onrecordaudioframe) |Returns audio data recorded by microphone |
|[onActiveVideoLayer](https://docs.byteplus.com/en/docs/12/docs-85517#IExternalVideoEncoderEventHandler-onactivevideolayer) |As the sender of a external encoded video stream, you will receive this callback at certain moments.<br><br>Based on the hints of this callback, you can selectively encode the video stream that is ready for transmission, in order to reduce the performance impact of video encoding on the local device. This callback is triggered based on a combination of factors, including the performance of the local device, the local network, and whether the stream is subscribed by the remote user. |
|[onRequestKeyFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IExternalVideoEncoderEventHandler-onrequestkeyframe) |This callback is used to inform the stream publisher that a keyframe needs to be regenerated. |
|[onRateUpdate](https://docs.byteplus.com/en/docs/12/docs-85517#IExternalVideoEncoderEventHandler-onrateupdate) |When the frame rate or bit rate of a custom encoded stream changes, the callback is triggered |
|[onStop](https://docs.byteplus.com/en/docs/12/docs-85517#IExternalVideoEncoderEventHandler-onstop) |When you receive the callback, you need to stop pushing custom encoded video frames to the SDK |
|[onStart](https://docs.byteplus.com/en/docs/12/docs-85517#IExternalVideoEncoderEventHandler-onstart) |Prompt custom encoded frames to start pushing callbacks.<br><br>After receiving this callback, you can call [pushExternalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-pushexternalencodedvideoframe) to push a custom encoded video frame to the SDK |


<span id="network-processing"></span>
## Network Processing


|Method |Description |
|---|---|
|[setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setlocalsimulcastmode) |Enable the Simulcast feature and configure the lower\-quality video streams settings. |
|[stopNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-stopnetworkdetection) |Stop pre\-call network probe |
|[startNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startnetworkdetection) |Pre\-call network detection |
|[setRemoteUserPriority](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setremoteuserpriority) |Set user priority |
|[setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setsubscribefallbackoption) |Sets the fallback option for subscribed RTC streams.<br><br>You can call this API to set whether to lower the resolution of currently subscribed stream under limited network conditions. |
|[setPublishFallbackOption](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setpublishfallbackoption) |Sets the fallback option for published audio & video streams.<br><br>You can call this API to set whether to automatically lower the resolution you set of the published streams under limited network conditions. |
|[setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setlocalsimulcastmode-2) |Enable the Simulcast feature. |



|Callback |Description |
|---|---|
|[onConnectionStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onconnectionstatechanged) |SDK connection state change callback with signaling server. Triggered when the connection state changes. |
|[onNetworkDetectionStopped](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onnetworkdetectionstopped) |Pre\-call network probing ends<br><br>The following will stop detection and receive this primary callback:<br><br><br>&nbsp;<br><br>1. This callback is received once when the [stopNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-stopnetworkdetection) interface is called to stop probing;<br><br>2. Stop detection when the first frame of remote/local audio is received;<br><br>3. Stop detecting when the detection exceeds 3 minutes;<br><br>4. When the probe link is disconnected for a certain period of time, the probe is stopped. |
|[onNetworkDetectionResult](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onnetworkdetectionresult) |Pre\-call network detection result.<br><br>After successfully calling [startNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startnetworkdetection), you will receive this callback for the first time in 3s and every 2s thereafter. |
|[onSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onseimessagereceived) |Receive this callback when you receive a video frame with a SEI message sent via [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendseimessage) |
|[onPerformanceAlarms](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onperformancealarms) |When the publish performance fallback [setPublishFallbackOption](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setpublishfallbackoption) is not turned on locally, and when insufficient device performance is detected, this callback is received.<br><br>When the publish performance fallback [setPublishFallbackOption](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setpublishfallbackoption) is locally turned on, and when the publish performance fallback/recovery is caused due to device performance/network reasons, this callback is received. |
|[onSimulcastSubscribeFallback](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onsimulcastsubscribefallback) |This callback is triggered when media streams start to fall back or restore from a fallback. |
|[onNetworkTypeChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onnetworktypechanged) |SDK Current network connection type change callback. Callbacks the event when the current network connection type of the SDK changes. |


<span id="messaging"></span>
## Messaging


|Method |Description |
|---|---|
|[sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendseimessage) |<span id="IRTCEngine\-sendseimessage\-2"\></span\> Sends SEI data.<br><br>In a video call scenario, SEI is sent with the video frame, while in a voice call scenario, SDK will automatically publish a black frame with a resolution of 16 × 16 pixels to carry SEI data.<br><br>&nbsp;<br><br>In a voice call, you should set this parameter to `kStreamIndexMain`, otherwise the SEI data is discarded and cannot be sent to the remote user. |
|[sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-senduserbinarymessage) |Sends a binary message (P2P) to the specified user in the room |
|[sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-sendusermessage) |Send a text message (P2P) to the specified user in the room |
|[sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-sendroombinarymessage) |Send broadcast messages to all other users in the room. |
|[sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-sendroommessage) |Send broadcast messages to all other users in the room. |
|[sendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendstreamsyncinfo) |Send audio stream synchronization information. The message is sent to the remote end through the audio stream and synchronized with the audio stream. After the interface is successfully called, the remote user will receive a [onStreamSyncInfoReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onstreamsyncinforeceived) callback. |
|[sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendserverbinarymessage) |Client side sends binary messages to the application server (P2Server) |
|[sendServerMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendservermessage) |The client side sends a text message to the application server (P2Server) |
|[sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-senduserbinarymessageoutsideroom) |Send binary messages (P2P) to a specified user outside the room |
|[sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendusermessageoutsideroom) |Send a text message (P2P) to a specified user outside the room |
|[getPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-getpeeronlinestatus) |Query the login status of the opposite or local user |
|[setServerParams](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setserverparams) |Set application server parameters<br><br>Client side calls [sendServerMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendservermessage) or [sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendserverbinarymessage) Before sending a message to the application server, a valid signature and application server address must be set. |
|[updateLoginToken](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-updatelogintoken) |Update the Token<br><br>Token used by the user to log in has a certain valid period. When the Token expires, you need to call this method to update the login Token information.<br><br>When calling the [login](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-login) method to log in, if an expired token is used, the login will fail and you will receive an [onLoginResult](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onloginresult) callback notification with an error code of kLoginErrorCodeInvalidToken. You need to reacquire the token and call this method to update the token. |
|[logout](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-logout) |Log out of RTS server.<br><br>Calls this interface to log out, it is impossible to call methods related to out\-of\-room messages and end\-to\-server messages or receive related callbacks. |
|[login](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-login) |Log in to RTS server.<br><br>Log in to call [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendusermessageoutsideroom) and [sendServerMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendservermessage) to send P2P messages or send messages to a server without joining the RTC room.<br><br>To log out, call [logout](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-logout). |
|[sendLivePushSEIMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendlivepushseimessage) |Sends SEI data in Key\-Value format through video frames.<br><br>Before calling this API, you must call [setLiveMode](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-setlivemode) and set the room live mode to `kRoomLiveModeSoloHost`. |



|Callback |Description |
|---|---|
|[onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onroommessagereceived) |Receives a callback for broadcast messages in the room. |
|[onSEIStreamUpdate](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onseistreamupdate) |Callback about publishing status of the black frame video stream .<br><br>In a voice call scenario, when the local user calls [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendseimessage) to send SEI data with a black frame, the sending status of the stream is notified to the remote user through this callback.<br><br>You can tell from this callback that the video frame carrying SEI data is a black frame and thus not render that video frame. |
|[onServerMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onservermessagesendresult) |Receives the callback after sending the message to the application server successfully. |
|[onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom-2) |This callback is triggered when a binary message is received from a user outside the room who calls [sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-senduserbinarymessageoutsideroom). |
|[onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onusermessagereceivedoutsideroom-2) |Triggered when you receive a text message from a user outside the room by calling [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendusermessageoutsideroom). |
|[onUserMessageSendResultOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onusermessagesendresultoutsideroom) |Callback for the result of sending a message to a user outside the room.<br><br>Triggered after sending a message to a user outside the room via [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendusermessageoutsideroom) or [sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-senduserbinarymessageoutsideroom). |
|[onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom) |\> This callback will be deprecated in version 3.64. Please use [onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom-2) instead.<br><br>Triggered when a binary message is received from a user outside the room who called [sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-senduserbinarymessageoutsideroom). |
|[onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onusermessagereceivedoutsideroom) |\> This interface will be deprecated in version 3.64. Please use [onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onusermessagereceivedoutsideroom-2) instead.<br><br>Triggered when a text message is received from a user outside the room who called [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendusermessageoutsideroom). |
|[onGetPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-ongetpeeronlinestatus) |The return result of querying the login status of the peer or local user |
|[onServerParamsSetResult](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onserverparamssetresult) |Set the return result of the application server parameter |
|[onLogout](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onlogout) |Callback of logout result |
|[onLoginResult](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onloginresult) |login result callback |
|[onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onuserbinarymessagereceived-2) |A single user receives a callback (P2P) of binary messages from other uid\-owned users in the same room. |
|[onUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onusermessagereceived-2) |Receive this callback when you receive a text message (P2P) from another user in the room. |
|[onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onroombinarymessagereceived-2) |Receives a callback to a binary broadcast message in the room. |
|[onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onroommessagereceived-2) |Callback for receiving room messages.<br><br>Other users in the same room will receive this callback when they call [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-sendusermessage) to send a broadcast message. |
|[onUserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onusermessagesendresult) |After sending a text or binary message (P2P) to a single user in the room, the message sender receives a callback with the result of the message. |
|[onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onuserbinarymessagereceived) |A single user receives a callback (P2P) of binary messages from other uid\-owned users in the same room.<br><br>\> The callback will be deprecated in version 3.64. Please use [onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onuserbinarymessagereceived-2) instead. |
|[onUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onusermessagereceived) |\> The interface will be deprecated in version 3.64. Please use [onUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onusermessagereceived-2) instead.<br><br>Receive this callback when you receive a text message (P2P) from another user in the room. |
|[onRoomMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onroommessagesendresult) |When the [sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTSRoom-sendroommessage) function is called to send a message, the sending result of this message (feedback) is called back. |
|[onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onroombinarymessagereceived) |Receives a callback to a binary broadcast message in the room. |


<span id="push-to-wtn"></span>
## Push to WTN


|Method |Description |
|---|---|
|[subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-subscribewtnvideostream) |Subscribe/ unsubscribe WTN video stream<br><br>A user can call this method to subscribe or unsubscribe a WTN stream whether he/she has joined the room or not. |
|[getWTNStream](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-getwtnstream) |Gets the WTN stream object.<br><br>You can use this method to get the WTN stream object to implement custom video rendering and processing.<br><br>After calling this method, you can call [subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-subscribewtnvideostream) or [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-subscribewtnaudiostream) to subscribe to the specified WTN stream.<br><br>To publish a WTN stream, call [startPushMixedStream](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startpushmixedstream). |
|[subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-subscribewtnaudiostream) |Subscribe/unsubscribe the WTN audio stream<br><br>A user can call this method to subscribe a WTN stream whether he/she has joined the room or not. |
|[setWTNRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-setwtnremotevideocanvas) |Assign a internal render view to the WTN stream |
|[setWTNRemoteVideoSink](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-setwtnremotevideosink) |Assign a custom renderer to the WTN stream. See [Custom Video Rendering](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-81201) |
|[setWTNRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-setwtnremoteaudioplaybackvolume) |Set the audio playback volume of the WTN stream. |
|[setWTNStreamEventHandler](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-setwtnstreameventhandler) |Set the WTN event handler. |



|Callback |Description |
|---|---|
|[onWTNRemoteVideoStats](https://docs.byteplus.com/en/docs/12/docs-85517#IWTNStreamEventHandler-onwtnremotevideostats) |Remote WTN video stream ID and statistics. |
|[onWTNRemoteAudioStats](https://docs.byteplus.com/en/docs/12/docs-85517#IWTNStreamEventHandler-onwtnremoteaudiostats) |Remote WTN audio stream ID and statistics. |
|[onWTNVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IWTNStreamEventHandler-onwtnvideosubscribestatechanged) |Callback for the change of WTN video stream's subscription status<br><br>You will be informed of the result of subscribing to the WTN video stream by this callback after calling [subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-subscribewtnvideostream). |
|[onWTNAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IWTNStreamEventHandler-onwtnaudiosubscribestatechanged) |Callback for the change of WTN audio stream's subscription status<br><br>You will be informed of the result of subscribing to the WTN audio stream by this callback after calling [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-subscribewtnaudiostream). |
|[onWTNFirstRemoteAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IWTNStreamEventHandler-onwtnfirstremoteaudioframe) |Callback of successfully decoding of the first audio frame of the WTN stream.<br><br>Refer to [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-subscribewtnaudiostream) for details about subscribing to a WTN audio stream. |
|[onWTNFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-85517#IWTNStreamEventHandler-onwtnfirstremotevideoframedecoded) |Callback of successfully decoding of the first video frame of the WTN stream<br><br>Refer to [subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-subscribewtnvideostream) for details about subscribing to a WTN video stream. |
|[onWTNSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IWTNStreamEventHandler-onwtnseimessagereceived) |Callback on receiving the SEI message carried by the WTN stream.<br><br>After calling [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-subscribewtnaudiostream)/[subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-subscribewtnvideostream), you will receive this callback if the WTN stream has an SEI message. |
|[onWTNDataMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IWTNStreamEventHandler-onwtndatamessagereceived) |The data information contained in the callback of WTN stream..<br><br>After calling [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-subscribewtnaudiostream)/[subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/docs-85516#IWTNStream-subscribewtnvideostream), you can listen to this callback and retrieve SEI messages inserted by Open API calls or audio volume. |


<span id="audio-mixing"></span>
## Audio Mixing


|Method |Description |
|---|---|
|[getAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-getaudioeffectplayer) |Create an instance for audio effect player. |
|[setEventHandler](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioEffectPlayer-seteventhandler) |Set the event handler. |
|[getDuration](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioEffectPlayer-getduration) |Get the duration of the audio effect file. |
|[getVolume](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioEffectPlayer-getvolume) |Gets the current volume. |
|[setVolumeAll](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioEffectPlayer-setvolumeall) |Sets the volume of all audio effect, including audio effect files and PCM effects. |
|[setVolume](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioEffectPlayer-setvolume) |Adjusts the volume level of a specified audio effect, including audio effect file and PCM effect. |
|[getPosition](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioEffectPlayer-getposition) |Gets the current position of audio effect file playback. |
|[setPosition](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioEffectPlayer-setposition) |Sets the start position of the audio effect file. |
|[resumeAll](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioEffectPlayer-resumeall) |Resumes the playback of all audio effect files. |
|[resume](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioEffectPlayer-resume) |Resumes the playback of audio effect files. |
|[pauseAll](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioEffectPlayer-pauseall) |Pauses the Playback of all audio effect files. |
|[pause](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioEffectPlayer-pause) |Pauses the playback of audio effect files. |
|[unloadAll](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioEffectPlayer-unloadall) |Unloads all audio effect files. |
|[unload](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioEffectPlayer-unload) |Unloads the specified audio effect file. |
|[preload](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioEffectPlayer-preload) |Preloads specified music files into memory to avoid repeated loading when playing the same file frequently and reduce CPU usage. |
|[stopAll](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioEffectPlayer-stopall) |Stops playback of all audio effect files. |
|[stop](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioEffectPlayer-stop) |Stops the playback of audio effect files. |
|[start](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioEffectPlayer-start) |Starts to play the audio effect file.<br><br>This API can be called multiple times with different IDs and filepaths for multiple effects at the same time. |
|[setEventHandler](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-seteventhandler) |Set the event handler. |
|[pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-pushexternalaudioframe) |Push PCM audio frame data for mixing. |
|[registerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-registeraudioframeobserver) |Register an observer to receive related callbacks when the local media file is mixing. |
|[setLoudness](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-setloudness) |To call [enableVocalInstrumentBalance](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-enablevocalinstrumentbalance) to adjust the volume of the mixed media file or the PCM audio data, you must pass in its original loudness through this API. |
|[setProgressInterval](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-setprogressinterval) |Set the interval of the periodic callback [onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-85517#IMediaPlayerEventHandler-onmediaplayerplayingprogress) during audio mixing. |
|[setPlaybackSpeed](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-setplaybackspeed) |Set the playback speed of the audio file. |
|[selectAudioTrack](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-selectaudiotrack) |Specifies the playback track of the current media file. |
|[getAudioTrackCount](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-getaudiotrackcount) |Gets the track count of the current media file. |
|[setAudioDualMonoMode](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-setaudiodualmonomode) |Sets the channel mode of the mixing of the media file. |
|[setPosition](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-setposition) |Sets the starting playback position of the media file. |
|[setAudioPitch](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-setaudiopitch) |Set the pitch of the local audio file mixing. Usually used in karaoke scenes. |
|[getState](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-getstate) |Get the state of the media player. |
|[getPosition](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-getposition) |Gets the playback progress of the media file. |
|[getPlaybackDuration](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-getplaybackduration) |Gets the actual playback duration of the mixed media file, in milliseconds. |
|[getTotalDuration](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-gettotalduration) |Gets the duration of the media file. |
|[getVolume](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-getvolume) |Gets the current volume. |
|[setVolume](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-setvolume) |Adjusts the volume of the specified audio mixing, including media file mixing and PCM mixing. |
|[resume](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-resume) |After calling [pause](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-pause) to pause audio mixing, call this API to resume audio mixing. |
|[pause](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-pause) |After calling [open](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-open), or [start](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-start) to start audio mixing, call this API to pause audio mixing. |
|[stop](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-stop) |After calling [open](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-open), [start](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-start), or [openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-openwithcustomsource) to start audio mixing, call this method to stop audio mixing. |
|[openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-openwithcustomsource) |Enable audio mixing with audio raw data.<br><br>To open the audio file, see [open](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-open). `open` and this API are mutually exclusive. |
|[start](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-start) |Start playing the audio. Call this API when you call [open](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-open) and set `AutoPlay=False`. |
|[open](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-open) |Open the audio file.<br><br>You can only open one audio file with one player instance at the same time. For multiple audio files at the same time, create multiple player instances.<br><br>For audio file in PCM format, see [openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-openwithcustomsource). `openWithCustomSource` and this API are mutually exclusive. |
|[getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-getmediaplayer) |Create a media player instance. |



|Callback |Description |
|---|---|
|[onAudioEffectPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IAudioEffectPlayerEventHandler-onaudioeffectplayerstatechanged) |Callback for audio mixing status change. |
|[onAudioMixingPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onaudiomixingplayingprogress) |Callback for playback progress of mixed audio files |
|[onMediaPlayerEvent](https://docs.byteplus.com/en/docs/12/docs-85517#IMediaPlayerEventHandler-onmediaplayerevent) |Callback for media player events. You would receive the notification after calling [selectAudioTrack](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-selectaudiotrack) and [setPosition](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-setposition). |
|[onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-85517#IMediaPlayerEventHandler-onmediaplayerplayingprogress) |Periodic callback for audio mixing progress. The period is set by [setProgressInterval](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-setprogressinterval). |
|[onMediaPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IMediaPlayerEventHandler-onmediaplayerstatechanged) |Callback for audio mixing status change. |
|[onSeek](https://docs.byteplus.com/en/docs/12/docs-85517#IMediaPlayerCustomSourceProvider-onseek) |Seeking the audio data based on the set starting position and offset to help SDK read and analyze data.<br><br>When you call [openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-openwithcustomsource) API to play the in\-memory audio data you input, or when you call [setPosition](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-setposition) to set the starting position of audio playing, this callback will be trigerred and you need to seek the audio data accorring to the value of offset and whence. |
|[onReadData](https://docs.byteplus.com/en/docs/12/docs-85517#IMediaPlayerCustomSourceProvider-onreaddata) |Callback of getting the path and size of the audio data you input.<br><br>When you call [openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-85516#IMediaPlayer-openwithcustomsource) API to play the in\-memory audio data you input, this callback will be triggered and you need to enter the path and size of the audio data. |
|[onFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IMediaPlayerAudioFrameObserver-onframe) |The callback for the audio frames during local audio file mixing. |


<span id="screen-sharing"></span>
## Screen Sharing


|Method |Description |
|---|---|
|[muteScreenAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-mutescreenaudiocapture) |Mutes/unmutes the audio captured when screen sharing.<br><br>Calling this method will send muted data instead of the screen audio data, and it does not affect the local audio device capture status and the SDK audio stream publishing status. |
|[release](https://docs.byteplus.com/en/docs/12/docs-85516#IScreenCaptureSourceList-release) |If you are finished with the [IScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/docs-85516#IScreenCaptureSourceList), call this API to destruct it and release the memory. |
|[getSourceInfo](https://docs.byteplus.com/en/docs/12/docs-85516#IScreenCaptureSourceList-getsourceinfo) |According to the index, get the elements in the screen share list |
|[getCount](https://docs.byteplus.com/en/docs/12/docs-85516#IScreenCaptureSourceList-getcount) |Get the length of the list |
|[startScreenAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startscreenaudiocapture) |When sharing the screen, start using RTC SDK internal collection method to collect screen audio |
|[stopScreenAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-stopscreenaudiocapture) |Stop RTC SDK's device audio recorder. |
|[getWindowAppIcon](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-getwindowappicon) |Get application window preview thumbnail for screen sharing. |
|[getThumbnail](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-getthumbnail) |Get the preview thumbnail of the screen\-sharing object |
|[getScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-getscreencapturesourcelist) |Get the item list for screen sharing. |
|[updateScreenCaptureMouseCursor](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-updatescreencapturemousecursor) |Update the processing settings for the mouse when capturing screen video streams through the capture module provided by the RTC SDK. Default acquisition mouse. |
|[updateScreenCaptureHighlightConfig](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-updatescreencapturehighlightconfig) |Update border highlighting settings when capturing screen video streams through the capture module provided by the RTC SDK. The default display table box. |
|[stopScreenVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-stopscreenvideocapture) |Stop screen video streaming. |
|[startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startscreenvideocapture) |Capture screen video stream for sharing. Screen video stream includes: content displayed on the screen, in the application window, or in the virtual screen.<br><br>Displaying contents in virtual screens is only available on Windows. |
|[updateScreenCaptureRegion](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-updatescreencaptureregion) |Update the capture area when capturing screen video streams through the capture module provided by the RTC SDK. Only used when the capture source is the monitor screen. |
|[setScreenCaptureVolume](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setscreencapturevolume) |Adjusts the volume of audio captured during screen sharing.<br><br>This method only changes the volume of audio data and does not affect the hardware volume of the local device. |



|Callback |Description |
|---|---|
|[onProcessScreenAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IAudioFrameProcessor-onprocessscreenaudioframe) |Returns the address of the shared\-screen audio frames for custom processing. |


<span id="security-and-encryption"></span>
## Security and Encryption


|Method |Description |
|---|---|
|[setEncryptInfo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setencryptinfo) |Sets the way to use built\-in encryption when transmitting. |
|[setLocalProxy](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setlocalproxy) |Sets local proxy. |
|[stopCloudProxy](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-stopcloudproxy) |Stop cloud proxy |
|[startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startcloudproxy) |Start cloud proxy |
|[setCustomizeEncryptHandler](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setcustomizeencrypthandler) |Sets custom encryption and decryption methods. |



|Callback |Description |
|---|---|
|[onEncryptData](https://docs.byteplus.com/en/docs/12/docs-85517#IEncryptHandler-onencryptdata) |Custom encryption.<br><br>Encrypts audio & video frame data before transmission using the custom encryption method set.<br><br>Encryption of the original audio and video frames is currently not available. |
|[onLocalProxyStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onlocalproxystatechanged) |Callback on local proxy connection. After calling [setLocalProxy](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setlocalproxy) to set local proxies, you will receive this callback that informs you of the states of local proxy connection. |
|[onCloudProxyConnected](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-oncloudproxyconnected) |Receives the callback when you call [startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startcloudproxy) to start cloud proxy, and the SDK connects the proxy server successfully. |
|[onDecryptData](https://docs.byteplus.com/en/docs/12/docs-85517#IEncryptHandler-ondecryptdata) |Custom decryption.<br><br>Decrypts custom encrypted audio & video frame data. For custom encryption, see [onEncryptData](https://docs.byteplus.com/en/docs/12/docs-85517#IEncryptHandler-onencryptdata). |


<span id="advanced-features"></span>
## Advanced Features


|Method |Description |
|---|---|
|[setAnsMode](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setansmode) |Set the Active Noise Cancellation(ANC) mode during audio and video communications. |
|[stopAudioRecording](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-stopaudiorecording) |Stop audio recording. |
|[startAudioRecording](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startaudiorecording) |Starts recording audio communication, and generate the local file.<br><br>If you call this API before or after joining the room without internal audio capture, then the recording task can still begin but the data will not be recorded in the local files. Only when you call [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startaudiocapture) to enable internal audio capture, the data will be recorded in the local files. |
|[stopFileRecording](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-stopfilerecording) |Stop local recording |
|[startFileRecording](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startfilerecording) |This method records the audio & video data during the call to a local file. |



|Callback |Description |
|---|---|
|[onExtensionAccessError](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onextensionaccesserror) |Failed to access the extension.<br><br>RTC SDK provides some features with extensions. Without implementing the extension, you cannot use the corresponding feature. |
|[onAudioRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onaudiorecordingstateupdate) |When calling [startAudioRecording](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startaudiorecording) or [stopAudioRecording](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-stopaudiorecording) to change the recording status, receive the callback. |
|[onRecordingProgressUpdate](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onrecordingprogressupdate) |Local recording progress callback.<br><br>This callback is triggered by [startFileRecording](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startfilerecording). When the recording state is normal, the system will prompt the recording progress through this callback every second. |
|[onRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onrecordingstateupdate) |Get a callback of the local recording status.<br><br>The callback is triggered by [startFileRecording](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startfilerecording) or [stopFileRecording](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-stopfilerecording). |
