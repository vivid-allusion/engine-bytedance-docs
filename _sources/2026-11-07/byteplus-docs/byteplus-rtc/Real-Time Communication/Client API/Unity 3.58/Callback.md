---
title: "Callback"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-191860"
---

<span id="Public-API"></span>
# Public API

<span id="function"></span>
## Function


|Return |Name |
|---|---|
|delegate void |[OnWarningEventHandler](https://docs.byteplus.com/en/docs/12/35815#onwarningeventhandler) |
|delegate void |[OnErrorEventHandler](https://docs.byteplus.com/en/docs/12/35815#onerroreventhandler) |
|delegate void |[OnLogReportEventHandler](https://docs.byteplus.com/en/docs/12/35815#onlogreporteventhandler) |
|delegate void |[OnConnectionStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onconnectionstatechangedeventhandler) |
|delegate void |[OnNetworkTypeChangedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onnetworktypechangedeventhandler) |
|delegate void |[OnSysStatsEventHandler](https://docs.byteplus.com/en/docs/12/35815#onsysstatseventhandler) |
|delegate void |[OnAudioRouteChangedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onaudioroutechangedeventhandler) |
|delegate void |[OnAudioDeviceStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onaudiodevicestatechangedeventhandler) |
|delegate void |[OnAudioDeviceWarningEventHandler](https://docs.byteplus.com/en/docs/12/35815#onaudiodevicewarningeventhandler) |
|delegate void |[OnLocalAudioPropertiesReportEventHandler](https://docs.byteplus.com/en/docs/12/35815#onlocalaudiopropertiesreporteventhandler) |
|delegate void |[OnRemoteAudioPropertiesReportEventHandler](https://docs.byteplus.com/en/docs/12/35815#onremoteaudiopropertiesreporteventhandler) |
|delegate void |[OnCreateRoomStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/35815#oncreateroomstatechangedeventhandler) |
|delegate void |[OnAudioRecordingStateUpdateEventHandler](https://docs.byteplus.com/en/docs/12/35815#onaudiorecordingstateupdateeventhandler) |
|delegate void |[OnRecordAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/35815#onrecordaudioframeeventhandler) |
|delegate void |[OnPlaybackAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/35815#onplaybackaudioframeeventhandler) |
|delegate void |[OnRemoteUserAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/35815#onremoteuseraudioframeeventhandler) |
|delegate void |[OnMixedAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/35815#onmixedaudioframeeventhandler) |
|delegate void |[OnRecordScreenAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/35815#onrecordscreenaudioframeeventhandler) |
|delegate void |[OnVideoDeviceStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onvideodevicestatechangedeventhandler) |
|delegate void |[OnVideoDeviceWarningEventHandler](https://docs.byteplus.com/en/docs/12/35815#onvideodevicewarningeventhandler) |
|delegate bool |[OnLocalVideoSinkOnFrameEventHandler](https://docs.byteplus.com/en/docs/12/35815#onlocalvideosinkonframeeventhandler) |
|delegate int |[OnLocalVideoSinkGetRenderElapseEventHandler](https://docs.byteplus.com/en/docs/12/35815#onlocalvideosinkgetrenderelapseeventhandler) |
|delegate void |[OnLocalVideoSinkReleaseEventHandler](https://docs.byteplus.com/en/docs/12/35815#onlocalvideosinkreleaseeventhandler) |
|delegate bool |[OnRemoteVideoSinkOnFrameEventHandler](https://docs.byteplus.com/en/docs/12/35815#onremotevideosinkonframeeventhandler) |
|delegate int |[OnRemoteVideoSinkGetRenderElapseEventHandler](https://docs.byteplus.com/en/docs/12/35815#onremotevideosinkgetrenderelapseeventhandler) |
|delegate void |[OnRemoteVideoSinkReleaseEventHandler](https://docs.byteplus.com/en/docs/12/35815#onremotevideosinkreleaseeventhandler) |
|delegate void |[OnUserStartAudioCaptureEventHandler](https://docs.byteplus.com/en/docs/12/35815#onuserstartaudiocaptureeventhandler) |
|delegate void |[OnUserStopAudioCaptureEventHandler](https://docs.byteplus.com/en/docs/12/35815#onuserstopaudiocaptureeventhandler) |
|delegate void |[OnFirstLocalAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/35815#onfirstlocalaudioframeeventhandler) |
|delegate void |[OnLocalAudioStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onlocalaudiostatechangedeventhandler) |
|delegate void |[OnAudioFrameSendStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onaudioframesendstatechangedeventhandler) |
|delegate void |[OnAudioFramePlayStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onaudioframeplaystatechangedeventhandler) |
|delegate int |[OnProcessRecordAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/35815#onprocessrecordaudioframeeventhandler) |
|delegate int |[OnProcessPlaybackAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/35815#onprocessplaybackaudioframeeventhandler) |
|delegate int |[OnProcessRemoteUserAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/35815#onprocessremoteuseraudioframeeventhandler) |
|delegate int |[OnProcessEarMonitorAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/35815#onprocessearmonitoraudioframeeventhandler) |
|delegate int |[OnProcessScreenAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/35815#onprocessscreenaudioframeeventhandler) |
|delegate void |[OnStreamSyncInfoReceivedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onstreamsyncinforeceivedeventhandler) |
|delegate void |[OnSEIMessageReceivedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onseimessagereceivedeventhandler) |
|delegate void |[OnSEIMessageUpdateEventHandler](https://docs.byteplus.com/en/docs/12/35815#onseimessageupdateeventhandler) |
|delegate void |[OnUserStartVideoCaptureEventHandler](https://docs.byteplus.com/en/docs/12/35815#onuserstartvideocaptureeventhandler) |
|delegate void |[OnUserStopVideoCaptureEventHandler](https://docs.byteplus.com/en/docs/12/35815#onuserstopvideocaptureeventhandler) |
|delegate void |[OnFirstLocalVideoFrameCapturedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onfirstlocalvideoframecapturedeventhandler) |
|delegate void |[OnLocalVideoSizeChangedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onlocalvideosizechangedeventhandler) |
|delegate void |[OnLocalVideoStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onlocalvideostatechangedeventhandler) |
|delegate void |[OnVideoFrameSendStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onvideoframesendstatechangedeventhandler) |
|delegate void |[OnScreenVideoFrameSendStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onscreenvideoframesendstatechangedeventhandler) |
|delegate void |[OnVideoFramePlayStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onvideoframeplaystatechangedeventhandler) |
|delegate void |[OnRemoteVideoSizeChangedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onremotevideosizechangedeventhandler) |
|delegate void |[OnRemoteVideoStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onremotevideostatechangedeventhandler) |
|delegate void |[OnRemoteAudioStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onremoteaudiostatechangedeventhandler) |
|delegate void |[OnNetworkQualityEventHandler](https://docs.byteplus.com/en/docs/12/35815#onnetworkqualityeventhandler) |
|delegate void |[OnLocalStreamStatsEventHandler](https://docs.byteplus.com/en/docs/12/35815#onlocalstreamstatseventhandler) |
|delegate void |[OnRemoteStreamStatsEventHandler](https://docs.byteplus.com/en/docs/12/35815#onremotestreamstatseventhandler) |
|delegate void |[OnFirstRemoteVideoFrameDecodedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onfirstremotevideoframedecodedeventhandler) |
|delegate void |[OnFirstRemoteVideoFrameRenderedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onfirstremotevideoframerenderedeventhandler) |
|delegate void |[OnFaceDetectResultEventHandler](https://docs.byteplus.com/en/docs/12/35815#onfacedetectresulteventhandler) |
|delegate void |[OnFirstRemoteAudioFrameEventHandler](https://docs.byteplus.com/en/docs/12/35815#onfirstremoteaudioframeeventhandler) |
|delegate void |[OnRoomStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onroomstatechangedeventhandler) |
|delegate void |[OnStreamStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onstreamstatechangedeventhandler) |
|delegate void |[OnLeaveRoomEventHandler](https://docs.byteplus.com/en/docs/12/35815#onleaveroomeventhandler) |
|delegate void |[OnUserJoinedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onuserjoinedeventhandler) |
|delegate void |[OnUserLeaveEventHandler](https://docs.byteplus.com/en/docs/12/35815#onuserleaveeventhandler) |
|delegate void |[OnRoomMessageReceivedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onroommessagereceivedeventhandler) |
|delegate void |[OnUserMessageReceivedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onusermessagereceivedeventhandler) |
|delegate void |[OnUserMessageSendResultEventHandler](https://docs.byteplus.com/en/docs/12/35815#onusermessagesendresulteventhandler) |
|delegate void |[OnRoomMessageSendResultEventHandler](https://docs.byteplus.com/en/docs/12/35815#onroommessagesendresulteventhandler) |
|delegate void |[OnUserPublishStreamEventHandler](https://docs.byteplus.com/en/docs/12/35815#onuserpublishstreameventhandler) |
|delegate void |[OnUserUnPublishStreamEventHandler](https://docs.byteplus.com/en/docs/12/35815#onuserunpublishstreameventhandler) |
|delegate void |[OnUserPublishScreenEventHandler](https://docs.byteplus.com/en/docs/12/35815#onuserpublishscreeneventhandler) |
|delegate void |[OnUserUnPublishScreenEventHandler](https://docs.byteplus.com/en/docs/12/35815#onuserunpublishscreeneventhandler) |
|delegate void |[OnStreamSubscribedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onstreamsubscribedeventhandler) |
|delegate void |[OnTokenWillExpireEventHandler](https://docs.byteplus.com/en/docs/12/35815#ontokenwillexpireeventhandler) |
|delegate void |[OnAudioStreamBannedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onaudiostreambannedeventhandler) |
|delegate void |[OnVideoStreamBannedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onvideostreambannedeventhandler) |
|delegate void |[OnForwardStreamStateChangedEventHandler](https://docs.byteplus.com/en/docs/12/35815#onforwardstreamstatechangedeventhandler) |
|delegate void |[OnForwardStreamEventEventHandler](https://docs.byteplus.com/en/docs/12/35815#onforwardstreameventeventhandler) |
|delegate void |[OnAVSyncStateChangeCallback](https://docs.byteplus.com/en/docs/12/35815#onavsyncstatechangecallback) |


<span id="instructions"></span>
## Instructions

<span id="onwarningeventhandler"></span>
### OnWarningEventHandler

```c#
delegate void bytertc.OnWarningEventHandler(int warn)
```


Warning callback occurred.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|warn |int |See [WarningCode](https://docs.byteplus.com/en/docs/12/docs-191861#WarningCode). |


**Notes**

SDK A (network or media\-related) warning occurred at the runtime. The SDK usually recovers automatically and warnings can be ignored.

<span id="onerroreventhandler"></span>
### OnErrorEventHandler

```c#
delegate void bytertc.OnErrorEventHandler(int err)
```


Error callback occurred.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|err |int |See [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-191861#ErrorCode). |


**Notes**

SDK An error (network or media related) occurred at runtime. The SDK usually does not recover automatically, and you may need to intervene.

<span id="onlogreporteventhandler"></span>
### OnLogReportEventHandler

```c#
delegate void bytertc.OnLogReportEventHandler(
    string logType,
    string logContent
)
```


Callback this event when logging is reported.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|logType |string |Log type. |
|logContent |string |Log content. |


<span id="onconnectionstatechangedeventhandler"></span>
### OnConnectionStateChangedEventHandler

```c#
delegate void bytertc.OnConnectionStateChangedEventHandler(ConnectionState state)
```


Callback SDK and signaling server connection status related events. Callbacks the event when the network connection state of the SDK to the signaling server changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|state |ConnectionState |The current SDK and signaling server connection status. See [ConnectionState](https://docs.byteplus.com/en/docs/12/docs-191862#ConnectionState). |


**Notes**

Triggers when the signaling server connection state changes, and informs the user of the current connection state and the reason for the change.

<span id="onnetworktypechangedeventhandler"></span>
### OnNetworkTypeChangedEventHandler

```c#
delegate void bytertc.OnNetworkTypeChangedEventHandler(NetworkType type)
```


SDK Current network connection type change callback. Callbacks the event when the current network connection type of the SDK changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |NetworkType |Network type. See [NetworkType](https://docs.byteplus.com/en/docs/12/docs-191862#NetworkType). |


<span id="onsysstatseventhandler"></span>
### OnSysStatsEventHandler

```c#
delegate void bytertc.OnSysStatsEventHandler(SysStats stats)
```


Callbacks occur every 2 seconds to inform the current CPU and memory usage information.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stats |SysStats |CPU and memory information. See [SysStats](https://docs.byteplus.com/en/docs/12/docs-191862#SysStats). |


<span id="onaudioroutechangedeventhandler"></span>
### OnAudioRouteChangedEventHandler

```c#
delegate void bytertc.OnAudioRouteChangedEventHandler(AudioRouteDevice device)
```


Receives this callback when the audio playback route changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|device |AudioRouteDevice |New audio playback route. See [AudioRouteDevice](https://docs.byteplus.com/en/docs/12/docs-191862#AudioRouteDevice). |


**Notes**

To set the audio playback route, see [SetAudioRoute](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setaudioroute).

<span id="onaudiodevicestatechangedeventhandler"></span>
### OnAudioDeviceStateChangedEventHandler

```c#
delegate void bytertc.OnAudioDeviceStateChangedEventHandler(
    string deviceID,
    RTCAudioDeviceType deviceType,
    MediaDeviceState deviceState,
    MediaDeviceError deviceError
)
```


Audio device state callback, returns the state of audio capture and audio playback devices.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|deviceID |string |Device ID |
|deviceType |RTCAudioDeviceType |Device type. See [RTCAudioDeviceType](https://docs.byteplus.com/en/docs/12/docs-191862#RTCAudioDeviceType). |
|deviceState |MediaDeviceState |Device state. See [MediaDeviceState](https://docs.byteplus.com/en/docs/12/docs-191862#MediaDeviceState). |
|deviceError |MediaDeviceError |Device error. See [MediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-191862#MediaDeviceError). |


<span id="onaudiodevicewarningeventhandler"></span>
### OnAudioDeviceWarningEventHandler

```c#
delegate void bytertc.OnAudioDeviceWarningEventHandler(
    string deviceID,
    RTCAudioDeviceType deviceType,
    MediaDeviceWarning deviceWarning
)
```


Media device warning callback. The media devices includes: audio capture devices, audio rendering devices, and video capture devices.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|deviceID |string |Device ID |
|deviceType |RTCAudioDeviceType |see [RTCAudioDeviceType](https://docs.byteplus.com/en/docs/12/docs-191862#RTCAudioDeviceType) |
|deviceWarning |MediaDeviceWarning |see [MediaDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-191862#MediaDeviceWarning) |


<span id="onlocalaudiopropertiesreporteventhandler"></span>
### OnLocalAudioPropertiesReportEventHandler

```c#
delegate void bytertc.OnLocalAudioPropertiesReportEventHandler(
    List<LocalAudioPropertiesInfo> audioPropertiesInfos,
    int audioPropertiesInfoNumber
)
```


After calling [EnableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-enableaudiopropertiesreport), you will periodically receive this callback for the information about local audio. Local audio includes the microphone audio and the screen audio captured using RTC SDK internal mechanisms.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioPropertiesInfos |List<LocalAudioPropertiesInfo\> |Local audio properties information. See [LocalAudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/docs-191862#LocalAudioPropertiesInfo). |
|audioPropertiesInfoNumber |int |Audio properties information number. |


<span id="onremoteaudiopropertiesreporteventhandler"></span>
### OnRemoteAudioPropertiesReportEventHandler

```c#
delegate void bytertc.OnRemoteAudioPropertiesReportEventHandler(
    List<RemoteAudioPropertiesInfo> audioPropertiesInfos,
    int audioPropertiesInfoNumber,
    int totalRemoteVolume
)
```


After calling [EnableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-enableaudiopropertiesreport), you will periodically receive this callback for the information about the subscribed remote audio streams. The remote audio streams includes the microphone audio and screen audio collected using the RTC SDK internal mechanism/custom mechanism.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioPropertiesInfos |List<RemoteAudioPropertiesInfo\> |See [RemoteAudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteAudioPropertiesInfo). |
|audioPropertiesInfoNumber |int |Audio properties information number. |
|totalRemoteVolume |int |The total volume of all the subscribed remote streams |


<span id="oncreateroomstatechangedeventhandler"></span>
### OnCreateRoomStateChangedEventHandler

```c#
delegate void bytertc.OnCreateRoomStateChangedEventHandler(
    string room_id,
    int error_code
)
```


Callback on create room failure.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|room_id |string |Room ID. |
|error_code |int |Create room error code. See [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-191861#ErrorCode) for specific indications. |


<span id="onaudiorecordingstateupdateeventhandler"></span>
### OnAudioRecordingStateUpdateEventHandler

```c#
delegate void bytertc.OnAudioRecordingStateUpdateEventHandler(
    AudioRecordingState state,
    AudioRecordingErrorCode error_code
)
```


When calling [StartAudioRecording](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-startaudiorecording) or [StopAudioRecording](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-stopaudiorecording) to change the recording status, receive the callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|state |AudioRecordingState |See [AudioRecordingState](https://docs.byteplus.com/en/docs/12/docs-191862#AudioRecordingState). |
|error_code |AudioRecordingErrorCode |See [AudioRecordingErrorCode](https://docs.byteplus.com/en/docs/12/docs-191861#AudioRecordingErrorCode). |


<span id="onrecordaudioframeeventhandler"></span>
### OnRecordAudioFrameEventHandler

```c#
delegate void bytertc.OnRecordAudioFrameEventHandler(AudioFrame audioFrame)
```


Returns the audio data recorded by local microphone.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrame |AudioFrame |Audio data. See [AudioFrame](https://docs.byteplus.com/en/docs/12/docs-191862#AudioFrame). |


<span id="onplaybackaudioframeeventhandler"></span>
### OnPlaybackAudioFrameEventHandler

```c#
delegate void bytertc.OnPlaybackAudioFrameEventHandler(AudioFrame audioFrame)
```


Returns the mixed audio data of all remote users subscribed by the local user.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrame |AudioFrame |Audio data. See [AudioFrame](https://docs.byteplus.com/en/docs/12/docs-191862#AudioFrame). |


<span id="onremoteuseraudioframeeventhandler"></span>
### OnRemoteUserAudioFrameEventHandler

```c#
delegate void bytertc.OnRemoteUserAudioFrameEventHandler(
    RemoteStreamKey streamInfo,
    AudioFrame audioFrame
)
```


Returns the audio data of one remote user.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamInfo |RemoteStreamKey |Remote stream information. See [RemoteStreamKey](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteStreamKey). |
|audioFrame |AudioFrame |Audio data. See [AudioFrame](https://docs.byteplus.com/en/docs/12/docs-191862#AudioFrame). |


**Notes**

This callback works on the playback thread. Don't do anything time\-consuming in this callback, or it may affect the entire audio playback chain.

<span id="onmixedaudioframeeventhandler"></span>
### OnMixedAudioFrameEventHandler

```c#
delegate void bytertc.OnMixedAudioFrameEventHandler(AudioFrame audioFrame)
```


Returns the mixed audio data including the data recorded by local microphone and that of all remote users subscribed by the local user.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrame |AudioFrame |Audio data. See [AudioFrame](https://docs.byteplus.com/en/docs/12/docs-191862#AudioFrame). |


<span id="onrecordscreenaudioframeeventhandler"></span>
### OnRecordScreenAudioFrameEventHandler

```c#
delegate void bytertc.OnRecordScreenAudioFrameEventHandler(AudioFrame audioFrame)
```


Returns the audio data played locally

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrame |AudioFrame |Audio data. See [AudioFrame](https://docs.byteplus.com/en/docs/12/docs-191862#AudioFrame) |


<span id="onvideodevicestatechangedeventhandler"></span>
### OnVideoDeviceStateChangedEventHandler

```c#
delegate void bytertc.OnVideoDeviceStateChangedEventHandler(
    string deviceID,
    RTCVideoDeviceType deviceType,
    MediaDeviceState deviceState,
    MediaDeviceError deviceError
)
```


Video device state callback, returns the state of video capture and screen capture devices.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|deviceID |string |Device ID. |
|deviceType |RTCVideoDeviceType |Device type. See [RTCVideoDeviceType](https://docs.byteplus.com/en/docs/12/docs-191862#RTCVideoDeviceType). |
|deviceState |MediaDeviceState |Device state. See [MediaDeviceState](https://docs.byteplus.com/en/docs/12/docs-191862#MediaDeviceState). |
|deviceError |MediaDeviceError |Device error. See [MediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-191862#MediaDeviceError). |


<span id="onvideodevicewarningeventhandler"></span>
### OnVideoDeviceWarningEventHandler

```c#
delegate void bytertc.OnVideoDeviceWarningEventHandler(
    string deviceID,
    RTCVideoDeviceType deviceType,
    MediaDeviceWarning deviceWarning
)
```


Video device warning callback, including video capture devices.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|deviceID |string |Device ID |
|deviceType |RTCVideoDeviceType |See [RTCVideoDeviceType](https://docs.byteplus.com/en/docs/12/docs-191862#RTCVideoDeviceType) |
|deviceWarning |MediaDeviceWarning |See [MediaDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-191862#MediaDeviceWarning) |


<span id="onlocalvideosinkonframeeventhandler"></span>
### OnLocalVideoSinkOnFrameEventHandler

```c#
delegate bool bytertc.OnLocalVideoSinkOnFrameEventHandler(
    StreamIndex index,
    VideoFrame videoFrame
)
```


Video frame callback from the cunstom video sink.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|index |StreamIndex |Stream index. See [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-191862#StreamIndex). |
|videoFrame |VideoFrame |Video frame structure. See [VideoFrame](https://docs.byteplus.com/en/docs/12/docs-191862#VideoFrame). |


<span id="onlocalvideosinkgetrenderelapseeventhandler"></span>
### OnLocalVideoSinkGetRenderElapseEventHandler

```c#
delegate int bytertc.OnLocalVideoSinkGetRenderElapseEventHandler(StreamIndex index)
```


Getting external rendering takes time.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|index |StreamIndex |Stream index. See [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-191862#StreamIndex). |


**Return Value**

Average external rendering time in milliseconds.

<span id="onlocalvideosinkreleaseeventhandler"></span>
### OnLocalVideoSinkReleaseEventHandler

```c#
delegate void bytertc.OnLocalVideoSinkReleaseEventHandler(StreamIndex index)
```


Releases the renderer.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|index |StreamIndex |Stream index. See [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-191862#StreamIndex). |


**Notes**

Used to notify the user that the renderer is about to be deprecated. Resources can be released upon receipt of this notification.

<span id="onremotevideosinkonframeeventhandler"></span>
### OnRemoteVideoSinkOnFrameEventHandler

```c#
delegate bool bytertc.OnRemoteVideoSinkOnFrameEventHandler(
    RemoteStreamKey key,
    VideoFrame videoFrame
)
```


Video frame callback from the cunstom video sink.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|key |RemoteStreamKey |Remote stream information. See [RemoteStreamKey](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteStreamKey). |
|videoFrame |VideoFrame |Video frame structure. See [VideoFrame](https://docs.byteplus.com/en/docs/12/docs-191862#VideoFrame). |


<span id="onremotevideosinkgetrenderelapseeventhandler"></span>
### OnRemoteVideoSinkGetRenderElapseEventHandler

```c#
delegate int bytertc.OnRemoteVideoSinkGetRenderElapseEventHandler(RemoteStreamKey key)
```


Getting external rendering takes time.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|key |RemoteStreamKey |Remote stream information. See [RemoteStreamKey](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteStreamKey). |


**Return Value**

Average external rendering time in milliseconds.

<span id="onremotevideosinkreleaseeventhandler"></span>
### OnRemoteVideoSinkReleaseEventHandler

```c#
delegate void bytertc.OnRemoteVideoSinkReleaseEventHandler(RemoteStreamKey key)
```


Releases the renderer.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|key |RemoteStreamKey |Remote stream information. See [RemoteStreamKey](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteStreamKey). |


**Notes**

Used to notify the user that the renderer is about to be deprecated. Resources can be released upon receipt of this notification.

<span id="onuserstartaudiocaptureeventhandler"></span>
### OnUserStartAudioCaptureEventHandler

```c#
delegate void bytertc.OnUserStartAudioCaptureEventHandler(
    string roomID,
    string userID
)
```


The remote clients in the room will be informed of the state change via this callback after the visible user starts audio capture by calling [StartAudioCapture](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-startaudiocapture).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |ID of the room where the remote user enables audio capture. |
|userID |string |The user who starts the internal audio capture. |


<span id="onuserstopaudiocaptureeventhandler"></span>
### OnUserStopAudioCaptureEventHandler

```c#
delegate void bytertc.OnUserStopAudioCaptureEventHandler(
    string roomID,
    string userID
)
```


The remote clients in the room will be informed of the state change via this callback after the visible user stops audio capture by calling [StopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-stopaudiocapture).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |ID of the room where the remote user disables audio capture. |
|userID |string |The user who stops the internal audio capture |


<span id="onfirstlocalaudioframeeventhandler"></span>
### OnFirstLocalAudioFrameEventHandler

```c#
delegate void bytertc.OnFirstLocalAudioFrameEventHandler(StreamIndex index)
```


Receive the callback when the first audio frame is locally collected.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|index |StreamIndex |Audio stream properties. See [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-191862#StreamIndex) |


<span id="onlocalaudiostatechangedeventhandler"></span>
### OnLocalAudioStateChangedEventHandler

```c#
delegate void bytertc.OnLocalAudioStateChangedEventHandler(
    LocalAudioStreamState state,
    LocalAudioStreamError error
)
```


When the state of the local audio stream changes, the callback notifies the current local audio stream state.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|state |LocalAudioStreamState |The status of the local audio device. See [LocalAudioStreamState](https://docs.byteplus.com/en/docs/12/docs-191862#LocalAudioStreamState) |
|error |LocalAudioStreamError |The error code when the state of the local audio stream changes. See [LocalAudioStreamError](https://docs.byteplus.com/en/docs/12/docs-191861#LocalAudioStreamError) |


<span id="onaudioframesendstatechangedeventhandler"></span>
### OnAudioFrameSendStateChangedEventHandler

```c#
delegate void bytertc.OnAudioFrameSendStateChangedEventHandler(
    string roomID,
    RtcUser user,
    FirstFrameSendState state
)
```


Receive this callback when the sending status of the first frame of the local audio changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |ID of the room from which the audio is published. |
|user |RtcUser |Local user information. See [RtcUser](https://docs.byteplus.com/en/docs/12/docs-191862#RtcUser). |
|state |FirstFrameSendState |First frame sending status. See [FirstFrameSendState](https://docs.byteplus.com/en/docs/12/docs-191862#FirstFrameSendState). |


<span id="onaudioframeplaystatechangedeventhandler"></span>
### OnAudioFramePlayStateChangedEventHandler

```c#
delegate void bytertc.OnAudioFramePlayStateChangedEventHandler(
    string roomID,
    RtcUser user,
    FirstFramePlayState state
)
```


Receive this callback when the audio first frame playback state changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |ID of the room from which the audio is published. |
|user |RtcUser |Remote user information. See [RtcUser](https://docs.byteplus.com/en/docs/12/docs-191862#RtcUser) |
|state |FirstFramePlayState |First frame playback status. See [FirstFramePlayState](https://docs.byteplus.com/en/docs/12/docs-191862#FirstFramePlayState) |


<span id="onprocessrecordaudioframeeventhandler"></span>
### OnProcessRecordAudioFrameEventHandler

```c#
delegate int bytertc.OnProcessRecordAudioFrameEventHandler(AudioFrameCallback audioFrameCallback)
```


Returns the address of the locally captured audio frame for custom processing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrameCallback |AudioFrameCallback |The address of the audio frame. See [AudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-191862#AudioFrameCallback) |


<span id="onprocessplaybackaudioframeeventhandler"></span>
### OnProcessPlaybackAudioFrameEventHandler

```c#
delegate int bytertc.OnProcessPlaybackAudioFrameEventHandler(AudioFrameCallback audioFrameCallback)
```


Returns the address of the locally captured audio frame for custom processing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrameCallback |AudioFrameCallback |The address of the audio frame. See [AudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-191862#AudioFrameCallback) |


**Notes**

After calling `enableAudioProcessor` with mixed remote audio, you will receive this callback.

<span id="onprocessremoteuseraudioframeeventhandler"></span>
### OnProcessRemoteUserAudioFrameEventHandler

```c#
delegate int bytertc.OnProcessRemoteUserAudioFrameEventHandler(
    RemoteStreamKey streamInfo,
    AudioFrameCallback audioFrameCallback
)
```


Returns the address of the locally captured audio frame for custom processing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamInfo |RemoteStreamKey |Information of the audio stream. See [RemoteStreamKey](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteStreamKey) |
|audioFrameCallback |AudioFrameCallback |The address of the audio frame. See [AudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-191862#AudioFrameCallback) |


**Notes**

After calling `enableAudioProcessor` with audio streams of the remote users, you will receive this callback.

<span id="onprocessearmonitoraudioframeeventhandler"></span>
### OnProcessEarMonitorAudioFrameEventHandler

```c#
delegate int bytertc.OnProcessEarMonitorAudioFrameEventHandler(AudioFrameCallback audioFrameCallback)
```


Returns the address of the ear monitor audio frame for custom processing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrameCallback |AudioFrameCallback |The address of the audio frame. See [audioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-191862#AudioFrameCallback) |


<span id="onprocessscreenaudioframeeventhandler"></span>
### OnProcessScreenAudioFrameEventHandler

```c#
delegate int bytertc.OnProcessScreenAudioFrameEventHandler(AudioFrameCallback audioFrameCallback)
```


Returns the address of the shared\-screen audio frames for custom processing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrameCallback |AudioFrameCallback |The address of the audio frame. See [AudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-191862#AudioFrameCallback) |


**Notes**

After calling `enableAudioProcessor` to set the audio input to the shared\-screen audio, you will receive this callback.

<span id="onstreamsyncinforeceivedeventhandler"></span>
### OnStreamSyncInfoReceivedEventHandler

```c#
delegate void bytertc.OnStreamSyncInfoReceivedEventHandler(
    RemoteStreamKey stream_key,
    SyncInfoStreamType stream_type,
    byte[] buffer
)
```


audio stream synchronization information callback. You can use this callback to receive audio stream synchronization information sent remotely after the remote user calls [SendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-sendstreamsyncinfo) to send an audio stream synchronization message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_key |RemoteStreamKey |For remote stream information. See [RemoteStreamKey](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteStreamKey). |
|stream_type |SyncInfoStreamType |Media stream type. See [SyncInfoStreamType](https://docs.byteplus.com/en/docs/12/docs-191862#SyncInfoStreamType). |
|buffer |byte[] |Message content. |


<span id="onseimessagereceivedeventhandler"></span>
### OnSEIMessageReceivedEventHandler

```c#
delegate void bytertc.OnSEIMessageReceivedEventHandler(
    RemoteStreamKey stream_key,
    byte[] buffer
)
```


Receive this callback when you receive a video frame with a SEI message sent by calling [SendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-sendseimessage)

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_key |RemoteStreamKey |Contains the user name, room name and media stream of the SEI sender, as detailed in [RemoteStreamKey](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteStreamKey) |
|buffer |byte[] |Received SEI message content |


<span id="onseimessageupdateeventhandler"></span>
### OnSEIMessageUpdateEventHandler

```c#
delegate void bytertc.OnSEIMessageUpdateEventHandler(
    RemoteStreamKey stream_key,
    SEIStreamEventType type
)
```


Callback about publishing status of the black frame video stream . In a voice call scenario, when the local user calls [SendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-sendseimessage) to send SEI data with a black frame, the sending status of the stream is notified to the remote user through this callback. You can tell from this callback that the video frame carrying SEI data is a black frame and thus not render that video frame.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_key |RemoteStreamKey |Information about stream from the remote user, see [RemoteStreamKey](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteStreamKey). |
|type |SEIStreamEventType |State of the black frame video stream, see [SEIStreamEventType](https://docs.byteplus.com/en/docs/12/docs-191862#SEIStreamEventType). |


<span id="onuserstartvideocaptureeventhandler"></span>
### OnUserStartVideoCaptureEventHandler

```c#
delegate void bytertc.OnUserStartVideoCaptureEventHandler(
    string roomID,
    string userID
)
```


The remote clients in the room will be informed of the state change via this callback after the visible user starts video capture by calling [StartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-startvideocapture).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |ID of the room where the remote user enables video capture. |
|userID |string |The user who starts the internal video capture. |


<span id="onuserstopvideocaptureeventhandler"></span>
### OnUserStopVideoCaptureEventHandler

```c#
delegate void bytertc.OnUserStopVideoCaptureEventHandler(
    string roomID,
    string userID
)
```


The remote clients in the room will be informed of the state change via this callback after the visible user stops video capture by calling [StopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-stopvideocapture).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |ID of the room where the remote user enables video capture. |
|userID |string |The user who starts the internal video capture. |


<span id="onfirstlocalvideoframecapturedeventhandler"></span>
### OnFirstLocalVideoFrameCapturedEventHandler

```c#
delegate void bytertc.OnFirstLocalVideoFrameCapturedEventHandler(
    StreamIndex index,
    VideoFrameInfo info
)
```


RTC SDK receives this callback when the first video frame or screen video frame capture is completed locally.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|index |StreamIndex |Stream properties. See [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-191862#StreamIndex) |
|info |VideoFrameInfo |Video information. See [VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-191862#VideoFrameInfo) |


**Notes**

For captured local video frames, you can call [SetLocalVideoSink](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-setlocalvideosink) to render locally.

<span id="onlocalvideosizechangedeventhandler"></span>
### OnLocalVideoSizeChangedEventHandler

```c#
delegate void bytertc.OnLocalVideoSizeChangedEventHandler(
    StreamIndex index,
    VideoFrameInfo info
)
```


Receive this callback when local video size or rotation information changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|index |StreamIndex |Stream properties. See [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-191862#StreamIndex). |
|info |VideoFrameInfo |Video frame information. See [VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-191862#VideoFrameInfo). |


<span id="onlocalvideostatechangedeventhandler"></span>
### OnLocalVideoStateChangedEventHandler

```c#
delegate void bytertc.OnLocalVideoStateChangedEventHandler(
    StreamIndex index,
    LocalVideoStreamState state,
    LocalVideoStreamError error
)
```


Receive this event when the state of the local video stream changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|index |StreamIndex |Stream property. See [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-191862#StreamIndex). |
|state |LocalVideoStreamState |Local video stream state. See [LocalVideoStreamState](https://docs.byteplus.com/en/docs/12/docs-191862#LocalVideoStreamState). |
|error |LocalVideoStreamError |Error code when local video state changes. See [LocalVideoStreamError](https://docs.byteplus.com/en/docs/12/docs-191861#LocalVideoStreamError). |


<span id="onvideoframesendstatechangedeventhandler"></span>
### OnVideoFrameSendStateChangedEventHandler

```c#
delegate void bytertc.OnVideoFrameSendStateChangedEventHandler(
    string roomID,
    RtcUser user,
    FirstFrameSendState state
)
```


Receive this callback when the sending status of the first frame of the local video changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |ID of the room from which the video is published. |
|user |RtcUser |Local user information. See [RtcUser](https://docs.byteplus.com/en/docs/12/docs-191862#RtcUser). |
|state |FirstFrameSendState |First frame sending status. See [FirstFrameSendState](https://docs.byteplus.com/en/docs/12/docs-191862#FirstFrameSendState). |


<span id="onscreenvideoframesendstatechangedeventhandler"></span>
### OnScreenVideoFrameSendStateChangedEventHandler

```c#
delegate void bytertc.OnScreenVideoFrameSendStateChangedEventHandler(
    string roomID,
    RtcUser user,
    FirstFrameSendState state
)
```


Receive this callback when the video first frame sending state of the screen sharing stream changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |ID of the room from which the screen video frame is published. |
|user |RtcUser |Local user information. See [RtcUser](https://docs.byteplus.com/en/docs/12/docs-191862#RtcUser). |
|state |FirstFrameSendState |First frame sending status. See [FirstFrameSendState](https://docs.byteplus.com/en/docs/12/docs-191862#FirstFrameSendState). |


<span id="onvideoframeplaystatechangedeventhandler"></span>
### OnVideoFramePlayStateChangedEventHandler

```c#
delegate void bytertc.OnVideoFramePlayStateChangedEventHandler(
    string roomID,
    RtcUser user,
    FirstFramePlayState state
)
```


Receive this callback when the playback state of the first frame of the video changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |ID of the room from which the video is published. |
|user |RtcUser |Remote user information. See [RtcUser](https://docs.byteplus.com/en/docs/12/docs-191862#RtcUser). |
|state |FirstFramePlayState |First frame playback status. See [FirstFramePlayState](https://docs.byteplus.com/en/docs/12/docs-191862#FirstFramePlayState). |


<span id="onremotevideosizechangedeventhandler"></span>
### OnRemoteVideoSizeChangedEventHandler

```c#
delegate void bytertc.OnRemoteVideoSizeChangedEventHandler(
    RemoteStreamKey key,
    VideoFrameInfo info
)
```


Users in the room who subscribe to this video stream receive this callback when the remote video size or rotation information changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|key |RemoteStreamKey |Remote Stream Information. See [RemoteStreamKey](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteStreamKey) |
|info |VideoFrameInfo |Video Frame Information. See [VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-191862#VideoFrameInfo) |


<span id="onremotevideostatechangedeventhandler"></span>
### OnRemoteVideoStateChangedEventHandler

```c#
delegate void bytertc.OnRemoteVideoStateChangedEventHandler(
    RemoteStreamKey key,
    RemoteVideoState state,
    RemoteVideoStateChangeReason reason
)
```


When the state of a remote video stream changes, users in the room who subscribe to this stream receive the event.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|key |RemoteStreamKey |Remote video stream information, room, user ID, stream attributes, etc.. See [RemoteStreamKey](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteStreamKey) |
|state |RemoteVideoState |Remote video stream status. See [RemoteVideoState](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteVideoState) |
|reason |RemoteVideoStateChangeReason |Remote video stream status change reason. See [RemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteVideoStateChangeReason) |


**Notes**

This callback is only applicable to the main stream but not to the screen stream.

<span id="onremoteaudiostatechangedeventhandler"></span>
### OnRemoteAudioStateChangedEventHandler

```c#
delegate void bytertc.OnRemoteAudioStateChangedEventHandler(
    RemoteStreamKey key,
    RemoteAudioState state,
    RemoteAudioStateChangeReason error
)
```


When the state of the audio stream from the remote user subscribes to changes, this callback will be received to understand the current state of the remote audio stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|key |RemoteStreamKey |Remote Stream Information. See [RemoteStreamKey](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteStreamKey) |
|state |RemoteAudioState |Remote Audio Stream Status. See [RemoteAudioState](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteAudioState) |
|error |RemoteAudioStateChangeReason |Remote Audio Stream Status Change Reason. See [RemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteAudioStateChangeReason) |


<span id="onnetworkqualityeventhandler"></span>
### OnNetworkQualityEventHandler

```c#
delegate void bytertc.OnNetworkQualityEventHandler(
    string roomID,
    NetworkQualityStats localQuality,
    List<NetworkQualityStats> remoteQualities,
    int remoteQualityNum
)
```


Report the network quality of the users every 2s after the local user joins the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |Room ID. |
|localQuality |NetworkQualityStats |Local network quality. Refer to [NetworkQualityStats](https://docs.byteplus.com/en/docs/12/docs-191862#NetworkQualityStats) for details. |
|remoteQualities |List<NetworkQualityStats\> |Network quality of the subscribed users. Refer to [NetworkQualityStats](https://docs.byteplus.com/en/docs/12/docs-191862#NetworkQualityStats) for details. |
|remoteQualityNum |int |Array length of `remoteQualities` |


<span id="onlocalstreamstatseventhandler"></span>
### OnLocalStreamStatsEventHandler

```c#
delegate void bytertc.OnLocalStreamStatsEventHandler(LocalStreamStats stat)
```


Local stream data statistics and network quality callback. After the local user publishes the flow successfully, the SDK will periodically (2s) notify the user through this callback event of the quality statistics of the published flow during this reference period. Statistics are passed to the user through the callback parameters of the [LocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-191862#LocalStreamStats) type, including the sent audio & video bit rate, sent frame rate, encoded frame rate, network quality, etc.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stat |LocalStreamStats |Audio & video stream and network status statistics. See [LocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-191862#LocalStreamStats). |


<span id="onremotestreamstatseventhandler"></span>
### OnRemoteStreamStatsEventHandler

```c#
delegate void bytertc.OnRemoteStreamStatsEventHandler(RemoteStreamStats stat)
```


Remote audio/video stream statistics and network quality callbacks for local subscriptions. After the local user subscribes to the stream successfully, the SDK will periodically (2s) notify the user through this callback event of the quality statistics of the subscribed stream during this reference period, including: sending audio & video bit rate, sending frame rate, encoded frame rate, network quality, etc.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stat |RemoteStreamStats |Audio & video stream and network status statistics. See [RemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteStreamStats). |


<span id="onfirstremotevideoframedecodedeventhandler"></span>
### OnFirstRemoteVideoFrameDecodedEventHandler

```c#
delegate void bytertc.OnFirstRemoteVideoFrameDecodedEventHandler(
    RemoteStreamKey key,
    VideoFrameInfo info
)
```


Receive this callback after the first frame of remote video stream is received and decoded by SDK.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|key |RemoteStreamKey |Remote Stream Information, see [RemoteStreamKey](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteStreamKey) |
|info |VideoFrameInfo |Video Frame Information, see [VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-191862#VideoFrameInfo) |


<span id="onfirstremotevideoframerenderedeventhandler"></span>
### OnFirstRemoteVideoFrameRenderedEventHandler

```c#
delegate void bytertc.OnFirstRemoteVideoFrameRenderedEventHandler(
    RemoteStreamKey key,
    VideoFrameInfo info
)
```


Receive this callback after the first frame of remote video stream is locally rendered by SDK.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|key |RemoteStreamKey |Remote stream information. See [RemoteStreamKey](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteStreamKey). |
|info |VideoFrameInfo |Video frame information. See [VideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-191862#VideoFrameInfo). |


<span id="onfacedetectresulteventhandler"></span>
### OnFaceDetectResultEventHandler

```c#
delegate void bytertc.OnFaceDetectResultEventHandler(FaceDetectResult result)
```


Callback of the result of face detection with Effect SDK. After calling [VideoSDKEnableFaceDetection](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideo-videosdkenablefacedetection) and using the Effect SDK integrated in the RTC SDK, you will receive this callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|result |FaceDetectResult |Face detection result. See [FaceDetectResult](https://docs.byteplus.com/en/docs/12/docs-191862#FaceDetectResult). |


<span id="onfirstremoteaudioframeeventhandler"></span>
### OnFirstRemoteAudioFrameEventHandler

```c#
delegate void bytertc.OnFirstRemoteAudioFrameEventHandler(RemoteStreamKey key)
```


Receives the callback when the first frame from a remote audio stream is received.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|key |RemoteStreamKey |Remote audio stream information. See [RemoteStreamKey](https://docs.byteplus.com/en/docs/12/docs-191862#RemoteStreamKey) |


**Notes**

The callback will be received when the user has just received each audio stream subscribed to in the room.

<span id="onroomstatechangedeventhandler"></span>
### OnRoomStateChangedEventHandler

```c#
delegate void bytertc.OnRoomStateChangedEventHandler(
    string roomID,
    string userID,
    int state,
    string ExtraInfo
)
```


Callback on room state changes. Via this callback you get notified of room relating warnings, errors and events. For example, the user joins the room, the user is removed from the room, and so on.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |Room ID. |
|userID |string |User ID. |
|state |int |Room state code.<br><br><br>* 0: Success.<br><br>* !0: Failure. See [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-191861#ErrorCode) and [WarningCode](https://docs.byteplus.com/en/docs/12/docs-191861#WarningCode) for specific indications. The user has been removed from the room due to one of the following reasons. \-1004: The same user joined the room in another client \-1006: The administrator kicked the user out of the room by calling openAPI. |
|ExtraInfo |string |Extra information. `join_type` indicates the type of room the user joins. `0` means the user joins the room for the first time, and `1` means the user rehoins the room. `elapsed` indicates the time interval from calling [JoinRoom](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-joinroom) to successfully joining room, in ms. |


<span id="onstreamstatechangedeventhandler"></span>
### OnStreamStateChangedEventHandler

```c#
delegate void bytertc.OnStreamStateChangedEventHandler(
    string roomID,
    string userID,
    int state,
    string ExtraInfo
)
```


Callback on stream state changes. You will receive this callback when you receive stream relating warnings and errors.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |Room ID. |
|userID |string |User ID. |
|state |int |Room state code. See [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-191861#ErrorCode) and [WarningCode](https://docs.byteplus.com/en/docs/12/docs-191861#WarningCode) for specific indications. |
|ExtraInfo |string |Extra information. Currently unavailable. |


<span id="onleaveroomeventhandler"></span>
### OnLeaveRoomEventHandler

```c#
delegate void bytertc.OnLeaveRoomEventHandler(
    string roomID,
    RtcRoomStats stats
)
```


After leaving the room successfully, receives the callback. When the user calls the [LeaveRoom](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-leaveroom), the SDK will stop all publishing subscription streams and release all call\-related media resources. After that, the user receives this callback .

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |Room ID. |
|stats |RtcRoomStats |Statistics for this call. See [RtcRoomStats](https://docs.byteplus.com/en/docs/12/docs-191862#RtcRoomStats). |


<span id="onuserjoinedeventhandler"></span>
### OnUserJoinedEventHandler

```c#
delegate void bytertc.OnUserJoinedEventHandler(
    string roomID,
    UserInfo userInfo,
    int elapsed
)
```


You will receive this callback in following cases:


* The remote user calls [SetUserVisibility](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-setuservisibility) turns visible and joins your room.

* The remote visible user is disconnected and then reconnected to your room.

* The invisible remote user in your room calls [SetUserVisibility](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-setuservisibility) and turns visible.

* You join the room when there are visible users in the room.


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |Room ID. |
|userInfo |UserInfo |See [UserInfo](https://docs.byteplus.com/en/docs/12/docs-191862#UserInfo). |
|elapsed |int |Reserved parameter. |


<span id="onuserleaveeventhandler"></span>
### OnUserLeaveEventHandler

```c#
delegate void bytertc.OnUserLeaveEventHandler(
    string roomID,
    string userID,
    UserOfflineReason reason
)
```


This callback is triggered when a remote user is disconnected or turns invisible.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |Room ID. |
|userID |string |ID of the user who leaves the room, or switches to invisible. |
|reason |UserOfflineReason |Reason to leave the room. See [UserOfflineReason](https://docs.byteplus.com/en/docs/12/docs-191862#UserOfflineReason). |


<span id="onroommessagereceivedeventhandler"></span>
### OnRoomMessageReceivedEventHandler

```c#
delegate void bytertc.OnRoomMessageReceivedEventHandler(
    string roomID,
    string userID,
    string message
)
```


Receive a callback for broadcast messages in the room. This callback is received when other users in the room call [sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-sendroommessage) to send a broadcast message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |Room ID. |
|userID |string |User ID of the message sender |
|message |string |Message content received |


<span id="onusermessagereceivedeventhandler"></span>
### OnUserMessageReceivedEventHandler

```c#
delegate void bytertc.OnUserMessageReceivedEventHandler(
    string roomID,
    string userID,
    string message
)
```


Receive this callback when you receive a peer\-to\-peer text message from another user in the room via [SendUserMessage](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-sendusermessage).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |Room ID. |
|userID |string |The user ID of the sender of the message. |
|message |string |The content of the received text message. |


<span id="onusermessagesendresulteventhandler"></span>
### OnUserMessageSendResultEventHandler

```c#
delegate void bytertc.OnUserMessageSendResultEventHandler(
    string roomID,
    long msgID,
    int error
)
```


After sending a point\-to\-point text or point\-to\-point binary message to a single user in the room, the message sender will receive a callback with the result of the message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |Room ID. |
|msgID |long |The ID of this message. |
|error |int |Text or binary message sending results. |


**Notes**

Call [sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-sendusermessage) interface to receive this callback.

<span id="onroommessagesendresulteventhandler"></span>
### OnRoomMessageSendResultEventHandler

```c#
delegate void bytertc.OnRoomMessageSendResultEventHandler(
    string roomID,
    long msgID,
    int error
)
```


Receives this callback after sending a text message or a binary message to a room with [SendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-sendroommessage).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |Room ID. |
|msgID |long |The ID of this message. |
|error |int |Message sending result. |


<span id="onuserpublishstreameventhandler"></span>
### OnUserPublishStreamEventHandler

```c#
delegate void bytertc.OnUserPublishStreamEventHandler(
    string roomID,
    string userID,
    MediaStreamType type
)
```


Callback on new media streams captured by camera/microphone in the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |Room ID. |
|userID |string |The ID of the remote user who published the stream. |
|type |MediaStreamType |Media stream type. See [MediaStreamType](https://docs.byteplus.com/en/docs/12/docs-191862#MediaStreamType). |


**Notes**

You will receive this callback after a remote user successfully published media streams captured by camera/microphone in the room with [PublishStream](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-publishstream). Then you can choose whether to call [SubscribeStream](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-subscribestream) to subscribe to the streams or not.

<span id="onuserunpublishstreameventhandler"></span>
### OnUserUnPublishStreamEventHandler

```c#
delegate void bytertc.OnUserUnPublishStreamEventHandler(
    string roomID,
    string userID,
    MediaStreamType type,
    StreamRemoveReason reason
)
```


Callback on removal of remote media stream captured by camera/microphone.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |Room ID. |
|userID |string |The ID of the remote user who removed the stream. |
|type |MediaStreamType |Media stream type. See [MediaStreamType](https://docs.byteplus.com/en/docs/12/docs-191862#MediaStreamType). |
|reason |StreamRemoveReason |The reason for the removal, see [StreamRemoveReason](https://docs.byteplus.com/en/docs/12/docs-191862#StreamRemoveReason). |


**Notes**

After receiving this callback, you can choose whether to call [UnsubscribeStream](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-unsubscribestream) to unsubscribe from the streams or not.

<span id="onuserpublishscreeneventhandler"></span>
### OnUserPublishScreenEventHandler

```c#
delegate void bytertc.OnUserPublishScreenEventHandler(
    string roomID,
    string userID,
    MediaStreamType type
)
```


Callback on new screen sharing media streams from remote users in the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |Room ID. |
|userID |string |The ID of the remote user who published the stream. |
|type |MediaStreamType |Media stream type. See [MediaStreamType](https://docs.byteplus.com/en/docs/12/docs-191862#MediaStreamType). |


**Notes**

You will receive this callback after a remote user successfully published screen sharing streams in the room with [PublishScreen](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-publishscreen). Then you can choose whether to call [SubscribeScreen](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-subscribescreen) to subscribe to the streams or not.

<span id="onuserunpublishscreeneventhandler"></span>
### OnUserUnPublishScreenEventHandler

```c#
delegate void bytertc.OnUserUnPublishScreenEventHandler(
    string roomID,
    string userID,
    MediaStreamType type,
    StreamRemoveReason reason
)
```


Callback on removal of screen sharing media streams from remote users in the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |Room ID. |
|userID |string |The ID of the remote user who removed the stream. |
|type |MediaStreamType |Media stream type. See [MediaStreamType](https://docs.byteplus.com/en/docs/12/docs-191862#MediaStreamType). |
|reason |StreamRemoveReason |The reason for the removal, see [StreamRemoveReason](https://docs.byteplus.com/en/docs/12/docs-191862#StreamRemoveReason). |


**Notes**

After receiving this callback, you can choose whether to call [UnsubscribeScreen](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-unsubscribescreen) to unsubscribe from the streams or not.

<span id="onstreamsubscribedeventhandler"></span>
### OnStreamSubscribedEventHandler

```c#
delegate void bytertc.OnStreamSubscribedEventHandler(
    string roomID,
    SubscribeState stateCode,
    string userID,
    SubscribeConfig info
)
```


Callback on subscription status of media streams

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |Room ID. |
|stateCode |SubscribeState |Subscription status of media streams, see [SubscribeState](https://docs.byteplus.com/en/docs/12/docs-191862#SubscribeState). |
|userID |string |The ID of the user who published the stream. |
|info |SubscribeConfig |Configurations of stream subscription, see [SubscribeConfig](https://docs.byteplus.com/en/docs/12/docs-191862#SubscribeConfig). |


**Notes**

Local users will receive this callback:


* After calling [SubscribeStream](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-subscribestream)/ [UnsubscribeStream](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-unsubscribestream) to change the subscription status of remote media streams captured by camera/microphone.

* After calling [SubscribeScreen](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-subscribescreen)/ [UnsubscribeScreen](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-unsubscribescreen) to change the subscription status of remote screen sharing streams.


<span id="ontokenwillexpireeventhandler"></span>
### OnTokenWillExpireEventHandler

```c#
delegate void bytertc.OnTokenWillExpireEventHandler(string roomID)
```


You will be informed 30 sec before the expiration via this callback. Call [UpdateToken](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-updatetoken) to renew the Token. If the Token expired, the user would be removed from the room and not be able to continue the call.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |The room ID. |


<span id="onaudiostreambannedeventhandler"></span>
### OnAudioStreamBannedEventHandler

```c#
delegate void bytertc.OnAudioStreamBannedEventHandler(
    string roomID,
    string userID,
    bool banned
)
```


This callback is triggered when the server level MuteUser/UnmuteUser method is called to disable/unban the sending of the specified user's audio and video stream in a specified room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |The room ID. |
|userID |string |Disabled/unbanned audio stream user ID |
|banned |bool |Audio stream sending status<br><br><br>* True: audio stream sending is disabled<br><br>* False: audio stream sending is unbanned |


<span id="onvideostreambannedeventhandler"></span>
### OnVideoStreamBannedEventHandler

```c#
delegate void bytertc.OnVideoStreamBannedEventHandler(
    string roomID,
    string userID,
    bool banned
)
```


This callback is triggered when the server level MuteUser/UnmuteUser method is invoked to disable/unban the sending of a specified user's video stream in a specified room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|roomID |string |Room ID of the video stream that was disabled/unbanned |
|userID |string |User ID of the video stream that was disabled/unbanned |
|banned |bool |Video stream sending status<br><br><br>* True: Video stream sending was disabled<br><br>* False: Video stream sending was unbanned |


<span id="onforwardstreamstatechangedeventhandler"></span>
### OnForwardStreamStateChangedEventHandler

```c#
delegate void bytertc.OnForwardStreamStateChangedEventHandler(
    List<ForwardStreamStateInfo> infos,
    int info_count
)
```


Callback returning the state and errors during relaying the media stream to each of the rooms

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|infos |List<ForwardStreamStateInfo\> |Array of the state and errors of each target room. Refer to [ForwardStreamStateInfo](https://docs.byteplus.com/en/docs/12/docs-191862#ForwardStreamStateInfo) for more information. |
|info_count |int |The number of the target rooms |


<span id="onforwardstreameventeventhandler"></span>
### OnForwardStreamEventEventHandler

```c#
delegate void bytertc.OnForwardStreamEventEventHandler(
    List<ForwardStreamEventInfo> infos,
    int info_count
)
```


Callback returning the events during relaying the media stream to each room

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|infos |List<ForwardStreamEventInfo\> |The Array of the event of each target room. Refer to [ForwardStreamEventInfo](https://docs.byteplus.com/en/docs/12/docs-191862#ForwardStreamEventInfo) for more information. |
|info_count |int |The number of the target rooms |


<span id="onavsyncstatechangecallback"></span>
### OnAVSyncStateChangeCallback

```c#
delegate void bytertc.OnAVSyncStateChangeCallback(AVSyncState state)
```


Stream publisher will receive this callback when the A/V synchronization state changes after [setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/docs-191859#IRTCVideoRoom-setmultideviceavsync) is called.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|state |AVSyncState |A/V synchronization state, see [AVSyncState](https://docs.byteplus.com/en/docs/12/docs-191862#AVSyncState). |
