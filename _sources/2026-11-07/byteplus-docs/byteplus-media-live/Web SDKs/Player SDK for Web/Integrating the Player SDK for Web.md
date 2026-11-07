---
title: "Integrating the Player SDK for Web"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1"
---

To embed a video player into your web page, you can integrate the Player SDK for Web (also known as VePlayer) into your web application. This topic describes how to integrate the Player SDK for Web.

<span id="e625f8f3"></span>
## Prerequisites


* Do the following based on the SDK version.

   * For version 2.11.0 and later (recommended): Create an SDK application, and get the license file, license URL, and app ID. For more information, see [Getting your SDK license](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management).

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Since version 2.11.0, you must use licenses to manage the usage rights and duration of the Player SDK and its value\-added services. The premium license includes more features, such as <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-adaptive-bitrate-streaming-abr">Adaptive bitrate streaming</a>, <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/adaptive-buffer-strategy">Adaptive buffer strategy</a>, <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/achieving_2-3s_live_stream_latency_with_low-latency_FLV_web">Low\-latency FLV stream pulling</a>, and <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/RTM-Streaming-Integration">Playing RTM streams</a>, but additional charges apply. For more information about different license types and billing information, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-licenses#0c916d6b">Player SDK for Web</a>.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">A trial license is for project testing only and cannot be renewed. An expired trial license will cause authentication to fail, which will interrupt the service. Upgrade to an official license before your project goes live. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#777c7de7">Upgrading a trial license to a basic or premium license</a>.      </div>
      

   * For versions earlier than 2.11.0: You only need to create an SDK application and get the App ID. A license is not required. For more information, see [Getting your SDK license](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management). We recommend that you upgrade to the latest version for better features and services.

