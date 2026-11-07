---
title: "Running the RTM demo for web"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-running-the-rtm-demo-for-web"
---

To test Real\-Time Media (RTM) streaming on the web, you can use the demo provided by BytePlus MediaLive. This topic walks you through the entire process, from generating push and pull stream addresses to pushing a stream and playing the stream on the web.

<span id="0439107b"></span>
## Prerequisite

You have activated BytePlus MediaLive.


* If you do not have push and pull stream domain names, you can use the test push and pull stream domain names provided by MediaLive.

* If you want to use your own domain names for testing, you need to add at least two domain names, one for stream pushing, and the other for stream pulling. The push and pull stream domain names must be configured under the same domain namespace.


<span id="a0cf172d"></span>
## Procedure

<span id="b5ad8b31"></span>
### Generating push/pull stream addresses


1. In the left\-side navigation pane, select **Toolkits** \> [Address Generator](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator).

2. Complete the configuration. Make sure the `AppName` and `StreamName` for generating the push and pull stream addresses are the same. For more information, see [Generating stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-address-generator).

3. Click **Generates Push stream address** to get an RTM push stream address in the **Result** section.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b1cdda2de8c41df99239d8d976cefb2~tplv-goo7wpa0wc-image.image" width="812px" />   </div>
   

4. Click **Generates Pull stream address**, and then you can get the **RTM Web SDK playback address** for the source stream on the **Pull Stream URL** tab or select a transcoding suffix on the **Transcoding stream** tab to get the **RTM Web SDK playback address** for the transcoded stream.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you cannot get the <strong>RTM Web SDK playback address</strong>, contact <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980">technical support</a>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The <strong>RTM Web SDK playback address</strong> supports automatic transcoding, including B\-frame removal and AAC\-to\-Opus audio conversion. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-generating-live-stream-addresses">Generating live\-stream addresses</a>.   </div>
   


<span id="ec1aebfd"></span>
### Pushing an RTM stream

You can push an RTM stream [through the BytePlus MediaLive console](https://docs.byteplus.com/en/byteplus-media-live/docs/web-push?version=v1.0) or use stream\-pushing tools such as Open Broadcaster Software (OBS). Use the address you get from the previous step as the push stream address.

<span id="d1b7ef3b"></span>
### Pulling an RTM stream


1. Go to [VePlayer](https://demo.byteplus.com/common/veplayer/basic/example), which is the demo of the BytePlus MediaLive Player SDK for Web.

2. Click **RTM Pull Stream** in the **Function configuration** tab.

3. In the **Code example** window, set the `url` field to the **RTM Web SDK playback address** you get from the previous step.

4. Click **Run** to play the live stream.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If your domain name does not have an SSL certificate enabled, please access the <a href="http://demo.byteplus.com/common/veplayer/basic/example?tab=function-display">unencrypted version</a> of the VePlayer demo by using an HTTP address instead. Please note that when using the demo, you should not pass any sensitive information.</div>
