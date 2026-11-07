---
title: "Integrating the Player SDK for Web"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web"
---

This article explains how to add BytePlus MediaLive Player SDK for Web (also known as VePlayer) to your web application. The integration process involves the following steps:


1. Importing dependencies

2. Adding a container for the player

3. Creating a VePlayer instance

4. Implementing more features


<span id="Prerequisites"></span>
## Prerequisites

If you want the Player SDK to pull streams distributed through BytePlus MediaLive, do the following before you begin:


* Add domain names and CNAME records. See [Adding domain names](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain#bb9e1337) and [Adding a CNAME record](https://docs.byteplus.com/docs/byteplus-media-live/docs-adding-a-cname-record) for more information.

* [Generate a pull stream address](https://docs.byteplus.com/byteplus-media-live/docs/address-generator). If you need to use an HTTPS pull stream address, you should first add a certificate and complete the HTTPS configuration. Refer to [Managing SSL certificates](https://docs.byteplus.com/docs/byteplus-media-live/docs-managing-certificates) and [Adding an SSL certificate ](https://docs.byteplus.com/docs/byteplus-media-live/docs-https)for more information.


<span id="Importing dependencies"></span>
## Importing dependencies

<span id="6298ac53"></span>
### Importing with CDN

To import the CSS and JS files for the Player SDK using CDN, add the following code to your local project's `index.html` file:

```HTML
<link rel="stylesheet" href="//sf-unpkg.bytepluscdn.com/obj/byteplusfe-sg/sdk/@byteplus/veplayer/1.6.3/index.min.css">
<script src="//sf-unpkg.bytepluscdn.com/obj/byteplusfe-sg/sdk/@byteplus/veplayer/1.6.3/index.min.js"></script>
```


<span id="6b8a8eb3"></span>
### Importing with NPM


1. To install the SDK dependency using NPM, run the following command:


```Bash
npm install @byteplus/veplayer
```



2. After installing, import VePlayer and its CSS file to your project as shown below:


```Bash
import VePlayer from '@byteplus/veplayer';
import '@byteplus/veplayer/dist/index.min.css';
```


<span id="Adding a container for the player"></span>
## Adding a container for the player

Add a player container to the page where you want to display the player. For example, add the following code to `index.html`:

```html
<div id="video"></div>
```


<span id="Creating a VePlayer instance"></span>
## Creating a VePlayer instance

Create a VePlayer instance by using the following code. The player starts playing once the page loads. If you want to play a live stream, set `isLive` to `true` and `url` to a pull stream address. Refer to the [API reference](https://docs.byteplus.com/byteplus-media-live/docs/api-reference) for details about the parameters.

```javascript
const playerSdk = new VePlayer({
  id: 'video',
  isLive: true,
  url: '//livepull.example.com/appname/streamname.flv'
});
```


<span id="Implementing more features"></span>
## Implementing more features

The Player SDK provides a variety of features covering multiple playback scenarios, including custom cover images, picture\-in\-picture, preview thumbnails when the progress bar is hovered over, and advanced features such as auto\-degradation of video resolution and playing live streams in RTM protocol.

Refer to the [API reference](https://docs.byteplus.com/byteplus-media-live/docs/api-reference) for detailed descriptions of the parameters, methods, and callbacks the Player SDK offers.
