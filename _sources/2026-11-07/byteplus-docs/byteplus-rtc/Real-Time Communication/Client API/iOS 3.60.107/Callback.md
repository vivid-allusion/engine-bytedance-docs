---
title: "Callback"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087"
---

<span id="ByteRTCMediaPlayerAudioFrameObserver"></span>
# ByteRTCMediaPlayerAudioFrameObserver

```objectivec
@protocol ByteRTCMediaPlayerAudioFrameObserver <NSObject>
```


observer for the audio frames during local audio file mixing.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onFrame:audioFrame:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCMediaPlayerAudioFrameObserver-onframe-audioframe) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCMediaPlayerAudioFrameObserver-onframe-audioframe"></span>
### onFrame:audioFrame:

```objectivec
- (void)onFrame:(int)playerId audioFrame:(ByteRTCAudioFrame* _Nonnull)audioFrame;
```


The callback for the audio frames during local audio file mixing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|playerId |int |Player's ID |
|audioFrame |ByteRTCAudioFrame\* |See [ByteRTCAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFrame). |


<span id="ByteRTCEngineDelegate"></span>
# ByteRTCEngineDelegate

```objectivec
@protocol ByteRTCEngineDelegate <NSObject>
```


ByteRTCEngineDelegate protocol contains the callback method provided by the SDK, which reports some run\-time events to the application through a proxy

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[rtcEngine:onWarning:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onwarning) |
|void |[rtcEngine:onError:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onerror) |
|void |[rtcEngine:onExtensionAccessError:msg:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onextensionaccesserror-msg) |
|void |[rtcEngine:onConnectionStateChanged:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onconnectionstatechanged) |
|void |[rtcEngine:onNetworkTypeChanged:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onnetworktypechanged) |
|void |[rtcEngine:onUserStartAudioCapture:info:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onuserstartaudiocapture-info) |
|void |[rtcEngine:onUserStopAudioCapture:info:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onuserstopaudiocapture-info) |
|void |[rtcEngine:onFirstRemoteAudioFrame:info:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onfirstremoteaudioframe-info) |
|void |[rtcEngine:onLocalAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onlocalaudiopropertiesreport) |
|void |[rtcEngine:onRemoteAudioPropertiesReport:totalRemoteVolume:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onremoteaudiopropertiesreport-totalremotevolume) |
|void |[rtcEngine:onActiveSpeaker:uid:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onactivespeaker-uid) |
|void |[rtcEngine:onUserStartVideoCapture:info:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onuserstartvideocapture-info) |
|void |[rtcEngine:onUserStopVideoCapture:info:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onuserstopvideocapture-info) |
|void |[rtcEngine:onFirstLocalVideoFrameCaptured:withFrameInfo:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onfirstlocalvideoframecaptured-withframeinfo) |
|void |[rtcEngine:onFirstRemoteVideoFrameRendered:info:withFrameInfo:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onfirstremotevideoframerendered-info-withframeinfo) |
|void |[rtcEngine:onFirstRemoteVideoFrameDecoded:info:withFrameInfo:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onfirstremotevideoframedecoded-info-withframeinfo) |
|void |[rtcEngine:onRemoteVideoSizeChanged:info:withFrameInfo:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onremotevideosizechanged-info-withframeinfo) |
|void |[rtcEngine:onLocalVideoSizeChanged:withFrameInfo:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onlocalvideosizechanged-withframeinfo) |
|void |[rtcEngine:onAudioDeviceStateChanged:device_type:device_state:device_error:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onaudiodevicestatechanged-device_type-device_state-device_error) |
|void |[rtcEngine:onVideoDeviceStateChanged:device_type:device_state:device_error:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onvideodevicestatechanged-device_type-device_state-device_error) |
|void |[rtcEngine:onAudioDeviceWarning:deviceType:deviceWarning:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onaudiodevicewarning-devicetype-devicewarning) |
|void |[rtcEngine:onVideoDeviceWarning:deviceType:deviceWarning:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onvideodevicewarning-devicetype-devicewarning) |
|void |[rtcEngine:onAudioFrameSendStateChanged:info:rtcUser:state:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onaudioframesendstatechanged-info-rtcuser-state) |
|void |[rtcEngine:onVideoFrameSendStateChanged:info:rtcUser:state:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onvideoframesendstatechanged-info-rtcuser-state) |
|void |[rtcEngine:onAudioFramePlayStateChanged:info:rtcUser:state:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onaudioframeplaystatechanged-info-rtcuser-state) |
|void |[rtcEngine:onVideoFramePlayStateChanged:info:rtcUser:state:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onvideoframeplaystatechanged-info-rtcuser-state) |
|void |[rtcEngine:onFirstLocalAudioFrame:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onfirstlocalaudioframe) |
|void |[rtcEngine:onAudioRouteChanged:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onaudioroutechanged) |
|void |[rtcEngine:onSEIMessageReceived:info:andMessage:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onseimessagereceived-info-andmessage) |
|void |[rtcEngine:onSEIStreamUpdate:info:eventType:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onseistreamupdate-info-eventtype) |
|void |[rtcEngine:onStreamSyncInfoReceived:info:streamType:data:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onstreamsyncinforeceived-info-streamtype-data) |
|void |[rtcEngine:onSysStats:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onsysstats) |
|void |[rtcEngine:onLocalAudioStateChanged:state:error:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onlocalaudiostatechanged-state-error) |
|void |[rtcEngine:onRemoteAudioStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onremoteaudiostatechanged-info-state-reason) |
|void |[rtcEngine:onLocalVideoStateChanged:withStreamState:withStreamError:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onlocalvideostatechanged-withstreamstate-withstreamerror) |
|void |[rtcEngine:onRemoteVideoStateChanged:info:withVideoState:withVideoStateReason:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onremotevideostatechanged-info-withvideostate-withvideostatereason) |
|void |[rtcEngine:onLoginResult:errorCode:elapsed:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onloginresult-errorcode-elapsed) |
|void |[rtcEngine:onLogout:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onlogout) |
|void |[rtcEngine:onServerParamsSetResult:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onserverparamssetresult) |
|void |[rtcEngine:onGetPeerOnlineStatus:status:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-ongetpeeronlinestatus-status) |
|void |[rtcEngine:onUserMessageReceivedOutsideRoom:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onusermessagereceivedoutsideroom-message) |
|void |[rtcEngine:onUserBinaryMessageReceivedOutsideRoom:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onuserbinarymessagereceivedoutsideroom-message) |
|void |[rtcEngine:onUserMessageReceivedOutsideRoom:uid:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onusermessagereceivedoutsideroom-uid-message) |
|void |[rtcEngine:onUserBinaryMessageReceivedOutsideRoom:uid:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onuserbinarymessagereceivedoutsideroom-uid-message) |
|void |[rtcEngine:onUserMessageSendResultOutsideRoom:error:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onusermessagesendresultoutsideroom-error) |
|void |[rtcEngine:onServerMessageSendResult:error:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onservermessagesendresult-error-message) |
|void |[rtcEngine:onNetworkDetectionResult:quality:rtt:lostRate:bitrate:jitter:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onnetworkdetectionresult-quality-rtt-lostrate-bitrate-jitter) |
|void |[rtcEngine:onNetworkDetectionStopped:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onnetworkdetectionstopped) |
|void |[rtcEngine:onAudioMixingPlayingProgress:progress:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onaudiomixingplayingprogress-progress) |
|void |[rtcEngine:onPerformanceAlarms:info:mode:reason:sourceWantedData:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onperformancealarms-info-mode-reason-sourcewanteddata) |
|void |[rtcEngine:onSimulcastSubscribeFallback:info:event:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onsimulcastsubscribefallback-info-event) |
|void |[rtcEngine:onRecordingStateUpdate:state:error_code:recording_info:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onrecordingstateupdate-state-error_code-recording_info) |
|void |[rtcEngine:onRecordingProgressUpdate:process:recording_info:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onrecordingprogressupdate-process-recording_info) |
|void |[rtcEngine:onAudioRecordingStateUpdate:error_code:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onaudiorecordingstateupdate-error_code) |
|void |[rtcEngine:onCloudProxyConnected:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-oncloudproxyconnected) |
|void |[rtcEngine:onEchoTestResult:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onechotestresult) |
|void |[rtcEngineOnNetworkTimeSynchronized:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengineonnetworktimesynchronized) |
|void |[rtcEngine:onHardwareEchoDetectionResult:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onhardwareechodetectionresult) |
|void |[rtcEngine:onLocalProxyStateChanged:withProxyState:withProxyError:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onlocalproxystatechanged-withproxystate-withproxyerror) |
|void |[rtcEngine:onMixedStreamEvent:withMixedStreamInfo:withErrorCode:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onmixedstreamevent-withmixedstreaminfo-witherrorcode) |
|void |[rtcEngine:onSingleStreamEvent:withTaskId:withErrorCode:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onsinglestreamevent-withtaskid-witherrorcode) |
|void |[rtcEngine:onRemoteSnapshotTakenToFile:info:filePath:width:height:errorCode:taskId:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onremotesnapshottakentofile-info-filepath-width-height-errorcode-taskid) |
|void |[rtcEngine:onLocalSnapshotTakenToFile:filePath:width:height:errorCode:taskId:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onlocalsnapshottakentofile-filepath-width-height-errorcode-taskid) |
|void |[deprecated] [rtcEngine:log:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-log) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCEngineDelegate-rtcengine-onwarning"></span>
### rtcEngine:onWarning:

```objectivec
- (void)rtcEngine:(ByteRTCEngine*_Nonnull)engine onWarning:(ByteRTCWarningCode)code;
```


A warning occurred during the SDK runtime. The SDK usually recovers automatically and warnings can be ignored.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object. |
|code |ByteRTCWarningCode |Warning code. See [ByteRTCWarningCode](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCWarningCode). |


<span id="ByteRTCEngineDelegate-rtcengine-onerror"></span>
### rtcEngine:onError:

```objectivec
- (void)rtcEngine:(ByteRTCEngine*_Nonnull)engine onError:(ByteRTCErrorCode)errorCode;
```


Error callback occurred. This callback is triggered when a network or media\-related error occurs during the

SDK runtime and cannot be automatically recovered and you may need to intervene.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object. |
|errorCode |ByteRTCErrorCode |BigInt. See [ByteRTCErrorCode](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCErrorCode). |


<span id="ByteRTCEngineDelegate-rtcengine-onextensionaccesserror-msg"></span>
### rtcEngine:onExtensionAccessError:msg:

```objectivec
- (void)rtcEngine:(ByteRTCEngine*_Nonnull)engine onExtensionAccessError:(NSString* _Nonnull)extensionName msg:(NSString* _Nonnull)msg;
```


> Available since 3.52


Failed to access the extension.

RTC SDK provides some features with extensions. Without implementing the extension, you cannot use the corresponding feature.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object. |
|extensionName |NSString\* |The name of extension. |
|msg |NSString\* |Error message. |


<span id="ByteRTCEngineDelegate-rtcengine-onconnectionstatechanged"></span>
### rtcEngine:onConnectionStateChanged:

```objectivec
- (void) rtcEngine:(ByteRTCEngine* _Nonnull)engine onConnectionStateChanged:(ByteRTCConnectionState) state;
```


SDK connection state change callback with signaling server. Triggered when the connection state changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|state |ByteRTCConnectionState |The current connection status between the SDK and the signaling server. See [ByteRTCConnectionState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCConnectionState). |


**Notes**

Refer to [Getting Connection Status](https://docs.byteplus.com/byteplus-rtc/docs/95376) for more details.

<span id="ByteRTCEngineDelegate-rtcengine-onnetworktypechanged"></span>
### rtcEngine:onNetworkTypeChanged:

```objectivec
- (void) rtcEngine:(ByteRTCEngine* _Nonnull)engine onNetworkTypeChanged:(ByteRTCNetworkType) type;
```


SDK current network connection type change callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|type |ByteRTCNetworkType |SDK The current network connection type. See [ByteRTCNetworkType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCNetworkType) |


<span id="ByteRTCEngineDelegate-rtcengine-onuserstartaudiocapture-info"></span>
### rtcEngine:onUserStartAudioCapture:info:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onUserStartAudioCapture:(NSString* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info;
```


The remote clients in the room will be informed of the state change via this callback after the visible user starts audio capture by calling [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-startaudiocapture).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine instance |
|streamId |NSString\* |The stream ID of the remote user who turns on audio capture |
|info |ByteRTCStreamInfo\* |Information of the remote user who turn on audio capture, see [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo). |


<span id="ByteRTCEngineDelegate-rtcengine-onuserstopaudiocapture-info"></span>
### rtcEngine:onUserStopAudioCapture:info:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onUserStopAudioCapture:(NSString* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info;
```


The remote clients in the room will be informed of the state change via this callback after the visible user stops audio capture by calling [stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-stopaudiocapture).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine instance |
|streamId |NSString\* |The stream ID |
|info |ByteRTCStreamInfo\* |Information of the audio stream. |


<span id="ByteRTCEngineDelegate-rtcengine-onfirstremoteaudioframe-info"></span>
### rtcEngine:onFirstRemoteAudioFrame:info:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onFirstRemoteAudioFrame:(NSString* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info;
```


The subscriber will receive this callback when the first frame of the receiving audio stream begins to decode. The following situations are included:


1. The publisher publishes audio, including the initial publication and restart after cancellation.

2. After the publisher stops audio capture, they restart it. When using an external source, this involves stopping the stream and then streaming again.

3. After the publisher publishes audio, the subscriber cancels the subscription to audio and then re\-subscribes to it.


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|streamId |NSString\* |ID of Remote stream information. |
|info |ByteRTCStreamInfo\* |Remote stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo). |


**Notes**

The callback will be received when the user has just received each audio stream in the room.

<span id="ByteRTCEngineDelegate-rtcengine-onlocalaudiopropertiesreport"></span>
### rtcEngine:onLocalAudioPropertiesReport:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onLocalAudioPropertiesReport:(NSArray<ByteRTCLocalAudioPropertiesInfo*>* _Nonnull)audioPropertiesInfos;
```


After calling [enableAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-enableaudiopropertiesreport), you will periodically receive this callback for the instantaneous information about local audio.

Local audio includes the microphone audio, the screen audio captured using RTC SDK internal mechanisms, and locally mixing audio.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|audioPropertiesInfos |NSArray<ByteRTCLocalAudioPropertiesInfo\*\>\* |See [ByteRTCLocalAudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCLocalAudioPropertiesInfo). |


<span id="ByteRTCEngineDelegate-rtcengine-onremoteaudiopropertiesreport-totalremotevolume"></span>
### rtcEngine:onRemoteAudioPropertiesReport:totalRemoteVolume:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onRemoteAudioPropertiesReport:(NSArray<ByteRTCRemoteAudioPropertiesInfo*>* _Nonnull)audioPropertiesInfos totalRemoteVolume:(NSInteger)totalRemoteVolume;
```


After calling [enableAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-enableaudiopropertiesreport), you will periodically receive this callback for the instantaneous information about the subscribed remote audio streams.

The remote audio streams includes the microphone audio and screen audio collected using the RTC SDK internal mechanism/custom mechanism.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|audioPropertiesInfos |NSArray<ByteRTCRemoteAudioPropertiesInfo\*\>\* |See [ByteRTCRemoteAudioPropertiesInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRemoteAudioPropertiesInfo). |
|totalRemoteVolume |NSInteger |The volume of the mixing of all the subscribed audio streams. The range is [0,255].<br><br><br>&nbsp;<br><br>* [0,25] Is close to silent;<br><br>* [25,75] Is low volume;<br><br>* [76,204] Is medium volume;<br><br>* [205,255] Is high volume. |


<span id="ByteRTCEngineDelegate-rtcengine-onactivespeaker-uid"></span>
### rtcEngine:onActiveSpeaker:uid:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onActiveSpeaker:(NSString* _Nonnull)roomId uid:(NSString*_Nonnull)uid;
```


After calling [enableAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-enableaudiopropertiesreport), you will periodically receive this callback for the active speaker information.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|roomId |NSString\* |Room ID. |
|uid |NSString\* |The user ID of the active speaker. |


<span id="ByteRTCEngineDelegate-rtcengine-onuserstartvideocapture-info"></span>
### rtcEngine:onUserStartVideoCapture:info:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onUserStartVideoCapture:(NSString* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info;
```


The remote clients in the room will be informed of the state change via this callback after the visible user starts video capture by [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-startvideocapture).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine instance |
|streamId |NSString\* |ID of the room where the user enables video capture |
|info |ByteRTCStreamInfo\* |Stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo). |


<span id="ByteRTCEngineDelegate-rtcengine-onuserstopvideocapture-info"></span>
### rtcEngine:onUserStopVideoCapture:info:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onUserStopVideoCapture:(NSString* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info;
```


The remote clients in the room will be informed of the state change via this callback after the visible user stops video capture by calling [stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-stopvideocapture).

If you don't start video capture before you publish video data, all visible user will receive this callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine instance |
|streamId |NSString\* |ID of the room where the user disables video capture |
|info |ByteRTCStreamInfo\* |Stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo). |


<span id="ByteRTCEngineDelegate-rtcengine-onfirstlocalvideoframecaptured-withframeinfo"></span>
### rtcEngine:onFirstLocalVideoFrameCaptured:withFrameInfo:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onFirstLocalVideoFrameCaptured:(ByteRTCVideoSource* _Nullable)videoSource withFrameInfo:(ByteRTCVideoFrameInfo* _Nonnull)frameInfo NS_SWIFT_NAME(rtcEngine(_:onFirstLocalVideoFrameCaptured:withFrameInfo:));
```


Receive this callback when the first locally captured video/screen share screen is rendered in the local view.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|videoSource |ByteRTCVideoSource\* |Reserved parameter |
|frameInfo |ByteRTCVideoFrameInfo\* |Video frame information. See [ByteRTCVideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoFrameInfo) |


<span id="ByteRTCEngineDelegate-rtcengine-onfirstremotevideoframerendered-info-withframeinfo"></span>
### rtcEngine:onFirstRemoteVideoFrameRendered:info:withFrameInfo:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onFirstRemoteVideoFrameRendered:(NSString* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info withFrameInfo:(ByteRTCVideoFrameInfo* _Nonnull)frameInfo NS_SWIFT_NAME(rtcEngine(_:onFirstRemoteVideoFrameRendered:info:withFrameInfo:));
```


The subscriber will receive this callback when the first frame of the receiving video stream begins to render. The following situations are included:


1. The publisher publishes video, including the initial publication and restart after cancellation.

2. After the publisher stops video capture, they restart it. When using an external source, this involves stopping the stream and then streaming again.

3. After the publisher publishes video, the subscriber cancels the subscription to video and then re\-subscribes to it.


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|streamId |NSString\* |ID of Remote stream information. |
|info |ByteRTCStreamInfo\* |Remote stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo). |
|frameInfo |ByteRTCVideoFrameInfo\* |Video frame information. See [ByteRTCVideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoFrameInfo) |


