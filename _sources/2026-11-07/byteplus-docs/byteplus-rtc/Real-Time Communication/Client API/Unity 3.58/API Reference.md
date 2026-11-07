---
title: "API Reference"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-191859"
---

<span id="IRangeAudio"></span>
# IRangeAudio

```c#
interface bytertc::IRangeAudio
```


Range audio interface

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[EnableRangeAudio](https://docs.byteplus.com/en/docs/12/35814#IRangeAudio-enablerangeaudio) |
|int |[UpdateReceiveRange](https://docs.byteplus.com/en/docs/12/35814#IRangeAudio-updatereceiverange) |
|int |[UpdatePosition](https://docs.byteplus.com/en/docs/12/35814#IRangeAudio-updateposition) |
|int |[SetAttenuationModel](https://docs.byteplus.com/en/docs/12/35814#IRangeAudio-setattenuationmodel) |
|void |[SetNoAttenuationFlags](https://docs.byteplus.com/en/docs/12/35814#IRangeAudio-setnoattenuationflags) |
|void |[Release](https://docs.byteplus.com/en/docs/12/35814#IRangeAudio-release) |


<span id="instructions"></span>
## Instructions

<span id="IRangeAudio-enablerangeaudio"></span>
### EnableRangeAudio

```c#
void bytertc.IRangeAudio.EnableRangeAudio(bool enable)
```


Enable/disable the range audio function. Range audio means that within a certain range in a same RTC room, the audio volume of the remote user received by the local user will be amplified/attenuated as the remote user moves closer/away. The audio coming from out of the range cannot be heard. See [UpdateReceiveRange](https://docs.byteplus.com/en/docs/12/35814#IRangeAudio-updatereceiverange) to set audio receiving range.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|enable |bool |Whether to enable audio range funcion：<br><br><br>* true: Enable<br><br>* false: Disable（Defaulting setting） |


**Notes**

You can call this API anytime before or after entering a room. To ensure a smooth switch to the range audio mode after entering the room, you need to call [UpdateReceiveRange](https://docs.byteplus.com/en/docs/12/35814#IRangeAudio-updatereceiverange) before this API to set your own position coordinates, and then enable the range audio function.

<span id="IRangeAudio-updatereceiverange"></span>
### UpdateReceiveRange

```c#
int bytertc.IRangeAudio.UpdateReceiveRange(ReceiveRange range)
```


Updates the audio receiving range for the local user.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|range |ReceiveRange |Audio receiving range, see [ReceiveRange](https://docs.byteplus.com/en/docs/12/docs-191862#ReceiveRange). |


**Return Value**

API call result:


* 0: Success

* !0: Failure


<span id="IRangeAudio-updateposition"></span>
### UpdatePosition

```c#
int bytertc.IRangeAudio.UpdatePosition(Position pos)
```


Updates the coordinate of the local user's position in the rectangular coordinate system in the current room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|pos |Position |3D coordinate values, the default value is [0, 0, 0]. See [Position](https://docs.byteplus.com/en/docs/12/docs-191862#Position). |


**Return Value**


* 0: Success.

* !0: Failure.


**Notes**

After calling this API, you should call [EnableRangeAudio](https://docs.byteplus.com/en/docs/12/35814#IRangeAudio-enablerangeaudio) to enable range audio function to actually enjoy the range audio effect.

<span id="IRangeAudio-setattenuationmodel"></span>
### SetAttenuationModel

```c#
int bytertc.IRangeAudio.SetAttenuationModel(
    AttenuationType type,
    float coefficient
)
```


Set the volume roll\-off mode that a 3D sound has in an audio source when using the Range Audio feature.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |AttenuationType |Volume roll\-off mode. It is linear roll\-off mode by default. Refer to [AttenuationType](https://docs.byteplus.com/en/docs/12/docs-191862#AttenuationType) for more details. |
|coefficient |float |Coefficient for the exponential roll\-off mode. The default value is 1. It ranges [0.1,100]. We recommended to set it to `50`. The volume roll\-off speed gets faster as this value increases. |


**Return Value**

Result of the call


* `0`: Success

* `-1`: Failure because of calling this API before the user has joined a room or before enabling the Range Audio feature by calling [EnableRangeAudio](https://docs.byteplus.com/en/docs/12/35814#IRangeAudio-enablerangeaudio).


**Notes**

Call [UpdateReceiveRange](https://docs.byteplus.com/en/docs/12/35814#IRangeAudio-updatereceiverange) to set the range outside which the volume of the sound does not attenuate.

<span id="IRangeAudio-setnoattenuationflags"></span>
### SetNoAttenuationFlags

```c#
void bytertc.IRangeAudio.SetNoAttenuationFlags(
    string[] flags,
    int len
)
```


Set the flags to mark the user groups, within which the users talk without attenuation. In the RTC room, if the flags of the users intersects with each other, the users talk without attenuation. For example, the user is a member of multiple teams, and teammates of the same team talks without attentuation. You can set the flag for each team, and includes the flags of the user's teams in the user's flags.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|flags |string[] |Array of flags. |
|len |int |The length of the flags array. |


<span id="IRangeAudio-release"></span>
### Release

```c#
void bytertc.IRangeAudio.Release()
```


Releases the resources occupied by the current [IRangeAudio](https://docs.byteplus.com/en/docs/12/35814#IRangeAudio) object.

<span id="IVideoDeviceManager"></span>
# IVideoDeviceManager

```c#
interface bytertc::IVideoDeviceManager
```


Mainly used to enumerate and set up video capture devices

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|IDeviceCollection |[EnumerateVideoCaptureDevices](https://docs.byteplus.com/en/docs/12/35814#IVideoDeviceManager-enumeratevideocapturedevices) |
|int |[SetVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/35814#IVideoDeviceManager-setvideocapturedevice) |
|int |[GetVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/35814#IVideoDeviceManager-getvideocapturedevice) |


<span id="instructions"></span>
## Instructions

<span id="IVideoDeviceManager-enumeratevideocapturedevices"></span>
### EnumerateVideoCaptureDevices

```c#
IDeviceCollection bytertc.IVideoDeviceManager.EnumerateVideoCaptureDevices()
```


Get a list of video capture devices in the current system.

**Return Value**

Contains a list of all video capture devices in the system. See [IDeviceCollection](https://docs.byteplus.com/en/docs/12/35814#IDeviceCollection).

<span id="IVideoDeviceManager-setvideocapturedevice"></span>
### SetVideoCaptureDevice

```c#
int bytertc.IVideoDeviceManager.SetVideoCaptureDevice(string deviceID)
```


Set the current video capture device

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|deviceID |string |Video device ID, which can be obtained through [EnumerateVideoCaptureDevices](https://docs.byteplus.com/en/docs/12/35814#IVideoDeviceManager-enumeratevideocapturedevices) |


**Return Value**


* 0: Success. \-! 0: failure


<span id="IVideoDeviceManager-getvideocapturedevice"></span>
### GetVideoCaptureDevice

```c#
int bytertc.IVideoDeviceManager.GetVideoCaptureDevice(ref string deviceID)
```


Get the video capture device information currently used by the SDK

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|deviceID |ref string |video device ID |


**Return Value**


* 0: Success. \-! 0: failure


<span id="IRTCVideo"></span>
# IRTCVideo

```c#
interface bytertc::IRTCVideo
```


Engine interface.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[CreateRTCVideo](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-creatertcvideo) |
|void |[Release](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-release) |
|string |[GetErrorDescription](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-geterrordescription) |
|string |[GetSDKVersion](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-getsdkversion) |
|int |[SetBusinessId](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setbusinessid) |
|int |[Feedback](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-feedback) |
|void |[SetRuntimeParameters](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setruntimeparameters) |
|IRTCVideoRoom |[CreateRTCRoom](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-creatertcroom) |
|int |[MuteAudioCapture](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-muteaudiocapture) |
|void |[SetCaptureVolume](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setcapturevolume) |
|void |[SetPlaybackVolume](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setplaybackvolume) |
|void |[StartAudioCapture](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-startaudiocapture) |
|void |[StopAudioCapture](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-stopaudiocapture) |
|void |[SetAudioProfile](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setaudioprofile) |
|void |[SetAudioScenario](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setaudioscenario) |
|int |[EnableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-enableaudiopropertiesreport) |
|int |[SetVoiceReverbType](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setvoicereverbtype) |
|int |[SetVoiceChangerType](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setvoicechangertype) |
|int |[SetLocalVoicePitch](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setlocalvoicepitch) |
|int |[SetLocalVoiceEqualization](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setlocalvoiceequalization) |
|int |[SetLocalVoiceReverbParam](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setlocalvoicereverbparam) |
|int |[EnableLocalVoiceReverb](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-enablelocalvoicereverb) |
|int |[SetDummyCaptureImagePath](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setdummycaptureimagepath) |
|int |[RequestRemoteVideoKeyFrame](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-requestremotevideokeyframe) |
|int |[StartPlayPublicStream](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-startplaypublicstream) |
|int |[StopPlayPublicStream](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-stopplaypublicstream) |
|int |[StartPushPublicStream](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-startpushpublicstream) |
|int |[StopPushPublicStream](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-stoppushpublicstream) |
|int |[SetPublicStreamAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setpublicstreamaudioplaybackvolume) |
|int |[SetVideoCaptureRotation](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setvideocapturerotation) |
|int |[SetVideoWatermark](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setvideowatermark) |
|int |[ClearVideoWatermark](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-clearvideowatermark) |
|int |[EnableEffectBeauty](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-enableeffectbeauty) |
|int |[SetBeautyIntensity](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setbeautyintensity) |
|int |[GetAuthMessage](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-getauthmessage) |
|int |[FreeAuthMessage](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-freeauthmessage) |
|int |[InitCVResource](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-initcvresource) |
|int |[EnableVideoEffect](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-enablevideoeffect) |
|int |[DisableVideoEffect](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-disablevideoeffect) |
|int |[SetEffectNodes](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-seteffectnodes) |
|int |[UpdateEffectNode](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-updateeffectnode) |
|int |[SetColorFilter](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setcolorfilter) |
|int |[SetColorFilterIntensity](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setcolorfilterintensity) |
|int |[EnableVirtualBackground](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-enablevirtualbackground) |
|int |[DisableVirtualBackground](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-disablevirtualbackground) |
|int |[VideoSDKEnableFaceDetection](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-videosdkenablefacedetection) |
|int |[VideoSDKDisableFaceDetection](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-videosdkdisablefacedetection) |
|int |[SetVideoDigitalZoomConfig](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setvideodigitalzoomconfig) |
|int |[SetVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setvideodigitalzoomcontrol) |
|int |[StartVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-startvideodigitalzoomcontrol) |
|int |[StopVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-stopvideodigitalzoomcontrol) |
|void |[SetEarMonitorMode](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setearmonitormode) |
|void |[SetEarMonitorVolume](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setearmonitorvolume) |
|void |[EnableVocalInstrumentBalance](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-enablevocalinstrumentbalance) |
|int |[SetRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setremoteaudioplaybackvolume) |
|int |[SetDefaultAudioRoute](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setdefaultaudioroute) |
|int |[SetAudioRoute](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setaudioroute) |
|AudioRouteDevice |[GetAudioRoute](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-getaudioroute) |
|int |[EnableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-enableaudioframecallback) |
|int |[DisableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-disableaudioframecallback) |
|int |[StartAudioRecording](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-startaudiorecording) |
|int |[StopAudioRecording](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-stopaudiorecording) |
|int |[SendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-sendstreamsyncinfo) |
|int |[SendSEIMessage](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-sendseimessage) |
|int |[EnableAudioProcessor](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-enableaudioprocessor) |
|int |[DisableAudioProcessor](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-disableaudioprocessor) |
|IAudioDeviceManager |[GetAudioDeviceManager](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-getaudiodevicemanager) |
|IVideoDeviceManager |[GetVideoDeviceManager](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-getvideodevicemanager) |
|void |[StartVideoCapture](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-startvideocapture) |
|void |[StopVideoCapture](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-stopvideocapture) |
|int |[SetVideoCaptureConfig](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setvideocaptureconfig) |
|int |[SetVideoEncoderConfig1](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setvideoencoderconfig1) |
|int |[SetScreenVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setscreenvideoencoderconfig) |
|void |[SetVideoSourceType](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setvideosourcetype) |
|void |[SetLocalVideoMirrorType](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setlocalvideomirrortype) |
|int |[SetVideoRotationMode](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setvideorotationmode) |
|void |[SetLocalVideoSink](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setlocalvideosink) |
|void |[SetRemoteVideoSink](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setremotevideosink) |
|IScreenCaptureSourceList |[GetScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-getscreencapturesourcelist) |
|int |[StartScreenVideoCapture](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-startscreenvideocapture) |
|void |[StopScreenVideoCapture](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-stopscreenvideocapture) |
|void |[UpdateScreenCaptureRegion](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-updatescreencaptureregion) |
|void |[UpdateScreenCaptureHighlightConfig](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-updatescreencapturehighlightconfig) |
|void |[UpdateScreenCaptureMouseCursor](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-updatescreencapturemousecursor) |
|void |[UpdateScreenCaptureFilterConfig](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-updatescreencapturefilterconfig) |
|VideoFrame |[GetThumbnail](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-getthumbnail) |
|void |[SetScreenAudioSourceType](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setscreenaudiosourcetype) |
|void |[SetScreenAudioStreamIndex](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setscreenaudiostreamindex) |
|void |[StartScreenAudioCapture](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-startscreenaudiocapture) |
|void |[StopScreenAudioCapture](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-stopscreenaudiocapture) |
|void |[StartScreenCapture](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-startscreencapture) |
|int |[PushScreenAudioFrame](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-pushscreenaudioframe) |
|int |[SwitchCamera](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-switchcamera) |
|int |[PushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-pushexternalaudioframe) |
|void |[SetAudioSourceType](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setaudiosourcetype) |
|int |[PushExternalVideoFrame](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-pushexternalvideoframe) |
|int |[PushScreenVideoFrame](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-pushscreenvideoframe) |


<span id="instructions"></span>
## Instructions

<span id="IRTCVideo-creatertcvideo"></span>
### CreateRTCVideo

```c#
int bytertc.IRTCVideo.CreateRTCVideo(RTCVideoEngineParams initParams)
```


Create GameRTCEngine instance. After the GameRTCEngine instance is successfully created, you can use other capabilities provided by the SDK.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|initParams |RTCVideoEngineParams |Engine initialization parameters. See [RTCVideoEngineParams](https://docs.byteplus.com/en/docs/12/docs-191862#RTCVideoEngineParams). |


<span id="IRTCVideo-release"></span>
### Release

```c#
void bytertc.IRTCVideo.Release()
```


Destroys the engine instance created by [CreateRTCVideo](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-creatertcvideo) and releases all related resources.

<span id="IRTCVideo-geterrordescription"></span>
### GetErrorDescription

```c#
string bytertc.IRTCVideo.GetErrorDescription(int code)
```


Get the description text of various error codes and warning codes in the SDK

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|code |int |Error code or warning code. |


**Return Value**

string Description.

<span id="IRTCVideo-getsdkversion"></span>
### GetSDKVersion

```c#
string bytertc.IRTCVideo.GetSDKVersion()
```


gets the current version number of the SDK.

**Return Value**

The current version number of the SDK.

<span id="IRTCVideo-setbusinessid"></span>
### SetBusinessId

```c#
int bytertc.IRTCVideo.SetBusinessId(string businessID)
```


Sets the business ID. You can use businessId to distinguish different business scenarios. You can customize your businessId to serve as a sub AppId, which can share and refine the function of the AppId, but it does not need authentication.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|businessID |string |Your customized businessId BusinessId is a tag, and you can customize its granularity. |


**Return Value**


* 0: Success

* < 0: Failure

* \-6001: The user is already in the room.

* \-6002: The input is invalid. Legal characters include all lowercase letters, uppercase letters, numbers, and four other symbols, including '.', '\-','_', and '@'.


**Notes**

You must call this API before the [JoinRoom](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-joinroom) API, otherwise it will be invalid.

<span id="IRTCVideo-feedback"></span>
### Feedback

```c#
int bytertc.IRTCVideo.Feedback(
    String roomID,
    String userID,
    List<int> typeArray,
    string problemDescription
)
```


End of call, report the user feedback to RTC.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |String |Room ID. |
|userID |String |User ID. |
|typeArray |List<int\> |List of preset problems. See [ProblemFeedbackOption](https://docs.byteplus.com/en/docs/12/docs-191862#ProblemFeedbackOption). |
|problemDescription |string |Specific description of other problems other than the preset problem. |


**Return Value**


* 0: Report successfully

* \-1: Failed to report, not yet joined the room

* \-2: Failed to report, data analysis error

* \-3: Failed to report, missing fields


<span id="IRTCVideo-setruntimeparameters"></span>
### SetRuntimeParameters

```c#
void bytertc.IRTCVideo.SetRuntimeParameters(string jsonString)
```


Setting runtime parameters.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|jsonString |string |String after json serialization. |


<span id="IRTCVideo-creatertcroom"></span>
### CreateRTCRoom

```c#
IRTCVideoRoom bytertc.IRTCVideo.CreateRTCRoom(string roomID)
```


Create room

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |Identify the room ID of the calling room, and the maximum length is 128 bytes of non\-empty string. Supported character set ranges are:<br><br><br>* 26 uppercase letters A~ Z<br><br>* 26 lowercase letters a~ z<br><br>* 10 digits 0~ 9<br><br>* underscore "_", at character "@" , Minus "\-" In multi\-room mode, after calling the create room interface, do not call the same roomID to create a room, otherwise it will cause the creation of a room to fail. |


**Return Value**

IRTCVideoRoom Created room IRTCVideoRoom

<span id="IRTCVideo-muteaudiocapture"></span>
### MuteAudioCapture

```c#
int bytertc.IRTCVideo.MuteAudioCapture(
    StreamIndex index,
    bool mute
)
```


> Available since 3.58.1


Set whether to mute the recording signal (without changing the local hardware).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|index |StreamIndex |Stream index, specifying the main stream or screen stream volume adjustment. See [StreamIndex](https://docs.byteplus.com/en/docs/12/70083#streamindex-2). |
|mute |bool |Whether to mute audio capture.<br><br><br>* True: Mute (disable microphone)<br><br>* False: (Default) Enable microphone |


**Return Value**


* 0: Success.

* < 0 : Failure.


<span id="IRTCVideo-setcapturevolume"></span>
### SetCaptureVolume

```c#
void bytertc.IRTCVideo.SetCaptureVolume(
    StreamIndex index,
    int volume
)
```


Adjust the volume of the audio capture

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|index |StreamIndex |Index of the stream, whose volume needs to be adjusted. Refer to [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-191862#StreamIndex) for more details. |
|volume |int |Ratio of capture volume to original volume. Ranging: [0,400]. Unit: %<br><br><br>* 0: Mute<br><br>* 100: Original volume. To ensure the audio quality, we recommend [0, 100].<br><br>* 400: Four times the original volume with signal\-clipping protection. |


**Notes**

Call this API to set the volume of the audio capture before or during the audio capture.

<span id="IRTCVideo-setplaybackvolume"></span>
### SetPlaybackVolume

```c#
void bytertc.IRTCVideo.SetPlaybackVolume(int volume)
```


Adjust the playback volume of the mixed remote audios.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|volume |int |Ratio of playback volume to original volume. Ranging: [0,400]. Unit: % To ensure the audio quality, we recommend setting the volume within `100`.<br><br><br>* 0: mute<br><br>* 100: original volume<br><br>* 400: Four times the original volume with signal\-clipping protection. |


<span id="IRTCVideo-startaudiocapture"></span>
### StartAudioCapture

```c#
void bytertc.IRTCVideo.StartAudioCapture()
```


Start internal audio capture. The default is off. Internal audio capture refers to: capturing audio using the built\-in module. The local client will be informed via [OnAudioDeviceStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onaudiodevicestatechangedeventhandler) after starting audio capture by calling this API. The remote clients in the room will be informed of the state change via [OnUserStartAudioCaptureEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserstartaudiocaptureeventhandler) after the visible user starts audio capture by calling this API.

<span id="IRTCVideo-stopaudiocapture"></span>
### StopAudioCapture

```c#
void bytertc.IRTCVideo.StopAudioCapture()
```


Stop internal audio capture. The default is off. Internal audio capture refers to: capturing audio using the built\-in module. The local client will be informed via [OnAudioDeviceStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onaudiodevicestatechangedeventhandler) after stopping audio capture by calling this API. The remote clients in the room will be informed of the state change via [OnUserStopAudioCaptureEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserstopaudiocaptureeventhandler) after the visible client stops audio capture by calling this API.

<span id="IRTCVideo-setaudioprofile"></span>
### SetAudioProfile

```c#
void bytertc.IRTCVideo.SetAudioProfile(AudioProfileType audioProfile)
```


Sets the sound quality gear. You should choose the appropriate sound quality gear according to the needs of the business scenario.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioProfile |AudioProfileType |Sound quality gear. See [AudioProfileType](https://docs.byteplus.com/en/docs/12/docs-191862#AudioProfileType) |


<span id="IRTCVideo-setaudioscenario"></span>
### SetAudioScenario

```c#
void bytertc.IRTCVideo.SetAudioScenario(AudioScenarioType scenario)
```


Sets the audio scenarios.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|scenario |AudioScenarioType |Audio scenarios. See [AudioScenarioType](https://docs.byteplus.com/en/docs/12/docs-191862#AudioScenarioType). |


**Notes**

You can call this API before or after joining room.

<span id="IRTCVideo-enableaudiopropertiesreport"></span>
### EnableAudioPropertiesReport

```c#
int bytertc.IRTCVideo.EnableAudioPropertiesReport(AudioPropertiesConfig config)
```


Enable audio information prompts.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|config |AudioPropertiesConfig |See [AudioPropertiesConfig](https://docs.byteplus.com/en/docs/12/docs-191862#AudioPropertiesConfig) |


**Notes**

After enable the prompt, you can:


* Get the information of the audio stream collected by the local microphone and screen audio stream through [OnLocalAudioPropertiesReportEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onlocalaudiopropertiesreporteventhandler);

* Get the information of the subscribed remote audio streams through [OnRemoteAudioPropertiesReportEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onremoteaudiopropertiesreporteventhandler).


<span id="IRTCVideo-setvoicereverbtype"></span>
### SetVoiceReverbType

```c#
int bytertc.IRTCVideo.SetVoiceReverbType(VoiceReverbType type)
```


Set the reverb effect type

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |VoiceReverbType |Reverb effect type. See [VoiceReverbType](https://docs.byteplus.com/en/docs/12/docs-191862#VoiceReverbType) |


<span id="IRTCVideo-setvoicechangertype"></span>
### SetVoiceChangerType

```c#
int bytertc.IRTCVideo.SetVoiceChangerType(VoiceChangerType voice_changer)
```


Set the sound change effect type

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|voice_changer |VoiceChangerType |The sound change effect type. See [VoiceChangerType](https://docs.byteplus.com/en/docs/12/docs-191862#VoiceChangerType). |


**Return Value**

API call result:


* 0: Success

* !0: Failure


<span id="IRTCVideo-setlocalvoicepitch"></span>
### SetLocalVoicePitch

```c#
int bytertc.IRTCVideo.SetLocalVoicePitch(int pitch)
```


Change local voice to a different key, mostly used in Karaoke scenarios. You can adjust the pitch of local voice such as ascending or descending with this method.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|pitch |int |The value that is higher or lower than the original local voice within a range from \-12 to 12. The default value is 0, i.e. No adjustment is made. The difference in pitch between two adjacent values within the value range is a semitone, with positive values indicating an ascending tone and negative values indicating a descending tone, and the larger the absolute value set, the more the pitch is raised or lowered. Out of the value range, the setting fails and triggers [OnWarningEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onwarningeventhandler) callback, indicating `WARNING_CODE_SET_SCREEN_STREAM_INVALID_VOICE_PITCH` for invalid value setting with [WarningCode](https://docs.byteplus.com/en/docs/12/docs-191861#WarningCode). |


**Return Value**


* 0: Success.

* < 0 : Fail.


<span id="IRTCVideo-setlocalvoiceequalization"></span>
### SetLocalVoiceEqualization

```c#
int bytertc.IRTCVideo.SetLocalVoiceEqualization(VoiceEqualizationConfig config)
```


Set the equalization effect for the local captured audio. The audio includes both internal captured audio and external captured voice, but not the mixing audio file.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|config |VoiceEqualizationConfig |See [VoiceEqualizationConfig](https://docs.byteplus.com/en/docs/12/docs-191862#VoiceEqualizationConfig). |


**Return Value**


* 0: Success.

* < 0: Failure.


**Notes**

According to the Nyquist acquisition rate, the audio acquisition rate must be greater than twice the set center frequency. Otherwise, the setting will not be effective.

<span id="IRTCVideo-setlocalvoicereverbparam"></span>
### SetLocalVoiceReverbParam

```c#
int bytertc.IRTCVideo.SetLocalVoiceReverbParam(VoiceReverbConfig param)
```


Set the reverb effect for the local captured audio. The audio includes both internal captured audio and external captured voice, but not the mixing audio file.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|param |VoiceReverbConfig |See [VoiceReverbConfig](https://docs.byteplus.com/en/docs/12/docs-191862#VoiceReverbConfig). |


**Return Value**


* 0: Success.

* < 0: Failure.


**Notes**

Call [EnableLocalVoiceReverb](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-enablelocalvoicereverb) to enable the reverb effect.

<span id="IRTCVideo-enablelocalvoicereverb"></span>
### EnableLocalVoiceReverb

```c#
int bytertc.IRTCVideo.EnableLocalVoiceReverb(bool enable)
```


Enable the reverb effect for the local captured voice.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|enable |bool |Whether to enable. |


**Return Value**


* 0: Success.

* < 0: Failure.


**Notes**

Call [SetLocalVoiceReverbParam](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setlocalvoicereverbparam) to set the reverb effect.

<span id="IRTCVideo-setdummycaptureimagepath"></span>
### SetDummyCaptureImagePath

```c#
int bytertc.IRTCVideo.SetDummyCaptureImagePath(string file_path)
```


Set an alternative image when the local internal video capture is not enabled. When you call `stopVideoCapture`, an alternative image will be pushed. You can set the path to null or open the camera to stop publishing the image. You can repeatedly call this API to update the image.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|file_path |string |Set the path of the static image. You can use the absolute path (file://xxx). The maximum size for the path is 512 bytes. You can upload a .JPG, .JPEG, .PNG, or .BMP file. When the aspect ratio of the image is inconsistent with the video encoder configuration, keep the aspect\-ratio to scale the image and the crop the longer sides. The framerate and the bitrate are consistent with the video encoder configuration. |


**Return Value**


* 0: Success.

* \-1: Failure.


<span id="IRTCVideo-requestremotevideokeyframe"></span>
### RequestRemoteVideoKeyFrame

```c#
int bytertc.IRTCVideo.RequestRemoteVideoKeyFrame(ref RemoteStreamKey stream_info)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_info |ref RemoteStreamKey |\- |


<span id="IRTCVideo-startplaypublicstream"></span>
### StartPlayPublicStream

```c#
int bytertc.IRTCVideo.StartPlayPublicStream(string public_stream_id)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|public_stream_id |string |\- |


<span id="IRTCVideo-stopplaypublicstream"></span>
### StopPlayPublicStream

```c#
int bytertc.IRTCVideo.StopPlayPublicStream(string public_stream_id)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|public_stream_id |string |\- |


<span id="IRTCVideo-startpushpublicstream"></span>
### StartPushPublicStream

```c#
int bytertc.IRTCVideo.StartPushPublicStream(
    string public_stream_id,
    IntPtr public_stream
)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|public_stream_id |string |\- |
|public_stream |IntPtr |\- |


<span id="IRTCVideo-stoppushpublicstream"></span>
### StopPushPublicStream

```c#
int bytertc.IRTCVideo.StopPushPublicStream(string public_stream_id)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|public_stream_id |string |\- |


<span id="IRTCVideo-setpublicstreamaudioplaybackvolume"></span>
### SetPublicStreamAudioPlaybackVolume

```c#
int bytertc.IRTCVideo.SetPublicStreamAudioPlaybackVolume(
    string public_stream_id,
    int volume
)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|public_stream_id |string |\- |
|volume |int |\- |


<span id="IRTCVideo-setvideocapturerotation"></span>
### SetVideoCaptureRotation

```c#
int bytertc.IRTCVideo.SetVideoCaptureRotation(VideoRotation rotation)
```


Set the rotation of the video images captured from the local device. Call this API to rotate the videos when the camera is fixed upside down or tilted.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rotation |VideoRotation |It defaults to `VIDEO_ROTATION_0(0)`, which means not to rotate. Refer to [VideoRotation](https://docs.byteplus.com/en/docs/12/docs-191862#VideoRotation). |


**Return Value**


* 0: Success.

* < 0 : Fail.


<span id="IRTCVideo-setvideowatermark"></span>
### SetVideoWatermark

```c#
int bytertc.IRTCVideo.SetVideoWatermark(
    StreamIndex stream_index,
    string image_path,
    RTCWatermarkConfig config
)
```


Adds watermark to designated video stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_index |StreamIndex |The index of the target stream. See [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-191862#StreamIndex). |
|image_path |string |The absolute path of the watermark image. The path should be less than 512 bytes. The watermark image should be in PNG or JPG format. |
|config |RTCWatermarkConfig |Watermark configurations. See [RTCWatermarkConfig](https://docs.byteplus.com/en/docs/12/docs-191862#RTCWatermarkConfig). |


**Return Value**


* 0: Success.

* < 0 : Fail.


<span id="IRTCVideo-clearvideowatermark"></span>
### ClearVideoWatermark

```c#
int bytertc.IRTCVideo.ClearVideoWatermark(StreamIndex stream_index)
```


Removes video watermark from designated video stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_index |StreamIndex |The index of the target stream. See [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-191862#StreamIndex). |


**Return Value**


* 0: Success.

* < 0 : Fail.


<span id="IRTCVideo-enableeffectbeauty"></span>
### EnableEffectBeauty

```c#
int bytertc.IRTCVideo.EnableEffectBeauty(bool enable)
```


Enables/Disables basic beauty effects.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|enable |bool |Whether to enable basic beauty effects.<br><br><br>* true: Enables basic beauty effects.<br><br>* false: (Default) Disables basic beauty effects. |


**Return Value**


* 0: Success.

* –1000: The Effect SDK is not integrated.

* –1001: This API is not available for your current RTC SDK.

* –1002: This API is not available for your current Effect SDK. You can upgrade your Effect SDK to v4.4.2+.

* –1003: Contact our technical support team for further instructions.

* –1004: Downloading related resources. The beauty effects will take effect after downloading.

* <0: Failure. Effect SDK internal error. For specific error code, see [Error Code Table](https://docs.byteplus.com/effects/docs/error-code-table).


<span id="IRTCVideo-setbeautyintensity"></span>
### SetBeautyIntensity

```c#
int bytertc.IRTCVideo.SetBeautyIntensity(
    EffectBeautyMode beauty_mode,
    float intensity
)
```


Sets the beauty effect intensity.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|beauty_mode |EffectBeautyMode |Basic beauty effect. See [EffectBeautyMode](https://docs.byteplus.com/en/docs/12/docs-191862#EffectBeautyMode). |
|intensity |float |Beauty effect intensity in range of [0,1]. When you set it to 0, the beauty effect will be turned off. The default values for the intensity of each beauty mode are as follows: 0.7 for brightning, 0.8 for smoothing, 0.5 for sharpening, and 0.7 for clarity. |


**Return Value**


* 0: Success.

* –1000: The Effect SDK is not integrated.

* –1001: This API is not available for your current RTC SDK.

* <0: Failure. Effect SDK internal error. For specific error code, see [error codes](https://docs.byteplus.com/effects/docs/error-code-table).


<span id="IRTCVideo-getauthmessage"></span>
### GetAuthMessage

```c#
int bytertc.IRTCVideo.GetAuthMessage(
    ref IntPtr ppmsg,
    ref int len
)
```


Get authorization messages from the Effect SDK to obtain online licenses.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|ppmsg |ref IntPtr |The pointer pointing to the authorization message string |
|len |ref int |Authorization message string length |


**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.


<span id="IRTCVideo-freeauthmessage"></span>
### FreeAuthMessage

```c#
int bytertc.IRTCVideo.FreeAuthMessage(string pmsg)
```


After using the authorization message string, free the memory.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|pmsg |string |The authorization message string returned by getAuthMessage. |


**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.


<span id="IRTCVideo-initcvresource"></span>
### InitCVResource

```c#
int bytertc.IRTCVideo.InitCVResource(
    string license_file_path,
    string algo_model_dir
)
```


Checks video effect license, sets the video effect resource model path, and initializes video effect.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|license_file_path |string |The absolute path of the license file for authorization. |
|algo_model_dir |string |The absolute path of the Effects SDK's models file. |


**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.


<span id="IRTCVideo-enablevideoeffect"></span>
### EnableVideoEffect

```c#
int bytertc.IRTCVideo.EnableVideoEffect()
```


Enables video effects including beauty and color filters.

**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.


<span id="IRTCVideo-disablevideoeffect"></span>
### DisableVideoEffect

```c#
int bytertc.IRTCVideo.DisableVideoEffect()
```


Disables video effects.

**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.


**Notes**

Call [EnableVideoEffect](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-enablevideoeffect) to enable video effects.

<span id="IRTCVideo-seteffectnodes"></span>
### SetEffectNodes

```c#
int bytertc.IRTCVideo.SetEffectNodes(
    string[] effect_node_paths,
    int node_num
)
```


Sets the video effects material package.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|effect_node_paths |string[] |Array of effect material package paths. To remove the current video effect, set it to null. |
|node_num |int |Number of effect material packages. |


**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.


**Notes**

You must call [EnableVideoEffect](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-enablevideoeffect) before calling this API.

<span id="IRTCVideo-updateeffectnode"></span>
### UpdateEffectNode

```c#
int bytertc.IRTCVideo.UpdateEffectNode(
    string effect_node_path,
    string node_key,
    float node_value
)
```


Sets the intensity of video effects.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|effect_node_path |string |The absolute path of the effects resource package, see [Resource Package Structure](https://docs.byteplus.com/effects/docs/resource-package-structure-v421-and-later). |
|node_key |string |The name of the material key to be set, see [Functions of Resource Keys](https://docs.byteplus.com/effects/docs/functions-of-resource-keys-v421-and-later) for the value. |
|node_value |float |The intensity value that needs to be set, the value range [0,1], and the setting is invalid when it exceeds the range. |


**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.


<span id="IRTCVideo-setcolorfilter"></span>
### SetColorFilter

```c#
int bytertc.IRTCVideo.SetColorFilter(string res_path)
```


Sets the color filter.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|res_path |string |Filter effects package absolute path. |


**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.


**Notes**

Call [SetColorFilterIntensity](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setcolorfilterintensity) to set the intensity of the color filter enabled. Set the intensity to 0 to turn off color filter.

<span id="IRTCVideo-setcolorfilterintensity"></span>
### SetColorFilterIntensity

```c#
int bytertc.IRTCVideo.SetColorFilterIntensity(float intensity)
```


Sets the intensity of the color filter enabled.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|intensity |float |Filter intensity. The value range [0,1] is set to be invalid when the range is exceeded. Set the intensity to 0 to turn off color filter. |


**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.


<span id="IRTCVideo-enablevirtualbackground"></span>
### EnableVirtualBackground

```c#
int bytertc.IRTCVideo.EnableVirtualBackground(
    string background_sticker_path,
    VirtualBackgroundSource source
)
```


Sets the original background to a specified image or a solid color.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|background_sticker_path |string |The absolute path of virtual background effects. |
|source |VirtualBackgroundSource |Virtual background source. See [VirtualBackgroundSource](https://docs.byteplus.com/en/docs/12/docs-191862#VirtualBackgroundSource). |


**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.


<span id="IRTCVideo-disablevirtualbackground"></span>
### DisableVirtualBackground

```c#
int bytertc.IRTCVideo.DisableVirtualBackground()
```


Turns off the virtual background.

**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.


**Notes**

After calling [EnableVirtualBackground](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-enablevirtualbackground) to enable the virtual background function, you can call this API to turn it off.

<span id="IRTCVideo-videosdkenablefacedetection"></span>
### VideoSDKEnableFaceDetection

```c#
int bytertc.IRTCVideo.VideoSDKEnableFaceDetection(
    uint interval_ms,
    string face_model_path
)
```


Starts face detection and registers the observer for the result. With this observer, you will receive [OnFaceDetectResultEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onfacedetectresulteventhandler) periodically.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|interval_ms |uint |The minimum time interval between two callbacks in milliseconds. The value should be greater than 0. The actual time interval is between interval_ms and interval_ms+the time slot of a captured video frame. |
|face_model_path |string |The absolute path of the face detection algorithm file. Typically it is the tt_face_vXXX.model file in the ttfacemodel folder. |


**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* \-1004: Initializing. This function will be available when the initialization is completed.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.


<span id="IRTCVideo-videosdkdisablefacedetection"></span>
### VideoSDKDisableFaceDetection

```c#
int bytertc.IRTCVideo.VideoSDKDisableFaceDetection()
```


Stops face detection.

**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.


<span id="IRTCVideo-setvideodigitalzoomconfig"></span>
### SetVideoDigitalZoomConfig

```c#
int bytertc.IRTCVideo.SetVideoDigitalZoomConfig(
    ZoomConfigType type,
    float size
)
```


> Available since 3.51


Set the step size for each digital zooming control to the local videos.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |ZoomConfigType |Required. Identifying which type the `size` is referring to. Refer to [ZoomConfigType](https://docs.byteplus.com/en/docs/12/docs-191862#ZoomConfigType). |
|size |float |Required. Reserved to three decimal places. It defaults to `0`. The meaning and range vary from different `type`s. If the scale or moving distance exceeds the range, the limit is taken as the result.<br><br><br>* `kZoomConfigTypeFocusOffset`: Increasement or decrease to the scaling factor. Range: [0, 7]. For example, when it is set to 0.5 and [SetVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setvideodigitalzoomcontrol) is called to zoom in, the scale will increase `0.5`. The scale ranges [1，8] and defaults to `1`, which means an original size.<br><br>* `kZoomConfigTypeMoveOffset`：Ratio of the distance to the border of video images. It ranges [0, 0.5] and defaults to `0`, which means no offset. When you call [SetVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setvideodigitalzoomcontrol) and choose `CAMERA_MOVE_LEFT`, the moving distance is size x original width. While for the `CAMERA_MOVE_UP`, the moving distance is size x original height. Suppose that a video spans 1080 px and the `size` is set to `0.5` so that the distance would be 0.5 x 1080 px = 540 px. |


**Return Value**


* 0: Success.

* ! 0: Failure.


**Notes**


* Only one size can be set for a single call. You must call this API to pass values respectively if you intend to set multiple `size`s.

* As the default `size` is `0`, you must call this API before performing any digital zoom control by calling [SetVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setvideodigitalzoomcontrol) or [StartVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-startvideodigitalzoomcontrol).


<span id="IRTCVideo-setvideodigitalzoomcontrol"></span>
### SetVideoDigitalZoomControl

```c#
int bytertc.IRTCVideo.SetVideoDigitalZoomControl(ZoomDirectionType direction)
```


> Available since 3.51


Digital zoom or move the local video image once. This action affects both the video preview locally and the stream published.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|direction |ZoomDirectionType |Action of the digital zoom control. Refer to [ZoomDirectionType](https://docs.byteplus.com/en/docs/12/docs-191862#ZoomDirectionType). |


**Return Value**


* 0: Success.

* ! 0: Failure.


**Notes**


* As the default offset is `0`, you must call [SetVideoDigitalZoomConfig](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setvideodigitalzoomconfig) before this API.

* You can only move video images after they are magnified via this API or [StartVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-startvideodigitalzoomcontrol).

* When you request an out\-of\-range scale or movement, SDK will execute it with the limits. For example, when the image has been moved to the border, the image cannot be zoomed out, or has been magnified to 8x.

* Call [StartVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-startvideodigitalzoomcontrol) to have a continuous and repeatedly digital zoom control.


<span id="IRTCVideo-startvideodigitalzoomcontrol"></span>
### StartVideoDigitalZoomControl

```c#
int bytertc.IRTCVideo.StartVideoDigitalZoomControl(ZoomDirectionType direction)
```


> Available since 3.51


Continuous and repeatedly digital zoom control. This action effect both the video preview locally and the stream published.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|direction |ZoomDirectionType |Action of the digital zoom control. Refer to [ZoomDirectionType](https://docs.byteplus.com/en/docs/12/docs-191862#ZoomDirectionType). |


**Return Value**


* 0: Success.

* ! 0: Failure.


<span id="IRTCVideo-stopvideodigitalzoomcontrol"></span>
### StopVideoDigitalZoomControl

```c#
int bytertc.IRTCVideo.StopVideoDigitalZoomControl()
```


> Available since 3.51


Stop the ongoing digital zoom control instantly.

**Return Value**


* 0: Success.

* ! 0: Failure.


**Notes**

Refer to [StartVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-startvideodigitalzoomcontrol) for starting digital zooming.

<span id="IRTCVideo-setearmonitormode"></span>
### SetEarMonitorMode

```c#
void bytertc.IRTCVideo.SetEarMonitorMode(EarMonitorMode mode)
```


Enable/Disable in\-ear monitoring.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mode |EarMonitorMode |Whether or not in\-ear monitoring is enabled. See [EarMonitorMode](https://docs.byteplus.com/en/docs/12/docs-191862#EarMonitorMode). |


<span id="IRTCVideo-setearmonitorvolume"></span>
### SetEarMonitorVolume

```c#
void bytertc.IRTCVideo.SetEarMonitorVolume(int volume)
```


Set the monitoring volume.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|volume |int |The monitoring volume with the adjustment range between 0% and 100%. |


**Notes**

Call [SetEarMonitorMode](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setearmonitormode) before setting the volume.

<span id="IRTCVideo-enablevocalinstrumentbalance"></span>
### EnableVocalInstrumentBalance

```c#
void bytertc.IRTCVideo.EnableVocalInstrumentBalance(bool enable)
```


Enables/disables the loudness equalization function. If you call this API with the parameter set to True, the loudness of user's voice will be adjusted to \-16lufs.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|enable |bool |Whether to enable loudness equalization funcion:<br><br><br>* True: Yes<br><br>* False: No |


<span id="IRTCVideo-setremoteaudioplaybackvolume"></span>
### SetRemoteAudioPlaybackVolume

```c#
int bytertc.IRTCVideo.SetRemoteAudioPlaybackVolume(
    string roomID,
    string userID,
    int volume
)
```


Adjusts the audio playback volume from the specified remote user, the default is 100.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |The room ID of the remote user |
|userID |string |Remote user ID of the audio source |
|volume |int |Playback volume, adjustment range: [0,400]<br><br><br>* 0: mute<br><br>* 100: original volume<br><br>* 400: Maximum can be 4 times the original volume (with overflow protection) |


<span id="IRTCVideo-setdefaultaudioroute"></span>
### SetDefaultAudioRoute

```c#
int bytertc.IRTCVideo.SetDefaultAudioRoute(AudioRouteDevice route)
```


Set the speaker or earpiece as the default audio playback device.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|route |AudioRouteDevice |Audio playback device. Refer to [AudioRouteDevice](https://docs.byteplus.com/en/docs/12/docs-191862#AudioRouteDevice). You can only use earpiece and speakerphone. |


**Return Value**


* 0: Success.

* < 0: failure. It fails when the device designated is neither a speaker nor an earpiece.


**Notes**

For the default audio route switching strategy of the RTC SDK, see [Set the Audio Route](https://docs.byteplus.com/byteplus-rtc/docs/117836).

<span id="IRTCVideo-setaudioroute"></span>
### SetAudioRoute

```c#
int bytertc.IRTCVideo.SetAudioRoute(AudioRouteDevice device)
```


Designate the device as the current audio playback device. When the audio playback route changes, you will get notified via [OnAudioRouteChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onaudioroutechangedeventhandler).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|device |AudioRouteDevice |Audio route. Refer to [AudioRouteDevice](https://docs.byteplus.com/en/docs/12/docs-191862#AudioRouteDevice) for more details. You cannot choose `AudioRouteUnknown`. You cannot choose `AudioRouteEarpiece` except in the communication audio mode. You can choose `AudioRouteHeadsetBluetooth` or `AudioRouteHeadsetUSB` except in the communication audio mode. |


**Return Value**


* 0: Success

* < 0: Failure


<span id="IRTCVideo-getaudioroute"></span>
### GetAudioRoute

```c#
AudioRouteDevice bytertc.IRTCVideo.GetAudioRoute()
```


Get the information of currently\-using playback route.

**Return Value**

See [AudioRouteDevice](https://docs.byteplus.com/en/docs/12/docs-191862#AudioRouteDevice).

**Notes**

To set the audio playback route, see [SetAudioRoute](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-setaudioroute).

<span id="IRTCVideo-enableaudioframecallback"></span>
### EnableAudioFrameCallback

```c#
int bytertc.IRTCVideo.EnableAudioFrameCallback(
    AudioFrameCallbackMethod method,
    AudioFormat format
)
```


Enable audio frames callback and set the format for the specified type of audio frames.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|method |AudioFrameCallbackMethod |Audio data callback method. See [AudioFrameCallbackMethod](https://docs.byteplus.com/en/docs/12/docs-191862#AudioFrameCallbackMethod) for the callback enabled by each `method`. Multiple API calls would be required if you want to enable or configure different types of callbacks. If `method` is set as `kAudioFrameCallbackRecord`, `kAudioFrameCallbackPlayback`, or `kAudioFrameCallbackMixed`、`kAudioFrameCallbackRecordScreen`, set `format` to the accurate value listed in the audio parameters format. If `method` is set as `kAudioFrameCallbackRemoteUser`, set `format` to `auto`. |
|format |AudioFormat |Audio parameters format. See [AudioFormat](https://docs.byteplus.com/en/docs/12/docs-191862#AudioFormat). |


**Return Value**


* 0: Success.

* < 0 : Failure


<span id="IRTCVideo-disableaudioframecallback"></span>
### DisableAudioFrameCallback

```c#
int bytertc.IRTCVideo.DisableAudioFrameCallback(AudioFrameCallbackMethod method)
```


Disables audio data callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|method |AudioFrameCallbackMethod |Audio data callback method. See [AudioFrameCallbackMethod](https://docs.byteplus.com/en/docs/12/docs-191862#AudioFrameCallbackMethod). |


**Return Value**


* 0: Success.

* < 0 : Failure


**Notes**

Call this API after calling [EnableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-enableaudioframecallback).

<span id="IRTCVideo-startaudiorecording"></span>
### StartAudioRecording

```c#
int bytertc.IRTCVideo.StartAudioRecording(AudioRecordingConfig config)
```


Start recording audio communication, and generate the local file. If you call this API before or after joining the room without internal audio capture, then the recording task can still begin but the data will not be recorded in the local files. Only when you call [startAudioCapture](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-startaudiocapture) to enable internal audio capture, the data will be recorded in the local files.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|config |AudioRecordingConfig |See [AudioRecordingConfig](https://docs.byteplus.com/en/docs/12/docs-191862#AudioRecordingConfig). |


**Return Value**


* 0: Success

* \-2: Invalid parameters

* \-3: Not valid in this SDK. Please contact the technical support.


<span id="IRTCVideo-stopaudiorecording"></span>
### StopAudioRecording

```c#
int bytertc.IRTCVideo.StopAudioRecording()
```


Stop audio recording.

**Return Value**


* 0: Success

* <0: Failure


**Notes**

Call [StartAudioRecording](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-startaudiorecording) to start the recording task.

<span id="IRTCVideo-sendstreamsyncinfo"></span>
### SendStreamSyncInfo

```c#
int bytertc.IRTCVideo.SendStreamSyncInfo(
    byte[] data,
    int length,
    int stream_index,
    int repeat_count
)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|data |byte[] |\- |
|length |int |\- |
|stream_index |int |\- |
|repeat_count |int |\- |


<span id="IRTCVideo-sendseimessage"></span>
### SendSEIMessage

```c#
int bytertc.IRTCVideo.SendSEIMessage(
    byte[] data,
    int length,
    int stream_index,
    int repeat_count,
    int sei_mode
)
```


Sends SEI data. In a video call scenario, SEI is sent with the video frame, while in a voice call scenario, SDK will automatically publish a black frame with a resolution of 16 × 16 pixels to carry SEI data.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|data |byte[] |SEI data. |
|length |int |SEI data length. No more than 4 KB SEI data per frame is recommended. |
|stream_index |int |Specifies the type of media stream that carries SEI data. See [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-191862#StreamIndex). In a voice call, you should set this parameter to `kStreamIndexMain`, otherwise the SEI data is discarded and cannot be sent to the remote user. |
|repeat_count |int |Number of times a message is sent repeatedly. The value range is [0, max{29, %{video frame rate}\-1}]. Recommended range: [2,4]. After calling this API, the SEI data will be added to a consecutive `repeat_count+1` number of video frames starting from the current frame. |
|sei_mode |int |SEI sending mode.<br><br><br>* 0: Single\-SEI mode. When you send multiple SEI messages in 1 frame, they will be sent frame by frame in a queue.<br><br>* 1: Multi\-SEI mode. When you send multiple SEI messages in 1 frame, they will be sent together in the next frame. |


**Return Value**


* \>= 0: The number of SEIs to be added to the video frame

* < 0: Failure


<span id="IRTCVideo-enableaudioprocessor"></span>
### EnableAudioProcessor

```c#
int bytertc.IRTCVideo.EnableAudioProcessor(
    AudioProcessorMethod method,
    AudioFormat format
)
```


Enable audio frames callback for custom processing and set the format for the specified type of audio frames.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|method |AudioProcessorMethod |The types of audio frames. See [AudioProcessorMethod](https://docs.byteplus.com/en/docs/12/docs-191862#AudioProcessorMethod). Set this parameter to process multiple types of audio. With different values, you will receive the corresponding callback:<br><br><br>* For locally captured audio, you will receive [OnProcessRecordAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onprocessrecordaudioframeeventhandler).<br><br>* For mixed remote audio, you will receive [OnProcessPlaybackAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onprocessplaybackaudioframeeventhandler).<br><br>* For audio from remote users, you will receive [OnProcessRemoteUserAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onprocessremoteuseraudioframeeventhandler).<br><br>* For SDK\-level in\-ear monitoring audio, you will receive [OnProcessEarMonitorAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onprocessearmonitoraudioframeeventhandler).<br><br>* For shared\-screen audio, you will receive [OnProcessScreenAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onprocessscreenaudioframeeventhandler). |
|format |AudioFormat |The format of audio frames. See [AudioFormat](https://docs.byteplus.com/en/docs/12/docs-191862#AudioFormat). |


**Return Value**


* 0: Success.

* < 0 : Fail.


**Notes**

To disable custom audio processing, call [DisableAudioProcessor](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-disableaudioprocessor).

<span id="IRTCVideo-disableaudioprocessor"></span>
### DisableAudioProcessor

```c#
int bytertc.IRTCVideo.DisableAudioProcessor(AudioProcessorMethod method)
```


Disable custom audio processing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|method |AudioProcessorMethod |Audio Frame type. See [AudioProcessorMethod](https://docs.byteplus.com/en/docs/12/docs-191862#AudioProcessorMethod). |


**Return Value**


* 0: Success.

* < 0 : Fail.


<span id="IRTCVideo-getaudiodevicemanager"></span>
### GetAudioDeviceManager

```c#
IAudioDeviceManager bytertc.IRTCVideo.GetAudioDeviceManager()
```


get audio device test interface

**Return Value**

audio device test interface

<span id="IRTCVideo-getvideodevicemanager"></span>
### GetVideoDeviceManager

```c#
IVideoDeviceManager bytertc.IRTCVideo.GetVideoDeviceManager()
```


Get [IVideoDeviceManager](https://docs.byteplus.com/en/docs/12/35814#IVideoDeviceManager)

**Return Value**

[IVideoDeviceManager](https://docs.byteplus.com/en/docs/12/35814#IVideoDeviceManager)

<span id="IRTCVideo-startvideocapture"></span>
### StartVideoCapture

```c#
void bytertc.IRTCVideo.StartVideoCapture()
```


Enable internal video capture immediately. The default setting is off. Internal video capture refers to: capturing video using the built\-in module. The local client will be informed via [OnVideoDeviceStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onvideodevicestatechangedeventhandler) after starting video capture by calling this API. The remote clients in the room will be informed of the state change via [OnUserStartVideoCaptureEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserstartvideocaptureeventhandler) after the visible client starts video capture by calling this API.

<span id="IRTCVideo-stopvideocapture"></span>
### StopVideoCapture

```c#
void bytertc.IRTCVideo.StopVideoCapture()
```


Disable internal video capture immediately. The default is off. Internal video capture refers to: capturing video using the built\-in module. The local client will be informed via [OnVideoDeviceStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onvideodevicestatechangedeventhandler) after stopping video capture by calling this API. The remote clients in the room will be informed of the state change via [OnUserStopVideoCaptureEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserstopvideocaptureeventhandler) after the visible client stops video capture by calling this API.

<span id="IRTCVideo-setvideocaptureconfig"></span>
### SetVideoCaptureConfig

```c#
int bytertc.IRTCVideo.SetVideoCaptureConfig(VideoCaptureConfig videoCaptureConfig)
```


Set the video capture parameters for internal capture of the RTC SDK. If your project uses the SDK internal capture module, you can specify the video capture parameters including preference, resolution and frame rate through this interface.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|videoCaptureConfig |VideoCaptureConfig |Video capture parameters. See: [VideoCaptureConfig](https://docs.byteplus.com/en/docs/12/docs-191862#VideoCaptureConfig). |


**Return Value**


* 0: Success;

* < 0: Failure;


<span id="IRTCVideo-setvideoencoderconfig1"></span>
### SetVideoEncoderConfig1

```c#
int bytertc.IRTCVideo.SetVideoEncoderConfig1(VideoEncoderConfig maxSolution)
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|maxSolution |VideoEncoderConfig |\- |


<span id="IRTCVideo-setscreenvideoencoderconfig"></span>
### SetScreenVideoEncoderConfig

```c#
int bytertc.IRTCVideo.SetScreenVideoEncoderConfig(ScreenVideoEncoderConfig screenSolution)
```


Video publisher call this API to set the expected configurations for the screen sharing video stream, including resolution, frame rate, bitrate, scale mode, and fallback strategy in poor network conditions.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|screenSolution |ScreenVideoEncoderConfig |You expected configurations for screen sharing video stream. See [ScreenVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-191862#ScreenVideoEncoderConfig). |


**Return Value**

API call result:


* 0: Success

* ! 0: Failure


**Notes**

Without calling this API, the default encoding parameters for screen sharing video streams are: resolution 1920px × 1080px, frame rate 15fps.

<span id="IRTCVideo-setvideosourcetype"></span>
### SetVideoSourceType

```c#
void bytertc.IRTCVideo.SetVideoSourceType(
    StreamIndex streamIndex,
    VideoSourceType type
)
```


Set the video source, including the screen recordings. The internal video capture is the default, which refers to capturing video using the built\-in module.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamIndex |StreamIndex |Stream index. Refer to [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-191862#StreamIndex) for more details. |
|type |VideoSourceType |Video source type. Refer to [VideoSourceType](https://docs.byteplus.com/en/docs/12/docs-191862#VideoSourceType) for more details. |


<span id="IRTCVideo-setlocalvideomirrortype"></span>
### SetLocalVideoMirrorType

```c#
void bytertc.IRTCVideo.SetLocalVideoMirrorType(MirrorType mirrorType)
```


Sets the mirror mode for the captured video stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mirrorType |MirrorType |Mirror type. See [MirrorType](https://docs.byteplus.com/en/docs/12/docs-191862#MirrorType). |


<span id="IRTCVideo-setvideorotationmode"></span>
### SetVideoRotationMode

```c#
int bytertc.IRTCVideo.SetVideoRotationMode(VideoRotationMode rotationMode)
```


Set the orientation of the video capture. By default, the App direction is used as the orientation reference. During rendering, the receiving client rotates the video in the same way as the sending client did.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rotationMode |VideoRotationMode |Rotation reference can be the orientation of the App or gravity. Refer to [VideoRotationMode](https://docs.byteplus.com/en/docs/12/docs-191862#VideoRotationMode) for details. |


**Return Value**


* 0: Success

* <0: Failure


<span id="IRTCVideo-setlocalvideosink"></span>
### SetLocalVideoSink

```c#
void bytertc.IRTCVideo.SetLocalVideoSink(
    StreamIndex index,
    VideoSinkPixelFormat requiredFormat
)
```


Binds the local video stream to a custom renderer.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|index |StreamIndex |Video stream type. See [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-191862#StreamIndex). |
|requiredFormat |VideoSinkPixelFormat |Video frame encoding format that applys to custom rendering. See [VideoSinkPixelFormat](https://docs.byteplus.com/en/docs/12/docs-191862#VideoSinkPixelFormat). |


<span id="IRTCVideo-setremotevideosink"></span>
### SetRemoteVideoSink

```c#
void bytertc.IRTCVideo.SetRemoteVideoSink(
    RemoteStreamKey streamKey,
    VideoSinkPixelFormat requiredFormat
)
```


Binds the remote video stream to a custom renderer.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamKey |RemoteStreamKey |Remote stream information which specifies the source and type of the video stream to be rendered. See [RemoteStreamKey](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteStreamKey) |
|requiredFormat |VideoSinkPixelFormat |Encoding format that applies to the custom renderer. See [VideoSinkPixelFormat](https://docs.byteplus.com/en/docs/12/docs-191862#VideoSinkPixelFormat) |


<span id="IRTCVideo-getscreencapturesourcelist"></span>
### GetScreenCaptureSourceList

```c#
IScreenCaptureSourceList bytertc.IRTCVideo.GetScreenCaptureSourceList()
```


Get the list of shared objects (application windows and desktops), after using it, you need to call the corresponding release interface to release

**Return Value**

Screen capture sources. See [IScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/35814#IScreenCaptureSourceList).

<span id="IRTCVideo-startscreenvideocapture"></span>
### StartScreenVideoCapture

```c#
int bytertc.IRTCVideo.StartScreenVideoCapture(
    ScreenCaptureSourceInfo sourceInfo,
    ScreenCaptureParameters captureParams
)
```


Use the capture module provided by the RTC SDK to capture the current screen video stream for sharing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|sourceInfo |ScreenCaptureSourceInfo |See [ScreenCaptureSourceInfo](https://docs.byteplus.com/en/docs/12/docs-191862#ScreenCaptureSourceInfo). |
|captureParams |ScreenCaptureParameters |See [ScreenCaptureParameters](https://docs.byteplus.com/en/docs/12/docs-191862#ScreenCaptureParameters). |


**Return Value**


* 0: Success.

* \-1: Failure.


<span id="IRTCVideo-stopscreenvideocapture"></span>
### StopScreenVideoCapture

```c#
void bytertc.IRTCVideo.StopScreenVideoCapture()
```


Stop screen video stream capture.

**Return Value**


* 0: Call succeeded

* \-1: Failure


**Notes**

Calling this interface does not affect on\-screen video stream publishing.

<span id="IRTCVideo-updatescreencaptureregion"></span>
### UpdateScreenCaptureRegion

```c#
void bytertc.IRTCVideo.UpdateScreenCaptureRegion(Rectangle regionRect)
```


Update the capture area when capturing screen video streams through the capture module provided by the RTC SDK.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|regionRect |Rectangle |Acquisition area. See [Rectangle](https://docs.byteplus.com/en/docs/12/docs-191862#Rectangle) This parameter describes the acquisition area after calling this interface, and the relative relationship between the 'source_info' setting area in [StartScreenVideoCapture](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-startscreenvideocapture). |


**Notes**

Before calling this interface, internal screen stream capture must have been turned on by calling [StartScreenVideoCapture](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-startscreenvideocapture).

<span id="IRTCVideo-updatescreencapturehighlightconfig"></span>
### UpdateScreenCaptureHighlightConfig

```c#
void bytertc.IRTCVideo.UpdateScreenCaptureHighlightConfig(HighlightConfig highlightConfig)
```


Update border highlighting settings when capturing screen video streams through the capture module provided by the RTC SDK. The default display table box.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|highlightConfig |HighlightConfig |Border highlighting settings. See [HighlightConfig](https://docs.byteplus.com/en/docs/12/docs-191862#HighlightConfig) |


**Notes**

Before calling this interface, you must have turned on internal screen flow collection by calling [StartScreenVideoCapture](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-startscreenvideocapture).

<span id="IRTCVideo-updatescreencapturemousecursor"></span>
### UpdateScreenCaptureMouseCursor

```c#
void bytertc.IRTCVideo.UpdateScreenCaptureMouseCursor(MouseCursorCaptureState captureMouseCursor)
```


Update the processing settings for the mouse when capturing screen video streams through the capture module provided by the RTC SDK. Default acquisition mouse.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|captureMouseCursor |MouseCursorCaptureState |See [MouseCursorCaptureState](https://docs.byteplus.com/en/docs/12/docs-191862#MouseCursorCaptureState) |


**Notes**

Before calling this interface, internal screen stream capture must have been turned on by calling [StartScreenVideoCapture](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-startscreenvideocapture).

<span id="IRTCVideo-updatescreencapturefilterconfig"></span>
### UpdateScreenCaptureFilterConfig

```c#
void bytertc.IRTCVideo.UpdateScreenCaptureFilterConfig(ScreenFilterConfig filterConfig)
```


When capturing screen video streams through the capture module provided by the RTC SDK, set the window that needs to be filtered.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|filterConfig |ScreenFilterConfig |Window filtering settings. See [ScreenFilterConfig](https://docs.byteplus.com/en/docs/12/docs-191862#ScreenFilterConfig) |


<span id="IRTCVideo-getthumbnail"></span>
### GetThumbnail

```c#
VideoFrame bytertc.IRTCVideo.GetThumbnail(
    ScreenCaptureSourceType type,
    IntPtr sourceID,
    int maxWidth,
    int maxHeight
)
```


Get the shared object thumbnail

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |ScreenCaptureSourceType |Type of the screen capture object. Refer to [ScreenCaptureSourceType](https://docs.byteplus.com/en/docs/12/docs-191862#ScreenCaptureSourceType) for more details. |
|sourceID |IntPtr |ID of the screen\-shared object. |
|maxWidth |int |Maximum width |
|maxHeight |int |Maximum height |


<span id="IRTCVideo-setscreenaudiosourcetype"></span>
### SetScreenAudioSourceType

```c#
void bytertc.IRTCVideo.SetScreenAudioSourceType(AudioSourceType sourceType)
```


Sets the screen audio source type. (internal capture/custom capture)

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|sourceType |AudioSourceType |Screen audio source type. See [AudioSourceType](https://docs.byteplus.com/en/docs/12/docs-191862#AudioSourceType). |


<span id="IRTCVideo-setscreenaudiostreamindex"></span>
### SetScreenAudioStreamIndex

```c#
void bytertc.IRTCVideo.SetScreenAudioStreamIndex(StreamIndex index)
```


Set the mixing mode of the screen audio stream and the audio stream collected by the microphone during screen sharing

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|index |StreamIndex |Mixing mode. See [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-191862#StreamIndex)<br><br><br>* 'kStreamIndexMain': Mixing the screen audio stream and the audio stream collected by the microphone<br><br>* 'kStreamIndexScreen': Divide the screen audio stream and the audio stream collected by the microphone into two audio streams |


**Notes**

You should call this method before [PublishScreen](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-publishscreen). Otherwise, you will receive an error from [OnWarningEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onwarningeventhandler): 'WARNING_CODE_SET_SCREEN_STREAM_INDEX_FAILED

<span id="IRTCVideo-startscreenaudiocapture"></span>
### StartScreenAudioCapture

```c#
void bytertc.IRTCVideo.StartScreenAudioCapture()
```


When sharing the screen, start using the RTC SDK internal acquisition method to capture the screen audio

<span id="IRTCVideo-stopscreenaudiocapture"></span>
### StopScreenAudioCapture

```c#
void bytertc.IRTCVideo.StopScreenAudioCapture()
```


Stop using RTC SDK internal capture method to capture screen audio during screen sharing.

<span id="IRTCVideo-startscreencapture"></span>
### StartScreenCapture

```c#
void bytertc.IRTCVideo.StartScreenCapture(
    ScreenMediaType type,
    string bundleId
)
```


Starts capturing the screen audio and/or video stream with the RTC SDK internal module.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |ScreenMediaType |Media type. See [ByteRTCScreenMediaType](https://docs.byteplus.com/en/docs/12/docs-191862#ScreenMediaType). |
|bundleId |string |The bundle ID of the Extension, which is used to only display your Extension in your app. |


<span id="IRTCVideo-pushscreenaudioframe"></span>
### PushScreenAudioFrame

```c#
int bytertc.IRTCVideo.PushScreenAudioFrame(AudioFrame frame)
```


Using a custom capture method, when capturing screen audio during screen sharing, push the audio frame to the RTC SDK for encoding and other processing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|frame |AudioFrame |Audio data frame. See [AudioFrame](https://docs.byteplus.com/en/docs/12/docs-191862#AudioFrame) |


**Return Value**


* 0: Success.

* < 0: Failure.


<span id="IRTCVideo-switchcamera"></span>
### SwitchCamera

```c#
int bytertc.IRTCVideo.SwitchCamera(CameraID cameraId)
```


Toggle the front/postcondition camera used for internal video capture After calling this interface, [OnVideoDeviceStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onvideodevicestatechangedeventhandler) callback will be triggered locally.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|cameraId |CameraID |Camera ID, mobile end camera. See [CameraID](https://docs.byteplus.com/en/docs/12/docs-191862#CameraID). |


**Return Value**


* 0: Success.

* !0: Failure.


<span id="IRTCVideo-pushexternalaudioframe"></span>
### PushExternalAudioFrame

```c#
int bytertc.IRTCVideo.PushExternalAudioFrame(AudioFrame frame)
```


Push custom captured audio data to the RTC SDK.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|frame |AudioFrame |Audio data frame. See [AudioFrame](https://docs.byteplus.com/en/docs/12/docs-191862#AudioFrame). |


**Return Value**


* 0: Success.

* < 0: Failure.


<span id="IRTCVideo-setaudiosourcetype"></span>
### SetAudioSourceType

```c#
void bytertc.IRTCVideo.SetAudioSourceType(AudioSourceType sourceType)
```


Switch the audio capture type.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|sourceType |AudioSourceType |Audio input source type. See [AudioSourceType](https://docs.byteplus.com/en/docs/12/docs-191862#AudioSourceType) Use internal audio capture by default. The audio capture type and the audio render type may be different from each other. |


**Return Value**


* ≥0: Success.

* \-1: Failure.


<span id="IRTCVideo-pushexternalvideoframe"></span>
### PushExternalVideoFrame

```c#
int bytertc.IRTCVideo.PushExternalVideoFrame(VideoFrame frame)
```


Push external video frames.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|frame |VideoFrame |The data information of the video frame. See [VideoFrame](https://docs.byteplus.com/en/docs/12/docs-191862#VideoFrame). |


**Return Value**


* 0: success

* \-1: failure


<span id="IRTCVideo-pushscreenvideoframe"></span>
### PushScreenVideoFrame

```c#
int bytertc.IRTCVideo.PushScreenVideoFrame(VideoFrame frame)
```


Push screen video frame.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|frame |VideoFrame |Video frame [VideoFrame](https://docs.byteplus.com/en/docs/12/docs-191862#VideoFrame) |


**Return Value**


* 0: call succeeded

* \-1: Failure


<span id="IAudioDeviceManager"></span>
# IAudioDeviceManager

```c#
interface bytertc::IAudioDeviceManager
```


Audio device management.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|IDeviceCollection |[EnumerateAudioPlaybackDevices](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-enumerateaudioplaybackdevices) |
|IDeviceCollection |[EnumerateAudioCaptureDevices](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-enumerateaudiocapturedevices) |
|void |[FollowSystemPlaybackDevice](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-followsystemplaybackdevice) |
|void |[FollowSystemCaptureDevice](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-followsystemcapturedevice) |
|int |[SetAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-setaudioplaybackdevice) |
|int |[SetAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-setaudiocapturedevice) |
|int |[SetAudioPlaybackDeviceVolume](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-setaudioplaybackdevicevolume) |
|int |[GetAudioPlaybackDeviceVolume](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-getaudioplaybackdevicevolume) |
|int |[SetAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-setaudiocapturedevicevolume) |
|int |[GetAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-getaudiocapturedevicevolume) |
|int |[SetAudioPlaybackDeviceMute](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-setaudioplaybackdevicemute) |
|int |[GetAudioPlaybackDeviceMute](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-getaudioplaybackdevicemute) |
|int |[SetAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-setaudiocapturedevicemute) |
|int |[GetAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-getaudiocapturedevicemute) |
|int |[GetAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-getaudioplaybackdevice) |
|int |[GetAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-getaudiocapturedevice) |


<span id="instructions"></span>
## Instructions

<span id="IAudioDeviceManager-enumerateaudioplaybackdevices"></span>
### EnumerateAudioPlaybackDevices

```c#
IDeviceCollection bytertc.IAudioDeviceManager.EnumerateAudioPlaybackDevices()
```


Gets a list of the audio playback device. If there are subsequent device changes, you need to call this interface again to get a new device list.

**Return Value**

A list of all audio playback devices. See [IDeviceCollection](https://docs.byteplus.com/en/docs/12/35814#IDeviceCollection).

<span id="IAudioDeviceManager-enumerateaudiocapturedevices"></span>
### EnumerateAudioCaptureDevices

```c#
IDeviceCollection bytertc.IAudioDeviceManager.EnumerateAudioCaptureDevices()
```


Get a list of audio acquisition devices in the current system. If there are subsequent device changes, you need to call this interface again to get a new device list.

**Return Value**

An object that contains a list of all audio capture devices in the system. See [IDeviceCollection](https://docs.byteplus.com/en/docs/12/35814#IDeviceCollection).

<span id="IAudioDeviceManager-followsystemplaybackdevice"></span>
### FollowSystemPlaybackDevice

```c#
void bytertc.IAudioDeviceManager.FollowSystemPlaybackDevice(Boolean followed)
```


Set the audio playback device to follow the OS default setting or not.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|followed |Boolean |* true: follow the os default setting. You can not call [SetAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-setaudioplaybackdevice) at the same time.<br><br>* false: do not follow the os default setting. You can call [SetAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-setaudioplaybackdevice) to set the audio playback device. |


<span id="IAudioDeviceManager-followsystemcapturedevice"></span>
### FollowSystemCaptureDevice

```c#
void bytertc.IAudioDeviceManager.FollowSystemCaptureDevice(Boolean followed)
```


Set the audio capture device to follow the OS default setting or not.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|followed |Boolean |* true: follow the os default setting. You can not call [SetAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-setaudiocapturedevice) at the same time.<br><br>* false: do not follow the os default setting. You can call [SetAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-setaudiocapturedevice) to set the audio capture device. |


<span id="IAudioDeviceManager-setaudioplaybackdevice"></span>
### SetAudioPlaybackDevice

```c#
int bytertc.IAudioDeviceManager.SetAudioPlaybackDevice(string deviceID)
```


Sets the audio playback device.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|deviceID |string |Audio playback device's ID. You can get the ID by calling [EnumerateAudioPlaybackDevices](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-enumerateaudioplaybackdevices). |


**Return Value**


* 0: Success

* < 0: Failure


<span id="IAudioDeviceManager-setaudiocapturedevice"></span>
### SetAudioCaptureDevice

```c#
int bytertc.IAudioDeviceManager.SetAudioCaptureDevice(string deviceID)
```


Set up audio capture devices.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|deviceID |string |Audio capture device ID, available through [EnumerateAudioCaptureDevices](https://docs.byteplus.com/en/docs/12/35814#IAudioDeviceManager-enumerateaudiocapturedevices). |


**Return Value**


* 0: Success.

* < 0: failure


<span id="IAudioDeviceManager-setaudioplaybackdevicevolume"></span>
### SetAudioPlaybackDeviceVolume

```c#
int bytertc.IAudioDeviceManager.SetAudioPlaybackDeviceVolume(uint volume)
```


Sets the current audio playback device volume

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|volume |uint |Audio playback device volume, the value range is [0,255], the setting beyond this range is invalid.<br><br><br>* [0,25] Is nearly silent;<br><br>* [25,75] Is low volume;<br><br>* [76,204] Is medium volume;<br><br>* [205,255] Is high volume. |


**Return Value**


* 0: Success.

* < 0: failure


<span id="IAudioDeviceManager-getaudioplaybackdevicevolume"></span>
### GetAudioPlaybackDeviceVolume

```c#
int bytertc.IAudioDeviceManager.GetAudioPlaybackDeviceVolume(ref uint volume)
```


Get the current audio playback device volume

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|volume |ref uint |Audio playback device volume, the range should be within [0,255].<br><br><br>* [0,25] Is nearly silent;<br><br>* [25,75] Is low volume;<br><br>* [76,204] Is medium volume;<br><br>* [205,255] Is high volume. |


**Return Value**


* 0: Success.

* < 0: failure


<span id="IAudioDeviceManager-setaudiocapturedevicevolume"></span>
### SetAudioCaptureDeviceVolume

```c#
int bytertc.IAudioDeviceManager.SetAudioCaptureDeviceVolume(uint volume)
```


Set the current audio acquisition device volume

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|volume |uint |Audio acquisition device volume, the value range is [0,255], the setting beyond this range is invalid.<br><br><br>* [0,25] Is nearly silent;<br><br>* [25,75] Is low volume;<br><br>* [76,204] Is medium volume;<br><br>* [205,255] Is high volume. |


**Return Value**


* 0: Success. The volume information returned by [OnLocalAudioPropertiesReportEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onlocalaudiopropertiesreporteventhandler) will be changed according to this value.

* < 0: failure


<span id="IAudioDeviceManager-getaudiocapturedevicevolume"></span>
### GetAudioCaptureDeviceVolume

```c#
int bytertc.IAudioDeviceManager.GetAudioCaptureDeviceVolume(ref uint volume)
```


Get the current audio capture device volume

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|volume |ref uint |Audio capture device volume, the range should be within [0,255].<br><br><br>* [0,25] Is nearly silent;<br><br>* [25,75] Is low volume;<br><br>* [76,204] Is medium volume;<br><br>* [205,255] Is high volume. |


**Return Value**


* 0: Success.

* < 0: failure


<span id="IAudioDeviceManager-setaudioplaybackdevicemute"></span>
### SetAudioPlaybackDeviceMute

```c#
int bytertc.IAudioDeviceManager.SetAudioPlaybackDeviceMute(bool mute)
```


Sets the current audio playback device to be mute, and the default is non\-mute.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mute |bool |* True: mute<br><br>* False: non\-mute |


**Return Value**


* 0: Success.

* < 0: failure


<span id="IAudioDeviceManager-getaudioplaybackdevicemute"></span>
### GetAudioPlaybackDeviceMute

```c#
int bytertc.IAudioDeviceManager.GetAudioPlaybackDeviceMute(ref bool mute)
```


Gets information about whether the current audio playback device is muted.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mute |ref bool |* True: mute<br><br>* False: non\-mute |


**Return Value**


* 0: Success.

* < 0: failure


<span id="IAudioDeviceManager-setaudiocapturedevicemute"></span>
### SetAudioCaptureDeviceMute

```c#
int bytertc.IAudioDeviceManager.SetAudioCaptureDeviceMute(bool mute)
```


Sets the current audio acquisition device to be mute, and the default is non\-mute.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mute |bool |* True: mute<br><br>* False: non\-mute |


**Return Value**


* 0: Success.

* < 0: failure


<span id="IAudioDeviceManager-getaudiocapturedevicemute"></span>
### GetAudioCaptureDeviceMute

```c#
int bytertc.IAudioDeviceManager.GetAudioCaptureDeviceMute(ref bool mute)
```


Gets information about whether the current audio capture device is silent.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mute |ref bool |* True: mute<br><br>* False: non\-mute |


**Return Value**


* 0: Success.

* < 0: failure


<span id="IAudioDeviceManager-getaudioplaybackdevice"></span>
### GetAudioPlaybackDevice

```c#
int bytertc.IAudioDeviceManager.GetAudioPlaybackDevice(ref string deviceID)
```


Gets the current audio playback device ID.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|deviceID |ref string |audio playback device ID |


**Return Value**


* 0: Success.

* < 0: failure


<span id="IAudioDeviceManager-getaudiocapturedevice"></span>
### GetAudioCaptureDevice

```c#
int bytertc.IAudioDeviceManager.GetAudioCaptureDevice(ref string deviceID)
```


Gets the current audio capture device ID.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|deviceID |ref string |audio capture device ID, the user is responsible for allocating and freeing memory according to the MAX_DEVICE_ID_LENGTH size |


**Return Value**


* 0: Success.

* < 0: failure


<span id="IDeviceCollection"></span>
# IDeviceCollection

```c#
interface bytertc::IDeviceCollection
```


Audio & video device information

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[GetCount](https://docs.byteplus.com/en/docs/12/35814#IDeviceCollection-getcount) |
|int |[GetDevice](https://docs.byteplus.com/en/docs/12/35814#IDeviceCollection-getdevice) |
|void |[Release](https://docs.byteplus.com/en/docs/12/35814#IDeviceCollection-release) |


<span id="instructions"></span>
## Instructions

<span id="IDeviceCollection-getcount"></span>
### GetCount

```c#
int bytertc.IDeviceCollection.GetCount()
```


Get the number of audio & video devices in the current system

**Return Value**

Number of audio & video devices

<span id="IDeviceCollection-getdevice"></span>
### GetDevice

```c#
int bytertc.IDeviceCollection.GetDevice(
    int index,
    ref string deviceName,
    ref string deviceID
)
```


According to the index number, get device information

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|index |int |Device index number, starting from 0, note that it must be less than the return value of [GetCount](https://docs.byteplus.com/en/docs/12/35814#IDeviceCollection-getcount). |
|deviceName |ref string |device name |
|deviceID |ref string |device ID |


**Return Value**


* 0: Success. \-! 0: failure


<span id="IDeviceCollection-release"></span>
### Release

```c#
void bytertc.IDeviceCollection.Release()
```


Releases the resources occupied by the current [IDeviceCollection](https://docs.byteplus.com/en/docs/12/35814#IDeviceCollection) object.

**Notes**

This method should be called to release related resources when you do not need to return a list of audio & video device related information.

<span id="IRTCVideoRoom"></span>
# IRTCVideoRoom

```c#
interface bytertc::IRTCVideoRoom
```


Room interface.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[Destroy](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-destroy) |
|int |[JoinRoom](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-joinroom) |
|void |[LeaveRoom](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-leaveroom) |
|void |[UpdateToken](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-updatetoken) |
|void |[SetUserVisibility](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-setuservisibility) |
|void |[PublishStream](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-publishstream) |
|void |[UnpublishStream](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-unpublishstream) |
|void |[PublishScreen](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-publishscreen) |
|void |[UnpublishScreen](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-unpublishscreen) |
|void |[SubscribeStream](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-subscribestream) |
|void |[UnsubscribeStream](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-unsubscribestream) |
|int |[StartForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-startforwardstreamtorooms) |
|int |[StopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-stopforwardstreamtorooms) |
|int |[UpdateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-updateforwardstreamtorooms) |
|int |[PauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-pauseforwardstreamtoallrooms) |
|int |[ResumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-resumeforwardstreamtoallrooms) |
|int |[SetMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-setmultideviceavsync) |
|void |[SubscribeScreen](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-subscribescreen) |
|void |[UnsubscribeScreen](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-unsubscribescreen) |
|void |[PauseAllSubscribedStream](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-pauseallsubscribedstream) |
|void |[ResumeAllSubscribedStream](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-resumeallsubscribedstream) |
|int |[SubscribeAllStreams](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-subscribeallstreams) |
|int |[UnsubscribeAllStreams](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-unsubscribeallstreams) |
|IRangeAudio |[GetRangeAudio](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-getrangeaudio) |
|ISpatialAudio |[GetSpatialAudio](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-getspatialaudio) |
|long |[SendUserMessage](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-sendusermessage) |
|long |[SendRoomMessage](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-sendroommessage) |


<span id="instructions"></span>
## Instructions

<span id="IRTCVideoRoom-destroy"></span>
### Destroy

```c#
void bytertc.IRTCVideoRoom.Destroy()
```


Leave and Destroy the room created by calling [CreateRTCRoom](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-creatertcroom).

<span id="IRTCVideoRoom-joinroom"></span>
### JoinRoom

```c#
int bytertc.IRTCVideoRoom.JoinRoom(
    string token,
    UserInfo info,
    MultiRoomConfig roomConfig
)
```


Join the room. Call [CreateRTCRoom](https://docs.byteplus.com/en/docs/12/35814#IRTCVideo-creatertcroom) After creating a room, call this method to join the room and make audio & video calls with other users in the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|token |string |Dynamic key for authentication and verification of users entering the room. You need to bring Token to enter the room. When testing, you can use the console to generate temporary tokens. The official launch requires the use of the key SDK to generate and issue tokens at your server level. Apps with different AppIDs are not interoperable. Make sure that the AppID used to generate the Token is the same as the AppID used to create the engine, otherwise it will cause the join room to fail. |
|info |UserInfo |User information. See [UserInfo](https://docs.byteplus.com/en/docs/12/docs-191862#UserInfo). |
|roomConfig |MultiRoomConfig |Room parameter configuration, set the room mode and whether to automatically publish or subscribe to the flow. See [MultiRoomConfig](https://docs.byteplus.com/en/docs/12/docs-191862#MultiRoomConfig) for the specific configuration mode. |


**Return Value**


* 0: Success.

* \-1: Invalid parameter.

* \-2: Already in the room. After the interface call is successful, as long as the return value of 0 is received and [LeaveRoom](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-leaveroom) is not called successfully, this return value will be triggered when the room entry interface is called again, regardless of whether the filled room ID and user ID are duplicated.

* \-3: Room is empty.


<span id="IRTCVideoRoom-leaveroom"></span>
### LeaveRoom

```c#
void bytertc.IRTCVideoRoom.LeaveRoom()
```


Leave the room. The user calls this method to leave the room, end the call process, and release all call\-related resources. After calling the [JoinRoom](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-joinroom) method to join the room, you must call this method to end the call, otherwise you cannot start the next call. This method can be called regardless of whether it is currently in the room. Repeated calls to this method have no negative impact. This method is an asynchronous operation, and the call returns without actually exiting the room. After you actually exit the room, you will receive a callback notification from [OnLeaveRoomEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onleaveroomeventhandler) locally.

<span id="IRTCVideoRoom-updatetoken"></span>
### UpdateToken

```c#
void bytertc.IRTCVideoRoom.UpdateToken(string token)
```


Update Token. You must call this API to update token to ensure the RTC call to continue when you receive [OnTokenWillExpireEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#ontokenwillexpireeventhandler).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|token |string |Valid token. If the Token is invalid, you will receive [OnRoomStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onroomstatechangedeventhandler) with the error code of `-1010`. |


<span id="IRTCVideoRoom-setuservisibility"></span>
### SetUserVisibility

```c#
void bytertc.IRTCVideoRoom.SetUserVisibility(bool enable)
```


Set the visibility of the user in the room. Visible by default.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|enable |bool |Visibility of the user in the room:<br><br><br>* True: The user can publish media streams. And the other users in the room get informed of the behaviors of the user, such as Joining room, starting video capture, and Leaving room.<br><br>* False: The user cannot publish media streams. And the other users in the room do not get informed of the behaviors of the user, such as joining, starting video capture, or leaving. |


<span id="IRTCVideoRoom-publishstream"></span>
### PublishStream

```c#
void bytertc.IRTCVideoRoom.PublishStream(MediaStreamType type)
```


Publishes media streams captured by camera/microphone in the current room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |MediaStreamType |Media stream type, used for specifying whether to publish audio stream or video stream. See [MediaStreamType](https://docs.byteplus.com/en/docs/12/docs-191862#MediaStreamType). |


<span id="IRTCVideoRoom-unpublishstream"></span>
### UnpublishStream

```c#
void bytertc.IRTCVideoRoom.UnpublishStream(MediaStreamType type)
```


Stops publishing media streams captured by camera/microphone in the current room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |MediaStreamType |Media stream type, used for specifying whether to stop publishing audio stream or video stream. See [MediaStreamType](https://docs.byteplus.com/en/docs/12/docs-191862#MediaStreamType). |


<span id="IRTCVideoRoom-publishscreen"></span>
### PublishScreen

```c#
void bytertc.IRTCVideoRoom.PublishScreen(MediaStreamType type)
```


Publishes local screen sharing streams in the current room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |MediaStreamType |Media stream type, used for specifying whether to publish audio stream or video stream. See [MediaStreamType](https://docs.byteplus.com/en/docs/12/docs-191862#MediaStreamType). |


<span id="IRTCVideoRoom-unpublishscreen"></span>
### UnpublishScreen

```c#
void bytertc.IRTCVideoRoom.UnpublishScreen(MediaStreamType type)
```


Stops publishing local screen sharing streams in the current room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |MediaStreamType |Media stream type, used for specifying whether to publish audio stream or video stream. See [MediaStreamType](https://docs.byteplus.com/en/docs/12/docs-191862#MediaStreamType). |


<span id="IRTCVideoRoom-subscribestream"></span>
### SubscribeStream

```c#
void bytertc.IRTCVideoRoom.SubscribeStream(
    string userID,
    MediaStreamType type
)
```


Subscribes to specific remote media streams captured by camera/microphone. Or update the options of the subscribed user.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|userID |string |ID of the remote user who published the target audio/video stream. |
|type |MediaStreamType |Media stream type, used for specifying whether to subscribe to the audio stream or the video stream. See [MediaStreamType](https://docs.byteplus.com/en/docs/12/docs-191862#MediaStreamType). |


<span id="IRTCVideoRoom-unsubscribestream"></span>
### UnsubscribeStream

```c#
void bytertc.IRTCVideoRoom.UnsubscribeStream(
    string userID,
    MediaStreamType type
)
```


Unsubscribes from specific remote media streams captured by camera/microphone. You can call this API in both automatic subscription mode and manual subscription mode.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|userID |string |The ID of the remote user who published the target audio/video stream. |
|type |MediaStreamType |Media stream type, used for specifying whether to unsubscribe from the audio stream or the video stream. See [MediaStreamType](https://docs.byteplus.com/en/docs/12/docs-191862#MediaStreamType). |


<span id="IRTCVideoRoom-startforwardstreamtorooms"></span>
### StartForwardStreamToRooms

```c#
int bytertc.IRTCVideoRoom.StartForwardStreamToRooms(ForwardStreamConfiguration configuration)
```


Start relaying media stream across rooms. After calling [JoinRoom](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-joinroom), you can call this method to publish the media stream to multiple rooms that applies to scenarios such as anOnline talent contest and so on.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|configuration |ForwardStreamConfiguration |Information of the rooms where you want to relay the media stream to. Refer to [ForwardStreamConfiguration](https://docs.byteplus.com/en/docs/12/docs-191862#ForwardStreamConfiguration) for more information. |


**Return Value**

0: Success <0: Failure

<span id="IRTCVideoRoom-stopforwardstreamtorooms"></span>
### StopForwardStreamToRooms

```c#
int bytertc.IRTCVideoRoom.StopForwardStreamToRooms()
```


Call to this method to stop relaying media stream to all rooms after calling [StartForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-startforwardstreamtorooms).

**Return Value**


* 0: Success.

* < 0 : Fail.


<span id="IRTCVideoRoom-updateforwardstreamtorooms"></span>
### UpdateForwardStreamToRooms

```c#
int bytertc.IRTCVideoRoom.UpdateForwardStreamToRooms(ForwardStreamConfiguration configuration)
```


Update information of the rooms where you want to relay the media stream to after calling [StartForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-startforwardstreamtorooms). Adding and removing rooms by calling this method will trigger [OnForwardStreamStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onforwardstreamstatechangedeventhandler) on the local.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|configuration |ForwardStreamConfiguration |Information of the rooms where you want to relay the media stream to. Refer to [ForwardStreamConfiguration](https://docs.byteplus.com/en/docs/12/docs-191862#ForwardStreamConfiguration) for more information. |


**Return Value**


* 0: Success

* <0: Failure


<span id="IRTCVideoRoom-pauseforwardstreamtoallrooms"></span>
### PauseForwardStreamToAllRooms

```c#
int bytertc.IRTCVideoRoom.PauseForwardStreamToAllRooms()
```


Call this method to pause relaying media stream to all rooms after calling [StartForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-startforwardstreamtorooms). After that, call [ResumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-resumeforwardstreamtoallrooms) to resume.

**Return Value**


* 0: Success.

* < 0 : Fail.


**Notes**

The other users in the room will receive callback of [OnUserUnpublishStreamEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserunpublishstreameventhandler)/ [OnUserUnPublishScreenEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserunpublishscreeneventhandler) and [OnUserLeaveEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserleaveeventhandler) when you pause relaying.

<span id="IRTCVideoRoom-resumeforwardstreamtoallrooms"></span>
### ResumeForwardStreamToAllRooms

```c#
int bytertc.IRTCVideoRoom.ResumeForwardStreamToAllRooms()
```


Call this method to resume relaying to all rooms from the pause by calling [PauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-pauseforwardstreamtoallrooms).

**Return Value**


* 0: Success.

* < 0 : Fail.


**Notes**

The other users in the room will receive callback of [OnUserJoinedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserjoinedeventhandler) and [OnUserPublishStreamEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserpublishstreameventhandler)/ [OnUserPublishScreenEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onuserpublishscreeneventhandler) when you resume relaying.

<span id="IRTCVideoRoom-setmultideviceavsync"></span>
### SetMultiDeviceAVSync

```c#
int bytertc.IRTCVideoRoom.SetMultiDeviceAVSync(string audio_user_id)
```


Synchronizes published audio and video. When the same user simultaneously uses separate devices to capture and publish audio and video, there is a possibility that the streams are out of sync due to the network disparity. In this case, you can call this API on the video publisher side and the SDK will automatically line the video stream up according to the timestamp of the audio stream, ensuring that the audio the receiver hears corresponds to the video the receiver watches.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audio_user_id |string |The ID of audio publisher. You can stop the current A/V synchronization by setting this parameter to null. |


**Return Value**


* 0: Success.

* < 0 : Fail.


<span id="IRTCVideoRoom-subscribescreen"></span>
### SubscribeScreen

```c#
void bytertc.IRTCVideoRoom.SubscribeScreen(
    string userID,
    MediaStreamType type
)
```


Subscribes to specific screen sharing media stream. Or update the subscribe options of the subscribed user.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|userID |string |The ID of the remote user who published the target screen audio/video stream. |
|type |MediaStreamType |Media stream type, used for specifying whether to subscribe to the audio stream or the video stream. See [MediaStreamType](https://docs.byteplus.com/en/docs/12/docs-191862#MediaStreamType). |


<span id="IRTCVideoRoom-unsubscribescreen"></span>
### UnsubscribeScreen

```c#
void bytertc.IRTCVideoRoom.UnsubscribeScreen(
    string userID,
    MediaStreamType type
)
```


Unsubscribes from specific screen sharing media stream. You can call this API in both automatic subscription mode and manual subscription mode.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|userID |string |The ID of the remote user who published the target screen audio/video stream. |
|type |MediaStreamType |Media stream type, used for specifying whether to unsubscribe from the audio stream or the video stream. See [MediaStreamType](https://docs.byteplus.com/en/docs/12/docs-191862#MediaStreamType). |


<span id="IRTCVideoRoom-pauseallsubscribedstream"></span>
### PauseAllSubscribedStream

```c#
void bytertc.IRTCVideoRoom.PauseAllSubscribedStream(PauseResumeControlMediaType mediaType)
```


Pause receiving remote media streams.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mediaType |PauseResumeControlMediaType |Media stream type subscribed to. Refer to [PauseResumeControlMediaType](https://docs.byteplus.com/en/docs/12/docs-191862#PauseResumeControlMediaType). |


<span id="IRTCVideoRoom-resumeallsubscribedstream"></span>
### ResumeAllSubscribedStream

```c#
void bytertc.IRTCVideoRoom.ResumeAllSubscribedStream(PauseResumeControlMediaType mediaType)
```


Resume receiving remote media streams

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mediaType |PauseResumeControlMediaType |Media stream type subscribed to. Refer to [PauseResumeControlMediaType](https://docs.byteplus.com/en/docs/12/docs-191862#PauseResumeControlMediaType) |


<span id="IRTCVideoRoom-subscribeallstreams"></span>
### SubscribeAllStreams

```c#
int bytertc.IRTCVideoRoom.SubscribeAllStreams(MediaStreamType type)
```


Subscribes to all remote media streams captured by camera/microphone. Or update the subscribe options of all subscribed user.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |MediaStreamType |Media stream type, used for specifying whether to subscribe to the audio stream or the video stream. See [MediaStreamType](https://docs.byteplus.com/en/docs/12/docs-191862#MediaStreamType). |


**Return Value**

API call result:


* 0: Success

* !0: Failure


<span id="IRTCVideoRoom-unsubscribeallstreams"></span>
### UnsubscribeAllStreams

```c#
int bytertc.IRTCVideoRoom.UnsubscribeAllStreams(MediaStreamType type)
```


Unsubscribes from all remote media streams captured by camera/microphone. You can call this API to unsubscribe from streams that are subscribed to either automatically or manually.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |MediaStreamType |Media stream type, used for specifying whether to unsubscribe from the audio stream or the video stream. See [MediaStreamType](https://docs.byteplus.com/en/docs/12/docs-191862#MediaStreamType). |


**Return Value**

API call result:


* 0: Success

* !0: Failure


<span id="IRTCVideoRoom-getrangeaudio"></span>
### GetRangeAudio

```c#
IRangeAudio bytertc.IRTCVideoRoom.GetRangeAudio()
```


Gets range audio interfaces.

**Return Value**

Range audio interfaces. See [IRangeAudio](https://docs.byteplus.com/en/docs/12/35814#IRangeAudio).

<span id="IRTCVideoRoom-getspatialaudio"></span>
### GetSpatialAudio

```c#
ISpatialAudio bytertc.IRTCVideoRoom.GetSpatialAudio()
```


Gets spatial audio interfaces.

**Return Value**

Spatial audio interfaces. See [ISpatialAudio](https://docs.byteplus.com/en/docs/12/35814#ISpatialAudio).

<span id="IRTCVideoRoom-sendusermessage"></span>
### SendUserMessage

```c#
long bytertc.IRTCVideoRoom.SendUserMessage(
    string userID,
    string message
)
```


Send a point\-to\-point text message to the specified user in the room

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|userID |string |User ID of the message receiver |
|message |string |Text message content sent. Message does not exceed 64 KB. |


**Return Value**


* \> 0: Sent successfully, return the number of the sent message, increment from 1

* \-1: Sent failed, RTCRoom instance not created

* \-2: Sent failed, userID is empty


**Notes**

Before sending an in\-room text message, you must call [JoinRoom](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-joinroom) to join the room.

<span id="IRTCVideoRoom-sendroommessage"></span>
### SendRoomMessage

```c#
long bytertc.IRTCVideoRoom.SendRoomMessage(string message)
```


Mass text messages to all other users in the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|message |string |The content of the text message sent. The message does not exceed 64 KB. |


**Notes**

Before broadcasting a text message in the room, you must call [JoinRoom](https://docs.byteplus.com/en/docs/12/35814#IRTCVideoRoom-joinroom) to join the room.

<span id="IScreenCaptureSourceList"></span>
# IScreenCaptureSourceList

```c#
interface bytertc::IScreenCaptureSourceList
```


Screen source type information list

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[GetCount](https://docs.byteplus.com/en/docs/12/35814#IScreenCaptureSourceList-getcount) |
|ScreenCaptureSourceInfo |[GetSourceInfo](https://docs.byteplus.com/en/docs/12/35814#IScreenCaptureSourceList-getsourceinfo) |
|void |[Release](https://docs.byteplus.com/en/docs/12/35814#IScreenCaptureSourceList-release) |


<span id="instructions"></span>
## Instructions

<span id="IScreenCaptureSourceList-getcount"></span>
### GetCount

```c#
int bytertc.IScreenCaptureSourceList.GetCount()
```


Get list size

**Return Value**

Get list size

<span id="IScreenCaptureSourceList-getsourceinfo"></span>
### GetSourceInfo

```c#
ScreenCaptureSourceInfo bytertc.IScreenCaptureSourceList.GetSourceInfo(int index)
```


According to the index, get the elements in the screen share list.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|index |int |Index number. |


**Return Value**

Screen source type information. See [ScreenCaptureSourceInfo](https://docs.byteplus.com/en/docs/12/docs-191862#ScreenCaptureSourceInfo).

**Notes**

Return a string of type char\* in the type, which is released after this object is released, please pay attention to memory management.

<span id="IScreenCaptureSourceList-release"></span>
### Release

```c#
void bytertc.IScreenCaptureSourceList.Release()
```


Destruct the current object and free up memory

**Notes**

Call delete the structure is strictly prohibited, this function should be called to free resources when the structure is not needed

<span id="ISpatialAudio"></span>
# ISpatialAudio

```c#
interface bytertc::ISpatialAudio
```


Position audio interface

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[EnableSpatialAudio](https://docs.byteplus.com/en/docs/12/35814#ISpatialAudio-enablespatialaudio) |
|int |[UpdatePosition](https://docs.byteplus.com/en/docs/12/35814#ISpatialAudio-updateposition) |
|int |[UpdateSelfOrientation](https://docs.byteplus.com/en/docs/12/35814#ISpatialAudio-updateselforientation) |
|void |[DisableRemoteOrientation](https://docs.byteplus.com/en/docs/12/35814#ISpatialAudio-disableremoteorientation) |
|void |[Release](https://docs.byteplus.com/en/docs/12/35814#ISpatialAudio-release) |


<span id="instructions"></span>
## Instructions

<span id="ISpatialAudio-enablespatialaudio"></span>
### EnableSpatialAudio

```c#
void bytertc.ISpatialAudio.EnableSpatialAudio(bool enable)
```


Enable or disable spatial audio effects.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|enable |bool |Spatial audio effect switch, off by default.<br><br><br>* True: enable spatial voice;<br><br>* False: disable spatial voice. |


<span id="ISpatialAudio-updateposition"></span>
### UpdatePosition

```c#
int bytertc.ISpatialAudio.UpdatePosition(Position pos)
```


Updates the coordinate of the local user's position as a sound source in the rectangular coordinate system in the current room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|pos |Position |3D coordinate values, the default value is [0, 0, 0], see [Position](https://docs.byteplus.com/en/docs/12/docs-191862#Position). |


**Return Value**


* 0: Success.

* !0: Failure.


**Notes**

Before calling this API, you should call [EnableSpatialAudio](https://docs.byteplus.com/en/docs/12/35814#ISpatialAudio-enablespatialaudio) first to enable spatial audio function.

<span id="ISpatialAudio-updateselforientation"></span>
### UpdateSelfOrientation

```c#
int bytertc.ISpatialAudio.UpdateSelfOrientation(HumanOrientation orientation)
```


Update own orientation. The local orientation setting only affects the audio effects heard locally, not the audio effects emitted locally.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|orientation |HumanOrientation |Orientation information, which must be a unit vector. See [HumanOrientation](https://docs.byteplus.com/en/docs/12/docs-191862#HumanOrientation). When the default value is used for the positive direction of the orientation, the coordinate system of the orientation is the same as the coordinate system used by the position information. At this time, the front facing is: `[1, 0, 0]`, the right facing is: `[0, 1, 0]`, and the top facing is: `[0, 0, 1]`. |


**Return Value**

0: Represents a successful update

**Notes**

The local user calls [EnableSpatialAudio](https://docs.byteplus.com/en/docs/12/35814#ISpatialAudio-enablespatialaudio) When using the spatial audio function, you need to call the [UpdatePosition](https://docs.byteplus.com/en/docs/12/35814#ISpatialAudio-updateposition) interface to update the position coordinates before Call this interface.

<span id="ISpatialAudio-disableremoteorientation"></span>
### DisableRemoteOrientation

```c#
void bytertc.ISpatialAudio.DisableRemoteOrientation()
```


Turn off the effect of the orientation of the local user as the sound source. After the effect is off, all the other users in the room listen to the local user as if the local user is in right front of each of them.

<span id="ISpatialAudio-release"></span>
### Release

```c#
void bytertc.ISpatialAudio.Release()
```


Releases the resources occupied by the current [ISpatialAudio](https://docs.byteplus.com/en/docs/12/35814#ISpatialAudio) object.
