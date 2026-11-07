---
title: "Refresh and warm-up"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-refresh-and-warm-up"
---

To ensure your users can access the latest video content or to improve download speeds for new releases, you can manage your CDN cache. This guide provides step\-by\-step instructions on how to configure cache refresh and content warm\-up tasks in the BytePlus VOD console.

<span id="eca66659"></span>
## What is refresh and warm\-up?


* Cache refreshing: Marks all cached resources in CDN nodes as invalid. Upon a subsequent request from a user, the CDN will fetch the resources from the origin server, return them to the user, and re\-cache them on the CDN node. Refresh may decrease the cache hit ratio.

* Content warm\-up: The origin server actively caches the resources to the CDN node(s) in advance. When you request a resource for the first time, you can directly obtain the latest resource from the CDN node without being redirected to the origin servers. Warm\-up can increase the cache hit ratio.


<span id="6cd4e649"></span>
## **Applicable scenarios**


|Feature |Applicable scenarios |
|---|---|
|Cache refresh |* Resource updates and releases: You can set the URLs or directories to refresh whenever resources on the origin server are updated or upgraded, to ensure users can access the latest content.<br><br>* Illegal resource clean\-up: Users will still be able to access any illegal content deleted from the origin server if the corresponding resources are cached on the CDN node(s). You can configure the corresponding URL or directory to clear the cache for such illegal content. |
|Content warm\-up |* Events: You can prewarm the static resources required by the event page to the CDN node in advance when hosting large\-scale events.<br><br>* Installation package release: You can prewarm relevant resources on the CDN node in advance when releasing updated installation packages. This allows the CDN node to respond to requests directly, which greatly improves download speeds and significantly reduces the pressure on origin servers when large numbers of users all initiate download requests upon an official product launch. |


<span id="7044ccbe"></span>
## Refresh quota

The daily file and directory refresh quotas per space are as follows:


* You can refresh up to 1,000 single files per day.

* You can refresh up to 50 directories per day.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The refresh quota is shared by the main account and sub\-accounts.</div>


<span id="dfa55e32"></span>
## Configuring the cache refreshing task


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration** \> **Refresh and warm\-up** in the left navigation bar.

3. You can configure your refresh task on the **Cache refresh** tab as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d15b4a921574da487aaaed29c72f2d5~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Description |
   |---|---|
   |Refresh type |The following refresh types are supported:<br><br><br>* **URL refresh**<br><br>* **Directory refresh** |
   |URL input |Input the URL(s). Separate multiple URLs with line breaks. Each URL must begin with either `http://` or `https://`<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">URLs must end in <code>/</code> for directory refreshes.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can only refresh domain names belonging to the current space.</div><br> |
   

4. Click **Submit**. You can check the status of successfully submitted tasks on the **Operation record** tab.


<span id="fabdc795"></span>
## Configure content warm\-up


1. Sign into the [BytePlus VOD console](https://console.volcengine.com/vod/overview/) and enter a specific space.

2. Click **Distribution acceleration** \> **Refresh and warm\-up** in the left navigation bar, then click the **Content warm\-up** tab.

3. Fill in the URL(s) on the **Content warm\-up** tab. Separate multiple URLs with line breaks. Each URL must begin with either `http://` or `https://`

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca69163c1a184d41bed1242e49953f02~tplv-goo7wpa0wc-image.image) </span>

4. Click **Submit**. You can check the status of successfully submitted tasks in the **Operation record**.