<span id="ByteRTCEngineDelegate-rtcengine-onfirstremotevideoframedecoded-info-withframeinfo"></span>
### rtcEngine:onFirstRemoteVideoFrameDecoded:info:withFrameInfo:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onFirstRemoteVideoFrameDecoded:(NSString* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info withFrameInfo:(ByteRTCVideoFrameInfo* _Nonnull)frameInfo NS_SWIFT_NAME(rtcEngine(_:onFirstRemoteVideoFrameDecoded:info:withFrameInfo:));
```


The subscriber will receive this callback when the first frame of the receiving video stream begins to decode. The following situations are included:


1. The publisher publishes video, including the initial publication and restart after cancellation.

2. After the publisher stops video capture, they restart it. When using an external source, this involves stopping the stream and then streaming again.

3. After the publisher publishes video, the subscriber cancels the subscription to video and then re\-subscribes to it.


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|streamId |NSString\* |ID of Remote stream information. |
|info |ByteRTCStreamInfo\* |Remote stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo). |
|frameInfo |ByteRTCVideoFrameInfo\* |Video frame information. See [ByteRTCVideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoFrameInfo) |


**Notes**


* For main stream, after joining the room, the subscriber will receive this callback only when the publisher publishes video stream for the first time.

* For screen\-sharing stream, the subscriber will receive this callback every time the publisher publishes or republishes the screen video stream.

    &nbsp;


<span id="rtcengine-onremotevideosizechanged-info-withframeinfo"></span>
### rtcEngine:onRemoteVideoSizeChanged:info:withFrameInfo:

```objectivec
- (void)rtcEngine:(ByteRTCEngine*_Nonnull)engine onRemoteVideoSizeChanged:(NSString*_Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info withFrameInfo:(ByteRTCVideoFrameInfo*_Nonnull)frameInfo NS_SWIFT_NAME(rtcEngine(_:onRemoteVideoSizeChanged:info:withFrameInfo:));
```


Users in the room who subscribe to this video stream receive this callback when the remote video size or rotation information changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|streamId |NSString\* |ID of Remote stream. |
|info |ByteRTCStreamInfo\* |Remote stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo). |
|frameInfo |ByteRTCVideoFrameInfo\* |Video frame information. See [ByteRTCVideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoFrameInfo) |


<span id="ByteRTCEngineDelegate-rtcengine-onlocalvideosizechanged-withframeinfo"></span>
### rtcEngine:onLocalVideoSizeChanged:withFrameInfo:

```objectivec
- (void)rtcEngine:(ByteRTCEngine*_Nonnull)engine onLocalVideoSizeChanged:(ByteRTCVideoSource* _Nullable)videoSource withFrameInfo:(ByteRTCVideoFrameInfo*_Nonnull)frameInfo NS_SWIFT_NAME(rtcEngine(_:onLocalVideoSizeChanged:withFrameInfo:));
```


Receive this callback when local video size or rotation information changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|videoSource |ByteRTCVideoSource\* |Reserved parameter |
|frameInfo |ByteRTCVideoFrameInfo\* |Frame information. See [ByteRTCVideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoFrameInfo) |


<span id="ByteRTCEngineDelegate-rtcengine-onaudiodevicestatechanged-device_type-device_state-device_error"></span>
### rtcEngine:onAudioDeviceStateChanged:device_type:device_state:device_error:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onAudioDeviceStateChanged:(NSString*_Nonnull)deviceID
      device_type:(ByteRTCAudioDeviceType)deviceType
     device_state:(ByteRTCMediaDeviceState)deviceState
     device_error:(ByteRTCMediaDeviceError)deviceError;
```


Audio device state callback, returns the state of audio capture and audio playback devices.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine instance |
|deviceID |NSString\* |Device ID |
|deviceType |ByteRTCAudioDeviceType |Device type. See [ByteRTCAudioDeviceType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioDeviceType). |
|deviceState |ByteRTCMediaDeviceState |Device state. See [ByteRTCMediaDeviceState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMediaDeviceState). |
|deviceError |ByteRTCMediaDeviceError |Device error. See [ByteRTCMediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMediaDeviceError). |


<span id="ByteRTCEngineDelegate-rtcengine-onvideodevicestatechanged-device_type-device_state-device_error"></span>
### rtcEngine:onVideoDeviceStateChanged:device_type:device_state:device_error:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onVideoDeviceStateChanged:(NSString*_Nonnull)deviceID
      device_type:(ByteRTCVideoDeviceType)deviceType
     device_state:(ByteRTCMediaDeviceState)deviceState
     device_error:(ByteRTCMediaDeviceError)deviceError;
```


Video device state callback. It returns the state of media devices, including video capture and screen capture.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|deviceID |NSString\* |Device ID |
|deviceType |ByteRTCVideoDeviceType |Device type. Refer to [ByteRTCVideoDeviceType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoDeviceType) for more details. |
|deviceState |ByteRTCMediaDeviceState |Device state. Refer to [ByteRTCMediaDeviceState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMediaDeviceState) for more details. |
|deviceError |ByteRTCMediaDeviceError |Device error. Refer to [ByteRTCMediaDeviceError](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMediaDeviceError) for more details. |


<span id="ByteRTCEngineDelegate-rtcengine-onaudiodevicewarning-devicetype-devicewarning"></span>
### rtcEngine:onAudioDeviceWarning:deviceType:deviceWarning:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onAudioDeviceWarning:(NSString*_Nonnull)deviceId
       deviceType:(ByteRTCAudioDeviceType)deviceType
    deviceWarning:(ByteRTCMediaDeviceWarning)deviceWarning;
```


Audio device warning callback. The audio devices includes audio capture devices and audio rendering devices.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|deviceId |NSString\* |Device ID |
|deviceType |ByteRTCAudioDeviceType |See [ByteRTCAudioDeviceType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioDeviceType) |
|deviceWarning |ByteRTCMediaDeviceWarning |See [ByteRTCMediaDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMediaDeviceWarning) |


<span id="ByteRTCEngineDelegate-rtcengine-onvideodevicewarning-devicetype-devicewarning"></span>
### rtcEngine:onVideoDeviceWarning:deviceType:deviceWarning:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onVideoDeviceWarning:(NSString*_Nonnull)deviceId
       deviceType:(ByteRTCVideoDeviceType)deviceType
    deviceWarning:(ByteRTCMediaDeviceWarning)deviceWarning;
```


Video device warning callback. The video devices includes video capture devices.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|deviceId |NSString\* |Device ID |
|deviceType |ByteRTCVideoDeviceType |See [ByteRTCVideoDeviceType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoDeviceType) |
|deviceWarning |ByteRTCMediaDeviceWarning |See [ByteRTCMediaDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMediaDeviceWarning) |


<span id="ByteRTCEngineDelegate-rtcengine-onaudioframesendstatechanged-info-rtcuser-state"></span>
### rtcEngine:onAudioFrameSendStateChanged:info:rtcUser:state:

```objectivec
- (void)rtcEngine:(ByteRTCEngine*_Nonnull)engine onAudioFrameSendStateChanged:(NSString* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info
              rtcUser:(ByteRTCUser*_Nonnull)user state:(ByteRTCFirstFrameSendState)state;
```


Receive this callback when the sending state of the first audio frame changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|streamId |NSString\* |ID of the audio stream |
|info |ByteRTCStreamInfo\* |Audio stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo) |
|user |ByteRTCUser\* |Local user information. See [ByteRTCUser](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCUser) |
|state |ByteRTCFirstFrameSendState |First frame sending status. See [ByteRTCFirstFrameSendState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCFirstFrameSendState) |


<span id="ByteRTCEngineDelegate-rtcengine-onvideoframesendstatechanged-info-rtcuser-state"></span>
### rtcEngine:onVideoFrameSendStateChanged:info:rtcUser:state:

```objectivec
- (void)rtcEngine:(ByteRTCEngine*_Nonnull)engine onVideoFrameSendStateChanged:(NSString* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info
          rtcUser:(ByteRTCUser*_Nonnull)user state:(ByteRTCFirstFrameSendState)state;
```


Triggered when the local video stream first frame sending state changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|streamId |NSString\* |ID of the video stream |
|info |ByteRTCStreamInfo\* |Video stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo) |
|user |ByteRTCUser\* |Local user information. See [ByteRTCUser](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCUser) |
|state |ByteRTCFirstFrameSendState |First frame sending status. See [ByteRTCFirstFrameSendState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCFirstFrameSendState) |


<span id="ByteRTCEngineDelegate-rtcengine-onaudioframeplaystatechanged-info-rtcuser-state"></span>
### rtcEngine:onAudioFramePlayStateChanged:info:rtcUser:state:

```objectivec
- (void)rtcEngine:(ByteRTCEngine*_Nonnull)engine onAudioFramePlayStateChanged:(NSString* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info 
          rtcUser:(ByteRTCUser*_Nonnull)user state:(ByteRTCFirstFramePlayState)state;
```


Receive this callback when the audio first frame playback state changes

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine instance. |
|streamId |NSString\* |ID of the audio stream |
|info |ByteRTCStreamInfo\* |Audio stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo) |
|user |ByteRTCUser\* |User information from the audio stream. See [ByteRTCUser](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCUser) |
|state |ByteRTCFirstFramePlayState |First frame playback status. See [ByteRTCFirstFramePlayState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCFirstFramePlayState) |


<span id="ByteRTCEngineDelegate-rtcengine-onvideoframeplaystatechanged-info-rtcuser-state"></span>
### rtcEngine:onVideoFramePlayStateChanged:info:rtcUser:state:

```objectivec
- (void)rtcEngine:(ByteRTCEngine*_Nonnull)engine onVideoFramePlayStateChanged:(NSString* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info
          rtcUser:(ByteRTCUser*_Nonnull)user state:(ByteRTCFirstFramePlayState)state;
```


Triggered when the remote video stream first frame playback state changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine instance. |
|streamId |NSString\* |ID of the video stream |
|info |ByteRTCStreamInfo\* |Video stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo) |
|user |ByteRTCUser\* |User information from the video stream source. See [ByteRTCUser](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCUser) |
|state |ByteRTCFirstFramePlayState |First frame playback state. See [ByteRTCFirstFramePlayState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCFirstFramePlayState) |


<span id="ByteRTCEngineDelegate-rtcengine-onfirstlocalaudioframe"></span>
### rtcEngine:onFirstLocalAudioFrame:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onFirstLocalAudioFrame:(ByteRTCAudioSource* _Nullable)audioSource;
```


Receive the callback when publishing local audio stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine instance |
|audioSource |ByteRTCAudioSource\* |Reserved parameter |


**Notes**

If you publish audio stream without enabling local audio capture, SDK will push blank audio frames that you will also get this notification.

<span id="ByteRTCEngineDelegate-rtcengine-onaudioroutechanged"></span>
### rtcEngine:onAudioRouteChanged:

```objectivec
- (void)rtcEngine:(ByteRTCEngine*_Nonnull)engine onAudioRouteChanged:(ByteRTCAudioRoute)device;
```


RTC notifies the audio route changes via this callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|device |ByteRTCAudioRoute |Current audio playback device. Refer to [ByteRTCAudioRoute](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioRoute) for more information. |


**Notes**

Either of the following actions will lead to audio route switching. See [Set the Audio Route](https://docs.byteplus.com/byteplus-rtc/docs/117836).


* Connecting/Disconnecting an audio device

* Designating the other audio device by calling [setAudioRoute:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setaudioroute).

    &nbsp;


<span id="rtcengine-onseimessagereceived-info-andmessage"></span>
### rtcEngine:onSEIMessageReceived:info:andMessage:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onSEIMessageReceived:(NSString* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info andMessage:(NSData* _Nonnull)message;
```


Receive this callback when you receive a video frame with a SEI message by calling [sendSEIMessage:andRepeatCount:andCountPerFrame:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-sendseimessage-andrepeatcount-andcountperframe).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |Current ByteRTCEngine instance |
|streamId |NSString\* |ID of Remote stream. |
|info |ByteRTCStreamInfo\* |Remote stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo). |
|message |NSData\* |Received SEI message content |


<span id="ByteRTCEngineDelegate-rtcengine-onseistreamupdate-info-eventtype"></span>
### rtcEngine:onSEIStreamUpdate:info:eventType:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onSEIStreamUpdate:(NSString* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info eventType:(ByteRTCSEIStreamEventType)eventType;
```


Callback about publishing status of the black frame video stream.

In a voice call scenario, when the local user calls [sendSEIMessage:andRepeatCount:andCountPerFrame:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-sendseimessage-andrepeatcount-andcountperframe) to send SEI data with a black frame, the sending status of the stream is notified to the remote user through this callback.

You can tell from this callback that the video frame carrying SEI data is a black frame and thus not render that video frame.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |Current ByteRTCEngine instance |
|streamId |NSString\* |ID of Remote stream. |
|info |ByteRTCStreamInfo\* |Remote stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo). |
|eventType |ByteRTCSEIStreamEventType |State of the black frame video stream, see [ByteRTCSEIStreamEventType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCSEIStreamEventType). |


<span id="ByteRTCEngineDelegate-rtcengine-onstreamsyncinforeceived-info-streamtype-data"></span>
### rtcEngine:onStreamSyncInfoReceived:info:streamType:data:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onStreamSyncInfoReceived:(NSString* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info streamType:(ByteRTCSyncInfoStreamType)streamType data:(NSData* _Nonnull)data;
```


Audio stream synchronization information callback. You can use this callback to receive audio stream synchronization information sent remotely after the remote user calls [sendStreamSyncInfo:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-sendstreamsyncinfo-config) to send an audio stream synchronization message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |Current ByteRTCEngine instance. |
|streamId |NSString\* |ID of Remote stream. |
|info |ByteRTCStreamInfo\* |Remote stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo). |
|streamType |ByteRTCSyncInfoStreamType |Media stream type. See [ByteRTCSyncInfoStreamType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCSyncInfoStreamType). |
|data |NSData\* |Message content. |


<span id="ByteRTCEngineDelegate-rtcengine-onsysstats"></span>
### rtcEngine:onSysStats:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onSysStats:(const ByteRTCSysStats* _Nonnull)stats NS_SWIFT_NAME(rtcEngine(_:onSysStats:));
```


Report the current device CPU and memory usage, which is triggered every 2s.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|stats |const ByteRTCSysStats\* |Cpu and memory usage information. See [ByteRTCSysStats](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCSysStats) data type |


<span id="ByteRTCEngineDelegate-rtcengine-onlocalaudiostatechanged-state-error"></span>
### rtcEngine:onLocalAudioStateChanged:state:error:

```objectivec
- (void)rtcEngine:(ByteRTCEngine*_Nonnull)engine onLocalAudioStateChanged:(ByteRTCAudioSource* _Nullable)audioSource
                     state:(ByteRTCLocalAudioStreamState)state
                     error:(ByteRTCLocalAudioStreamError)error;
```


Receive this callback when the state of the local audio stream changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|audioSource |ByteRTCAudioSource\* |Reserved parameter |
|state |ByteRTCLocalAudioStreamState |The current state of the local audio device. See [ByteRTCLocalAudioStreamState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCLocalAudioStreamState) |
|error |ByteRTCLocalAudioStreamError |Error code when the state of the local audio stream changes. See [ByteRTCLocalAudioStreamError](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCLocalAudioStreamError) |


<span id="ByteRTCEngineDelegate-rtcengine-onremoteaudiostatechanged-info-state-reason"></span>
### rtcEngine:onRemoteAudioStateChanged:info:state:reason:

```objectivec
- (void)rtcEngine:(ByteRTCEngine*_Nonnull)engine onRemoteAudioStateChanged:(NSString*_Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info
                      state:(ByteRTCRemoteAudioState)state
                      reason:(ByteRTCRemoteAudioStateChangeReason)reason;
```


Receive this callback when the state of the remote audio stream subscribed to changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|streamId |NSString\* |ID of Remote stream. |
|info |ByteRTCStreamInfo\* |Remote stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo). |
|state |ByteRTCRemoteAudioState |The current state of the remote audio stream. See [ByteRTCRemoteAudioState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRemoteAudioState) |
|reason |ByteRTCRemoteAudioStateChangeReason |The reason for the change in the state of the remote audio stream. See [ByteRTCRemoteAudioStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRemoteAudioStateChangeReason) |


<span id="ByteRTCEngineDelegate-rtcengine-onlocalvideostatechanged-withstreamstate-withstreamerror"></span>
### rtcEngine:onLocalVideoStateChanged:withStreamState:withStreamError:

```objectivec
- (void)rtcEngine:(ByteRTCEngine*_Nonnull)engine onLocalVideoStateChanged:(ByteRTCVideoSource* _Nullable)videoSource
             withStreamState:(ByteRTCLocalVideoStreamState)state
             withStreamError:(ByteRTCLocalVideoStreamError)error NS_SWIFT_NAME(rtcEngine(_:onLocalVideoStateChanged:withStreamState:withStreamError:));
```


Receive this event when the state of the local video stream changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|videoSource |ByteRTCVideoSource\* |Reserved parameter |
|state |ByteRTCLocalVideoStreamState |Current state of local video stream. See [ByteRTCLocalVideoStreamState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCLocalVideoStreamState) |
|error |ByteRTCLocalVideoStreamError |Error code when local video state changes. See [ByteRTCLocalVideoStreamError](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCLocalVideoStreamError) |


<span id="ByteRTCEngineDelegate-rtcengine-onremotevideostatechanged-info-withvideostate-withvideostatereason"></span>
### rtcEngine:onRemoteVideoStateChanged:info:withVideoState:withVideoStateReason:

```objectivec
- (void)rtcEngine:(ByteRTCEngine*_Nonnull)engine onRemoteVideoStateChanged:(NSString*_Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info
                withVideoState:(ByteRTCRemoteVideoState)state
                withVideoStateReason:(ByteRTCRemoteVideoStateChangeReason)reason NS_SWIFT_NAME(rtcEngine(_:onRemoteVideoStateChanged:info:withVideoState:withVideoStateReason:));
```


When the state of the remote video stream changes, users in the room who subscribe to this stream will receive the event.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|streamId |NSString\* |ID of Remote stream. |
|info |ByteRTCStreamInfo\* |Remote stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo). |
|state |ByteRTCRemoteVideoState |The current state of the remote video stream. See [ByteRTCRemoteVideoState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRemoteVideoState) |
|reason |ByteRTCRemoteVideoStateChangeReason |The reason for the change in the state of the remote video stream. See [ByteRTCRemoteVideoStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRemoteVideoStateChangeReason) |


**Notes**

This callback is only applicable to the main stream and not applicable to the screen stream.

<span id="ByteRTCEngineDelegate-rtcengine-onloginresult-errorcode-elapsed"></span>
### rtcEngine:onLoginResult:errorCode:elapsed:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onLoginResult:(NSString* _Nonnull)uid errorCode:(ByteRTCLoginErrorCode)errorCode elapsed:(NSInteger)elapsed;
```


Login result callback

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|uid |NSString\* |Login user ID |
|errorCode |ByteRTCLoginErrorCode |Login result<br><br>&nbsp;<br><br>See [ByteRTCLoginErrorCode](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCLoginErrorCode). |
|elapsed |NSInteger |The time it takes from calling the [login:uid:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-login-uid) interface to return the result.<br><br>&nbsp;<br><br>Is in ms. |


**Notes**

Receive this callback after calling [login:uid:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-login-uid).

<span id="ByteRTCEngineDelegate-rtcengine-onlogout"></span>
### rtcEngine:onLogout:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onLogout:(ByteRTCLogoutReason)reason;
```


Callback of the logout result

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|reason |ByteRTCLogoutReason |It describes the reason why users log out. See [ByteRTCLogoutReason](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCLogoutReason) |


**Notes**

You will receive this callback when calling [logout](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-logout) or when the local user is kicked out because another user logs in with the same UserId.

<span id="ByteRTCEngineDelegate-rtcengine-onserverparamssetresult"></span>
### rtcEngine:onServerParamsSetResult:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onServerParamsSetResult:(NSInteger)errorCode;
```


Set the return result of the application server parameter

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|errorCode |NSInteger |* 200, set successfully<br><br>* != 200: Failure. Refer to [ByteRTCUserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCUserMessageSendResult) for details. |


**Notes**

Receive this callback after calling [setServerParams:url:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setserverparams-url).

<span id="ByteRTCEngineDelegate-rtcengine-ongetpeeronlinestatus-status"></span>
### rtcEngine:onGetPeerOnlineStatus:status:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onGetPeerOnlineStatus:(NSString* _Nonnull)peerUserId status:(ByteRTCUserOnlineStatus)status;
```


Returns the result of querying the login status of the peer or local user

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|peerUserId |NSString\* |User ID to query |
|status |ByteRTCUserOnlineStatus |User login status of the query<br><br>&nbsp;<br><br>See [ByteRTCUserOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCUserOnlineStatus). |


**Notes**

You must first call [getPeerOnlineStatus:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-getpeeronlinestatus) to receive this callback.

<span id="ByteRTCEngineDelegate-rtcengine-onusermessagereceivedoutsideroom-message"></span>
### rtcEngine:onUserMessageReceivedOutsideRoom:message:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onUserMessageReceivedOutsideRoom:(NSString* _Nonnull)uid message:(NSString* _Nonnull)message;
```


> This interface will be deprecated since version 3.64. Use [rtcEngine:onUserMessageReceivedOutsideRoom:uid:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onusermessagereceivedoutsideroom-uid-message) instead.

> Receive this callback when you receive a text message from an out\-of\-room user calling [sendUserMessageOutsideRoom:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-sendusermessageoutsideroom-message-config)


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object. |
|uid |NSString\* |User ID of the message sender. |
|message |NSString\* |The content of the received text message. |


<span id="ByteRTCEngineDelegate-rtcengine-onuserbinarymessagereceivedoutsideroom-message"></span>
### rtcEngine:onUserBinaryMessageReceivedOutsideRoom:message:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onUserBinaryMessageReceivedOutsideRoom:(NSString* _Nonnull)uid message:(NSData* _Nonnull)message;
```


> This interface will be deprecated since version 3.64. Use [rtcEngine:onUserBinaryMessageReceivedOutsideRoom:uid:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onuserbinarymessagereceivedoutsideroom-uid-message) instead.

> Receive this callback when you receive a binary message from an out\-of\-room user call [sendUserBinaryMessageOutsideRoom:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-senduserbinarymessageoutsideroom-message-config).


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|uid |NSString\* |User ID of the message sender. |
|message |NSData\* |The content of the received binary message. |


<span id="ByteRTCEngineDelegate-rtcengine-onusermessagereceivedoutsideroom-uid-message"></span>
### rtcEngine:onUserMessageReceivedOutsideRoom:uid:message:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onUserMessageReceivedOutsideRoom:(NSInteger)msgid uid:(NSString* _Nonnull)uid message:(NSString* _Nonnull)message;
```


Receive this callback when you receive a text message from an out\-of\-room user calling [sendUserMessageOutsideRoom:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-sendusermessageoutsideroom-message-config)

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|msgid |NSInteger |Message number. |
|uid |NSString\* |User ID of the message sender. |
|message |NSString\* |The content of the received text message. |


<span id="ByteRTCEngineDelegate-rtcengine-onuserbinarymessagereceivedoutsideroom-uid-message"></span>
### rtcEngine:onUserBinaryMessageReceivedOutsideRoom:uid:message:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onUserBinaryMessageReceivedOutsideRoom:(NSInteger)msgid uid:(NSString* _Nonnull)uid message:(NSData* _Nonnull)message;
```


Receive this callback when you receive a binary message from an out\-of\-room user call [sendUserBinaryMessageOutsideRoom:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-senduserbinarymessageoutsideroom-message-config).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|msgid |NSInteger |Message number. |
|uid |NSString\* |User ID of the message sender. |
|message |NSData\* |The content of the received binary message. |


<span id="ByteRTCEngineDelegate-rtcengine-onusermessagesendresultoutsideroom-error"></span>
### rtcEngine:onUserMessageSendResultOutsideRoom:error:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onUserMessageSendResultOutsideRoom:(NSInteger)msgid error:(ByteRTCUserMessageSendResult)error;
```


A callback that sends a message to a specified user outside the room

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|msgid |NSInteger |The ID of this message<br><br>&nbsp;<br><br>All P2P and P2Server messages share a single ID sequence. |
|error |ByteRTCUserMessageSendResult |Message sending result<br><br>&nbsp;<br><br>See [ByteRTCUserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCUserMessageSendResult). |


**Notes**

Receive this callback when you send a message by calling [sendUserMessageOutsideRoom:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-sendusermessageoutsideroom-message-config) or [sendUserBinaryMessageOutsideRoom:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-senduserbinarymessageoutsideroom-message-config).

<span id="ByteRTCEngineDelegate-rtcengine-onservermessagesendresult-error-message"></span>
### rtcEngine:onServerMessageSendResult:error:message:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onServerMessageSendResult:(int64_t)msgid error:(ByteRTCUserMessageSendResult)error message:(NSData* _Nonnull)message;
```


Callback to send a message to the application server.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object. |
|msgid |int64_t |The ID of this message. All P2P and P2Server messages share a single ID sequence. |
|error |ByteRTCUserMessageSendResult |Message sending result, see [ByteRTCUserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCUserMessageSendResult). |
|message |NSData\* |The message returned in ACK when the application server receives HTTP request. The message should not exceed 64 KB. |


**Notes**

This callback is asynchronous. Receive this callback when a message is sent by calling the [sendServerMessage:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-sendservermessage) or [sendServerBinaryMessage:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-sendserverbinarymessage) interface.

<span id="ByteRTCEngineDelegate-rtcengine-onnetworkdetectionresult-quality-rtt-lostrate-bitrate-jitter"></span>
### rtcEngine:onNetworkDetectionResult:quality:rtt:lostRate:bitrate:jitter:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onNetworkDetectionResult:(ByteRTCNetworkDetectionLinkType)type quality:(ByteRTCNetworkQuality)quality rtt:(int)rtt lostRate:(double)lostRate bitrate:(int)bitrate jitter:(int)jitter;
```


Callback of pre\-call network detection result.

After successfully calling [startNetworkDetection:uplinkBandwidth:downlink:downlinkBandwidth:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-startnetworkdetection-uplinkbandwidth-downlink-downlinkbandwidth), you will receive this callback for the first time in 3s and every 2s thereafter.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine instance. |
|type |ByteRTCNetworkDetectionLinkType |Identifies the network type as uplink/downlink. |
|quality |ByteRTCNetworkQuality |Network quality, see [ByteRTCNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCNetworkQuality). |
|rtt |int |Network RTT in ms. |
|lostRate |double |Packet loss rate. |
|bitrate |int |Network bandwidth in kbps. |
|jitter |int |Network jitter in ms |


<span id="ByteRTCEngineDelegate-rtcengine-onnetworkdetectionstopped"></span>
### rtcEngine:onNetworkDetectionStopped:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onNetworkDetectionStopped:(ByteRTCNetworkDetectionStopReason)errorCode;
```


Pre\-call network probing ends

The following will stop detection and receive this primary callback:


1. This callback is received once when the [stopNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-stopnetworkdetection) interface is called to stop probing;

2. Stop detection when the first frame of remote/local audio is received;

3. Stop detecting when the detection exceeds 3 minutes;

4. When the probe link is disconnected for a certain period of time, the probe is stopped.


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|errorCode |ByteRTCNetworkDetectionStopReason |See [ByteRTCNetworkDetectionStopReason](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCNetworkDetectionStopReason) for reasons of stopping probing. |


<span id="ByteRTCEngineDelegate-rtcengine-onaudiomixingplayingprogress-progress"></span>
### rtcEngine:onAudioMixingPlayingProgress:progress:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onAudioMixingPlayingProgress:(NSInteger)mixId progress:(int64_t) progress;
```


Callback for playback progress of mixed audio files

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |Current RTC SDK object |
|mixId |NSInteger |ID of the mixing task |
|progress |int64_t |The current playback progress (ms) of the mixed audio file |


**Notes**

After calling setAudioMixingProgressInterval:interval: to set the time interval to a value greater than 0, or calling startAudioMixing:filePath:config: to set the time interval in ByteRTCAudioMixingConfig to a value greater than 0, the SDK will trigger the callback according to the set time interval.

<span id="ByteRTCEngineDelegate-rtcengine-onperformancealarms-info-mode-reason-sourcewanteddata"></span>
### rtcEngine:onPerformanceAlarms:info:mode:reason:sourceWantedData:

```objectivec
- (void)rtcEngine:(ByteRTCEngine*_Nonnull)engine onPerformanceAlarms:(NSString* _Nonnull)streamId 
                           info:(ByteRTCStreamInfo* _Nonnull)info
                           mode:(ByteRTCPerformanceAlarmMode)mode
                         reason:(ByteRTCPerformanceAlarmReason)reason
               sourceWantedData:(ByteRTCSourceWantedData*_Nonnull)data;
```


When the publish performance fallback [setPublishFallbackOption:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setpublishfallbackoption) is not turned on locally, and when insufficient device performance is detected, this callback is received.

When the [setPublishFallbackOption:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setpublishfallbackoption) is locally turned on, and when the publish performance fallback/recovery is caused due to device performance/network reasons, this callback is received.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|streamId |NSString\* |Stream ID |
|info |ByteRTCStreamInfo\* |Stream information, see [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo). |
|mode |ByteRTCPerformanceAlarmMode |Indicates whether the release fallback function is turned on locally. See [ByteRTCPerformanceAlarmMode](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCPerformanceAlarmMode)<br><br><br>&nbsp;<br><br>* When the publiiher does not turn on the release performance fallback, the mode value is ByteRTCPerformanceAlarmModeNormal.<br><br>* When the publisher turns on the release performance fallback, the mode value is ByteRTCPerformanceAlarmModeSimulcast. |
|reason |ByteRTCPerformanceAlarmReason |For alarm reasons. See [ByteRTCPerformanceAlarmReason](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCPerformanceAlarmReason) |
|data |ByteRTCSourceWantedData\* |Performance fallback related data. See [ByteRTCSourceWantedData](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCSourceWantedData). |


<span id="ByteRTCEngineDelegate-rtcengine-onsimulcastsubscribefallback-info-event"></span>
### rtcEngine:onSimulcastSubscribeFallback:info:event:

```objectivec
- (void)rtcEngine:(ByteRTCEngine*_Nonnull)engine onSimulcastSubscribeFallback:(NSString* _Nonnull)streamId 
             info:(ByteRTCStreamInfo* _Nonnull)info event:(ByteRTCRemoteStreamSwitchEvent*_Nonnull)event;
```


Once the fallback option is set, fillback or reverting from a Fallback of a media stream will trigger this callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |Current ByteRTCEngine instance |
|streamId |NSString\* |Stream ID |
|info |ByteRTCStreamInfo\* |Stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo). |
|event |ByteRTCRemoteStreamSwitchEvent\* |Information of stream switching. Refer to [ByteRTCRemoteStreamSwitchEvent](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRemoteStreamSwitchEvent) for more details. |


<span id="ByteRTCEngineDelegate-rtcengine-onrecordingstateupdate-state-error_code-recording_info"></span>
### rtcEngine:onRecordingStateUpdate:state:error_code:recording_info:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onRecordingStateUpdate:(ByteRTCVideoSource* _Nullable)videoSource
                         state:(ByteRTCRecordingState)state
                    error_code:(ByteRTCRecordingErrorCode)errorCode
                recording_info:(ByteRTCRecordingInfo* _Nonnull)recordingInfo;
```


Get local recording status callback.

The callback is triggered by either [startFileRecording:type:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-startfilerecording-type) or [stopFileRecording:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-stopfilerecording).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|videoSource |ByteRTCVideoSource\* |Reserved parameter |
|state |ByteRTCRecordingState |Recording status. See [ByteRTCRecordingState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRecordingState) |
|errorCode |ByteRTCRecordingErrorCode |Recording error code. See [ByteRTCRecordingErrorCode](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRecordingErrorCode) |
|recordingInfo |ByteRTCRecordingInfo\* |Recording file details. See [ByteRTCRecordingInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRecordingInfo) |


<span id="ByteRTCEngineDelegate-rtcengine-onrecordingprogressupdate-process-recording_info"></span>
### rtcEngine:onRecordingProgressUpdate:process:recording_info:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onRecordingProgressUpdate:(ByteRTCVideoSource* _Nullable)videoSource
                          process:(ByteRTCRecordingProgress* _Nonnull)process
                   recording_info:(ByteRTCRecordingInfo* _Nonnull)recordingInfo;
```


Local recording progress callback.

This callback is triggered by [startFileRecording:type:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-startfilerecording-type). When the recording state is normal, the system will prompt the recording progress through this callback every second.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|videoSource |ByteRTCVideoSource\* |Reserved parameter |
|process |ByteRTCRecordingProgress\* |Recording progress. See [ByteRTCRecordingProgress](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRecordingProgress) |
|recordingInfo |ByteRTCRecordingInfo\* |Details of the recorded file. See [ByteRTCRecordingInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRecordingInfo) |


<span id="ByteRTCEngineDelegate-rtcengine-onaudiorecordingstateupdate-error_code"></span>
### rtcEngine:onAudioRecordingStateUpdate:error_code:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine
        onAudioRecordingStateUpdate:(ByteRTCAudioRecordingState)state
                         error_code:(ByteRTCAudioRecordingErrorCode)errorCode;
```


When calling [startAudioRecording:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-startaudiorecording) or [stopAudioRecording](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-stopaudiorecording) to change the recording status, receive the callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|state |ByteRTCAudioRecordingState |See [ByteRTCAudioRecordingState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioRecordingState). |
|errorCode |ByteRTCAudioRecordingErrorCode |See [ByteRTCAudioRecordingErrorCode](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCAudioRecordingErrorCode). |


<span id="ByteRTCEngineDelegate-rtcengine-oncloudproxyconnected"></span>
### rtcEngine:onCloudProxyConnected:

```objectivec
- (void)rtcEngine:(ByteRTCEngine*  _Nonnull)engine onCloudProxyConnected:(NSInteger)interval;
```


Receives the callback when you call [startCloudProxy:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-startcloudproxy) to start cloud proxy, and the SDK connects the proxy server successfully.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|interval |NSInteger |The interval in ms between starting cloud proxy and connects the cloud proxy server successfully. |


<span id="ByteRTCEngineDelegate-rtcengine-onechotestresult"></span>
### rtcEngine:onEchoTestResult:

```objectivec
- (void)rtcEngine:(ByteRTCEngine*_Nonnull)engine onEchoTestResult:(ByteRTCEchoTestResult)result NS_SWIFT_NAME(rtcEngine(_:onEchoTestResult:));
```


Callback about the call test result.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |`ByteRTCEngine` object |
|result |ByteRTCEchoTestResult |Test result, see [ByteRTCEchoTestResult](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCEchoTestResult). |


**Notes**

The timing when this callback will be triggered is as follows:


* A device\-related error occurred during the test；

* After a successful test；

* After stopping the test, provided that the audio/video playback was not received during the test due to non\-device reasons.

    &nbsp;


<span id="rtcengineonnetworktimesynchronized"></span>
### rtcEngineOnNetworkTimeSynchronized:

```objectivec
- (void)rtcEngineOnNetworkTimeSynchronized:(ByteRTCEngine*_Nonnull)engine;
```


After calling [getNetworkTimeInfo](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-getnetworktimeinfo) for the first time, the SDK starts network time synchronization internally. This callback will be triggered when the synchronization is completed.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |See [ByteRTCEngine](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine). |


<span id="ByteRTCEngineDelegate-rtcengine-onhardwareechodetectionresult"></span>
### rtcEngine:onHardwareEchoDetectionResult:

```objectivec
- (void)rtcEngine:(ByteRTCEngine*_Nonnull)engine onHardwareEchoDetectionResult:(ByteRTCHardwareEchoDetectionResult)result NS_SWIFT_NAME(rtcEngine(_:onHardwareEchoDetectionResult:));
```


Callback that notifies you the result of the echo detection before a call

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object. |
|result |ByteRTCHardwareEchoDetectionResult |Refer to [ByteRTCHardwareEchoDetectionResult](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCHardwareEchoDetectionResult) for more details. |


**Notes**


* This callback notifies you the result of the echo detection by calling [startHardwareEchoDetection:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-starthardwareechodetection).

* We recommend to call [stopHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-stophardwareechodetection) to stop the detection.

* Listen to `ByteRTCMediaDeviceWarningDetectLeakEcho` in the callback of [rtcEngine:onAudioDeviceWarning:deviceType:deviceWarning:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEngineDelegate-rtcengine-onaudiodevicewarning-devicetype-devicewarning) for the echo issue during a call.

    &nbsp;


<span id="rtcengine-onlocalproxystatechanged-withproxystate-withproxyerror"></span>
### rtcEngine:onLocalProxyStateChanged:withProxyState:withProxyError:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onLocalProxyStateChanged:(ByteRTCLocalProxyType)type withProxyState:(ByteRTCLocalProxyState)state withProxyError:(ByteRTCLocalProxyError)error;
```


Callback on local proxy connection. After calling [setLocalProxy:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setlocalproxy) to set local proxies, you will receive this callback that informs you of the states of local proxy connection.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object |
|type |ByteRTCLocalProxyType |The types of local proxies. Refer to [ByteRTCLocalProxyType](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCLocalProxyType) for details. |
|state |ByteRTCLocalProxyState |The states of local proxy connection. Refer to [ByteRTCLocalProxyState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCLocalProxyState) for details. |
|error |ByteRTCLocalProxyError |The errors of local proxy connection. Refer to [ByteRTCLocalProxyError](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCLocalProxyError) for details. |


<span id="ByteRTCEngineDelegate-rtcengine-onmixedstreamevent-withmixedstreaminfo-witherrorcode"></span>
### rtcEngine:onMixedStreamEvent:withMixedStreamInfo:withErrorCode:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onMixedStreamEvent:(ByteRTCMixedStreamTaskEvent)event withMixedStreamInfo:(ByteRTCMixedStreamTaskInfo*)info withErrorCode:(ByteRTCMixedStreamTaskErrorCode)errorCode;
```


> Available since 3.60. Since version 3.60, this callback replaces the `onStreamMixingEvent:taskId:error:mixType:` and `rtcEngine:onPushPublicStreamResult:publicStreamId:errorCode:` methods for the functions described below. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this callback.


Reports events during pushing a mixed stream to CDN or a WTN stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object. |
|event |ByteRTCMixedStreamTaskEvent |Stream mixing and pushing status, see [ByteRTCMixedStreamTaskEvent](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMixedStreamTaskEvent). |
|info |ByteRTCMixedStreamTaskInfo\* |Task details, see [ByteRTCMixedStreamTaskInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMixedStreamTaskInfo). |
|errorCode |ByteRTCMixedStreamTaskErrorCode |Errors occurring during the pushing process. See [ByteRTCMixedStreamTaskErrorCode](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCMixedStreamTaskErrorCode). |


<span id="ByteRTCEngineDelegate-rtcengine-onsinglestreamevent-withtaskid-witherrorcode"></span>
### rtcEngine:onSingleStreamEvent:withTaskId:withErrorCode:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine onSingleStreamEvent:(ByteRTCSingleStreamTaskEvent)event withTaskId:(NSString*)taskId withErrorCode:(ByteRTCSingleStreamTaskErrorCode)errorCode;
```


> Available since 3.60.


Reports events during pushing a single stream to CDN.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object. |
|event |ByteRTCSingleStreamTaskEvent |Stream pushing status, see [ByteRTCSingleStreamTaskEvent](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCSingleStreamTaskEvent). |
|taskId |NSString\* |Task ID. |
|errorCode |ByteRTCSingleStreamTaskErrorCode |Errors occurring during the pushing process. See [ByteRTCSingleStreamTaskErrorCode](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCSingleStreamTaskErrorCode). |


<span id="ByteRTCEngineDelegate-rtcengine-onremotesnapshottakentofile-info-filepath-width-height-errorcode-taskid"></span>
### rtcEngine:onRemoteSnapshotTakenToFile:info:filePath:width:height:errorCode:taskId:

```objectivec
- (void)rtcEngine:(ByteRTCEngine*_Nonnull)engine onRemoteSnapshotTakenToFile:(NSString* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info filePath:(NSString* _Nonnull)filePath width:(NSInteger)width height:(NSInteger)height errorCode:(ByteRTCSnapshotErrorCode)errorCode taskId:(NSInteger)taskId;
```


> Available since 3.60.


Triggered after calling [takeRemoteSnapshotToFile:filePath:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-takeremotesnapshottofile-filepath) to report whether the snapshot is taken successfully and provide details of the snapshot image.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object. |
|streamId |NSString\* |ID of the video stream for taking snapshot. |
|info |ByteRTCStreamInfo\* |Stream information, see [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo). |
|filePath |NSString\* |The path where the snapshot file is saved. |
|width |NSInteger |The width (px) of the snapshot image. |
|height |NSInteger |The height (px) of the snapshot image. |
|errorCode |ByteRTCSnapshotErrorCode |The error code for the snapshot task. See [ByteRTCSnapshotErrorCode](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCSnapshotErrorCode) for specific indications. |
|taskId |NSInteger |The index of the snapshot task, which matches the return value of [takeRemoteSnapshotToFile:filePath:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-takeremotesnapshottofile-filepath). |


<span id="ByteRTCEngineDelegate-rtcengine-onlocalsnapshottakentofile-filepath-width-height-errorcode-taskid"></span>
### rtcEngine:onLocalSnapshotTakenToFile:filePath:width:height:errorCode:taskId:

```objectivec
- (void)rtcEngine:(ByteRTCEngine*_Nonnull)engine onLocalSnapshotTakenToFile:(ByteRTCVideoSource* _Nullable)videoSource filePath:(NSString* _Nonnull)filePath width:(NSInteger)width height:(NSInteger)height errorCode:(ByteRTCSnapshotErrorCode)errorCode taskId:(NSInteger)taskId;
```


> Available since 3.60.


Triggered after calling [takeLocalSnapshotToFile:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-takelocalsnapshottofile) to report whether the snapshot is taken successfully and provide details of the snapshot image.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object. |
|videoSource |ByteRTCVideoSource\* |Reserved parameter |
|filePath |NSString\* |The path where the snapshot file is saved. |
|width |NSInteger |The width (px) of the snapshot image. |
|height |NSInteger |The height (px) of the snapshot image. |
|errorCode |ByteRTCSnapshotErrorCode |The error code for the snapshot task. See [ByteRTCSnapshotErrorCode](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCSnapshotErrorCode) for specific indications. |
|taskId |NSInteger |The index of the snapshot task, which matches the return value of [takeLocalSnapshotToFile:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-takelocalsnapshottofile). |


<span id="ByteRTCEngineDelegate-rtcengine-log"></span>
### rtcEngine:log:

```objectivec
- (void)rtcEngine:(ByteRTCEngine* _Nonnull)engine log:(NSDictionary* _Nonnull)dict;
```


> Deprecated since 3.45 and will be deleted in 3.51.


SDK Internal log callbacks.

SDK internal runtime will call back the log to the business side to facilitate troubleshooting.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|engine |ByteRTCEngine\* |ByteRTCEngine object. |
|dict |NSDictionary\* |Log content. |


<span id="ByteRTCFaceDetectionObserver"></span>
# ByteRTCFaceDetectionObserver

```objectivec
@protocol ByteRTCFaceDetectionObserver <NSObject>
```


Face detection observer

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onFaceDetectResult:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCFaceDetectionObserver-onfacedetectresult) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCFaceDetectionObserver-onfacedetectresult"></span>
### onFaceDetectResult:

```objectivec
- (void)onFaceDetectResult:(ByteRTCFaceDetectionResult* _Nonnull)result;
```


Callback of the result of face detection with Effect SDK.

After calling [enableFaceDetection:withInterval:withModelPath:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCVideoEffect-enablefacedetection-withinterval-withmodelpath) and using the Effect SDK integrated in the RTC SDK, you will receive this callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|result |ByteRTCFaceDetectionResult\* |Face detection result. See [ByteRTCFaceDetectionResult](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCFaceDetectionResult). |


<span id="ByteRTCEncryptHandler"></span>
# ByteRTCEncryptHandler

```objectivec
@protocol ByteRTCEncryptHandler <NSObject>
```


Custom encryption interface

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|NSData\* |[onEncryptData:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEncryptHandler-onencryptdata) |
|NSData\* |[onDecryptData:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEncryptHandler-ondecryptdata) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCEncryptHandler-onencryptdata"></span>
### onEncryptData:

```objectivec
- (NSData* _Nonnull) onEncryptData:(NSData* _Nonnull)rawData;
```


Custom encryption.

Encrypts audio & video frame data before transmission using the custom encryption method set.

Encryption of the original audio and video frames is currently not available.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rawData |NSData\* |Original audio & video frame data |


**Return Value**

Encrypted data


* Non\-empty, indicating that the encrypted data

* Is empty, indicating that the data has been discarded


**Notes**


* Before using this interface for custom encryption, you must first set the custom encryption method. See `setCustomizeEncryptHandler:`.

* Use [onDecryptData:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEncryptHandler-ondecryptdata) to decrypt encrypted audio & video frame data.

* The returned data size should be controlled within 90%~ 120% of the original data source, otherwise it will be discarded.

    &nbsp;


<span id="ondecryptdata"></span>
### onDecryptData:

```objectivec
- (NSData* _Nonnull) onDecryptData:(NSData* _Nonnull)rawData;
```


Custom decryption.

Decrypts custom encrypted audio & video frame data. For custom encryption, see [onEncryptData:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCEncryptHandler-onencryptdata).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rawData |NSData\* |Received encrypted audio & video frame data |


**Return Value**

Decrypted data


* Non\-empty, indicating that the decrypted data

* Is empty, indicating that the frame is discarded


**Notes**


* Before using this interface to decrypt, you must first set the decryption method. See `setCustomizeEncryptHandler:`.

* The returned data size should be controlled within 90%~ 120% of the original data source, otherwise it will be discarded.

    &nbsp;


<span id="bytertcwtnstreamdelegate"></span>
# ByteRTCWTNStreamDelegate

```objectivec
BYTERTC_APPLE_EXPORT @protocol ByteRTCWTNStreamDelegate<NSObject>
```


WTN event handler.

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onWTNRemoteVideoStats:videoStats:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCWTNStreamDelegate-onwtnremotevideostats-videostats) |
|void |[onWTNRemoteAudioStats:audioStats:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCWTNStreamDelegate-onwtnremoteaudiostats-audiostats) |
|void |[onWTNVideoSubscribeStateChanged:state:reason:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCWTNStreamDelegate-onwtnvideosubscribestatechanged-state-reason) |
|void |[onWTNAudioSubscribeStateChanged:state:reason:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCWTNStreamDelegate-onwtnaudiosubscribestatechanged-state-reason) |
|void |[onWTNFirstRemoteVideoFrameDecoded:withFrameInfo:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCWTNStreamDelegate-onwtnfirstremotevideoframedecoded-withframeinfo) |
|void |[onWTNFirstRemoteAudioFrame:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCWTNStreamDelegate-onwtnfirstremoteaudioframe) |
|void |[onWTNSEIMessageReceived:andChannelId:andMessage:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCWTNStreamDelegate-onwtnseimessagereceived-andchannelid-andmessage) |
|void |[onWTNDataMessageReceived:andMessage:andSourceType:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCWTNStreamDelegate-onwtndatamessagereceived-andmessage-andsourcetype) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCWTNStreamDelegate-onwtnremotevideostats-videostats"></span>
### onWTNRemoteVideoStats:videoStats:

```objectivec
- (void)onWTNRemoteVideoStats:(NSString* _Nonnull)streamId
                   videoStats:(const ByteRTCRemoteVideoStats* _Nonnull)videoStats;
```


> Available since 3.60.


Remote WTN video stream ID and statistics.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of the WTN stream |
|videoStats |const ByteRTCRemoteVideoStats\* |Remote WTN video stream statistics. See [ByteRTCRemoteVideoStats](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRemoteVideoStats). |


<span id="ByteRTCWTNStreamDelegate-onwtnremoteaudiostats-audiostats"></span>
### onWTNRemoteAudioStats:audioStats:

```objectivec
- (void)onWTNRemoteAudioStats:(NSString* _Nonnull)streamId
                   audioStats:(const ByteRTCRemoteAudioStats* _Nonnull)audioStats;
```


> Available since 3.60.


Remote WTN audio stream ID and statistics.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of the WTN stream |
|audioStats |const ByteRTCRemoteAudioStats\* |Remote audio stream statistic. See [ByteRTCRemoteAudioStats](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRemoteAudioStats). |


<span id="ByteRTCWTNStreamDelegate-onwtnvideosubscribestatechanged-state-reason"></span>
### onWTNVideoSubscribeStateChanged:state:reason:

```objectivec
- (void)onWTNVideoSubscribeStateChanged:(NSString*_Nonnull)streamId
                                  state:(ByteRTCWTNSubscribeState)state reason:(ByteRTCWTNSubscribeStateChangeReason)reason;
```


> Available since 3.60. Since version 3.60, this callback replaces `rtcEngine:onPlayPublicStreamResult:errorCode:` for reporting the subscription status changes of WTN video streams. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this callback.


Callback for the change of WTN video stream's subscription status

You will be informed of the result of subscribing to the WTN video stream by this callback after calling [subscribeWTNVideoStream:subscribe:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCWTNStream-subscribewtnvideostream-subscribe).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of the WTN video stream |
|state |ByteRTCWTNSubscribeState |Video stream state code. See [ByteRTCWTNSubscribeState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCWTNSubscribeState) for specific indications. |
|reason |ByteRTCWTNSubscribeStateChangeReason |The reason why subscription state changes. See [ByteRTCWTNSubscribeStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCWTNSubscribeStateChangeReason). |


<span id="ByteRTCWTNStreamDelegate-onwtnaudiosubscribestatechanged-state-reason"></span>
### onWTNAudioSubscribeStateChanged:state:reason:

```objectivec
- (void)onWTNAudioSubscribeStateChanged:(NSString*_Nonnull)streamId
                                  state:(ByteRTCWTNSubscribeState)state reason:(ByteRTCWTNSubscribeStateChangeReason)reason;
```


> Available since 3.60. Since version 3.60, this callback replaces `rtcEngine:onPlayPublicStreamResult:errorCode:` for reporting the subscription status changes of WTN audio streams. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this callback.


Callback for the change of WTN audio stream's subscription status

You will be informed of the result of subscribing to the WTN audio stream by this callback after calling [subscribeWTNAudioStream:subscribe:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCWTNStream-subscribewtnaudiostream-subscribe).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of the WTN audio stream |
|state |ByteRTCWTNSubscribeState |Audio stream state code. See [ByteRTCWTNSubscribeStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCWTNSubscribeStateChangeReason). |
|reason |ByteRTCWTNSubscribeStateChangeReason |The reason why subscription state changes. See [ByteRTCWTNSubscribeStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCWTNSubscribeStateChangeReason). |


<span id="ByteRTCWTNStreamDelegate-onwtnfirstremotevideoframedecoded-withframeinfo"></span>
### onWTNFirstRemoteVideoFrameDecoded:withFrameInfo:

```objectivec
- (void)onWTNFirstRemoteVideoFrameDecoded:(NSString* _Nonnull)streamId withFrameInfo:(ByteRTCVideoFrameInfo* _Nonnull)frameInfo NS_SWIFT_NAME(onWTNFirstRemoteVideoFrameDecoded(streamId:withFrameInfo:));
```


> Available since 3.60. Since version 3.60, this callback replaces `onWTNFirstRemoteVideoFrameDecoded:withFrameInfo:`. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this callback.


Callback of successfully decoding of the first video frame of the WTN stream

Refer to [subscribeWTNVideoStream:subscribe:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCWTNStream-subscribewtnvideostream-subscribe) for details about subscribing to a WTN stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of the WTN stream |
|frameInfo |ByteRTCVideoFrameInfo\* |Information of the video stream. Refer to [ByteRTCVideoFrameInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoFrameInfo) for more details. |


<span id="ByteRTCWTNStreamDelegate-onwtnfirstremoteaudioframe"></span>
### onWTNFirstRemoteAudioFrame:

```objectivec
- (void)onWTNFirstRemoteAudioFrame:(NSString* _Nonnull)streamId;
```


> Available since 3.60. Since version 3.60, this callback replaces `rtcEngine:onFirstPublicStreamAudioFrame:`. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this callback.


Callback of successfully decoding of the first audio frame of the WTN stream

Refer to [subscribeWTNAudioStream:subscribe:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCWTNStream-subscribewtnaudiostream-subscribe) for details about subscribing to a WTN audio stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of the WTN stream |


<span id="ByteRTCWTNStreamDelegate-onwtnseimessagereceived-andchannelid-andmessage"></span>
### onWTNSEIMessageReceived:andChannelId:andMessage:

```objectivec
- (void)onWTNSEIMessageReceived:(NSString* _Nonnull)streamId andChannelId:(int)channelId andMessage:(NSData* _Nonnull)message;
```


> Available since 3.60. Since version 3.60, this callback replaces `rtcEngine:onPublicStreamSEIMessageReceived:andMessage:andSourceType:` for the following function. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this callback.


Callback on receiving the SEI message carried by the WTN video stream.

After [subscribeWTNAudioStream:subscribe:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCWTNStream-subscribewtnaudiostream-subscribe)/[subscribeWTNVideoStream:subscribe:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCWTNStream-subscribewtnvideostream-subscribe), you will receive this callback if the WTN stream has an SEI message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |The ID of the WTN stream. |
|channelId |int |SEI message channel ID. The value range is [0 \- 255]. With this parameter, you can set different ChannelIDs for different recipients. In this way, different recipients can choose the SEI information based on the ChannelID received in the callback. |
|message |NSData\* |The SEI(supplemental enhancement information) message carried by the WTN video stream.<br><br>&nbsp;<br><br>The SEI you can get via this callback is inserted by calling `sendPublicStreamSEIMessage` in the SDK.<br><br>You receive SEI from all the video streams if the SEI messages do not have conflicts. However, if the SEI messages from different video streams have conflicts, you will receive only one of them. |


**Notes**

You can get the custom information inserted by calling the Open API via the callback [onWTNDataMessageReceived:andMessage:andSourceType:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCWTNStreamDelegate-onwtndatamessagereceived-andmessage-andsourcetype).

<span id="ByteRTCWTNStreamDelegate-onwtndatamessagereceived-andmessage-andsourcetype"></span>
### onWTNDataMessageReceived:andMessage:andSourceType:

```objectivec
- (void)onWTNDataMessageReceived:(NSString* _Nonnull)streamId andMessage:(NSData* _Nonnull)message andSourceType:(ByteRTCDataMessageSourceType)sourceType;
```


> Available since 3.60.


Callback on receiving the data message carried by the WTN video stream.

After subscribing to the WTN stream via [subscribeWTNAudioStream:subscribe:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCWTNStream-subscribewtnaudiostream-subscribe) / [subscribeWTNVideoStream:subscribe:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCWTNStream-subscribewtnvideostream-subscribe), you can obtain data messages from the WTN stream through this callback, including SEI messages and volume callbacks sent by calling the Open API.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |ID of the WTN stream |
|message |NSData\* |The data messages carried by the WTN video stream.<br><br><br>&nbsp;<br><br>* Data inserted by calling the OpenAPI.<br><br>* Media volume in JSON, before you can receive which you need to enable it via calling the OpenAPI. Refer to the definition below to parse the JSON string.<br><br>   {<br><br>&nbsp;<br><br>   "Type" : "VolumeIndication", //Specific business type.<br><br>&nbsp;<br><br>   "VolumeInfos" : [ // Business type corresponding information<br><br>&nbsp;<br><br>   {<br><br>&nbsp;<br><br>   "RoomId":"1000001", // Room ID<br><br>&nbsp;<br><br>   "UserId":"1000001", // User ID<br><br>&nbsp;<br><br>   "StreamType":0, // 0:camera stream；1:screen stream<br><br>&nbsp;<br><br>   "LinearVolume":1 // LinearVolume<br><br>&nbsp;<br><br>   } |
|sourceType |ByteRTCDataMessageSourceType |Message source. |


**Notes**

You also need to listen to [onWTNSEIMessageReceived:andChannelId:andMessage:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCWTNStreamDelegate-onwtnseimessagereceived-andchannelid-andmessage) to receive SEI inserted via API by the client SDK.

<span id="ByteRTCVideoSnapshotCallbackDelegate"></span>
# ByteRTCVideoSnapshotCallbackDelegate

```objectivec
BYTERTC_APPLE_EXPORT @protocol ByteRTCVideoSnapshotCallbackDelegate <NSObject>
```


Screenshot\-taking callback class.

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onTakeLocalSnapshotResult:videoSource:image:errorCode:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCVideoSnapshotCallbackDelegate-ontakelocalsnapshotresult-videosource-image-errorcode) |
|void |[onTakeRemoteSnapshotResult:streamId:info:image:errorCode:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCVideoSnapshotCallbackDelegate-ontakeremotesnapshotresult-streamid-info-image-errorcode) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCVideoSnapshotCallbackDelegate-ontakelocalsnapshotresult-videosource-image-errorcode"></span>
### onTakeLocalSnapshotResult:videoSource:image:errorCode:

```objectivec
- (void)onTakeLocalSnapshotResult:(NSInteger) taskId
                      videoSource:(ByteRTCVideoSource* _Nullable)videoSource
                            image:(ByteRTCImage* _Nullable)image
                        errorCode:(NSInteger)errorCode;
```


Receives the callback after calling [takeLocalSnapshot:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-takelocalsnapshot).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|taskId |NSInteger |The index for the snapshot, the same as the return value of [takeLocalSnapshot:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-takelocalsnapshot). |
|videoSource |ByteRTCVideoSource\* |Reserved parameter |
|image |ByteRTCImage\* |The snapshot image. If the snapshot task fails, the value is `null`. |
|errorCode |NSInteger |Error code:<br><br><br>&nbsp;<br><br>* 0: Success.<br><br>* \-1: Failure. Fails to generate the image.<br><br>* \-2: Failure. The stream is invalid.<br><br>* \-3: Failure. snapshot timeout, default 1s. |


<span id="ByteRTCVideoSnapshotCallbackDelegate-ontakeremotesnapshotresult-streamid-info-image-errorcode"></span>
### onTakeRemoteSnapshotResult:streamId:info:image:errorCode:

```objectivec
- (void)onTakeRemoteSnapshotResult:(NSInteger)taskId
                              streamId:(NSString*)streamId
                                  info:(ByteRTCStreamInfo* _Nonnull)info
                                 image:(ByteRTCImage* _Nullable)image
                             errorCode:(NSInteger)errorCode;
```


Receives the callback after calling [takeRemoteSnapshot:callback:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-takeremotesnapshot-callback).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|taskId |NSInteger |The index for the remote snapshot, the same as the return value of [takeRemoteSnapshot:callback:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-takeremotesnapshot-callback). |
|streamId |NSString\* |The ID of the remote video stream. |
|info |ByteRTCStreamInfo\* |See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo). |
|image |ByteRTCImage\* |The snapshot image. If the snapshot task fails, the value is `null`. |
|errorCode |NSInteger |Error code:<br><br><br>&nbsp;<br><br>* 0: Success.<br><br>* \-1: Failure. Fails to generate the image.<br><br>* \-2: Failure. The stream is invalid.<br><br>* \-3: Failure. snapshot timeout, default 1s. |


<span id="ByteRTCAudioFrameObserver"></span>
# ByteRTCAudioFrameObserver

```objectivec
@protocol ByteRTCAudioFrameObserver <NSObject>
```


Audio data callback observer

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

The time interval for all callback functions in this interface is 20 ms.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onRecordAudioFrame:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCAudioFrameObserver-onrecordaudioframe) |
|void |[onPlaybackAudioFrame:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCAudioFrameObserver-onplaybackaudioframe) |
|void |[onRemoteUserAudioFrame:info:audioFrame:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCAudioFrameObserver-onremoteuseraudioframe-info-audioframe) |
|void |[onMixedAudioFrame:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCAudioFrameObserver-onmixedaudioframe) |
|void |[onCaptureMixedAudioFrame:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCAudioFrameObserver-oncapturemixedaudioframe) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCAudioFrameObserver-onrecordaudioframe"></span>
### onRecordAudioFrame:

```objectivec
- (void)onRecordAudioFrame:(ByteRTCAudioFrame* _Nonnull)audioFrame;
```


Returns audio data recorded by microphone

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrame |ByteRTCAudioFrame\* |Audio data recorded by microphone, see [ByteRTCAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFrame) |


<span id="ByteRTCAudioFrameObserver-onplaybackaudioframe"></span>
### onPlaybackAudioFrame:

```objectivec
- (void)onPlaybackAudioFrame:(ByteRTCAudioFrame* _Nonnull)audioFrame;
```


Returns the mixed audio data of all subscribed remote users

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrame |ByteRTCAudioFrame\* |Mixed audio data, see [ByteRTCAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFrame) |


<span id="ByteRTCAudioFrameObserver-onremoteuseraudioframe-info-audioframe"></span>
### onRemoteUserAudioFrame:info:audioFrame:

```objectivec
- (void)onRemoteUserAudioFrame:(NSString* _Nonnull)streamId
                          info:(ByteRTCStreamInfo* _Nonnull)info
                    audioFrame:(ByteRTCAudioFrame* _Nonnull)audioFrame;
```


Returns the audio data of one remote user.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |The unique identifier of the remote stream. |
|info |ByteRTCStreamInfo\* |Detailed information of the remote stream. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo). |
|audioFrame |ByteRTCAudioFrame\* |Audio data. See [ByteRTCAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFrame). |


**Notes**

This callback works on the playback thread. Don't do anything time\-consuming in this callback, or it may affect the entire audio playback chain.

<span id="ByteRTCAudioFrameObserver-onmixedaudioframe"></span>
### onMixedAudioFrame:

```objectivec
- (void)onMixedAudioFrame:(ByteRTCAudioFrame* _Nonnull)audioFrame;
```


Returns mixed audio data including both data recorded by the local microphone and data from all subscribed remote users

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrame |ByteRTCAudioFrame\* |Mixed audio data, see [ByteRTCAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFrame) |


<span id="ByteRTCAudioFrameObserver-oncapturemixedaudioframe"></span>
### onCaptureMixedAudioFrame:

```objectivec
- (void)onCaptureMixedAudioFrame:(ByteRTCAudioFrame* _Nonnull)audioFrame;
```


Return the mixed audio data of the data recorded by local microphone and the audio data of `MediaPlayer` and `EffectPlayer`.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrame |ByteRTCAudioFrame\* |Mixed audio data, see [ByteRTCAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFrame) |


<span id="ByteRtcScreenCapturerExtDelegate"></span>
# ByteRtcScreenCapturerExtDelegate

```objectivec
BYTE_RTC_EXPORT @protocol ByteRtcScreenCapturerExtDelegate <NSObject>
```


Screen capture related extension delegate, used for SDK internal capture only.

```Plain Text
   The SampleHandler generated after the user creates the extension needs to inherit this delegate to implement screen sharing related capabilities. 
```


Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onQuitFromApp](https://docs.byteplus.com/en/docs/12/16382#ByteRtcScreenCapturerExtDelegate-onquitfromapp) |
|void |[onReceiveMessageFromApp:](https://docs.byteplus.com/en/docs/12/16382#ByteRtcScreenCapturerExtDelegate-onreceivemessagefromapp) |
|void |[onSocketDisconnect](https://docs.byteplus.com/en/docs/12/16382#ByteRtcScreenCapturerExtDelegate-onsocketdisconnect) |
|void |[onSocketConnect](https://docs.byteplus.com/en/docs/12/16382#ByteRtcScreenCapturerExtDelegate-onsocketconnect) |
|void |[onNotifyAppRunning](https://docs.byteplus.com/en/docs/12/16382#ByteRtcScreenCapturerExtDelegate-onnotifyapprunning) |


<span id="instructions"></span>
## Instructions

<span id="ByteRtcScreenCapturerExtDelegate-onquitfromapp"></span>
### onQuitFromApp

```objectivec
- (void)onQuitFromApp;
```


Notify Broadcast Upload Extension to stop capturing and exit.

**Notes**

After the user calls [stopScreenCapture](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-stopscreencapture), this method will be triggered to notify the SDK on the Extension side to stop the screen capture.

<span id="ByteRtcScreenCapturerExtDelegate-onreceivemessagefromapp"></span>
### onReceiveMessageFromApp:

```objectivec
- (void)onReceiveMessageFromApp:(NSData*)message;
```


The callback is triggered when the socket receives a message from the App side

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|message |NSData\* |Message received from the App side |


<span id="ByteRtcScreenCapturerExtDelegate-onsocketdisconnect"></span>
### onSocketDisconnect

```objectivec
- (void)onSocketDisconnect;
```


This callback is triggered when the socket is disconnected

<span id="ByteRtcScreenCapturerExtDelegate-onsocketconnect"></span>
### onSocketConnect

```objectivec
- (void)onSocketConnect;
```


This callback is triggered when the socket is successfully connected

<span id="ByteRtcScreenCapturerExtDelegate-onnotifyapprunning"></span>
### onNotifyAppRunning

```objectivec
- (void)onNotifyAppRunning;
```


This callback is triggered when the App is detected to be making an audio/video call.

<span id="ByteRTCAudioEffectPlayerEventHandler"></span>
# ByteRTCAudioEffectPlayerEventHandler

```objectivec
@protocol ByteRTCAudioEffectPlayerEventHandler <NSObject>
```


Event handler for [ByteRTCAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCAudioEffectPlayer). You must call [setEventHandler:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCAudioEffectPlayer-seteventhandler) to set the corresponding event handler to get the events.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onAudioEffectPlayerStateChanged:state:error:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCAudioEffectPlayerEventHandler-onaudioeffectplayerstatechanged-state-error) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCAudioEffectPlayerEventHandler-onaudioeffectplayerstatechanged-state-error"></span>
### onAudioEffectPlayerStateChanged:state:error:

```objectivec
-(void)onAudioEffectPlayerStateChanged:(int)effectId state:(ByteRTCPlayerState)state error:(ByteRTCPlayerError)error;
```


Callback for audio mixing status change.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|effectId |int |The ID of [ByteRTCAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCAudioEffectPlayer). Set by [getAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-getaudioeffectplayer). |
|state |ByteRTCPlayerState |See [ByteRTCPlayerState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCPlayerState). |
|error |ByteRTCPlayerError |See [ByteRTCPlayerError](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCPlayerError). |


<span id="ByteRTCAudioFrameProcessor"></span>
# ByteRTCAudioFrameProcessor

```objectivec
@protocol ByteRTCAudioFrameProcessor <NSObject>
```


Custom audio processor

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[onProcessRecordAudioFrame:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCAudioFrameProcessor-onprocessrecordaudioframe) |
|int |[onProcessPlayBackAudioFrame:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCAudioFrameProcessor-onprocessplaybackaudioframe) |
|int |[onProcessRemoteUserAudioFrame:info:audioFrame:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCAudioFrameProcessor-onprocessremoteuseraudioframe-info-audioframe) |
|int |[onProcessEarMonitorAudioFrame:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCAudioFrameProcessor-onprocessearmonitoraudioframe) |
|int |[onProcessScreenAudioFrame:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCAudioFrameProcessor-onprocessscreenaudioframe) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCAudioFrameProcessor-onprocessrecordaudioframe"></span>
### onProcessRecordAudioFrame:

```objectivec
- (int)onProcessRecordAudioFrame:(ByteRTCAudioFrame* _Nonnull)audioFrame;
```


Returns the address of the locally captured audio frame for custom processing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrame |ByteRTCAudioFrame\* |The address of the audio frame. See [ByteRTCAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFrame). |


**Return Value**


* 0: Success.

* <0: Failure.


**Notes**


* After custom processing, SDK will encode the processed audio frames and transmit to the remote user. The processing does not affect the SDK\-level ear\-monitoring audio.

* To enable this callback, call [enableAudioProcessor:audioFormat:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-enableaudioprocessor-audioformat). You will receive this callback every 10 ms.

    &nbsp;


<span id="onprocessplaybackaudioframe"></span>
### onProcessPlayBackAudioFrame:

```objectivec
- (int)onProcessPlayBackAudioFrame:(ByteRTCAudioFrame* _Nonnull)audioFrame;
```


Returns the address of the locally captured audio frame for custom processing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrame |ByteRTCAudioFrame\* |The address of the audio frame. See [ByteRTCAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFrame) |


**Notes**

After calling [enableAudioProcessor:audioFormat:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-enableaudioprocessor-audioformat) with mixed remote audio, you will receive this callback every 10 ms.

<span id="ByteRTCAudioFrameProcessor-onprocessremoteuseraudioframe-info-audioframe"></span>
### onProcessRemoteUserAudioFrame:info:audioFrame:

```objectivec
- (int)onProcessRemoteUserAudioFrame:(NSString* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info audioFrame:(ByteRTCAudioFrame* _Nonnull)audioFrame;
```


Returns the address of the locally captured audio frame for custom processing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |The unique identifier of the audio stream. |
|info |ByteRTCStreamInfo\* |Detailed information of the audio stream. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo) |
|audioFrame |ByteRTCAudioFrame\* |The address of the audio frame. See [ByteRTCAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFrame) |


**Notes**

After calling [enableAudioProcessor:audioFormat:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-enableaudioprocessor-audioformat), with audio streams of the remote users, you will receive this callback every 10 ms.

<span id="ByteRTCAudioFrameProcessor-onprocessearmonitoraudioframe"></span>
### onProcessEarMonitorAudioFrame:

```objectivec
- (int)onProcessEarMonitorAudioFrame:(ByteRTCAudioFrame* _Nonnull)audioFrame;
```


> Available since 3.50


You will receive the address of SDK\-level in\-ear monitoring audio frames for custom processing.

The audio effects set by `setVoiceReverbType:` and `setVoiceChangerType:` are included.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrame |ByteRTCAudioFrame\* |The address of the in\-ear monitoring audio frames. See [ByteRTCAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFrame). |


**Return Value**


* 0: Success.

* <0: Failure.


**Notes**


* Modifying the data affects only SDK\-level in\-ear monitoring audio.

* To enable this callback, call [enableAudioProcessor:audioFormat:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-enableaudioprocessor-audioformat). You will receive this callback every 10 ms.

    &nbsp;


<span id="onprocessscreenaudioframe"></span>
### onProcessScreenAudioFrame:

```objectivec
- (int)onProcessScreenAudioFrame:(ByteRTCAudioFrame* _Nonnull)audioFrame;
```


Returns the address of the shared\-screen audio frames for custom processing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audioFrame |ByteRTCAudioFrame\* |The address of audio frames. See [ByteRTCAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAudioFrame). |


**Notes**

After calling `enableAudioProcessor:` to set the audio input to the shared\-screen audio, you will receive this callback every 10 ms.

<span id="ByteRTCRoomDelegate"></span>
# ByteRTCRoomDelegate

```objectivec
@protocol ByteRTCRoomDelegate <NSObject>
```


Room event callback interface

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo) |
|void |[rtcRoom:onLeaveRoom:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onleaveroom) |
|void |[rtcRoom:onAVSyncStateChange:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onavsyncstatechange) |
|void |[rtcRoom:onVideoPublishStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onvideopublishstatechanged-info-state-reason) |
|void |[rtcRoom:onAudioPublishStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onaudiopublishstatechanged-info-state-reason) |
|void |[rtcRoom:onVideoSubscribeStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onvideosubscribestatechanged-info-state-reason) |
|void |[rtcRoom:onAudioSubscribeStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onaudiosubscribestatechanged-info-state-reason) |
|void |[rtcRoom:onRoomStats:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onroomstats) |
|void |[rtcRoom:onLocalStreamStats:info:stats:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onlocalstreamstats-info-stats) |
|void |[rtcRoom:onRemoteStreamStats:info:stats:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onremotestreamstats-info-stats) |
|void |[rtcRoom:onUserJoined:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onuserjoined) |
|void |[rtcRoom:onUserLeave:reason:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onuserleave-reason) |
|void |[onTokenWillExpire:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-ontokenwillexpire) |
|void |[onPublishPrivilegeTokenWillExpire:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-onpublishprivilegetokenwillexpire) |
|void |[onSubscribePrivilegeTokenWillExpire:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-onsubscribeprivilegetokenwillexpire) |
|void |[rtcRoom:onAVSyncEvent:userId:eventCode:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onavsyncevent-userid-eventcode) |
|void |[rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish) |
|void |[rtcRoom:onUserPublishStreamAudio:info:isPublish:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamaudio-info-ispublish) |
|void |[rtcRoom:onRoomMessageReceived:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onroommessagereceived-message) |
|void |[rtcRoom:onRoomBinaryMessageReceived:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onroombinarymessagereceived-message) |
|void |[rtcRoom:onUserMessageReceived:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onusermessagereceived-message) |
|void |[rtcRoom:onUserBinaryMessageReceived:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onuserbinarymessagereceived-message) |
|void |[rtcRoom:onRoomMessageReceived:uid:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onroommessagereceived-uid-message) |
|void |[rtcRoom:onRoomBinaryMessageReceived:uid:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onroombinarymessagereceived-uid-message) |
|void |[rtcRoom:onUserMessageReceived:uid:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onusermessagereceived-uid-message) |
|void |[rtcRoom:onUserBinaryMessageReceived:uid:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onuserbinarymessagereceived-uid-message) |
|void |[rtcRoom:onUserMessageSendResult:error:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onusermessagesendresult-error) |
|void |[rtcRoom:onRoomMessageSendResult:error:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onroommessagesendresult-error) |
|void |[rtcRoom:onSetRoomExtraInfoResult:result:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onsetroomextrainforesult-result) |
|void |[rtcRoom:onRoomExtraInfoUpdate:value:lastUpdateUserId:lastUpdateTimeMs:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onroomextrainfoupdate-value-lastupdateuserid-lastupdatetimems) |
|void |[rtcRoom:onRoomStreamExtraInfoUpdate:info:extraInfo:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onroomstreamextrainfoupdate-info-extrainfo) |
|void |[rtcRoom:onUserVisibilityChanged:errorCode:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onuservisibilitychanged-errorcode) |
|void |[rtcRoom:onVideoStreamBanned:isBanned:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onvideostreambanned-isbanned) |
|void |[rtcRoom:onAudioStreamBanned:isBanned:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onaudiostreambanned-isbanned) |
|void |[rtcRoom:onForwardStreamStateChanged:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onforwardstreamstatechanged) |
|void |[rtcRoom:onForwardStreamEvent:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onforwardstreamevent) |
|void |[rtcRoom:onNetworkQuality:remoteQualities:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onnetworkquality-remotequalities) |
|void |[deprecated] [rtcRoom:onStreamStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onstreamstatechanged-withuid-state-extrainfo) |
|void |[deprecated] [rtcRoom:onStreamAdd:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onstreamadd) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo"></span>
### rtcRoom:onRoomStateChanged:withUid:state:extraInfo:

```objectivec
- (void)rtcRoom:(ByteRTCRoom*_Nonnull)rtcRoom onRoomStateChanged:(NSString*_Nonnull)roomId
             withUid:(nonnull NSString*)uid
               state:(NSInteger)state
           extraInfo:(NSString*_Nonnull)extraInfo;
```


Callback on room state changes. Via this callback you get notified of room relating warnings, errors and events. For example, the user joins the room, the user is removed from the room, and so on.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCAudioRoom instance |
|roomId |NSString\* |Room ID. |
|uid |NSString\* |User ID. |
|state |NSInteger |Room state code.<br><br><br>&nbsp;<br><br>* 0: Join room success.<br><br>* !0: Failed to join a room, abnormal exit, room\-related warnings or errors. See [ByteRTCErrorCode](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCErrorCode) and [ByteRTCWarningCode](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCWarningCode) for specific indications. |
|extraInfo |NSString\* |Extra information.<br><br>&nbsp;<br><br>`join_type` indicates the type of room the user joins. `0` means the user joins the room for the first time, and `1` means the user rejoins the room.<br><br>&nbsp;<br><br>`elapsed` indicates the time interval from calling [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig) to successfully joining room, in ms. |


<span id="ByteRTCRoomDelegate-rtcroom-onleaveroom"></span>
### rtcRoom:onLeaveRoom:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onLeaveRoom:(ByteRTCRoomStats*_Nonnull)stats;
```


Leave the room successfully callback.

When the user calls the [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-leaveroom) method, the SDK stops all publish subscription streams and releases all call\-related audio & video resources. This callback notifies the user when the SDK completes all resource releases.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |
|stats |ByteRTCRoomStats\* |Reserved parameter. |


**Notes**


* After the user calls the [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-leaveroom) method to leave the room, if [destroy](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-destroy) is called to destroy the room instance or [destroyRTCEngine](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-destroyrtcengine) method is called to destroy the RTC engine immediately, this callback event will not be received.

* If the app needs to use the system audio & video device after leaving the room, it is recommended to initialize the audio & video device after receiving this callback, otherwise the initialization may fail due to the SDK occupying the audio & video device.

    &nbsp;


<span id="rtcroom-onavsyncstatechange"></span>
### rtcRoom:onAVSyncStateChange:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onAVSyncStateChange:(ByteRTCAVSyncState)state;
```


Stream publisher will receive this callback when the A/V synchronization state changes after [setMultiDeviceAVSync:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-setmultideviceavsync) is called.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |The ByteRTCRoom instance. |
|state |ByteRTCAVSyncState |A/V synchronization state, see [ByteRTCAVSyncState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAVSyncState). |


<span id="ByteRTCRoomDelegate-rtcroom-onvideopublishstatechanged-info-state-reason"></span>
### rtcRoom:onVideoPublishStateChanged:info:state:reason:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onVideoPublishStateChanged:(NSString*_Nonnull)streamId
           info:(ByteRTCStreamInfo* _Nonnull)info
           state:(ByteRTCPublishState)state
           reason:(ByteRTCPublishStateChangeReason)reason;
```


> Available since 3.60. Since version 3.60, this callback replaces `rtcRoom:onStreamStateChanged:withUid:state:extraInfo:` for reporting video publishing state changes. If you have upgraded to SDK version 3.60 or later and are still using this method, please migrate to this callback.


Callback on the publishing state change of the local video stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |The ByteRTCRoom instance. |
|streamId |NSString\* |Stream ID. |
|info |ByteRTCStreamInfo\* |Stream information. |
|state |ByteRTCPublishState |Room state code. See [ByteRTCPublishState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCPublishState) for more. |
|reason |ByteRTCPublishStateChangeReason |The reason for the change of the publishing state of the local video stream. See [ByteRTCPublishStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCPublishStateChangeReason) for more. |


<span id="ByteRTCRoomDelegate-rtcroom-onaudiopublishstatechanged-info-state-reason"></span>
### rtcRoom:onAudioPublishStateChanged:info:state:reason:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onAudioPublishStateChanged:(NSString*_Nonnull)streamId
           info:(ByteRTCStreamInfo* _Nonnull)info
           state:(ByteRTCPublishState)state
           reason:(ByteRTCPublishStateChangeReason)reason;
```


> Available since 3.60. Since version 3.60, this callback replaces `rtcRoom:onStreamStateChanged:withUid:state:extraInfo:` for reporting audio publishing state changes. If you have upgraded to SDK version 3.60 or later and are still using this method, please migrate to this callback.


Callback on the publishing state change of the local audio stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |The ByteRTCRoom instance. |
|streamId |NSString\* |Stream ID. |
|info |ByteRTCStreamInfo\* |Stream information. |
|state |ByteRTCPublishState |Room state code. See [ByteRTCPublishState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCPublishState) for more. |
|reason |ByteRTCPublishStateChangeReason |The reason for the change of the publishing state of the local audio stream. See [ByteRTCPublishStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCPublishStateChangeReason) for more. |


<span id="ByteRTCRoomDelegate-rtcroom-onvideosubscribestatechanged-info-state-reason"></span>
### rtcRoom:onVideoSubscribeStateChanged:info:state:reason:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onVideoSubscribeStateChanged:(NSString*_Nonnull)streamId
           info:(ByteRTCStreamInfo* _Nonnull)info
           state:(ByteRTCSubscribeState)state
           reason:(ByteRTCSubscribeStateChangeReason)reason;
```


> Available since 3.60. Since version 3.60, this callback replaces `rtcRoom:onStreamStateChanged:withUid:state:extraInfo:` and `rtcRoom:onStreamSubscribed:userId:subscribeConfig:` for reporting the state changes of the subscription to camera\-video streams. If you have upgraded to SDK version 3.60 or later and are still using this two methods, please migrate to this callback.


Callback on the publishing state change of the video stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |The ByteRTCRoom instance. |
|streamId |NSString\* |Stream ID. |
|info |ByteRTCStreamInfo\* |Stream information. |
|state |ByteRTCSubscribeState |Room state code. See [ByteRTCPublishState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCPublishState) for more. |
|reason |ByteRTCSubscribeStateChangeReason |The reason for the change of the subscription state of the video stream. See [ByteRTCPublishStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCPublishStateChangeReason) for more. |


**Notes**

You will receive the callback after calling [subscribeStreamVideo:subscribe:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-subscribestreamvideo-subscribe).

<span id="ByteRTCRoomDelegate-rtcroom-onaudiosubscribestatechanged-info-state-reason"></span>
### rtcRoom:onAudioSubscribeStateChanged:info:state:reason:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onAudioSubscribeStateChanged:(NSString*_Nonnull)streamId
            info:(ByteRTCStreamInfo* _Nonnull)info
           state:(ByteRTCSubscribeState)state
           reason:(ByteRTCSubscribeStateChangeReason)reason;
```


> Available since 3.60. Since version 3.60, this callback replaces `rtcRoom:onStreamStateChanged:withUid:state:extraInfo:` and `rtcRoom:onStreamSubscribed:userId:subscribeConfig:` for reporting the state changes of the subscription to camera\-video streams. If you have upgraded to SDK version 3.60 or later and are still using this two methods, please migrate to this callback.


Callback on the subscribing state change of the audio stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |The ByteRTCRoom instance. |
|streamId |NSString\* |Stream ID. |
|info |ByteRTCStreamInfo\* |Stream information. |
|state |ByteRTCSubscribeState |Room state code. See [ByteRTCSubscribeState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCSubscribeState) for more. |
|reason |ByteRTCSubscribeStateChangeReason |The reason for the change of the subscription state of the audio stream. See [ByteRTCSubscribeStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCSubscribeStateChangeReason) for more. |


**Notes**

You will receive the callback after calling [subscribeStreamVideo:subscribe:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-subscribestreamvideo-subscribe).

<span id="ByteRTCRoomDelegate-rtcroom-onroomstats"></span>
### rtcRoom:onRoomStats:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onRoomStats:(ByteRTCRoomStats*_Nonnull)stats NS_SWIFT_NAME(rtcRoom(_:onRoomStats:));
```


In\-room call statistics callback.

After the user enters the room and starts the call, he receives this callback every 2s.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |
|stats |ByteRTCRoomStats\* |Current ByteRTCRoom statistics, see: [ByteRTCRoomStats](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRoomStats) |


<span id="ByteRTCRoomDelegate-rtcroom-onlocalstreamstats-info-stats"></span>
### rtcRoom:onLocalStreamStats:info:stats:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onLocalStreamStats:(NSString*_Nonnull)streamId
           info:(ByteRTCStreamInfo* _Nonnull)info
          stats:(ByteRTCLocalStreamStats*_Nonnull)stats NS_SWIFT_NAME(rtcRoom(_:onLocalStreamStats:));
```


Local stream data statistics and network quality callback.

After the local user publishes the flow successfully, the SDK will periodically (2s) notify the user through this callback event of the quality statistics of the published flow during this reference period.

Statistics are passed to the user through the callback parameters of the [ByteRTCLocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCLocalStreamStats) type, including the sent audio & video bit rate, sent frame rate, encoded frame rate, network quality, etc.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |
|streamId |NSString\* |Stream ID. |
|info |ByteRTCStreamInfo\* |Stream information. |
|stats |ByteRTCLocalStreamStats\* |Current room local stream data statistics. See: [ByteRTCLocalStreamStats](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCLocalStreamStats) |


<span id="ByteRTCRoomDelegate-rtcroom-onremotestreamstats-info-stats"></span>
### rtcRoom:onRemoteStreamStats:info:stats:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onRemoteStreamStats:(NSString*_Nonnull)streamId
           info:(ByteRTCStreamInfo* _Nonnull)info
          stats:(ByteRTCRemoteStreamStats*_Nonnull)stats NS_SWIFT_NAME(rtcRoom(_:onRemoteStreamStats:));
```


Remote audio/video stream statistics and network quality callbacks for local subscriptions.

After the local user subscribes to the stream successfully, the SDK will periodically (2s) notify the user through this callback event of the quality statistics of the subscribed stream during this reference period, including: sending audio & video bit rate, sending frame rate, encoded frame rate, network quality, etc.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |
|streamId |NSString\* |Stream ID. |
|info |ByteRTCStreamInfo\* |Stream information. |
|stats |ByteRTCRemoteStreamStats\* |Current room local stream statistics. See: [ByteRTCRemoteStreamStats](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCRemoteStreamStats) |


<span id="ByteRTCRoomDelegate-rtcroom-onuserjoined"></span>
### rtcRoom:onUserJoined:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onUserJoined:(ByteRTCUserInfo*_Nonnull)userInfo;
```


Callback for when a remote visible user joins the room, or when an invisible user in the room switches to being visible.


1. When a remote user sets themselves to be visible by calling the [setUserVisibility:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-setuservisibility) method and then joins the room, other users in the room will receive this event.

2. When a remote visible user who has been disconnected re\-enters the room, other users in the room will receive this event.

3. When a hidden remote user in the room switches to being visible by calling the [setUserVisibility:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-setuservisibility) method, other users in the room will receive this event.

4. A new user entering the room will receive an entry callback notification for visible users who were already in the room before they entered.


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |
|userInfo |ByteRTCUserInfo\* |For user information. See [ByteRTCUserInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCUserInfo). |


<span id="ByteRTCRoomDelegate-rtcroom-onuserleave-reason"></span>
### rtcRoom:onUserLeave:reason:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onUserLeave:(NSString*_Nonnull)uid reason:(ByteRTCUserOfflineReason)reason;
```


This callback is triggered when a remote user is disconnected or turns invisible.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |
|uid |NSString\* |ID of the user who leaves the RTC room, or switches to invisible. |
|reason |ByteRTCUserOfflineReason |Reason to leave the room:<br><br><br>&nbsp;<br><br>* 0: The remote client calls [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-leaveroom) to leave the room.<br><br>* 1: The remote client is disconnected because of poor network connection or expired Token.<br><br>* 2: The remote client calls [setUserVisibility:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-setuservisibility) to turn invisible.<br><br>* 3: The remote user has been removed from the room by the administrator via a OpenAPI call. |


<span id="ByteRTCRoomDelegate-ontokenwillexpire"></span>
### onTokenWillExpire:

```objectivec
- (void)onTokenWillExpire:( ByteRTCRoom*_Nonnull)rtcRoom;
```


The callback is triggered when the SDK detects the joining room privilege from the Token will expires within 30s.

After receiving this callback, you must call [updateToken:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-updatetoken) to update the joining room privilege Token.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |


**Notes**

After a user's joining room privilege expires:


* When attempting to join a room, the user will receive [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo)with the error code "\-1000" indicating that the Token is invalid.

* If the user is already in the room, he/she will be removed from the room and receive [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo) with the error code "\-1009" indicating that the Token is expired. Remote users in the room will receive [rtcRoom:onUserLeave:reason:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onuserleave-reason) with the reason "2" indicating that the Token is invalid.

    &nbsp;


<span id="onpublishprivilegetokenwillexpire"></span>
### onPublishPrivilegeTokenWillExpire:

```objectivec
- (void)onPublishPrivilegeTokenWillExpire:( ByteRTCRoom*_Nonnull)rtcRoom;
```


Callback triggered 30s before the publishing privilege of the Token expires.

After receiving this callback, you must call [updateToken:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-updatetoken) to update the publishing privilege Token.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |


**Notes**

Once a user's publishing privilege expires:


* Either during stream publishing or when attempting to publish a stream, the user will get the notification of `kPublishStateChangeReasonNoPublishPermission` via [rtcRoom:onVideoPublishStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onvideopublishstatechanged-info-state-reason), [rtcRoom:onAudioPublishStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onaudiopublishstatechanged-info-state-reason).

* The publishing streams of the user will be removed, and remote users in the room will get informed via [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish), [rtcRoom:onUserPublishStreamAudio:info:isPublish:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamaudio-info-ispublish).

    &nbsp;


<span id="onsubscribeprivilegetokenwillexpire"></span>
### onSubscribePrivilegeTokenWillExpire:

```objectivec
- (void)onSubscribePrivilegeTokenWillExpire:( ByteRTCRoom*_Nonnull)rtcRoom;
```


Callback triggered 30s before the subscribing privilege of the Token expires.

After receiving this callback, you must call [updateToken:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-updatetoken) to update the subscribing privilege Token.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |


**Notes**

After a user's subscribing privilege expires, the user will fail to subscribe to new streams, or the subscribed streams will be removed, and he/she will receive [rtcRoom:onVideoSubscribeStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onvideosubscribestatechanged-info-state-reason), [rtcRoom:onAudioSubscribeStateChanged:info:state:reason:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onaudiosubscribestatechanged-info-state-reason) with error code "\-1003" indicating no permission to subscribe to streams.

<span id="ByteRTCRoomDelegate-rtcroom-onavsyncevent-userid-eventcode"></span>
### rtcRoom:onAVSyncEvent:userId:eventCode:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onAVSyncEvent:(NSString*_Nonnull)roomId userId:(NSString*_Nonnull)userId eventCode:(ByteRTCAVSyncEvent)eventCode;
```


> Available since 3.60.


Stream publisher will receive this callback when the A/V synchronization error occurs after [setMultiDeviceAVSync:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-setmultideviceavsync) is called.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object |
|roomId |NSString\* |Room ID. |
|userId |NSString\* |User ID. |
|eventCode |ByteRTCAVSyncEvent |A/V synchronization error, see [ByteRTCAVSyncEvent](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCAVSyncEvent). |


<span id="ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish"></span>
### rtcRoom:onUserPublishStreamVideo:info:isPublish:

```objectivec
- (void)rtcRoom:(ByteRTCRoom* _Nonnull)rtcRoom onUserPublishStreamVideo:(NSString* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info isPublish:(BOOL)isPublish;
```


> Available since 3.60. Since version 3.60, this callback replaces the `onUserPublishStream`, `onUserUnpublishStream`, `onUserPublishScreen` and `onUserUnpublishScreen` methods for the functions described below. If you have upgraded to SDK version 3.60 or later and are still using these methods, please migrate to this callback.


Callback on a remote user publishing or stopping publishing video streams in the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |
|streamId |NSString\* |Stream ID. |
|info |ByteRTCStreamInfo\* |Stream information. |
|isPublish |BOOL |Whether the stream is published.<br><br><br>* `true`: Published.<br><br>* `false`: Stopped publishing. |


**Notes**

You will receive this callback after a remote user successfully published video stream in the room with [publishStreamVideo:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-publishstreamvideo). Then you can choose whether to call [subscribeStreamVideo:subscribe:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-subscribestreamvideo-subscribe) to subscribe to the streams or not.

<span id="ByteRTCRoomDelegate-rtcroom-onuserpublishstreamaudio-info-ispublish"></span>
### rtcRoom:onUserPublishStreamAudio:info:isPublish:

```objectivec
- (void)rtcRoom:(ByteRTCRoom* _Nonnull)rtcRoom onUserPublishStreamAudio:(NSString* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info isPublish:(BOOL)isPublish;
```


> Available since 3.60. Since version 3.60, this callback replaces the `onUserPublishStream`, `onUserUnpublishStream`, `onUserPublishScreen` and `onUserUnpublishScreen` methods for the functions described below. If you have upgraded to SDK version 3.60 or later and are still using these methods, please migrate to this callback.


Callback on a remote user publishing or stopping publishing remote audio streams in the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |
|streamId |NSString\* |Stream ID. |
|info |ByteRTCStreamInfo\* |Stream information. |
|isPublish |BOOL |Whether the stream is published.<br><br><br>* `true`: Published<br><br>* `false`: Removed |


**Notes**

You will receive this callback after a remote user successfully published audio streams in the room with [publishStreamAudio:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-publishstreamaudio). Then you can choose whether to call [subscribeStreamAudio:subscribe:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-subscribestreamaudio-subscribe) to subscribe to the streams or not.

<span id="ByteRTCRoomDelegate-rtcroom-onroommessagereceived-message"></span>
### rtcRoom:onRoomMessageReceived:message:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onRoomMessageReceived:(NSString*_Nonnull)uid
        message:(NSString*_Nonnull)message;
```


> This interface will be deprecated since version 3.64. Use [onRoomMessageReceived:uid:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onroommessagereceived-uid-message) instead.

> Receive this callback when you receive a broadcast text message from the room called [sendRoomMessage:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-sendroommessage).


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object |
|uid |NSString\* |User ID of the message sender. |
|message |NSString\* |The content of the received text message. |


<span id="ByteRTCRoomDelegate-rtcroom-onroombinarymessagereceived-message"></span>
### rtcRoom:onRoomBinaryMessageReceived:message:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onRoomBinaryMessageReceived:(NSString*_Nonnull)uid
        message:(NSData*_Nonnull)message;
```


> This interface will be deprecated since version 3.64. Use [onRoomBinaryMessageReceived:uid:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onroombinarymessagereceived-uid-message) instead.

> Receive this callback when you receive a broadcast binary message sent by the room call [sendRoomBinaryMessage:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-sendroombinarymessage).


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object |
|uid |NSString\* |User ID of the message sender. |
|message |NSData\* |The binary message content received. |


<span id="ByteRTCRoomDelegate-rtcroom-onusermessagereceived-message"></span>
### rtcRoom:onUserMessageReceived:message:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onUserMessageReceived:(NSString*_Nonnull)uid
               message:(NSString*_Nonnull)message;
```


> This interface will be deprecated since version 3.64. Use [onUserMessageReceived:uid:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onusermessagereceived-uid-message) instead.

> Receive text messages (P2P) from other users in the room via [sendUserMessage:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-sendusermessage-message-config).


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object |
|uid |NSString\* |The user ID of the sender of the message. |
|message |NSString\* |The content of the received text message. |


<span id="ByteRTCRoomDelegate-rtcroom-onuserbinarymessagereceived-message"></span>
### rtcRoom:onUserBinaryMessageReceived:message:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onUserBinaryMessageReceived:(NSString*_Nonnull)uid
               message:(NSData*_Nonnull)message;
```


> This interface will be deprecated since version 3.64. Use [onUserBinaryMessageReceived:uid:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onuserbinarymessagereceived-uid-message) instead.

> Receive a binary message from another user in the room via [sendUserBinaryMessage:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-senduserbinarymessage-message-config) Receive this callback.


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object |
|uid |NSString\* |The user ID of the sender of the message. |
|message |NSData\* |The binary message content received. |


<span id="ByteRTCRoomDelegate-rtcroom-onroommessagereceived-uid-message"></span>
### rtcRoom:onRoomMessageReceived:uid:message:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onRoomMessageReceived:(NSInteger)msgid uid:(NSString*_Nonnull)uid
        message:(NSString*_Nonnull)message;
```


Receive this callback when you receive a broadcast text message from the room called [sendRoomMessage:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-sendroommessage).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object |
|msgid |NSInteger |Message number. |
|uid |NSString\* |User ID of the message sender. |
|message |NSString\* |The content of the received text message. |


<span id="ByteRTCRoomDelegate-rtcroom-onroombinarymessagereceived-uid-message"></span>
### rtcRoom:onRoomBinaryMessageReceived:uid:message:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onRoomBinaryMessageReceived:(NSInteger)msgid uid:(NSString*_Nonnull)uid
        message:(NSData*_Nonnull)message;
```


Receive this callback when you receive a broadcast binary message sent by the room call [sendRoomBinaryMessage:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-sendroombinarymessage).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object |
|msgid |NSInteger |Message number. |
|uid |NSString\* |User ID of the message sender. |
|message |NSData\* |The binary message content received. |


<span id="ByteRTCRoomDelegate-rtcroom-onusermessagereceived-uid-message"></span>
### rtcRoom:onUserMessageReceived:uid:message:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onUserMessageReceived:(NSInteger)msgid uid:(NSString*_Nonnull)uid
               message:(NSString*_Nonnull)message;
```


Receive text messages (P2P) from other users in the room via [sendUserMessage:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-sendusermessage-message-config).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object |
|msgid |NSInteger |Message number. |
|uid |NSString\* |The user ID of the sender of the message. |
|message |NSString\* |The content of the received text message. |


<span id="ByteRTCRoomDelegate-rtcroom-onuserbinarymessagereceived-uid-message"></span>
### rtcRoom:onUserBinaryMessageReceived:uid:message:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onUserBinaryMessageReceived:(NSInteger)msgid uid:(NSString*_Nonnull)uid
               message:(NSData*_Nonnull)message;
```


Receive a binary message from another user in the room via [sendUserBinaryMessage:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-senduserbinarymessage-message-config) Receive this callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object |
|msgid |NSInteger |Message number. |
|uid |NSString\* |The user ID of the sender of the message. |
|message |NSData\* |The binary message content received. |


<span id="ByteRTCRoomDelegate-rtcroom-onusermessagesendresult-error"></span>
### rtcRoom:onUserMessageSendResult:error:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onUserMessageSendResult:(NSInteger)msgid error:(ByteRTCUserMessageSendResult)error;
```


After sending a text or binary message (P2P) to a single user in the room, the message sender will receive a callback with the result of the message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |
|msgid |NSInteger |The ID of this message. |
|error |ByteRTCUserMessageSendResult |Message result. See [ByteRTCUserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCUserMessageSendResult) |


**Notes**


* You should call [sendUserMessage:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-sendusermessage-message-config) to send a text message to a single user in the room

* You should call [sendUserBinaryMessage:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-senduserbinarymessage-message-config) to send a binary message to a single user in the room

    &nbsp;


<span id="rtcroom-onroommessagesendresult-error"></span>
### rtcRoom:onRoomMessageSendResult:error:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onRoomMessageSendResult:(NSInteger)msgid error:(ByteRTCRoomMessageSendResult)error;
```


Receives this callback after sending a text message or a binary message to a room with [sendRoomMessage:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-sendroommessage) or [sendRoomBinaryMessage:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-sendroombinarymessage).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |
|msgid |NSInteger |The ID of this message. |
|error |ByteRTCRoomMessageSendResult |Message sending results. See [ByteRTCRoomMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCRoomMessageSendResult) |


**Notes**


* You should call [sendRoomMessage:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-sendroommessage) Send a mass text message to the room

* You should call [sendRoomBinaryMessage:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-sendroombinarymessage) Send a mass binary message to the room

    &nbsp;


<span id="rtcroom-onsetroomextrainforesult-result"></span>
### rtcRoom:onSetRoomExtraInfoResult:result:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onSetRoomExtraInfoResult:(NSInteger)taskId result:(ByteRTCSetRoomExtraInfoResult)result;
```


> Available since 3.52.


Receives this callback after invoke [setRoomExtraInfo:value:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-setroomextrainfo-value).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |
|taskId |NSInteger |The ID of this setRoomExtraInfo invoke. |
|result |ByteRTCSetRoomExtraInfoResult |setRoomExtraInfo result. See [ByteRTCSetRoomExtraInfoResult](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCSetRoomExtraInfoResult) |


<span id="ByteRTCRoomDelegate-rtcroom-onroomextrainfoupdate-value-lastupdateuserid-lastupdatetimems"></span>
### rtcRoom:onRoomExtraInfoUpdate:value:lastUpdateUserId:lastUpdateTimeMs:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onRoomExtraInfoUpdate:(NSString*_Nonnull)key value:(NSString*_Nonnull)value lastUpdateUserId:(NSString*_Nonnull)lastUpdateUserId lastUpdateTimeMs:(NSInteger)lastUpdateTimeMs;
```


> Available since 3.52.


Receive a callback when other user invoke [setRoomExtraInfo:value:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-setroomextrainfo-value) .

or when user joinRoom success and this room has room extra info.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |
|key |NSString\* |Key of room attribute |
|value |NSString\* |Key of room attribute |
|lastUpdateUserId |NSString\* |The userId that last updated this attribute |
|lastUpdateTimeMs |NSInteger |The last time this attribute was updated, in milliseconds，unixtime style |


<span id="ByteRTCRoomDelegate-rtcroom-onroomstreamextrainfoupdate-info-extrainfo"></span>
### rtcRoom:onRoomStreamExtraInfoUpdate:info:extraInfo:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onRoomStreamExtraInfoUpdate:(NSString*_Nonnull)streamId info:(ByteRTCStreamInfo*_Nonnull)streamInfo extraInfo:(NSString*_Nonnull)extraInfo;
```


> Available since 3.54


Receive the extra information set by the other users in the same room with [setStreamExtraInfo:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-setstreamextrainfo).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |
|streamId |NSString\* |Stream ID of the extra information. |
|streamInfo |ByteRTCStreamInfo\* |Stream information of the extra information. |
|extraInfo |NSString\* |Extra information. |


<span id="ByteRTCRoomDelegate-rtcroom-onuservisibilitychanged-errorcode"></span>
### rtcRoom:onUserVisibilityChanged:errorCode:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onUserVisibilityChanged:(BOOL)currentUserVisibility errorCode:(ByteRTCUserVisibilityChangeError)errorCode;
```


> Available since 3.54


Callback for user to set user visibility by calling [setUserVisibility:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-setuservisibility).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |
|currentUserVisibility |BOOL |Visibility of the current user.<br><br><br>&nbsp;<br><br>* YES: Visible. The user can publish media streams. The other users in the room get informed of the behaviors of the user, such as joining room, starting video capture, and leaving room.<br><br>* NO: Invisible. The user cannot publish media streams. The other users in the room do not get informed of the behaviors of the user, such as joining room, starting video capture, or leaving room. |
|errorCode |ByteRTCUserVisibilityChangeError |Error code for setting user visibility. See [ByteRTCUserVisibilityChangeError](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCUserVisibilityChangeError). |


<span id="ByteRTCRoomDelegate-rtcroom-onvideostreambanned-isbanned"></span>
### rtcRoom:onVideoStreamBanned:isBanned:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onVideoStreamBanned:(NSString*_Nonnull)uid isBanned:(BOOL)banned;
```


All the users in the room will get informed via this callback when a user is banned or the ban of the user has been lifted by calling BanUserStream/UnbanUserStream on the server side.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |
|uid |NSString\* |Disabled/unbanned video stream user ID |
|banned |BOOL |Video stream sending status<br><br><br>&nbsp;<br><br>* true: Video stream sending is disabled<br><br>* false: Video stream sending is unbanned |


**Notes**


* When the specified user in the room is banned/unbanned video stream sending, all users in the room will receive the callback.

* If the banned user leaves or disconnects and then rejoins the room, the user is still banned from publishing audio stream, and all users in the room will be informed via the callback.

* After the specified user is banned, other users in the room will check out and enter the room again, and will receive the callback again.

* After the same room is disbanded and created again, the status in the room is cleared.

    &nbsp;


<span id="rtcroom-onaudiostreambanned-isbanned"></span>
### rtcRoom:onAudioStreamBanned:isBanned:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onAudioStreamBanned:(NSString*_Nonnull)uid isBanned:(BOOL)banned;
```


All the users in the room will get informed via this callback when a user is banned or the ban of the user has been lifted by calling BanUserStream/UnbanUserStream on the server side.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |
|uid |NSString\* |Disabled/unbanned audio stream user ID |
|banned |BOOL |Audio stream sending status<br><br><br>&nbsp;<br><br>* true: Audio stream sending is disabled<br><br>* false: Audio stream sending is unbanned |


**Notes**


* When the specified user in the room is disabled/unbanned audio stream sending, all users in the room will receive the callback.

* If the banned user leaves or disconnects and then rejoins the room, the user is still banned from publishing audio stream, and all users in the room will be informed via the callback.

* After the specified user is banned, other users in the room will check out and enter the room again, and will receive the callback again.

* After the same room is disbanded and created again, the status in the room is cleared.

* If the Audio selection is enabled in the console, only the user whose stream is banned will receive this callback.

    &nbsp;


<span id="rtcroom-onforwardstreamstatechanged"></span>
### rtcRoom:onForwardStreamStateChanged:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onForwardStreamStateChanged:(NSArray<ByteRTCForwardStreamStateInfo*>* _Nonnull)infos;
```


Callback returning the state and errors during relaying the media stream to each of the rooms

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object |
|infos |NSArray<ByteRTCForwardStreamStateInfo\*\>\* |Array of the state and errors of each designated room. Refer to [ByteRTCForwardStreamStateInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCForwardStreamStateInfo) for more information. |


<span id="ByteRTCRoomDelegate-rtcroom-onforwardstreamevent"></span>
### rtcRoom:onForwardStreamEvent:

```objectivec
- (void)rtcRoom:( ByteRTCRoom* _Nonnull)rtcRoom onForwardStreamEvent:(NSArray<ByteRTCForwardStreamEventInfo*>* _Nonnull)infos;
```


Callback returning the events during relaying the media stream to each room

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |RTCRoom object |
|infos |NSArray<ByteRTCForwardStreamEventInfo\*\>\* |Array of the event of each designated room. Refer to [ByteRTCForwardStreamEventInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCForwardStreamEventInfo) for more information. |


<span id="ByteRTCRoomDelegate-rtcroom-onnetworkquality-remotequalities"></span>
### rtcRoom:onNetworkQuality:remoteQualities:

```objectivec
- (void)rtcRoom:(ByteRTCRoom* _Nonnull)rtcRoom onNetworkQuality:(ByteRTCNetworkQualityStats*_Nonnull)localQuality remoteQualities:(NSArray<ByteRTCNetworkQualityStats*>*_Nonnull)remoteQualities;
```


Report the network quality of the users every 2s after the local user joins the room and starts publishing or subscribing to a stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object |
|localQuality |ByteRTCNetworkQualityStats\* |Local network quality. Refer to [ByteRTCNetworkQualityStats](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCNetworkQualityStats). |
|remoteQualities |NSArray<ByteRTCNetworkQualityStats\*\>\* |Network quality of the subscribed users. Refer to [ByteRTCNetworkQualityStats](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCNetworkQualityStats) for details. |


<span id="ByteRTCRoomDelegate-rtcroom-onstreamstatechanged-withuid-state-extrainfo"></span>
### rtcRoom:onStreamStateChanged:withUid:state:extraInfo:

```objectivec
- (void)rtcRoom:(ByteRTCRoom*_Nonnull)rtcRoom onStreamStateChanged:(NSString*_Nonnull)roomId
            withUid:(nonnull NSString*)uid
              state:(NSInteger)state
          extraInfo:(NSString*_Nonnull)extraInfo;
```


> Deprecated since 3.60, refer to [Upgrade Guide](https://docs.byteplus.com/en/docs/12/docs-changelogs) for more.


Callback on stream state changes. The user will receive this callback when they receive stream relating warnings and errors.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |
|roomId |NSString\* |Room ID. |
|uid |NSString\* |User ID. |
|state |NSInteger |Room state code. See [ByteRTCErrorCode](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCErrorCode) and [ByteRTCWarningCode](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCWarningCode) for specific indications. |
|extraInfo |NSString\* |Extra information. Currently unavailable. |


<span id="ByteRTCRoomDelegate-rtcroom-onstreamadd"></span>
### rtcRoom:onStreamAdd:

```objectivec
- (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onStreamAdd:(id<ByteRTCStream> _Nonnull)stream __deprecated_msg("Will be removed in new version");
```


> Deprecated since 3.45 and will be deleted in 3.51, use [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish)instead.


The following conditions trigger this callback:


* When users in the room post a new audio & video stream, other users in the room will receive this callback notification.

* When the user's original audio and video stream in the room is removed and the audio & video stream is republished, other users in the room will receive this callback notification.

* When the user first joins the room, he receives this callback, including all published streams in the room.


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtcRoom |ByteRTCRoom\* |ByteRTCRoom object. |
|stream |id<ByteRTCStream\> |Stream property. See [ByteRTCStream](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStream). |


<span id="ByteRTCExternalVideoEncoderEventHandler"></span>
# ByteRTCExternalVideoEncoderEventHandler

```objectivec
BYTERTC_APPLE_EXPORT @protocol ByteRTCExternalVideoEncoderEventHandler<NSObject>
```


Custom coded frame callback class

**Notes**

Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onStart:info:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCExternalVideoEncoderEventHandler-onstart-info) |
|void |[onStop:info:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCExternalVideoEncoderEventHandler-onstop-info) |
|void |[onRateUpdate:info:withVideoIndex:withFps:withBitRate:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCExternalVideoEncoderEventHandler-onrateupdate-info-withvideoindex-withfps-withbitrate) |
|void |[onRequestKeyFrame:info:withVideoIndex:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCExternalVideoEncoderEventHandler-onrequestkeyframe-info-withvideoindex) |
|void |[onActiveVideoLayer:info:withVideoIndex:withActive:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCExternalVideoEncoderEventHandler-onactivevideolayer-info-withvideoindex-withactive) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCExternalVideoEncoderEventHandler-onstart-info"></span>
### onStart:info:

```objectivec
- (void)onStart:(NSString*)streamId info:(ByteRTCStreamInfo* _Nonnull)info;
```


Prompt custom encoded frames to start pushing callbacks.

After receiving this callback, you can call [pushExternalEncodedVideoFrame:withEncodedVideoFrame:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-pushexternalencodedvideoframe-withencodedvideoframe) Push custom encoded video frames to the SDK

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |Custom encoded stream ID |
|info |ByteRTCStreamInfo\* |Custom encoded stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo) |


<span id="ByteRTCExternalVideoEncoderEventHandler-onstop-info"></span>
### onStop:info:

```objectivec
- (void)onStop:(NSString*)streamId info:(ByteRTCStreamInfo* _Nonnull)info;
```


When receiving the callback, you need to stop pushing custom encoded video frames to the SDK

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |Custom encoded stream ID |
|info |ByteRTCStreamInfo\* |Custom encoded stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo) |


<span id="ByteRTCExternalVideoEncoderEventHandler-onrateupdate-info-withvideoindex-withfps-withbitrate"></span>
### onRateUpdate:info:withVideoIndex:withFps:withBitRate:

```objectivec
- (void)onRateUpdate:(NSString*)streamId info:(ByteRTCStreamInfo* _Nonnull)info
      withVideoIndex:(NSInteger)videoIndex
             withFps:(NSInteger)fps
         withBitRate:(NSInteger)bitRateKps;
```


When the frame rate or bit rate of a custom encoded stream changes, the callback is triggered

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |Remote encoded stream ID |
|info |ByteRTCStreamInfo\* |Remote encoded stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo) |
|videoIndex |NSInteger |Corresponding to the subscript of the encoded stream |
|fps |NSInteger |Changed frame rate, unit: fps |
|bitRateKps |NSInteger |Changed bit rate, unit: kbps |


<span id="ByteRTCExternalVideoEncoderEventHandler-onrequestkeyframe-info-withvideoindex"></span>
### onRequestKeyFrame:info:withVideoIndex:

```objectivec
- (void)onRequestKeyFrame:(NSString*)streamId info:(ByteRTCStreamInfo* _Nonnull)info
           withVideoIndex:(NSInteger)videoIndex;
```


This callback is used to inform the stream publisher that a keyframe needs to be regenerated.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |Remote encoded stream ID |
|info |ByteRTCStreamInfo\* |Remote encoded stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo) |
|videoIndex |NSInteger |The subscript of the corresponding encoded stream |


<span id="ByteRTCExternalVideoEncoderEventHandler-onactivevideolayer-info-withvideoindex-withactive"></span>
### onActiveVideoLayer:info:withVideoIndex:withActive:

```objectivec
- (void)onActiveVideoLayer:(NSString*)streamId info:(ByteRTCStreamInfo* _Nonnull)info
            withVideoIndex:(NSInteger)videoIndex
                withActive:(BOOL)active;
```


> Available since 3.56


As the sender of a external encoded video stream, you will receive this callback at certain moments.

Based on the hints of this callback, you can selectively encode the video stream that is ready for transmission, in order to reduce the performance impact of video encoding on the local device. This callback is triggered based on a combination of factors, including the performance of the local device, the local network, and whether the stream is subscribed by the remote user.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |Custom encoded stream ID |
|info |ByteRTCStreamInfo\* |Custom encoded stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo) |
|videoIndex |NSInteger |Subscript of the corresponding encoded stream. |
|active |BOOL |The active state of the corresponding encoded stream. |


**Notes**

To receive the callback, call [setVideoSourceType:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setvideosourcetype) to set the input video source to custom encoded video and call [setExternalVideoEncoderEventHandler:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setexternalvideoencodereventhandler) to set the callback handler.

<span id="ByteRTCVideoProcessorDelegate"></span>
# ByteRTCVideoProcessorDelegate

```objectivec
BYTERTC_APPLE_EXPORT @protocol ByteRTCVideoProcessorDelegate <NSObject>
```


video processing callback interface

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|ByteRTCVideoFrame |[processVideoFrame:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCVideoProcessorDelegate-processvideoframe) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCVideoProcessorDelegate-processvideoframe"></span>
### processVideoFrame:

```objectivec
- (id<ByteRTCVideoFrame> _Nullable)processVideoFrame:(id<ByteRTCVideoFrame> _Nonnull)srcFrame;
```


Get RTC SDK acquired video frames, according to [registerLocalVideoProcessor:withConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-registerlocalvideoprocessor-withconfig) set the video preprocessor, video preprocessing, and finally the processed video frames to the RTC SDK for encoding transmission.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|srcFrame |id<ByteRTCVideoFrame\> |RTC SDK captured video frames, reference: [ByteRTCVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoFrame) |


**Return Value**

After video preprocessing video frames, returned to the RTC SDK for encoding and transmission, reference: [ByteRTCVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCVideoFrame)

**Notes**


* If you need to cancel the video preprocessing, you can set the video preprocessor to nullptr.

* When implementing `processVideoFrame`, you can directly modify the buffer of src_frame, call `addRef` to add the `src_frame` reference count by one, and return the modified `src_frame`, or you can also create a new video frame and return it.

* For the video frame returned by `processVideoFrame`, after consuming by the SDK layer, the SDK always calls the `releaseRef` method of this video frame.

    &nbsp;


<span id="bytertcmediaplayereventhandler"></span>
# ByteRTCMediaPlayerEventHandler

```objectivec
@protocol ByteRTCMediaPlayerEventHandler <NSObject>
```


Event handler for [ByteRTCMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCMediaPlayer). You must call [setEventHandler:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCMediaPlayer-seteventhandler) to set the corresponding event handler to get the events.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onMediaPlayerStateChanged:state:error:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCMediaPlayerEventHandler-onmediaplayerstatechanged-state-error) |
|void |[onMediaPlayerPlayingProgress:progress:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCMediaPlayerEventHandler-onmediaplayerplayingprogress-progress) |
|void |[onMediaPlayerEvent:event:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCMediaPlayerEventHandler-onmediaplayerevent-event-message) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCMediaPlayerEventHandler-onmediaplayerstatechanged-state-error"></span>
### onMediaPlayerStateChanged:state:error:

```objectivec
-(void)onMediaPlayerStateChanged:(int)playerId state:(ByteRTCPlayerState)state error:(ByteRTCPlayerError)error;
```


Callback for audio mixing status change.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|playerId |int |The ID of [ByteRTCMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCMediaPlayer). Set by [getMediaPlayer:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-getmediaplayer). |
|state |ByteRTCPlayerState |See [ByteRTCPlayerState](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCPlayerState). |
|error |ByteRTCPlayerError |See [ByteRTCPlayerError](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCPlayerError). |


<span id="ByteRTCMediaPlayerEventHandler-onmediaplayerplayingprogress-progress"></span>
### onMediaPlayerPlayingProgress:progress:

```objectivec
-(void)onMediaPlayerPlayingProgress:(int)playerId progress:(int64_t)progress;
```


Periodic callback for audio mixing progress. The period is set by [setProgressInterval:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCMediaPlayer-setprogressinterval).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|playerId |int |The ID of [ByteRTCMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCMediaPlayer). Set by [getMediaPlayer:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-getmediaplayer). |
|progress |int64_t |Mixing progress in ms. |


<span id="ByteRTCMediaPlayerEventHandler-onmediaplayerevent-event-message"></span>
### onMediaPlayerEvent:event:message:

```objectivec
-(void)onMediaPlayerEvent:(int)playerId event:(ByteRTCPlayerEvent)event message:(NSString*_Nullable)message;
```


> Available since 3.59


Callback for audio mixing player events. This callback is triggered after you call [selectAudioTrack:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCMediaPlayer-selectaudiotrack) and [setPosition:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCMediaPlayer-setposition).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|playerId |int |The ID of [ByteRTCMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCMediaPlayer). Set by [getMediaPlayer:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-getmediaplayer). |
|event |ByteRTCPlayerEvent |See [ByteRTCPlayerEvent](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCPlayerEvent). |
|message |NSString\* |Event description message, which may be empty. |


<span id="ByteRTCRTSRoomDelegate"></span>
# ByteRTCRTSRoomDelegate

```objectivec
@protocol ByteRTCRTSRoomDelegate <NSObject>
```


RTS room event callback interface

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[rtsRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRTSRoomDelegate-rtsroom-onroomstatechanged-withuid-state-extrainfo) |
|void |[rtsRoom:onLeaveRoom:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRTSRoomDelegate-rtsroom-onleaveroom) |
|void |[rtsRoom:onUserJoined:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRTSRoomDelegate-rtsroom-onuserjoined) |
|void |[rtsRoom:onUserLeave:reason:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRTSRoomDelegate-rtsroom-onuserleave-reason) |
|void |[rtsRoom:onRoomMessageReceived:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRTSRoomDelegate-rtsroom-onroommessagereceived-message) |
|void |[rtsRoom:onRoomBinaryMessageReceived:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRTSRoomDelegate-rtsroom-onroombinarymessagereceived-message) |
|void |[rtsRoom:onRoomMessageSendResult:error:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRTSRoomDelegate-rtsroom-onroommessagesendresult-error) |
|void |[rtsRoom:onUserMessageReceived:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRTSRoomDelegate-rtsroom-onusermessagereceived-message) |
|void |[rtsRoom:onUserBinaryMessageReceived:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRTSRoomDelegate-rtsroom-onuserbinarymessagereceived-message) |
|void |[rtsRoom:onRoomMessageReceived:uid:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRTSRoomDelegate-rtsroom-onroommessagereceived-uid-message) |
|void |[rtsRoom:onRoomBinaryMessageReceived:uid:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRTSRoomDelegate-rtsroom-onroombinarymessagereceived-uid-message) |
|void |[rtsRoom:onUserMessageReceived:uid:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRTSRoomDelegate-rtsroom-onusermessagereceived-uid-message) |
|void |[rtsRoom:onUserBinaryMessageReceived:uid:message:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRTSRoomDelegate-rtsroom-onuserbinarymessagereceived-uid-message) |
|void |[rtsRoom:onUserMessageSendResult:error:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRTSRoomDelegate-rtsroom-onusermessagesendresult-error) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCRTSRoomDelegate-rtsroom-onroomstatechanged-withuid-state-extrainfo"></span>
### rtsRoom:onRoomStateChanged:withUid:state:extraInfo:

```objectivec
- (void)rtsRoom:(ByteRTCRTSRoom* _Nonnull)rtsRoom onRoomStateChanged:(NSString* _Nonnull)roomId
        withUid:(nonnull NSString*)uid state:(NSInteger)state
       extraInfo:(nonnull NSString*)extraInfo;
```


Callback on RTS room state changes. Via this callback you get notified of room relating warnings, errors and events. For example, the user joins the room, the user is removed from the room, and so on.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtsRoom |ByteRTCRTSRoom\* |RTS room instance. |
|roomId |NSString\* |Room ID. |
|uid |NSString\* |User ID. |
|state |NSInteger |Room state code.<br><br><br>&nbsp;<br><br>* 0: Join room success.<br><br>* !0: Failed to join a room, abnormal exit, room\-related warnings or errors. |
|extraInfo |NSString\* |Extra information.<br><br>`join_type` indicates the type of room the user joins. `0` means the user joins the room for the first time, and `1` means the user rejoins the room.<br><br>&nbsp;<br><br>`elapsed` indicates the time interval from calling [joinRTSRoom:userInfo:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-joinrtsroom-userinfo) to successfully joining room, in ms. |


<span id="ByteRTCRTSRoomDelegate-rtsroom-onleaveroom"></span>
### rtsRoom:onLeaveRoom:

```objectivec
- (void)rtsRoom:( ByteRTCRTSRoom*_Nonnull)rtsRoom onLeaveRoom:(ByteRTCRoomStats*_Nonnull)stats;
```


Leave the RTS room successfully callback.

After the user call [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-leaveroom), the SDK will stop sending/receiving broadcast messages in the room and, after releasing all relevant resources, notify the user via this callback that leaving the room was successful.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtsRoom |ByteRTCRTSRoom\* |RTSRoom object. |
|stats |ByteRTCRoomStats\* |Reserved parameter. |


**Notes**


* After the user calls the [leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-leaveroom) method to leave the room, if [destroy](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-destroy) is called to destroy the room instance immediately, this callback event will not be received.

* If the app needs to use the system audio & video device after leaving the room, it is recommended to initialize the audio & video device after receiving this callback, otherwise the initialization may fail due to the SDK occupying the audio & video device.


<span id="ByteRTCRTSRoomDelegate-rtsroom-onuserjoined"></span>
### rtsRoom:onUserJoined:

```objectivec
- (void)rtsRoom:(ByteRTCRTSRoom* _Nonnull)rtsRoom onUserJoined:(ByteRTCUserInfo*_Nonnull)userInfo;
```


When the remote user enters the room for the first time, or reconnects to the room after being disconnected, the other users in the room will receive this callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtsRoom |ByteRTCRTSRoom\* |ByteRTCRTSRoom object. |
|userInfo |ByteRTCUserInfo\* |For user information. See [ByteRTCUserInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCUserInfo). |


<span id="ByteRTCRTSRoomDelegate-rtsroom-onuserleave-reason"></span>
### rtsRoom:onUserLeave:reason:

```objectivec
- (void)rtsRoom:(ByteRTCRTSRoom* _Nonnull)rtsRoom onUserLeave:(NSString* _Nonnull)uid
         reason:(ByteRTCUserOfflineReason)reason;
```


This callback is triggered when a remote user is disconnected or turns invisible.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtsRoom |ByteRTCRTSRoom\* |ByteRTCRTSRoom object. |
|uid |NSString\* |ID of the user who leaves the room, or switches to invisible. |
|reason |ByteRTCUserOfflineReason |Reason to leave the room. See [ByteRTCUserOfflineReason](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCUserOfflineReason). |


<span id="ByteRTCRTSRoomDelegate-rtsroom-onroommessagereceived-message"></span>
### rtsRoom:onRoomMessageReceived:message:

```objectivec
- (void)rtsRoom:(ByteRTCRTSRoom* _Nonnull)rtsRoom onRoomMessageReceived:(NSString* _Nonnull)uid
        message:(NSString* _Nonnull)message;
```


Receive this callback when you receive a broadcast text message from the room called [sendRoomMessage:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-sendroommessage).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtsRoom |ByteRTCRTSRoom\* |ByteRTCRTSRoom object |
|uid |NSString\* |Message sender ID. |
|message |NSString\* |The content of the received text message. |


<span id="ByteRTCRTSRoomDelegate-rtsroom-onroombinarymessagereceived-message"></span>
### rtsRoom:onRoomBinaryMessageReceived:message:

```objectivec
- (void)rtsRoom:(ByteRTCRTSRoom* _Nonnull)rtsRoom onRoomBinaryMessageReceived:(NSString* _Nonnull)uid
        message:(NSData* _Nonnull)message;
```


Receive this callback when you receive a broadcast binary message sent by the room call [sendRoomBinaryMessage:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-sendroombinarymessage).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtsRoom |ByteRTCRTSRoom\* |ByteRTCRTSRoom object |
|uid |NSString\* |Message sender ID. |
|message |NSData\* |The binary message content received. |


<span id="ByteRTCRTSRoomDelegate-rtsroom-onroommessagesendresult-error"></span>
### rtsRoom:onRoomMessageSendResult:error:

```objectivec
- (void)rtsRoom:(ByteRTCRTSRoom* _Nonnull)rtsRoom onRoomMessageSendResult:(NSInteger)msgid
          error:(ByteRTCRoomMessageSendResult)error;
```


After sending a text or binary message to all users in the room, the message sender will receive a callback with the result of the message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtsRoom |ByteRTCRTSRoom\* |ByteRTCRTSRoom object. |
|msgid |NSInteger |The ID of this message. |
|error |ByteRTCRoomMessageSendResult |Message sending results. See [ByteRTCRoomMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCRoomMessageSendResult) |


**Notes**


* You should call [sendRoomMessage:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-sendroommessage) Send a mass text message to the room

* You should call [sendRoomBinaryMessage:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-sendroombinarymessage) Send a mass binary message to the room

    &nbsp;


<span id="rtsroom-onusermessagereceived-message"></span>
### rtsRoom:onUserMessageReceived:message:

```objectivec
- (void)rtsRoom:( ByteRTCRTSRoom*_Nonnull)rtsRoom onUserMessageReceived:(NSString*_Nonnull)uid
               message:(NSString*_Nonnull)message;
```


Receive text messages (P2P) from other users in the room via [sendUserMessage:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-sendusermessage-message-config).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtsRoom |ByteRTCRTSRoom\* |ByteRTCRoom object |
|uid |NSString\* |The user ID of the sender of the message. |
|message |NSString\* |The content of the received text message. |


<span id="ByteRTCRTSRoomDelegate-rtsroom-onuserbinarymessagereceived-message"></span>
### rtsRoom:onUserBinaryMessageReceived:message:

```objectivec
- (void)rtsRoom:( ByteRTCRTSRoom*_Nonnull)rtsRoom onUserBinaryMessageReceived:(NSString*_Nonnull)uid
               message:(NSData*_Nonnull)message;
```


Receive a binary message from another user in the room via [sendUserBinaryMessage:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-senduserbinarymessage-message-config) Receive this callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtsRoom |ByteRTCRTSRoom\* |ByteRTCRoom object |
|uid |NSString\* |The user ID of the sender of the message. |
|message |NSData\* |The binary message content received. |


<span id="ByteRTCRTSRoomDelegate-rtsroom-onroommessagereceived-uid-message"></span>
### rtsRoom:onRoomMessageReceived:uid:message:

```objectivec
- (void)rtsRoom:( ByteRTCRTSRoom*_Nonnull)rtsRoom onRoomMessageReceived:(NSInteger)msgid uid:(NSString*_Nonnull)uid
        message:(NSString*_Nonnull)message;
```


Receive this callback when you receive a broadcast text message from the room called [sendRoomMessage:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-sendroommessage).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtsRoom |ByteRTCRTSRoom\* |ByteRTCRoom object |
|msgid |NSInteger |Message number. |
|uid |NSString\* |User ID of the message sender. |
|message |NSString\* |The content of the received text message. |


<span id="ByteRTCRTSRoomDelegate-rtsroom-onroombinarymessagereceived-uid-message"></span>
### rtsRoom:onRoomBinaryMessageReceived:uid:message:

```objectivec
- (void)rtsRoom:( ByteRTCRTSRoom*_Nonnull)rtsRoom onRoomBinaryMessageReceived:(NSInteger)msgid uid:(NSString*_Nonnull)uid
        message:(NSData*_Nonnull)message;
```


Receive this callback when you receive a broadcast binary message sent by the room call [sendRoomBinaryMessage:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-sendroombinarymessage).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtsRoom |ByteRTCRTSRoom\* |ByteRTCRoom object |
|msgid |NSInteger |Message number. |
|uid |NSString\* |User ID of the message sender. |
|message |NSData\* |The binary message content received. |


<span id="ByteRTCRTSRoomDelegate-rtsroom-onusermessagereceived-uid-message"></span>
### rtsRoom:onUserMessageReceived:uid:message:

```objectivec
- (void)rtsRoom:( ByteRTCRTSRoom*_Nonnull)rtsRoom onUserMessageReceived:(NSInteger)msgid uid:(NSString*_Nonnull)uid
               message:(NSString*_Nonnull)message;
```


Receive text messages (P2P) from other users in the room via [sendUserMessage:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-sendusermessage-message-config).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtsRoom |ByteRTCRTSRoom\* |ByteRTCRoom object |
|msgid |NSInteger |Message number. |
|uid |NSString\* |The user ID of the sender of the message. |
|message |NSString\* |The content of the received text message. |


<span id="ByteRTCRTSRoomDelegate-rtsroom-onuserbinarymessagereceived-uid-message"></span>
### rtsRoom:onUserBinaryMessageReceived:uid:message:

```objectivec
- (void)rtsRoom:( ByteRTCRTSRoom*_Nonnull)rtsRoom onUserBinaryMessageReceived:(NSInteger)msgid uid:(NSString*_Nonnull)uid
               message:(NSData*_Nonnull)message;
```


Receive a binary message from another user in the room via [sendUserBinaryMessage:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-senduserbinarymessage-message-config) Receive this callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtsRoom |ByteRTCRTSRoom\* |ByteRTCRoom object |
|msgid |NSInteger |Message number. |
|uid |NSString\* |The user ID of the sender of the message. |
|message |NSData\* |The binary message content received. |


<span id="ByteRTCRTSRoomDelegate-rtsroom-onusermessagesendresult-error"></span>
### rtsRoom:onUserMessageSendResult:error:

```objectivec
- (void)rtsRoom:( ByteRTCRTSRoom*_Nonnull)rtsRoom onUserMessageSendResult:(NSInteger)msgid error:(ByteRTCUserMessageSendResult)error;
```


After sending a text or binary message (P2P) to a single user in the room, the message sender will receive a callback with the result of the message.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rtsRoom |ByteRTCRTSRoom\* |ByteRTCRoom object. |
|msgid |NSInteger |The ID of this message. |
|error |ByteRTCUserMessageSendResult |Message result. See [ByteRTCUserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70085#ByteRTCUserMessageSendResult) |


**Notes**


* You should call [sendUserMessage:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-sendusermessage-message-config) to send a text message to a single user in the room

* You should call [sendUserBinaryMessage:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-senduserbinarymessage-message-config) to send a binary message to a single user in the room

    &nbsp;


<span id="bytertclocalencodedvideoframeobserver"></span>
# ByteRTCLocalEncodedVideoFrameObserver

```objectivec
BYTERTC_APPLE_EXPORT @protocol ByteRTCLocalEncodedVideoFrameObserver<NSObject>
 @optional
```


Local video frame observer

Note: Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onLocalEncodedVideoFrame:Frame:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCLocalEncodedVideoFrameObserver-onlocalencodedvideoframe-frame) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCLocalEncodedVideoFrameObserver-onlocalencodedvideoframe-frame"></span>
### onLocalEncodedVideoFrame:Frame:

```objectivec
- (void)onLocalEncodedVideoFrame:(ByteRTCVideoSource* _Nullable)videoSource
                           Frame:(ByteRTCEncodedVideoFrame* _Null_unspecified)frame;
```


After calling [registerLocalEncodedVideoFrameObserver:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-registerlocalencodedvideoframeobserver), SDK will trigger this callback when it receives local video frames.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|videoSource |ByteRTCVideoSource\* |Reserved parameter |
|frame |ByteRTCEncodedVideoFrame\*_Null_unspecified |Information about the local video frame. See [ByteRTCEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCEncodedVideoFrame). |


<span id="ByteRTCRemoteEncodedVideoFrameObserver"></span>
# ByteRTCRemoteEncodedVideoFrameObserver

```objectivec
BYTERTC_APPLE_EXPORT @protocol ByteRTCRemoteEncodedVideoFrameObserver<NSObject>
```


Custom coded frame callback class.

**Notes**

Callback functions are thrown synchronously in a non\-UI thread within the SDK. Therefore, you must not perform any time\-consuming operations or direct UI operations within the callback function, as this may cause the app to crash.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|void |[onRemoteEncodedVideoFrame:info:withEncodedVideoFrame:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCRemoteEncodedVideoFrameObserver-onremoteencodedvideoframe-info-withencodedvideoframe) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCRemoteEncodedVideoFrameObserver-onremoteencodedvideoframe-info-withencodedvideoframe"></span>
### onRemoteEncodedVideoFrame:info:withEncodedVideoFrame:

```objectivec
- (void)onRemoteEncodedVideoFrame:(NSString*)streamId info:(ByteRTCStreamInfo* _Nonnull)info
                   withEncodedVideoFrame:(ByteRTCEncodedVideoFrame* _Nonnull)videoFrame;
```


Call [registerRemoteEncodedVideoFrameObserver:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-registerremoteencodedvideoframeobserver) After the SDK detects the remote encoded video data, the callback is triggered

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamId |NSString\* |Remote stream ID. |
|info |ByteRTCStreamInfo\* |Remote stream information. See [ByteRTCStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCStreamInfo) |
|videoFrame |ByteRTCEncodedVideoFrame\* |Received remote video frame information. See [ByteRTCEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCEncodedVideoFrame) |


<span id="ByteRTCMediaPlayerCustomSourceProvider"></span>
# ByteRTCMediaPlayerCustomSourceProvider

```objectivec
BYTERTC_APPLE_EXPORT @protocol ByteRTCMediaPlayerCustomSourceProvider <NSObject>
```


In\-memory audio data playing callback interface

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|int |[onReadData:bufferSize:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCMediaPlayerCustomSourceProvider-onreaddata-buffersize) |
|int64_t |[onSeek:whence:](https://docs.byteplus.com/en/docs/12/16382#ByteRTCMediaPlayerCustomSourceProvider-onseek-whence) |


<span id="instructions"></span>
## Instructions

<span id="ByteRTCMediaPlayerCustomSourceProvider-onreaddata-buffersize"></span>
### onReadData:bufferSize:

```objectivec
-(int)onReadData:(uint8_t*_Nonnull) buffer bufferSize:(int)bufferSize;
```


> Available since 3.53


Callback of getting the path and size of the audio data you input.

When you call [openWithCustomSource:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCMediaPlayer-openwithcustomsource-config) API to play the in\-memory audio data you input, this callback will be triggered and you need to enter the path and size of the audio data.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|buffer |uint8_t\* |The path of the audio data you input. The size of audio data should be equal to or less than the value of bufferSize. The supported formats are: mp3, aac, m4a, 3gp, wav. |
|bufferSize |int |The size of the audio data, in bytes. If you want to stop audio playing, you can enter a figure less than or equal to zero into bufferSize and then SDK will stop calling this callback. |


**Return Value**

Returns the size of the audio data that are actually read.

**Notes**

If calling [openWithCustomSource:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCMediaPlayer-openwithcustomsource-config) API failed, please enter 0 into buffer and bufferSize. In this situation, SDK will stop calling this callback.

<span id="ByteRTCMediaPlayerCustomSourceProvider-onseek-whence"></span>
### onSeek:whence:

```objectivec
-(int64_t)onSeek:(int64_t)offset whence:(ByteRTCMediaPlayerCustomSourceSeekWhence)whence;
```


> Available since 3.53


Seeking the audio data based on the set starting position and offset to help SDK read and analyze data.

When you call [openWithCustomSource:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCMediaPlayer-openwithcustomsource-config) API to play the in\-memory audio data you input, or when you call [setPosition:position:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCAudioEffectPlayer-setposition-position) to set the starting position of audio playing, this callback will be trigerred and you need to seek the audio data accorring to the value of offset and whence.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|offset |int64_t |The offset of the target position relative to the starting position, in bytes. The value can be positive or negative. |
|whence |ByteRTCMediaPlayerCustomSourceSeekWhence |The starting position of the seeking. Refer to [ByteRTCMediaPlayerCustomSourceSeekWhence](https://docs.byteplus.com/en/docs/12/docs-70088#ByteRTCMediaPlayerCustomSourceSeekWhence) for more details. |


**Return Value**

If the seeking succeeded, the information on the final adjusted play position after seeking or the size of the audio data will be returned.

If the seeking failed, \-1 will be returned.
