---
title: "Beauty Effects on Native"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-372605"
---

To enhance user appearance in video chats and live streams, you can implement the basic Beauty Effects function. This free feature provides whitening, sharpening, and smoothing effects. This guide demonstrates how to enable the function and set the intensity of each effect. For more advanced options such as color filters and background stickers, see the paid [Video Effects (paid feature)](https://docs.byteplus.com/en/docs/12/docs-114717) feature.

<span id="changelogs"></span>
## **Changelogs**

Beauty Effects (Native) is available since v3.42.

<span id="prerequisite"></span>
## **Prerequisite**


* You have implemented video communications by integrating RTC SDK.

* Beauty Effects rely on Effects SDK provided in the [RTC SDK package](https://docs.byteplus.com/en/docs/12/docs-75707#download-sdk). You can also choose other versions of Effects SDK (version 4.3.2 or earlier).

* Beauty Effects requires an initial network connection to download necessary files. Please ensure that your device is connected to the internet and the system time is accurate.


<span id="procedure"></span>
## Procedure


1. Call `enableEffectBeauty` and set the parameter `enable` to `true` to enable the beauty effect. If the beauty effect intensity is not set before enabling the beauty effect, the intensity for whitening, sharpening, and skin smoothing is 0.5 by default.

2. Call `setBeautyIntensity` to set the beauty effect intensity. If you set the intensity before enabling the beauty effect, the effect starts with the specified intensity. If you destroy the engine, the intensity settings are reset. The intensity will revert to the default value when the beauty effect is enabled again.

3. Call `enableEffectBeauty` and pass `false` to the argument `enable` to disable the beauty effect.


<span id="note"></span>
## Note

When you install the app for the first time, calling `enableEffectBeauty(true)` will return `-1004`, indicating that the required files for beauty effects are being downloaded. Once the download is complete, the beauty effect is automatically enabled, and subsequent calls to enable the effect will return `0`.

The valid range for beauty intensity is from 0 to 1. A value of 0 disables the effect.

<span id="sample-code"></span>
## Sample code

<span id="android"></span>
### Android

```Java
// Enable beauty effects. After enabling, the default intensity for whitening, skin smoothing, and sharpening is 0.5.
mRTCEngine.enableEffectBeauty(true);
// Sets the beauty intensity. For example, set the whitening intensity to 0.8.
mRTCEngine.setBeautyIntensity(EffectBeautyMode.EFFECT_WHITE_MODE, 0.8);
// Disables beauty effects.
mRTCEngine.enableEffectBeauty(false);
// Sets the skin smoothing intensity. For example, set the skin smoothing intensity to 0.2.
mRTCEngine.setBeautyIntensity(EffectBeautyMode.EFFECT_SMOOTH_MODE, 0.2);
// Enables beauty effects. After enabling, the whitening intensity is 0.8, the skin smoothing intensity is 0.2, and the sharpening intensity is 0.5.
mRTCEngine.enableEffectBeauty(true);
java
```


<span id="ios"></span>
### iOS

```objectivec
// Enable beauty effects. After enabling, the intensity for whitening, skin smoothing, and sharpening are all set to 0.5.
[self.RTCEngine enableEffectBeauty:YES];
// Set the beauty intensity. For example, set the whitening intensity to 0.8.
[self.RTCEngine setBeautyIntensity:ByteRTCEffectWhiteMode withIntensity:0.8f];
// Disable beauty effects. After disabling, there will be no beauty effect on the image.
[self.RTCEngine enableEffectBeauty:NO];
// Set the skin smoothing intensity. For example, set the skin smoothing intensity to 0.2.
[self.RTCEngine setBeautyIntensity:ByteRTCEffectSmoothMode withIntensity:0.2f];
// Enable beauty effects. After enabling, the whitening intensity is 0.8, the skin smoothing intensity is 0.2, and the sharpening intensity is 0.5.
[self.RTCEngine enableEffectBeauty:YES];
objectivec
```


<span id="api-reference"></span>
## API reference


| |Android |iOS |Windows |
|---|---|---|---|
|Enable/disable beauty effects |[enableEffectBeauty](https://docs.byteplus.com/en/docs/12/docs-70080#enableeffectbeauty) |[enableEffectBeauty](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-enableeffectbeauty) |[enableEffectBeauty](https://docs.byteplus.com/en/docs/12/docs-70095#enableeffectbeauty) |
|Set beauty effect intensity |[setBeautyIntensity](https://docs.byteplus.com/en/docs/12/docs-70080#setbeautyintensity) |[setBeautyIntensity:withIntensity:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setbeautyintensity-withintensity) |[setBeautyIntensity](https://docs.byteplus.com/en/docs/12/docs-70095#setbeautyintensity) |
