---
title: "Beauty Effects on Flutter"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1182380"
---

This article introduces how to use the basic Beauty Effects function of the free version. Different from Video Effects, the paid feature, basic Beauty Effects provide effects including whitening, sharpening and smoothing, which are widely used in video chat and video streaming. If you need more effects such as color filters, stickers, or style makeup, we recommend that you refer to [Video Effects (paid feature)](https://docs.byteplus.com/en/docs/12/docs-114717) for more details.

<span id="prerequisite"></span>
## Prerequisite


* You have already implemented video communications by integrating RTC SDK.

* You have already integrated CV SDK. Beauty Effects rely on Effects SDK provided in the RTC SDK package. You can also choose other versions of Effects SDK (the minimum required version is 4.3.2).

* Beauty Effects requires an initial network connection to download necessary files. Please ensure that your device is connected to the internet and the system time is accurate.


<span id="procedure"></span>
## Procedure

<span id="initialize"></span>
### Initialize

Call `createRTCVideo` to create an engine instance and call `startVideoCapture`. Once the beauty effect is enabled, you will be able to see the effect in the local preview.

```Dart
RTCVideo rtcVideo = await RTCVideo.createRTCVideo(engineContext)
rtcVideo.startVideoCapture();
```


<span id="enable-beauty-effects"></span>
### Enable beauty effects

Call `enableEffectBeauty` and set the `enable` parameter to `true`.

> Note:

> When calling this interface for the first time after installing the app, it may return an error code '\-1004', which indicates that the beauty files are being downloaded. After the download is complete, you must call the method again to apply the effect. This subsequent call will take effect immediately and return 0. At this point, you will be able to see the effect in the local preview.


```Dart
int? ret = await rtcVideo.enableEffectBeauty(true);
```


<span id="set-intensity-for-the-effect"></span>
### Set intensity for the effect

You can update the beauty intensity by calling the `setBeautyIntensity` interface. The valid range for intensity is [0, 1], and the method call will fail for any value outside this range. When the intensity is set to 0, no beauty effect will be applied.

```Dart
int? ret = await rtcVideo.setBeautyIntensity(beautyMode: EffectBeautyMode.white, intensity: 0.8);
```
