---
title: "Overview"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104477"
---

<span id="engine-management"></span>
## Engine Management


|Method |Description |
|---|---|
|[createEngine](https://docs.byteplus.com/en/docs/12/docs-104478#byteplusrtc-createengine) |Call this API to create an IRTCEngine instance that provides RTC service.<br><br>Call this API before calling any other APIs within the RTC SDK.<br><br>Calling this API repeatedly will create multiple IRTCEngine instances. |
|[destroyEngine](https://docs.byteplus.com/en/docs/12/docs-104478#byteplusrtc-destroyengine) |Call this API to destroy the IRTCEngine instance created by [createEngine](https://docs.byteplus.com/en/docs/12/docs-104478#createengine). |
|[setBusinessId](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setbusinessid) |Set the business ID.<br><br>You can use businessId to distinguish different business scenarios. You can customize your businessId to serve as a sub AppId, which can share and refine the function of the AppId, but it does not need authentication. |
|[getSdkVersion](https://docs.byteplus.com/en/docs/12/docs-104478#byteplusrtc-getsdkversion) |Get the current version of the SDK. |
|[isSupported](https://docs.byteplus.com/en/docs/12/docs-104478#byteplusrtc-issupported) |Call this API to check whether the browser is supported. |
|[getSupportedCodecs](https://docs.byteplus.com/en/docs/12/docs-104478#byteplusrtc-getsupportedcodecs) |Gets the codec type supported by current browser.<br><br>If you have enabled vp8 codec, you can call the API to check whether the current browser supports vp8 encoding type before entering the room. |
|[setLogConfig](https://docs.byteplus.com/en/docs/12/docs-104478#byteplusrtc-setlogconfig) |Configures the logging level of local cache, and the maximum cache space that can be used. |
|[downloadLog](https://docs.byteplus.com/en/docs/12/docs-104478#byteplusrtc-downloadlog) |Download the generated local cache file. |


<span id="device-management"></span>
## Device Management


|Method |Description |
|---|---|
|[enumerateDevices](https://docs.byteplus.com/en/docs/12/docs-104478#byteplusrtc-enumeratedevices) |Call this API to enumerate media devices and their IDs, such as microphones, cameras, and headsets.<br><br>Call this API to get deviceId used to specify the device when calling [setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-104478#setaudioplaybackdevice), [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startvideocapture), and [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startaudiocapture). |
|[enableDevices](https://docs.byteplus.com/en/docs/12/docs-104478#byteplusrtc-enabledevices) |Call this API to request access to video and audio devices. |
|[enumerateAudioCaptureDevices](https://docs.byteplus.com/en/docs/12/docs-104478#byteplusrtc-enumerateaudiocapturedevices) |Call this API to enumerate microphone devices.<br><br>Call this API to get Device IDs used to specify the device when calling [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startaudiocapture) and [setAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-104478#setaudiocapturedevice). |
|[enumerateVideoCaptureDevices](https://docs.byteplus.com/en/docs/12/docs-104478#byteplusrtc-enumeratevideocapturedevices) |Call this API to enumerate audio and video devices and their IDs, such as microphones, cameras, and headsets.<br><br>Call this API to get Device IDs used to specify the device when calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startvideocapture) and [setVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-104478#setvideocapturedevice). |
|[enumerateAudioPlaybackDevices](https://docs.byteplus.com/en/docs/12/docs-104478#byteplusrtc-enumerateaudioplaybackdevices) |Call this API to enumerate audio playback devices and their IDs, such as speakers and headsets.<br><br>Call this API to get Device IDs used to specify the device when calling [setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-104478#setaudioplaybackdevice). |
|[startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-startaudioplaybackdevicetest) |Start the playback test for the local audio device. RTC will start playing the audio file specified. And RTC will notify the audio volume via the [onAudioPlaybackDeviceTestVolume](https://docs.byteplus.com/en/docs/12/docs-104479#onaudioplaybackdevicetestvolume) periodically. |
|[stopAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-stopaudioplaybackdevicetest) |Stop the playback test for the local audio device. |
|[startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-startaudiodevicerecordtest) |Start the capture and playback test for local audio devices.<br><br>We recommend registering [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104479#onlocalaudiopropertiesreport) callback via [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104478#enableaudiopropertiesreport). Once the test starts, you can get the volume of the capturing audio by this callback. |
|[stopAudioDeviceRecordAndPlayTest](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-stopaudiodevicerecordandplaytest) |Call this API to stop recording in the test and start to play the recording.<br><br>After calling [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-104478#startaudiodevicerecordtest), you need to call this API within 30 seconds. Otherwise, the recording will automatically stop and begin playing back the recorded audio. |
|[stopAudioDevicePlayTest](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-stopaudiodeviceplaytest) |Stop the capture and playback test for local audio devices started by calling [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-104478#startaudiodevicerecordtest).<br><br>Before the test ends by itself, you can call this API to stop the recording or playing. |
|[onAudioPlaybackDeviceTestVolume](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onaudioplaybackdevicetestvolume) |Remote audio properties report callback |
|[setAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setaudiocapturedevice) |Switch the microphone used for internal audio capturing. |
|[onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onaudiodevicestatechanged) |Triggered when the audio device connection state changes. For example, due to device disconnection or reconnection.<br><br>\> You need to get microphone or speaker permission ([enableDevices](https://docs.byteplus.com/en/docs/12/docs-104478#enabledevices)) before you can receive this callback. |
|[setVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setvideocapturedevice) |Switch the camera used for internal video capturing. |
|[onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onvideodevicestatechanged) |Triggered when the video device connection state changes. For example, due to device disconnection or reconnection.<br><br>\> You need to get camera permission ([enableDevices](https://docs.byteplus.com/en/docs/12/docs-104478#enabledevices)) before you can receive this callback. |


<span id="room-management"></span>
## Room Management


|Method |Description |
|---|---|
|[joinRoom](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-joinroom) |Join an existing room or create a new room and join.<br><br>When calling this method, you need to specify the `roomId`. If a room corresponding to the specified roomId already exists, the SDK will directly join that room. If no room corresponds to the specified roomId, the SDK will automatically create a new room using that roomId and join it. |
|[leaveRoom](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-leaveroom) |Leave the room.<br><br>The user calls this API to leave the room, end the call process, and release all call\-related resources. |
|[getCallId](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-getcallid) |Get the call ID. Call this method after joining a room.<br><br>After creating a room, a `callId` is generated to identify the call for this room. |
|[updateToken](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-updatetoken) |Update Token.<br><br>You will receive [onTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-104479#ontokenwillexpire) 30 s before the Token expires. Call this API to submit a new Token. |
|[setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setuservisibility) |Set user visibility. The local user is visible to others by default before calling this API.<br><br>An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Room Capability](https://docs.byteplus.com/en/docs/12/docs-257549). |
|[setAudioSelectionConfig](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setaudioselectionconfig) |Set the priority of the local audio stream to be published. |
|[onUserJoined](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserjoined) |Callback for a remote visible user joining the room, or an invisible user in the room switching to visible. |
|[onUserLeave](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserleave) |Callback for a remote visible user leaving the room, or a visible user in the room switching to invisible. |
|[onConnectionStateChanged](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onconnectionstatechanged) |Connection state changed |
|[onError](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onerror) |An error occurred in the SDK. |
|[onTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-ontokenwillexpire) |You will receive this callback 30 seconds before the Token expires.<br><br>Call [updateToken](https://docs.byteplus.com/en/docs/12/docs-104478#updatetoken) to submit a new Token. The user will be removed from the room when the Token expires. |
|[onTokenPublishPrivilegeWillExpire](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-ontokenpublishprivilegewillexpire) |This callback will be triggered 30 seconds before the token publishing permission expires.<br><br>Upon receiving this callback, call [updateToken](https://docs.byteplus.com/en/docs/12/docs-104478#updatetoken) to update the token. |
|[onTokenPublishPrivilegeDidExpired](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-ontokenpublishprivilegedidexpired) |This callback is triggered when the token publishing permission expires. Call [updateToken](https://docs.byteplus.com/en/docs/12/docs-104478#updatetoken) to update the Token. |
|[onTokenSubscribePrivilegeWillExpire](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-ontokensubscribeprivilegewillexpire) |This callback will be triggered 30 seconds before the token subscription permission expires.<br><br>Upon receiving this callback, call [updateToken](https://docs.byteplus.com/en/docs/12/docs-104478#updatetoken) to update the token. |
|[onTokenSubscribePrivilegeDidExpired](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-ontokensubscribeprivilegedidexpired) |This callback is triggered when the token subscription permission expires. Call [updateToken](https://docs.byteplus.com/en/docs/12/docs-104478#updatetoken) to update the Token. |


<span id="audio-management"></span>
## Audio Management


|Method |Description |
|---|---|
|[setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setaudioplaybackdevice) |Sets the speaker or the earpiece as the audio playback device. The audio playback device defaults to the speaker. |
|[startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-startaudiocapture) |Start internal audio capture. The default is off.<br><br>Internal audio capture refers to: capturing audio using the built\-in module.<br><br>The remote clients in the room will be informed of the state change via [onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104479#onuserstartaudiocapture) after the publisher starts audio capture by calling this API. |
|[startAudioAndVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-startaudioandvideocapture) |Enable audio and video capture using the internal capture module. When calling this method, the browser will request microphone and camera permissions simultaneously, and the user only needs to grant permission once.<br><br>When calling this method, other users in the room will receive the callback of [onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104479#onuserstartvideocapture) and [onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104479#onuserstartaudiocapture). |
|[stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-stopaudiocapture) |Stop internal audio capture. The default is off.<br><br>Internal audio capture refers to: capturing audio using the built\-in module.<br><br>The remote clients in the room will be informed of the state change via [onUserStopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104479#onuserstopaudiocapture) after stopping audio capture by calling this API. |
|[setAudioProfile](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setaudioprofile) |Set the sound quality. |
|[setCaptureVolume](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setcapturevolume) |Adjust audio capture volume. |
|[setPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setplaybackvolume) |Adjust audio playback volume of a specified remote user. |
|[getAudioVolume](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-getaudiovolume) |Gets the volume of the remote audio stream or the local audio stream captured by the local microphone and screen audio stream. |
|[setAudioCaptureConfig](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setaudiocaptureconfig) |Configure the internal audio capture. Different browsers have their own default settings. |
|[enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-enableaudiopropertiesreport) |Enable audio information prompts. |
|[onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onlocalaudiopropertiesreport) |After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104478#enableaudiopropertiesreport), you will periodically receive this callback for the instant information about local audio.<br><br>Local audio includes the microphone audio and the screen audio captured using RTC SDK internal mechanisms. |
|[onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onremoteaudiopropertiesreport) |After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104478#enableaudiopropertiesreport), you will receive the cycling callbacks, each providing instant information about the subscribed remote audio streams.<br><br>The remote audio streams include the microphone audio and screen audio collected using the RTC SDK internal mechanism/custom mechanism. |
|[onActiveSpeaker](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onactivespeaker) |After calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-104478#enableaudiopropertiesreport), you will periodically receive this callback for the information of the user with the highest voice volume. |
|[onAudioPlaybackDeviceChanged](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onaudioplaybackdevicechanged) |The current playback device has been changed successfully by calling [setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-104478#setaudioplaybackdevice). |
|[onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserstartaudiocapture) |The remote clients in the room will be informed of the state change via this event after the publisher starts audio capture by calling [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startaudiocapture). |
|[onUserStopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserstopaudiocapture) |The remote clients in the room will be informed of the state change via this event after the publisher stops audio capture by calling [stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104478#stopaudiocapture). |
|[setEarMonitorMode](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setearmonitormode) |Enable/Disable in\-ear monitoring. |
|[setEarMonitorVolume](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setearmonitorvolume) |Set the monitoring volume. |


<span id="video-management"></span>
## Video Management


|Method |Description |
|---|---|
|[startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-startvideocapture) |Enable internal video capture. The default state is off.<br><br>Internal video capture refers to: capturing video using the built\-in module.<br><br>The remote clients in the room will be informed of the state change via [onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104479#onuserstartvideocapture) after the publisher starts video capture by calling this API. |
|[stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-stopvideocapture) |Stop internal video capture immediately.<br><br>Internal video capture refers to: capturing video using the built\-in module.<br><br>The remote clients in the room will be informed of the state change via [onUserStopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104479#onuserstopvideocapture) after the publisher stops video capture by calling this API. |
|[setLocalVideoPlayer](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setlocalvideoplayer) |Add the local media stream to a player and set the rendering mode for the rendering of the local stream.<br><br>Listen to `onPlayerEvent` for the state after binding a view to the local video stream.<br><br>Call this API again with a blank view to remove the stream from the player. Doing this without a playerId while there are multiple players including a default player will remove the stream from the default player. |
|[setRemoteVideoPlayer](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setremotevideoplayer) |Add the remote media stream to a player and set the rendering mode for the rendering of the remote stream.<br><br>It is recommended to call this API and bind a view once the event of [onUserPublishStream](https://docs.byteplus.com/en/docs/12/docs-104479#onuserpublishstream)/[onUserPublishScreen](https://docs.byteplus.com/en/docs/12/docs-104479#onuserpublishscreen) is triggered.<br><br>Call this API again with a blank view to remove the stream from the player. Doing this without a playerId while there are multiple players including a default player will remove the stream from the default player. |
|[play](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-play) |Play audio and video stream manually.<br><br>Call this API when the user needs to take part in the audio and video interaction after calling [createEngine](https://docs.byteplus.com/en/docs/12/docs-104478#createengine) and setting autoPlay to False. |
|[stop](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-stop) |Pause the specified media stream. |
|[setLocalVideoMirrorType](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setlocalvideomirrortype) |Enable or disable the mirror mode for the local video stream. |
|[setRemoteVideoMirrorType](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setremotevideomirrortype) |When using internal rendering, enable mirroring for the remote stream. |
|[setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setvideoencoderconfig) |Configures the encoding settings for the camera videos on the publisher side. |
|[setDummyCaptureImagePath](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setdummycaptureimagepath) |Set the placeholder image during local video capture pause |
|[onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserstartvideocapture) |The remote clients in the room will be informed of the state change via this event after the publisher starts video capture by calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startvideocapture). |
|[onUserStopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserstopvideocapture) |The remote clients in the room will be informed of the state change via this event after the publisher stops video capture by calling [stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104478#stopvideocapture). |
|[onLocalVideoSizeChanged](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onlocalvideosizechanged) |The callback of the actual video capturing configuration. |
|[onPlayerEvent](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onplayerevent) |Player event |
|[onAutoplayFailed](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onautoplayfailed) |Auto\-play fails. |
|[onTrackEnded](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-ontrackended) |Media track ended event. Please restart capture in the callback thread. |
|[onPlayerVisibility](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onplayervisibility) |Event of player visibility change, triggered every 30 seconds to notify users of changes in the visibility status of the player. |
|[getLocalVideoPlayerVisibility](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-getlocalvideoplayervisibility) |Get the visibility state of local video player and reasons for invisibility. |
|[getRemotePlayerVisibility](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-getremoteplayervisibility) |Gets the visibility state of remote video player and reasons for invisibility. |


<span id="audio-video-transport"></span>
## Audio & Video Transport


|Method |Description |
|---|---|
|[publishStream](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-publishstream) |Publishes media streams captured by camera/microphone in the current room. |
|[onRemoteStatsException](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onremotestatsexception) |SDK detects an abnormal event, which is usually caused by external factors such as network or capture/playback devices. The abnormal event is not an error, but it usually causes a problem with the call quality. If the problem is resolved, you will also receive this callback. |
|[onLocalStatsException](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onlocalstatsexception) |SDK detects an abnormal event, which is usually caused by external factors such as network or capture/playback devices. The abnormal event is not an error, but it usually causes a problem with the call quality. If the problem is resolved, you will also receive this callback. |
|[unpublishStream](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-unpublishstream) |Stops publishing media streams captured by camera/microphone in the current room. |
|[subscribeStream](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-subscribestream) |Subscribes to specific remote media streams captured by camera/microphone.<br><br>You can call this API in both automatic subscription mode and manual subscription mode. |
|[unsubscribeStream](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-unsubscribestream) |Unsubscribes from specific remote media streams captured by camera/microphone.<br><br>You can call this API in both automatic subscription mode and manual subscription mode. |
|[pauseAllSubscribedStream](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-pauseallsubscribedstream) |Pause receiving remote media streams. |
|[resumeAllSubscribedStream](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-resumeallsubscribedstream) |Resume receiving remote media streams |
|[setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setlocalsimulcastmode) |Enables the Simulcast feature and configures the lower\-quality camera videos for the stream publisher. |
|[setRemoteSimulcastStreamType](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setremotesimulcaststreamtype) |Sets your expected quality level of the remote video stream that you want to subscribe to or have subscribed to. |
|[setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setsubscribefallbackoption) |Set the fallback option for remote media stream<br><br>Fallback means to enable media stream fallback or to subscribe to only audio stream under poor network conditions to ensure smooth communication. |
|[setRemoteUserPriority](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setremoteuserpriority) |Set the priority of the remote user's media stream.<br><br>Use this API with [setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/docs-104478#setsubscribefallbackoption).<br><br>With video stream fallback enabled and user priority specified, the stream quality of higher priority user is the last to be compromised. |
|[startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-startforwardstreamtorooms) |Start forwarding media stream across rooms. See [Forward media stream across rooms](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104398) for details.<br><br>After calling [joinRoom](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-joinroom), you can call this API to publish the media stream to multiple rooms. This feature is suitable for scenarios such as co\-host PK and online karaoke. |
|[updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-updateforwardstreamtorooms) |Update information of the rooms where the stream will be forwarded after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-startforwardstreamtorooms). |
|[stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-stopforwardstreamtorooms) |Stop forwarding media stream to all rooms. |
|[pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-pauseforwardstreamtoallrooms) |Pause forwarding media stream to all rooms.<br><br>After calling this API, call [resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-resumeforwardstreamtoallrooms) to resume. |
|[resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-resumeforwardstreamtoallrooms) |Resume forwarding media stream to all rooms. |
|[onUserPublishStream](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserpublishstream) |Callback on new media streams captured by camera/microphone in the room. |
|[onUserUnpublishStream](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserunpublishstream) |Callback on removal of remote media stream captured by camera/microphone. |
|[onRemoteVideoFirstFrame](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onremotevideofirstframe) |The first video frame rendered. |
|[getRemoteVideoStats](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-getremotevideostats) |Gets the statistics of subscribed video streams and network states. |
|[onRemoteAudioFirstFrame](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onremoteaudiofirstframe) |First remote audio frame received |
|[getRemoteAudioStats](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-getremoteaudiostats) |Gets the statistics of subscribed audio streams and network states. |
|[getLocalVideoStats](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-getlocalvideostats) |Gets the statistics of local video streams and network states. |
|[getLocalAudioStats](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-getlocalaudiostats) |Gets the statistics of local audio streams and network states. |
|[onRemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onremotestreamstats) |Statistics of subscribed media streams and network states in a cycle of 2s |
|[onLocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onlocalstreamstats) |Statistics of local media streams and network states in a cycle of 2s |
|[onAutoSubscribeResult](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onautosubscriberesult) |Result of the Auto\-Subscription |
|[onAutoPublishResult](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onautopublishresult) |Result of Auto\-publishing. You will receive this event if you enable Auto\-publish when calling `joinRoom` |
|[onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onnetworkquality) |The callback reports the upstream and downstream network quality of the local user every 2s after the user enters the room. |
|[onSimulcastSubscribeFallback](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onsimulcastsubscribefallback) |Receives this callback when fallback happens or the stream recovers from fallback. |
|[onRemoteVideoSizeChanged](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onremotevideosizechanged) |When the resolution of remote video changes, users who subscribed to the stream will receive this callback. |
|[onVideoStreamBanned](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onvideostreambanned) |The callback is triggered when the openAPI BanUserStream/UnbanUserStream is called to ban/unban the video stream of the specified user from publishing. |
|[onAudioStreamBanned](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onaudiostreambanned) |The callback is triggered when the openAPI BanUserStream/UnbanUserStream is called to ban/unban the audio stream of the specified user from publishing. |
|[onForwardStreamError](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onforwardstreamerror) |Event of failing to forward stream across rooms. |


<span id="wtn-stream"></span>
## WTN Stream


|Method |Description |
|---|---|
|[startPushPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-startpushpublicstream) |Starts publishing a WTN stream after the user joins a room. |
|[updatePublicStreamParam](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-updatepublicstreamparam) |Update the properties of the WTN stream published by the current user via [startPushPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-startpushpublicstream). |
|[stopPushPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-stoppushpublicstream) |Stops publishing the WTN stream published by the current user via [startPushPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-startpushpublicstream). |
|[onPushPublicStreamResult](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onpushpublicstreamresult) |Callback of the result of publishing the WTN stream.<br><br>After calling [startPushPublicStream](https://docs.byteplus.com/en/docs/12/docs-104478#startpushpublicstream), you will be informed of the result through this callback. |
|[getWTNStreamManager](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-getwtnstreammanager) |Creates a WTN stream manager object. |
|[startPushWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startpushwtn) |Starts publishing a WTN stream without joining a room. |
|[stopPushWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-stoppushwtn) |Stops publishing the WTN stream which was published via [startPushWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startpushwtn). |
|[muteWTNLocalVideo](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-mutewtnlocalvideo) |Pauses/Resumes publishing the video of a WTN stream. |
|[muteWTNLocalAudio](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-mutewtnlocalaudio) |Pauses/Resumes publishing the audio of a WTN stream. |
|[onWTNPushStateChanged](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnpushstatechanged) |Callback of the result of publishing the WTN stream.<br><br>After calling [startPushWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startpushwtn), you will be informed of the result through this callback. |
|[startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn) |Subscribes to a designated WTN stream.<br><br>You can call this API to subscribe to a WTN stream whether you joined the room or not. |
|[stopPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-stopplaywtn) |Unsubscribes from a designated WTN stream. |
|[muteWTNRemoteAudio](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-mutewtnremoteaudio) |Pauses/Resumes subscribing to the audio of a WTN stream. |
|[muteWTNRemoteVideo](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-mutewtnremotevideo) |Pauses/Resumes subscribing to the video of a WTN stream. |
|[setWTNRemoteVideoPlayer](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-setwtnremotevideoplayer) |Sets the player information and rendering mode for the WTN stream. |
|[setWTNRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-setwtnremoteaudioplaybackvolume) |Adjusts audio playback volume of a WTN stream. |
|[onWTNRemoteAudioStateChanged](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnremoteaudiostatechanged) |Callback of the subscription state of the audio of the WTN stream.<br><br>After calling [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn), you will be informed of the result through this callback. |
|[getWTNVideoPlayerVisibility](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-getwtnvideoplayervisibility) |Gets the visibility status of the specified WTN stream's video player. |
|[onWTNRemoteVideoStateChanged](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnremotevideostatechanged) |Callback of the subscription state of the video of the WTN stream.<br><br>After calling [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn), you will be informed of the result through this callback. |
|[onWTNPlayStateChanged](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnplaystatechanged) |Callback of the result of subscribing to the WTN stream.<br><br>After calling [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn), you will be informed of the result through this callback. |
|[onWTNRemoteAudioStats](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnremoteaudiostats) |Callback carrying the audio statistics of the WTN stream.<br><br>You can receive this callback every 2 seconds after subscribing to the audio of a WTN stream via [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn). |
|[onWTNRemoteVideoStats](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnremotevideostats) |Callback carrying the video statistics of the WTN stream.<br><br>You can receive this callback every 2 seconds after subscribing to the video of a WTN stream via [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn). |
|[onWTNFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnfirstremotevideoframedecoded) |Callback of the successful decoding of the first video frame of the WTN stream.<br><br>Refer to [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn) for details about subscribing to a WTN stream. |
|[sendWTNSEIMessage](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-sendwtnseimessage) |Sends SEI via a WTN stream. |
|[onWTNSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnseimessagereceived) |Callback of the SEI carried by the public video stream.<br><br>You will receive SEI by this callback if the WTN stream you subscribed to by calling [startPlayWTN](https://docs.byteplus.com/en/docs/12/docs-104478#wtnstream-startplaywtn) is carrying SEI. |
|[onWTNLocalStatsException](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnlocalstatsexception) |Exception event callback of local WTN media stream. |
|[onWTNRemoteStatsException](https://docs.byteplus.com/en/docs/12/docs-104479#wtnstreamevents-onwtnremotestatsexception) |Exception event callback of remote WTN media stream. |


<span id="screen-sharing"></span>
## Screen Sharing


|Method |Description |
|---|---|
|[startScreenCapture](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-startscreencapture) |Use the capture module provided by the RTC SDK to capture the current screen stream for sharing. |
|[stopScreenCapture](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-stopscreencapture) |Stop screen sharing. |
|[getElectronScreenSources](https://docs.byteplus.com/en/docs/12/docs-104478#byteplusrtc-getelectronscreensources) |Get the list of screen\-sharing objects. |
|[setScreenEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setscreenencoderconfig) |Set the encoding configuration of the screen\-sharing stream, which is also applied in video capture.<br><br>If the configuration is not supported by your browser, the video will be captured based on the supported configuration. You will also receive the callback [onLocalVideoSizeChanged](https://docs.byteplus.com/en/docs/12/docs-104479#onlocalvideosizechanged). |
|[publishScreen](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-publishscreen) |Publishes local screen sharing streams in the current room. |
|[unpublishScreen](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-unpublishscreen) |Stops publishing local screen sharing streams in the current room. |
|[subscribeScreen](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-subscribescreen) |Subscribes to specific screen sharing media stream.<br><br>You can call this API in both automatic subscription mode and manual subscription mode. |
|[unsubscribeScreen](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-unsubscribescreen) |Unsubscribes from specific screen sharing media stream.<br><br>You can call this API in both automatic subscription mode and manual subscription mode. |
|[onUserPublishScreen](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserpublishscreen) |Callback on new screen sharing media streams from remote users in the room. |
|[onUserUnpublishScreen](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserunpublishscreen) |Callback on removal of screen sharing media streams from remote users in the room. |


<span id="audio-mixing"></span>
## Audio Mixing


|Method |Description |
|---|---|
|[getAudioMixingManager](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-getaudiomixingmanager) |Creates an audio mixing manager object. |
|[startAudioMixing](https://docs.byteplus.com/en/docs/12/docs-104478#audiomixingmanager-startaudiomixing) |Start playing audio files and mixes.<br><br>This method can be called many times by passing in different IDs and filepaths to realize simultaneous playback of multiple mixing files and mixing overlay. |
|[stopAudioMixing](https://docs.byteplus.com/en/docs/12/docs-104478#audiomixingmanager-stopaudiomixing) |Stop playing audio files and mixes |
|[pauseAudioMixing](https://docs.byteplus.com/en/docs/12/docs-104478#audiomixingmanager-pauseaudiomixing) |Pause playing audio files and mixes |
|[resumeAudioMixing](https://docs.byteplus.com/en/docs/12/docs-104478#audiomixingmanager-resumeaudiomixing) |Resume playing audio files and mixing |
|[preloadAudioMixing](https://docs.byteplus.com/en/docs/12/docs-104478#audiomixingmanager-preloadaudiomixing) |Preload the specified audio file into memory |
|[unloadAudioMixing](https://docs.byteplus.com/en/docs/12/docs-104478#audiomixingmanager-unloadaudiomixing) |Unload the specified audio file |
|[getAudioMixingVolume](https://docs.byteplus.com/en/docs/12/docs-104478#audiomixingmanager-getaudiomixingvolume) |Get volume of the audio files. |
|[setAudioMixingVolume](https://docs.byteplus.com/en/docs/12/docs-104478#audiomixingmanager-setaudiomixingvolume) |Adjust the volume of the audio\-file mixing. |
|[getAudioMixingDuration](https://docs.byteplus.com/en/docs/12/docs-104478#audiomixingmanager-getaudiomixingduration) |Get audio file duration |
|[getAudioMixingCurrentPosition](https://docs.byteplus.com/en/docs/12/docs-104478#audiomixingmanager-getaudiomixingcurrentposition) |Get audio file playback progress |
|[setAudioMixingPosition](https://docs.byteplus.com/en/docs/12/docs-104478#audiomixingmanager-setaudiomixingposition) |Set the starting playback position of the audio file |
|[enableAudioMixingBuffer](https://docs.byteplus.com/en/docs/12/docs-104478#audiomixingmanager-enableaudiomixingbuffer) |Start PCM mixing.<br><br>To mix multiple PCM audio streams, call this API multiple times with different IDs. |
|[disableAudioMixingBuffer](https://docs.byteplus.com/en/docs/12/docs-104478#audiomixingmanager-disableaudiomixingbuffer) |Disable PCM mixing. |
|[pushAudioMixingBuffer](https://docs.byteplus.com/en/docs/12/docs-104478#audiomixingmanager-pushaudiomixingbuffer) |Push PCM audio frame data for mixing |
|[onAudioMixingStateChanged](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onaudiomixingstatechanged) |Event of the state change of audio mixing |
|[setAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-104478#audiomixingmanager-setaudioframecallback) |Toggle the callbacks carrying the mixing audio frames. |


<span id="push-to-cdn"></span>
## Push to CDN


|Method |Description |
|---|---|
|[defaultTranscoding](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-defaulttranscoding) |Get the default parameters of `LiveTranscodeConfig`. |
|[startLiveTranscoding](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-startlivetranscoding) |Starts pushing media streams to CDN and sets the relevant configurations. |
|[updateLiveTranscoding](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-updatelivetranscoding) |Update configuration needed when pushing media streams to CDN.<br><br>After calling [startLiveTranscoding](https://docs.byteplus.com/en/docs/12/docs-104478#startlivetranscoding) to enable the function of pushing streams to CDN, you can call this API to update the relevant configurations. |
|[stopLiveTranscoding](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-stoplivetranscoding) |Stop pushing media streams to CDN<br><br>For starting pushing media streams to CDN. Refer to [startLiveTranscoding](https://docs.byteplus.com/en/docs/12/docs-104478#startlivetranscoding). |
|[onStreamMixingEvent](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onstreammixingevent) |Events of pushing a mixed stream to CDN |


<span id="custom-stream-processing"></span>
## Custom Stream Processing


|Method |Description |
|---|---|
|[setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setvideosourcetype) |Switch the source from the internal to custom video capture.<br><br>Internal video capture refers to using the built\-in video capture module. |
|[setExternalVideoTrack](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setexternalvideotrack) |Set a custom videoTrack as the video source.<br><br>Before calling this API, you must call [setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-104478#setvideosourcetype) to enable custom video capture. |
|[setAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setaudiosourcetype) |Switch the source from the internal to custom audio capture.<br><br>Internal audio capture refers to using built\-in audio capture. |
|[setExternalAudioTrack](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setexternalaudiotrack) |Set a custom audioTrack as the audio source.<br><br>Before calling this API, you must call [setAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-104478#setaudiosourcetype) to enable custom audio capture. |
|[getLocalStreamTrack](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-getlocalstreamtrack) |Get the [MediaStreamTrack](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack) of the local audio or video. |
|[getRemoteStreamTrack](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-getremotestreamtrack) |Get the [MediaStreamTrack](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack) of the remote audio or video. |
|[getPublicStreamTrack](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-getpublicstreamtrack) |Get the [MediaStreamTrack](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack) of the audio or video from the subscribed WTN stream. |
|[setRemoteStreamRenderSync](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setremotestreamrendersync) |Set whether the remote audio and video streams are rendered synchronously.<br><br>You can achieve ultra low latency by turning off the audio and video synchronization. |
|[setAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setaudioframecallback) |Toggle the callbacks carrying the audio frames. |


<span id="message"></span>
## Message


|Method |Description |
|---|---|
|[sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-sendusermessage) |Send point\-to\-point text messages to a specified user in the room.<br><br>The recipient receives the message via [onUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#onusermessagereceived) once the message is sent successfully. |
|[sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-senduserbinarymessage) |Send point\-to\-point binary messages to a specified user in the room.<br><br>The recipient receives the message via [onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#onuserbinarymessagereceived) once the message is sent successfully. |
|[sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-sendroommessage) |Send text messages to all other users in the room.<br><br>Users in the room will receive message via [onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#onroommessagereceived) once the message is sent successfully. |
|[sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-sendroombinarymessage) |Send binary messages to all other users in the room.<br><br>Users in the room will receive binary message via [onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#onroombinarymessagereceived) once the message is sent successfully. |
|[sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-sendseimessage) |Send supplemental enhancement information (SEI) through video frames.<br><br>In the video call scenario, the SEI data will be sent with the video frames. In the voice call scenario, the SDK will generate a 16px × 16px black frame video stream to send the data. |
|[login](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-login) |Sign in to the RTM server.<br><br>Call this method before users within the same `appID` can communicate with each other via messages. |
|[logout](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-logout) |Log out of the RTS service. After calling this API to log out, you are not able to call APIs to send messages and server messages. |
|[updateLoginToken](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-updatelogintoken) |Update the Token used to login. Since all tokens have a limited time\-to\-live, call this API to refresh the token. |
|[getPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-getpeeronlinestatus) |Get the status of a user before sending him/her a P2P message. You can also call this API to check the status of the current user. |
|[sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-sendusermessageoutsideroom) |Send point\-to\-point (P2P) text message to a user. |
|[sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-senduserbinarymessageoutsideroom) |Send point\-to\-point (P2P) binary message to a user. |
|[setServerParams](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-setserverparams) |Set the params of the server before calling [sendServerMessage](https://docs.byteplus.com/en/docs/12/docs-104478#sendservermessage) or [sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-104478#sendserverbinarymessage) to send messages to the server. |
|[sendServerMessage](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-sendservermessage) |Send point\-to\-point (P2P) text message to the server. |
|[sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-sendserverbinarymessage) |Send point\-to\-point (P2P) binary message to the server. |
|[onUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onusermessagereceived) |Receiving a point\-to\-point text message from one of the users in the room by calling [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-104478#sendusermessage) |
|[onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserbinarymessagereceived) |Receiving a point\-to\-point binary message from one of the users in the room |
|[onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onroommessagereceived) |Event of receiving a broadcast text message in the room |
|[onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onroombinarymessagereceived) |Event of receiving a broadcast binary message in the room |
|[onSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onseimessagereceived) |Event of receiving SEI data from video frames |
|[onSEIStreamUpdate](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onseistreamupdate) |Stream update event of stream that contains SEI information.<br><br>In a voice call scenario, when a remote user calls [sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-104478#sendseimessage) to send SEI data via the black frame video stream, the stream's sending status will be notified to the local user through this event callback.<br><br>If the video frame carrying SEI data is a black frame, you do not need to render the video frame. |
|[onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onusermessagereceivedoutsideroom) |Event of receiving a text message |
|[onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserbinarymessagereceivedoutsideroom) |Event of receiving a binary message |
|[onServerParamsSetResult](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onserverparamssetresult) |Event of whether the setting for the message server succeeds |


<span id="video-snapshot"></span>
## Video Snapshot


|Method |Description |
|---|---|
|[takeLocalSnapshot](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-takelocalsnapshot) |Take a snapshot of the local video. |
|[takeRemoteSnapshot](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-takeremotesnapshot) |Take a snapshot of the remote video. |


<span id="security-and-encryption"></span>
## Security and Encryption


|Method |Description |
|---|---|
|[startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-startcloudproxy) |Start cloud proxy |
|[stopCloudProxy](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-stopcloudproxy) |Stop cloud proxy |
|[onCloudProxyConnected](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-oncloudproxyconnected) |Receives the callback when you call [startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-104478#startcloudproxy) to start cloud proxy, and the SDK connects to the proxy server successfully. |


<span id="extensions"></span>
## Extensions


|Method |Description |
|---|---|
|[registerExtension](https://docs.byteplus.com/en/docs/12/docs-104478#rtcengine-registerextension) |Registers an extension.<br><br>You can use the extension to implement features such as [Beauty Effects](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-148646), [Virtual Background](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-148647). |
