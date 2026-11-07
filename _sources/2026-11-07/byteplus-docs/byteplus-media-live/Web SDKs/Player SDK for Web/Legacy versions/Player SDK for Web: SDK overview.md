---
title: "Player SDK for Web: SDK overview"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction-to-the-player-sdk-for-web"
---

The BytePlus MediaLive Player SDK for Web (also known as VePlayer), together with [BytePlus MediaLive's streaming service](https://www.byteplus.com/en/product/medialive), offers smooth, stable, and high\-quality playback solutions for live content. The SDK is compatible with multiple operating systems. You can easily integrate it into your existing web applications.

<span id="fe6b462a"></span>
## SDK demo

To try the SDK demo, visit [VePlayer](https://demo.byteplus.com/common/veplayer/basic/example) and switch between tabs to explore different features. Sample code is available to help you learn how to implement the features, and you can tweak the code to see how the player's behavior changes.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e7e7ac0d5984d6a88e824809da38da1~tplv-goo7wpa0wc-image.image) </span>

<span id="6e1358a3"></span>
## Protocol support

The following table lists the streaming protocols the Player SDK supports:


|**Protocol** |**Pros and Cons** |**H.264** ||**H.265** ||
|---|---|---|---|---|---|
|||**PC** |**Mobile** |**PC** |**Mobile** |
|HLS |* Broad compatibility<br><br>* High latency |Supported |Supported |Supported |Partially supported |
|FLV |* Low latency<br><br>* Poor H5 support |Supported |Partially supported |Supported |Partially supported |
|RTM |* Low latency<br><br>* Resilient in poor network connections |Supported |Partially supported |Not supported |Not supported |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When using the RTM protocol for playback, the browser must support <a href="https://caniuse.com/?search=WebRTC%20Peer-to-peer%20connections">WebRTC</a>.</div>


* <div data-tips="true" data-tips-type="tip">On Android devices, some browsers may hijack the player, disabling some of its features.</div>


* <div data-tips="true" data-tips-type="tip">If you want to play live streams encoded in H.265 format and streamed in HLS or FLV protocols, you must first confirm whether the browser supports H.265 software or hardware decoding.</div>



<span id="8af48d51"></span>
## Features

The Player SDK is compatible with mainstream browsers. It automatically selects the optimal playback solution based on the operating system.


|**Feature** |**PC** |**Mobile** |
|---|---|---|
|Custom player size |Supported |Supported |
|Custom cover image |Supported |Supported |
|Autoplay |Supported |Supported |
|Multiple players on a same page |Supported |Supported |
|Resolution switching |Supported |Supported |
|Full screen |Supported |Supported |
|Video rotation |Supported |Supported |
|Volume control |Supported |Supported |
|Picture\-in\-Picture (PiP) |Supported |Partially supported |
|H.264 |Supported |Supported |
|H.265 |Partially supported |Partially supported |
|Custom error messages |Supported |Supported |
|Bullet comments |Supported |Supported |
|Dynamic downgrading to backup streams |Supported |Supported |
|Dynamic downgrading to lower resolutions |Supported |Supported |
|Live information panel |Supported |Supported |
|Log upload |Supported |Supported |
|Playing time\-shifted live content |Supported |Supported |
|Pulling RTM streams |Partially supported |Partially supported |
|Listening for SEI messages |Supported |Supported |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The Player SDK for Web has autoplay enabled by default. However, some browser policies can affect autoplay behavior. For example, <a href="https://developer.chrome.com/blog/autoplay/">Autoplay policy in Chrome</a>.</div>


* <div data-tips="true" data-tips-type="tip"><a href="https://caniuse.com/?search=HEVC">Browsers supporting H.265 hardware decoding</a> can directly play H.265 encoded video, while other browsers can enable software decoding by setting <code>useSoftDecoding</code> to <code>true</code> to play H.265 encoded video.</div>
