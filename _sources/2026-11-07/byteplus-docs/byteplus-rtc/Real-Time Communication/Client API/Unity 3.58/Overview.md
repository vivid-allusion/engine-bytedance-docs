---
title: "Overview"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-191858"
---

<span id="methods"></span>
# Methods

<span id="engine-management"></span>
## Engine Management


|Method |Description |
|---|---|
|[CreateRTCVideo](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-creatertcvideo) |Create an instance of RTCVideoEngine.<br><br>After the RTCVideoEngine instance is successfully created, you can use other capabilities provided by the SDK. |
|[GetSDKVersion](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-getsdkversion) |Get the current version number of the SDK. |
|[Feedback](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-feedback) |After the call ends, report user feedback to RTC. |
|[GetErrorDescription](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-geterrordescription) |Get the description text for various error codes and warning codes within the SDK. |
|[SetBusinessId](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setbusinessid) |Set the business identifier parameter.<br><br>You can distinguish different business scenarios through businessId. businessId is customized by the customer, equivalent to a "tag", which can share and refine the logical division function of the current AppId without the need for authentication. |
|[SetRuntimeParameters](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setruntimeparameters) |Set runtime parameters. |


<span id="room-management"></span>
## Room Management


|Method |Description |
|---|---|
|[CreateRTCRoom](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-creatertcroom) |Create a room. |
|[Release](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-release) |Exit and destroy the room created by calling [CreateRTCRoom](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-creatertcroom). |
|[JoinRoom](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-joinroom) |Join a room.<br><br>After creating a room by calling [CreateRTCRoom](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-creatertcroom), call this method to join the room and have audio and video calls with other users in the same room. |
|[LeaveRoom](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-leaveroom) |Leave a room.<br><br>The user calls this method to leave the room, end the call process, and release all call\-related resources. |
|[SetUserVisibility](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-setuservisibility) |Set user visibility. Default is visible. |
|[UpdateToken](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-updatetoken) |Update the Token.<br><br>When you receive [OnTokenWillExpireEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#ontokenwillexpireeventhandler), you must re\-acquire the Token and call this method to update the Token to ensure the call proceeds normally. |


<span id="audio-management"></span>
## Audio Management


|Method |Description |
|---|---|
|[SetAudioRoute](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setaudioroute) |Set the current audio playback route.<br><br>When the audio playback route changes, you will receive a [OnAudioRouteChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onaudioroutechangedeventhandler) callback. |
|[SetDefaultAudioRoute](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setdefaultaudioroute) |Set the default audio output device to the earpiece or speaker. |
|[GetAudioRoute](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-getaudioroute) |Get the current audio playback route. |
|[EnumerateAudioPlaybackDevices](https://docs.byteplus.com/en/docs/12/docs-191859#IAudioDeviceManager-enumerateaudioplaybackdevices) |Get the list of audio playback devices in the system. If devices change later, you need to call this interface again to get the new list of devices. |
|[EnumerateAudioCaptureDevices](https://docs.byteplus.com/en/docs/12/docs-191859#IAudioDeviceManager-enumerateaudiocapturedevices) |Get the list of audio capture devices in the system. If devices change later, you need to call this interface again to get the new list of devices. |
|[SetAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-191859#IAudioDeviceManager-setaudioplaybackdevice) |Set the audio playback device. |
|[SetAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-191859#IAudioDeviceManager-setaudiocapturedevice) |Set the audio capture device. |
|[MuteAudioCapture](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-muteaudiocapture) |Set whether to mute the recording signal (without changing the local hardware). |
|[GetAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-191859#IAudioDeviceManager-getaudioplaybackdevice) |Get the ID of the current audio playback device. |
|[GetAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-191859#IAudioDeviceManager-getaudiocapturedevice) |Get the ID of the current audio capture device. |
|[FollowSystemPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-191859#IAudioDeviceManager-followsystemplaybackdevice) |Set whether the audio playback route follows the system. |
|[FollowSystemCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-191859#IAudioDeviceManager-followsystemcapturedevice) |Set whether the audio capture route follows the system. |
|[SetAudioPlaybackDeviceVolume](https://docs.byteplus.com/en/docs/12/docs-191859#IAudioDeviceManager-setaudioplaybackdevicevolume) |Set the volume of the current audio playback device. |
|[GetAudioPlaybackDeviceVolume](https://docs.byteplus.com/en/docs/12/docs-191859#IAudioDeviceManager-getaudioplaybackdevicevolume) |Get the volume of the current audio playback device. |
|[SetAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/docs-191859#IAudioDeviceManager-setaudiocapturedevicevolume) |Set the volume of the current audio capture device. |
|[GetAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/docs-191859#IAudioDeviceManager-getaudiocapturedevicevolume) |Get the volume of the current audio capture device. |
|[SetAudioPlaybackDeviceMute](https://docs.byteplus.com/en/docs/12/docs-191859#IAudioDeviceManager-setaudioplaybackdevicemute) |Set the mute status of the current audio playback device, default is not muted. |
|[GetAudioPlaybackDeviceMute](https://docs.byteplus.com/en/docs/12/docs-191859#IAudioDeviceManager-getaudioplaybackdevicemute) |Get whether the current audio playback device is muted. |
|[SetAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/docs-191859#IAudioDeviceManager-setaudiocapturedevicemute) |Set the mute status of the current audio capture device, default is not muted. |
|[GetAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/docs-191859#IAudioDeviceManager-getaudiocapturedevicemute) |Get whether the current audio capture device is muted. |
|[SetCaptureVolume](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setcapturevolume) |Adjust the volume of audio capture. |
|[SetPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setplaybackvolume) |Adjust the volume of all remote users' audio mixed locally, including remote voices, music, sound effects, etc. |
|[SetRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setremoteaudioplaybackvolume) |Adjust the volume of audio playback from a specified remote user, default is 100. |
|[EnableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-enableaudiopropertiesreport) |Enable audio property reporting. |
|[StartAudioCapture](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-startaudiocapture) |Start internal audio capture. Default is off.<br><br>Internal capture refers to: using the RTC SDK's built\-in video capture mechanism for video capture.<br><br>After calling this method, local users will receive a callback of [OnAudioDeviceStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onaudiodevicestatechangedeventhandler).<br><br>Visible users who call this method after entering the room will trigger a callback of [OnUserStartAudioCaptureEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserstartaudiocaptureeventhandler) for other users in the room. |
|[StopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-stopaudiocapture) |Immediately stop internal audio capture. Default is off.<br><br>Internal capture refers to: using the RTC SDK's built\-in video capture mechanism for video capture.<br><br>After calling this method, local users will receive a callback of [OnAudioDeviceStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onaudiodevicestatechangedeventhandler).<br><br>Visible users who call this method after entering the room will trigger a callback of [OnUserStopAudioCaptureEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserstopaudiocaptureeventhandler) for other users in the room. |
|[SetAudioScenario](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setaudioscenario) |Set the audio scenario type. |
|[StartScreenAudioCapture](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-startscreenaudiocapture) |When screen sharing, start capturing screen audio using the RTC SDK's internal capture method. |
|[StopScreenAudioCapture](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-stopscreenaudiocapture) |When screen sharing, stop capturing screen audio using the RTC SDK's internal capture method. |
|[SetAudioProfile](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setaudioprofile) |Set the audio quality level. You should choose the appropriate audio quality level based on the business scenario. |
|[GetAudioDeviceManager](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-getaudiodevicemanager) |Get the audio device management interface, which depends on the engine. |


<span id="video-management"></span>
## Video Management


|Method |Description |
|---|---|
|[StartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-startvideocapture) |Immediately start internal video capture. Default is off.<br><br>Internal video capture refers to: using the RTC SDK's built\-in video capture module for capture.<br><br>After calling this method, the local user will receive a [OnVideoDeviceStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onvideodevicestatechangedeventhandler) callback.<br><br>When the local user calls this method while not in stealth mode, other users in the room will receive a [OnUserStartVideoCaptureEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserstartvideocaptureeventhandler) callback. |
|[StopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-stopvideocapture) |Immediately stop internal video capture. Default is off.<br><br>Internal video capture refers to: using the RTC SDK's built\-in video capture module for capture.<br><br>After calling this method, the local user will receive a [OnVideoDeviceStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onvideodevicestatechangedeventhandler) callback.<br><br>When a visible user enters the room and calls this method, other users in the room will receive a [OnUserStopVideoCaptureEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserstopvideocaptureeventhandler) callback. |
|[SetVideoCaptureConfig](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setvideocaptureconfig) |Set the video capture parameters when the RTC SDK is capturing internally.<br><br>If your project uses the SDK's internal capture module, you can specify video capture parameters including mode, resolution, frame rate through this interface. |
|[SetVideoRotationMode](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setvideorotationmode) |Set the rotation mode for captured video. The default rotation reference is the app's orientation.<br><br>When the receiving end renders the video, it will rotate in the same way as the sender. |
|[SwitchCamera](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-switchcamera) |Switch between the front and rear cameras used for internal video capture.<br><br>After calling this interface, a [OnVideoDeviceStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onvideodevicestatechangedeventhandler) callback will be triggered locally. |
|[EnumerateVideoCaptureDevices](https://docs.byteplus.com/en/docs/12/docs-191859#IVideoDeviceManager-enumeratevideocapturedevices) |Get the list of video capture devices currently in the system. |
|[SetVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-191859#IVideoDeviceManager-setvideocapturedevice) |Set the current video capture device. |
|[GetVideoDeviceManager](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-getvideodevicemanager) |Get the video device management interface. |
|[GetVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/docs-191859#IVideoDeviceManager-getvideocapturedevice) |Get information about the video capture device currently being used by the SDK. |
|[SetVideoEncoderConfig1](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setvideoencoderconfig1) |Set the maximum resolution video stream parameters expected to be published by the video publisher, including resolution, frame rate, bitrate, scaling mode, fallback strategy when the network is poor, etc. |


<span id="audio-video-transport"></span>
## Audio & Video Transport


|Method |Description |
|---|---|
|[PublishStream](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-publishstream) |Publish local media streams captured by the camera/microphone in the current room. |
|[UnpublishStream](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-unpublishstream) |Stop publishing local media streams captured by the camera/microphone to the current room. |
|[SubscribeStream](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-subscribestream) |Subscribe to the specified media streams captured by the camera/microphone in the room, or update the subscription options for the specified remote user. |
|[UnsubscribeStream](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-unsubscribestream) |Unsubscribe from the specified media streams captured by the camera/microphone in the room.<br><br>This method applies to both automatic and manual subscription modes. |
|[SubscribeAllStreams](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-subscribeallstreams) |Subscribe to all media streams captured by the camera/microphone in the room, or update subscription options. |
|[UnsubscribeAllStreams](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-unsubscribeallstreams) |Unsubscribe from all media streams captured by the camera/microphone in the room.<br><br>Streams subscribed automatically and manually can both be unsubscribed using this method. |
|[PauseAllSubscribedStream](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-pauseallsubscribedstream) |Pause receiving media streams from remote sources. |
|[ResumeAllSubscribedStream](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-resumeallsubscribedstream) |Resume receiving media streams from remote sources. |
|[SetDummyCaptureImagePath](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setdummycaptureimagepath) |When the camera is turned off, fill the local pushed video stream with a static image.<br><br>Calling the stopVideoCapture interface will start pushing a static image. To stop sending images, you can pass an empty string or enable internal camera capture.<br><br>This interface can be called repeatedly to update the image. |
|[StartForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-startforwardstreamtorooms) |Start forwarding media streams to multiple rooms.<br><br>Call this interface after [JoinRoom](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-joinroom) to forward media streams to multiple rooms, suitable for scenarios like cross\-room interaction. |
|[StopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-stopforwardstreamtorooms) |Stop forwarding media streams to rooms.<br><br>You can call this method to stop forwarding media streams to all target rooms after initiating the forwarding with [StartForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-startforwardstreamtorooms). |
|[UpdateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-updateforwardstreamtorooms) |Update the information for forwarding media streams to rooms.<br><br>You can call this method to add or remove target rooms, or update room keys after initiating the forwarding with [StartForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-startforwardstreamtorooms).<br><br>After calling this method to add or remove rooms, the [OnForwardStreamStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onforwardstreamstatechangedeventhandler) callback will be triggered on the local end, including the forwarding status of the media streams in the target rooms that have changed. |
|[PauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-pauseforwardstreamtoallrooms) |Pause forwarding media streams to all rooms.<br><br>You can call this method to pause forwarding media streams to all target rooms after initiating the forwarding with [StartForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-startforwardstreamtorooms).<br><br>You can call [ResumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-resumeforwardstreamtoallrooms) at any time to quickly resume forwarding. |
|[ResumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-resumeforwardstreamtoallrooms) |Resume forwarding media streams to all rooms.<br><br>Call this method to resume forwarding media streams to all target rooms after pausing with [PauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-pauseforwardstreamtoallrooms). |
|[SetMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-setmultideviceavsync) |Set audio and video synchronization for the streaming end.<br><br>When a user simultaneously uses two communication devices to capture and send audio and video, the published streams may become unsynchronized due to different network conditions of the two devices. At this time, you can call this interface on the video sending end, and the SDK will automatically calibrate the video stream based on the audio stream timestamps to ensure the synchronicity of audio and video at the receiving end. |


<span id="video-processing"></span>
## Video Processing


|Method |Description |
|---|---|
|[SetLocalVideoMirrorType](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setlocalvideomirrortype) |Enable mirroring for the captured video stream. |
|[SetVideoCaptureRotation](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setvideocapturerotation) |Set the rotation angle of the video frames captured by this end.<br><br>When the camera is inverted or tilted, this interface can be called for adjustment. |
|[SetVideoWatermark](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setvideowatermark) |Add a watermark to the specified video stream. |
|[ClearVideoWatermark](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-clearvideowatermark) |Remove the watermark from the specified video stream. |
|[EnableEffectBeauty](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-enableeffectbeauty) |Turn on/off basic beauty effects. |
|[SetBeautyIntensity](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setbeautyintensity) |Adjust the intensity of the basic beauty effects. |
|[GetAuthMessage](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-getauthmessage) |Obtain an authorization message from the special effects SDK for obtaining an online license. |
|[FreeAuthMessage](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-freeauthmessage) |Release memory after using the authorization message string. |
|[InitCVResource](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-initcvresource) |Check the video effects certificate, set the path of the algorithm model, and initialize the special effects module. |
|[EnableVideoEffect](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-enablevideoeffect) |Turn on advanced beauty effects, filters, and other video effects. |
|[DisableVideoEffect](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-disablevideoeffect) |Turn off video effects. |
|[SetEffectNodes](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-seteffectnodes) |Set the video effect material package. |
|[UpdateEffectNode](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-updateeffectnode) |Set the intensity of the special effects. |
|[SetColorFilter](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setcolorfilter) |Set a color filter. |
|[SetColorFilterIntensity](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setcolorfilterintensity) |Set the intensity of the enabled color filter. |
|[EnableVirtualBackground](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-enablevirtualbackground) |Replace the background of the camera\-captured image with a specified image or solid color background. |
|[DisableVirtualBackground](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-disablevirtualbackground) |Turn off the virtual background. |
|[VideoSDKEnableFaceDetection](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-videosdkenablefacedetection) |Turn on face recognition and set an observer for face detection results.<br><br>You will periodically receive a callback of [OnFaceDetectResultEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onfacedetectresulteventhandler) after setting this observer. |
|[VideoSDKDisableFaceDetection](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-videosdkdisablefacedetection) |Turn off face recognition. |
|[SetVideoDigitalZoomConfig](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setvideodigitalzoomconfig) |Set local camera digital zoom parameters, including zoom factor and movement step size. |
|[SetVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setvideodigitalzoomcontrol) |Control local camera digital zoom, zoom in or move once. Settings apply to both local preview and video published to the remote end. |
|[StartVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-startvideodigitalzoomcontrol) |Start continuous digital zoom of the local camera, zoom in or move. Settings apply to both local preview and video published to the remote end. |
|[StopVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-stopvideodigitalzoomcontrol) |Stop continuous digital zoom of the local camera. |


<span id="audio-processing"></span>
## Audio Processing


|Method |Description |
|---|---|
|[SetVoiceReverbType](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setvoicereverbtype) |Set the type of reverb effect. |
|[SetVoiceChangerType](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setvoicechangertype) |Set the type of voice changer effect. |
|[SetLocalVoicePitch](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setlocalvoicepitch) |Enable local voice pitch adjustment feature, often used in karaoke scenarios.<br><br>With this method, you can adjust the pitch of local voice by raising or lowering it. |
|[SetLocalVoiceEqualization](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setlocalvoiceequalization) |Set the equalization effect for locally captured voice. Includes internal and external capture, but does not include mixed audio files. |
|[SetLocalVoiceReverbParam](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setlocalvoicereverbparam) |Set the reverb effect for locally captured audio. Includes internal and external capture, but does not include mixed audio files. |
|[EnableLocalVoiceReverb](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-enablelocalvoicereverb) |Enable local audio effect reverb. |


<span id="custom-stream-processing"></span>
## Custom Stream Processing


|Method |Description |
|---|---|
|[SetVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setvideosourcetype) |Set the video source input to the SDK, including screen streaming.<br><br>Default is to use internal capture. Internal capture refers to: using the RTC SDK's built\-in video capture mechanism for video capture. |
|[PushExternalVideoFrame](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-pushexternalvideoframe) |Push external video frames. |
|[SetLocalVideoSink](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setlocalvideosink) |Bind the local video stream with a custom renderer. |
|[SetRemoteVideoSink](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setremotevideosink) |Bind the remote video stream with a custom renderer. |
|[SetAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setaudiosourcetype) |Switch audio capture methods. |
|[PushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-pushexternalaudioframe) |Push custom captured audio data to the RTC SDK. |
|[EnableAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-enableaudioprocessor) |Set and enable a specified audio frame callback for custom processing. |
|[DisableAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-disableaudioprocessor) |Turn off custom audio processing. |
|[EnableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-enableaudioframecallback) |Set and enable a specified audio data frame callback. |
|[DisableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-disableaudioframecallback) |Turn off audio callbacks. |


<span id="messages"></span>
## Messages


|Method |Description |
|---|---|
|[SendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-sendroommessage) |Broadcast text messages to all other users in the room. |
|[SendUserMessage](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-sendusermessage) |Send point\-to\-point text messages (P2P) to a specified user in the room. |
|[SendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-sendstreamsyncinfo) |Send audio stream synchronization information. The message is sent to the remote end through the audio stream, achieving synchronization with the audio stream. After this interface is called successfully, the remote user will receive the [OnStreamSyncInfoReceivedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onstreamsyncinforeceivedeventhandler) callback. |
|[SendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-sendseimessage) |Send SEI data through video frames.<br><br>In video call scenarios, SEI data is sent with video frames; in voice call scenarios, the SDK automatically generates a 16px × 16px black frame video stream for sending SEI data. |


<span id="audio-mixing"></span>
## Audio Mixing


|Method |Description |
|---|---|
|[EnableVocalInstrumentBalance](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-enablevocalinstrumentbalance) |Turn on/off the volume balance feature.<br><br>After turning on the volume balance feature, the loudness of the human voice will be adjusted to \-16lufs. |


<span id="screen-sharing"></span>
## Screen Sharing


|Method |Description |
|---|---|
|[StartScreenCapture](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-startscreencapture) |Start capturing screen audio and/or video streams using the RTC SDK's internal capture module. |
|[GetScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-getscreencapturesourcelist) |Get the list of shared objects (application windows and desktops), and call the corresponding release interface to release after use. |
|[StartScreenVideoCapture](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-startscreenvideocapture) |Use the capture module provided by the RTC SDK to capture the current screen video stream for sharing. |
|[UpdateScreenCaptureHighlightConfig](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-updatescreencapturehighlightconfig) |Update the border highlight settings when capturing screen video streams using the capture module provided by the RTC SDK. Default to display a border. |
|[UpdateScreenCaptureMouseCursor](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-updatescreencapturemousecursor) |Update the mouse handling settings when capturing screen video streams using the capture module provided by the RTC SDK. Default to capture the mouse. |
|[UpdateScreenCaptureFilterConfig](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-updatescreencapturefilterconfig) |Set the windows to be filtered when capturing screen video streams using the capture module provided by the RTC SDK. |
|[UpdateScreenCaptureRegion](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-updatescreencaptureregion) |Update the capture region when using the RTC SDK's screen video capture module. |
|[StopScreenVideoCapture](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-stopscreenvideocapture) |Stop capturing the screen video stream. |
|[PublishScreen](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-publishscreen) |Publish local screen sharing audio and video streams in the current room. |
|[UnpublishScreen](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-unpublishscreen) |Stop publishing local screen sharing audio and video streams to the current room. |
|[GetThumbnail](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-getthumbnail) |Get the thumbnail of the shared object. |
|[SetScreenAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setscreenaudiosourcetype) |Set the screen audio capture method (internal capture/ custom capture) when sharing the screen. |
|[SetScreenAudioStreamIndex](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setscreenaudiostreamindex) |Set the mixing method of screen audio streams and microphone\-capture audio streams during screen sharing. |
|[PushScreenAudioFrame](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-pushscreenaudioframe) |Push the audio frames to the RTC SDK for encoding and other processing when using custom capture for screen sharing audio. |
|[PushScreenVideoFrame](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-pushscreenvideoframe) |Push screen video frames. |
|[SetScreenVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setscreenvideoencoderconfig) |Set the desired encoding parameters for the published screen sharing video stream, including resolution, frame rate, bitrate, scaling mode, and fallback strategies when the network is poor. |
|[SubscribeScreen](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-subscribescreen) |Subscribe to the specified remote screen sharing audio and video streams in the room, or update the subscription options for the specified remote user. |
|[UnsubscribeScreen](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-unsubscribescreen) |Unsubscribe from the specified remote screen sharing audio and video streams in the room.<br><br>This method applies to both automatic and manual subscription modes. |


<span id="advanced-features"></span>
## Advanced Features


|Method |Description |
|---|---|
|[StartAudioRecording](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-startaudiorecording) |Start recording voice calls and generate local files. |
|[StopAudioRecording](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-stopaudiorecording) |Stop recording audio files. |
|[SetEarMonitorMode](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setearmonitormode) |Turn on/off ear monitoring. |
|[SetEarMonitorVolume](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setearmonitorvolume) |Set the ear monitoring volume. |
|[GetSpatialAudio](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-getspatialaudio) |Obtain the spatial audio interface. |
|[EnableSpatialAudio](https://docs.byteplus.com/en/docs/12/docs-191859#ISpatialAudio-enablespatialaudio) |Set whether to enable spatial audio. |
|[UpdatePosition](https://docs.byteplus.com/en/docs/12/docs-191859#ISpatialAudio-updateposition) |Update the local user's position in the room's spatial coordinate system when speaking. |
|[UpdateSelfOrientation](https://docs.byteplus.com/en/docs/12/docs-191859#ISpatialAudio-updateselforientation) |Update your own orientation. The setting of local orientation only affects the audio effect heard locally and does not affect the audio effect of local发声. |
|[DisableRemoteOrientation](https://docs.byteplus.com/en/docs/12/docs-191859#ISpatialAudio-disableremoteorientation) |Turn off the influence of local user orientation on the local user's speaking effect.<br><br>After calling this interface, other users in the room will hear the sound source in front of the listener when listening to the local user's voice. |
|[GetRangeAudio](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-getrangeaudio) |Obtain the range audio interface. |
|[EnableRangeAudio](https://docs.byteplus.com/en/docs/12/docs-191859#IRangeAudio-enablerangeaudio) |Turn on/off range audio functionality.<br><br>Range audio refers to the volume of audio heard by local users from remote users increasing/decreasing as they approach/move away within a set audio reception range in the same RTC room; if the remote user is outside the set range, the local user cannot receive their audio. See [UpdateReceiveRange](https://docs.byteplus.com/en/docs/12/docs-191859#IRangeAudio-updatereceiverange) for audio reception range settings. |
|[SetAttenuationModel](https://docs.byteplus.com/en/docs/12/docs-191859#IRangeAudio-setattenuationmodel) |Set the volume attenuation model for range audio. |
|[SetNoAttenuationFlags](https://docs.byteplus.com/en/docs/12/docs-191859#IRangeAudio-setnoattenuationflags) |Add a tag group to mark user groups whose calls do not attenuate.<br><br>In the same RTC room, if there is an intersection between the tag groups of multiple users, their calls will not attenuate when talking to each other.<br><br>For example, if users are in multiple teams and team members' calls do not attenuate, each team can be assigned exclusive tags, and each user's tag group can include the tags of the teams they belong to. |
|[UpdatePosition](https://docs.byteplus.com/en/docs/12/docs-191859#IRangeAudio-updateposition) |Update the local user's position in the room's spatial coordinate system. |
|[UpdateReceiveRange](https://docs.byteplus.com/en/docs/12/docs-191859#IRangeAudio-updatereceiverange) |Update the local user's audio listening range. |


<span id="callbacks"></span>
# Callbacks

<span id="engine-management"></span>
## Engine Management


|Callback |Description |
|---|---|
|[OnLogReportEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onlogreporteventhandler) |This event is called back when logging is reported. |
|[OnSysStatsEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onsysstatseventhandler) |A callback that occurs every 2 seconds, notifying information about current CPU and memory usage. |
|[OnWarningEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onwarningeventhandler) |A callback that occurs when a warning happens. |
|[OnErrorEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onerroreventhandler) |A callback that occurs when an error happens. |
|[OnTokenWillExpireEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#ontokenwillexpireeventhandler) |This callback is triggered when the SDK detects that the token's room entry permission will expire within 30 seconds.<br><br>Call [UpdateToken](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-updatetoken) to update the token. Otherwise, after the token expires, the user will be removed from the room and will not be able to continue audio and video calls. |


<span id="room-management"></span>
## Room Management


|Callback |Description |
|---|---|
|[OnRoomStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onroomstatechangedeventhandler) |A callback for room state changes, received when joining a room, exiting a room abnormally, or when room\-related warnings or errors occur. |
|[OnCreateRoomStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#oncreateroomstatechangedeventhandler) |A callback for room creation failure. |
|[OnLeaveRoomEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onleaveroomeventhandler) |A callback for successful room exit.<br><br>After a user calls the [LeaveRoom](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-leaveroom) method, the SDK will stop all publishing and subscribing streams, and when all call\-related audio and video resources are released, this callback will notify the user that the room has been successfully exited. |
|[OnUserJoinedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserjoinedeventhandler) |A callback for when a remote visible user joins the room or when a room\-invisible user switches to visible.<br><br>+ When a remote visible user calls the [SetUserVisibility](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-setuservisibility) method to set themselves as visible and then joins the room, other users in the room will receive this event.<br><br>+ When a remote visible user who has been disconnected from the network re\-enters the room, other users in the room will receive this event.<br><br>+ When an invisible remote user in the room calls the [SetUserVisibility](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-setuservisibility) method to switch to visible, other users in the room will receive this event.<br><br>+ New users entering the room will also receive a callback notification for visible users who were already in the room before they entered. |
|[OnUserLeaveEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserleaveeventhandler) |A local user will receive this event when a remote user leaves the room or becomes invisible. |


<span id="audio-management"></span>
## Audio Management


|Callback |Description |
|---|---|
|[OnAudioDeviceWarningEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onaudiodevicewarningeventhandler) |Media device warning callback. Media devices include: audio capture devices, audio rendering devices, and video capture devices. |
|[OnAudioDeviceStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onaudiodevicestatechangedeventhandler) |Audio device state callback. Indicates the state of media devices such as audio capture and audio playback. |
|[OnAudioRouteChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onaudioroutechangedeventhandler) |Received when the audio playback route changes. |
|[OnLocalAudioPropertiesReportEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onlocalaudiopropertiesreporteventhandler) |After calling [EnableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-enableaudiopropertiesreport), you will periodically receive this callback based on the set Interval value to understand information about the local audio.<br><br>Local audio includes microphone audio and screen audio captured using the RTC SDK's internal mechanism. |
|[OnRemoteAudioPropertiesReportEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onremoteaudiopropertiesreporteventhandler) |After a remote user enters the room, the local call to [EnableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-enableaudiopropertiesreport) will result in periodic callbacks based on the set interval value, providing information about the subscribed remote user's instantaneous audio information.<br><br>The remote user's audio includes microphone audio and screen audio captured using the RTC SDK's internal mechanism/custom mechanism. |
|[OnUserStartAudioCaptureEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserstartaudiocaptureeventhandler) |When a visible user in the room calls [StartAudioCapture](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-startaudiocapture) to start audio capture, other users in the room will receive this callback. |
|[OnUserStopAudioCaptureEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserstopaudiocaptureeventhandler) |When a visible user in the room calls [StopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-stopaudiocapture) to stop audio capture, other users in the room will receive this callback. |
|[OnStreamSyncInfoReceivedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onstreamsyncinforeceivedeventhandler) |Audio stream synchronization information callback. You can receive the audio stream synchronization information sent by the remote user through this callback after the remote user calls [SendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-sendstreamsyncinfo) to send an audio stream synchronization message. |
|[OnAudioStreamBannedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onaudiostreambannedeventhandler) |This callback is triggered when the MuteUser/UnmuteUser method is called on the server to disable/unban the sending of audio and video streams for a specified user in a specified room. |
|[OnLocalAudioStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onlocalaudiostatechangedeventhandler) |This callback notifies the current local audio stream state when the state of the local audio stream changes. |


<span id="video-management"></span>
## Video Management


|Callback |Description |
|---|---|
|[OnUserStartVideoCaptureEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserstartvideocaptureeventhandler) |When a visible user in the room calls [StartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-startvideocapture) to start internal video capture, other users in the room will receive this callback. |
|[OnUserStopVideoCaptureEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserstopvideocaptureeventhandler) |When a visible user in the room calls [StopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-stopvideocapture) to stop internal video capture, other users in the room will receive this callback. |
|[OnVideoDeviceStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onvideodevicestatechangedeventhandler) |Video device state callback. Indicates the status of media devices such as camera video capture and screen video capture. |
|[OnVideoDeviceWarningEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onvideodevicewarningeventhandler) |Video device warning callback, including devices such as video capture. |


<span id="audio-video-transmission"></span>
## Audio/Video Transmission


|Callback |Description |
|---|---|
|[OnStreamStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onstreamstatechangedeventhandler) |Stream state change callback, received when there are stream\-related warnings or errors. |
|[OnUserPublishStreamEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserpublishstreameventhandler) |Callback when a new remote camera/microphone media stream is added in the room. |
|[OnUserUnPublishStreamEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserunpublishstreameventhandler) |Callback when a remote camera/microphone media stream is removed in the room. |
|[OnStreamSubscribedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onstreamsubscribedeventhandler) |Callback for changes in the status of subscribed media streams. |
|[OnAudioFrameSendStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onaudioframesendstatechangedeventhandler) |Received when the status of the first local audio frame sent changes. |
|[OnVideoFrameSendStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onvideoframesendstatechangedeventhandler) |Received when the status of the first local video frame sent changes. |
|[OnAudioFramePlayStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onaudioframeplaystatechangedeventhandler) |Received when the status of the first audio frame played changes. |
|[OnVideoFramePlayStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onvideoframeplaystatechangedeventhandler) |Received when the status of the first video frame played changes. |
|[OnLocalStreamStatsEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onlocalstreamstatseventhandler) |Local stream statistics and network quality callback.<br><br>After a local user publishes a stream successfully, the SDK will periodically (every 2 seconds) notify the user of the quality statistics of the published stream during this statistical period through this callback event.<br><br>Statistics are passed to the user through the [LocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-191862#localstreamstats) type of callback parameter, including sent audio and video bitrate, sent frame rate, encoding frame rate, network quality, etc. |
|[OnRemoteStreamStatsEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onremotestreamstatseventhandler) |Callback for statistics and network quality of locally subscribed remote audio/video streams.<br><br>After a local user subscribes to a stream, the SDK periodically (every 2 seconds) notifies the user of the quality statistics of the subscribed stream during this period, including: sent audio/video bitrate, sent frame rate, encoded frame rate, network quality, etc. |
|[OnNetworkQualityEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onnetworkqualityeventhandler) |After joining a room, the network quality information of the user is reported at a frequency of once every 2 seconds. |
|[OnForwardStreamStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onforwardstreamstatechangedeventhandler) |Callback for status and errors of media stream forwarding across rooms. |
|[OnForwardStreamEventEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onforwardstreameventeventhandler) |Callback for events related to media stream forwarding across rooms. |
|[OnFirstLocalAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onfirstlocalaudioframeeventhandler) |This callback is received when the first local audio frame is captured. |
|[OnFirstRemoteAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onfirstremoteaudioframeeventhandler) |This callback is received when the first frame of an audio stream from a remote source is received. |
|[OnFirstLocalVideoFrameCapturedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onfirstlocalvideoframecapturedeventhandler) |This callback is received when the RTC SDK completes the capture of the first local video frame or screen video frame. |
|[OnLocalVideoSizeChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onlocalvideosizechangedeventhandler) |This callback is received when there is a change in the size or rotation of the local video. |
|[OnLocalVideoStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onlocalvideostatechangedeventhandler) |This event is received when the status of the local video stream changes. |
|[OnRemoteVideoSizeChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onremotevideosizechangedeventhandler) |When there is a change in the size or rotation of the remote video, users who subscribe to this video stream in the room will receive this callback. |
|[OnRemoteVideoStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onremotevideostatechangedeventhandler) |Users who subscribe to this stream in the room will receive this event when the status of the remote video stream changes. |
|[OnRemoteAudioStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onremoteaudiostatechangedeventhandler) |When the status of the audio stream subscribed from a remote source changes, this callback is received to understand the current status of the remote audio stream. |
|[OnFirstRemoteVideoFrameRenderedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onfirstremotevideoframerenderedeventhandler) |This callback is received after the SDK successfully renders the first frame of the remote video stream internally. |
|[OnVideoStreamBannedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onvideostreambannedeventhandler) |This callback is triggered when the sending of a specified user's video stream in a specified room is disabled/enabled through the MuteUser/UnmuteUser method on the server. |
|[OnFirstRemoteVideoFrameDecodedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onfirstremotevideoframedecodedeventhandler) |This callback is received after the SDK receives and decodes the first frame of the remote video stream. |
|[OnAVSyncStateChangeCallback](https://docs.byteplus.com/en/docs/12/docs-191860#onavsyncstatechangecallback) |When the audio/video synchronization status changes after the publisher calls [SetMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-setmultideviceavsync), this callback is received. |


<span id="video-processing"></span>
## Video Processing


|Callback |Description |
|---|---|
|[OnFaceDetectResultEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onfacedetectresulteventhandler) |Callback for the face detection results of the special effects SDK.<br><br>You will receive this callback when you call [VideoSDKEnableFaceDetection](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-videosdkenablefacedetection) to enable this callback and use the special effects SDK included in the RTC SDK for video special effects processing. |


<span id="custom-stream-processing"></span>
## Custom Stream Processing


|Callback |Description |
|---|---|
|[OnProcessEarMonitorAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onprocessearmonitoraudioframeeventhandler) |Callback for the ear monitor data audio frame address for custom audio processing. |
|[OnProcessPlaybackAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onprocessplaybackaudioframeeventhandler) |Callback for the mixed audio frame address of remote audio for custom audio processing. |
|[OnProcessRecordAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onprocessrecordaudioframeeventhandler) |Callback for the local captured audio frame address for custom audio processing. |
|[OnProcessRemoteUserAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onprocessremoteuseraudioframeeventhandler) |Callback for the audio frame address of a single remote user for custom audio processing. |
|[OnProcessScreenAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onprocessscreenaudioframeeventhandler) |Callback for the screen sharing audio frame address. You can customize audio processing based on this callback. |
|[OnRecordAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onrecordaudioframeeventhandler) |Returns the audio data recorded by the microphone. |
|[OnPlaybackAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onplaybackaudioframeeventhandler) |Returns the audio data of all remote users mixed after subscription. |
|[OnRemoteUserAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onremoteuseraudioframeeventhandler) |Returns the audio data of a single remote user. |
|[OnMixedAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onmixedaudioframeeventhandler) |Returns the audio data mixed from local microphone recording and all remote users subscribed. |
|[OnRecordScreenAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onrecordscreenaudioframeeventhandler) |Returns the audio data recorded from local screen sharing. |
|[OnLocalVideoSinkOnFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onlocalvideosinkonframeeventhandler) |Custom renderer local video frame callback. |
|[OnLocalVideoSinkGetRenderElapseEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onlocalvideosinkgetrenderelapseeventhandler) |Custom rendering local video frame elapsed time. |
|[OnLocalVideoSinkReleaseEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onlocalvideosinkreleaseeventhandler) |Release local custom renderer. |
|[OnRemoteVideoSinkOnFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onremotevideosinkonframeeventhandler) |Custom renderer remote video frame callback. |
|[OnRemoteVideoSinkGetRenderElapseEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onremotevideosinkgetrenderelapseeventhandler) |Custom rendering remote video frame elapsed time. |
|[OnRemoteVideoSinkReleaseEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onremotevideosinkreleaseeventhandler) |Release remote custom renderer. |


<span id="network-management"></span>
## Network Management


|Callback |Description |
|---|---|
|[OnConnectionStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onconnectionstatechangedeventhandler) |Callback for SDK connection state events with the signaling server. This event is called when the network connection state between the SDK and the signaling server changes. |
|[OnNetworkTypeChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onnetworktypechangedeventhandler) |Callback for changes in the current network connection type of the SDK. This event is called when the current network connection type of the SDK changes. |
|[OnSEIMessageReceivedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onseimessagereceivedeventhandler) |Callback received when a video frame with an SEI message is received through the call to [SendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-sendseimessage). |
|[OnSEIMessageUpdateEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onseimessageupdateeventhandler) |Callback for the status of black frame video stream publishing.<br><br>In voice call scenarios, when a local user calls [SendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-sendseimessage) to send SEI data through a black frame video stream, the status of the stream's transmission is notified to the remote user through this callback.<br><br>You can use this callback to determine that the video frame carrying the SEI data is a black frame, and thus not render the video frame. |


<span id="messages"></span>
## Messages


|Callback |Description |
|---|---|
|[OnRoomMessageReceivedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onroommessagereceivedeventhandler) |Callback received when a broadcast message is received in the room.<br><br>This callback is received when other users in the room call [SendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-sendroommessage) to send a broadcast message. |
|[OnUserMessageReceivedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onusermessagereceivedeventhandler) |Callback received when a point\-to\-point text message is received from other users in the room through [SendUserMessage](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-sendusermessage). |
|[OnUserMessageSendResultEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onusermessagesendresulteventhandler) |Callback received by the message sender after sending a point\-to\-point text or binary message to a single user in the room. |
|[OnRoomMessageSendResultEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onroommessagesendresulteventhandler) |Callback received by the message sender after broadcasting a text or binary message to the room through [SendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-sendroommessage). |


<span id="screen-sharing"></span>
## Screen Sharing


|Callback |Description |
|---|---|
|[OnUserPublishScreenEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserpublishscreeneventhandler) |Callback for when a new remote screen sharing audio/video stream is added in the room. |
|[OnUserUnPublishScreenEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserunpublishscreeneventhandler) |Callback for when a remote screen sharing audio/video stream is removed from the room. |
|[OnScreenVideoFrameSendStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onscreenvideoframesendstatechangedeventhandler) |This callback is received when the sending status of the first frame of the screen sharing stream video changes. |


<span id="advanced-features"></span>
## Advanced Features


|Callback |Description |
|---|---|
|[OnAudioRecordingStateUpdateEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onaudiorecordingstateupdateeventhandler) |This callback is received when the audio file recording status is changed by calling [StartAudioRecording](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-startaudiorecording) or [StopAudioRecording](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-stopaudiorecording). |
