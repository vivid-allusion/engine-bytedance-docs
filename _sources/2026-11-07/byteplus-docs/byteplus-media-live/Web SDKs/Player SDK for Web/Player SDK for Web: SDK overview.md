---
title: "Player SDK for Web: SDK overview"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-web-sdk-overview"
---

The BytePlus MediaLive Player SDK for Web (also known as VePlayer), together with [BytePlus MediaLive's streaming service](https://www.byteplus.com/en/product/medialive), offers smooth, stable, and high\-quality playback solutions for live content. The SDK is compatible with multiple operating systems. You can easily integrate it into your existing web applications.

Player SDK for Web provides three types of licenses: basic, premium, and trial.


* **Basic license**: Suitable for live streaming scenarios that require only basic stream pulling features, such as sports events, entertainment, e\-commerce, and education.

* **Premium license**: Suitable for live streaming scenarios that require both basic stream pulling features and advanced features such as Adaptive Bitrate (ABR) streaming, adaptive buffer strategy, and [Real Time Media (RTM)](https://docs.byteplus.com/en/byteplus-media-live/docs/introduction-to-real-time-media). For more information, see [Features](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-sdk-overview#ba9be9fe).

* **Trial license**: Suitable for trial scenarios such as testing. It includes all features of the Player SDK for Web.


<span id="b49f0040"></span>
## Versions

The Player SDK for Web 2.x features the following optimizations compared to version 1.x:


* improved integration processes and reduced package size;

* enhanced player creation processes;

* optimized player configurations, methods, properties, and event formats.


These optimizations significantly enhance player performance and user experience, while also facilitating integration and usage. We recommend upgrading to version 2.x for better player performance and experience.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Version 2.x introduces breaking changes and does not support the video\-on\-demand (VOD) feature. If you want to play both live streams and VOD, use previous versions of the SDK instead. Refer to <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions">Player SDK for Web: 1.x versions</a> for more information.</div>


<span id="356d2ba0"></span>
## SDK demo

To try the SDK demo, visit [VePlayer](https://demo.byteplus.com/common/veplayer/v2/basic/example?tab=function-display) and switch between tabs to explore different features. Sample code is available to help you learn how to implement the features, and you can tweak the code to see how the player's behavior changes.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee01088a972943a385f4f2ba99ab856b~tplv-goo7wpa0wc-image.image) </span>

<span id="600333d3"></span>
## Protocol support

The following table lists the streaming protocols the Player SDK supports:


|**Protocol** |**Characteristics** |**H.264** ||**H.265** ||
|---|---|---|---|---|---|
|||**PC** |**Mobile** |**PC** |**Mobile** |
|HLS |* Broad compatibility<br><br>* High latency |Supported |Supported |Supported |Partially supported |
|FLV |* Low latency<br><br>* Poor H5 support |Supported |Partially supported |Supported |Partially supported |
|RTM |* Low latency<br><br>* Resilient in poor network connections |Supported |Partially supported |Not supported |Not supported |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When using the RTM protocol for playback, the browser must support <a href="https://caniuse.com/?search=WebRTC%20Peer-to-peer%20connections">WebRTC</a>.</div>


* <div data-tips="true" data-tips-type="tip">On Android devices, some browsers may hijack the player, disabling some of its features.</div>


* <div data-tips="true" data-tips-type="tip">If you want to play live streams encoded in H.265 format and streamed in HLS or FLV protocols, you must first confirm whether the browser supports H.265 software or hardware decoding.</div>



<span id="ba9be9fe"></span>
## Features

The Player SDK is compatible with mainstream browsers. It automatically selects the optimal playback solution based on the operating system.


|**Feature** |**PC** |**Mobile** |
|---|---|---|
|Custom player size |Supported |Supported |
|Custom cover image |Supported |Supported |
|Autoplay |Supported |Supported |
|Multiple players on a same page |Supported |Supported |
|Resolution switching |Supported |Supported |
|Screenshot capturing |Supported |Supported |
|Full screen |Supported |Supported |
|Video rotation |Supported |Supported |
|Volume control |Supported |Supported |
|Picture\-in\-Picture (PiP) |Supported |Not supported |
|H.264 |Supported |Supported |
|H.265 |Partially supported |Partially supported |
|URL authentication |Supported |Supported |
|Referer allowlist and blocklist |Supported |Supported |
|IP allowlist and blocklist |Supported |Supported |
|Custom error messages |Supported |Supported |
|Bullet comments |Supported |Supported |
|Dynamic downgrading to backup streams |Supported |Supported |
|Dynamic downgrading to lower resolutions |Supported |Supported |
|Live information panel |Supported |Supported |
|Log upload |Supported |Supported |
|Playing time\-shifted live content |Supported |Supported |
|Playing RTM streams |Partially supported only by the premium or trial license |Partially supported only by the premium or trial license |
|Listening for SEI messages |Supported |Supported |
|ABR streaming |Supported only by the premium or trial license |Partially supported only by the premium or trial license |
|Adaptive buffer strategy |Partially supported only by the premium or trial license |Partially supported only by the premium or trial license |
|Low\-latency FLV stream pulling |Supported only by the premium or trial license |Partially supported only by the premium or trial license |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The Player SDK for Web has autoplay enabled by default. However, some browser policies can affect autoplay behavior. For example, <a href="https://developer.chrome.com/blog/autoplay/">Autoplay policy in Chrome</a>.</div>


* <div data-tips="true" data-tips-type="tip">The implementation of Picture\-in\-Picture (PiP) is based on the <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-sdk-overview">picture\-in\-picture</a> support provided by the PC version of the Chrome browser.</div>


* <div data-tips="true" data-tips-type="tip"><a href="https://caniuse.com/?search=HEVC">Browsers supporting H.265 hardware decoding</a> can directly play H.265 encoded video, while other browsers can enable software decoding by setting the <code>degradation</code> parameter to play H.265 encoded video.</div>
