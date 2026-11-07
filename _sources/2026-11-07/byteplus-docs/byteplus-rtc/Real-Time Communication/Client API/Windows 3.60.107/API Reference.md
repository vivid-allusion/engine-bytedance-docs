---
title: "API Reference"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70095"
---

# IVideoEffect

```cpp
class bytertc::IVideoEffect
```

Advanced video effects. See [integration guide](https://docs.byteplus.com/byteplus-rtc/docs/114717).

## Member Functions

|Return |Name |
|---|---|
|virtual |[~IVideoEffect](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-~ivideoeffect) |
|virtual int |[initCVResource](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-initcvresource) |
|virtual int |[getAuthMessage](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-getauthmessage) |
|virtual int |[freeAuthMessage](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-freeauthmessage) |
|virtual int |[enableVideoEffect](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-enablevideoeffect) |
|virtual int |[disableVideoEffect](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-disablevideoeffect) |
|virtual int |[setEffectNodes](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-seteffectnodes) |
|virtual int |[updateEffectNode](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-updateeffectnode) |
|virtual int |[setColorFilter](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-setcolorfilter) |
|virtual int |[setColorFilterIntensity](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-setcolorfilterintensity) |
|virtual int |[enableVirtualBackground](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-enablevirtualbackground) |
|virtual int |[disableVirtualBackground](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-disablevirtualbackground) |
|virtual int |[enableFaceDetection](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-enablefacedetection) |
|virtual int |[disableFaceDetection](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-disablefacedetection) |

## Instructions

### ~IVideoEffect

```cpp
virtual ~IVideoEffect() = default;
```

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

* After obtaining authorization messages through this API, you must refer to [Online License Guide](https://docs.byteplus.com/en/effects/docs/windows-license-guide) to implement the business logic of obtaining online licenses by yourself. After obtaining the license, you must call [initCVResource](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-initcvresource) to confirm that the license is valid. Then you can use the CV function.

* After obtaining the authorization message, call [freeAuthMessage](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-freeauthmessage) to free memory.

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

* You must call [initCVResource](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-initcvresource) before calling this API.

* This API does not enable video effects directly, you must call [setEffectNodes](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-seteffectnodes) or [setColorFilter](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-setcolorfilter) next.

* Call [disableVideoEffect](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-disablevideoeffect) to turn off video effects.

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

Call [enableVideoEffect](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-enablevideoeffect) to enable video effects.

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
|effect_node_paths |const char\*\* |Array of effect material package paths.<br><br> <br><br>To remove the current video effect, set it to null. |
|node_num |int |Number of effect material packages. |

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

**Notes**

You must call [enableVideoEffect](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-enablevideoeffect) before calling this API.

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

Call [setColorFilterIntensity](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-setcolorfilterintensity) to set the intensity of the color filter enabled. Set the intensity to 0 to turn off color filter.

### setColorFilterIntensity

```cpp
virtual int setColorFilterIntensity(float intensity) = 0;
```

Sets the intensity of the color filter enabled.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|intensity |float |Filter intensity. The value range [0,1] is set to be invalid when the range is exceeded.<br><br> <br><br>Set the intensity to 0 to turn off color filter. |

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

### enableVirtualBackground

```cpp
virtual int enableVirtualBackground(
    const char* background_sticker_path,
    const VirtualBackgroundSource& source
) = 0;
```

Sets the original background to a specified image or a solid color.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|background_sticker_path |const char\* |The absolute path of virtual background effects. |
|source |const VirtualBackgroundSource& |Virtual background source. See [VirtualBackgroundSource](https://docs.byteplus.com/en/docs/12/docs-70098#VirtualBackgroundSource). |

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

**Notes**

* You must call [initCVResource](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-initcvresource) before calling this API.

* Call [disableVirtualBackground](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-disablevirtualbackground) to turn off the virtual background.

### disableVirtualBackground

```cpp
virtual int disableVirtualBackground() = 0;
```

Turns off the virtual background.

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

**Notes**

After calling [enableVirtualBackground](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-enablevirtualbackground) to enable the virtual background function, you can call this API to turn it off.

### enableFaceDetection

```cpp
virtual int enableFaceDetection(
    IFaceDetectionObserver* observer,
    unsigned int interval_ms,
    const char* face_model_path
) = 0;
```

Starts face detection and registers the observer for the result.

With this observer, you will receive [onFaceDetectResult](https://docs.byteplus.com/en/docs/12/docs-70096#IFaceDetectionObserver-onfacedetectresult) periodically.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|observer |IFaceDetectionObserver\* |See [IFaceDetectionObserver](https://docs.byteplus.com/en/docs/12/docs-70096#IFaceDetectionObserver). |
|interval_ms |unsigned int |The minimum time interval between two callbacks in milliseconds. The value should be greater than 0. The actual time interval is between interval_ms and interval_ms+the time slot of a captured video frame. |
|face_model_path |const char\* |The absolute path of the face detection algorithm file. Typically it is the tt_face_vXXX.model file in the ttfacemodel folder. |

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* \-1004: Initializing. This function will be available when the initialization is completed.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

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

# IRangeAudio

```cpp
class bytertc::IRangeAudio
```

Range audio instance

## Member Functions

|Return |Name |
|---|---|
|virtual void |[enableRangeAudio](https://docs.byteplus.com/en/docs/12/14184#IRangeAudio-enablerangeaudio) |
|virtual int |[updateReceiveRange](https://docs.byteplus.com/en/docs/12/14184#IRangeAudio-updatereceiverange) |
|virtual int |[updatePosition](https://docs.byteplus.com/en/docs/12/14184#IRangeAudio-updateposition) |
|virtual int |[setAttenuationModel](https://docs.byteplus.com/en/docs/12/14184#IRangeAudio-setattenuationmodel) |
|virtual void |[setNoAttenuationFlags](https://docs.byteplus.com/en/docs/12/14184#IRangeAudio-setnoattenuationflags) |

## Instructions

### enableRangeAudio

```cpp
virtual void enableRangeAudio(bool enable) = 0;
```

Enable/disable the range audio function.

Range audio means that within a certain range in a same RTC room, the audio volume of the remote user received by the local user will be amplified/attenuated as the remote user moves closer/away. The audio coming from out of the range cannot be heard. See [updateReceiveRange](https://docs.byteplus.com/en/docs/12/14184#IRangeAudio-updatereceiverange) to set audio receiving range.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |bool |Whether to enable audio range function:<br><br><br> <br><br>* true: Enable<br><br>* false: Disable（Defaulting setting） |

**Notes**

You can call this API anytime before or after entering a room. To ensure a smooth switch to the range audio mode after entering the room, you need to call [updatePosition](https://docs.byteplus.com/en/docs/12/14184#IRangeAudio-updateposition) before this API to set your own position coordinates, and then enable the range audio function.

### updateReceiveRange

```cpp
virtual int updateReceiveRange(const ReceiveRange&range) = 0;
```

Updates the audio receiving range for the local user.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|range |const ReceiveRange& |Audio receiving range, see [ReceiveRange](https://docs.byteplus.com/en/docs/12/docs-70098#ReceiveRange). |

**Return Value**

API call result:

* 0: Success

* !0: Failure

### updatePosition

```cpp
virtual int updatePosition(const Position&pos) = 0;
```

Updates the coordinate of the local user's position in the rectangular coordinate system in the current room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|pos |const Position& |3D coordinate values, the default value is [0, 0, 0], see [Position](https://docs.byteplus.com/en/docs/12/docs-70098#Position) |

**Return Value**

API call result:

* 0: Success

* !0: Failure

**Notes**

* After calling this API, you should call [enableRangeAudio](https://docs.byteplus.com/en/docs/12/14184#IRangeAudio-enablerangeaudio) to enable range audio function to actually enjoy the range audio effect.

### setAttenuationModel

```cpp
virtual int setAttenuationModel(
    AttenuationType type,
    float coefficient
) = 0;
```

Set the volume roll\-off mode that a 3D sound has in an audio source when using the Range Audio feature.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |AttenuationType |Volume roll\-off mode. It is linear roll\-off mode by default. Refer to [AttenuationType](https://docs.byteplus.com/en/docs/12/docs-70098#AttenuationType) for more details. |
|coefficient |float |Coefficient for the exponential roll\-off mode. The default value is 1. It ranges [0.1,100]. We recommended to set it to `50`. The volume roll\-off speed gets faster as this value increases. |

**Return Value**

Result of the call

* `0`: Success

* `-1`: Failure because of calling this API before the user has joined a room or before enabling the Range Audio feature by calling [enableRangeAudio](https://docs.byteplus.com/en/docs/12/14184#IRangeAudio-enablerangeaudio).

**Notes**

Call [updateReceiveRange](https://docs.byteplus.com/en/docs/12/14184#IRangeAudio-updatereceiverange) to set the range outside which the volume of the sound does not attenuate.

### setNoAttenuationFlags

```cpp
virtual void setNoAttenuationFlags(
    const char** flags,
    int len
) = 0;
```

Set the flags to mark the user groups, within which the users talk without attenuation.

In the RTC room, if the flags of the users intersect with each other, the users talk without attenuation.

For example, the user is a member of multiple teams, and teammates of the same team talk without attenuation. You can set the flag for each team, and include the flags of the user's teams in the user's flags.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|flags |const char\*\* |Array of flags. |
|len |int |The length of the array of flags. |

# IRTCEngine

```cpp
class bytertc::IRTCEngine
```

Engine API

## Static Functions

|Return |Name |
|---|---|
|BYTERTC_STATIC_API IRTCEngine\* |[createRTCEngine](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-creatertcengine) |
|BYTERTC_STATIC_API void |[destroyRTCEngine](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-destroyrtcengine) |
|BYTERTC_STATIC_API const char\* |[getSDKVersion](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-getsdkversion) |
|BYTERTC_STATIC_API int |[setLogConfig](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setlogconfig) |

## Member Functions

|Return |Name |
|---|---|
|virtual int |[muteAudioCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-muteaudiocapture) |
|virtual int |[muteScreenAudioCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-mutescreenaudiocapture) |
|virtual int |[setCaptureVolume](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setcapturevolume) |
|virtual int |[setScreenCaptureVolume](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setscreencapturevolume) |
|virtual int |[setPlaybackVolume](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setplaybackvolume) |
|virtual int |[setEarMonitorMode](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setearmonitormode) |
|virtual int |[setEarMonitorMode](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setearmonitormode-2) |
|virtual int |[setEarMonitorVolume](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setearmonitorvolume) |
|virtual int |[startAudioCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startaudiocapture) |
|virtual int |[stopAudioCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stopaudiocapture) |
|virtual int |[setVoiceChangerType](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvoicechangertype) |
|virtual int |[setVoiceReverbType](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvoicereverbtype) |
|virtual int |[setLocalVoiceEqualization](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setlocalvoiceequalization) |
|virtual int |[setLocalVoiceReverbParam](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setlocalvoicereverbparam) |
|virtual int |[enableLocalVoiceReverb](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-enablelocalvoicereverb) |
|virtual int |[setAudioProfile](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setaudioprofile) |
|virtual int |[setAnsMode](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setansmode) |
|virtual int |[enableAGC](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-enableagc) |
|virtual int |[setAudioSourceType](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setaudiosourcetype) |
|virtual int |[setAudioRenderType](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setaudiorendertype) |
|virtual int |[pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-pushexternalaudioframe) |
|virtual int |[pullExternalAudioFrame](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-pullexternalaudioframe) |
|virtual int |[pushReferenceAudioPCMData](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-pushreferenceaudiopcmdata) |
|virtual int |[startVideoCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startvideocapture) |
|virtual int |[stopVideoCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stopvideocapture) |
|virtual int |[setVideoCaptureConfig](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvideocaptureconfig) |
|virtual int |[setVideoCaptureRotation](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvideocapturerotation) |
|virtual int |[setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvideoencoderconfig) |
|virtual int |[setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setlocalsimulcastmode) |
|virtual int |[setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setlocalsimulcastmode-2) |
|virtual int |[enableAlphaChannelVideoEncode](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-enablealphachannelvideoencode) |
|virtual int |[disableAlphaChannelVideoEncode](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-disablealphachannelvideoencode) |
|virtual int |[setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setlocalvideocanvas) |
|virtual int |[updateLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-updatelocalvideocanvas) |
|virtual int |[setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setremotevideocanvas) |
|virtual int |[updateRemoteStreamVideoCanvas](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-updateremotestreamvideocanvas-2) |
|virtual int |[setLocalVideoSink](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setlocalvideosink-2) |
|virtual int |[setRemoteVideoSink](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setremotevideosink-2) |
|virtual int |[updateScreenCaptureRegion](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-updatescreencaptureregion) |
|virtual int |[startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startscreenvideocapture) |
|virtual int |[stopScreenVideoCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stopscreenvideocapture) |
|virtual int |[updateScreenCaptureHighlightConfig](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-updatescreencapturehighlightconfig) |
|virtual int |[updateScreenCaptureMouseCursor](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-updatescreencapturemousecursor) |
|virtual int |[updateScreenCaptureFilterConfig](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-updatescreencapturefilterconfig) |
|virtual IScreenCaptureSourceList\* |[getScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-getscreencapturesourcelist) |
|virtual IVideoFrame\* |[getThumbnail](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-getthumbnail) |
|virtual IVideoFrame\* |[getWindowAppIcon](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-getwindowappicon) |
|virtual int |[setVideoSourceType](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvideosourcetype) |
|virtual int |[pushExternalVideoFrame](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-pushexternalvideoframe) |
|virtual IRTCRoom\* |[createRTCRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-creatertcroom) |
|virtual IRTSRoom\* |[createRTSRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-creatertsroom) |
|virtual int |[setPublishFallbackOption](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setpublishfallbackoption) |
|virtual int |[setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setsubscribefallbackoption) |
|virtual int |[setRemoteUserPriority](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setremoteuserpriority) |
|virtual int |[setBusinessId](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setbusinessid) |
|virtual int |[setLocalVideoMirrorType](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setlocalvideomirrortype) |
|virtual int |[setRemoteVideoMirrorType](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setremotevideomirrortype) |
|virtual IVideoEffect\* |[getVideoEffectInterface](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-getvideoeffectinterface) |
|virtual int |[enableEffectBeauty](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-enableeffectbeauty) |
|virtual int |[setBeautyIntensity](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setbeautyintensity) |
|virtual int |[setEncryptInfo](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setencryptinfo) |
|virtual int |[setCustomizeEncryptHandler](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setcustomizeencrypthandler) |
|virtual int |[enableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-enableaudioframecallback) |
|virtual int |[disableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-disableaudioframecallback) |
|virtual int |[registerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-registeraudioframeobserver) |
|virtual int |[registerAudioProcessor](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-registeraudioprocessor) |
|virtual int |[enableAudioProcessor](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-enableaudioprocessor) |
|virtual int |[disableAudioProcessor](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-disableaudioprocessor) |
|virtual int |[registerLocalVideoProcessor](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-registerlocalvideoprocessor) |
|virtual int |[setVideoDigitalZoomConfig](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvideodigitalzoomconfig) |
|virtual int |[setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvideodigitalzoomcontrol) |
|virtual int |[startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startvideodigitalzoomcontrol) |
|virtual int |[stopVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stopvideodigitalzoomcontrol) |
|virtual int |[sendSEIMessage](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-sendseimessage) |
|virtual int |[sendLivePushSEIMessage](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-sendlivepushseimessage) |
|virtual IVideoDeviceManager\* |[getVideoDeviceManager](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-getvideodevicemanager) |
|virtual IAudioDeviceManager\* |[getAudioDeviceManager](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-getaudiodevicemanager) |
|virtual int |[startFileRecording](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startfilerecording) |
|virtual int |[stopFileRecording](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stopfilerecording) |
|virtual int |[startAudioRecording](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startaudiorecording) |
|virtual int |[stopAudioRecording](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stopaudiorecording) |
|virtual int |[enableExternalSoundCard](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-enableexternalsoundcard) |
|virtual int |[setRuntimeParameters](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setruntimeparameters) |
|virtual int |[feedback](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-feedback) |
|virtual IAudioEffectPlayer\* |[getAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-getaudioeffectplayer) |
|virtual IMediaPlayer\* |[getMediaPlayer](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-getmediaplayer) |
|virtual int |[login](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-login) |
|virtual int |[logout](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-logout) |
|virtual int |[updateLoginToken](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-updatelogintoken) |
|virtual int |[setServerParams](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setserverparams) |
|virtual int |[getPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-getpeeronlinestatus) |
|virtual int64_t |[sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-sendusermessageoutsideroom) |
|virtual int64_t |[sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-senduserbinarymessageoutsideroom) |
|virtual int64_t |[sendServerMessage](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-sendservermessage) |
|virtual int64_t |[sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-sendserverbinarymessage) |
|virtual int |[startNetworkDetection](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startnetworkdetection) |
|virtual int |[stopNetworkDetection](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stopnetworkdetection) |
|virtual int |[setScreenAudioSourceType](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setscreenaudiosourcetype) |
|virtual int |[setScreenAudioChannel](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setscreenaudiochannel) |
|virtual int |[startScreenAudioCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startscreenaudiocapture-2) |
|virtual int |[stopScreenAudioCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stopscreenaudiocapture) |
|virtual int |[pushScreenAudioFrame](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-pushscreenaudioframe) |
|virtual int |[startPushMixedStream](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startpushmixedstream) |
|virtual int |[updatePushMixedStream](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-updatepushmixedstream) |
|virtual int |[stopPushMixedStream](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stoppushmixedstream) |
|virtual int |[startPushSingleStream](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startpushsinglestream) |
|virtual int |[stopPushSingleStream](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stoppushsinglestream) |
|virtual int |[enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-enableaudiopropertiesreport) |
|virtual int |[setRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setremoteaudioplaybackvolume) |
|virtual int |[enableVocalInstrumentBalance](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-enablevocalinstrumentbalance) |
|virtual int |[enablePlaybackDucking](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-enableplaybackducking) |
|virtual int |[registerLocalEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-registerlocalencodedvideoframeobserver) |
|virtual int |[registerRemoteEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-registerremoteencodedvideoframeobserver) |
|virtual int |[setExternalVideoEncoderEventHandler](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setexternalvideoencodereventhandler) |
|virtual int |[pushExternalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-pushexternalencodedvideoframe) |
|virtual int |[setVideoDecoderConfig](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvideodecoderconfig) |
|virtual int |[requestRemoteVideoKeyFrame](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-requestremotevideokeyframe) |
|virtual int |[sendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-sendstreamsyncinfo) |
|virtual int |[setLocalVoicePitch](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setlocalvoicepitch) |
|virtual int |[setVideoWatermark](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvideowatermark) |
|virtual int |[clearVideoWatermark](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-clearvideowatermark) |
|virtual long |[takeLocalSnapshot](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-takelocalsnapshot) |
|virtual long |[takeRemoteSnapshot](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-takeremotesnapshot) |
|virtual long |[takeRemoteSnapshotToFile](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-takeremotesnapshottofile) |
|virtual long |[takeLocalSnapshotToFile](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-takelocalsnapshottofile) |
|virtual int |[setDummyCaptureImagePath](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setdummycaptureimagepath) |
|virtual int |[startCloudProxy](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startcloudproxy) |
|virtual int |[stopCloudProxy](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stopcloudproxy) |
|virtual int |[startEchoTest](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startechotest) |
|virtual int |[stopEchoTest](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stopechotest) |
|virtual NetworkTimeInfo |[getNetworkTimeInfo](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-getnetworktimeinfo) |
|virtual int |[startHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-starthardwareechodetection) |
|virtual int |[stopHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stophardwareechodetection) |
|virtual int |[setLocalProxy](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setlocalproxy) |
|virtual int |[setLowLightAdjusted](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setlowlightadjusted) |
|virtual IWTNStream\* |[getWTNStream](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-getwtnstream) |
|virtual int |[deprecated] [updateRemoteStreamVideoCanvas](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-updateremotestreamvideocanvas) |
|virtual int |[deprecated] [setLocalVideoSink](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setlocalvideosink) |
|virtual int |[deprecated] [setRemoteVideoSink](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setremotevideosink) |

## Instructions

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
|config |const EngineConfig& |[EngineConfig](https://docs.byteplus.com/en/docs/12/docs-70098#EngineConfig) |
|event_handler |IRTCEngineEventHandler\* |Handler sent from SDK to App. See [IRTCEngineEventHandler](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler) |

**Return Value**

* IRTCEngine: A successfully created engine instance.

* Null: app_id is null or empty. event_handler is null.

### destroyRTCEngine

```cpp
static BYTERTC_STATIC_API void destroyRTCEngine();
```

Destroy the engine instance created by [createRTCEngine](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-creatertcengine), and release all related resources.

**Notes**

* Call this API after all business scenarios related to the engine instance are destroyed. In a multi\-thread scenario, you must not call [IRTCEngine](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine) related APIs after calling this interface, or the SDK may crash. When the API is called, RTC SDK destroys all memory associated with the engine instance and stops any interaction with the media server.

* Calling this API will start the SDK exit logic. The engine thread is held until the exit logic is complete. The engine thread is retained until the exit logic is complete. Therefore, do not call this API directly in the callback thread, or it will cause a deadlock. This function takes a long time to execute, so it's not recommended to call this API in the main thread, or the main thread may be blocked.

### getSDKVersion

```cpp
static BYTERTC_STATIC_API const char* getSDKVersion();
```

Get the current SDK version information.

**Return Value**

Current SDK version information.

### setLogConfig

```cpp
static BYTERTC_STATIC_API int setLogConfig(const LogConfig& log_config);
```

Configures the local log parameters of RTC SDK, including the logging level, directory, the limits for total log file size and the prefix of log.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|log_config |const LogConfig& |Local log parameters. See [LogConfig](https://docs.byteplus.com/en/docs/12/docs-70098#LogConfig). |

**Return Value**

* 0: Success.

* –1: Failure. This API must be called before creating engine.

* –2: Failure. Invalid parameters.

**Notes**

This API must be called before [createRTCEngine](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-creatertcengine).

### muteAudioCapture

```cpp
virtual int muteAudioCapture(bool mute) = 0;
```

> Available since 3.58.1

Set whether to mute the recording signal (without changing the local hardware).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mute |bool |Whether to mute audio capture.<br><br><br> <br><br>* True: Mute (disable microphone)<br><br>* False: (Default) Enable microphone |

**Return Value**

* 0: Success.

* < 0 : Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* Calling this API does not affect the status of SDK audio stream publishing.

* Adjusting the volume by calling [setCaptureVolume](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setcapturevolume) after muting will not cancel the mute state. The volume state will be retained until unmuted.

* You can use this interface to set the capture volume before or after calling [startAudioCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startaudiocapture) to enable audio capture.

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
|mute |bool |Whether to mute the audio capture when screen sharing.<br><br><br> <br><br>* True: Mute the audio capture when screen sharing.<br><br>* False: (Default) Unmute the audio capture when screen sharing. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* Adjusting the volume by calling [setCaptureVolume](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setcapturevolume) after muting will not cancel the mute state. The volume state will be retained until unmuted.

* You can use this interface to set the capture volume before or after calling [startAudioCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startaudiocapture) to enable audio capture.

### setCaptureVolume

```cpp
virtual int setCaptureVolume(int volume) = 0;
```

Adjust the audio capture volume

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |int |Ratio of capture volume to original volume. Ranging: [0,400]. Unit: %<br><br> <br><br>This changes the volume property of the audio data other than the hardware volume.<br><br><br> <br><br>* 0: Mute<br><br>* 100: Original volume. To ensure the audio quality, we recommend [0, 100].<br><br>* 400: Four times the original volume with signal\-clipping protection. |

**Return Value**

* 0: Success.

* < 0: Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

Call this API to set the volume of the audio capture before or during the audio capture.

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
|volume |int |Ratio(%) of capture volume to original volume, in the range [0, 400], with overflow protection.<br><br> <br><br>To ensure better call quality, we recommend setting the volume to [0, 100].<br><br><br> <br><br>* 0: Mute<br><br>* 100: Original volume<br><br>* 400: Four times the original volume with signal\-clipping protection |

**Return Value**

* 0: Success.

* < 0: Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

You can call this API to set the capture volume either before or after enabling screen audio capture.

### setPlaybackVolume

```cpp
virtual int setPlaybackVolume(const int volume) = 0;
```

Adjust the playback volume of the mixed remote audio. You can call this API before or during the playback.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |const int |Ratio(%) of playback volume to original volume, in the range [0, 400], with overflow protection.<br><br> <br><br>This changes the volume property of the audio data other than the hardware volume.<br><br> <br><br>To ensure the audio quality, we recommend setting the volume to `100`.<br><br><br> <br><br>* 0: mute<br><br>* 100: original volume<br><br>* 400: Four times the original volume with signal\-clipping protection. |

**Return Value**

* 0: Success.

* < 0: Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

Suppose a remote user A is always within the range of the target user whose playback volume will be adjusted, if you use both this method and [setRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setremoteaudioplaybackvolume)/[setRemoteRoomAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-setremoteroomaudioplaybackvolume), the volume that the local user hears from user A is the overlay of both settings.

### setEarMonitorMode

```cpp
virtual int setEarMonitorMode(EarMonitorMode mode) = 0;
```

Turn on/off the earphone monitor function

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mode |EarMonitorMode |Whether to turn on the earphone monitor function. See [EarMonitorMode](https://docs.byteplus.com/en/docs/12/docs-70098#EarMonitorMode). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* In\-ear monitoring is effective for audio captured by the RTC SDK.

* You can use ear monitoring feature when the earpiece is directly connected to the device by 3.5mm interface, USB interface, or BlueTooth. You cannot use ear monitoring feature when the earpiece is connected to a monitor via the HDMI or USB\-C interface, and then connected to the device, or connected to an OTG external sound card, and then connected to the device.

### setEarMonitorMode

```cpp
virtual int setEarMonitorMode(
    EarMonitorMode mode,
    int filter
) = 0;
```

> Available since 3.60.

Enables/disables in\-ear monitoring and controls whether to apply local audio processing to the in\-ear monitoring audio.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mode |EarMonitorMode |Whether to enable in\-ear monitoring. See [EarMonitorMode](https://docs.byteplus.com/en/docs/12/docs-70098#EarMonitorMode). Defaults to off. |
|filter |int |Whether to apply local audio processing to the in\-ear monitoring audio. See [EarMonitorAudioFilter](https://docs.byteplus.com/en/docs/12/docs-70098#EarMonitorAudioFilter). Defaults to no audio processing. |

**Return Value**

* 0: Success.

* < 0: Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* In\-ear monitoring is effective for audio captured by the RTC SDK.

* Ensure the users use the earpiece directly connected to the device by 3.5mm audio jack, USB, or Bluetooth. Earpiece connected to the device with the use of an intermediary device can not access to the in\-ear monitoring feature, such as earpiece connected to the device through a monitor via HDMI or USB\-C interface, or through an OTG sound card.

### setEarMonitorVolume

```cpp
virtual int setEarMonitorVolume(const int volume) = 0;
```

Set the volume of the earphone monitor

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |const int |The volume of the earphone monitor, the value range: [0,100], the unit:% |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

Before setting the volume of the earphone monitor, you must first call [setEarMonitorMode](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setearmonitormode) to turn on the earphone monitor function.

### startAudioCapture

```cpp
virtual int startAudioCapture() = 0;
```

Start internal audio capture. The default is off.

Internal audio capture refers to: capturing audio using the built\-in module.

The local client will be informed via [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onaudiodevicestatechanged) after starting audio capture by calling this API.

The remote clients in the room will be informed of the state change via [onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onuserstartaudiocapture) after the visible user starts audio capture by calling this API.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* If the current device does not have permission to access the microphone, calling this method will trigger the `onAudioDeviceStateChanged` callback, with the corresponding error code being `MediaDeviceError.kMediaDeviceErrorDeviceNoPermission = 1`.

* Call [stopAudioCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stopaudiocapture) to stop the internal audio capture. Otherwise, the internal audio capture will sustain until you destroy the engine instance.

* To mute and unmute microphones, we recommend using [publishStreamAudio](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-publishstreamaudio), other than [stopAudioCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stopaudiocapture) and this API. Because starting and stopping capture devices often need some time waiting for the response of the device, that may lead to a short silence during the communication.

* Once you create the engine instance, you can start internal audio capture regardless of the audio publishing state. The audio stream will start publishing only after the audio capture starts.

* To switch from custom to internal audio capture, stop publishing before disabling the custom audio capture module and then call this API to enable the internal audio capture.

### stopAudioCapture

```cpp
virtual int stopAudioCapture() = 0;
```

Stop internal audio capture. The default is off.

Internal audio capture refers to: capturing audio using the built\-in module.

The local client will be informed via [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onaudiodevicestatechanged) after stopping audio capture by calling this API.

.

The remote clients in the room will be informed of the state change via [onUserStopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onuserstopaudiocapture) after the visible client stops audio capture by calling this API.

.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* Call [startAudioCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startaudiocapture)to enable the internal audio capture.

* Without calling this API the internal audio capture will sustain until you destroy the engine instance.

### setVoiceChangerType

```cpp
virtual int setVoiceChangerType(VoiceChangerType voice_changer) = 0;
```

Set the sound change effect type

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|voice_changer |VoiceChangerType |The sound change effect type. See [VoiceChangerType](https://docs.byteplus.com/en/docs/12/docs-70098#VoiceChangerType). |

**Return Value**

API call result:

* 0: Success

* !0: Failure

**Notes**

* To use this feature, you need to integrate the SAMI dynamic library. See [Integrate Plugins on Demand](https://docs.byteplus.com/en/docs/12/1108726).

* You can call it before and after entering the room.

* Effective for both internal and external audio source.

* Only valid for mono\-channel audio.

* Mutually exclusive with [setVoiceReverbType](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvoicereverbtype), and the effects set later will override the effects set first.

* Before using the feature, you must implement [Audio SDK](https://go.byteplus.com/audio-sdk). Please contact the technical support.

### setVoiceReverbType

```cpp
virtual int setVoiceReverbType(VoiceReverbType voice_reverb) = 0;
```

Set the reverb effect type

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|voice_reverb |VoiceReverbType |The reverb effect type. See [VoiceReverbType](https://docs.byteplus.com/en/docs/12/docs-70098#VoiceReverbType). |

**Return Value**

API call result:

* 0: Success

* !0: Failure

**Notes**

* You can call it before and after entering the room.

* Effective for both internal and external audio source.

* Only valid for mono\-channel audio.

* Mutually exclusive with [setVoiceChangerType](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvoicechangertype), and the effects set later will override the effects set first.

### setLocalVoiceEqualization

```cpp
virtual int setLocalVoiceEqualization(VoiceEqualizationConfig config) = 0;
```

Set the equalization effect for the local captured audio. The audio includes both internal captured audio and external captured voice, but not the mixing audio file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|config |VoiceEqualizationConfig |See [VoiceEqualizationConfig](https://docs.byteplus.com/en/docs/12/docs-70098#VoiceEqualizationConfig). |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

According to the Nyquist acquisition rate, the audio acquisition rate must be greater than twice the set center frequency. Otherwise, the setting will not be effective.

### setLocalVoiceReverbParam

```cpp
virtual int setLocalVoiceReverbParam(VoiceReverbConfig param) = 0;
```

Set the reverb effect for the local captured audio. The audio includes both internal captured audio and external captured voice, but not the mixing audio file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|param |VoiceReverbConfig |See [VoiceReverbConfig](https://docs.byteplus.com/en/docs/12/docs-70098#VoiceReverbConfig). |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

Call [enableLocalVoiceReverb](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-enablelocalvoicereverb) to enable the reverb effect.

### enableLocalVoiceReverb

```cpp
virtual int enableLocalVoiceReverb(bool enable) = 0;
```

Enable the reverb effect for the local captured voice.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |bool |Whether to enable |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

Call [setLocalVoiceReverbParam](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setlocalvoicereverbparam) to set the reverb effect.

### setAudioProfile

```cpp
virtual int setAudioProfile(AudioProfileType audio_profile) = 0;
```

Sets the sound quality. Call this API to change the sound quality if the audio settings in the current [RoomProfileType](https://docs.byteplus.com/en/docs/12/docs-70098#RoomProfileType) can not meet your requirements.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audio_profile |AudioProfileType |Sound quality. See [AudioProfileType](https://docs.byteplus.com/en/docs/12/docs-70098#AudioProfileType) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* You can call this API before and after entering the room.

* Support dynamic switching of sound quality during a call.

### setAnsMode

```cpp
virtual int setAnsMode(AnsMode ans_mode) = 0;
```

> Available since 3.52

Set the Active Noise Cancellation(ANC) mode during audio and video communications.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|ans_mode |AnsMode |ANC modes. See [AnsMode](https://docs.byteplus.com/en/docs/12/docs-70098#AnsMode). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* You can call this API before or after entering a room. When you repeatedly call it, only the last call takes effect.

The AI noise cancellation can be enabled by calling this interface only in the following [RoomProfileType](https://docs.byteplus.com/en/docs/12/docs-70098#RoomProfileType) scenarios.

\- Game Voice: kRoomProfileTypeGame

\- High\-Quality Game: kRoomProfileTypeGameHD

\- Cloud Gaming: kRoomProfileTypeCloudGame

\- 1 vs 1 Audio and Video Call: kRoomProfileTypeChat

\- Multi\-End Synchronized Audio and Video Playback: kRoomProfileTypeLwTogether

\- Personal Device in Cloud Meeting: kRoomProfileTypeMeeting

\- Classroom Interaction: kRoomProfileTypeClassroom

\- Conference Room Terminals in Cloud Meetings: kRoomProfileTypeMeetingRoom

### enableAGC

```cpp
virtual int enableAGC(bool enable) = 0;
```

> Available since 3.51

Turns on/ off AAGC (Analog Automatic Gain Control).

After AAGC is enabled, SDK can automatically adjust microphone pickup volume to keep the output volume at a steady level.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |bool |whether to turn on AAGC.<br><br><br> <br><br>* true: AAGC is turned on.<br><br>* false: AAGC is turned off. |

**Return Value**

* 0: Success.

* \-1: Failure.

**Notes**

You can call this method before and after joining the room. To turn on AGC before joining the room, you need to contact the technical support to get a private parameter to set [RoomProfileType](https://docs.byteplus.com/en/docs/12/docs-70098#RoomProfileType).

To enable AAGC after joining the room, you must set [RoomProfileType](https://docs.byteplus.com/en/docs/12/docs-70098#RoomProfileType) to `kRoomProfileTypeMeeting`,`kRoomProfileTypeMeetingRoom` or `kRoomProfileTypeClassroom` .

It is not recommended to call [setAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-setaudiocapturedevicevolume) to adjust microphone pickup volume with AAGC on.

### setAudioSourceType

```cpp
virtual int setAudioSourceType (AudioSourceType type) = 0;
```

Switch the audio capture type.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |AudioSourceType |Audio input source type. See [AudioSourceType](https://docs.byteplus.com/en/docs/12/docs-70098#AudioSourceType)<br><br> <br><br>Use internal audio capture by default. The audio capture type and the audio render type may be different from each other. |

**Return Value**

Method call result:

* =0: Success.

* <0: Failure.

**Notes**

* You can call this API before or after joining the room.

* If you call this API to switch from internal audio capture to custom capture, the internal audio capture is automatically disabled. You must call [pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-pushexternalaudioframe) to push custom captured audio data to RTC SDK for transmission.

* If you call this API to switch from custom capture to internal capture, you must then call [startAudioCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startaudiocapture) to enable internal capture.

### setAudioRenderType

```cpp
virtual int setAudioRenderType (AudioRenderType type) = 0;
```

Switch the audio render type.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |AudioRenderType |Audio output source type. See [AudioRenderType](https://docs.byteplus.com/en/docs/12/docs-70098#AudioRenderType).<br><br> <br><br>Use internal audio render by default. The audio capture type and the audio render type may be different from each other. |

**Return Value**

Method call result:

* =0: Success.

* <0: Failure.

**Notes**

* You can call this API before or after joining the room.

* After calling this API to enable custom audio rendering, call [pullExternalAudioFrame](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-pullexternalaudioframe) for audio data.

### pushExternalAudioFrame

```cpp
virtual int pushExternalAudioFrame(IAudioFrame* audio_frame) = 0;
```

Push custom captured audio data to the RTC SDK.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audio_frame |IAudioFrame\* |The audio data of 10 ms. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70098#IAudioFrame)。<br><br><br> <br><br>* The audio sampling format must be S16. The data format within the audio buffer must be PCM, and its capacity should be audioFrame.samples × audioFrame.channel × 2.<br><br>* A specific sample rate and the number of channels must be specified; it is not supported to set them to automatic. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* Before calling this API, you must call [setAudioSourceType](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setaudiosourcetype) to enable custom audio capture.

* You must push custom captured audio data every 10 ms.

### pullExternalAudioFrame

```cpp
virtual int pullExternalAudioFrame(IAudioFrame* audio_frame) = 0;
```

Pull remote audio data. You can use the data for audio processing or custom rendering.

After calling this method, the SDK will actively pull the audio data that is ready to be played, including the decoded and mixed audio data from remote end for external playback.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audio_frame |IAudioFrame\* |The obtained audio data of 10 ms. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70098#IAudioFrame)。 |

**Return Value**

API call result:

* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for specific reasons.

**Notes**

* Before pulling the audio data, call [setAudioRenderType](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setaudiorendertype) to enable custom rendering.

* You should pull audio data every 10 milliseconds since the duration of a RTC SDK audio frame is 10 milliseconds. Samples x call frequency = audio_frame's sample rate. Assume that the sampling rate is set to 48000, call this API every 10 ms, so that 480 sampling points should be pulled each time.

* This function runs in the user calling thread and is a synchronous function.

### pushReferenceAudioPCMData

```cpp
virtual int pushReferenceAudioPCMData(IAudioFrame* audio_frame) = 0;
```

Push custom aec reference audio data to the RTC SDK.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audio_frame |IAudioFrame\* |The audio data of 10 ms. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70098#IAudioFrame)。 |

**Return Value**

* 0: Success

* <\-1: Failure

* <\-302：Warning. The configuration delivers an invalid aec scene.

* <\-303：Warning. The configuration delivers an invalid aec type.

**Notes**

* `audio_frame` must include all playback audio signals that you expect AEC to remove, such as RTC playback and third\-party audio that is actually played by the device.

* Push one 10 ms audio frame every 10 ms from a stable thread. Keep the scheduling jitter within approximately 1 ms. The number of samples multiplied by the call frequency must equal `audio_frame`'s sample rate. For example, at a sample rate of 48000 Hz, push 480 samples per call.

* The audio sampling format is S16. The data format in the audio buffer is PCM data, and its capacity is `audio_frame.samples × audio_frame.channel × 2` bytes.

### startVideoCapture

```cpp
virtual int startVideoCapture() = 0;
```

Enable internal video capture immediately. The default is off.

Internal video capture refers to using the RTC SDK built\-in video capture module to capture.

The local client will be informed via [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onvideodevicestatechanged) after starting video capture by calling this API.

The remote clients in the room will be informed of the state change via [onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onuserstartvideocapture) after the visible client starts video capture by calling this API.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* Call [stopVideoCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stopvideocapture) to stop the internal video capture. Otherwise, the internal video capture will sustain until you destroy the engine instance.

* Once you create the engine instance, you can start internal video capture regardless of the video publishing state. The video stream will start publishing only after the video capture starts.

* To switch from custom to internal video capture, stop publishing before disabling the custom video capture module and then call this API to enable the internal video capture.

### stopVideoCapture

```cpp
virtual int stopVideoCapture() = 0;
```

Disable internal video capture immediately. The default is off.

Internal video capture refers to using the RTC SDK built\-in video capture module to capture.

The local client will be informed via [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onvideodevicestatechanged) after stopping video capture by calling this API.

The remote clients in the room will be informed of the state change via [onUserStopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onuserstopvideocapture) after the visible client stops video capture by calling this API.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* Call [startVideoCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startvideocapture) to enable the internal video capture.

* Without calling this API the internal video capture will sustain until you destroy the engine instance.

### setVideoCaptureConfig

```cpp
virtual int setVideoCaptureConfig(const VideoCaptureConfig& video_capture_config) = 0;
```

Set the video capture parameters for internal capture of the RTC SDK.

If your project uses the SDK internal capture module, you can specify the video capture parameters including preference, resolution and frame rate through this interface.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|video_capture_config |const VideoCaptureConfig& |Video capture parameters. See: [VideoCaptureConfig](https://docs.byteplus.com/en/docs/12/docs-70098#VideoCaptureConfig). |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* This API can be called after the engine is created and takes effect immediately after being called. It is recommended to call this interface before calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startvideocapture).

* It is recommended that different Engines on the same device use the same video capture parameters.

* If you used the internal module to start video capture before calling this interface, the capture parameters default to Auto.

### setVideoCaptureRotation

```cpp
virtual int setVideoCaptureRotation(VideoRotation rotation) = 0;
```

Set the rotation of the video images captured from the local device.

Call this API to rotate the videos when the camera is fixed upside down or tilted.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|rotation |VideoRotation |It defaults to `VIDEO_ROTATION_0(0)`, which means not to rotate. Refer to [VideoRotation](https://docs.byteplus.com/en/docs/12/docs-70098#VideoRotation). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* This API affects the external\-sourced videos. The final rotation would be the original rotation angles adding up with the rotation set by calling this API.

* For the Windows SDK, the elements added during the video pre\-processing stage, such as video sticker and background applied using [enableVirtualBackground](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect-enablevirtualbackground) will also be rotated by this API.

### setVideoEncoderConfig

```cpp
virtual int setVideoEncoderConfig(const VideoEncoderConfig& encoder_config) = 0;
```

Sets the expected quality of the video stream by specifying the resolution, frame rate, bitrate, and the fallback strategy when the network is poor.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|encoder_config |const VideoEncoderConfig& |See [VideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70098#VideoEncoderConfig). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* This method can only set a single profile for the video stream. If you intend to publish the stream in multiple qualities, use [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setlocalsimulcastmode).

* Without calling this method, only one stream will be sent with a profile of 640px × 360px @15fps. The default encoding preference is frame rate\-first.

* If you use an external video source, you can also use this method to set the encoding parameters.

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
|mode |VideoSimulcastMode |Whether to publish lower\-quality streams and how many of them to be published. See [VideoSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-70098#VideoSimulcastMode). By default, it is set to Single, where the publisher sends the video in a single profile. In the other modes, the low\-quality stream is set to a default resolution of 160px × 90px with a bitrate of 50Kbps. |
|stream_config |const VideoEncoderConfig\* |The specification of the lower quality stream. See [VideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70098#VideoEncoderConfig). The resolution of the lower quality stream must be smaller than the standard stream set via [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvideoencoderconfig). The specifications in the array must be arranged in ascending order based on resolution.<br><br>In the other modes, the low\-quality stream is set to a default resolution of 160px × 90px with a bitrate of 50Kbps. |
|num |int |The number of the lower quality streams, which is also the length of the stream_config array. The maximum value is 3. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* The default specification of the video stream is 640px × 360px @15fps.

* The method applies to the camera video only.

* Refer to [Simulcasting](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70139) for more information.

### setLocalSimulcastMode

```cpp
virtual int setLocalSimulcastMode(VideoSimulcastMode mode) = 0;
```

> Available since 3.60.

Enable the Simulcast feature.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mode |VideoSimulcastMode |Whether to publish lower\-quality streams and how many of them to be published. See [VideoSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-70098#VideoSimulcastMode).<br><br>By default, it is set to Single, where the publisher sends the video in a single profile. In the other modes, the low\-quality stream is set to a default resolution of 160px × 90px with a bitrate of 50Kbps. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* Call this method before the user joins a room.

* The default specification of the video stream is 640px × 360px @15fps.

* If you intend to specify the lower\-quality streams, use setLocalSimulcastMode(VideoSimulcastMode mode, const VideoEncoderConfig\* stream_config, int num).

* The method applies to the camera video only.

* Refer to [Simulcasting](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70139) for more information.

### enableAlphaChannelVideoEncode

```cpp
virtual int enableAlphaChannelVideoEncode(AlphaLayout alpha_layout) = 0;
```

> Available since 3.58

Enables the Alpha channel encoding feature for custom capture video frames.

Suitable for scenarios where the video subject needs to be separated from the background at the push\-streaming end, and the background can be custom rendered at the receive\-streaming end.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|alpha_layout |AlphaLayout |The arrangement position of the separated Alpha channel relative to the RGB channel information. Currently, only AlphaLayout.kAlphaLayoutTop is supported, which is positioned above the RGB channel information. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* This interface only applies to custom capture video frames that use the RGBA color model, including:

   * Windows: VideoPixelFormat.kVideoPixelFormatRGBA;

   * Android: VideoPixelFormat.TEXTURE_2D, VideoPixelFormat.TEXTURE_OES, VideoPixelFormat.RGBA;

   * iOS: ByteRTCVideoPixelFormat.ByteRTCVideoPixelFormatCVPixelBuffer.

* This interface must be called before publishing the video stream.

* After enabling Alpha channel encoding with this interface, you need to call pushExternalVideoFrame to push custom captured video frames to the RTC SDK. If a video frame format that is not supported is pushed, the call to pushExternalVideoFrame will return the error code ReturnStatus.kReturnStatusParameterErr.

### disableAlphaChannelVideoEncode

```cpp
virtual int disableAlphaChannelVideoEncode() = 0;
```

> Available since 3.58

Disables the Alpha channel encoding feature for custom captured video frames.

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

This interface must be called after stopping publishing the video stream.

### setLocalVideoCanvas

```cpp
virtual int setLocalVideoCanvas(const VideoCanvas& canvas) = 0;
```

Sets the view to be used for local video rendering and the rendering mode.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|canvas |const VideoCanvas& |View information and rendering mode. See [VideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70098#VideoCanvas). |

**Return Value**

* 0: Success.

* \-2: Invalid parameter.

* \-12: This method is not available in the Audio SDK.

**Notes**

* You should bind your stream to a view before joining the room. This setting will remain in effect after you leave the room.

* If you need to unbind the local video stream from the current view, you can call this API and set the videoCanvas to `null`.

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
|render_mode |const enum RenderMode |See [RenderMode](https://docs.byteplus.com/en/docs/12/docs-70098#RenderMode). |
|background_color |const uint32_t |See [VideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70098#VideoCanvas).background_color. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

Calling this API during local video rendering will be effective immediately.

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
|stream_id |const char\* |identifier of stream |
|canvas |const VideoCanvas& |canvas and rendering mode. See [VideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70098#VideoCanvas) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

When the local user leaves the room, the setting will be invalid. The remote user leaving the room does not affect the setting.

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
|remote_video_render_config |const RemoteVideoRenderConfig& |Video rendering settings. See [RemoteVideoRenderConfig](https://docs.byteplus.com/en/docs/12/docs-70098#RemoteVideoRenderConfig). |

**Return Value**

* 0: Success.

* < 0 : Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* After setting the rendering configuration for the remote video frame with [setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setremotevideocanvas), you can call this API to update settings including render mode, background color, and rotation angle.

* Calling this API during remote video rendering will be effective immediately.

### setLocalVideoSink

```cpp
virtual int setLocalVideoSink(
    IVideoSink* video_sink,
    LocalVideoSinkConfig& config
) = 0;
```

> Available since 3.60.

Binds the local video stream to a custom renderer. You can get video frame data at specified positions and formats through parameter settings.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|video_sink |IVideoSink\* |Custom video renderer. See [IVideoSink](https://docs.byteplus.com/en/docs/12/docs-70098#IVideoSink). |
|config |LocalVideoSinkConfig& |Local video frame callback configuration, see [LocalVideoSinkConfig](https://docs.byteplus.com/en/docs/12/docs-70098#LocalVideoSinkConfig)。 |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* RTC SDK uses its own renderer (internal renderer) for video rendering by default.

* Leaving the room will clear the binding status.

* If you need to unbind the video stream from the custom renderer, you must set video_sink to `null`.

* Generally, after receiving the [onFirstLocalVideoFrameCaptured](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onfirstlocalvideoframecaptured) callback notification that the first local video frame has been captured, call this method to bind a custom renderer to a video stream and join the room.

### setRemoteVideoSink

```cpp
virtual int setRemoteVideoSink(
    const char* stream_id,
    IVideoSink* video_sink,
    RemoteVideoSinkConfig& config
) = 0;
```

> Available since 3.57

Binds the remote video stream to a custom renderer. You can get video frame data at specified positions and formats through parameter settings.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of stream |
|video_sink |IVideoSink\* |Custom video renderer. See [IVideoSink](https://docs.byteplus.com/en/docs/12/docs-70098#IVideoSink). |
|config |RemoteVideoSinkConfig& |remote video frame callback configuration, see [RemoteVideoSinkConfig](https://docs.byteplus.com/en/docs/12/docs-70098#RemoteVideoSinkConfig)。 |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* RTC SDK uses its own renderer (internal renderer) for video rendering by default.

* This method can be called both before and after entering the room. If you are unable to obtain remote stream information in advance, you can call this method after joining the room and receiving the remote stream information through the onUserPublishStream callback.

* Leaving the room will clear the binding status.

* If you need to unbind the video stream from the custom renderer, you must set video_sink to `null`.

### updateScreenCaptureRegion

```cpp
virtual int updateScreenCaptureRegion(const Rectangle& region_rect) = 0;
```

Update the capture area when capturing screen video streams through the capture module provided by the RTC SDK. Only used when the capture source is the monitor screen.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|region_rect |const Rectangle& |Region to be shared. See [Rectangle](https://docs.byteplus.com/en/docs/12/docs-70098#Rectangle)<br><br> <br><br>This parameter describes the region to be shared after calling this API, and the relative relationship between the `source_info` setting area in [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startscreenvideocapture). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

Before calling this interface, internal screen stream capture must have been turned on by calling [startScreenVideoCapture]

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
|source_info |const ScreenCaptureSourceInfo& |Screen capture source information. See [ScreenCaptureSourceInfo](https://docs.byteplus.com/en/docs/12/docs-70098#ScreenCaptureSourceInfo).<br><br> <br><br>Call [getScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-getscreencapturesourcelist) to get all the screen sources that can be shared. |
|capture_params |const ScreenCaptureParameters& |Screen capture parameters. See [ScreenCaptureParameters](https://docs.byteplus.com/en/docs/12/docs-70098#ScreenCaptureParameters). |

**Return Value**

* 0: Success;

* \-1: Failure;

**Notes**

* The call of this API takes effect only when you are using RTC SDK to record screen. You will get a warning by [onVideoDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onvideodevicewarning) after calling this API when the video source is set to an external recorder.

* This API only starts screen capturing but does not publish the captured video. Call [publishStreamVideo](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-publishstreamvideo) to publish the captured video.

* To turn off screen video capture, call [stopScreenVideoCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stopscreenvideocapture).

* Local users will receive [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onvideodevicestatechanged) on the state of screen capturing such as start, pause, resume, and error.

* After successfully calling this API, local users will receive [onFirstLocalVideoFrameCaptured](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onfirstlocalvideoframecaptured).

* Before calling this API, you can call [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvideoencoderconfig) to set the frame rate and encoding resolution of the screen video stream.

* After receiving [onFirstLocalVideoFrameCaptured](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onfirstlocalvideoframecaptured), you can set the local screen sharing view by calling [setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setlocalvideocanvas) or setLocalVideoSink .

* You can also register an observer by calling [setLocalVideoSink](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setlocalvideosink) and receive the captured screen video frame through [onFrame](https://docs.byteplus.com/en/docs/12/docs-70098#IVideoSink-onframe).

* For Windows SDK, after you start capturing screen video stream for sharing，you can call [updateScreenCaptureHighlightConfig](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-updatescreencapturehighlightconfig) to update border highlighting settings, [updateScreenCaptureMouseCursor](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-updatescreencapturemousecursor) to update the processing settings for the mouse, and [updateScreenCaptureFilterConfig](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-updatescreencapturefilterconfig) to set the window that needs to be filtered.

### stopScreenVideoCapture

```cpp
virtual int stopScreenVideoCapture() = 0;
```

Stop screen video streaming.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* This API can only stop the screen capture by the RTC SDK. If the video source has been set to external recorder, the call of this API will fail. You need to stop it in the external recorder.

* The call of this API takes effect only when you are using RTC SDK to record screen. You will get a warning by [onVideoDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onvideodevicewarning) after calling this API when the video source is set to an external recorder.

* To turn on screen video stream capture, calling [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startscreenvideocapture)

* Local users will receive the [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onvideodevicestatechanged) callback.

* Calling this interface does not affect screen video stream publishing.

### updateScreenCaptureHighlightConfig

```cpp
virtual int updateScreenCaptureHighlightConfig(const HighlightConfig& highlight_config) = 0;
```

Update border highlighting settings when capturing screen video streams through the capture module provided by the RTC SDK. By default, a highlight border is displayed.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|highlight_config |const HighlightConfig& |Border highlighting settings. See [HighlightConfig](https://docs.byteplus.com/en/docs/12/docs-70098#HighlightConfig) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* Before calling this interface, you must have turned on internal screen flow collection by calling [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startscreenvideocapture).

* For Linux with X11 protocol, the API is valid; for Linux with Wayland, the API is not valid.

### updateScreenCaptureMouseCursor

```cpp
virtual int updateScreenCaptureMouseCursor(MouseCursorCaptureState capture_mouse_cursor) = 0;
```

Update the processing settings for the mouse when capturing screen video streams through the capture module provided by the RTC SDK. By default, the mouse cursor is captured.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|capture_mouse_cursor |MouseCursorCaptureState |See [MouseCursorCaptureState](https://docs.byteplus.com/en/docs/12/docs-70098#MouseCursorCaptureState) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* Before calling this interface, internal screen stream capture must have been turned on by calling [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startscreenvideocapture).

### updateScreenCaptureFilterConfig

```cpp
virtual int updateScreenCaptureFilterConfig(const ScreenFilterConfig& filter_config) = 0;
```

When capturing screen video streams through the capture module provided by the RTC SDK, set the window that needs to be filtered.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|filter_config |const ScreenFilterConfig& |Window filtering settings. See [ScreenFilterConfig](https://docs.byteplus.com/en/docs/12/docs-70098#ScreenFilterConfig) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* Before calling this interface, internal screen stream capture must have been turned on by calling [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startscreenvideocapture).

* This function only works when the screen source category is a screen rather than an application form. See [ScreenCaptureSourceType](https://docs.byteplus.com/en/docs/12/docs-70098#ScreenCaptureSourceType).

### getScreenCaptureSourceList

```cpp
virtual IScreenCaptureSourceList* getScreenCaptureSourceList() = 0;
```

Get the item list for screen sharing.

**Return Value**

List of the screen\-sharing objects, including application window and screens. See [IScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/14184#IScreenCaptureSourceList). After deciding which item to be shared, the user can share the object with [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startscreenvideocapture).

**Notes**

* For Linux with X11 protocol, the API is valid; for Linux with Wayland, the API is not valid. For Linux with Wayland, when you call [startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startscreenvideocapture), the system pops up a window for the user to choose the object to share.

* Call [release](https://docs.byteplus.com/en/docs/12/14184#IScreenCaptureSourceList-release) to release the resources.

### getThumbnail

```cpp
virtual IVideoFrame* getThumbnail(
            ScreenCaptureSourceType type, view_t source_id, int max_width, int max_height) = 0;
```

Get the preview thumbnail of the screen\-sharing object

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |ScreenCaptureSourceType |Type of the screen capture object. Refer to [ScreenCaptureSourceType](https://docs.byteplus.com/en/docs/12/docs-70098#ScreenCaptureSourceType) for more details. |
|source_id |view_t |ID of the screen sharing object, which can be obtained from the list of shared objects enumerated by [getScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-getscreencapturesourcelist). For more details, see [view_t](https://docs.byteplus.com/en/docs/12/14184#view_t). |
|max_width |int |Maximum width of the preview thumbnail. RTC will scale the thumbnail to fit the given size while maintaining the original aspect ratio. If the aspect ratio of the given size does not match the sharing object, the thumbnail will have blank borders. |
|max_height |int |Maximum height of the preview thumbnail. Refer to the note for `max_width`. |

**Return Value**

Preview thumbnail of the screen\-sharing object Refer to [IVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70098#IVideoFrame) for more details.

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
|source_id |view_t |ID of the screen\-sharing object. You can get the ID by calling [getScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-getscreencapturesourcelist). |
|max_width |int |Maximum width of the App icon. The width is always equal to the height. SDK will set the height and width to the smaller value if the given values are unequal. RTC will return nullptr if you set the value with a number out of the valid range, [32, 256]. The default size is 100 x 100. |
|max_height |int |Maximum height of the app icon. Refer to the note for `max_width` |

**Return Value**

Refer to [IVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70098#IVideoFrame) for more details. You can get the icon when the item to be shared is an application and the application is assigned with an icon. If not, the return value will be nullptr.

### setVideoSourceType

```cpp
virtual int setVideoSourceType(VideoSourceType type) = 0;
```

Set the video source, including the screen recordings.

The internal video capture is the default, which refers to capturing video using the built\-in module.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |VideoSourceType |Video source type. Refer to [VideoSourceType](https://docs.byteplus.com/en/docs/12/docs-70098#VideoSourceType) for more details. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* You can call this API whether the user is in a room or not.

* Calling this API to switch to the custom video source will stop the enabled internal video capture.

* To switch to internal video capture, call this API to stop custom capture and then call [startVideoCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startvideocapture) to enable internal video capture.

* To push custom encoded video frames to the SDK, call this API to switch `VideoSourceType` to `VideoSourceTypeEncodedWithAutoSimulcast` or `VideoSourceTypeEncodedWithoutAutoSimulcast`.

### pushExternalVideoFrame

```cpp
virtual int pushExternalVideoFrame(const VideoFrameData& frame) = 0;
```

Pushes external video frames.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|frame |const VideoFrameData& |Set the video frame. See [IVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70098#IVideoFrame). |

**Return Value**

API call result:

* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for specific reasons.

**Notes**

* Support for I420, NV12, RGBA, BGRA, and ARGB.

* This function runs in the user calling thread.

* Before pushing external video frames, you must call [setVideoSourceType](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvideosourcetype) to turn on external video source capture.

### createRTCRoom

```cpp
virtual IRTCRoom* createRTCRoom(const char* room_id) = 0;
```

Create a RTC room instance.

This API only returns an RTC room instance. You still need to call [joinRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-joinroom) to actually create/join the room.

Each call of this API creates one [IRTCRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom) instance. Call this API as many times as the number of rooms you need, and then call [joinRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-joinroom) of each IRTCRoom instance to join multiple rooms at the same time.

In multi\-room mode, a user can subscribe to media streams in the joined rooms at the same time.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|room_id |const char\* |The string matches the regular expression: `[a-zA-Z0-9_\@\-\.]{1,128}`. |

**Return Value**

[IRTCRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom) instance.

If you get NULL instead of an RTCRoom instance, please ensure the room_id is valid. And the specified room is not yet created.

**Notes**

* If the room that you wish to join already exists, you still need to call this API first to create the IRTCRoom instance, and then call [joinRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-joinroom).

* Do not create multiple rooms with the same room_id, otherwise the newly created room instance will replace the old one.

* To forward streams to the other rooms, call [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-startforwardstreamtorooms) instead of enabling Multi\-room mode.

### createRTSRoom

```cpp
virtual IRTSRoom* createRTSRoom(const char* room_id) = 0;
```

Create an RTS room instance.

This API only returns an RTS room instance. You still need to call [joinRTSRoom](https://docs.byteplus.com/en/docs/12/14184#IRTSRoom-joinrtsroom) to actually create/join the room.

Each call of this API creates one [IRTSRoom](https://docs.byteplus.com/en/docs/12/14184#IRTSRoom) instance. Call this API as many times as the number of rooms you need, and then call [joinRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-joinroom) of each IRTCRoom instance to join multiple rooms at the same time.

In multi\-room mode, a user can send and receive RTS messages in the joined rooms at the same time.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|room_id |const char\* |The string matches the regular expression: `[a-zA-Z0-9_\@\-\.]{1,128}`. |

**Return Value**

[IRTSRoom](https://docs.byteplus.com/en/docs/12/14184#IRTSRoom) instance.

If you get NULL instead of an RTCRoom instance, please ensure the room_id is valid. And the specified room is not yet created.

**Notes**

* If the room that you wish to join already exists, you still need to call this API first to create the IRTSRoom instance, and then call [joinRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-joinroom).

* Do not create multiple rooms with the same room_id, otherwise the newly created room instance will replace the old one.

### setPublishFallbackOption

```cpp
virtual int setPublishFallbackOption(PublishFallbackOption option) = 0;
```

Sets the fallback option for published audio & video streams.

You can call this API to set whether to automatically lower the resolution you set of the published streams under limited network conditions.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|option |PublishFallbackOption |Fallback option, see [PublishFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70098#PublishFallbackOption). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* This API only works after you call [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setlocalsimulcastmode) to enable the mode of publishing multiple streams.

* You must call this API before entering the room.

* After calling this method, if there is a performance degradation or recovery due to poor performance or network conditions, the local end will receive early warnings through the [onPerformanceAlarms](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onperformancealarms) callback to adjust the capture device.

* After you allow video stream to fallback, your stream subscribers will receive [onSimulcastSubscribeFallback](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onsimulcastsubscribefallback) when the resolution of your published stream is lowered or restored.

* You can alternatively set fallback options with distributions from server side, which is of higher priority.

### setSubscribeFallbackOption

```cpp
virtual int setSubscribeFallbackOption(SubscribeFallbackOption option) = 0;
```

Sets the fallback option for subscribed RTC streams.

You can call this API to set whether to lower the resolution of currently subscribed stream under limited network conditions.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|option |SubscribeFallbackOption |Fallback option, see [SubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70098#SubscribeFallbackOption) for more details. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* You must call this API before entering the room.

* After you enables the fallback, you will receive [onSimulcastSubscribeFallback](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onsimulcastsubscribefallback) and [onRemoteVideoSizeChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onremotevideosizechanged) when the resolution of your subscribed stream is lowered or restored.

* You can alternatively set fallback options with distributions from server side, which is of higher priority.

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
|priority |RemoteUserPriority |Remote user's requirement priority. See enumeration type [RemoteUserPriority](https://docs.byteplus.com/en/docs/12/docs-70098#RemoteUserPriority) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* This method is used with [setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setsubscribefallbackoption).

* If the subscription flow fallback option is turned on, weak connections or insufficient performance will give priority to ensuring the quality of the flow received by high\-priority users.

* This method can be used before and after entering the room, and the priority of the remote user can be modified.

### setBusinessId

```cpp
virtual int setBusinessId(const char* business_id) = 0;
```

Sets the business ID

You can use businessId to distinguish different business scenarios. You can customize your businessId to serve as a sub AppId, which can share and refine the function of the AppId, but it does not need authentication.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|business_id |const char\* |Your customized businessId<br><br> <br><br>BusinessId is a tag, and you can customize its granularity. |

**Return Value**

* 0: Success.

* \-2: The input is invalid. Legal characters include all lowercase letters, uppercase letters, numbers, and four other symbols, including '.', '\-','_', and '@'.

**Notes**

* You must call this API before the [joinRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-joinroom) API, otherwise it will be invalid.

### setLocalVideoMirrorType

```cpp
virtual int setLocalVideoMirrorType(MirrorType mirror_type) = 0;
```

Sets the mirror mode for the captured video stream.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mirror_type |MirrorType |Mirror type. See [MirrorType](https://docs.byteplus.com/en/docs/12/docs-70098#MirrorType). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* Switching video streams does not affect the settings of the mirror type.

* This API is not applicable to screen\-sharing streams.

* When using an external renderer, you can set `mirrorType` to `0` and `3`, but you cannot set it to `1`.

* Before you call this API, the initial states of each video stream are as follows:

| |Front\-facing camera |Back\-facing camera |Custom capturing |Built\-in camera |
|---|---|---|---|---|
|Mobile device |The preview is mirrored. The published video stream is not mirrored. |The preview and the published video stream are not mirrored. |The preview and the published video stream are not mirrored. |/ |
|PC |/ |/ |The preview and the published video stream are not mirrored. |The preview is mirrored. The published video stream is not mirrored. |

  ### setRemoteVideoMirrorType ```cpp virtual int setRemoteVideoMirrorType( const char\* stream_id, RemoteMirrorType mirror_type ) = 0; ``` \> Available since 3.57

When using internal rendering, enable mirroring for the remote stream.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of stream |
|mirror_type |RemoteMirrorType |The mirror type for the remote stream, see RemoteMirrorType . |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

### getVideoEffectInterface

```cpp
virtual IVideoEffect* getVideoEffectInterface() = 0;
```

Gets video effect APIs.

**Return Value**

Video effect APIs. See [IVideoEffect](https://docs.byteplus.com/en/docs/12/14184#IVideoEffect).

### enableEffectBeauty

```cpp
virtual int enableEffectBeauty(bool enable) = 0;
```

Enables/Disables basic beauty effects.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |bool |Whether to enable basic beauty effects.<br><br><br> <br><br>* true: Enables basic beauty effects.<br><br>* false: (Default) Disables basic beauty effects. |

**Return Value**

* 0: Success.

* –1001: This method is not available for your current RTC SDK.

* \-12: This method is not available in the Audio SDK.

* <0: Failure. Effect SDK internal error. For specific error code, see [Error Code Table](https://docs.byteplus.com/effects/docs/error-code-table).

**Notes**

* You cannot use the basic beauty effects and the advanced effect features at the same time. See [how to use advanced effect features](https://docs.byteplus.com/byteplus-rtc/docs/114717) for more information.

* You need to integrate Effect SDK before calling this API. Effect SDK v4.4.2+ is recommended.

* Call [setBeautyIntensity](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setbeautyintensity) to set the beauty effect intensity. If you do not set the intensity before calling this API, the default intensity will be enabled. The default values for the intensity of each beauty mode are as follows: 0.7 for brightening, 0.8 for smoothing, 0.5 for sharpening, and 0.7 for clarity.

* This API is not applicable to screen capturing.

### setBeautyIntensity

```cpp
virtual int setBeautyIntensity(
    EffectBeautyMode beauty_mode,
    float intensity
) = 0;
```

Sets the beauty effect intensity.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|beauty_mode |EffectBeautyMode |Basic beauty effect. See [EffectBeautyMode](https://docs.byteplus.com/en/docs/12/docs-70098#EffectBeautyMode). |
|intensity |float |Beauty effect intensity in the range of [0,1]. When you set it to 0, the beauty effect will be turned off.<br><br> <br><br>The default values for the intensity of each beauty mode are as follows: 0.7 for brightening, 0.8 for smoothing, 0.5 for sharpening, and 0.7 for clarity. |

**Return Value**

* 0: Success.

* –2: `intensity` is out of range.

* –1001: This API is not available for your current RTC SDK.

* <0: Failure. Effect SDK internal error. For specific error code, see [error codes](https://docs.byteplus.com/effects/docs/error-code-table).

**Notes**

* If you call this API before calling [enableEffectBeauty](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-enableeffectbeauty), the default settings of beauty effect intensity will adjust accordingly.

* If you destroy the engine, the beauty effect settings will be invalid.

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
|encrypt_type |EncryptType |Built\-in encryption algorithm. See [EncryptType](https://docs.byteplus.com/en/docs/12/docs-70098#EncryptType) |
|key |const char\* |Encryption key. The length is limited to 36 bits, and the excess will be truncated |
|key_size |int |The length of the parameter key |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* Use this method when using the built\-in encryption on transfer; if you need to use custom encryption on transfer. See onEncryptData . Built\-in encryption and custom encryption are mutually exclusive, and the transmission is determined to be encrypted according to the last method called.

* This method must be called before entering the room, and can be called repeatedly, taking the last called parameter as the effective parameter.

### setCustomizeEncryptHandler

```cpp
virtual int setCustomizeEncryptHandler(IEncryptHandler* handler) = 0;
```

Sets custom encryption and decryption methods.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|handler |IEncryptHandler\* |Custom encryption handler, you need to implement the handler's encryption and decryption method. See [IEncryptHandler](https://docs.byteplus.com/en/docs/12/docs-70096#IEncryptHandler). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* This method is mutually exclusive with [setEncryptInfo](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setencryptinfo), you can only select custom encryption method or default encryption method. The encryption method that takes effect depends on the last method called.

* This method must be called before entering the room, and can be called repeatedly, taking the last called parameter as the effective parameter.

* Whether encrypted or decrypted, the length of the modified data needs to be controlled under 180%. That is, if the input data is 100 bytes, the processed data must be less than 180 bytes. If the encryption or decryption result exceeds the limit, the audio & video frame may be discarded.

* Data encryption/decryption is performed serially, so depending on the implementation, it may affect the final rendering efficiency. Whether to use this method needs to be carefully evaluated by users.

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
|method |AudioFrameCallbackMethod |Audio data callback method. See [AudioFrameCallbackMethod](https://docs.byteplus.com/en/docs/12/docs-70098#AudioFrameCallbackMethod).<br><br> <br><br>If `method` is set as `kRecord`, `kPlayback`, `kMixed`, `kRecordScreen`, `kCaptureMixed`, set `format` to the accurate value listed in the audio parameters format.<br><br> <br><br>If `method` is set as `kRemoteUser`, set `format` to `auto`. |
|format |AudioFormat |Audio parameters format. See [AudioFormat](https://docs.byteplus.com/en/docs/12/docs-70098#AudioFormat). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

After calling this API and [registerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-registeraudioframeobserver), [IAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioFrameObserver) will receive the corresponding audio data callback. However, these two APIs are independent of each other and the calling order is not restricted.

### disableAudioFrameCallback

```cpp
virtual int disableAudioFrameCallback(AudioFrameCallbackMethod method) = 0;
```

Disables audio data callback.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|method |AudioFrameCallbackMethod |Audio data callback method. See [AudioFrameCallbackMethod](https://docs.byteplus.com/en/docs/12/docs-70098#AudioFrameCallbackMethod). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

Call this API after calling [enableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-enableaudioframecallback).

### registerAudioFrameObserver

```cpp
virtual int registerAudioFrameObserver(IAudioFrameObserver* observer) = 0;
```

Register an audio frame observer.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|observer |IAudioFrameObserver\* |Audio data callback observer. See [IAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioFrameObserver). Use `null` to cancel the registration. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

After calling this API and [enableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-enableaudioframecallback), [IAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioFrameObserver) receives the corresponding audio data callback. You can retrieve the audio data and perform processing on it without affecting the audio that RTC SDK uses to encode or render.

### registerAudioProcessor

```cpp
virtual int registerAudioProcessor(IAudioFrameProcessor* processor) = 0;
```

Register a custom audio preprocessor.

After that, you can call [enableAudioProcessor](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-enableaudioprocessor) to process the audio streams that either captured locally or received from the remote side. RTC SDK then encodes or renders the processed data.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|processor |IAudioFrameProcessor\* |Custom audio processor. See [IAudioFrameProcessor](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioFrameProcessor)。<br><br> <br><br>SDK only holds weak references to the processor, you should guarantee its Life Time. To cancel registration, set the parameter to nullptr. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* When this interface is repeatedly called, only the last call takes effect.

* Refer to [Custom Audio Processing](https://docs.byteplus.com/en/byteplus-rtc/docs/80635) for more information.

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
|method |AudioProcessorMethod |The types of audio frames. See [AudioProcessorMethod](https://docs.byteplus.com/en/docs/12/docs-70098#AudioProcessorMethod). Set this parameter to process multiple types of audio.<br><br> <br><br>With different values, you will receive the corresponding callback:<br><br><br> <br><br>* For locally captured audio, you will receive [onProcessRecordAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioFrameProcessor-onprocessrecordaudioframe).<br><br>* For mixed remote audio, you will receive [onProcessPlayBackAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioFrameProcessor-onprocessplaybackaudioframe).<br><br>* For audio from remote users, you will receive [onProcessRemoteUserAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioFrameProcessor-onprocessremoteuseraudioframe).<br><br>* For shared\-screen audio, you will receive [onProcessScreenAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioFrameProcessor-onprocessscreenaudioframe). (Only on Windows) |
|format |AudioFormat |The format of audio frames. See [AudioFormat](https://docs.byteplus.com/en/docs/12/docs-70098#AudioFormat). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* Before calling this API, call [registerAudioProcessor](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-registeraudioprocessor) to register a processor.

* To disable custom audio processing, call [disableAudioProcessor](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-disableaudioprocessor).

### disableAudioProcessor

```cpp
virtual int disableAudioProcessor(AudioProcessorMethod method) = 0;
```

Disable custom audio processing.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|method |AudioProcessorMethod |Audio Frame type. See [AudioProcessorMethod](https://docs.byteplus.com/en/docs/12/docs-70098#AudioProcessorMethod). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

### registerLocalVideoProcessor

```cpp
virtual int registerLocalVideoProcessor(
    IVideoProcessor* processor,
    VideoPreprocessorConfig config
) = 0;
```

Set up a custom video preprocessor.

Using this video preprocessor, you can call [processVideoFrame](https://docs.byteplus.com/en/docs/12/14184#IVideoProcessor-processvideoframe) to preprocess the video frames collected by the RTC SDK, and use the processed video frames for RTC audio & video communication.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|processor |IVideoProcessor\* |Custom video processor. See [IVideoProcessor](https://docs.byteplus.com/en/docs/12/14184#IVideoProcessor). If null is passed in, the video frames captured by the RTC SDK are not preprocessed.<br><br> <br><br>SDK only holds weak references to the processor, you should guarantee its Life Time. |
|config |VideoPreprocessorConfig |Customize the settings applicable to the video pre\-processor. See [VideoPreprocessorConfig](https://docs.byteplus.com/en/docs/12/docs-70098#VideoPreprocessorConfig).<br><br> <br><br>Currently, the 'required_pixel_format 'in'config' only supports: 'kVideoPixelFormatI420' and'kVideoPixelFormatUnknown ':<br><br><br> <br><br>* When set to'kVideoPixelFormatUnknown', the RTC SDK gives the format of the video frame for processing by the processor, that is, the format of the acquisition.<br><br>   You can get the actual captured video frame format and pixel type by [VideoBufferType](https://docs.byteplus.com/en/docs/12/docs-70098#VideoBufferType) and [VideoPixelFormat](https://docs.byteplus.com/en/docs/12/docs-70098#VideoPixelFormat).<br><br>* When set to 'kVideoPixelFormatI420', the RTC SDK converts the captured video frames into the corresponding format for preprocessing. This method call fails when<br><br>* Is set to another value. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* For Windows platforms, the preprocessed video frame format returned only supports'kVideoPixelFormatI420 '

* For Windows platforms, setting the required_pixel_format in'config' to'kVideoPixelFormatI420 'can bring some performance optimization by avoiding format conversion.

* When this interface is repeatedly called, only the last call takes effect. The effects do not stack.

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
|type |ZoomConfigType |Required. Identifying which type the `size` is referring to. Refer to [ZoomConfigType](https://docs.byteplus.com/en/docs/12/docs-70098#ZoomConfigType). |
|size |float |Required. Reserved to three decimal places. It defaults to `0`.<br><br> <br><br>The meaning and range vary from different `type`s. If the scale or moving distance exceeds the range, the limit is taken as the result.<br><br><br> <br><br>* `kZoomConfigTypeFocusOffset`: Increase or decrease the scaling factor. Range: [0, 7]. For example, when it is set to 0.5 and [setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvideodigitalzoomcontrol) is called to zoom in, the scale will increase `0.5`. The scale ranges [1，8] and defaults to `1`, which means an original size.<br><br>* `kZoomConfigTypeMoveOffset`：Ratio of the distance to the border of video images. It ranges [0, 0.5] and defaults to `0`, which means no offset. When you call [setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvideodigitalzoomcontrol) and choose `CAMERA_MOVE_LEFT`, the moving distance is size x original width. While for the `CAMERA_MOVE_UP`, the moving distance is size x original height. Suppose that a video spans 1080 px and the `size` is set to `0.5` so that the distance would be 0.5 x 1080 px = 540 px. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* Only one size can be set for a single call. You must call this API to pass values respectively if you intend to set multiple `size`s.

* As the default `size` is `0`, you must call this API before performing any digital zoom control by calling [setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvideodigitalzoomcontrol) or [startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startvideodigitalzoomcontrol).

### setVideoDigitalZoomControl

```cpp
virtual int setVideoDigitalZoomControl(ZoomDirectionType direction) = 0;
```

> Available since 3.51

Digitally zoom or move the local video image once. This action affects both the local video preview and the published stream.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|direction |ZoomDirectionType |Action of the digital zoom control. Refer to [ZoomDirectionType](https://docs.byteplus.com/en/docs/12/docs-70098#ZoomDirectionType). |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* As the default offset is `0`, you must call [setVideoDigitalZoomConfig](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvideodigitalzoomconfig) before this API.

* You can only move video images after they are magnified via this API or [startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startvideodigitalzoomcontrol).

* When you request an out\-of\-range scale or movement, SDK will execute it with the limits. For example, when the image has been moved to the border, the image cannot be zoomed out, or has been magnified to 8x.

* Call [startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startvideodigitalzoomcontrol) to have a continuous and repeatedly digital zoom control.

* Mobile devices can control the optical zoom of the camera, see `setCameraZoomRatio`.

### startVideoDigitalZoomControl

```cpp
virtual int startVideoDigitalZoomControl(ZoomDirectionType direction) = 0;
```

> Available since 3.51

Continuous and repeated digital zoom control. This action affects both the video preview locally and the stream published.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|direction |ZoomDirectionType |Action of the digital zoom control. Refer to [ZoomDirectionType](https://docs.byteplus.com/en/docs/12/docs-70098#ZoomDirectionType). |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* As the default offset is `0`, you must call [setVideoDigitalZoomConfig](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvideodigitalzoomconfig) before this API.

* You can only move video images after they are magnified via this API or [setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvideodigitalzoomcontrol).

* The control process stops when the scale reaches the limit, or the images have been moved to the border. If the next action exceeds the scale or movement range, SDK will execute it with the limits.

* Call [stopVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stopvideodigitalzoomcontrol) to stop the ongoing zoom control.

* Call [setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvideodigitalzoomcontrol) to have a one\-time digital zoom control.

* Mobile devices can control the optical zoom of the camera, see `setCameraZoomRatio`.

### stopVideoDigitalZoomControl

```cpp
virtual int stopVideoDigitalZoomControl() = 0;
```

> Available since 3.51

Stop the ongoing digital zoom control instantly.

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

Refer to [startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startvideodigitalzoomcontrol) for starting digital zooming.

### sendSEIMessage

```cpp
virtual int sendSEIMessage(
    const uint8_t* message,
    int length,
    int repeat_count,
    SEICountPerFrame mode
) = 0;
```

 Sends SEI data.

In a video call scenario, SEI is sent with the video frame, while in a voice call scenario, SDK will automatically publish a black frame with a resolution of 16 × 16 pixels to carry SEI data.

In a voice call, you should set this parameter to `kStreamIndexMain`, otherwise the SEI data is discarded and cannot be sent to the remote user.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|message |const uint8_t\* |SEI data. |
|length |int |SEI data length. No more than 4 KB SEI data per frame is recommended. |
|repeat_count |int |Number of times a message is sent repeatedly. The value range is [0, max{29, %{video frame rate}\-1}]. Recommended range: [2,4].<br><br> <br><br>After calling this API, the SEI data will be added to a consecutive `repeat_count+1` number of video frames starting from the current frame. |
|mode |SEICountPerFrame |SEI sending mode. See [SEICountPerFrame](https://docs.byteplus.com/en/docs/12/docs-70098#SEICountPerFrame). |

**Return Value**

* \>= 0: The number of SEIs to be added to the video frame

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* We recommend the number of SEI messages per second should not exceed the current video frame rate. In a voice call, the blank\-frame rate is 15 fps.

* We recommended using the same sending mode from the start to the end of the program.

* In a voice call, this API can be called to send SEI data only in internal capture mode.

* In a video call, the custom captured video frame can also be used for sending SEI data if the original video frame contains no SEI data, otherwise calling this method will not take effect.

* Each video frame carries only the SEI data received within 2s before and after. In a voice call scenario, if no SEI data is sent within 1min after calling this API, SDK will automatically cancel publishing black frames.

* After the message is sent successfully, the remote user who subscribed your video stream will receive [onSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onseimessagereceived).

* When you switch from a voice call to a video call, SEI data will automatically start to be sent with normally captured video frames instead of black frames.

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

Before calling this API, you must call [setLiveMode](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-setlivemode) and set the room live mode to `kRoomLiveModeSoloHost`.

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

### getVideoDeviceManager

```cpp
virtual IVideoDeviceManager* getVideoDeviceManager() = 0;
```

Create a video Device Management instance

**Return Value**

Video Device Management instance. See [IVideoDeviceManager](https://docs.byteplus.com/en/docs/12/14184#IVideoDeviceManager)

### getAudioDeviceManager

```cpp
virtual IAudioDeviceManager* getAudioDeviceManager() = 0;
```

Device audio management interface creation

**Return Value**

Audio Device Management interface

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
|config |RecordingConfig |Local recording parameter configuration. See [RecordingConfig](https://docs.byteplus.com/en/docs/12/docs-70098#RecordingConfig) |
|recording_type |RecordingType |Local recording media type. See [RecordingType](https://docs.byteplus.com/en/docs/12/docs-70098#RecordingType).<br><br> <br><br>Note: Screen stream only supports recording video (kRecordingTypeVideoOnl); Main stream supports recording all types. |

**Return Value**

* 0: normal

* \-1: Parameter setting exception

* \-2: The current version of the SDK does not support this Feature, please contact technical support staff

**Notes**

* You must join a room before calling this method.

* After calling this method, you will receive an [onRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onrecordingstateupdate) callback.

* If the recording is normal, the system will notify the recording progress through [onRecordingProgressUpdate](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onrecordingprogressupdate) Callback every second.

### stopFileRecording

```cpp
virtual int stopFileRecording() = 0;
```

Stop local recording

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* Call [startFileRecording](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startfilerecording) After starting local recording, you must call this method to stop recording.

* After calling this method, you will receive an [onRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onrecordingstateupdate) callback prompting you to record the result.

### startAudioRecording

```cpp
virtual int startAudioRecording(AudioRecordingConfig& config) = 0;
```

Starts recording audio communication and generates the local file.

If you call this API before or after joining the room without internal audio capture, then the recording task can still begin but the data will not be recorded in the local files. Only when you call [startAudioCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startaudiocapture) to enable internal audio capture, the data will be recorded in the local files.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|config |AudioRecordingConfig& |See [AudioRecordingConfig](https://docs.byteplus.com/en/docs/12/docs-70098#AudioRecordingConfig). |

**Return Value**

* 0: `kReturnStatusSuccess`: Success

* \-2: `kReturnStatusParameterErr`: Invalid parameters

* \-3: `kReturnStatusWrongState`: Not valid in this SDK. Please contact the technical support.

**Notes**

* All audio effects are valid in the file. Mixed audio file is not included in the file.

* Call [stopAudioRecording](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stopaudiorecording) to stop recording.

* You can call this API before and after joining the room. If this API is called before you join the room, you need to call [stopAudioRecording](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stopaudiorecording) to stop recording. If this API is called after you join the room, the recording task ends automatically. If you join multiple rooms, audio from all rooms are recorded in one file.

* After calling the API, you'll receive [onAudioRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onaudiorecordingstateupdate).

### stopAudioRecording

```cpp
virtual int stopAudioRecording() = 0;
```

Stop audio recording.

**Return Value**

* 0: Success

* <0: Failure

**Notes**

Call [startAudioRecording](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startaudiorecording) to start the recording task.

### enableExternalSoundCard

```cpp
virtual int enableExternalSoundCard(bool enable) = 0;
```

Enable the audio processing mode for an external sound card.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |bool |* true: enable<br><br>* false: disable (by default) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* When you use an external sound card for audio capture, enable this mode for better audio quality.

* When using the mode, you can only use earphones. If you need to use internal or external speaker, disable this mode.

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

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

Call this API before [joinRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-joinroom) and [startAudioCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startaudiocapture).

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
|type |uint64_t |List of preset problems. See [ProblemFeedbackOption](https://docs.byteplus.com/en/docs/12/docs-70098#ProblemFeedbackOption) |
|info |const ProblemFeedbackInfo\* |Specific description of other problems other than the preset problem, and room's information. See [ProblemFeedbackInfo](https://docs.byteplus.com/en/docs/12/docs-70098#ProblemFeedbackInfo) |

**Return Value**

* 0: Success.

* \-3: Failure.

**Notes**

If the user is in the room when reporting, the report is associated with the room or rooms where the user is currently located;

If the user is not in the room when reporting, the report leads to the previously exited Room.

### getAudioEffectPlayer

```cpp
virtual IAudioEffectPlayer* getAudioEffectPlayer() = 0;
```

> Available since 3.53

Create an instance for audio effect player.

**Return Value**

See [IAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer).

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

Media player instance. See [IMediaPlayer](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer).

### login

```cpp
virtual int login(
    const char* token,
    const char* uid
) = 0;
```

Sign in to the RTS server.

Sign in to call [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-sendusermessageoutsideroom) and [sendServerMessage](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-sendservermessage) to send P2P messages or send messages to a server without joining the RTC room.

```Plain Text
   To sign out, call [logout](#IRTCEngine-logout).
```

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|token |const char\* |Token is required during login for authentication.<br><br> <br><br>This Token is different from that required by calling joinRoom. You can assign any value even null to `roomId` to generate a login token. During developing and testing, you can use temporary tokens generated on the console. Deploy the token generating application on your server. |
|uid |const char\* |User ID<br><br> <br><br>User ID is unique within one appid. |

**Return Value**

* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for specific reasons.

**Notes**

You will receive [onLoginResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onloginresult) after calling this API and signing in successfully. But remote users will not receive notification about that.

### logout

```cpp
virtual int logout() = 0;
```

Sign out of the RTS server.

After calling this API to sign out, you cannot call methods related to out\-of\-room messages and end\-to\-server messages or receive related callbacks.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* Before calling this interface to log out, you must call [login](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-login) to sign in.

* After local users call this method to log out, they will receive the result of the [onLogout](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onlogout) callback notification, and remote users will not receive the notification.

### updateLoginToken

```cpp
virtual int updateLoginToken(const char* token) = 0;
```

Update the Token

Token used by the user to sign in has a certain valid period. When the Token expires, you need to call this method to update the login Token information.

When calling the [login](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-login) method to sign in, if an expired token is used, the login will fail and you will receive an [onLoginResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onloginresult) callback notification with an error code of kLoginErrorCodeInvalidToken. You need to reacquire the token and call this method to update the token.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|token |const char\* |Updated dynamic key |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* If the token is invalid and the login fails, call this method. After updating the token, the SDK will automatically log back in, and the user does not need to call the [login](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-login) method.

* If the token expires after you have successfully signed in, it will not be affected. An expired Token error will be notified to the user the next time you log in with an expired Token, or when you log in again due to a disconnection due to poor local network conditions.

### setServerParams

```cpp
virtual int setServerParams(
    const char* signature,
    const char* url
) = 0;
```

Set application server parameters

Before the client side calls [sendServerMessage](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-sendservermessage) or [sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-sendserverbinarymessage) to send a message to the application server, a valid signature and application server address must be set.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|signature |const char\* |Dynamic signature. The App server may use the signature to verify the source of messages.<br><br> <br><br>You need to define the signature yourself. It can be any non\-empty string. It is recommended to encode information such as UID into the signature.<br><br> <br><br>The signature will be sent to the address set through the "url" parameter in the form of a POST request. |
|url |const char\* |The address of the application server |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* The user must call [login](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-login) to sign in before calling this interface.

* After calling this interface, the SDK will use [onServerParamsSetResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onserverparamssetresult) to return the corresponding result.

### getPeerOnlineStatus

```cpp
virtual int getPeerOnlineStatus(const char* peer_user_id) = 0;
```

Query the sign\-in status of the remote or local user

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|peer_user_id |const char\* |User ID to be queried |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* [login](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-login) must be called before this interface can be called.

* After calling this interface, the SDK notifies the query result using the [onGetPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-ongetpeeronlinestatus) callback.

* Before sending an out\-of\-room message, the user can know whether the peer user is signed in through this API to decide whether to send a message. You can also check your sign\-in status through this API.

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
|config |MessageConfig |Message type, see [MessageConfig](https://docs.byteplus.com/en/docs/12/docs-70098#MessageConfig). |

**Return Value**

* \> 0: Sent successfully, return the number of the sent message, increment from 1.

**Notes**

* Before calling this API, make sure you have enabled the [Advanced RTS functions](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode) in the RTC console.

> If this feature is enabled while the SDK is running, you must re\-initialize the engine for the configuration to take effect.

* You must call [login](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-login) to complete the login before you can send a message outside the room.

* After the user calls this API to send a text message, he will receive an [onUserMessageSendResultOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onusermessagesendresultoutsideroom) callback to know whether the message was successfully sent.

* If the text message is sent successfully, the user specified by uid receives the message via the [onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onusermessagereceivedoutsideroom) callback.

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
|config |MessageConfig |Message type, see [MessageConfig](https://docs.byteplus.com/en/docs/12/docs-70098#MessageConfig). |

**Return Value**

* \> 0: sent successfully, return the number of the sent message, increment from 1.

* \-1: Sending failed due to an empty message.

**Notes**

* Before calling this API, make sure you have enabled the [Advanced RTS functions](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode) in the RTC console.

> If this feature is enabled while the SDK is running, you must re\-initialize the engine for the configuration to take effect.

* [login](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-login) must be called before sending out\-of\-room binary messages.

* After the user calls this API to send a binary message, he will receive an [onUserMessageSendResultOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onusermessagesendresultoutsideroom) callback to notify whether the message was sent successfully.

* If the binary message is sent successfully, the user specified by uid will receive the message through the [onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom) callback.

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

* Before sending a text message to the application server, you must first call [login](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-login) to complete the login, and then call [setServerParams](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setserverparams) Set up the application server.

* After calling this interface, you will receive an [onServerMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onservermessagesendresult) callback to inform the message sender whether the message was sent successfully.

* If the text message is sent successfully, the application server that previously called [setServerParams](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setserverparams) will receive the message.

### sendServerBinaryMessage

```cpp
virtual int64_t sendServerBinaryMessage(
    int length,
    const uint8_t* message
) = 0;
```

The client side sends binary messages to the application server (P2Server)

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|length |int |Length of binary string |
|message |const uint8_t\* |Binary message content sent. Message does not exceed 64 KB. |

**Return Value**

* \> 0: sent successfully, return the number of the sent message, increment from 1.

* \-1: Sending failed due to an empty message.

**Notes**

* Before calling this API, make sure you have enabled the [Advanced RTS functions](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode) in the RTC console.

> If this feature is enabled while the SDK is running, you must re\-initialize the engine for the configuration to take effect.

* Before sending a binary message to the application server, you must first call [login](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-login) to complete the login, and then call [setServerParams](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setserverparams) Set up the application server.

* After calling this interface, you will receive an [onServerMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onservermessagesendresult) callback to inform the message sender that the sending succeeded or failed.

* If the binary message is sent successfully, the application server that previously called [setServerParams](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setserverparams) will receive the message.

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
|expected_uplink_bitrate |int |Expected uplink bandwidth, unit: kbps<br><br>Range: {0, [100\-10000]}, `0`: Auto, that RTC will set the highest bitrate. |
|is_test_downlink |bool |Whether to detect downlink bandwidth |
|expected_downlink_biterate |int |Expected downlink bandwidth, unit: kbps<br><br>Range: {0, [100\-10000]}, `0`: Auto, that RTC will set the highest bitrate. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* After calling this interface, you will receive [onNetworkDetectionResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onnetworkdetectionresult) within 3s and every 2s thereafter notifying the probe result;

* If the probe stops, you will receive [onNetworkDetectionStopped](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onnetworkdetectionstopped) notify that probing has stopped.

### stopNetworkDetection

```cpp
virtual int stopNetworkDetection() = 0;
```

Stop pre\-call network probe

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* After calling this interface, you will receive [onNetworkDetectionStopped](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onnetworkdetectionstopped) notifying that the probing has stopped.

### setScreenAudioSourceType

```cpp
virtual int setScreenAudioSourceType(AudioSourceType source_type) = 0;
```

Set the screen audio acquisition method (internal acquisition/custom acquisition)

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|source_type |AudioSourceType |Screen audio input source type. See [AudioSourceType](https://docs.byteplus.com/en/docs/12/docs-70098#AudioSourceType) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* The default acquisition method is internal to the RTC SDK.

* If it is set to internal collection, you must call [startScreenAudioCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startscreenaudiocapture-2) to start collection.

* If it is set to custom collection, you must call [pushScreenAudioFrame](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-pushscreenaudioframe) to customize the collected screen audio frame Push to the RTC SDK.

* Whether it is an internal capture or a custom capture, you must call [publishStreamAudio](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-publishstreamaudio) to push the captured screen audio to the remote end.

### setScreenAudioChannel

```cpp
virtual int setScreenAudioChannel(AudioChannel channel) = 0;
```

Set the audio channel of the screen\-sharing audio stream

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|channel |AudioChannel |The number of Audio channels. See [AudioChannel](https://docs.byteplus.com/en/docs/12/docs-70098#AudioChannel). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

### startScreenAudioCapture

```cpp
virtual int startScreenAudioCapture(const char device_id[MAX_DEVICE_ID_LENGTH]) = 0;
```

> Available since 3.59

When sharing the screen, start using RTC SDK internal collection method to collect screen audio.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|device_id |const char[MAX_DEVICE_ID_LENGTH] |For macOS, device_id means ID of the virtual device; For Windows, device_id means process name that shares (for example: QQMusic.exe). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* The call of this API takes effect only when you are using RTC SDK to record screen. You will get a warning by [onAudioDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onaudiodevicewarning) after calling this API when the video source is set to an external recorder.

* After collection, you also need to call [publishStreamAudio](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-publishstreamaudio) to collect the screen audio Push to the far end.

* To turn off screen audio internal capture, call [stopScreenAudioCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stopscreenaudiocapture).

### stopScreenAudioCapture

```cpp
virtual int stopScreenAudioCapture() = 0;
```

Stop RTC SDK's device audio recorder.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* The call of this API takes effect only when you are using RTC SDK to record screen. You will get a warning by [onAudioDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onaudiodevicewarning) after calling this API when the video source is set to an external recorder.

* This API can only stop the screen capture by the RTC SDK. If the video source has been set to external recorder, the call of this API will fail with a warning message. You need to stop it in the external recorder.

* To start the device audio recording, call [startScreenAudioCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startscreenaudiocapture-2).

### pushScreenAudioFrame

```cpp
virtual int pushScreenAudioFrame(IAudioFrame* frame) = 0;
```

Using a custom capture method, when capturing screen audio during screen sharing, push the audio frame to the RTC SDK for encoding and other processing.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|frame |IAudioFrame\* |Audio data frame. See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70098#IAudioFrame)<br><br><br>* The audio sampling format is S16. The data format within the audio buffer must be PCM data, and its capacity should be samples × frame.channel × 2.<br><br>* A specific sample rate and the number of channels must be specified; it is not supported to set them to automatic. |

**Return Value**

Method call result

* 0: Setup succeeded.

* < 0: Setup failed. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* Before calling this interface to push custom collected audio data during screen sharing, you must call [setScreenAudioSourceType](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setscreenaudiosourcetype) Enable custom capture of screen audio.

* You should call this method every 10 milliseconds to push a custom captured audio frame. A push audio frame should contain frame.sample _rate/100 audio sample points. For example, if the sampling rate is 48000Hz, 480 sampling points should be pushed each time.

* After calling this interface to push the custom captured audio frame to the RTC SDK, you must call [publishStreamAudio](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-publishstreamaudio) to push the captured screen audio to the remote end. Audio frame information pushed to the RTC SDK is lost before calling [publishStreamAudio](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-publishstreamaudio).

### startPushMixedStream

```cpp
virtual int startPushMixedStream(
    const char* task_id,
    MixedStreamPushTargetConfig push_target_config,
    IMixedStreamConfig* config
) = 0;
```

> Available since 3.60. Since version 3.60, this interface replaces the `startPushMixedStreamToCDN` and `startPushPublicStream` methods for the functions described below. If you have upgraded to version 3.60 or later and are still using these two methods, please migrate to this interface.

Specifies the streams to be mixed and initiates the task to push the mixed stream to CDN or WTN.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|task_id |const char\* |Task ID. The length should not exceed 127 bytes.<br><br> <br><br>When [IMixedStreamConfig](https://docs.byteplus.com/en/docs/12/docs-70098#IMixedStreamConfig) is set to `PushTargetType = 0`, this ID is used to identify the task.<br><br> <br><br>You may want to push more than one mixed stream to CDN from the same room. When you do that, use different ID for corresponding tasks; if you will start only one task, use an empty string.<br><br> <br><br>When `PushTargetType = 1` (WTN stream), this parameter is invalid. Pass an empty string. |
|push_target_config |MixedStreamPushTargetConfig |Push target config, such as the push URL and WTN stream ID. See [MixedStreamPushTargetConfig](https://docs.byteplus.com/en/docs/12/docs-70098#MixedStreamPushTargetConfig). |
|config |IMixedStreamConfig\* |Configurations to be set when pushing streams to CDN or WTN. See [IMixedStreamConfig](https://docs.byteplus.com/en/docs/12/docs-70098#IMixedStreamConfig). |

**Return Value**

* 0: Success. You can get notified the result of the task and the events in the process of pushing the stream to CDN via [onMixedStreamEvent](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onmixedstreamevent).

* !0: Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* Subscribe to the Push\-to\-CDN and the WTN stream notifications in the [console](https://console.byteplus.com/rtc/cloudRTC?tab=callback?from=doc) to receive notifications about task status changes. When calling this API repeatedly, subsequent calls to this API will trigger both [TranscodeStarted](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#transcodestarted) and [TranscodeUpdated](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#transcodeupdated) callbacks.

* Call [stopPushMixedStream](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stoppushmixedstream) to stop pushing streams to CDN.

* Call [updatePushMixedStream](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-updatepushmixedstream) to update part of the configurations of the task.

### updatePushMixedStream

```cpp
virtual int updatePushMixedStream(
    const char* task_id,
    MixedStreamPushTargetConfig push_target_config,
    IMixedStreamConfig* config
) = 0;
```

> Available since 3.60. Since version 3.60, this interface replaces the `updatePushMixedStreamToCDN` and `updatePublicStreamParam` methods for the functions described below. If you have upgraded to version 3.60 or later and are still using these two methods, please migrate to this interface.

Update the task configuration during the task started via [startPushMixedStream](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startpushmixedstream). You will be informed of the change via the [onMixedStreamEvent](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onmixedstreamevent) callback.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|task_id |const char\* |Task ID. Specifies of the task to be updated.<br><br> <br><br>When [IMixedStreamConfig](https://docs.byteplus.com/en/docs/12/docs-70098#IMixedStreamConfig) is set to `PushTargetType = 0`, this ID is used to identify the task. |
|push_target_config |MixedStreamPushTargetConfig |Push target config, such as the push url and WTN stream ID. See [MixedStreamPushTargetConfig](https://docs.byteplus.com/en/docs/12/docs-70098#MixedStreamPushTargetConfig). |
|config |IMixedStreamConfig\* |Configurations that you want to update. See [IMixedStreamConfig](https://docs.byteplus.com/en/docs/12/docs-70098#IMixedStreamConfig) for specific indications. You can update any property for the task unless it is specified as unavailable for updates.<br><br> <br><br>If you left some properties blank, you can expect these properties to be set to their default values. |

**Return Value**

* 0: Success.

* !0: Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

### stopPushMixedStream

```cpp
virtual int stopPushMixedStream(
    const char* task_id,
    MixedStreamPushTargetType target_type
) = 0;
```

> Available since 3.60. Since version 3.60, this interface replaces the `stopPushStreamToCDN` method for stopping the push of mixed streams to CDN or WTN. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this interface.

Stops the task started via [startPushMixedStream](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startpushmixedstream).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|task_id |const char\* |Task ID. Specifies of which pushing task you want to update the parameters. |
|target_type |MixedStreamPushTargetType |See [MixedStreamPushTargetType](https://docs.byteplus.com/en/docs/12/docs-70098#MixedStreamPushTargetType). |

**Return Value**

* 0: Success

* !0: Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

### startPushSingleStream

```cpp
virtual int startPushSingleStream(
    const char* task_id,
    PushSingleStreamParam& param
) = 0;
```

> Available since 3.60. Since version 3.60, this interface replaces the `startPushSingleStreamToCDN` method. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this interface.

Pushes a single media stream to CDN or RTC room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|task_id |const char\* |Task ID.<br><br> <br><br>You may want to start more than one task to push streams to CDN or RTC room. When you do that, use different IDs for corresponding tasks; if you will start only one task, use an empty string. |
|param |PushSingleStreamParam& |Configurations for pushing a single stream to CDN or RTC room. See [PushSingleStreamParam](https://docs.byteplus.com/en/docs/12/docs-70098#PushSingleStreamParam). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* Before calling this API，you need to enable Push to CDN on the [console](https://console.byteplus.com/rtc/workplaceRTC).

* After calling this API, you will be informed of the result and errors during the pushing process with [onSingleStreamEvent](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onsinglestreamevent).

* Subscribe to the Push\-to\-CDN and the WTN stream notifications in the [console](https://console.byteplus.com/rtc/cloudRTC?tab=callback?from=doc) to receive notifications about task status changes. When calling this API repeatedly, subsequent calls to this API will trigger both [TranscodeStarted](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#transcodestarted) and [TranscodeUpdated](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#transcodeupdated) callbacks.

* Call [stopPushSingleStream](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stoppushsinglestream) to stop the task.

* Since this API does not perform encoding and decoding, the video stream pushed to RTMP will change according to the resolution, encoding method, and whether the camera on the publisher side is turned off.

### stopPushSingleStream

```cpp
virtual int stopPushSingleStream(const char* task_id) = 0;
```

> Available since 3.60. Since version 3.60, this interface replaces the `stopPushStreamToCDN` method for stopping the push of single media streams to CDN. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this interface.

Stops the task started via [startPushSingleStream](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startpushsinglestream).

This method stops pushing a single stream to CDN.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|task_id |const char\* |Task ID. Specifies the task you want to stop. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

### enableAudioPropertiesReport

```cpp
virtual int enableAudioPropertiesReport(const AudioPropertiesConfig& config) = 0;
```

Enable audio information prompts. After that, you will receive [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onlocalaudiopropertiesreport), [onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onremoteaudiopropertiesreport), and [onActiveSpeaker](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onactivespeaker).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|config |const AudioPropertiesConfig& |See [AudioPropertiesConfig](https://docs.byteplus.com/en/docs/12/docs-70098#AudioPropertiesConfig) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

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
|volume |int |The ratio between the playing volume of the original volume. The range is `[0, 400]` with overflow protection. The unit is %.<br><br> <br><br>For better audio quality, you are recommended to set the value to `[0, 100]`. |

**Return Value**

result

* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus).

**Notes**

Assume that a remote user A is always within the scope of the adjusted target users:

* When this API is used together with [setRemoteRoomAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-setremoteroomaudioplaybackvolume), the volume of local listening user A is the volume set by the API called later;

* When this API is used together with the [setPlaybackVolume](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setplaybackvolume), the volume of local listening user A will be the superposition of the two set volume effects.

* When you call this API to set the remote stream volume, if the remote user leaves the room, the setting will be invalid.

### enableVocalInstrumentBalance

```cpp
virtual int enableVocalInstrumentBalance(bool enable) = 0;
```

Enables/disables the loudness equalization function.

If you call this API with the parameter set to True, the loudness of user's voice will be adjusted to \-16lufs. If then you also call setAudioMixingLoudness and import the original loudness of the audio data used in audio mixing, the loudness will be adjusted to \-20lufs when the audio data starts to play.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |bool |Whether to enable loudness equalization function:<br><br><br> <br><br>* true: Yes<br><br>* false: No |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

You must call this API before starting to play the audio file with [start](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-start).

### enablePlaybackDucking

```cpp
virtual int enablePlaybackDucking(bool enable) = 0;
```

Enables/disables the playback ducking function. This function is usually used in scenarios where short videos or music will be played simultaneously during RTC calls.

With the function on, if remote voice is detected, the local media volume of RTC will be lowered to ensure the clarity of the remote voice. If remote voice disappears, the local media volume of RTC restores.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |bool |Whether to enable playback ducking:<br><br><br> <br><br>* true: Yes<br><br>* false: No |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

### registerLocalEncodedVideoFrameObserver

```cpp
virtual int registerLocalEncodedVideoFrameObserver(ILocalEncodedVideoFrameObserver* observer) = 0;
```

Register a local video frame observer.

This method applies to both internal capturing and custom capturing.

After calling this API, SDK triggers [onLocalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70096#ILocalEncodedVideoFrameObserver-onlocalencodedvideoframe) whenever a video frame is captured.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|observer |ILocalEncodedVideoFrameObserver\* |Local video frame observer. See [ILocalEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70096#ILocalEncodedVideoFrameObserver). You can cancel the registration by setting it to `nullptr`. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

You can call this API before or after entering the RTC room. Calling this API before entering the room ensures that video frames are monitored and callbacks are triggered as early as possible.

### registerRemoteEncodedVideoFrameObserver

```cpp
virtual int registerRemoteEncodedVideoFrameObserver(IRemoteEncodedVideoFrameObserver* observer) = 0;
```

Video data callback after registering remote encoding.

After registration, when the SDK detects a remote encoded video frame, it will trigger the [onRemoteEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IRemoteEncodedVideoFrameObserver-onremoteencodedvideoframe) callback

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|observer |IRemoteEncodedVideoFrameObserver\* |Remote encoded video data monitor. See [IRemoteEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70096#IRemoteEncodedVideoFrameObserver) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* See [Custom Video Encoding and Decoding](https://docs.byteplus.com/byteplus-rtc/docs/82921#custom-video-decoding) for more details about custom video decoding.

* This method applies to manual subscription mode and can be called either before or after entering the Room. It is recommended to call it before entering the room.

* The engine needs to be unregistered before it is destroyed. Call this method to set the parameter to nullptr.

### setExternalVideoEncoderEventHandler

```cpp
virtual int setExternalVideoEncoderEventHandler(IExternalVideoEncoderEventHandler* encoder_handler) = 0;
```

Register custom encoded frame push event callback

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|encoder_handler |IExternalVideoEncoderEventHandler\* |Custom encoded frame callback class. See [IExternalVideoEncoderEventHandler](https://docs.byteplus.com/en/docs/12/docs-70096#IExternalVideoEncoderEventHandler) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* This method needs to be called before entering the room.

* The engine needs to be unregistered before it is destroyed. Call this method to set the parameter to nullptr.

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
|video_index |int |The corresponding encoded stream subscript, starting from 0, if you call [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvideoencoderconfig) to set multiple streams, the number here must be consistent with it |
|video_stream |IEncodedVideoFrame\* |Encoded stream video frame information. See [IEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70098#IEncodedVideoFrame). |

**Return Value**

API call result:

* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for specific reasons.

**Notes**

* Currently, only video frames in H264 and ByteVC1 formats are supported, and the video stream protocol must be in an Annex B format.

* This function runs within the user calling thread

* Before pushing a custom encoded video frame, you must call [setVideoSourceType](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvideosourcetype) to switch the video input source to the custom encoded video source.

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
|config |VideoDecoderConfig |Video decoding method. See [VideoDecoderConfig](https://docs.byteplus.com/en/docs/12/docs-70098#VideoDecoderConfig). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* When you want to custom decode a remote stream, you need to call [registerRemoteEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-registerremoteencodedvideoframeobserver) to register the remote video stream monitor, and then call the interface to set the decoding method to custom decoding. The monitored video data will be called back through [onRemoteEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IRemoteEncodedVideoFrameObserver-onremoteencodedvideoframe).

* Since version 3.56, for automatic subscription, you can set the `RoomId` and `UserId` of `key` as `nullptr`. In this case, the decoding settings set by calling the API apply to all remote main streams or screen sharing streams based on the `StreamIndex` value of `key`.

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

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* This method is only suitable for manual subscription mode and is used after successful subscription to the remote stream.

* This method is suitable for calling [setVideoDecoderConfig](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setvideodecoderconfig) to turn on the custom decoding function, and the custom decoding fails

### sendStreamSyncInfo

```cpp
virtual int sendStreamSyncInfo(
    const uint8_t* data,
    int32_t length,
    const StreamSyncInfoConfig& config
) = 0;
```

Send audio stream synchronization information. The message is sent to the remote end through the audio stream and synchronized with the audio stream. After the API is successfully called, the remote user will receive a [onStreamSyncInfoReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onstreamsyncinforeceived) callback.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|data |const uint8_t\* |Message content. |
|length |int32_t |Message length. Message length must be [1,16] bytes. |
|config |const StreamSyncInfoConfig& |For configuration of media stream information synchronization. See [StreamSyncInfoConfig](https://docs.byteplus.com/en/docs/12/docs-70098#StreamSyncInfoConfig). |

**Return Value**

* \> = 0: Message sent successfully. Returns the number of successful sends.

* \-1: Message sending failed. Message length greater than 16 bytes.

* \-2: Message sending failed. The content of the incoming message is empty.

* \-3: Message sending failed. This screen stream was not published when the message was synchronized through the screen stream.

* \-4: Message sending failed. This audio stream is not yet published when you synchronize messages with an audio stream captured by a microphone or custom device, as described in [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-70097#ErrorCode).

**Notes**

* Regarding the frequency, we recommend no more than 50 calls per second.

* When using `kRoomProfileTypeInteractivePodcast` as room profile, the data will be delivered. For other room profiles, the data may be lost when the local user is muted.

### setLocalVoicePitch

```cpp
virtual int setLocalVoicePitch(int pitch) = 0;
```

Change local voice to a different key, mostly used in Karaoke scenarios.

You can adjust the pitch of local voice such as ascending or descending with this method.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|pitch |int |The value that is higher or lower than the original local voice within a range from \-12 to 12. The default value is 0, i.e. No adjustment is made.<br><br> <br><br>The difference in pitch between two adjacent values within the value range is a semitone, with positive values indicating an ascending tone and negative values indicating a descending tone, and the larger the absolute value set, the more the pitch is raised or lowered.<br><br> <br><br>Out of the value range, the setting fails and triggers [onWarning](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onwarning) callback, indicating `WARNING_CODE_SET_SCREEN_STREAM_INVALID_VOICE_PITCH` for invalid value setting with [WarningCode](https://docs.byteplus.com/en/docs/12/docs-70097#WarningCode). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

### setVideoWatermark

```cpp
virtual int setVideoWatermark(
    const char* image_path,
    RTCWatermarkConfig config
) = 0;
```

Adds a watermark to the designated video stream.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|image_path |const char\* |The absolute path of the watermark image. The path should be less than 512 bytes.<br><br> <br><br>The watermark image should be in PNG or JPG format. |
|config |RTCWatermarkConfig |Watermark configurations. See [RTCWatermarkConfig](https://docs.byteplus.com/en/docs/12/docs-70098#RTCWatermarkConfig). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* Call [clearVideoWatermark](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-clearvideowatermark) to remove the watermark from the designated video stream.

* You can only add one watermark to one video stream. The newly added watermark replaces the previous one. You can call this API multiple times to add watermarks to different streams.

* If you mirror the preview, or the preview and the published stream, the watermark will also be mirrored locally, but the published watermark will not be mirrored.

* When you enable simulcast mode, the watermark will be added to all video streams, and it will be scaled down to smaller encoding configurations accordingly.

### clearVideoWatermark

```cpp
virtual int clearVideoWatermark() = 0;
```

Removes video watermark from designated video stream.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

### takeLocalSnapshot

```cpp
virtual long takeLocalSnapshot(ISnapshotResultCallback* callback) = 0;
```

Take a snapshot of the local video.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|callback |ISnapshotResultCallback\* |See [ISnapshotResultCallback](https://docs.byteplus.com/en/docs/12/docs-70096#ISnapshotResultCallback). |

**Return Value**

The index of the local snapshot task, starting from `1`.

**Notes**

* The snapshot is taken with all video effects on, like rotation, and mirroring.

* You can take the snapshot either using SDK internal video capture or customized capture.

### takeRemoteSnapshot

```cpp
virtual long takeRemoteSnapshot(
    const char* stream_id,
    ISnapshotResultCallback* callback
) = 0;
```

Take a snapshot of the remote video.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of stream |
|callback |ISnapshotResultCallback\* |See [ISnapshotResultCallback](https://docs.byteplus.com/en/docs/12/docs-70096#ISnapshotResultCallback). |

**Return Value**

The index of the remote snapshot task, starting from `1`.

### takeRemoteSnapshotToFile

```cpp
virtual long takeRemoteSnapshotToFile(
    const char* stream_id,
    const char* file_path
) = 0;
```

> Available since 3.60.

Takes a snapshot of the remote video stream and saves it as a JPG file at the specified local path.

After calling this method, the SDK triggers [onRemoteSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onremotesnapshottakentofile) to report whether the snapshot is taken successfully and provide details of the snapshot image.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of the remote video stream for taking snapshot. |
|file_path |const char\* |The absolute file path where the snapshot JPG file will be saved. The file extension must be `.jpg`. Ensure that the directory exists and is writable. Examples: `C:\\Users\\YourName\\Pictures\\snapshot.jpg`. |

**Return Value**

The index of the remote snapshot task, starting from `1`. The index can be used to track the task status or perform other management operations.

### takeLocalSnapshotToFile

```cpp
virtual long takeLocalSnapshotToFile(const char* file_path) = 0;
```

> Available since 3.60.

Takes a snapshot of the local video stream and saves it as a JPG file at the specified local path.

After calling this method, the SDK triggers [onLocalSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onlocalsnapshottakentofile) to report whether the snapshot is taken successfully and provide details of the snapshot image.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|file_path |const char\* |The absolute file path where the snapshot JPG file will be saved. The file extension must be `.jpg`. Ensure that the directory exists and is writable. Examples: `C:\\Users\\YourName\\Pictures\\snapshot.jpg`. |

**Return Value**

The index of the remote snapshot task, starting from `1`. The index can be used to track the task status or perform other management operations.

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
|file_path |const char\* |Set the path of the static image.<br><br> <br><br>You can use the absolute path (file://xxx). The maximum size for the path is 512 bytes.<br><br> <br><br>You can upload a .JPG, .JPEG, .PNG, or .BMP file.<br><br> <br><br>When the aspect ratio of the image is inconsistent with the video encoder configuration, keep the aspect\-ratio to scale the image and crop the longer sides. The framerate and the bitrate are consistent with the video encoder configuration. |

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

### startCloudProxy

```cpp
virtual int startCloudProxy(const CloudProxyConfiguration& configuration) = 0;
```

Start cloud proxy

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|configuration |const CloudProxyConfiguration& |cloud proxy information list. See [CloudProxyConfiguration](https://docs.byteplus.com/en/docs/12/docs-70098#CloudProxyConfiguration). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* Call this API before joining the room.

* Start pre\-call network detection after starting cloud proxy.

* After starting cloud proxy and connects the cloud proxy server successfully, receives [onCloudProxyConnected](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-oncloudproxyconnected).

* To stop cloud proxy, call [stopCloudProxy](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stopcloudproxy).

### stopCloudProxy

```cpp
virtual int stopCloudProxy() = 0;
```

Stop cloud proxy

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

To start cloud proxy, call [startCloudProxy](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startcloudproxy).

### startEchoTest

```cpp
virtual int startEchoTest(
    EchoTestConfig echo_test_config,
    unsigned int play_delay_time
) = 0;
```

Starts a call test.

Before entering the room, you can call this API to test whether your local audio/video equipment as well as the upstream and downstream networks are working correctly.

Once the test starts, SDK will record your sound or video. If you receive the playback within the delay range you set, the test is considered normal.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|echo_test_config |EchoTestConfig |Test configurations, see [EchoTestConfig](https://docs.byteplus.com/en/docs/12/docs-70098#EchoTestConfig). |
|play_delay_time |unsigned int |Delayed audio/video playback time specifying how long you expect to receive the playback after starting the test. The range of the value is [2,10] in seconds and the default value is 2. |

**Return Value**

API call result:

* 0: Success.

* \-2: Failure due to parameter exception.

* \-4: Failure because the user has joined a room.

* \-6: Failure for the testing is in progress.

* \-7: Failure for the request included neither video nor audio.

* \-8: Failure for the roomID is already used.

**Notes**

* Once you start the test, you can either call [stopEchoTest](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stopechotest) or wait until the test stops automatically after 60s, to start the next test or enter the room.

* All APIs related to device control and stream control called before this API are invalidated during the test and are restored after the test.

* All APIs related to device control, stream control, and room entry called during the test do not take effect, and you will receive [onWarning](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onwarning) with the warning code `kWarningCodeInEchoTestMode`.

* You will receive the test result from [onEchoTestResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onechotestresult).

### stopEchoTest

```cpp
virtual int stopEchoTest() = 0;
```

Stop the current call test.

After calling [startEchoTest](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startechotest), you must call this API to stop the test.

**Return Value**

API call result:

* 0: Success.

* \-3: Failure, no test is in progress.

**Notes**

After stopping the test with this API, all the system devices and streams are restored to the state they were in before the test.

### getNetworkTimeInfo

```cpp
virtual NetworkTimeInfo getNetworkTimeInfo() = 0;
```

Obtain the synchronization network time information.

**Return Value**

See [NetworkTimeInfo](https://docs.byteplus.com/en/docs/12/docs-70098#NetworkTimeInfo).

**Notes**

* When you call this API for the first time, you start synchronizing the network time information and receive the return value `0`. After the synchronization finishes, you will receive [onNetworkTimeSynchronized](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onnetworktimesynchronized). After that, calling this API will get you the correct network time.

* Under chorus scenario, participants shall start audio mixing at the same network time.

### startHardwareEchoDetection

```cpp
virtual int startHardwareEchoDetection(const char* test_audio_file_path) = 0;
```

Start echo detection before joining a room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|test_audio_file_path |const char\* |Absolute path of the music file for the detection. It is expected to encode with UTF\-8. The following files are supported: mp3, aac, m4a, 3gp, wav.<br><br> <br><br>We recommend to assign a music file whose duration is between 10 to 20 seconds.<br><br> <br><br>Do not pass a Silent file. |

**Return Value**

Method call result:

* 0: Success.

* \-1: Failure due to the ongoing process of the previous detection. Call [stopHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stophardwareechodetection) to stop it before calling this API again.

* \-2: Failure due to an invalid file path or file format.

**Notes**

* You can use this feature only when [RoomProfileType](https://docs.byteplus.com/en/docs/12/docs-70098#RoomProfileType) is set to `kRoomProfileTypeMeeting` or `kRoomProfileTypeMeetingRoom`.

* Before calling this API, ask the user for the permissions to access the local audio devices.

* Before calling this api, make sure the audio devices are active and keep the capture volume and the playback volume within a reasonable range.

* The detection result is passed as the argument of [onHardwareEchoDetectionResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onhardwareechodetectionresult).

* During the detection, the SDK is not able to respond to the other testing APIs, such as [startEchoTest](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startechotest)、[startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-startaudiodevicerecordtest) or [startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-startaudioplaybackdevicetest).

* Call [stopHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-stophardwareechodetection) to stop the detection and release the audio devices.

### stopHardwareEchoDetection

```cpp
virtual int stopHardwareEchoDetection() = 0;
```

Stop the echo detection before joining a room.

**Return Value**

Method call result:

* 0: Success.

* \-1: Failure.

**Notes**

* Refer to [startHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-starthardwareechodetection) for information on how to start an echo detection.

* We recommend calling this API to stop the detection once getting the detection result from [onHardwareEchoDetectionResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onhardwareechodetectionresult).

* You must stop the echo detection to release the audio devices before the user joins a room. Otherwise, the detection may interfere with the call.

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
|configurations |const LocalProxyConfiguration\* |Local proxy configurations. Refer to [LocalProxyConfiguration](https://docs.byteplus.com/en/docs/12/docs-70098#LocalProxyConfiguration).<br><br> <br><br>You can set both Http tunnel and Socks5 as your local proxies, or only set one of them based on your needs. If you set both Http tunnel and Socks5 as your local proxies, then media traffic and signaling are routed through Socks5 proxy and Http requests through Http tunnel proxy. If you set either Http tunnel or Socks5 as your local proxy, then media traffic, signaling and Http requests are all routed through the proxy you chose.<br><br> <br><br>If you want to remove the existing local proxy configurations, you can call this API with the parameter set to null. |
|configuration_num |int |The number of local proxy configurations. |

**Notes**

* You must call this API before joining the room.

* After calling this API, you will receive [onLocalProxyStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onlocalproxystatechanged) callback that informs you of the states of local proxy connection.

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
|mode |VideoEnhancementMode |It defaults to Disable. Refer to [VideoEnhancementMode](https://docs.byteplus.com/en/docs/12/docs-70098#VideoEnhancementMode) for more details. |

**Return Value**

* 0: Success. After you call this method, it will take action immediately. But it may require some time for downloads and detection processes before you can see the enhancement.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* Turning on this mode will impact device performance. This feature should be activated only when required and the device performance is adequate.

* Functionality applies to videos captured by the internal module as well as those from custom collections.

### getWTNStream

```cpp
virtual IWTNStream* getWTNStream() = 0;
```

> Available since 3.60

Gets the WTN stream object.

You can use this method to get the WTN stream object to implement custom video rendering and processing.

After calling this method, you can call [subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/14184#IWTNStream-subscribewtnvideostream) or [subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/14184#IWTNStream-subscribewtnaudiostream) to subscribe to the specified WTN stream.

To publish a WTN stream, call [startPushMixedStream](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-startpushmixedstream).

**Return Value**

IWTNStream：WTN stream object. See [IWTNStream](https://docs.byteplus.com/en/docs/12/14184#IWTNStream).

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
|render_mode |const enum RenderMode |See [RenderMode](https://docs.byteplus.com/en/docs/12/docs-70098#RenderMode). |
|background_color |const uint32_t |See [VideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70098#VideoCanvas).background_color. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

Calling this API during remote video rendering will be effective immediately.

### setLocalVideoSink

```cpp
virtual int setLocalVideoSink(
    IVideoSink* video_sink,
    IVideoSink::PixelFormat required_format
) = 0;
```

> Deprecated since 3.60, use [setLocalVideoSink](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setlocalvideosink) instead.

Binds the local video stream to a custom renderer.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|video_sink |IVideoSink\* |Custom video renderer. See [IVideoSink](https://docs.byteplus.com/en/docs/12/docs-70098#IVideoSink). |
|required_format |IVideoSink::PixelFormat |Video frame encoding format that applies to custom rendering. See [PixelFormat](https://docs.byteplus.com/en/docs/12/docs-70098#PixelFormat). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* RTC SDK uses its own renderer (internal renderer) for video rendering by default.

* Joining or leaving the room will not affect the binding state.

* If you need to unbind the video stream from the custom renderer, you must set video_sink to `null`.

* You should call this API before joining the room, and after receiving [onFirstLocalVideoFrameCaptured](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onfirstlocalvideoframecaptured) which reports that the first local video frame has been successfully captured.

* This method gets video frames that have undergone preprocessing.

### setRemoteVideoSink

```cpp
virtual int setRemoteVideoSink(
    const char* stream_id,
    IVideoSink* video_sink,
    IVideoSink::PixelFormat required_format
) = 0;
```

> Deprecated since 3.57, use [setRemoteVideoRender](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setremotevideosink) instead.

Binds the remote video stream to a custom renderer.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of stream |
|video_sink |IVideoSink\* |Custom video renderer. See [IVideoSink](https://docs.byteplus.com/en/docs/12/docs-70098#IVideoSink). |
|required_format |IVideoSink::PixelFormat |Encoding format which applies to the custom renderer. See [PixelFormat](https://docs.byteplus.com/en/docs/12/docs-70098#PixelFormat). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* RTC SDK uses its own renderer (internal renderer) for video rendering by default.

* Joining or leaving the room will not affect the binding state.

* This API can be called before and after entering the room. To call before entering the room, you need to get the remote stream information before joining the room; if you cannot get the remote stream information in advance, you can call the API after joining the room and getting the remote stream information via [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserpublishstreamvideo).

* If you need to unbind, you must set videoSink to null.

* This method gets video frames that have undergone processing.

# IRTSRoom

```cpp
class bytertc::IRTSRoom
```

RTS room interface

## Member Functions

|Return |Name |
|---|---|
|virtual void |[destroy](https://docs.byteplus.com/en/docs/12/14184#IRTSRoom-destroy) |
|virtual int |[leaveRoom](https://docs.byteplus.com/en/docs/12/14184#IRTSRoom-leaveroom) |
|virtual int |[setRTSRoomEventHandler](https://docs.byteplus.com/en/docs/12/14184#IRTSRoom-setrtsroomeventhandler) |
|virtual int64_t |[sendRoomMessage](https://docs.byteplus.com/en/docs/12/14184#IRTSRoom-sendroommessage) |
|virtual int64_t |[sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/14184#IRTSRoom-sendroombinarymessage) |
|virtual int |[joinRTSRoom](https://docs.byteplus.com/en/docs/12/14184#IRTSRoom-joinrtsroom) |
|virtual int |[updateToken](https://docs.byteplus.com/en/docs/12/14184#IRTSRoom-updatetoken) |
|virtual int64_t |[sendUserMessage](https://docs.byteplus.com/en/docs/12/14184#IRTSRoom-sendusermessage) |
|virtual int64_t |[sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/14184#IRTSRoom-senduserbinarymessage) |

## Instructions

### destroy

```cpp
virtual void destroy() = 0;
```

Leave and destroy the RTS room instance created by calling [createRTSRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-creatertsroom).

### leaveRoom

```cpp
virtual int leaveRoom() = 0;
```

Leave the RTC or RTS room.

The user calls this method to leave the room, end the call process, and release all call\-related resources.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* This method is an asynchronous operation and does not really exit the room when the call returns. After you actually exit the room, you will receive a callback notification from [onLeaveRoom](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onleaveroom) locally.

* After the visible user leaves the room, other users in the room will receive an [onUserLeave](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onuserleave) callback notification.

* If the engine is destroyed immediately after this method is called, the SDK will not be able to trigger the [onLeaveRoom](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onleaveroom) callback.

* After calling the [joinRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-joinroom) or [joinRTSRoom](https://docs.byteplus.com/en/docs/12/14184#IRTSRoom-joinrtsroom) method to join the room, you must call this method to leave the room, otherwise you cannot enter the next room. This method can be called regardless of whether it is currently in the room. Repeated calls to this method have no negative impact.

### setRTSRoomEventHandler

```cpp
virtual int setRTSRoomEventHandler(IRTSRoomEventHandler* room_event_handler) = 0;
```

Set the event handler of the [IRTSRoom](https://docs.byteplus.com/en/docs/12/14184#IRTSRoom) object.

You can listen for callback events for the room corresponding to this [IRTSRoom](https://docs.byteplus.com/en/docs/12/14184#IRTSRoom) object by setting the event handle.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|room_event_handler |IRTSRoomEventHandler\* |Callback processor. See [IRTSRoomEventHandler](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

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

The sequence number of the sent message, starting from 1.

**Notes**

* Before sending in\-room binary messages, you must call [joinRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-joinroom) to join the room.

* After calling this function, you get an [onRoomMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroommessagesendresult) callback.

* Other users in the same room receive an [onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroommessagereceived) callback.

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

The sequence number of the sent message, starting from 1.

**Notes**

* Before sending in\-room binary messages, you must call [joinRTSRoom](https://docs.byteplus.com/en/docs/12/14184#IRTSRoom-joinrtsroom) to join the room.

* After calling this function, you get an [onRoomMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroommessagesendresult) callback.

* Other users in the same room receive an [onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroombinarymessagereceived) callback.

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
|token |const char\* |Token is required during login for authentication.<br><br> <br><br>This Token is different from that required by calling joinRoom. You can assign any value even null to `roomId` to generate a login token. During developing and testing, you can use temporary tokens generated on the console. Deploy the token generating application on your server. |
|user_info |const UserInfo& |User information, see [UserInfo](https://docs.byteplus.com/en/docs/12/docs-70098#UserInfo). |

**Return Value**

* 0: Success

* \-1: token / user_info.uid contains invalid parameters.

* \-2: Already in the room.

**Notes**

* In the same room with the same App ID, the user ID of each user must be unique. If two users have the same user ID, the user who entered the room later will kick the user who entered the room out of the room, and the user who entered the room will receive the [OnError](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onerror) callback notification. For the error type. See kErrorCodeDuplicateLogin in [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-70097#ErrorCode).

* Local users will receive callback notification after calling this method to join the room successfully.

* After the user successfully joins the room, the SDK may lose connection to the server in case of poor local network conditions, and the SDK will automatically reconnect at this time. After a successful reconnection, you will receive a local callback notification. If the user is set to visiable, the remote user will receive [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onuserjoined) callback notification.

### updateToken

```cpp
virtual int updateToken(const char* token) = 0;
```

Update Token.

You must call this API to update token to ensure the RTC call continues when you receive [onTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-ontokenwillexpire), [onPublishPrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onpublishprivilegetokenwillexpire), or [onSubscribePrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onsubscribeprivilegetokenwillexpire).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|token |const char\* |Valid token.<br><br> <br><br>If the Token is invalid, you will receive [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) with the error code of `-1010`. |

**Return Value**

API call result:

* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for specific reasons.

**Notes**

* In versions before 3.50, the publish and subscribe privileges contained in the Token are reserved parameters with no actual control permissions. In version 3.50 and later, the publish/subscribe privileges will be effective for whitelisted users. Please contact the technical support team to include you in the whitelist if you need this function.

* Do not call both [updateToken](https://docs.byteplus.com/en/docs/12/14184#IRTSRoom-updatetoken) and [joinRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-joinroom) to update the Token. If you fail to join the room or have been removed from the room due to an expired or invalid Token, call [joinRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-joinroom) with a valid token to rejoin the room.

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
|config |MessageConfig |Message type, see [MessageConfig](https://docs.byteplus.com/en/docs/12/docs-70098#MessageConfig). |

**Return Value**

The sequence number of the sent message, starting from 1.

**Notes**

* Before sending an in\-room text message, you must call [joinRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-joinroom) or [joinRTSRoom](https://docs.byteplus.com/en/docs/12/14184#IRTSRoom-joinrtsroom) to join the room.

* After calling this function, you will receive an [onUserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onusermessagesendresult) callback to notify the message sender that the sending was successful or failed;

* If the text message is sent successfully, the user specified by uid will receive [onUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onusermessagereceived) callback.

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
|config |MessageConfig |Message type, see [MessageConfig](https://docs.byteplus.com/en/docs/12/docs-70098#MessageConfig). |

**Return Value**

Serial number of the message, starting form 1.

**Notes**

* Before sending in\-room binary messages, you must call [joinRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-joinroom) or [joinRTSRoom](https://docs.byteplus.com/en/docs/12/14184#IRTSRoom-joinrtsroom) to join the room.

* After calling this function, you will receive an [onUserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onusermessagesendresult) callback to notify the sender of the success or failure of the message;

* If the binary message is sent successfully, the user specified by uid will receive the [onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onuserbinarymessagereceived) callback.

# IAudioDeviceCollection

```cpp
class bytertc::IAudioDeviceCollection
```

Audio equipment related information

## Member Functions

|Return |Name |
|---|---|
|virtual int |[getCount](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceCollection-getcount) |
|virtual int |[getDevice](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceCollection-getdevice) |
|virtual void |[release](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceCollection-release) |
|virtual int |[getDevice](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceCollection-getdevice-2) |

## Instructions

### getCount

```cpp
virtual int getCount() override {return 0;};
```

Get the number of audio and video devices in the current system

**Return Value**

Number of audio devices

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
|index |int |Device index number, starting from 0, note that it must be less than the return value of [getCount](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceCollection-getcount). |
|device_name |char[MAX_DEVICE_ID_LENGTH] |Device name |
|device_id |char[MAX_DEVICE_ID_LENGTH] |Device ID |

**Return Value**

* 0: Success.

   +! 0: failure

### release

```cpp
virtual void release()override {};
```

Releases the resources occupied by the current [IAudioDeviceCollection](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceCollection) object.

**Notes**

This method should be called to release related resources when you do not need to return a list of audio device related information.

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
|index |int |Device index number, starting from 0, note that it must be less than the return value of [getCount](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceCollection-getcount). |
|audio_device_info |AudioDeviceInfo\* |device info. Refer to [AudioDeviceInfo](https://docs.byteplus.com/en/docs/12/docs-70098#AudioDeviceInfo) for details. |

**Return Value**

* 0: Success.

   +! 0: failure

# IScreenCaptureSourceList

```cpp
class bytertc::IScreenCaptureSourceList
```

Information list of the screen\-sharing objects

Calling [release](https://docs.byteplus.com/en/docs/12/14184#IScreenCaptureSourceList-release) will release all the objects related to this class.

## Member Functions

|Return |Name |
|---|---|
|virtual int32_t |[getCount](https://docs.byteplus.com/en/docs/12/14184#IScreenCaptureSourceList-getcount) |
|virtual ScreenCaptureSourceInfo |[getSourceInfo](https://docs.byteplus.com/en/docs/12/14184#IScreenCaptureSourceList-getsourceinfo) |
|virtual void |[release](https://docs.byteplus.com/en/docs/12/14184#IScreenCaptureSourceList-release) |

## Instructions

### getCount

```cpp
virtual int32_t getCount() = 0;
```

Get the length of the list

**Return Value**

Number of the items in the list

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

Screen source item. Refer to [ScreenCaptureSourceInfo](https://docs.byteplus.com/en/docs/12/docs-70098#ScreenCaptureSourceInfo) for more details.

### release

```cpp
virtual void release() = 0;
```

If you are finished with the [IScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/14184#IScreenCaptureSourceList), call this API to destruct it and release the memory.

# ISpatialAudio

```cpp
class bytertc::ISpatialAudio
```

Spatial audio instance

## Member Functions

|Return |Name |
|---|---|
|virtual void |[enableSpatialAudio](https://docs.byteplus.com/en/docs/12/14184#ISpatialAudio-enablespatialaudio) |
|virtual void |[disableRemoteOrientation](https://docs.byteplus.com/en/docs/12/14184#ISpatialAudio-disableremoteorientation) |
|virtual int |[updateSelfPosition](https://docs.byteplus.com/en/docs/12/14184#ISpatialAudio-updateselfposition) |
|virtual int |[updateRemotePosition](https://docs.byteplus.com/en/docs/12/14184#ISpatialAudio-updateremoteposition) |
|virtual int |[removeRemotePosition](https://docs.byteplus.com/en/docs/12/14184#ISpatialAudio-removeremoteposition) |
|virtual int |[removeAllRemotePosition](https://docs.byteplus.com/en/docs/12/14184#ISpatialAudio-removeallremoteposition) |

## Instructions

### enableSpatialAudio

```cpp
virtual void enableSpatialAudio(bool enable) = 0;
```

Enable/disable spatial audio function.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |bool |Whether to enable spatial audio function:<br><br><br> <br><br>* true：Enable<br><br>* false：Disable (Default setting) |

**Notes**

You need to call [updateSelfPosition](https://docs.byteplus.com/en/docs/12/14184#ISpatialAudio-updateselfposition) as well to really enjoy the spatial audio effect.

### disableRemoteOrientation

```cpp
virtual void disableRemoteOrientation() = 0;
```

Turn off the effect of the orientation of the local user as the sound source.

After the effect is off, all the other users in the room listen to the local user as if the local user is right in front of each of them.

**Notes**

* After the orientation effect as the sound source is disabled, you cannot enable it during the lifetime of the `SpatialAudio` instance.

* Calling this API does not affect the orientation effect of the local user as a listener. See [updateSelfPosition](https://docs.byteplus.com/en/docs/12/14184#ISpatialAudio-updateselfposition) and [updateRemotePosition](https://docs.byteplus.com/en/docs/12/14184#ISpatialAudio-updateremoteposition)

### updateSelfPosition

```cpp
virtual int updateSelfPosition(const PositionInfo& position_info) = 0;
```

> Available since 3.52

Sets the coordinate and orientation of the local user as a listener in the rectangular coordinate system the local user built to achieve expected spatial audio effects.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|position_info |const PositionInfo& |Information on the local user's position. Refer to [PositionInfo](https://docs.byteplus.com/en/docs/12/docs-70098#PositionInfo) for details. |

**Return Value**

* 0: Success.

* <0: Failure.

* \-2: Failure. The reason is that any two of the 3D coordinate vectors of your position are not perpendicular to each other.

**Notes**

* You need to call this API after joining the room.

* Before calling this API, you should call [enableSpatialAudio](https://docs.byteplus.com/en/docs/12/14184#ISpatialAudio-enablespatialaudio) first to enable the spatial audio function.

* The settings made locally will not influence other users' spatial audio experience.

### updateRemotePosition

```cpp
virtual int updateRemotePosition(
    const char* uid,
    const PositionInfo& position_info
) = 0;
```

> Available since 3.52

Sets the coordinate and orientation of the remote user as a speaker in the rectangular coordinate system of the local user. In this case, the local user hears from the remote user with the expected spatial audio effects.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|uid |const char\* |User ID |
|position_info |const PositionInfo& |Information on the remote user's position. Refer to [PositionInfo](https://docs.byteplus.com/en/docs/12/docs-70098#PositionInfo) for details. |

**Return Value**

* 0: Success.

* <0: Failure.

* \-2: Failure. The reason is that any two of the 3D coordinate vectors of the position of the remote user are not perpendicular to each other.

**Notes**

* You must call this API after creating the room.

* The settings made locally will not influence other users' spatial audio experience.

### removeRemotePosition

```cpp
virtual int removeRemotePosition(const char* uid) = 0;
```

> Available since 3.52

Disables all spatial audio effects set by calling [updateRemotePosition](https://docs.byteplus.com/en/docs/12/14184#ISpatialAudio-updateremoteposition) for a certain remote user.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|uid |const char\* |User ID of the remote user. |

**Return Value**

* 0: Success.

* <0: Failure.

### removeAllRemotePosition

```cpp
virtual int removeAllRemotePosition() = 0;
```

> Available since 3.52

Disables all spatial audio effects set by calling [updateRemotePosition](https://docs.byteplus.com/en/docs/12/14184#ISpatialAudio-updateremoteposition) for all remote users.

**Return Value**

* 0: Success.

* <0: Failure.

# IVideoDeviceCollection

```cpp
class bytertc::IVideoDeviceCollection
```

Video equipment related information

## Member Functions

|Return |Name |
|---|---|
|virtual int |[getCount](https://docs.byteplus.com/en/docs/12/14184#IVideoDeviceCollection-getcount) |
|virtual int |[getDevice](https://docs.byteplus.com/en/docs/12/14184#IVideoDeviceCollection-getdevice) |
|virtual void |[release](https://docs.byteplus.com/en/docs/12/14184#IVideoDeviceCollection-release) |
|virtual int |[getDevice](https://docs.byteplus.com/en/docs/12/14184#IVideoDeviceCollection-getdevice-2) |

## Instructions

### getCount

```cpp
virtual int getCount() override {return 0;};
```

Get the number of video devices in the current system

**Return Value**

Number of video devices

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
|index |int |Device index number, starting from 0, note that it must be less than the return value of [getCount](https://docs.byteplus.com/en/docs/12/14184#IVideoDeviceCollection-getcount). |
|device_name |char[MAX_DEVICE_ID_LENGTH] |device name |
|device_id |char[MAX_DEVICE_ID_LENGTH] |device ID |

**Return Value**

* 0: Success.

   +! 0: failure

### release

```cpp
virtual void release()override {};
```

Releases the resources occupied by the current [IVideoDeviceCollection](https://docs.byteplus.com/en/docs/12/14184#IVideoDeviceCollection) object.

**Notes**

This method should be called to release related resources when you do not need to return a list of video device related information.

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
|index |int |Device index, starting from 0. It must be less than the return value of [getCount](https://docs.byteplus.com/en/docs/12/14184#IVideoDeviceCollection-getcount). |
|video_device_info |VideoDeviceInfo\* |Device information |

**Return Value**

* 0: Success.

   +! 0: failure

# IWTNStream

```cpp
class bytertc::IWTNStream
```

WTN stream process

## Member Functions

|Return |Name |
|---|---|
|virtual |[~IWTNStream](https://docs.byteplus.com/en/docs/12/14184#IWTNStream-~iwtnstream) |
|virtual int |[subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/14184#IWTNStream-subscribewtnvideostream) |
|virtual int |[subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/14184#IWTNStream-subscribewtnaudiostream) |
|virtual int |[setWTNRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/14184#IWTNStream-setwtnremotevideocanvas) |
|virtual int |[setWTNRemoteVideoSink](https://docs.byteplus.com/en/docs/12/14184#IWTNStream-setwtnremotevideosink) |
|virtual int |[setWTNRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/14184#IWTNStream-setwtnremoteaudioplaybackvolume) |
|virtual int |[setWTNStreamEventHandler](https://docs.byteplus.com/en/docs/12/14184#IWTNStream-setwtnstreameventhandler) |

## Instructions

### ~IWTNStream

```cpp
virtual ~IWTNStream() = default;
```

### subscribeWTNVideoStream

```cpp
virtual int subscribeWTNVideoStream(
    const char* stream_id,
    bool subscribe
) = 0;
```

> Available since 3.60. Since version 3.60, this interface replaces the `startPlayPublicStream` and `stopPlayPublicStream` methods for subscribing to and unsubscribing from WTN video streams. If you are using these methods, please migrate to this interface.

Subscribe/ unsubscribe WTN video stream

A user can call this method to subscribe or unsubscribe to a WTN stream whether he/she has joined the room or not.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of the WTN stream. If the stream has not been published then, the local client will receive the WTN stream once it starts publishing. |
|subscribe |bool |Whether to subscribe to the WTN stream.<br><br><br> <br><br>* true: Subscribe<br><br>* false: Unsubscribe |

**Return Value**

* 0: Success. You will also be informed by [onWTNVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IWTNStreamEventHandler-onwtnvideosubscribestatechanged).

* !0: Failure because of invalid parameter or empty parameters.

**Notes**

* A client can play up to 5 WTN streams simultaneously. Please call [subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/14184#IWTNStream-subscribewtnvideostream)/[subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/14184#IWTNStream-subscribewtnaudiostream) in time to cancel the subscription to WTN streams to avoid exceeding the limit of subscribed WTN streams.

* We recommend to bind a view for the WTN stream before calling this API to subscribe to a WTN stream.

   \- Internal renderer: By calling [setWTNRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/14184#IWTNStream-setwtnremotevideocanvas) or

   \- Custom renderer: By calling [setWTNRemoteVideoSink](https://docs.byteplus.com/en/docs/12/14184#IWTNStream-setwtnremotevideosink)

* After calling this API, you will be informed once the first frame has been decoded successfully by [onWTNFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-70096#IWTNStreamEventHandler-onwtnfirstremotevideoframedecoded).

* If the WTN stream contains SEI information, you will be informed by [oonWTNSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IWTNStreamEventHandler-onwtnseimessagereceived).

### subscribeWTNAudioStream

```cpp
virtual int subscribeWTNAudioStream(
    const char* stream_id,
    bool subscribe
) = 0;
```

> Available since 3.60. Since version 3.60, this interface replaces the `startPlayPublicStream` and `stopPlayPublicStream` methods for subscribing to and unsubscribing from WTN audio streams. If you are using these methods, please migrate to this interface.

Subscribe/unsubscribe the WTN audio stream

A user can call this method to subscribe to a WTN stream whether he/she has joined the room or not.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of the WTN stream. If the stream has not been published then, the local client will receive the WTN stream once it starts publishing. |
|subscribe |bool |Whether to subscribe to the WTN stream.<br><br><br> <br><br>* true: Subscribe<br><br>* false: Unsubscribe |

**Return Value**

* 0: Success. You will also be informed by [onWTNAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IWTNStreamEventHandler-onwtnaudiosubscribestatechanged).

* !0: Failure because of invalid parameter or empty parameters.

**Notes**

* A client can play up to 5 WTN streams simultaneously. Please call [subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/14184#IWTNStream-subscribewtnvideostream)/[subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/14184#IWTNStream-subscribewtnaudiostream) in time to cancel the subscription to WTN streams to avoid exceeding the limit of subscribed WTN streams.

* We recommend to bind a view for the WTN stream before calling this API to subscribe to a WTN stream.

   \- Internal renderer: By calling [setWTNRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/14184#IWTNStream-setwtnremotevideocanvas) or

   \- Custom renderer: By calling [setWTNRemoteVideoSink](https://docs.byteplus.com/en/docs/12/14184#IWTNStream-setwtnremotevideosink)

* After calling this API, you will be informed once the first frame has been decoded successfully by [onWTNFirstRemoteAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IWTNStreamEventHandler-onwtnfirstremoteaudioframe).

* If the WTN stream contains SEI information, you will be informed by [onWTNSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IWTNStreamEventHandler-onwtnseimessagereceived).

### setWTNRemoteVideoCanvas

```cpp
virtual int setWTNRemoteVideoCanvas(
    const char* stream_id,
    const VideoCanvas& canvas
) = 0;
```

> Available since 3.60. Since version 3.60, this interface replaces `setPublicStreamVideoCanvas` for the following function. If you have upgraded to version 3.60 or above and are still using this method, please migrate to this interface.

Assign an internal render view to the WTN stream

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|stream_id |const char\* |ID of the WTN stream |
|canvas |const VideoCanvas& |Internal render view. If you want to unbind the video, set `videoCanvas` to null. Refer to [VideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70098#VideoCanvas) for more details. |

**Return Value**

* 0: Success

* !0: Failure

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
|video_sink |IVideoSink\* |Custom renderer. Set to be `null` when you want to release the renderer. Refer to [IVideoSink](https://docs.byteplus.com/en/docs/12/docs-70098#IVideoSink) for more details. |
|config |RemoteVideoSinkConfig& |Remote video frame callback configuration. Refer to [RemoteVideoSinkConfig](https://docs.byteplus.com/en/docs/12/docs-70098#RemoteVideoSinkConfig) for more details. |

**Return Value**

* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for specific reasons.

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
|volume |int |Ratio(%) of the audio playback volume to the original volume, in the range `[0, 400]`, with overflow protection. The default volume is 100.<br><br> <br><br>To ensure the audio quality, the recommended range is `[0, 100]`. |

**Return Value**

* 0: Success.

* \-2: Wrong parameter.

### setWTNStreamEventHandler

```cpp
virtual int setWTNStreamEventHandler(IWTNStreamEventHandler* handler) = 0;
```

> Available since 3.60.

Set the WTN event handler.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|handler |IWTNStreamEventHandler\* |See [IWTNStreamEventHandler](https://docs.byteplus.com/en/docs/12/docs-70096#IWTNStreamEventHandler). |

# IRTCRoom

```cpp
class bytertc::IRTCRoom
```

Room interface

## Member Functions

|Return |Name |
|---|---|
|virtual void |[destroy](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-destroy) |
|virtual int |[setUserVisibility](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-setuservisibility) |
|virtual int |[setRTCRoomEventHandler](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-setrtcroomeventhandler) |
|virtual int |[joinRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-joinroom) |
|virtual int |[publishStreamVideo](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-publishstreamvideo) |
|virtual int |[publishStreamAudio](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-publishstreamaudio) |
|virtual int |[subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-subscribestreamvideo) |
|virtual int |[subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-subscribestreamaudio) |
|virtual int |[setRemoteSimulcastStreamType](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-setremotesimulcaststreamtype) |
|virtual int |[setRemoteVideoConfig](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-setremotevideoconfig) |
|virtual int |[setStreamExtraInfo](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-setstreamextrainfo) |
|virtual int |[subscribeAllStreamsVideo](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-subscribeallstreamsvideo) |
|virtual int |[subscribeAllStreamsAudio](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-subscribeallstreamsaudio) |
|virtual int |[pauseAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-pauseallsubscribedstreamvideo) |
|virtual int |[pauseAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-pauseallsubscribedstreamaudio) |
|virtual int |[resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-resumeallsubscribedstreamvideo) |
|virtual int |[resumeAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-resumeallsubscribedstreamaudio) |
|virtual int |[setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-setmultideviceavsync) |
|virtual int |[startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-startforwardstreamtorooms) |
|virtual int |[updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-updateforwardstreamtorooms) |
|virtual int |[stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-stopforwardstreamtorooms) |
|virtual int |[pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-pauseforwardstreamtoallrooms) |
|virtual int |[resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-resumeforwardstreamtoallrooms) |
|virtual IRangeAudio\* |[getRangeAudio](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-getrangeaudio) |
|virtual ISpatialAudio\* |[getSpatialAudio](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-getspatialaudio) |
|virtual int |[setRemoteRoomAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-setremoteroomaudioplaybackvolume) |
|virtual int |[setAudioSelectionConfig](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-setaudioselectionconfig) |
|virtual int64_t |[setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-setroomextrainfo) |
|virtual const char\* |[getRoomId](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-getroomid) |
|virtual const char\* |[getCallId](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-getcallid) |
|virtual int |[setLiveMode](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-setlivemode) |

## Instructions

### destroy

```cpp
virtual void destroy() = 0;
```

Leave and destroy the RTC room instance created by calling [createRTCRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-creatertcroom).

### setUserVisibility

```cpp
virtual int setUserVisibility(bool enable) = 0;
```

Set the visibility of the user in the room. The local user is visible to others by default before calling this API.

An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Room Capacity](https://docs.byteplus.com/en/byteplus-rtc/docs/257549).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |bool |Visibility of the user in the room.<br><br><br> <br><br>* true: The user can publish media streams. The other users in the room get informed of the behaviors of the user, such as joining room, starting video capture, and leaving room.<br><br>* false: The user cannot publish media streams. The other users in the room do not get informed of the behaviors of the user, such as joining room, starting video capture, or leaving room. |

**Return Value**

* 0: Success.

* < 0 : Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus).

   You will receive [onUserVisibilityChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuservisibilitychanged) after calling this API. (Available since v3.54)

* If you call this API before joining room, and the set value is different from the default value, you will receive the callback when you join the room.

* If you call this API after joining room, and the current visibility is different from the previous value, you will receive the callback.

* When reconnecting after losing internet connection, if the visibility changes, you will receive the callback.

**Notes**

* You can call this API whether the user is in a room or not.

   * When you call this API while you are in the room, the other users in the room will be informed via the following callback.

      • When you switch from `false` to `true`, they will receive [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onuserjoined).

• When you switch from `true` to `false`, they will receive [onUserLeave](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onuserleave).

• The invisible user will receive the warning code, `kWarningCodePublishStreamForbidden`, when trying to publish media streams.

### setRTCRoomEventHandler

```cpp
virtual int setRTCRoomEventHandler(IRTCRoomEventHandler* room_event_handler) = 0;
```

Listens for event callbacks related to the [IRTCRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom) instance by setting the event handler of this instance.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|room_event_handler |IRTCRoomEventHandler\* |Refer to [IRTCRoomEventHandler](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

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

After creating a room by calling [createRTCRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-creatertcroom), call this API to join the room and make audio & video calls with other users in the room.

> Users (including backend bots) who successfully join the RTC room will start billing. If the room only has 1 user, the audio billing time will be calculated. See [Audio Billing](https://docs.byteplus.com/en/docs/12/docs-69871) for more details.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|token |const char\* |Dynamic key for authenticating the signed\-in user.<br><br> <br><br>You need to bring Token to enter the room. When testing, you can use the console to generate temporary tokens. For production use, use the server\-side SDK to generate and issue tokens on your server. See [Authentication with Token](https://docs.byteplus.com/en/docs/12/docs-70121) for token validity and generation method.<br><br><br> <br><br>* Apps with different App IDs cannot communicate with each other.<br><br>* Make sure that the App ID used to generate the Token is the same as the App ID used to create the engine, otherwise it will cause joining the room to fail. |
|user_info |const UserInfo& |User information. See [UserInfo](https://docs.byteplus.com/en/docs/12/docs-70098#UserInfo). |
|user_visibility |bool |User visibility. We recommend setting the user visibility to `false` when entering the room, and then setting it to `true` via [setUserVisibility](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-setuservisibility) when the user needs to send audio & video streams. Joining fails when the number of users in an RTC room reaches the upper limit. An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Capability of Users and Streams](https://docs.byteplus.com/en/byteplus-rtc/docs/257549). |
|config |const RTCRoomConfig& |Room parameter configuration, set the room mode and whether to automatically publish or subscribe to the flow. See [RTCRoomConfig](https://docs.byteplus.com/en/docs/12/docs-70098#RTCRoomConfig) for the specific configuration mode. |

**Return Value**

* 0: Success.

   * Local users receive notifications of the room state via [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged).

   * Local users receive notifications of the local\-stream state via [onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onvideopublishstatechanged), [onAudioPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onaudiopublishstatechanged).

   * Local users receive notifications of the subscribed\-stream state via [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserpublishstreamaudio).

   * Local users receive notifications of the published\-stream state via [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserpublishstreamaudio).

   * If the local user is also a visible user, the other participants receive [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserjoined) callback.

* \-1: Room_id/user_info.uid contains invalid parameters.

* \-2: Already in the room. After the API call is successful, as long as the return value of 0 is received and [leaveRoom](https://docs.byteplus.com/en/docs/12/14184#IRTSRoom-leaveroom) is not called successfully, this return value is triggered when the room entry API is called again, regardless of whether the filled room ID and user ID are duplicated.

   The reason for the failure will be communicated via the [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) callback.

**Notes**

* In the same room with the same App ID, the user ID of each user must be unique. If two users have the same user ID, the user who entered the room later will kick the user who entered the room out of the room, and the user who entered the room will receive the [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) callback notification. For the error type. See kErrorCodeDuplicateLogin in [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-70097#ErrorCode).

* After the user successfully joins the room, the SDK may lose connection to the server in case of poor local network conditions. At this point, [onConnectionStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onconnectionstatechanged) callback will be triggered and the SDK will automatically retry until it successfully reconnects to the server. After a successful reconnection, you will receive a local [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) callback notification.

### publishStreamVideo

```cpp
virtual int publishStreamVideo(bool publish) = 0;
```

> Available since 3.60. Since version 3.60, this interface replaces the `publishStream`, `unpublishStream`, `publishScreen` and `unpublishScreen` methods for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.

Publishes or stops publishing video streams.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|publish |bool |Whether to publish the video stream.<br><br><br> <br><br>* `true`: Publish.<br><br>* `false`: Stop publishing. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* You don't need to call this API if you set it to Auto\-publish when calling [joinRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-joinroom).

* An invisible user cannot publish media streams. Call [setUserVisibility](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-setuservisibility) to change your visibility in the room.

* Call [publishStreamAudio](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-publishstreamaudio) to start or stop publishing the audio stream captured by the microphone.

* Call [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-startforwardstreamtorooms) to forward the published streams to the other rooms.

* After you call this API, the other users in the room will receive [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserpublishstreamvideo). Those who successfully received your streams will receive [onFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onfirstremotevideoframedecoded) at the same time.

### publishStreamAudio

```cpp
virtual int publishStreamAudio(bool publish) = 0;
```

> Available since 3.60. Since version 3.60, this interface replaces the `publishStream`, `unpublishStream`, `publishScreen` and `unpublishScreen` methods for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.

Publishes or stops publishing audio streams in the current room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|publish |bool |Whether to publish the audio stream.<br><br><br> <br><br>* `true`: Publish.<br><br>* `false`: Stop publishing. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* You don't need to call this API if you set it to Auto\-publish when calling [joinRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-joinroom).

* An invisible user cannot publish media streams. Call [setUserVisibility](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-setuservisibility) to change your visibility in the room.

* Call [publishStreamVideo](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-publishstreamvideo) to start or stop publishing the video stream captured by the camera.

* Call [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-startforwardstreamtorooms) to forward the published streams to the other rooms.

* After you call this API, the other users in the room will receive [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserpublishstreamaudio). Those who successfully received your streams will receive [onFirstRemoteAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onfirstremoteaudioframe) at the same time.

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
|subscribe |bool |Whether to subscribe to the video stream.<br><br><br> <br><br>* `true`: Subscribe.<br><br>* `false`: Unsubscribe. |

**Return Value**

API call result:

* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for specific reasons.

**Notes**

* Calling this API to update the subscribe configuration when the user has subscribedd the remote user either by calling this API or by auto\-subscribe.

* You must first get the remote stream information through [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserpublishstreamvideo) before calling this API to subscribe to streams accordingly.

* After calling this API, you will be informed of the calling result with [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onvideosubscribestatechanged).

* Once the local user subscribes to the stream of a remote user, the subscription to the remote user will sustain until the local user leaves the room or unsubscribe from it by calling [subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-subscribestreamvideo).

* Any other exceptions will be included in [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onvideosubscribestatechanged), see [SubscribeStateChangeReason](https://docs.byteplus.com/en/docs/12/docs-70098#SubscribeStateChangeReason) for the reasons.

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
|subscribe |bool |Whether to subscribe to the audio stream.<br><br><br> <br><br>* `true`: Subscribe.<br><br>* `false`: Unsubscribe. |

**Return Value**

API call result:

* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for specific reasons.

**Notes**

* Calling this API to update the subscribe configuration when the user has subscribedd the remote user either by calling this API or by auto\-subscribe.

* You must first get the remote stream information through [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserpublishstreamaudio) before calling this API to subscribe to streams accordingly.

* After calling this API, you will be informed of the calling result with [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onaudiosubscribestatechanged).

* Once the local user subscribes to the stream of a remote user, the subscription to the remote user will sustain until the local user leaves the room or unsubscribe from it by calling [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-subscribestreamaudio).

* Any other exceptions will be included in [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onaudiosubscribestatechanged), see [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-70097#ErrorCode) for the reasons.

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
|stream_type |SimulcastStreamType |Video stream type, see [SimulcastStreamType](https://docs.byteplus.com/en/docs/12/docs-70098#SimulcastStreamType). |

**Return Value**

API call result:

* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for specific reasons.

**Notes**

* This API only works after the publisher calls [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setlocalsimulcastmode) to enable publishing multiple\-quality video streams, in which case the subscriber will receive the stream from the publisher that is closest to the set configuration; otherwise the subscriber will only receive one video stream with a resolution of 640px × 360px and a frame rate of 15fps.

* If you don't call this API after the publisher enables the function of publishing multiple streams, you will receive by default the video stream with the largest resolution set by the publisher.

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
|remote_video_config |const RemoteVideoConfig& |Parameters you want to configure for the remote video stream, see [RemoteVideoConfig](https://docs.byteplus.com/en/docs/12/docs-70098#RemoteVideoConfig). |

**Return Value**

API call result:

* 0: Success.

* !0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for specific reasons.

**Notes**

* This API only works after the publisher calls [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setlocalsimulcastmode) to enable publishing multiple video streams, in which case the subscriber will receive the stream from the publisher that is closest to the set configuration; otherwise the subscriber will only receive one video stream with a resolution of 640px × 360px and a frame rate of 15fps..

* If you don't call this API after the publisher enables the function of publishing multiple streams, you will receive by default the video stream with the largest resolution set by the publisher.

* You should call this API in the room.

* The SDK will automatically select the stream to be published or subscribed to based on the settings of both sides. See for details.

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

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for specific reasons.

**Notes**

* This function can be used to set the stream extra information for the current streaming. The stream additional information serves as an additional information identifier for the stream ID. Unlike the stream ID, which cannot be modified during the streaming process, the stream additional information can be updated midway through the streaming of the corresponding stream ID. Developers can leverage the stream additional information to achieve synchronization of variable content related to the stream ID.

* This method can be called either before or after entering the room.

* Other users in the same room will receive notifications via the [onRoomStreamExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onroomstreamextrainfoupdate) callback function.

### subscribeAllStreamsVideo

```cpp
virtual int subscribeAllStreamsVideo(bool subscribe) = 0;
```

> Available since 3.60. Since version 3.60, this interface replaces the `subscribeAllStreams` and `unsubscribeAllStreams` methods for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.

Subscribes to or unsubscribes from all remote video streams (by the camera).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|subscribe |bool |Whether to subscribe to all remote video streams.<br><br><br> <br><br>* `true`: Subscribe.<br><br>* `false`: Unsubscribe. |

**Return Value**

API call result:

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* If the subscription options conflict with the previous ones, they are subject to the configurations in the last call.

* With the Audio selection enabled, if the number of media streams exceeds the limit, we recommend that you subscribe to each target media stream with the following APIs: [subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-subscribestreamvideo), [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-subscribestreamaudio).

* After calling this API, you will be informed of the calling result with [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onvideosubscribestatechanged), [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onaudiosubscribestatechanged). You can also find exceptions cause from the callbacks above.

* Once the local user subscribes to the stream of a remote user, the subscription to the remote user will sustain until the local user leaves the room or unsubscribe from it by calling [subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-subscribestreamvideo), [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-subscribestreamaudio).

### subscribeAllStreamsAudio

```cpp
virtual int subscribeAllStreamsAudio(bool subscribe) = 0;
```

> Available since 3.60. Since version 3.60, this interface replaces the `subscribeAllStreams` and `unsubscribeAllStreams` methods for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.

Subscribes to or unsubscribes from all remote audio streams (by the microphone).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|subscribe |bool |Whether to subscribe to all remote audio streams.<br><br><br> <br><br>* `true`: Subscribe.<br><br>* `false`: Unsubscribe. |

**Return Value**

API call result:

* 0: Success

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* If the subscription options conflict with the previous ones, they are subject to the configurations in the last call.

* With the Audio selection enabled, if the number of media streams exceeds the limit, we recommend that you subscribe to each target media stream with the following APIs: [subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-subscribestreamvideo), [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-subscribestreamaudio).

* After calling this API, you will be informed of the calling result with [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onvideosubscribestatechanged), [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onaudiosubscribestatechanged). You can also find exceptions cause from the callbacks above.

* Once the local user subscribes to the stream of a remote user, the subscription to the remote user will sustain until the local user leaves the room or unsubscribe from it by calling [subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-subscribestreamvideo), [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-subscribestreamaudio).

### pauseAllSubscribedStreamVideo

```cpp
virtual int pauseAllSubscribedStreamVideo() = 0;
```

> Available since 3.60. Since version 3.60, this interface replaces the `pauseAllSubscribedStreamAudio` for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.

Pauses receiving all the video streams of all remote users.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* Calling this API does not change the capture state and the transmission state of the remote clients.

* Calling this API does not cancel the subscription or change any subscription configuration.

* To resume, call [resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-resumeallsubscribedstreamvideo).

* In a multi\-room scenario, this API only pauses the reception of streams published in the current room.

### pauseAllSubscribedStreamAudio

```cpp
virtual int pauseAllSubscribedStreamAudio() = 0;
```

> Available since 3.60. Since version 3.60, this interface replaces the `pauseAllSubscribedStream` for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.

Pauses receiving the audio streams of all remote users.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* Calling this API does not change the capture state and the transmission state of the remote clients.

* Calling this API does not cancel the subscription or change any subscription configuration.

* To resume, call [resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-resumeallsubscribedstreamvideo).

* In a multi\-room scenario, this API only pauses the reception of streams published in the current room.

### resumeAllSubscribedStreamVideo

```cpp
virtual int resumeAllSubscribedStreamVideo() = 0;
```

> Available since 3.60. Since version 3.60, this interface replaces the `resumeAllSubscribedStream` method to implement the below functions. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this interface.

Resumes receiving all the video streams of all remote users.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* Calling this API does not change the capture state and the transmission state of the remote clients.

* Calling this API does not change any subscription configuration.

### resumeAllSubscribedStreamAudio

```cpp
virtual int resumeAllSubscribedStreamAudio() = 0;
```

> Available since 3.60. Since version 3.60, this interface replaces the `resumeAllSubscribedStream` method to implement the below functions. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this interface.

Resumes receiving all the audio streams of all remote users.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

* Calling this API does not change the capture state and the transmission state of the remote clients.

* Calling this API does not change any subscription configuration.

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

* 0: Success. When the A/V synchronization state changes, you will receive [onAVSyncStateChange](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onavsyncstatechange).

* < 0 : Fail. You can also learn the error details via [onAVSyncEvent](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onavsyncevent). More than one pair of audio and video can be synchronized simultaneously in the same RTC room, but you should note that one single audio source cannot be synchronized with multiple video sources at the same time.

**Notes**

* You can call this API anytime before or after entering the room.

* The source user IDs of the audio and video stream to be synchronized must be in the same RTC room.

* If you want to change the audio source, call this API again with a new `audio_user_id`. If you want to change the video source, you need to stop the current synchronization first, then call this API on the new video publisher side.

### startForwardStreamToRooms

```cpp
virtual int startForwardStreamToRooms(const ForwardStreamConfiguration& configuration) = 0;
```

Start relaying media stream across rooms.

After calling [joinRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-joinroom), you can call this method to publish the media stream to multiple rooms that applies to scenarios such as an online talent contest and so on.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|configuration |const ForwardStreamConfiguration& |Information of the rooms where you want to relay the media stream to. Refer to [ForwardStreamConfiguration](https://docs.byteplus.com/en/docs/12/docs-70098#ForwardStreamConfiguration) for more information. |

**Return Value**

* 0: Success

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* Call this method will trigger [onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onforwardstreamstatechanged).

* After calling this method, listen the events from each room during the relaying by registering [onForwardStreamEvent](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onforwardstreamevent).

* Once the relaying begins, the other users in the room will receive callback of [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserjoined), [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserpublishstreamaudio).

* Call [updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-updateforwardstreamtorooms) to add or remove the target room(s) after calling this method.

* Call [stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-stopforwardstreamtorooms) to stop relaying to all rooms after calling this method.

* Call [pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-pauseforwardstreamtoallrooms) to pause relaying to all rooms after calling this method.

### updateForwardStreamToRooms

```cpp
virtual int updateForwardStreamToRooms(const ForwardStreamConfiguration& configuration) = 0;
```

Update information of the rooms where you want to relay the media stream to after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-startforwardstreamtorooms).

Adding and removing rooms by calling this method will trigger [onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onforwardstreamstatechanged) on the local.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|configuration |const ForwardStreamConfiguration& |Information of the rooms where you want to relay the media stream to. Refer to [ForwardStreamConfiguration](https://docs.byteplus.com/en/docs/12/docs-70098#ForwardStreamConfiguration) for more information. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

Users in the room which is added or removed from the target list by calling this method will receive [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserjoined), [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserpublishstreamaudio).

### stopForwardStreamToRooms

```cpp
virtual int stopForwardStreamToRooms() = 0;
```

Call this method to stop relaying media stream to all rooms after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-startforwardstreamtorooms).

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* Call this method will trigger [onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onforwardstreamstatechanged).

* The other users in the room will receive callback of [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserjoined), [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserpublishstreamaudio) when you stop relaying.

* To stop relaying media stream to specific rooms, call [updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-updateforwardstreamtorooms) instead.

* To resume the relaying in a short time, call [pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-pauseforwardstreamtoallrooms) instead and then call [resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-resumeforwardstreamtoallrooms) to resume after that.

### pauseForwardStreamToAllRooms

```cpp
virtual int pauseForwardStreamToAllRooms() = 0;
```

Call this method to pause relaying media stream to all rooms after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-startforwardstreamtorooms).

After that, call [resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-resumeforwardstreamtoallrooms) to resume.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

The other users in the room will receive callback of [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserpublishstreamaudio) when you pause relaying.

### resumeForwardStreamToAllRooms

```cpp
virtual int resumeForwardStreamToAllRooms() = 0;
```

Call this method to resume relaying to all rooms from the pause by calling [pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-pauseforwardstreamtoallrooms).

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

The other users in the room will receive callback of [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserjoined), [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onuserpublishstreamaudio) when you resume relaying.

### getRangeAudio

```cpp
virtual IRangeAudio* getRangeAudio() = 0;
```

Gets range audio instance.

**Return Value**

API call result:

* IRangeAudio: Success. You will get an [IRangeAudio](https://docs.byteplus.com/en/docs/12/14184#IRangeAudio) returned from the SDK.

* nullptr: Failure. The current SDK does not offer range audio function.

**Notes**

The first time this API is called must be between you create a room and you actually enter the room. Refer to [Range Voice](https://docs.byteplus.com/byteplus-rtc/docs/114727) for more information.

### getSpatialAudio

```cpp
virtual ISpatialAudio* getSpatialAudio() = 0;
```

Gets spatial audio instance.

**Return Value**

API call result:

* ISpatialAudio: Success. You will get an [ISpatialAudio](https://docs.byteplus.com/en/docs/12/14184#ISpatialAudio) returned from the SDK.

* nullptr: Failure. The current SDK does not offer spatial audio function.

**Notes**

* The first time this API is called must be between you create a room and you actually enter the room. Refer to [Spatial Audio](https://docs.byteplus.com/byteplus-rtc/docs/93903) for more information.

* Only using real dual\-channel playback device can you actually enjoy spatial audio effect.

* Low\-end device may have audio stalling issues due to its poor performance, so it is not recommended to enable spatial audio function on such kind of devices.

* SDK currently supports up to 30 users publishing audio with spatial audio enabled at the same time in the same room.

### setRemoteRoomAudioPlaybackVolume

```cpp
virtual int setRemoteRoomAudioPlaybackVolume(int volume) = 0;
```

Adjusts the audio playback volume from all the remote users in a room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |int |Ratio(%) of playback volume to original volume, in the range [0, 400], with overflow protection.<br><br> <br><br>To ensure the audio quality, we recommend setting the volume to `100`.<br><br><br> <br><br>* 0: mute<br><br>* 100: original volume. Default value.<br><br>* 400: Up to 4 times the original volume (with overflow protection) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details

**Notes**

Suppose a remote user A is always within the range of the target user whose playback volume will be adjusted,

* If you use both this method and [setRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setremoteaudioplaybackvolume), the volume that the local user hears from user A is the volume set by the method called later.

* If you use both this method and [setPlaybackVolume](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-setplaybackvolume), the volume that the local user hears from user A is the overlay of both settings.

### setAudioSelectionConfig

```cpp
virtual int setAudioSelectionConfig(AudioSelectionPriority audio_selection_priority) = 0;
```

> Available since 3.52.

Set the priority of the local audio stream to be published.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audio_selection_priority |AudioSelectionPriority |The priority of the local audio stream which defaults to be subscribable only up to the result of the Audio Selection. Refer to [AudioSelectionPriority](https://docs.byteplus.com/en/docs/12/docs-70098#AudioSelectionPriority). |

**Notes**

* You must enable Audio Selection in the RTC console before using this API. You can call this API whether the user has joined a room. Refer to [Audio Selection](https://docs.byteplus.com/byteplus-rtc/docs/113547).

* The setting is independent in each room that the user joins.

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
|key |const char\* |Key of the extra information, less than 10 bytes in length.<br><br> <br><br>A maximum of 5 keys can exist in the same room, beyond which the first key will be replaced. |
|value |const char\* |Content of the extra information, less than 128 bytes in length. |

**Return Value**

API call result:

* 0: Success with a taskId returned.

* <0: Failure. See [SetRoomExtraInfoResult](https://docs.byteplus.com/en/docs/12/docs-70098#SetRoomExtraInfoResult) for the reasons.

**Notes**

* Call [joinRoom](https://docs.byteplus.com/en/docs/12/14184#IRTCRoom-joinroom) first before you call this API to set extra information.

* After calling this API, you will receive [onSetRoomExtraInfoResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onsetroomextrainforesult) callback informing you the result of the setting.

* After the extra information is successfully set, other users in the same room will receive the information through [onRoomExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCRoomEventHandler-onroomextrainfoupdate) callback.

* Users who join the room later will be notified of all extra information in the room set prior to entering.

### getRoomId

```cpp
virtual const char* getRoomId() = 0;
```

> Available since 3.53

Get room ID.

**Return Value**

Room ID.

### getCallId

```cpp
virtual const char* getCallId() = 0;
```

> Available since 3.60.

Gets call ID.

Call this method after joining a room. After creating a room, a call ID is generated to identify the call for this room.

**Return Value**

Call ID.

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
|live_mode |RoomLiveMode |Live mode. See [RoomLiveMode](https://docs.byteplus.com/en/docs/12/docs-70098#RoomLiveMode) for details. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

# Public API

## Member Property

|Type |Name |
|---|---|
|void\* |[view_t](https://docs.byteplus.com/en/docs/12/14184#view_t) |

## Function

|Return |Name |
|---|---|
|BYTERTC_API IAudioFrame\* |[buildAudioFrame](https://docs.byteplus.com/en/docs/12/14184#buildaudioframe) |
|BYTERTC_API IEncodedVideoFrame\* |[buildEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/14184#buildencodedvideoframe) |
|BYTERTC_API IHWDeviceContext\* |[createStreamingHwDeviceContext](https://docs.byteplus.com/en/docs/12/14184#createstreaminghwdevicecontext) |
|STREAMING_RTC_API IStreamingRTCEngine\* |[createStreamingRTCEngine](https://docs.byteplus.com/en/docs/12/14184#createstreamingrtcengine) |
|STREAMING_RTC_API void |[destroyStreamingRTCEngine](https://docs.byteplus.com/en/docs/12/14184#destroystreamingrtcengine) |

## Instructions

### view_t

```cpp
typedef void* bytertc::view_t
```

Windows window id, Windows platform down to Windows window handle

### buildAudioFrame

```cpp
BYTERTC_API IAudioFrame* buildAudioFrame(const AudioFrameBuilder& builder);
```

Create IAudioFrame

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|builder |const AudioFrameBuilder& |Audio frame build instance. See [AudioFrameBuilder](https://docs.byteplus.com/en/docs/12/docs-70098#AudioFrameBuilder) |

**Return Value**

Refer to [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70098#IAudioFrame) for more details.

### buildEncodedVideoFrame

```cpp
BYTERTC_API IEncodedVideoFrame* buildEncodedVideoFrame(const EncodedVideoFrameBuilder& builder);
```

Create IEncodedVideoFrame

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|builder |const EncodedVideoFrameBuilder& |Encoded video frame build instance. See [EncodedVideoFrameBuilder](https://docs.byteplus.com/en/docs/12/docs-70098#EncodedVideoFrameBuilder) |

**Return Value**

[IEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70098#IEncodedVideoFrame) instance

### createStreamingHwDeviceContext

```cpp
BYTERTC_API IHWDeviceContext* createStreamingHwDeviceContext(HWDeviceType device_type);
```

create hw_context.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|device_type |HWDeviceType |See [HWDeviceType](https://docs.byteplus.com/en/docs/12/docs-70098#HWDeviceType). |

**Return Value**

See [IHWDeviceContext](https://docs.byteplus.com/en/docs/12/docs-70098#IHWDeviceContext).

### createStreamingRTCEngine

```cpp
STREAMING_RTC_API IStreamingRTCEngine* createStreamingRTCEngine(const streamingrtc::EngineConfig& config,
        IStreamingRTCEventHandler* handler, const char* parameters);
```

Create an IStreamingRTCEngine instance.

This is the first API you must call if you want to use all the RTC capabilities.

If the current thread does not have an engine instance, calling this API will create one. If an engine instance has been created, calling this API again will create another instance.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|config |const streamingrtc::EngineConfig& |Set type of IStreamingRTCEngine, ports and appid. Refer to [EngineConfig](https://docs.byteplus.com/en/docs/12/docs-70098#EngineConfig) for details. |
|handler |IStreamingRTCEventHandler\* |Handler sent from SDK to App. Refer to [IStreamingRTCEventHandler](https://docs.byteplus.com/en/docs/12/docs-70096#IStreamingRTCEventHandler) for more details. |
|parameters |const char\* |Reserved parameter, in JSON string format. |

**Return Value**

* IStreamingRTCEngine: A successfully created engine instance

* Null: Creation failed

**Notes**

* If you want to destroy multiple engine instances created in the same thread, destroy each of these instances by calling [destroyStreamingRTCEngine](https://docs.byteplus.com/en/docs/12/14184#destroystreamingrtcengine).

* The number of engine instances created on a device depends on the hardware performance.

### destroyStreamingRTCEngine

```cpp
STREAMING_RTC_API void destroyStreamingRTCEngine(IStreamingRTCEngine* engine);
```

Destroy the engine instance created by calling [createStreamingRTCEngine](https://docs.byteplus.com/en/docs/12/14184#createstreamingrtcengine), and release all related resources.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|engine |IStreamingRTCEngine\* |The engine instance created by calling [createStreamingRTCEngine](https://docs.byteplus.com/en/docs/12/14184#createstreamingrtcengine) |

**Notes**

* Call this API after all tasks related to the engine instance end.

* When calling the API, Streaming RTC SDK destroys all memory associated with the engine instance and stops any interaction with the media server.

* Calling this API will start the SDK exit logic. The engine thread is held until the exit logic is complete. The engine thread is retained until the exit logic is complete. Therefore, do not call this API directly in the callback thread, or it will cause a deadlock. This function takes a long time to execute, so it's not recommended to call this API in the main thread, or the main thread may be blocked.

# IStreamingRTCEngine

```cpp
class bytertc::streamingrtc::IStreamingRTCEngine
```

The features of high bitrate and low latency make the streaming engine an ideal choice for P2P transmission in game streaming and other similar scenarios.

Contact our presales specialist or technical service for the SDK with the streaming engine if you need the feature.

## Member Functions

|Return |Name |
|---|---|
|virtual int |[startup](https://docs.byteplus.com/en/docs/12/14184#IStreamingRTCEngine-startup) |
|virtual int |[shutdown](https://docs.byteplus.com/en/docs/12/14184#IStreamingRTCEngine-shutdown) |
|virtual int64_t |[sendP2PMessage](https://docs.byteplus.com/en/docs/12/14184#IStreamingRTCEngine-sendp2pmessage) |
|virtual int64_t |[sendP2PBinaryMessage](https://docs.byteplus.com/en/docs/12/14184#IStreamingRTCEngine-sendp2pbinarymessage) |
|virtual int |[pullAudioFrame](https://docs.byteplus.com/en/docs/12/14184#IStreamingRTCEngine-pullaudioframe) |
|virtual int |[pushAudioFrame](https://docs.byteplus.com/en/docs/12/14184#IStreamingRTCEngine-pushaudioframe) |
|virtual int |[setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/14184#IStreamingRTCEngine-setvideoencoderconfig) |
|virtual void |[setVideoDecoderConfig](https://docs.byteplus.com/en/docs/12/14184#IStreamingRTCEngine-setvideodecoderconfig) |
|virtual void |[setVideoSourceHWDeviceContext](https://docs.byteplus.com/en/docs/12/14184#IStreamingRTCEngine-setvideosourcehwdevicecontext) |
|virtual void |[setVideoSourceType](https://docs.byteplus.com/en/docs/12/14184#IStreamingRTCEngine-setvideosourcetype) |
|virtual int |[pushVideoFrame](https://docs.byteplus.com/en/docs/12/14184#IStreamingRTCEngine-pushvideoframe) |
|virtual int |[pushEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/14184#IStreamingRTCEngine-pushencodedvideoframe) |
|virtual void |[requestRemoteVideoKeyFrame](https://docs.byteplus.com/en/docs/12/14184#IStreamingRTCEngine-requestremotevideokeyframe) |
|virtual void |[setReportExtraInfo](https://docs.byteplus.com/en/docs/12/14184#IStreamingRTCEngine-setreportextrainfo) |

## Instructions

### startup

```cpp
virtual int startup() = 0;
```

startup StreamingRTCEngine

Set types and ports of the engine instance in [EngineConfig](https://docs.byteplus.com/en/docs/12/docs-70098#EngineConfig).

**Return Value**

* 0:Success

* !0:Failure

**Notes**

If the connection is terminated, the client will retry until the connection establishes.

### shutdown

```cpp
virtual int shutdown() = 0;
```

Shutdown StreamingRTCEngine

**Return Value**

* 0:Success

* !0:Failure

### sendP2PMessage

```cpp
virtual int64_t sendP2PMessage(
    const char* message,
    bool reliable
) = 0;
```

Send point\-to\-point text messages

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|message |const char\* |Text message within 62 KB<br><br> <br><br>The size of an unreliable message is under 1 KB. |
|reliable |bool |true: The message will be reliably delivered to the online peer.<br><br> <br><br>false: It is faster though the online peer may not receive the message. |

**Return Value**

* `>= 0`：Success. The return value is an ID of the message.

* `< 0`：Failure.

### sendP2PBinaryMessage

```cpp
virtual int64_t sendP2PBinaryMessage(
    const uint8_t* message,
    int length,
    bool reliable
) = 0;
```

Send point\-to\-point binary messages

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|message |const uint8_t\* |Binary message to be sent |
|length |int |Length of the message in byte. The maximum length is 62 KB.<br><br> <br><br>The maximum length of an unreliable message is 1 KB. |
|reliable |bool |true: The message will be reliably delivered to the online peer.<br><br> <br><br>false: It is faster though the online peer may not receive the message. |

**Return Value**

* `>= 0`：Success. The return value is an ID of the message.

* `< 0`：Failure.

### pullAudioFrame

```cpp
virtual int pullAudioFrame(bytertc::IAudioFrame* audio_frame) = 0;
```

Pull Audio data

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audio_frame |bytertc::IAudioFrame\* |Received audio data. Refer to [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70098#IAudioFrame) for more details.<br><br> <br><br>Refer to [pushAudioFrame](https://docs.byteplus.com/en/docs/12/14184#IStreamingRTCEngine-pushaudioframe) for information on how to push audio frames. |

**Return Value**

See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus).

### pushAudioFrame

```cpp
virtual int pushAudioFrame(bytertc::IAudioFrame* audio_frame) = 0;
```

Send Audio data

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audio_frame |bytertc::IAudioFrame\* |Audio frames to be sent. Refer to [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70098#IAudioFrame) for more details<br><br> <br><br>Refer to [AudioFrameBuilder](https://docs.byteplus.com/en/docs/12/docs-70098#AudioFrameBuilder) and [buildAudioFrame](https://docs.byteplus.com/en/docs/12/14184#buildaudioframe) for information of building Audio Frames.<br><br> <br><br>Refer to [pullAudioFrame](https://docs.byteplus.com/en/docs/12/14184#IStreamingRTCEngine-pullaudioframe) for information on how to pull audio frames. |

**Return Value**

See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus).

**Notes**

Push audio frame need to set the time stamp `AudioFrameBuilder.timestamp_us`.

### setVideoEncoderConfig

```cpp
virtual int setVideoEncoderConfig(
    streamingrtc::StreamIndex stream_index,
    const VideoSolution* solutions,
    int solution_num
) = 0;
```

Sets the video encoder configuration of each individual stream for simulcasting, including resolution, frame rate, bitrate, scale mode, fallback strategy under poor network conditions, etc.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|stream_index |streamingrtc::StreamIndex |Stream index. Refer to [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-70098#StreamIndex) for more details. |
|solutions |const VideoSolution\* |Video configuration of each individual stream for simulcasting. Refer to [VideoSolution](https://docs.byteplus.com/en/docs/12/docs-70098#VideoSolution) for more details.<br><br> <br><br>The maximum resolution is 4096 px × 4096 px. The simulcasting fails if the resolution exceeds the maximum or the other circumstances fail the encoding. |
|solution_num |int |The length of `solutions` array.<br><br> <br><br>The length of `solutions` is no more than 4. The resolutions must be in descending sort. |

**Return Value**

* 0: Success

   +! 0: Failure

### setVideoDecoderConfig

```cpp
virtual void setVideoDecoderConfig(
    streamingrtc::StreamIndex stream_index,
    VideoDecoderConfig config
) = 0;
```

Set decoding options for remote video data

Call this API before calling [startup](https://docs.byteplus.com/en/docs/12/14184#IStreamingRTCEngine-startup).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|stream_index |streamingrtc::StreamIndex |Designate the remote video stream to be decoded. Refer to [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-70098#StreamIndex) for more details. |
|config |VideoDecoderConfig |Video decoding options. Refer to [VideoDecoderConfig](https://docs.byteplus.com/en/docs/12/docs-70098#VideoDecoderConfig) for more details. |

**Notes**

To decode a remote stream in a custom way, call this API and set the decoding method to custom decoding. You can get the data through [onP2PRemoteEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IStreamingRTCEventHandler-onp2premoteencodedvideoframe) and/or [onP2PRemoteVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IStreamingRTCEventHandler-onp2premotevideoframe).

### setVideoSourceHWDeviceContext

```cpp
virtual void setVideoSourceHWDeviceContext(
    StreamIndex stream_index,
    IHWDeviceContext* hw_context
) = 0;
```

Set the device context information of the video source

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|stream_index |StreamIndex |See [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-70098#StreamIndex). |
|hw_context |IHWDeviceContext\* |See [IHWDeviceContext](https://docs.byteplus.com/en/docs/12/docs-70098#IHWDeviceContext). |

### setVideoSourceType

```cpp
virtual void setVideoSourceType(
    streamingrtc::StreamIndex stream_index,
    VideoSourceType type
) = 0;
```

Set the video source of the StreamingEngine.

The internal video capture is the default video source, which refers to capturing video using the built\-in module.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|stream_index |streamingrtc::StreamIndex |Stream index. Refer to [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-70098#StreamIndex) for more details. |
|type |VideoSourceType |Video source type. Currently, `VideoSourceType::VideoSourceTypeInternal` is not available for `type`. Refer to [VideoSourceType](https://docs.byteplus.com/en/docs/12/docs-70098#VideoSourceType) for more details. |

**Notes**

You can call this API whether the engine has started or not.

### pushVideoFrame

```cpp
virtual int pushVideoFrame(
    streamingrtc::StreamIndex stream_index,
    IVideoFrame* frame
) = 0;
```

Send external\-source video data

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|stream_index |streamingrtc::StreamIndex |Stream index. Designate the video stream where the external video frames to be pushed. Refer to [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-70098#StreamIndex) for more details. |
|frame |IVideoFrame\* |Video frame format. Only YUV420P is available. Refer to [IVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70098#IVideoFrame) for more details. |

**Return Value**

See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus).

**Notes**

* Call this API within the thread called by the user.

* Before pushing external video frames, call [setVideoSourceType](https://docs.byteplus.com/en/docs/12/14184#IStreamingRTCEngine-setvideosourcetype) to switch to external video source.

### pushEncodedVideoFrame

```cpp
virtual int pushEncodedVideoFrame(
    streamingrtc::StreamIndex stream_index,
    int video_index,
    IEncodedVideoFrame* video_stream
) = 0;
```

Push video stream encoded with the external encoder.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|stream_index |streamingrtc::StreamIndex |Designate the video stream where the encoded video frames to be pushed. Refer to [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-70098#StreamIndex) for more details. |
|video_index |int |Designate the resolution index of the video stream in the simulcast. The number starts from 0 and must match the setting when calling [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/14184#IStreamingRTCEngine-setvideoencoderconfig). |
|video_stream |IEncodedVideoFrame\* |Encoded stream video frame information. Only video frames in H264 and ByteVC1 formats are supported.<br><br>. Refer to [IEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70098#IEncodedVideoFrame). |

**Return Value**

See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus).

**Notes**

* Call this API within the thread called by the user.

* Before pushing custom encoded video frames, call [setVideoSourceType](https://docs.byteplus.com/en/docs/12/14184#IStreamingRTCEngine-setvideosourcetype) to switch to the external video\-encoding module.

### requestRemoteVideoKeyFrame

```cpp
virtual void requestRemoteVideoKeyFrame(streamingrtc::StreamIndex stream_index) = 0;
```

After subscribing to the remote video stream, request the key frame to the remote

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|stream_index |streamingrtc::StreamIndex |Designate the video stream to be requested. Refer to [StreamIndex](https://docs.byteplus.com/en/docs/12/docs-70098#StreamIndex) for more details. |

**Notes**

* This API is available after successful subscription to the remote stream in the manual\-subscription way.

* This API is available after failing to decode using the external decoder.

### setReportExtraInfo

```cpp
virtual void setReportExtraInfo(const char* extra_info)=0;
```

Set extra_info of trace.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|extra_info |const char\* |Reported info |

# IMediaPlayer

```cpp
class bytertc::IMediaPlayer
```

> Available since 3.53

Media player

Call [setEventHandler](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-seteventhandler) to set the callback handler to receive related callbacks.

## Member Functions

|Return |Name |
|---|---|
|IMediaPlayer |[IMediaPlayer](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-imediaplayer) |
|virtual |[~IMediaPlayer](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-~imediaplayer) |
|virtual int |[open](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-open) |
|virtual int |[start](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-start) |
|virtual int |[openWithCustomSource](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-openwithcustomsource) |
|virtual int |[stop](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-stop) |
|virtual int |[pause](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-pause) |
|virtual int |[resume](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-resume) |
|virtual int |[setVolume](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-setvolume) |
|virtual int |[getVolume](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-getvolume) |
|virtual int |[getTotalDuration](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-gettotalduration) |
|virtual int |[getPlaybackDuration](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-getplaybackduration) |
|virtual int |[getPosition](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-getposition) |
|virtual PlayerState |[getState](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-getstate) |
|virtual int |[setAudioPitch](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-setaudiopitch) |
|virtual int |[setPosition](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-setposition) |
|virtual int |[setAudioDualMonoMode](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-setaudiodualmonomode) |
|virtual int |[getAudioTrackCount](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-getaudiotrackcount) |
|virtual int |[selectAudioTrack](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-selectaudiotrack) |
|virtual int |[setPlaybackSpeed](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-setplaybackspeed) |
|virtual int |[setProgressInterval](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-setprogressinterval) |
|virtual int |[setLoudness](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-setloudness) |
|virtual int |[registerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-registeraudioframeobserver) |
|virtual int |[pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-pushexternalaudioframe) |
|virtual int |[setEventHandler](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-seteventhandler) |

## Instructions

### IMediaPlayer

```cpp
IMediaPlayer(){}
```

### ~IMediaPlayer

```cpp
virtual ~IMediaPlayer() {}
```

### open

```cpp
virtual int open(
    const char* file_path,
    const MediaPlayerConfig& config
) = 0;
```

Open the audio file.

You can only open one audio file with one player instance at the same time. For multiple audio files at the same time, create multiple player instances.

For audio file in PCM format, see [openWithCustomSource](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-openwithcustomsource). `openWithCustomSource` and this API are mutually exclusive.

**Input Parameters**

|Audio file paths.<br><br> <br><br>URL of online file, URI of local file, or full path to local file. For URL of online file, only the https protocol is supported.<br><br> <br><br>Recommended sample rate for audio effect files: 8KHz, 16KHz, 22.05KHz, 44.1KHz, 48KHz.<br><br> <br><br>Local audio effect file formats supported by different platforms:<br><br> <br><br> <br><br> <br><br> <br><br>Online audio effect file formats supported by different platforms.<br><br> <br><br> <br><br> | | |
|---|---|---|
|config |const MediaPlayerConfig& |See [MediaPlayerConfig](https://docs.byteplus.com/en/docs/12/docs-70098#MediaPlayerConfig). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

### start

```cpp
virtual int start() = 0;
```

Start playing the audio. Call this API when you call [open](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-open) and set `AutoPlay=False`.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* For audio file in PCM format, see [openWithCustomSource](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-openwithcustomsource). `openWithCustomSource` and this API are mutually exclusive.

* After calling this API, call [stop](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-stop) to stop playing the audio file.

### openWithCustomSource

```cpp
virtual int openWithCustomSource(
    const MediaPlayerCustomSource& source,
    const MediaPlayerConfig& config
) = 0;
```

Enable audio mixing with audio raw data.

To open the audio file, see [open](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-open). `open` and this API are mutually exclusive.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|source |const MediaPlayerCustomSource& |See [MediaPlayerCustomSource](https://docs.byteplus.com/en/docs/12/docs-70098#MediaPlayerCustomSource). |
|config |const MediaPlayerConfig& |See [MediaPlayerConfig](https://docs.byteplus.com/en/docs/12/docs-70098#MediaPlayerConfig). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* After calling this API, you must call [pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-pushexternalaudioframe) to push audio data and start the audio mixing.

* To stop the raw data audio mixing, call [stop](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-stop).

### stop

```cpp
virtual int stop() = 0;
```

After calling [open](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-open), [start](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-start), or [openWithCustomSource](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-openwithcustomsource) to start audio mixing, call this method to stop audio mixing.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

### pause

```cpp
virtual int pause() = 0;
```

After calling [open](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-open), or [start](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-start) to start audio mixing, call this API to pause audio mixing.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* After calling this API to pause audio mixing, call [resume](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-resume) to resume audio mixing.

* The API is valid for audio files, not PCM data.

### resume

```cpp
virtual int resume() = 0;
```

After calling [pause](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-pause) to pause audio mixing, call this API to resume audio mixing.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

The API is valid for audio files, not PCM data.

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
|type |AudioMixingType |See [AudioMixingType](https://docs.byteplus.com/en/docs/12/docs-70098#AudioMixingType). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

Call this API only when audio is mixing.

### getVolume

```cpp
virtual int getVolume(AudioMixingType type) = 0;
```

Gets the current volume.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |AudioMixingType |See [AudioMixingType](https://docs.byteplus.com/en/docs/12/docs-70098#AudioMixingType). |

**Return Value**

* \>0: Success, the current volume.

* < 0: Failed.

**Notes**

Call this API only when audio is mixing, including media file mixing and PCM mixing.

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

* The API is valid for audio files, not PCM data.

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

* Call this API only when audio is mixing and the interval set by [setProgressInterval](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-setprogressinterval) is above `0`.

* The API is valid for audio files, not PCM data.

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

* The API is valid for audio files, not PCM data.

### getState

```cpp
virtual PlayerState getState() = 0;
```

Get the state of the media player.

**Return Value**

The current state of the media player. See [PlayerState](https://docs.byteplus.com/en/docs/12/docs-70098#PlayerState).

**Notes**

You can call this method after the creating a `IMediaPlayer` instance.

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

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* Call this API only when audio is mixing.

* Support audio file only and not PCM data.

### setPosition

```cpp
virtual int setPosition(int position) = 0;
```

Sets the starting playback position of the media file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|position |int |The starting position of the media file in milliseconds.<br><br> <br><br>You can get the total duration of the media file through [getTotalDuration](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-gettotalduration). The value of position should be less than the total duration of the media file. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* The API is valid for audio files, not PCM data.

* When playing online files, calling this API may cause playback delay.

### setAudioDualMonoMode

```cpp
virtual int setAudioDualMonoMode(AudioMixingDualMonoMode mode) = 0;
```

Sets the channel mode of the mixing of the media file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mode |AudioMixingDualMonoMode |The mode of channel. The default channel mode is the same as the source file. See [AudioMixingDualMonoMode](https://docs.byteplus.com/en/docs/12/docs-70098#AudioMixingDualMonoMode). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* Call this API only when audio is mixing.

* Audio file is supported, but not PCM data.

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

### selectAudioTrack

```cpp
virtual int selectAudioTrack(int index) = 0;
```

Specifies the playback track of the current media file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|index |int |The specified playback audio track, starting from 0, and the range is `[0, getAudioTrackCount()-1]`. The value must be less than the return value of [getAudioTrackCount](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-getaudiotrackcount). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* Call this API only when audio is mixing.

* This API is valid for audio file, not PCM data.

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

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* Call this API only when audio is mixing.

* The API is valid for audio files and not PCM data.

### setProgressInterval

```cpp
virtual int setProgressInterval(int64_t interval) = 0;
```

Set the interval of the periodic callback [onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-70096#IMediaPlayerEventHandler-onmediaplayerplayingprogress) during audio mixing.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|interval |int64_t |interval in ms.<br><br><br> <br><br>* interval \> 0: The callback is enabled. The actual interval is a multiple of 10. If the input value is not divisible by 10, it will be automatically rounded up. For example, if the input is `52`, the actual interval will be 60 milliseconds.<br><br>* interval <= 0: The callback is disabled. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* Call this API only when audio is mixing.

* This API is valid for audio file, not PCM data.

### setLoudness

```cpp
virtual int setLoudness(float loudness) = 0;
```

To call [enableVocalInstrumentBalance](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-enablevocalinstrumentbalance) to adjust the volume of the mixed media file or the PCM audio data, you must pass in its original loudness through this API.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|loudness |float |Original loudness in lufs. The range is `[-70.0, 0.0]`.<br><br> <br><br>When the value is less than \-70.0lufs, it will be adjusted to \-70.0lufs by default, and if it is more than 0.0lufs, the loudness will not be equalized. The default value is 1.0lufs, which means no processing. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* Call this API only when audio is mixing.

* The API is valid for audio files and PCM data.

### registerAudioFrameObserver

```cpp
virtual int registerAudioFrameObserver(IMediaPlayerAudioFrameObserver* observer) = 0;
```

Register an observer to receive related callbacks when the local media file is mixing.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|observer |IMediaPlayerAudioFrameObserver\* |See [IMediaPlayerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70096#IMediaPlayerAudioFrameObserver). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

The API is valid for audio files, not PCM data.

### pushExternalAudioFrame

```cpp
virtual int pushExternalAudioFrame(IAudioFrame* audio_frame) = 0;
```

Push PCM audio frame data for mixing.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audio_frame |IAudioFrame\* |See [IAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70098#IAudioFrame).<br><br><br> <br><br>* The audio sampling format must be S16. The data format within the audio buffer must be PCM, and its capacity should be `audioFrame.samples × audioFrame.channel × 2`.<br><br>* A specific sample rate and the number of channels must be specified; it is not supported to set them to automatic. |

**Return Value**

* 0: Success.

* < 0: Failed.

**Notes**

* Before calling this method, the raw audio data mixing must be enabled through [openWithCustomSource](https://docs.byteplus.com/en/docs/12/14184#IMediaPlayer-openwithcustomsource).

* Suggestions: Before pushing data for the first time, please cache a certain amount of data (like 200 ms) on the application side, and then push it at once. Schedule subsequent push operation every 10 ms with audio data of 10 ms.

* To pause the playback, just pause the push.

### setEventHandler

```cpp
virtual int setEventHandler(IMediaPlayerEventHandler* handler) = 0;
```

Set the event handler.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|handler |IMediaPlayerEventHandler\* |See [IMediaPlayerEventHandler](https://docs.byteplus.com/en/docs/12/docs-70096#IMediaPlayerEventHandler). |

**Return Value**

* 0: Success.

* < 0: Failed.

# IAudioEffectPlayer

```cpp
class bytertc::IAudioEffectPlayer
```

> Available since 3.53

Audio effect player

Call [setEventHandler](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-seteventhandler) to set the callback handler to receive related callbacks.

## Member Functions

|Return |Name |
|---|---|
|IAudioEffectPlayer |[IAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-iaudioeffectplayer) |
|virtual |[~IAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-~iaudioeffectplayer) |
|virtual int |[start](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-start) |
|virtual int |[stop](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-stop) |
|virtual int |[stopAll](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-stopall) |
|virtual int |[preload](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-preload) |
|virtual int |[unload](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-unload) |
|virtual int |[unloadAll](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-unloadall) |
|virtual int |[pause](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-pause) |
|virtual int |[pauseAll](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-pauseall) |
|virtual int |[resume](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-resume) |
|virtual int |[resumeAll](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-resumeall) |
|virtual int |[setPosition](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-setposition) |
|virtual int |[getPosition](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-getposition) |
|virtual int |[setVolume](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-setvolume) |
|virtual int |[setVolumeAll](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-setvolumeall) |
|virtual int |[getVolume](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-getvolume) |
|virtual int |[getDuration](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-getduration) |
|virtual int |[setEventHandler](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-seteventhandler) |

## Instructions

### IAudioEffectPlayer

```cpp
IAudioEffectPlayer(){}
```

### ~IAudioEffectPlayer

```cpp
virtual ~IAudioEffectPlayer() {}
```

### start

```cpp
virtual int start(
    int effect_id,
    const char* file_path,
    const AudioEffectPlayerConfig& config
) = 0;
```

Starts to play the audio effect file.

This API can be called multiple times with different IDs and file paths for multiple effects at the same time.

**Input Parameters**

|Audio effect file paths.<br><br> <br><br>URL of online file, URI of local file, or full path to the local file are supported. For URL of online file, only the https protocol is supported.<br><br> <br><br>Recommended sample rate for audio effect files: 8KHz, 16KHz, 22.05KHz, 44.1KHz, 48KHz.<br><br> <br><br>Local audio effect file formats supported by different platforms:<br><br> <br><br> <br><br> <br><br> <br><br>Online audio effect file formats supported by different platforms.<br><br> <br><br> <br><br> | | |
|---|---|---|
|config |const AudioEffectPlayerConfig& |See [AudioEffectPlayerConfig](https://docs.byteplus.com/en/docs/12/docs-70098#AudioEffectPlayerConfig). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* If the file has been loaded into memory via [preload](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-preload), make sure that the ID here is the same as the ID set by [preload](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-preload).

* After starting to play an audio effect file, you can call the [stop](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-stop) API to stop playing the audio effect file.

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

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* After calling the [start](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-start) API to start playing the audio effect file, you can call this API to stop playing the audio effect file.

* After calling this API to stop playing an audio effect file, the audio effect file will be unloaded automatically.

### stopAll

```cpp
virtual int stopAll() = 0;
```

Stops playback of all audio effect files.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* After calling [start](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-start) to start playing audio effect files, you can call this API to stop playing all audio effect files.

* After calling this API to stop playing all audio effect files, the audio effect files will be unloaded automatically.

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
|effect_id |int |Audio effect ID. Used for identifying the audio effect. Please ensure that the audio effect ID is unique.<br><br> <br><br>If this API is called repeatedly with the same ID, the later one will overwrite the previous one.<br><br> <br><br>If you call [start](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-start) first and then call this API with the same ID, the SDK will stop the previous effect and then load the next one, and you will receive [onAudioEffectPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioEffectPlayerEventHandler-onaudioeffectplayerstatechanged).<br><br> <br><br>After calling this API to preload A.mp3, if you need to call [start](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-start) to play B.mp3 with the same ID, please call [unload](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-unload) to unload A.mp3 first, otherwise SDK will report an error AUDIO_MIXING_ERROR_LOAD_CONFLICT. |
|file_path |const char\* |The filepath of effect file. URI of local file.<br><br> <br><br>The length of the pre\-loaded file must not exceed 20s.<br><br> <br><br>Audio effect file formats supported are the same as [start](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-start). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* This API just preloads the specified audio effect file, and only calls the [start](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-start) API to start playing the specified audio effect file.

* The specified audio effect file preloaded by calling this API can be unloaded by [unload](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-unload).

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

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

Call this API after [start](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-start) or [preload](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-preload).

### unloadAll

```cpp
virtual int unloadAll() = 0;
```

Unloads all audio effect files.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

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

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* After calling the [start](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-start) API to start playing the audio effect file, you can pause the audio effect file by calling this API.

* After calling this API to pause the audio effect file, you can call the [resume](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-resume) API to resume playback.

### pauseAll

```cpp
virtual int pauseAll() = 0;
```

Pauses the Playback of all audio effect files.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* After calling the [start](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-start) API to start playing audio effect files, you can pause playing all audio effect files by calling this API.

* After calling this API to pause the playback of all audio effect files, you can call the [resumeAll](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-resumeall) API to resume all playback.

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

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

After calling the [pause](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-pause) API to pause the audio effect file, you can resume playback by calling this API.

### resumeAll

```cpp
virtual int resumeAll() = 0;
```

Resumes the playback of all audio effect files.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

After calling the [pauseAll](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-pauseall) API to pause all the audio effect files being played, you can resume playback by calling this API.

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
|pos |int |The starting playback position of the audio effect file in milliseconds.<br><br> <br><br>You can get the total duration of the audio effect file by calling [getDuration](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-getduration), the value of pos should be less than the total duration of the audio effect file. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

* When playing online files, calling this API may cause a delay in playback.

* Call this API after [start](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-start).

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

* Call this API after [start](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-start).

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

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

Call this API after [start](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-start).

### setVolumeAll

```cpp
virtual int setVolumeAll(int volume) = 0;
```

Sets the volume of all audio effects, including audio effect files and PCM effects.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |int |The ratio of the volume to the original volume in % with overflow protection. The range is `[0, 400]` and the recommended range is `[0, 100]`. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70098#ReturnStatus) for more details.

**Notes**

This API has a lower priority than [setVolume](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-setvolume), i.e. the volume of the audio effect set by [setVolume](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-setvolume) is not affected by this API.

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

Call this API after [start](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-start).

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

Call this API after [start](https://docs.byteplus.com/en/docs/12/14184#IAudioEffectPlayer-start).

### setEventHandler

```cpp
virtual int setEventHandler(IAudioEffectPlayerEventHandler* handler) = 0;
```

Set the event handler.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|handler |IAudioEffectPlayerEventHandler\* |See [IAudioEffectPlayerEventHandler](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioEffectPlayerEventHandler). |

**Return Value**

* 0: Success.

* < 0: Failed.

# IVideoProcessor

```cpp
class bytertc::IVideoProcessor
```

Video processor

## Member Functions

|Return |Name |
|---|---|
|virtual IVideoFrame\* |[processVideoFrame](https://docs.byteplus.com/en/docs/12/14184#IVideoProcessor-processvideoframe) |

## Instructions

### processVideoFrame

```cpp
virtual IVideoFrame* processVideoFrame(IVideoFrame* src_frame) = 0;
```

Gets the video frames captured by the RTC SDK, preprocesses them according to the settings in [registerLocalVideoProcessor](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-registerlocalvideoprocessor), and returns the processed video frames to the RTC SDK for encoding and transmission.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|src_frame |IVideoFrame\* |Video frames captured by the RTC SDK. See [IVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70098#IVideoFrame). |

**Return Value**

The video frame after video preprocessing is returned to the RTC SDK for encoding and transmission. See [IVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70098#IVideoFrame).

**Notes**

* Before video preprocessing, you need to call [registerLocalVideoProcessor](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-registerlocalvideoprocessor) to set up the video preprocessor.

* If you need to cancel the video preprocessing, you can set the video preprocessor to nullptr.

* When implementing `processVideoFrame`, you can directly modify the buffer of src_frame, call `addRef` to add the src_frame reference count by one, and return the modified `src_frame`, or you can also create a new video frame and return it.

* For the video frame returned by `processVideoFrame`, after being consumed by the SDK layer, the SDK always calls the `releaseRef` method of this video frame.

# IAudioDeviceManager

```cpp
class bytertc::IAudioDeviceManager
```

Audio device management

## Member Functions

|Return |Name |
|---|---|
|virtual IAudioDeviceCollection\* |[enumerateAudioPlaybackDevices](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-enumerateaudioplaybackdevices) |
|virtual IAudioDeviceCollection\* |[enumerateAudioCaptureDevices](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-enumerateaudiocapturedevices) |
|virtual void |[followSystemPlaybackDevice](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-followsystemplaybackdevice) |
|virtual void |[followSystemCaptureDevice](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-followsystemcapturedevice) |
|virtual int |[setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-setaudioplaybackdevice) |
|virtual int |[setAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-setaudiocapturedevice) |
|virtual int |[setAudioPlaybackDeviceVolume](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-setaudioplaybackdevicevolume) |
|virtual int |[getAudioPlaybackDeviceVolume](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-getaudioplaybackdevicevolume) |
|virtual int |[setAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-setaudiocapturedevicevolume) |
|virtual int |[getAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-getaudiocapturedevicevolume) |
|virtual int |[setAudioPlaybackDeviceMute](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-setaudioplaybackdevicemute) |
|virtual int |[getAudioPlaybackDeviceMute](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-getaudioplaybackdevicemute) |
|virtual int |[setAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-setaudiocapturedevicemute) |
|virtual int |[getAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-getaudiocapturedevicemute) |
|virtual int |[getAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-getaudioplaybackdevice) |
|virtual int |[getAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-getaudiocapturedevice) |
|virtual int |[initAudioPlaybackDeviceForTest](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-initaudioplaybackdevicefortest) |
|virtual int |[initAudioCaptureDeviceForTest](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-initaudiocapturedevicefortest) |
|virtual int |[startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-startaudioplaybackdevicetest) |
|virtual int |[stopAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-stopaudioplaybackdevicetest) |
|virtual int |[startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-startaudiodevicerecordtest) |
|virtual int |[stopAudioDeviceRecordAndPlayTest](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-stopaudiodevicerecordandplaytest) |
|virtual int |[stopAudioDevicePlayTest](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-stopaudiodeviceplaytest) |

## Instructions

### enumerateAudioPlaybackDevices

```cpp
virtual IAudioDeviceCollection* enumerateAudioPlaybackDevices() = 0;
```

Get a list of the audio playback devices. When the audio playback device changes, you will receive `onAudioMediaDeviceStateChanged` and you need to call this API again to get the new device list.

**Return Value**

A list of all audio playback devices. See [IAudioDeviceCollection](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceCollection).

If a time\-out occurs, it returns an empty list. By default, the time\-out duration is set to 10 seconds. We recommend to call this API once you get notification of `kMediaDeviceListUpdated` via [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onaudiodevicestatechanged).

**Notes**

When receiving [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onaudiodevicestatechanged) for device change, you can call this API to get the latest list of audio playback devices.

### enumerateAudioCaptureDevices

```cpp
virtual IAudioDeviceCollection* enumerateAudioCaptureDevices() = 0;
```

Get a list of audio acquisition devices in the current system. If there are subsequent device changes, you need to call this API again to get a new device list.

**Return Value**

An object that contains a list of all audio capture devices in the system. See [IAudioDeviceCollection](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceCollection).

If a time\-out occurs, it returns an empty list. By default, the time\-out duration is set to 10 seconds. We recommend to call this API once you get notification of `kMediaDeviceListUpdated` via [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onaudiodevicestatechanged).

**Notes**

When receiving [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onaudiodevicestatechanged) for device change, you can call this API to get the latest list of audio playback devices.

### followSystemPlaybackDevice

```cpp
virtual void followSystemPlaybackDevice(bool followed) = 0;
```

Set the audio playback device to follow the OS setting or not.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|followed |bool |* true: follow the OS setting. You can not call [setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-setaudioplaybackdevice) at the same time. The default value.<br><br>* false: do not follow the OS setting. You can call [setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-setaudioplaybackdevice) to set the audio playback device. |

### followSystemCaptureDevice

```cpp
virtual void followSystemCaptureDevice(bool followed) = 0;
```

Set the audio capture device to follow the OS setting or not.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|followed |bool |* true: follow the OS setting. You can not call [setAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-setaudiocapturedevice) at the same time. The default value.<br><br>* false: do not follow the OS setting. You can call [setAudioCaptureDevice](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-setaudiocapturedevice) to set the audio capture device. |

### setAudioPlaybackDevice

```cpp
virtual int setAudioPlaybackDevice(const char device_id[MAX_DEVICE_ID_LENGTH]) = 0;
```

Sets the audio playback device.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|device_id |const char[MAX_DEVICE_ID_LENGTH] |Audio playback device's ID. You can get the ID by calling<br><br> <br><br>[enumerateAudioPlaybackDevices](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-enumerateaudioplaybackdevices). |

**Return Value**

* 0: Success

* < 0: Failure

**Notes**

After you call [followSystemPlaybackDevice](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-followsystemplaybackdevice) to set the audio playback device to follow the system setting, you cannot call this API to set the audio playback device.

### setAudioCaptureDevice

```cpp
virtual int setAudioCaptureDevice(const char device_id[MAX_DEVICE_ID_LENGTH]) = 0;
```

Set up audio capture devices.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|device_id |const char[MAX_DEVICE_ID_LENGTH] |Audio capture device ID, available through [enumerateAudioCaptureDevices](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-enumerateaudiocapturedevices). |

**Return Value**

Method call result

* 0: Success.

* < 0: failure

**Notes**

After you call [followSystemCaptureDevice](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-followsystemcapturedevice) to set the audio playback device to follow the system setting, you cannot call this API to set the audio capture device.

### setAudioPlaybackDeviceVolume

```cpp
virtual int setAudioPlaybackDeviceVolume(unsigned int volume) = 0;
```

Set the current audio playback device volume

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |unsigned int |Audio playback device volume, the value range is [0,255], the setting beyond this range is invalid.<br><br><br> <br><br>* [0,25] Is nearly silent;<br><br>* [26,75] Is low volume;<br><br>* [76,204] Is medium volume;<br><br>* [205,255] Is high volume. |

**Return Value**

Method call result

* 0: Success.

* < 0: failure

### getAudioPlaybackDeviceVolume

```cpp
virtual int getAudioPlaybackDeviceVolume(unsigned int* volume) = 0;
```

Get the current audio playback device volume.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |unsigned int\* |Audio playback device volume, the range should be within [0,255].<br><br><br> <br><br>* [0,25] Is nearly silent;<br><br>* [26,75] Is low volume;<br><br>* [76,204] Is medium volume;<br><br>* [205,255] Is high volume. |

**Return Value**

Method call result

* 0: Success.

* < 0: failure

### setAudioCaptureDeviceVolume

```cpp
virtual int setAudioCaptureDeviceVolume(unsigned int volume) = 0;
```

Set the current audio capture volume

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |unsigned int |Audio capture volume, the value range is [0,255], the setting beyond this range is invalid.<br><br><br> <br><br>* [0,25] Is nearly silent;<br><br>* [26,75] Is low volume;<br><br>* [76,204] Is medium volume;<br><br>* [205,255] Is high volume. |

**Return Value**

Method call result

* 0: Success. The volume information returned by [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onlocalaudiopropertiesreport) will be changed according to this value.

* < 0: failure

**Notes**

The setting will take effect after you unmute the device via [setAudioCaptureDeviceMute](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-setaudiocapturedevicemute).

### getAudioCaptureDeviceVolume

```cpp
virtual int getAudioCaptureDeviceVolume(unsigned int* volume) = 0;
```

Get the current audio capture volume.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |unsigned int\* |Audio capture volume, the range is within [0,255].<br><br><br> <br><br>* [0,25] Is nearly silent;<br><br>* [26,75] Is low volume;<br><br>* [76,204] Is medium volume;<br><br>* [205,255] Is high volume. |

**Return Value**

Method call result

* 0: Success.

* < 0: failure

### setAudioPlaybackDeviceMute

```cpp
virtual int setAudioPlaybackDeviceMute(bool mute) = 0;
```

Mute or Unmute the current audio playback device. The default state is speaking.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mute |bool |* true: Mute<br><br>* false: Unmuted |

**Return Value**

Method call result

* 0: Success.

* < 0: failure

### getAudioPlaybackDeviceMute

```cpp
virtual int getAudioPlaybackDeviceMute(bool* mute) = 0;
```

Get the mute state of the current audio playback device.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mute |bool\* |* true: Mute<br><br>* false: Unmuted |

**Return Value**

Method call result

* 0: Success.

* < 0: failure

### setAudioCaptureDeviceMute

```cpp
virtual int setAudioCaptureDeviceMute(bool mute) = 0;
```

Mute or Unmute the current audio capture device. The default state is speaking.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mute |bool |* true: Mute<br><br>* false: Unmuted |

**Return Value**

Method call result

* 0: Success.

* < 0: failure

**Notes**

* This method affects all audio input of the system. You can choose to mute the audio signal from the microphone that excludes the media player. Refer to [muteAudioCapture](https://docs.byteplus.com/en/docs/12/14184#IRTCEngine-muteaudiocapture).

   — When the audio device is muted, volume setting via [setAudioCaptureDeviceVolume](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-setaudiocapturedevicevolume) will take effect once the device becomes unmuted.

### getAudioCaptureDeviceMute

```cpp
virtual int getAudioCaptureDeviceMute(bool* mute) = 0;
```

Get state of the audio capture device.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mute |bool\* |* true: Mute<br><br>* false: Unmuted |

**Return Value**

Method call result

* 0: Success.

* < 0: failure

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

* Call [stopAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-stopaudioplaybackdevicetest) to stop the playback test before moving on to the other device tests.

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

Call this API to stop the playback test started by calling [startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-startaudioplaybackdevicetest) before moving on to the other device tests.

### startAudioDeviceRecordTest

```cpp
virtual int startAudioDeviceRecordTest(int indication_interval) = 0;
```

Start the capture and playback test for local audio devices.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|indication_interval |int |During the test, you'll receive `onLocalAudioPropertiesReport` periodically. Set the period in ms with this parameter. Recommended value is 200 ms; the minimal value is 10 ms. |

**Return Value**

result

* 0: success

* < 0: failure

**Notes**

* The audio capturing stops in 30s after calling this API and begins to play the recording audio. Before that, you can call [stopAudioDeviceRecordAndPlayTest](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-stopaudiodevicerecordandplaytest) to stop audio capturing and start playing the recording audio.

* Call [stopAudioDevicePlayTest](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-stopaudiodeviceplaytest) to stop the test, including capturing and playing the recording.

* You must stop the test before starting another test for audio devices.

* You must stop the test before calling `enableAudioPropertiesReport`.

* This test performs locally and does not involve network connection testing.

### stopAudioDeviceRecordAndPlayTest

```cpp
virtual int stopAudioDeviceRecordAndPlayTest() = 0;
```

Call this API to stop recording in the test and start to play the recording in 30 s after calling [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-startaudiodevicerecordtest).

**Return Value**

result

* 0: Success

* < 0: Failure

**Notes**

After calling this API, the recording starts playing during which you can call [stopAudioDevicePlayTest](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-stopaudiodeviceplaytest) to stop playing.

### stopAudioDevicePlayTest

```cpp
virtual int stopAudioDevicePlayTest() = 0;
```

Stop the capture and playback test for local audio devices which is started by calling [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceManager-startaudiodevicerecordtest).

Before the test ends by itself, you can call this API to stop the recording or playing.

**Return Value**

* 0: Success

* < 0: failure

# IVideoDeviceManager

```cpp
class bytertc::IVideoDeviceManager
```

Mainly used to enumerate and set up video capture devices

## Member Functions

|Return |Name |
|---|---|
|virtual IVideoDeviceCollection\* |[enumerateVideoCaptureDevices](https://docs.byteplus.com/en/docs/12/14184#IVideoDeviceManager-enumeratevideocapturedevices) |
|virtual int |[setVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/14184#IVideoDeviceManager-setvideocapturedevice) |
|virtual int |[getVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/14184#IVideoDeviceManager-getvideocapturedevice) |

## Instructions

### enumerateVideoCaptureDevices

```cpp
virtual IVideoDeviceCollection* enumerateVideoCaptureDevices() = 0;
```

Get a list of video capture devices in the current system.

**Return Value**

Contains a list of all video capture devices in the system. See [IVideoDeviceCollection](https://docs.byteplus.com/en/docs/12/14184#IVideoDeviceCollection).

If a time\-out occurs, it returns an empty list. By default, the time\-out duration is set to 10 seconds. We recommend to call this API once you get notification of `kMediaDeviceListUpdated` via [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onvideodevicestatechanged).

**Notes**

When receiving [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onvideodevicestatechanged) for device change, you can call this API to get the latest list of audio playback devices.

### setVideoCaptureDevice

```cpp
virtual int setVideoCaptureDevice(const char device_id[MAX_DEVICE_ID_LENGTH]) = 0;
```

Set the current video capture device

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|device_id |const char[MAX_DEVICE_ID_LENGTH] |Video device ID, which can be obtained through [enumerateVideoCaptureDevices](https://docs.byteplus.com/en/docs/12/14184#IVideoDeviceManager-enumeratevideocapturedevices) |

**Return Value**

* 0: Success.

   +! 0: failure

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

# IDeviceCollection

```cpp
class bytertc::IDeviceCollection
```

> Deprecated since 3.45 and will be deleted in 3.51, use [IAudioDeviceCollection](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceCollection) and [IVideoDeviceCollection](https://docs.byteplus.com/en/docs/12/14184#IVideoDeviceCollection) instead.

Audio & video equipment related information

## Member Functions

|Return |Name |
|---|---|
|virtual int |[getCount](https://docs.byteplus.com/en/docs/12/14184#IDeviceCollection-getcount) |
|virtual int |[getDevice](https://docs.byteplus.com/en/docs/12/14184#IDeviceCollection-getdevice) |
|virtual void |[release](https://docs.byteplus.com/en/docs/12/14184#IDeviceCollection-release) |

## Instructions

### getCount

```cpp
virtual int getCount() = 0;
```

Get the number of audio and video devices in the current system

**Return Value**

Number of audio and video devices

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
|index |int |Device index number, starting from 0, note that it must be less than the return value of [getCount](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceCollection-getcount). |
|device_name |char[MAX_DEVICE_ID_LENGTH] |device name |
|device_id |char[MAX_DEVICE_ID_LENGTH] |device ID |

**Return Value**

* 0: Success.

   +! 0: failure

### release

```cpp
virtual void release() = 0;
```

Releases the resources occupied by the current [IDeviceCollection](https://docs.byteplus.com/en/docs/12/14184#IAudioDeviceCollection) object.

**Notes**

This method should be called to release related resources when you do not need to return a list of audio and video device related information.
