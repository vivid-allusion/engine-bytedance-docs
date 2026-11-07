---
title: "Playback overview"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-playing-videos-overview"
---

To play audio and video files stored in BytePlus VOD, you can preview them in the console, integrate the Player SDK for a secure playback experience, or use a third\-party player. This guide details the required preparations, such as configuring a domain name and publishing your media, and provides instructions for each playback method.

<span id="6125b0e6"></span>
## Preparations

After uploading audio and video to the BytePlus VOD service, you need to complete the following preparations before playback:


* Configure and enable a **playback domain name** for generating the playback address for audio and video content. For details, see [Adding domain name](https://docs.byteplus.com/docs/byteplus-vod/docs-domain-name-management).

* Bind a CNAME record to the domain name. If you do not bind a CNAME record to the domain name, video playback fails. For details, see [Adding CNAME record](https://docs.byteplus.com/docs/byteplus-vod/docs-configuring-cname).

* Publish the audio and video. You can only obtain the playback address when the audio and video status is "Published". For details, see [Publishing status of audio and video assets](https://docs.byteplus.com/docs/byteplus-vod/docs-publishing-status). You can call the [GetMediaInfos](https://docs.byteplus.com/docs/byteplus-vod/reference-getmediainfos) API to check the publishing status of the audio and video through the `PublishStatus` parameter.

* Check the transcoding configuration. BytePlus VOD supports playing both the source files you upload without transcoding, and the transcoded videos.

* Check the security configuration. BytePlus VOD provides a comprehensive mechanism for securing audio and video content, including access restrictions, URL authentication, and video encryption. You can choose the appropriate security measures based on the security requirements of your business scenario.


<span id="f6a0c76f"></span>
## Playback methods

<span id="3965005c"></span>
### Using the console

You can preview a video stream in the BytePlus VOD console by the following two methods:

**Method 1: Quick preview**


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a space.

2. On the **Videos** page, click either the thumbnail of the desired video or the **Preview** button in the **Action** column to quickly preview the original video.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/598f9476ab964448a632bb3d80b59d3c~tplv-goo7wpa0wc-image.image) </span>


**Method 2: Multi\-stream preview**


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a space.

2. On the **Videos** page, select the desired video and navigate to the **Details** page.

3. Click on the **Playback address** tab.

4. Choose the desired stream for preview, as shown in the image below:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bea5d314d4e64201a6a10fd6445e5f3f~tplv-goo7wpa0wc-image.image) </span>


<span id="3d1a3176"></span>
### Using the Player SDK


* You can obtain a temporary playback token from your app server and distribute it to the client for playback. This method provides higher security. For more information, see [Playing videos with temporary playback tokens](https://docs.byteplus.com/docs/byteplus-vod/docs-playing-videos-with-temporary-playback-tokens).

* The Player SDK also supports directly passing the obtained playback address to the player for playback. For more information, see [Playing videos with playback addresses](https://docs.byteplus.com/docs/byteplus-vod/docs-playing-videos-with-playback-addresses).


<span id="341e3244"></span>
### **Using other players**

You can obtain the playback address from BytePlus VOD and then use any player for playback. For more information, see [Playing videos with playback addresses](https://docs.byteplus.com/docs/byteplus-vod/docs-playing-videos-with-playback-addresses).
