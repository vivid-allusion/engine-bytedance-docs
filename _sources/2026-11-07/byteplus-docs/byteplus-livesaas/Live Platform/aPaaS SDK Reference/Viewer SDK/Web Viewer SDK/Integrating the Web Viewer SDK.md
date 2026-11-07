---
title: "Integrating the Web Viewer SDK"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-integrating-the-web-viewer-sdk"
---

The Web Viewer SDK enables your Web app on PC or mobile platforms to include features such as watching a live stream, sending comments, and participating in lucky draws. This topic describes how to integrate the Web Viewer SDK into your Web app, and the corresponding parameters, events, and APIs.

<span id="Prerequisite"></span>
## Prerequisite

Because the APIs of the Web Viewer SDK cannot be called across domains, contact BytePlus Live technical support to add your domain name to the allowlist of BytePlus Live.

<span id="Demo"></span>
## Demo

BytePlus Live provides demo playgrounds for both PC and mobile platforms. You can review the effects below, and visit [BytePlus Live aPaaS Solution Web SDK Demo](https://live.byteplus.com/demo/sdk/index.html) to perform online debugging and obtain a real\-time preview.


<Tabs>
<Tab zoneid="HN4l1czWSJ" title="Effeccts on PC">
<TabTitle>Effeccts on PC</TabTitle>

On the demo playground for PC, click **View Code** to edit the code and preview the effect.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d6e24c8579c455c9d15cdd99e5a2b63~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="NoZZ7YL4lq" title="Effects on mobile">
<TabTitle>Effects on mobile</TabTitle>

On the demo playground for mobile, you can directly edit the code on the right side to see the effect.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94c477739a434b97aa40f44ffa4da243~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


<span id="Features"></span>
## Features

For the list of Web SDK features, see the *Web Viewer SDK* column in the table in the [Feature comparison between SaaS and aPaaS](https://docs.byteplus.com/docs/byteplus-livesaas/docs-feature-comparison-between-saas-and-apaas) document.

<span id="855885cc"></span>
## Integration method

Complete the following steps to integrate the Web Viewer SDK into your Web app.

<span id="7f20b494"></span>
### Step 1: Import CSS and JS resources

Select the appropriate integration method based on your platform and feature requirements and use `link` and `script` tags to import CSS and JS resources.

<span id="80ac0262"></span>
#### **PC integration resources**

To integrate the SDK into your PC\-based web application, select one of the resources described below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For tablets, it is recommended to integrate the PC Web SDK for a better visual experience.</div>


* <div data-tips="true" data-tips-type="tip">Modify the version number in the URL directly to update the version. Make sure a platform has the same CSS version and JS version.</div>




<Tabs>
<Tab zoneid="kXHPWBREJx" title="Modular integration">
<TabTitle>Modular integration</TabTitle>

Use when full live room features are required, such as chat, product cards, and check\-in.

```HTML
// Modular integration on PC
<link rel="stylesheet" href="https://res.gcloudcache.com/bp-fe/livesaas-client/pc/css/index.2.0.31.css">
<script src="https://res.gcloudcache.com/bp-fe/livesaas-client/pc/js/index.2.0.31.js"></script>
```



</Tab>
<Tab zoneid="AEATZlAgHV" title="Player-only integration">
<TabTitle>Player-only integration</TabTitle>

Use when only playback features are needed, including VOD, live streaming, quality switching, playback speed, and multi\-line options.

This method's performance is higher than modular integration.

```HTML
// Player-only integration on PC
<link rel="stylesheet" href="https://res.gcloudcache.com/bp-fe/livesaas-client/player-pc/css/index.2.0.31.css">
<script src="https://res.gcloudcache.com/bp-fe/livesaas-client/player-pc/js/index.2.0.31.js"></script>
```



</Tab>
</Tabs>


<span id="a7cb4e3d"></span>
#### Mobile **integration resources**

To integrate the SDK into your mobile web application, select one of the resources described below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Modify the version number in the URL directly to update the version. Make sure a platform has the same CSS version and JS version.</div>



<Tabs>
<Tab zoneid="KXqzyRM5dJ" title="Modular-and-full-page integration">
<TabTitle>Modular-and-full-page integration</TabTitle>

Use when full live room features are required, such as chat, product cards, and check\-in.

```HTML
// Modular or full-page integration on Mobile
<link rel="stylesheet" href="https://res.gcloudcache.com/bp-fe/livesaas-client/mobile/css/index.2.0.31.css">
<script src="https://res.gcloudcache.com/bp-fe/livesaas-client/mobile/js/index.2.0.31.js"></script>
```



</Tab>
<Tab zoneid="acWCI1VMN5" title="Full-page-only integration">
<TabTitle>Full-page-only integration</TabTitle>

Use when you need to integrate features such as live event reservation, host accounts, or header images that do not belong to a specific module.

This method's performance is higher than modular\-and\-full\-page integration.

```HTML
// Full-page integration on Mobile
<link rel="stylesheet" href="https://res.gcloudcache.com/bp-fe/livesaas-client/mobile-all/css/index.2.0.31.css">
<script src="https://res.gcloudcache.com/bp-fe/livesaas-client/mobile-all/js/index.2.0.31.js"></script>
```



</Tab>
<Tab zoneid="aIGbnU018C" title="Player-only integration">
<TabTitle>Player-only integration</TabTitle>

You must use this integration method when:


* You need to display an on\-demand player on the viewing page.

* You need to display multiple live or on\-demand players on the same page.


This method's performance is higher than modular\-and\-full\-page integration.

```HTML
// Player-only integration on Mobile
<link rel="stylesheet" href="https://res.gcloudcache.com/bp-fe/livesaas-client/player-mobile/css/index.2.0.31.css">
<script src="https://res.gcloudcache.com/bp-fe/livesaas-client/player-mobile/js/index.2.0.31.js"></script>
```



</Tab>
</Tabs>


Domain name: `https://res.gcloudcache.com/bp-fe`

Latest version: 2.0.31

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Starting from version <strong>2.0.30</strong>, the domain has been changed from <code>https://res.bytepluscdn.com/obj/bp-console-fe-sg</code> to <code>https://res.gcloudcache.com/bp-fe</code>. When integrating SDK version <strong>2.0.30</strong> or above, please make sure to use the new domain <code>https://res.gcloudcache.com/bp-fe</code>.</div>


* <div data-tips="true" data-tips-type="warning">Starting from version 1.3.8, <code>byteplus</code> following <code>mobile/</code> or <code>pc/</code> in the URL has been removed. For example, <code><link rel="stylesheet" href="https://mediaservice-fe.bytepluscdn.com/obj/vcloud-fe-sgcomm/livesaas-client/pc/byteplus/css/index.VERSIONNUMBER.css"></code> is changed to <code><link rel="stylesheet" href="https://mediaservice-fe.bytepluscdn.com/obj/vcloud-fe-sgcomm/livesaas-client/pc/css/index.VERSIONNUMBER.css"></code>.</div>



<span id="829352b2"></span>
### Step 2: Integrate the Web Viewer SDK


1. After resources are imported, ByteLiveWebSDK is mounted under `window`. Use the following method to integrate the Web Viewer SDK into your Web app.

   ```JavaScript
   var webSDK = new window.ByteLiveWebSDK({
     activityId: 173312069231****,
     token: 'ZQ****',
     service: '',
     mode: 1,
     modules: [
       {
         id: "player",
         mode: "player", 
       }, 
       {
         id: "menu", 
         mode: "menu",
         menu: ["comment"],
       }
     ],
     options: {}
   })
   
   webSDK.emit('player.pause'); // Trigger events
   webSDK.on('player.pause', () => {}); // Listen for events
   ```
   

   For more information about the parameter configuration in the code, see [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters). For more information about listening for and triggering events, see [Web Viewer SDK: Events](https://docs.byteplus.com/docs/byteplus-livesaas/events). For more information about calling APIs, see [API](https://docs.byteplus.com/docs/byteplus-livesaas/api).

2. (Optional) Override the style. The `class` attribute values of SDK elements cannot be changed. You can change the style attributes and the corresponding values of a `class` attribute to override the style of the corresponding element.


<span id="dc1eff46"></span>
### Step 3: Debug

Use one of the following methods to debug.


* Online debugging: We recommend that you use the SDK demo playground for online debugging on your PC. By using said playground, you can configure various live rooms and SDKs of different versions, modify the code in the template, and then preview the effect in real time. For more information, see [Web Viewer SDK demo playground](https://live.byteplus.com/demo/sdk/index.playground.html?mode=pc).

* Local debugging: Debug on your local port, `localhost:8080`. You cannot play previews or playbacks with this method.

   1. Download and unzip the package [byte-live-sdk-demo-master-plus.zip](https://lf6-cdn-tos.douyinstatic.com/obj/livesaas/byte-live-sdk-demo-master-plus.zip).

   2. Open the terminal and run the `cd` command to go to the directory of the unzipped folder. For example, `cd C:\Users\Admin\Downloads\byte-live-sdk-demo-master-plus`.

   3. Run the `yarn` command to install dependencies.

   4. To start the service, run the `yarn start` command for Mac and the `yarn start-win` command for Windows.

   5. Open [http://localhost:8080/demo/sdk/index.html](http://localhost:8080/demo/sdk/index.html) to debug.


<span id="1164a8f8"></span>
## FAQs

[Web Viewer SDK FAQs](https://docs.byteplus.com/docs/byteplus-livesaas/docs-faqs-about-web-viewer-sdk)