* To use the BytePlus MediaLive service to pull streams, complete the following prerequisites:

   * Add domain names and CNAME records. For more information, see [Adding a domain name](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain) and [Adding a CNAME record](https://docs.byteplus.com/docs/byteplus-media-live/docs-adding-a-cname-record).

   * [Generate a pull stream address](https://docs.byteplus.com/byteplus-media-live/docs/address-generator). If you need to use an HTTPS pull stream address, you must first add an SSL certificate and complete the HTTPS configuration. For more information, see [Managing SSL certificates](https://docs.byteplus.com/docs/byteplus-media-live/docs-managing-certificates) and [HTTPS configuration](https://docs.byteplus.com/docs/byteplus-media-live/docs-https).


<span id="ceef554f"></span>
## Step 1: Import dependencies

Choose either of the following ways to import the SDK:


<Tabs>
<Tab zoneid="mvgfw2Ha5f" title="CDN">
<TabTitle>CDN</TabTitle>

To import the CSS and JS files for the Player SDK using CDN, add the following code to your local project's `index.html` file:

```HTML
<link rel="stylesheet" href="https://sf-unpkg.bytepluscdn.com/obj/byteplusfe-sg/sdk/@byteplus/veplayer/2.12.1/umd/veplayer.production.css">

<script src="https://sf-unpkg.bytepluscdn.com/obj/byteplusfe-sg/sdk/@byteplus/veplayer/2.12.1/umd/veplayer.production.js"></script>
```



</Tab>
<Tab zoneid="wH2FT8Xclx" title="NPM">
<TabTitle>NPM</TabTitle>

1. Run the following commands to install the Player SDK.

   ```Plain
   npm install @byteplus/veplayer@next
   npm install @byteplus/veplayer-plugin@next
   ```
   

2. Add the following code to your local project's `index.html` file.

   ```Plain
   import { createLivePlayer, register } from '@byteplus/veplayer';
   import '@byteplus/veplayer/style';
   ```
   

3. Import and register plugins when necessary. The sample code is as follows.

   ```JavaScript
   // To play HLS streams
   import { hlsjs } from '@byteplus/veplayer-plugin';
   register([hlsjs]);
   
   // To play FLV streams
   import { flv } from '@byteplus/veplayer-plugin';
   register([flv]);
   
   // To play RTM streams
   import { rtm } from '@byteplus/veplayer-plugin';
   register([rtm]);
   
   // To play multiple streams in different protocols
   import { flv, hlsjs, rtm } from '@byteplus/veplayer-plugin';
   register([rtm, flv, hlsjs]);
   ```
   

   To reduce the package size, you can import a single plugin by its path. For example, replace `import { hlsjs } from '@byteplus/veplayer-plugin';` with `import * as hlsjs from '@byteplus/veplayer-plugin/hlsjs';` to import the hlsjs plugin. Similarly, you can import the following plugins on demand: `flv`, `rtm`, `abr`, `drm`, `timeshift`, and `ad`.


</Tab>
</Tabs>


<span id="7d0334fc"></span>
## Step 2: Add a player container

Add a player container to the page where you want to display the player. For example, add the following code to `index.html`:

```html
<div id="veplayer"></div>
```


<span id="f1396aa0"></span>
## Step 3: Configure the license

Starting from version 2.11.0, you must configure a license to use the Player SDK. Follow the steps to complete the configuration.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">A license is not required for versions earlier than 2.11.0, but we recommend that you upgrade to the latest version for better features and services.</div>


* <div data-tips="true" data-tips-type="warning">License verification will fail in the following cases:</div>


   * <div data-tips="true" data-tips-type="warning"><strong>Web</strong> (for browser pages): Make sure the domain of the page where you plan to embed the player matches the wildcard domain configured for your SDK application. For example, if you configured <code>*.example.com</code> as the wildcard domain, the domain of your page must be a first\-level subdomain, such as <code>a.example.com</code>.</div>


   * <div data-tips="true" data-tips-type="warning"><strong>WebOTT</strong> (Web Over\-The\-Top, for web apps running on Tizen and webOS smart TV systems): Make sure the current Tizen or webOS application identifier matches the application identifier configured for your SDK application. WebOTT is supported only by Player SDK for Web 2.12.0 and later.</div>



For browser pages, license verification is performed at the page level, so you only need to set it once, even in a single\-page, multi\-instance scenario. To optimize the playback experience and improve the first\-frame loading speed, it is recommended to configure the license before initializing the player.

You can configure the license in any of the following ways.


<Tabs>
<Tab zoneid="EMNucus5Wp" title="Set license file content">
<TabTitle>Set license file content</TabTitle>

Call [setLicenseConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1156178#setlicenseconfig) and provide the license file content.


* `sign`: The `Signature` from the license file, used for authentication.

* `content`: The `Content` from the license file, which includes permission levels and version information.

* `mainUrl` (Optional but recommended): The `MainURL` from the license file, which is the license URL. If set, the SDK automatically updates to the latest license version after the license is upgraded or renewed, without requiring manual updates. For more information on how to get the license URL, see [Step 2: Get the license file](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management#8a4f3efc).


The sample code is as follows.


* CDN

   ```JavaScript
   VePlayer.live.setLicenseConfig({
     license: {
        sign: "xxx",
        content: "xxx",
        mainUrl: "https://example.com/obj/license-byteplus/license.lic", 
    }
   })
   ```
   

* NPM

   ```JavaScript
   import { live } from '@byteplus/veplayer';
   live.setLicenseConfig({
     license: {
        sign: "xxx",
        content: "xxx",
        mainUrl: "https://example.com/obj/license-byteplus/license.lic", 
    }
   })
   ```
   


</Tab>
<Tab zoneid="GfDIHOYpf5" title="Set license URL">
<TabTitle>Set license URL</TabTitle>

Call [setLicenseConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1156178#setlicenseconfig) and provide the license URL. For more information on how to get the license URL, see [Step 2: Get the license file](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management#8a4f3efc).

The SDK will automatically handle the authentication logic and enable automatic license updates. The sample code is as follows.


* CDN

   ```JavaScript
   VePlayer.setLicenseConfig({
       // The license URL. The SDK automatically updates to the latest license version after the license is upgraded or renewed, without requiring manual updates.
       license: "https://example.com/obj/license-byteplus/license.lic"
   }) 
   ```
   

* NPM

   ```JavaScript
   import { live } from '@byteplus/veplayer';
   live.setLicenseConfig({
       // The license URL. The SDK automatically updates to the latest license version after the license is upgraded or renewed, without requiring manual updates.
       license: "https://example.com/obj/license-byteplus/license.lic"
   }) 
   ```
   


</Tab>
</Tabs>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the player initializes and plays video without any license\-related errors, the verification is successful.</div>


<span id="f816d63b"></span>
## Step 4: Create a VePlayer instance and enable log reporting

Create a VePlayer instance and enable log reporting by using the following code. The player starts playing once the page loads. If you want to play a live stream, set `url` to a pull stream address.


<Tabs>
<Tab zoneid="rD3hRXmqnm" title="CDN">
<TabTitle>CDN</TabTitle>

```javascript
VePlayer.createLivePlayer({
  width: 640,
  height: 360,
  url: 'https://livepull.example.com/appname/streamname.flv',
  logger:{
    // Enable log reporting. Once enabled, the SDK sends playback-related information to BytePlus MediaLive servers for troubleshooting and analysis, helping improve the stability and user experience of your application.
    appId: 'APP_ID', // Required. Replace APP_ID with the app ID from your created SDK application. 
    userId: 'USER_ID', // Optional. Replace USER_ID with the application user ID.
    deviceId: 'DEVICE_ID', // Optional. Replace DEVICE_ID with the user's device ID.
  }
}).then(function(veplayer){
  console.log('VePlayer is successfully created. The VePlayer instance is:', veplayer)
}).catch(function(err){
  console.log('Creating VePlayer failed due to:', err)
});
```



</Tab>
<Tab zoneid="QFhwpyvQAc" title="NPM">
<TabTitle>NPM</TabTitle>

```javascript
createLivePlayer({
  width: 640,
  height: 360,
  url: 'https://livepull.example.com/appname/streamname.flv',
  logger:{
    // Enable log reporting. Once enabled, the SDK sends playback-related information to BytePlus MediaLive servers for troubleshooting and analysis, helping improve the stability and user experience of your application.
    appId: 'APP_ID', // Required. Replace APP_ID with the app ID from your created SDK application. 
    userId: 'USER_ID', // Optional. Replace USER_ID with the application user ID.
    deviceId: 'DEVICE_ID', // Optional. Replace DEVICE_ID with the user's device ID.
  }
}).then(function(veplayer){
  console.log('VePlayer is successfully created. The VePlayer instance is:', veplayer)
}).catch(function(err){
  console.log('Creating VePlayer failed due to:', err)
});
```



</Tab>
</Tabs>


If playback issues occur during a live stream, collect relevant information, such as the time when the issue occurred and the user ID, and [contact technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) for troubleshooting.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Starting from version 2.12.0, failure to configure <code>appId</code> will trigger a console error.</div>


* <div data-tips="true" data-tips-type="tip">It is strongly recommended to pass both <code>userId</code> and <code>deviceId</code>. This helps to quickly locate and troubleshoot playback issues. If <code>userId</code> and <code>deviceId</code> are not provided, the SDK will generate random values based on the user's browser and store them locally.</div>



<span id="fa2afbea"></span>
## Next steps

The Player SDK provides a variety of features covering multiple playback scenarios, including custom cover images, picture\-in\-picture, progress bar thumbnail previews, and advanced features such as automatic video resolution degradation and playing RTM streams. For more information, see [Feature Integration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-web-feature-integration).

VePlayer also offers a wide range of features tailored to various playback scenarios. Try the [Web player demo](https://demo.byteplus.com/common/veplayer/basic/example?tab=function-display) to explore its features, effects, and integration methods.
