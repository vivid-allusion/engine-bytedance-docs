---
title: "Beauty Effects on Electron"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1134358"
---

You can choose one of the two ways to equip your app with the beauty effects provided by the RTC SDK.

* Standard Beauty includes brightness, smoothness, and sharpness effects, which are widely used in video chat and video streaming scenarios.

* Advanced Beauty provides the Standard Beauty effects, as well as color filters and background stickers. Prior to integration, you must purchase [BytePlus Effects](https://www.byteplus.com/en/product/effects).

## Prerequisite

* Your app already has real\-time video and audio communication capabilities by integrating with the Electron RTC SDK.

* Hardware requirements:

   * macOS: macOS 10.11+

   * Windows: Win 7+

* Ensure your device has Internet access and the system time is correct as the beauty module needs to download resources from the internet for initialization.

## Procedure

### Step 1. Integrate the beauty module

1. Locate the dynamic library files from the RTC SDK.

   * [Windows](https://docs.byteplus.com/en/docs/12/docs-75707): BytePlusRTC/bin/Win32(x64)/effect.dll and pthreadVC2.dll

   * [macOS](https://docs.byteplus.com/en/docs/12/docs-75707): libeffect.dylib

2. Update the packaging settings to copy the dynamic library files to the designated directory.

   For the electron\-builder, specify the target path in the `extraResources` field.

   * Windows: Same folder as the main program

   * macOS: Frameworks/\*

```json
  "build": {
    "win": {
       "extraResources": [
        {
          "from": "./effect.dll",
          "to": "../effect.dll" 
        },
        {
          "from": "./pthreadVC2.dll",
          "to": "../pthreadVC2.dll" 
        }
      ]
    },
    "mac": {
       "extraResources": [
        {
          "from": "./libeffect.dylib",
          "to": "../Frameworks/libeffect.dylib"
        }
      ]
    }
  }
```

### Step 2. Add resources

Download the beauty resource package from BytePlus Effects and copy the extracted resource directory into your Electron project's packaged resources directory.

```text
basic_beauty/
  ComposeMakeup/
    beauty_Android_lite/
    ...
```

### Step 3. Initialize

Create and initialize an `RTCEngine` instance, and then call [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startvideocapture) to start local video capture.

```TypeScript
const { RTCEngine } = require('@byteplus/byteplus-electron-sdk');

const rtcEngine = new RTCEngine();
const ret = rtcEngine.createRTCEngine({
  app_id: APP_ID,
  parameters: '',
});
if (ret === 0) {
  rtcEngine.startVideoCapture();
}
```

### Step 4. Enable beauty effect

Call [enableEffectBeauty](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableeffectbeauty) and pass `true` to the argument `enabled` to enable the beauty effect.

> The first time you call [enableEffectBeauty](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableeffectbeauty) after app installation, it returns `1004`. This indicates that the SDK is downloading the necessary resource files for the beauty feature. After the download is complete, subsequent calls to this API return `0`, and you can instantly preview the beauty effects on the local video.

The intensity of the brightness, smoothness, and sharpness effects is set to 0.5 by default.

```TypeScript
const beautyRet = rtcEngine.enableEffectBeauty(true);
if (beautyRet !== 0 && beautyRet !== 1004) {
  console.error(`Failed to enable beauty effects: ${beautyRet}`);
}
```

### Step 5. Set intensity for the effect

Call [setBeautyIntensity](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setbeautyintensity) to set the beauty effect intensity either before or after enabling the beauty effect.

The valid range is from 0 to 1. Set it to 0 to disable the corresponding beauty effect.

> You lose your intensity settings once the video engine is destroyed. The settings revert to their default values when the video engine is recreated.

```TypeScript
// EffectBeautyMode.kEffectBeautyWhite = 0
const intensityRet = rtcEngine.setBeautyIntensity(0, 0.8);
if (intensityRet !== 0) {
  console.error(`Failed to set beauty intensity: ${intensityRet}`);
}
```

### Step 6. Disable beauty effect

Call [enableEffectBeauty](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableeffectbeauty) and pass `false` to the argument `enabled` to disable the beauty effect.

```TypeScript
const disableRet = rtcEngine.enableEffectBeauty(false);
if (disableRet !== 0) {
  console.error(`Failed to disable beauty effects: ${disableRet}`);
}
```
