---
title: "Methods & Properties"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-methods_properties"
---

<span id="livepusher"></span>
## LivePusher

Type：`class`

The core class of the BytePlus MediaLive Broadcast SDK, handling audio/video capture, local mixing, and streaming.

<span id="property"></span>
### Property


|Property |Type |Description |
|---|---|---|
|observer |Observer |`Readonly` Receives notifications about streaming status, errors, warnings, and more. |
|isEnableMixing |boolean |`Readonly` Indicates whether local mixing is enabled. The default value is `false`.<br><br>Local mixing merges multiple audio and video streams (e.g., camera, microphone, screen sharing) into a single stream for easier remote transmission or recording.<br><br><br>* `true`: Enables local mixing, merging all input streams into a single stream.<br><br>* `false`: Disables local mixing, pushing each stream independently. |
|pushMode |[PushMode](https://docs.byteplus.com/en/docs/24/ref#pushmode) |`Readonly` The current streaming mode supports rtm, indicating RTM protocol streaming. |


<span id="new-livepusher"></span>
### new LivePusher()

Create a new `LivePusher` instance.

**Type**

```ts
constructor(options?: ConfigOptions)
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|options |[ConfigOptions](https://docs.byteplus.com/en/docs/24/docs-configuration#configoptions) \| undefined |No |None |Configuration options defining parameters for push streaming. |


<span id="getdeviceslist"></span>
### getDevicesList()  

Retrieves the list of available audio input and video input devices.

**Type**

```ts
(kind?: 'audioinput' | 'videoinput') => Promise<MediaDeviceInfo[]>
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|kind |"audioinput" \| "videoinput" \| undefined |No |None |Specify the device type. If omitted, returns all available devices.<br><br><br>* `audioinput`: Audio input device.<br><br>* `videoinput`: Video input device. |


**Return Value**

`Promise<MediaDeviceInfo[]>`


* **Success**: Returns an array of [MediaDeviceInfo](https://developer.mozilla.org/en-US/docs/Web/API/MediaDeviceInfo) objects, each representing detailed information about an audio input device or a video input device.

* **Failure**: Returns an error message.


<span id="getcameras"></span>
### getCameras()  

Get the list of camera devices.

**Type**

```ts
() => Promise<MediaDeviceInfo[]>
```


**Return Value**

`Promise<MediaDeviceInfo[]>`


* **Success**: Returns an array of [MediaDeviceInfo](https://developer.mozilla.org/en-US/docs/Web/API/MediaDeviceInfo) objects, each representing a camera device.

* **Failure**: Returns an error message.


<span id="getmicrophones"></span>
### getMicrophones()  

Retrieve available microphone devices.

**Type**

```ts
() => Promise<MediaDeviceInfo[]>
```


**Return Value**

`Promise<MediaDeviceInfo[]>`


* **Success**: Returns an array of [MediaDeviceInfo](https://developer.mozilla.org/en-US/docs/Web/API/MediaDeviceInfo) objects, each representing a microphone device.

* **Failure**: Returns an error message.


<span id="startcamera"></span>
### startCamera()  

Start camera video capture.

**Notes**

If camera permission is denied, an error will be thrown.

**Type**

```ts
(deviceId?: string) => Promise<string>
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|deviceId |string \| undefined |No |None |Specify the camera device ID to start capturing. You can obtain it using [getDevicesList](https://docs.byteplus.com/en/docs/24/37448#livepusher-getdeviceslist) or [getCameras](https://docs.byteplus.com/en/docs/24/37448#livepusher-getcameras).<br><br>On mobile devices, you can pass `user` or `environment`:<br><br><br>* `user`: Access the front camera.<br><br>* `environment`: Access the rear camera. |


**Return Value**

`Promise<string>` Returns a `Promise` object.


* **Success**: Returns the captured stream ID, which is used as a parameter for mixing and stopping the capture.

* **Failure**: Returns an error message.


<span id="stopcamera"></span>
### stopCamera()  

Stop video capture from the camera.

**Type**

```ts
(streamId?: string) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|streamId |string \| undefined |No |None |Specify the stream ID returned by [startCamera](https://docs.byteplus.com/en/docs/24/37448#livepusher-startcamera) to stop capturing. If omitted, stops all camera captures. |


<span id="startmicrophone"></span>
### startMicrophone()  

Start microphone audio capture.

**Notes**

If the host has not granted microphone access, a permission error will be thrown.

**Type**

```ts
(deviceId?: string) => Promise<string>
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|deviceId |string \| undefined |No |None |Specify the device ID to start capturing, which can be obtained using [getDevicesList](https://docs.byteplus.com/en/docs/24/37448#livepusher-getdeviceslist) or [getMicrophones](https://docs.byteplus.com/en/docs/24/37448#livepusher-getmicrophones). If omitted, all microphone captures will be started. |


**Return Value**

`Promise<string>` Returns a `Promise` object.


* **Success**: Returns the captured stream ID, which is used as a parameter for mixing and stopping the capture.

* **Failure**: Returns an error message.


<span id="stopmicrophone"></span>
### stopMicrophone()  

Stop microphone audio capture.

**Type**

```ts
(streamId?: string) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|streamId |string \| undefined |No |None |The stream ID that needs to stop capturing, returned upon a successful call to [startMicrophone](https://docs.byteplus.com/en/docs/24/37448#livepusher-startmicrophone). If omitted, stops all microphone captures. |


<span id="startvideofilecapture"></span>
### startVideoFileCapture()  

Start video file capture.

**Notes**

Currently, only Google Chrome is supported for data capture.

**Type**

```ts
(url: string) => Promise<string | undefined>
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|url |string |Yes |None |The URL of the video file, supporting both online URLs and Blob URLs.<br><br><br>* **Online URL**: A publicly accessible video file URL on the internet, e.g., `https://example.com/video.mp4`.<br><br>* **Blob URL**: A temporary address dynamically generated using the browser's Blob object, e.g., `blob:http://example.com/abc1234`. |


**Return Value**

`Promise<string | undefined>` Returns a `Promise` object.


* **Success**: Returns the captured stream ID, which can be used for merging or stopping the capture.

* **Failure**: Returns an error object.


<span id="stopvideofilecapture"></span>
### stopVideoFileCapture()  

Stop video file capture.

**Type**

```ts
(streamId?: string) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|streamId |string \| undefined |No |None |The captured stream ID, which is the return value of [startVideoFileCapture](https://docs.byteplus.com/en/docs/24/37448#livepusher-startvideofilecapture). If streamId is not provided, all video file captures will be stopped by default. |


<span id="startscreencapture"></span>
### startScreenCapture()  

Start screen capture.

**Notes**


* Screen sound capture function is only available in Chrome 74+ and Edge 79+ browser versions.

* For more details, please refer to [getDisplayMedia()](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getDisplayMedia#browser_compatibility) for browser compatibility.


**Type**

```ts
(audio?: boolean) => Promise<string>
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|audio |boolean |Yes |`false` |Whether to capture system or tab sound.<br><br><br>* `true`: Capture sound.<br><br>* `false`: Do not capture sound. |


**Return Value**

`Promise<string>` Returns a `Promise` object.


* **Success**: Returns the captured stream ID, which is used as a parameter for stream mixing and stopping capture.

* **Failure**: Returns an error object.


<span id="stopscreencapture"></span>
### stopScreenCapture()  

Stop screen capture.

**Type**

```ts
(streamId?: string) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|streamId |string \| undefined |No |None |The captured stream ID. The stream ID corresponds to the return value of [startScreenCapture](https://docs.byteplus.com/en/docs/24/37448#livepusher-startscreencapture). If streamId is not provided, it will stop the capture of all screens by default. |


<span id="startaudiofilecapture"></span>
### startAudioFileCapture()  

Start audio file capture.

**Notes**

Supported only in Google Chrome.

**Type**

```ts
(url: string) => Promise<string | undefined>
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|url |string |Yes |None |The URL of the audio file. Supports both online URLs and Blob URLs.<br><br><br>* **Online URL**: A publicly accessible audio file URL on the internet, e.g., `https://example.com/audio-file.mp3`.<br><br>* **Blob URL**: A temporary URL dynamically generated by the browser's Blob object, e.g., `blob:http://example.com/71d7a6d8`. |


**Return Value**

`Promise<string | undefined>` Returns a `Promise` object.


* **Success**: Returns the captured stream ID, which can be used as a parameter for mixing or stopping capture.

* **Failure**: Returns an error object.


<span id="stopaudiofilecapture"></span>
### stopAudioFileCapture()  

Stop audio file capture.

**Type**

```ts
(streamId?: string) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|streamId |string \| undefined |No |None |The captured stream ID, which corresponds to the return value of [startAudioFileCapture](https://docs.byteplus.com/en/docs/24/37448#livepusher-startaudiofilecapture). If streamId is not provided, all audio file captures will be stopped by default. |


<span id="startimagecapture"></span>
### startImageCapture()  

Start image capture.

**Type**

```ts
(url: string) => Promise<string | undefined>
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|url |string |Yes |None |The URL of the image file. Supports both online URLs and Blob URLs.<br><br><br>* **Online URL**: A publicly accessible image file URL on the internet, e.g., `https://example.com/image-file.png`.<br><br>* **Blob URL**: A temporary URL dynamically generated by the browser's Blob object, e.g., `blob:http://example.com/71d7a6d8`. |


**Return Value**

`Promise<string | undefined>` Returns a `Promise` object.


* **Success**: Returns the captured stream ID, which can be used as a parameter for merging or stopping the capture.

* **Failure**: Returns an error object.


<span id="stopimagecapture"></span>
### stopImageCapture()  

Stop image capture.

**Type**

```ts
(streamId?: string) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|streamId |string \| undefined |No |None |The ID of the stream to capture. The stream ID corresponds to the return value of [startImageCapture](https://docs.byteplus.com/en/docs/24/37448#livepusher-startimagecapture). If `streamId` is not provided, all image capturing will be stopped by default. |


<span id="startcustomvideocapture"></span>
### startCustomVideoCapture()  

Start custom video stream capture.

**Type**

```ts
(track: MediaStreamTrack) => string | undefined
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|track |MediaStreamTrack |Yes |None |The video stream to be captured. It can come from a device camera, screen sharing, or a video generated via `Canvas` rendering. For example, a `VideoTrack` obtained from a camera or screen sharing. |


**Return Value**

`string | undefined`


* **Success**: Returns the captured stream ID, which can be used as a parameter for merging or stopping the capture.

* **Failure**: Returns an error object.


<span id="stopcustomvideocapture"></span>
### stopCustomVideoCapture()  

Stop capturing the custom video stream.

**Type**

```ts
(streamId?: string) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|streamId |string \| undefined |No |None |The captured stream ID, returned by [startCustomVideoCapture](https://docs.byteplus.com/en/docs/24/37448#livepusher-startcustomvideocapture). If not provided, all custom video streams will be stopped. |


<span id="startcustomaudiocapture"></span>
### startCustomAudioCapture()  

Start capturing the custom audio stream.

**Type**

```ts
(track: MediaStreamTrack) => string | undefined
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|track |MediaStreamTrack |Yes |None |The custom audio stream to be captured. It can come from a microphone, an audio file, or other audio sources. For example, an `AudioTrack` obtained from a microphone. |


**Return Value**

`string | undefined`


* **Success**: Returns the captured stream ID, which can be used as a parameter for mixing and stopping capture.

* **Failure**: Returns an error object.


<span id="stopcustomaudiocapture"></span>
### stopCustomAudioCapture()  

Stop custom audio stream capture.

**Type**

```ts
(streamId?: string) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|streamId |string \| undefined |No |None |The captured stream ID, which is the return value corresponding to [startCustomAudioCapture](https://docs.byteplus.com/en/docs/24/37448#livepusher-startcustomaudiocapture). If streamId is not provided, the capture of all custom audio streams will be stopped by default. |


<span id="startvolumedetect"></span>
### startVolumeDetect()  

Start volume detection. Used to monitor the volume level of a specified audio stream or the final mixed output.

**Notes**


* Ensure the audio stream has started and is streaming correctly; check if the audio track is valid before calling.

* After starting volume detection, use the [getVolume()](https://docs.byteplus.com/en/docs/24/37448#livepusher-getvolume) method to obtain real\-time volume levels.


**Type**

```ts
(streamId?: string) => Promise<void>
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|streamId |string \| undefined |No |None |Specify the stream ID for volume detection.<br><br><br>* If `streamId` is `undefined`, the volume of the final mixed output, including all participating audio streams, will be detected.<br><br>* If `streamId` is specified, only the volume of the specified audio stream will be detected. |


**Return Value**

`Promise<void>` Returns a `Promise` object.


* **Success**: No return value.

* **Failure**: Returns an error message.


<span id="stopvolumedetect"></span>
### stopVolumeDetect()  

Stop volume detection.

**Notes**


* Applicable when needing to stop volume detection for a specific audio stream or the final output audio stream.

* After stopping the volume detection, the volume of the corresponding stream can no longer be obtained through the [getVolume()](https://docs.byteplus.com/en/docs/24/37448#livepusher-getvolume) method.


**Type**

```ts
(streamId?: string) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|streamId |string \| undefined |No |None |Specify the stream ID for stopping volume detection.<br><br><br>* If `streamId` is `undefined`, volume detection for the final mixed output will be stopped.<br><br>* If `streamId` is specified, only volume detection for the specified audio stream will be stopped. |


<span id="getvolume"></span>
### getVolume()  

Get volume.

**Notes**

Before calling this method, you need to call the [startVolumeDetect()](https://docs.byteplus.com/en/docs/24/37448#livepusher-startvolumedetect) method to start volume detection. Usage example:

```js
await livePusher.startVolumeDetect()
const volume = livePusher.getVolume()
console.log(volume)
```


**Type**

```ts
(streamId?: string) => number
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|streamId |string \| undefined |No |None |Specify the stream ID to retrieve the volume.<br><br><br>* If `streamId` is `undefined`, the volume of the final mixed output, including all participating audio streams, will be returned.<br><br>* If `streamId` is specified, only the volume of the specified audio stream will be returned. |


**Return Value**

`number` Returns the volume level for the specified stream ID, ranging from `[1, 10]`, with higher values indicating higher volume.

<span id="enablemixing"></span>
### enableMixing()  

Enable or disable local mixing functionality.

**Notes**


* Local mixing must be enabled before starting the push stream, and cannot be switched once the stream is running.

* You can call [setMixingConfig()](https://docs.byteplus.com/en/docs/24/37448#livepusher-setmixingconfig) both before and after enabling local mixing to configure canvas parameters (e.g., width, height, frame rate), ensuring the merged output meets your requirements.


**Type**

```ts
(enable: boolean) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|enable |boolean |Yes |None |Indicates whether local mixing is enabled.<br><br><br>* `true`: Enabled.<br><br>* `false`: Disabled. |


<span id="setmixingconfig"></span>
### setMixingConfig()  

Configure the mixing parameters, including the width, height, and frame rate of the mixing canvas.

**Type**

```ts
(config: IMixingViewConfig) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|config |[IMixingViewConfig](https://docs.byteplus.com/en/docs/24/docs-configuration#imixingviewconfig) |Yes |None |Attributes of the mixing canvas, such as width, height, frame rate, etc. |


<span id="setrenderview"></span>
### setRenderView()  

Set the preview area of the video. The local video will be previewed within the specified container, and the preview content will be identical to the streamed video and audio.

**Type**

```ts
(containerId: string) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|containerId |string |Yes |None |Used to specify the HTML container element ID for the preview area. |


<span id="startpreview"></span>
### startPreview()  

Start local video preview. Enabling the local video preview feature allows the host to see the local video effect through the preview area.

**Type**

```ts
() => void
```


<span id="stoppreview"></span>
### stopPreview()  

Stop local video preview.

**Notes**

When calling this API to stop the local video preview, it will not affect the actual stream.

**Type**

```ts
() => void
```


<span id="startpush"></span>
### startPush()  

Start streaming, supporting the RTM streaming method.

**Type**

```ts
(rtmUrl: string) => Promise<void>
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|rtmUrl |string |Yes |None |The streaming URL can be generated using the [BytePlus MediaLive Console](https://console.byteplus.com/live/main/locationGenerate), where you can obtain an RTM push stream address. |


**Return Value**

`Promise<void>` Returns a `Promise` object.


* **Success**: No return value.

* **Failure**: Returns an error message.


<span id="addvideostream"></span>
### addVideoStream()  

Adding video streams to the mixing canvas allows multiple video streams (e.g., the broadcaster's camera feed, screen sharing) to be combined into the same mixing canvas. If the video streams contain audio information, the audio will also be added to the mixing module.

**Notes**

Must be used after the [enableMixing()](https://docs.byteplus.com/en/docs/24/37448#livepusher-enablemixing) method has been called to enable the mixing function.

**Type**

```ts
(config: IVideoStreamLayoutParams | IVideoStreamLayoutParams[]) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|config |[IVideoStreamLayoutParams](https://docs.byteplus.com/en/docs/24/docs-configuration#ivideostreamlayoutparams) \| [IVideoStreamLayoutParams](https://docs.byteplus.com/en/docs/24/docs-configuration#ivideostreamlayoutparams)[] |Yes |None |The video stream layout parameters can be a single object or an array of multiple objects. |


<span id="removevideostream"></span>
### removeVideoStream()  

Remove the specified video stream from the mixing canvas. Use this to remove a video stream from the mixing canvas.

**Type**

```ts
(streamId: string) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|streamId |string |Yes |None |The video stream ID to be removed. |


<span id="updatevideostream"></span>
### updateVideoStream()  

Update the layout parameters of the added video stream, such as position and size. This is applicable to scenarios like dynamic layout adjustments.

**Type**

```ts
(config: IVideoStreamLayoutParams | IVideoStreamLayoutParams[]) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|config |[IVideoStreamLayoutParams](https://docs.byteplus.com/en/docs/24/docs-configuration#ivideostreamlayoutparams) \| [IVideoStreamLayoutParams](https://docs.byteplus.com/en/docs/24/docs-configuration#ivideostreamlayoutparams)[] |Yes |None |Update the video stream parameters. When an array is passed, multiple video streams are updated. |


<span id="mutevideostream"></span>
### muteVideoStream()  

Hide the video stream in the mixing canvas. Use this when a video needs to be temporarily hidden without removing the video stream from the mixing canvas.

**Type**

```ts
(streamId?: string) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|streamId |string \| undefined |No |None |The ID of the video stream to hide. If omitted, all video streams will be hidden. |


<span id="unmutevideostream"></span>
### unmuteVideoStream()  

Unhides the video stream in the mixing canvas. Use this when you need to show a video stream that was previously hidden.

**Type**

```ts
(streamId?: string) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|streamId |string \| undefined |No |None |To unhide video stream id; if not provided, unhide all video streams. |


<span id="addaudiostream"></span>
### addAudioStream()  

Add an audio stream to the mix module (requires enabling the co\-streaming feature). This is used when an additional audio source needs to be included in the co\-streamed audio, such as adding background music.

**Notes**

The method [enableMixing()](https://docs.byteplus.com/en/docs/24/37448#livepusher-enablemixing) must be called to enable the mixing function before use.

**Type**

```ts
(config: IAudioStreamLayoutParams | IAudioStreamLayoutParams[]) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|config |[IAudioStreamLayoutParams](https://docs.byteplus.com/en/docs/24/docs-configuration#iaudiostreamlayoutparams) \| [IAudioStreamLayoutParams](https://docs.byteplus.com/en/docs/24/docs-configuration#iaudiostreamlayoutparams)[] |Yes |None |Audio stream parameters can be a single object or an array of multiple objects. |


<span id="removeaudiostream"></span>
### removeAudioStream()  

Remove the specified audio stream. If the target is an individual audio stream, it will be removed directly; if the target is a video stream containing an audio track, only the audio portion will be affected, leaving the video intact.

**Type**

```ts
(streamId: string) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|streamId |string |Yes |None |The stream ID to be removed. If omitted, all audio streams will be removed. |


<span id="updateaudiostream"></span>
### updateAudioStream()  

Update the volume of the audio stream. Adjust the volume of one or multiple audio streams in a mixing scenario, such as balancing the host's voice, background music, and video audio.

**Notes**

You can call the interfaces in the following order.


* Call `enableMixing(true)` to enable the mixing function.

* Use `addAudioStream()` to add an audio stream to the mixing module.

* Call `updateAudioStream()` to update the parameters of the audio stream.


**Type**

```ts
(config: IAudioStreamLayoutParams | IAudioStreamLayoutParams[]) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|config |[IAudioStreamLayoutParams](https://docs.byteplus.com/en/docs/24/docs-configuration#iaudiostreamlayoutparams) \| [IAudioStreamLayoutParams](https://docs.byteplus.com/en/docs/24/docs-configuration#iaudiostreamlayoutparams)[] |Yes |None |Update the audio stream parameters. Pass in an array to update multiple audio streams. |


<span id="muteaudiostream"></span>
### muteAudioStream()  

Mute the specified audio stream or video stream containing an audio track. Use this when certain audio stream content does not need to be output.

**Notes**

Mute the specified audio stream. If the target is an individual audio stream, mute it directly. If the target is a video stream containing an audio track, it will only affect the audio part of the video stream without impacting the video footage.

**Type**

```ts
(streamId?: string) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|streamId |string \| undefined |No |None |The ID of the stream to mute. If omitted, mute all streams. |


<span id="unmuteaudiostream"></span>
### unmuteAudioStream()  

Cancel the mute operation for a specific audio stream or unmute all audio streams.

**Type**

```ts
(streamId?: string) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|streamId |string \| undefined |No |None |The stream ID to unmute. If omitted, all streams will be unmuted. |


<span id="setproperty"></span>
### setProperty()  

Set streaming and capturing related configuration properties, including video resolution, frame rate, bitrate, audio sampling rate, etc. Suitable for scenarios where key configurations need to be adjusted, such as adjusting the clarity of video capture or selecting a streaming protocol (e.g., RTM) based on the target service.

**Notes**


* Some attributes need to be configured before starting the stream (such as resolution and frame rate). Please ensure to call the relevant configuration before starting the stream.

* The attribute `setPushMode` should be configured during the initialization stage and does not support dynamic switching.


**Type**

```ts
<K extends keyof IProperty>(key: K, value: IProperty[K]) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|key |K |Yes |None |The name of the attribute to be set. |
|value |[IProperty](https://docs.byteplus.com/en/docs/24/37448#iproperty)[K] |Yes |None |Fill in the value of the corresponding attribute according to the type of `key`. |


<span id="setvideoquality"></span>
### setVideoQuality()  

Set the video quality for streaming and capturing.

**Type**

```ts
(quality: keyof typeof VIDEO_DEFAULT_QUALITY) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|quality |"120p" \| "180p" \| "240p" \| "360p" \| "480p" \| "720p\-1" \| "720p\-2" \| "720p\-3" \| "1080p\-1" \| "1080p\-2" \| "1080p\-3" |Yes |None |Video Quality, see [VIDEO_DEFAULT_QUALITY](https://docs.byteplus.com/en/docs/24/docs-configuration#video_default_quality). |


<span id="setaudioquality"></span>
### setAudioQuality()  

Set the quality of audio streaming and capturing, including sample rate and bitrate:


* Sample rate: Only affects the audio capture quality of the microphone.

* Bitrate: Determines the quality of the final streaming audio.


**Type**

```ts
(quality: keyof typeof AUDIO_DEFAULT_QUALITY) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|quality |"STANDARD" \| "HIGH" |Yes |None |Audio quality.<br><br>`STANDARD`: Standard audio quality (low bitrate), suitable for voice calls and poor network conditions.<br><br>`HIGH`: High audio quality (high bitrate), suitable for music streaming and high\-quality scenarios. |


<span id="stoppush"></span>
### stopPush()  

Stop streaming.

**Type**

```ts
() => Promise<void>
```


**Return Value**

`Promise<void>` Returns a `Promise` object.


* **Success**: No return value.

* **Failure**: Returns an error message.


<span id="ispushing"></span>
### isPushing()  

Determine if the current streaming is ongoing.

**Type**

```ts
() => boolean
```


**Return Value**

`boolean`


* `true`: Streaming in progress.

* `false`: Not streaming.


<span id="getstats"></span>
### getStats()  

Get the current stream status information. This function is used to monitor streaming quality and adjust parameters.

**Type**

```ts
() => Promise<StatsSnapshoot | RTMPStats | undefined>
```


**Return Value**

`Promise<`[StatsSnapshoot](https://docs.byteplus.com/en/docs/24/37448#statssnapshoot)` | `[RTMPStats](https://docs.byteplus.com/en/docs/24/37448#rtmpstats)` | undefined>` Statistics of the current stream (e.g., packet loss rate, bitrate).

<span id="getpreviewelement"></span>
### getPreviewElement()  

Get the preview `video` element. Used to set the volume or style of the preview area.

**Notes**

After starting the preview, use `getPreviewElement` to obtain the corresponding preview element and set the preview volume.

**Type**

```ts
() => HTMLVideoElement | null | undefined
```


**Return Value**

`HTMLVideoElement | null | undefined` `video` element of the preview screen.

<span id="destroy"></span>
### destroy()  

Clean up the SDK instance to avoid potential memory leaks.

**Notes**

Calling this interface during a live stream will cause the stream to be interrupted.

**Type**

```ts
() => Promise<void>
```


**Return Value**

`Promise<void>` Returns a `Promise` object.


* **Success**: No return value.

* **Failure**: Returns an error message.


<span id="static-issupported"></span>
### `static` isSupported()  

Checks whether RTM streaming is supported.

**Type**

```ts
(mode: PushMode) => Promise<boolean>
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|mode |[PushMode](https://docs.byteplus.com/en/docs/24/ref#pushmode) |Yes |None |The push streaming mode supports the value `rtm` to check if RTM streaming is supported. |


**Return Value**

`Promise<boolean>`


* `true`: The specified streaming mode is supported.

* `false`: The specified streaming mode is not supported.


<span id="iproperty"></span>
## IProperty  

Type：`interface`

Used for fine\-tuning the internal configurations of the streaming SDK, including video capture resolution, frame rate, and audio\-related parameters.

**Notes**

Set the video resolution to 1920×1080, frame rate to 30. Code example:

```js
livePusher.setProperty('setVideoResolution', { width: 1920, height: 1080 });
livePusher.setProperty('setVideoFps', 30);
```


<span id="setvideoresolution"></span>
### setVideoResolution  

Type：`{ width: number; height: number; }`

Set the video capture resolution.

**Member**


|Name |Type |Description |
|---|---|---|
|width |`number` |Resolution width. |
|height |`number` |Resolution height. |


<span id="setvideofps"></span>
### setVideoFps  

Type：`number`

Set the frame rate for video capture.

<span id="setvideobitrate"></span>
### setVideoBitrate  

Type：`number`

Set the push stream video bitrate in bps.

<span id="setaudiobitrate"></span>
### setAudioBitrate  

Type：`number`

Set the audio bitrate for push stream in bps.

<span id="setaudiosamplerate"></span>
### setAudioSampleRate  

Type：`number`

Set the microphone sampling rate in Hz.

<span id="setpushmode"></span>
### setPushMode  

Type：[PushMode](https://docs.byteplus.com/en/docs/24/ref#pushmode)

Set push stream mode.

<span id="statssnapshoot"></span>
## StatsSnapshoot  

Describes detailed information about the status of the RTM push stream, including various video and audio metrics.

**Notes**

To get a snapshot of the push stream status, see the example below:

```js
const stats = await livePusher.getStats();
console.log('Current video bitrate:', stats.video.sendBitrate);
console.log('Audio packet loss rate:', stats.audio.packetsLostPercent);
```


**Type**

```ts
{
  video?: {
    codec: string;
    sendBitrate: number;
    frameWidth: number;
    frameHeight: number;
    framesPerSecond: number;
    framesEncoded: number;
    keyFramesEncoded: number;
    framesSent: number;
    frameEncodeAvgTime: number;
    packetsSent: number;
    packetSendDelay: number;
    nackCount: number;
    firCount: number;
    pliCount: number;
    packetsLost: number;
    packetsLostPercent: number;
  };
  audio?: {
    codec: string | undefined;
    channels: number | undefined;
    sendBitrate: number | undefined;
    packetsSent: number | undefined;
    nackCount: number | undefined;
    packetsLost: number | undefined;
    packetsLostPercent: number | undefined;
  };
}
```


**Member**


|Name |Type |Description |
|---|---|---|
|video |`{ codec: string; sendBitrate: number; frameWidth: number; frameHeight: number; framesPerSecond: number; framesEncoded: number; keyFramesEncoded: number; framesSent: number; frameEncodeAvgTime: number; packetsSent: number; packetSendDelay: number; nackCount: number; firCount: number; pliCount: number; packetsLost: number; packetsLostPercent: number; } \| undefined` |Video Information. |
|codec |`string` |Use the push stream video codec method, for example, H.264. |
|sendBitrate |`number` |The push stream video bit rate, in bps. |
|frameWidth |`number` |Video resolution width. |
|frameHeight |`number` |The height of the video resolution. |
|framesPerSecond |`number` |Frame rate. |
|framesEncoded |`number` |Encoded frames. |
|keyFramesEncoded |`number` |Number of encoded keyframes. |
|framesSent |`number` |Number of frames sent. |
|frameEncodeAvgTime |`number` |The average encoding time per frame, measured in milliseconds (ms). |
|packetsSent |`number` |The number of packets sent. |
|packetSendDelay |`number` |The average buffering time before sending the data packet, measured in ms. |
|nackCount |`number` |The number of received NACK packets. |
|firCount |`number` |The number of received FIR (Full Intra Request) packets. |
|pliCount |`number` |The number of received PLI (Picture Loss Indication) packets. |
|packetsLost |`number` |Number of lost data packets. |
|packetsLostPercent |`number` |Packet loss rate. |
|codec |`string \| undefined` |Audio encoding format, such as AAC. |
|channels |`number \| undefined` |The number of audio channels, such as mono or stereo. |
|sendBitrate |`number \| undefined` |push stream audio bitrate, unit in bps |
|packetsSent |`number \| undefined` |The number of packets sent. |
|nackCount |`number \| undefined` |The number of received NACK packets. |
|packetsLost |`number \| undefined` |The number of lost data packets. |
|packetsLostPercent |`number \| undefined` |Packet loss rate. |
