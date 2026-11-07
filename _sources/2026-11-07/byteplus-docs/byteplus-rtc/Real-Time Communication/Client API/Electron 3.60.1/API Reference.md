---
title: "API Reference"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-85532"
---

## RTCEngine

Type: `class`

* **API**

|Method |Description |
|---|---|
|[createRTCEngine](https://docs.byteplus.com/en/docs/12/14196#rtcengine-creatertcengine) |Create an engine instance. |
|[createRTCRoom](https://docs.byteplus.com/en/docs/12/14196#rtcengine-creatertcroom) |Create a room for the call. |
|[destroyRTCEngine](https://docs.byteplus.com/en/docs/12/14196#rtcengine-destroyrtcengine) |Destroy the engine instance created by [createRTCEngine](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-creatertcengine), and release all related resources. |
|[feedback](https://docs.byteplus.com/en/docs/12/14196#rtcengine-feedback) |Report the user feedback to RTC. |
|[setBusinessId](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setbusinessid) |Sets the business ID. |
|[setEncryptInfo](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setencryptinfo) |Set the way to use built\-in encryption when transmitting. |
|[initializePluginManager](https://docs.byteplus.com/en/docs/12/14196#rtcengine-initializepluginmanager) |Initialize the plugin manager. |
|[releasePluginManager](https://docs.byteplus.com/en/docs/12/14196#rtcengine-releasepluginmanager) |Release plugin manager. |
|[registerPlugin](https://docs.byteplus.com/en/docs/12/14196#rtcengine-registerplugin) |Registers a plugin library. |
|[getPlugin](https://docs.byteplus.com/en/docs/12/14196#rtcengine-getplugin) |Gets the control interface for a registered plugin. |
|[unregisterPlugin](https://docs.byteplus.com/en/docs/12/14196#rtcengine-unregisterplugin) |Uninstall plugin. |
|[muteAudioCapture](https://docs.byteplus.com/en/docs/12/14196#rtcengine-muteaudiocapture) |Set whether to mute the recording signal (without changing the local hardware). |
|[startAudioCapture](https://docs.byteplus.com/en/docs/12/14196#rtcengine-startaudiocapture) |Start internal audio capture. The default is off. |
|[stopAudioCapture](https://docs.byteplus.com/en/docs/12/14196#rtcengine-stopaudiocapture) |Stop internal audio capture. The default is off. |
|[enumerateAudioPlaybackDevices](https://docs.byteplus.com/en/docs/12/14196#rtcengine-enumerateaudioplaybackdevices) |Get a list of the audio playback device. When the audio playback device changes, you will receive the [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onaudiodevicestatechanged), and you need to call this API again to get the new device list. |
|[enumerateAudioCaptureDevices](https://docs.byteplus.com/en/docs/12/14196#rtcengine-enumerateaudiocapturedevices) |Get a list of audio acquisition devices in the current system. If there are subsequent device changes, you need to call this interface again to get a new device list. |
|[setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setaudioplaybackdevice) |Sets the audio playback device. |
|[setAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setaudiocapturedevice) |Set up audio capture devices. |
|[getAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/14196#rtcengine-getaudioplaybackdevice) |Gets the current audio playback device ID. |
|[getAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/14196#rtcengine-getaudiocapturedevice) |Gets the current audio capture device ID. |
|[setAudioPlaybackDeviceVolume](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setaudioplaybackdevicevolume) |Set the current audio playback device volume. |
|[getAudioPlaybackDeviceVolume](https://docs.byteplus.com/en/docs/12/14196#rtcengine-getaudioplaybackdevicevolume) |Get the current audio playback device volume. |
|[setAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setaudiocapturedevicevolume) |Set the current audio capture volume. |
|[getAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/14196#rtcengine-getaudiocapturedevicevolume) |Get the current audio capture volume. |
|[setAudioPlaybackDeviceMute](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setaudioplaybackdevicemute) |Mute or Unmute the current audio playback device. The default state is speaking. |
|[getAudioPlaybackDeviceMute](https://docs.byteplus.com/en/docs/12/14196#rtcengine-getaudioplaybackdevicemute) |Get state of the audio playback device. |
|[setAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setaudiocapturedevicemute) |Mute or Unmute the current audio capture device. The default state is speaking. |
|[getAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/14196#rtcengine-getaudiocapturedevicemute) |Get state of the audio capture device. |
|[setCaptureVolume](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setcapturevolume) |Adjust the audio capture volume. |
|[setScreenCaptureVolume](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setscreencapturevolume) |Adjust the volume of the audio captured during screen sharing.<br><br>This only changes the volume property of the audio data, without affecting the microphone capture volume or the local device volume. |
|[setPlaybackVolume](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setplaybackvolume) |Adjust the playback volume of the mixed remote audios. You can call this API before or during the playback. |
|[setRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setremoteaudioplaybackvolume) |Adjust the audio playback volume of the remote user. |
|[stopAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/14196#rtcengine-stopaudioplaybackdevicetest) |Stop the playback test for the local audio device. |
|[setVoiceChangerType](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setvoicechangertype) |Set the sound effect type. |
|[setVoiceReverbType](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setvoicereverbtype) |Set the reverb effect type. |
|[setAudioProfile](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setaudioprofile) |Sets the sound quality. |
|[startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/14196#rtcengine-startaudioplaybackdevicetest) |Start the playback test for the local audio device. RTC will start playing the audio file specified. And RTC will notify the audio volume via the [onAudioPlaybackDeviceTestVolume](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onaudioplaybackdevicetestvolume) periodically. |
|[startEchoTest](https://docs.byteplus.com/en/docs/12/14196#rtcengine-startechotest) |Audio/video loopback testing is unavailable in the single\-stream version. |
|[stopEchoTest](https://docs.byteplus.com/en/docs/12/14196#rtcengine-stopechotest) |Stopping an audio/video loopback test is unavailable in the single\-stream version. |
|[initAudioPlaybackDeviceForTest](https://docs.byteplus.com/en/docs/12/14196#rtcengine-initaudioplaybackdevicefortest) |Try to initialize the audio playback device for device test. |
|[initAudioCaptureDeviceForTest](https://docs.byteplus.com/en/docs/12/14196#rtcengine-initaudiocapturedevicefortest) |Try to initialize the audio capture device for device test. |
|[enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/14196#rtcengine-enableaudiopropertiesreport) |Enable audio information prompts. |
|[enableVocalInstrumentBalance](https://docs.byteplus.com/en/docs/12/14196#rtcengine-enablevocalinstrumentbalance) |Enables/disables the loudness equalization function. |
|[setDummyCaptureImagePath](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setdummycaptureimagepath) |Set an alternative image when the local internal video capture is not enabled. You can repeatedly call this API to update the image. You can set the path to null or open the camera to stop publishing the image. |
|[startVideoCapture](https://docs.byteplus.com/en/docs/12/14196#rtcengine-startvideocapture) |Enable internal video capture immediately. The default is off. |
|[stopVideoCapture](https://docs.byteplus.com/en/docs/12/14196#rtcengine-stopvideocapture) |Disable internal video capture immediately. The default is off. |
|[enumerateVideoCaptureDevices](https://docs.byteplus.com/en/docs/12/14196#rtcengine-enumeratevideocapturedevices) |Get a list of video capture devices in the current system. |
|[followSystemPlaybackDevice](https://docs.byteplus.com/en/docs/12/14196#rtcengine-followsystemplaybackdevice) |Set the audio playback device to follow the OS setting or not. |
|[followSystemCaptureDevice](https://docs.byteplus.com/en/docs/12/14196#rtcengine-followsystemcapturedevice) |Set the audio capture device to follow the OS setting or not. |
|[setVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setvideocapturedevice) |Set the current video capture device. |
|[getVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/14196#rtcengine-getvideocapturedevice) |Get the video capture device information currently used by the SDK. |
|[setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setvideoencoderconfig) |Sets the expected maximum published video stream configuration. |
|[enableAlphaChannelVideoEncode](https://docs.byteplus.com/en/docs/12/14196#rtcengine-enablealphachannelvideoencode) |Enables encoding of video frames with an alpha channel. |
|[disableAlphaChannelVideoEncode](https://docs.byteplus.com/en/docs/12/14196#rtcengine-disablealphachannelvideoencode) |Disables encoding of video frames with an alpha channel. |
|[setLocalVideoMirrorType](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setlocalvideomirrortype) |Sets the mirror mode for the captured video stream. |
|[setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setlocalsimulcastmode) |Sets the local simulcast mode and optional substream configurations. |
|[initCVResource](https://docs.byteplus.com/en/docs/12/14196#rtcengine-initcvresource) |Video effects license check. |
|[getAuthMessage](https://docs.byteplus.com/en/docs/12/14196#rtcengine-getauthmessage) |Get authorization messages from the Effect SDK to obtain online licenses. |
|[enableVideoEffect](https://docs.byteplus.com/en/docs/12/14196#rtcengine-enablevideoeffect) |Enables video effects including beauty and color filters. |
|[disableVideoEffect](https://docs.byteplus.com/en/docs/12/14196#rtcengine-disablevideoeffect) |Disables video effects. |
|[enableEffectBeauty](https://docs.byteplus.com/en/docs/12/14196#rtcengine-enableeffectbeauty) |Enables/Disables basic beauty effects. |
|[setBeautyIntensity](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setbeautyintensity) |Sets the beauty effect intensity. |
|[setEffectNodes](https://docs.byteplus.com/en/docs/12/14196#rtcengine-seteffectnodes) |Set video effects material package. |
|[updateEffectNode](https://docs.byteplus.com/en/docs/12/14196#rtcengine-updateeffectnode) |Set the effect intensity. |
|[setColorFilter](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setcolorfilter) |Set the color filter. |
|[setColorFilterIntensity](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setcolorfilterintensity) |Set the intensity of the color filter enabled. |
|[setVideoSourceType](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setvideosourcetype) |Sets the input video source for the SDK, including screen streams. Internal capture is used by default. |
|[pushExternalVideoFrame](https://docs.byteplus.com/en/docs/12/14196#rtcengine-pushexternalvideoframe) |Pushes an external video frame. |
|[setAudioSourceType](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setaudiosourcetype) |Switches the audio capture source type. |
|[pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/14196#rtcengine-pushexternalaudioframe) |Pushes custom audio data to the RTC SDK. |
|[startPushSingleStream](https://docs.byteplus.com/en/docs/12/14196#rtcengine-startpushsinglestream) |Start forwarding a single media stream to a specified RTC room or CDN address. |
|[stopPushSingleStream](https://docs.byteplus.com/en/docs/12/14196#rtcengine-stoppushsinglestream) |Stop a single\-stream forwarding task. |
|[setAnsMode](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setansmode) |Set the Active Noise Cancellation(ANC) mode during audio and video communications. |
|[takeLocalSnapshot](https://docs.byteplus.com/en/docs/12/14196#rtcengine-takelocalsnapshot) |Take a snapshot of the local video. |
|[takeLocalSnapshotToFile](https://docs.byteplus.com/en/docs/12/14196#rtcengine-takelocalsnapshottofile) |Take a snapshot of the local video stream and save it as a JPG file at the specified local path.<br><br>After calling this method, the SDK triggers [onLocalSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onlocalsnapshottakentofile) to report whether the snapshot is taken successfully and provide details of the snapshot image. |
|[takeRemoteSnapshot](https://docs.byteplus.com/en/docs/12/14196#rtcengine-takeremotesnapshot) |Take a snapshot of the remote video. |
|[takeRemoteSnapshotToFile](https://docs.byteplus.com/en/docs/12/14196#rtcengine-takeremotesnapshottofile) |Take a snapshot of the local/remote video stream and save it as a JPG file at the specified local path.<br><br>After calling this method, the SDK triggers [onRemoteSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onremotesnapshottakentofile) to report whether the snapshot is taken successfully and provide details of the snapshot image. |
|[getNetworkTimeInfo](https://docs.byteplus.com/en/docs/12/14196#rtcengine-getnetworktimeinfo) |Obtain the synchronization network time information. |
|[sendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/14196#rtcengine-sendstreamsyncinfo) |Send audio stream synchronization information. The message is sent to the remote end through the audio stream and synchronized with the audio stream. |
|[startCloudProxy](https://docs.byteplus.com/en/docs/12/14196#rtcengine-startcloudproxy) |Start cloud proxy. |
|[stopCloudProxy](https://docs.byteplus.com/en/docs/12/14196#rtcengine-stopcloudproxy) |Stop cloud proxy. |
|[startScreenAudioCapture](https://docs.byteplus.com/en/docs/12/14196#rtcengine-startscreenaudiocapture) |When sharing the screen, start using RTC SDK internal collection method to collect screen audio. |
|[startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/14196#rtcengine-startscreenvideocapture) |Capture screen video stream for sharing. Screen video stream includes: content displayed on the screen, in the application window, or in the virtual screen. |
|[stopScreenAudioCapture](https://docs.byteplus.com/en/docs/12/14196#rtcengine-stopscreenaudiocapture) |Stop recording device audio. |
|[muteScreenAudioCapture](https://docs.byteplus.com/en/docs/12/14196#rtcengine-mutescreenaudiocapture) |Mute/Unmute the screen audio. |
|[stopScreenVideoCapture](https://docs.byteplus.com/en/docs/12/14196#rtcengine-stopscreenvideocapture) |Stop screen video streaming. |
|[updateScreenCaptureRegion](https://docs.byteplus.com/en/docs/12/14196#rtcengine-updatescreencaptureregion) |Update the capture area when capturing screen video streams through the capture module provided by the RTC SDK. |
|[updateScreenCaptureHighlightConfig](https://docs.byteplus.com/en/docs/12/14196#rtcengine-updatescreencapturehighlightconfig) |Update border highlighting settings when capturing screen video streams through the capture module provided by the RTC SDK. By default, a highlighted border is displayed. |
|[updateScreenCaptureMouseCursor](https://docs.byteplus.com/en/docs/12/14196#rtcengine-updatescreencapturemousecursor) |Update the processing settings for the mouse when capturing screen video streams through the capture module provided by the RTC SDK. The mouse cursor is captured by default. |
|[updateScreenCaptureFilterConfig](https://docs.byteplus.com/en/docs/12/14196#rtcengine-updatescreencapturefilterconfig) |When capturing screen video streams through the capture module provided by the RTC SDK, set the window that needs to be filtered. |
|[setScreenAudioChannel](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setscreenaudiochannel) |Set the audio channel of the screen\-sharing audio stream. |
|[getScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/14196#rtcengine-getscreencapturesourcelist) |Get the item list for screen sharing. |
|[getThumbnail](https://docs.byteplus.com/en/docs/12/14196#rtcengine-getthumbnail) |Get the preview thumbnail of the screen\-sharing object. |
|[getWindowAppIcon](https://docs.byteplus.com/en/docs/12/14196#rtcengine-getwindowappicon) |Get application window preview thumbnail for screen sharing. |
|[login](https://docs.byteplus.com/en/docs/12/14196#rtcengine-login) |Log in to send P2P messages or send messages to a server without joining the RTC room. |
|[logout](https://docs.byteplus.com/en/docs/12/14196#rtcengine-logout) |Calls this interface to log out, it is impossible to call methods related to out\-of\-room messages and end\-to\-server messages or receive related callbacks. |
|[updateLoginToken](https://docs.byteplus.com/en/docs/12/14196#rtcengine-updatelogintoken) |Update the Token. |
|[setServerParams](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setserverparams) |Set application server parameters. |
|[getPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/14196#rtcengine-getpeeronlinestatus) |Query the login status of the remote or local user. |
|[sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/14196#rtcengine-sendusermessageoutsideroom) |Send a text message (P2P) to a specified user outside the room. |
|[sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/14196#rtcengine-senduserbinarymessageoutsideroom) |Send binary messages (P2P) to a specified user outside the room. |
|[sendServerMessage](https://docs.byteplus.com/en/docs/12/14196#rtcengine-sendservermessage) |The client side sends a text message to the application server (P2Server). |
|[sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/14196#rtcengine-sendserverbinarymessage) |Client side sends binary messages to the application server (P2Server). |
|[sendSEIMessage](https://docs.byteplus.com/en/docs/12/14196#rtcengine-sendseimessage) |Sends SEI data. |
|[sendLivePushSEIMessage](https://docs.byteplus.com/en/docs/12/14196#rtcengine-sendlivepushseimessage) |Sends SEI data in key\-value format through video frames. |
|[setVideoCaptureConfig](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setvideocaptureconfig) |Set the video capture parameters for internal capture of the RTC SDK. |
|[setLocalVoicePitch](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setlocalvoicepitch) |Change local voice to a different key, mostly used in Karaoke scenarios. You can adjust the pitch of local voice such as ascending or descending with this method. |
|[startFileRecording](https://docs.byteplus.com/en/docs/12/14196#rtcengine-startfilerecording) |This method records the audio & video data during the call to a local file. |
|[stopFileRecording](https://docs.byteplus.com/en/docs/12/14196#rtcengine-stopfilerecording) |Stop local recording. |
|[setPublishFallbackOption](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setpublishfallbackoption) |Sets the fallback option for published audio & video streams. You can call this API to set whether to automatically lower the resolution you set of the published streams under limited network conditions. |
|[setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setsubscribefallbackoption) |Sets the fallback option for subscribed RTC streams. You can call this API to set whether to lower the resolution of currently subscribed stream under limited network conditions. |
|[setRemoteUserPriority](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setremoteuserpriority) |Set user priority. |
|[startNetworkDetection](https://docs.byteplus.com/en/docs/12/14196#rtcengine-startnetworkdetection) |Pre\-call network detection. |
|[stopNetworkDetection](https://docs.byteplus.com/en/docs/12/14196#rtcengine-stopnetworkdetection) |Stop pre\-call network probe. |
|[enableVirtualBackground](https://docs.byteplus.com/en/docs/12/14196#rtcengine-enablevirtualbackground) |Set the original background to a specified image or a solid color. To disable this effect, set the modelPath parameter to null. |
|[disableVirtualBackground](https://docs.byteplus.com/en/docs/12/14196#rtcengine-disablevirtualbackground) |Turns off the virtual background. |
|[enableFaceDetection](https://docs.byteplus.com/en/docs/12/14196#rtcengine-enablefacedetection) |Starts face detection and registers the observer for the result. |
|[disableFaceDetection](https://docs.byteplus.com/en/docs/12/14196#rtcengine-disablefacedetection) |Stops face detection. |
|[setVideoWatermark](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setvideowatermark) |Adds watermark to the local video stream. |
|[clearVideoWatermark](https://docs.byteplus.com/en/docs/12/14196#rtcengine-clearvideowatermark) |Removes video watermark from the local video stream. |
|[setupLocalVideo](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setuplocalvideo) |Set the view for the local video. |
|[removeLocalVideo](https://docs.byteplus.com/en/docs/12/14196#rtcengine-removelocalvideo) |Unbind the local video stream from its rendering view. |
|[setupRemoteVideo](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setupremotevideo) |Bind the remote video stream to the view. |
|[removeRemoteVideo](https://docs.byteplus.com/en/docs/12/14196#rtcengine-removeremotevideo) |Unbind the remote video from the view. |
|[removeAllRemoteVideo](https://docs.byteplus.com/en/docs/12/14196#rtcengine-removeallremotevideo) |Unbind all remote videos from the views. |
|[requestRemoteVideoKeyFrame](https://docs.byteplus.com/en/docs/12/14196#rtcengine-requestremotevideokeyframe) |Requests a key video frame from a subscribed remote video stream. |
|[setLocalVideoSink](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setlocalvideosink) |Get local video stream. |
|[unsetLocalVideoSink](https://docs.byteplus.com/en/docs/12/14196#rtcengine-unsetlocalvideosink) |Stop get local video stream. |
|[setRemoteVideoSink](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setremotevideosink) |Get remote video stream. |
|[unsetRemoteVideoSink](https://docs.byteplus.com/en/docs/12/14196#rtcengine-unsetremotevideosink) |Stop getting the remote video stream. |
|[setLocalVoiceEqualization](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setlocalvoiceequalization) |Set the equalization effect for the local captured audio. The audio includes both internal captured audio and external captured voice, but not the mixing audio file. |
|[setLocalVoiceReverbParam](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setlocalvoicereverbparam) |Set the equalization effect for the local captured audio. The audio includes both internal captured audio and external captured voice, but not the mixing audio file. |
|[enableLocalVoiceReverb](https://docs.byteplus.com/en/docs/12/14196#rtcengine-enablelocalvoicereverb) |Enable the reverb effect for the local captured voice. |
|[startAudioRecording](https://docs.byteplus.com/en/docs/12/14196#rtcengine-startaudiorecording) |Start recording audio communication, and generate the local file. |
|[stopAudioRecording](https://docs.byteplus.com/en/docs/12/14196#rtcengine-stopaudiorecording) |Stops local audio recording. |
|[enableAGC](https://docs.byteplus.com/en/docs/12/14196#rtcengine-enableagc) |Enable or disable automatic gain control to adjust microphone pickup volume. |
|[setVideoCaptureRotation](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setvideocapturerotation) |Set the rotation of the local video images. Call this API to rotate the videos when the camera is fixed upside down or tilted. |
|[setVideoDigitalZoomConfig](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setvideodigitalzoomconfig) |Set the step size for each digital zooming control to the local videos. |
|[setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setvideodigitalzoomcontrol) |Digital zoom or move the local video image once. This action affects both the video preview locally and the stream published. |
|[startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14196#rtcengine-startvideodigitalzoomcontrol) |Continuous and repeatedly digital zoom control. This action affects both the local video preview and the published stream. |
|[stopVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14196#rtcengine-stopvideodigitalzoomcontrol) |Stop the ongoing digital zoom control instantly. |
|[startPushMixedStream](https://docs.byteplus.com/en/docs/12/14196#rtcengine-startpushmixedstream) |Starts a task that publishes a mixed stream to CDN or publishes a WTN stream. |
|[updatePushMixedStream](https://docs.byteplus.com/en/docs/12/14196#rtcengine-updatepushmixedstream) |Updates parameters of a task started by [startPushMixedStream](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startpushmixedstream). |
|[stopPushMixedStream](https://docs.byteplus.com/en/docs/12/14196#rtcengine-stoppushmixedstream) |Stop pushing a mixed stream to its target. |
|[startHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/14196#rtcengine-starthardwareechodetection) |Start echo detection before joining a room. |
|[stopHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/14196#rtcengine-stophardwareechodetection) |Stop the echo detection before joining a room. |
|[setLocalProxy](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setlocalproxy) |Sets local proxy. |
|[setEarMonitorMode](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setearmonitormode) |Turn on/off the earphone monitor function. |
|[setEarMonitorVolume](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setearmonitorvolume) |Set the volume of the earphone monitor. |
|[getAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/14196#rtcengine-getaudioeffectplayer) |Create an instance for audio effect player. |
|[getMediaPlayer](https://docs.byteplus.com/en/docs/12/14196#rtcengine-getmediaplayer) |Create a media player instance. |
|[getWTNStream](https://docs.byteplus.com/en/docs/12/14196#rtcengine-getwtnstream) |Gets the WTN stream instance. |
|[enableExternalSoundCard](https://docs.byteplus.com/en/docs/12/14196#rtcengine-enableexternalsoundcard) |Enable the audio process mode for external sound card. |
|[enableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/14196#rtcengine-enableaudioframecallback) |Enable audio frames callback and set the format for the specified type of audio frames. |
|[disableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/14196#rtcengine-disableaudioframecallback) |Disables audio data callback. |
|[setAudioAlignmentProperty](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setaudioalignmentproperty) |On the listener side, set all subscribed audio streams precisely timely aligned. |
|[enablePlaybackDucking](https://docs.byteplus.com/en/docs/12/14196#rtcengine-enableplaybackducking) |Enables/disables the playback ducking function. This function is usually used in scenarios where short videos or music will be played simultaneously during RTC calls. |
|[startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/14196#rtcengine-startaudiodevicerecordtest) |Start the capture and playback test for local audio devices. |
|[stopAudioDeviceRecordAndPlayTest](https://docs.byteplus.com/en/docs/12/14196#rtcengine-stopaudiodevicerecordandplaytest) |Call this API to stop recording in the test and start to play the recording in 30 s after calling [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudiodevicerecordtest). |
|[stopAudioDevicePlayTest](https://docs.byteplus.com/en/docs/12/14196#rtcengine-stopaudiodeviceplaytest) |Stop the capture and playback test for local audio devices which is started by calling [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudiodevicerecordtest).<br><br>Before the test ends by itself, you can call this API to stop the recording or playing. |
|[sendPublicStreamSEIMessage](https://docs.byteplus.com/en/docs/12/14196#rtcengine-sendpublicstreamseimessage) | |
|[setLowLightAdjusted](https://docs.byteplus.com/en/docs/12/14196#rtcengine-setlowlightadjusted) |Sets the low\-light video enhancement mode. Enable this feature in low\-light, unevenly lit, or backlit environments to improve video quality. |
|[notifyRemoteStreamUnpublished](https://docs.byteplus.com/en/docs/12/14196#rtcengine-notifyremotestreamunpublished) | |
|`static` [getSDKVersion](https://docs.byteplus.com/en/docs/12/14196#static-rtcengine-getsdkversion) |Get the current SDK version information. |
|`static` [setLogConfig](https://docs.byteplus.com/en/docs/12/14196#static-rtcengine-setlogconfig) |Configure the logs. |
|`static` [getCurrentProcessId](https://docs.byteplus.com/en/docs/12/14196#static-rtcengine-getcurrentprocessid) |Get process ID of the engine for commissioning. |
|`static` [setRenderType](https://docs.byteplus.com/en/docs/12/14196#static-rtcengine-setrendertype) |set render type. |
|`static` [getTimestampMs](https://docs.byteplus.com/en/docs/12/14196#static-rtcengine-gettimestampms) |Gets the timestamp in milliseconds. |
|`static` [getTimestampUs](https://docs.byteplus.com/en/docs/12/14196#static-rtcengine-gettimestampus) |Gets the timestamp in microseconds. |

### createRTCEngine

Create an engine instance.

* **Signature**

   ```ts
   (engine_config: EngineConfig) => number
   ```

* **Notes**

   * This is the very first API that you must call if you want to use all the RTC capabilities.

   * If there is no engine instance in current thread, calling this API will create one. If an engine instance has been created, calling this API again will have the created engine instance returned.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |engine_config |[EngineConfig](https://docs.byteplus.com/en/docs/12/docs-85535#engineconfig) |Engine configurations. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1`: Failure.

### createRTCRoom

Create a room for the call.

* **Signature**

   ```ts
   (room_id: string) => veRTCRoom
   ```

* **Notes**

   * Each call of this API creates one `veRTCRoom` instance. Call this API as many times as the number of rooms you need. And then call [joinRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-joinroom) of each `IRTCRoom` instance to join multiple rooms at the same time. These enable Multi\-room mode. In Multi\-room mode, a user can subscribe to media streams in the joined rooms at the same time.

   * To forward streams to the other rooms, call [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-startforwardstreamtorooms) instead of enabling Multi\-room mode.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |room_id |string |roomId is an non\-empty string within 128 bytes. Each room created by calling this API requires a unique roomid. So that the room can be distinguished from each other.<br><br>The following character sets are supported:<br><br><br>* 26 uppercase letters A~ Z<br><br>* 26 lowercase letters a~ z<br><br>* 10 numbers: 0~ 9<br><br>* Underscore "_", at sign "@" , and minus sign "\-"<br><br><br>Do not create multiple rooms with the same roomId, otherwise the newly created room instance will replace the old one. |

* **Return Value**

   Type: veRTCRoom

   The created `veRTCRoom` instance. If the room cannot be created, check whether a room with the same ID already exists or whether `room_id` is invalid.

### destroyRTCEngine

Destroy the engine instance created by [createRTCEngine](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-creatertcengine), and release all related resources.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * Call this API after all business scenarios related to the engine instance are destroyed. In a multi\-thread scenario, you must not call `RTCVideo` related APIs after calling this interface, or the SDK may crash. When the API is called, RTC SDK destroys all memory associated with the engine instance and stops any interaction with the media server.

   * Calling this API will start the SDK exit logic. The engine thread is held until the exit logic is complete. The engine thread is retained until the exit logic is complete. Therefore, do not call this API directly in the callback thread, or wait for the execution of the main thread in the callback and call this API in the main thread at the same time. Otherwise, it will cause a deadlock.

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1`: Failure.

### feedback

Report the user feedback to RTC.

* **Signature**

   ```ts
   (
     type: ProblemFeedbackOption,
     info: ProblemFeedbackInfo
   ) => number
   ```

* **Notes**

   * If the user is in the room when reporting, the report leads to the room / rooms where the user is currently located;

   * If the user is not in the room when reporting, the report leads to the previously exited Room.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |type |[ProblemFeedbackOption](https://docs.byteplus.com/en/docs/12/docs-85535#problemfeedbackoption) |List of preset problems. |
   |info |[ProblemFeedbackInfo](https://docs.byteplus.com/en/docs/12/docs-85535#problemfeedbackinfo) |Specific description of other problems other than the preset problem. |

* **Return Value**

   Type: number

   * 0: Report successfully.

   * \-1: Failed to report, not yet joined the room.

   * \-2: Failed to report, data analysis error.

   * \-3: Failed to report, missing fields.

### setBusinessId

Sets the business ID.

* **Signature**

   ```ts
   (business_id: string) => number
   ```

* **Notes**

   * You can use businessId to distinguish different business scenarios. You can customize your businessId to serve as a sub AppId, which can share and refine the function of the AppId, but it does not need authentication.

   * You must call this API before the [joinRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-joinroom) API, otherwise it will be invalid.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |business_id |string |Your customized businessId<br><br>BusinessId is a tag, and you can customize its granularity. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

   * \-2: Invalid value.

### setEncryptInfo

Set the way to use built\-in encryption when transmitting.

* **Signature**

   ```ts
   (
     encrypt_type: number,
     key: string
   ) => number
   ```

* **Notes**

   * Use this method when using the built\-in encryption on transfer; if you need to use custom encryption on transfer. Built\-in encryption and custom encryption are mutually exclusive, and the transmission is determined to be encrypted according to the last method called.

   * This method must be called before entering the room, and can be called repeatedly, taking the last called parameter as the effective parameter.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |encrypt_type |number |Built\-in encryption algorithm. |
   |key |string |Encryption key, the length is limited to 36 bits, and the excess will be Truncate. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### initializePluginManager

Initialize the plugin manager.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   This method must be called after creating the engine and before entering the room.

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1`: Failure.

### releasePluginManager

Release plugin manager.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   This method must be called after the plugin manager is initialized and before the engine is destroyed.

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1`: Failure.

### registerPlugin

Registers a plugin library.

* **Signature**

   ```ts
   (info: RTCPluginInfo) => number
   ```

* **Notes**

   * This method must be called after the plugin manager has been initialized.

   * After registration succeeds, call [getPlugin](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getplugin) with `info.id` to obtain the plugin control interface.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |info |[RTCPluginInfo](https://docs.byteplus.com/en/docs/12/docs-85535#rtcplugininfo) |Plugin registration information, including the plugin ID and plugin library path. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1`: Failure.

### getPlugin

Gets the control interface for a registered plugin.

* **Signature**

   ```ts
   (plugin_id: string) => RTCPlugin | undefined
   ```

* **Notes**

   This method must be called after registering the plugin.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |plugin_id |string |Plugin ID used when calling [registerPlugin](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-registerplugin). |

* **Return Value**

   Type: [RTCPlugin](https://docs.byteplus.com/en/docs/12/docs-85535#rtcplugin) | undefined

   The control interface for the registered plugin, or `undefined` if the plugin does not exist.

### unregisterPlugin

Uninstall plugin.

* **Signature**

   ```ts
   (plugin_id: string) => number
   ```

* **Notes**

   This method must be called after registering the plugin.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |plugin_id |string |is the unique identifier for the plugin. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1`: Failure.

### muteAudioCapture

Set whether to mute the recording signal (without changing the local hardware).

* **Signature**

   ```ts
   (
     index: number,
     mute: boolean
   ) => number
   ```

* **Notes**

   * Calling this API does not affect the status of SDK audio stream publishing.

   * Adjusting the volume by calling [setCaptureVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setcapturevolume) after muting will not cancel the mute state. The volume state will be retained until unmuted.

   * You can use this interface to set the capture volume before or after calling [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudiocapture) to enable audio capture.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |index |number |Reserved for backward compatibility and ignored. This API always controls microphone audio. To mute screen\-sharing audio, call [muteScreenAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-mutescreenaudiocapture). |
   |mute |boolean |Whether to mute audio capture.<br><br><br>* True: Mute (disable microphone)<br><br>* False: (Default) Enable microphone. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0 : Failure.

### startAudioCapture

Start internal audio capture. The default is off.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * The local client will be informed via onAudioDeviceStateChanged after starting audio capture by calling this API.

   * To enable a microphone without the user's permission will trigger onWarning.

   * Call stopAudioCapture to stop the internal audio capture. Otherwise, the internal audio capture will sustain until you destroy the engine instance.

   * To mute and unmute microphones, we recommend using [publishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-publishstreamaudio), other than stopAudioCapture and this API. Because starting and stopping capture devices often need some time waiting for the response of the device, that may lead to a short silence during the communication.

   * Once you create the engine instance, you can start internal audio capture regardless of the audio publishing state. The audio stream will start publishing only after the audio capture starts.

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### stopAudioCapture

Stop internal audio capture. The default is off.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * The local client will be informed via onAudioDeviceStateChanged after stopping audio capture by calling this API.

   * The remote clients in the room will be informed of the state change via onUserStopAudioCapture after the visible client stops audio capture by calling this API.

   * Call startAudioCapture to enable the internal audio capture.

   * Without calling this API the internal audio capture will sustain until you destroy the engine instance.

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### enumerateAudioPlaybackDevices

Get a list of the audio playback device. When the audio playback device changes, you will receive the [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onaudiodevicestatechanged), and you need to call this API again to get the new device list.

* **Signature**

   ```ts
   () => { device_name: string; device_id: string;}[]
   ```

* **Return Value**

   Type: { device_name: string; device_id: string; }[]

   A list of all audio playback devices.

### enumerateAudioCaptureDevices

Get a list of audio acquisition devices in the current system. If there are subsequent device changes, you need to call this interface again to get a new device list.

* **Signature**

   ```ts
   () => { device_name: string; device_id: string;}[]
   ```

* **Return Value**

   Type: { device_name: string; device_id: string; }[]

   An object that contains a list of all audio capture devices in the system.

### setAudioPlaybackDevice

Sets the audio playback device.

* **Signature**

   ```ts
   (device_id: string) => number
   ```

* **Notes**

   After you call followSystemPlaybackDevice to set the audio playback device to follow the system setting, you cannot call this API to set the audio playback device.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |device_id |string |Audio playback device's ID. You can get the ID by calling enumerateAudioPlaybackDevices. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setAudioCaptureDevice

Set up audio capture devices.

* **Signature**

   ```ts
   (device_id: string) => number
   ```

* **Notes**

   After you call followSystemCaptureDevice to set the audio playback device to follow the system setting, you cannot call this API to set the audio capture device.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |device_id |string |Audio capture device ID, available through enumerateAudioCaptureDevices. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### getAudioPlaybackDevice

Gets the current audio playback device ID.

* **Signature**

   ```ts
   () => string
   ```

* **Return Value**

   Type: string

   Audio playback device ID.

### getAudioCaptureDevice

Gets the current audio capture device ID.

* **Signature**

   ```ts
   () => string
   ```

* **Return Value**

   Type: string

   Audio capture device ID.

### setAudioPlaybackDeviceVolume

Set the current audio playback device volume.

* **Signature**

   ```ts
   (volume: number) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |volume |number |Audio playback device volume, the value range is [0,255], the setting beyond this range is invalid.<br><br><br>* [0,25] Is nearly silent;<br><br>* [26,75] Is low volume;<br><br>* [76,204] Is medium volume;<br><br>* [205,255] Is high volume. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### getAudioPlaybackDeviceVolume

Get the current audio playback device volume.

* **Signature**

   ```ts
   () => number
   ```

* **Return Value**

   Type: number

   Audio playback device volume, the range should be within [0,255].

   * [0,25] Is nearly silent;

   * [26,75] Is low volume;

   * [76,204] Is medium volume;

   * [205,255] Is high volume.

### setAudioCaptureDeviceVolume

Set the current audio capture volume.

* **Signature**

   ```ts
   (volume: number) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |volume |number |Audio capture volume, the value range is [0,255], the setting beyond this range is invalid.<br><br><br>* [0,25] Is nearly silent;<br><br>* [26,75] Is low volume;<br><br>* [76,204] Is medium volume;<br><br>* [205,255] Is high volume. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### getAudioCaptureDeviceVolume

Get the current audio capture volume.

* **Signature**

   ```ts
   () => number
   ```

* **Return Value**

   Type: number

   Audio capture volume, the range is within [0,255].

   * [0,25] Is nearly silent;

   * [26,75] Is low volume;

   * [76,204] Is medium volume;

   * [205,255] Is high volume.

### setAudioPlaybackDeviceMute

Mute or Unmute the current audio playback device. The default state is speaking.

* **Signature**

   ```ts
   (mute: boolean) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |mute |boolean |* true: mute<br><br>* false: non\-mute. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### getAudioPlaybackDeviceMute

Get state of the audio playback device.

* **Signature**

   ```ts
   () => boolean
   ```

* **Return Value**

   Type: boolean

   * true: Mute.

   * false: Speaking.

### setAudioCaptureDeviceMute

Mute or Unmute the current audio capture device. The default state is speaking.

* **Signature**

   ```ts
   (mute: boolean) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |mute |boolean |* true: Mute<br><br>* false: Speaking. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### getAudioCaptureDeviceMute

Get state of the audio capture device.

* **Signature**

   ```ts
   () => boolean
   ```

* **Return Value**

   Type: boolean

   * true: Mute.

   * false: Speaking.

### setCaptureVolume

Adjust the audio capture volume.

* **Signature**

   ```ts
   (volume: number) => number
   ```

* **Notes**

   Call this API to set the volume of the audio capture before or during the audio capture.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |volume |number |Ratio of capture volume to original volume.<br><br>This changes the volume property of the audio data other than the hardware volume.<br><br>Ranging: [0,400]. Unit: %<br><br><br>* 0: Mute<br><br>* 100: Original volume. To ensure the audio quality, we recommend [0, 100].<br><br>* 400: Four times the original volume with signal\-clipping protection. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setScreenCaptureVolume

Adjust the volume of the audio captured during screen sharing.

This only changes the volume property of the audio data, without affecting the microphone capture volume or the local device volume.

* **Signature**

   ```ts
   (volume: number) => number
   ```

* **Notes**

   You can call this API before or after screen audio capture starts.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |volume |number |Ratio(%) of capture volume to the original volume, in the range [0, 400], with overflow protection.<br><br>To ensure the audio quality, we recommend setting the volume within [0, 100].<br><br><br>* 0: mute<br><br>* 100: original volume<br><br>* 400: Four times the original volume with signal\-clipping protection. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setPlaybackVolume

Adjust the playback volume of the mixed remote audios. You can call this API before or during the playback.

* **Signature**

   ```ts
   (volume: number) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |volume |number |Ratio(%) of playback volume to original volume, in the range [0, 400], with overflow protection.<br><br>This changes the volume property of the audio data other than the hardware volume.<br><br>To ensure the audio quality, we recommend setting the volume within `100`.<br><br><br>* 0: mute<br><br>* 100: original volume<br><br>* 400: Four times the original volume with signal\-clipping protection. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setRemoteAudioPlaybackVolume

Adjust the audio playback volume of the remote user.

* **Signature**

   ```ts
   (
     stream_id: string,
     volume: number
   ) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Remote stream ID. |
   |volume |number |Ratio(%) of playback volume to original volume, in the range [0, 400], with overflow protection.<br><br>This changes the volume property of the audio data other than the hardware volume.<br><br>To ensure the audio quality, we recommend setting the volume within `100`.<br><br><br>* 0: mute<br><br>* 100: original volume. Default value.<br><br>* 400: Up to 4 times the original volume (with overflow protection). |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### stopAudioPlaybackDeviceTest

Stop the playback test for the local audio device.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   Call this API to stop the playback test started by calling [startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudioplaybackdevicetest) before moving on to the other device tests.

* **Return Value**

   Type: number

   * `0`: Success.

   * `< 0`: Failure.

### setVoiceChangerType

Set the sound effect type.

* **Signature**

   ```ts
   (change_type: VoiceChangerType) => number
   ```

* **Notes**

   * You can call it before and after entering the room.

   * Effective for both internal and external audio source.

   * Only valid for mono\-channel audio.

   * Only valid in SDKs that include the ability of sound effects.

   * Mutually exclusive with setVoiceReverbType, and the effects set later will override the effects set first.

   * To use this feature, contact us for technical support.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |change_type |[VoiceChangerType](https://docs.byteplus.com/en/docs/12/docs-85535#voicechangertype) |Sound effect type. See VoiceChangerType.<br><br><br>* `0`:    Unchanged<br><br>* `1`:    Giant<br><br>* `2`:    Chipmunk<br><br>* `3`:    Minions<br><br>* `4`:    Vibrato<br><br>* `5`:    Robot. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setVoiceReverbType

Set the reverb effect type.

* **Signature**

   ```ts
   (voice_reverb_type: VoiceReverbType) => number
   ```

* **Notes**

   * You can call it before and after entering the room.

   * Effective for both internal and external audio source.

   * Only valid for mono\-channel audio.

   * Only valid in SDKs that include the ability of sound effects.

   * Mutually exclusive with setVoiceChangerType, and the effects set later will override the effects set first.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |voice_reverb_type |[VoiceReverbType](https://docs.byteplus.com/en/docs/12/docs-85535#voicereverbtype) |Reverb effect type. See VoiceReverbType.<br><br><br>* `0`:    Unchanged<br><br>* `1`:    Echo<br><br>* `2`:    Music concert<br><br>* `3`:    Ethereal<br><br>* `4`:    Karaoke<br><br>* `5`:    Recording studio<br><br>* `6`:    Virtual stereo<br><br>* `7`:    Spacious<br><br>* `8`:    3D voice. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setAudioProfile

Sets the sound quality.

* **Signature**

   ```ts
   (audio_profile: number) => number
   ```

* **Notes**

   * Call this API to change the sound quality if the audio settings in the current RoomProfileType can not meet your requirements.

   * You can call this API before and after entering the room.

   * Support dynamic switching of sound quality during a call.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |audio_profile |number |Sound quality<br><br><br>* `0`:    Default sound quality. The sound quality configuration of RoomProfileType set by the server or client.<br><br>* `1`: Fluent. Sample rate: 16 KHz. Mono\-channel. Encoding bitrate: 32 Kpbs. Low resource consumption, and small network packets guarantees a smooth call. It is suitable for most game scenarios, such as team\-wide voice chat, group\-wide voice chat, nation\-wide voice chat.<br><br>* `2`: Mono\-channel standard. Sample rate: 24 KHz. Encoding bitrate: 48 Kpbs. For scenarios requiring distinct voice, you can choose this mode, which achieves balanced latency, consumption, and network packets. It is suitable for educational Apps and the online Mafia Games.<br><br>* `3`:    Dual\-channel music. Sample rate: 48 KHz. Encoding bitrate: 128 Kpbs. This mode provides high\-resolution audio at a cost of high latency, consumption, and large network packets. It is suitable for music Apps such as co\-hosting and online talent contests. Not recommended for game Apps.<br><br>* `4`:    Dual\-channel standard. Sample rate: 48 KHz. Encoding bitrate: 80 Kpbs<br><br>* `5`:    Mono\-channel music. Sample rate: 48 KHz. Encoding bitrate: 64 Kpbs. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `!0`: Failure.

### startAudioPlaybackDeviceTest

Start the playback test for the local audio device. RTC will start playing the audio file specified. And RTC will notify the audio volume via the [onAudioPlaybackDeviceTestVolume](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onaudioplaybackdevicetestvolume) periodically.

* **Signature**

   ```ts
   (
     test_audio_file_path: string,
     indication_interval: number
   ) => number
   ```

* **Notes**

   * You can call this API whether the user is in the room.

   * Call [stopAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopaudioplaybackdevicetest) to stop the playback test before moving on to the other device tests.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |test_audio_file_path |string |Specify the path of the audio file for the playback test, including \*.mp3, \*.aac, \*.m4a, \*.3gp, and \*.wav. |
   |indication_interval |number |The time interval between each callback in milliseconds. We recommend setting it to 200 ms. The minimal value is 10 ms. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### startEchoTest

Audio/video loopback testing is unavailable in the single\-stream version.

* **Signature**

   ```ts
   (
     echo_test_config: EchoTestConfig,
     play_delay_time: number
   ) => number
   ```

* **Notes**

   This API always returns `-1` and does not start a loopback test.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |echo_test_config |[EchoTestConfig](https://docs.byteplus.com/en/docs/12/docs-85535#echotestconfig) |Test configurations. |
   |play_delay_time |number |Delayed audio/video playback time specifying how long you expect to receive the playback after starting the. The range of the value is [2,10] in seconds and the default value is 2. |

* **Return Value**

   Type: number

   `-1`. This API is unavailable in the single\-stream version.

### stopEchoTest

Stopping an audio/video loopback test is unavailable in the single\-stream version.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   This API always returns `-1`.

* **Return Value**

   Type: number

   `-1`. This API is unavailable in the single\-stream version.

### initAudioPlaybackDeviceForTest

Try to initialize the audio playback device for device test.

* **Signature**

   ```ts
   (device_id: string) => number
   ```

* **Notes**

   * Call this API before the user joins the room.

   * You may still fail to enable the device even you passed the test. Occupation by other application or shortage of CPU / memory may cause the failure.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |device_id |string |Device ID. |

* **Return Value**

   Type: number

   * 0: Status normal.

   * \-1: Test not executed.

   * \-2: Init failed due to lack of permission.

   * \-3: The device does not exist. No device or device removed.

   * \-4: The audio format is not supported.

   * \-5: Error for other reasons.

### initAudioCaptureDeviceForTest

Try to initialize the audio capture device for device test.

* **Signature**

   ```ts
   (device_id: string) => number
   ```

* **Notes**

   * Call this API before the user joins the room.

   * You may still fail to enable the device even you passed the test. Occupation by other application or shortage of CPU / memory may cause the failure.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |device_id |string |Device ID. |

* **Return Value**

   Type: number

   * 0: Status normal.

   * \-1: Test not executed.

   * \-2: Init failed due to lack of permission.

   * \-3: The device does not exist. No device or device removed.

   * \-4: The audio format is not supported.

   * \-5: Error for other reasons.

### enableAudioPropertiesReport

Enable audio information prompts.

* **Signature**

   ```ts
   (config: AudioPropertiesConfig) => number
   ```

* **Notes**

   After enable the prompt, you can:

   * Get the information of the audio stream collected by the local microphone and screen audio stream through [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onlocalaudiopropertiesreport).

   * Get the information of the subscribed remote audio streams through [onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onremoteaudiopropertiesreport).

   * Get the information of the active speaker through [onActiveSpeaker](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onactivespeaker).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |config |[AudioPropertiesConfig](https://docs.byteplus.com/en/docs/12/docs-85535#audiopropertiesconfig) |Configuration for audio property prompt. |

* **Return Value**

   Type: number

### enableVocalInstrumentBalance

Enables/disables the loudness equalization function.

* **Signature**

   ```ts
   (enable: boolean) => number
   ```

* **Notes**

   * If you call this API with the parameter set to true, the loudness of user's voice will be adjusted to \-16 lufs.

   * Call this API before playing the reference audio file.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |enable |boolean |Whether to enable loudness equalization function:<br><br><br>* true: Yes<br><br>* false: No. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setDummyCaptureImagePath

Set an alternative image when the local internal video capture is not enabled. You can repeatedly call this API to update the image. You can set the path to null or open the camera to stop publishing the image.

* **Signature**

   ```ts
   (file_path: string) => number
   ```

* **Notes**

   * The API is only effective when publishing an internally captured video.

   * You cannot locally preview the image.

   * You can call this API before and after joining an RTC room. In the multi\-room mode, the image can be only displayed in the room you publish the stream.

   * You cannot apply effects like filters and mirroring to the image, while you can watermark the image.

   * The image is not effective for a screen\-sharing stream.

   * When you enable the simulcast mode, the image will be added to all video streams, and it will be proportionally scaled down to smaller encoding configurations.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |file_path |string |Set the path of the static image.<br><br>You can use the absolute path (file://xxx). The maximum size for the path is 512 bytes.<br><br>You can upload a .JPG, .JPEG, .PNG, or .BMP file.<br><br>When the aspect ratio of the image is inconsistent with the video encoder configuration, the image will be proportionally resized, with the remaining pixels rendered black. The framerate and the bitrate are consistent with the video encoder configuration. |

* **Return Value**

   Type: number

   * 0: Success.

   * \-1: Failure.

### startVideoCapture

Enable internal video capture immediately. The default is off.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * Internal video capture refers to: use the RTC SDK built\-in video capture module to capture.

   * The local client will be informed via [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onvideodevicestatechanged) after starting video capture by calling this API.

   * The remote clients in the room will be informed of the state change via [onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onuserstartvideocapture) after the visible client starts video capture by calling this API.

   * Call stopVideoCapture to stop the internal video capture. Otherwise, the internal video capture will sustain until you destroy the engine instance.

   * Once you create the engine instance, you can start internal video capture regardless of the video publishing state. The video stream will start publishing only after the video capture starts.

   * To switch from custom to internal video capture, stop publishing before disabling the custom video capture module and then call this API to enable the internal video capture.

* **Return Value**

   Type: number

   * `0`: Success.

   * `!0`: Failure.

### stopVideoCapture

Disable internal video capture immediately. The default is off.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * Internal video capture refers to: use the RTC SDK built\-in video capture module to capture.

   * The local client will be informed via onVideoDeviceStateChanged after stopping video capture by calling this API.

   * The remote clients in the room will be informed of the state change via onUserStopVideoCapture after the visible client stops video capture by calling this API.

   * Call startVideoCapture to enable the internal video capture.

   * Without calling this API the internal video capture will sustain until you destroy the engine instance.

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### enumerateVideoCaptureDevices

Get a list of video capture devices in the current system.

* **Signature**

   ```ts
   () => { device_name: string; device_id: string;}[]
   ```

* **Return Value**

   Type: { device_name: string; device_id: string; }[]

   Contains a list of all video capture devices in the system.

### followSystemPlaybackDevice

Set the audio playback device to follow the OS setting or not.

* **Signature**

   ```ts
   (followed: boolean) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |followed |boolean |Whether the audio playback device follows the OS setting.<br><br><br>* true: follow the OS setting. You can not call [setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setaudioplaybackdevice) at the same time. The default value.<br><br>* false: do not follow the OS setting. You can call [setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setaudioplaybackdevice) to set the audio playback device. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### followSystemCaptureDevice

Set the audio capture device to follow the OS setting or not.

* **Signature**

   ```ts
   (followed: boolean) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |followed |boolean |Whether the audio capture device follows the OS setting.<br><br><br>* true: follow the OS setting. Default value. You can not call [setAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setaudiocapturedevice) at the same time.<br><br>* false: do not follow the OS setting. You can call [setAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setaudiocapturedevice) to set the audio capture device. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setVideoCaptureDevice

Set the current video capture device.

* **Signature**

   ```ts
   (device_id: string) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |device_id |string |Video device ID, which can be obtained through [EnumerateVideoCaptureDevices](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enumeratevideocapturedevices). |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### getVideoCaptureDevice

Get the video capture device information currently used by the SDK.

* **Signature**

   ```ts
   () => string
   ```

* **Return Value**

   Type: string

   Device ID.

### setVideoEncoderConfig

Sets the expected maximum published video stream configuration.

* **Signature**

   ```ts
   (encoder_config: VideoEncoderConfig) => number
   ```

* **Notes**

   * This API only sets one video stream. To publish simulcast streams, call [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setlocalsimulcastmode).

   * This API is applicable to the video stream captured by the camera.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |encoder_config |[VideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-85535#videoencoderconfig) |Video encoder configuration for the main stream. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### enableAlphaChannelVideoEncode

Enables encoding of video frames with an alpha channel.

* **Signature**

   ```ts
   (
     index: StreamIndex,
     layout: AlphaLayout
   ) => any
   ```

* **Notes**

   * This is suitable for scenarios where the sender's foreground and background need to be separated and the receiver renders the background customly.

   * Call this API before publishing the video stream.

   * After enabling this feature, use custom video capture with [pushExternalVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-pushexternalvideoframe) and push RGBA frames using `kVideoPixelFormatRGBA`.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |index |[StreamIndex](https://docs.byteplus.com/en/docs/12/docs-85535#streamindex) |Stream index. Only `0`, which represents the main stream, is currently supported. |
   |layout |[AlphaLayout](https://docs.byteplus.com/en/docs/12/docs-85535#alphalayout) |Layout position of the alpha\-channel data. Only `kAlphaLayoutTop`, which places alpha data above RGB data, is currently supported. |

* **Return Value**

   * `0`: Success.

   * `<0`: Failure.

### disableAlphaChannelVideoEncode

Disables encoding of video frames with an alpha channel.

* **Signature**

   ```ts
   (index: StreamIndex) => any
   ```

* **Notes**

   Call this API after you stop publishing the video stream. Otherwise, the call fails.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |index |[StreamIndex](https://docs.byteplus.com/en/docs/12/docs-85535#streamindex) |Stream index. Only `0`, which represents the main stream, is currently supported. |

* **Return Value**

   * `0`: Success.

   * `<0`: Failure.

### setLocalVideoMirrorType

Sets the mirror mode for the captured video stream.

* **Signature**

   ```ts
   (mirror_type: MirrorType) => number
   ```

* **Notes**

   * You must call [setupLocalVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setuplocalvideo) before this API.

   * Switching video streams does not affect the settings of the mirror type.

   * This API is not applicable to screen\-sharing streams.

   * Before you call this API, the initial states of each video stream are as follows:

   ```Plain Text
   <tr><th></th><th>Front-facing camera</th><th>Back-facing camera</th><th>Custom capturing</th><th>Built-in camera</th></tr>
   <tr><td>Mobile device</td><td>The preview is mirrored. The published video stream is not mirrored.</td><td>The preview and the published video stream are not mirrored.</td><td>The preview and the published video stream are not mirrored.</td><td>/</td></tr>
   <tr><td>PC</td><td>/</td><td>/</td><td>The preview and the published video stream are not mirrored.</td><td>The preview is mirrored. The published video stream is not mirrored.</td></tr>
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |mirror_type |[MirrorType](https://docs.byteplus.com/en/docs/12/docs-85535#mirrortype) |Mirror type. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setLocalSimulcastMode

Sets the local simulcast mode and optional substream configurations.

* **Signature**

   ```ts
   (
     mode: VideoSimulcastMode,
     stream_config?: VideoEncoderConfig[]
   ) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |mode |[VideoSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-85535#videosimulcastmode) |Simulcast mode. |
   |stream_config |[VideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-85535#videoencoderconfig)[] \| undefined |Optional substream configurations sorted from small to large.<br><br>Each substream resolution must be smaller than the main stream set by [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvideoencoderconfig). |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### initCVResource

Video effects license check.

* **Signature**

   ```ts
   (
     license_path: string,
     algo_model_dir: string
   ) => number
   ```

* **Notes**

   Before you start using video effects, you must first call this method for license verification.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |license_path |string |Absolute path of license file from platforms. |
   |algo_model_dir |string |The absolute path of the Effects SDK's models file. |

* **Return Value**

   Type: number

   * `0`: call succeeded.

   * `1000`: not integrated cv sdk.

   * `1001`: cv function is not supported in this RTC version.

   * `< 0`: Failure Please refer to [Error Code Table](https://docs.byteplus.com/en/effects/docs/error-code-table).

### getAuthMessage

Get authorization messages from the Effect SDK to obtain online licenses.

* **Signature**

   ```ts
   () => string
   ```

* **Notes**

   * You must obtain an online license for the Effect SDK before using the CV functions.

   * After obtaining authorization messages through this API, you must refer to [Online Authorization Instructions](https://docs.byteplus.com/en/effects/docs/online-license-guide) to implement the business logic of obtaining online licenses by yourself.

   * After obtaining the license, you must call [initCVResource](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-initcvresource) to confirm that the license is valid. Then you can use the CV function.

* **Return Value**

   Type: string

   Authorization message string address.

### enableVideoEffect

Enables video effects including beauty and color filters.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * You must call [initCVResource](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-initcvresource) before calling this API.

   * This API does not turn on video effects directly, you must call [setEffectNodes](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-seteffectnodes) or [setColorFilter](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setcolorfilter) next.

   * Call [disableVideoEffect](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-disablevideoeffect) to turn off video effects.

* **Return Value**

   Type: number

   * 0: Success.

   * –1000: The Effects SDK is not integrated.

   * –1001: This API is unavailable for your Effects SDK.

   * –1002: Your Effects SDK's version is incompatible.

   * < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

### disableVideoEffect

Disables video effects.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   Call [enableVideoEffect](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enablevideoeffect) to enable video effects.

* **Return Value**

   Type: number

   * 0: Success.

   * –1000: The Effects SDK is not integrated.

   * –1001: This API is unavailable for your Effects SDK.

   * –1002: Your Effects SDK's version is incompatible.

   * < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

### enableEffectBeauty

Enables/Disables basic beauty effects.

* **Signature**

   ```ts
   (enabled: boolean) => number
   ```

* **Notes**

   * You cannot use the basic beauty effects and the advanced effect features at the same time. Call [enableVideoEffect](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enablevideoeffect) to use advanced effect features.

   * You need to integrate Effect SDK before calling this API. Effect SDK V4.3.1+ is recommended.

   * Call [setBeautyIntensity](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setbeautyintensity) to set the beauty effect intensity. If you do not set the intensity, the brightness, smoothness, and sharpness intensity will default to 0.5.

   * This API is not applicable to screen capturing.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |enabled |boolean |Whether to enable basic beauty effects.<br><br><br>* true: Enables basic beauty effects.<br><br>* false: (Default) Disables basic beauty effects. |

* **Return Value**

   Type: number

   * 0: Success.

   * 1000: The Effect SDK is not integrated.

   * 1001: This API is not available for your current RTC SDK.

   * 1002: This API is not available for your current Effect SDK. You can upgrade your Effect SDK to V4.3.1+.

   * 1003: Contact our technical support team for further instructions.

   * 1004: Downloading related resources. The beauty effects will take effect after downloading.

   * <0: Failure. Effect SDK internal error. For specific error code, see [error codes](https://docs.byteplus.com/effects/docs/error-code-table).

### setBeautyIntensity

Sets the beauty effect intensity.

* **Signature**

   ```ts
   (
     beauty_mode: EffectBeautyMode,
     intensity: number
   ) => number
   ```

* **Notes**

   * We recommend to call [initCVResource](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-initcvresource) to validate the license before using video effect enhancement.

   * If you call this API before calling [enableEffectBeauty](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableeffectbeauty), the default settings of beauty effect intensity will adjust accordingly.

   * If you destroy the engine, the beauty effect settings will be invalid.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |beauty_mode |[EffectBeautyMode](https://docs.byteplus.com/en/docs/12/docs-85535#effectbeautymode) |Basic beauty effect. |
   |intensity |number |Beauty effect intensity in range of [0,1], default to 0.5. When you set it to 0, the beauty effect will be turned off. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1000`: The Effect SDK is not integrated.

   * `-1001`: This API is not available for your current RTC SDK.

   * `<0`: Failure. Effect SDK internal error. For specific error code, see [error codes](https://docs.byteplus.com/effects/docs/error-code-table).

### setEffectNodes

Set video effects material package.

* **Signature**

   ```ts
   (effect_node_paths: string[] | null) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |effect_node_paths |string[] \| null |Array of effect material package paths. To remove the current video effect, set it to null. |

* **Return Value**

   Type: number

   * 0: Success.

   * 1000: The Effect SDK is not integrated.

   * 1001: This API is not available for your Effect SDK.

   * < 0: Failure. For specific error codes.

### updateEffectNode

Set the effect intensity.

* **Signature**

   ```ts
   (
     effect_node_path: string,
     node_key: string,
     node_value: number
   ) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |effect_node_path |string |Special effects material package path. |
   |node_key |string |The name of the material key to be set. |
   |node_value |number |The intensity value that needs to be set, the value range [0,1], and the setting is invalid when it exceeds the range. |

* **Return Value**

   Type: number

   * 0: Success.

   * –1000: The Effects SDK is not integrated.

   * –1001: This API is unavailable for your Effects SDK.

   * –1002: Your Effects SDK's version is incompatible.

   * < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

### setColorFilter

Set the color filter.

* **Signature**

   ```ts
   (res_path: string) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |res_path |string |Filter effects package absolute path. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

   * 1000: The Effect SDK is not integrated.

   * 1001: This API is not available for your Effect SDK.

   * <0: Other errors.

### setColorFilterIntensity

Set the intensity of the color filter enabled.

* **Signature**

   ```ts
   (intensity: number) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |intensity |number |Filter intensity. The value range [0,1] is set to be invalid when the range is exceeded. |

* **Return Value**

   Type: number

   * 0: Success.

   * 1000: The Effect SDK is not integrated.

   * 1001: This API is not available for your Effect SDK.

   * < 0: Failure.

### setVideoSourceType

Sets the input video source for the SDK, including screen streams. Internal capture is used by default.

* **Signature**

   ```ts
   (type: VideoSourceType) => any
   ```

* **Notes**

   * You can call this API before or after joining a room.

   * If you switch to custom capture after calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startvideocapture), the SDK automatically stops internal capture.

   * To switch back to internal capture after enabling custom capture, first disable custom capture through this API, then call [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startvideocapture) manually.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |type |[VideoSourceType](https://docs.byteplus.com/en/docs/12/docs-85535#videosourcetype) |Input video source type. |

* **Return Value**

   * `0`: Success.

   * `<0`: Failure.

### pushExternalVideoFrame

Pushes an external video frame.

* **Signature**

   ```ts
   (frame: ExternalVideoFrame) => any
   ```

* **Notes**

   * Supported formats: `I420`, `NV12`, `RGBA`, `BGRA`, and `ARGB`.

   * This method runs on the caller thread.

   * Before pushing external video frames, call [setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvideosourcetype) to enable external video source capture.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |frame |[ExternalVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85535#externalvideoframe) |Video frame to push. |

* **Return Value**

   * `0`: Success.

   * `<0`: Failure.

### setAudioSourceType

Switches the audio capture source type.

* **Signature**

   ```ts
   (type: AudioSourceType) => any
   ```

* **Notes**

   * This API can be called before or after joining a room.

   * When switching from internal capture to custom capture, the SDK automatically stops internal capture. Then call [pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-pushexternalaudioframe) to push custom audio data.

   * When switching from custom capture back to internal capture, call [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudiocapture) manually.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |type |[AudioSourceType](https://docs.byteplus.com/en/docs/12/docs-85535#audiosourcetype) |Audio source type.<br><br>Internal audio capture is used by default. Audio capture and rendering modes do not need to match. |

* **Return Value**

   * `0`: Success.

   * `<0`: Failure.

### pushExternalAudioFrame

Pushes custom audio data to the RTC SDK.

* **Signature**

   ```ts
   (frame: ExternalAudioFrame) => any
   ```

* **Notes**

   * Before pushing custom audio data, call [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudiocapture) to enable custom capture.

   * You must push data every 10 ms.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |frame |[ExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85535#externalaudioframe) |Audio data for 10 ms. |

* **Return Value**

   * `0`: Success.

   * `<0`: Failure.

### startPushSingleStream

Start forwarding a single media stream to a specified RTC room or CDN address.

* **Signature**

   ```ts
   (
     task_id: string,
     param: PushSingleStreamParam
   ) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |task_id |string |Task ID.<br><br>You may want to start more than one single\-stream forwarding task. When you do that, use different IDs for corresponding tasks; if you will start only one task, use an empty string. |
   |param |[PushSingleStreamParam](https://docs.byteplus.com/en/docs/12/docs-85535#pushsinglestreamparam) |Single\-stream forwarding configuration. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85535#returnstatus) for more details.

### stopPushSingleStream

Stop a single\-stream forwarding task.

* **Signature**

   ```ts
   (task_id: string) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |task_id |string |Task ID. Specifies the single\-stream forwarding task to stop. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85535#returnstatus) for details.

### setAnsMode

Set the Active Noise Cancellation(ANC) mode during audio and video communications.

* **Signature**

   ```ts
   (ans_mode: AnsMode) => number
   ```

* **Notes**

   When you repeatedly call this API, only the last call takes effect.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |ans_mode |[AnsMode](https://docs.byteplus.com/en/docs/12/docs-85535#ansmode) |ANC modes. |

* **Return Value**

   Type: number

### takeLocalSnapshot

Take a snapshot of the local video.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * The snapshot is taken with all video effects on, like rotation, and mirroring.

   * You can take the snapshot either using SDK internal video capture or customized capture.

* **Return Value**

   Type: number

   The index of the local snapshot task, starting from `1`. You can get the snapshot from [onTakeLocalSnapshotResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-ontakelocalsnapshotresult).

### takeLocalSnapshotToFile

Take a snapshot of the local video stream and save it as a JPG file at the specified local path.

After calling this method, the SDK triggers [onLocalSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onlocalsnapshottakentofile) to report whether the snapshot is taken successfully and provide details of the snapshot image.

* **Signature**

   ```ts
   (file_path: string) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |file_path |string |The absolute file path where the snapshot JPG file will be saved. The file extension must be `.jpg`. Ensure that the directory exists and is writable. Examples: `C:\\Users\\YourName\\Pictures\\snapshot.jpg`. |

* **Return Value**

   Type: number

   The index of the local snapshot task, starting from `1`. The index can be used to track the task status or perform other management operations.

### takeRemoteSnapshot

Take a snapshot of the remote video.

* **Signature**

   ```ts
   (stream_id: string) => number
   ```

* **Notes**

   * The snapshot is taken with all video effects on, like rotation, and mirroring.

   * You can take the snapshot either using SDK internal video capture or customized capture.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Remote stream ID. |

* **Return Value**

   Type: number

   The index of the remote snapshot task, starting from `1`. You can get the snapshot from [onTakeRemoteSnapshotResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-ontakeremotesnapshotresult).

### takeRemoteSnapshotToFile

Take a snapshot of the local/remote video stream and save it as a JPG file at the specified local path.

After calling this method, the SDK triggers [onRemoteSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onremotesnapshottakentofile) to report whether the snapshot is taken successfully and provide details of the snapshot image.

* **Signature**

   ```ts
   (
     stream_id: string,
     file_path: string
   ) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Specifies the remote video stream ID to take a snapshot from. |
   |file_path |string |The absolute file path where the snapshot JPG file will be saved. The file extension must be `.jpg`. Ensure that the directory exists and is writable. Examples: `C:\\Users\\YourName\\Pictures\\snapshot.jpg`. |

* **Return Value**

   Type: number

   The index of the remote snapshot task, starting from `1`. The index can be used to track the task status or perform other management operations.

### getNetworkTimeInfo

Obtain the synchronization network time information.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * When you call this API for the first time, you starts synchornizing the network time information and receive the return value `0`. After the synchonization finishes, you will receive [onNetworkTimeSynchronized](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onnetworktimesynchronized). After that, calling this API will get you the correct network time.

   * Under chorus scenario, participants shall start audio mixing at the same network time.

* **Return Value**

   Type: number

### sendStreamSyncInfo

Send audio stream synchronization information. The message is sent to the remote end through the audio stream and synchronized with the audio stream.

* **Signature**

   ```ts
   (
     data: Uint8Array,
     config: StreamSyncInfoConfig
   ) => number
   ```

* **Notes**

   * Regarding the frequency, we recommend no more than 50 calls per second.

   * The data may be lost when the local user is muted.

   * After the interface is successfully called, the remote user will receive a [onStreamSyncInfoReceived](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onstreamsyncinforeceived) callback.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |data |Uint8Array |Message content. |
   |config |[StreamSyncInfoConfig](https://docs.byteplus.com/en/docs/12/docs-85535#streamsyncinfoconfig) |Configuration related to audio stream synchronization information. |

* **Return Value**

   Type: number

   * `>= 0`: Message sent successfully. Returns the number of successful sends.

   * `-1`: Message sending failed. Message length greater than 16 bytes.

   * `-2`: Message sending failed. The content of the incoming message is empty.

   * `-3`: Message sending failed. This screen stream was not published when the message was synchronized through the screen stream.

   * `-4`: Message sending failed. This audio stream is not yet published when you synchronize messages with an audio stream captured by a microphone or custom device, as described in ErrorCode.

### startCloudProxy

Start cloud proxy.

* **Signature**

   ```ts
   (cloud_proxies?: CloudProxyInfo[]) => number
   ```

* **Notes**

   * Call this API before joining the room.

   * Start pre\-call network detection after starting cloud proxy.

   * After starting cloud proxy and connects the cloud proxy server successfully, receives [onCloudProxyConnected](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-oncloudproxyconnected).

   * To stop cloud proxy, call [stopCloudProxy](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopcloudproxy).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |cloud_proxies |[CloudProxyInfo](https://docs.byteplus.com/en/docs/12/docs-85535#cloudproxyinfo)[] |cloud proxy informarion list. |

* **Return Value**

   Type: number

### stopCloudProxy

Stop cloud proxy.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   To start cloud proxy, call [startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startcloudproxy).

* **Return Value**

   Type: number

### startScreenAudioCapture

When sharing the screen, start using RTC SDK internal collection method to collect screen audio.

* **Signature**

   ```ts
   (device_id?: string) => number
   ```

* **Notes**

   * After collection, you also need to call [publishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-publishstreamaudio) to push the captured screen audio to the far end.

   * To turn off screen audio internal capture, call [stopScreenAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopscreenaudiocapture).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |device_id |string \| undefined |ID of the virtual device. You need to pass the ID to the API only for Mac. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `!0`: Failure.

### startScreenVideoCapture

Capture screen video stream for sharing. Screen video stream includes: content displayed on the screen, in the application window, or in the virtual screen.

* **Signature**

   ```ts
   (
     source_info: ScreenCaptureSourceInfo,
     capture_params: ScreenCaptureParameters
   ) => number
   ```

* **Notes**

   * Displaying contents in virtual screens is only available on Windows.

   * This API only starts screen capturing but does not publish the captured video. Call [publishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-publishstreamvideo) to publish the captured video.

   * To turn off screen video capture, call stopScreenVideoCapture.

   * Local users will receive [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onvideodevicestatechanged) on the state of screen capturing such as start, pause, resume, and error.

   * After successfully calling this API, local users will receive [onFirstLocalVideoFrameCaptured](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onfirstlocalvideoframecaptured).

   * Before calling this API, you can call [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvideoencoderconfig) to set the frame rate and encoding resolution of the screen video stream.

   * After receiving [onFirstLocalVideoFrameCaptured](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onfirstlocalvideoframecaptured), you can set the local screen sharing view by calling [setupLocalVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setuplocalvideo) or [setLocalVideoSink](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setlocalvideosink).

   * You can call [setLocalVideoSink](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setlocalvideosink) to bind the local video stream to a custom renderer and get captured local video frames from [onLocalVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onlocalvideoframe).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |source_info |[ScreenCaptureSourceInfo](https://docs.byteplus.com/en/docs/12/docs-85535#screencapturesourceinfo) |Screen capture source information. Call [getScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getscreencapturesourcelist) to get all the screen sources that can be shared. |
   |capture_params |[ScreenCaptureParameters](https://docs.byteplus.com/en/docs/12/docs-85535#screencaptureparameters) |Screen capture parameters. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### stopScreenAudioCapture

Stop recording device audio.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   To start the device audio recording, call [startScreenAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startscreenaudiocapture).

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### muteScreenAudioCapture

Mute/Unmute the screen audio.

* **Signature**

   ```ts
   (mute: boolean) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |mute |boolean |Mute or not. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### stopScreenVideoCapture

Stop screen video streaming.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * To turn on screen video stream capture, calling [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startscreenvideocapture).

   * Local users will receive the [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onvideodevicestatechanged) callback.

   * Calling this interface does not affect screen video stream publishing.

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### updateScreenCaptureRegion

Update the capture area when capturing screen video streams through the capture module provided by the RTC SDK.

* **Signature**

   ```ts
   (region_rect?: Rectangle) => number
   ```

* **Notes**

   Before calling this interface, internal screen stream capture must have been turned on by calling [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startscreenvideocapture).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |region_rect |[Rectangle](https://docs.byteplus.com/en/docs/12/docs-85535#rectangle) |Region to be shared. This parameter describes the acquisition area after calling this interface, and the relative relationship between the 'source_info' setting area in [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startscreenvideocapture). |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### updateScreenCaptureHighlightConfig

Update border highlighting settings when capturing screen video streams through the capture module provided by the RTC SDK. The default display table box.

* **Signature**

   ```ts
   (highlight_config?: HighlightConfig) => number
   ```

* **Notes**

   Before calling this interface, you must have turned on internal screen flow collection by calling [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startscreenvideocapture).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |highlight_config |[HighlightConfig](https://docs.byteplus.com/en/docs/12/docs-85535#highlightconfig) |Border highlighting settings. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### updateScreenCaptureMouseCursor

Update the processing settings for the mouse when capturing screen video streams through the capture module provided by the RTC SDK. Default acquisition mouse.

* **Signature**

   ```ts
   (capture_mouse_cursor?: MouseCursorCaptureState) => number
   ```

* **Notes**

   Before calling this interface, internal screen stream capture must have been turned on by calling [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startscreenvideocapture).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |capture_mouse_cursor |[MouseCursorCaptureState](https://docs.byteplus.com/en/docs/12/docs-85535#mousecursorcapturestate) |Whether to capture the mouse cursor during internal screen\-video capture. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### updateScreenCaptureFilterConfig

When capturing screen video streams through the capture module provided by the RTC SDK, set the window that needs to be filtered.

* **Signature**

   ```ts
   (filter_config?: number[]) => number
   ```

* **Notes**

   * Before calling this interface, internal screen stream capture must have been turned on by calling [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startscreenvideocapture).

   * This function only works when the screen source category is a screen rather than an application window.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |filter_config |number[] |Window filtering settings. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setScreenAudioChannel

Set the audio channel of the screen\-sharing audio stream.

* **Signature**

   ```ts
   (channel: AudioChannel) => number
   ```

* **Notes**

   When the microphone audio stream and the screen\-sharing audio stream are mixed, the audio channel is set by [setAudioProfile](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setaudioprofile) rather than this API.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |channel |[AudioChannel](https://docs.byteplus.com/en/docs/12/docs-85535#audiochannel) |The number of Audio channels. |

* **Return Value**

   Type: number

### getScreenCaptureSourceList

Get the item list for screen sharing.

* **Signature**

   ```ts
   () => ScreenCaptureSourceInfo[]
   ```

* **Notes**

   Whether to include the minimized windows is different based on platforms:

   * The minimized windows are included in the return value for Windows;

   * The minimized windows are not included in the return value for macOS or Linux.

* **Return Value**

   Type: [ScreenCaptureSourceInfo](https://docs.byteplus.com/en/docs/12/docs-85535#screencapturesourceinfo)[]

   List of the screen\-sharing objects, including application window and screens. After the user has decided which item to be shared, pass the object to RTC as an argument of [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startscreenvideocapture).

### getThumbnail

Get the preview thumbnail of the screen\-sharing object.

* **Signature**

   ```ts
   (
     type: ScreenCaptureSourceType,
     source_id: number,
     max_width: number,
     max_height: number
   ) => ThumbnailInfo
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |type |[ScreenCaptureSourceType](https://docs.byteplus.com/en/docs/12/docs-85535#screencapturesourcetype) |Type of the screen capture object. |
   |source_id |number |ID of the screen\-shared object. |
   |max_width |number |Maximum width. The thumbnail preserves the source aspect ratio and is scaled to fit within the specified maximum dimensions. Black bars are added if the specified aspect ratio differs from the source. |
   |max_height |number |Maximum height. Other requirements are the same as for `max_width`. |

* **Return Value**

   Type: [ThumbnailInfo](https://docs.byteplus.com/en/docs/12/docs-85535#thumbnailinfo)

   Screen\-sharing object thumbnail.

### getWindowAppIcon

Get application window preview thumbnail for screen sharing.

* **Signature**

   ```ts
   (
     source_id: number,
     max_width: number,
     max_height: number
   ) => AppIconInfo
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |source_id |number |ID of the screen\-sharing object. You can get the ID by calling [getScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getscreencapturesourcelist). |
   |max_width |number |Maximum width of the App icon. The width is always equal to the height. SDK will set the height and width to the smaller value if the given values are unequal. RTC will return nullptr if you set the value with a number out of the valid range, [32, 256]. The default size is 100 x 100. |
   |max_height |number |Maximum height of the app icon. Other requirements are the same as for `max_width`. |

* **Return Value**

   Type: [AppIconInfo](https://docs.byteplus.com/en/docs/12/docs-85535#appiconinfo)

   You can get the icon when the item to be shared is an application and the application is assigned with an icon. If not, the return value will be nullptr.

### login

Log in to send P2P messages or send messages to a server without joining the RTC room.

* **Signature**

   ```ts
   (
     token: string,
     uid: string
   ) => number
   ```

* **Notes**

   * To log out, call [logout](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-logout).

   * You will receive [onLoginResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onloginresult) after calling this API and log in successfully. But remote users will not receive notification about that.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |token |string |Token is required during login for authentication.<br><br>This Token is different from that required by calling joinRoom. When generating a temporary login token for testing, you can set `roomId` in the token to any value. When generating a production login token, set `roomId` in the token to `null`. |
   |uid |string |User ID which is unique within one appid. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1`: Failure due to invalid parameter.

   * `-2`: Invalid call. RTC will return this value when you call this API after the user has been logged in to the server.

### logout

Calls this interface to log out, it is impossible to call methods related to out\-of\-room messages and end\-to\-server messages or receive related callbacks.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * Before calling this interface to log out, you must call [login](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-login) to log in.

   * After local users call this method to log out, they will receive the result of the [onLogout](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onlogout) callback notification, and remote users will not receive the notification.

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### updateLoginToken

Update the Token.

* **Signature**

   ```ts
   (token: string) => number
   ```

* **Notes**

   * When calling the [login](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-login) method to log in, if an expired token is used, the login will fail and you will receive an [onLoginResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onloginresult) notification with an error code of kLoginErrorCodeInvalidToken. You need to reacquire the token and call this method to update the token.

   * If the token is invalid and the login fails, call this method. After updating the token, the SDK will automatically log back in, and the user does not need to call the [login](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-login) method.

   * Token expires, if you have successfully logged in, it will not be affected. An expired Token error will be notified to the user the next time you log in with an expired Token, or when you log in again due to a disconnection due to poor local network conditions.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |token |string |Token used by the user to log in has a certain valid period. When the Token expires, you need to call this method to update the login Token information. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setServerParams

Set application server parameters.

* **Signature**

   ```ts
   (
     signature: string,
     url: string
   ) => number
   ```

* **Notes**

   * Before the client calls [sendServerMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-sendservermessage) or [sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-sendserverbinarymessage) to send a message to the application server, you must set a valid signature and application server address. You can call this API only after [login](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-login) succeeds.

   * After calling this interface, the SDK will use [onServerParamsSetResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onserverparamssetresult) to return the corresponding result.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |signature |string |Dynamic signature. The App server may use the signature to verify the source of messages.<br><br>You need to define the signature yourself. It can be any non\-empty string. It is recommended to encode information such as UID into the signature.<br><br>The signature will be sent to the address set through the "url" parameter in the form of a POST request. |
   |url |string |The address of the application server. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### getPeerOnlineStatus

Query the login status of the opposite or local user.

* **Signature**

   ```ts
   (peer_user_id: string) => number
   ```

* **Notes**

   * [login](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-login) must be called before this interface can be called.

   * After calling this interface, the SDK notifies the query result using the [onGetPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-ongetpeeronlinestatus) callback.

   * Before sending an out\-of\-room message, the user can know whether the peer user is logged in through this interface to decide whether to send a message. You can also check your login status through this interface.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |peer_user_id |string |User ID to be queried. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### sendUserMessageOutsideRoom

Send a text message (P2P) to a specified user outside the room.

* **Signature**

   ```ts
   (
     uid: string,
     message: string,
     config: MessageConfig
   ) => number
   ```

* **Notes**

   * [Enable the advanced RTS feature in the RTC console](https://console.volcengine.com/rtc/cloudRTC?tab=RTSMode) before calling this API. If you enable it while the SDK is running, recreate the engine for the configuration to take effect.

   * Call this API to send an out\-of\-room text message. You must call [login](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-login) first.

   * After the user calls this interface to send a text message, he will receive an [onUserMessageSendResultOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onusermessagesendresultoutsideroom) callback to know whether the message was successfully sent.

   * If the text message is sent successfully, the user specified by uid receives the message via the [onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onusermessagereceivedoutsideroom) callback.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |uid |string |Message receiving user's ID. |
   |message |string |Text message content sent. Message does not exceed 64 KB. |
   |config |[MessageConfig](https://docs.byteplus.com/en/docs/12/docs-85535#messageconfig) |Message type. |

* **Return Value**

   Type: number

   * \> 0: Sent successfully, return the number of the sent message, increment from 1.

   * \-1: Sent failed, the RTCEngine instance is not created.

   * \-2: Sent failed, uid is empty.

### sendUserBinaryMessageOutsideRoom

Send binary messages (P2P) to a specified user outside the room.

* **Signature**

   ```ts
   (
     uid: string,
     length: number,
     message: Uint8Array,
     config: MessageConfig
   ) => number
   ```

* **Notes**

   * [Enable the advanced RTS feature in the RTC console](https://console.volcengine.com/rtc/cloudRTC?tab=RTSMode) before calling this API. If you enable it while the SDK is running, recreate the engine for the configuration to take effect.

   * [login](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-login) must be called before sending out\-of\-room binary messages.

   * After the user calls this interface to send a binary message, he will receive an [onUserMessageSendResultOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onusermessagesendresultoutsideroom) callback to notify whether the message was sent successfully.

   * If the binary message is sent successfully, the user specified by uid will receive the message through the [onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onusermessagereceivedoutsideroom) callback.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |uid |string |ID of the user receiving the message. |
   |length |number |Length of the binary message in bytes. |
   |message |Uint8Array |Content of the binary message sent. Message does not exceed 64 KB. |
   |config |[MessageConfig](https://docs.byteplus.com/en/docs/12/docs-85535#messageconfig) |Message type. |

* **Return Value**

   Type: number

   * \> 0: sent successfully, return the number of the sent message, increment from 1.

   * \-1: Sent failed, the RTCEngine instance is not created.

   * \-2: Sent failed, uid is empty.

### sendServerMessage

The client side sends a text message to the application server (P2Server).

* **Signature**

   ```ts
   (message: string) => number
   ```

* **Notes**

   * [Enable the advanced RTS feature in the RTC console](https://console.volcengine.com/rtc/cloudRTC?tab=RTSMode) before calling this API. If you enable it while the SDK is running, recreate the engine for the configuration to take effect.

   * Before sending a text message to the application server, call [login](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-login), and then call [setServerParams](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setserverparams) to configure the application server.

   * After calling this interface, you will receive an [onServerMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onservermessagesendresult) callback to inform the message sender whether the message was sent successfully.

   * If the text message is sent successfully, the application server that previously called [setServerParams](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setserverparams) will receive the message.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |message |string |Text message content sent to the application server. The message must not exceed 64 KB. |

* **Return Value**

   Type: number

   * \> 0: Sent successfully, return the number of the sent message, increment from 1.

   * \-1: Sent failed, the RTCEngine instance is not created.

### sendServerBinaryMessage

Client side sends binary messages to the application server (P2Server).

* **Signature**

   ```ts
   (
     length: number,
     message: Uint8Array
   ) => number
   ```

* **Notes**

   * [Enable the advanced RTS feature in the RTC console](https://console.volcengine.com/rtc/cloudRTC?tab=RTSMode) before calling this API. If you enable it while the SDK is running, recreate the engine for the configuration to take effect.

   * Before sending a binary message to the application server, call [login](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-login), and then call [setServerParams](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setserverparams) to configure the application server.

   * After calling this interface, you will receive an [onServerMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onservermessagesendresult) callback to inform the message sender that the sending succeeded or failed.

   * If the binary message is sent successfully, the application server that previously called [setServerParams](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setserverparams) will receive the message.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |length |number |Length of the binary message in bytes. |
   |message |Uint8Array |Binary message content sent to the application server. The message must not exceed 64 KB. |

* **Return Value**

   Type: number

   * \> 0: Sent successfully, return the number of the sent message, increment from 1.

   * \-1: Sent failed, the RTCEngine instance is not created.

### sendSEIMessage

Sends SEI data.

* **Signature**

   ```ts
   (
     message: Uint8Array,
     repeat_count: number,
     mode: SEICountPerFrame
   ) => number
   ```

* **Notes**

   * We recommend the number of SEI messages per second should not exceed the current video frame rate. Because each SEI is sent with a video frame. While in a voice call, SDK will automatically publish a blank video stream with a resolution of 16px × 16px at a frame rate of 15 fps to carry SEI data.

   * In a voice call scenario, this API can be called to send SEI data only in internal capture mode and with a frequency of 15/repeat_count FPS.

   * Each video frame carries only the SEI data received within 2s before and after. In a voice call scenario, if no SEI data is sent within 1min after calling this API, SDK will automatically cancel publishing black frames.

   * After the message is sent successfully, the remote user who subscribed your video stream will receive [onSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onseimessagereceived).

   * When you switch from a voice call to a video call, SEI data transmission will stop and you will need to call this API again to resume the transmission.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |message |Uint8Array |SEI data. The message would be discarded if it exceeds 4 KB. |
   |repeat_count |number |Number of times a message is sent repeatedly. The value range is [0, max{29, %{video frame rate}\-1}]. Recommended range: [2,4].<br><br>This value specifies how many consecutive video frames, starting with the current video frame, the SEI data will be added to after calling this API. |
   |mode |[SEICountPerFrame](https://docs.byteplus.com/en/docs/12/docs-85535#seicountperframe) |SEI message sending mode. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### sendLivePushSEIMessage

Sends SEI data in key\-value format through video frames.

* **Signature**

   ```ts
   (
     json_string: string,
     count: number,
     is_key_frame_only: boolean,
     allow_overwrite: boolean
   ) => number
   ```

* **Notes**

   Before calling this API, join a live\-streaming room and call [setLiveMode](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setlivemode) with `kRoomLiveModeSoloHost`.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |json_string |string |Key\-value pairs in JSON format, for example `{"key1":"value1","key2":"value2"}`.<br><br>If the value for a key is an empty string or `null`, the key is removed from the SEI dictionary.<br><br>The total size of all merged key\-value pairs cannot exceed 10 KB. |
   |count |number |Number of consecutive video frames carrying the SEI data. When `is_key_frame_only` is `true`, this is the number of key frames. |
   |is_key_frame_only |boolean |Whether to send the SEI data only with key frames. |
   |allow_overwrite |boolean |Whether later requests can overwrite the values written by this request. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1`: The video module is not enabled.

   * `-2`: Invalid parameters. `json_string` is empty or `count` is not positive.

   * `-3`: Invalid JSON.

   * `-4`: The total SEI data exceeds the size limit.

### setVideoCaptureConfig

Set the video capture parameters for internal capture of the RTC SDK.

* **Signature**

   ```ts
   (video_capture_config?: VideoCaptureConfig) => number
   ```

* **Notes**

   * This interface can be called after the engine is created and takes effect immediately after being called. It is recommended to call this interface before calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startvideocapture).

   * It is recommended that different Engines on the same device use the same video capture parameters.

   * If you used the internal module to start video capture before calling this interface, the capture parameters default to Auto.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |video_capture_config |[VideoCaptureConfig](https://docs.byteplus.com/en/docs/12/docs-85535#videocaptureconfig) \| undefined |Video capture parameters. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setLocalVoicePitch

Change local voice to a different key, mostly used in Karaoke scenarios. You can adjust the pitch of local voice such as ascending or descending with this method.

* **Deprecated**

   since 325.1, use RTCMediaPlayer and RTCAudioEffectPlayer instead.

* **Signature**

   ```ts
   (pitch: number) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |pitch |number |The value that is higher or lower than the original local voice within a range from \-12 to 12. The default value is 0, Unchanged.<br><br>The difference in pitch between two adjacent values within the value range is a semitone, with positive values indicating an ascending tone and negative values indicating a descending tone, and the larger the absolute value set, the more the pitch is raised or lowered.<br><br>Out of the value range, the setting fails and triggers [onWarning](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onwarning) callback, indicating `WARNING_CODE_SET_SCREEN_STREAM_INVALID_VOICE_PITCH` for invalid value setting with WarningCode. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### startFileRecording

This method records the audio & video data during the call to a local file.

* **Signature**

   ```ts
   (
     config: RecordingConfig,
     recording_type: RecordingType
   ) => number
   ```

* **Notes**

   * After calling this method, you will receive an [onRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onrecordingstateupdate) callback.

   * If the recording is normal, the system will notify the recording progress through [onRecordingProgressUpdate](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onrecordingprogressupdate) callback every second.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |config |[RecordingConfig](https://docs.byteplus.com/en/docs/12/docs-85535#recordingconfig) |Local recording parameter configuration. |
   |recording_type |[RecordingType](https://docs.byteplus.com/en/docs/12/docs-85535#recordingtype) |Recording stored file format. |

* **Return Value**

   Type: number

   * 0: normal.

   * \-1: Parameter setting exception.

   * \-2: The current version of the SDK does not support this Feature, please contact technical support staff.

### stopFileRecording

Stop local recording.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * Call [startFileRecording](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startfilerecording) After starting local recording, you must call this method to stop recording.

   * After calling this method, you will receive an [onRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onrecordingstateupdate) callback prompting you to record the result.

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setPublishFallbackOption

Sets the fallback option for published audio & video streams. You can call this API to set whether to automatically lower the resolution you set of the published streams under limited network conditions.

* **Signature**

   ```ts
   (option: number) => number
   ```

* **Notes**

   * This API only works after you call [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setlocalsimulcastmode) to enable publishing multiple streams.

   * You must call this API before entering the room.

   * If fallback or recovery occurs because of poor device performance or network conditions, the local user receives [onPerformanceAlarms](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onperformancealarms) in advance.

   * After you allow video stream to fallback, your stream subscribers will receive [onSimulcastSubscribeFallback](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onsimulcastsubscribefallback) when the resolution of your published stream are lowered or restored.

   * You can alternatively set fallback options with distrubutions from server side, which is of higher priority.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |option |number |Fallback option:<br><br><br>* `0`: Disable fallback for published audio and video streams. This is the default.<br><br>* `1`: Publish only the low\-resolution video stream when uplink network conditions or device performance are poor. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setSubscribeFallbackOption

Sets the fallback option for subscribed RTC streams. You can call this API to set whether to lower the resolution of currently subscribed stream under limited network conditions.

* **Signature**

   ```ts
   (option: number) => number
   ```

* **Notes**

   * You must call this API before enterting the room.

   * After you enables the fallback, you will receive [onSimulcastSubscribeFallback](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onsimulcastsubscribefallback) and [onRemoteVideoSizeChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onremotevideosizechanged) when the resolution of your subscribed stream is lowered or restored.

   * You can alternatively set fallback options with distrubutions from server side, which is of higher priority.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |option |number |Fallback option:<br><br><br>* `0`: Disable subscription fallback.<br><br>* `1`: Receive only the low\-resolution video stream.<br><br>* `2`: Receive the low\-resolution video stream first, then fall back to audio only if video cannot be displayed. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setRemoteUserPriority

Set user priority.

* **Signature**

   ```ts
   (
     room_id: string,
     user_id: string,
     priority: RemoteUserPriority
   ) => number
   ```

* **Notes**

   * This method is used with [setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setsubscribefallbackoption).

   * If the subscription flow fallback option is turned on, weak connections or insufficient performance will give priority to ensuring the quality of the flow received by high\-priority users.

   * This method can be used before and after entering the room, and the priority of the remote user can be modified.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |room_id |string |Room ID. |
   |user_id |string |Remote user's ID. |
   |priority |[RemoteUserPriority](https://docs.byteplus.com/en/docs/12/docs-85535#remoteuserpriority) |Remote user's requirement priority. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### startNetworkDetection

Pre\-call network detection.

* **Signature**

   ```ts
   (
     is_test_uplink: boolean,
     expected_uplink_bitrate: number,
     is_test_downlink: boolean,
     expected_downlink_biterate: number
   ) => number
   ```

* **Notes**

   * After calling this interface, you will receive [onNetworkDetectionResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onnetworkdetectionresult) within 3s and every 2s thereafter notifying the probe result;

   * If the probe stops, you will receive [onNetworkDetectionStopped](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onnetworkdetectionstopped) notify that probing has stopped.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |is_test_uplink |boolean |Whether to detect uplink bandwidth. |
   |expected_uplink_bitrate |number |Expected uplink bandwidth, unit: kbpsRange: {0, [100\-10000]}, `0`: Auto, that RTC will set the highest bitrate. |
   |is_test_downlink |boolean |Whether to detect downlink bandwidth. |
   |expected_downlink_biterate |number |Expected downlink bandwidth, unit: kbpsRange: {0, [100\-10000]}, `0`: Auto, that RTC will set the highest bite rate. |

* **Return Value**

   Type: number

   * 0: Network probing enabled successfully.

   * 1: Failed to start probing. Parameter error, both uplink and downlink probes are 'false ', or the expected bandwidth exceeds the range [100,10000].

   * 2: Failed to start probing. The reason for the failure is that the local push\-pull flow has started.

   * 3: Detection has started, no need to open it again.

   * 4: Do not support this feature.

### stopNetworkDetection

Stop pre\-call network probe.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   After calling this interface, you will receive [onNetworkDetectionStopped](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onnetworkdetectionstopped) notifying that the probing has stopped.

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### enableVirtualBackground

Set the original background to a specified image or a solid color. To disable this effect, set the modelPath parameter to null.

* **Signature**

   ```ts
   (
     background_sticker_path: string,
     source: VirtualBackgroundSource
   ) => number
   ```

* **Notes**

   * You must call [initCVResource](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-initcvresource) before calling this API.

   * Call [disableVirtualBackground](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-disablevirtualbackground) to turn off the virtual background.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |background_sticker_path |string |The absolute path of virtual background effects. |
   |source |[VirtualBackgroundSource](https://docs.byteplus.com/en/docs/12/docs-85535#virtualbackgroundsource) |Virtual background source. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1000`：The BytePlus Effects SDK is not integrated.

   * `-1001`：This feature is not supported in the BytePlus Effects SDK.

   * `–1002`: Your Effects SDK's version is incompatible.

   * `<0`：Other errors. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

### disableVirtualBackground

Turns off the virtual background.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   After calling [enableVirtualBackground](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enablevirtualbackground) to enable the virtual background function, you can call this API to turn it off.

* **Return Value**

   Type: number

   * `0`: Success.

   * `–1000`: The Effects SDK is not integrated.

   * `–1001`: This API is unavailable for your Effects SDK.

   * `–1002`: Your Effects SDK's version is incompatible.

   * `< 0`: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

### enableFaceDetection

Starts face detection and registers the observer for the result.

* **Signature**

   ```ts
   (
     interval_ms: number,
     face_model_path: string
   ) => number
   ```

* **Notes**

   With this observer, you will receive [onFaceDetectResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onfacedetectresult) periodically.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |interval_ms |number |The minimum time interval between two callbacks in milliseconds. The value should be greater than 0. The actual time interval is between `interval_ms` and `interval_ms+the time slot of a captured video frame`. |
   |face_model_path |string |The absolute path of the face detection algorithm file. Typically it is the tt_face_vXXX.model file in the ttfacemodel folder. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `–1000`: The Effects SDK is not integrated.

   * `–1001`: This API is unavailable for your Effects SDK.

   * `–1002`: Your Effects SDK's version is incompatible.

   * `-1004`: Initializing. This function will be available when the initialization is completed.

   * `<0`: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

### disableFaceDetection

Stops face detection.

* **Signature**

   ```ts
   () => number
   ```

* **Return Value**

   Type: number

   * `0`: Success.

   * `–1000`: The Effects SDK is not integrated.

   * `–1001`: This API is unavailable for your Effects SDK.

   * `–1002`: Your Effects SDK's version is incompatible.

   * `<0`: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

### setVideoWatermark

Adds watermark to the local video stream.

* **Signature**

   ```ts
   (
     image_path: string,
     config: RTCWatermarkConfig
   ) => number
   ```

* **Notes**

   * Call [clearVideoWatermark](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-clearvideowatermark) to remove the watermark from the local video stream.

   * You can only add one watermark at a time. The newly added watermark replaces the previous one.

   * If you mirror the preview, or the preview and the published stream, the watermark will also be mirrored locally, but the published watermark will not be mirrored.

   * When you enable simulcast mode, the watermark will be added to all video streams, and it will be scaled down to smaller encoding configurations accordingly.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |image_path |string |File path of the watermark image. You can use the absolute path or the asset path(/assets/xx.png). The path should be less than 512 bytes.<br><br>The watermark image should be in PNG or JPG format. |
   |config |[RTCWatermarkConfig](https://docs.byteplus.com/en/docs/12/docs-85535#rtcwatermarkconfig) |Watermark configurations. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### clearVideoWatermark

Removes video watermark from the local video stream.

* **Signature**

   ```ts
   () => any
   ```

* **Return Value**

   * 0: Succeed.

   * 1000: Integrating CV SDK failed.

   * 1001: Invalid SDK version.

   * <0: Failed.

### setupLocalVideo

Set the view for the local video.

* **Signature**

   ```ts
   (
     view: HTMLDivElement,
     render_options?: RenderOptions,
     position?: LocalVideoSinkPosition
   ) => number
   ```

* **Notes**

   If you need to unbind the video stream from the current view, call [removeLocalVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-removelocalvideo).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |view |HTMLDivElement |View. |
   |render_options |[RenderOptions](https://docs.byteplus.com/en/docs/12/docs-85535#renderoptions) |Render options. |
   |position |[LocalVideoSinkPosition](https://docs.byteplus.com/en/docs/12/docs-85535#localvideosinkposition) |Local video frame callback position. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1`: Failure.

### removeLocalVideo

Unbind the local video stream from its rendering view.

* **Signature**

   ```ts
   () => number
   ```

* **Return Value**

   Type: number

   * `0`: Success.

   * `< 0`: Failure.

### setupRemoteVideo

Bind the remote video stream to the view.

* **Signature**

   ```ts
   (
     stream_id: string,
     view: HTMLDivElement,
     render_options?: RenderOptions,
     sink_config?: RemoteVideoSinkConfig
   ) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Remote stream ID. |
   |view |HTMLDivElement |The view for rendering the remote video stream. |
   |render_options |[RenderOptions](https://docs.byteplus.com/en/docs/12/docs-85535#renderoptions) |Rendering options for the remote video stream. |
   |sink_config |[RemoteVideoSinkConfig](https://docs.byteplus.com/en/docs/12/docs-85535#remotevideosinkconfig) |Remote video sink config. Optional. Supports `pixel_format`, `apply_rotation`, and `mirror_type`. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1`: Failure.

### removeRemoteVideo

Unbind the remote video from the view.

* **Signature**

   ```ts
   (stream_id: string) => number
   ```

* **Notes**

   Call this API after stopping receiving the remote video.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Remote stream ID. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1`: Failure.

### removeAllRemoteVideo

Unbind all remote videos from the views.

* **Signature**

   ```ts
   (room_id: string) => number
   ```

* **Notes**

   Call this API after stopping receiving the remote video.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |room_id |string |Room ID. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1`: Failure.

### requestRemoteVideoKeyFrame

Requests a key video frame from a subscribed remote video stream.

* **Signature**

   ```ts
   (stream_id: string) => number
   ```

* **Notes**

   * Call this API after subscribing to the remote video stream.

   * The native SDK limits this API to manual subscription scenarios. It is mainly used after enabling custom decoding with `setVideoDecoderConfig`, when the custom decoder needs a fresh key frame.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Remote stream ID. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `<0`: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85535#returnstatus) for details.

### setLocalVideoSink

Get local video stream.

* **Signature**

   ```ts
   (config: LocalVideoSinkConfig) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |config |[LocalVideoSinkConfig](https://docs.byteplus.com/en/docs/12/docs-85535#localvideosinkconfig) |Local video sink config. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1`: Failure.

### unsetLocalVideoSink

Stop get local video stream.

* **Signature**

   ```ts
   () => number
   ```

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1`: Failure.

### setRemoteVideoSink

Get remote video stream.

* **Signature**

   ```ts
   (
     stream_id: string,
     config?: RemoteVideoSinkConfig
   ) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Remote stream id. |
   |config |[RemoteVideoSinkConfig](https://docs.byteplus.com/en/docs/12/docs-85535#remotevideosinkconfig) |Remote video sink config. Optional. Supports `pixel_format`, `apply_rotation`, and `mirror_type`. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1`: Failure.

### unsetRemoteVideoSink

Stop get remote video stream.

* **Signature**

   ```ts
   (stream_id: string) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |Remote stream ID. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1`: Failure.

### setLocalVoiceEqualization

Set the equalization effect for the local captured audio. The audio includes both internal captured audio and external captured voice, but not the mixing audio file.

* **Signature**

   ```ts
   (config: VoiceEqualizationConfig) => number
   ```

* **Notes**

   According to the Nyquist acquisition rate, the audio acquisition rate must be greater than twice the set center frequency. Otherwise, the setting will not be effective.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |config |[VoiceEqualizationConfig](https://docs.byteplus.com/en/docs/12/docs-85535#voiceequalizationconfig) |Voice equalization config. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `<0`: Failure.

### setLocalVoiceReverbParam

Set the equalization effect for the local captured audio. The audio includes both internal captured audio and external captured voice, but not the mixing audio file.

* **Signature**

   ```ts
   (param?: VoiceReverbConfig) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |param |[VoiceReverbConfig](https://docs.byteplus.com/en/docs/12/docs-85535#voicereverbconfig) \| undefined |Equalization settings. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `<0`: Failure.

### enableLocalVoiceReverb

Enable the reverb effect for the local captured voice.

* **Signature**

   ```ts
   (enable: boolean) => number
   ```

* **Notes**

   Call [setLocalVoiceReverbParam](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setlocalvoicereverbparam) to set the reverb effect.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |enable |boolean |Whether to enable the reverb effect. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `<0`: Failure.

### startAudioRecording

Start recording audio communication, and generate the local file.

* **Signature**

   ```ts
   (config: AudioRecordingConfig) => number
   ```

* **Notes**

   * All audio effects are valid in the file. Mixed audio file is not included in the file.

   * Call [stopAudioRecording](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopaudiorecording) to stop recording.

   * Call this API after joining the room. If you join multiple rooms, audio from all rooms are recorded in one file. After you leave the last room, the recording task ends automatically.

   * After calling the API, you'll receive [onAudioRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onaudiorecordingstateupdate).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |config |[AudioRecordingConfig](https://docs.byteplus.com/en/docs/12/docs-85535#audiorecordingconfig) |Recording configuration. |

* **Return Value**

   Type: number

   * `0`: `kReturnStatusSuccess`: Success.

   * `-2`: `kReturnStatusParameterErr`: Invalid parameters.

   * `-3`: `kReturnStatusWrongState`: Not valid in this SDK. Please contact the technical support.

### stopAudioRecording

Stops local audio recording.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   Call [startAudioRecording](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudiorecording) to start local audio recording.

* **Return Value**

   Type: number

   * `0`: Success.

   * `-3`: The current SDK version does not support this feature. Contact technical support.

### enableAGC

Enable or disable automatic gain control to adjust microphone pickup volume.

* **Signature**

   ```ts
   (enable: boolean) => number
   ```

* **Notes**

   * You can call this method before and after joining the room. To turn on AGC before joining the room, you need to contact the technical support to get a private parameter to set [RoomProfileType](https://docs.byteplus.com/en/docs/12/docs-85535#roomprofiletype).

   * To enable AGC after joining the room, you must set [RoomProfileType](https://docs.byteplus.com/en/docs/12/docs-85535#roomprofiletype) to `kRoomProfileTypeMeeting`, `kRoomProfileTypeMeetingRoom` or `kRoomProfileTypeClassroom`.

   * It is not recommended to call [setAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setaudiocapturedevicevolume) to adjust microphone pickup volume with AGC on.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |enable |boolean |whether to turn on AGC.<br><br><br>* true: AGC is turned on.<br><br>* false: AGC is turned off. |

* **Return Value**

   Type: number

   * 0: Success.

   * \-1: Failure.

### setVideoCaptureRotation

Set the rotation of the local video images. Call this API to rotate the videos when the camera is fixed upside down or tilted.

* **Signature**

   ```ts
   (rotation: VideoRotation) => number
   ```

* **Notes**

   * This API affects the external\-sourced videos. The final rotation would be the original rotation angles adding up with the rotation set by calling this API.

   * This API would not rotate the background added by calling [enableVirtualBackground](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enablevirtualbackground).

   * The rotation would not be applied to the Stream pushed to CDN.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |rotation |[VideoRotation](https://docs.byteplus.com/en/docs/12/docs-85535#videorotation) |It defaults to `VIDEO_ROTATION_0(0)`, which means not to rotate. |

* **Return Value**

   Type: number

### setVideoDigitalZoomConfig

Set the step size for each digital zooming control to the local videos.

* **Signature**

   ```ts
   (
     type: ZoomConfigType,
     size: number
   ) => number
   ```

* **Notes**

   * Only one size can be set for a single call. You must call this API to pass values respectively if you intend to set multiple `size`s.

   * As the default `size` is `0`, you must call this API before performing any digital zoom control by calling [setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvideodigitalzoomcontrol) or [startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startvideodigitalzoomcontrol).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |type |[ZoomConfigType](https://docs.byteplus.com/en/docs/12/docs-85535#zoomconfigtype) |Required. Identifying which type the `size` is referring to. |
   |size |number |Required. Reserved to three decimal places. It defaults to `0`.<br><br>The meaning and range vary from different `type`s. If the scale or moving distance exceeds the range, the limit is taken as the result.<br><br><br>* `kZoomFocusOffset`: Increase or decrease to the scaling factor. Range: [0, 7]. For example, when it is set to 0.5 and [setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvideodigitalzoomcontrol) is called to zoom in, the scale will increase `0.5`. The scale ranges [1，8] and defaults to `1`, which means an original size.<br><br>* `kZoomMoveOffset`：Ratio of the distance to the border of video images. It ranges [0, 0.5] and defaults to `0`, which means no offset. When you call [setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvideodigitalzoomcontrol) and choose `CAMERA_MOVE_LEFT`, the moving distance is size x original width. While for the `CAMERA_MOVE_UP`, the moving distance is size x original height. Suppose that a video spans 1080 px and the `size` is set to `0.5` so that the distance would be 0.5 x 1080 px = 540 px. |

* **Return Value**

   Type: number

### setVideoDigitalZoomControl

Digital zoom or move the local video image once. This action affects both the video preview locally and the stream published.

* **Signature**

   ```ts
   (direction: ZoomDirectionType) => number
   ```

* **Notes**

   * As the default offset is `0`, you must call [setVideoDigitalZoomConfig](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvideodigitalzoomconfig) before this API.

   * You can only move video images after they are magnified via this API or [startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startvideodigitalzoomcontrol).

   * When you request an out\-of\-range scale or movement, SDK will execute it with the limits. For example, when the image has been moved to the border, the image cannot be zoomed out, or has been magnified to 8x.

   * Call [startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startvideodigitalzoomcontrol) to have a continuous and repeatedly digital zoom control.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |direction |[ZoomDirectionType](https://docs.byteplus.com/en/docs/12/docs-85535#zoomdirectiontype) |Action of the digital zoom control. |

* **Return Value**

   Type: number

### startVideoDigitalZoomControl

Continuous and repeatedly digital zoom control. This action effect both the video preview locally and the stream published.

* **Signature**

   ```ts
   (direction: ZoomDirectionType) => number
   ```

* **Notes**

   * As the default offset is `0`, you must call [setVideoDigitalZoomConfig](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvideodigitalzoomconfig) before this API.

   * You can only move video images after they are magnified via this API or [setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvideodigitalzoomcontrol).

   * The control process stops when the scale reaches the limit, or the images have been moved to the border. if the next action exceeds the scale or movement range, SDK will execute it with the limits.

   * Call [stopVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopvideodigitalzoomcontrol) to stop the ongoing zoom control.

   * Call [setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvideodigitalzoomcontrol) to have a one\-time digital zoom control.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |direction |[ZoomDirectionType](https://docs.byteplus.com/en/docs/12/docs-85535#zoomdirectiontype) |Action of the digital zoom control. |

* **Return Value**

   Type: number

### stopVideoDigitalZoomControl

Stop the ongoing digital zoom control instantly.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   Refer to [startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startvideodigitalzoomcontrol) for starting digital zooming.

* **Return Value**

   Type: number

### startPushMixedStream

Starts a task that publishes a mixed stream to CDN or publishes a WTN stream.

* **Signature**

   ```ts
   (
     task_id: string,
     config: IMixedStreamConfig
   ) => number
   ```

* **Notes**

   * Since 3.60, this API replaces the old push\-to\-CDN and public\-stream publishing APIs.

   * Call [updatePushMixedStream](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-updatepushmixedstream) to update the task and [stopPushMixedStream](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stoppushmixedstream) to stop it.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |task_id |string |Task ID. It is used to identify the push task when the target type is CDN. When the target type is WTN, this value is ignored and can be an empty string. |
   |config |[IMixedStreamConfig](https://docs.byteplus.com/en/docs/12/docs-85535#imixedstreamconfig) |Mixed stream task configurations. |

* **Return Value**

   Type: number

   * `0`: Success. Use [onMixedStreamEvent](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onmixedstreamevent) to receive task events and errors.

   * `!0`: Failure.

### updatePushMixedStream

Updates parameters of a task started by [startPushMixedStream](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startpushmixedstream).

* **Signature**

   ```ts
   (
     task_id: string,
     config: IMixedStreamConfig
   ) => number
   ```

* **Notes**

   Properties omitted in the config may be reset to default values by the SDK.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |task_id |string |Task ID. It takes effect when the target type is CDN. |
   |config |[IMixedStreamConfig](https://docs.byteplus.com/en/docs/12/docs-85535#imixedstreamconfig) |Mixed stream task configurations to update. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `!0`: Failure.

### stopPushMixedStream

Stop pushing a mixed stream to its target.

* **Signature**

   ```ts
   (
     task_id: string,
     target_type?: MixedStreamPushTargetType
   ) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |task_id |string |Mixed\-stream push task ID. |
   |target_type |[MixedStreamPushTargetType](https://docs.byteplus.com/en/docs/12/docs-85535#mixedstreampushtargettype) |Push target type. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `<0`: Failure.

### startHardwareEchoDetection

Start echo detection before joining a room.

* **Signature**

   ```ts
   (test_audio_file_path: string) => number
   ```

* **Notes**

   * You can use this feature only when `RoomProfileType` is set to `kRoomProfileTypeMeeting` or `kRoomProfileTypeMeetingRoom`.

   * Before calling this API, ask the user for the permissions to access the local audio devices.

   * Before calling this api, make sure the audio devices are active and keep the capture volume and the playback volume within a reasonable range.

   * The detection result is passed as the argument of [onHardwareEchoDetectionResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onhardwareechodetectionresult).

   * During the detection, the SDK is not able to response to the other testing APIs, such as [startEchoTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startechotest) or [startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudioplaybackdevicetest).

   * Call [stopHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stophardwareechodetection) to stop the detection and release the audio devices.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |test_audio_file_path |string |Absolute path of the music file for the detection. It is expected to encode with UTF\-8. The following files are supported: mp3, aac, m4a, 3gp, wav.<br><br>We recommend to assign a music file whose duration is between 10 to 20 seconds.<br><br>Do not pass a Silent file. |

* **Return Value**

   Type: number

   Method call result:

   * 0: Success.

   * \-1: Failure due to the onging process of the previous detection. Call [stopHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stophardwareechodetection) to stop it before calling this API again.

   * \-2: Failure due to an invalid file path or file format.

### stopHardwareEchoDetection

Stop the echo detection before joining a room.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * Refer to [startHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-starthardwareechodetection) for information on how to start a echo detection.

   * We recommend calling this API to stop the detection once getting the detection result from [onHardwareEchoDetectionResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onhardwareechodetectionresult).

   * You must stop the echo detection to release the audio devices before the user joins a room. Otherwise, the detection may interfere with the call.

* **Return Value**

   Type: number

   Method call result:

   * 0: Success.

   * \-1: Failure.

### setLocalProxy

Sets local proxy.

* **Signature**

   ```ts
   (configurations: LocalProxyConfiguration[]) => number
   ```

* **Notes**

   * You must call this API before joining the room.

   * After calling this API, you will receive [onLocalProxyStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onlocalproxystatechanged) callback that informs you of the states of local proxy connection.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |configurations |[LocalProxyConfiguration](https://docs.byteplus.com/en/docs/12/docs-85535#localproxyconfiguration)[] |Local proxy configurations.<br><br>You can set both Http tunnel and Socks5 as your local proxies, or only set one of them based on your needs. If you set both Http tunnel and Socks5 as your local proxies, then media traffic and signaling are routed through Socks5 proxy and Http requests through Http tunnel proxy. If you set either Http tunnel or Socks5 as your local proxy, then media traffic, signaling and Http requests are all routed through the proxy you chose.<br><br>If you want to remove the existing local proxy configurations, you can call this API with the parameter set to null. |

* **Return Value**

   Type: number

### setEarMonitorMode

Turn on/off the earphone monitor function.

* **Signature**

   ```ts
   (mode: EarMonitorMode) => number
   ```

* **Notes**

   You can use ear monitoring feature when the earpiece is directly connected to the device by 3.5mm interface, USB interface, or Bluetooth. You cannot use ear monitoring feature when the earpiece is connected to a monitor via the HDMI or USB\-C interface, and then connected to the device, or connected to an OTG external sound card, and then connected to the device.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |mode |[EarMonitorMode](https://docs.byteplus.com/en/docs/12/docs-85535#earmonitormode) |Whether to turn on the earphone monitor function. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0 : Fail.

### setEarMonitorVolume

Set the volume of the earphone monitor.

* **Signature**

   ```ts
   (volume: number) => number
   ```

* **Notes**

   Before setting the volume of the earphone monitor, you must first call [setEarMonitorMode](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setearmonitormode) to turn on the earphone monitor function.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |volume |number |The volume of the earphone monitor, the value range: [0,100], the unit:%. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0 : Fail.

### getAudioEffectPlayer

Create an instance for audio effect player.

* **Signature**

   ```ts
   () => veRTCAudioEffectPlayer
   ```

* **Return Value**

   Type: veRTCAudioEffectPlayer

   an instance for audio effect player.

### getMediaPlayer

Create a media player instance.

* **Signature**

   ```ts
   (player_id: number) => veRTCMediaPlayer
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |player_id |number |Media player id. The range is `[0, 3]`. You can create up to 4 instances at the same time. If it exceeds the range, nullptr will be returned. |

* **Return Value**

   Type: veRTCMediaPlayer

   Media player instance.

### getWTNStream

Gets the WTN stream instance.

* **Signature**

   ```ts
   () => veRTCWTNStream
   ```

* **Return Value**

   Type: veRTCWTNStream

   WTN stream instance.

### enableExternalSoundCard

Enable the audio process mode for external sound card.

* **Signature**

   ```ts
   (enable: boolean) => number
   ```

* **Notes**

   * When you use external sound card for audio capture, enable this mode for better audio quality.

   * When using the mode, you can only use earphones. If you need to use internal or external speaker, disable this mode.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |enable |boolean |Whether to enable the mode.<br><br><br>* true: enable<br><br>* false: disable (by default). |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0 : Fail.

### enableAudioFrameCallback

Enable audio frames callback and set the format for the specified type of audio frames.

* **Signature**

   ```ts
   (
     method: AudioFrameCallbackMethod,
     format: AudioFormat
   ) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |method |[AudioFrameCallbackMethod](https://docs.byteplus.com/en/docs/12/docs-85535#audioframecallbackmethod) |Audio data callback method.<br><br>If `method` is set as `kRecord`, `kPlayback`, `kMixed`, `kRecordScreen`, set `format` to the accurate value listed in the audio parameters format.<br><br>If `method` is set as `kRemoteUser`, set `format` to default value. |
   |format |[AudioFormat](https://docs.byteplus.com/en/docs/12/docs-85535#audioformat) |Audio parameters format. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0 : Fail.

### disableAudioFrameCallback

Disables audio data callback.

* **Signature**

   ```ts
   (method: AudioFrameCallbackMethod) => number
   ```

* **Notes**

   Call this API after calling [enableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableaudioframecallback).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |method |[AudioFrameCallbackMethod](https://docs.byteplus.com/en/docs/12/docs-85535#audioframecallbackmethod) |Audio data callback method. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0 : Fail.

### setAudioAlignmentProperty

On the listener side, set all subscribed audio streams precisely timely aligned.

* **Signature**

   ```ts
   (
     stream_id: string,
     mode: AudioAlignmentMode
   ) => number
   ```

* **Notes**

   * You must use the function when all participants set [RoomProfileType](https://docs.byteplus.com/en/docs/12/docs-85535#roomprofiletype) to `kRoomProfileTypeChorus` when joining the room.

   * All remote participants must use RTCMediaPlayer to play background music and keep progress synchronized to the recorded frame.

   * If the subscribed audio stream is delayed too much, it may not be precisely aligned.

   * The chorus participants must not enable the alignment. If you wish to change the role from listener to participant, you should disable the alignment.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |The remote audio stream ID used as the benchmark during time alignment.<br><br>You are recommended to use the audio stream from the lead singer.<br><br>You must call this API after receiving [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserpublishstreamaudio). |
   |mode |[AudioAlignmentMode](https://docs.byteplus.com/en/docs/12/docs-85535#audioalignmentmode) |Whether to enable the alignment. Disabled by default. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0 : Fail.

### enablePlaybackDucking

Enables/disables the playback ducking function. This function is usually used in scenarios where short videos or music will be played simultaneously during RTC calls.

* **Signature**

   ```ts
   (enable: boolean) => number
   ```

* **Notes**

   With the function on, if remote voice is detected, the local media volume will be lowered to ensure the clarity of the remote voice. If remote voice disappears, the local media volume restores.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |enable |boolean |Whether to enable playback ducking:<br><br><br>* true: Yes<br><br>* false: No. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0 : Fail.

### startAudioDeviceRecordTest

Start the capture and playback test for local audio devices.

* **Signature**

   ```ts
   (indication_interval: number) => number
   ```

* **Notes**

   * The audio capturing stops in 30s after calling this API and begins to play the recording audio. Before that, you can call [stopAudioDeviceRecordAndPlayTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopaudiodevicerecordandplaytest) to stop audio capturing and start playing the recording audio.

   * Call [stopAudioDevicePlayTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopaudiodeviceplaytest) to stop the test, including capturing and playing the recording.

   * You must stop the test before starting another test for audio devices.

   * You must stop the test before calling [enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableaudiopropertiesreport).

   * This test performs locally and does not involve network connection testing.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |indication_interval |number |During the test, you'll receive [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onlocalaudiopropertiesreport) periodically. Set the period in ms with this parameter. Recommended value is 200 ms; the minimal value is 10 ms. |

* **Return Value**

   Type: number

   result:

   * 0: success.

   * < 0: failure.

### stopAudioDeviceRecordAndPlayTest

Call this API to stop recording in the test and start to play the recording in 30 s after calling [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudiodevicerecordtest).

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   After calling this API, the recording starts playing during which you can call [stopAudioDevicePlayTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-stopaudiodeviceplaytest) to stop playing.

* **Return Value**

   Type: number

   result:

   * 0: Success.

   * < 0: Failure.

### stopAudioDevicePlayTest

Stop the capture and playback test for local audio devices which is started by calling [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startaudiodevicerecordtest).

Before the test ends by itself, you can call this API to stop the recording or playing.

* **Signature**

   ```ts
   () => number
   ```

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: failure.

### sendPublicStreamSEIMessage

* **Signature**

   ```ts
   (
     channel_id: number,
     message: Uint8Array,
     repeat_count: number,
     mode: SEICountPerFrame
   ) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |channel_id |number | |
   |message |Uint8Array | |
   |repeat_count |number | |
   |mode |[SEICountPerFrame](https://docs.byteplus.com/en/docs/12/docs-85535#seicountperframe) | |

* **Return Value**

   Type: number

### setLowLightAdjusted

Sets the low\-light video enhancement mode. Enable this feature in low\-light, unevenly lit, or backlit environments to improve video quality.

* **Signature**

   ```ts
   (mode: VideoEnhancementMode) => number
   ```

* **Notes**

   * Enabling this feature increases device resource usage. Enable it based on actual requirements and device performance.

   * This feature applies to video captured internally by the RTC SDK and externally captured video.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |mode |[VideoEnhancementMode](https://docs.byteplus.com/en/docs/12/docs-85535#videoenhancementmode) |Video enhancement mode. The feature is disabled by default. |

* **Return Value**

   Type: number

   * `0`: Success. The setting takes effect immediately, but the enhanced result is available only after model download and detection are complete.

   * `< 0`: Failure.

### notifyRemoteStreamUnpublished

* **Signature**

   ```ts
   (
     _streamInfo: StreamInfo,
     streamId: string
   ) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |_streamInfo |[StreamInfo](https://docs.byteplus.com/en/docs/12/docs-85535#streaminfo) | |
   |streamId |string | |

### `static` getSDKVersion

Get the current SDK version information.

* **Signature**

   ```ts
   () => string
   ```

* **Return Value**

   Type: string

   Current SDK version information.

### `static` setLogConfig

Configure the logs.

* **Signature**

   ```ts
   (log_config: LogConfig) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |log_config |[LogConfig](https://docs.byteplus.com/en/docs/12/docs-85535#logconfig) |Log configuration. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1`: Failure.

### `static` getCurrentProcessId

Get process ID of the engine for commissioning.

* **Signature**

   ```ts
   () => string
   ```

* **Return Value**

   Type: string

   Process ID.

### `static` setRenderType

set render type.

* **Signature**

   ```ts
   (type: RenderType) => void
   ```

* **Notes**

   * The default rendering type is WebGL rendering.

   * Set WebGL rendering，if WebGL rendering is not supported or WebGL rendering fails, it will automatically switch to Software rendering.

   * After setting the rendering type, the newly created canvas rendering type will take effect in the new rendering mode.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |type |[RenderType](https://docs.byteplus.com/en/docs/12/docs-85535#rendertype) |render type. |

### `static` getTimestampMs

Gets the timestamp in milliseconds.

* **Signature**

   ```ts
   () => number
   ```

* **Return Value**

   Type: number

   Timestamp in milliseconds.

### `static` getTimestampUs

Gets the timestamp in microseconds.

* **Signature**

   ```ts
   () => number
   ```

* **Return Value**

   Type: number

   Timestamp in microseconds.

## RTCRoom

Type: `class`

* **API**

|Method |Description |
|---|---|
|[getRoomId](https://docs.byteplus.com/en/docs/12/14196#rtcroom-getroomid) |Get room ID. |
|[getCallId](https://docs.byteplus.com/en/docs/12/14196#rtcroom-getcallid) |Get Call ID。<br><br>This method needs to be called after joining a room. |
|[setLiveMode](https://docs.byteplus.com/en/docs/12/14196#rtcroom-setlivemode) |Sets the live\-streaming mode for the room. |
|[destroy](https://docs.byteplus.com/en/docs/12/14196#rtcroom-destroy) |Leave and destroy the room. |
|[joinRoom](https://docs.byteplus.com/en/docs/12/14196#rtcroom-joinroom) |Join the room. |
|[leaveRoom](https://docs.byteplus.com/en/docs/12/14196#rtcroom-leaveroom) |Leave RTC room. |
|[setUserVisibility](https://docs.byteplus.com/en/docs/12/14196#rtcroom-setuservisibility) |Set the visibility of the user in the room. The local user is visible to others by default before calling this API. |
|[setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/14196#rtcroom-setmultideviceavsync) |Synchronizes published audio and video. |
|[updateToken](https://docs.byteplus.com/en/docs/12/14196#rtcroom-updatetoken) |Update Token. A Token contains the privilege of joining a room, publishing streams, and subscribing to streams. Each privilege has an expiration time. A callback will be triggered 30s before expiration, informing the user to update the Token. In this case, you need to get a new Token and update the Token with this API to ensure the normal call. |
|[publishStreamVideo](https://docs.byteplus.com/en/docs/12/14196#rtcroom-publishstreamvideo) |Start or stop publishing video streams captured by camera in the current room. |
|[publishStreamAudio](https://docs.byteplus.com/en/docs/12/14196#rtcroom-publishstreamaudio) |Start or stop publishing media streams captured by the local microphone in the current room. |
|[subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/14196#rtcroom-subscribestreamvideo) |Subscribes to specific remote media streams captured by the local camera. Or update the subscribe options of the subscribed user. |
|[subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/14196#rtcroom-subscribestreamaudio) |Subscribes to specific remote media streams captured by the local microphone. Or update the subscribe options of the subscribed user. |
|[setRemoteVideoConfig](https://docs.byteplus.com/en/docs/12/14196#rtcroom-setremotevideoconfig) |Sets your expected configuration of the remote video stream that you want to subscribe to or have subscribed to. |
|[subscribeAllStreamsAudio](https://docs.byteplus.com/en/docs/12/14196#rtcroom-subscribeallstreamsaudio) |Subscribes to all remote audio streams captured by microphone. |
|[unsubscribeAllStreamsAudio](https://docs.byteplus.com/en/docs/12/14196#rtcroom-unsubscribeallstreamsaudio) |Unsubscribes from all remote audio streams captured by microphone. |
|[subscribeAllStreamsVideo](https://docs.byteplus.com/en/docs/12/14196#rtcroom-subscribeallstreamsvideo) |Subscribes to all remote video streams captured by camera. |
|[unsubscribeAllStreamsVideo](https://docs.byteplus.com/en/docs/12/14196#rtcroom-unsubscribeallstreamsvideo) |Unsubscribes from all remote video streams captured by camera. |
|[pauseAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/14196#rtcroom-pauseallsubscribedstreamaudio) |Pause receiving remote audio streams. |
|[resumeAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/14196#rtcroom-resumeallsubscribedstreamaudio) |Resume receiving remote audio streams. |
|[pauseAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/14196#rtcroom-pauseallsubscribedstreamvideo) |Pause receiving remote video streams. |
|[resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/14196#rtcroom-resumeallsubscribedstreamvideo) |Resume receiving remote video streams. |
|[sendUserMessage](https://docs.byteplus.com/en/docs/12/14196#rtcroom-sendusermessage) |Send a text message (P2P) to the specified user in the room. |
|[sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/14196#rtcroom-senduserbinarymessage) |Sends a binary message (P2P) to the specified user in the room. |
|[sendRoomMessage](https://docs.byteplus.com/en/docs/12/14196#rtcroom-sendroommessage) |Send broadcast messages to all other users in the room. |
|[sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/14196#rtcroom-sendroombinarymessage) |Send broadcast messages to all other users in the room. |
|[startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14196#rtcroom-startforwardstreamtorooms) |Start relaying media stream across rooms. |
|[updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14196#rtcroom-updateforwardstreamtorooms) |Update information of the rooms where you want to relay the media stream to. |
|[stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14196#rtcroom-stopforwardstreamtorooms) |Stop relaying media streams to all rooms. |
|[pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14196#rtcroom-pauseforwardstreamtoallrooms) |Pause relaying media streams to all rooms. |
|[resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14196#rtcroom-resumeforwardstreamtoallrooms) |Resume relaying media streams to all rooms. |
|[enableRangeAudio](https://docs.byteplus.com/en/docs/12/14196#rtcroom-enablerangeaudio) |Enable/disable the range audio function. |
|[updateReceiveRange](https://docs.byteplus.com/en/docs/12/14196#rtcroom-updatereceiverange) |Updates the audio receiving range for the local user. |
|[updateRangePosition](https://docs.byteplus.com/en/docs/12/14196#rtcroom-updaterangeposition) |Updates the coordinate of the local user's position in the rectangular coordinate system in the current room. |
|[setAttenuationModel](https://docs.byteplus.com/en/docs/12/14196#rtcroom-setattenuationmodel) |Set the volume roll\-off mode that a 3D sound has in an audio source when using the Range Audio feature. |
|[setNoAttenuationFlags](https://docs.byteplus.com/en/docs/12/14196#rtcroom-setnoattenuationflags) |Set the flags to mark the user groups, within which the users talk without attenuation.<br><br>In the RTC room, if the flags of the users intersects with each other, the users talk without attenuation.<br><br>For example, the user is a member of multiple teams, and teammates of the same team talk without attentuation. You can set the flag for each team, and includes the flags of the user's teams in the user's flags. |
|[enableSpatialAudio](https://docs.byteplus.com/en/docs/12/14196#rtcroom-enablespatialaudio) |Enable/disable spatial audio function. |
|[disableRemoteOrientation](https://docs.byteplus.com/en/docs/12/14196#rtcroom-disableremoteorientation) |Calling this API in each client to neglect the orientation of the remote speakers. From the local user's perspective, all the remote users will be facing him/her. |
|[setRemoteRoomAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/14196#rtcroom-setremoteroomaudioplaybackvolume) |Adjusts the audio playback volume from all the remote users in a room. |
|[setAudioSelectionConfig](https://docs.byteplus.com/en/docs/12/14196#rtcroom-setaudioselectionconfig) |Set the priority of the local audio stream to be published. |
|[setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/14196#rtcroom-setroomextrainfo) |Sets extra information about the room the local user joins. |
|[setStreamExtraInfo](https://docs.byteplus.com/en/docs/12/14196#rtcroom-setstreamextrainfo) |Sets extra information for the currently published stream. |
|[updateSelfPosition](https://docs.byteplus.com/en/docs/12/14196#rtcroom-updateselfposition) |Sets the coordinate and orientation of the local user as a listener in the rectangular coordinate system the local user built to achieve expected spatial audio effects. |
|[updateRemotePosition](https://docs.byteplus.com/en/docs/12/14196#rtcroom-updateremoteposition) |Sets the coordinate and orientation of the remote user as a speaker in the rectangular coordinate system of the local user. In this case, the local user hears from the remote user with the expected spatial audio effects. |
|[removeRemotePosition](https://docs.byteplus.com/en/docs/12/14196#rtcroom-removeremoteposition) |Disables all spatial audio effects set by calling [updateRemotePosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updateremoteposition) for a certain remote user. |
|[removeAllRemotePosition](https://docs.byteplus.com/en/docs/12/14196#rtcroom-removeallremoteposition) |Disables all spatial audio effects set by calling [updateRemotePosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updateremoteposition) for all remote users. |
|[processCallback](https://docs.byteplus.com/en/docs/12/14196#rtcroom-processcallback) | |

### getRoomId

Get room ID.

* **Signature**

   ```ts
   () => string
   ```

* **Return Value**

   Type: string

   Room ID.

### getCallId

Get Call ID。

This method needs to be called after joining a room.

* **Signature**

   ```ts
   () => string
   ```

* **Return Value**

   Type: string

   Call ID。

### setLiveMode

Sets the live\-streaming mode for the room.

* **Signature**

   ```ts
   (live_mode: RoomLiveMode) => number
   ```

* **Notes**

   Call this API after joining the room.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |live_mode |[RoomLiveMode](https://docs.byteplus.com/en/docs/12/docs-85535#roomlivemode) |Live\-streaming mode. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `!0`: Failure.

### destroy

Leave and destroy the room.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   Refer to [createRTCRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-creatertcroom) for more information on how to create a room.

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### joinRoom

Join the room.

* **Signature**

   ```ts
   (
     token: string,
     user_info: UserInfo,
     user_visibility: boolean,
     config?: RTCRoomConfig
   ) => number
   ```

* **Notes**

   * Billing starts once a user, including a server\-side bot, successfully joins an RTC room. Audio duration is charged even when there is only one user in the room.

   * In the same room with the same App ID, the user ID of each user must be unique. If two users have the same user ID, the user who entered the room later will kick the user who entered the room out of the room, and the user who entered the room will receive the `onRoomStateChanged` callback notification. For the error type. See kErrorCodeDuplicateLogin in [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-85534#errorcode).

   * Local users will receive `onRoomStateChanged` callback notification after calling this method to join the room successfully. If the local user is also a visible user, the remote user will receive an [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserjoined) callback notification when joining the room. For visibility settings, see [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setuservisibility).

   * By default, the user is visible in an RTC room. Joining fails when the number of users in an RTC room reaches the upper limit. To avoid this, call [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setuservisibility). to change the visibility of the audience users to `false` by considering the capacity for the invisible users is much larger than that for visible users. An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Room Capability](https://docs.byteplus.com/en/byteplus-rtc/docs/257549).

   * After the user successfully joins the room, the SDK may lose connection to the server in case of poor local network conditions. At this point, [onConnectionStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onconnectionstatechanged) callback will be triggered and the SDK will automatically retry until it successfully reconnects to the server. After a successful reconnection, you will receive a local `onRoomStateChanged` callback notification.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |token |string |Dynamic key for authenticating the logged\-in user.<br><br>You need to bring Token to enter the room. When testing, you can use the console to generate temporary tokens. The official launch requires the use of the key SDK to generate and issue tokens at your server level. See [Use Token to complete authentication](https://docs.byteplus.com/en/docs/12/docs-70121) for token validity and generation method.<br><br><br>* Apps with different App IDs cannot communicate with each other.<br><br>* Make sure that the App ID used to generate the Token is the same as the App ID used to create the engine, otherwise it will cause the join room to fail. |
   |user_info |[UserInfo](https://docs.byteplus.com/en/docs/12/docs-85535#userinfo) |User information. |
   |user_visibility |boolean |User visibility in the room. You are advised to set it to `false` when joining the room and call [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-setuservisibility) to change it to `true` when you need to publish media streams. |
   |config |[RTCRoomConfig](https://docs.byteplus.com/en/docs/12/docs-85535#rtcroomconfig) \| undefined |Optional room configuration that specifies the room mode and whether to automatically publish or subscribe to streams. |

* **Return Value**

   Type: number

   * 0: Success.

   * \-1: Room_id/user_info.uid contains invalid parameters.

   * \-2: Already in the room. After the interface call is successful, as long as the return value of 0 is received and [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-leaveroom) is not called successfully, this return value is triggered when the room entry interface is called again, regardless of whether the filled room ID and user ID are duplicated.

      The reason for the failure will be communicated via the `onRoomStateChanged` callback.

### leaveRoom

Leave RTC room.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * The user calls this method to leave the RTC room, end the call process, and release all call\-related resources.

   * It is an asynchronous operation, and the call returns without actually exiting the room. When actually exiting the room, you will receive [onLeaveRoom](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onleaveroom).

   * When visible users leave the room, others in the room will receive [onUserLeave](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserleave).

   * If the engine is destroyed immediately after this method is called, you will not receive [onLeaveRoom](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onleaveroom).

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setUserVisibility

Set the visibility of the user in the room. The local user is visible to others by default before calling this API.

* **Signature**

   ```ts
   (enable: Boolean) => number
   ```

* **Notes**

   * You can call this API whether the user is in a room or not.

   * An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Room Capacity](https://docs.byteplus.com/en/byteplus-rtc/docs/257549).

   * When you call this API, the other users in the room will be informed via the related callback:

   * Switch from `false` to `true`: [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserjoined).

   * Switch from `true` to `false`: [onUserLeave](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserleave).

   * The invisible user will receive the warning code, `kWarningCodePublishStreamForbiden`, when trying to publish media streams.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |enable |Boolean |Visibility of the user in the room:<br><br><br>* true: The user can publish media streams. And the other users in the room get informed of the behaviors of the user, such as Joining room, starting video capture, and Leaving room.<br><br>* false: The user cannot publish media streams. And the other users in the room do not get informed of the behaviors of the user, such as joining, starting video capture, or leaving. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setMultiDeviceAVSync

Synchronizes published audio and video.

* **Signature**

   ```ts
   (audio_user_id: string) => number
   ```

* **Notes**

   * When the same user simultaneously uses separate devices to capture and publish audio and video, there is a possibility that the streams are out of sync due to the network disparity. In this case, you can call this API on the video publisher side and the SDK will automatically line the video stream up according to the timestamp of the audio stream, ensuring that the audio the receiver hears corresponds to the video the receiver watches.

   * You can call this API anytime before or after entering the room.

   * The source user IDs of the audio and video stream to be synchronized must be in the same RTC room.

   * When the A/V synchronization state changes, you will receive [onAVSyncStateChange](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onavsyncstatechange).

   * More than one pair of audio and video can be synchronized simultaneously in the same RTC room, but you should note that one single audio source cannot be synchronized with multiple video sources at the same time.

   * If you want to change the audio source, call this API again with a new `audio_user_id`. If you want to change the video source, you need to stop the current synchronization first, then call this API on the new video publisher side.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |audio_user_id |string |The ID of audio publisher. You can stop the current A/V synchronization by setting this parameter to null. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### updateToken

Update Token. A Token contains the privilege of joining a room, publishing streams, and subscribing to streams. Each privilege has an expiration time. A callback will be triggered 30s before expiration, informing the user to update the Token. In this case, you need to get a new Token and update the Token with this API to ensure the normal call.

* **Signature**

   ```ts
   (token: string) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |token |string |Valid token.<br><br>If the Token is invalid, a callback will be triggered with the [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-85534) `-1010` indicating that the updated Token is invalid. |

* **Return Value**

   Type: number

### publishStreamVideo

Start or stop publishing video streams captured by camera in the current room.

* **Signature**

   ```ts
   (publish: Boolean) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |publish |Boolean |Whether to publish the media stream. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85535#returnstatus) for more details.

### publishStreamAudio

Start or stop publishing media streams captured by the local microphone in the current room.

* **Signature**

   ```ts
   (publish: Boolean) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |publish |Boolean |Whether to publish the media stream. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85535#returnstatus) for more details.

### subscribeStreamVideo

Subscribes to specific remote media streams captured by the local camera. Or update the subscribe options of the subscribed user.

* **Signature**

   ```ts
   (
     stream_id: string,
     subscribe: Boolean
   ) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |The ID of the remote stream to subscribe to. |
   |subscribe |Boolean |Whether to subscribe to the stream. |

* **Return Value**

   Type: number

   API call result:

   * 0: Success.

   * <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85535#returnstatus) for specific reasons.

### subscribeStreamAudio

Subscribes to specific remote media streams captured by the local microphone. Or update the subscribe options of the subscribed user.

* **Signature**

   ```ts
   (
     stream_id: string,
     subscribe: Boolean
   ) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |The ID of the remote stream to subscribe to. |
   |subscribe |Boolean |Whether to subscribe to the audio stream. |

* **Return Value**

   Type: number

   API call result:

   * 0: Success.

   * <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85535#returnstatus) for specific reasons.

### setRemoteVideoConfig

Sets your expected configuration of the remote video stream that you want to subscribe to or have subscribed to.

* **Signature**

   ```ts
   (
     stream_id: string,
     remote_video_config: RemoteVideoConfig
   ) => number
   ```

* **Notes**

   * This API only works after the publisher calls [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setlocalsimulcastmode) to enable publishing multiple video streams, in which case the subscriber will receive the stream from the publisher that is closest to the set configuration; otherwise the subscriber will only receive one video stream with a resolution of 640px × 360px and a frame rate of 15fps.

   * If you don't call this API after the publisher enables the function of publishing multiple streams, you will receive by default the video stream with the largest resolution set by the publisher.

   * You should call this API in the room. If you want to call it before entering the room, you should set the `remote_video_config` in the `room_config` when calling [joinRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-joinroom).

   * SDK will automatically select the stream to be published or subscribed based on the settings of both sides.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |ID of the remote video stream for which you want to configure subscription parameters. |
   |remote_video_config |[RemoteVideoConfig](https://docs.byteplus.com/en/docs/12/docs-85535#remotevideoconfig) |The parameters you expect to configure for the remote video stream. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### subscribeAllStreamsAudio

Subscribes to all remote audio streams captured by microphone.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * In the Conference Mode, if the number of subscribed audio streams exceeds the limit, we recommend you call [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-subscribestreamaudio) to subscribe to each target stream individually.

   * After calling this API, you will be informed of the calling result with [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onaudiosubscribestatechanged).

   * Once the local user subscribes to a remote audio stream, the subscription will sustain until the local user leaves the room or unsubscribes by calling [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-subscribestreamaudio) with `subscribe` set to `false`.

   * Any other exceptions will be included in [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onaudiosubscribestatechanged), see `SubscribeStateChangeReason` for the reasons.

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1`: Failure.

### unsubscribeAllStreamsAudio

Unsubscribes from all remote audio streams captured by microphone.

* **Signature**

   ```ts
   () => number
   ```

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1`: Failure.

### subscribeAllStreamsVideo

Subscribes to all remote video streams captured by camera.

* **Signature**

   ```ts
   () => number
   ```

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1`: Failure.

### unsubscribeAllStreamsVideo

Unsubscribes from all remote video streams captured by camera.

* **Signature**

   ```ts
   () => number
   ```

* **Return Value**

   Type: number

   * `0`: Success.

   * `-1`: Failure.

### pauseAllSubscribedStreamAudio

Pause receiving remote audio streams.

* **Signature**

   ```ts
   () => number
   ```

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### resumeAllSubscribedStreamAudio

Resume receiving remote audio streams.

* **Signature**

   ```ts
   () => number
   ```

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### pauseAllSubscribedStreamVideo

Pause receiving remote video streams.

* **Signature**

   ```ts
   () => number
   ```

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### resumeAllSubscribedStreamVideo

Resume receiving remote video streams.

* **Signature**

   ```ts
   () => number
   ```

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### sendUserMessage

Send a text message (P2P) to the specified user in the room.

* **Signature**

   ```ts
   (
     uid: string,
     message: string,
     config: MessageConfig
   ) => number
   ```

* **Notes**

   * Before sending an in\-room text message, you must call [joinRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-joinroom) to join the room.

   * After calling this function, you will receive an [onUserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onusermessagesendresult) callback to notify the message sender that the sending was successful or failed;

   * If the text message is sent successfully, the user specified by uid will receive [onUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onusermessagereceived) callback.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |uid |string |User ID of the message receiver. |
   |message |string |Text message content. By default, the maximum size of a single message is 1 KB. To send larger messages, [enable the advanced RTS feature in the RTC console](https://console.volcengine.com/rtc/cloudRTC?tab=RTSMode). The maximum size is 64 KB. If you enable the feature while the SDK is running, recreate the engine for the configuration to take effect. |
   |config |[MessageConfig](https://docs.byteplus.com/en/docs/12/docs-85535#messageconfig) |Message type. |

* **Return Value**

   Type: number

   * \> 0: Success. The return value is the serial number of the message, starting from 1.

   * < 0: Failure.

### sendUserBinaryMessage

Sends a binary message (P2P) to the specified user in the room.

* **Signature**

   ```ts
   (
     uid: string,
     length: number,
     message: Uint8Array,
     config: MessageConfig
   ) => number
   ```

* **Notes**

   * Before sending in\-room binary messages, you must call [joinRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-joinroom) to join the room.

   * After calling this function, you will receive an [onUserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onusermessagesendresult) callback to notify the sender of the success or failure of the message;

   * If the binary message is sent successfully, the user specified by uid will receive the [onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserbinarymessagereceived) callback.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |uid |string |User ID of the message receiver. |
   |length |number |Length of the binary message in bytes. |
   |message |Uint8Array |Binary message content. By default, the maximum size of a single message is 1 KB. To send larger messages, [enable the advanced RTS feature in the RTC console](https://console.volcengine.com/rtc/cloudRTC?tab=RTSMode). The maximum size is 64 KB. If you enable the feature while the SDK is running, recreate the engine for the configuration to take effect. |
   |config |[MessageConfig](https://docs.byteplus.com/en/docs/12/docs-85535#messageconfig) |Message type. |

* **Return Value**

   Type: number

   * \> 0: Success. Serial number of the message, starting from 1.

   * < 0: Failure.

### sendRoomMessage

Send broadcast messages to all other users in the room.

* **Signature**

   ```ts
   (message: string) => number
   ```

* **Notes**

   * Before sending an in\-room text broadcast message, you must call [joinRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-joinroom) to join the room.

   * After calling this function, you get an [onRoomMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onroommessagesendresult) callback.

   * Other users in the same room receive an [onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onroommessagereceived) callback.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |message |string |Text broadcast message content. By default, the maximum size of a single message is 1 KB. To send larger messages, [enable the advanced RTS feature in the RTC console](https://console.volcengine.com/rtc/cloudRTC?tab=RTSMode). The maximum size is 64 KB. If you enable the feature while the SDK is running, recreate the engine for the configuration to take effect. |

* **Return Value**

   Type: number

   * \> 0: Success. The return value is the serial number of the message, starting from 1.

   * < 0: Failure.

### sendRoomBinaryMessage

Send broadcast messages to all other users in the room.

* **Signature**

   ```ts
   (
     size: number,
     message: Uint8Array
   ) => number
   ```

* **Notes**

   * Before sending in\-room binary messages, you must call [joinRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-joinroom) to join the room.

   * After calling this function, you get an [onRoomMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onroommessagesendresult) callback.

   * Other users in the same room receive an [onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onroombinarymessagereceived) callback.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |size |number |Length of the binary message in bytes. |
   |message |Uint8Array |Binary broadcast message content. By default, the maximum size of a single message is 1 KB. To send larger messages, [enable the advanced RTS feature in the RTC console](https://console.volcengine.com/rtc/cloudRTC?tab=RTSMode). The maximum size is 64 KB. If you enable the feature while the SDK is running, recreate the engine for the configuration to take effect. |

* **Return Value**

   Type: number

   * \> 0: Success. The return value is the serial number of the message, starting from 1.

   * < 0: Failure.

### startForwardStreamToRooms

Start relaying media stream across rooms.

* **Signature**

   ```ts
   (configuration: ForwardStreamConfiguration) => number
   ```

* **Notes**

   * After calling [joinRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-joinroom), you can call this method to publish the media stream to multiple rooms that applies to scenarios such as an online talent contest and so on.

   * Calling this method will trigger [onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onforwardstreamstatechanged).

   * After calling this method, listen the events from each room during the relaying by registering [onForwardStreamEvent](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onforwardstreamevent).

   * Once the relaying begins, the other users in the room will receive callback of [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserjoined) and [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserpublishstreamvideo)/[onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserpublishstreamaudio).

   * Call [updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updateforwardstreamtorooms) to add or remove the target room(s) after calling this method.

   * Call [stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-stopforwardstreamtorooms) to stop relaying to all rooms after calling this method.

   * Call [pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-pauseforwardstreamtoallrooms) to pause relaying to all rooms after calling this method.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |configuration |[ForwardStreamConfiguration](https://docs.byteplus.com/en/docs/12/docs-85535#forwardstreamconfiguration) |Information of the rooms where you want to relay the media stream to. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### updateForwardStreamToRooms

Update information of the rooms where you want to relay the media stream to.

* **Signature**

   ```ts
   (configuration: ForwardStreamConfiguration) => number
   ```

* **Notes**

   * Update information of the rooms where you want to relay the media stream to after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-startforwardstreamtorooms).

   * Adding and removing rooms by calling this method will trigger [onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onforwardstreamstatechanged) on the local.

   * Users in the room which is added by calling this method will receive [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserjoined) and [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserpublishstreamvideo)/[onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserpublishstreamaudio).

   * Users in the room which is removed by calling this method will receive [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserpublishstreamvideo)/[onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserpublishstreamaudio) with `is_publish` set to `false`, and then [onUserLeave](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserleave).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |configuration |[ForwardStreamConfiguration](https://docs.byteplus.com/en/docs/12/docs-85535#forwardstreamconfiguration) |Information of the rooms where you want to relay the media stream to. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### stopForwardStreamToRooms

Stop relaying media streams to all rooms.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * Call this method to stop relaying media stream to all rooms after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-startforwardstreamtorooms).

   * Call this method will trigger [onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onforwardstreamstatechanged).

   * The users in the target rooms will receive [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserpublishstreamvideo)/[onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserpublishstreamaudio) with `is_publish` set to `false`, and then [onUserLeave](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserleave) when you stop relaying.

   * To stop relaying media stream to specific rooms, call [updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updateforwardstreamtorooms) instead.

   * To resume the relaying in a short time, call [pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-pauseforwardstreamtoallrooms) instead and then call resumeForwardStreamToAllRooms(#resumeforwardstreamtoallrooms) to resume after that.

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### pauseForwardStreamToAllRooms

Pause relaying media streams to all rooms.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * Call this method to pause relaying media stream to all rooms after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-startforwardstreamtorooms).

   * After that, call resumeForwardStreamToAllRooms(#resumeforwardstreamtoallrooms) to resume.

   * The users in the target rooms will receive [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserpublishstreamvideo)/[onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserpublishstreamaudio) with `is_publish` set to `false`, and then [onUserLeave](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserleave) when you pause relaying.

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### resumeForwardStreamToAllRooms

Resume relaying media streams to all rooms.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * Call this method to resume relaying to all rooms from the pause by calling [pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-pauseforwardstreamtoallrooms).

   * The other users in the room will receive callback of [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserjoined) and [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserpublishstreamvideo)/[onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onuserpublishstreamaudio) when you resume relaying.

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### enableRangeAudio

Enable/disable the range audio function.

* **Signature**

   ```ts
   (enable: boolean) => number
   ```

* **Notes**

   * Range audio means that within a certain range in a same RTC room, the audio volume of the remote user received by the local user will be amplified/attenuated as the remote user moves closer/away. The audio coming from out of the range cannot be heard. See [updateReceiveRange](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updatereceiverange) to set audio receiving range.

   * You can call this API anytime before or after entering a room. To ensure a smooth switch to the range audio mode after entering the room, you need to call [updateRangePosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updaterangeposition) before this API to set your own position coordinates, and then enable the range audio function.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |enable |boolean |Whether to enable audio range funcion：<br><br><br>* true: Enable<br><br>* false: Disable（Defaulting setting）. |

* **Return Value**

   Type: number

   * 0: Success.

   * (Default) < 0: Failure.

### updateReceiveRange

Updates the audio receiving range for the local user.

* **Signature**

   ```ts
   (range: ReceiveRange) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |range |[ReceiveRange](https://docs.byteplus.com/en/docs/12/docs-85535#receiverange) |Audio receiving range. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `!0`: Failure.

### updateRangePosition

Updates the coordinate of the local user's position in the rectangular coordinate system in the current room.

* **Signature**

   ```ts
   (pos: Position) => number
   ```

* **Notes**

   After calling this API, you should call [enableRangeAudio](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-enablerangeaudio) to enable range audio function to actually enjoy the range audio effect.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |pos |[Position](https://docs.byteplus.com/en/docs/12/docs-85535#position) |X, Y, Z coordinates. It defaults to [0, 0, 0]. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setAttenuationModel

Set the volume roll\-off mode that a 3D sound has in an audio source when using the Range Audio feature.

* **Signature**

   ```ts
   (
     type: AttenuationType,
     coefficient: number
   ) => number
   ```

* **Notes**

   Call [updateReceiveRange](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updatereceiverange) to set the range outside which the volume of the sound does not attenuate.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |type |[AttenuationType](https://docs.byteplus.com/en/docs/12/docs-85535#attenuationtype) |Volume roll\-off mode. It is linear roll\-off mode by default. |
   |coefficient |number |Coefficient for the exponential roll\-off mode. The default value is 1. It ranges [0.1,100]. We recommended to set it to `50`. The volume roll\-off speed gets faster as this value increases. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure because of calling this API before the user has joined a room or before enabling the Range Audio feature by calling [enableRangeAudio](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-enablerangeaudio).

### setNoAttenuationFlags

Set the flags to mark the user groups, within which the users talk without attenuation.

In the RTC room, if the flags of the users intersects with each other, the users talk without attenuation.

For example, the user is a member of multiple teams, and teammates of the same team talks without attentuation. You can set the flag for each team, and includes the flags of the user's teams in the user's flags.

* **Signature**

   ```ts
   (flags?: string[]) => any
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |flags |string[] |Array of flags. |

### enableSpatialAudio

Enable/disable spatial audio function.

* **Signature**

   ```ts
   (enable: boolean) => number
   ```

* **Notes**

   You need to call [updateSelfPosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updateselfposition) as well to really enjoy the spatial audio effect.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |enable |boolean |Whether to enable spatial audio function:<br><br><br>* true：Enable<br><br>* false：Disable(Default setting). |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### disableRemoteOrientation

Calling this API in each client to neglect the orientation of the remote speakers. From the local user's perspective, all the remote users will be facing him/her.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * Once the orientation is disabled by calling this API, the orientation settings in [updateSelfPosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updateselfposition) will not notify remote users. However, as a listener, the local user can still experience the sound effect varies with the change of one's orientation.

   * You can call this API before or after the local user joins the room.

   * Once the orientation is disabled by calling this API, you cannot enable it again within the lifetime of the `SpatialAudio` instance.

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setRemoteRoomAudioPlaybackVolume

Adjusts the audio playback volume from all the remote users in a room.

* **Signature**

   ```ts
   (volume: number) => number
   ```

* **Notes**

   Suppose a remote user A is always within the range of the target user whose playback volume will be adjusted,:

   * If you use both this method and [setRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setremoteaudioplaybackvolume), the volume that the local user hears from user A is the volume set by the method called later.

   * If you use both this method and [setPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setplaybackvolume), the volume that the local user hears from user A is the overlay of both settings.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |volume |number |Ratio(%) of playback volume to original volume, in the range [0, 400], with overflow protection.<br><br>To ensure the audio quality, we recommend setting the volume to `100`.<br><br><br>* 0: mute<br><br>* 100: original volume. Default value.<br><br>* 400: Up to 4 times the original volume (with overflow protection). |

* **Return Value**

   Type: number

### setAudioSelectionConfig

Set the priority of the local audio stream to be published.

* **Signature**

   ```ts
   (audio_selection_priority: AudioSelectionPriority) => number
   ```

* **Notes**

   * You must enable Audio Selection in the RTC console before using this API. You can call this API whether the user has joined a room. Refer to [Audio Selection](https://docs.byteplus.com/byteplus-rtc/docs/113547).

   * The setting is independent in each room that the user joins.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |audio_selection_priority |[AudioSelectionPriority](https://docs.byteplus.com/en/docs/12/docs-85535#audioselectionpriority) |The priority of the local audio stream which defaults to be subscribable only up to the result of the Audio Selection. |

* **Return Value**

   Type: number

### setRoomExtraInfo

Sets extra information about the room the local user joins.

* **Signature**

   ```ts
   (
     key: string,
     value: string
   ) => any
   ```

* **Notes**

   * Call [joinRoom](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-joinroom) first before you call this API to set extra information.

   * After the extra information is successfully set, other users in the same room will receive the information through [onRoomExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onroomextrainfoupdate) callback.

   * Users who join the room later will be notified of all extra information in the room set prior to entering.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |key |string |Key of the extra information, less than 10 bytes in length.<br><br>A maximum of 5 keys can exist in the same room, beyond which the first key will be replaced. |
   |value |string |Content of the extra information, less than 128 bytes in length. |

* **Return Value**

   API call result:

   * 0: Success with a taskId returned.

   * <0: Failure. You can find the reason via [onSetRoomExtraInfoResult](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onsetroomextrainforesult) callback which informs you of the result of the setting after calling this API.

### setStreamExtraInfo

Sets extra information for the currently published stream.

* **Signature**

   ```ts
   (extra_info: string) => number
   ```

* **Notes**

   * You can use this API to set extra information for the currently published stream. Stream extra information is additional information identifying the stream ID. Unlike the stream ID, which cannot be modified during publishing, stream extra information can be updated while publishing the corresponding stream ID. You can use stream extra information to synchronize mutable content related to the stream ID.

   * This method can be called before or after joining the room.

   * Other users in the same room will receive the notification through [onRoomStreamExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/docs-85533#rtcroomcallback-onroomstreamextrainfoupdate).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |extra_info |string |Stream extra information. The string length must not exceed 1024. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `!0`: Failure.

### updateSelfPosition

Sets the coordinate and orientation of the local user as a listener in the rectangular coordinate system the local user built to achieve expected spatial audio effects.

* **Signature**

   ```ts
   (position_info: PositionInfo) => number
   ```

* **Notes**

   Call this API after joining the room. Before calling this API, you should call [enableSpatialAudio](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-enablespatialaudio) first to enable the spatial audio function.

   The settings made locally will not influence other users' spatial audio experience.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |position_info |[PositionInfo](https://docs.byteplus.com/en/docs/12/docs-85535#positioninfo) |Information on the local user's position. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `<0`: Failure.

   * `-2`: Failure. The reason is that any two of the 3D coordinate vectors of your position are not perpendicular to each other.

### updateRemotePosition

Sets the coordinate and orientation of the remote user as a speaker in the rectangular coordinate system of the local user. In this case, the local user hears from the remote user with the expected spatial audio effects.

* **Signature**

   ```ts
   (
     uid: string,
     position_info: PositionInfo
   ) => number
   ```

* **Notes**

   Call this API after creating the room.

   The settings made locally will not influence other users' spatial audio experience.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |uid |string |User ID. |
   |position_info |[PositionInfo](https://docs.byteplus.com/en/docs/12/docs-85535#positioninfo) |Information on the remote user's position. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `<0`: Failure.

   * `-2`: Failure. The reason is that any two of the 3D coordinate vectors of the position of the remote user are not perpendicular to each other.

### removeRemotePosition

Disables all spatial audio effects set by calling [updateRemotePosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updateremoteposition) for a certain remote user.

* **Signature**

   ```ts
   (uid: string) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |uid |string |User ID of the remote user. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `<0`: Failure.

### removeAllRemotePosition

Disables all spatial audio effects set by calling [updateRemotePosition](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-updateremoteposition) for all remote users.

* **Signature**

   ```ts
   () => number
   ```

* **Return Value**

   Type: number

   * `0`: Success.

   * `<0`: Failure.

### processCallback

* **Signature**

   ```ts
   (event: EventType) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |event |[EventType](https://docs.byteplus.com/en/docs/12/docs-85535#eventtype) | |

## RTCAudioEffectPlayer

Type: `class`

* **API**

|Method |Description |
|---|---|
|[start](https://docs.byteplus.com/en/docs/12/14196#rtcaudioeffectplayer-start) |Starts to play the audio effect file.<br><br>This API can be called multiple times with different IDs and filepaths for multiple effects at the same time. |
|[stop](https://docs.byteplus.com/en/docs/12/14196#rtcaudioeffectplayer-stop) |Stops the playback of audio effect files. |
|[stopAll](https://docs.byteplus.com/en/docs/12/14196#rtcaudioeffectplayer-stopall) |Stops playback of all audio effect files. |
|[preload](https://docs.byteplus.com/en/docs/12/14196#rtcaudioeffectplayer-preload) |Preloads specified music files into memory to avoid repeated loading when playing the same file frequently and reduce CPU usage. |
|[unload](https://docs.byteplus.com/en/docs/12/14196#rtcaudioeffectplayer-unload) |Unloads the specified audio effect file. |
|[unloadAll](https://docs.byteplus.com/en/docs/12/14196#rtcaudioeffectplayer-unloadall) |Unloads all audio effect files. |
|[pause](https://docs.byteplus.com/en/docs/12/14196#rtcaudioeffectplayer-pause) |Pauses the playback of audio effect files. |
|[pauseAll](https://docs.byteplus.com/en/docs/12/14196#rtcaudioeffectplayer-pauseall) |Pauses the Playback of all audio effect files. |
|[resume](https://docs.byteplus.com/en/docs/12/14196#rtcaudioeffectplayer-resume) |Resumes the playback of audio effect files. |
|[resumeAll](https://docs.byteplus.com/en/docs/12/14196#rtcaudioeffectplayer-resumeall) |Resumes the playback of all audio effect files. |
|[setPosition](https://docs.byteplus.com/en/docs/12/14196#rtcaudioeffectplayer-setposition) |Sets the start position of the audio effect file. |
|[getPosition](https://docs.byteplus.com/en/docs/12/14196#rtcaudioeffectplayer-getposition) |Gets the current position of audio effect file playback. |
|[setVolume](https://docs.byteplus.com/en/docs/12/14196#rtcaudioeffectplayer-setvolume) |Adjusts the volume level of a specified audio effect, including audio effect file and PCM effect. |
|[setVolumeAll](https://docs.byteplus.com/en/docs/12/14196#rtcaudioeffectplayer-setvolumeall) |Sets the volume of all audio effect, including audio effect files and PCM effects. |
|[getVolume](https://docs.byteplus.com/en/docs/12/14196#rtcaudioeffectplayer-getvolume) |Gets the current volume. |
|[getDuration](https://docs.byteplus.com/en/docs/12/14196#rtcaudioeffectplayer-getduration) |Get the duration of the audio effect file. |
|[setEventHandler](https://docs.byteplus.com/en/docs/12/14196#rtcaudioeffectplayer-seteventhandler) |Set the event handler. |
|[processCallback](https://docs.byteplus.com/en/docs/12/14196#rtcaudioeffectplayer-processcallback) | |

### start

Starts to play the audio effect file.

This API can be called multiple times with different IDs and filepaths for multiple effects at the same time.

* **Signature**

   ```ts
   (
     effect_id: number,
     file_path: string,
     config: AudioEffectPlayerConfig
   ) => number
   ```

* **Notes**

   * If the file has been loaded into memory via [preload](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-preload), make sure that the ID here is the same as the ID set by [preload](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-preload).

   * After starting to play an audio effect file, you can call the [stop](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-stop) API to stop playing the audio effect file.

* **Parameters**

   |Audio effect file paths.<br><br>URL of online file, URI of local file, or full path to the local file are supported. For URL of online file, only the https protocol is supported.<br><br>Recommended sample rate for audio effect files: 8KHz、16KHz、22.05KHz、44.1KHz、48KHz.<br><br>Local audio effect file formats supported by different platforms:<br><br> <br><br> <br><br> <br><br> <br><br>Online audio effect file formats supported by different platforms.<br><br> <br><br> <br><br> | | |
   |---|---|---|
   |config |[AudioEffectPlayerConfig](https://docs.byteplus.com/en/docs/12/docs-85535#audioeffectplayerconfig) |Effect config. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### stop

Stops the playback of audio effect files.

* **Signature**

   ```ts
   (effect_id: number) => number
   ```

* **Notes**

   * After calling the [start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-start) API to start playing the audio effect file, you can call this API to stop playing the audio effect file.

   * After calling this API to stop playing an audio effect file, the audio effect file will be unloaded automatically.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |effect_id |number |Audio effect ID. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### stopAll

Stops playback of all audio effect files.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * After calling [start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-start) to start playing audio effect files, you can call this API to stop playing all audio effect files.

   * After calling this API to stop playing all audio effect files, the audio effect files will be unloaded automatically.

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### preload

Preloads specified music files into memory to avoid repeated loading when playing the same file frequently and reduce CPU usage.

* **Signature**

   ```ts
   (
     effect_id: number,
     file_path: string
   ) => number
   ```

* **Notes**

   * This API just preloads the specified audio effect file, and only calls the [start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-start) API to start playing the specified audio effect file.

   * The specified audio effect file preloaded by calling this API can be unloaded by [unload](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-unload).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |effect_id |number |Audio effect ID。Used for identifying the audio effect. Please ensure that the audio effect ID is unique.<br><br>If this API is called repeatedly with the same ID, the later one will overwrite the previous one.<br><br>If you call [start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-start) first and then call this API with the same ID, the SDK will stop the previous effect and then load the next one, and you will receive [onAudioEffectPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcaudioeffectplayercallback-onaudioeffectplayerstatechanged).<br><br>After calling this API to preload A.mp3, if you need to call [start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-start) to play B.mp3 with the same ID, please call [unload](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-unload) to unload A.mp3 first, otherwise SDK will report an error AUDIO_MIXING_ERROR_LOAD_CONFLICT. |
   |file_path |string |The filepath of effect file. URI of local file, or full path to local file.<br><br>The length of the pre\-loaded file must not exceed 20s.<br><br>Audio effect file formats supported are the same as [start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-start). |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### unload

Unloads the specified audio effect file.

* **Signature**

   ```ts
   (effect_id: number) => number
   ```

* **Notes**

   Call this API after [start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-start) or [preload](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-preload).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |effect_id |number |Audio effect ID. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### unloadAll

Unloads all audio effect files.

* **Signature**

   ```ts
   () => number
   ```

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### pause

Pauses the playback of audio effect files.

* **Signature**

   ```ts
   (effect_id: number) => number
   ```

* **Notes**

   * After calling the [start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-start) API to start playing the audio effect file, you can pause the audio effect file by calling this API.

   * After calling this API to pause the audio effect file, you can call the [resume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-resume) API to resume playback.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |effect_id |number |Audio effect ID. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### pauseAll

Pauses the Playback of all audio effect files.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * After calling the [start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-start) API to start playing audio effect files, you can pause playing all audio effect files by calling this API.

   * After calling this API to pause the playback of all audio effect files, you can call the [resumeAll](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-resumeall) API to resume all playback.

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### resume

Resumes the playback of audio effect files.

* **Signature**

   ```ts
   (effect_id: number) => number
   ```

* **Notes**

   After calling the [pause](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-pause) API to pause the audio effect file, you can resume playback by calling this API.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |effect_id |number |Audio effect ID. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### resumeAll

Resumes the playback of all audio effect files.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   After calling the [pauseAll](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-pauseall) API to pause all the audio effect files being played, you can resume playback by calling this API.

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setPosition

Sets the start position of the audio effect file.

* **Signature**

   ```ts
   (
     effect_id: number,
     pos: number
   ) => number
   ```

* **Notes**

   * When playing online files, calling this API may cause a delay in playback.

   * Call this API after [start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-start).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |effect_id |number |Audio effect ID. |
   |pos |number |The starting playback position of the audio effect file in milliseconds.<br><br>You can get the total duration of the audio effect file by calling [getDuration](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-getduration), the value of pos should be less than the total duration of the audio effect file. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### getPosition

Gets the current position of audio effect file playback.

* **Signature**

   ```ts
   (effect_id: number) => number
   ```

* **Notes**

   * When playing online files, calling this API may cause a delay in playback.

   * Call this API after [start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-start).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |effect_id |number |Audio effect ID. |

* **Return Value**

   Type: number

   * \>0: Success, the current progress of audio effect file playback in milliseconds.

   * < 0: Failure.

### setVolume

Adjusts the volume level of a specified audio effect, including audio effect file and PCM effect.

* **Signature**

   ```ts
   (
     effect_id: number,
     volume: number
   ) => number
   ```

* **Notes**

   Call this API after [start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-start).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |effect_id |number |Audio effect ID. |
   |volume |number |The ratio of the volume to the original volume in % with overflow protection. The range is `[0, 400]` and the recommended range is `[0, 100]`. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setVolumeAll

Sets the volume of all audio effect, including audio effect files and PCM effects.

* **Signature**

   ```ts
   (volume: number) => number
   ```

* **Notes**

   This API has a lower priority than [setVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-setvolume), i.e. the volume of the audio effect set by [setVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-setvolume) is not affected by this API.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |volume |number |The ratio of the volume to the original volume in % with overflow protection. The range is `[0, 400]` and the recommended range is `[0, 100]`. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### getVolume

Gets the current volume.

* **Signature**

   ```ts
   (effect_id: number) => number
   ```

* **Notes**

   Call this API after [start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-start).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |effect_id |number |Audio effect ID. |

* **Return Value**

   Type: number

   * \>0: Success, the current volume value.

   * < 0: Failed.

### getDuration

Get the duration of the audio effect file.

* **Signature**

   ```ts
   (effect_id: number) => number
   ```

* **Notes**

   Call this API after [start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer-start).

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |effect_id |number |Audio effect ID. |

* **Return Value**

   Type: number

   * \>0: Success, the duration of the audio effect file in milliseconds.

   * < 0: failed.

### setEventHandler

Set the event handler.

* **Signature**

   ```ts
   () => number
   ```

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### processCallback

* **Signature**

   ```ts
   (event: EventType) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |event |[EventType](https://docs.byteplus.com/en/docs/12/docs-85535#eventtype) | |

## RTCMediaPlayer

Type: `class`

* **API**

|Method |Description |
|---|---|
|[open](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-open) |Open the audio file.<br><br>You can only open one audio file with one player instance at the same time. For multiple audio files at the same time, create multiple player instances. |
|[start](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-start) |Start playing the audio. Call this API when you call [open](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-open) and set `AutoPlay=false`. |
|[stop](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-stop) |After calling [open](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-open) or [start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-start) to start audio mixing, call this method to stop audio mixing. |
|[pause](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-pause) |After calling [open](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-open), or [start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-start) to start audio mixing, call this API to pause audio mixing. |
|[resume](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-resume) |After calling [pause](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-pause) to pause audio mixing, call this API to resume audio mixing. |
|[setVolume](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-setvolume) |Adjusts the volume of the specified audio mixing, including media file mixing and PCM mixing. |
|[getVolume](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-getvolume) |Gets the current volume. |
|[getTotalDuration](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-gettotalduration) |Gets the duration of the media file. |
|[getPlaybackDuration](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-getplaybackduration) |Gets the actual playback duration of the mixed media file, in milliseconds. |
|[getPosition](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-getposition) |Gets the playback progress of the media file. |
|[setPosition](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-setposition) |Sets the starting playback position of the media file. |
|[setAudioPitch](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-setaudiopitch) |Set the pitch of the local audio file mixing. Usually used in karaoke scenes. |
|[setAudioDualMonoMode](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-setaudiodualmonomode) |Sets the channel mode of the mixing of the media file. |
|[getAudioTrackCount](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-getaudiotrackcount) |Gets the track count of the current media file. |
|[selectAudioTrack](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-selectaudiotrack) |Specifies the playback track of the current media file. |
|[setPlaybackSpeed](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-setplaybackspeed) |Sets the playback speed of the audio file. |
|[setProgressInterval](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-setprogressinterval) |Set the interval of the periodic callback [onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-85533#rtcmediaplayercallback-onmediaplayerplayingprogress) during audio mixing. |
|[setLoudness](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-setloudness) |To call [enableVocalInstrumentBalance](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enablevocalinstrumentbalance) to adjust the volume of the mixed media file or the PCM audio data, you must pass in its original loudness through this API. |
|[setEventHandler](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-seteventhandler) |Register an observer to receive related callbacks when the local media file is mixing. |
|[openWithCustomSource](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-openwithcustomsource) |Starts mixing PCM audio data from a custom source. |
|[pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-pushexternalaudioframe) |Pushes PCM audio frames for mixing. |
|[processCallback](https://docs.byteplus.com/en/docs/12/14196#rtcmediaplayer-processcallback) | |

### open

Open the audio file.

You can only open one audio file with one player instance at the same time. For multiple audio files at the same time, create multiple player instances.

* **Signature**

   ```ts
   (
     file_path: string,
     config: MediaPlayerConfig
   ) => number
   ```

* **Parameters**

   |Audio file paths.<br><br>URL of online file, URI of local file, or full path to local file. For URL of online file, only the https protocol is supported.<br><br>Recommended sample rate for audio effect files: 8KHz、16KHz、22.05KHz、44.1KHz、48KHz.<br><br>Local audio effect file formats supported by different platforms:<br><br> <br><br> <br><br> <br><br> <br><br>Online audio effect file formats supported by different platforms.<br><br> <br><br> <br><br> | | |
   |---|---|---|
   |config |[MediaPlayerConfig](https://docs.byteplus.com/en/docs/12/docs-85535#mediaplayerconfig) |Media player configurations. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### start

Start playing the audio. Call this API when you call [open](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-open) and set `AutoPlay=false`.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   After calling this API, call [stop](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-stop) to stop playing the audio file.

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### stop

After calling [open](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-open) or [start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-start) to start audio mixing, call this method to stop audio mixing.

* **Signature**

   ```ts
   () => number
   ```

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### pause

After calling [open](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-open), or [start](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-start) to start audio mixing, call this API to pause audio mixing.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   After calling this API to pause audio mixing, call [resume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-resume) to resume audio mixing.

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### resume

After calling [pause](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-pause) to pause audio mixing, call this API to resume audio mixing.

* **Signature**

   ```ts
   () => number
   ```

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setVolume

Adjusts the volume of the specified audio mixing, including media file mixing and PCM mixing.

* **Signature**

   ```ts
   (
     volume: number,
     type: AudioMixingType
   ) => number
   ```

* **Notes**

   If you call this API before playback starts, the configured value is cached and takes effect after playback starts.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |volume |number |The ratio of the volume to the original volume in % with overflow protection. The range is `[0, 400]` and the recommended range is `[0, 100]`. |
   |type |[AudioMixingType](https://docs.byteplus.com/en/docs/12/docs-85535#audiomixingtype) |Mixing type. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### getVolume

Gets the current volume.

* **Signature**

   ```ts
   (type: AudioMixingType) => number
   ```

* **Notes**

   Call this API only when audio is mixing, including media file mixing and PCM mixing.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |type |[AudioMixingType](https://docs.byteplus.com/en/docs/12/docs-85535#audiomixingtype) |Mixing type. |

* **Return Value**

   Type: number

   * \>0: Success, the current volume.

   * < 0: Failed.

### getTotalDuration

Gets the duration of the media file.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * Call this API only when audio is mixing.

   * The API is valid for audio file, not PCM data.

* **Return Value**

   Type: number

   * \>0: Success, the duration of the media file in milliseconds.

   * < 0: Failed.

### getPlaybackDuration

Gets the actual playback duration of the mixed media file, in milliseconds.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * The actual playback time refers to the playback time of the song without being affected by stop, jump, double speed, and freeze. For example, if the song stops playing for 30 seconds at 1:30 or skips to 2:00, and then continues to play normally for 2 minutes, the actual playing time is 3 minutes and 30 seconds.

   * Call this API only when audio is mixing.

   * The API is valid for audio file, not PCM data.

* **Return Value**

   Type: number

   * \>0: Success, the actual playback time.

   * < 0: Failed.

### getPosition

Gets the playback progress of the media file.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * Call this API only when audio is mixing.

   * The API is valid for audio file, not PCM data.

* **Return Value**

   Type: number

   * \>0: Success, the playback progress of media file in ms.

   * < 0: Failed.

### setPosition

Sets the starting playback position of the media file.

* **Signature**

   ```ts
   (position: number) => number
   ```

* **Notes**

   When playing online files, calling this API may cause playback delay.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |position |number |The starting position of the media file in milliseconds.<br><br>You can get the total duration of the media file through [getTotalDuration](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-gettotalduration). The value of position should be less than the total duration of the media file. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setAudioPitch

Set the pitch of the local audio file mixing. Usually used in karaoke scenes.

* **Signature**

   ```ts
   (pitch: number) => number
   ```

* **Notes**

   * Call this API only when audio is mixing.

   * Support audio file and not PCM data.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |pitch |number |The increase or decrease value compared with the original pitch of the music file. The range is `[-12, 12]`. The default value is 0. The pitch distance between two adjacent values is half a step. A positive value indicates a rising pitch, and a negative value indicates a falling pitch. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setAudioDualMonoMode

Sets the channel mode of the mixing of the media file.

* **Signature**

   ```ts
   (mode: AudioMixingDualMonoMode) => number
   ```

* **Notes**

   * Call this API only when audio is mixing.

   * Audio file is supported, but not PCM data.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |mode |[AudioMixingDualMonoMode](https://docs.byteplus.com/en/docs/12/docs-85535#audiomixingdualmonomode) |The channel mode. The default channel mode is the same as the source file. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### getAudioTrackCount

Gets the track count of the current media file.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   * Call this API only when audio is mixing.

   * This API is valid for audio files, not PCM data.

* **Return Value**

   Type: number

   * `>= 0`: Success. Returns the track count of the current media file.

   * `< 0`: Failure.

### selectAudioTrack

Specifies the playback track of the current media file.

* **Signature**

   ```ts
   (index: number) => number
   ```

* **Notes**

   * Call this API only when audio is mixing.

   * This API is valid for audio files, not PCM data.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |index |number |The target playback track, starting from `0`, and the range is `[0, getAudioTrackCount() - 1]`.<br><br>The value must be less than the return value of [getAudioTrackCount](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-getaudiotrackcount). |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setPlaybackSpeed

Sets the playback speed of the audio file.

* **Signature**

   ```ts
   (speed: number) => number
   ```

* **Notes**

   * Call this API only when audio is mixing.

   * This API is valid for audio files, not PCM data.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |speed |number |Ratio of the playback speed to the original speed in `%`. The range is `[50, 200]`. The default value is `100`. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `< 0`: Failure.

### setProgressInterval

Set the interval of the periodic callback [onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-85533#rtcmediaplayercallback-onmediaplayerplayingprogress) during audio mixing.

* **Signature**

   ```ts
   (interval: string) => number
   ```

* **Notes**

   * Call this API only when audio is mixing.

   * This API is valid for audio files, not PCM data.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |interval |string |Playback progress callback interval in milliseconds, represented as a string.<br><br><br>* interval \> 0: The callback is enabled. The actual interval is always a multiple of 10. If the provided value is not divisible by 10, it will automatically be rounded up using a ceiling function. For example, if 52 is provided, the actual interval will be 60ms.<br><br>* interval <= 0: The callback is disabled. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setLoudness

To call [enableVocalInstrumentBalance](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enablevocalinstrumentbalance) to adjust the volume of the mixed media file or the PCM audio data, you must pass in its original loudness through this API.

* **Signature**

   ```ts
   (loudness: number) => number
   ```

* **Notes**

   * Call this API only when audio is mixing.

   * The API is valid for audio file and PCM data.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |loudness |number |Original loudness in lufs. The range is `[-70.0, 0.0]`.<br><br>When the value is less than \-70.0lufs, it will be adjusted to \-70.0lufs by default, and if it is more than 0.0lufs, the loudness will not be equalized. The default value is 1.0lufs, which means no processing. |

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### setEventHandler

Register an observer to receive related callbacks when the local media file is mixing.

* **Signature**

   ```ts
   () => number
   ```

* **Notes**

   Triggers [onMediaPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcmediaplayercallback-onmediaplayerstatechanged) and [onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-85533#rtcmediaplayercallback-onmediaplayerplayingprogress).

* **Return Value**

   Type: number

   * 0: Success.

   * < 0: Failure.

### openWithCustomSource

Starts mixing PCM audio data from a custom source.

* **Signature**

   ```ts
   (
     source: MediaPlayerCustomSource,
     config: MediaPlayerConfig
   ) => number
   ```

* **Notes**

   * To play an audio file, use [open](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-open). This API and [open](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-open) are mutually exclusive.

   * After calling this method, push PCM data through [pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-pushexternalaudioframe) to start mixing.

   * Call [stop](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-stop) to stop PCM mixing.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |source |[MediaPlayerCustomSource](https://docs.byteplus.com/en/docs/12/docs-85535#mediaplayercustomsource) |Audio source description. |
   |config |[MediaPlayerConfig](https://docs.byteplus.com/en/docs/12/docs-85535#mediaplayerconfig) |Player configurations. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `<0`: Failure.

### pushExternalAudioFrame

Pushes PCM audio frames for mixing.

* **Signature**

   ```ts
   (frame: ExternalAudioFrame) => any
   ```

* **Notes**

   * Before calling this method, start external audio mixing with [openWithCustomSource](https://docs.byteplus.com/en/docs/12/docs-85532#rtcmediaplayer-openwithcustomsource).

   * It is recommended to buffer some data in the app first, for example 200 ms, before the first push. Then push 10 ms of audio data every 10 ms.

   * To pause playback, stop pushing audio frames.

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |frame |[ExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85535#externalaudioframe) |Audio frame. |

* **Return Value**

   * `0`: Success.

   * `<0`: Failure.

### processCallback

* **Signature**

   ```ts
   (event: EventType) => void
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |event |[EventType](https://docs.byteplus.com/en/docs/12/docs-85535#eventtype) | |

## RTCWTNStream

Type: `class`

* **API**

|Method |Description |
|---|---|
|[dispose](https://docs.byteplus.com/en/docs/12/14196#rtcwtnstream-dispose) |Releases the WTN stream instance. |
|[subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/14196#rtcwtnstream-subscribewtnvideostream) |Subscribes to or unsubscribes from a specified WTN video stream. |
|[subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/14196#rtcwtnstream-subscribewtnaudiostream) |Subscribes to or unsubscribes from a specified WTN audio stream. |
|[setupWTNRemoteVideo](https://docs.byteplus.com/en/docs/12/14196#rtcwtnstream-setupwtnremotevideo) |Binds an internal render view for a specified WTN remote video stream. |
|[removeWTNRemoteVideo](https://docs.byteplus.com/en/docs/12/14196#rtcwtnstream-removewtnremotevideo) |Removes the internal render view bound to a specified WTN remote video stream. |
|[setWTNRemoteVideoSink](https://docs.byteplus.com/en/docs/12/14196#rtcwtnstream-setwtnremotevideosink) |Binds a custom video sink for a specified WTN remote video stream. |
|[unsetWTNRemoteVideoSink](https://docs.byteplus.com/en/docs/12/14196#rtcwtnstream-unsetwtnremotevideosink) |Unbinds the custom video sink of a specified WTN remote video stream. |
|[setWTNRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/14196#rtcwtnstream-setwtnremoteaudioplaybackvolume) |Adjusts the playback volume of a specified WTN remote audio stream. |

### dispose

Releases the WTN stream instance.

* **Signature**

   ```ts
   () => void
   ```

### subscribeWTNVideoStream

Subscribes to or unsubscribes from a specified WTN video stream.

* **Signature**

   ```ts
   (
     stream_id: string,
     subscribe: boolean
   ) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |WTN stream ID. If the stream is not published yet, the local client receives data after it starts publishing. |
   |subscribe |boolean |Whether to subscribe to the stream.<br><br><br>* `true`: Subscribe.<br><br>* `false`: Unsubscribe. |

* **Return Value**

   Type: number

   * `0`: Success. You will also receive [onWTNVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcwtnstreamcallback-onwtnvideosubscribestatechanged).

   * `!0`: Failure.

### subscribeWTNAudioStream

Subscribes to or unsubscribes from a specified WTN audio stream.

* **Signature**

   ```ts
   (
     stream_id: string,
     subscribe: boolean
   ) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |WTN stream ID. If the stream is not published yet, the local client receives data after it starts publishing. |
   |subscribe |boolean |Whether to subscribe to the stream.<br><br><br>* `true`: Subscribe.<br><br>* `false`: Unsubscribe. |

* **Return Value**

   Type: number

   * `0`: Success. You will also receive [onWTNAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcwtnstreamcallback-onwtnaudiosubscribestatechanged).

   * `!0`: Failure.

### setupWTNRemoteVideo

Binds an internal render view for a specified WTN remote video stream.

* **Signature**

   ```ts
   (
     stream_id: string,
     view: HTMLDivElement,
     renderOptions?: RenderOptions
   ) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |WTN stream ID. |
   |view |HTMLDivElement |Render container. |
   |renderOptions |[RenderOptions](https://docs.byteplus.com/en/docs/12/docs-85535#renderoptions) |Render options. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `!0`: Failure.

### removeWTNRemoteVideo

Removes the internal render view bound to a specified WTN remote video stream.

* **Signature**

   ```ts
   (stream_id: string) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |WTN stream ID. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `!0`: Failure.

### setWTNRemoteVideoSink

Binds a custom video sink for a specified WTN remote video stream.

* **Signature**

   ```ts
   (
     stream_id: string,
     required_format: PixelFormat
   ) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |WTN stream ID. |
   |required_format |[PixelFormat](https://docs.byteplus.com/en/docs/12/docs-85535#pixelformat) |Required pixel format. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `<0`: Failure.

### unsetWTNRemoteVideoSink

Unbinds the custom video sink of a specified WTN remote video stream.

* **Signature**

   ```ts
   (stream_id: string) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |WTN stream ID. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `!0`: Failure.

### setWTNRemoteAudioPlaybackVolume

Adjusts the playback volume of a specified WTN remote audio stream.

* **Signature**

   ```ts
   (
     stream_id: string,
     volume: number
   ) => number
   ```

* **Parameters**

   |Parameter |Type |Description |
   |---|---|---|
   |stream_id |string |WTN stream ID. |
   |volume |number |Ratio of the playback volume to the original volume in `%`, ranging from `[0, 400]`. The recommended range is `[0, 100]`. |

* **Return Value**

   Type: number

   * `0`: Success.

   * `-2`: Invalid parameter.
