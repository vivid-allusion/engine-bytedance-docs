---
title: "Web SDK browser compatibility and known issues"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-111854"
---

To ensure a stable, high\-quality real\-time communication experience in your web application, it is crucial to understand the browser compatibility of the Volcengine Web RTC SDK. This document provides a comprehensive reference on supported browsers, known issues with their solutions, and specific functional limitations you may encounter during development.

<span id="浏览器兼容性"></span>
## Supported browsers

We recommend using the latest stable version of your browser for a higher\-quality, more stable audio and video call experience.

<span id="5453d263"></span>
### Desktop


|Operating system |Browser |Minimum browser version requirements |Subscribe to audio and video streams (pull stream) |Publish audio and video streams (push stream) |Screen sharing |
|---|---|---|---|---|---|
|Windows |Chrome |70 |✅ |✅ |✅ (requires Chrome 74 or above) |
||Edge |83 |✅ |✅ |✅ (requires Edge 99 or above) |
||Firefox |80 |✅ |✅ |✅ |
||360 Extreme Browser |13 |✅ |✅ |✅ |
|macOS |Safari |12 |✅ |✅ |✅ (requires Safari 13 or above) |
||Chrome |70 |✅ |✅ |✅ (requires Chrome 74 or above) |
||Edge |83 |✅ |✅ |✅ (requires Edge 99 or above) |
||Firefox |80 |✅ |✅ |✅ |
||360 Extreme Browser |13 |✅ |✅ |✅ |


<span id="移动端"></span>
### Mobile

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Browser support on Android depends on device hardware and the version of WebView used.</div>



|Operating system |Browser |Minimum browser version requirements |Subscribe to audio and video streams (pull stream) |Publish audio and video streams (push stream) |Screen sharing |
|---|---|---|---|---|---|
|Android |Chrome |86 |✅ |✅ |❌ |
||WeChat embedded browser |8.0.32 |✅ |✅ |❌ |
|iOS 12+ |Safari |Consistent with operating system version |✅ |✅ |❌ |
||Chrome |No explicit information |✅ |❌ |❌ |
||WeChat embedded browser |8.0.32 |✅ |❌ |❌ |
|iOS 14.3+ |Safari |Consistent with operating system version |✅ |✅ |❌ |
||Chrome |No explicit information |✅ |✅ |❌ |
||WeChat embedded browser |8.0.32 |✅ |✅ |❌ |


<span id="浏览器已知问题"></span>
## Browser known issues

This section lists the known browser issues and solutions for the Web RTC SDK.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Unless there are special requirements, it is recommended to use VP8 video encoding. Using H.264 encoding may cause a series of issues after enabling hardware acceleration, including frame rate, bit rate, and resolution not reaching target values; garbled screen, black screen; poor experience in weak network environments, and more.</div>


<span id="桌面端"></span>
### Desktop


