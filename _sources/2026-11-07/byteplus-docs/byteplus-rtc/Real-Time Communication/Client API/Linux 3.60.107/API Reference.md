---
title: "API Reference"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-85516"
---

<span id="IVideoEffect"></span>
# IVideoEffect

```cpp
class bytertc::IVideoEffect
```


Advanced video effects. See [integration guide](https://docs.byteplus.com/byteplus-rtc/docs/114717).

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual |[~IVideoEffect](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect-~ivideoeffect) |
|virtual int |[initCVResource](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect-initcvresource) |
|virtual int |[getAuthMessage](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect-getauthmessage) |
|virtual int |[freeAuthMessage](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect-freeauthmessage) |
|virtual int |[enableVideoEffect](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect-enablevideoeffect) |
|virtual int |[disableVideoEffect](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect-disablevideoeffect) |
|virtual int |[setEffectNodes](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect-seteffectnodes) |
|virtual int |[updateEffectNode](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect-updateeffectnode) |
|virtual int |[setColorFilter](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect-setcolorfilter) |
|virtual int |[setColorFilterIntensity](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect-setcolorfilterintensity) |
|virtual int |[enableFaceDetection](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect-enablefacedetection) |
|virtual int |[disableFaceDetection](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect-disablefacedetection) |


<span id="instructions"></span>
## Instructions

<span id="IVideoEffect-~ivideoeffect"></span>
### ~IVideoEffect

```cpp
virtual ~IVideoEffect() = default;
```


<span id="IVideoEffect-initcvresource"></span>
### initCVResource

```cpp
virtual int initCVResource(
    const char* license_file_path,
    const char* algo_model_dir
) = 0;
```


Checks video effect license, sets the video effect resource model path, and initializes video effect.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|license_file_path |const char\* |The absolute path of the license file for authorization. |
|algo_model_dir |const char\* |The absolute path of the Effects SDK's models file. |


**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.


**Notes**

When validating the license, the difference of the timestamp of the CV server and the timestamp of the client is checked. You must not change the time of the client.

<span id="IVideoEffect-getauthmessage"></span>
### getAuthMessage

```cpp
virtual int getAuthMessage(
    char** ppmsg,
    int* len
) = 0;
```


Get authorization messages from the Effect SDK to obtain online licenses.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|ppmsg |char\*\* |Authorization message string address |
|len |int\* |Authorization message string length |


**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.


**Notes**


* You must obtain an online license for the Effect SDK before using the CV functions.

* After obtaining authorization messages through this API, you must refer to [Online License Guide](https://docs.byteplus.com/en/effects/docs/windows-license-guide) to implement the business logic of obtaining online licenses by yourself. After obtaining the license, you must call [initCVResource](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect-initcvresource) to confirm that the license is valid. Then you can use the CV function.

* After obtaining the authorization message, call [freeAuthMessage](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect-freeauthmessage) to free memory.

    &nbsp;


<span id="freeauthmessage"></span>
### freeAuthMessage

```cpp
virtual int freeAuthMessage(char* pmsg) = 0;
```


After using the authorization message string, free the memory.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|pmsg |char\* |The authorization message string returned by getAuthMessage. |


**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

    &nbsp;


<span id="enablevideoeffect"></span>
### enableVideoEffect

```cpp
virtual int enableVideoEffect() = 0;
```


Enables video effects including beauty and color filters.

**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.


**Notes**


* You must call [initCVResource](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect-initcvresource) before calling this API.

* This API does not turn on video effects directly, you must call [setEffectNodes](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect-seteffectnodes) or [setColorFilter](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect-setcolorfilter) next.

* Call [disableVideoEffect](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect-disablevideoeffect) to turn off video effects.

    &nbsp;


<span id="disablevideoeffect"></span>
### disableVideoEffect

```cpp
virtual int disableVideoEffect() = 0;
```


Disables video effects.

**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.


**Notes**

Call [enableVideoEffect](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect-enablevideoeffect) to enable video effects.

<span id="IVideoEffect-seteffectnodes"></span>
### setEffectNodes

```cpp
virtual int setEffectNodes(
    const char** effect_node_paths,
    int node_num
) = 0;
```


Sets the video effects material package.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|effect_node_paths |const char\*\* |Array of effect material package paths.<br><br>&nbsp;<br><br>To remove the current video effect, set it to null. |
|node_num |int |Number of effect material packages. |


**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.


**Notes**

You must call [enableVideoEffect](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect-enablevideoeffect) before calling this API.

<span id="IVideoEffect-updateeffectnode"></span>
### updateEffectNode

```cpp
virtual int updateEffectNode(
    const char* effect_node_path,
    const char* node_key,
    float node_value
) = 0;
```


Sets the intensity of video effects.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|effect_node_path |const char\* |The absolute path of the effects resource package, see [Resource Package Structure](https://docs.byteplus.com/effects/docs/resource-package-structure-v421-and-later). |
|node_key |const char\* |The name of the material key to be set, see [Functions of Resource Keys](https://docs.byteplus.com/effects/docs/functions-of-resource-keys-v421-and-later) for the value. |
|node_value |float |The intensity value that needs to be set, the value range [0,1], and the setting is invalid when it exceeds the range. |


**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

    &nbsp;


<span id="setcolorfilter"></span>
### setColorFilter

```cpp
virtual int setColorFilter(const char* res_path) = 0;
```


Sets the color filter.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|res_path |const char\* |Filter effects package absolute path. |


**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.


**Notes**

Call [setColorFilterIntensity](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect-setcolorfilterintensity) to set the intensity of the color filter enabled. Set the intensity to 0 to turn off color filter.

<span id="IVideoEffect-setcolorfilterintensity"></span>
### setColorFilterIntensity

```cpp
virtual int setColorFilterIntensity(float intensity) = 0;
```


Sets the intensity of the color filter enabled.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|intensity |float |Filter intensity. The value range [0,1] is set to be invalid when the range is exceeded.<br><br>&nbsp;<br><br>Set the intensity to 0 to turn off color filter. |


**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

    &nbsp;


<span id="enablefacedetection"></span>
### enableFaceDetection

```cpp
virtual int enableFaceDetection(
    IFaceDetectionObserver* observer,
    unsigned int interval_ms,
    const char* face_model_path
) = 0;
```


Starts face detection and registers the observer for the result.

With this observer, you will receive [onFaceDetectResult](https://docs.byteplus.com/en/docs/12/docs-85517#IFaceDetectionObserver-onfacedetectresult) periodically.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|observer |IFaceDetectionObserver\* |See [IFaceDetectionObserver](https://docs.byteplus.com/en/docs/12/docs-85517#IFaceDetectionObserver). |
|interval_ms |unsigned int |The minimum time interval between two callbacks in milliseconds. The value should be greater than 0. The actual time interval is between interval_ms and interval_ms+the time slot of a captured video frame. |
|face_model_path |const char\* |The absolute path of the face detection algorithm file. Typically it is the tt_face_vXXX.model file in the ttfacemodel folder. |


**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* \-1004: Initializing. This function will be available when the initialization is completed.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

    &nbsp;


<span id="disablefacedetection"></span>
### disableFaceDetection

```cpp
virtual int disableFaceDetection() = 0;
```


Stops face detection.

**Return Value**


* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

    &nbsp;


<span id="irtcengine"></span>
# IRTCEngine

```cpp
class bytertc::IRTCEngine
```


Engine API

<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|BYTERTC_STATIC_API IRTCEngine\* |[createRTCEngine](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-creatertcengine) |
|BYTERTC_STATIC_API void |[destroyRTCEngine](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-destroyrtcengine) |
|BYTERTC_STATIC_API const char\* |[getSDKVersion](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-getsdkversion) |
|BYTERTC_STATIC_API int |[setLogConfig](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setlogconfig) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual int |[muteAudioCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-muteaudiocapture) |
|virtual int |[muteScreenAudioCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-mutescreenaudiocapture) |
|virtual int |[setCaptureVolume](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setcapturevolume) |
|virtual int |[setScreenCaptureVolume](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setscreencapturevolume) |
|virtual int |[setPlaybackVolume](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setplaybackvolume) |
|virtual int |[startAudioCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startaudiocapture) |
|virtual int |[stopAudioCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-stopaudiocapture) |
|virtual int |[setAudioProfile](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setaudioprofile) |
|virtual int |[setAnsMode](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setansmode) |
|virtual int |[enableAGC](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-enableagc) |
|virtual int |[setAudioSourceType](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setaudiosourcetype) |
|virtual int |[setAudioRenderType](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setaudiorendertype) |
|virtual int |[pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-pushexternalaudioframe) |
|virtual int |[pullExternalAudioFrame](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-pullexternalaudioframe) |
|virtual int |[startVideoCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startvideocapture) |
|virtual int |[stopVideoCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-stopvideocapture) |
|virtual int |[setVideoCaptureConfig](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setvideocaptureconfig) |
|virtual int |[setVideoCaptureRotation](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setvideocapturerotation) |
|virtual int |[setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setvideoencoderconfig) |
|virtual int |[setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setlocalsimulcastmode) |
|virtual int |[setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setlocalsimulcastmode-2) |
|virtual int |[setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setlocalvideocanvas) |
|virtual int |[updateLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-updatelocalvideocanvas) |
|virtual int |[setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setremotevideocanvas) |
|virtual int |[updateRemoteStreamVideoCanvas](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-updateremotestreamvideocanvas-2) |
|virtual int |[setLocalVideoSink](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setlocalvideosink-2) |
|virtual int |[setRemoteVideoSink](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setremotevideosink-2) |
|virtual int |[updateScreenCaptureRegion](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-updatescreencaptureregion) |
|virtual int |[startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startscreenvideocapture) |
|virtual int |[stopScreenVideoCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-stopscreenvideocapture) |
|virtual int |[updateScreenCaptureHighlightConfig](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-updatescreencapturehighlightconfig) |
|virtual int |[updateScreenCaptureMouseCursor](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-updatescreencapturemousecursor) |
|virtual IScreenCaptureSourceList\* |[getScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-getscreencapturesourcelist) |
|virtual IVideoFrame\* |[getThumbnail](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-getthumbnail) |
|virtual IVideoFrame\* |[getWindowAppIcon](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-getwindowappicon) |
|virtual int |[setVideoSourceType](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setvideosourcetype) |
|virtual int |[pushExternalVideoFrame](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-pushexternalvideoframe) |
|virtual IRTCRoom\* |[createRTCRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-creatertcroom) |
|virtual IRTSRoom\* |[createRTSRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-creatertsroom) |
|virtual int |[setPublishFallbackOption](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setpublishfallbackoption) |
|virtual int |[setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setsubscribefallbackoption) |
|virtual int |[setRemoteUserPriority](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setremoteuserpriority) |
|virtual int |[setBusinessId](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setbusinessid) |
|virtual int |[setRemoteVideoMirrorType](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setremotevideomirrortype) |
|virtual IVideoEffect\* |[getVideoEffectInterface](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-getvideoeffectinterface) |
|virtual int |[setEncryptInfo](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setencryptinfo) |
|virtual int |[setCustomizeEncryptHandler](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setcustomizeencrypthandler) |
|virtual int |[enableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-enableaudioframecallback) |
|virtual int |[disableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-disableaudioframecallback) |
|virtual int |[registerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-registeraudioframeobserver) |
|virtual int |[registerAudioProcessor](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-registeraudioprocessor) |
|virtual int |[enableAudioProcessor](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-enableaudioprocessor) |
|virtual int |[disableAudioProcessor](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-disableaudioprocessor) |
|virtual int |[registerLocalVideoProcessor](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-registerlocalvideoprocessor) |
|virtual int |[setVideoDigitalZoomConfig](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setvideodigitalzoomconfig) |
|virtual int |[setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setvideodigitalzoomcontrol) |
|virtual int |[startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startvideodigitalzoomcontrol) |
|virtual int |[stopVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-stopvideodigitalzoomcontrol) |
|virtual int |[sendSEIMessage](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-sendseimessage) |
|virtual int |[sendLivePushSEIMessage](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-sendlivepushseimessage) |
|virtual IVideoDeviceManager\* |[getVideoDeviceManager](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-getvideodevicemanager) |
|virtual IAudioDeviceManager\* |[getAudioDeviceManager](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-getaudiodevicemanager) |
|virtual int |[startFileRecording](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startfilerecording) |
|virtual int |[stopFileRecording](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-stopfilerecording) |
|virtual int |[startAudioRecording](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startaudiorecording) |
|virtual int |[stopAudioRecording](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-stopaudiorecording) |
|virtual int |[enableExternalSoundCard](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-enableexternalsoundcard) |
|virtual int |[setRuntimeParameters](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setruntimeparameters) |
|virtual int |[feedback](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-feedback) |
|virtual IAudioEffectPlayer\* |[getAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-getaudioeffectplayer) |
|virtual IMediaPlayer\* |[getMediaPlayer](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-getmediaplayer) |
|virtual int |[login](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-login) |
|virtual int |[logout](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-logout) |
|virtual int |[updateLoginToken](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-updatelogintoken) |
|virtual int |[setServerParams](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setserverparams) |
|virtual int |[getPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-getpeeronlinestatus) |
|virtual int64_t |[sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-sendusermessageoutsideroom) |
|virtual int64_t |[sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-senduserbinarymessageoutsideroom) |
|virtual int64_t |[sendServerMessage](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-sendservermessage) |
|virtual int64_t |[sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-sendserverbinarymessage) |
|virtual int |[startNetworkDetection](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startnetworkdetection) |
|virtual int |[stopNetworkDetection](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-stopnetworkdetection) |
|virtual int |[stopScreenAudioCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-stopscreenaudiocapture) |
|virtual int |[enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-enableaudiopropertiesreport) |
|virtual int |[setRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setremoteaudioplaybackvolume) |
|virtual int |[enableVocalInstrumentBalance](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-enablevocalinstrumentbalance) |
|virtual int |[enablePlaybackDucking](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-enableplaybackducking) |
|virtual int |[registerLocalEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-registerlocalencodedvideoframeobserver) |
|virtual int |[registerRemoteEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-registerremoteencodedvideoframeobserver) |
|virtual int |[setExternalVideoEncoderEventHandler](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setexternalvideoencodereventhandler) |
|virtual int |[pushExternalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-pushexternalencodedvideoframe) |
|virtual int |[setVideoDecoderConfig](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setvideodecoderconfig) |
|virtual int |[requestRemoteVideoKeyFrame](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-requestremotevideokeyframe) |
|virtual int |[sendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-sendstreamsyncinfo) |
|virtual int |[setLocalVoicePitch](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setlocalvoicepitch) |
|virtual int |[setVideoWatermark](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setvideowatermark) |
|virtual int |[clearVideoWatermark](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-clearvideowatermark) |
|virtual int |[setDummyCaptureImagePath](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setdummycaptureimagepath) |
|virtual int |[startCloudProxy](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startcloudproxy) |
|virtual int |[stopCloudProxy](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-stopcloudproxy) |
|virtual int |[setLocalProxy](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setlocalproxy) |
|virtual int |[setLowLightAdjusted](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setlowlightadjusted) |
|virtual IWTNStream\* |[getWTNStream](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-getwtnstream) |
|virtual int |[deprecated] [updateRemoteStreamVideoCanvas](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-updateremotestreamvideocanvas) |
|virtual int |[deprecated] [setLocalVideoSink](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setlocalvideosink) |
|virtual int |[deprecated] [setRemoteVideoSink](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setremotevideosink) |
|virtual int |[deprecated] [startScreenAudioCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startscreenaudiocapture) |


<span id="instructions"></span>
## Instructions

<span id="IRTCEngine-creatertcengine"></span>
### createRTCEngine

```cpp
static BYTERTC_STATIC_API IRTCEngine* createRTCEngine(
    const EngineConfig& config,
    IRTCEngineEventHandler* event_handler
);
```


Creates an engine instance.

This is the very first API that you must call if you want to use all the RTC capabilities.

If there is no engine instance in current process, calling this API will create one. If an engine instance has been created, calling this API again will have the created engine instance returned.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|config |const EngineConfig& |[EngineConfig](https://docs.byteplus.com/en/docs/12/docs-85519#EngineConfig) |
|event_handler |IRTCEngineEventHandler\* |Handler sent from SDK to App. See [IRTCEngineEventHandler](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler) |


**Return Value**


* IRTCEngine: A successfully created engine instance.

* Null: app_id is null or empty. event_handler is null.

    &nbsp;


<span id="destroyrtcengine"></span>
### destroyRTCEngine

```cpp
static BYTERTC_STATIC_API void destroyRTCEngine();
```


Destroy the engine instance created by [createRTCEngine](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-creatertcengine), and release all related resources.

**Notes**


* Call this API after all business scenarios related to the engine instance are destroyed. In a multi\-thread scenario, you must not call [IRTCEngine](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine) related APIs after calling this interface, or the SDK may crash. When the API is called, RTC SDK destroys all memory associated with the engine instance and stops any interaction with the media server.

* Calling this API will start the SDK exit logic. The engine thread is held until the exit logic is complete. The engine thread is retained until the exit logic is complete. Therefore, do not call this API directly in the callback thread, or it will cause a deadlock. This function takes a long time to execute, so it's not recommended to call this API in the main thread, or the main thread may be blocked.

    &nbsp;


<span id="getsdkversion"></span>
### getSDKVersion

```cpp
static BYTERTC_STATIC_API const char* getSDKVersion();
```


Get the current SDK version information.

**Return Value**

Current SDK version information.

<span id="IRTCEngine-setlogconfig"></span>
### setLogConfig

```cpp
static BYTERTC_STATIC_API int setLogConfig(const LogConfig& log_config);
```


Configures the local log parameters of RTC SDK, including the logging level, directory, the limits for total log file size and the prefix of log.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|log_config |const LogConfig& |Local log parameters. See [LogConfig](https://docs.byteplus.com/en/docs/12/docs-85519#LogConfig). |


**Return Value**


* 0: Success.

* –1: Failure. This API must be called before creating engine.

* –2: Failure. Invalid parameters.


**Notes**

This API must be called before [createRTCEngine](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-creatertcengine).

<span id="IRTCEngine-muteaudiocapture"></span>
### muteAudioCapture

```cpp
virtual int muteAudioCapture(bool mute) = 0;
```


> Available since 3.58.1


Set whether to mute the recording signal (without changing the local hardware).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mute |bool |Whether to mute audio capture.<br><br><br>&nbsp;<br><br>* True: Mute (disable microphone)<br><br>* False: (Default) Enable microphone |


**Return Value**


* 0: Success.

* < 0 : Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* Calling this API does not affect the status of SDK audio stream publishing.

* Adjusting the volume by calling [setCaptureVolume](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setcapturevolume) after muting will not cancel the mute state. The volume state will be retained until unmuted.

* You can use this interface to set the capture volume before or after calling [startAudioCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startaudiocapture) to enable audio capture.

    &nbsp;


<span id="mutescreenaudiocapture"></span>
### muteScreenAudioCapture

```cpp
virtual int muteScreenAudioCapture(bool mute) = 0;
```


> Available since 3.60.


Mutes/unmutes the audio captured when screen sharing.

Calling this method will send muted data instead of the screen audio data, and it does not affect the local audio device capture status and the SDK audio stream publishing status.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mute |bool |Whether to mute the audio capture when screen sharing.<br><br><br>&nbsp;<br><br>* True: Mute the audio capture when screen sharing.<br><br>* False: (Default) Unmute the audio capture when screen sharing. |


**Return Value**


* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* Adjusting the volume by calling [setCaptureVolume](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setcapturevolume) after muting will not cancel the mute state. The volume state will be retained until unmuted.

* You can use this interface to set the capture volume before or after calling [startAudioCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startaudiocapture) to enable audio capture.

    &nbsp;


<span id="setcapturevolume"></span>
### setCaptureVolume

```cpp
virtual int setCaptureVolume(int volume) = 0;
```


Adjust the audio capture volume

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|volume |int |Ratio of capture volume to original volume. Ranging: [0,400]. Unit: %<br><br>&nbsp;<br><br>This changes the volume property of the audio data other than the hardware volume.<br><br><br>&nbsp;<br><br>* 0: Mute<br><br>* 100: Original volume. To ensure the audio quality, we recommend [0, 100].<br><br>* 400: Four times the original volume with signal\-clipping protection. |


**Return Value**


* 0: Success.

* < 0: Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**

Call this API to set the volume of the audio capture before or during the audio capture.

<span id="IRTCEngine-setscreencapturevolume"></span>
### setScreenCaptureVolume

```cpp
virtual int setScreenCaptureVolume(int volume) = 0;
```


> Available Available since 3.60.


Adjusts the volume of audio captured during screen sharing.

This method only changes the volume of audio data and does not affect the hardware volume of the local device.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|volume |int |Ratio(%) of capture volume to original volume, in the range [0, 400], with overflow protection.<br><br>&nbsp;<br><br>To ensure better call quality, we recommend setting the volume to [0, 100].<br><br><br>&nbsp;<br><br>* 0: Mute<br><br>* 100: Original volume<br><br>* 400: Four times the original volume with signal\-clipping protection |


**Return Value**


* 0: Success.

* < 0: Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**

You can call this API to set the capture volume either before or after enabling screen audio capture.

<span id="IRTCEngine-setplaybackvolume"></span>
### setPlaybackVolume

```cpp
virtual int setPlaybackVolume(const int volume) = 0;
```


Adjust the playback volume of the mixed remote audios. You can call this API before or during the playback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|volume |const int |Ratio(%) of playback volume to original volume, in the range [0, 400], with overflow protection.<br><br>&nbsp;<br><br>This changes the volume property of the audio data other than the hardware volume.<br><br>&nbsp;<br><br>To ensure the audio quality, we recommend setting the volume to `100`.<br><br><br>&nbsp;<br><br>* 0: mute<br><br>* 100: original volume<br><br>* 400: Four times the original volume with signal\-clipping protection. |


**Return Value**


* 0: Success.

* < 0: Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**

Suppose a remote user A is always within the range of the target user whose playback volume will be adjusted, if you use both this method and [setRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setremoteaudioplaybackvolume)/[setRemoteRoomAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-setremoteroomaudioplaybackvolume), the volume that the local user hears from user A is the overlay of both settings.

<span id="IRTCEngine-startaudiocapture"></span>
### startAudioCapture

```cpp
virtual int startAudioCapture() = 0;
```


Start internal audio capture. The default is off.

Internal audio capture refers to: capturing audio using the built\-in module.

The local client will be informed via [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onaudiodevicestatechanged) after starting audio capture by calling this API.

The remote clients in the room will be informed of the state change via [onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onuserstartaudiocapture) after the visible user starts audio capture by calling this API..

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* If the current device does not have permission to access the microphone, calling this method will trigger the `onAudioDeviceStateChanged` callback, with the corresponding error code being `MediaDeviceError.kMediaDeviceErrorDeviceNoPermission = 1`.

* Call [stopAudioCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-stopaudiocapture) to stop the internal audio capture. Otherwise, the internal audio capture will sustain until you destroy the engine instance.

* To mute and unmute microphones, we recommend using [publishStreamAudio](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-publishstreamaudio), other than [stopAudioCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-stopaudiocapture) and this API. Because starting and stopping capture devices often need some time waiting for the response of the device, that may lead to a short silence during the communication.

* Once you create the engine instance, you can start internal audio capture regardless of the audio publishing state. The audio stream will start publishing only after the audio capture starts.

* To switch from custom to internal audio capture, stop publishing before disabling the custom audio capture module and then call this API to enable the internal audio capture.

    &nbsp;


<span id="stopaudiocapture"></span>
### stopAudioCapture

```cpp
virtual int stopAudioCapture() = 0;
```


Stop internal audio capture. The default is off.

Internal audio capture refers to: capturing audio using the built\-in module.

The local client will be informed via [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onaudiodevicestatechanged) after stopping audio capture by calling this API.

.

The remote clients in the room will be informed of the state change via [onUserStopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onuserstopaudiocapture) after the visible client stops audio capture by calling this API.

.

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* Call [startAudioCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startaudiocapture)to enable the internal audio capture.

* Without calling this API the internal audio capture will sustain until you destroy the engine instance.

    &nbsp;


<span id="setaudioprofile"></span>
### setAudioProfile

```cpp
virtual int setAudioProfile(AudioProfileType audio_profile) = 0;
```


Sets the sound quality. Call this API to change the sound quality if the audio settings in the current [RoomProfileType](https://docs.byteplus.com/en/docs/12/docs-85519#RoomProfileType) can not meet your requirements.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audio_profile |AudioProfileType |Sound quality. See [AudioProfileType](https://docs.byteplus.com/en/docs/12/docs-85519#AudioProfileType) |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* You can call this API before and after entering the room.

* Support dynamic switching of sound quality during a call.

    &nbsp;


<span id="setansmode"></span>
### setAnsMode

```cpp
virtual int setAnsMode(AnsMode ans_mode) = 0;
```


> Available since 3.52


Set the Active Noise Cancellation(ANC) mode during audio and video communications.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|ans_mode |AnsMode |ANC modes. See [AnsMode](https://docs.byteplus.com/en/docs/12/docs-85519#AnsMode). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* You can call this API before or after entering a room. When you repeatedly call it, only the last call takes effect.


The AI noise cancellation can be enabled by calling this interface only in the following [RoomProfileType](https://docs.byteplus.com/en/docs/12/docs-85519#RoomProfileType) scenarios.

\- Game Voice: kRoomProfileTypeGame

\- High\-Quality Game: kRoomProfileTypeGameHD

\- Cloud Gaming: kRoomProfileTypeCloudGame

\- 1 vs 1 Audio and Video Call: kRoomProfileTypeChat

\- Multi\-End Synchronized Audio and Video Playback: kRoomProfileTypeLwTogether

\- Personal Device in Cloud Meeting: kRoomProfileTypeMeeting

\- Classroom Interaction: kRoomProfileTypeClassroom

\- Conference Room Terminals in Cloud Meetings: kRoomProfileTypeMeetingRoom

<span id="IRTCEngine-enableagc"></span>
### enableAGC

```cpp
virtual int enableAGC(bool enable) = 0;
```


> Available since 3.51


Turns on/ off AAGC（Analog Automatic Gain Control）.

After AAGC is enabled, SDK can automatically adjust microphone pickup volume to keep the output volume at a steady level.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|enable |bool |whether to turn on AAGC.<br><br><br>&nbsp;<br><br>* true: AAGC is turned on.<br><br>* false: AAGC is turned off. |


**Return Value**


* 0: Success.

* \-1: Failure.


**Notes**

You can call this method before and after joining the room. To turn on AGC before joining the room, you need to contact the technical support to get a private parameter to set [RoomProfileType](https://docs.byteplus.com/en/docs/12/docs-85519#RoomProfileType).

To enable AAGC after joining the room, you must set [RoomProfileType](https://docs.byteplus.com/en/docs/12/docs-85519#RoomProfileType) to `kRoomProfileTypeMeeting`,`kRoomProfileTypeMeetingRoom` or `kRoomProfileTypeClassroom` .

It is not recommended to call [setAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-setaudiocapturedevicevolume) to adjust microphone pickup volume with AAGC on.

<span id="IRTCEngine-setaudiosourcetype"></span>
### setAudioSourceType

```cpp
virtual int setAudioSourceType (AudioSourceType type) = 0;
```


Switch the audio capture type.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |AudioSourceType |Audio input source type. See [AudioSourceType](https://docs.byteplus.com/en/docs/12/docs-85519#AudioSourceType)<br><br>&nbsp;<br><br>Use internal audio capture by default. The audio capture type and the audio render type may be different from each other. |


**Return Value**

Method call result:


* =0: Success.

* <0: Failure.


**Notes**


* You can call this API before or after joining the room.

* If you call this API to switch from internal audio capture to custom capture, the internal audio capture is automatically disabled. You must call [pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-pushexternalaudioframe) to push custom captured audio data to RTC SDK for transmission.

* If you call this API to switch from custom capture to internal capture, you must then call [startAudioCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startaudiocapture) to enable internal capture.

    &nbsp;


<span id="setaudiorendertype"></span>
### setAudioRenderType

```cpp
virtual int setAudioRenderType (AudioRenderType type) = 0;
```


Switch the audio render type.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |AudioRenderType |Audio output source type. See [AudioRenderType](https://docs.byteplus.com/en/docs/12/docs-85519#AudioRenderType).<br><br>&nbsp;<br><br>Use internal audio render by default. The audio capture type and the audio render type may be different from each other. |


**Return Value**

Method call result:


* =0: Success.

* <0: Failure.


**Notes**


* You can call this API before or after joining the room.

* After calling this API to enable custom audio rendering, call [pullExternalAudioFrame](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-pullexternalaudioframe) for audio data.

    &nbsp;


<span id="pushexternalaudioframe"></span>
### pushExternalAudioFrame

```cpp
virtual int pushExternalAudioFrame(IAudioFrame* audio_frame) = 0;
```


Push custom captured audio data to the RTC SDK.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audio_frame |IAudioFrame\* |The audio data of 10 ms. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IAudioFrame)。<br><br><br>&nbsp;<br><br>* The audio sampling format must be S16. The data format within the audio buffer must be PCM, and its capacity should be audioFrame.samples × audioFrame.channel × 2.<br><br>* A specific sample rate and the number of channels must be specified; it is not supported to set them to automatic. |


**Return Value**


* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* Before calling this API, you must call [setAudioSourceType](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setaudiosourcetype) to enable custom audio capture.

* You must push custom captured audio data every 10 ms.

    &nbsp;


<span id="pullexternalaudioframe"></span>
### pullExternalAudioFrame

```cpp
virtual int pullExternalAudioFrame(IAudioFrame* audio_frame) = 0;
```


Pull remote audio data. You can use the data for audio processing or custom rendering.

After calling this method, the SDK will actively pull the audio data that is ready to be played, including the decoded and mixed audio data from remote end for external playback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audio_frame |IAudioFrame\* |The obtained audio data of 10 ms. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IAudioFrame)。 |


**Return Value**

API call result:


* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for specific reasons.


**Notes**


* Before pulling the audio data, call [setAudioRenderType](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setaudiorendertype) to enable custom rendering.

* You should pull audio data every 10 milliseconds since the duration of a RTC SDK audio frame is 10 milliseconds. Samples x call frequency = audio_frame's sample rate. Assume that the sampling rate is set to 48000, call this API every 10 ms, so that 480 sampling points should be pulled each time.

* This function runs in the user calling thread and is a synchronous function.

    &nbsp;


<span id="startvideocapture"></span>
### startVideoCapture

```cpp
virtual int startVideoCapture() = 0;
```


Enable internal video capture immediately. The default is off.

Internal video capture refers to: use the RTC SDK built\-in video capture module to capture.

The local client will be informed via [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onvideodevicestatechanged) after starting video capture by calling this API.

The remote clients in the room will be informed of the state change via [onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onuserstartvideocapture) after the visible client starts video capture by calling this API.

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* Call [stopVideoCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-stopvideocapture) to stop the internal video capture. Otherwise, the internal video capture will sustain until you destroy the engine instance.

* Once you create the engine instance, you can start internal video capture regardless of the video publishing state. The video stream will start publishing only after the video capture starts.

* To switch from custom to internal video capture, stop publishing before disabling the custom video capture module and then call this API to enable the internal video capture.

    &nbsp;


<span id="stopvideocapture"></span>
### stopVideoCapture

```cpp
virtual int stopVideoCapture() = 0;
```


Disable internal video capture immediately. The default is off.

Internal video capture refers to: use the RTC SDK built\-in video capture module to capture.

The local client will be informed via [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onvideodevicestatechanged) after stopping video capture by calling this API.

The remote clients in the room will be informed of the state change via [onUserStopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onuserstopvideocapture) after the visible client stops video capture by calling this API.

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* Call [startVideoCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startvideocapture) to enable the internal video capture.

* Without calling this API the internal video capture will sustain until you destroy the engine instance.

    &nbsp;


<span id="setvideocaptureconfig"></span>
### setVideoCaptureConfig

```cpp
virtual int setVideoCaptureConfig(const VideoCaptureConfig& video_capture_config) = 0;
```


Set the video capture parameters for internal capture of the RTC SDK.

If your project uses the SDK internal capture module, you can specify the video capture parameters including preference, resolution and frame rate through this interface.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|video_capture_config |const VideoCaptureConfig& |Video capture parameters. See: [VideoCaptureConfig](https://docs.byteplus.com/en/docs/12/docs-85519#VideoCaptureConfig). |


**Return Value**


* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* This interface can be called after the engine is created and takes effect immediately after being called. It is recommended to call this interface before calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startvideocapture).

* It is recommended that different Engines on the same device use the same video capture parameters.

* If you used the internal module to start video capture before calling this interface, the capture parameters default to Auto.

    &nbsp;


<span id="setvideocapturerotation"></span>
### setVideoCaptureRotation

```cpp
virtual int setVideoCaptureRotation(VideoRotation rotation) = 0;
```


Set the rotation of the video images captured from the local device.

Call this API to rotate the videos when the camera is fixed upside down or tilted.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rotation |VideoRotation |It defaults to `VIDEO_ROTATION_0(0)`, which means not to rotate. Refer to [VideoRotation](https://docs.byteplus.com/en/docs/12/docs-85519#VideoRotation). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* This API affects the external\-sourced videos. The final rotation would be the original rotation angles adding up with the rotation set by calling this API.

    &nbsp;


<span id="setvideoencoderconfig"></span>
### setVideoEncoderConfig

```cpp
virtual int setVideoEncoderConfig(const VideoEncoderConfig& encoder_config) = 0;
```


Sets the expected quality of the video stream by specifying the resolution, frame rate, bitrate, and the fallback strategy when the network is poor.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|encoder_config |const VideoEncoderConfig& |See [VideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-85519#VideoEncoderConfig). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* This method can only set a single profile for the video stream. If you intend to publish the stream in multiple qualities, use [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setlocalsimulcastmode).

* Without calling this method, only one stream will be sent with a profile of 640px × 360px @15fps. The default encoding preference is frame rate\-first.

* If you use an external video source, you can also use this method to set the encoding parameters.

    &nbsp;


<span id="setlocalsimulcastmode"></span>
### setLocalSimulcastMode

```cpp
virtual int setLocalSimulcastMode(
    VideoSimulcastMode mode,
    const VideoEncoderConfig* stream_config,
    int num
) = 0;
```


> Available since 3.60.


Enable the Simulcast feature and configure the lower\-quality video streams settings.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mode |VideoSimulcastMode |Whether to publish lower\-quality streams and how many of them to be published. See [VideoSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-85519#VideoSimulcastMode). By default, it is set to Single, where the publisher sends the video in a single profile. In the other modes, the low\-quality stream is set to a default resolution of 160px × 90px with a bitrate of 50Kbps. |
|stream_config |const VideoEncoderConfig\* |The specification of the lower quality stream. See [VideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-85519#VideoEncoderConfig). The resolution of the lower quality stream must be smaller than the standard stream set via [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setvideoencoderconfig). The specifications in the array must be arranged in ascending order based on resolution.<br><br>In the other modes, the low\-quality stream is set to a default resolution of 160px × 90px with a bitrate of 50Kbps. |
|num |int |The number of the lower quality streams, which is also the length of the stream_config array. The maximum value is 3. |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* The default specification of the video stream is 640px × 360px @15fps.

* The method applies to the camera video only.

* Refer to [Simulcasting](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70139) for more information.

    &nbsp;


<span id="setlocalsimulcastmode"></span>
### setLocalSimulcastMode

```cpp
virtual int setLocalSimulcastMode(VideoSimulcastMode mode) = 0;
```


> Available since 3.60.


Enable the Simulcast feature.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mode |VideoSimulcastMode |Whether to publish lower\-quality streams and how many of them to be published. See [VideoSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-85519#VideoSimulcastMode).<br><br>By default, it is set to Single, where the publisher sends the video in a single profile. In the other modes, the low\-quality stream is set to a default resolution of 160px × 90px with a bitrate of 50Kbps. |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* Call this method before the user joins a room.

* The default specification of the video stream is 640px × 360px @15fps.

* If you intend to specify the lower\-quality streams, use setLocalSimulcastMode(VideoSimulcastMode mode, const VideoEncoderConfig\* stream_config, int num).

* The method applies to the camera video only.

* Refer to [Simulcasting](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70139) for more information.

    &nbsp;


<span id="setlocalvideocanvas"></span>
### setLocalVideoCanvas

```cpp
virtual int setLocalVideoCanvas(const VideoCanvas& canvas) = 0;
```


Sets the view to be used for local video rendering and the rendering mode.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|canvas |const VideoCanvas& |View information and rendering mode. See [VideoCanvas](https://docs.byteplus.com/en/docs/12/docs-85519#VideoCanvas). |


**Return Value**


* 0: Success.

* \-2: Invalid parameter.

* \-12: This method is not available in the Audio SDK.


**Notes**


* You should bind your stream to a view before joining the room. This setting will remain in effect after you leave the room.

* If you need to unbind the local video stream from the current view, you can call this API and set the videoCanvas to `null`.

* For Linux SDK: Only available in Client version, not available in Server version.

    &nbsp;


<span id="updatelocalvideocanvas"></span>
### updateLocalVideoCanvas

```cpp
virtual int updateLocalVideoCanvas(
    const enum RenderMode render_mode,
    const uint32_t background_color
) = 0;
```


Update the render mode and background color of local video rendering

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|render_mode |const enum RenderMode |See [RenderMode](https://docs.byteplus.com/en/docs/12/docs-85519#RenderMode). |
|background_color |const uint32_t |See [VideoCanvas](https://docs.byteplus.com/en/docs/12/docs-85519#VideoCanvas).background_color. |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**

Calling this API during local video rendering will be effective immediately.

<span id="IRTCEngine-setremotevideocanvas"></span>
### setRemoteVideoCanvas

```cpp
virtual int setRemoteVideoCanvas(
    const char* stream_id,
    const VideoCanvas& canvas
) = 0;
```


Set the view and mode for rendering the specific video stream.

If you need to unbind the canvas for the video stream, set the canvas to `Null`.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |identifier o fstream |
|canvas |const VideoCanvas& |canvas and rendering mode. See [VideoCanvas](https://docs.byteplus.com/en/docs/12/docs-85519#VideoCanvas) |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* When the local user leaves the room, the setting will be invalid. The remote user leaving the room does not affect the setting.

* For Linux SDK: Only available in Client version, not available in Server version.

    &nbsp;


<span id="updateremotestreamvideocanvas"></span>
### updateRemoteStreamVideoCanvas

```cpp
virtual int updateRemoteStreamVideoCanvas(
    const char* stream_id,
    const RemoteVideoRenderConfig& remote_video_render_config
) = 0;
```


> Available since 3.56


Modifies remote video frame rendering settings, including render mode, background color, and rotation angle, while using the internal rendering of the SDK.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of stream |
|remote_video_render_config |const RemoteVideoRenderConfig& |Video rendering settings. See [RemoteVideoRenderConfig](https://docs.byteplus.com/en/docs/12/docs-85519#RemoteVideoRenderConfig). |


**Return Value**


* 0: Success.

* < 0 : Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* After setting the rendering configuration for the remote video frame with [setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setremotevideocanvas), you can call this API to update settings including render mode, background color, and rotation angle.

* Calling this API during remote video rendering will be effective immediately.

    &nbsp;


<span id="setlocalvideosink"></span>
### setLocalVideoSink

```cpp
virtual int setLocalVideoSink(
    IVideoSink* video_sink,
    LocalVideoSinkConfig& config
) = 0;
```


> Available since 3.60.


Binds the local video stream to a custom renderer.You can get video frame data at specified positions and formats through parameter settings.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|video_sink |IVideoSink\* |Custom video renderer. See [IVideoSink](https://docs.byteplus.com/en/docs/12/docs-85519#IVideoSink). |
|config |LocalVideoSinkConfig& |Local video frame callback configuration, see [LocalVideoSinkConfig](https://docs.byteplus.com/en/docs/12/docs-85519#LocalVideoSinkConfig)。 |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* RTC SDK uses its own renderer (internal renderer) for video rendering by default.

* Leaving the room will clear the binding status.

* If you need to unbind the video stream from the custom renderer, you must set video_sink to `null`.

* Generally, after receiving the [onFirstLocalVideoFrameCaptured](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onfirstlocalvideoframecaptured) callback notification that the first local video frame has been captured, call this method to bind a custom renderer to a video stream and join the room.

    &nbsp;


<span id="setremotevideosink"></span>
### setRemoteVideoSink

```cpp
virtual int setRemoteVideoSink(
    const char* stream_id,
    IVideoSink* video_sink,
    RemoteVideoSinkConfig& config
) = 0;
```


> Available since 3.57


Binds the remote video stream to a custom renderer.You can get video frame data at specified positions and formats through parameter settings.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of stream |
|video_sink |IVideoSink\* |Custom video renderer. See [IVideoSink](https://docs.byteplus.com/en/docs/12/docs-85519#IVideoSink). |
|config |RemoteVideoSinkConfig& |remote video frame callback configuration, see [RemoteVideoSinkConfig](https://docs.byteplus.com/en/docs/12/docs-85519#RemoteVideoSinkConfig)。 |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* RTC SDK uses its own renderer (internal renderer) for video rendering by default.

* This method can be called both before and after entering the room. If you are unable to obtain remote stream information in advance, you can call this method after joining the room and receiving the remote stream information through the onUserPublishStream callback.

* Leaving the room will clear the binding status.

* If you need to unbind the video stream from the custom renderer, you must set video_sink to `null`.

    &nbsp;


<span id="updatescreencaptureregion"></span>
### updateScreenCaptureRegion

```cpp
virtual int updateScreenCaptureRegion(const Rectangle& region_rect) = 0;
```


Update the capture area when capturing screen video streams through the capture module provided by the RTC SDK. Only used when the capture source is the monitor screen.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|region_rect |const Rectangle& |Region to be shared. See [Rectangle](https://docs.byteplus.com/en/docs/12/docs-85519#Rectangle)<br><br>&nbsp;<br><br>This parameter describes the region to be shared after calling this API, and the relative relationship between the `source_info` setting area in [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startscreenvideocapture). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* Before calling this interface, internal screen stream capture must have been turned on by calling [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startscreenvideocapture).

* For Linux SDK: Only available in Client version, not available in Server version.

    &nbsp;


<span id="startscreenvideocapture"></span>
### startScreenVideoCapture

```cpp
virtual int startScreenVideoCapture(
    const ScreenCaptureSourceInfo& source_info,
    const ScreenCaptureParameters& capture_params
) = 0;
```


Capture screen video stream for sharing. Screen video stream includes: content displayed on the screen, in the application window, or in the virtual screen.

Displaying contents in virtual screens is only available on Windows.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|source_info |const ScreenCaptureSourceInfo& |Screen capture source information. See [ScreenCaptureSourceInfo](https://docs.byteplus.com/en/docs/12/docs-85519#ScreenCaptureSourceInfo).<br><br>&nbsp;<br><br>Call [getScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-getscreencapturesourcelist) to get all the screen sources that can be shared. |
|capture_params |const ScreenCaptureParameters& |Screen capture parameters. See [ScreenCaptureParameters](https://docs.byteplus.com/en/docs/12/docs-85519#ScreenCaptureParameters). |


**Return Value**


* 0: Success;

* \-1: Failure;


**Notes**


* The call of this API takes effects only when you are using RTC SDK to record screen. You will get a warning by [onVideoDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onvideodevicewarning) after calling this API when the video source is set to an external recorder.

* This API only starts screen capturing but does not publish the captured video. Call [publishStreamVideo](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-publishstreamvideo) to publish the captured video.

* To turn off screen video capture, call [stopScreenVideoCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-stopscreenvideocapture).

* Local users will receive [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onvideodevicestatechanged) on the state of screen capturing such as start, pause, resume, and error.

* After successfully calling this API, local users will receive [onFirstLocalVideoFrameCaptured](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onfirstlocalvideoframecaptured).

* Before calling this API, you can call [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setvideoencoderconfig) to set the frame rate and encoding resolution of the screen video stream.

* After receiving [onFirstLocalVideoFrameCaptured](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onfirstlocalvideoframecaptured), you can set the local screen sharing view by calling [setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setlocalvideocanvas) or setLocalVideoSink .

* You can also register an observer by calling [setLocalVideoSink](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setlocalvideosink) and receive the captured screen video frame through [onFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IVideoSink-onframe).

* For Linux SDK: Only available in Client version, not available in Server version.

    &nbsp;


<span id="stopscreenvideocapture"></span>
### stopScreenVideoCapture

```cpp
virtual int stopScreenVideoCapture() = 0;
```


Stop screen video streaming.

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* This API can only stop the screen capture by the RTC SDK. If the video source has been set to external recorder, the call of this API will fail. You need to stop it in the external recorder.

* The call of this API takes effects only when you are using RTC SDK to record screen. You will get a warning by [onVideoDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onvideodevicewarning) after calling this API when the video source is set to an external recorder.

* To turn on screen video stream capture, calling [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startscreenvideocapture)

* Local users will receive the [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onvideodevicestatechanged) callback.

* Calling this interface does not affect screen video stream publishing.

* For Linux SDK: Only available in Client version, not available in Server version.

    &nbsp;


<span id="updatescreencapturehighlightconfig"></span>
### updateScreenCaptureHighlightConfig

```cpp
virtual int updateScreenCaptureHighlightConfig(const HighlightConfig& highlight_config) = 0;
```


Update border highlighting settings when capturing screen video streams through the capture module provided by the RTC SDK. The default display table box.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|highlight_config |const HighlightConfig& |Border highlighting settings. See [HighlightConfig](https://docs.byteplus.com/en/docs/12/docs-85519#HighlightConfig) |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* Before calling this interface, you must have turned on internal screen flow collection by calling [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startscreenvideocapture).

* For Linux with X11 protocal, the API is valid; for Linux with Wayland, the API is not valid.

* For Linux SDK: Only available in Client version, not available in Server version.

    &nbsp;


<span id="updatescreencapturemousecursor"></span>
### updateScreenCaptureMouseCursor

```cpp
virtual int updateScreenCaptureMouseCursor(MouseCursorCaptureState capture_mouse_cursor) = 0;
```


Update the processing settings for the mouse when capturing screen video streams through the capture module provided by the RTC SDK. Default acquisition mouse.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|capture_mouse_cursor |MouseCursorCaptureState |See [MouseCursorCaptureState](https://docs.byteplus.com/en/docs/12/docs-85519#MouseCursorCaptureState) |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* Before calling this interface, internal screen stream capture must have been turned on by calling [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startscreenvideocapture).

* For Linux SDK: Only available in Client version, not available in Server version.

    &nbsp;


<span id="getscreencapturesourcelist"></span>
### getScreenCaptureSourceList

```cpp
virtual IScreenCaptureSourceList* getScreenCaptureSourceList() = 0;
```


Get the item list for screen sharing.

**Return Value**

List of the screen\-sharing objects, including application window and screens. See [IScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/25049#IScreenCaptureSourceList). After deciding which item to be shared, the user can share the object with [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startscreenvideocapture).

**Notes**


* For Linux with X11 protocal, the API is valid; for Linux with Wayland, the API is not valid. For Linux with Wayland, when you call [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startscreenvideocapture), the system pops a windows for the user to choose the object to share.

* Call [release](https://docs.byteplus.com/en/docs/12/25049#IScreenCaptureSourceList-release) to release the resources.

* For Linux SDK: Only available in Client version, not available in Server version.

    &nbsp;


<span id="getthumbnail"></span>
### getThumbnail

```cpp
virtual IVideoFrame* getThumbnail(
            ScreenCaptureSourceType type, view_t source_id, int max_width, int max_height) = 0;
```


Get the preview thumbnail of the screen\-sharing object

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |ScreenCaptureSourceType |Type of the screen capture object. Refer to [ScreenCaptureSourceType](https://docs.byteplus.com/en/docs/12/docs-85519#ScreenCaptureSourceType) for more details. |
|source_id |view_t |ID of the screen sharing object, which can be obtained from the list of shared objects enumerated by [getScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-getscreencapturesourcelist). For more details, see [view_t](https://docs.byteplus.com/en/docs/12/25049#view_t). |
|max_width |int |Maximum width of the preview thumbnail. RTC will scale the thumbnail to fit the given size while maintaining the original aspect ratio. If the aspect ratio of the given size does not match the sharing object, the thumbnail will have blank borders. |
|max_height |int |Maximum height of the preview thumbnail. Refer to the note for `max_width`. |


**Return Value**

Preview thumbnail of the screen\-sharing object Refer to [IVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IVideoFrame) for more details.

**Notes**


* For Linux with X11 protocal, the API is valid; for Linux with Wayland, the API is not valid.

* For Linux SDK: Only available in Client version, not available in Server version.

    &nbsp;


<span id="getwindowappicon"></span>
### getWindowAppIcon

```cpp
virtual IVideoFrame* getWindowAppIcon(
    view_t source_id,
    int max_width = 100,
    int max_height = 100
) = 0;
```


Get application window preview thumbnail for screen sharing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|source_id |view_t |ID of the screen\-sharing object. You can get the ID by calling [getScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-getscreencapturesourcelist). |
|max_width |int |Maximum width of the App icon. The width is always equal to the height. SDK will set the height and width to the smaller value if the given values are unequal. RTC will return nullptr if you set the value with a number out of the valid range, [32, 256]. The default size is 100 x 100. |
|max_height |int |Maximum height of the app icon. Refer to the note for `max_width` |


**Return Value**

Refer to [IVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IVideoFrame) for more details. You can get the icon when the item to be shared is an application and the application is assigned with an icon. If not, the return value will be nullptr.

**Notes**


* For Linux with X11 protocal, the API is valid; for Linux with Wayland, the API is not valid.

* For Linux SDK: Only available in Client version, not available in Server version.

    &nbsp;


<span id="setvideosourcetype"></span>
### setVideoSourceType

```cpp
virtual int setVideoSourceType(VideoSourceType type) = 0;
```


Set the video source, including the screen recordings.

The internal video capture is the default, which refers to capturing video using the built\-in module.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |VideoSourceType |Video source type. Refer to [VideoSourceType](https://docs.byteplus.com/en/docs/12/docs-85519#VideoSourceType) for more details. |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* You can call this API whether the user is in a room or not.

* Calling this API to switch to the custom video source will stop the enabled internal video capture.

* To switch to internal video capture, call this API to stop custom capture and then call [startVideoCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startvideocapture) to enable internal video capture.

* To push custom encoded video frames to the SDK, call this API to switch `VideoSourceType` to `VideoSourceTypeEncodedWithAutoSimulcast` or `VideoSourceTypeEncodedWithoutAutoSimulcast`.

    &nbsp;


<span id="pushexternalvideoframe"></span>
### pushExternalVideoFrame

```cpp
virtual int pushExternalVideoFrame(const VideoFrameData& frame) = 0;
```


Pushes external video frames.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|frame |const VideoFrameData& |Set the video frame. See [IVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IVideoFrame). |


**Return Value**

API call result:


* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for specific reasons.


**Notes**


* Support for I420, NV12, RGBA, BGRA, and ARGB.

* This function runs in the user calling thread.

* Before pushing external video frames, you must call [setVideoSourceType](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setvideosourcetype) to turn on external video source capture.

    &nbsp;


<span id="creatertcroom"></span>
### createRTCRoom

```cpp
virtual IRTCRoom* createRTCRoom(const char* room_id) = 0;
```


Create a RTC room instance.

This API only returns a RTCroom instance. You still need to call [joinRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-joinroom) to actually create/join the room.

Each call of this API creates one [IRTCRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom) instance. Call this API as many times as the number of rooms you need, and then call [joinRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-joinroom) of each IRTCRoom instance to join multiple rooms at the same time.

In multi\-room mode, a user can subscribe to media streams in the joined rooms at the same time.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|room_id |const char\* |The string matches the regular expression: `[a-zA-Z0-9_\@\\-\\.]{1,128}`. |


**Return Value**

[IRTCRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom) instance.

If you get NULL instead of an RTCRoom instance, please ensure the room_id is valid. And the specified room is not yet created.

**Notes**


* If the room that you wish to join already exists, you still need to call this API first to create the IRTCRoom instance, and then call [joinRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-joinroom).

* Do not create multiple rooms with the same room_id, otherwise the newly created room instance will replace the old one.

* To forward streams to the other rooms, call [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-startforwardstreamtorooms) instead of enabling Multi\-room mode.

    &nbsp;


<span id="creatertsroom"></span>
### createRTSRoom

```cpp
virtual IRTSRoom* createRTSRoom(const char* room_id) = 0;
```


Create an RTS room instance.

This API only returns an RTS room instance. You still need to call [joinRTSRoom](https://docs.byteplus.com/en/docs/12/25049#IRTSRoom-joinrtsroom) to actually create/join the room.

Each call of this API creates one [IRTSRoom](https://docs.byteplus.com/en/docs/12/25049#IRTSRoom) instance. Call this API as many times as the number of rooms you need, and then call [joinRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-joinroom) of each IRTCRoom instance to join multiple rooms at the same time.

In multi\-room mode, a user can send and receive rts message in the joined rooms at the same time.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|room_id |const char\* |The string matches the regular expression: `[a-zA-Z0-9_\@\\-\\.]{1,128}`. |


**Return Value**

[IRTSRoom](https://docs.byteplus.com/en/docs/12/25049#IRTSRoom) instance.

If you get NULL instead of an RTCRoom instance, please ensure the room_id is valid. And the specified room is not yet created.

**Notes**


* If the room that you wish to join already exists, you still need to call this API first to create the IRTSRoom instance, and then call [joinRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-joinroom).

* Do not create multiple rooms with the same room_id, otherwise the newly created room instance will replace the old one.

    &nbsp;


<span id="setpublishfallbackoption"></span>
### setPublishFallbackOption

```cpp
virtual int setPublishFallbackOption(PublishFallbackOption option) = 0;
```


Sets the fallback option for published audio & video streams.

You can call this API to set whether to automatically lower the resolution you set of the published streams under limited network conditions.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|option |PublishFallbackOption |Fallback option, see [PublishFallbackOption](https://docs.byteplus.com/en/docs/12/docs-85519#PublishFallbackOption). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* This API only works after you call [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setlocalsimulcastmode) to enable the mode of publishing multiple streams.

* You must call this API before entering the room.

* After calling this method, if there is a performance degradation or recovery due to poor performance or network conditions, the local end will receive early warnings through the [onPerformanceAlarms](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onperformancealarms) callback to adjust the capture device.

* After you allow video stream to fallback, your stream subscribers will receive [onSimulcastSubscribeFallback](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onsimulcastsubscribefallback) when the resolution of your published stream are lowered or restored.

* You can alternatively set fallback options with distrubutions from server side, which is of higher priority.

    &nbsp;


<span id="setsubscribefallbackoption"></span>
### setSubscribeFallbackOption

```cpp
virtual int setSubscribeFallbackOption(SubscribeFallbackOption option) = 0;
```


Sets the fallback option for subscribed RTC streams.

You can call this API to set whether to lower the resolution of currently subscribed stream under limited network conditions.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|option |SubscribeFallbackOption |Fallback option, see [SubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/docs-85519#SubscribeFallbackOption) for more details. |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* You must call this API before enterting the room.

* After you enables the fallback, you will receive [onSimulcastSubscribeFallback](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onsimulcastsubscribefallback) and [onRemoteVideoSizeChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onremotevideosizechanged) when the resolution of your subscribed stream is lowered or restored.

* You can alternatively set fallback options with distrubutions from server side, which is of higher priority.

    &nbsp;


<span id="setremoteuserpriority"></span>
### setRemoteUserPriority

```cpp
virtual int setRemoteUserPriority(
    const char* room_id,
    const char* user_id,
    RemoteUserPriority priority
) = 0;
```


Set user priority

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|room_id |const char\* |Room ID |
|user_id |const char\* |Remote user's ID |
|priority |RemoteUserPriority |Remote user's requirement priority. See enumeration type [RemoteUserPriority](https://docs.byteplus.com/en/docs/12/docs-85519#RemoteUserPriority) |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* This method is used with [setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setsubscribefallbackoption).

* If the subscription flow fallback option is turned on, weak connections or insufficient performance will give priority to ensuring the quality of the flow received by high\-priority users.

* This method can be used before and after entering the room, and the priority of the remote user can be modified.

       &nbsp;


<span id="setbusinessid"></span>
### setBusinessId

```cpp
virtual int setBusinessId(const char* business_id) = 0;
```


Sets the business ID

You can use businessId to distinguish different business scenarios. You can customize your businessId to serve as a sub AppId, which can share and refine the function of the AppId, but it does not need authentication.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|business_id |const char\* |Your customized businessId<br><br>&nbsp;<br><br>BusinessId is a tag, and you can customize its granularity. |


**Return Value**


* 0: Success.

* \-2: The input is invalid. Legal characters include all lowercase letters, uppercase letters, numbers, and four other symbols, including '.', '\-','_', and '@'.


**Notes**


* You must call this API before the [joinRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-joinroom) API, otherwise it will be invalid.

    &nbsp;


<span id="setremotevideomirrortype"></span>
### setRemoteVideoMirrorType

```cpp
virtual int setRemoteVideoMirrorType(
    const char* stream_id,
    RemoteMirrorType mirror_type
) = 0;
```


> Available since 3.57


When using internal rendering, enable mirroring for the remote stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of stream |
|mirror_type |RemoteMirrorType |The mirror type for the remote stream, see RemoteMirrorType . |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details

    &nbsp;


<span id="getvideoeffectinterface"></span>
### getVideoEffectInterface

```cpp
virtual IVideoEffect* getVideoEffectInterface() = 0;
```


Gets video effect interfaces.

**Return Value**

Video effect interfaces. See [IVideoEffect](https://docs.byteplus.com/en/docs/12/25049#IVideoEffect).

<span id="IRTCEngine-setencryptinfo"></span>
### setEncryptInfo

```cpp
virtual int setEncryptInfo(
    EncryptType encrypt_type,
    const char* key,
    int key_size
) = 0;
```


Sets the way to use built\-in encryption when transmitting.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|encrypt_type |EncryptType |Built\-in encryption algorithm. See [EncryptType](https://docs.byteplus.com/en/docs/12/docs-85519#EncryptType) |
|key |const char\* |Encryption key, the length is limited to 36 bits, and the excess will be Truncate |
|key_size |int |The length of the parameter key |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* Use this method when using the built\-in encryption on transfer; if you need to use custom encryption on transfer. See onEncryptData . Built\-in encryption and custom encryption are mutually exclusive, and the transmission is determined to be encrypted according to the last method called.

* This method must be called before entering the room, and can be called repeatedly, taking the last called parameter as the effective parameter.

    &nbsp;


<span id="setcustomizeencrypthandler"></span>
### setCustomizeEncryptHandler

```cpp
virtual int setCustomizeEncryptHandler(IEncryptHandler* handler) = 0;
```


Sets custom encryption and decryption methods.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|handler |IEncryptHandler\* |Custom encryption handler, you need to implement the handler's encryption and decryption method. See [IEncryptHandler](https://docs.byteplus.com/en/docs/12/docs-85517#IEncryptHandler). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* This method is mutually exclusive with [setEncryptInfo](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setencryptinfo), you can only select custom encryption method or default encryption method. The encryption method that takes effect depends on the last method called.

* This method must be called before entering the room, and can be called repeatedly, taking the last called parameter as the effective parameter.

* Whether encrypted or decrypted, the length of the modified data needs to be controlled under 180%. That is, if the input data is 100 bytes, the processed data must be less than 180 bytes. If the encryption or decryption result exceeds the limit, the audio & video frame may be discarded.

* Data encryption/decryption is performed serially, so depending on the implementation, it may affect the final rendering efficiency. Whether to use this method needs to be carefully evaluated by users.

    &nbsp;


<span id="enableaudioframecallback"></span>
### enableAudioFrameCallback

```cpp
virtual int enableAudioFrameCallback(
    AudioFrameCallbackMethod method,
    AudioFormat format
) = 0;
```


Enable audio frames callback and set the format for the specified type of audio frames.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|method |AudioFrameCallbackMethod |Audio data callback method. See [AudioFrameCallbackMethod](https://docs.byteplus.com/en/docs/12/docs-85519#AudioFrameCallbackMethod).<br><br>&nbsp;<br><br>If `method` is set as `kRecord`, `kPlayback`, `kMixed`, `kRecordScreen`, `kCaptureMixed`, set `format` to the accurate value listed in the audio parameters format.<br><br>&nbsp;<br><br>If `method` is set as `kRemoteUser`, set `format` to `auto`. |
|format |AudioFormat |Audio parameters format. See [AudioFormat](https://docs.byteplus.com/en/docs/12/docs-85519#AudioFormat). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**

After calling this API and [registerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-registeraudioframeobserver), [IAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-85517#IAudioFrameObserver) will receive the corresponding audio data callback. However, these two APIs are independent of each other and the calling order is not restricted.

<span id="IRTCEngine-disableaudioframecallback"></span>
### disableAudioFrameCallback

```cpp
virtual int disableAudioFrameCallback(AudioFrameCallbackMethod method) = 0;
```


Disables audio data callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|method |AudioFrameCallbackMethod |Audio data callback method. See [AudioFrameCallbackMethod](https://docs.byteplus.com/en/docs/12/docs-85519#AudioFrameCallbackMethod). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**

Call this API after calling [enableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-enableaudioframecallback).

<span id="IRTCEngine-registeraudioframeobserver"></span>
### registerAudioFrameObserver

```cpp
virtual int registerAudioFrameObserver(IAudioFrameObserver* observer) = 0;
```


Register an audio frame observer.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|observer |IAudioFrameObserver\* |Audio data callback observer. See [IAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-85517#IAudioFrameObserver). Use `null` to cancel the registration. |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**

After calling this API and [enableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-enableaudioframecallback), [IAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-85517#IAudioFrameObserver) receives the corresponding audio data callback. You can retrieve the audio data and perform processing on it without affecting the audio that RTC SDK uses to encode or render.

<span id="IRTCEngine-registeraudioprocessor"></span>
### registerAudioProcessor

```cpp
virtual int registerAudioProcessor(IAudioFrameProcessor* processor) = 0;
```


Register a custom audio preprocessor.

After that, you can call [enableAudioProcessor](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-enableaudioprocessor) to process the audio streams that either captured locally or received from the remote side. RTC SDK then encodes or renders the processed data.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|processor |IAudioFrameProcessor\* |Custom audio processor. See [IAudioFrameProcessor](https://docs.byteplus.com/en/docs/12/docs-85517#IAudioFrameProcessor)。<br><br>&nbsp;<br><br>SDK only holds weak references to the processor, you should guarantee its Life Time. To cancel registration, set the parameter to nullptr. |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* When this interface is repeatedly called, only the last call takes effect.

* Refer to [Custom Audio Processing](https://docs.byteplus.com/en/byteplus-rtc/docs/80635) for more information.

    &nbsp;


<span id="enableaudioprocessor"></span>
### enableAudioProcessor

```cpp
virtual int enableAudioProcessor(
    AudioProcessorMethod method,
    AudioFormat format
) = 0;
```


Enable audio frames callback for custom processing and set the format for the specified type of audio frames.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|method |AudioProcessorMethod |The types of audio frames. See [AudioProcessorMethod](https://docs.byteplus.com/en/docs/12/docs-85519#AudioProcessorMethod). Set this parameter to process multiple types of audio.<br><br>&nbsp;<br><br>With different values, you will receive the corresponding callback:<br><br><br>&nbsp;<br><br>* For locally captured audio, you will receive [onProcessRecordAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IAudioFrameProcessor-onprocessrecordaudioframe).<br><br>* For mixed remote audio, you will receive [onProcessPlayBackAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IAudioFrameProcessor-onprocessplaybackaudioframe).<br><br>* For audio from remote users, you will receive [onProcessRemoteUserAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IAudioFrameProcessor-onprocessremoteuseraudioframe). |
|format |AudioFormat |The format of audio frames. See [AudioFormat](https://docs.byteplus.com/en/docs/12/docs-85519#AudioFormat). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* Before calling this API, call [registerAudioProcessor](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-registeraudioprocessor) to register a processor.

* To disable custom audio processing, call [disableAudioProcessor](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-disableaudioprocessor).

    &nbsp;


<span id="disableaudioprocessor"></span>
### disableAudioProcessor

```cpp
virtual int disableAudioProcessor(AudioProcessorMethod method) = 0;
```


Disable custom audio processing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|method |AudioProcessorMethod |Audio Frame type. See [AudioProcessorMethod](https://docs.byteplus.com/en/docs/12/docs-85519#AudioProcessorMethod). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details

    &nbsp;


<span id="registerlocalvideoprocessor"></span>
### registerLocalVideoProcessor

```cpp
virtual int registerLocalVideoProcessor(
    IVideoProcessor* processor,
    VideoPreprocessorConfig config
) = 0;
```


Set up a custom video preprocessor.

Using this video preprocessor, you can call [processVideoFrame](https://docs.byteplus.com/en/docs/12/25049#IVideoProcessor-processvideoframe) to preprocess the video frames collected by the RTC SDK, and use the processed video frames for RTC audio & video communication.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|processor |IVideoProcessor\* |Custom video processor. See [IVideoProcessor](https://docs.byteplus.com/en/docs/12/25049#IVideoProcessor). If null is passed in, the video frames captured by the RTC SDK are not preprocessed.<br><br>&nbsp;<br><br>SDK only holds weak references to the processor, you should guarantee its Life Time. |
|config |VideoPreprocessorConfig |Customize the settings applicable to the video pre\-processor. See [VideoPreprocessorConfig](https://docs.byteplus.com/en/docs/12/docs-85519#VideoPreprocessorConfig).<br><br>&nbsp;<br><br>Currently, the 'required_pixel_format 'in'config' only supports: 'kVideoPixelFormatI420' and'kVideoPixelFormatUnknown ':<br><br><br>&nbsp;<br><br>* When set to'kVideoPixelFormatUnknown', the RTC SDK gives the format of the video frame for processing by the processor, that is, the format of the acquisition.<br><br>   You can get the actual captured video frame format and pixel type by [VideoBufferType](https://docs.byteplus.com/en/docs/12/docs-85519#VideoBufferType) and [VideoPixelFormat](https://docs.byteplus.com/en/docs/12/docs-85519#VideoPixelFormat).<br><br>* When set to'kVideoPixelFormatI420 ', the RTC SDK converts the captured video frames into the corresponding format for pre\-processing. This method call fails when<br><br>* Is set to another value. |


**Return Value**


* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**

When this interface is repeatedly called, only the last call takes effect. The effects do not stack.

<span id="IRTCEngine-setvideodigitalzoomconfig"></span>
### setVideoDigitalZoomConfig

```cpp
virtual int setVideoDigitalZoomConfig(
    ZoomConfigType type,
    float size
) = 0;
```


> Available since 3.51


Set the step size for each digital zooming control to the local videos.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |ZoomConfigType |Required. Identifying which type the `size` is referring to. Refer to [ZoomConfigType](https://docs.byteplus.com/en/docs/12/docs-85519#ZoomConfigType). |
|size |float |Required. Reserved to three decimal places. It defaults to `0`.<br><br>&nbsp;<br><br>The meaning and range vary from different `type`s. If the scale or moving distance exceeds the range, the limit is taken as the result.<br><br><br>&nbsp;<br><br>* `kZoomConfigTypeFocusOffset`: Increasement or decrease to the scaling factor. Range: [0, 7]. For example, when it is set to 0.5 and [setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setvideodigitalzoomcontrol) is called to zoom in, the scale will increase `0.5`. The scale ranges [1，8] and defaults to `1`, which means an original size.<br><br>* `kZoomConfigTypeMoveOffset`：Ratio of the distance to the border of video images. It ranges [0, 0.5] and defaults to `0`, which means no offset. When you call [setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setvideodigitalzoomcontrol) and choose `CAMERA_MOVE_LEFT`, the moving distance is size x original width. While for the `CAMERA_MOVE_UP`, the moving distance is size x original height. Suppose that a video spans 1080 px and the `size` is set to `0.5` so that the distance would be 0.5 x 1080 px = 540 px. |


**Return Value**


* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* Only one size can be set for a single call. You must call this API to pass values respectively if you intend to set multiple `size`s.

* As the default `size` is `0`, you must call this API before performing any digital zoom control by calling [setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setvideodigitalzoomcontrol) or [startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startvideodigitalzoomcontrol).

    &nbsp;


<span id="setvideodigitalzoomcontrol"></span>
### setVideoDigitalZoomControl

```cpp
virtual int setVideoDigitalZoomControl(ZoomDirectionType direction) = 0;
```


> Available since 3.51


Digital zoom or move the local video image once. This action affects both the video preview locally and the stream published.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|direction |ZoomDirectionType |Action of the digital zoom control. Refer to [ZoomDirectionType](https://docs.byteplus.com/en/docs/12/docs-85519#ZoomDirectionType). |


**Return Value**


* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* As the default offset is `0`, you must call [setVideoDigitalZoomConfig](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setvideodigitalzoomconfig) before this API.

* You can only move video images after they are magnified via this API or [startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startvideodigitalzoomcontrol).

* When you request an out\-of\-range scale or movement, SDK will execute it with the limits. For example, when the image has been moved to the border, the image cannot be zoomed out, or has been magnified to 8x.

* Call [startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startvideodigitalzoomcontrol) to have a continuous and repeatedly digital zoom control.

* Mobile devices can control the optical zoom of the camera, see `setCameraZoomRatio`.

    &nbsp;


<span id="startvideodigitalzoomcontrol"></span>
### startVideoDigitalZoomControl

```cpp
virtual int startVideoDigitalZoomControl(ZoomDirectionType direction) = 0;
```


> Available since 3.51


Continuous and repeatedly digital zoom control. This action effect both the video preview locally and the stream published.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|direction |ZoomDirectionType |Action of the digital zoom control. Refer to [ZoomDirectionType](https://docs.byteplus.com/en/docs/12/docs-85519#ZoomDirectionType). |


**Return Value**


* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* As the default offset is `0`, you must call [setVideoDigitalZoomConfig](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setvideodigitalzoomconfig) before this API.

* You can only move video images after they are magnified via this API or [setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setvideodigitalzoomcontrol).

* The control process stops when the scale reaches the limit, or the images have been moved to the border. if the next action exceeds the scale or movement range, SDK will execute it with the limits.

* Call [stopVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-stopvideodigitalzoomcontrol) to stop the ongoing zoom control.

* Call [setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setvideodigitalzoomcontrol) to have a one\-time digital zoom control.

* Mobile devices can control the optical zoom of the camera, see `setCameraZoomRatio`.

    &nbsp;


<span id="stopvideodigitalzoomcontrol"></span>
### stopVideoDigitalZoomControl

```cpp
virtual int stopVideoDigitalZoomControl() = 0;
```


> Available since 3.51


Stop the ongoing digital zoom control instantly.

**Return Value**


* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**

Refer to [startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startvideodigitalzoomcontrol) for starting digital zooming.

<span id="IRTCEngine-sendseimessage"></span>
### sendSEIMessage

```cpp
virtual int sendSEIMessage(
    const uint8_t* message,
    int length,
    int repeat_count,
    SEICountPerFrame mode
) = 0;
```


<span id="IRTCEngine\-sendseimessage\-2"\></span\> Sends SEI data.

In a video call scenario, SEI is sent with the video frame, while in a voice call scenario, SDK will automatically publish a black frame with a resolution of 16 × 16 pixels to carry SEI data.

In a voice call, you should set this parameter to `kStreamIndexMain`, otherwise the SEI data is discarded and cannot be sent to the remote user.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|message |const uint8_t\* |SEI data. |
|length |int |SEI data length. No more than 4 KB SEI data per frame is recommended. |
|repeat_count |int |Number of times a message is sent repeatedly. The value range is [0, max{29, %{video frame rate}\-1}]. Recommended range: [2,4].<br><br>&nbsp;<br><br>After calling this API, the SEI data will be added to a consecutive `repeat_count+1` number of video frames starting from the current frame. |
|mode |SEICountPerFrame |SEI sending mode. See [SEICountPerFrame](https://docs.byteplus.com/en/docs/12/docs-85519#SEICountPerFrame). |


**Return Value**


* \>= 0: The number of SEIs to be added to the video frame

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* We recommend the number of SEI messages per second should not exceed the current video frame rate. In a voice call, the blank\-frame rate is 15 fps.

* We recommended using the same sending mode from the start to the end of the program.

* In a voice call, this API can be called to send SEI data only in internal capture mode.

* In a video call, the custom captured video frame can also be used for sending SEI data if the original video frame contains no SEI data, otherwise calling this method will not take effect.

* Each video frame carrys only the SEI data received within 2s before and after. In a voice call scenario, if no SEI data is sent within 1min after calling this API, SDK will automatically cancel publishing black frames.

* After the message is sent successfully, the remote user who subscribed your video stream will receive [onSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onseimessagereceived).

* When you switch from a voice call to a video call, SEI data will automatically start to be sent with normally captured video frames instead of black frames.

    &nbsp;


<span id="sendlivepushseimessage"></span>
### sendLivePushSEIMessage

```cpp
virtual int sendLivePushSEIMessage(
    std::string json_string,
    int count,
    bool is_key_frame_only,
    bool allow_overwrite
) = 0;
```


Sends SEI data in Key\-Value format through video frames.

Before calling this API, you must set the room profile to `kRoomLiveModeSoloHost` when calling [setLiveMode](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-setlivemode) to enable Live Push mode.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|json_string |std::string |JSON formatted key\-value pairs, for example, `{"key1":"value1","key2":"value2"}`:<br><br><br>* If a key has an empty value (e.g., `""` or `null`), that key will be deleted from the SEI dictionary.<br><br>* Total size of merged SEI data must not exceed 10 KB. |
|count |int |The number of times this SEI data is continuously sent.<br><br><br>* When `is_key_frame_only` is true, it means sending with `count` keyframes (I\-frames);<br><br>* When `is_key_frame_only` is false, it means sending with `count` video frames. |
|is_key_frame_only |bool |Whether to send SEI only with keyframes (I\-frames):<br><br><br>* true: Send only with keyframes.<br><br>* false: Send with all frames. |
|allow_overwrite |bool |Whether subsequent requests are allowed to overwrite the value of this key:<br><br><br>* true: Subsequent requests can overwrite the key's value, and the `count` will also be updated to the new value;<br><br>* false: Subsequent requests will ignore any new value for this key and keep the original value. For an existing key, whether this write is allowed depends on the overwrite policy previously saved for that key. |


**Return Value**


* 0: Success.

* < 0: Failure.

* \-1: Video module not enabled.

* \-2: Parameter error (empty JSON or count <= 0).

* \-3: Invalid JSON format.

* \-4: Total SEI data size exceeds limit.

    &nbsp;


<span id="getvideodevicemanager"></span>
### getVideoDeviceManager

```cpp
virtual IVideoDeviceManager* getVideoDeviceManager() = 0;
```


Create a video Facility Management instance

**Return Value**

Video Facility Management instance. See [IVideoDeviceManager](https://docs.byteplus.com/en/docs/12/25049#IVideoDeviceManager)

<span id="IRTCEngine-getaudiodevicemanager"></span>
### getAudioDeviceManager

```cpp
virtual IAudioDeviceManager* getAudioDeviceManager() = 0;
```


Device audio management interface creation

**Return Value**

Audio Facility Management interface

<span id="IRTCEngine-startfilerecording"></span>
### startFileRecording

```cpp
virtual int startFileRecording(
    RecordingConfig config,
    RecordingType recording_type
) = 0;
```


This method records the audio & video data during the call to a local file.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|config |RecordingConfig |Local recording parameter configuration. See [RecordingConfig](https://docs.byteplus.com/en/docs/12/docs-85519#RecordingConfig) |
|recording_type |RecordingType |Local recording media type. See [RecordingType](https://docs.byteplus.com/en/docs/12/docs-85519#RecordingType).<br><br>&nbsp;<br><br>Note：Screen stream only supports recording video (kRecordingTypeVideoOnl)；Main stream supports recording all types. |


**Return Value**


* 0: normal

* \-1: Parameter setting exception

* \-2: The current version of the SDK does not support this Feature, please contact technical support staff


**Notes**


* You must join a room before calling this method.

* After calling this method, you will receive an [onRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onrecordingstateupdate) callback.

* If the recording is normal, the system will notify the recording progress through [onRecordingProgressUpdate](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onrecordingprogressupdate) Callback every second.

    &nbsp;


<span id="stopfilerecording"></span>
### stopFileRecording

```cpp
virtual int stopFileRecording() = 0;
```


Stop local recording

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* Call [startFileRecording](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startfilerecording) After starting local recording, you must call this method to stop recording.

* After calling this method, you will receive an [onRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onrecordingstateupdate) callback prompting you to record the result.

    &nbsp;


<span id="startaudiorecording"></span>
### startAudioRecording

```cpp
virtual int startAudioRecording(AudioRecordingConfig& config) = 0;
```


Starts recording audio communication, and generate the local file.

If you call this API before or after joining the room without internal audio capture, then the recording task can still begin but the data will not be recorded in the local files. Only when you call [startAudioCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startaudiocapture) to enable internal audio capture, the data will be recorded in the local files.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|config |AudioRecordingConfig& |See [AudioRecordingConfig](https://docs.byteplus.com/en/docs/12/docs-85519#AudioRecordingConfig). |


**Return Value**


* 0: `kReturnStatusSuccess`: Success

* \-2: `kReturnStatusParameterErr`: Invalid parameters

* \-3: `kReturnStatusWrongState`: Not valid in this SDK. Please contact the technical support.


**Notes**


* All audio effects are valid in the file. Mixed audio file is not included in the file.

* Call [stopAudioRecording](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-stopaudiorecording) to stop recording.

* You can call this API before and after joining the room. If this API is called before you join the room, you need to call [stopAudioRecording](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-stopaudiorecording) to stop recording. If this API is called after you join the room, the recording task ends automatically. If you join multiple rooms, audio from all rooms are recorded in one file.

* After calling the API, you'll receive [onAudioRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onaudiorecordingstateupdate).

    &nbsp;


<span id="stopaudiorecording"></span>
### stopAudioRecording

```cpp
virtual int stopAudioRecording() = 0;
```


Stop audio recording.

**Return Value**


* 0: Success

* <0: Failure


**Notes**

Call [startAudioRecording](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startaudiorecording) to start the recording task.

<span id="IRTCEngine-enableexternalsoundcard"></span>
### enableExternalSoundCard

```cpp
virtual int enableExternalSoundCard(bool enable) = 0;
```


Enable the audio process mode for external sound card.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|enable |bool |* true: enable<br><br>* false: disable (by default) |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* When you use external sound card for audio capture, enable this mode for better audio quality.

* When using the mode, you can only use earphones. If you need to use internal or external speaker, disable this mode.

    &nbsp;


<span id="setruntimeparameters"></span>
### setRuntimeParameters

```cpp
virtual int setRuntimeParameters(const char* json_string) = 0;
```


Set runtime parameters

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|json_string |const char\* |String after json serialization |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**

Call this API before [joinRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-joinroom) and [startAudioCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startaudiocapture).

<span id="IRTCEngine-feedback"></span>
### feedback

```cpp
virtual int feedback(
    uint64_t type,
    const ProblemFeedbackInfo* info
) = 0;
```


Report the user feedback to RTC.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |uint64_t |List of preset problems. See [ProblemFeedbackOption](https://docs.byteplus.com/en/docs/12/docs-85519#ProblemFeedbackOption) |
|info |const ProblemFeedbackInfo\* |Specific description of other problems other than the preset problem, and room's information. See [ProblemFeedbackInfo](https://docs.byteplus.com/en/docs/12/docs-85519#ProblemFeedbackInfo) |


**Return Value**


* 0: Success.

* \-3: Failure.


**Notes**

If the user is in the room when reporting, the report leads to the room / rooms where the user is currently located;

If the user is not in the room when reporting, the report leads to the previously exited Room.

<span id="IRTCEngine-getaudioeffectplayer"></span>
### getAudioEffectPlayer

```cpp
virtual IAudioEffectPlayer* getAudioEffectPlayer() = 0;
```


> Available since 3.53


Create an instance for audio effect player.

**Return Value**

See [IAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer).

<span id="IRTCEngine-getmediaplayer"></span>
### getMediaPlayer

```cpp
virtual IMediaPlayer* getMediaPlayer(int player_id) = 0;
```


> Available since 3.53


Create a media player instance.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player_id |int |Media player id. The range is `[0, 3]`. You can create up to 4 instances at the same time. If it exceeds the range, nullptr will be returned. |


**Return Value**

Media player instance. See [IMediaPlayer](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer).

<span id="IRTCEngine-login"></span>
### login

```cpp
virtual int login(
    const char* token,
    const char* uid
) = 0;
```


Log in to RTS server.

Log in to call [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-sendusermessageoutsideroom) and [sendServerMessage](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-sendservermessage) to send P2P messages or send messages to a server without joining the RTC room.

```Plain Text
   To log out, call [logout](#IRTCEngine-logout).
```


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|token |const char\* |Token is required during login for authentication.<br><br>&nbsp;<br><br>This Token is different from that required by calling joinRoom. You can assign any value even null to `roomId` to generate a login token. During developing and testing, you can use temporary tokens generated on the console. Deploy the token generating application on your server. |
|uid |const char\* |User ID<br><br>&nbsp;<br><br>User ID is unique within one appid. |


**Return Value**


* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for specific reasons.


**Notes**

You will receive [onLoginResult](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onloginresult) after calling this API and log in successfully. But remote users will not receive notification about that.

<span id="IRTCEngine-logout"></span>
### logout

```cpp
virtual int logout() = 0;
```


Log out of RTS server.

Calls this interface to log out, it is impossible to call methods related to out\-of\-room messages and end\-to\-server messages or receive related callbacks.

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* Before calling this interface to log out, you must call [login](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-login) to log in.

* After local users call this method to log out, they will receive the result of the [onLogout](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onlogout) callback notification, and remote users will not receive the notification.

    &nbsp;


<span id="updatelogintoken"></span>
### updateLoginToken

```cpp
virtual int updateLoginToken(const char* token) = 0;
```


Update the Token

Token used by the user to log in has a certain valid period. When the Token expires, you need to call this method to update the login Token information.

When calling the [login](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-login) method to log in, if an expired token is used, the login will fail and you will receive an [onLoginResult](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onloginresult) callback notification with an error code of kLoginErrorCodeInvalidToken. You need to reacquire the token and call this method to update the token.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|token |const char\* |Updated dynamic key |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* If the token is invalid and the login fails, call this method. After updating the token, the SDK will automatically log back in, and the user does not need to call the [login](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-login) method.

* Token expires, if you have successfully logged in, it will not be affected. An expired Token error will be notified to the user the next time you log in with an expired Token, or when you log in again due to a disconnection due to poor local network conditions.

    &nbsp;


<span id="setserverparams"></span>
### setServerParams

```cpp
virtual int setServerParams(
    const char* signature,
    const char* url
) = 0;
```


Set application server parameters

Client side calls [sendServerMessage](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-sendservermessage) or [sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-sendserverbinarymessage) Before sending a message to the application server, a valid signature and application server address must be set.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|signature |const char\* |Dynamic signature. The App server may use the signature to verify the source of messages.<br><br>&nbsp;<br><br>You need to define the signature yourself. It can be any non\-empty string. It is recommended to encode information such as UID into the signature.<br><br>&nbsp;<br><br>The signature will be sent to the address set through the "url" parameter in the form of a POST request. |
|url |const char\* |The address of the application server |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* The user must call [login](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-login) to log in before calling this interface.

* After calling this interface, the SDK will use [onServerParamsSetResult](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onserverparamssetresult) to return the corresponding result.

    &nbsp;


<span id="getpeeronlinestatus"></span>
### getPeerOnlineStatus

```cpp
virtual int getPeerOnlineStatus(const char* peer_user_id) = 0;
```


Query the login status of the opposite or local user

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|peer_user_id |const char\* |User ID to be queried |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* [login](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-login) must be called before this interface can be called.

* After calling this interface, the SDK notifies the query result using the [onGetPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-ongetpeeronlinestatus) callback.

* Before sending an out\-of\-room message, the user can know whether the peer user is logged in through this interface to decide whether to send a message. You can also check your login status through this interface.

    &nbsp;


<span id="sendusermessageoutsideroom"></span>
### sendUserMessageOutsideRoom

```cpp
virtual int64_t sendUserMessageOutsideRoom(
    const char* uid,
    const char* message,
    MessageConfig config = kMessageConfigReliableOrdered
) = 0;
```


Send a text message (P2P) to a specified user outside the room

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |const char\* |User ID of the message receiver |
|message |const char\* |Text message content sent. Message does not exceed 64 KB. |
|config |MessageConfig |Message type, see [MessageConfig](https://docs.byteplus.com/en/docs/12/docs-85519#MessageConfig). |


**Return Value**


* \> 0: Sent successfully, return the number of the sent message, increment from 1.


**Notes**


* Before calling this API, make sure you have enabled the [Advanced RTS functions](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode) in the RTC console.

> If this feature is enabled while the SDK is running, you must re\-initialize the engine for the configuration to take effect.


* You must call [login](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-login) to complete the login before you can send a message in a foreign text of the room.

* After the user calls this interface to send a text message, he will receive an [onUserMessageSendResultOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onusermessagesendresultoutsideroom) callback to know whether the message was successfully sent.

* If the text message is sent successfully, the user specified by uid receives the message via the [onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onusermessagereceivedoutsideroom) callback.

    &nbsp;


<span id="senduserbinarymessageoutsideroom"></span>
### sendUserBinaryMessageOutsideRoom

```cpp
virtual int64_t sendUserBinaryMessageOutsideRoom(
    const char* uid,
    int length,
    const uint8_t* message,
    MessageConfig config = kMessageConfigReliableOrdered
) = 0;
```


Send binary messages (P2P) to a specified user outside the room

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |const char\* |ID of the user receiving the message |
|length |int |Length of the binary string |
|message |const uint8_t\* |Content of the binary message sent. Message does not exceed 64 KB. |
|config |MessageConfig |Message type, see [MessageConfig](https://docs.byteplus.com/en/docs/12/docs-85519#MessageConfig). |


**Return Value**


* \> 0: sent successfully, return the number of the sent message, increment from 1.

* \-1: Sent failed due to empty message.


**Notes**


* Before calling this API, make sure you have enabled the [Advanced RTS functions](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode) in the RTC console.

> If this feature is enabled while the SDK is running, you must re\-initialize the engine for the configuration to take effect.


* [login](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-login) must be called before sending out\-of\-room binary messages.

* After the user calls this interface to send a binary message, he will receive an [onUserMessageSendResultOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onusermessagesendresultoutsideroom) callback to notify whether the message was sent successfully.

* If the binary message is sent successfully, the user specified by uid will receive the message through the [onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom) callback.

    &nbsp;


<span id="sendservermessage"></span>
### sendServerMessage

```cpp
virtual int64_t sendServerMessage(const char* message) = 0;
```


The client side sends a text message to the application server (P2Server)

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|message |const char\* |The content of the text message sent. The message does not exceed 64 KB. |


**Return Value**


* \> 0: Sent successfully, return the number of the sent message, increment from 1.


**Notes**


* Before calling this API, make sure you have enabled the [Advanced RTS functions](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode) in the RTC console.

> If this feature is enabled while the SDK is running, you must re\-initialize the engine for the configuration to take effect.


* Before sending a text message to the application server, you must first call [login](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-login) to complete the login, and then call [setServerParams](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setserverparams) Set up the application server.

* After calling this interface, you will receive an [onServerMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onservermessagesendresult) callback to inform the message sender whether the message was sent successfully.

* If the text message is sent successfully, the application server that previously called [setServerParams](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setserverparams) will receive the message.

    &nbsp;


<span id="sendserverbinarymessage"></span>
### sendServerBinaryMessage

```cpp
virtual int64_t sendServerBinaryMessage(
    int length,
    const uint8_t* message
) = 0;
```


Client side sends binary messages to the application server (P2Server)

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|length |int |Length of binary string |
|message |const uint8_t\* |Binary message content sent. Message does not exceed 64 KB. |


**Return Value**


* \> 0: sent successfully, return the number of the sent message, increment from 1.

* \-1: Sent failed due to empty message.


**Notes**


* Before calling this API, make sure you have enabled the [Advanced RTS functions](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode) in the RTC console.

> If this feature is enabled while the SDK is running, you must re\-initialize the engine for the configuration to take effect.


* Before sending a binary message to the application server, you must first call [login](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-login) to complete the login, and then call [setServerParams](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setserverparams) Set up the application server.

* After calling this interface, you will receive an [onServerMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onservermessagesendresult) callback to inform the message sender that the sending succeeded or failed.

* If the binary message is sent successfully, the application server that previously called [setServerParams](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setserverparams) will receive the message.

    &nbsp;


<span id="startnetworkdetection"></span>
### startNetworkDetection

```cpp
virtual int startNetworkDetection(
    bool is_test_uplink,
    int expected_uplink_bitrate,
    bool is_test_downlink,
    int expected_downlink_biterate
) = 0;
```


Pre\-call network detection

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|is_test_uplink |bool |Whether to detect uplink bandwidth |
|expected_uplink_bitrate |int |Expected uplink bandwidth, unit: kbps<br><br>Range: {0, [100\-10000]}, `0`: Auto, that RTC will set the highest bite rate. |
|is_test_downlink |bool |Whether to detect downlink bandwidth |
|expected_downlink_biterate |int |Expected downlink bandwidth, unit: kbps<br><br>Range: {0, [100\-10000]}, `0`: Auto, that RTC will set the highest bite rate. |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* After calling this interface, you will receive [onNetworkDetectionResult](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onnetworkdetectionresult) within 3s and every 2s thereafter notifying the probe result;

* If the probe stops, you will receive [onNetworkDetectionStopped](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onnetworkdetectionstopped) notify that probing has stopped.

    &nbsp;


<span id="stopnetworkdetection"></span>
### stopNetworkDetection

```cpp
virtual int stopNetworkDetection() = 0;
```


Stop pre\-call network probe

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* After calling this interface, you will receive [onNetworkDetectionStopped](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onnetworkdetectionstopped) notifying that the the probing has stopped.

    &nbsp;


<span id="stopscreenaudiocapture"></span>
### stopScreenAudioCapture

```cpp
virtual int stopScreenAudioCapture() = 0;
```


Stop RTC SDK's device audio recorder.

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* The call of this API takes effects only when you are using RTC SDK to record screen. You will get a warning by [onAudioDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onaudiodevicewarning) after calling this API when the video source is set to an external recorder.

* This API can only stop the screen capture by the RTC SDK. If the video source has been set to external recorder, the call of this API will fail with a warning message. You need to stop it in the external recorder.

* To start the device audio recording, call [startScreenAudioCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startscreenaudiocapture).

    &nbsp;


<span id="enableaudiopropertiesreport"></span>
### enableAudioPropertiesReport

```cpp
virtual int enableAudioPropertiesReport(const AudioPropertiesConfig& config) = 0;
```


Enable audio information prompts. After that, you will receive [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onlocalaudiopropertiesreport), [onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onremoteaudiopropertiesreport), and [onActiveSpeaker](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onactivespeaker).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|config |const AudioPropertiesConfig& |See [AudioPropertiesConfig](https://docs.byteplus.com/en/docs/12/docs-85519#AudioPropertiesConfig) |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details

    &nbsp;


<span id="setremoteaudioplaybackvolume"></span>
### setRemoteAudioPlaybackVolume

```cpp
virtual int setRemoteAudioPlaybackVolume(
    const char* stream_id,
    int volume
) = 0;
```


Set the audio volume of playing the received remote stream. You must join the room before calling the API. The validity of the setting is not associated with the publishing status of the stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of stream |
|volume |int |The ratio between the playing voilume of the original volume. The range is `[0, 400]` with overflow protection. The unit is %.<br><br>&nbsp;<br><br>For better audio quality, you are recommended to se the value to `[0, 100]`. |


**Return Value**

result


* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus).


**Notes**

Assume that a remote user A is always within the scope of the adjusted target users:


* When this API is used together with [setRemoteRoomAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-setremoteroomaudioplaybackvolume), the volume of local listening user A is the volume set by the API called later;

* When this API is used together with the [setPlaybackVolume](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setplaybackvolume), the volume of local listening user A will be the superposition of the two set volume effects.

* When you call this API to set the remote stream volume, if the remote user leaves the room, the setting will be invalid.

    &nbsp;


<span id="enablevocalinstrumentbalance"></span>
### enableVocalInstrumentBalance

```cpp
virtual int enableVocalInstrumentBalance(bool enable) = 0;
```


Enables/disables the loudness equalization function.

If you call this API with the parameter set to True, the loudness of user's voice will be adjusted to \-16lufs. If then you also call setAudioMixingLoudness and import the original loudness of the audio data used in audio mixing, the loudness will be adjusted to \-20lufs when the audio data starts to play.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|enable |bool |Whether to enable loudness equalization function:<br><br><br>&nbsp;<br><br>* true: Yes<br><br>* false: No |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**

You must call this API before starting to play the audio file with [start](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-start).

<span id="IRTCEngine-enableplaybackducking"></span>
### enablePlaybackDucking

```cpp
virtual int enablePlaybackDucking(bool enable) = 0;
```


Enables/disables the playback ducking function. This function is usually used in scenarios where short videos or music will be played simultaneously during RTC calls.

With the function on, if remote voice is detected, the local media volume of RTC will be lowered to ensure the clarity of the remote voice. If remote voice disappears, the local media volume of RTC restores.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|enable |bool |Whether to enable playback ducking:<br><br><br>&nbsp;<br><br>* true: Yes<br><br>* false: No |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details

    &nbsp;


<span id="registerlocalencodedvideoframeobserver"></span>
### registerLocalEncodedVideoFrameObserver

```cpp
virtual int registerLocalEncodedVideoFrameObserver(ILocalEncodedVideoFrameObserver* observer) = 0;
```


Register a local video frame observer.

This method applys to both internal capturing and custom capturing.

After calling this API, SDK triggers [onLocalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85517#ILocalEncodedVideoFrameObserver-onlocalencodedvideoframe) whenever a video frame is captured.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|observer |ILocalEncodedVideoFrameObserver\* |Local video frame observer. See [ILocalEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-85517#ILocalEncodedVideoFrameObserver). You can cancel the registration by setting it to `nullptr`. |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**

You can call this API before or after entering the RTC room. Calling this API before entering the room ensures that video frames are monitored and callbacks are triggered as early as possible.

<span id="IRTCEngine-registerremoteencodedvideoframeobserver"></span>
### registerRemoteEncodedVideoFrameObserver

```cpp
virtual int registerRemoteEncodedVideoFrameObserver(IRemoteEncodedVideoFrameObserver* observer) = 0;
```


Video data callback after registering remote encoding.

After registration, when the SDK detects a remote encoded video frame, it will trigger the [onRemoteEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IRemoteEncodedVideoFrameObserver-onremoteencodedvideoframe) callback

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|observer |IRemoteEncodedVideoFrameObserver\* |Remote encoded video data monitor. See [IRemoteEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-85517#IRemoteEncodedVideoFrameObserver) |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* See [Custom Video Encoding and Decoding](https://docs.byteplus.com/byteplus-rtc/docs/82921#custom-video-decoding) for more details about custom video decoding.

* This method applys to manual subscription mode and can be called either before or after entering the Room. It is recommended to call it before entering the room.

* The engine needs to be unregistered before it is destroyed. Call this method to set the parameter to nullptr.

    &nbsp;


<span id="setexternalvideoencodereventhandler"></span>
### setExternalVideoEncoderEventHandler

```cpp
virtual int setExternalVideoEncoderEventHandler(IExternalVideoEncoderEventHandler* encoder_handler) = 0;
```


Register custom encoded frame push event callback

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|encoder_handler |IExternalVideoEncoderEventHandler\* |Custom encoded frame callback class. See [IExternalVideoEncoderEventHandler](https://docs.byteplus.com/en/docs/12/docs-85517#IExternalVideoEncoderEventHandler) |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* This method needs to be called before entering the room.

* The engine needs to be unregistered before it is destroyed. Call this method to set the parameter to nullptr.

    &nbsp;


<span id="pushexternalencodedvideoframe"></span>
### pushExternalEncodedVideoFrame

```cpp
virtual int pushExternalEncodedVideoFrame(
    int video_index,
    IEncodedVideoFrame* video_stream
) = 0;
```


Push custom encoded video stream

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|video_index |int |The corresponding encoded stream subscript, starting from 0, if you call [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setvideoencoderconfig) to set multiple streams, the number here must be consistent with it |
|video_stream |IEncodedVideoFrame\* |Encoded stream video frame information. See [IEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IEncodedVideoFrame). |


**Return Value**

API call result:


* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for specific reasons.


**Notes**


* Currently, only video frames in H264 and ByteVC1 formats are supported, and the video stream protocol must be in an Annex B format.

* This function runs within the user calling thread

* Before pushing a custom encoded video frame, you must call [setVideoSourceType](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setvideosourcetype) to switch the video input source to the custom encoded video source.

    &nbsp;


<span id="setvideodecoderconfig"></span>
### setVideoDecoderConfig

```cpp
virtual int setVideoDecoderConfig(
    const char* stream_id,
    VideoDecoderConfig config
) = 0;
```


Before subscribing to the remote video stream, set the remote video data decoding method

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |The remote stream ID |
|config |VideoDecoderConfig |Video decoding method. See [VideoDecoderConfig](https://docs.byteplus.com/en/docs/12/docs-85519#VideoDecoderConfig). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* When you want to custom decode a remote stream, you need to call [registerRemoteEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-registerremoteencodedvideoframeobserver) to register the remote video stream monitor, and then call the interface to set the decoding method to custom decoding. The monitored video data will be called back through [onRemoteEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IRemoteEncodedVideoFrameObserver-onremoteencodedvideoframe).

* Since version 3.56, for automatic subscription, you can set the `RoomId` and `UserId` of `key` as `nullptr`. In this case, the decoding settings set by calling the API applies to all remote main streams or screen sharing streams based on the `StreamIndex` value of `key`.

    &nbsp;


<span id="requestremotevideokeyframe"></span>
### requestRemoteVideoKeyFrame

```cpp
virtual int requestRemoteVideoKeyFrame(const char* stream_id) = 0;
```


After subscribing to the remote video stream, request the key frame to the remote

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |The remote stream ID |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* This method is only suitable for manual subscription mode and is used after successful subscription to the remote flow.

* This method is suitable for calling [setVideoDecoderConfig](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setvideodecoderconfig) to turn on the custom decoding function, and the custom decoding fails

    &nbsp;


<span id="sendstreamsyncinfo"></span>
### sendStreamSyncInfo

```cpp
virtual int sendStreamSyncInfo(
    const uint8_t* data,
    int32_t length,
    const StreamSyncInfoConfig& config
) = 0;
```


Send audio stream synchronization information. The message is sent to the remote end through the audio stream and synchronized with the audio stream. After the interface is successfully called, the remote user will receive a [onStreamSyncInfoReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onstreamsyncinforeceived) callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|data |const uint8_t\* |Message content. |
|length |int32_t |Message length. Message length must be [1,16] bytes. |
|config |const StreamSyncInfoConfig& |For configuration of media stream information synchronization. See [StreamSyncInfoConfig](https://docs.byteplus.com/en/docs/12/docs-85519#StreamSyncInfoConfig). |


**Return Value**


* \> = 0: Message sent successfully. Returns the number of successful sends.

* \-1: Message sending failed. Message length greater than 16 bytes.

* \-2: Message sending failed. The content of the incoming message is empty.

* \-3: Message sending failed. This screen stream was not published when the message was synchronized through the screen stream.

* \-4: Message sending failed. This audio stream is not yet published when you synchronize messages with an audio stream captured by a microphone or custom device, as described in [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-85518#ErrorCode).


**Notes**


* Regarding the frequency, we recommend no more than 50 calls per second.

* When using `kRoomProfileTypeInteractivePodcast` as room profile, the data will be delivered. For other coom profiles, the data may be lost when the local user is muted.

    &nbsp;


<span id="setlocalvoicepitch"></span>
### setLocalVoicePitch

```cpp
virtual int setLocalVoicePitch(int pitch) = 0;
```


Change local voice to a different key, mostly used in Karaoke scenarios.

You can adjust the pitch of local voice such as ascending or descending with this method.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|pitch |int |The value that is higher or lower than the original local voice within a range from \-12 to 12. The default value is 0, i.e. No adjustment is made.<br><br>&nbsp;<br><br>The difference in pitch between two adjacent values within the value range is a semitone, with positive values indicating an ascending tone and negative values indicating a descending tone, and the larger the absolute value set, the more the pitch is raised or lowered.<br><br>&nbsp;<br><br>Out of the value range, the setting fails and triggers [onWarning](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onwarning) callback, indicating `WARNING_CODE_SET_SCREEN_STREAM_INVALID_VOICE_PITCH` for invalid value setting with [WarningCode](https://docs.byteplus.com/en/docs/12/docs-85518#WarningCode). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details

    &nbsp;


<span id="setvideowatermark"></span>
### setVideoWatermark

```cpp
virtual int setVideoWatermark(
    const char* image_path,
    RTCWatermarkConfig config
) = 0;
```


Adds watermark to designated video stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|image_path |const char\* |The absolute path of the watermark image. The path should be less than 512 bytes.<br><br>&nbsp;<br><br>The watermark image should be in PNG or JPG format. |
|config |RTCWatermarkConfig |Watermark configurations. See [RTCWatermarkConfig](https://docs.byteplus.com/en/docs/12/docs-85519#RTCWatermarkConfig). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* Call [clearVideoWatermark](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-clearvideowatermark) to remove the watermark from the designated video stream.

* You can only add one watermark to one video stream. The newly added watermark replaces the previous one. You can call this API multiple times to add watermarks to different streams.

* If you mirror the preview, or the preview and the published stream, the watermark will also be mirrored locally, but the published watermark will not be mirrored.

* When you enable simulcast mode, the watermark will be added to all video streams, and it will be scaled down to smaller encoding configurations accordingly.

    &nbsp;


<span id="clearvideowatermark"></span>
### clearVideoWatermark

```cpp
virtual int clearVideoWatermark() = 0;
```


Removes video watermark from designated video stream.

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details

    &nbsp;


<span id="setdummycaptureimagepath"></span>
### setDummyCaptureImagePath

```cpp
virtual int setDummyCaptureImagePath(const char* file_path) = 0;
```


Set an alternative image when the local internal video capture is not enabled.

When you call `stopVideoCapture`, an alternative image will be pushed. You can set the path to null or open the camera to stop publishing the image.

You can repeatedly call this API to update the image.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|file_path |const char\* |Set the path of the static image.<br><br>&nbsp;<br><br>You can use the absolute path (file://xxx). The maximum size for the path is 512 bytes.<br><br>&nbsp;<br><br>You can upload a .JPG, .JPEG, .PNG, or .BMP file.<br><br>&nbsp;<br><br>When the aspect ratio of the image is inconsistent with the video encoder configuration, keep the aspect\-ratio to scale the image and the crop the longer sides. The framerate and the bitrate are consistent with the video encoder configuration. |


**Return Value**


* 0: Success.

* \-2: Failure. Ensure that the file_path is valid.

* \-12: This method is not available in the Audio SDK.


**Notes**


* The API is only effective when publishing an internally captured video.

* You cannot locally preview the image.

* You can call this API before and after joining an RTC room. In the multi\-room mode, the image can be only displayed in the room you publish the stream.

* You cannot apply effects like filters and mirroring to the image, while you can watermark the image.

* The image is not effective for a screen\-sharing stream.

* When you enable the simulcast mode, the image will be added to all video streams, and it will be proportionally scaled down to smaller encoding configurations.

    &nbsp;


<span id="startcloudproxy"></span>
### startCloudProxy

```cpp
virtual int startCloudProxy(const CloudProxyConfiguration& configuration) = 0;
```


Start cloud proxy

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|configuration |const CloudProxyConfiguration& |cloud proxy informarion list. See [CloudProxyConfiguration](https://docs.byteplus.com/en/docs/12/docs-85519#CloudProxyConfiguration). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* Call this API before joining the room.

* Start pre\-call network detection after starting cloud proxy.

* After starting cloud proxy and connects the cloud proxy server successfully, receives [onCloudProxyConnected](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-oncloudproxyconnected).

* To stop cloud proxy, call [stopCloudProxy](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-stopcloudproxy).

    &nbsp;


<span id="stopcloudproxy"></span>
### stopCloudProxy

```cpp
virtual int stopCloudProxy() = 0;
```


Stop cloud proxy

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**

To start cloud proxy, call [startCloudProxy](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-startcloudproxy).

<span id="IRTCEngine-setlocalproxy"></span>
### setLocalProxy

```cpp
virtual int setLocalProxy(
    const LocalProxyConfiguration* configurations,
    int configuration_num
) = 0;
```


Sets local proxy.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|configurations |const LocalProxyConfiguration\* |Local proxy configurations. Refer to [LocalProxyConfiguration](https://docs.byteplus.com/en/docs/12/docs-85519#LocalProxyConfiguration).<br><br>&nbsp;<br><br>You can set both Http tunnel and Socks5 as your local proxies, or only set one of them based on your needs. If you set both Http tunnel and Socks5 as your local proxies, then media traffic and signaling are routed through Socks5 proxy and Http requests through Http tunnel proxy. If you set either Http tunnel or Socks5 as your local proxy, then media traffic, signaling and Http requests are all routed through the proxy you chose.<br><br>&nbsp;<br><br>If you want to remove the existing local proxy configurations, you can call this API with the parameter set to null. |
|configuration_num |int |The number of local proxy configurations. |


**Notes**


* You must call this API before joining the room.

* After calling this API, you will receive [onLocalProxyStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onlocalproxystatechanged) callback that informs you of the states of local proxy connection.

    &nbsp;


<span id="setlowlightadjusted"></span>
### setLowLightAdjusted

```cpp
virtual int setLowLightAdjusted(VideoEnhancementMode mode) = 0;
```


> Available since 3.57


Sets the video lowlight enhancement mode.

It can significantly improve image quality in scenarios with insufficient light, contrast lighting, or backlit situations.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mode |VideoEnhancementMode |It defaults to Disable. Refer to [VideoEnhancementMode](https://docs.byteplus.com/en/docs/12/docs-85519#VideoEnhancementMode) for more details. |


**Return Value**


* 0: Success. After you call this method, it will take action immediately. But it may require some time for downloads and detection processes before you can see the enhancement.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* Turning on this mode will impact device performance. This feature should be activated only when required and the device performance is adequate.

* Functionality applies to videos captured by the internal module as well as those from custom collections.

    &nbsp;


<span id="getwtnstream"></span>
### getWTNStream

```cpp
virtual IWTNStream* getWTNStream() = 0;
```


> Available since 3.60


Gets the WTN stream object.

You can use this method to get the WTN stream object to implement custom video rendering and processing.

After calling this method, you can call [subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/25049#IWTNStream-subscribewtnvideostream) or [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/25049#IWTNStream-subscribewtnaudiostream) to subscribe to the specified WTN stream.

**Return Value**

IWTNStream：WTN stream object. See [IWTNStream](https://docs.byteplus.com/en/docs/12/25049#IWTNStream).

<span id="IRTCEngine-updateremotestreamvideocanvas"></span>
### updateRemoteStreamVideoCanvas

```cpp
virtual int updateRemoteStreamVideoCanvas(
    const char* stream_id,
    const enum RenderMode render_mode,
    const uint32_t background_color
) = 0;
```


> Deprecated since 3.56, and will be deleted in 3.62.


Modifies remote video frame rendering settings, including render mode and background color.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of stream |
|render_mode |const enum RenderMode |See [RenderMode](https://docs.byteplus.com/en/docs/12/docs-85519#RenderMode). |
|background_color |const uint32_t |See [VideoCanvas](https://docs.byteplus.com/en/docs/12/docs-85519#VideoCanvas).background_color. |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**

Calling this API during remote video rendering will be effective immediately.

<span id="IRTCEngine-setlocalvideosink"></span>
### setLocalVideoSink

```cpp
virtual int setLocalVideoSink(
    IVideoSink* video_sink,
    IVideoSink::PixelFormat required_format
) = 0;
```


> Deprecated since 3.60, use [setLocalVideoSink](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setlocalvideosink) instead.


Binds the local video stream to a custom renderer.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|video_sink |IVideoSink\* |Custom video renderer. See [IVideoSink](https://docs.byteplus.com/en/docs/12/docs-85519#IVideoSink). |
|required_format |IVideoSink::PixelFormat |Video frame encoding format that applies to custom rendering. See [PixelFormat](https://docs.byteplus.com/en/docs/12/docs-85519#PixelFormat). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* RTC SDK uses its own renderer (internal renderer) for video rendering by default.

* Joining or leaving the room will not affect the binding state.

* If you need to unbind the video stream from the custom renderer, you must set video_sink to `null`.

* You should call this API before joining the room, and after receiving [onFirstLocalVideoFrameCaptured](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onfirstlocalvideoframecaptured) which reports that the first local video frame has been successfully captured.

* This method gets video frames that have undergone preprocessing.

    &nbsp;


<span id="setremotevideosink"></span>
### setRemoteVideoSink

```cpp
virtual int setRemoteVideoSink(
    const char* stream_id,
    IVideoSink* video_sink,
    IVideoSink::PixelFormat required_format
) = 0;
```


> Deprecated since 3.57, use [setRemoteVideoRender](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setremotevideosink) instead.


Binds the remote video stream to a custom renderer.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of stream |
|video_sink |IVideoSink\* |Custom video renderer. See [IVideoSink](https://docs.byteplus.com/en/docs/12/docs-85519#IVideoSink). |
|required_format |IVideoSink::PixelFormat |Encoding format which applies to the custom renderer. See [PixelFormat](https://docs.byteplus.com/en/docs/12/docs-85519#PixelFormat). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* RTC SDK uses its own renderer (internal renderer) for video rendering by default.

* Joining or leaving the room will not affect the binding state.

* This API can be called before and after entering the room. To call before entering the room, you need to get the remote stream information before joining the room; if you cannot get the remote stream information in advance, you can call the API after joining the room and getting the remote stream information via [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserpublishstreamvideo).

* If you need to unbind, you must set videoSink to null.

* This method gets video frames that have undergone processing.

    &nbsp;


<span id="startscreenaudiocapture"></span>
### startScreenAudioCapture

```cpp
virtual int startScreenAudioCapture() = 0;
```


> Deprecated on Windows since 3.59, use `startScreenAudioCapture` with the "device_id" parameter as a replacement.


When sharing the screen, start using RTC SDK internal collection method to collect screen audio

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* The call of this API takes effects only when you are using RTC SDK to record screen. You will get a warning by [onAudioDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onaudiodevicewarning) after calling this API when the video source is set to an external recorder.

* After collection, you also need to call [publishStreamAudio](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-publishstreamaudio) to collect the screen audio Push to the far end.

* To turn off screen audio internal capture, call [stopScreenAudioCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-stopscreenaudiocapture).

    &nbsp;


<span id="irtsroom"></span>
# IRTSRoom

```cpp
class bytertc::IRTSRoom
```


RTS room interface

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual void |[destroy](https://docs.byteplus.com/en/docs/12/25049#IRTSRoom-destroy) |
|virtual int |[leaveRoom](https://docs.byteplus.com/en/docs/12/25049#IRTSRoom-leaveroom) |
|virtual int |[setRTSRoomEventHandler](https://docs.byteplus.com/en/docs/12/25049#IRTSRoom-setrtsroomeventhandler) |
|virtual int64_t |[sendRoomMessage](https://docs.byteplus.com/en/docs/12/25049#IRTSRoom-sendroommessage) |
|virtual int64_t |[sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/25049#IRTSRoom-sendroombinarymessage) |
|virtual int |[joinRTSRoom](https://docs.byteplus.com/en/docs/12/25049#IRTSRoom-joinrtsroom) |
|virtual int |[updateToken](https://docs.byteplus.com/en/docs/12/25049#IRTSRoom-updatetoken) |
|virtual int64_t |[sendUserMessage](https://docs.byteplus.com/en/docs/12/25049#IRTSRoom-sendusermessage) |
|virtual int64_t |[sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/25049#IRTSRoom-senduserbinarymessage) |


<span id="instructions"></span>
## Instructions

<span id="IRTSRoom-destroy"></span>
### destroy

```cpp
virtual void destroy() = 0;
```


Leave and destroy the RTS room instance created by calling [createRTSRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-creatertsroom).

<span id="IRTSRoom-leaveroom"></span>
### leaveRoom

```cpp
virtual int leaveRoom() = 0;
```


Leave the RTC or RTS room.

The user calls this method to leave the room, end the call process, and release all call\-related resources.

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* This method is an asynchronous operation and does not really exit the room when the call returns. After you actually exit the room, you will receive a callback notification from [onLeaveRoom](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onleaveroom) locally.

* After the visible user leaves the room, other users in the room will receive an [onUserLeave](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onuserleave) callback notification.

* If the engine is destroyed immediately after this method is called, the SDK will not be able to trigger the [onLeaveRoom](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onleaveroom) callback.

* After calling the [joinRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-joinroom) or [joinRTSRoom](https://docs.byteplus.com/en/docs/12/25049#IRTSRoom-joinrtsroom) method to join the room, you must call this method to leave the room, otherwise you cannot enter the next room. This method can be called regardless of whether it is currently in the room. Repeated calls to this method have no negative impact.


<span id="IRTSRoom-setrtsroomeventhandler"></span>
### setRTSRoomEventHandler

```cpp
virtual int setRTSRoomEventHandler(IRTSRoomEventHandler* room_event_handler) = 0;
```


Set the event handle of the [IRTSRoom](https://docs.byteplus.com/en/docs/12/25049#IRTSRoom) object.

You can listen for callback events for the room corresponding to this [IRTSRoom](https://docs.byteplus.com/en/docs/12/25049#IRTSRoom) object by setting the event handle.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|room_event_handler |IRTSRoomEventHandler\* |Callback processor. See [IRTSRoomEventHandler](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details

    &nbsp;


<span id="sendroommessage"></span>
### sendRoomMessage

```cpp
virtual int64_t sendRoomMessage(const char* message) = 0;
```


Send broadcast messages to all other users in the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|message |const char\* |The broadcast message sent by the user. The default size of a single message package is 1 KB. For larger message transmission (up to 64 KB), you need to [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode). **Note**: If you enable Advanced RTS functions while the SDK is running, you must re\-initialize the engine for the configuration to take effect. |


**Return Value**

The number of the message sent this time is incremented from 1.

**Notes**


* Before sending in\-room binary messages, you must call [joinRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-joinroom) to join the room.

* After calling this function, you get an [onRoomMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onroommessagesendresult) callback.

* Other users in the same room receive an [onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onroommessagereceived) callback.

    &nbsp;


<span id="sendroombinarymessage"></span>
### sendRoomBinaryMessage

```cpp
virtual int64_t sendRoomBinaryMessage(
    int size,
    const uint8_t* message
) = 0;
```


Send broadcast messages to all other users in the room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|size |int |The length of the binary message sent |
|message |const uint8_t\* |The binary broadcast message sent by the user. The default size of a single message package is 1 KB. For larger message transmission (up to 64 KB), you need to [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode). **Note**: If you enable Advanced RTS functions while the SDK is running, you must re\-initialize the engine for the configuration to take effect. |


**Return Value**

The number of the message sent this time is incremented from 1.

**Notes**


* Before sending in\-room binary messages, you must call [joinRTSRoom](https://docs.byteplus.com/en/docs/12/25049#IRTSRoom-joinrtsroom) to join the room.

* After calling this function, you get an [onRoomMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onroommessagesendresult) callback.

* Other users in the same room receive an [onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onroombinarymessagereceived) callback.

    &nbsp;


<span id="joinrtsroom"></span>
### joinRTSRoom

```cpp
virtual int joinRTSRoom(
    const char* token,
    const UserInfo& user_info
) = 0;
```


Joins an RTS room.

Users in the same room can talk to each other.

Repeated calls after entering the room are invalid. The user must call `leaveRoom` to exit the current room before joining the next room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|token |const char\* |Token is required during login for authentication.<br><br>&nbsp;<br><br>This Token is different from that required by calling joinRoom. You can assign any value even null to `roomId` to generate a login token. During developing and testing, you can use temporary tokens generated on the console. Deploy the token generating application on your server. |
|user_info |const UserInfo& |User information, see [UserInfo](https://docs.byteplus.com/en/docs/12/docs-85519#UserInfo). |


**Return Value**


* 0: Success

* \-1: token / user_info.uid contains invalid parameters.

* \-2: Already in the room.


**Notes**


* In the same room with the same App ID, the user ID of each user must be unique. If two users have the same user ID, the user who entered the room later will kick the user who entered the room out of the room, and the user who entered the room will receive the [OnError](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onerror) callback notification. For the error type. See kErrorCodeDuplicateLogin in [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-85518#ErrorCode).

* Local users will receive callback notification after calling this method to join the room successfully.

* After the user successfully joins the room, the SDK may lose connection to the server in case of poor local network conditions, and the SDK will automatically reconnect at this time. After a successful reconnection, you will receive a local callback notification. If the user is set to visiable, the remote user will receive [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onuserjoined) callback notification.

    &nbsp;


<span id="updatetoken"></span>
### updateToken

```cpp
virtual int updateToken(const char* token) = 0;
```


Update Token.

You must call this API to update token to ensure the RTC call to continue when you receive [onTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-ontokenwillexpire), [onPublishPrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onpublishprivilegetokenwillexpire), or [onSubscribePrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onsubscribeprivilegetokenwillexpire).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|token |const char\* |Valid token.<br><br>&nbsp;<br><br>If the Token is invalid, you will receive [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onroomstatechanged) with the error code of `-1010`. |


**Return Value**

API call result:


* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for specific reasons.


**Notes**


* In versions before 3.50, the publish and subscribe privileges contained in the Token are reserved parameters with no actual control permissions. In version 3.50 and later, the publish/subscribe privileges will be effective for whitelisted users. Please contact the technical support team to include you in the whitelist if you need this function.

* Do not call both [updateToken](https://docs.byteplus.com/en/docs/12/25049#IRTSRoom-updatetoken) and [joinRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-joinroom) to update the Token. If you fail to join the room or have been removed from the room due to an expired or invalid Token, call [joinRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-joinroom) with a valid token to rejoin the room.

    &nbsp;


<span id="sendusermessage"></span>
### sendUserMessage

```cpp
virtual int64_t sendUserMessage(
    const char* uid,
    const char* message,
    MessageConfig config = kMessageConfigReliableOrdered
) = 0;
```


Send a text message (P2P) to the specified user in the room

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |const char\* |User ID of the message receiver |
|message |const char\* |Text message content sent. The default size of a single message package is 1 KB. For larger message transmission (up to 64 KB), you need to [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode). **Note**: If you enable Advanced RTS functions while the SDK is running, you must re\-initialize the engine for the configuration to take effect. |
|config |MessageConfig |Message type, see [MessageConfig](https://docs.byteplus.com/en/docs/12/docs-85519#MessageConfig). |


**Return Value**

The number of the message sent this time is incremented from 1.

**Notes**


* Before sending an in\-room text message, you must call [joinRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-joinroom) or [joinRTSRoom](https://docs.byteplus.com/en/docs/12/25049#IRTSRoom-joinrtsroom) to join the room.

* After calling this function, you will receive an [onUserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onusermessagesendresult) callback to notify the message sender that the sending was successful or failed;

* If the text message is sent successfully, the user specified by uid will receive [onUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onusermessagereceived) callback.

    &nbsp;


<span id="senduserbinarymessage"></span>
### sendUserBinaryMessage

```cpp
virtual int64_t sendUserBinaryMessage(
    const char* uid,
    int length,
    const uint8_t* message,
    MessageConfig config = kMessageConfigReliableOrdered
) = 0;
```


Sends a binary message (P2P) to the specified user in the room

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|uid |const char\* |User ID of the message receiver |
|length |int |The length of the binary string. |
|message |const uint8_t\* |The content of the binary message. The default size of a single message package is 1 KB. For larger message transmission (up to 64 KB), you need to [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode). **Note**: If you enable Advanced RTS functions while the SDK is running, you must re\-initialize the engine for the configuration to take effect. |
|config |MessageConfig |Message type, see [MessageConfig](https://docs.byteplus.com/en/docs/12/docs-85519#MessageConfig). |


**Return Value**

Serial number of the message, starting form 1.

**Notes**


* Before sending in\-room binary messages, you must call [joinRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-joinroom) or [joinRTSRoom](https://docs.byteplus.com/en/docs/12/25049#IRTSRoom-joinrtsroom) to join the room.

* After calling this function, you will receive an [onUserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onusermessagesendresult) callback to notify the sender of the success or failure of the message;

* If the binary message is sent successfully, the user specified by uid will receive the [onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onuserbinarymessagereceived) callback.

    &nbsp;


<span id="iaudiodevicecollection"></span>
# IAudioDeviceCollection

```cpp
class bytertc::IAudioDeviceCollection
```


Audio equipment related information

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual int |[getCount](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceCollection-getcount) |
|virtual int |[getDevice](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceCollection-getdevice) |
|virtual void |[release](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceCollection-release) |
|virtual int |[getDevice](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceCollection-getdevice-2) |


<span id="instructions"></span>
## Instructions

<span id="IAudioDeviceCollection-getcount"></span>
### getCount

```cpp
virtual int getCount() override {return 0;};
```


Get the number of audio & video devices in the current system

**Return Value**

Number of audio devices

<span id="IAudioDeviceCollection-getdevice"></span>
### getDevice

```cpp
virtual int getDevice(
    int index,
    char device_name[MAX_DEVICE_ID_LENGTH],
    char device_id[MAX_DEVICE_ID_LENGTH]
) override {return 0;};
```


According to the index number, get device information

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|index |int |Device index number, starting from 0, note that it must be less than the return value of [getCount](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceCollection-getcount). |
|device_name |char[MAX_DEVICE_ID_LENGTH] |Device name |
|device_id |char[MAX_DEVICE_ID_LENGTH] |Device ID |


**Return Value**


* 0: Success.

   +! 0: failure

    &nbsp;


<span id="release"></span>
### release

```cpp
virtual void release()override {};
```


Releases the resources occupied by the current [IAudioDeviceCollection](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceCollection) object.

**Notes**

This method should be called to release related resources when you do not need to return a list of audio device related information.

<span id="IAudioDeviceCollection-getdevice-2"></span>
### getDevice

```cpp
virtual int getDevice(
    int index,
    AudioDeviceInfo* audio_device_info
) = 0;
protected:
```


Get the information of the specific audio device. You can get the device information by index, device info (ID, product ID, etc.).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|index |int |Device index number, starting from 0, note that it must be less than the return value of [getCount](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceCollection-getcount). |
|audio_device_info |AudioDeviceInfo\* |device info. Refer to [AudioDeviceInfo](https://docs.byteplus.com/en/docs/12/docs-85519#AudioDeviceInfo) for details. |


**Return Value**


* 0: Success.

   +! 0: failure

    &nbsp;


<span id="iscreencapturesourcelist"></span>
# IScreenCaptureSourceList

```cpp
class bytertc::IScreenCaptureSourceList
```


Information list of the screen\-sharing objects

Calling [release](https://docs.byteplus.com/en/docs/12/25049#IScreenCaptureSourceList-release) will release all the objects related to this class.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual int32_t |[getCount](https://docs.byteplus.com/en/docs/12/25049#IScreenCaptureSourceList-getcount) |
|virtual ScreenCaptureSourceInfo |[getSourceInfo](https://docs.byteplus.com/en/docs/12/25049#IScreenCaptureSourceList-getsourceinfo) |
|virtual void |[release](https://docs.byteplus.com/en/docs/12/25049#IScreenCaptureSourceList-release) |


<span id="instructions"></span>
## Instructions

<span id="IScreenCaptureSourceList-getcount"></span>
### getCount

```cpp
virtual int32_t getCount() = 0;
```


Get the length of the list

**Return Value**

Number of the items in the list

<span id="IScreenCaptureSourceList-getsourceinfo"></span>
### getSourceInfo

```cpp
virtual ScreenCaptureSourceInfo getSourceInfo(int32_t index) = 0;
```


According to the index, get the elements in the screen share list

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|index |int32_t |Index number |


**Return Value**

Screen source item. Refer to [ScreenCaptureSourceInfo](https://docs.byteplus.com/en/docs/12/docs-85519#ScreenCaptureSourceInfo) for more details.

<span id="IScreenCaptureSourceList-release"></span>
### release

```cpp
virtual void release() = 0;
```


If you are finished with the [IScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/25049#IScreenCaptureSourceList), call this API to destruct it and release the memory.

<span id="IVideoDeviceCollection"></span>
# IVideoDeviceCollection

```cpp
class bytertc::IVideoDeviceCollection
```


Video equipment related information

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual int |[getCount](https://docs.byteplus.com/en/docs/12/25049#IVideoDeviceCollection-getcount) |
|virtual int |[getDevice](https://docs.byteplus.com/en/docs/12/25049#IVideoDeviceCollection-getdevice) |
|virtual void |[release](https://docs.byteplus.com/en/docs/12/25049#IVideoDeviceCollection-release) |
|virtual int |[getDevice](https://docs.byteplus.com/en/docs/12/25049#IVideoDeviceCollection-getdevice-2) |


<span id="instructions"></span>
## Instructions

<span id="IVideoDeviceCollection-getcount"></span>
### getCount

```cpp
virtual int getCount() override {return 0;};
```


Get the number of video devices in the current system

**Return Value**

Number of video devices

<span id="IVideoDeviceCollection-getdevice"></span>
### getDevice

```cpp
virtual int getDevice(
    int index,
    char device_name[MAX_DEVICE_ID_LENGTH],
    char device_id[MAX_DEVICE_ID_LENGTH]
) override {return 0;};
```


Get the information of the specific video device. You can get the device information by index, device name, or device ID.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|index |int |Device index number, starting from 0, note that it must be less than the return value of [getCount](https://docs.byteplus.com/en/docs/12/25049#IVideoDeviceCollection-getcount). |
|device_name |char[MAX_DEVICE_ID_LENGTH] |device name |
|device_id |char[MAX_DEVICE_ID_LENGTH] |device ID |


**Return Value**


* 0: Success.

   +! 0: failure

    &nbsp;


<span id="release"></span>
### release

```cpp
virtual void release()override {};
```


Releases the resources occupied by the current [IVideoDeviceCollection](https://docs.byteplus.com/en/docs/12/25049#IVideoDeviceCollection) object.

**Notes**

This method should be called to release related resources when you do not need to return a list of video device related information.

<span id="IVideoDeviceCollection-getdevice-2"></span>
### getDevice

```cpp
virtual int getDevice(
    int index,
    VideoDeviceInfo* video_device_info
) = 0;
protected:
```


Get the information of the specific video device. You can get the device information by index, device info (ID, product ID, etc.).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|index |int |Device index, starting from 0. It must be less than the return value of [getCount](https://docs.byteplus.com/en/docs/12/25049#IVideoDeviceCollection-getcount). |
|video_device_info |VideoDeviceInfo\* |Device information |


**Return Value**


* 0: Success.

   +! 0: failure

    &nbsp;


<span id="iwtnstream"></span>
# IWTNStream

```cpp
class bytertc::IWTNStream
```


WTN stream process

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual |[~IWTNStream](https://docs.byteplus.com/en/docs/12/25049#IWTNStream-~iwtnstream) |
|virtual int |[subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/25049#IWTNStream-subscribewtnvideostream) |
|virtual int |[subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/25049#IWTNStream-subscribewtnaudiostream) |
|virtual int |[setWTNRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/25049#IWTNStream-setwtnremotevideocanvas) |
|virtual int |[setWTNRemoteVideoSink](https://docs.byteplus.com/en/docs/12/25049#IWTNStream-setwtnremotevideosink) |
|virtual int |[setWTNRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/25049#IWTNStream-setwtnremoteaudioplaybackvolume) |
|virtual int |[setWTNStreamEventHandler](https://docs.byteplus.com/en/docs/12/25049#IWTNStream-setwtnstreameventhandler) |


<span id="instructions"></span>
## Instructions

<span id="IWTNStream-~iwtnstream"></span>
### ~IWTNStream

```cpp
virtual ~IWTNStream() = default;
```


<span id="IWTNStream-subscribewtnvideostream"></span>
### subscribeWTNVideoStream

```cpp
virtual int subscribeWTNVideoStream(
    const char* stream_id,
    bool subscribe
) = 0;
```


> Available since 3.60. Since version 3.60, this interface replaces the `startPlayPublicStream` and `stopPlayPublicStream` methods for subscribing to and unsubscribing from WTN video streams. If you are using these methods, please migrate to this interface.


Subscribe/ unsubscribe WTN video stream

A user can call this method to subscribe or unsubscribe a WTN stream whether he/she has joined the room or not.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of the WTN stream. If the stream has not been published then, the local client will receive the WTN stream once it starts publishing. |
|subscribe |bool |Whether to subscribe to the WTN stream.<br><br><br>&nbsp;<br><br>* true: Subscribe<br><br>* false: Unsubscribe |


**Return Value**


* 0: Success. You will also be informed by [onWTNVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IWTNStreamEventHandler-onwtnvideosubscribestatechanged).

* !0: Failure because of invalid parameter or empty parameters.


**Notes**


* A client can play up to 5 WTN streams simultaneously. Please call [subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/25049#IWTNStream-subscribewtnvideostream)/[subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/25049#IWTNStream-subscribewtnaudiostream) in time to cancel the subscription to WTN streams to avoid exceeding the limit of subscribed WTN streams.

* We recommend to bind a view for the WTN stream before calling this API to subscribe a WTN stream.

   \- Internal renderer: By calling [setWTNRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/25049#IWTNStream-setwtnremotevideocanvas) or

   \- Custom renderer: By calling [setWTNRemoteVideoSink](https://docs.byteplus.com/en/docs/12/25049#IWTNStream-setwtnremotevideosink)

* After calling this API, you will be informed once the first frame has been decoded successfully by [onWTNFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-85517#IWTNStreamEventHandler-onwtnfirstremotevideoframedecoded).

* If the WTN stream contains SEI information, you will be informed by [oonWTNSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IWTNStreamEventHandler-onwtnseimessagereceived).

    &nbsp;


<span id="subscribewtnaudiostream"></span>
### subscribeWTNAudioStream

```cpp
virtual int subscribeWTNAudioStream(
    const char* stream_id,
    bool subscribe
) = 0;
```


> Available since 3.60. Since version 3.60, this interface replaces the `startPlayPublicStream` and `stopPlayPublicStream` methods for subscribing to and unsubscribing from WTN audio streams. If you are using these methods, please migrate to this interface.


Subscribe/unsubscribe the WTN audio stream

A user can call this method to subscribe a WTN stream whether he/she has joined the room or not.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of the WTN stream. If the stream has not been published then, the local client will receive the WTN stream once it starts publishing. |
|subscribe |bool |Whether to subscribe to the WTN stream.<br><br><br>&nbsp;<br><br>* true: Subscribe<br><br>* false: Unsubscribe |


**Return Value**


* 0: Success. You will also be informed by [onWTNAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IWTNStreamEventHandler-onwtnaudiosubscribestatechanged).

* !0: Failure because of invalid parameter or empty parameters.


**Notes**


* A client can play up to 5 WTN streams simultaneously. Please call [subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/25049#IWTNStream-subscribewtnvideostream)/[subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/25049#IWTNStream-subscribewtnaudiostream) in time to cancel the subscription to WTN streams to avoid exceeding the limit of subscribed WTN streams.

* We recommend to bind a view for the WTN stream before calling this API to subscribe a WTN stream.

   \- Internal renderer: By calling [setWTNRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/25049#IWTNStream-setwtnremotevideocanvas) or

   \- Custom renderer: By calling [setWTNRemoteVideoSink](https://docs.byteplus.com/en/docs/12/25049#IWTNStream-setwtnremotevideosink)

* After calling this API, you will be informed once the first frame has been decoded successfully by [onWTNFirstRemoteAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IWTNStreamEventHandler-onwtnfirstremoteaudioframe).

* If the WTN stream contains SEI information, you will be informed by [onWTNSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IWTNStreamEventHandler-onwtnseimessagereceived).

    &nbsp;


<span id="setwtnremotevideocanvas"></span>
### setWTNRemoteVideoCanvas

```cpp
virtual int setWTNRemoteVideoCanvas(
    const char* stream_id,
    const VideoCanvas& canvas
) = 0;
```


> Available since 3.60. Since version 3.60, this interface replaces `setPublicStreamVideoCanvas` for the following function. If you have upgraded to version 3.60 or above and are still using this method, please migrate to this interface.


Assign a internal render view to the WTN stream

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of the WTN stream |
|canvas |const VideoCanvas& |Internal render view. If you want to unbind the video, set `videoCanvas` to null. Refer to [VideoCanvas](https://docs.byteplus.com/en/docs/12/docs-85519#VideoCanvas) for more details. |


**Return Value**


* 0: Success

* !0: Failure

    &nbsp;


<span id="setwtnremotevideosink"></span>
### setWTNRemoteVideoSink

```cpp
virtual int setWTNRemoteVideoSink(
    const char* stream_id,
    IVideoSink* video_sink,
    RemoteVideoSinkConfig& config
) = 0;
```


> Available since 3.60. Since version 3.60, this interface replaces `setPublicStreamVideoSink` for the following function. If you have upgraded to version 3.60 or above and are still using this method, please migrate to this interface.


Assign a custom renderer to the WTN stream. See [Custom Video Rendering](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-81201)

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of the WTN stream |
|video_sink |IVideoSink\* |Custom renderer. Set to be `null` when you want to release the renderer. Refer to [IVideoSink](https://docs.byteplus.com/en/docs/12/docs-85519#IVideoSink) for more details. |
|config |RemoteVideoSinkConfig& |Remote video frame callback configuration. Refer to [RemoteVideoSinkConfig](https://docs.byteplus.com/en/docs/12/docs-85519#RemoteVideoSinkConfig) for more details. |


**Return Value**


* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for specific reasons.

    &nbsp;


<span id="setwtnremoteaudioplaybackvolume"></span>
### setWTNRemoteAudioPlaybackVolume

```cpp
virtual int setWTNRemoteAudioPlaybackVolume(
    const char* stream_id,
    int volume
) = 0;
```


> Available since 3.60. Since version 3.60, this interface replaces `setPublicStreamAudioPlaybackVolume` for the following function. If you have upgraded to version 3.60 or above and are still using this method, please migrate to this interface.


Set the audio playback volume of the WTN stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of the WTN stream. |
|volume |int |Ratio(%) of the audio playback volume to the original volume, in the range `[0, 400]`, with overflow protection. The default volume is 100.<br><br>&nbsp;<br><br>To ensure the audio quality, the recommended range is `[0, 100]`. |


**Return Value**


* 0: Success.

* \-2: Wrong parameter.

    &nbsp;


<span id="setwtnstreameventhandler"></span>
### setWTNStreamEventHandler

```cpp
virtual int setWTNStreamEventHandler(IWTNStreamEventHandler* handler) = 0;
```


> Available since 3.60.


Set the WTN event handler.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|handler |IWTNStreamEventHandler\* |See [IWTNStreamEventHandler](https://docs.byteplus.com/en/docs/12/docs-85517#IWTNStreamEventHandler). |


<span id="IRTCRoom"></span>
# IRTCRoom

```cpp
class bytertc::IRTCRoom
```


Room interface

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual void |[destroy](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-destroy) |
|virtual int |[setUserVisibility](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-setuservisibility) |
|virtual int |[setRTCRoomEventHandler](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-setrtcroomeventhandler) |
|virtual int |[joinRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-joinroom) |
|virtual int |[publishStreamVideo](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-publishstreamvideo) |
|virtual int |[publishStreamAudio](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-publishstreamaudio) |
|virtual int |[subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-subscribestreamvideo) |
|virtual int |[subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-subscribestreamaudio) |
|virtual int |[setRemoteSimulcastStreamType](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-setremotesimulcaststreamtype) |
|virtual int |[setRemoteVideoConfig](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-setremotevideoconfig) |
|virtual int |[setStreamExtraInfo](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-setstreamextrainfo) |
|virtual int |[subscribeAllStreamsVideo](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-subscribeallstreamsvideo) |
|virtual int |[subscribeAllStreamsAudio](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-subscribeallstreamsaudio) |
|virtual int |[pauseAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-pauseallsubscribedstreamvideo) |
|virtual int |[pauseAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-pauseallsubscribedstreamaudio) |
|virtual int |[resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-resumeallsubscribedstreamvideo) |
|virtual int |[resumeAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-resumeallsubscribedstreamaudio) |
|virtual int |[setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-setmultideviceavsync) |
|virtual int |[startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-startforwardstreamtorooms) |
|virtual int |[updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-updateforwardstreamtorooms) |
|virtual int |[stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-stopforwardstreamtorooms) |
|virtual int |[pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-pauseforwardstreamtoallrooms) |
|virtual int |[resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-resumeforwardstreamtoallrooms) |
|virtual int |[setRemoteRoomAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-setremoteroomaudioplaybackvolume) |
|virtual int |[setAudioSelectionConfig](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-setaudioselectionconfig) |
|virtual int64_t |[setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-setroomextrainfo) |
|virtual const char\* |[getRoomId](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-getroomid) |
|virtual const char\* |[getCallId](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-getcallid) |
|virtual int |[setLiveMode](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-setlivemode) |


<span id="instructions"></span>
## Instructions

<span id="IRTCRoom-destroy"></span>
### destroy

```cpp
virtual void destroy() = 0;
```


Leave and destroy the RTC room instance created by calling [createRTCRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-creatertcroom).

<span id="IRTCRoom-setuservisibility"></span>
### setUserVisibility

```cpp
virtual int setUserVisibility(bool enable) = 0;
```


Set the visibility of the user in the room. The local user is visible to others by default before calling this API.

An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Room Capacity](https://docs.byteplus.com/en/byteplus-rtc/docs/257549).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|enable |bool |Visibility of the user in the room.<br><br><br>&nbsp;<br><br>* true: The user can publish media streams. The other users in the room get informed of the behaviors of the user, such as joining room, starting video capture, and leaving room.<br><br>* false: The user cannot publish media streams. The other users in the room do not get informed of the behaviors of the user, such as joining room, starting video capture, or leaving room. |


**Return Value**


* 0: Success.

* < 0 : Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus).

   You will receive [onUserVisibilityChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuservisibilitychanged) after calling this API. (Available since v3.54)

* If you call this API before joining room, and the set value is different from the default value, you will receive the callback when you join the room.

* If you call this API after joining room, and the current visibility is different from the previous value, you will receive the callback.

* When reconnecting after losing internet connection, if the visibility changes, you will receive the callback.


**Notes**


* You can call this API whether the user is in a room or not.

   * When you call this API while you are in the room, the other users in the room will be informed via the following callback.

      • When you switch from `false` to `true`, they will receive [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onuserjoined).


• When you switch from `true` to `false`, they will receive [onUserLeave](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onuserleave).

• The invisible user will receive the warning code, `kWarningCodePublishStreamForbidden`, when trying to publish media streams.

<span id="IRTCRoom-setrtcroomeventhandler"></span>
### setRTCRoomEventHandler

```cpp
virtual int setRTCRoomEventHandler(IRTCRoomEventHandler* room_event_handler) = 0;
```


Listens for event callbacks related to the [IRTCRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom) instance by setting the event handler of this instance.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|room_event_handler |IRTCRoomEventHandler\* |Refer to [IRTCRoomEventHandler](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details

    &nbsp;


<span id="joinroom"></span>
### joinRoom

```cpp
virtual int joinRoom(
    const char* token,
    const UserInfo& user_info,
    bool user_visibility,
    const RTCRoomConfig& config
) = 0;
```


Join an RTC room.

After creating a room by calling [createRTCRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-creatertcroom), call this API to join the room and make audio & video calls with other users in the room.

> Users (including backend bots) who successfully join the RTC room will start billing. If the room only has 1 user, the audio billing time will be calculated. See [Audio Billing](https://docs.byteplus.com/en/docs/12/docs-69871) for more details.


**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|token |const char\* |Dynamic key for authenticating the logged\-in user.<br><br>&nbsp;<br><br>You need to bring Token to enter the room. When testing, you can use the console to generate temporary tokens. The official launch requires the use of the key SDK to generate and issue tokens at your server level. See [Authentication with Token](https://docs.byteplus.com/en/docs/12/docs-70121) for token validity and generation method.<br><br><br>&nbsp;<br><br>* Apps with different App IDs cannot communicate with each other.<br><br>* Make sure that the App ID used to generate the Token is the same as the App ID used to create the engine, otherwise it will cause the join room to fail. |
|user_info |const UserInfo& |User information. See [UserInfo](https://docs.byteplus.com/en/docs/12/docs-85519#UserInfo). |
|user_visibility |bool |User visibility. We recommend setting the user visibility to `false` when entering the room, and then setting it to `true` via [setUserVisibility](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-setuservisibility) when the user needs to send audio & video streams. Joining fails when the number of users in an RTC room reaches the upper limit. An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Capability of Users and Streams](https://docs.byteplus.com/en/byteplus-rtc/docs/257549). |
|config |const RTCRoomConfig& |Room parameter configuration, set the room mode and whether to automatically publish or subscribe to the flow. See [RTCRoomConfig](https://docs.byteplus.com/en/docs/12/docs-85519#RTCRoomConfig) for the specific configuration mode. |


**Return Value**


* 0: Success.

   * Local users receive notifications of the room state via [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onroomstatechanged).

   * Local users receive notifications of the local\-stream state via [onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onvideopublishstatechanged), [onAudioPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onaudiopublishstatechanged).

   * Local users receive notifications of the subscribed\-stream state via [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserpublishstreamaudio).

   * Local users receive notifications of the published\-stream state via [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserpublishstreamaudio).

   * If the local user is also a visible user, the other participants receive [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserjoined) callback.

* \-1: Room_id/user_info.uid contains invalid parameters.

* \-2: Already in the room. After the interface call is successful, as long as the return value of 0 is received and [leaveRoom](https://docs.byteplus.com/en/docs/12/25049#IRTSRoom-leaveroom) is not called successfully, this return value is triggered when the room entry interface is called again, regardless of whether the filled room ID and user ID are duplicated.

   The reason for the failure will be communicated via the [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onroomstatechanged) callback.


**Notes**


* In the same room with the same App ID, the user ID of each user must be unique. If two users have the same user ID, the user who entered the room later will kick the user who entered the room out of the room, and the user who entered the room will receive the [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onroomstatechanged) callback notification. For the error type. See kErrorCodeDuplicateLogin in [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-85518#ErrorCode).

* After the user successfully joins the room, the SDK may lose connection to the server in case of poor local network conditions. At this point, [onConnectionStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onconnectionstatechanged) callback will be triggered and the SDK will automatically retry until it successfully reconnects to the server. After a successful reconnection, you will receive a local [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTSRoomEventHandler-onroomstatechanged) callback notification.

    &nbsp;


<span id="publishstreamvideo"></span>
### publishStreamVideo

```cpp
virtual int publishStreamVideo(bool publish) = 0;
```


> Available since 3.60. Since version 3.60, this interface replaces the `publishStream`, `unpublishStream`, `publishScreen` and `unpublishScreen` methods for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.


Publishes or stops publishing video streams.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|publish |bool |Whether to publish the video stream.<br><br><br>&nbsp;<br><br>* `true`: Publish.<br><br>* `false`: Stop publishing. |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* You don't need to call this API if you set it to Auto\-publish when calling [joinRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-joinroom).

* An invisible user cannot publish media streams. Call [setUserVisibility](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-setuservisibility) to change your visibility in the room.

* Call [publishStreamAudio](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-publishstreamaudio) to start or stop publishing the audio stream captured by the microphone.

* Call [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-startforwardstreamtorooms) to forward the published streams to the other rooms.

* After you call this API, the other users in the room will receive [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserpublishstreamvideo). Those who successfully received your streams will receive [onFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onfirstremotevideoframedecoded) at the same time.

    &nbsp;


<span id="publishstreamaudio"></span>
### publishStreamAudio

```cpp
virtual int publishStreamAudio(bool publish) = 0;
```


> Available since 3.60. Since version 3.60, this interface replaces the `publishStream`, `unpublishStream`, `publishScreen` and `unpublishScreen` methods for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.


Publishes or stops publishing audio streams in the current room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|publish |bool |Whether to publish the audio stream.<br><br><br>&nbsp;<br><br>* `true`: Publish.<br><br>* `false`: Stop publishing. |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* You don't need to call this API if you set it to Auto\-publish when calling [joinRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-joinroom).

* An invisible user cannot publish media streams. Call [setUserVisibility](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-setuservisibility) to change your visibility in the room.

* Call [publishStreamVideo](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-publishstreamvideo) to start or stop publishing the video stream captured by the camera.

* Call [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-startforwardstreamtorooms) to forward the published streams to the other rooms.

* After you call this API, the other users in the room will receive [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserpublishstreamaudio). Those who successfully received your streams will receive [onFirstRemoteAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onfirstremoteaudioframe) at the same time.

    &nbsp;


<span id="subscribestreamvideo"></span>
### subscribeStreamVideo

```cpp
virtual int subscribeStreamVideo(
    const char*stream_id,
    bool subscribe
) = 0;
```


> Available since 3.60. Since version 3.60, this interface replaces the `subscribeStream`, `unsubscribeStream`, `subscribeScreen` and `unsubscribeScreen` methods for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.


Subscribes to or unsubscribes from the specific remote video stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |The ID of the remote video stream. |
|subscribe |bool |Whether to subscribe to the video stream.<br><br><br>&nbsp;<br><br>* `true`: Subscribe.<br><br>* `false`: Unsubscribe. |


**Return Value**

API call result:


* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for specific reasons.


**Notes**


* Calling this API to update the subscribe configuration when the user has subscribed the remote user either by calling this API or by auto\-subscribe.

* You must first get the remote stream information through [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserpublishstreamvideo) before calling this API to subscribe to streams accordingly.

* After calling this API, you will be informed of the calling result with [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onvideosubscribestatechanged).

* Once the local user subscribes to the stream of a remote user, the subscription to the remote user will sustain until the local user leaves the room or unsubscribe from it by calling [subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-subscribestreamvideo).

* Any other exceptions will be included in [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onvideosubscribestatechanged), see [SubscribeStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-85519#SubscribeStateChangeReason) for the reasons.

    &nbsp;


<span id="subscribestreamaudio"></span>
### subscribeStreamAudio

```cpp
virtual int subscribeStreamAudio(
    const char*stream_id,
    bool subscribe
) = 0;
```


> Available since 3.60. Since version 3.60, this interface replaces the `subscribeStream`, `unsubscribeStream`, `subscribeScreen` and `unsubscribeScreen` methods for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.


Subscribes to or unsubscribes from the specific remote audio streams.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |The ID of the target remote audio stream. |
|subscribe |bool |Whether to subscribe to the audio stream.<br><br><br>&nbsp;<br><br>* `true`: Subscribe.<br><br>* `false`: Unsubscribe. |


**Return Value**

API call result:


* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for specific reasons.


**Notes**


* Calling this API to update the subscribe configuration when the user has subscribed the remote user either by calling this API or by auto\-subscribe.

* You must first get the remote stream information through [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserpublishstreamaudio) before calling this API to subscribe to streams accordingly.

* After calling this API, you will be informed of the calling result with [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onaudiosubscribestatechanged).

* Once the local user subscribes to the stream of a remote user, the subscription to the remote user will sustain until the local user leaves the room or unsubscribe from it by calling [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-subscribestreamaudio).

* Any other exceptions will be included in [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onaudiosubscribestatechanged), see [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-85518#ErrorCode) for the reasons.

    &nbsp;


<span id="setremotesimulcaststreamtype"></span>
### setRemoteSimulcastStreamType

```cpp
virtual int setRemoteSimulcastStreamType(
    const char* stream_id,
    SimulcastStreamType stream_type
) = 0;
```


> Available since 3.60.


Sets the type of the remote video stream to subscribe to.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of the remote video stream you expect to subscribe to. |
|stream_type |SimulcastStreamType |Video stream type, see [SimulcastStreamType](https://docs.byteplus.com/en/docs/12/docs-85519#SimulcastStreamType). |


**Return Value**

API call result:


* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for specific reasons.


**Notes**


* This API only works after the publisher calls [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setlocalsimulcastmode) to enable publishing multiple\-quality video streams, in which case the subscriber will receive the stream from the publisher that is closest to the set configuration; otherwise the subscriber will only receive one video stream with a resolution of 640px × 360px and a frame rate of 15fps.

* If you don't call this API after the publisher enables the function of publishing multiple streams, you will receive by default the video stream with the largest resolution set by the publisher.

    &nbsp;


<span id="setremotevideoconfig"></span>
### setRemoteVideoConfig

```cpp
virtual int setRemoteVideoConfig(
    const char*stream_id,
    const RemoteVideoConfig&remote_video_config
) = 0;
```


Sets your expected configuration of the remote video stream that you want to subscribe to or have subscribed to.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of the remote video stream you want to configure subscription parameters for. |
|remote_video_config |const RemoteVideoConfig& |Parameters you want to configure for the remote video stream, see [RemoteVideoConfig](https://docs.byteplus.com/en/docs/12/docs-85519#RemoteVideoConfig). |


**Return Value**

API call result:


* 0: Success.

* !0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for specific reasons.


**Notes**


* This API only works after the publisher calls [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setlocalsimulcastmode) to enable publishing multiple video streams, in which case the subscriber will receive the stream from the publisher that is closest to the set configuration; otherwise the subscriber will only receive one video stream with a resolution of 640px × 360px and a frame rate of 15fps..

* If you don't call this API after the publisher enables the function of publishing multiple streams, you will receive by default the video stream with the largest resolution set by the publisher.

* You should call this API in the room.

* SDK will automatically select the stream to be published or subcribed based on the settings of both sides see for details.

    &nbsp;


<span id="setstreamextrainfo"></span>
### setStreamExtraInfo

```cpp
virtual int setStreamExtraInfo(const char* extra_info) = 0;
```


> Available Available since 3.60


Sets the stream extra info.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|extra_info |const char\* |Stream extra info. The length cannot exceed 1024 bytes. |


**Return Value**

API call result:


* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for specific reasons.


**Notes**


* This function can be used to set the stream extra information for the current streaming. The stream additional information serves as an additional information identifier for the stream ID. Unlike the stream ID, which cannot be modified during the streaming process, the stream additional information can be updated midway through the streaming of the corresponding stream ID. Developers can leverage the stream additional information to achieve synchronization of variable content related to the stream ID.

* This method can be called either before or after entering the room.

* Other users in the same room will receive notifications via the [onRoomStreamExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onroomstreamextrainfoupdate) callback function.

    &nbsp;


<span id="subscribeallstreamsvideo"></span>
### subscribeAllStreamsVideo

```cpp
virtual int subscribeAllStreamsVideo(bool subscribe) = 0;
```


> Available since 3.60. Since version 3.60, this interface replaces the `subscribeAllStreams` and `unsubscribeAllStreams` methods for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.


Subscribes to or unsubscribes from all remote video streams (by the camera).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|subscribe |bool |Whether to subscribe to all remote video streams.<br><br><br>&nbsp;<br><br>* `true`: Subscribe.<br><br>* `false`: Unsubscribe. |


**Return Value**

API call result:


* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* If the subscription options conflict with the previous ones, they are subject to the configurations in the last call.

* With the Audio selection enabled, if the number of media streams exceeds the limit, we recommend you subscribe each target media stream with the API follows: [subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-subscribestreamvideo), [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-subscribestreamaudio).

* After calling this API, you will be informed of the calling result with [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onvideosubscribestatechanged), [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onaudiosubscribestatechanged). You can also find exceptions cause from the callbacks above.

* Once the local user subscribes to the stream of a remote user, the subscription to the remote user will sustain until the local user leaves the room or unsubscribe from it by calling [subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-subscribestreamvideo), [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-subscribestreamaudio).

    &nbsp;


<span id="subscribeallstreamsaudio"></span>
### subscribeAllStreamsAudio

```cpp
virtual int subscribeAllStreamsAudio(bool subscribe) = 0;
```


> Available since 3.60. Since version 3.60, this interface replaces the `subscribeAllStreams` and `unsubscribeAllStreams` methods for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.


Subscribes to or unsubscribes from all remote audio streams (by the microphone).

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|subscribe |bool |Whether to subscribe to all remote audio streams.<br><br><br>&nbsp;<br><br>* `true`: Subscribe.<br><br>* `false`: Unsubscribe. |


**Return Value**

API call result:


* 0: Success

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* If the subscription options conflict with the previous ones, they are subject to the configurations in the last call.

* With the Audio selection enabled, if the number of media streams exceeds the limit, we recommend you subscribe each target media stream with the API follows: [subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-subscribestreamvideo), [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-subscribestreamaudio).

* After calling this API, you will be informed of the calling result with [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onvideosubscribestatechanged), [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onaudiosubscribestatechanged). You can also find exceptions cause from the callbacks above.

* Once the local user subscribes to the stream of a remote user, the subscription to the remote user will sustain until the local user leaves the room or unsubscribe from it by calling [subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-subscribestreamvideo), [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-subscribestreamaudio).

    &nbsp;


<span id="pauseallsubscribedstreamvideo"></span>
### pauseAllSubscribedStreamVideo

```cpp
virtual int pauseAllSubscribedStreamVideo() = 0;
```


> Available since 3.60. Since version 3.60, this interface replaces the `pauseAllSubscribedStreamAudio` for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.


Pauses receiving all the video streams of all remote users.

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* Calling this API does not change the capture state and the transmission state of the remote clients.

* Calling this API does not cancel the subscription or change any subscription configuration.

* To resume, call [resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-resumeallsubscribedstreamvideo).

* In a multi\-room scenario, this API only pauses the reception of streams published in the current room.

    &nbsp;


<span id="pauseallsubscribedstreamaudio"></span>
### pauseAllSubscribedStreamAudio

```cpp
virtual int pauseAllSubscribedStreamAudio() = 0;
```


> Available since 3.60. Since version 3.60, this interface replaces the `pauseAllSubscribedStream` for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.


Pauses receiving the audio streams of all remote users.

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* Calling this API does not change the capture state and the transmission state of the remote clients.

* Calling this API does not cancel the subscription or change any subscription configuration.

* To resume, call [resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-resumeallsubscribedstreamvideo).

* In a multi\-room scenario, this API only pauses the reception of streams published in the current room.

    &nbsp;


<span id="resumeallsubscribedstreamvideo"></span>
### resumeAllSubscribedStreamVideo

```cpp
virtual int resumeAllSubscribedStreamVideo() = 0;
```


> Available since 3.60. Since version 3.60, this interface replaces the `resumeAllSubscribedStream` method to implement the below functions. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this interface.


Resumes receiving all the video streams of all remote users.

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* Calling this API does not change the capture state and the transmission state of the remote clients.

* Calling this API does not change any subscription configuration.

    &nbsp;


<span id="resumeallsubscribedstreamaudio"></span>
### resumeAllSubscribedStreamAudio

```cpp
virtual int resumeAllSubscribedStreamAudio() = 0;
```


> Available since 3.60. Since version 3.60, this interface replaces the `resumeAllSubscribedStream` method to implement the below functions. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this interface.


Resumes receiving all the audio streams of all remote users.

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**


* Calling this API does not change the capture state and the transmission state of the remote clients.

* Calling this API does not change any subscription configuration.

    &nbsp;


<span id="setmultideviceavsync"></span>
### setMultiDeviceAVSync

```cpp
virtual int setMultiDeviceAVSync(const char* audio_user_id) = 0;
```


Synchronizes published audio and video.

When the same user simultaneously uses separate devices to capture and publish audio and video, there is a possibility that the streams are out of sync due to the network disparity. In this case, you can call this API on the video publisher side and the SDK will automatically line the video stream up according to the timestamp of the audio stream, ensuring that the audio the receiver hears corresponds to the video the receiver watches.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audio_user_id |const char\* |The ID of audio publisher. You can stop the current A/V synchronization by setting this parameter to null. |


**Return Value**


* 0: Success. When the A/V synchronization state changes, you will receive [onAVSyncStateChange](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onavsyncstatechange).

* < 0 : Fail. You can also learn the error details via [onAVSyncEvent](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onavsyncevent). More than one pair of audio and video can be synchronized simultaneously in the same RTC room, but you should note that one single audio source cannot be synchronized with multiple video sources at the same time.


**Notes**


* You can call this API anytime before or after entering the room.

* The source user IDs of the audio and video stream to be synchronized must be in the same RTC room.

* If you want to change the audio source, call this API again with a new `audio_user_id`. If you want to change the video source, you need to stop the current synchronization first, then call this API on the new video publisher side.

    &nbsp;


<span id="startforwardstreamtorooms"></span>
### startForwardStreamToRooms

```cpp
virtual int startForwardStreamToRooms(const ForwardStreamConfiguration& configuration) = 0;
```


Start relaying media stream across rooms.

After calling [joinRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-joinroom), you can call this method to publish the media stream to multiple rooms that applies to scenarios such as anOnline talent contest and so on.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|configuration |const ForwardStreamConfiguration& |Information of the rooms where you want to relay the media stream to. Refer to [ForwardStreamConfiguration](https://docs.byteplus.com/en/docs/12/docs-85519#ForwardStreamConfiguration) for more information. |


**Return Value**


* 0: Success

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* Call this method will trigger [onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onforwardstreamstatechanged).

* After calling this method, listen the events from each room during the relaying by registering [onForwardStreamEvent](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onforwardstreamevent).

* Once the relaying begins, the other users in the room will receive callback of [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserjoined), [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserpublishstreamaudio).

* Call [updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-updateforwardstreamtorooms) to add or remove the target room(s) after calling this method.

* Call [stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-stopforwardstreamtorooms) to stop relaying to all rooms after calling this method.

* Call [pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-pauseforwardstreamtoallrooms) to pause relaying to all rooms after calling this method.

    &nbsp;


<span id="updateforwardstreamtorooms"></span>
### updateForwardStreamToRooms

```cpp
virtual int updateForwardStreamToRooms(const ForwardStreamConfiguration& configuration) = 0;
```


Update information of the rooms where you want to relay the media stream to after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-startforwardstreamtorooms).

Adding and removing rooms by calling this method will trigger [onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onforwardstreamstatechanged) on the local.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|configuration |const ForwardStreamConfiguration& |Information of the rooms where you want to relay the media stream to. Refer to [ForwardStreamConfiguration](https://docs.byteplus.com/en/docs/12/docs-85519#ForwardStreamConfiguration) for more information. |


**Return Value**


* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**

Users in the room which is added or removed from the target list by calling this method will receive [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserjoined), [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserpublishstreamaudio).

<span id="IRTCRoom-stopforwardstreamtorooms"></span>
### stopForwardStreamToRooms

```cpp
virtual int stopForwardStreamToRooms() = 0;
```


Call to this method to stop relaying media stream to all rooms after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-startforwardstreamtorooms).

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* Call this method will trigger [onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onforwardstreamstatechanged).

* The other users in the room will receive callback of [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserjoined), [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserpublishstreamaudio) when you stop relaying.

* To stop relaying media stream to specific rooms, call [updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-updateforwardstreamtorooms) instead.

* To resume the relaying in a short time, call [pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-pauseforwardstreamtoallrooms) instead and then call [resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-resumeforwardstreamtoallrooms) to recsume after that.

    &nbsp;


<span id="pauseforwardstreamtoallrooms"></span>
### pauseForwardStreamToAllRooms

```cpp
virtual int pauseForwardStreamToAllRooms() = 0;
```


Call this method to pause relaying media stream to all rooms after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-startforwardstreamtorooms).

After that, call [resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-resumeforwardstreamtoallrooms) to resume.

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**

The other users in the room will receive callback of [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserpublishstreamaudio) when you pause relaying.

<span id="IRTCRoom-resumeforwardstreamtoallrooms"></span>
### resumeForwardStreamToAllRooms

```cpp
virtual int resumeForwardStreamToAllRooms() = 0;
```


Call this method to resume relaying to all rooms from the pause by calling [pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-pauseforwardstreamtoallrooms).

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**

The other users in the room will receive callback of [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserjoined), [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onuserpublishstreamaudio) when you resume relaying.

<span id="IRTCRoom-setremoteroomaudioplaybackvolume"></span>
### setRemoteRoomAudioPlaybackVolume

```cpp
virtual int setRemoteRoomAudioPlaybackVolume(int volume) = 0;
```


Adjusts the audio playback volume from all the remote users in a room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|volume |int |Ratio(%) of playback volume to original volume, in the range [0, 400], with overflow protection.<br><br>&nbsp;<br><br>To ensure the audio quality, we recommend setting the volume to `100`.<br><br><br>&nbsp;<br><br>* 0: mute<br><br>* 100: original volume. Default value.<br><br>* 400: Up to 4 times the original volume (with overflow protection) |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details


**Notes**

Suppose a remote user A is always within the range of the target user whose playback volume will be adjusted,


* If you use both this method and [setRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setremoteaudioplaybackvolume), the volume that the local user hears from user A is the volume set by the method called later.

* If you use both this method and [setPlaybackVolume](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-setplaybackvolume), the volume that the local user hears from user A is the overlay of both settings.

    &nbsp;


<span id="setaudioselectionconfig"></span>
### setAudioSelectionConfig

```cpp
virtual int setAudioSelectionConfig(AudioSelectionPriority audio_selection_priority) = 0;
```


> Available since 3.52.


Set the priority of the local audio stream to be published.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audio_selection_priority |AudioSelectionPriority |The priority of the local audio stream which defaults to be subscribable only up to the result of the Audio Selection. Refer to [AudioSelectionPriority](https://docs.byteplus.com/en/docs/12/docs-85519#AudioSelectionPriority). |


**Notes**


* You must enable Audio Selection in the RTC console before using this API. You can call this API whether the user has joined a room. Refer to [Audio Selection](https://docs.byteplus.com/byteplus-rtc/docs/113547).

* The setting is independent in each room that the user joins.

    &nbsp;


<span id="setroomextrainfo"></span>
### setRoomExtraInfo

```cpp
virtual int64_t setRoomExtraInfo(
    const char*key,
    const char*value
) = 0;
```


> Available since 3.52.


Sets extra information about the room the local user joins.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|key |const char\* |Key of the extra information, less than 10 bytes in length.<br><br>&nbsp;<br><br>A maximum of 5 keys can exist in the same room, beyond which the first key will be replaced. |
|value |const char\* |Content of the extra information, less than 128 bytes in length. |


**Return Value**

API call result:


* 0: Success with a taskId returned.

* <0: Failure. See [SetRoomExtraInfoResult](https://docs.byteplus.com/en/docs/12/docs-85519#SetRoomExtraInfoResult) for the reasons.


**Notes**


* Call [joinRoom](https://docs.byteplus.com/en/docs/12/25049#IRTCRoom-joinroom) first before you call this API to set extra information.

* After calling this API, you will receive [onSetRoomExtraInfoResult](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onsetroomextrainforesult) callback informing you the result of the setting.

* After the extra information is successfully set, other users in the same room will receive the information through [onRoomExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCRoomEventHandler-onroomextrainfoupdate) callback.

* Users who join the room later will be notified of all extra information in the room set prior to entering.

    &nbsp;


<span id="getroomid"></span>
### getRoomId

```cpp
virtual const char* getRoomId() = 0;
```


> Available since 3.53


Get room ID.

**Return Value**

Room ID.

<span id="IRTCRoom-getcallid"></span>
### getCallId

```cpp
virtual const char* getCallId() = 0;
```


> Available since 3.60.


Gets call ID.

Call this method after joining a room. After creating a room, a call ID is generated to identify the call for this room.

**Return Value**

Call ID.

<span id="IRTCRoom-setlivemode"></span>
### setLiveMode

```cpp
virtual int setLiveMode(RoomLiveMode live_mode) = 0;
```


> Available since 3.60.


Sets room live mode.

Call this method after joining a room.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|live_mode |RoomLiveMode |Live mode. See [RoomLiveMode](https://docs.byteplus.com/en/docs/12/docs-85519#RoomLiveMode) for details. |


**Return Value**


* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.

    &nbsp;


<span id="public-api"></span>
# Public API

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|void\* |[view_t](https://docs.byteplus.com/en/docs/12/25049#view_t) |


<span id="function"></span>
## Function


|Return |Name |
|---|---|
|BYTERTC_API IAudioFrame\* |[buildAudioFrame](https://docs.byteplus.com/en/docs/12/25049#buildaudioframe) |
|BYTERTC_API IEncodedVideoFrame\* |[buildEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/25049#buildencodedvideoframe) |


<span id="instructions"></span>
## Instructions

<span id="view_t"></span>
### view_t

```cpp
typedef void* bytertc::view_t
```


Windows window id, Windows platform down to Windows window handle

<span id="instructions"></span>
## Instructions

<span id="buildaudioframe"></span>
### buildAudioFrame

```cpp
BYTERTC_API IAudioFrame* buildAudioFrame(const AudioFrameBuilder& builder);
```


Create IAudioFrame

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|builder |const AudioFrameBuilder& |Audio frame build instance. See [AudioFrameBuilder](https://docs.byteplus.com/en/docs/12/docs-85519#AudioFrameBuilder) |


**Return Value**

Refer to [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IAudioFrame) for more details.

<span id="buildencodedvideoframe"></span>
### buildEncodedVideoFrame

```cpp
BYTERTC_API IEncodedVideoFrame* buildEncodedVideoFrame(const EncodedVideoFrameBuilder& builder);
```


Create IEncodedVideoFrame

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|builder |const EncodedVideoFrameBuilder& |Encoded video frame build instance. See [EncodedVideoFrameBuilder](https://docs.byteplus.com/en/docs/12/docs-85519#EncodedVideoFrameBuilder) |


**Return Value**

[IEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IEncodedVideoFrame) instance

<span id="IMediaPlayer"></span>
# IMediaPlayer

```cpp
class bytertc::IMediaPlayer
```


> Available since 3.53


Media player

Call [setEventHandler](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-seteventhandler) to set the callback handler to receive related callbacks.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|IMediaPlayer |[IMediaPlayer](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-imediaplayer) |
|virtual |[~IMediaPlayer](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-~imediaplayer) |
|virtual int |[open](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-open) |
|virtual int |[start](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-start) |
|virtual int |[openWithCustomSource](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-openwithcustomsource) |
|virtual int |[stop](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-stop) |
|virtual int |[pause](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-pause) |
|virtual int |[resume](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-resume) |
|virtual int |[setVolume](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-setvolume) |
|virtual int |[getVolume](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-getvolume) |
|virtual int |[getTotalDuration](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-gettotalduration) |
|virtual int |[getPlaybackDuration](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-getplaybackduration) |
|virtual int |[getPosition](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-getposition) |
|virtual PlayerState |[getState](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-getstate) |
|virtual int |[setAudioPitch](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-setaudiopitch) |
|virtual int |[setPosition](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-setposition) |
|virtual int |[setAudioDualMonoMode](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-setaudiodualmonomode) |
|virtual int |[getAudioTrackCount](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-getaudiotrackcount) |
|virtual int |[selectAudioTrack](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-selectaudiotrack) |
|virtual int |[setPlaybackSpeed](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-setplaybackspeed) |
|virtual int |[setProgressInterval](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-setprogressinterval) |
|virtual int |[setLoudness](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-setloudness) |
|virtual int |[registerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-registeraudioframeobserver) |
|virtual int |[pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-pushexternalaudioframe) |
|virtual int |[setEventHandler](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-seteventhandler) |


<span id="instructions"></span>
## Instructions

<span id="IMediaPlayer-imediaplayer"></span>
### IMediaPlayer

```cpp
IMediaPlayer(){}
```


<span id="IMediaPlayer-~imediaplayer"></span>
### ~IMediaPlayer

```cpp
virtual ~IMediaPlayer() {}
```


<span id="IMediaPlayer-open"></span>
### open

```cpp
virtual int open(
    const char* file_path,
    const MediaPlayerConfig& config
) = 0;
```


Open the audio file.

You can only open one audio file with one player instance at the same time. For multiple audio files at the same time, create multiple player instances.

For audio file in PCM format, see [openWithCustomSource](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-openwithcustomsource). `openWithCustomSource` and this API are mutually exclusive.

**Input Parameters**


|Audio file paths.<br><br>&nbsp;<br><br>URL of online file, URI of local file, or full path to local file. For URL of online file, only the https protocol is supported.<br><br>&nbsp;<br><br>Recommended sample rate for audio effect files: 8KHz、16KHz、22.05KHz、44.1KHz、48KHz.<br><br>&nbsp;<br><br>Local audio effect file formats supported by different platforms:<br><br>&nbsp;<br><br>&nbsp;<br><br>&nbsp;<br><br>&nbsp;<br><br>Online audio effect file formats supported by different platforms.<br><br>&nbsp;<br><br>&nbsp;<br><br> | | |
|---|---|---|
|config |const MediaPlayerConfig& |See [MediaPlayerConfig](https://docs.byteplus.com/en/docs/12/docs-85519#MediaPlayerConfig). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.

    &nbsp;


<span id="start"></span>
### start

```cpp
virtual int start() = 0;
```


Start playing the audio. Call this API when you call [open](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-open) and set `AutoPlay=False`.

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* For audio file in PCM format, see [openWithCustomSource](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-openwithcustomsource). `openWithCustomSource` and this API are mutually exclusive.

* After calling this API, call [stop](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-stop) to stop playing the audio file.

    &nbsp;


<span id="openwithcustomsource"></span>
### openWithCustomSource

```cpp
virtual int openWithCustomSource(
    const MediaPlayerCustomSource& source,
    const MediaPlayerConfig& config
) = 0;
```


Enable audio mixing with audio raw data.

To open the audio file, see [open](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-open). `open` and this API are mutually exclusive.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|source |const MediaPlayerCustomSource& |See [MediaPlayerCustomSource](https://docs.byteplus.com/en/docs/12/docs-85519#MediaPlayerCustomSource). |
|config |const MediaPlayerConfig& |See [MediaPlayerConfig](https://docs.byteplus.com/en/docs/12/docs-85519#MediaPlayerConfig). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* After calling this API, you must call [pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-pushexternalaudioframe) to push audio data and start the audio mixing.

* To stop the raw data audio mixing, call [stop](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-stop).

    &nbsp;


<span id="stop"></span>
### stop

```cpp
virtual int stop() = 0;
```


After calling [open](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-open), [start](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-start), or [openWithCustomSource](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-openwithcustomsource) to start audio mixing, call this method to stop audio mixing.

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.

    &nbsp;


<span id="pause"></span>
### pause

```cpp
virtual int pause() = 0;
```


After calling [open](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-open), or [start](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-start) to start audio mixing, call this API to pause audio mixing.

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* After calling this API to pause audio mixing, call [resume](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-resume) to resume audio mixing.

* The API is valid for audio file, not PCM data.

    &nbsp;


<span id="resume"></span>
### resume

```cpp
virtual int resume() = 0;
```


After calling [pause](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-pause) to pause audio mixing, call this API to resume audio mixing.

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**

The API is valid for audio file, not PCM data.

<span id="IMediaPlayer-setvolume"></span>
### setVolume

```cpp
virtual int setVolume(
    int volume,
    AudioMixingType type
) = 0;
```


Adjusts the volume of the specified audio mixing, including media file mixing and PCM mixing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|volume |int |The ratio of the volume to the original volume in % with overflow protection. The range is `[0, 400]` and the recommended range is `[0, 100]`. |
|type |AudioMixingType |See [AudioMixingType](https://docs.byteplus.com/en/docs/12/docs-85519#AudioMixingType). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**

Call this API only when audio is mixing.

<span id="IMediaPlayer-getvolume"></span>
### getVolume

```cpp
virtual int getVolume(AudioMixingType type) = 0;
```


Gets the current volume.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |AudioMixingType |See [AudioMixingType](https://docs.byteplus.com/en/docs/12/docs-85519#AudioMixingType). |


**Return Value**


* \>0: Success, the current volume.

* < 0: Failed.


**Notes**

Call this API only when audio is mixing, including media file mixing and PCM mixing.

<span id="IMediaPlayer-gettotalduration"></span>
### getTotalDuration

```cpp
virtual int getTotalDuration() = 0;
```


Gets the duration of the media file.

**Return Value**


* \>0: Success, the duration of the media file in milliseconds.

* < 0: Failed.


**Notes**


* Call this API only when audio is mixing.

* The API is valid for audio file, not PCM data.

    &nbsp;


<span id="getplaybackduration"></span>
### getPlaybackDuration

```cpp
virtual int getPlaybackDuration() = 0;
```


Gets the actual playback duration of the mixed media file, in milliseconds.

**Return Value**


* \>0: Success, the actual playback time.

* < 0: Failed.


**Notes**


* The actual playback time refers to the playback time of the song without being affected by stop, jump, double speed, and freeze. For example, if the song stops playing for 30 seconds at 1:30 or skips to 2:00, and then continues to play normally for 2 minutes, the actual playing time is 3 minutes and 30 seconds.

* Call this API only when audio is mixing and the interval set by [setProgressInterval](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-setprogressinterval) is above `0`.

* The API is valid for audio file, not PCM data.

    &nbsp;


<span id="getposition"></span>
### getPosition

```cpp
virtual int getPosition() = 0;
```


Gets the playback progress of the media file.

**Return Value**


* \>0: Success, the playback progress of media file in ms.

* < 0: Failed.


**Notes**


* Call this API only when audio is mixing.

* The API is valid for audio file, not PCM data.

    &nbsp;


<span id="getstate"></span>
### getState

```cpp
virtual PlayerState getState() = 0;
```


Get the state of the media player.

**Return Value**

The current state of the media player. See [PlayerState](https://docs.byteplus.com/en/docs/12/docs-85519#PlayerState).

**Notes**

You can call this method after the creating a `IMediaPlayer` instance.

<span id="IMediaPlayer-setaudiopitch"></span>
### setAudioPitch

```cpp
virtual int setAudioPitch(int pitch) = 0;
```


Set the pitch of the local audio file mixing. Usually used in karaoke scenes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|pitch |int |The increase or decrease value compared with the original pitch of the music file. The range is `[-12, 12]`. The default value is 0. The pitch distance between two adjacent values is half a step. A positive value indicates a rising pitch, and a negative value indicates a falling pitch. |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* Call this API only when audio is mixing.

* Support audio file only and not PCM data.

    &nbsp;


<span id="setposition"></span>
### setPosition

```cpp
virtual int setPosition(int position) = 0;
```


Sets the starting playback position of the media file.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|position |int |The starting position of the media file in milliseconds.<br><br>&nbsp;<br><br>You can get the total duration of the media file through [getTotalDuration](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-gettotalduration). The value of position should be less than the total duration of the media file. |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* The API is valid for audio file, not PCM data.

* When playing online files, calling this API may cause playback delay.

    &nbsp;


<span id="setaudiodualmonomode"></span>
### setAudioDualMonoMode

```cpp
virtual int setAudioDualMonoMode(AudioMixingDualMonoMode mode) = 0;
```


Sets the channel mode of the mixing of the media file.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mode |AudioMixingDualMonoMode |The mode of channel. The default channel mode is the same as the source file. See [AudioMixingDualMonoMode](https://docs.byteplus.com/en/docs/12/docs-85519#AudioMixingDualMonoMode). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* Call this API only when audio is mixing.

* Audio file is supported, but not PCM data.

    &nbsp;


<span id="getaudiotrackcount"></span>
### getAudioTrackCount

```cpp
virtual int getAudioTrackCount() = 0;
```


Gets the track count of the current media file.

**Return Value**


* \>= 0：Success. Return the track count of the current media file.

* < 0：Failed.


**Notes**


* Call this API only when audio is mixing.

* This API is valid for audio file, not PCM data.

    &nbsp;


<span id="selectaudiotrack"></span>
### selectAudioTrack

```cpp
virtual int selectAudioTrack(int index) = 0;
```


Specifies the playback track of the current media file.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|index |int |The specified playback audio track, starting from 0, and the range is `[0, getAudioTrackCount()-1]`. The value must be less than the return value of [getAudioTrackCount](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-getaudiotrackcount). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* Call this API only when audio is mixing.

* This API is valid for audio file, not PCM data.

    &nbsp;


<span id="setplaybackspeed"></span>
### setPlaybackSpeed

```cpp
virtual int setPlaybackSpeed(int speed) = 0;
```


Set the playback speed of the audio file.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|speed |int |The ratio of the actual playback speed than that of the original speed of the audio file in %. The range is `[50,200]`. The default value is 100. |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* Call this API only when audio is mixing.

* The API is valid for audio file and not PCM data.

    &nbsp;


<span id="setprogressinterval"></span>
### setProgressInterval

```cpp
virtual int setProgressInterval(int64_t interval) = 0;
```


Set the interval of the periodic callback [onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-85517#IMediaPlayerEventHandler-onmediaplayerplayingprogress) during audio mixing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|interval |int64_t |interval in ms.<br><br><br>&nbsp;<br><br>* interval \> 0: The callback is enabled. The actual interval is a multiple of 10. If the input value is not divisible by 10, it will be automatically rounded up. For example, if the input is `52`, the actual interval will be 60 milliseconds.<br><br>* interval <= 0: The callback is disabled. |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* Call this API only when audio is mixing.

* This API is valid for audio file, not PCM data.

    &nbsp;


<span id="setloudness"></span>
### setLoudness

```cpp
virtual int setLoudness(float loudness) = 0;
```


To call [enableVocalInstrumentBalance](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-enablevocalinstrumentbalance) to adjust the volume of the mixed media file or the PCM audio data, you must pass in its original loudness through this API.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|loudness |float |Original loudness in lufs. The range is `[-70.0, 0.0]`.<br><br>&nbsp;<br><br>When the value is less than \-70.0lufs, it will be adjusted to \-70.0lufs by default, and if it is more than 0.0lufs, the loudness will not be equalized. The default value is 1.0lufs, which means no processing. |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* Call this API only when audio is mixing.

* The API is valid for audio file and PCM data.

    &nbsp;


<span id="registeraudioframeobserver"></span>
### registerAudioFrameObserver

```cpp
virtual int registerAudioFrameObserver(IMediaPlayerAudioFrameObserver* observer) = 0;
```


Register an observer to receive related callbacks when the local media file is mixing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|observer |IMediaPlayerAudioFrameObserver\* |See [IMediaPlayerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-85517#IMediaPlayerAudioFrameObserver). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**

The API is valid for audio file, not PCM data.

<span id="IMediaPlayer-pushexternalaudioframe"></span>
### pushExternalAudioFrame

```cpp
virtual int pushExternalAudioFrame(IAudioFrame* audio_frame) = 0;
```


Push PCM audio frame data for mixing.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|audio_frame |IAudioFrame\* |See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IAudioFrame).<br><br><br>&nbsp;<br><br>* The audio sampling format must be S16. The data format within the audio buffer must be PCM, and its capacity should be `audioFrame.samples × audioFrame.channel × 2`.<br><br>* A specific sample rate and the number of channels must be specified; it is not supported to set them to automatic. |


**Return Value**


* 0: Success.

* < 0: Failed.


**Notes**


* Before calling this method, the raw audio data mixing must be enabled through [openWithCustomSource](https://docs.byteplus.com/en/docs/12/25049#IMediaPlayer-openwithcustomsource).

* Suggestions: Before pushing data for the first time, please cache a certain amount of data (like 200 ms) on the application side, and then push it at once. Schedule subsequent push operation every 10 ms with audio data of 10 ms.

* To pause the playback, just pause the push.

    &nbsp;


<span id="seteventhandler"></span>
### setEventHandler

```cpp
virtual int setEventHandler(IMediaPlayerEventHandler* handler) = 0;
 };
```


Set the event handler.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|handler |IMediaPlayerEventHandler\* |See [IMediaPlayerEventHandler](https://docs.byteplus.com/en/docs/12/docs-85517#IMediaPlayerEventHandler). |


**Return Value**


* 0: Success.

* < 0: Failed.

    &nbsp;


<span id="iaudioeffectplayer"></span>
# IAudioEffectPlayer

```cpp
class bytertc::IAudioEffectPlayer
```


> Available since 3.53


Audio effect player

Call [setEventHandler](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-seteventhandler) to set the callback handler to receive related callbacks.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|IAudioEffectPlayer |[IAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-iaudioeffectplayer) |
|virtual |[~IAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-~iaudioeffectplayer) |
|virtual int |[start](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-start) |
|virtual int |[stop](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-stop) |
|virtual int |[stopAll](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-stopall) |
|virtual int |[preload](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-preload) |
|virtual int |[unload](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-unload) |
|virtual int |[unloadAll](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-unloadall) |
|virtual int |[pause](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-pause) |
|virtual int |[pauseAll](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-pauseall) |
|virtual int |[resume](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-resume) |
|virtual int |[resumeAll](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-resumeall) |
|virtual int |[setPosition](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-setposition) |
|virtual int |[getPosition](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-getposition) |
|virtual int |[setVolume](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-setvolume) |
|virtual int |[setVolumeAll](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-setvolumeall) |
|virtual int |[getVolume](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-getvolume) |
|virtual int |[getDuration](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-getduration) |
|virtual int |[setEventHandler](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-seteventhandler) |


<span id="instructions"></span>
## Instructions

<span id="IAudioEffectPlayer-iaudioeffectplayer"></span>
### IAudioEffectPlayer

```cpp
IAudioEffectPlayer(){}
```


<span id="IAudioEffectPlayer-~iaudioeffectplayer"></span>
### ~IAudioEffectPlayer

```cpp
virtual ~IAudioEffectPlayer() {}
```


<span id="IAudioEffectPlayer-start"></span>
### start

```cpp
virtual int start(
    int effect_id,
    const char* file_path,
    const AudioEffectPlayerConfig& config
) = 0;
```


Starts to play the audio effect file.

This API can be called multiple times with different IDs and filepaths for multiple effects at the same time.

**Input Parameters**


|Audio effect file paths.<br><br>&nbsp;<br><br>URL of online file, URI of local file, or full path to the local file are supported. For URL of online file, only the https protocol is supported.<br><br>&nbsp;<br><br>Recommended sample rate for audio effect files: 8KHz、16KHz、22.05KHz、44.1KHz、48KHz.<br><br>&nbsp;<br><br>Local audio effect file formats supported by different platforms:<br><br>&nbsp;<br><br>&nbsp;<br><br>&nbsp;<br><br>&nbsp;<br><br>Online audio effect file formats supported by different platforms.<br><br>&nbsp;<br><br>&nbsp;<br><br> | | |
|---|---|---|
|config |const AudioEffectPlayerConfig& |See [AudioEffectPlayerConfig](https://docs.byteplus.com/en/docs/12/docs-85519#AudioEffectPlayerConfig). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* If the file has been loaded into memory via [preload](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-preload), make sure that the ID here is the same as the ID set by [preload](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-preload).

* After starting to play an audio effect file, you can call the [stop](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-stop) API to stop playing the audio effect file.

    &nbsp;


<span id="stop"></span>
### stop

```cpp
virtual int stop(int effect_id) = 0;
```


Stops the playback of audio effect files.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|effect_id |int |Audio effect ID |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* After calling the [start](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-start) API to start playing the audio effect file, you can call this API to stop playing the audio effect file.

* After calling this API to stop playing an audio effect file, the audio effect file will be unloaded automatically.

    &nbsp;


<span id="stopall"></span>
### stopAll

```cpp
virtual int stopAll() = 0;
```


Stops playback of all audio effect files.

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* After calling [start](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-start) to start playing audio effect files, you can call this API to stop playing all audio effect files.

* After calling this API to stop playing all audio effect files, the audio effect files will be unloaded automatically.

    &nbsp;


<span id="preload"></span>
### preload

```cpp
virtual int preload(
    int effect_id,
    const char* file_path
) = 0;
```


Preloads specified music files into memory to avoid repeated loading when playing the same file frequently and reduce CPU usage.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|effect_id |int |Audio effect ID。Used for identifying the audio effect. Please ensure that the audio effect ID is unique.<br><br>&nbsp;<br><br>If this API is called repeatedly with the same ID, the later one will overwrite the previous one.<br><br>&nbsp;<br><br>If you call [start](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-start) first and then call this API with the same ID, the SDK will stop the previous effect and then load the next one, and you will receive [onAudioEffectPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IAudioEffectPlayerEventHandler-onaudioeffectplayerstatechanged).<br><br>&nbsp;<br><br>After calling this API to preload A.mp3, if you need to call [start](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-start) to play B.mp3 with the same ID, please call [unload](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-unload) to unload A.mp3 first, otherwise SDK will report an error AUDIO_MIXING_ERROR_LOAD_CONFLICT. |
|file_path |const char\* |The filepath of effect file. URI of local file.<br><br>&nbsp;<br><br>The length of the pre\-loaded file must not exceed 20s.<br><br>&nbsp;<br><br>Audio effect file formats supported are the same as [start](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-start). |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* This API just preloads the specified audio effect file, and only calls the [start](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-start) API to start playing the specified audio effect file.

* The specified audio effect file preloaded by calling this API can be unloaded by [unload](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-unload).

    &nbsp;


<span id="unload"></span>
### unload

```cpp
virtual int unload(int effect_id) = 0;
```


Unloads the specified audio effect file.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|effect_id |int |Audio effect ID |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**

Call this API after [start](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-start) or [preload](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-preload).

<span id="IAudioEffectPlayer-unloadall"></span>
### unloadAll

```cpp
virtual int unloadAll() = 0;
```


Unloads all audio effect files.

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.

    &nbsp;


<span id="pause"></span>
### pause

```cpp
virtual int pause(int effect_id) = 0;
```


Pauses the playback of audio effect files.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|effect_id |int |Audio effect ID |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* After calling the [start](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-start) API to start playing the audio effect file, you can pause the audio effect file by calling this API.

* After calling this API to pause the audio effect file, you can call the [resume](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-resume) API to resume playback.

    &nbsp;


<span id="pauseall"></span>
### pauseAll

```cpp
virtual int pauseAll() = 0;
```


Pauses the Playback of all audio effect files.

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* After calling the [start](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-start) API to start playing audio effect files, you can pause playing all audio effect files by calling this API.

* After calling this API to pause the playback of all audio effect files, you can call the [resumeAll](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-resumeall) API to resume all playback.

    &nbsp;


<span id="resume"></span>
### resume

```cpp
virtual int resume(int effect_id) = 0;
```


Resumes the playback of audio effect files.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|effect_id |int |Audio effect ID |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**

After calling the [pause](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-pause) API to pause the audio effect file, you can resume playback by calling this API.

<span id="IAudioEffectPlayer-resumeall"></span>
### resumeAll

```cpp
virtual int resumeAll() = 0;
```


Resumes the playback of all audio effect files.

**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**

After calling the [pauseAll](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-pauseall) API to pause all the audio effect files being played, you can resume playback by calling this API.

<span id="IAudioEffectPlayer-setposition"></span>
### setPosition

```cpp
virtual int setPosition(
    int effect_id,
    int pos
) = 0;
```


Sets the start position of the audio effect file.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|effect_id |int |Audio effect ID |
|pos |int |The starting playback position of the audio effect file in milliseconds.<br><br>&nbsp;<br><br>You can get the total duration of the audio effect file by calling [getDuration](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-getduration), the value of pos should be less than the total duration of the audio effect file. |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**


* When playing online files, calling this API may cause a delay in playback.

* Call this API after [start](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-start).

    &nbsp;


<span id="getposition"></span>
### getPosition

```cpp
virtual int getPosition(int effect_id) = 0;
```


Gets the current position of audio effect file playback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|effect_id |int |Audio effect ID |


**Return Value**


* \>0: Success, the current progress of audio effect file playback in milliseconds.

* < 0: Failure.


**Notes**


* When playing online files, calling this API may cause a delay in playback.

* Call this API after [start](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-start).

    &nbsp;


<span id="setvolume"></span>
### setVolume

```cpp
virtual int setVolume(
    int effect_id,
    int volume
) = 0;
```


Adjusts the volume level of a specified audio effect, including audio effect file and PCM effect.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|effect_id |int |Audio effect ID |
|volume |int |The ratio of the volume to the original volume in % with overflow protection. The range is `[0, 400]` and the recommended range is `[0, 100]`. |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**

Call this API after [start](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-start).

<span id="IAudioEffectPlayer-setvolumeall"></span>
### setVolumeAll

```cpp
virtual int setVolumeAll(int volume) = 0;
```


Sets the volume of all audio effect, including audio effect files and PCM effects.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|volume |int |The ratio of the volume to the original volume in % with overflow protection. The range is `[0, 400]` and the recommended range is `[0, 100]`. |


**Return Value**


* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-85519#ReturnStatus) for more details.


**Notes**

This API has a lower priority than [setVolume](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-setvolume), i.e. the volume of the audio effect set by [setVolume](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-setvolume) is not affected by this API.

<span id="IAudioEffectPlayer-getvolume"></span>
### getVolume

```cpp
virtual int getVolume(int effect_id) = 0;
```


Gets the current volume.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|effect_id |int |Audio effect ID |


**Return Value**


* \>0: Success, the current volume value.

* < 0: Failed.


**Notes**

Call this API after [start](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-start).

<span id="IAudioEffectPlayer-getduration"></span>
### getDuration

```cpp
virtual int getDuration(int effect_id) = 0;
```


Get the duration of the audio effect file.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|effect_id |int |Audio effect ID |


**Return Value**


* \>0: Success, the duration of the audio effect file in milliseconds.

* < 0: failed.


**Notes**

Call this API after [start](https://docs.byteplus.com/en/docs/12/25049#IAudioEffectPlayer-start).

<span id="IAudioEffectPlayer-seteventhandler"></span>
### setEventHandler

```cpp
virtual int setEventHandler(IAudioEffectPlayerEventHandler* handler) = 0;
```


Set the event handler.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|handler |IAudioEffectPlayerEventHandler\* |See [IAudioEffectPlayerEventHandler](https://docs.byteplus.com/en/docs/12/docs-85517#IAudioEffectPlayerEventHandler). |


**Return Value**


* 0: Success.

* < 0: Failed.

    &nbsp;


<span id="ivideoprocessor"></span>
# IVideoProcessor

```cpp
class bytertc::IVideoProcessor
```


Video processor

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual IVideoFrame\* |[processVideoFrame](https://docs.byteplus.com/en/docs/12/25049#IVideoProcessor-processvideoframe) |


<span id="instructions"></span>
## Instructions

<span id="IVideoProcessor-processvideoframe"></span>
### processVideoFrame

```cpp
virtual IVideoFrame* processVideoFrame(IVideoFrame* src_frame) = 0;
```


Get RTC SDK acquired video frames obtained, according to the video pre\-processor [registerLocalVideoProcessor](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-registerlocalvideoprocessor) set, video pre\-processing, the final processed video frames to the RTC SDK for encoding transmission.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|src_frame |IVideoFrame\* |Video frames captured by the RTC SDK. See [IVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IVideoFrame). |


**Return Value**

The video frame after video preprocessing is returned to the RTC SDK for encoding and transmission. See [IVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85519#IVideoFrame).

**Notes**


* Before video preprocessing, you need to call [registerLocalVideoProcessor](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-registerlocalvideoprocessor) to set up the video preprocessor.

* If you need to cancel the video preprocessing, you can set the video preprocessor to nullptr.

* When implementing `processVideoFrame`, you can directly modify the buffer of src_frame, call `addRef` to add the src_frame reference count by one, and return the modified `src_frame`, or you can also create a new video frame and return it.

* For the video frame returned by `processVideoFrame`, after consuming by the SDK layer, the SDK always calls the `releaseRef` method of this video frame.

    &nbsp;


<span id="iaudiodevicemanager"></span>
# IAudioDeviceManager

```cpp
class bytertc::IAudioDeviceManager
```


Audio device management

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual IAudioDeviceCollection\* |[enumerateAudioPlaybackDevices](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-enumerateaudioplaybackdevices) |
|virtual IAudioDeviceCollection\* |[enumerateAudioCaptureDevices](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-enumerateaudiocapturedevices) |
|virtual void |[followSystemPlaybackDevice](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-followsystemplaybackdevice) |
|virtual void |[followSystemCaptureDevice](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-followsystemcapturedevice) |
|virtual int |[setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-setaudioplaybackdevice) |
|virtual int |[setAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-setaudiocapturedevice) |
|virtual int |[setAudioPlaybackDeviceVolume](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-setaudioplaybackdevicevolume) |
|virtual int |[getAudioPlaybackDeviceVolume](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-getaudioplaybackdevicevolume) |
|virtual int |[setAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-setaudiocapturedevicevolume) |
|virtual int |[getAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-getaudiocapturedevicevolume) |
|virtual int |[setAudioPlaybackDeviceMute](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-setaudioplaybackdevicemute) |
|virtual int |[getAudioPlaybackDeviceMute](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-getaudioplaybackdevicemute) |
|virtual int |[setAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-setaudiocapturedevicemute) |
|virtual int |[getAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-getaudiocapturedevicemute) |
|virtual int |[getAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-getaudioplaybackdevice) |
|virtual int |[getAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-getaudiocapturedevice) |
|virtual int |[initAudioPlaybackDeviceForTest](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-initaudioplaybackdevicefortest) |
|virtual int |[initAudioCaptureDeviceForTest](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-initaudiocapturedevicefortest) |
|virtual int |[startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-startaudioplaybackdevicetest) |
|virtual int |[stopAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-stopaudioplaybackdevicetest) |


<span id="instructions"></span>
## Instructions

<span id="IAudioDeviceManager-enumerateaudioplaybackdevices"></span>
### enumerateAudioPlaybackDevices

```cpp
virtual IAudioDeviceCollection* enumerateAudioPlaybackDevices() = 0;
```


Get a list of the audio playback device. When the audio playback device changes, you will receive `onAudioMediaDeviceStateChanged` and you need to call this API again to get the new device list.

**Return Value**

A list of all audio playback devices. See [IAudioDeviceCollection](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceCollection).

If a time\-out occurs, it returns an empty list. By default, the time\-out duration is set to 10 seconds. We recommend to call this API once you get notification of `kMediaDeviceListUpdated` via [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onaudiodevicestatechanged).

**Notes**

When receiving [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onaudiodevicestatechanged) for device change, you can call this API to get the latest list of audio playback devices.

<span id="IAudioDeviceManager-enumerateaudiocapturedevices"></span>
### enumerateAudioCaptureDevices

```cpp
virtual IAudioDeviceCollection* enumerateAudioCaptureDevices() = 0;
```


Get a list of audio acquisition devices in the current system. If there are subsequent device changes, you need to call this interface again to get a new device list.

**Return Value**

An object that contains a list of all audio capture devices in the system. See [IAudioDeviceCollection](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceCollection).

If a time\-out occurs, it returns an empty list. By default, the time\-out duration is set to 10 seconds. We recommend to call this API once you get notification of `kMediaDeviceListUpdated` via [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onaudiodevicestatechanged).

**Notes**


* When receiving [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onaudiodevicestatechanged) for device change, you can call this API to get the latest list of audio playback devices.

* For Linux SDK: Only available in Client version, not available in Server version.

    &nbsp;


<span id="followsystemplaybackdevice"></span>
### followSystemPlaybackDevice

```cpp
virtual void followSystemPlaybackDevice(bool followed) = 0;
```


Set the audio playback device to follow the OS setting or not.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|followed |bool |* true: follow the OS setting. You can not call [setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-setaudioplaybackdevice) at the same time. The default value.<br><br>* false: do not follow the OS setting. You can call [setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-setaudioplaybackdevice) to set the audio playback device. |


<span id="IAudioDeviceManager-followsystemcapturedevice"></span>
### followSystemCaptureDevice

```cpp
virtual void followSystemCaptureDevice(bool followed) = 0;
```


Set the audio capture device to follow the OS setting or not.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|followed |bool |* true: follow the OS setting. You can not call [setAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-setaudiocapturedevice) at the same time. The default value.<br><br>* false: do not follow the OS setting. You can call [setAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-setaudiocapturedevice) to set the audio capture device. |


**Notes**

For Linux SDK: Only available in Client version, not available in Server version.

<span id="IAudioDeviceManager-setaudioplaybackdevice"></span>
### setAudioPlaybackDevice

```cpp
virtual int setAudioPlaybackDevice(const char device_id[MAX_DEVICE_ID_LENGTH]) = 0;
```


Sets the audio playback device.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|device_id |const char[MAX_DEVICE_ID_LENGTH] |Audio playback device's ID. You can get the ID by calling<br><br>&nbsp;<br><br>[enumerateAudioPlaybackDevices](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-enumerateaudioplaybackdevices). |


**Return Value**


* 0: Success

* < 0: Failure


**Notes**

After you call [followSystemPlaybackDevice](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-followsystemplaybackdevice) to set the audio playback device to follow the system setting, you cannot call this API to set the audio playback device.

<span id="IAudioDeviceManager-setaudiocapturedevice"></span>
### setAudioCaptureDevice

```cpp
virtual int setAudioCaptureDevice(const char device_id[MAX_DEVICE_ID_LENGTH]) = 0;
```


Set up audio capture devices.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|device_id |const char[MAX_DEVICE_ID_LENGTH] |Audio capture device ID, available through [enumerateAudioCaptureDevices](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-enumerateaudiocapturedevices). |


**Return Value**

Method call result


* 0: Success.

* < 0: failure


**Notes**


* After you call [followSystemCaptureDevice](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-followsystemcapturedevice) to set the audio playback device to follow the system setting, you cannot call this API to set the audio capture device.

* For Linux SDK: Only available in Client version, not available in Server version.

    &nbsp;


<span id="setaudioplaybackdevicevolume"></span>
### setAudioPlaybackDeviceVolume

```cpp
virtual int setAudioPlaybackDeviceVolume(unsigned int volume) = 0;
```


Set the current audio playback device volume

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|volume |unsigned int |Audio playback device volume, the value range is [0,255], the setting beyond this range is invalid.<br><br><br>&nbsp;<br><br>* [0,25] Is nearly silent;<br><br>* [25,75] Is low volume;<br><br>* [76,204] Is medium volume;<br><br>* [205,255] Is high volume. |


**Return Value**

Method call result


* 0: Success.

* < 0: failure

    &nbsp;


<span id="getaudioplaybackdevicevolume"></span>
### getAudioPlaybackDeviceVolume

```cpp
virtual int getAudioPlaybackDeviceVolume(unsigned int* volume) = 0;
```


Get the current audio playback device volume.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|volume |unsigned int\* |Audio playback device volume, the range should be within [0,255].<br><br><br>&nbsp;<br><br>* [0,25] Is nearly silent;<br><br>* [25,75] Is low volume;<br><br>* [76,204] Is medium volume;<br><br>* [205,255] Is high volume. |


**Return Value**

Method call result


* 0: Success.

* < 0: failure

    &nbsp;


<span id="setaudiocapturedevicevolume"></span>
### setAudioCaptureDeviceVolume

```cpp
virtual int setAudioCaptureDeviceVolume(unsigned int volume) = 0;
```


Set the current audio capture volume

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|volume |unsigned int |Audio capture volume, the value range is [0,255], the setting beyond this range is invalid.<br><br><br>&nbsp;<br><br>* [0,25] Is nearly silent;<br><br>* [25,75] Is low volume;<br><br>* [76,204] Is medium volume;<br><br>* [205,255] Is high volume. |


**Return Value**

Method call result


* 0: Success. The volume information returned by [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onlocalaudiopropertiesreport) will be changed according to this value.

* < 0: failure


**Notes**


* The setting will take effect after you unmute the device via [setAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-setaudiocapturedevicemute).

* For Linux SDK: Only available in Client version, not available in Server version.

    &nbsp;


<span id="getaudiocapturedevicevolume"></span>
### getAudioCaptureDeviceVolume

```cpp
virtual int getAudioCaptureDeviceVolume(unsigned int* volume) = 0;
```


Get the current audio capture volume.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|volume |unsigned int\* |Audio capture volume, the range is within [0,255].<br><br><br>&nbsp;<br><br>* [0,25] Is nearly silent;<br><br>* [25,75] Is low volume;<br><br>* [76,204] Is medium volume;<br><br>* [205,255] Is high volume. |


**Return Value**

Method call result


* 0: Success.

* < 0: failure


**Notes**

For Linux SDK: Only available in Client version, not available in Server version.

<span id="IAudioDeviceManager-setaudioplaybackdevicemute"></span>
### setAudioPlaybackDeviceMute

```cpp
virtual int setAudioPlaybackDeviceMute(bool mute) = 0;
```


Mute or Unmute the current audio playback device. The default state is speaking.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mute |bool |* true: Mute<br><br>* false: Speaking |


**Return Value**

Method call result


* 0: Success.

* < 0: failure

    &nbsp;


<span id="getaudioplaybackdevicemute"></span>
### getAudioPlaybackDeviceMute

```cpp
virtual int getAudioPlaybackDeviceMute(bool* mute) = 0;
```


Get the mute state of the current audio playback device.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mute |bool\* |* true: Mute<br><br>* false: Speaking |


**Return Value**

Method call result


* 0: Success.

* < 0: failure

    &nbsp;


<span id="setaudiocapturedevicemute"></span>
### setAudioCaptureDeviceMute

```cpp
virtual int setAudioCaptureDeviceMute(bool mute) = 0;
```


Mute or Unmute the current audio capture device. The default state is speaking.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mute |bool |* true: Mute<br><br>* false: Speaking |


**Return Value**

Method call result


* 0: Success.

* < 0: failure


**Notes**


* This method effluences all the audio input of the system. You can choose to mute the audio signal from the microphone that excludes the media player. Refer to [muteAudioCapture](https://docs.byteplus.com/en/docs/12/25049#IRTCEngine-muteaudiocapture).

   — When the audio device is muted, volume setting via [setAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-setaudiocapturedevicevolume) will be take effect once the device become unmuted.

* For Linux SDK: Only available in Client version, not available in Server version.

    &nbsp;


<span id="getaudiocapturedevicemute"></span>
### getAudioCaptureDeviceMute

```cpp
virtual int getAudioCaptureDeviceMute(bool* mute) = 0;
```


Get state of the audio capture device.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mute |bool\* |* true: Mute<br><br>* false: Speaking |


**Return Value**

Method call result


* 0: Success.

* < 0: failure


**Notes**

For Linux SDK: Only available in Client version, not available in Server version.

<span id="IAudioDeviceManager-getaudioplaybackdevice"></span>
### getAudioPlaybackDevice

```cpp
virtual int getAudioPlaybackDevice(char device_id[MAX_DEVICE_ID_LENGTH]) = 0;
```


Gets the current audio playback device ID.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|device_id |char[MAX_DEVICE_ID_LENGTH] |Audio playback device ID |


**Return Value**

Method call result


* 0: Success.

* < 0: failure

    &nbsp;


<span id="getaudiocapturedevice"></span>
### getAudioCaptureDevice

```cpp
virtual int getAudioCaptureDevice(char device_id[MAX_DEVICE_ID_LENGTH]) = 0;
```


Gets the current audio capture device ID.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|device_id |char[MAX_DEVICE_ID_LENGTH] |audio capture device ID. You should allocate and free memory according to the MAX_DEVICE_ID_LENGTH size. |


**Return Value**

Method call result


* 0: Success.

* < 0: failure


**Notes**

For Linux SDK: Only available in Client version, not available in Server version.

<span id="IAudioDeviceManager-initaudioplaybackdevicefortest"></span>
### initAudioPlaybackDeviceForTest

```cpp
virtual int initAudioPlaybackDeviceForTest(const char device_id[MAX_DEVICE_ID_LENGTH]) = 0;
```


Try to initialize the audio playback device, and you can detect abnormal problems such as the device does not exist, permissions are denied/disabled, etc.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|device_id |const char[MAX_DEVICE_ID_LENGTH] |Device index number |


**Return Value**

Device status error code


* 0: device detection result is normal

* \-1: The interface status is incorrect, for example, the interface is called for detection after the acquisition is started normally

* \-2: The acquisition device does not have microphone permission, and attempts to initialize the device fail

* \-3: The device does not exist, there is currently no device or return when the device is removed

* \-4: Device audio format not supported

* \-5: Error for other reasons


**Notes**


1. This interface needs to be called before entering the room;

2. Successful detection does not necessarily mean that the device can be started successfully. It may also fail to start due to the device being monopolized by other application processes, or CPU/memory shortage.

    &nbsp;


<span id="initaudiocapturedevicefortest"></span>
### initAudioCaptureDeviceForTest

```cpp
virtual int initAudioCaptureDeviceForTest(const char device_id[MAX_DEVICE_ID_LENGTH]) = 0;
```


Try to initialize the audio capture device, which can detect abnormal problems such as the device does not exist, permissions are denied/disabled, etc.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|device_id |const char[MAX_DEVICE_ID_LENGTH] |Device index |


**Return Value**

Device status error code


* 0: device detection result is normal

* \-1: The interface status is incorrect, for example, the interface is called for detection after the acquisition is started normally

* \-2: The acquisition device does not have microphone permission, and attempts to initialize the device fail

* \-3: The device does not exist, there is currently no device or return when the device is removed

* \-4: Device audio format not supported

* \-5: Error for other reasons


**Notes**


* This interface needs to be called before entering the room;

* Successful detection does not necessarily mean that the device can be started successfully. It may also fail to start due to the device being monopolized by other application processes, or CPU/memory shortage.

* For Linux SDK: Only available in Client version, not available in Server version.

    &nbsp;


<span id="startaudioplaybackdevicetest"></span>
### startAudioPlaybackDeviceTest

```cpp
virtual int startAudioPlaybackDeviceTest(
    const char* test_audio_file_path,
    int indication_interval
) = 0;
```


Start the playback test for the local audio device. RTC will start playing the audio file specified. And RTC will notify the audio volume via the `onAudioPlaybackDeviceTestVolume` periodically.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|test_audio_file_path |const char\* |Specify the path of the audio file for the playback test, including \*.mp3, \*.aac, \*.m4a, \*.3gp, and \*.wav. |
|indication_interval |int |The time interval between each callback in milliseconds. We recommend setting it to 200 ms. The minimal value is 10 ms. |


**Return Value**


* 0: Success

* < 0: Failure


**Notes**


* You can call this API whether the user is in the room.

* Call [stopAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-stopaudioplaybackdevicetest) to stop the playback test before moving on to the other device tests.

    &nbsp;


<span id="stopaudioplaybackdevicetest"></span>
### stopAudioPlaybackDeviceTest

```cpp
virtual int stopAudioPlaybackDeviceTest() = 0;
```


Stop the playback test for the local audio device.

**Return Value**

Result


* 0: Success

* < 0: Failure


**Notes**

Call this API to stop the playback test started by calling [startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceManager-startaudioplaybackdevicetest) before moving on to the other device tests.

<span id="IVideoDeviceManager"></span>
# IVideoDeviceManager

```cpp
class bytertc::IVideoDeviceManager
```


Mainly used to enumerate and set up video capture devices

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual IVideoDeviceCollection\* |[enumerateVideoCaptureDevices](https://docs.byteplus.com/en/docs/12/25049#IVideoDeviceManager-enumeratevideocapturedevices) |
|virtual int |[setVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/25049#IVideoDeviceManager-setvideocapturedevice) |
|virtual int |[getVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/25049#IVideoDeviceManager-getvideocapturedevice) |


<span id="instructions"></span>
## Instructions

<span id="IVideoDeviceManager-enumeratevideocapturedevices"></span>
### enumerateVideoCaptureDevices

```cpp
virtual IVideoDeviceCollection* enumerateVideoCaptureDevices() = 0;
```


Get a list of video capture devices in the current system.

**Return Value**

Contains a list of all video capture devices in the system. See [IVideoDeviceCollection](https://docs.byteplus.com/en/docs/12/25049#IVideoDeviceCollection).

If a time\-out occurs, it returns an empty list. By default, the time\-out duration is set to 10 seconds. We recommend to call this API once you get notification of `kMediaDeviceListUpdated` via [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onvideodevicestatechanged).

**Notes**

When receiving [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onvideodevicestatechanged) for device change, you can call this API to get the latest list of audio playback devices.

<span id="IVideoDeviceManager-setvideocapturedevice"></span>
### setVideoCaptureDevice

```cpp
virtual int setVideoCaptureDevice(const char device_id[MAX_DEVICE_ID_LENGTH]) = 0;
```


Set the current video capture device

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|device_id |const char[MAX_DEVICE_ID_LENGTH] |Video device ID, which can be obtained through [enumerateVideoCaptureDevices](https://docs.byteplus.com/en/docs/12/25049#IVideoDeviceManager-enumeratevideocapturedevices) |


**Return Value**


* 0: Success.

   +! 0: failure

    &nbsp;


<span id="getvideocapturedevice"></span>
### getVideoCaptureDevice

```cpp
virtual int getVideoCaptureDevice(char device_id[MAX_DEVICE_ID_LENGTH]) = 0;
```


Get the video capture device information currently used by the SDK

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|device_id |char[MAX_DEVICE_ID_LENGTH] |Device ID. The parameter is both input parameter and output parameter. |


**Return Value**


* 0: Success.

   +! 0: failure

    &nbsp;


<span id="idevicecollection"></span>
# IDeviceCollection

```cpp
class bytertc::IDeviceCollection
```


> Deprecated since 3.45 and will be deleted in 3.51, use [IAudioDeviceCollection](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceCollection) and [IVideoDeviceCollection](https://docs.byteplus.com/en/docs/12/25049#IVideoDeviceCollection) instead.


Audio & video equipment related information

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|virtual int |[getCount](https://docs.byteplus.com/en/docs/12/25049#IDeviceCollection-getcount) |
|virtual int |[getDevice](https://docs.byteplus.com/en/docs/12/25049#IDeviceCollection-getdevice) |
|virtual void |[release](https://docs.byteplus.com/en/docs/12/25049#IDeviceCollection-release) |


<span id="instructions"></span>
## Instructions

<span id="IDeviceCollection-getcount"></span>
### getCount

```cpp
virtual int getCount() = 0;
```


Get the number of audio & video devices in the current system

**Return Value**

Number of audio & video devices

<span id="IDeviceCollection-getdevice"></span>
### getDevice

```cpp
virtual int getDevice(
    int index,
    char device_name[MAX_DEVICE_ID_LENGTH],
    char device_id[MAX_DEVICE_ID_LENGTH]
) = 0;
```


Get the information of the specific audio device. You can get the device information by index, device name, or device ID.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|index |int |Device index number, starting from 0, note that it must be less than the return value of [getCount](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceCollection-getcount). |
|device_name |char[MAX_DEVICE_ID_LENGTH] |device name |
|device_id |char[MAX_DEVICE_ID_LENGTH] |device ID |


**Return Value**


* 0: Success.

   +! 0: failure

    &nbsp;


<span id="release"></span>
### release

```cpp
virtual void release() = 0;
```


Releases the resources occupied by the current [IDeviceCollection](https://docs.byteplus.com/en/docs/12/25049#IAudioDeviceCollection) object.

**Notes**

This method should be called to release related resources when you do not need to return a list of audio & video device related information.
