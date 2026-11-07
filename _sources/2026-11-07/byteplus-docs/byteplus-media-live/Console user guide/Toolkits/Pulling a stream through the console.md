---
title: "Pulling a stream through the console"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-web-pull"
---

This topic describes how to pull streams through the BytePlus MediaLive console by using the **Web pull** tool.

Web Pull integrates the BytePlus MediaLive Player SDK for Web. To integrate the SDK into your own application, refer to [Player SDK for Web: SDK overview](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction-to-the-player-sdk-for-web).

<span id="Prerequisites"></span>
## Prerequisites

Web Pull provides a default pull stream address. Use the address if you just want to experience the many features of BytePlus MediaLive, such as playing, muting, bullet comments, and picture\-in\-picture (PiP). If you want to use your own pull stream address, do the following before you start Web Pull:


* A domain name for stream pulling, with an SSL certificate configured. Refer to [Adding a domain name](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain) and [Adding an SSL certificate ](https://docs.byteplus.com/docs/byteplus-media-live/docs-https)for more information.

* Associate the domain name for streaming pulling with a domain name for stream pushing. Refer to [Domain](https://docs.byteplus.com/byteplus-media-live/docs/domain) for details.

* Start streaming by using the associated domain name of stream pushing. You can stream by using [web push](https://docs.byteplus.com/byteplus-media-live/docs/web-push), OBS, and other methods.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Web Pull supports HTTPS addresses only. To play HTTP addresses, go to <a href="https://demo.byteplus.com/common/veplayer/basic/example">VePlayer</a>, which demonstrates a wider range of features provided by BytePlus MediaLive Player SDK for Web.</div>


<span id="Procedure"></span>
## Procedure


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, go to **Toolkits** \> **Web pull**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae4bc1d7f0274bf1a316926cbee6ace7~tplv-goo7wpa0wc-image.image) </span>

3. If you want to use your own pull stream address, enter it in the input box next to the **Click to play** button. If you do not have the address already, click **Generate addresses** and complete the form to generate one in M3U8 format, or use the [Address generator](https://docs.byteplus.com/byteplus-media-live/docs/address-generator) to generate one in the format of your choice.

4. Click **Click to play** to start pulling the stream. During the playback, you can pause, turn on bullet comments, and switch to full\-screen mode or PiP mode.
