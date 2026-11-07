---
title: "API Reference"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080"
---

# ISpatialAudio

```java
public interface com.ss.bytertc.engine.audio.ISpatialAudio
```

Spatial audio instance.

## Member Functions

|Return |Name |
|---|---|
|void |[enableSpatialAudio](https://docs.byteplus.com/en/docs/12/14166#ISpatialAudio-enablespatialaudio) |
|void |[disableRemoteOrientation](https://docs.byteplus.com/en/docs/12/14166#ISpatialAudio-disableremoteorientation) |
|int |[updateSelfPosition](https://docs.byteplus.com/en/docs/12/14166#ISpatialAudio-updateselfposition) |
|int |[updateRemotePosition](https://docs.byteplus.com/en/docs/12/14166#ISpatialAudio-updateremoteposition) |
|int |[removeRemotePosition](https://docs.byteplus.com/en/docs/12/14166#ISpatialAudio-removeremoteposition) |
|int |[removeAllRemotePosition](https://docs.byteplus.com/en/docs/12/14166#ISpatialAudio-removeallremoteposition) |

## Instructions

### enableSpatialAudio

```java
void com.ss.bytertc.engine.audio.ISpatialAudio.enableSpatialAudio(boolean enable)
```

Enable/disable spatial audio function.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |boolean |Whether to enable spatial audio function:<br><br><br> <br><br>* true：Enable<br><br>* false：Disable(Default setting) |

**Notes**

You need to call [updateSelfPosition](https://docs.byteplus.com/en/docs/12/14166#ISpatialAudio-updateselfposition) as well to really enjoy the spatial audio effect.

### disableRemoteOrientation

```java
void com.ss.bytertc.engine.audio.ISpatialAudio.disableRemoteOrientation()
```

Turn off the effect of the orientation of the local user as the sound source.

After the effect is off, all the other users in the room listen to the local user as if the local user is right in front of each of them.

**Notes**

* After the orientation effect as the sound source is disabled, you cannot enable it during the lifetime of the `SpatialAudio` instance.

* Calling this API does not affect the orientation effect of the local user as a listener. See [updateSelfPosition](https://docs.byteplus.com/en/docs/12/14166#ISpatialAudio-updateselfposition) and [updateRemotePosition](https://docs.byteplus.com/en/docs/12/14166#ISpatialAudio-updateremoteposition).

### updateSelfPosition

```java
int com.ss.bytertc.engine.audio.ISpatialAudio.updateSelfPosition(PositionInfo positionInfo)
```

> Available since 3.52

Sets the coordinate and orientation of the local user as a listener in the rectangular coordinate system the local user built to achieve expected spatial audio effects.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|positionInfo |PositionInfo |Information on the local user's position. Refer to [PositionInfo](https://docs.byteplus.com/en/docs/12/docs-70083#PositionInfo) for details. |

**Return Value**

* 0: Success.

* <0: Failure.

* \-2: Failure. The reason is that any two of the 3D coordinate vectors of your position are not perpendicular to each other.

**Notes**

* You need to call this API after joining the room.

* Before calling this API, you should call [enableSpatialAudio](https://docs.byteplus.com/en/docs/12/14166#ISpatialAudio-enablespatialaudio) first to enable the spatial audio function.

* The settings made locally will not influence other users' spatial audio experience.

### updateRemotePosition

```java
int com.ss.bytertc.engine.audio.ISpatialAudio.updateRemotePosition(
    String uid,
    PositionInfo positionInfo
)
```

> Available since 3.52

Sets the coordinate and orientation of the remote user as a speaker in the rectangular coordinate system of the local user. In this case, the local user hears from the remote user with the expected spatial audio effects.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|uid |String |User ID |
|positionInfo |PositionInfo |Information on the remote user's position. Refer to [PositionInfo](https://docs.byteplus.com/en/docs/12/docs-70083#PositionInfo) for details. |

**Return Value**

* 0: Success.

* <0: Failure.

* \-2: Failure. The reason is that any two of the 3D coordinate vectors of the position of the remote user are not perpendicular to each other.

**Notes**

* You must call this API after creating the room.

* The settings made locally will not influence other users' spatial audio experience.

### removeRemotePosition

```java
int com.ss.bytertc.engine.audio.ISpatialAudio.removeRemotePosition(String uid)
```

> Available since 3.52

Disables all spatial audio effects set by calling [updateRemotePosition](https://docs.byteplus.com/en/docs/12/14166#ISpatialAudio-updateremoteposition) for a certain remote user.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|uid |String |User ID of the remote user. |

**Return Value**

* 0: Success.

* <0: Failure.

### removeAllRemotePosition

```java
int com.ss.bytertc.engine.audio.ISpatialAudio.removeAllRemotePosition()
```

> Available since 3.52

Disables all spatial audio effects set by calling [updateRemotePosition](https://docs.byteplus.com/en/docs/12/14166#ISpatialAudio-updateremoteposition) for all remote users.

**Return Value**

* 0: Success.

* <0: Failure.

# IVideoDeviceManager

```java
public interface com.ss.bytertc.engine.video.IVideoDeviceManager
```

> Available since 3.56

Mainly used to enumerate and set up video capture devices

## Member Functions

|Return |Name |
|---|---|
|abstract List<VideoDeviceInfo\> |[enumerateVideoCaptureDevices](https://docs.byteplus.com/en/docs/12/14166#IVideoDeviceManager-enumeratevideocapturedevices) |
|abstract int |[setVideoCaptureDevice](https://docs.byteplus.com/en/docs/12/14166#IVideoDeviceManager-setvideocapturedevice) |

## Instructions

### enumerateVideoCaptureDevices

```java
abstract List<VideoDeviceInfo> com.ss.bytertc.engine.video.IVideoDeviceManager.enumerateVideoCaptureDevices()
```

> Available since 3.56

Get a list of video capture devices in the current system.

**Return Value**

Contains a list of all video capture devices in the system. See [VideoDeviceInfo](https://docs.byteplus.com/en/docs/12/docs-70083#VideoDeviceInfo).

### setVideoCaptureDevice

```java
abstract int com.ss.bytertc.engine.video.IVideoDeviceManager.setVideoCaptureDevice(final String deviceId)
```

> Available since 3.56

Set the current video capture device

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|deviceId |final String |Video device ID, which can be obtained through [enumerateVideoCaptureDevices](https://docs.byteplus.com/en/docs/12/14166#IVideoDeviceManager-enumeratevideocapturedevices) |

**Return Value**

* 0: Success.

   +! 0: failure

# IVideoEffect

```java
public abstract class com.ss.bytertc.engine.video.IVideoEffect
```

Advanced video effects. See [integration guide](https://docs.byteplus.com/byteplus-rtc/docs/114717).

## Member Functions

|Return |Name |
|---|---|
|abstract int |[initCVResource](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-initcvresource) |
|abstract String |[getAuthMessage](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-getauthmessage) |
|abstract int |[enableVideoEffect](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-enablevideoeffect) |
|abstract int |[disableVideoEffect](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-disablevideoeffect) |
|abstract int |[setEffectNodes](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-seteffectnodes) |
|abstract int |[updateEffectNode](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-updateeffectnode) |
|abstract int |[setColorFilter](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-setcolorfilter) |
|abstract int |[setColorFilterIntensity](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-setcolorfilterintensity) |
|abstract int |[enableVirtualBackground](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-enablevirtualbackground) |
|abstract int |[disableVirtualBackground](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-disablevirtualbackground) |
|abstract int |[enableFaceDetection](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-enablefacedetection) |
|abstract int |[disableFaceDetection](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-disablefacedetection) |

## Instructions

### initCVResource

```java
public abstract int com.ss.bytertc.engine.video.IVideoEffect.initCVResource(
    String licenseFile,
    String algoModelDir
)
```

Checks video effect license, sets the video effect resource model path, and initializes video effect.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|licenseFile |String |The absolute path of the license file for authorization. |
|algoModelDir |String |The absolute path of the Effects SDK's models file. |

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

**Notes**

When validating the license, the difference of the timestamp of the CV server and the timestamp of the client is checked. You must not change the time of the client.

### getAuthMessage

```java
public abstract String com.ss.bytertc.engine.video.IVideoEffect.getAuthMessage()
```

Get authorization messages from the Effect SDK for the online license.

**Return Value**

Authorization message string address. If getting the message fails, nullptr is returned.

**Notes**

* You must get an online license for the Effect SDK before using the CV functions.

* After getting authorization messages with this API, implement the code of getting the online license with [Online License Guide](https://docs.byteplus.com/en/effects/docs/windows-license-guide). Then call [initCVResource](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-initcvresource) to validate the license. After that, you can use the CV function.

### enableVideoEffect

```java
public abstract int com.ss.bytertc.engine.video.IVideoEffect.enableVideoEffect()
```

Enables video effects including beauty and color filters.

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

**Notes**

* You must call [initCVResource](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-initcvresource) before calling this API.

* This API does not enable video effects directly, you must call [setEffectNodes](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-seteffectnodes) or [setColorFilter](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-setcolorfilter) next.

* Call [disableVideoEffect](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-disablevideoeffect) to turn off video effects.

### disableVideoEffect

```java
public abstract int com.ss.bytertc.engine.video.IVideoEffect.disableVideoEffect()
```

Disables video effects.

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

**Notes**

Call [enableVideoEffect](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-enablevideoeffect) to enable video effects.

### setEffectNodes

```java
public abstract int com.ss.bytertc.engine.video.IVideoEffect.setEffectNodes(List<String> effectNodes)
```

Sets the video effects material package.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectNodes |List<String\> |Array of effect material package paths.<br><br> <br><br>To remove the current video effect, set it to null. |

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

**Notes**

You must call [enableVideoEffect](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-enablevideoeffect) before calling this API.

### updateEffectNode

```java
public abstract int com.ss.bytertc.engine.video.IVideoEffect.updateEffectNode(
    String effectNode,
    String key,
    float value
)
```

Sets the intensity of video effects.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectNode |String |The absolute path of the effects resource package, see [Resource Package Structure](https://docs.byteplus.com/effects/docs/resource-package-structure-v421-and-later). |
|key |String |The name of the material key to be set, see [Functions of Resource Keys](https://docs.byteplus.com/effects/docs/functions-of-resource-keys-v421-and-later) for the value. |
|value |float |The intensity value that needs to be set, the value range [0,1], and the setting is invalid when it exceeds the range. |

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

### setColorFilter

```java
public abstract int com.ss.bytertc.engine.video.IVideoEffect.setColorFilter(String filterRes)
```

Sets the color filter.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|filterRes |String |Filter effects package absolute path. |

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

**Notes**

Call [setColorFilterIntensity](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-setcolorfilterintensity) to set the intensity of the color filter enabled. Set the intensity to 0 to turn off color filter.

### setColorFilterIntensity

```java
public abstract int com.ss.bytertc.engine.video.IVideoEffect.setColorFilterIntensity(float intensity)
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

```java
public abstract int com.ss.bytertc.engine.video.IVideoEffect.enableVirtualBackground(
    String backgroundStickerRes,
    VirtualBackgroundSource source
)
```

Sets the original background to a specified image or a solid color.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|backgroundStickerRes |String |The absolute path of virtual background effects. |
|source |VirtualBackgroundSource |Virtual background source. See [VirtualBackgroundSource](https://docs.byteplus.com/en/docs/12/docs-70083#VirtualBackgroundSource). |

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

**Notes**

* You must call [initCVResource](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-initcvresource) before calling this API.

* Call [disableVirtualBackground](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-disablevirtualbackground) to turn off the virtual background.

### disableVirtualBackground

```java
public abstract int com.ss.bytertc.engine.video.IVideoEffect.disableVirtualBackground()
```

Turns off the virtual background.

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

**Notes**

After calling [enableVirtualBackground](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-enablevirtualbackground) to enable the virtual background function, you can call this API to turn it off.

### enableFaceDetection

```java
public abstract int com.ss.bytertc.engine.video.IVideoEffect.enableFaceDetection(
    IFaceDetectionObserver observer,
    int intervalMs,
    String faceModelPath
)
```

Starts face detection and registers the observer for the result.

With this observer, you will receive [onFaceDetectResult](https://docs.byteplus.com/en/docs/12/docs-70081#IFaceDetectionObserver-onfacedetectresult) periodically.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|observer |IFaceDetectionObserver |See [IFaceDetectionObserver](https://docs.byteplus.com/en/docs/12/docs-70081#IFaceDetectionObserver). |
|intervalMs |int |The minimum time interval between two callbacks in milliseconds. The value should be greater than 0. The actual time interval is between interval_ms and interval_ms+the time slot of a captured video frame. |
|faceModelPath |String |The absolute path of the face detection algorithm file. Typically it is the tt_face_vXXX.model file in the ttfacemodel folder. |

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* \-1004: Initializing. This function will be available when the initialization is completed.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

### disableFaceDetection

```java
public abstract int com.ss.bytertc.engine.video.IVideoEffect.disableFaceDetection()
```

Stops face detection.

**Return Value**

* 0: Success.

* –1000: The Effects SDK is not integrated.

* –1001: This API is unavailable for your Effects SDK.

* –1002: Your Effects SDK's version is incompatible.

* < 0: Other error. See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions.

# IRTCAudioDeviceManager

```java
public interface com.ss.bytertc.engine.IRTCAudioDeviceManager
```

IRTCAudioDeviceManager interface

## Member Functions

|Return |Name |
|---|---|
|abstract int |[startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/14166#IRTCAudioDeviceManager-startaudioplaybackdevicetest) |
|abstract int |[stopAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/14166#IRTCAudioDeviceManager-stopaudioplaybackdevicetest) |
|abstract int |[startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/14166#IRTCAudioDeviceManager-startaudiodevicerecordtest) |
|abstract int |[stopAudioDeviceRecordAndPlayTest](https://docs.byteplus.com/en/docs/12/14166#IRTCAudioDeviceManager-stopaudiodevicerecordandplaytest) |
|abstract int |[stopAudioDevicePlayTest](https://docs.byteplus.com/en/docs/12/14166#IRTCAudioDeviceManager-stopaudiodeviceplaytest) |

## Instructions

### startAudioPlaybackDeviceTest

```java
abstract int com.ss.bytertc.engine.IRTCAudioDeviceManager.startAudioPlaybackDeviceTest(
    String testAudioFilePath,
    int interval
)
```

Start the playback test for the local audio device. RTC will start playing the audio file specified. And RTC will notify the audio volume via the `onAudioPlaybackDeviceTestVolume` periodically.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|testAudioFilePath |String |Specify the path of the audio file for the playback test, including \*.mp3, \*.aac, \*.m4a, \*.3gp, and \*.wav. |
|interval |int |The time interval between each `onAudioPlaybackDeviceTestVolume` callback in milliseconds. We recommend setting it to 200 ms. The minimal value is 10 ms. |

**Return Value**

* 0: Success

* < 0: Failure

**Notes**

* You can call this API whether the user is in the room.

* Call [stopAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/14166#IRTCAudioDeviceManager-stopaudioplaybackdevicetest) to stop the playback test before moving on to the other device tests.

### stopAudioPlaybackDeviceTest

```java
abstract int com.ss.bytertc.engine.IRTCAudioDeviceManager.stopAudioPlaybackDeviceTest()
```

Stop the playback test for the local audio device.

**Return Value**

Result

* 0: Success

* < 0: Failure

**Notes**

Call this API to stop the playback test started by calling [startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/14166#IRTCAudioDeviceManager-startaudioplaybackdevicetest) before moving on to the other device tests.

### startAudioDeviceRecordTest

```java
abstract int com.ss.bytertc.engine.IRTCAudioDeviceManager.startAudioDeviceRecordTest(int interval)
```

Start the capture and playback test for local audio devices.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|interval |int |During the test, you'll receive `enableAudioPropertiesReport` periodically. Set the period in ms with this parameter. Recommended value is 200 ms; the minimal value is 10 ms. |

**Return Value**

result

* 0: success

* < 0: failure

**Notes**

* The audio capturing stops in 30s after calling this API and begins to play the recording audio. Before that, you can call [stopAudioDeviceRecordAndPlayTest](https://docs.byteplus.com/en/docs/12/14166#IRTCAudioDeviceManager-stopaudiodevicerecordandplaytest) to stop audio capturing and start playing the recording audio.

* Call [stopAudioDevicePlayTest](https://docs.byteplus.com/en/docs/12/14166#IRTCAudioDeviceManager-stopaudiodeviceplaytest) to stop the test, including capturing and playing the recording.

* You must stop the test before starting another test for audio devices.

* You must stop the test before calling `enableAudioPropertiesReport`.

* This test performs locally and does not involve network connection testing.

### stopAudioDeviceRecordAndPlayTest

```java
abstract int com.ss.bytertc.engine.IRTCAudioDeviceManager.stopAudioDeviceRecordAndPlayTest()
```

Call this API to stop recording in the test and start to play the recording in 30 s after calling [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/14166#IRTCAudioDeviceManager-startaudiodevicerecordtest).

**Return Value**

Result

* 0: Success

* < 0: Failure

**Notes**

After calling this API, the recording starts playing during which you can call [stopAudioDevicePlayTest](https://docs.byteplus.com/en/docs/12/14166#IRTCAudioDeviceManager-stopaudiodeviceplaytest) to stop playing.

### stopAudioDevicePlayTest

```java
abstract int com.ss.bytertc.engine.IRTCAudioDeviceManager.stopAudioDevicePlayTest()
```

Stop the capture and playback test for local audio devices which is started by calling [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/14166#IRTCAudioDeviceManager-startaudiodevicerecordtest).

Before the test ends by itself, you can call this API to stop the recording or playing.

**Return Value**

* 0: Success

* < 0: Failure

# RTCRoom

```java
public abstract class com.ss.bytertc.engine.RTCRoom
```

RTCRoom Class

## Member Functions

|Return |Name |
|---|---|
|abstract void |[destroy](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-destroy) |
|abstract int |[joinRoom](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-joinroom) |
|abstract int |[setRTCRoomEventHandler](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-setrtcroomeventhandler) |
|abstract int |[setUserVisibility](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-setuservisibility) |
|abstract int |[setMultiDeviceAVSync](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-setmultideviceavsync) |
|abstract int |[setRemoteSimulcastStreamType](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-setremotesimulcaststreamtype) |
|abstract int |[setLiveMode](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-setlivemode) |
|abstract int |[publishStreamVideo](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-publishstreamvideo) |
|abstract int |[publishStreamAudio](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-publishstreamaudio) |
|abstract int |[subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-subscribestreamvideo) |
|abstract int |[subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-subscribestreamaudio) |
|abstract int |[subscribeAllStreamsVideo](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-subscribeallstreamsvideo) |
|abstract int |[subscribeAllStreamsAudio](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-subscribeallstreamsaudio) |
|abstract int |[pauseAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-pauseallsubscribedstreamvideo) |
|abstract int |[pauseAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-pauseallsubscribedstreamaudio) |
|abstract int |[resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-resumeallsubscribedstreamvideo) |
|abstract int |[resumeAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-resumeallsubscribedstreamaudio) |
|abstract int |[startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-startforwardstreamtorooms) |
|abstract int |[updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-updateforwardstreamtorooms) |
|abstract int |[stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-stopforwardstreamtorooms) |
|abstract int |[pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-pauseforwardstreamtoallrooms) |
|abstract int |[resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-resumeforwardstreamtoallrooms) |
|abstract IRangeAudio |[getRangeAudio](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-getrangeaudio) |
|abstract ISpatialAudio |[getSpatialAudio](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-getspatialaudio) |
|abstract int |[setRemoteRoomAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-setremoteroomaudioplaybackvolume) |
|abstract int |[setAudioSelectionConfig](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-setaudioselectionconfig) |
|abstract long |[setRoomExtraInfo](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-setroomextrainfo) |
|abstract int |[setStreamExtraInfo](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-setstreamextrainfo) |
|abstract int |[setRemoteVideoConfig](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-setremotevideoconfig) |
|abstract String |[getRoomId](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-getroomid) |
|abstract String |[getCallId](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-getcallid) |

## Instructions

### destroy

```java
public abstract void com.ss.bytertc.engine.RTCRoom.destroy()
```

Leave and destroy the room instance created by calling [createRTCRoom](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-creatertcroom).

### joinRoom

```java
public abstract int com.ss.bytertc.engine.RTCRoom.joinRoom(
    String token,
    UserInfo userInfo,
    boolean userVisibility,
    RTCRoomConfig roomConfig
)
```

Join the RTC room.

After creating a room by calling [createRTCRoom](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-creatertcroom), call this API to join the room and make audio & video calls with other users in the room.

> Users (including backend bots) who successfully join the RTC room will start billing. If the room only has 1 user, the audio billing time will be calculated. See [Audio Billing](https://docs.byteplus.com/en/docs/12/docs-69871) for more details.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|token |String |Dynamic key. It is used for authentication and verification of users entering the room.<br><br> <br><br>You need to bring Token to enter the room. When testing, you can use the console to generate temporary tokens. For production use, use the server\-side SDK to generate and issue tokens on your server. See [Use Token to complete authentication](https://docs.byteplus.com/en/docs/12/docs-70121) for token validity and generation method.<br><br> <br><br>Apps with different AppIDs are not interoperable.<br><br> <br><br>Make sure that the AppID used to generate the Token is the same as the AppID used to create the engine, otherwise it will cause joining the room to fail. |
|userInfo |UserInfo |User information. See [UserInfo](https://docs.byteplus.com/en/docs/12/docs-70083#UserInfo). |
|userVisibility |boolean |User visibility. We recommend setting the user visibility to `false` when entering the room, and then setting it to `true` via [setUserVisibility](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-setuservisibility) when the user needs to send audio & video streams. Joining fails when the number of users in an RTC room reaches the upper limit. An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Capability of Users and Streams](https://docs.byteplus.com/en/byteplus-rtc/docs/257549). |
|roomConfig |RTCRoomConfig |Room parameter configuration, set the room mode and whether to automatically publish or subscribe to the flow. See [RTCRoomConfig](https://docs.byteplus.com/en/docs/12/docs-70083#RTCRoomConfig) for the specific configuration mode. |

**Return Value**

* 0: Success.

   * Local users receive notifications of the room state via [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged).

   * Local users receive notifications of the local\-stream state via [onVideoPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onvideopublishstatechanged), [onAudioPublishStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onaudiopublishstatechanged).

   * Local users receive notifications of the subscribed\-stream state via [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamaudio).

   * Local users receive notifications of the published\-stream state via [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamaudio).

   * Local users receive notifications of the subscribed\-stream state via [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onvideosubscribestatechanged), [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onaudiosubscribestatechanged).

   * If the local user is also a visible user, the other participants receive [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserjoined) callback.

* \-1: RoomID/userInfo.uid contains invalid parameters.

* \-2: Already in the room. After the API call is successful, as long as the return value of 0 is received and [leaveRoom](https://docs.byteplus.com/en/docs/12/14166#RTSRoom-leaveroom) is not called successfully, this return value is triggered when the room entry API is called again, regardless of whether the filled room ID and user ID are duplicated.

   The reason for the failure will be communicated via the [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged) callback.

**Notes**

* In the same room with the same App ID, the user ID of each user must be unique. If two users have the same user ID, the user who entered the room later will kick the user who entered the room out of the room, and the user who entered the room will receive the [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged) callback notification. For the error type. See kErrorCodeDuplicateLogin in [ERROR_CODE_DUPLICATE_LOGIN](https://docs.byteplus.com/en/docs/12/docs-70082#ErrorCode-error_code_duplicate_login).

* By default, the user is visible in an RTC room. Joining fails when the number of users in an RTC room reaches the upper limit. To avoid this, call [setUserVisibility](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-setuservisibility) to change the visibility of the audience users to `false` by considering the capacity for the invisible users is much larger than that for visible users. An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Capability of Users and Streams](https://docs.byteplus.com/en/byteplus-rtc/docs/257549).

* After the user successfully joins the room, the SDK may lose connection to the server in case of poor local network conditions. At this point, [onConnectionStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onconnectionstatechanged) callback will be triggered and the SDK will automatically retry until it successfully reconnects to the server. After successful reconnection, [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged) callback notification will be received locally.

### setRTCRoomEventHandler

```java
public abstract int com.ss.bytertc.engine.RTCRoom.setRTCRoomEventHandler(IRTCRoomEventHandler rtcRoomEventHandler)
```

Listens for event callbacks related to the [RTCRoom](https://docs.byteplus.com/en/docs/12/14166#RTCRoom) instance by setting the event handler of this instance.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|rtcRoomEventHandler |IRTCRoomEventHandler |Refer to [IRTCRoomEventHandler](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

### setUserVisibility

```java
public abstract int com.ss.bytertc.engine.RTCRoom.setUserVisibility(boolean enable)
```

Set the visibility of the user in the room. The local user is visible to others by default before calling this API.

An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Room Capacity](https://docs.byteplus.com/en/byteplus-rtc/docs/257549).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |boolean |Visibility of the user in the room.<br><br><br> <br><br>* true: The user can publish media streams. The other users in the room get informed of the behaviors of the user, such as joining room, starting video capture, and leaving room.<br><br>* false: The user cannot publish media streams. The other users in the room do not get informed of the behaviors of the user, such as joining room, starting video capture, or leaving room. |

**Return Value**

* 0: Success.

* < 0 : Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus).

   You will receive [onUserVisibilityChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuservisibilitychanged) after calling this API. (Available since v3.54)

* If you call this API before joining room, and the set value is different from the default value, you will receive the callback when you join the room.

* If you call this API after joining room, and the current visibility is different from the previous value, you will receive the callback.

* When reconnecting after losing internet connection, if the visibility changes, you will receive the callback.

**Notes**

* You can call this API whether the user is in a room or not.

   * When you call this API while you are in the room, the other users in the room will be informed via the following callback.

      • When you switch from `false` to `true`, they will receive [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserjoined).

• When you switch from `true` to `false`, they will receive [onUserLeave](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserleave).

• The invisible user will receive the warning code, `WARNING_CODE_PUBLISH_STREAM_FORBIDEN`, when trying to publish media streams.

### setMultiDeviceAVSync

```java
public abstract int com.ss.bytertc.engine.RTCRoom.setMultiDeviceAVSync(String audioUserId)
```

Synchronizes published audio and video.

When the same user simultaneously uses separate devices to capture and publish audio and video, there is a possibility that the streams are out of sync due to the network disparity. In this case, you can call this API on the video publisher side and the SDK will automatically line the video stream up according to the timestamp of the audio stream, ensuring that the audio the receiver hears corresponds to the video the receiver watches.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioUserId |String |The ID of audio publisher. You can stop the current A/V synchronization by setting this parameter to null. |

**Return Value**

* 0: Success. When the A/V synchronization state changes, you will receive [onAVSyncStateChange](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onavsyncstatechange).

* < 0 : Fail. You can also learn the error details via [onAVSyncEvent](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onavsyncevent). More than one pair of audio and video can be synchronized simultaneously in the same RTC room, but you should note that one single audio source cannot be synchronized with multiple video sources at the same time.

**Notes**

* You can call this API anytime before or after entering the room.

* The source user IDs of the audio and video stream to be synchronized must be in the same RTC room.

* If you want to change the audio source, call this API again with a new `audioUserId`. If you want to change the video source, you need to stop the current synchronization first, then call this API on the new video publisher side.

### setRemoteSimulcastStreamType

```java
public abstract int com.ss.bytertc.engine.RTCRoom.setRemoteSimulcastStreamType(
    String streamId,
    SimulcastStreamType streamType
)
```

> Available since 3.60.

Sets the type of the remote video stream to subscribe to.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |String |ID of the remote video stream you expect to subscribe to. |
|streamType |SimulcastStreamType |Video stream type, see [SimulcastStreamType](https://docs.byteplus.com/en/docs/12/docs-70083#SimulcastStreamType). |

**Return Value**

API call result:

* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for specific reasons.

**Notes**

* This API only works after the publisher calls [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setlocalsimulcastmode) to enable publishing multiple\-quality video streams, in which case the subscriber will receive the stream from the publisher that is closest to the set configuration; otherwise the subscriber will only receive one video stream with a resolution of 640px × 360px and a frame rate of 15fps.

* If you don't call this API after the publisher enables the function of publishing multiple streams, you will receive by default the video stream with the largest resolution set by the publisher.

* This API only affects camera video streams published by remote users.

### setLiveMode

```java
public abstract int com.ss.bytertc.engine.RTCRoom.setLiveMode(LiveMode liveMode)
```

> Available since 3.60.

Sets live mode.

Call this method after joining a room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|liveMode |LiveMode |Live mode. See [LiveMode](https://docs.byteplus.com/en/docs/12/docs-70083#LiveMode) for details. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

### publishStreamVideo

```java
public abstract int com.ss.bytertc.engine.RTCRoom.publishStreamVideo(boolean publish)
```

> Available since 3.60. Since version 3.60, this interface replaces the `publishStream`, `unpublishStream`, `publishScreen` and `unpublishScreen` methods for the following functions. If you have upgraded to version 3.60 or above and are still using these two methods, please migrate to this interface.

Publishes or stops publishing video streams.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|publish |boolean |Whether to publish the video stream.<br><br><br> <br><br>* `true`: Publish.<br><br>* `false`: Stop publishing. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* You don't need to call this API if you set it to Auto\-publish when calling [joinRoom](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-joinroom).

* An invisible user cannot publish media streams. Call [setUserVisibility](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-setuservisibility) to change your visibility in the room.

* Call [publishStreamAudio](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-publishstreamaudio) to start or stop publishing the audio stream captured by the microphone.

* Call [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-startforwardstreamtorooms) to forward the published streams to the other rooms.

* After you call this API, the other users in the room will receive [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo). Those who successfully received your streams will receive [onFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onfirstremotevideoframedecoded) at the same time.

### publishStreamAudio

```java
public abstract int com.ss.bytertc.engine.RTCRoom.publishStreamAudio(boolean publish)
```

> Available since 3.60. Since version 3.60, this interface replaces the `publishStream`, `unpublishStream`, `publishScreen` and `unpublishScreen` methods for the following functions. If you have upgraded to version 3.60 or above and are still using these two methods, please migrate to this interface.

Publishes or stops publishing audio streams in the current room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|publish |boolean |Whether to publish the audio stream.<br><br><br> <br><br>* `true`: Publish.<br><br>* `false`: Stop publishing. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* You don't need to call this API if you set it to Auto\-publish when calling [joinRoom](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-joinroom).

* An invisible user cannot publish media streams. Call [setUserVisibility](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-setuservisibility) to change your visibility in the room.

* Call [publishStreamVideo](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-publishstreamvideo) to start or stop publishing the video stream captured by the camera.

* Call [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-startforwardstreamtorooms) to forward the published streams to the other rooms.

* After you call this API, the other users in the room will receive [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamaudio). Those who successfully received your streams will receive [onFirstRemoteAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onfirstremoteaudioframe) at the same time.

### subscribeStreamVideo

```java
public abstract int com.ss.bytertc.engine.RTCRoom.subscribeStreamVideo(
    String streamId,
    boolean subscribe
)
```

> Available since 3.60. Since version 3.60, this interface replaces the `subscribeStream`, `unsubscribeStream`, `subscribeScreen` and `unsubscribeScreen` methods for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.

Subscribes to or unsubscribes from the specific remote video streams captured by the camera.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |String |The ID of the target remote video stream. |
|subscribe |boolean |Whether to subscribe to the video stream.<br><br><br> <br><br>* `true`: Subscribe.<br><br>* `false`: Unsubscribe. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* If you have already subscribed to the remote stream (manually or automatically) when you call this method, the subscription configuration will be updated based on the parameters passed in this call.

* You must call [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo) callback to get the current remote camera stream information in the room, and then call this method to subscribe to the remote media streams.

* After you call this method, you will receive [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onvideosubscribestatechanged) notification method call results.

* After you successfully subscribe to the remote video stream, the subscription relationship will continue until you call [subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-subscribestreamvideo) to unsubscribe from it or the local user leaves the room.

* Any other exceptions will be included in [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onvideosubscribestatechanged) callback notification.

### subscribeStreamAudio

```java
public abstract int com.ss.bytertc.engine.RTCRoom.subscribeStreamAudio(
    String streamId,
    boolean subscribe
)
```

> Available since 3.60. Since version 3.60, this interface replaces the `subscribeStream`, `unsubscribeStream`, `subscribeScreen` and `unsubscribeScreen` methods for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.

Subscribes to or unsubscribes from the specific remote audio streams captured by the microphone.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |String |The ID of the target remote audio stream. |
|subscribe |boolean |Whether to subscribe to the audio stream.<br><br><br> <br><br>* `true`: Subscribe.<br><br>* `false`: Unsubscribe. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* If you have already subscribed to the remote audio stream (manually or automatically) when you call this method, the subscription configuration will be updated based on the parameters passed in this call.

* You must call [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamaudio) callback to get the current remote microphone stream information in the room, and then call this method to subscribe to the remote media streams.

* After you call this method, you will receive [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onaudiosubscribestatechanged) notification method call results.

* After you successfully subscribe to the remote audio stream, the subscription relationship will continue until you call [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-subscribestreamaudio) to unsubscribe from it or the local user leaves the room.

* Any other exceptions will be included in [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onaudiosubscribestatechanged) callback notification.

### subscribeAllStreamsVideo

```java
public abstract int com.ss.bytertc.engine.RTCRoom.subscribeAllStreamsVideo(boolean subscribe)
```

> Available since 3.60. Since version 3.60, this interface replaces the `subscribeAllStreams` and `unsubscribeAllStreams` methods for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.

Subscribes to or unsubscribes from all remote video streams (by the camera).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|subscribe |boolean |Whether to subscribe to all remote video streams.<br><br><br> <br><br>* `true`: Subscribe.<br><br>* `false`: Unsubscribe. |

**Return Value**

API call result:

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* If the subscription options conflict with the previous ones, they are subject to the configurations in the last call.

* With the Audio selection enabled, if the number of media streams exceeds the limit, we recommend that you subscribe to each target media stream with the following APIs: [subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-subscribestreamvideo), [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-subscribestreamaudio).

* After calling this API, you will be informed of the calling result with [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onvideosubscribestatechanged), [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onaudiosubscribestatechanged). You can also find exception causes from the callbacks above.

* Once the local user subscribes to the stream of a remote user, the subscription to the remote user will continue until the local user leaves the room or unsubscribes from it by calling [subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-subscribestreamvideo), [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-subscribestreamaudio).

### subscribeAllStreamsAudio

```java
public abstract int com.ss.bytertc.engine.RTCRoom.subscribeAllStreamsAudio(boolean subscribe)
```

> Available since 3.60. Since version 3.60, this interface replaces the `subscribeAllStreams` and `unsubscribeAllStreams` methods for the below functions. If you have upgraded to version 3.60 or later and are still using these methods, please migrate to this interface.

Subscribes to or unsubscribes from all remote audio streams.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|subscribe |boolean |Whether to subscribe to all remote audio streams:<br><br><br> <br><br>* `true`: Subscribe.<br><br>* `false`: Unsubscribe. |

**Return Value**

API call result:

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* If the subscription options conflict with the previous ones, they are subject to the configurations in the last call.

* With the Audio selection enabled, if the number of media streams exceeds the limit, we recommend that you subscribe to each target media stream with the following APIs: [subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-subscribestreamvideo), [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-subscribestreamaudio).

* After calling this API, you will be informed of the calling result with [onVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onvideosubscribestatechanged), [onAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onaudiosubscribestatechanged). You can also find exception causes from the callbacks above.

* Once the local user subscribes to the stream of a remote user, the subscription to the remote user will continue until the local user leaves the room or unsubscribes from it by calling [subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-subscribestreamvideo), [subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-subscribestreamaudio).

### pauseAllSubscribedStreamVideo

```java
public abstract int com.ss.bytertc.engine.RTCRoom.pauseAllSubscribedStreamVideo()
```

> Available since 3.60. Since version 3.60, this interface replaces the `pauseAllSubscribedStream` method for the below functions. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this interface.

Pauses receiving all remote video streams.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* Calling this API does not change the capture state and the transmission state of the remote clients.

* Calling this API does not cancel the subscription or change any subscription configuration.

* To resume, call [resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-resumeallsubscribedstreamvideo).

* In a multi\-room scenario, this API only pauses the reception of streams published in the current room.

### pauseAllSubscribedStreamAudio

```java
public abstract int com.ss.bytertc.engine.RTCRoom.pauseAllSubscribedStreamAudio()
```

> Available since 3.60. Since version 3.60, this interface replaces the `pauseAllSubscribedStream` method for the below functions. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this interface.

Pauses receiving all remote audio streams.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* Calling this API does not change the capture state and the transmission state of the remote clients.

* Calling this API does not cancel the subscription or change any subscription configuration.

* To resume, call [resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-resumeallsubscribedstreamvideo).

* In a multi\-room scenario, this API only pauses the reception of streams published in the current room.

### resumeAllSubscribedStreamVideo

```java
public abstract int com.ss.bytertc.engine.RTCRoom.resumeAllSubscribedStreamVideo()
```

> Available since 3.60. Since version 3.60, this interface replaces the `resumeAllSubscribedStream` method for the below functions. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this interface.

Resumes receiving all remote video streams.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* Calling this API does not change the capture state and the transmission state of the remote clients.

* Calling this API does not change any subscription configuration.

### resumeAllSubscribedStreamAudio

```java
public abstract int com.ss.bytertc.engine.RTCRoom.resumeAllSubscribedStreamAudio()
```

> Available since 3.60. Since version 3.60, this interface replaces the `resumeAllSubscribedStream` method for the below functions. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this interface.

Resumes receiving all remote audio streams.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* Calling this API does not change the capture state and the transmission state of the remote clients.

* Calling this API does not change any subscription configuration.

### startForwardStreamToRooms

```java
public abstract int com.ss.bytertc.engine.RTCRoom.startForwardStreamToRooms(List<ForwardStreamInfo> forwardStreamInfos)
```

Start relaying media stream across rooms.

After calling [joinRoom](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-joinroom), you can call this method to publish the media stream to multiple rooms that applies to scenarios such as an online talent contest and so on.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|forwardStreamInfos |List<ForwardStreamInfo\> |Information of the rooms where you want to relay the media stream to. Refer to [ForwardStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#ForwardStreamInfo) for more information. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* Call this method will trigger [onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onforwardstreamstatechanged).

* After calling this method, listen to the events from each room during the relaying by registering [onForwardStreamEvent](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onforwardstreamevent).

* Once the relaying begins, the other users in the room will receive callback of [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserjoined), [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamaudio).

* Call [updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-updateforwardstreamtorooms) to add or remove the designated room(s) after calling this method.

* Call [stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-stopforwardstreamtorooms) to stop relaying to all rooms after calling this method.

* Call [pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-pauseforwardstreamtoallrooms) to pause relaying to all rooms after calling this method.

### updateForwardStreamToRooms

```java
public abstract int com.ss.bytertc.engine.RTCRoom.updateForwardStreamToRooms(List<ForwardStreamInfo> forwardStreamInfos)
```

Update information of the rooms where you want to relay the media stream to after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-startforwardstreamtorooms).

Adding and removing rooms by calling this method will trigger [onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onforwardstreamstatechanged) on the local.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|forwardStreamInfos |List<ForwardStreamInfo\> |Information of the rooms where you want to relay the media stream to. Refer to [ForwardStreamInfo](https://docs.byteplus.com/en/docs/12/docs-70083#ForwardStreamInfo) for more information. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

Users in the room which is added or removed from the target list by calling this method will receive [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserjoined), [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamaudio).

### stopForwardStreamToRooms

```java
public abstract int com.ss.bytertc.engine.RTCRoom.stopForwardStreamToRooms()
```

Call this method to stop relaying media stream to all rooms after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-startforwardstreamtorooms).

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* Call this method will trigger [onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onforwardstreamstatechanged).

* The other users in the room will receive callback of [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserjoined), [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamaudio) when you stop relaying.

* To stop relaying media stream to specific rooms, call [updateForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-updateforwardstreamtorooms) instead.

* To resume the relaying in a short time, call [pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-pauseforwardstreamtoallrooms) instead and then call [resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-resumeforwardstreamtoallrooms) to resume after that.

### pauseForwardStreamToAllRooms

```java
public abstract int com.ss.bytertc.engine.RTCRoom.pauseForwardStreamToAllRooms()
```

Call this method to pause relaying media stream to all rooms after calling [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-startforwardstreamtorooms).

After that, call [resumeForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-resumeforwardstreamtoallrooms) to resume.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

The other users in the room will receive callback of [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserjoined), [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamaudio) when you stop relaying.

### resumeForwardStreamToAllRooms

```java
public abstract int com.ss.bytertc.engine.RTCRoom.resumeForwardStreamToAllRooms()
```

Call this method to resume relaying to all rooms from the pause by calling [pauseForwardStreamToAllRooms](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-pauseforwardstreamtoallrooms).

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

The other users in the room will receive callback of [onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserjoined) and [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo), [onUserPublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamaudio) when you resume relaying.

### getRangeAudio

```java
public abstract IRangeAudio com.ss.bytertc.engine.RTCRoom.getRangeAudio()
```

Gets range audio instance.

**Return Value**

API call result:

* IRangeAudio: Success. You will get an [IRangeAudio](https://docs.byteplus.com/en/docs/12/14166#IRangeAudio) returned from the SDK.

* null: Failure. The current SDK does not offer range audio function.

**Notes**

This API must be called for the first time between creating a room and actually entering it. Refer to [Range Voice](https://docs.byteplus.com/byteplus-rtc/docs/114727) for more information.

### getSpatialAudio

```java
public abstract ISpatialAudio com.ss.bytertc.engine.RTCRoom.getSpatialAudio()
```

Get location audio interface instances.

**Return Value**

Spatial audio management interface instance. If NULL is returned, spatial audio is not supported. See [ISpatialAudio](https://docs.byteplus.com/en/docs/12/14166#ISpatialAudio).

**Notes**

* This API must be called for the first time between creating a room and actually entering it. Refer to [Spatial Audio](https://docs.byteplus.com/byteplus-rtc/docs/93903) for more information.

* The spatial audio effect can only be turned on when using a device that supports true two\-channel playback;

* In the case of poor network conditions, even if this function is turned on, the spatial audio effect will not be generated;

* Insufficient performance of the model may cause audio stuttering. When using a low\-end machine, it is not recommended to turn on the spatial audio effect;

* Spatial audio effects do not take effect when server level routing is enabled.

### setRemoteRoomAudioPlaybackVolume

```java
public abstract int com.ss.bytertc.engine.RTCRoom.setRemoteRoomAudioPlaybackVolume(int volume)
```

Adjusts the audio playback volume from all the remote users in a room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |int |Ratio(%) of playback volume to original volume, in the range [0, 400], with overflow protection.<br><br> <br><br>To ensure the audio quality, we recommend setting the volume to `100`.<br><br><br> <br><br>* 0: mute<br><br>* 100: original volume. Default value.<br><br>* 400: Up to 4 times the original volume (with overflow protection) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

Suppose a remote user A is always within the range of the target user whose playback volume will be adjusted,

* If you use both this method and [setRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setremoteaudioplaybackvolume), the volume that the local user hears from user A is the volume set by the method called later.

* If you use both this method and [setPlaybackVolume](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setplaybackvolume), the volume that the local user hears from user A is the overlay of both settings.

### setAudioSelectionConfig

```java
public abstract int com.ss.bytertc.engine.RTCRoom.setAudioSelectionConfig(AudioSelectionPriority audioSelectionPriority)
```

> Available since 3.52

Set the priority of the local audio stream to be published.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioSelectionPriority |AudioSelectionPriority |The priority of the local audio stream which defaults to be subscribable only up to the result of the Audio Selection. Refer to [AudioSelectionPriority](https://docs.byteplus.com/en/docs/12/docs-70083#AudioSelectionPriority). |

**Notes**

You must enable Audio Selection in the RTC console before using this API. You can call this API whether the user has joined a room. Refer to [Audio Selection](https://docs.byteplus.com/byteplus-rtc/docs/113547).

The setting is independent in each room that the user joins.

### setRoomExtraInfo

```java
public abstract long com.ss.bytertc.engine.RTCRoom.setRoomExtraInfo(
    String key,
    String value
)
```

> Available since 3.52

Sets extra information about the RTC room the local user joins.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|key |String |Key of the extra information, less than 10 bytes in length.<br><br> <br><br>A maximum of 5 keys can exist in the same room, beyond which the first key will be replaced. |
|value |String |Content of the extra information, less than 128 bytes in length. |

**Return Value**

API call result:

* 0: Success with a taskId returned.

* <0: Failure. See [SetRoomExtraInfoResult](https://docs.byteplus.com/en/docs/12/docs-70083#SetRoomExtraInfoResult) for the reasons.

**Notes**

* Call [joinRoom](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-joinroom) first before you call this API to set extra information.

* After calling this API, you will receive [onSetRoomExtraInfoResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onsetroomextrainforesult) callback informing you the result of the setting.

* After the extra information is successfully set, other users in the same room will receive the information through [onRoomExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomextrainfoupdate) callback.

* Users who join the room later will be notified of all extra information in the room set prior to entering.

### setStreamExtraInfo

```java
public abstract int com.ss.bytertc.engine.RTCRoom.setStreamExtraInfo(String extra_info)
```

Sets extra information about the stream the local user publishes.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|extra_info |String |Extra information of the stream. The length does not exceed 1024 bytes. |

**Return Value**

* 0: Success.

* < 0: Failure.

**Notes**

* You can use this function to set extra information about the stream the local user publishes. Stream extra information is additional information attached to the stream ID. Unlike the stream ID, the stream extra information can be modified during the publishing of the corresponding stream ID. Developers can use the stream extra information to synchronize the content of the stream ID with the corresponding stream ID.

* You can call this API before or after you call [joinRoom](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-joinroom).

* Other users in the same room will receive the notification through [onRoomStreamExtraInfoUpdate](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstreamextrainfoupdate).

### setRemoteVideoConfig

```java
public abstract int com.ss.bytertc.engine.RTCRoom.setRemoteVideoConfig(
    String streamId,
    RemoteVideoConfig remoteVideoConfig
)
```

Sets your expected configuration of the remote video stream that you want to subscribe to or have subscribed to.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |String |ID of the remote video stream publisher you expect to configure subscription parameters for. |
|remoteVideoConfig |RemoteVideoConfig |The parameters you expect to configure for the remote video stream, see [RemoteVideoConfig](https://docs.byteplus.com/en/docs/12/docs-70083#RemoteVideoConfig). |

**Return Value**

API call result:

* 0: Success.

* !0: Failure.

**Notes**

* This API only works after the publisher calls [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setlocalsimulcastmode) to enable sending multiple video streams, in which case the subscriber will receive the stream from the publisher that is closest to the set configuration; otherwise the subscriber will only receive one video stream with a resolution of 640px × 360px and a frame rate of 15fps.

* If you don't call this API after the publisher enables the function of publishing multiple streams, you will receive by default the video stream with the largest resolution set by the publisher.

* You should call this API in the room.

* The SDK will automatically select the stream to be published or subscribed to based on the settings of both sides.

### getRoomId

```java
public abstract String com.ss.bytertc.engine.RTCRoom.getRoomId()
```

> Available since 3.53

Get RTC room ID.

**Return Value**

Room ID.

### getCallId

```java
public abstract String com.ss.bytertc.engine.RTCRoom.getCallId()
```

> Available since 3.60.

Gets call ID.

Call this method after joining an RTC room. After creating a room, a call ID is generated to identify the call for this room.

**Return Value**

Call ID.

# IWTNStream

```java
public interface com.ss.bytertc.engine.IWTNStream
```

WTN stream process

## Member Functions

|Return |Name |
|---|---|
|abstract int |[subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/14166#IWTNStream-subscribewtnvideostream) |
|abstract int |[subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/14166#IWTNStream-subscribewtnaudiostream) |
|abstract int |[setWTNRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/14166#IWTNStream-setwtnremotevideocanvas) |
|abstract int |[setWTNRemoteVideoSink](https://docs.byteplus.com/en/docs/12/14166#IWTNStream-setwtnremotevideosink) |
|abstract int |[setWTNRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/14166#IWTNStream-setwtnremoteaudioplaybackvolume) |
|abstract int |[setWTNStreamEventHandler](https://docs.byteplus.com/en/docs/12/14166#IWTNStream-setwtnstreameventhandler) |

## Instructions

### subscribeWTNVideoStream

```java
abstract int com.ss.bytertc.engine.IWTNStream.subscribeWTNVideoStream(
    String streamId,
    boolean subscribe
)
```

> Available since 3.60. Since version 3.60, this interface replaces the `startPlayPublicStream` and `stopPlayPublicStream` methods for subscribing to and unsubscribing from WTN video streams. If you are using these methods, please migrate to this interface.

Subscribe/ unsubscribe WTN video stream

A user can call this method to subscribe or unsubscribe to a WTN stream whether he/she has joined the room or not.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |String |ID of the WTN stream. If the stream has not been published then, the local client will receive the WTN stream once it starts publishing. |
|subscribe |boolean |Whether to subscribe to the WTN stream.<br><br><br> <br><br>* true: Subscribe<br><br>* false: Unsubscribe |

**Return Value**

* 0: Success. You will also be informed by [onWTNVideoSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IWTNStreamEventHandler-onwtnvideosubscribestatechanged).

* !0: Failure because of invalid parameter or empty parameters.

**Notes**

* A client can play up to 5 WTN streams simultaneously. Please call [subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/14166#IWTNStream-subscribewtnvideostream)/[subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/14166#IWTNStream-subscribewtnaudiostream) in time to cancel the subscription to WTN streams to avoid exceeding the limit of subscribed WTN streams.

* We recommend to bind a view for the WTN stream before calling this API to subscribe to a WTN stream.

   \- Internal renderer: By calling [setWTNRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/14166#IWTNStream-setwtnremotevideocanvas) or

   \- Custom renderer: By calling [setWTNRemoteVideoSink](https://docs.byteplus.com/en/docs/12/14166#IWTNStream-setwtnremotevideosink)

* After calling this API, you will be informed once the first frame has been decoded successfully by [onWTNFirstRemoteVideoFrameDecoded](https://docs.byteplus.com/en/docs/12/docs-70081#IWTNStreamEventHandler-onwtnfirstremotevideoframedecoded).

* If the WTN stream contains SEI information, you will be informed by [oonWTNSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IWTNStreamEventHandler-onwtnseimessagereceived).

### subscribeWTNAudioStream

```java
abstract int com.ss.bytertc.engine.IWTNStream.subscribeWTNAudioStream(
    String streamId,
    boolean subscribe
)
```

> Available since 3.60. Since version 3.60, this interface replaces the `startPlayPublicStream` and `stopPlayPublicStream` methods for subscribing to and unsubscribing from WTN audio streams. If you are using these methods, please migrate to this interface.

Subscribe/unsubscribe the WTN audio stream

A user can call this method to subscribe to a WTN stream whether he/she has joined the room or not.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |String |ID of the WTN stream. If the stream has not been published then, the local client will receive the WTN stream once it starts publishing. |
|subscribe |boolean |Whether to subscribe to the WTN stream.<br><br><br> <br><br>* true: Subscribe<br><br>* false: Unsubscribe |

**Return Value**

* 0: Success. You will also be informed by [onWTNAudioSubscribeStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IWTNStreamEventHandler-onwtnaudiosubscribestatechanged).

* !0: Failure because of invalid parameter or empty parameters.

**Notes**

* A client can play up to 5 WTN streams simultaneously. Please call [subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/12/14166#IWTNStream-subscribewtnvideostream)/[subscribeWTNAudioStream](https://docs.byteplus.com/en/docs/12/14166#IWTNStream-subscribewtnaudiostream) in time to cancel the subscription to WTN streams to avoid exceeding the limit of subscribed WTN streams.

* We recommend to bind a view for the WTN stream before calling this API to subscribe to a WTN stream.

   \- Internal renderer: By calling [setWTNRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/14166#IWTNStream-setwtnremotevideocanvas) or

   \- Custom renderer: By calling [setWTNRemoteVideoSink](https://docs.byteplus.com/en/docs/12/14166#IWTNStream-setwtnremotevideosink)

* After calling this API, you will be informed once the first frame has been decoded successfully by [onWTNFirstRemoteAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IWTNStreamEventHandler-onwtnfirstremoteaudioframe).

* If the WTN stream contains SEI information, you will be informed by [onWTNSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IWTNStreamEventHandler-onwtnseimessagereceived).

### setWTNRemoteVideoCanvas

```java
abstract int com.ss.bytertc.engine.IWTNStream.setWTNRemoteVideoCanvas(
    String streamId,
    VideoCanvas canvas
)
```

> Available since 3.60. Since version 3.60, this interface replaces `setPublicStreamVideoCanvas` for the following function. If you have upgraded to version 3.60 or above and are still using this method, please migrate to this interface.

Assign an internal render view to the WTN stream

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |String |ID of the WTN stream |
|canvas |VideoCanvas |Internal render view. If you want to unbind the video, set `videoCanvas` to null. Refer to [VideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70083#VideoCanvas) for more details. |

**Return Value**

* 0: Success

* !0: Failure

### setWTNRemoteVideoSink

```java
abstract int com.ss.bytertc.engine.IWTNStream.setWTNRemoteVideoSink(
    String streamId,
    IVideoSink videoSink,
    RemoteVideoSinkConfig config
)
```

> Available since 3.60.

Assign a custom renderer to the WTN stream. See [Custom Video Rendering](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-81201)

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |String |ID of the WTN stream |
|videoSink |IVideoSink |Custom renderer. Set to be `null` when you want to release the renderer. Refer to [IVideoSink](https://docs.byteplus.com/en/docs/12/docs-70083#IVideoSink) for more details. |
|config |RemoteVideoSinkConfig |Remote video frame callback configuration. Refer to [RemoteVideoSinkConfig](https://docs.byteplus.com/en/docs/12/docs-70083#RemoteVideoSinkConfig) for more details. |

**Return Value**

* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for specific reasons.

### setWTNRemoteAudioPlaybackVolume

```java
abstract int com.ss.bytertc.engine.IWTNStream.setWTNRemoteAudioPlaybackVolume(
    String streamId,
    int volume
)
```

> Available since 3.60. Since version 3.60, this interface replaces `setPublicStreamAudioPlaybackVolume` for the following function. If you have upgraded to version 3.60 or above and are still using this method, please migrate to this interface.

Set the audio playback volume of the WTN stream.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |String |ID of the WTN stream. |
|volume |int |Ratio(%) of the audio playback volume to the original volume, in the range `[0, 400]`, with overflow protection. The default volume is 100.<br><br> <br><br>To ensure the audio quality, the recommended range is `[0, 100]`. |

**Return Value**

* 0: Success.

* \-2: Wrong parameter.

### setWTNStreamEventHandler

```java
abstract int com.ss.bytertc.engine.IWTNStream.setWTNStreamEventHandler(IWTNStreamEventHandler handler)
```

> Available since 3.60.

Set the WTN event handler.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|handler |IWTNStreamEventHandler |See [IWTNStreamEventHandler](https://docs.byteplus.com/en/docs/12/docs-70081#IWTNStreamEventHandler). |

# IVideoProcessor

```java
public abstract class com.ss.bytertc.engine.video.IVideoProcessor
```

video processing

## Member Functions

|Return |Name |
|---|---|
|abstract IVideoFrame |[processVideoFrame](https://docs.byteplus.com/en/docs/12/14166#IVideoProcessor-processvideoframe) |

## Instructions

### processVideoFrame

```java
public abstract IVideoFrame com.ss.bytertc.engine.video.IVideoProcessor.processVideoFrame(IVideoFrame frame)
```

Get RTC SDK acquired video frame, according to the video pre\-processor [registerLocalVideoProcessor](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-registerlocalvideoprocessor) set, video pre\-processing, the final processed video frame to the RTC SDK for encoding transmission.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|frame |IVideoFrame |RTC SDK captured video frames. See [IVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70083#IVideoFrame). |

**Return Value**

The video frame after video preprocessing is returned to the RTC SDK for encoding and transmission. See [IVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70083#IVideoFrame).

**Notes**

* Before video preprocessing, you need to call [registerLocalVideoProcessor](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-registerlocalvideoprocessor) to set up the video preprocessor.

* If you need to cancel the video preprocessing, you can set the video preprocessor to nullptr.

# RTSRoom

```java
public abstract class com.ss.bytertc.engine.RTSRoom
```

RTSRoom Class

## Member Functions

|Return |Name |
|---|---|
|abstract void |[destroy](https://docs.byteplus.com/en/docs/12/14166#RTSRoom-destroy) |
|abstract int |[joinRTSRoom](https://docs.byteplus.com/en/docs/12/14166#RTSRoom-joinrtsroom) |
|abstract int |[updateToken](https://docs.byteplus.com/en/docs/12/14166#RTSRoom-updatetoken) |
|abstract int |[leaveRoom](https://docs.byteplus.com/en/docs/12/14166#RTSRoom-leaveroom) |
|abstract int |[setRTSRoomEventHandler](https://docs.byteplus.com/en/docs/12/14166#RTSRoom-setrtsroomeventhandler) |
|abstract long |[sendUserMessage](https://docs.byteplus.com/en/docs/12/14166#RTSRoom-sendusermessage) |
|abstract long |[sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/14166#RTSRoom-senduserbinarymessage) |
|abstract long |[sendRoomMessage](https://docs.byteplus.com/en/docs/12/14166#RTSRoom-sendroommessage) |
|abstract long |[sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/14166#RTSRoom-sendroombinarymessage) |

## Instructions

### destroy

```java
public abstract void com.ss.bytertc.engine.RTSRoom.destroy()
```

Leave and destroy the room instance created by calling [createRTSRoom](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-creatertsroom).

### joinRTSRoom

```java
public abstract int com.ss.bytertc.engine.RTSRoom.joinRTSRoom(
    String token,
    UserInfo userInfo
)
```

Joins the RTS room.

After creating a room by calling [createRTSRoom](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-creatertsroom), call this API to join the room and make audio & video calls with other users in the room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|token |String |Dynamic key. It is used for authentication and verification of users entering the room.<br><br> <br><br>You need to bring Token to enter the room. When testing, you can use the console to generate temporary tokens. For production use, use the server\-side SDK to generate and issue tokens on your server. See [Use Token to complete authentication](https://docs.byteplus.com/en/docs/12/docs-70121) for token validity and generation method.<br><br> <br><br>Apps with different AppIDs are not interoperable.<br><br> <br><br>Make sure that the AppID used to generate the Token is the same as the AppID used to create the engine, otherwise it will cause joining the room to fail. |
|userInfo |UserInfo |User information. See [UserInfo](https://docs.byteplus.com/en/docs/12/docs-70083#UserInfo). |

**Return Value**

* 0: Success.

   * Local users receive notifications of the room state via [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onroomstatechanged).

* \-1: RoomID/userInfo.uid contains invalid parameters.

* \-2: Already in the room. After the API call is successful, as long as the return value of 0 is received and [leaveRoom](https://docs.byteplus.com/en/docs/12/14166#RTSRoom-leaveroom) is not called successfully, this return value is triggered when the room entry API is called again, regardless of whether the filled room ID and user ID are duplicated.

   The reason for the failure will be communicated via the [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onroomstatechanged) callback.

**Notes**

* In the same room with the same App ID, the user ID of each user must be unique. If two users have the same user ID, the user who entered the room later will kick the user who entered the room out of the room, and the user who entered the room will receive the [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onroomstatechanged) callback notification. For the error type. See kErrorCodeDuplicateLogin in [ERROR_CODE_DUPLICATE_LOGIN](https://docs.byteplus.com/en/docs/12/docs-70082#ErrorCode-error_code_duplicate_login).

* After the user successfully joins the room, the SDK may lose connection to the server in case of poor local network conditions. At this point, [onConnectionStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onconnectionstatechanged) callback will be triggered and the SDK will automatically retry until it successfully reconnects to the server. After successful reconnection, [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onroomstatechanged) callback notification will be received locally.

### updateToken

```java
public abstract int com.ss.bytertc.engine.RTSRoom.updateToken(String token)
```

Updates the room token.

You must call this API to update token to ensure the RTC call continues when you receive [onTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-ontokenwillexpire), [onPublishPrivilegeTokenWillExpire](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onpublishprivilegetokenwillexpire), or .

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|token |String |Valid token.<br><br> <br><br>If the Token is invalid, you will receive [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onroomstatechanged) with the error code of `-1010`. |

**Return Value**

API call result:

* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for specific reasons.

**Notes**

* Do not call both [updateToken](https://docs.byteplus.com/en/docs/12/14166#RTSRoom-updatetoken) and [joinRTSRoom](https://docs.byteplus.com/en/docs/12/14166#RTSRoom-joinrtsroom) to update the Token. If you fail to join the room or have been removed from the room due to an expired or invalid Token, call [joinRTSRoom](https://docs.byteplus.com/en/docs/12/14166#RTSRoom-joinrtsroom) with a valid token to rejoin the room.

### leaveRoom

```java
public abstract int com.ss.bytertc.engine.RTSRoom.leaveRoom()
```

Leave the RTS room.

The user calls this method to leave the room, end the call process, and release all call\-related resources.

**Return Value**

* 0: Success. If the user is a host:

   * The other participants receive [onUserLeave](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onuserleave) callback.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* After a user who calls [setUserVisibility](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-setuservisibility) to make himself visible leaves the room, other users in the room will receive a callback notification from [onUserLeave](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onuserleave).

* This method is an asynchronous operation, and the call returns without actually exiting the room. After you actually exit the room, you will receive a callback notification from [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onroomstatechanged) locally. If the engine is destroyed immediately after this method is called, the SDK will not be able to trigger the [onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onroomstatechanged) callback.

### setRTSRoomEventHandler

```java
public abstract int com.ss.bytertc.engine.RTSRoom.setRTSRoomEventHandler(IRTSRoomEventHandler rtcRoomEventHandler)
```

Listens for event callbacks related to the [RTCRoom](https://docs.byteplus.com/en/docs/12/14166#RTCRoom) instance by setting the event handler of this instance.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|rtcRoomEventHandler |IRTSRoomEventHandler |Refer to [IRTSRoomEventHandler](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

### sendUserMessage

```java
public abstract long com.ss.bytertc.engine.RTSRoom.sendUserMessage(
    String userId,
    String messageStr,
    MessageConfig config
)
```

Send a point\-to\-point text message to the specified user in the room

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|userId |String |User ID of the message receiver |
|messageStr |String |Text message content sent. The default size of a single message package is 1 KB. For larger message transmission (up to 64 KB), you need to [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode). **Note**: If you enable Advanced RTS functions while the SDK is running, you must re\-initialize the engine for the configuration to take effect. |
|config |MessageConfig |See [MessageConfig](https://docs.byteplus.com/en/docs/12/docs-70083#MessageConfig). |

**Return Value**

* \> 0: Sent successfully, return the number of the sent message, increment from 1

* \-1: Sent failed, RTCRoom instance not created

* \-2: Sent failed, uid is empty

**Notes**

* Before sending an in\-room text message, you must call [joinRTSRoom](https://docs.byteplus.com/en/docs/12/14166#RTSRoom-joinrtsroom) to join the room.

* After the call, you will receive an [onUserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onusermessagesendresult) callback to notify that the message was sent successfully or failed;

* If the message was sent successfully, the user specified by the userId will receive an [onUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onusermessagereceived) callback.

### sendUserBinaryMessage

```java
public abstract long com.ss.bytertc.engine.RTSRoom.sendUserBinaryMessage(
    String userId,
    byte[] buffer,
    MessageConfig config
)
```

Sends a point\-to\-point binary message to the specified user in the room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|userId |String |User ID of the message receiver |
|buffer |byte[] |Binary message content sent. The default size of a single message package is 1 KB. For larger message transmission (up to 64 KB), you need to [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode). **Note**: If you enable Advanced RTS functions while the SDK is running, you must re\-initialize the engine for the configuration to take effect. |
|config |MessageConfig |See [MessageConfig](https://docs.byteplus.com/en/docs/12/docs-70083#MessageConfig) |

**Notes**

* Before sending in\-room binary messages, you must call [joinRTSRoom](https://docs.byteplus.com/en/docs/12/14166#RTSRoom-joinrtsroom) to join the room.

* After the call, you will receive an [onUserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onusermessagesendresult) callback to notify that the message was sent successfully or failed;

* If the message was sent successfully, the user specified by the userId will receive an [onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onuserbinarymessagereceived) callback.

### sendRoomMessage

```java
public abstract long com.ss.bytertc.engine.RTSRoom.sendRoomMessage(String messageStr)
```

Send text messages to all other users in the room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|messageStr |String |The content of the text message sent. The default size of a single message package is 1 KB. For larger message transmission (up to 64 KB), you need to [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode). **Note**: If you enable Advanced RTS functions while the SDK is running, you must re\-initialize the engine for the configuration to take effect. |

**Notes**

* Before broadcasting a text message in the room, you must call [joinRTSRoom](https://docs.byteplus.com/en/docs/12/14166#RTSRoom-joinrtsroom) to join the room.

* After the call, you will receive the [onRoomMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onroommessagesendresult) callback;

* Other users in the same room will receive the [onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onroommessagereceived) callback.

### sendRoomBinaryMessage

```java
public abstract long com.ss.bytertc.engine.RTSRoom.sendRoomBinaryMessage(byte[] buffer)
```

Send binary messages to all other users in the room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|buffer |byte[] |The content of the binary message sent. The default size of a single message package is 1 KB. For larger message transmission (up to 64 KB), you need to [enable Advanced RTS functions in the console](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode). **Note**: If you enable Advanced RTS functions while the SDK is running, you must re\-initialize the engine for the configuration to take effect. |

**Notes**

* Before broadcasting binary messages in the room, you must call [joinRTSRoom](https://docs.byteplus.com/en/docs/12/14166#RTSRoom-joinrtsroom) to join the room.

* After the call, you will receive the [onRoomMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onroommessagesendresult) callback;

* Other users in the same room will receive the [onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onroombinarymessagereceived) callback.

# IRangeAudio

```java
public interface com.ss.bytertc.engine.audio.IRangeAudio
```

Range audio instance

## Member Functions

|Return |Name |
|---|---|
|void |[enableRangeAudio](https://docs.byteplus.com/en/docs/12/14166#IRangeAudio-enablerangeaudio) |
|int |[updatePosition](https://docs.byteplus.com/en/docs/12/14166#IRangeAudio-updateposition) |
|int |[updateReceiveRange](https://docs.byteplus.com/en/docs/12/14166#IRangeAudio-updatereceiverange) |
|int |[setAttenuationModel](https://docs.byteplus.com/en/docs/12/14166#IRangeAudio-setattenuationmodel) |
|void |[setNoAttenuationFlags](https://docs.byteplus.com/en/docs/12/14166#IRangeAudio-setnoattenuationflags) |

## Instructions

### enableRangeAudio

```java
void com.ss.bytertc.engine.audio.IRangeAudio.enableRangeAudio(boolean enable)
```

Enable/disable the range audio function.

Range audio means that within a certain range in a same RTC room, the audio volume of the remote user received by the local user will be amplified/attenuated as the remote user moves closer/away. The audio coming from out of the range cannot be heard. See [updateReceiveRange](https://docs.byteplus.com/en/docs/12/14166#IRangeAudio-updatereceiverange) to set audio receiving range.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |boolean |Whether to enable audio range function:<br><br><br> <br><br>* true: Enable<br><br>* false: Disable（Defaulting setting） |

**Notes**

You can call this API anytime before or after entering a room. To ensure a smooth switch to the range audio mode after entering the room, you need to call [updatePosition](https://docs.byteplus.com/en/docs/12/14166#IRangeAudio-updateposition) before this API to set your own position coordinates, and then enable the range audio function.

### updatePosition

```java
int com.ss.bytertc.engine.audio.IRangeAudio.updatePosition(Position pos)
```

Updates the coordinate of the local user's position in the rectangular coordinate system in the current room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|pos |Position |3D coordinate values, the default value is [0, 0, 0], see [Position](https://docs.byteplus.com/en/docs/12/docs-70083#Position). |

**Return Value**

API call result:

* 0: Success

* !0: Failure

**Notes**

* After calling this API, you should call [enableRangeAudio](https://docs.byteplus.com/en/docs/12/14166#IRangeAudio-enablerangeaudio) to enable range audio function to actually enjoy the range audio effect.

### updateReceiveRange

```java
int com.ss.bytertc.engine.audio.IRangeAudio.updateReceiveRange(ReceiveRange range)
```

Updates the audio receiving range for the local user.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|range |ReceiveRange |Audio receiving range, see [ReceiveRange](https://docs.byteplus.com/en/docs/12/docs-70083#ReceiveRange). |

**Return Value**

API call result:

* 0: Success

* !0: Failure

### setAttenuationModel

```java
int com.ss.bytertc.engine.audio.IRangeAudio.setAttenuationModel(
    AttenuationType type,
    float coefficient
)
```

Set the volume roll\-off mode that a 3D sound has in an audio source when using the Range Audio feature.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |AttenuationType |Volume roll\-off mode. It is linear roll\-off mode by default. Refer to [AttenuationType](https://docs.byteplus.com/en/docs/12/docs-70083#AttenuationType) for more details. |
|coefficient |float |Coefficient for the exponential roll\-off mode. The default value is 1. It ranges [0.1,100]. We recommended to set it to `50`. The volume roll\-off speed gets faster as this value increases. |

**Return Value**

Result of the call

* `0`: Success

* `-1`: Failure because of calling this API before the user has joined a room or before enabling the Range Audio feature by calling [enableRangeAudio](https://docs.byteplus.com/en/docs/12/14166#IRangeAudio-enablerangeaudio).

**Notes**

Call [updateReceiveRange](https://docs.byteplus.com/en/docs/12/14166#IRangeAudio-updatereceiverange) to set the range outside which the volume of the sound does not attenuate.

### setNoAttenuationFlags

```java
void com.ss.bytertc.engine.audio.IRangeAudio.setNoAttenuationFlags(List<String> flags)
```

Set the flags to mark the user groups, within which the users talk without attenuation.

In the RTC room, if the flags of the users intersect with each other, the users talk without attenuation.

For example, the user is a member of multiple teams, and teammates of the same team talk without attenuation. You can set the flag for each team, and include the flags of the user's teams in the user's flags.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|flags |List<String\> |Array of flags. |

# RTCEngine

```java
public abstract class com.ss.bytertc.engine.RTCEngine
```

RTCEngine Class

## Static Functions

|Return |Name |
|---|---|
|static synchronized RTCEngine |[createRTCEngine](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-creatertcengine) |
|static synchronized void |[destroyRTCEngine](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-destroyrtcengine) |
|static String |[getSDKVersion](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-getsdkversion) |
|static int |[setLogConfig](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setlogconfig) |

## Member Functions

|Return |Name |
|---|---|
|abstract IRTCAudioDeviceManager |[getAudioDeviceManager](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-getaudiodevicemanager) |
|abstract int |[startVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startvideocapture) |
|abstract int |[stopVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopvideocapture) |
|abstract int |[startAudioCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startaudiocapture) |
|abstract int |[stopAudioCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopaudiocapture) |
|abstract int |[setAudioScenario](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setaudioscenario) |
|abstract int |[setAudioProfile](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setaudioprofile) |
|abstract int |[setAnsMode](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setansmode) |
|abstract int |[setVoiceChangerType](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvoicechangertype) |
|abstract int |[setVoiceReverbType](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvoicereverbtype) |
|abstract int |[setLocalVoiceEqualization](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setlocalvoiceequalization) |
|abstract int |[setLocalVoiceReverbParam](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setlocalvoicereverbparam) |
|abstract int |[enableLocalVoiceReverb](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-enablelocalvoicereverb) |
|abstract int |[setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setlocalvideocanvas) |
|abstract int |[updateLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-updatelocalvideocanvas) |
|abstract int |[setLocalVideoSink](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setlocalvideosink-2) |
|abstract int |[setLocalVideoMirrorType](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setlocalvideomirrortype) |
|abstract int |[setRemoteVideoMirrorType](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setremotevideomirrortype) |
|abstract int |[setVideoRotationMode](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideorotationmode) |
|abstract int |[switchCamera](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-switchcamera) |
|abstract int |[setAudioRoute](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setaudioroute) |
|abstract AudioRoute |[getAudioRoute](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-getaudioroute) |
|abstract int |[setDefaultAudioRoute](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setdefaultaudioroute) |
|abstract int |[enableExternalSoundCard](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-enableexternalsoundcard) |
|abstract int |[muteAudioCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-muteaudiocapture) |
|abstract int |[muteScreenAudioCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-mutescreenaudiocapture) |
|abstract int |[setCaptureVolume](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setcapturevolume) |
|abstract int |[setScreenCaptureVolume](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setscreencapturevolume) |
|abstract int |[setPlaybackVolume](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setplaybackvolume) |
|abstract int |[setLocalVoicePitch](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setlocalvoicepitch) |
|abstract int |[enableVocalInstrumentBalance](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-enablevocalinstrumentbalance) |
|abstract int |[enablePlaybackDucking](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-enableplaybackducking) |
|abstract int |[login](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-login) |
|abstract int |[logout](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-logout) |
|abstract int |[updateLoginToken](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-updatelogintoken) |
|abstract int |[setServerParams](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setserverparams) |
|abstract int |[getPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-getpeeronlinestatus) |
|abstract long |[sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-sendusermessageoutsideroom) |
|abstract long |[sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-senduserbinarymessageoutsideroom) |
|abstract long |[sendServerMessage](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-sendservermessage) |
|abstract long |[sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-sendserverbinarymessage) |
|abstract int |[startNetworkDetection](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startnetworkdetection) |
|abstract int |[stopNetworkDetection](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopnetworkdetection) |
|abstract int |[enableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-enableaudioframecallback) |
|abstract int |[disableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-disableaudioframecallback) |
|abstract int |[registerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-registeraudioframeobserver) |
|abstract int |[registerAudioProcessor](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-registeraudioprocessor) |
|abstract int |[enableAudioProcessor](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-enableaudioprocessor) |
|abstract int |[disableAudioProcessor](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-disableaudioprocessor) |
|abstract int |[registerLocalVideoProcessor](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-registerlocalvideoprocessor) |
|abstract int |[setVideoDigitalZoomConfig](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideodigitalzoomconfig) |
|abstract int |[setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideodigitalzoomcontrol) |
|abstract int |[startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startvideodigitalzoomcontrol) |
|abstract int |[stopVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopvideodigitalzoomcontrol) |
|abstract int |[registerLocalEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-registerlocalencodedvideoframeobserver) |
|abstract int |[registerRemoteEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-registerremoteencodedvideoframeobserver) |
|abstract int |[setVideoSourceType](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideosourcetype) |
|abstract int |[pushExternalVideoFrame](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-pushexternalvideoframe) |
|abstract int |[startPushMixedStream](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startpushmixedstream) |
|abstract int |[updatePushMixedStream](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-updatepushmixedstream) |
|abstract int |[stopPushMixedStream](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stoppushmixedstream) |
|abstract int |[startPushSingleStream](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startpushsinglestream) |
|abstract int |[stopPushSingleStream](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stoppushsinglestream) |
|abstract int |[setVideoCaptureConfig](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideocaptureconfig) |
|abstract int |[setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideoencoderconfig) |
|abstract int |[setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setlocalsimulcastmode) |
|abstract int |[setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setlocalsimulcastmode-2) |
|abstract int |[setAudioSourceType](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setaudiosourcetype) |
|abstract int |[setAudioRenderType](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setaudiorendertype) |
|abstract int |[pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-pushexternalaudioframe) |
|abstract int |[pullExternalAudioFrame](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-pullexternalaudioframe) |
|abstract int |[pushReferenceAudioPCMData](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-pushreferenceaudiopcmdata) |
|abstract RTCRoom |[createRTCRoom](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-creatertcroom) |
|abstract RTSRoom |[createRTSRoom](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-creatertsroom) |
|abstract int |[setPublishFallbackOption](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setpublishfallbackoption) |
|abstract int |[setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setsubscribefallbackoption) |
|abstract int |[setRemoteUserPriority](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setremoteuserpriority) |
|abstract int |[setBusinessId](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setbusinessid) |
|abstract int |[setEncryptInfo](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setencryptinfo) |
|abstract int |[setCustomizeEncryptHandler](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setcustomizeencrypthandler) |
|abstract IVideoEffect |[getVideoEffectInterface](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-getvideoeffectinterface) |
|abstract int |[enableEffectBeauty](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-enableeffectbeauty) |
|abstract int |[setBeautyIntensity](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setbeautyintensity) |
|abstract int |[setVideoOrientation](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideoorientation) |
|abstract int |[setRuntimeParameters](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setruntimeparameters) |
|abstract int |[feedback](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-feedback) |
|abstract long |[getNativeHandle](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-getnativehandle) |
|abstract int |[startAudioRecording](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startaudiorecording) |
|abstract int |[stopAudioRecording](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopaudiorecording) |
|abstract IAudioEffectPlayer |[getAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-getaudioeffectplayer) |
|abstract IMediaPlayer |[getMediaPlayer](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-getmediaplayer) |
|abstract int |[setScreenAudioSourceType](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setscreenaudiosourcetype) |
|abstract int |[pushScreenAudioFrame](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-pushscreenaudioframe) |
|abstract int |[setExternalVideoEncoderEventHandler](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setexternalvideoencodereventhandler) |
|abstract int |[setEarMonitorMode](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setearmonitormode) |
|abstract int |[setEarMonitorMode](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setearmonitormode-2) |
|abstract int |[setEarMonitorVolume](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setearmonitorvolume) |
|abstract int |[enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-enableaudiopropertiesreport) |
|abstract int |[sendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-sendstreamsyncinfo) |
|abstract boolean |[isCameraTorchSupported](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-iscameratorchsupported) |
|abstract boolean |[isCameraZoomSupported](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-iscamerazoomsupported) |
|abstract int |[setCameraZoomRatio](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setcamerazoomratio) |
|abstract float |[getCameraZoomMaxRatio](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-getcamerazoommaxratio) |
|abstract int |[setCameraTorch](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setcameratorch) |
|abstract boolean |[isCameraFocusPositionSupported](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-iscamerafocuspositionsupported) |
|abstract int |[setCameraFocusPosition](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setcamerafocusposition) |
|abstract boolean |[isCameraExposurePositionSupported](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-iscameraexposurepositionsupported) |
|abstract int |[setCameraExposurePosition](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setcameraexposureposition) |
|abstract int |[setCameraExposureCompensation](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setcameraexposurecompensation) |
|abstract int |[enableCameraAutoExposureFaceMode](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-enablecameraautoexposurefacemode) |
|abstract int |[setCameraAdaptiveMinimumFrameRate](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setcameraadaptiveminimumframerate) |
|abstract int |[enableAlphaChannelVideoEncode](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-enablealphachannelvideoencode) |
|abstract int |[disableAlphaChannelVideoEncode](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-disablealphachannelvideoencode) |
|abstract int |[sendSEIMessage](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-sendseimessage) |
|abstract int |[sendLivePushSEIMessage](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-sendlivepushseimessage) |
|abstract int |[startFileRecording](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startfilerecording) |
|abstract int |[stopFileRecording](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopfilerecording) |
|abstract int |[pushExternalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-pushexternalencodedvideoframe) |
|abstract int |[startScreenCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startscreencapture) |
|abstract int |[updateScreenCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-updatescreencapture) |
|abstract int |[stopScreenCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopscreencapture) |
|abstract int |[setVideoWatermark](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideowatermark) |
|abstract int |[clearVideoWatermark](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-clearvideowatermark) |
|abstract int |[setDummyCaptureImagePath](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setdummycaptureimagepath) |
|abstract long |[takeLocalSnapshot](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-takelocalsnapshot) |
|abstract long |[takeRemoteSnapshot](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-takeremotesnapshot) |
|abstract long |[takeRemoteSnapshotToFile](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-takeremotesnapshottofile) |
|abstract long |[takeLocalSnapshotToFile](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-takelocalsnapshottofile) |
|abstract int |[startEchoTest](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startechotest) |
|abstract int |[stopEchoTest](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopechotest) |
|abstract int |[setRemoteVideoSink](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setremotevideosink-2) |
|abstract int |[updateRemoteStreamVideoCanvas](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-updateremotestreamvideocanvas-2) |
|abstract int |[setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setremotevideocanvas) |
|abstract int |[setRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setremoteaudioplaybackvolume) |
|abstract int |[setVideoDecoderConfig](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideodecoderconfig) |
|abstract int |[requestRemoteVideoKeyFrame](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-requestremotevideokeyframe) |
|abstract int |[startCloudProxy](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startcloudproxy) |
|abstract int |[stopCloudProxy](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopcloudproxy) |
|abstract NetworkTimeInfo |[getNetworkTimeInfo](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-getnetworktimeinfo) |
|abstract IWTNStream |[getWTNStream](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-getwtnstream) |
|abstract int |[startHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-starthardwareechodetection) |
|abstract int |[stopHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stophardwareechodetection) |
|abstract int |[setCellularEnhancement](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setcellularenhancement) |
|abstract int |[setLocalProxy](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setlocalproxy) |
|abstract IVideoDeviceManager |[getVideoDeviceManager](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-getvideodevicemanager) |
|abstract int |[setVideoCaptureRotation](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideocapturerotation) |
|abstract int |[deprecated] [setLocalVideoSink](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setlocalvideosink) |
|abstract int |[deprecated] [setRemoteVideoSink](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setremotevideosink) |
|abstract int |[deprecated] [updateRemoteStreamVideoCanvas](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-updateremotestreamvideocanvas) |

## Instructions

### createRTCEngine

```java
public static synchronized RTCEngine com.ss.bytertc.engine.RTCEngine.createRTCEngine(
    EngineConfig config,
    IRTCEngineEventHandler handler
)
```

Creates an engine instance.

This is the very first API that you must call if you want to use all the RTC capabilities.

If there is no engine instance in current process, calling this API will create one. If an engine instance has been created, calling this API again will have the created engine instance returned.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|config |EngineConfig |SDK Engine Config，see [EngineConfig](https://docs.byteplus.com/en/docs/12/docs-70083#EngineConfig) |
|handler |IRTCEngineEventHandler |Handler sent from SDK to App. See [IRTCEngineEventHandler](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler) |

**Return Value**

* RTCEngine: A successfully created engine instance.

* Null: EngineConfig is inValid see [EngineConfig](https://docs.byteplus.com/en/docs/12/docs-70083#EngineConfig). Failed to load the so file

**Notes**

The lifecycle of the handler must be longer than that of the RTCEngine, i.e. the handler must be created before calling [createRTCEngine](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-creatertcengine) and destroyed after calling [destroyRTCEngine](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-destroyrtcengine).

### destroyRTCEngine

```java
public static synchronized void com.ss.bytertc.engine.RTCEngine.destroyRTCEngine()
```

Destroy the engine instance created by [createRTCEngine](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-creatertcengine), and release all related resources.

**Notes**

* Call this API after all business scenarios related to the engine instance are destroyed.

* When the API is called, RTC SDK destroys all memory associated with the engine instance and stops any interaction with the media server.

* Calling this API will start the SDK exit logic. The engine thread is held until the exit logic is complete. The engine thread is retained until the exit logic is complete. Therefore, do not call this API directly in the callback thread, or it will cause a deadlock. This function takes a long time to execute, so it's not recommended to call this API in the main thread, or the main thread may be blocked.

### getSDKVersion

```java
public static String com.ss.bytertc.engine.RTCEngine.getSDKVersion()
```

Get the current version number of the SDK.

**Return Value**

The current SDK version number.

### setLogConfig

```java
public static int com.ss.bytertc.engine.RTCEngine.setLogConfig(RTCLogConfig logConfig)
```

Configures the local log parameters of RTC SDK, including the logging level, directory, the limits for total log file size, and the prefix to the log file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|logConfig |RTCLogConfig |Local log parameters. See [RTCLogConfig](https://docs.byteplus.com/en/docs/12/docs-70083#RTCLogConfig). |

**Return Value**

* 0: Success.

* –1: Failure. This API must be called before creating engine.

* –2: Failure. Invalid parameters.

**Notes**

This API must be called before [createRTCEngine](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-creatertcengine).

### getAudioDeviceManager

```java
public abstract IRTCAudioDeviceManager com.ss.bytertc.engine.RTCEngine.getAudioDeviceManager()
```

Gets audio device management API class.

**Return Value**

See [IRTCAudioDeviceManager](https://docs.byteplus.com/en/docs/12/14166#IRTCAudioDeviceManager).

### startVideoCapture

```java
public abstract int com.ss.bytertc.engine.RTCEngine.startVideoCapture()
```

Stop internal video capture immediately.

Internal video capture refers to: capturing video using the built\-in module.

The local client will be informed via [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onvideodevicestatechanged) after starting video capture by calling this API.

The remote clients in the room will be informed of the state change via [onUserStartVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onuserstartvideocapture) after the visible client starts video capture by calling this API.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* Since the upgrade in v3.37.0, you need to add Kotlin plugin to Gradle in the project to use this API.

* Call [stopVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopvideocapture) to stop the internal video capture. Otherwise, the internal video capture will sustain until you destroy the engine instance.

* Once you create the engine instance, you can start internal video capture regardless of the video publishing state. The video stream will start publishing only after the video capture starts.

* To switch from custom to internal video capture, stop publishing before disabling the custom video capture module and then call this API to enable the internal video capture.

* Call [switchCamera](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-switchcamera) to switch the camera used by the internal video capture module.

* If the default video format can not meet your requirement, contact our technical specialist to help you with Cloud Config. After that, you can push and apply these configurations to Android clients at any time.

### stopVideoCapture

```java
public abstract int com.ss.bytertc.engine.RTCEngine.stopVideoCapture()
```

Disable internal video capture immediately. The default is off.

Internal video capture refers to: capturing video using the built\-in module.

The local client will be informed via [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onvideodevicestatechanged) after stopping video capture by calling this API.

The remote clients in the room will be informed of the state change via [onUserStopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onuserstopvideocapture) after the visible client stops video capture by calling this API.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* Call startVideoCapture to enable the internal video capture.

* Without calling this API the internal video capture will sustain until you destroy the engine instance.

### startAudioCapture

```java
public abstract int com.ss.bytertc.engine.RTCEngine.startAudioCapture()
```

Start internal audio capture. The default is off.

Internal audio capture refers to: capturing audio using the built\-in module.

The local client will be informed via [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onaudiodevicestatechanged) after starting audio capture by calling this API.

The remote clients in the room will be informed of the state change via [onUserStartAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onuserstartaudiocapture) after the visible user starts audio capture by calling this API.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* To enable a microphone without the user's permission will trigger [onWarning](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onwarning).

* Call [stopAudioCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopaudiocapture) to stop the internal audio capture. Otherwise, the internal audio capture will sustain until you destroy the engine instance.

* To mute and unmute microphones, we recommend using [publishStreamAudio](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-publishstreamaudio), other than [stopAudioCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopaudiocapture) and this API. Because starting and stopping capture devices often need some time waiting for the response of the device, that may lead to a short silence during the communication.

* To switch from custom to internal audio capture, stop publishing before disabling the custom audio capture module and then call this API to enable the internal audio capture.

### stopAudioCapture

```java
public abstract int com.ss.bytertc.engine.RTCEngine.stopAudioCapture()
```

Stop internal audio capture. The default is off.

Internal audio capture refers to: capturing audio using the built\-in module.

The local client will be informed via [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onaudiodevicestatechanged) after stopping audio capture by calling this API.

The remote clients in the room will be informed of the state change via [onUserStopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onuserstopaudiocapture) after the visible client stops audio capture by calling this API.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* Call [startAudioCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startaudiocapture) to enable the internal audio capture.

* Without calling this API the internal audio capture will sustain until you destroy the engine instance.

### setAudioScenario

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setAudioScenario(AudioScenarioType audioScenario)
```

> Available since 3.60.

Sets the audio scenarios.

After selecting the audio scenario, SDK will automatically switch to the proper volume modes (the call/media volume) according to the scenarios and the best audio configurations under such scenarios.

This API should not be used at the same time with the old one.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioScenario |AudioScenarioType |Audio scenarios. See [AudioScenarioType](https://docs.byteplus.com/en/docs/12/docs-70083#AudioScenarioType). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* You can only use this API before joining the room.

* Call volume is more suitable for calls, meetings and other scenarios that demand information accuracy. Call volume will activate the system hardware signal processor, making the sound clearer. The volume cannot be reduced to 0.

* Media volume is more suitable for entertainment scenarios, which require musical expression. The volume can be reduced to 0.

### setAudioProfile

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setAudioProfile(AudioProfileType audioProfile)
```

Sets the sound quality. Call this API to change the sound quality if the audio settings in the current [ChannelProfile](https://docs.byteplus.com/en/docs/12/docs-70083#ChannelProfile) can not meet your requirements.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioProfile |AudioProfileType |Sound quality. See [AudioProfileType](https://docs.byteplus.com/en/docs/12/docs-70083#AudioProfileType) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* This method can be called before and after entering the room.

* Support dynamic switching of sound quality during a call.

### setAnsMode

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setAnsMode(AnsMode ansMode)
```

> Available since 3.52

Set the Active Noise Cancellation(ANC) mode during audio and video communications.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|ansMode |AnsMode |ANC modes. See [AnsMode](https://docs.byteplus.com/en/docs/12/docs-70083#AnsMode). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* You can call this API before or after entering a room. When you repeatedly call it, only the last call takes effect.

* The noise reduction algorithm includes both traditional noise reduction and AI noise reduction. Traditional noise reduction is primarily aimed at suppressing steady noises, such as the hum of air conditioners and the whir of fans. AI noise reduction, on the other hand, is mainly designed to suppress non\-stationary noises, like the tapping of keyboards and the clattering of tables and chairs.

* The AI noise reduction can only be enabled through this interface when the following [ChannelProfile](https://docs.byteplus.com/en/docs/12/docs-70083#ChannelProfile) scenarios are engaged:

   * Gaming voice mode: `CHANNEL_PROFILE_GAME(2)`

   * High\-fidelity gaming mode: `CHANNEL_PROFILE_GAME_HD(8)`

   * Cloud gaming mode: `CHANNEL_PROFILE_CLOUD_GAME(3)`

   * 1 vs 1 audio/video call: `CHANNEL_PROFILE_CHAT(5)`

   * Multi\-client synchronized audio/video playback: `CHANNEL_PROFILE_LW_TOGETHER(7)`

   * Personal devices in cloud meetings: `CHANNEL_PROFIEL_MEETING`

   * Classroom interaction mode: `CHANNEL_PROFILE_MEETING_ROOM(17)`

   * Meeting room terminals in cloud meetings: `CHANNEL_PROFILE_CLASSROOM(18)`

### setVoiceChangerType

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setVoiceChangerType(VoiceChangerType voiceChanger)
```

> Available since 3.32

Set the sound change effect type

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|voiceChanger |VoiceChangerType |The sound change effect type. See [VoiceChangerType](https://docs.byteplus.com/en/docs/12/docs-70083#VoiceChangerType) |

**Return Value**

API call result:

* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for specific reasons.

**Notes**

* To use this feature, you need to integrate the SAMI library. See [On-Demand Plugin Integration](https://docs.byteplus.com/en/docs/12/1108726).

* You can call it before and after entering the room.

* Effective for both internal and external audio source.

* Only valid for mono\-channel audio.

* Mutually exclusive with [setVoiceReverbType](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvoicereverbtype), and the effects set later will override the effects set first.

### setVoiceReverbType

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setVoiceReverbType(VoiceReverbType voiceReverb)
```

> Available since 3.32

Set the reverb effect type

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|voiceReverb |VoiceReverbType |Reverb effect type. See [VoiceReverbType](https://docs.byteplus.com/en/docs/12/docs-70083#VoiceReverbType) |

**Return Value**

API call result:

* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for specific reasons.

**Notes**

* You can call it before and after entering the room.

* Effective for both internal and external audio source.

* Only valid for mono\-channel audio.

* Mutually exclusive with [setVoiceChangerType](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvoicechangertype), and the effects set later will override the effects set first.

### setLocalVoiceEqualization

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setLocalVoiceEqualization(VoiceEqualizationConfig voiceEqualizationConfig)
```

Set the equalization effect for the local captured audio. The audio includes both internal captured audio and external captured voice, but not the mixing audio file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|voiceEqualizationConfig |VoiceEqualizationConfig |See [VoiceEqualizationConfig](https://docs.byteplus.com/en/docs/12/docs-70083#VoiceEqualizationConfig). |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

According to the Nyquist acquisition rate, the audio acquisition rate must be greater than twice the set center frequency. Otherwise, the setting will not be effective.

### setLocalVoiceReverbParam

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setLocalVoiceReverbParam(VoiceReverbConfig config)
```

Set the reverb effect for the local captured audio. The audio includes both internal captured audio and external captured voice, but not the mixing audio file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|config |VoiceReverbConfig |See [VoiceReverbConfig](https://docs.byteplus.com/en/docs/12/docs-70083#VoiceReverbConfig). |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

Call [enableLocalVoiceReverb](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-enablelocalvoicereverb) to enable the reverb effect.

### enableLocalVoiceReverb

```java
public abstract int com.ss.bytertc.engine.RTCEngine.enableLocalVoiceReverb(boolean enable)
```

Enable the reverb effect for the local captured voice.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |boolean |Whether to enable. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

Call [setLocalVoiceReverbParam](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setlocalvoicereverbparam) to set the reverb effect.

### setLocalVideoCanvas

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setLocalVideoCanvas(VideoCanvas videoCanvas)
```

Sets the view to be used for local video rendering and the rendering mode.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|videoCanvas |VideoCanvas |View information and rendering mode. See [VideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70083#VideoCanvas). |

**Return Value**

* 0: Success.

* \-2: Invalid parameter.

* \-12: This method is not available in the Audio SDK.

**Notes**

* You should bind your stream to a view before joining the room. This setting will remain in effect after you leave the room.

* If you need to unbind the local video stream from the current view, you can call this API and set the videoCanvas to `null`.

### updateLocalVideoCanvas

```java
public abstract int com.ss.bytertc.engine.RTCEngine.updateLocalVideoCanvas(
    int renderMode,
    int backgroundColor
)
```

Update the render mode and background color of local video rendering

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|renderMode |int |See [VideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70083#VideoCanvas).renderMode |
|backgroundColor |int |See [VideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70083#VideoCanvas).backgroundColor |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

Calling this API during local video rendering will be effective immediately.

### setLocalVideoSink

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setLocalVideoSink(
    IVideoSink videoSink,
    LocalVideoSinkConfig config
)
```

> Available since 3.57

Binds the local video stream to a custom renderer. You can get video frame data at specified positions and formats through parameter settings.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|videoSink |IVideoSink |Custom video renderer. See [IVideoSink](https://docs.byteplus.com/en/docs/12/docs-70083#IVideoSink). |
|config |LocalVideoSinkConfig |Local video frame callback configuration, see [LocalVideoSinkConfig](https://docs.byteplus.com/en/docs/12/docs-70083#LocalVideoSinkConfig)。 |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* RTC SDK uses its own renderer (internal renderer) for video rendering by default.

* Leaving the room will clear the binding status.

* If you need to unbind the video stream from the custom renderer, you must set video_sink to `null`.

* Generally, after receiving the [onFirstLocalVideoFrameCaptured](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onfirstlocalvideoframecaptured) callback notification that the first local video frame has been captured, call this method to bind a custom renderer to a video stream and join the room.

### setLocalVideoMirrorType

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setLocalVideoMirrorType(MirrorType mirrorType)
```

Sets the mirror mode for the captured video stream.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mirrorType |MirrorType |Mirror type. See [MirrorType](https://docs.byteplus.com/en/docs/12/docs-70083#MirrorType). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* Switching video streams does not affect the settings of the mirror type.

* This API is not applicable to screen\-sharing streams.

* When using an external renderer, you can set `mirrorType` to `0` and `3`, but you cannot set it to `1`.

* Before you call this API, the initial states of each video stream are as follows:

| |Front\-facing camera |Back\-facing camera |Custom capturing |Built\-in camera |
|---|---|---|---|---|
|Mobile device |The preview is mirrored. The published video stream is not mirrored. |The preview and the published video stream are not mirrored. |The preview and the published video stream are not mirrored. |/ |
|PC |/ |/ |The preview and the published video stream are not mirrored. |The preview is mirrored. The published video stream is not mirrored. |

  ### setRemoteVideoMirrorType ```java public abstract int com.ss.bytertc.engine.RTCEngine.setRemoteVideoMirrorType( String streamId, RemoteMirrorType mirrorType ) ``` \> Available since 3.57

When using internal rendering, enable mirroring for the remote stream.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |String |Stream ID, used to specify the video stream that needs to be mirrored. |
|mirrorType |RemoteMirrorType |The mirror type for the remote stream, see [RemoteMirrorType](https://docs.byteplus.com/en/docs/12/docs-70083#RemoteMirrorType). |

**Return Value**

* 0: Successful call.

* < 0: Call failed, see [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more error details.

### setVideoRotationMode

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setVideoRotationMode(VideoRotationMode rotationMode)
```

Set the orientation of the video capture. By default, the App direction is used as the orientation reference.

During rendering, the receiving client rotates the video in the same way as the sending client did.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|rotationMode |VideoRotationMode |Rotation reference can be the orientation of the App or gravity. Refer to [VideoRotationMode](https://docs.byteplus.com/en/docs/12/docs-70083#VideoRotationMode) for details. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* The orientation setting is effective for internal video capture only. That is, the orientation setting is not effective to the custom video source or the screen\-sharing stream.

* If the video capture is on, the setting will be effective once you call this API. If the video capture is off, the setting will be effective when capture starts.

### switchCamera

```java
public abstract int com.ss.bytertc.engine.RTCEngine.switchCamera(CameraId cameraId)
```

Switch to the front\-facing/back\-facing camera used in the internal video capture

The local client will be informed via [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onvideodevicestatechanged) after calling this API.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|cameraId |CameraId |Camera ID. Refer to [CameraId](https://docs.byteplus.com/en/docs/12/docs-70083#CameraId) for more details. |

**Return Value**

* 0: Success

* < 0: Failure

**Notes**

* Front\-facing camera is the default camera.

* If the internal video capturing is on, the switch is effective once you call this API. If the internal video capturing is off, the setting will be effective when capture starts.

### setAudioRoute

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setAudioRoute(AudioRoute audioRoute)
```

Set the current audio playback route. The default device is set via [setDefaultAudioRoute](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setdefaultaudioroute).

When the audio playback route changes, you will receive [onAudioRouteChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onaudioroutechanged).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioRoute |AudioRoute |Audio route. Refer to [AudioRoute](https://docs.byteplus.com/en/docs/12/docs-70083#AudioRoute).<br><br> <br><br>For Android devices, the valid audio playback devices may vary due to different audio device connection status. See [Set the Audio Route](https://docs.byteplus.com/byteplus-rtc/docs/117836). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* You can implement most scenarios by calling [setDefaultAudioRoute](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setdefaultaudioroute) and the default audio route switching strategy of the RTC SDK. For details about the strategy, see [Set the Audio Route](https://docs.byteplus.com/byteplus-rtc/docs/117836). You should use this API in a few exceptional scenarios like manually switching audio route with external audio device connected.

* This interface is only supported in communication mode.

* For the volume type in different audio scenarios, refer to [AudioScenarioType](https://docs.byteplus.com/en/docs/12/docs-70083#AudioScenarioType).

### getAudioRoute

```java
public abstract AudioRoute com.ss.bytertc.engine.RTCEngine.getAudioRoute()
```

Get the information of currently\-using playback route.

**Return Value**

See [AudioRoute](https://docs.byteplus.com/en/docs/12/docs-70083#AudioRoute).

**Notes**

To set the audio playback route, see [setAudioRoute](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setaudioroute).

### setDefaultAudioRoute

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setDefaultAudioRoute(AudioRoute route)
```

Set the speaker or earpiece as the default audio playback device.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|route |AudioRoute |Audio playback device. Refer to [AudioRoute](https://docs.byteplus.com/en/docs/12/docs-70083#AudioRoute). You can only use earpiece and speakerphone. |

**Return Value**

* 0: Success.

* < 0: failure. It fails when the device designated is neither a speaker nor an earpiece.

**Notes**

For the default audio route switching strategy of the RTC SDK, see [Set the Audio Route](https://docs.byteplus.com/byteplus-rtc/docs/117836).

### enableExternalSoundCard

```java
public abstract int com.ss.bytertc.engine.RTCEngine.enableExternalSoundCard(boolean enable)
```

Enable the audio processing mode for an external sound card.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |boolean |* true: enable<br><br>* false: disable (by default) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* When you use an external sound card for audio capture, enable this mode for better audio quality.

* When using the mode, you can only use earphones. If you need to use internal or external speaker, disable this mode.

### muteAudioCapture

```java
public abstract int com.ss.bytertc.engine.RTCEngine.muteAudioCapture(boolean mute)
```

> Available since 3.58.1

Set whether to mute the recording signal (without changing the local hardware).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mute |boolean |Whether to mute audio capture.<br><br><br> <br><br>* True: Mute (disable microphone)<br><br>* False: (Default) Enable microphone |

**Return Value**

* 0: Success.

* < 0 : Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* Calling this API does not affect the status of SDK audio stream publishing.

* Adjusting the volume by calling [setCaptureVolume](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setcapturevolume) after muting will not cancel the mute state. The volume state will be retained until unmuted.

* You can use this interface to set the capture volume before or after calling [startAudioCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startaudiocapture) to enable audio capture.

### muteScreenAudioCapture

```java
public abstract int com.ss.bytertc.engine.RTCEngine.muteScreenAudioCapture(boolean mute)
```

> Available since 3.60.

Mutes/unmutes the audio captured when screen sharing.

Calling this method will send muted data instead of the screen audio data, and it does not affect the local audio device capture status and the SDK audio stream publishing status.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mute |boolean |Whether to mute the audio capture when screen sharing.<br><br><br> <br><br>* True: Mute the audio capture when screen sharing.<br><br>* False: (Default) Unmute the audio capture when screen sharing. |

**Return Value**

* 0: Success.

* < 0 : Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* Adjusting the volume by calling [setCaptureVolume](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setcapturevolume) after muting will not cancel the mute state. The volume state will be retained until unmuted.

* You can use this interface to set the capture volume before or after calling [startAudioCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startaudiocapture) to enable audio capture.

### setCaptureVolume

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setCaptureVolume(int volume)
```

Adjust the volume of the audio capture

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |int |Ratio of capture volume to original volume.<br><br> <br><br>This changes the volume property of the audio data other than the hardware volume.<br><br>Ranging: [0,400]. Unit: %<br><br> <br><br>To ensure the audio quality, we recommend setting the volume to `100`.<br><br><br> <br><br>* 0: Mute<br><br>* 100: Original volume. To ensure the audio quality, we recommend [0, 100].<br><br>* 400: Four times the original volume with signal\-clipping protection. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

Call this API to set the volume of the audio capture before or during the audio capture.

### setScreenCaptureVolume

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setScreenCaptureVolume(int volume)
```

> Available Available since 3.60.

Adjusts the volume of audio captured during screen sharing.

This method only changes the volume of audio data and does not affect the hardware volume of the local device.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |int |The ratio of the capture volume to the original volume, in the range of [0, 400], in %, with built\-in overflow protection.<br><br> <br><br>To ensure better call quality, it is recommended to set the volume value to [0, 100].<br><br><br> <br><br>* 0: Mute<br><br>* 100: Original volume. To ensure the audio quality, we recommend [0, 100].<br><br>* 400: Four times the original volume with signal\-clipping protection. |

**Return Value**

* 0: Success.

* < 0: Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

You can use this interface to set the capture volume before or after enabling screen audio capture.

### setPlaybackVolume

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setPlaybackVolume(int volume)
```

Adjusts the locally playing volume after mixing sounds of all remote users. You can call this API before or during the playback.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |int |Ratio(%) of playback volume to original volume, in the range [0, 400], with overflow protection.<br><br> <br><br>To ensure the audio quality, we recommend setting the volume to `100`.<br><br><br> <br><br>* 0: mute<br><br>* 100: original volume<br><br>* 400: Four times the original volume with signal\-clipping protection. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

Suppose a remote user A is always within the range of the target user whose playback volume will be adjusted, if you use both this method and [setRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setremoteaudioplaybackvolume)/[setRemoteRoomAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-setremoteroomaudioplaybackvolume), the volume that the local user hears from user A is the overlay of both settings.

### setLocalVoicePitch

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setLocalVoicePitch(int pitch)
```

Change local voice to a different key, mostly used in Karaoke scenarios.

You can adjust the pitch of local voice such as ascending or descending with this method.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|pitch |int |The value that is higher or lower than the original local voice within a range from \-12 to 12. The default value is 0, i.e. No adjustment is made.<br><br> <br><br>The difference in pitch between two adjacent values within the value range is a semitone, with positive values indicating an ascending tone and negative values indicating a descending tone, and the larger the absolute value set, the more the pitch is raised or lowered.<br><br> <br><br>Out of the value range, the setting fails and triggers [onWarning](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onwarning) callback, indicating `WARNING_CODE_SET_SCREEN_STREAM_INVALID_VOICE_PITCH` for invalid value setting with [WarningCode](https://docs.byteplus.com/en/docs/12/docs-70082#WarningCode). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

### enableVocalInstrumentBalance

```java
public abstract int com.ss.bytertc.engine.RTCEngine.enableVocalInstrumentBalance(boolean enable)
```

Enables/disables the loudness equalization function.

If you call this API with the parameter set to True, the loudness of user's voice will be adjusted to \-16lufs. If then you also call setAudioMixingLoudness and import the original loudness of the audio data used in audio mixing, the loudness will be adjusted to \-20lufs when the audio data starts to play.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |boolean |Whether to enable loudness equalization function:<br><br><br> <br><br>* true: Yes<br><br>* false: No |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

You must call this API before starting to play the audio file with [start](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-start).

### enablePlaybackDucking

```java
public abstract int com.ss.bytertc.engine.RTCEngine.enablePlaybackDucking(boolean enable)
```

Enables/disables the playback ducking function. This function is usually used in scenarios where short videos or music will be played simultaneously during RTC calls.

With the function on, if remote voice is detected, the local media volume of RTC will be lowered to ensure the clarity of the remote voice. If remote voice disappears, the local media volume of RTC restores.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |boolean |Whether to enable playback ducking:<br><br><br> <br><br>* true: Yes<br><br>* false: No |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

### login

```java
public abstract int com.ss.bytertc.engine.RTCEngine.login(
    String token,
    String uid
)
```

Sign in to call [sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-sendusermessageoutsideroom) and [sendServerMessage](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-sendservermessage) to send P2P messages or send messages to a server without joining the RTC room.

To sign out, call [logout](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-logout).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|token |String |Token is required during login for authentication.<br><br> <br><br>This Token is different from that required by calling joinRoom. You can assign any value even null to `roomId` to generate a login token. During developing and testing, you can use temporary tokens generated on the console. Deploy the token generating application on your server. |
|uid |String |User ID<br><br> <br><br>User ID is unique within one appid. |

**Return Value**

* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for specific reasons.

**Notes**

You will receive [onLoginResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onloginresult) after calling this API and signing in successfully. But remote users will not receive notification about that.

### logout

```java
public abstract int com.ss.bytertc.engine.RTCEngine.logout()
```

After calling this method to log out, it is impossible to call methods related to out\-of\-room messages and end\-to\-server messages or receive related callbacks.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* After calling this interface to log out, you must first call [login](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-login) to sign in.

* After local users call this method to log out, they will receive the result of the [onLogout](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onlogout) callback notification, and remote users will not receive the notification.

### updateLoginToken

```java
public abstract int com.ss.bytertc.engine.RTCEngine.updateLoginToken(String token)
```

Update the Token

Token used by the user for login has a certain valid period. When the Token expires, you need to call this method to update the login Token information.

When calling the [login](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-login) method to sign in, if an expired token is used, the login will fail and you will receive an [onLoginResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onloginresult) callback notification with an error code of 'LOGIN_ERROR_CODE_INVALID_TOKEN'. You need to reacquire the token and call this method to update the token.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|token |String |Updated dynamic key |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* If the token is invalid and the login fails, the SDK will automatically log in again after updating the token by calling this method, and the user does not need to call the [login](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-login) method himself.

* If the token expires after you have successfully signed in, it will not be affected. An expired Token error will be notified to the user the next time you log in with an expired Token, or when you log in again due to a disconnection due to poor local network conditions.

### setServerParams

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setServerParams(
    String signature,
    String url
)
```

Set application server parameters

Before the client side calls [sendServerMessage](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-sendservermessage) or [sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-sendserverbinarymessage) to send a message to the application server, you must set a valid signature and application server address.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|signature |String |Dynamic signature. The App server may use the signature to verify the source of messages.<br><br> <br><br>You need to define the signature yourself. It can be any non\-empty string. It is recommended to encode information such as UID into the signature.<br><br> <br><br>The signature will be sent to the address set through the "url" parameter in the form of a POST request. |
|url |String |The address of the application server |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* The user must call [login](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-login) to sign in before calling this interface.

* After calling this interface, the SDK will use [onServerParamsSetResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onserverparamssetresult) to return the corresponding result.

### getPeerOnlineStatus

```java
public abstract int com.ss.bytertc.engine.RTCEngine.getPeerOnlineStatus(String peerUserID)
```

Query the sign\-in status of the remote or local user

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|peerUserID |String |The user ID to be queried |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* You must call [login](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-login) to sign in before calling this interface.

* After calling this interface, the SDK notifies the query result using the [onGetPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-ongetpeeronlinestatus) callback.

* Before sending an out\-of\-room message, the user can know whether the peer user is signed in through this API to decide whether to send a message. You can also check your sign\-in status through this API.

### sendUserMessageOutsideRoom

```java
public abstract long com.ss.bytertc.engine.RTCEngine.sendUserMessageOutsideRoom(
    String uid,
    String message,
    MessageConfig config
)
```

Send a text message (P2P) to a specified user outside the room

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|uid |String |User ID of the message receiver |
|message |String |Text message content sent. Message does not exceed 64 KB. |
|config |MessageConfig |Message type, see [MessageConfig](https://docs.byteplus.com/en/docs/12/docs-70083#MessageConfig). |

**Return Value**

* \> 0: Sent successfully, return the number of the sent message, increment from 1.

**Notes**

* Before calling this API, make sure you have enabled the [Advanced RTS functions](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode) in the RTC console.

> If this feature is enabled while the SDK is running, you must re\-initialize the engine for the configuration to take effect.

* Before sending an out\-of\-room text message, you must call [login](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-login) to login.

* After the user calls this API to send a text message, he will receive an [onUserMessageSendResultOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onusermessagesendresultoutsideroom) callback to know whether the message was successfully sent.

* If the text message is sent successfully, the user specified by uid receives the message via the [onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onusermessagereceivedoutsideroom) callback.

### sendUserBinaryMessageOutsideRoom

```java
public abstract long com.ss.bytertc.engine.RTCEngine.sendUserBinaryMessageOutsideRoom(
    String uid,
    byte[] buffer,
    MessageConfig config
)
```

Send binary messages (P2P) to the specified user outside the room

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|uid |String |User ID of the message receiver |
|buffer |byte[] |Binary message content sent. Message does not exceed 64KB. |
|config |MessageConfig |Message type, see [MessageConfig](https://docs.byteplus.com/en/docs/12/docs-70083#MessageConfig). |

**Return Value**

* \> 0: sent successfully, return the number of the sent message, increment from 1.

* \-1: Sending failed due to an empty message.

**Notes**

* Before calling this API, make sure you have enabled the [Advanced RTS functions](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode) in the RTC console.

> If this feature is enabled while the SDK is running, you must re\-initialize the engine for the configuration to take effect.

* Before sending out\-of\-room binary messages, you should call [login](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-login) first.

* After the user calls this API to send a binary message, he will receive an [onUserMessageSendResultOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onusermessagesendresultoutsideroom) callback to notify whether the message was sent successfully;

* If the binary message is sent successfully, the user specified by uid will receive the message through the [onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom) callback.

### sendServerMessage

```java
public abstract long com.ss.bytertc.engine.RTCEngine.sendServerMessage(String message)
```

The client side sends a text message to the application server (P2Server)

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|message |String |The content of the text message sent. The message does not exceed 64 KB. |

**Return Value**

* \> 0: Sent successfully, return the number of the sent message, increment from 1.

**Notes**

* Before calling this API, make sure you have enabled the [Advanced RTS functions](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode) in the RTC console.

> If this feature is enabled while the SDK is running, you must re\-initialize the engine for the configuration to take effect.

* Before sending a text message to the application server, you must first call [login](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-login) to complete the login, and then call [setServerParams](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setserverparams) Set up the application server.

* After calling this interface, you will receive an [onServerMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onservermessagesendresult) callback to inform the message sender whether the message was sent successfully.

* If the text message is sent successfully, the application server that previously called the [setServerParams](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setserverparams) setting will receive the message.

### sendServerBinaryMessage

```java
public abstract long com.ss.bytertc.engine.RTCEngine.sendServerBinaryMessage(byte[] buffer)
```

The client side sends binary messages to the application server (P2Server)

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|buffer |byte[] |Binary message content sent. Message does not exceed 64KB. |

**Return Value**

* \> 0: sent successfully, return the number of the sent message, increment from 1.

* \-1: Sending failed due to an empty message.

**Notes**

* Before calling this API, make sure you have enabled the [Advanced RTS functions](https://console.byteplus.com/rtc/cloudRTC?tab=RTSMode) in the RTC console.

> If this feature is enabled while the SDK is running, you must re\-initialize the engine for the configuration to take effect.

* Before sending a binary message to the application server, you must first call [login](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-login) to complete the login, and then call [setServerParams](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setserverparams) Set up the application server.

* After calling this interface, you will receive an [onServerMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onservermessagesendresult) callback to inform the message sender that the sending succeeded or failed;

* If the binary message is sent successfully, the application server that previously called the [setServerParams](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setserverparams) setting will receive the message.

### startNetworkDetection

```java
public abstract int com.ss.bytertc.engine.RTCEngine.startNetworkDetection(
    boolean isTestUplink,
    int expectedUplinkBitrate,
    boolean isTestDownlink,
    int expectedDownlinkBitrate
)
```

Enable pre\-call network detection

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|isTestUplink |boolean |Whether to detect uplink bandwidth |
|expectedUplinkBitrate |int |Expected uplink bandwidth in kbps, unit: kbps<br><br>Range: `{0, [100-10000]}`, `0`: Auto, that RTC will set the highest bitrate. |
|isTestDownlink |boolean |Whether to detect downlink bandwidth |
|expectedDownlinkBitrate |int |Expected downlink bandwidth in kbps, unit: kbps<br><br>Range: `{0, [100-10000]}`, `0`: Auto, that RTC will set the highest bitrate. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* After successfully calling this interface, you will receive [onNetworkDetectionResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onnetworkdetectionresult) within 3s and every 2s thereafter notifying the probe results;

* If the probe stops, you will receive [onNetworkDetectionStopped](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onnetworkdetectionstopped) to notify the probe to stop.

### stopNetworkDetection

```java
public abstract int com.ss.bytertc.engine.RTCEngine.stopNetworkDetection()
```

Stop pre\-call network probe

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* After calling this interface, you will receive an [onNetworkDetectionStopped](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onnetworkdetectionstopped) callback to notify the probe to stop.

### enableAudioFrameCallback

```java
public abstract int com.ss.bytertc.engine.RTCEngine.enableAudioFrameCallback(
    AudioFrameCallbackMethod method,
    AudioFormat format
)
```

Enable audio frames callback and set the format for the specified type of audio frames.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|method |AudioFrameCallbackMethod |Audio data callback method. See [AudioFrameCallbackMethod](https://docs.byteplus.com/en/docs/12/docs-70083#AudioFrameCallbackMethod).<br><br> <br><br>If `method` is set as `AUDIO_FRAME_CALLBACK_RECORD(0)`, `AUDIO_FRAME_CALLBACK_PLAYBACK(1)`, `AUDIO_FRAME_CALLBACK_MIXED(2)`, or `AUDIO_FRAME_CALLBACK_CAPTURE_MIXED(5)`, set `format` to the accurate value listed in the audio parameters format.<br><br> <br><br>If `method` is set as `AUDIO_FRAME_CALLBACK_REMOTE_USER(3)`, set `format` to `auto`. |
|format |AudioFormat |Audio parameters format. See [AudioFormat](https://docs.byteplus.com/en/docs/12/docs-70083#AudioFormat). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

After calling this API and [registerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-registeraudioframeobserver), [IAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioFrameObserver) will receive the corresponding audio data callback. However, these two APIs are independent of each other and the calling order is not restricted.

### disableAudioFrameCallback

```java
public abstract int com.ss.bytertc.engine.RTCEngine.disableAudioFrameCallback(AudioFrameCallbackMethod method)
```

Disables audio data callback.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|method |AudioFrameCallbackMethod |Audio data callback method. See [AudioFrameCallbackMethod](https://docs.byteplus.com/en/docs/12/docs-70083#AudioFrameCallbackMethod). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

Call this API after calling [enableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-enableaudioframecallback).

### registerAudioFrameObserver

```java
public abstract int com.ss.bytertc.engine.RTCEngine.registerAudioFrameObserver(IAudioFrameObserver observer)
```

Register an audio frame observer.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|observer |IAudioFrameObserver |Audio data callback observer. See [IAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioFrameObserver). Use `null` to cancel the registration. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

After calling this API and [enableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-enableaudioframecallback), [IAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioFrameObserver) receives the corresponding audio data callback. You can retrieve the audio data and perform processing on it without affecting the audio that RTC SDK uses to encode or render.

### registerAudioProcessor

```java
public abstract int com.ss.bytertc.engine.RTCEngine.registerAudioProcessor(IAudioFrameProcessor processor)
```

Register a custom audio preprocessor.

After that, you can call [enableAudioProcessor](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-enableaudioprocessor) to process the audio streams that are either captured locally or received from the remote side. RTC SDK then encodes or renders the processed data.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|processor |IAudioFrameProcessor |Custom audio processor. See [IAudioFrameProcessor](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioFrameProcessor)。<br><br> <br><br>SDK only holds weak references to the processor, you should guarantee its Life Time. To cancel registration, set the parameter to nullptr. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* When this interface is repeatedly called, only the last call takes effect.

* Refer to [Custom Audio Processing](https://docs.byteplus.com/en/byteplus-rtc/docs/80635) for more information.

### enableAudioProcessor

```java
public abstract int com.ss.bytertc.engine.RTCEngine.enableAudioProcessor(
    AudioProcessorMethod method,
    AudioFormat format
)
```

Enable audio frames callback for custom processing and set the format for the specified type of audio frames.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|method |AudioProcessorMethod |The types of audio frames. See [AudioProcessorMethod](https://docs.byteplus.com/en/docs/12/docs-70083#AudioProcessorMethod). Set this parameter to process multiple types of audio.<br><br> <br><br>With different values, you will receive the corresponding callback:<br><br><br> <br><br>* For locally captured audio, you will receive [onProcessRecordAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioFrameProcessor-onprocessrecordaudioframe).<br><br>* For mixed remote audio, you will receive [onProcessPlayBackAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioFrameProcessor-onprocessplaybackaudioframe).<br><br>* For audio from remote users, you will receive [onProcessRemoteUserAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioFrameProcessor-onprocessremoteuseraudioframe).<br><br>* For SDK\-level in\-ear monitoring audio, you will receive [onProcessEarMonitorAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioFrameProcessor-onprocessearmonitoraudioframe).<br><br>* For shared\-screen audio, you will receive [onProcessScreenAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioFrameProcessor-onprocessscreenaudioframe). |
|format |AudioFormat |The format of audio frames. See [AudioFormat](https://docs.byteplus.com/en/docs/12/docs-70083#AudioFormat). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* Before calling this API, call [registerAudioProcessor](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-registeraudioprocessor) to register a processor.

* To disable custom audio processing, call [disableAudioProcessor](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-disableaudioprocessor).

### disableAudioProcessor

```java
public abstract int com.ss.bytertc.engine.RTCEngine.disableAudioProcessor(AudioProcessorMethod method)
```

Disable custom audio processing.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|method |AudioProcessorMethod |Audio Frame type. See [AudioProcessorMethod](https://docs.byteplus.com/en/docs/12/docs-70083#AudioProcessorMethod). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

### registerLocalVideoProcessor

```java
public abstract int com.ss.bytertc.engine.RTCEngine.registerLocalVideoProcessor(
    IVideoProcessor processor,
    VideoPreprocessorConfig config
)
```

Set up a custom video preprocessor.

Using this video preprocessor, you can call [processVideoFrame](https://docs.byteplus.com/en/docs/12/14166#IVideoProcessor-processvideoframe) to preprocess the video frames collected by the RTC SDK, and use the processed video frames for RTC audio & video communication.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|processor |IVideoProcessor |Custom video processor. See [IVideoProcessor](https://docs.byteplus.com/en/docs/12/14166#IVideoProcessor). If null is passed in, the video frames captured by the RTC SDK are not preprocessed.<br><br> <br><br>SDK only holds weak references to the processor, you should guarantee its Life Time. |
|config |VideoPreprocessorConfig |Customize the settings applicable to the video preprocessor. See [VideoPreprocessorConfig](https://docs.byteplus.com/en/docs/12/docs-70083#VideoPreprocessorConfig).<br><br> <br><br>Currently, the required_pixel_format in'config 'only supports:' I420 ',' TEXTURE_2D 'and'Unknown':<br><br><br> <br><br>* When set to'Unknown', the RTC SDK gives the format of the video frame for processing by the processor, that is, the format of the capture.<br><br>   You can get the actual captured video frame format through [pixelFormat](https://docs.byteplus.com/en/docs/12/docs-70083#IVideoFrame-pixelformat). The supported formats are: 'I420', 'TEXTURE_2D' and 'TEXTURE_OES'<br><br>* When set to 'I420' or 'TEXTURE_2D', the RTC SDK will convert the captured video into the corresponding format for pre\-processing. This method call fails when set to another value. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

After preprocessing, the video frame format returned to the RTC SDK only supports' I420 'and' TEXTURE_2D '.

### setVideoDigitalZoomConfig

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setVideoDigitalZoomConfig(
    ZoomConfigType type,
    float size
)
```

> Available since 3.51

Set the step size for each digital zooming control to the local videos.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |ZoomConfigType |Required. Identifying which type the `size` is referring to. Refer to [ZoomConfigType](https://docs.byteplus.com/en/docs/12/docs-70083#ZoomConfigType). |
|size |float |Required. Reserved to three decimal places. It defaults to `0`.<br><br> <br><br>The meaning and range vary from different `type`s. If the scale or moving distance exceeds the range, the limit is taken as the result.<br><br><br> <br><br>* `kZoomFocusOffset`: Increment or decrease to the scaling factor. Range: [0, 7]. For example, when it is set to 0.5 and [setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideodigitalzoomcontrol) is called to zoom in, the scale will increase `0.5`. The scale ranges [1, 8] and defaults to `1`, which means an original size.<br><br>* `kZoomMoveOffset`：Ratio of the distance to the border of video images. It ranges [0, 0.5] and defaults to `0`, which means no offset. When you call [setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideodigitalzoomcontrol) and choose `CAMERA_MOVE_LEFT`, the moving distance is size x original width. While for the `CAMERA_MOVE_UP`, the moving distance is size x original height. Suppose that a video spans 1080 px and the `size` is set to `0.5` so that the distance would be 0.5 x 1080 px = 540 px. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* Only one size can be set for a single call. You must call this API to pass values respectively if you intend to set multiple `size`s.

* As the default `size` is `0`, you must call this API before performing any digital zoom control by calling [setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideodigitalzoomcontrol) or [startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startvideodigitalzoomcontrol).

### setVideoDigitalZoomControl

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setVideoDigitalZoomControl(ZoomDirectionType direction)
```

> Available since 3.51

Digital zoom or move the local video image once. This action affects both the video preview locally and the stream published.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|direction |ZoomDirectionType |Action of the digital zoom control. Refer to [ZoomDirectionType](https://docs.byteplus.com/en/docs/12/docs-70083#ZoomDirectionType). |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* As the default offset is `0`, you must call [setVideoDigitalZoomConfig](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideodigitalzoomconfig) before this API.

* You can only move video images after they are magnified via this API or [startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startvideodigitalzoomcontrol).

* When you request an out\-of\-range scale or movement, SDK will execute it with the limits. For example, when the image has been moved to the border, the image cannot be zoomed out, or has been magnified to 8x.

* Call [startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startvideodigitalzoomcontrol) to have a continuous and repeated digital zoom control.

* Refer to [setCameraZoomRatio](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setcamerazoomratio) if you intend to have an optical zoom control to the camera.

### startVideoDigitalZoomControl

```java
public abstract int com.ss.bytertc.engine.RTCEngine.startVideoDigitalZoomControl(ZoomDirectionType direction)
```

> Available since 3.51

Continuous and repeated digital zoom control. This action affects both the video preview locally and the stream published.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|direction |ZoomDirectionType |Action of the digital zoom control. Refer to [ZoomDirectionType](https://docs.byteplus.com/en/docs/12/docs-70083#ZoomDirectionType). |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* As the default offset is `0`, you must call [setVideoDigitalZoomConfig](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideodigitalzoomconfig) before this API.

* You can only move video images after they are magnified via this API or [setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideodigitalzoomcontrol).

* The control process stops when the scale reaches the limit, or the images have been moved to the border. If the next action exceeds the scale or movement range, SDK will execute it with the limits.

* Call [stopVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopvideodigitalzoomcontrol) to stop the ongoing zoom control.

* Call [setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideodigitalzoomcontrol) to have a one\-time digital zoom control.

* Refer to [setCameraZoomRatio](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setcamerazoomratio) if you intend to have an optical zoom control to the camera.

### stopVideoDigitalZoomControl

```java
public abstract int com.ss.bytertc.engine.RTCEngine.stopVideoDigitalZoomControl()
```

> Available since 3.51

Stop the ongoing digital zoom control instantly.

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

Refer to [startVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startvideodigitalzoomcontrol) for starting digital zooming.

### registerLocalEncodedVideoFrameObserver

```java
public abstract int com.ss.bytertc.engine.RTCEngine.registerLocalEncodedVideoFrameObserver(ILocalEncodedVideoFrameObserver observer)
```

Register a local video frame observer.

This method applies to both internal capturing and custom capturing.

After calling this API, SDK triggers [onLocalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70081#ILocalEncodedVideoFrameObserver-onlocalencodedvideoframe) whenever a video frame is captured.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|observer |ILocalEncodedVideoFrameObserver |Local video frame observer. See [ILocalEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70081#ILocalEncodedVideoFrameObserver). You can cancel the registration by setting it to `null`. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

You can call this API before or after entering the RTC room. Calling this API before entering the room ensures that video frames are monitored and callbacks are triggered as early as possible.

### registerRemoteEncodedVideoFrameObserver

```java
public abstract int com.ss.bytertc.engine.RTCEngine.registerRemoteEncodedVideoFrameObserver(IRemoteEncodedVideoFrameObserver observer)
```

Video data callback after registering remote encoding.

After registration, when the SDK detects a remote encoded video frame, it will trigger the [onRemoteEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IRemoteEncodedVideoFrameObserver-onremoteencodedvideoframe) callback

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|observer |IRemoteEncodedVideoFrameObserver |Remote encoded video data monitor. See [IRemoteEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70081#IRemoteEncodedVideoFrameObserver) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* See [Custom Video Encoding and Decoding](https://docs.byteplus.com/byteplus-rtc/docs/82921#custom-video-decoding) for more details about custom video decoding.

* This method applies to manual subscription mode and can be called either before or after entering the Room. It is recommended to call it before entering the room.

* The engine needs to be unregistered before it is destroyed. Call this method to set the parameter to "null".

### setVideoSourceType

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setVideoSourceType(VideoSourceType type)
```

Set the video source, including the screen recordings.

The internal video capture is the default, which refers to capturing video using the built\-in module.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |VideoSourceType |Video source type. Refer to [VideoSourceType](https://docs.byteplus.com/en/docs/12/docs-70083#VideoSourceType) for more details. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* You can call this API whether the user is in a room or not.

* Calling this API to switch to the custom video source will stop the enabled internal video capture.

* To switch to internal video capture, call this API to stop custom capture and then call [startVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startvideocapture) to enable internal video capture.

* To push custom encoded video frames to the SDK, call this API to switch `VideoSourceType` to `VIDEO_SOURCE_TYPE_ENCODED_WITH_SIMULCAST(2)` or `VIDEO_SOURCE_TYPE_ENCODED_WITHOUT_SIMULCAST(3)`.

### pushExternalVideoFrame

```java
public abstract int com.ss.bytertc.engine.RTCEngine.pushExternalVideoFrame(VideoFrameData frame)
```

Pushes external video frames.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|frame |VideoFrameData |The data information of the video frame |

**Return Value**

API call result:

* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for specific reasons.

**Notes**

* This method actively encapsulates the video frame data with the [VideoFrameData](https://docs.byteplus.com/en/docs/12/docs-70083#VideoFrameData) class and passes it to the SDK.

* Make sure that [setVideoSourceType](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideosourcetype) is set to custom video capture before you call this method.

* When using texture data, make sure eglContext in [createRTCEngine](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-creatertcengine) is sharedContext or the same as eglContext in frame, otherwise it will not be able to encode

* Support for raw data in I420, NV12, RGBA, and texture of Texture2D and TextureOES

### startPushMixedStream

```java
public abstract int com.ss.bytertc.engine.RTCEngine.startPushMixedStream(
    String taskId,
    MixedStreamPushTargetConfig pushTargetConfig,
    MixedStreamConfig mixedConfig
)
```

> Available since 3.60. Since version 3.60, this interface replaces the `startPushMixedStreamToCDN` and `startPushPublicStream` methods for the functions described below. If you have upgraded to version 3.60 or later and are still using these two methods, please migrate to this interface.

Specifies the streams to be mixed and initiates the task to push the mixed stream to CDN or WTN.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|taskId |String |Task ID. The length should not exceed 127 bytes.<br><br> <br><br>You may want to push more than one mixed stream to CDN from the same room. When you do that, use different ID for corresponding tasks; if you will start only one task, use an empty string.<br><br> <br><br>When `PushTargetType = 1` (WTN stream), this parameter is invalid. Pass an empty string. |
|pushTargetConfig |MixedStreamPushTargetConfig |Push target config, such as the push URL and WTN stream ID. See [MixedStreamPushTargetConfig](https://docs.byteplus.com/en/docs/12/docs-70083#MixedStreamPushTargetConfig). |
|mixedConfig |MixedStreamConfig |Configurations to be set when pushing streams to CDN or WTN. See [MixedStreamConfig](https://docs.byteplus.com/en/docs/12/docs-70083#MixedStreamConfig). |

**Return Value**

* 0: Success. You can get notified the result of the task and the events in the process of pushing the stream to CDN via [onMixedStreamEvent](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onmixedstreamevent).

* !0: Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* Subscribe to the Push\-to\-CDN and the WTN stream notifications in the [console](https://console.byteplus.com/rtc/cloudRTC?tab=callback) to receive notifications about task status changes. When calling this API repeatedly, subsequent calls to this API will trigger both [TranscodeStarted](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#transcodestarted) and [TranscodeUpdated](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#transcodeupdated) callbacks.

* Call [stopPushMixedStream](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stoppushmixedstream) to stop pushing streams to CDN.

* Call [updatePushMixedStream](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-updatepushmixedstream) to update part of the configurations of the task.

* Call [startPushSingleStream](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startpushsinglestream) to push a single stream to CDN.

### updatePushMixedStream

```java
public abstract int com.ss.bytertc.engine.RTCEngine.updatePushMixedStream(
    String taskId,
    MixedStreamPushTargetConfig pushTargetConfig,
    MixedStreamConfig mixedConfig
)
```

> Available since 3.60. Since version 3.60, this interface replaces the `updatePushMixedStreamToCDN` and `updatePublicStreamParam` methods for the functions described below. If you have upgraded to version 3.60 or later and are still using these two methods, please migrate to this interface.

Update the task configuration during the task started via [startPushMixedStream](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startpushmixedstream). You will be informed of the change via the [onMixedStreamEvent](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onmixedstreamevent) callback.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|taskId |String |Task ID. Specifies the task to be updated.<br><br>When [MixedStreamConfig](https://docs.byteplus.com/en/docs/12/docs-70083#MixedStreamConfig) is set to `PushTargetType = 0`, this ID is used to identify the task. |
|pushTargetConfig |MixedStreamPushTargetConfig |Push target config, such as the push url and WTN stream ID. See [MixedStreamPushTargetConfig](https://docs.byteplus.com/en/docs/12/docs-70083#MixedStreamPushTargetConfig). |
|mixedConfig |MixedStreamConfig |Configurations that you want to update. See [MixedStreamConfig](https://docs.byteplus.com/en/docs/12/docs-70083#MixedStreamConfig) for specific indications. You can update any property for the task unless it is specified as unavailable for updates.<br><br> <br><br>If you left some properties blank, you can expect these properties to be set to their default values. |

**Return Value**

* 0: Success.

* !0: Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

### stopPushMixedStream

```java
public abstract int com.ss.bytertc.engine.RTCEngine.stopPushMixedStream(
    String taskId,
    MixedStreamPushTargetType targetType
)
```

> Available since 3.60. Since version 3.60, this interface replaces the `stopPushStreamToCDN` method for stopping the push of mixed streams to CDN. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this interface.

Stops the task started via [startPushMixedStream](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startpushmixedstream).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|taskId |String |Task ID. Specifies of which pushing task you want to update the parameters. |
|targetType |MixedStreamPushTargetType |See [MixedStreamPushTargetType](https://docs.byteplus.com/en/docs/12/docs-70083#MixedStreamPushTargetType). |

**Return Value**

* 0: Success

* !0: Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

### startPushSingleStream

```java
public abstract int com.ss.bytertc.engine.RTCEngine.startPushSingleStream(
    String taskId,
    PushSingleStreamParam param
)
```

> Available since 3.60.

Pushes a single media stream to CDN or RTC room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|taskId |String |Task ID.<br><br> <br><br>You may want to start more than one task to push streams to CDN. When you do that, use different IDs for corresponding tasks; if you will start only one task, use an empty string. |
|param |PushSingleStreamParam |Configurations for pushing a single stream to CDN. See [PushSingleStreamParam](https://docs.byteplus.com/en/docs/12/docs-70083#PushSingleStreamParam). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* After calling this API, you will be informed of the result and errors during the pushing process with [onSingleStreamEvent](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onsinglestreamevent).

* Subscribe to the Push\-to\-CDN and the WTN stream notifications in the [console](https://console.byteplus.com/rtc/cloudRTC?tab=callback) to receive notifications about task status changes. When calling this API repeatedly, subsequent calls to this API will trigger both [TranscodeStarted](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#transcodestarted) and [TranscodeUpdated](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125#transcodeupdated) callbacks.

* Call [stopPushSingleStream](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stoppushsinglestream) to stop the task.

* Since this API does not perform encoding and decoding, the video stream pushed to RTMP will change according to the resolution, encoding method, and whether the camera on the publisher side is turned off.

### stopPushSingleStream

```java
public abstract int com.ss.bytertc.engine.RTCEngine.stopPushSingleStream(String taskId)
```

> Available since 3.60. Since version 3.60, this interface replaces the `stopPushStreamToCDN` method for stopping the push of single media streams to CDN. If you have upgraded to version 3.60 or later and are still using this method, please migrate to this interface.

Stops the task of pushing a single media stream to CDN started via [startPushSingleStream](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startpushsinglestream).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|taskId |String |Task ID. Specifies the task you want to stop. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

### setVideoCaptureConfig

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setVideoCaptureConfig(VideoCaptureConfig videoCaptureConfig)
```

Set the video capture parameters for internal capture of the RTC SDK.

If your project uses the SDK internal capture module, you can specify the video capture parameters including preference, resolution and frame rate through this interface.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|videoCaptureConfig |VideoCaptureConfig |Video capture parameters. See: [VideoCaptureConfig](https://docs.byteplus.com/en/docs/12/docs-70083#VideoCaptureConfig). |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* This API can be called after the engine is created. It is recommended to call this interface before calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startvideocapture).

* It is recommended that different Engines on the same device use the same video capture parameters.

* If you used the internal module to start video capture before calling this interface, the capture parameters default to Auto.

### setVideoEncoderConfig

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setVideoEncoderConfig(VideoEncoderConfig encoderConfig)
```

Sets the expected quality of the video stream by specifying the resolution, frame rate, bitrate, and the fallback strategy when the network is poor.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|encoderConfig |VideoEncoderConfig |See [VideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70083#VideoEncoderConfig). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* Since V3.61, this method can only set a single profile for the video stream. If you intend to publish the stream in multiple qualities, use [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setlocalsimulcastmode).

* Without calling this method, only one stream will be sent with a profile of 640px × 360px @15fps. The default encoding preference is frame rate\-first.

* If you use an external video source, you can also use this method to set the encoding parameters.

### setLocalSimulcastMode

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setLocalSimulcastMode(
    VideoSimulcastMode mode,
    VideoEncoderConfig[] streamConfig
)
```

> Available since 3.60.

Enable the Simulcast feature and configure the lower\-quality video streams settings.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mode |VideoSimulcastMode |Whether to publish lower\-quality streams and how many of them to be published. See [VideoSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-70083#VideoSimulcastMode). By default, it is set to Single, where the publisher sends the video in a single profile. In the other modes, the low\-quality stream is set to a default resolution of 160px × 90px with a bitrate of 50Kbps. |
|streamConfig |VideoEncoderConfig [] |The specification of the lower quality stream. You can configure up to three low\-quality streams for a video source. See [VideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70083#VideoEncoderConfig). The resolution of the lower quality stream must be smaller than the standard stream set via [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideoencoderconfig). The specifications in the array must be arranged in ascending order based on resolution.<br><br>In the other modes, the low\-quality stream is set to a default resolution of 160px × 90px with a bitrate of 50Kbps. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* The default specification of the video stream is 640px × 360px @15fps.

* The method applies to the camera video only.

* Refer to [Simulcasting](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70139) for more information.

### setLocalSimulcastMode

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setLocalSimulcastMode(VideoSimulcastMode mode)
```

> Available since 3.60.

Enable the Simulcast feature.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mode |VideoSimulcastMode |Whether to publish lower\-quality streams and how many of them to be published. See [VideoSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-70083#VideoSimulcastMode).<br><br>By default, it is set to Single, where the publisher sends the video in a single profile. In the other modes, the low\-quality stream is set to a default resolution of 160px × 90px with a bitrate of 50Kbps. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* Call this method before the user joins a room.

* The default specification of the video stream is 640px × 360px @15fps.

* If you intend to specify the lower\-quality streams, use setLocalSimulcastMode(VideoSimulcastMode mode, VideoEncoderConfig[] streamConfig).

* The method applies to the camera video only.

* Refer to [Simulcasting](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70139) for more information.

### setAudioSourceType

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setAudioSourceType(AudioSourceType type)
```

Switch the audio capture type.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |AudioSourceType |Audio input source type. See [AudioSourceType](https://docs.byteplus.com/en/docs/12/docs-70083#AudioSourceType)<br><br> <br><br>Use internal audio capture by default. The audio capture type and the audio render type may be different from each other. |

**Return Value**

Method call result:

* =0: Success.

* <0: Failure.

**Notes**

* You can call this API before or after joining the room.

* If you call this API to switch from internal audio capture to custom capture, the internal audio capture is automatically disabled. You must call [pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-pushexternalaudioframe) to push custom captured audio data to RTC SDK for transmission.

* If you call this API to switch from custom capture to internal capture, you must then call [startAudioCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startaudiocapture) to enable internal capture.

### setAudioRenderType

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setAudioRenderType(AudioRenderType type)
```

Switch the audio render type.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |AudioRenderType |Audio output source type. See [AudioRenderType](https://docs.byteplus.com/en/docs/12/docs-70083#AudioRenderType).<br><br> <br><br>Use internal audio render by default. The audio capture type and the audio render type may be different from each other. |

**Return Value**

Method call result:

* =0: Success.

* <0: Failure.

**Notes**

* You can call this API before or after joining the room.

* After calling this API to enable custom audio rendering, call [pullExternalAudioFrame](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-pullexternalaudioframe) for audio data.

### pushExternalAudioFrame

```java
public abstract int com.ss.bytertc.engine.RTCEngine.pushExternalAudioFrame(AudioFrame audioFrame)
```

Push custom captured audio data to the RTC SDK.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioFrame |AudioFrame |Audio data frame. See [AudioFrame](https://docs.byteplus.com/en/docs/12/docs-70083#AudioFrame)<br><br><br> <br><br>* The audio sampling format must be S16. The data format within the audio buffer must be PCM, and its capacity size should be audioFrame.samples × audioFrame.channel × 2.<br><br>* Specific sample rates and the number of channels must be designated; automatic settings are not supported. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* Before pushing external audio data, you must call [setAudioSourceType](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setaudiosourcetype) to enable custom audio capture.

* You must push custom captured audio data every 10 milliseconds. The samples (number of audio sampling points) of a single push should be `audioFrame.sample Rate/100`. For example, when the sampling rate is set to 48000, data of 480 sampling points should be pushed each time.

### pullExternalAudioFrame

```java
public abstract int com.ss.bytertc.engine.RTCEngine.pullExternalAudioFrame(AudioFrame audioFrame)
```

Pulls audio data for external playback.

After calling this method, the SDK will actively fetch the audio data to play, including the decoded and mixed audio data from the remote source, for external playback.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioFrame |AudioFrame |Audio data frame. See [AudioFrame](https://docs.byteplus.com/en/docs/12/docs-70083#AudioFrame) |

**Return Value**

Method call result

* 0: Setup succeeded

* < 0: Setup failed

**Notes**

* Before pulling external audio data, [setAudioRenderType](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setaudiorendertype) must be called Enable custom audio rendering.

* You should pull audio data every 10 milliseconds since the duration of a RTC SDK audio frame is 10 milliseconds. Samples x call frequency = audioFrame's sample rate. Assume that the sampling rate is set to 48000, call this API every 10 ms, so that 480 sampling points should be pulled each time.

* The audio sampling format is S16. The data format in the audio buffer is PCM data, and its capacity size is audioFrame.samples × audioFrame.channel × 2.

### pushReferenceAudioPCMData

```java
public abstract int com.ss.bytertc.engine.RTCEngine.pushReferenceAudioPCMData(AudioFrame audioFrame)
```

Push custom aec reference audio data to the RTC SDK.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioFrame |AudioFrame |Audio data frame. See [AudioFrame](https://docs.byteplus.com/en/docs/12/docs-70083#AudioFrame) |

**Return Value**

Method call result

* 0: Success

* <\-1: Failure

**Notes**

* `audioFrame` must include all playback audio signals that you expect AEC to remove, such as RTC playback and third\-party audio that is actually played by the device.

* Push one 10 ms audio frame every 10 ms from a stable thread. Keep the scheduling jitter within approximately 1 ms. The number of samples multiplied by the call frequency must equal `audioFrame`'s sample rate. For example, at a sample rate of 48000 Hz, push 480 samples per call.

* The audio sampling format is S16. The data format in the audio buffer is PCM data, and its capacity is `audioFrame.samples × audioFrame.channel × 2` bytes.

### createRTCRoom

```java
public abstract RTCRoom com.ss.bytertc.engine.RTCEngine.createRTCRoom(String roomId)
```

Create a RTCroom instance.

This API only returns a room instance. You still need to call [joinRoom](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-joinroom) to actually create/join the room.

Each call of this API creates one [RTCRoom](https://docs.byteplus.com/en/docs/12/14166#RTCRoom) instance. Call this API as many times as the number of rooms you need, and then call [joinRoom](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-joinroom) of each RTCRoom instance to join multiple rooms at the same time.

In multi\-room mode, a user can subscribe to media streams in the joined rooms at the same time.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|roomId |String |The string matches the regular expression: `[a-zA-Z0-9_\@\-\.]{1,128}`. |

**Return Value**

[RTCRoom](https://docs.byteplus.com/en/docs/12/14166#RTCRoom) instance.

If you get NULL instead of an RTCRoom instance, please ensure the roomId is valid and the specified room is not yet created.

**Notes**

* If the room that you wish to join already exists, you still need to call this API first to create the RTCRoom instance, and then call [joinRoom](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-joinroom).

* Do not create multiple rooms with the same roomId, otherwise the newly created room instance will replace the old one.

* To forward streams to the other rooms, call [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-startforwardstreamtorooms) instead of enabling Multi\-room mode.

### createRTSRoom

```java
public abstract RTSRoom com.ss.bytertc.engine.RTCEngine.createRTSRoom(String roomId)
```

Create a [RTSRoom](https://docs.byteplus.com/en/docs/12/14166#RTSRoom) instance.

This API only returns a room instance. You still need to call [joinRTSRoom](https://docs.byteplus.com/en/docs/12/14166#RTSRoom-joinrtsroom) to actually create/join the room.

Each call of this API creates one [RTSRoom](https://docs.byteplus.com/en/docs/12/14166#RTSRoom) instance. Call this API as many times as the number of rooms you need, and then call [joinRTSRoom](https://docs.byteplus.com/en/docs/12/14166#RTSRoom-joinrtsroom) of each RTSRoom instance to join multiple rooms at the same time.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|roomId |String |The string matches the regular expression: `[a-zA-Z0-9_\@\-\.]{1,128}`. |

**Return Value**

[RTSRoom](https://docs.byteplus.com/en/docs/12/14166#RTSRoom) instance.

If you get NULL instead of an RTSRoom instance, please ensure the roomId is valid and the specified room is not yet created.

**Notes**

* If the room that you wish to join already exists, you still need to call this API first to create the RTSRoom instance, and then call [joinRTSRoom](https://docs.byteplus.com/en/docs/12/14166#RTSRoom-joinrtsroom).

* Do not create multiple rooms with the same roomId, otherwise the newly created room instance will replace the old one.

### setPublishFallbackOption

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setPublishFallbackOption(PublishFallbackOption option)
```

Sets the fallback option for published audio & video streams.

You can call this API to set whether to automatically lower the resolution you set of the published streams under limited network conditions.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|option |PublishFallbackOption |Fallback option, see [PublishFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70083#PublishFallbackOption). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* This API only works after you call [setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setlocalsimulcastmode-2) to enable the mode of publishing multiple streams.

* You must call this API before entering the room.

* After calling this method, if there is a performance degradation or recovery due to poor performance or network conditions, the local end will receive early warnings through the [onPerformanceAlarms](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onperformancealarms) callback to adjust the capture device.

* After you allow video stream to fallback, your stream subscribers will receive [onSimulcastSubscribeFallback](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onsimulcastsubscribefallback) when the resolution of your published stream is lowered or restored.

* You can alternatively set fallback options with distributions from server side, which is of higher priority.

### setSubscribeFallbackOption

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setSubscribeFallbackOption(SubscribeFallbackOptions option)
```

Sets the fallback option for subscribed RTC streams.

You can call this API to set whether to lower the resolution of currently subscribed stream under limited network conditions.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|option |SubscribeFallbackOptions |Fallback option, see [SubscribeFallbackOptions](https://docs.byteplus.com/en/docs/12/docs-70083#SubscribeFallbackOptions) for more details. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* You must call this API before entering the room.

* After you enable the fallback, you will receive [onSimulcastSubscribeFallback](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onsimulcastsubscribefallback) and [onRemoteVideoSizeChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onremotevideosizechanged) when the resolution of your subscribed stream is lowered or restored.

* You can alternatively set fallback options with distributions from server side, which is of higher priority.

### setRemoteUserPriority

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setRemoteUserPriority(
    String roomid,
    String uid,
    RemoteUserPriority priority
)
```

Set user priority.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|roomid |String |Room ID |
|uid |String |The ID of the remote user. |
|priority |RemoteUserPriority |Priority for remote users. See enumeration type [RemoteUserPriority](https://docs.byteplus.com/en/docs/12/docs-70083#RemoteUserPriority). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* This method is used with [setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setsubscribefallbackoption).

* If the subscription flow fallback option is turned on, weak connections or insufficient performance will give priority to ensuring the quality of the flow received by high\-priority users.

* This method can be used before and after entering the room, and the priority of the remote user can be modified.

### setBusinessId

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setBusinessId(String businessId)
```

Sets the business ID

You can use businessId to distinguish different business scenarios. You can customize your businessId to serve as a sub AppId, which can share and refine the function of the AppId, but it does not need authentication.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|businessId |String |Your customized businessId<br><br> <br><br>BusinessId is a tag, and you can customize its granularity. |

**Return Value**

* 0: Success.

* \-2: The input is invalid. Legal characters include all lowercase letters, uppercase letters, numbers, and four other symbols, including '.', '\-','_', and '@'.

**Notes**

* You must call this API before entering the room, otherwise it will be invalid.

### setEncryptInfo

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setEncryptInfo(
    int aesType,
    String key
)
```

Sets the way to use built\-in encryption when transmitting.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|aesType |int |Encryption type. Optional parameters are 0, 1, 2, 3, and 4. The meaning is as follows:<br><br><br> <br><br>1. Not encrypted.<br><br>2. AES\-128\-CBC<br><br>3. AES\-256\-CBC<br><br>4. AES\-128\-ECB<br><br>5. AES\-256\-ECB |
|key |String |Encryption key. The length is limited to 36 bits, and the excess will be truncated |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* This method is mutually exclusive with [setCustomizeEncryptHandler](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setcustomizeencrypthandler), that is, according to the order of invocation, the last method called is the final version that takes effect.

* This method must be called before calling [joinRoom](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-joinroom). It can be called repeatedly, with the last called parameter as the effective parameter

* AES encryption algorithm limit, more than 36 bits of key will be truncated, only the first 36 bits

### setCustomizeEncryptHandler

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setCustomizeEncryptHandler(RTCEncryptHandler handler)
```

Sets custom encryption and decryption methods.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|handler |RTCEncryptHandler |The custom encryption handler needs to implement the encryption and decryption method inside. See [IRTCEncryptionHandler](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEncryptionHandler). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* This method and [setEncryptInfo](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setencryptinfo) are mutually exclusive, that is, according to Call order, the last method called is the final effective version

* This method must be called before entering the room, which can be called repeatedly, with the last called parameter as the effective parameter

* Whether encrypted or decrypted, the length of the modified data needs to be controlled under 180%. That is, if the input data is 100 bytes, the processed data must be less than 180 bytes. If the encryption or decryption result exceeds the limit, the audio & video frame may be discarded.

* Data encryption/decryption is performed serially, so depending on the implementation method, it may affect the final rendering efficiency. Whether to use this method needs to be carefully evaluated by the user

### getVideoEffectInterface

```java
public abstract IVideoEffect com.ss.bytertc.engine.RTCEngine.getVideoEffectInterface()
```

Gets video effect APIs.

**Return Value**

Video effect APIs. See [IVideoEffect](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect).

### enableEffectBeauty

```java
public abstract int com.ss.bytertc.engine.RTCEngine.enableEffectBeauty(boolean enable)
```

Enables/Disables basic beauty effects.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |boolean |Whether to enable basic beauty effects.<br><br><br> <br><br>* true: Enables basic beauty effects.<br><br>* false: (Default) Disables basic beauty effects. |

**Return Value**

* 0: Success.

* –1001: This method is not available for your current RTC SDK.

* \-12: This method is not available in the Audio SDK.

* <0: Failure. Effect SDK internal error. For specific error code, see [Error Code Table](https://docs.byteplus.com/effects/docs/error-code-table).

**Notes**

* You cannot use the basic beauty effects and the advanced effect features at the same time. See [how to use advanced effect features](https://docs.byteplus.com/byteplus-rtc/docs/114717) for more information.

* You need to integrate Effect SDK before calling this API. Effect SDK v4.4.2+ is recommended.

* Call [setBeautyIntensity](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setbeautyintensity) to set the beauty effect intensity. If you do not set the intensity before calling this API, the default intensity will be enabled. The default values for the intensity of each beauty mode are as follows: 0.7 for brightening, 0.8 for smoothing, 0.5 for sharpening, and 0.7 for clarity.

* This API is not applicable to screen capturing.

### setBeautyIntensity

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setBeautyIntensity(
    EffectBeautyMode beautyMode,
    float intensity
)
```

Sets the beauty effect intensity.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|beautyMode |EffectBeautyMode |Basic beauty effect. See [EffectBeautyMode](https://docs.byteplus.com/en/docs/12/docs-70083#EffectBeautyMode). |
|intensity |float |Beauty effect intensity in the range of [0,1]. When you set it to 0, the beauty effect will be turned off.<br><br> <br><br>The default values for the intensity of each beauty mode are as follows: 0.7 for brightening, 0.8 for smoothing, 0.5 for sharpening, and 0.7 for clarity. |

**Return Value**

* 0: Success.

* –2: `intensity` is out of range.

* –1001: This API is not available for your current RTC SDK.

* <0: Failure. Effect SDK internal error. For specific error code, see [error codes](https://docs.byteplus.com/effects/docs/error-code-table).

**Notes**

* If you call this API before calling [enableEffectBeauty](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-enableeffectbeauty), the default settings of beauty effect intensity will adjust accordingly.

* If you destroy the engine, the beauty effect settings will be invalid.

### setVideoOrientation

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setVideoOrientation(VideoOrientation orientation)
```

Sets the orientation of the video frame before custom video processing and encoding. The default value is `Adaptive`.

You should set the orientation to `Portrait` when using video effects or custom processing.

You should set the orientation to `Portrait` or `Landscape` when pushing a single stream to the CDN.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|orientation |VideoOrientation |Orientation of the video frame. See [VideoOrientation](https://docs.byteplus.com/en/docs/12/docs-70083#VideoOrientation). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* The orientation setting is only applicable to internal captured video sources. For custom captured video sources, setting the video frame orientation may result in errors, such as swapping width and height. Screen sources do not support video frame orientation setting.

* We recommend setting the orientation before joining the room. The updates to the encoding configuration and orientation are asynchronous; therefore, they can cause a brief preview malfunction if you change the orientation after joining the room.

### setRuntimeParameters

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setRuntimeParameters(JSONObject params)
```

Setting runtime parameters

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|params |JSONObject |Preserved parameters. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

Call this API before [joinRoom](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-joinroom) and [startAudioCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startaudiocapture).

### feedback

```java
public abstract int com.ss.bytertc.engine.RTCEngine.feedback(
    List<ProblemFeedbackOption> types,
    ProblemFeedbackInfo info
)
```

Report the user feedback to RTC.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|types |List<ProblemFeedbackOption\> |List of preset problems. See [ProblemFeedbackOption](https://docs.byteplus.com/en/docs/12/docs-70083#ProblemFeedbackOption) |
|info |ProblemFeedbackInfo |Specific description of other problems other than the preset problem, room's information. [ProblemFeedbackInfo](https://docs.byteplus.com/en/docs/12/docs-70083#ProblemFeedbackInfo) |

**Return Value**

* 0: Success.

* \-3: Failure.

**Notes**

If the user is in the room when reporting, the report is associated with the room or rooms where the user is currently located;

If the user is not in the room when reporting, the report leads to the previously exited Room.

### getNativeHandle

```java
public abstract long com.ss.bytertc.engine.RTCEngine.getNativeHandle()
```

Get [IRTCEngine](https://docs.byteplus.com/byteplus-rtc/docs/70095#irtcengine) in C++ layer.

**Return Value**

* \>0：Success. Return the address of `IRTCEngine` in C++ layer.

* \-1：Failure.

**Notes**

In some scenarios, getting and working with `IRTCEngine` in C++ layer has much higher execution efficiency than through the Java encapsulation layer. Typical scenarios include: custom processing of video/audio frames, encryption of audio and video calls, etc.

### startAudioRecording

```java
public abstract int com.ss.bytertc.engine.RTCEngine.startAudioRecording(AudioRecordingConfig config)
```

Starts recording audio communication and generates the local file.

If you call this API before or after joining the room without internal audio capture, then the recording task can still begin but the data will not be recorded in the local files. Only when you call [startAudioCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startaudiocapture) to enable internal audio capture, the data will be recorded in the local files.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|config |AudioRecordingConfig |See [AudioRecordingConfig](https://docs.byteplus.com/en/docs/12/docs-70083#AudioRecordingConfig). |

**Return Value**

* 0: Success

* \-2: Invalid parameters

* \-3: Not valid in this SDK. Please contact the technical support.

**Notes**

* All audio effects are valid in the file. Mixed audio file is not included in the file.

* Call [stopAudioRecording](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopaudiorecording) to stop recording.

* You can call this API before and after joining the room. If this API is called before you join the room, you need to call [stopAudioRecording](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopaudiorecording) to stop recording. If this API is called after you join the room, the recording task ends automatically. If you join multiple rooms, audio from all rooms is recorded in one file.

* After calling the API, you'll receive [onAudioRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onaudiorecordingstateupdate).

### stopAudioRecording

```java
public abstract int com.ss.bytertc.engine.RTCEngine.stopAudioRecording()
```

Stop audio recording.

**Return Value**

* 0: Success

* <0: Failure

**Notes**

Call [startAudioRecording](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startaudiorecording) to start the recording task.

### getAudioEffectPlayer

```java
public abstract IAudioEffectPlayer com.ss.bytertc.engine.RTCEngine.getAudioEffectPlayer()
```

> Available since 3.53

Create an instance for audio effect player.

**Return Value**

See [IAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer).

### getMediaPlayer

```java
public abstract IMediaPlayer com.ss.bytertc.engine.RTCEngine.getMediaPlayer(int playerId)
```

> Available since 3.53

Create a media player instance.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|playerId |int |Media player id. The range is `[0, 3]`. You can create up to 4 instances at the same time. If it exceeds the range, nullptr will be returned. |

**Return Value**

Media player instance. See [IMediaPlayer](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer).

### setScreenAudioSourceType

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setScreenAudioSourceType(AudioSourceType sourceType)
```

Sets the screen audio source type. (internal capture/custom capture)

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|sourceType |AudioSourceType |Screen audio source type. See [AudioSourceType](https://docs.byteplus.com/en/docs/12/docs-70083#AudioSourceType). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* The default screen audio source type is RTC SDK internal capture.

* You should call this API before calling publishScreenAudio. Otherwise, you will receive [onWarning](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onwarning) with 'WARNING_CODE_SET_SCREEN_AUDIO_SOURCE_TYPE_FAILED'.

* When using internal capture, you need to call startScreenCapture to start capturing. After that, as you switch to an external source by calling this API, the internal capture will stop.

* When using custom capture, you need to call [pushScreenAudioFrame](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-pushscreenaudioframe) to push the audio stream to the RTC SDK.

* Whether you use internal capture or custom capture, you must call publishScreenAudio to publish the captured screen audio stream.

### pushScreenAudioFrame

```java
public abstract int com.ss.bytertc.engine.RTCEngine.pushScreenAudioFrame(AudioFrame audioFrame)
```

Using a custom capture method, when capturing screen audio during screen sharing, push the audio frame to the RTC SDK for encoding and other processing.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioFrame |AudioFrame |Audio data frame. See [AudioFrame](https://docs.byteplus.com/en/docs/12/docs-70083#AudioFrame) |

**Return Value**

Method call result

* 0: Setup succeeded.

* < 0: Setup failed. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* Before calling this API to push custom collected audio data, you must call [setScreenAudioSourceType](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setscreenaudiosourcetype) to start custom capture of the screen audio.

* You should call this method every 10 milliseconds to push a custom captured audio frame. A push audio frame should contain frame.sample_rate/100 audio sample points. For example, if the sampling rate is 48000Hz, 480 sampling points should be pushed each time.

* The audio sampling format is S16. The data format in the audio buffer must be PCM data, and its capacity size should be samples × frame.channel × 2.

* After calling this interface to push the custom captured audio frame to the RTC SDK, you must call publishScreenAudio to push the captured screen audio to the remote end. Audio frame information pushed to the RTC SDK is lost before calling publishScreenAudio.

### setExternalVideoEncoderEventHandler

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setExternalVideoEncoderEventHandler(IExternalVideoEncoderEventHandler handler)
```

Register custom coded frame push event callback

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|handler |IExternalVideoEncoderEventHandler |Custom coded frame callback class. See [IExternalVideoEncoderEventHandler](https://docs.byteplus.com/en/docs/12/docs-70081#IExternalVideoEncoderEventHandler) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* This method needs to be called before entering the room.

* The engine needs to be unregistered before it is destroyed. Call this method to set the parameter to "null".

### setEarMonitorMode

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setEarMonitorMode(EarMonitorMode mode)
```

Enables/disables in\-ear monitoring.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mode |EarMonitorMode |Whether to enable in\-ear monitoring. See [EarMonitorMode](https://docs.byteplus.com/en/docs/12/docs-70083#EarMonitorMode). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* In\-ear monitoring is effective for audio captured by the RTC SDK.

* We recommend that you use wired earbuds/headphones for a low\-latency experience.

* The RTC SDK supports both hardware\-level and SDK\-level in\-ear monitoring. Hardware\-level monitoring typically offers lower latency and better audio quality. If your App is in the manufacturer's trusted list for this feature and the environment meets the required conditions, the RTC SDK will automatically default to hardware\-level in\-ear monitoring when enabled.

### setEarMonitorMode

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setEarMonitorMode(
    EarMonitorMode mode,
    int filter
)
```

> Available since 3.60.

Enables/disables in\-ear monitoring and controls whether to apply local audio processing to the in\-ear monitoring audio.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mode |EarMonitorMode |Whether to enable in\-ear monitoring. See [EarMonitorMode](https://docs.byteplus.com/en/docs/12/docs-70083#EarMonitorMode). Defaults to off. |
|filter |int |Whether to apply local audio processing to the in\-ear monitoring audio. See [EarMonitorAudioFilter](https://docs.byteplus.com/en/docs/12/docs-70083#EarMonitorAudioFilter). Defaults to no audio processing. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* In\-ear monitoring is effective for audio captured by the RTC SDK.

* We recommend that you use wired earbuds/headphones for a low\-latency experience.

* The RTC SDK supports both hardware\-level and SDK\-level in\-ear monitoring. Hardware\-level monitoring typically offers lower latency and better audio quality. If your App is in the manufacturer's trusted list for this feature and the environment meets the required conditions, the RTC SDK will automatically default to hardware\-level in\-ear monitoring when enabled.

### setEarMonitorVolume

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setEarMonitorVolume(int volume)
```

Set the monitoring volume.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |int |The monitoring volume with the adjustment range between 0% and 100%. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* Call [setEarMonitorMode](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setearmonitormode) before setting the volume.

### enableAudioPropertiesReport

```java
public abstract int com.ss.bytertc.engine.RTCEngine.enableAudioPropertiesReport(AudioPropertiesConfig config)
```

Enable audio information prompts. After that, you will receive [onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onlocalaudiopropertiesreport), [onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onremoteaudiopropertiesreport), and [onActiveSpeaker](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onactivespeaker).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|config |AudioPropertiesConfig |See [AudioPropertiesConfig](https://docs.byteplus.com/en/docs/12/docs-70083#AudioPropertiesConfig) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

### sendStreamSyncInfo

```java
public abstract int com.ss.bytertc.engine.RTCEngine.sendStreamSyncInfo(
    byte[] data,
    StreamSyncInfoConfig config
)
```

Send audio stream synchronization information. The message is sent to the remote end through the audio stream and synchronized with the audio stream. After the API is successfully called, the remote user will receive a [onStreamSyncInfoReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onstreamsyncinforeceived) callback.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|data |byte[] |Message content. |
|config |StreamSyncInfoConfig |Configuration related to audio stream synchronization information. See [StreamSyncInfoConfig](https://docs.byteplus.com/en/docs/12/docs-70083#StreamSyncInfoConfig). |

**Return Value**

* \> = 0: Message sent successfully. Returns the number of successful sends.

* \-1: Message sending failed. Message length greater than 16 bytes.

* \-2: Message sending failed. The content of the incoming message is empty.

* \-3: Message sending failed. This screen stream was not published when the message was synchronized through the screen stream.

* \-4: Message sending failed. This audio stream is not yet published when you synchronize messages with an audio stream captured by a microphone or custom device, as described in [ErrorCode](https://docs.byteplus.com/en/docs/12/docs-70082#ErrorCode).

**Notes**

* Regarding the frequency, we recommend no more than 50 calls per second.

* When using `CHANNEL_PROFILE_INTERACTIVE_PODCAST` as room profile, the data will be delivered. For other room profiles, the data may be lost when the local user is muted.

### isCameraTorchSupported

```java
public abstract boolean com.ss.bytertc.engine.RTCEngine.isCameraTorchSupported()
```

Detect whether the currently used camera (front/rear) supports flash.

**Return Value**

* true: Support

* false: Not supported

**Notes**

You must have called [startVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startvideocapture) for video capture using the SDK internal capture module to detect flash capability.

### isCameraZoomSupported

```java
public abstract boolean com.ss.bytertc.engine.RTCEngine.isCameraZoomSupported()
```

Detect whether the currently used camera (front/rear) supports zoom (digital/optical zoom).

**Return Value**

* true: Support

* false: Not supported

**Notes**

Camera zoom capability can only be detected if [startVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startvideocapture) is used for video capture using the SDK internal capture module.

### setCameraZoomRatio

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setCameraZoomRatio(float zoom)
```

Change the optical zoom magnification.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|zoom |float |Zoom magnification of the currently used camera (front/rear). The value range is [1, < Maximum Zoom Multiplier \>].<br><br> <br><br>The maximum zoom factor can be obtained by calling [getCameraZoomMaxRatio](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-getcamerazoommaxratio). |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* The camera zoom factor can only be set when [startVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startvideocapture) is called for video capture using the SDK internal capture module.

* The setting result fails after calling [stopVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopvideocapture) to turn off internal collection.

* Call [setVideoDigitalZoomConfig](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideodigitalzoomconfig) to set digital zoom. Call [setVideoDigitalZoomControl](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideodigitalzoomcontrol) to perform digital zoom.

### getCameraZoomMaxRatio

```java
public abstract float com.ss.bytertc.engine.RTCEngine.getCameraZoomMaxRatio()
```

Get the maximum zoom factor of the currently used camera (front/rear)

**Return Value**

Maximum zoom factor

**Notes**

You must have called [startVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startvideocapture) using the SDK internal capture module for video capture, the maximum zoom factor of the camera can be detected.

### setCameraTorch

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setCameraTorch(TorchState torchState)
```

Turn on/off the flash state of the currently used camera (front/rear)

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|torchState |TorchState |Flash state. Refer to [TorchState](https://docs.byteplus.com/en/docs/12/docs-70083#TorchState) |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* The flash can only be set if you have called [startVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startvideocapture) for video capture using the SDK internal capture module.

* The setting result fails after calling [stopVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopvideocapture) to turn off internal collection.

### isCameraFocusPositionSupported

```java
public abstract boolean com.ss.bytertc.engine.RTCEngine.isCameraFocusPositionSupported()
```

Checks if manual focus is available for the currently used camera.

**Return Value**

* true: Available.

* false: Unavailable.

**Notes**

You must call [startVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startvideocapture) to start SDK internal video capturing before calling this API.

### setCameraFocusPosition

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setCameraFocusPosition(
    float x,
    float y
)
```

Sets the manual focus position for the currently used camera.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|x |float |The x\-coordinate of the focus point in the range of [0, 1]. The upper\-left corner of the canvas is set as the origin. |
|y |float |The y\-coordinate of the focus point in the range of [0, 1]. The upper\-left corner of the canvas is set as the origin. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* You must call [startVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startvideocapture) to start SDK internal video capturing, and use SDK internal rendering before calling this API.

* The focus point setting will be canceled when you move the device.

* The camera focus point setting will be invalid after calling [stopVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopvideocapture) to stop internal capturing.

### isCameraExposurePositionSupported

```java
public abstract boolean com.ss.bytertc.engine.RTCEngine.isCameraExposurePositionSupported()
```

Checks if manual exposure setting is available for the currently used camera.

**Return Value**

* true: Available.

* false: Unavailable.

**Notes**

You must call [startVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startvideocapture) to start SDK internal video capturing before calling this API.

### setCameraExposurePosition

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setCameraExposurePosition(
    float x,
    float y
)
```

Sets the manual exposure position for the currently used camera.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|x |float |The x\-coordinate of the exposure point in the range of [0, 1]. The upper\-left corner of the canvas is set as the origin. |
|y |float |The y\-coordinate of the focus point in the range of [0, 1]. The upper\-left corner of the canvas is set as the origin. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* You must call [startVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startvideocapture) to start SDK internal video capturing, and use SDK internal rendering before calling this API.

* The exposure point setting will be canceled when you move the device.

* The camera exposure point setting will be invalid after calling [stopVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopvideocapture) to stop internal capturing.

### setCameraExposureCompensation

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setCameraExposureCompensation(float val)
```

Sets the exposure compensation for the currently used camera.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|val |float |Exposure compensation in the range of [\-1, 1]. Default to 0, which means no exposure compensation. |

**Return Value**

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* You must call [startVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startvideocapture) to start SDK internal video capturing, and use SDK internal rendering before calling this API.

* The camera exposure compensation setting will be invalid after calling [stopVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopvideocapture) to stop internal capturing.

### enableCameraAutoExposureFaceMode

```java
public abstract int com.ss.bytertc.engine.RTCEngine.enableCameraAutoExposureFaceMode(boolean enable)
```

> Available since 353

Enable or disable face auto exposure mode during internal video capture. This mode fixes the problem that the face is too dark under strong backlight; but it will also cause the problem of too bright/too dark in the area outside the ROI region.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|enable |boolean |Whether to enable the mode. True by default for iOS, False by default for Android. |

**Return Value**

* 0: Success.

* < 0: Failure.

**Notes**

You must call this API before calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startvideocapture) to enable internal capture to make the setting valid.

### setCameraAdaptiveMinimumFrameRate

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setCameraAdaptiveMinimumFrameRate(int framerate)
```

> Available since 353

Set the minimum frame rate of the dynamic framerate mode during internal video capture.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|framerate |int |The minimum value in fps. The default value is 7.<br><br> <br><br>The maximum value of the dynamic framerate mode is set by calling [setVideoCaptureConfig](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideocaptureconfig). When minimum value exceeds the maximum value, the frame rate is set to a fixed value as the maximum value; otherwise, dynamic framerate mode is enabled. |

**Return Value**

* 0: Success.

* !0: Failure.

**Notes**

* You must call this API before calling [startVideoCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startvideocapture) to enable internal capture to make the setting valid.

* If the maximum frame rate changes due to performance degradation, static adaptation, etc., the set minimum frame rate value will be re\-compared with the new maximum value. Changes in comparison results may cause switch between fixed and dynamic frame rate modes.

* For Android, dynamic framerate mode is enabled.

* For iOS, dynamic framerate mode is disabled.

### enableAlphaChannelVideoEncode

```java
public abstract int com.ss.bytertc.engine.RTCEngine.enableAlphaChannelVideoEncode(AlphaLayout alphaLayout)
```

> Available since 3.58

Enables the Alpha channel encoding feature for custom captured video frames.

Suitable for scenarios where the video subject and background need to be separated at the push stream end, and the background can be custom rendered at the pull stream end.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|alphaLayout |AlphaLayout |The relative position of the separated Alpha channel to the RGB channel information. Currently, only AlphaLayout.TOP is supported, which means it is placed above the RGB channel information. |

**Return Value**

Method call result:

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* This API only applies to custom captured video frames that use the RGBA color model, including VideoPixelFormat.TEXTURE_2D, VideoPixelFormat.TEXTURE_OES, VideoPixelFormat.RGBA.

* This API must be called before publishing the video stream.

* After calling this API to enable Alpha channel encoding, you must call [pushExternalVideoFrame](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-pushexternalvideoframe) to push the custom captured video frames to the RTC SDK. If a video frame format that is not supported is pushed, calling [pushExternalVideoFrame](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-pushexternalvideoframe) will return the error code ReturnStatus.RETURN_STATUS_PARAMETER_ERR.

### disableAlphaChannelVideoEncode

```java
public abstract int com.ss.bytertc.engine.RTCEngine.disableAlphaChannelVideoEncode()
```

> Available since 3.58

Disables the Alpha channel encoding feature for externally captured video frames.

**Return Value**

Method call result:

* 0: Success.

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

This API must be called after stopping the publish of the video stream.

### sendSEIMessage

```java
public abstract int com.ss.bytertc.engine.RTCEngine.sendSEIMessage(
    byte[] message,
    int repeatCount,
    SEICountPerFrame mode
)
```

Sends SEI data.

In a video call scenario, SEI is sent with the video frame, while in a voice call scenario, SDK will automatically publish a black frame with a resolution of 16 × 16 pixels to carry SEI data.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|message |byte[] |SEI data. No more than 4 KB SEI data per frame is recommended. |
|repeatCount |int |Number of times a message is sent repeatedly. The value range is [0, max{29, %{video frame rate}\-1}]. Recommended range: [2,4].<br><br> <br><br>After calling this API, the SEI data will be added to a consecutive `\%{repeatCount}+1` number of video frames starting from the current frame. |
|mode |SEICountPerFrame |SEI sending mode. See [SEICountPerFrame](https://docs.byteplus.com/en/docs/12/docs-70083#SEICountPerFrame). |

**Return Value**

* \>= 0: The number of SEIs to be added to the video frame

* < 0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* We recommend the number of SEI messages per second should not exceed the current video frame rate. In a voice call, the blank\-frame rate is 15 fps.

* In a voice call, this API can be called to send SEI data only in internal capture mode.

* In a video call, the custom captured video frame can also be used for sending SEI data if the original video frame contains no SEI data, otherwise calling this method will not take effect.

* Each video frame carriess only the SEI data received within 2s before and after. In a voice call scenario, if no SEI data is sent within 1min after calling this API, SDK will automatically cancel publishing black frames.

* After the message is sent successfully, the remote user who subscribed your video stream will receive [onSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onseimessagereceived).

* When you switch from a voice call to a video call, SEI data will automatically start to be sent with normally captured video frames instead of black frames.

### sendLivePushSEIMessage

```java
public abstract int com.ss.bytertc.engine.RTCEngine.sendLivePushSEIMessage(
    String jsonString,
    int count,
    boolean isKeyFrameOnly,
    boolean allowOverwrite
)
```

Sends SEI data in Key\-Value format through video frames.

Before calling this API, you must call [setLiveMode](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-setlivemode) and set the room live mode to `LIVE_MODE_SOLO_HOST`.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|jsonString |String |JSON formatted key\-value pairs, for example, `{"key1":"value1","key2":"value2"}`:<br><br><br>* If a key has an empty value (e.g., `""` or `null`), that key will be deleted from the SEI dictionary.<br><br>* Total size of merged SEI data must not exceed 10 KB. |
|count |int |The number of times this SEI data is continuously sent.<br><br><br>* When `isKeyFrameOnly` is true, it means sending with `count` keyframes (I\-frames);<br><br>* When `isKeyFrameOnly` is false, it means sending with `count` video frames. |
|isKeyFrameOnly |boolean |Whether to send SEI only with keyframes (I\-frames):<br><br><br>* true: Send only with keyframes.<br><br>* false: Send with all frames. |
|allowOverwrite |boolean |whether subsequent requests are allowed to overwrite the value of this key:<br><br><br>* true: Subsequent requests can overwrite the key's value, and the `count` will also be updated to the new value;<br><br>* false: Subsequent requests will ignore any new value for this key and keep the original value. For an existing key, whether this write is allowed depends on the overwrite policy previously saved for that key. |

**Return Value**

* 0: Success.

* < 0: Failure.

* \-1: Video module not enabled.

* \-2: Parameter error (empty JSON or count <= 0).

* \-3: Invalid JSON format.

* \-4: Total SEI data size exceeds limit.

### startFileRecording

```java
public abstract int com.ss.bytertc.engine.RTCEngine.startFileRecording(
    RecordingConfig config,
    RecordingType recordingType
)
```

This method records the audio & video data during the call to a local file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|config |RecordingConfig |Local recording parameter configuration. See [RecordingConfig](https://docs.byteplus.com/en/docs/12/docs-70083#RecordingConfig) |
|recordingType |RecordingType |Locally recorded media type, see [RecordingType](https://docs.byteplus.com/en/docs/12/docs-70083#RecordingType)<br><br> <br><br>Note: Screen stream only supports recording video (RECORD_VIDEO_ONLY); Main stream supports recording all types. |

**Return Value**

0: Normal

\-1: Parameter setting exception

\-2: The current version of the SDK does not support this feature, please contact technical support staff

**Notes**

* You must join a room before calling this method.

* When you use this method, you get an [onRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onrecordingstateupdate) callback.

* If the recording is normal, the system will notify the recording progress through the [onRecordingProgressUpdate](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onrecordingprogressupdate) callback every second.

### stopFileRecording

```java
public abstract int com.ss.bytertc.engine.RTCEngine.stopFileRecording()
```

Stop local recording

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* Call [startFileRecording](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startfilerecording) After starting local recording, you must call this method to stop recording.

* After calling this method, you will receive an [onRecordingStateUpdate](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onrecordingstateupdate) callback prompting you to record the result.

### pushExternalEncodedVideoFrame

```java
public abstract int com.ss.bytertc.engine.RTCEngine.pushExternalEncodedVideoFrame(
    int videoIndex,
    RTCEncodedVideoFrame encodedVideoFrame
)
```

Push a custom encoded video stream

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|videoIndex |int |The corresponding encoded stream subscript, starting from 0, if the call [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideoencoderconfig) sets multiple streams, the number here must be consistent with it |
|encodedVideoFrame |RTCEncodedVideoFrame |Encoded video stream frame information. See [RTCEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70083#RTCEncodedVideoFrame). |

**Return Value**

API call result:

* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for specific reasons.

**Notes**

* Currently, only video frames in H264 and ByteVC1 formats are supported, and the video stream protocol must be in an Annex B format.

* This function runs within the user calling thread

* Before pushing a custom encoded video frame, you must call [setVideoSourceType](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideosourcetype) to switch the video input source to the custom encoded video source.

### startScreenCapture

```java
public abstract int com.ss.bytertc.engine.RTCEngine.startScreenCapture(
    ScreenMediaType type,
    Intent mediaProjectionResultData
)
```

The RTC SDK starts capturing the screen audio and/or video stream internally.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |ScreenMediaType |Media type. See [ScreenMediaType](https://docs.byteplus.com/en/docs/12/docs-70083#ScreenMediaType) |
|mediaProjectionResultData |Intent |The Intent obtained after applying for screen sharing permission from the Android device. See [getMediaProjection](https://developer.android.com/reference/android/media/projection/MediaProjectionManager#getMediaProjection). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* The call of this API takes effects only when you are using RTC SDK to record screen. You will get a warning by [onVideoDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onvideodevicewarning) or [onAudioDeviceWarning](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onaudiodevicewarning) after calling this API when the source is set to an external recorder.

* After capturing, you need to call [publishStreamAudio](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-publishstreamaudio) and/or [publishStreamVideo](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-publishstreamvideo) to push to the remote end.

* You will receive [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onvideodevicestatechanged) and [onAudioDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onaudiodevicestatechanged) when the capturing is started.

* To stop capturing, call [stopScreenCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopscreencapture).

### updateScreenCapture

```java
public abstract int com.ss.bytertc.engine.RTCEngine.updateScreenCapture(ScreenMediaType type)
```

Updates the media type of the internal screen capture.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |ScreenMediaType |Media type. See [ScreenMediaType](https://docs.byteplus.com/en/docs/12/docs-70083#ScreenMediaType). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

Call this API after calling [startScreenCapture](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startscreencapture).

### stopScreenCapture

```java
public abstract int com.ss.bytertc.engine.RTCEngine.stopScreenCapture()
```

### setVideoWatermark

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setVideoWatermark(
    String imagePath,
    RTCWatermarkConfig watermarkConfig
)
```

Adds a watermark to the designated video stream.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|imagePath |String |File path of the watermark image. You can use the absolute path, the asset path(/assets/xx.png), or the URI path(content://). The path should be less than 512 bytes.<br><br> <br><br>The watermark image should be in PNG or JPG format. |
|watermarkConfig |RTCWatermarkConfig |Watermark configurations. See [RTCWatermarkConfig](https://docs.byteplus.com/en/docs/12/docs-70083#RTCWatermarkConfig). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* Call [clearVideoWatermark](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-clearvideowatermark) to remove the watermark on the designated video stream.

* You can only add one watermark to one video stream. The newly added watermark replaces the previous one. You can call this API multiple times to add watermarks to different streams.

* You can call this API before and after joining room.

* If you mirror the preview, or the preview and the published stream, the watermark will also be mirrored locally, but the published watermark will not be mirrored.

* When you enable simulcast mode, the watermark will be added to all video streams, and it will scale down to smaller encoding configurations accordingly.

### clearVideoWatermark

```java
public abstract int com.ss.bytertc.engine.RTCEngine.clearVideoWatermark()
```

Removes video watermark from designated video stream.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

### setDummyCaptureImagePath

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setDummyCaptureImagePath(String filePath)
```

Set an alternative image when the local internal video capture is not enabled.

When you call `stopVideoCapture`, an alternative image will be pushed. You can set the path to null or open the camera to stop publishing the image.

You can repeatedly call this API to update the image.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|filePath |String |Set the path of the static image.<br><br> <br><br>You can use the absolute path (file://xxx) or the asset directory path (/assets/xx.png). The maximum size for the path is 512 bytes.<br><br> <br><br>You can upload a .JPG, .JPEG, .PNG, or .BMP file.<br><br> <br><br>When the aspect ratio of the image is inconsistent with the video encoder configuration, the image will be proportionally resized, with the remaining pixels rendered black. The framerate and the bitrate are consistent with the video encoder configuration. |

**Return Value**

* 0: Success.

* \-2: Failure. Ensure that the filePath is valid.

* \-12: This method is not available in the Audio SDK.

**Notes**

* The API is only effective when publishing an internally captured video.

* You cannot locally preview the image.

* You can call this API before and after joining an RTC room. In the multi\-room mode, the image can be only displayed in the room you publish the stream.

* You cannot apply effects like filters and mirroring to the image, while you can watermark the image.

* The image is not effective for a screen\-sharing stream.

* When you enable the simulcast mode, the image will be added to all video streams, and it will be proportionally scaled down to smaller encoding configurations.

### takeLocalSnapshot

```java
public abstract long com.ss.bytertc.engine.RTCEngine.takeLocalSnapshot(ISnapshotResultCallback callback)
```

Take a snapshot of the local video.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|callback |ISnapshotResultCallback |See [ISnapshotResultCallback](https://docs.byteplus.com/en/docs/12/docs-70081#ISnapshotResultCallback). |

**Return Value**

The index of the local snapshot task, starting from `1`.

**Notes**

* The snapshot is taken with all video effects on, like rotation, and mirroring.

* You can take the snapshot either using SDK internal video capture or customized capture.

### takeRemoteSnapshot

```java
public abstract long com.ss.bytertc.engine.RTCEngine.takeRemoteSnapshot(
    String streamId,
    ISnapshotResultCallback callback
)
```

Takes a snapshot of the local video.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |String |The streamId of the remote user. |
|callback |ISnapshotResultCallback |See [ISnapshotResultCallback](https://docs.byteplus.com/en/docs/12/docs-70081#ISnapshotResultCallback). |

**Return Value**

The index of the local snapshot task, starting from `1`.

**Notes**

* The snapshot is taken with all video effects on, like rotation, and mirroring.

* You can take the snapshot either using SDK internal video capture or customized capture.

### takeRemoteSnapshotToFile

```java
public abstract long com.ss.bytertc.engine.RTCEngine.takeRemoteSnapshotToFile(
    String streamId,
    String filePath
)
```

Takes a snapshot of the remote video stream and saves it as a JPG file at the specified local path.

After calling this method, the SDK triggers [onRemoteSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onremotesnapshottakentofile) to report whether the snapshot is taken successfully and provide details of the snapshot image.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |String |ID of the remote video stream. |
|filePath |String |The absolute file path where the snapshot JPG file will be saved. The file extension must be `.jpg`. Ensure that the directory exists and is writable. Example: `/sdcard/Pictures/snapshot.jpg`. |

**Return Value**

The index of the remote snapshot task, starting from `1`. The index can be used to track the task status or perform other management operations.

### takeLocalSnapshotToFile

```java
public abstract long com.ss.bytertc.engine.RTCEngine.takeLocalSnapshotToFile(String filePath)
```

Takes a snapshot of the local/remote video stream and saves it as a JPG file at the specified local path.

After calling this method, the SDK triggers [onLocalSnapshotTakenToFile](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onlocalsnapshottakentofile) to report whether the snapshot is taken successfully and provide details of the snapshot image.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|filePath |String |The absolute file path where the snapshot JPG file will be saved. The file extension must be `.jpg`. Ensure that the directory exists and is writable. Example: `/sdcard/Pictures/snapshot.jpg`. |

**Return Value**

The index of the remote snapshot task, starting from `1`. The index can be used to track the task status or perform other management operations.

### startEchoTest

```java
public abstract int com.ss.bytertc.engine.RTCEngine.startEchoTest(
    EchoTestConfig config,
    int delayTime
)
```

Starts a call test.

Before entering the room, you can call this API to test whether your local audio/video equipment as well as the upstream and downstream networks are working correctly.

Once the test starts, SDK will record your sound or video. If you receive the playback within the delay range you set, the test is considered normal.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|config |EchoTestConfig |Test configurations, see [EchoTestConfig](https://docs.byteplus.com/en/docs/12/docs-70083#EchoTestConfig). |
|delayTime |int |Delayed audio/video playback time specifying how long you expect to receive the playback after starting the test. The range of the value is [2,10] in seconds and the default value is 2. |

**Return Value**

API call result:

* 0: Success.

* \-2: Failure due to parameter exception.

* \-4: Failure because the user has joined a room.

* \-6: Failure for the testing is in progress.

* \-7: Failure for the request included neither video nor audio.

* \-8: Failure for the roomID is already used.

**Notes**

* Once you start the test, you can either call [stopEchoTest](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopechotest) or wait until the test stops automatically after 60s, to start the next test or enter the room.

* All APIs related to device control and stream control called before this API are invalidated during the test and are restored after the test.

* All APIs related to device control, stream control, and room entry called during the test do not take effect, and you will receive [onWarning](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onwarning) with the warning code `WARNING_CODE_IN_ECHO_TEST_MODE`.

* You will receive the test result from [onEchoTestResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onechotestresult).

### stopEchoTest

```java
public abstract int com.ss.bytertc.engine.RTCEngine.stopEchoTest()
```

Stop the current call test.

After calling [startEchoTest](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startechotest), you must call this API to stop the test.

**Return Value**

API call result:

* 0: Success.

* \-3: Failure, no test is in progress.

**Notes**

After stopping the test with this API, all the system devices and streams are restored to the state they were in before the test.

### setRemoteVideoSink

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setRemoteVideoSink(
    String streamId,
    IVideoSink videoSink,
    RemoteVideoSinkConfig config
)
```

> Available since 3.57

Binds the remote video stream to a custom renderer. You can get video frame data at specified positions and formats through parameter settings.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |String |Stream ID, used to specify the video stream to be rendered. |
|videoSink |IVideoSink |Custom video renderer. See [IVideoSink](https://docs.byteplus.com/en/docs/12/docs-70083#IVideoSink). |
|config |RemoteVideoSinkConfig |remote video frame callback configuration, see [RemoteVideoSinkConfig](https://docs.byteplus.com/en/docs/12/docs-70083#RemoteVideoSinkConfig)。 |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* RTC SDK uses its own renderer (internal renderer) for video rendering by default.

* This method can be called both before and after entering the room. If you are unable to obtain remote stream information in advance, you can call this method after joining the room and receiving the remote stream information through the [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo) callback.

* Leaving the room will clear the binding status.

* If you need to unbind the video stream from the custom renderer, you must set video_sink to `null`.

### updateRemoteStreamVideoCanvas

```java
public abstract int com.ss.bytertc.engine.RTCEngine.updateRemoteStreamVideoCanvas(
    String streamId,
    RemoteVideoRenderConfig remoteVideoRenderConfig
)
```

> Available since 3.56

Modifies remote video frame rendering settings, including render mode, background color, and rotation angle, while using the internal rendering of the SDK.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |String |Stream ID, used to specify the video stream for which the rendering settings need to be modified. |
|remoteVideoRenderConfig |RemoteVideoRenderConfig |Video rendering settings. See [RemoteVideoRenderConfig](https://docs.byteplus.com/en/docs/12/docs-70083#RemoteVideoRenderConfig). |

**Return Value**

* 0: Success.

* < 0 : Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* After setting the rendering configuration for the remote video frame with [setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setremotevideocanvas), you can call this API to update settings including render mode, background color, and rotation angle.

* Calling this API during remote video rendering will be effective immediately.

### setRemoteVideoCanvas

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setRemoteVideoCanvas(
    String streamId,
    VideoCanvas videoCanvas
)
```

Sets the view to be used for remote video rendering and the rendering mode.

To unbind the canvas, set `videoCanvas` to Null.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |String |Stream ID, used to specify the video stream for which the view and rendering mode need to be set. |
|videoCanvas |VideoCanvas |View information and rendering mode. See [VideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70083#VideoCanvas). Starting from version 3.56, you can set the rotation angle of the remote video rendering using `renderRotation`. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

When the local user leaves the room, the setting will be invalid. The remote user leaving the room does not affect the setting.

### setRemoteAudioPlaybackVolume

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setRemoteAudioPlaybackVolume(
    String streamId,
    int volume
)
```

Set the audio volume of playing the received remote stream. You must join the room before calling the API. The validity of the setting is not associated with the publishing status of the stream.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |String |Stream ID, used to specify the remote stream whose volume is to be adjusted. |
|volume |int |The ratio between the playing volume of the original volume. The range is `[0, 400]` with overflow protection. The unit is %.<br><br> <br><br>For better audio quality, you are recommended to set the value to `[0, 100]`. |

**Return Value**

result

* 0: Success.

* <0: Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus).

**Notes**

Assume that a remote user A is always within the scope of the adjusted target users:

* When this API is used together with [setRemoteRoomAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/14166#RTCRoom-setremoteroomaudioplaybackvolume), the volume of local listening user A is the volume set by the API called later;

* When this API is used together with the [setPlaybackVolume](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setplaybackvolume), the volume of local listening user A will be the superposition of the two set volume effects.

* When you call this API to set the remote stream volume, if the remote user leaves the room, the setting will be invalid.

### setVideoDecoderConfig

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setVideoDecoderConfig(
    String streamId,
    VideoDecoderConfig config
)
```

Before subscribing to the remote video stream, set the remote video data decoding method

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |String |The remote stream ID specifies which video stream to decode. |
|config |VideoDecoderConfig |Video decoding method. See [VideoDecoderConfig](https://docs.byteplus.com/en/docs/12/docs-70083#VideoDecoderConfig). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* When you want to custom decode a remote stream, you need to call [registerRemoteEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-registerremoteencodedvideoframeobserver) to register the remote video stream monitor, and then call the interface to set the decoding method to custom decoding. The monitored video data will be called back through [onRemoteEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IRemoteEncodedVideoFrameObserver-onremoteencodedvideoframe).

* Since version 3.56, for automatic subscription, you can set the `RoomId` and `UserId` of `key` as `nullptr`. In this case, the decoding settings set by calling the API apply to all remote main streams or screen sharing streams based on the `StreamIndex` value of `key`.

### requestRemoteVideoKeyFrame

```java
public abstract int com.ss.bytertc.engine.RTCEngine.requestRemoteVideoKeyFrame(String streamId)
```

After subscribing to the remote video stream, request the keyframe

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |String |Remote stream ID. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* This method is only suitable for manual subscription mode and is used after successful subscription to the remote stream.

* This method is suitable for calling [setVideoDecoderConfig](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideodecoderconfig) to turn on the custom decoding function, and the custom decoding fails

### startCloudProxy

```java
public abstract int com.ss.bytertc.engine.RTCEngine.startCloudProxy(List<CloudProxyInfo> cloudProxiesInfo)
```

Start cloud proxy

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|cloudProxiesInfo |List<CloudProxyInfo\> |cloud proxy information list. See [CloudProxyInfo](https://docs.byteplus.com/en/docs/12/docs-70083#CloudProxyInfo). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* Call this API before joining the room.

* Start pre\-call network detection after starting cloud proxy.

* After starting the cloud proxy and successfully connecting to the cloud proxy server, you will receive [onCloudProxyConnected](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-oncloudproxyconnected).

* To stop cloud proxy, call [stopCloudProxy](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stopcloudproxy).

### stopCloudProxy

```java
public abstract int com.ss.bytertc.engine.RTCEngine.stopCloudProxy()
```

Stop cloud proxy

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

To start cloud proxy, call [startCloudProxy](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startcloudproxy).

### getNetworkTimeInfo

```java
public abstract NetworkTimeInfo com.ss.bytertc.engine.RTCEngine.getNetworkTimeInfo()
```

Obtain the synchronization network time information.

**Return Value**

See [NetworkTimeInfo](https://docs.byteplus.com/en/docs/12/docs-70083#NetworkTimeInfo).

**Notes**

* When you call this API for the first time, you start synchronizing the network time information and receive the return value `0`. After the synchronization finishes, you will receive [onNetworkTimeSynchronized](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onnetworktimesynchronized). After that, calling this API will get you the correct network time.

* Under chorus scenario, participants shall start audio mixing at the same network time.

### getWTNStream

```java
public abstract IWTNStream com.ss.bytertc.engine.RTCEngine.getWTNStream()
```

Get the WTN stream APIs.

**Return Value**

WTN stream APIs. See [IWTNStream](https://docs.byteplus.com/en/docs/12/14166#IWTNStream).

### startHardwareEchoDetection

```java
public abstract int com.ss.bytertc.engine.RTCEngine.startHardwareEchoDetection(String testAudioFilePath)
```

Start echo detection before joining a room.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|testAudioFilePath |String |Absolute path of the music file for the detection. It is expected to encode with UTF\-8. The following files are supported: mp3, aac, m4a, 3gp, wav.<br><br> <br><br>We recommend to assign a music file whose duration is between 10 to 20 seconds.<br><br> <br><br>Do not pass a Silent file. |

**Return Value**

Method call result:

* 0: Success.

* \-1: Failure due to the ongoing process of the previous detection. Call [stopHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stophardwareechodetection) to stop it before calling this API again.

* \-2: Failure due to an invalid file path or file format.

**Notes**

* You can use this feature only when [ChannelProfile](https://docs.byteplus.com/en/docs/12/docs-70083#ChannelProfile) is set to `CHANNEL_PROFIEL_MEETING` or `CHANNEL_PROFILE_MEETING_ROOM`.

* Before calling this API, ask the user for the permissions to access the local audio devices.

* Before calling this api, make sure the audio devices are active and keep the capture volume and the playback volume within a reasonable range.

* The detection result is passed as the argument of onHardwareEchoDetectionResult.

* During the detection, the SDK is not able to respond to the other testing APIs, such as [startEchoTest](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-startechotest), [startAudioDeviceRecordTest](https://docs.byteplus.com/en/docs/12/14166#IRTCAudioDeviceManager-startaudiodevicerecordtest) or [startAudioPlaybackDeviceTest](https://docs.byteplus.com/en/docs/12/14166#IRTCAudioDeviceManager-startaudioplaybackdevicetest).

* Call [stopHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-stophardwareechodetection) to stop the detection and release the audio devices.

### stopHardwareEchoDetection

```java
public abstract int com.ss.bytertc.engine.RTCEngine.stopHardwareEchoDetection()
```

Stop the echo detection before joining a room.

**Return Value**

Method call result:

* 0: Success.

* \-1: Failure.

**Notes**

* Refer to [startHardwareEchoDetection](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-starthardwareechodetection) for information on how to start an echo detection.

* We recommend calling this API to stop the detection once getting the detection result from [onHardwareEchoDetectionResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onhardwareechodetectionresult).

* You must stop the echo detection to release the audio devices before the user joins a room. Otherwise, the detection may interfere with the call.

### setCellularEnhancement

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setCellularEnhancement(MediaTypeEnhancementConfig config)
```

Enable cellular network assisted communication to improve call quality.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|config |MediaTypeEnhancementConfig |See [MediaTypeEnhancementConfig](https://docs.byteplus.com/en/docs/12/docs-70083#MediaTypeEnhancementConfig). |

**Return Value**

Method call result:

* 0: Success.

* \-1: Failure, internal error.

* \-2: Failure, invalid parameters.

**Notes**

The function is off by default.

### setLocalProxy

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setLocalProxy(List<LocalProxyConfiguration> configurations)
```

Sets local proxy.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|configurations |List<LocalProxyConfiguration\> |Local proxy configurations. Refer to [LocalProxyConfiguration](https://docs.byteplus.com/en/docs/12/docs-70083#LocalProxyConfiguration).<br><br> <br><br>You can set both Http tunnel and Socks5 as your local proxies, or only set one of them based on your needs. If you set both Http tunnel and Socks5 as your local proxies, then media traffic and signaling are routed through Socks5 proxy and Http requests through Http tunnel proxy. If you set either Http tunnel or Socks5 as your local proxy, then media traffic, signaling and Http requests are all routed through the proxy you chose.<br><br> <br><br>If you want to remove the existing local proxy configurations, you can call this API with the parameter set to null. |

**Notes**

* You must call this API before joining the room.

* After calling this API, you will receive [onLocalProxyStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onlocalproxystatechanged) callback that informs you of the states of local proxy connection.

### getVideoDeviceManager

```java
public abstract IVideoDeviceManager com.ss.bytertc.engine.RTCEngine.getVideoDeviceManager()
```

> Available since 3.56

Create a video Device Management instance

**Return Value**

Video Device Management instance. See [IVideoDeviceManager](https://docs.byteplus.com/en/docs/12/14166#IVideoDeviceManager)

### setVideoCaptureRotation

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setVideoCaptureRotation(VideoRotation rotation)
```

Set the rotation of the video images captured from the local device.

Call this API to rotate the videos when the camera is fixed upside down or tilted. For rotating videos on a phone, we recommend to use [setVideoRotationMode](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideorotationmode).

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|rotation |VideoRotation |It defaults to `VIDEO_ROTATION_0(0)`, which means not to rotate. Refer to [VideoRotation](https://docs.byteplus.com/en/docs/12/docs-70083#VideoRotation). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* For the videos captured by the internal module, the rotation will be combined with that set by calling [setVideoRotationMode](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideorotationmode).

* This API affects the external\-sourced videos. The final rotation would be the original rotation angles adding up with the rotation set by calling this API.

* The elements added during the video pre\-processing stage, such as video sticker and background applied using [enableVirtualBackground](https://docs.byteplus.com/en/docs/12/14166#IVideoEffect-enablevirtualbackground) will also be rotated by this API.

* The rotation would be applied to both locally rendered videos and those sent out. However, if you need to rotate a video which is intended for pushing to CDN individually, use [setVideoOrientation](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setvideoorientation).

### setLocalVideoSink

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setLocalVideoSink(
    IVideoSink videoSink,
    @IVideoSink.PixelFormat int requiredFormat
)
```

> Deprecated since 3.57, use [setLocalVideoSink](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setlocalvideosink) instead.

Binds the local video stream to a custom renderer.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|videoSink |IVideoSink |Custom video renderer. See [IVideoSink](https://docs.byteplus.com/en/docs/12/docs-70083#IVideoSink). |
|requiredFormat |@IVideoSink.PixelFormat int |Video frame encoding format that applies to custom rendering. See [PixelFormat](https://docs.byteplus.com/en/docs/12/docs-70083#PixelFormat). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* RTC SDK uses its own renderer (internal renderer) for video rendering by default.

* Joining or leaving the room will not affect the binding state.

* If you need to unbind the video stream from the custom render, you must set videoSink to `null`.

* You should call this API before joining the room, and after receiving [onFirstLocalVideoFrameCaptured](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onfirstlocalvideoframecaptured) which reports that the first local video frame has been successfully captured.

* This method gets video frames that have undergone preprocessing. If you need to obtain video frames from other positions, such as after capture, you should call setLocalVideoRender instead.

### setRemoteVideoSink

```java
public abstract int com.ss.bytertc.engine.RTCEngine.setRemoteVideoSink(
    String streamId,
    IVideoSink videoSink,
    @IVideoSink.PixelFormat int requiredFormat
)
```

> Deprecated since 3.57, use [setRemoteVideoSink](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-setremotevideosink) instead.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |String |Stream ID, used to specify the video stream to be rendered. |
|videoSink |IVideoSink |Custom video renderer. See [IVideoSink](https://docs.byteplus.com/en/docs/12/docs-70083#IVideoSink) |
|requiredFormat |@IVideoSink.PixelFormat int |Encoding format that applies to the custom renderer. See [PixelFormat](https://docs.byteplus.com/en/docs/12/docs-70083#PixelFormat) |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

* RTC SDK uses its own renderer (internal renderer) for video rendering by default.

* Joining or leaving the room will not affect the binding state.

* This API can be called before and after entering the room. To call before entering the room, you need to get the remote stream information before joining the room; if you cannot get the remote stream information in advance, you can call the API after joining the room and getting the remote stream information via [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo).

* If you need to unbind the remote stream from the renderer, you must set videoSink to null.

* This method retrieves video frames after post\-processing. If you need to obtain video frames from other locations (such as video frames after decoding), please call setRemoteVideoRender.

### updateRemoteStreamVideoCanvas

```java
public abstract int com.ss.bytertc.engine.RTCEngine.updateRemoteStreamVideoCanvas(
    String streamId,
    int renderMode,
    int backgroundColor
)
```

> Deprecated since 3.56 and will be deleted in 3.62. Use [updateRemoteStreamVideoCanvas](https://docs.byteplus.com/en/docs/12/14166#updateremotestreamvideocanvas-2) instead.

Modifies remote video frame rendering settings, including render mode and background color.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|streamId |String |Stream ID, used to specify the video stream for which the rendering settings need to be modified. |
|renderMode |int |See [VideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70083#VideoCanvas).renderMode. |
|backgroundColor |int |See [VideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70083#VideoCanvas).background_color， |

**Return Value**

* 0: Success.

* < 0 : Failure. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details

**Notes**

Calling this API during remote video rendering will be effective immediately.

# IMediaPlayer

```java
public abstract class com.ss.bytertc.engine.audio.IMediaPlayer
```

> Available since 3.53

Audio effect player

Call [setEventHandler](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-seteventhandler) to set the callback handler to receive related callbacks.

## Member Functions

|Return |Name |
|---|---|
|abstract int |[open](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-open) |
|abstract int |[start](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-start) |
|abstract int |[openWithCustomSource](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-openwithcustomsource) |
|abstract int |[stop](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-stop) |
|abstract int |[pause](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-pause) |
|abstract int |[resume](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-resume) |
|abstract int |[setVolume](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-setvolume) |
|abstract int |[getVolume](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-getvolume) |
|abstract int |[getTotalDuration](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-gettotalduration) |
|abstract int |[getPlaybackDuration](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-getplaybackduration) |
|abstract int |[getPosition](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-getposition) |
|abstract PlayerState |[getState](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-getstate) |
|abstract int |[setAudioPitch](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-setaudiopitch) |
|abstract int |[setPosition](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-setposition) |
|abstract int |[setAudioDualMonoMode](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-setaudiodualmonomode) |
|abstract int |[getAudioTrackCount](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-getaudiotrackcount) |
|abstract int |[selectAudioTrack](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-selectaudiotrack) |
|abstract int |[setPlaybackSpeed](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-setplaybackspeed) |
|abstract int |[setProgressInterval](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-setprogressinterval) |
|abstract int |[setLoudness](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-setloudness) |
|abstract int |[registerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-registeraudioframeobserver) |
|abstract int |[pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-pushexternalaudioframe) |
|abstract int |[setEventHandler](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-seteventhandler) |

## Instructions

### open

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.open(
    String filePath,
    MediaPlayerConfig config
)
```

Open the audio file.

You can only open one audio file with one player instance at the same time. For multiple audio files at the same time, create multiple player instances.

For audio file in PCM format, see [openWithCustomSource](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-openwithcustomsource). `openWithCustomSource` and this API are mutually exclusive.

**Input Parameters**

|Audio file paths.<br><br> <br><br>URL of online file, URI of local file, full path to local file, or path to local file starting with `/assets/` are supported. For URL of online file, only the https protocol is supported.<br><br> <br><br>Recommended sample rate for audio effect files: 8KHz, 16KHz, 22.05KHz, 44.1KHz, 48KHz.<br><br> <br><br>Local audio effect file formats supported by different platforms:<br><br> <br><br> <br><br> <br><br> <br><br>Online audio effect file formats supported by different platforms.<br><br> <br><br> <br><br> | | |
|---|---|---|
|config |MediaPlayerConfig |See [MediaPlayerConfig](https://docs.byteplus.com/en/docs/12/docs-70083#MediaPlayerConfig). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

### start

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.start()
```

Start playing the audio. Call this API when you call [open](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-open) and set `AutoPlay=False`.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* For audio file in PCM format, see [openWithCustomSource](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-openwithcustomsource). `openWithCustomSource` and this API are mutually exclusive.

* After calling this API, call [stop](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-stop) to stop playing the audio file.

### openWithCustomSource

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.openWithCustomSource(
    MediaPlayerCustomSource source,
    MediaPlayerConfig config
)
```

Enable audio mixing with audio raw data.

To open the audio file, see [open](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-open). `open` and this API are mutually exclusive.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|source |MediaPlayerCustomSource |See [MediaPlayerCustomSource](https://docs.byteplus.com/en/docs/12/docs-70083#MediaPlayerCustomSource). |
|config |MediaPlayerConfig |See [MediaPlayerConfig](https://docs.byteplus.com/en/docs/12/docs-70083#MediaPlayerConfig). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* After calling this API, you must call [pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-pushexternalaudioframe) to push audio data and start the audio mixing.

* To stop the raw data audio mixing, call [stop](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-stop).

### stop

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.stop()
```

After calling [open](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-open), [start](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-start), or [openWithCustomSource](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-openwithcustomsource) to start audio mixing, call this method to stop audio mixing.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

### pause

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.pause()
```

After calling [open](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-open), or [start](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-start) to start audio mixing, call this API to pause audio mixing.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* After calling this API to pause audio mixing, call [resume](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-resume) to resume audio mixing.

* The API is valid for audio files, not PCM data.

### resume

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.resume()
```

After calling [pause](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-pause) to pause audio mixing, call this API to resume audio mixing.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

The API is valid for audio files, not PCM data.

### setVolume

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.setVolume(
    int volume,
    AudioMixingType type
)
```

Adjusts the volume of the specified audio mixing, including media file mixing and PCM mixing.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |int |The ratio of the volume to the original volume in % with overflow protection. The range is `[0, 400]` and the recommended range is `[0, 100]`. |
|type |AudioMixingType |See [AudioMixingType](https://docs.byteplus.com/en/docs/12/docs-70083#AudioMixingType). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

Call this API only when audio is mixing.

### getVolume

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.getVolume(AudioMixingType type)
```

Gets the current volume.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|type |AudioMixingType |See [AudioMixingType](https://docs.byteplus.com/en/docs/12/docs-70083#AudioMixingType). |

**Return Value**

* \>0: Success, the current volume.

* < 0: Failed.

**Notes**

Call this API only when audio is mixing, including media file mixing and PCM mixing.

### getTotalDuration

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.getTotalDuration()
```

Gets the duration of the media file.

**Return Value**

* \>0: Success, the duration of the media file in milliseconds.

* < 0: Failed.

**Notes**

* Call this API only when audio is mixing.

* The API is valid for audio files, not PCM data.

### getPlaybackDuration

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.getPlaybackDuration()
```

Gets the actual playback duration of the mixed media file, in milliseconds.

**Return Value**

* \>0: Success, the actual playback time.

* < 0: Failed.

**Notes**

* The actual playback time refers to the playback time of the song without being affected by stop, jump, double speed, and freeze. For example, if the song stops playing for 30 seconds at 1:30 or skips to 2:00, and then continues to play normally for 2 minutes, the actual playing time is 3 minutes and 30 seconds.

* Call this API only when audio is mixing and the interval set by [setProgressInterval](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-setprogressinterval) is above `0`.

* The API is valid for audio files, not PCM data.

### getPosition

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.getPosition()
```

Gets the playback progress of the media file.

**Return Value**

* \>0: Success, the playback progress of media file in ms.

* < 0: Failed.

**Notes**

* Call this API only when audio is mixing.

* The API is valid for audio files, not PCM data.

### getState

```java
public abstract PlayerState com.ss.bytertc.engine.audio.IMediaPlayer.getState()
```

Get the state of the media player.

**Return Value**

The current state of the media player. See [PlayerState](https://docs.byteplus.com/en/docs/12/docs-70083#PlayerState).

**Notes**

You can call this method after the creating a `IMediaPlayer` instance.

### setAudioPitch

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.setAudioPitch(int pitch)
```

Set the pitch of the local audio file mixing. Usually used in karaoke scenes.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|pitch |int |The increase or decrease value compared with the original pitch of the music file. The range is `[-12, 12]`. The default value is 0. The pitch distance between two adjacent values is half a step. A positive value indicates a rising pitch, and a negative value indicates a falling pitch. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* Call this API only when audio is mixing.

* Support audio file only and not PCM data.

### setPosition

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.setPosition(int position)
```

Sets the starting playback position of the media file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|position |int |The starting position of the media file in milliseconds.<br><br> <br><br>You can get the total duration of the media file through [getTotalDuration](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-gettotalduration). The value of position should be less than the total duration of the media file. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* The API is valid for audio files, not PCM data.

* When playing online files, calling this API may cause playback delay.

* After calling this API, you will receive [onMediaPlayerEvent](https://docs.byteplus.com/en/docs/12/docs-70081#IMediaPlayerEventHandler-onmediaplayerevent) callback.

### setAudioDualMonoMode

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.setAudioDualMonoMode(AudioMixingDualMonoMode mode)
```

Sets the channel mode of the mixing of the media file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|mode |AudioMixingDualMonoMode |The mode of channel. The default channel mode is the same as the source file. See [AudioMixingDualMonoMode](https://docs.byteplus.com/en/docs/12/docs-70083#AudioMixingDualMonoMode). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* Call this API only when audio is mixing.

* Audio file is supported, but not PCM data.

### getAudioTrackCount

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.getAudioTrackCount()
```

Gets the track count of the current media file.

**Return Value**

* \>= 0：Success. Return the track count of the current media file.

* < 0：Failed.

**Notes**

* Call this API only when audio is mixing.

* This API is valid for audio file, not PCM data.

### selectAudioTrack

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.selectAudioTrack(int index)
```

Specifies the playback track of the current media file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|index |int |The specified playback audio track, starting from 0, and the range is `[0, getAudioTrackCount()-1]`. The value must be less than the return value of [getAudioTrackCount](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-getaudiotrackcount). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* Call this API only when audio is mixing.

* This API is valid for audio file, not PCM data.

* After calling this API, you will receive [onMediaPlayerEvent](https://docs.byteplus.com/en/docs/12/docs-70081#IMediaPlayerEventHandler-onmediaplayerevent) callback.

### setPlaybackSpeed

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.setPlaybackSpeed(int speed)
```

Set the playback speed of the audio file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|speed |int |The ratio of the actual playback speed than that of the original speed of the audio file in %. The range is `[50,200]`. The default value is 100. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* Call this API only when audio is mixing.

* The API is valid for audio files and not PCM data.

### setProgressInterval

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.setProgressInterval(long interval)
```

Set the interval of the periodic callback [onMediaPlayerPlayingProgress](https://docs.byteplus.com/en/docs/12/docs-70081#IMediaPlayerEventHandler-onmediaplayerplayingprogress) during audio mixing.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|interval |long |interval in ms.<br><br><br> <br><br>* interval \> 0: The callback is enabled. The actual interval is `10*(mod(10)+1)`.<br><br>* interval <= 0: The callback is disabled. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* Call this API only when audio is mixing.

* This API is valid for audio file, not PCM data.

### setLoudness

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.setLoudness(float loudness)
```

To call [enableVocalInstrumentBalance](https://docs.byteplus.com/en/docs/12/14166#RTCEngine-enablevocalinstrumentbalance) to adjust the volume of the mixed media file or the PCM audio data, you must pass in its original loudness through this API.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|loudness |float |Original loudness in lufs. The range is `[-70.0, 0.0]`.<br><br> <br><br>When the value is less than \-70.0lufs, it will be adjusted to \-70.0lufs by default, and if it is more than 0.0lufs, the loudness will not be equalized. The default value is 1.0lufs, which means no processing. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* Call this API only when audio is mixing.

* The API is valid for audio files and PCM data.

### registerAudioFrameObserver

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.registerAudioFrameObserver(IMediaPlayerAudioFrameObserver observer)
```

Register an observer to receive related callbacks when the local media file is mixing.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|observer |IMediaPlayerAudioFrameObserver |See [IMediaPlayerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70081#IMediaPlayerAudioFrameObserver). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

The API is valid for audio files, not PCM data.

### pushExternalAudioFrame

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.pushExternalAudioFrame(AudioFrame audioFrame)
```

Push PCM audio frame data for mixing.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|audioFrame |AudioFrame |See [AudioFrame](https://docs.byteplus.com/en/docs/12/docs-70083#AudioFrame).<br><br><br> <br><br>* The audio sampling format must be S16. The data format within the audio buffer must be PCM, and its capacity size should be `audioFrame.samples × audioFrame.channel × 2`.<br><br>* A specific sample rate and the number of channels must be specified. Setting them to automatic is not supported. |

**Return Value**

* 0: Success.

* < 0: Failed.

**Notes**

* Before calling this method, the raw audio data mixing must be enabled through [openWithCustomSource](https://docs.byteplus.com/en/docs/12/14166#IMediaPlayer-openwithcustomsource).

* Suggestions: Before pushing data for the first time, please cache a certain amount of data (like 200 ms) on the application side, and then push it at once. Schedule subsequent push operation every 10 ms with audio data of 10 ms.

* To pause the playback, just pause the push.

### setEventHandler

```java
public abstract int com.ss.bytertc.engine.audio.IMediaPlayer.setEventHandler(IMediaPlayerEventHandler handler)
```

Set the event handler.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|handler |IMediaPlayerEventHandler |See [IMediaPlayerEventHandler](https://docs.byteplus.com/en/docs/12/docs-70081#IMediaPlayerEventHandler). |

**Return Value**

* 0: Success.

* < 0: Failed.

# IAudioEffectPlayer

```java
public abstract class com.ss.bytertc.engine.audio.IAudioEffectPlayer
```

> Available since 3.53

Audio effect player

Call [setEventHandler](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-seteventhandler) to set the callback handler to receive related callbacks.

## Member Functions

|Return |Name |
|---|---|
|abstract int |[start](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-start) |
|abstract int |[stop](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-stop) |
|abstract int |[stopAll](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-stopall) |
|abstract int |[preload](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-preload) |
|abstract int |[unload](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-unload) |
|abstract int |[unloadAll](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-unloadall) |
|abstract int |[pause](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-pause) |
|abstract int |[pauseAll](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-pauseall) |
|abstract int |[resume](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-resume) |
|abstract int |[resumeAll](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-resumeall) |
|abstract int |[setPosition](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-setposition) |
|abstract int |[getPosition](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-getposition) |
|abstract int |[setVolume](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-setvolume) |
|abstract int |[setVolumeAll](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-setvolumeall) |
|abstract int |[getVolume](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-getvolume) |
|abstract int |[getDuration](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-getduration) |
|abstract int |[setEventHandler](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-seteventhandler) |

## Instructions

### start

```java
public abstract int com.ss.bytertc.engine.audio.IAudioEffectPlayer.start(
    int effectId,
    String filePath,
    AudioEffectPlayerConfig config
)
```

Starts to play the audio effect file.

This API can be called multiple times with different IDs and file paths for multiple effects at the same time.

**Input Parameters**

|Audio effect file paths.<br><br> <br><br>URL of online file, URI of local file, full path to local file, or path to local file starting with `/assets/` are supported. For URL of online file, only the https protocol is supported.<br><br> <br><br>Recommended sample rate for audio effect files: 8KHz, 16KHz, 22.05KHz, 44.1KHz, 48KHz.<br><br> <br><br>Local audio effect file formats supported by different platforms:<br><br> <br><br> <br><br> <br><br> <br><br>Online audio effect file formats supported by different platforms.<br><br> <br><br> <br><br> | | |
|---|---|---|
|config |AudioEffectPlayerConfig |See [AudioEffectPlayerConfig](https://docs.byteplus.com/en/docs/12/docs-70083#AudioEffectPlayerConfig). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* If the file has been loaded into memory via [preload](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-preload), make sure that the ID here is the same as the ID set by [preload](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-preload).

* After starting to play an audio effect file, you can call the [stop](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-stop) API to stop playing the audio effect file.

### stop

```java
public abstract int com.ss.bytertc.engine.audio.IAudioEffectPlayer.stop(int effectId)
```

Stops the playback of audio effect files.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectId |int |Audio effect ID |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* After calling the [start](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-start) API to start playing the audio effect file, you can call this API to stop playing the audio effect file.

* After calling this API to stop playing an audio effect file, the audio effect file will be unloaded automatically.

### stopAll

```java
public abstract int com.ss.bytertc.engine.audio.IAudioEffectPlayer.stopAll()
```

Stops playback of all audio effect files.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* After calling [start](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-start) to start playing audio effect files, you can call this API to stop playing all audio effect files.

* After calling this API to stop playing all audio effect files, the audio effect files will be unloaded automatically.

### preload

```java
public abstract int com.ss.bytertc.engine.audio.IAudioEffectPlayer.preload(
    int effectId,
    String filePath
)
```

Preloads specified music files into memory to avoid repeated loading when playing the same file frequently and reduce CPU usage.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectId |int |Audio effect ID. Used for identifying the audio effect. Please ensure that the audio effect ID is unique.<br><br> <br><br>If this API is called repeatedly with the same ID, the later one will overwrite the previous one.<br><br> <br><br>If you call [start](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-start) first and then call this API with the same ID, the SDK will stop the previous effect and then load the next one, and you will receive [onAudioEffectPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioEffectPlayerEventHandler-onaudioeffectplayerstatechanged).<br><br> <br><br>After calling this API to preload A.mp3, if you need to call [start](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-start) to play B.mp3 with the same ID, please call [unload](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-unload) to unload A.mp3 first, otherwise SDK will report an error AUDIO_MIXING_ERROR_LOAD_CONFLICT. |
|filePath |String |The filepath of effect file. URI of local file, full path to local file, or path to local files starting with `/assets/` are supported.<br><br> <br><br>The length of the pre\-loaded file must not exceed 20s.<br><br> <br><br>Audio effect file formats supported are the same as [start](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-start). |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* This API just preloads the specified audio effect file, and only calls the [start](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-start) API to start playing the specified audio effect file.

* The specified audio effect file preloaded by calling this API can be unloaded by [unload](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-unload).

### unload

```java
public abstract int com.ss.bytertc.engine.audio.IAudioEffectPlayer.unload(int effectId)
```

Unloads the specified audio effect file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectId |int |Audio effect ID |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

Call this API after [start](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-start) or [preload](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-preload).

### unloadAll

```java
public abstract int com.ss.bytertc.engine.audio.IAudioEffectPlayer.unloadAll()
```

Unloads all audio effect files.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

### pause

```java
public abstract int com.ss.bytertc.engine.audio.IAudioEffectPlayer.pause(int effectId)
```

Pauses the playback of audio effect files.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectId |int |Audio effect ID |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* After calling the [start](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-start) API to start playing the audio effect file, you can pause the audio effect file by calling this API.

* After calling this API to pause the audio effect file, you can call the [resume](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-resume) API to resume playback.

### pauseAll

```java
public abstract int com.ss.bytertc.engine.audio.IAudioEffectPlayer.pauseAll()
```

Pauses the Playback of all audio effect files.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* After calling the [start](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-start) API to start playing audio effect files, you can pause playing all audio effect files by calling this API.

* After calling this API to pause the playback of all audio effect files, you can call the [resumeAll](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-resumeall) API to resume all playback.

### resume

```java
public abstract int com.ss.bytertc.engine.audio.IAudioEffectPlayer.resume(int effectId)
```

Resumes the playback of audio effect files.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectId |int |Audio effect ID |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

After calling the [pause](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-pause) API to pause the audio effect file, you can resume playback by calling this API.

### resumeAll

```java
public abstract int com.ss.bytertc.engine.audio.IAudioEffectPlayer.resumeAll()
```

Resumes the playback of all audio effect files.

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

After calling the [pauseAll](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-pauseall) API to pause all the audio effect files being played, you can resume playback by calling this API.

### setPosition

```java
public abstract int com.ss.bytertc.engine.audio.IAudioEffectPlayer.setPosition(
    int effectId,
    int position
)
```

Sets the start position of the audio effect file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectId |int |Audio effect ID |
|position |int |The starting playback position of the audio effect file in milliseconds.<br><br> <br><br>You can get the total duration of the audio effect file by calling [getDuration](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-getduration), the value of position should be less than the total duration of the audio effect file. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

* When playing online files, calling this API may cause a delay in playback.

* Call this API after [start](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-start).

### getPosition

```java
public abstract int com.ss.bytertc.engine.audio.IAudioEffectPlayer.getPosition(int effectId)
```

Gets the current position of audio effect file playback.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectId |int |Audio effect ID |

**Return Value**

* \>0: Success, the current progress of audio effect file playback in milliseconds.

* < 0: Failure.

**Notes**

* When playing online files, calling this API may cause a delay in playback.

* Call this API after [start](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-start).

### setVolume

```java
public abstract int com.ss.bytertc.engine.audio.IAudioEffectPlayer.setVolume(
    int effectId,
    int volume
)
```

Adjusts the volume level of a specified audio effect, including audio effect file and PCM effect.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectId |int |Audio effect ID |
|volume |int |The ratio of the volume to the original volume in % with overflow protection. The range is `[0, 400]` and the recommended range is `[0, 100]`. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

Call this API after [start](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-start).

### setVolumeAll

```java
public abstract int com.ss.bytertc.engine.audio.IAudioEffectPlayer.setVolumeAll(int volume)
```

Sets the volume of all audio effects, including audio effect files and PCM effects.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|volume |int |The ratio of the volume to the original volume in % with overflow protection. The range is `[0, 400]` and the recommended range is `[0, 100]`. |

**Return Value**

* 0: Success.

* < 0 : Fail. See [ReturnStatus](https://docs.byteplus.com/en/docs/12/docs-70083#ReturnStatus) for more details.

**Notes**

This API has a lower priority than [setVolume](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-setvolume), i.e. the volume of the audio effect set by [setVolume](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-setvolume) is not affected by this API.

### getVolume

```java
public abstract int com.ss.bytertc.engine.audio.IAudioEffectPlayer.getVolume(int effectId)
```

Gets the current volume.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectId |int |Audio effect ID |

**Return Value**

* \>0: Success, the current volume value.

* < 0: Failed.

**Notes**

Call this API after [start](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-start).

### getDuration

```java
public abstract int com.ss.bytertc.engine.audio.IAudioEffectPlayer.getDuration(int effectId)
```

Get the duration of the audio effect file.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|effectId |int |Audio effect ID |

**Return Value**

* \>0: Success, the duration of the audio effect file in milliseconds.

* < 0: failed.

**Notes**

Call this API after [start](https://docs.byteplus.com/en/docs/12/14166#IAudioEffectPlayer-start).

### setEventHandler

```java
public abstract int com.ss.bytertc.engine.audio.IAudioEffectPlayer.setEventHandler(IAudioEffectPlayerEventHandler handler)
```

Set the event handler.

**Input Parameters**

|Name |Type |Instructions |
|---|---|---|
|handler |IAudioEffectPlayerEventHandler |See [IAudioEffectPlayerEventHandler](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioEffectPlayerEventHandler). |

**Return Value**

* 0: Success.

* < 0: Failed.
