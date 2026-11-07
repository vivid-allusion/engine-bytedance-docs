---
title: "Beauty Effects Extension (Web)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-148646"
---

With BytePlus RTC Beauty Effects Extension, you can apply brightening, skin\-smoothing, and sharpening effects to your video stream.

<span id="prerequisites"></span>
## Prerequisites


1. You have integrated the RTC SDK v4.47+ for basic audio & video calling.

2. See [Web SDK browser compatibility and known issues](https://docs.byteplus.com/docs/byteplus-rtc/docs-111854). Since the extension relies on WASM files that require high performance, we do not recommend using this extension on mobile devices.

3. For best performance, the following specifications are recommended.

   1. Dual\-core Intel Core i5+

   2. 8 GB+ of RAM

   3. 64\-bit operating system


<span id="implementation-procedures"></span>
## Implementation Procedures


1. Import the beauty effects extension into your project.

   * You can import the extension directly.

   ```typescript
   import RTCBeautyExtension from '@byteplus/rtc/extension-beauty';
   ```
   

   * Since v4.51.1, you can import through UMD package.

   ```typescript
   const {EffectBeautyMode, RTCBeautyExtension} = window.BytePlusRTCExtensions;
   ```
   

2. Register the beauty effects extension.

> After registering the extension, the video stream frame rate cannot be modified. You can call `setVideoEncoderConfig` to modify the frame rate before registering the extension.


```typescript
import BytePlusRTC from '@byteplus/rtc';

// Create an IRTCEngine instance.
const engine = BytePlusRTC.createEngine('appid');

// Create a beauty effects extension instance.
const beautyExtension = new RTCBeautyExtension();
// Register the beauty effects extension.
try {
  await engine.registerExtension(beautyExtension);
} catch (error) {
  // Failed to register. See error.message.
}
```



3. Start capturing video and set the view and rendering mode for the local video stream. The following code snippet uses internal video capturing as an example. To enable external video capturing, see `setVideoSourceType`.

> Warning: The beauty effects apply to the main and local streams, but not to screen or remote streams. The `StreamIndex` must be `STREAM_INDEX_MAIN`.


```typescript
// Enable internal video capture.
engine.startVideoCapture();
// Set the view and the rendering mode for the local video stream.
engine.setLocalVideoPlayer(StreamIndex.STREAM_INDEX_MAIN, {
  renderDom: 'yourDomId'
});
```



4. Set the intensity for the brightness, smoothness, and sharpness effects. See [setBeautyIntensity ](https://docs.byteplus.com/docs/byteplus-rtc/docs-148646#setbeautyintensity).


```typescript
import { EffectBeautyMode } from '@byteplus/rtc/extension-beauty';

// Set brightness intensity.
beautyExtension.setBeautyIntensity(EffectBeautyMode.EFFECT_WHITE_MODE, 0.2);
// Set smoothness intensity.
beautyExtension.setBeautyIntensity(EffectBeautyMode.EFFECT_SMOOTH_MODE, 0.2);
// Set sharpness intensity.
beautyExtension.setBeautyIntensity(EffectBeautyMode.EFFECT_SHARPEN_MODE, 0.2);
```



5. Enable basic beauty effects.

> Note: If you do not set the intensity before enabling beauty effects, the brightness, smoothness, and sharpness levels will all default to 0.5.


```typescript
// Enable basic beauty effects.
beautyExtension.enableBeauty();
```



6. Disable basic beauty effects.

> Note: If you call [enableBeauty ](https://docs.byteplus.com/docs/byteplus-rtc/docs-148646#enablebeauty)after [disableBeauty ](https://docs.byteplus.com/docs/byteplus-rtc/docs-148646#disablebeauty), the extension uses the previously configured intensity settings. If you destroy the engine, the beauty effect settings are discarded.


```typescript
// Disable basic beauty effects.
beautyExtension.disableBeauty();
```


<span id="api-reference"></span>
## API Reference

<span id="irtcbeautyextension"></span>
### IRTCBeautyExtension

Type: `interface`


* **API**



|Method |Description |
|---|---|
|[checkCompatibility](https://docs.byteplus.com/docs/byteplus-rtc/docs-148646#irtcbeautyextension-checkcompatibility) |Checks if the current browser is compatible with the beauty effects extension. |
|[enableBeauty](https://docs.byteplus.com/docs/byteplus-rtc/docs-148646#irtcbeautyextension-enablebeauty) |Enable basic beauty effects. |
|[disableBeauty](https://docs.byteplus.com/docs/byteplus-rtc/docs-148646#irtcbeautyextension-disablebeauty) |Disable basic beauty effects. |
|[setBeautyIntensity](https://docs.byteplus.com/docs/byteplus-rtc/docs-148646#irtcbeautyextension-setbeautyintensity) |Set the beauty effect intensity. |


<span id="checkcompatibility"></span>
#### checkCompatibility  

Checks if the current browser is compatible with the beauty effects extension.


* **Type**

   ```ts
   () => Promise<CompatibilityCheckResult>
   ```
   

* **Return Value**

   Type: Promise<[CompatibilityCheckResult ](https://docs.byteplus.com/docs/byteplus-rtc/docs-148646#compatibilitycheckresult)\>

   Compatibility check result.


<span id="enablebeauty"></span>
#### enableBeauty  

Enable basic beauty effects.


* **Type**

   ```ts
   () => void
   ```
   

* **Notes**

   * Call [setBeautyIntensity ](https://docs.byteplus.com/docs/byteplus-rtc/docs-148646#setbeautyintensity)to set the beauty effect intensity. If you do not set the intensity, the brightness, smoothness, and sharpness intensity will default to 0.5.

   * Call [disableBeauty ](https://docs.byteplus.com/docs/byteplus-rtc/docs-148646#disablebeauty)to turn off basic beauty effects.

   * This API is not applicable to screen capturing.


<span id="disablebeauty"></span>
#### disableBeauty  

Disable basic beauty effects.


* **Type**

   ```ts
   () => void
   ```
   


<span id="setbeautyintensity"></span>
#### setBeautyIntensity  

Set the beauty effect intensity.


* **Type**

   ```ts
   (beautyMode: EffectBeautyMode, intensity: number) => void
   ```
   

* **Notes**

   * If you call this API before calling [enableBeauty ](https://docs.byteplus.com/docs/byteplus-rtc/docs-148646#enablebeauty), the default settings of beauty effect intensity will adjust accordingly.

   * If you destroy the engine, the beauty effect settings are discarded.

* **Parameters**

   * **beautyMode**

      Type: [EffectBeautyMode](https://docs.byteplus.com/docs/byteplus-rtc/docs-148646#effectbeautymode)

      Basic beauty effect.

   * **intensity**

      Type: `number`

      The intensity of the beauty effect ranges from 0.0 to 1.0, with a default value of 0.5. When you set it to 0, the beauty effect will be turned off.


<span id="compatibilitycheckresult"></span>
### CompatibilityCheckResult  

Type: `interface`

Compatibility check result.

**isCompatible**  ** ** 

Type: `boolean`

Whether the system is compatible.

`true`: The system meets the requirements.

`false`: Incompatible.

**reasons**  ** ** 

Type: `number[]`

Incompatible reasons.


* 0: Other unknown reasons.

* 1: The browser does not support the getUserMedia API.

* 2: Browser does not support WebAssembly.

* 3: The browser cannot access video input devices.

* 100: Failed to load WebAR SDK.


<span id="effectbeautymode"></span>
### EffectBeautyMode  

Type: `enum`

Basic beauty effect mode.


* **Member**

   
   |Property |Value |Description |
   |---|---|---|
   |EFFECT_WHITE_MODE |`0` |Brightness. |
   |EFFECT_SMOOTH_MODE |`1` |Smoothness. |
   |EFFECT_SHARPEN_MODE |`2` |Sharpness. |
   


<span id="changelog"></span>
## Changelog


1. In RTC SDK v4.60.2, the following changes are made to this feature.

   * When creating an instance of the Beauty Effects Extension, an authentication file is required. You can obtain this file from our technical support team.

   * Browser compatibility changed as follows.

      
      |Type |Browser |
      |---|---|
      |Desktop |Chrome 78 |
      ||Safari 15 |
      ||Firefox 80 |
      ||Edge 83 |
      |Mobile |Chrome 78 |
      ||Safari 15.4 |
      ||Wechat's built\-in browser 8.0.32 |
      

2. In RTC SDK v4.52, the following changes are made to this feature.

   * After registration, the beauty effect is no longer enabled by default; you must call [enableBeauty ](https://docs.byteplus.com/docs/byteplus-rtc/docs-148646#enablebeauty)to enable it.

   * The method names changed from `enable` to `enableBeauty`, and from `disable` to `disableBeauty`. The original methods are now deprecated.

   * The browser compatibility for this feature was optimized, with minimum supported versions changed from Chrome 94+ and Edge 94+ to Chrome 70+, Edge 83+, Safari 12+, and Firefox 80+. This aligns with the current [Web SDK browser compatibility and known issues](https://docs.byteplus.com/docs/byteplus-rtc/docs-111854).

3. This feature is available since RTC SDK v4.47.