|**Browser** |**Known issues and solutions** |
|---|---|
|Chrome |* On certain Windows devices, hardware acceleration for video rendering may cause screen jitter.<br><br>   Solution: Disable hardware acceleration.<br><br>* When using Chrome on Windows devices for screen sharing, selecting to share WeChat, QQ, DingTalk, or WPS application windows may result in a black screen during capture, or a black screen when dragging the application window.<br><br>   Solution: It is recommended to share the entire screen.<br><br>* When using a microphone with `deviceId` set to `"default"` or `"communications"` on Windows devices, if a new microphone is plugged in and then removed, the original microphone capture may be interrupted.<br><br>   Solution: Avoid using microphones with `deviceId` set to `"default"` or `"communications"`.<br><br>* When using Chrome and Safari simultaneously for audio and video calls on the same PC device, the subscriber may experience lower audio volume in Chrome and find that video images in Safari are slightly larger than those in Chrome. |
|Safari |* When taking screenshots of externally captured video in Safari 16, the screenshot is a black screen.<br><br>* Safari 13 may not be able to hear remote users' audio. |
|Firefox |* Because Firefox does not have an RTP extension header for rotating video frames, when using Firefox to communicate with other devices, users on Firefox may see rotated video images from other devices.<br><br>   Solution: Use CSS to achieve rotation.<br><br>* Firefox only supports setting the video frame rate to 30 FPS.<br><br>* When Firefox is installed for the first time, the H.264 codec will be dynamically installed while online. Before installation is complete, Web SDK streaming will not function correctly.<br><br>   Solution: Call [getSupportedCodecs](https://docs.byteplus.com/en/docs/12/docs-104478#byteplusrtc-getsupportedcodecs) to obtain the codec types supported by the current browser. If Firefox is detected to not support the H.264 codec, use Firefox to open `about:addons`, check the installation status of OpenH264 under "Plugins", and wait for the installation to complete before making a call.<br><br>* Due to browser limitations, Firefox does not support the simulcast feature. |


<span id="394e426d"></span>
### Mobile


|**Platform** |**Known issues and solutions** |
|---|---|
|Android |* Due to restrictions on Huawei devices, some versions of the Huawei browser and the Chrome browser on Huawei devices cannot publish or subscribe to video streams.<br><br>   Solution: Use VP8 encoding.<br><br>* On certain Android 12 devices (such as Google Pixel 3/Pixel 4, Redmi K50), enabling video hardware encoding in Chrome or Chromium\-based browsers below version 97 may cause screen artifacts.<br><br>   Solution: Use Chrome 97 or above.<br><br>* Audio routing on Android is managed by the operating system and cannot be modified by Chromium. Consequently, in some Chromium\-based browsers (such as version 97.0.4692.98, common on Honor phones), when a user switches from the speaker to a Bluetooth headset, the remote audio may continue to play through the phone's speaker or earpiece, potentially causing low or no volume. See Chromium Issue 1317548. It is recommended to use the Chrome browser, version M106 or above.<br><br>* Simulcast cannot be sent using H.264 encoding on Android Chrome.<br><br>   Solution: Use VP8 encoding.<br><br>* On some Xiaomi, OnePlus, and Vivo models, if a user captures and sends audio using a Bluetooth headset, the remote user may not hear any audio.<br><br>* When hardware acceleration is enabled in Chrome 88, using HTMLMediaElement.captureStream to publish MP4 files results in a black screen for remote viewers. See [Chromium Issue 1156408](https://bugs.chromium.org/p/chromium/issues/detail?id=1156408).<br><br>   Solution: Upgrade to Chrome 96 or above.<br><br>* On Huawei MediaPad M5 lite, when using Chrome or the default browser, the first Bluetooth connection cannot switch to the Bluetooth headset; only the second connection allows normal switching.<br><br>* On Huawei P30 Pro, the default camera used may vary depending on different capture parameter settings. To specify the front or rear camera, it is recommended not to use the default value during capture.<br><br>* Support for H.264 in Android Chrome depends on hardware; some Android devices do not support the H.264 codec format. Compatibility can be checked by calling the [isSupported](https://docs.byteplus.com/en/docs/12/docs-104478#byteplusrtc-issupported) interface.<br><br>* The built\-in browser on Xiaomi phones does not support WebRTC. |
|iOS |* On iOS 15.x, all browsers and applications embedded with WKWebView (such as WeChat browser and Chrome browser) may experience video playback black screens when playing videos in the DOM and adding certain CSS properties (such as `transform` or `animation`) to the `video` element or its parent element, or after changing CSS properties to redraw the video rendering area. See [Webkit Bug 230532](https://bugs.webkit.org/show_bug.cgi?id=230532).<br><br>   Solution: Minimize changes to the CSS properties of the `video` element and its parent elements.<br><br>* Using H.264 streaming on iOS 15.1 causes page crashes. See [Webkit Bug 232381](https://bugs.webkit.org/show_bug.cgi?id=232381), [Webkit Bug 231505](https://bugs.webkit.org/show_bug.cgi?id=231505).<br><br>   Solution: Use iOS 15.2+ or stream with VP8.<br><br>* On iPhone 14 Pro/iPhone 14 Pro Max devices running iOS 16.0, audio capture may fail or audio may be interrupted.<br><br>   Solution: Use iOS 16.1+.<br><br>* Versions below iOS 15 cannot use the `video` element to play external video captured by `canvas.captureStream`. See [Webkit Bug 181663](https://bugs.webkit.org/show_bug.cgi?id=181663).<br><br>   Solution: Use iOS 15+.<br><br>* Versions below iOS 15 cannot switch to the built\-in microphone when headphones are connected, and always use the headphone microphone for input. See [Webkit Bug 233634](https://bugs.webkit.org/show_bug.cgi?id=233634).<br><br>* On iPad devices running versions below iOS 15, calling [enumerateDevices](https://docs.byteplus.com/en/docs/12/docs-104478#byteplusrtc-enumeratedevices) cannot obtain information about external audio input devices.<br><br>   Solution: Use iOS 15+.<br><br>* On iOS 13 and iOS 14, remote user volume may change randomly.<br><br>* When switching between front and rear cameras, the captured image may rotate momentarily.<br><br>* Audio routing is unstable; audio may play through the speaker when external headphones are connected, or automatically switch between the speaker and earpiece when headphones are not connected.<br><br>* When calling getUserMedia twice in succession to obtain tracks of the same media type, the first media track may be muted or display a black screen. Avoid this operation.<br><br>* After using audio or video input devices in other applications (such as Siri or WeChat), local audio or video cannot be captured via the Web SDK.<br><br>* In iOS 11 and 12, the RTP extension header for rotating video frames does not take effect.<br><br>   Solution: Use CSS to implement rotation.<br><br>* On iOS 15, the Safari browser and applications with embedded WKWebView on iOS 14.4 to iOS 15 (such as the WeChat browser and Chrome browser) experience interruptions in audio stream transmission when the browser or application switches to the background. See [Webkit Bug 231105](https://bugs.webkit.org/show_bug.cgi?id=231105) and [Apple forum discussion](https://developer.apple.com/forums/thread/689182).<br><br>   Solution: Locally listen for the visibilityChange event. If the application is switched to the background, notify remote users via signaling so that a prompt appears in their UI. |


<span id="功能已知限制"></span>
## Known functional limitations

The following section lists the known functional limitations of the Web RTC SDK.

<span id="屏幕共享"></span>
### Screen sharing


* The [startScreenCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104478#startscreencapture) method is only supported on desktop (Windows and macOS), and the required browsers and versions are as follows:

   * Chrome 74+

   * Firefox 80+

   * Edge 99+

   * Safari 13+

   * 360 Secure Browser 13+ (Windows does not support sharing tabs)

* Only Chrome, Edge, and 360 Secure Browser support sharing screen audio, that is, the [startScreenCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104478#startscreencapture) method's `screenConfig.enableAudio` parameter. Support for screen audio sharing by browser is as follows:

   
   |Operating system |Browser |Share entire screen |Share tab |Share application window |
   |---|---|---|---|---|
   |Windows |Chrome |✅ |✅ |❌ |
   ||Edge |✅ |✅ |❌ |
   ||360 Extreme Browser |✅ |❌ |❌ |
   |macOS |Chrome |❌ |✅ |❌ |
   ||Edge |❌ |✅ |❌ |
   ||360 Extreme Browser |❌ |✅ |❌ |
   

* The types of content that can be shared in different browsers are as follows:

   
   |Browser |Share entire screen |Share tab |Share application window |
   |---|---|---|---|
   |Chrome |✅ |✅ |✅ |
   |Edge |✅ |✅ |✅ |
   |Firefox |✅ |❌ |✅ |
   |Safari |✅ |❌ |❌ |
   |360 Extreme Browser |✅ |✅ |❌ |
   

* Firefox does not support setting the content type of the screen\-captured video in the setScreenEncoderConfig method, specifically the ScreenEncoderConfig.contentHint parameter. For more details, please refer to contentHint browser compatibility.


<span id="发布-simulcast-流"></span>
### Publishing Simulcast streams

The publisher\-side Simulcast feature is supported on the following browser versions:


* Chrome 74 or later

* Safari 14.1 or later

* Chrome 128 or later on Android

* iOS 15 or later


<span id="获取设备列表"></span>
### Obtaining the device list


* To protect user privacy, Chrome 81+, Safari, Huawei browser, and Firefox require media device permissions before device IDs can be obtained. This limitation affects [enumerateDevices](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104478#enumeratedevices), [enumerateAudioCaptureDevices](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104478#enumerateaudiocapturedevices), and [enumerateVideoCaptureDevices](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104478#enumeratevideocapturedevices).

* We recommend first requesting device permissions from the user by calling enableDevices, and then obtaining the device list.


<span id="获取和设置扬声器设备"></span>
### Obtaining and setting speaker devices

Only Chrome supports enumerateAudioCaptureDevices and setAudioPlaybackDevice, and calling these methods in other browsers will return an empty list.

<span id="收发-sei-消息"></span>
### Sending and receiving SEI messages

Compatibility notes for SEI message send/receive interfaces such as [sendSEIMessage](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104478#sendseimessage):


* SEI messages are only supported in browsers using H.264 encoding and with a Chromium 86+, Firefox 117+, or Safari 15.4+ engine.

* Android devices cannot automatically generate a black frame video stream to send SEI data in voice call scenarios.


<span id="插件功能"></span>
### Plugin features


* The Beauty Effects Extension and Virtual Background Extension are not recommended for use on mobile devices. It is not supported on Safari 15.4 and below, as the known Webkit Bug 181663 can cause a black screen problem.

* The AI Noise\-Canceling Extension is only supported on Windows and macOS with the following browsers and versions:

   * Chrome 94+

   * Edge 94+

   * Firefox 80+

   * Safari 14.1+


<span id="发布和订阅-h-265-视频"></span>
### Publishing and Subscribing to H.265 Video


* H.265 video format is supported only in the following browser versions:

   * Chrome 136+

   * Safari 18+

> To prevent runtime failures due to an unsupported environment, call [getSupportedCodecs](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104478#byteplusrtc-getsupportedcodecs) to verify H.265 codec compatibility before use.


* Resolutions lower than 146x146 may lead to encoding/decoding failures or visual artifacts due to hardware chipset limitations. Therefore, a resolution higher than 146x146 is recommended when using H.265.
