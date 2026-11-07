---
title: "Common playback configurations"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/common-playback-configurations"
---

To get a playback address tailored to your specific needs from the BytePlus VOD service, you can configure various settings. This guide explains how to customize the playback URL by managing domain names, applying transcoding rules, and setting specific playback parameters to suit different scenarios.

<span id="9cff79a8"></span>
## Domain name configuration

<span id="bfd6e3dc"></span>
### Configure domain names

Add domain names to generate playback addresses. See [Adding domain name](https://docs.byteplus.com/en/docs/byteplus-vod/docs-domain-name-management) for details.

<span id="ddcb9c9a"></span>
### Configure CNAME

Make sure you have added a CNAME record for your domain name, or playback will not be possible. See [Adding CNAME record](https://docs.byteplus.com/en/docs/byteplus-vod/docs-configuring-cname) for details.

<span id="b72ef549"></span>
### Configure custom\-origin domain names

Add a custom\-origin domain name if you need to redirect to a third\-party origin server that does not belong to BytePlus VOD. See [Adding domain name](https://docs.byteplus.com/en/docs/byteplus-vod/docs-domain-name-management) for details.

<span id="2fb72358"></span>
### Configure playback address validity duration

When you get the playback address by calling [GetPlayInfo](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getplayinfo), you can:


* Configure the [anti-hotlinking with timestamp](https://docs.byteplus.com/en/docs/byteplus-vod/docs-timestamp-) feature to control playback address validity duration for playback domain names. The validity duration is set to 60 minutes by default.

* Configure the validity duration in the URL signing feature to control the playback address validity duration for custom\-origin domain names. See [URL signing](https://docs.byteplus.com/en/docs/byteplus-vod/docs-url-authentication-overview) for details.


<span id="14b27098"></span>
### Configure SSL certificate

By default, the protocol for playback and image addresses returned by BytePlus VOD is HTTP. If you require an HTTPS address, you must [configure the SSL certificate](https://docs.byteplus.com/en/docs/byteplus-vod/docs-configuring-ssl-certificates).

<span id="9771e063"></span>
### Select from multiple domain names

If multiple domain names are configured on your origin server, set the `PlayDomain` parameter in `PlayConfig` when calling [GetPlayInfo](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getplayinfo) to get the playback address for the specified domain name.

<span id="8793e0fe"></span>
### Configure cross\-domain access

If using the Web Player SDK generates an `Access-Control-Allow-Origin` or other cross\-domain resource permission error, you will need to configure the playback domain name to allow cross\-domain access. See [Configure HTTP response headers](https://docs.byteplus.com/en/docs/byteplus-vod/docs-http-response-headers) for details. The table below lists the HTTP response headers you will need to configure:


|Response Header Name |Response Header Value |
|---|---|
|Access\-Control\-Allow\-Origin |Specify the sites that can be accessed by cross\-domain requests. The value obtained can be `*` or your website domain name; for example if your website is `https://www.example.com`, the parameter value will be `https://www.example.com`. |
|Access\-Control\-Allow\-Methods |Specify allowed cross\-domain request methods. The value can be `*` or can include `GET, HEAD, OPTIONS`. |
|Access\-Control\-Expose\-Headers |Specify the HTTP request headers that can be contained in cross\-domain requests. The value can be `*` or can include `Range`. |


<span id="444e5314"></span>
## Transcoding configuration

BytePlus VOD lets you decide whether to transcode the audio and video files you upload to BytePlus VOD.


* If you do not transcode your files, the playback address that you obtain from the playback service will be the original file you uploaded to BytePlus VOD and playback will use the original resolution.

* If you transcode your files, the playback address obtained will be generated post\-transcoding. You can use transcoding to generate files of different formats, resolutions, encryption methods (or none) and/or watermarks. For more information, see [Audio and video transcoding](https://docs.byteplus.com/en/docs/byteplus-vod/docs-audio-and-video-transcoding).


<span id="63579b96"></span>
## Set playback parameters

You can set different playback parameters for different playback methods:


* Console preview: No configuration needed.

* Get playback address: Call [GetPlayInfo](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getplayinfo) and set various request parameters to get the corresponding playback address. If a parameter does not correspond to an available transcoding output, the service defaults to using the original input video.

   * `Definition`: Get a playback address for a specific resolution. If left empty, the API will return playback addresses for all resolutions that exist for the specified video.

   * `Format`: Get a playback address for a specific container format. You can choose between different formats of transcoding output files for playback based on various playback scenarios.

   * `FileType`: Get an unencrypted or encrypted playback address.

* Player SDK: The Player SDK supports using temporary playback tokens to automatically exchange them for playback addresses. Configure the playback settings in the Player SDK so that the player automatically gets the corresponding playback address. The playback settings supported by each SDK are listed below:

   * Android Player SDK: Vid mode supports codec and default resolution settings. See [Set playback sources](https://docs.byteplus.com/en/docs/byteplus-vod/docs-getting-started-with-the-android-player-sdk#step-6-set-the-playback-source) for details.

   * iOS Player SDK: Vid mode supports codec and default resolution settings. See [Configure playback sources](https://docs.byteplus.com/en/docs/byteplus-vod/docs-getting-started-with-the-ios-player-sdk#step-8-set-the-playback-source) for details.

   * Web Player SDK: Supports resolution settings. See [Display multiple resolutions](https://docs.byteplus.com/en/docs/byteplus-vod/docs-implementing-basic-features-web#displaying-multiple-resolutions) for details.
