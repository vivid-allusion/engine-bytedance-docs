---
title: "Virtual Background (Web)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-697417"
---

In scenarios like live streaming or video conferencing, you can enhance user privacy and video quality by replacing the real\-world background with a custom image or a blur effect. This guide provides step\-by\-step instructions and API references for implementing the virtual background feature on the Web platform using the RTC SDK.

<span id="25e32d48"></span>
## **Try it Online**

We offer a web\-based demo that allows you to experience the feature without writing any code. [Try It Now](https://demo.byteplus.com/rtc/advance/virtualBackground)

<span id="prerequisites"></span>
## Prerequisites


1. This feature is provided at an additional charge. Please contact our technical support team to obtain the authentication files.

2. You have integrated the RTC SDK v4.52+ for basic audio & video calling.

3. See [Web SDK browser compatibility and known issues](https://docs.byteplus.com/docs/byteplus-rtc/docs-111854). Since the extension relies on a couple of WASM files that demand high performance, it is not recommended to use this extension on mobile devices.

4. For best performance, the following specifications are recommended.

   1. Dual\-core Intel Core i5+

   2. 8 GB+ of RAM

   3. 64\-bit operating system


<span id="implementation-procedures"></span>
## Implementation Procedures


1. Import the virtual background extension into your project.

   * Import the extension directly.

   ```TypeScript
   import RTCBeautyExtension from '@byteplus/rtc/extension-beauty';
   ```
   

   * Import through UMD package.

   ```TypeScript
   const {EffectBeautyMode, RTCBeautyExtension} = window.BytePlusRTCExtensions;
   ```
   

2. Register the virtual background extension.


> After the extension is registered, the video stream frame rate cannot be modified. You can call [setVideoSourceType](https://docs.byteplus.com/docs/byteplus-rtc/docs-104478#rtcengine-setvideosourcetype) to modify the frame rate before registering the extension.


```TypeScript
import BytePlusRTC from '@byteplus/rtc';
import RTCBeautyExtension, { BackgroundAIBackend } from '@byteplus/rtc/extension-beauty';

// Create an IRTCEngine instance.
const engine = BytePlusRTC.createEngine('appid');

// Create a virtual background extension instance. You must provide the URL of the authentication files.
const extension = new RTCBeautyExtension({ 
  authFileUrl: 'https://xxxx.auth',
  // Since v4.53, you can choose GPU mode.
  aiBackend: BackgroundAIBackend.GPU
});
// Register the extension.
try {
  await engine.registerExtension(extension);
} catch (error) {
  // Failed to register. See error.message.
}
```



3. Start capturing video and set the view and rendering mode for the local video stream. The following code snippet uses internal video capturing as an example. To enable external video capturing, see [setVideoSourceType](https://docs.byteplus.com/docs/byteplus-rtc/docs-104478#rtcengine-setvideosourcetype).


> Warning: The virtual background effect applies to the main local video stream, but not to screen\-sharing streams or remote user streams. The `StreamIndex` must be `STREAM_INDEX_MAIN`.


```TypeScript
// Enable internal video capture.
engine.startVideoCapture();
// Set the view and the rendering mode for the local video stream.
engine.setLocalVideoPlayer(StreamIndex.STREAM_INDEX_MAIN, {
  renderDom: 'yourDomId'
});
```



4. Set the virtual background mode.


```TypeScript
import { BackgroundMode } from '@byteplus/rtc/extension-beauty';

// ① (Default) Blur background.
extension.setBackgroundMode(BackgroundMode.BACKGROUND_BLUR);
// ② Image background.
extension.setBackgroundMode(BackgroundMode.BACKGROUND_IMAGE);
extension.loadBackgroundImage('https://image_url');
```



5. Enable virtual background.


```TypeScript
extension.enableVirtualBackground();
```



6. Disable virtual background.


```TypeScript
extension.disableVirtualBackground();
```


<span id="api-reference"></span>
## API Reference

<span id="irtcbeautyextension"></span>
### IRTCBeautyExtension

Type: `interface`

<span id="checkcompatibility"></span>
#### checkCompatibility  

Checks the compatibility of the current browser.


* **Type**

   ```ts
   () => Promise<CompatibilityCheckResult>
   ```
   

* **Return Value**

   Type: `Promise<`[CompatibilityCheckResult  ](https://docs.byteplus.com/docs/byteplus-rtc/docs-697417#compatibilitycheckresult)`>`

   The result of the compatibility check.


<span id="enablevirtualbackground"></span>
#### enableVirtualBackground  

Enable virtual background.


* **Type**

   ```ts
   () => void
   ```
   

* **Notes**

   * Call [setBackgroundMode  ](https://docs.byteplus.com/docs/byteplus-rtc/docs-697417#setbackgroundmode) to set the virtual background mode. If you do not set the mode, the blur background will be enabled.

   * Call [disableVirtualBackground  ](https://docs.byteplus.com/docs/byteplus-rtc/docs-697417#disablevirtualbackground) to turn off virtual background.

   * This API is not applicable to screen capturing.


<span id="disablevirtualbackground"></span>
#### disableVirtualBackground  

Disable virtual background.


* **Type**

   ```ts
   () => void
   ```
   


<span id="setbackgroundmode"></span>
#### setBackgroundMode  

Sets the virtual background mode.


* **Type**

   ```ts
   (mode: BackgroundMode) => void
   ```
   

* **Notes**

   After enabling the virtual background, you can call this API to switch the virtual background mode.

* **Parameters**

   * **mode**

      Type: [BackgroundMode  ](https://docs.byteplus.com/docs/byteplus-rtc/docs-697417#backgroundmode)

      Virtual background mode.


<span id="getbackgroundimage"></span>
#### getBackgroundImage  

Gets the current virtual background image.


* **Type**

   ```ts
   () => string
   ```
   

* **Return Value**

   Type: `string`

   The URL of the current virtual background image.


<span id="loadbackgroundimage"></span>
#### loadBackgroundImage  

Set the virtual background image. Ensure that the background mode is set to `BACKGROUND_IMAGE`.


* **Type**

   ```ts
   (url: string) => Promise<void>
   ```
   

* **Notes**

   * You can upload a .JPG, .PNG, or .JPEG file.

   * If the image's aspect ratio differs from the video's, the image is scaled to fit while maintaining its aspect ratio, and then cropped to fill the video frame.

   * The transparent area in the image will be filled with black.

   * This setting persists for the lifecycle of the extension.

* **Parameters**

   * **url**

      Type: `string`

      URL of the virtual background image.

* **Return Value**

   Type: `Promise<void>`


<span id="setaimodeltype"></span>
#### setAIModelType  

Set the priority of the facial recognition AI algorithm.


* **Type**

   ```ts
   (type: BackgroundAIModelType) => void
   ```
   

* **Parameters**

   * **type**

      Type: [BackgroundAIModelType  ](https://docs.byteplus.com/docs/byteplus-rtc/docs-697417#backgroundaimodeltype)

      The priority of the facial recognition AI algorithm.


<span id="setbackgroundblurradius"></span>
#### setBackgroundBlurRadius  

Sets the radius of the blur effect, measured in pixels (px). Ensure that the background mode is set to `BACKGROUND_BLUR`.


* **Type**

   ```ts
   (radius: number) => void
   ```
   

* **Notes**

   This setting persists for the lifecycle of the extension.

* **Parameters**

   * **radius**

      Type: `number`

      The radius of the blur effect. The blur radius defaults to 20 px.

      The valid range for the radius is [0, ∞). However, note that the blur effect will no longer change beyond the half of the longer side of the video.

      For example, in a video of 640x480, if you set a blur radius greater than 320 pixels, it will have the same effect as setting it to 320 pixels.


<span id="setbackgroundcolor"></span>
#### setBackgroundColor  

Set the background color. Ensure that the background mode is set to `BACKGROUND_COLOR`.


* **Type**

   ```ts
   (color: string) => boolean
   ```
   

* **Notes**

   This setting persists for the lifecycle of the extension.

* **Parameters**

   * **color**

      Type: `string`

      Color specified as RGBA(red, green, blue, alpha) or #RRGGBBAA.

      Each component's value ranges from 0 to 255. The alpha component represents the opacity of the color and ranges from `0` (transparent) to `1` (opaque).

      For example, rgba(255, 255, 255, 1) represents the color white with full opacity.

      You can also use the hexadecimal color format #RRGGBBAA, where each pair of digits represents the values for red, green, blue, and alpha components. The alpha component ranges from 00 (transparent) to FF (opaque). For example, #FFFFFFFF represents the color white with full opacity.

* **Return Value**

   Type: `boolean`

   * `true`: Success.

   * `false`: Failure.


<span id="loadbackgroundvideo"></span>
#### loadBackgroundVideo  

Sets the URL of the virtual background video. Ensure that the background mode is set to `BACKGROUND_VIDEO`.


* **Type**

   ```ts
   (url: string) => Promise<void>
   ```
   

* **Notes**

   The setting can be stored and continue to be effective throughout the duration of the extension's lifecycle.

* **Parameters**

   * **url**

      Type: `string`

      URL of the virtual background video.

* **Return Value**

   Type: `Promise<void>`

   A rejected Promise is returned if an error occurs.


<span id="getbackgroundvideo"></span>
#### getBackgroundVideo  

Gets the URL of the virtual background video. Ensure that the background mode is set to `BACKGROUND_VIDEO`.


* **Type**

   ```ts
   () => string
   ```
   

* **Notes**

   This setting persists for the lifecycle of the extension.

* **Return Value**

   Type: `string`

   URL of the virtual background video.


<span id="compatibilitycheckresult"></span>
### CompatibilityCheckResult  

Type: `interface`

Compatibility check result.

**isCompatible **  ** ** 

Type: `boolean`

Whether the system is compatible.

`true`: The system meets the requirements.

`false`: Incompatible.

**reasons **  ** ** 

Type: `number[]`

The reasons for incompatibility.


* 0: Other unknown reasons.

* 1: Browser does not support getUserMedia API.

* 2: Browser does not support WebAssembly.

* 3: The browser cannot access video input devices.

* 100: Failed to load WebAR SDK.


<span id="irtcbeautyextensionconfig"></span>
### IRTCBeautyExtensionConfig  

Type: `interface`

Beauty extension configuration.

**authFileUrl **  ** ** 

Type: `string`

The authentication file's URL.

**aiBackend **  ** ** 

Type: [BackgroundAIBackend  ](https://docs.byteplus.com/docs/byteplus-rtc/docs-697417#backgroundaibackend)

Whether to use CPU or GPU mode. CPU mode is set by default.

**aiModelType **  ** ** 

Type: [BackgroundAIModelType  ](https://docs.byteplus.com/docs/byteplus-rtc/docs-697417#backgroundaimodeltype)

The priority of the facial recognition AI algorithm.

<span id="backgroundmode"></span>
### BackgroundMode  

Type: `enum`

Virtual background mode.


* **Member**

   
   |Property |Value |Description |
   |---|---|---|
   |BACKGROUND_BLUR |`'blur'` |Blur background. |
   |BACKGROUND_IMAGE |`'image'` |Image background. |
   


<span id="backgroundaimodeltype"></span>
### BackgroundAIModelType  

Type: `enum`

The priority of the facial recognition AI algorithm.


* **Member**

   
   |Property |Value |Description |
   |---|---|---|
   |PERFORMANCE |`0` |Performance mode. |
   |QUALITY |`1` |Quality mode. |
   


<span id="backgroundaibackend"></span>
### BackgroundAIBackend  

Type: `enum`

Whether to use CPU or GPU mode. CPU mode is set by default.


* **Member**

   
   |Property |Value |Description |
   |---|---|---|
   |CPU |`-1` |CPU mode. |
   |GPU |`1` |GPU mode. The SDK will check whether the current browser supports GPU mode, and will automatically fall back to CPU mode if GPU mode is not supported. |
   


<span id="changelog"></span>
## Changelog


1. In RTC SDK v4.60.2, the following changes are made to this feature.

* The following literal values in the enumeration types have been modified:

   * Value of `BackgroundMode`.`BACKGROUND_IMAGE` changed from `'image'` to `'image-url'`.

   * Value of `BackgroundAIModelType`.`PERFORMANCE` changed from `0` to `'fast'`, while `QUALITY` changed from `1` to `'accurate'`.

   * Value of `BackgroundAIBackend`.`CPU` changed from `-1` to `'cpu'`, while `GPU` changed from `1` to `'gpu'`.

* New options for `BackgroundMode`, including choosing a video or a solid color.

* The blur radius can be adjusted for the blur background.

* Browser compatibility changed as follows.

   
   |Type |Browser |
   |---|---|
   |Desktop |Chrome 78 |
   ||Safari 15 |
   ||Firefox 80 |
   ||Edge 83 |
   |Mobile |Chrome 78 |
   ||Safari 15.4 |
   ||WeChat's built\-in browser 8.0.32 |
   

1. Since RTC SDK v4.53, you can choose GPU mode when initializing.

2. This feature is available since RTC SDK v4.52.
