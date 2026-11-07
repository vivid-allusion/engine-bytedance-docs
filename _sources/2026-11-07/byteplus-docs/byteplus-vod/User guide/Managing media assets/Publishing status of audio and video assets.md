---
title: "Publishing status of audio and video assets"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-publishing-status"
---

By default, newly uploaded audio and video assets in BytePlus VOD are **Unpublished** and cannot be played. To make them accessible, you must change their status to **Published**. This guide provides instructions on how to publish your media assets manually through the console, API, or Server SDKs, and also explains how to configure automatic publishing after uploading.

<span id="73a524d6"></span>
## Manual publishing

<span id="71eb4a49"></span>
### Using the console


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. In the left navigation bar, click **Media assets \> Videos**.

3. In the Actions column, click **Publish** or **Unpublish**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14a3c95418f2438e98d1bececef9a1f2~tplv-goo7wpa0wc-image.image) </span>


<span id="617a9e70"></span>
### Using the API

Call the [UpdateMediaPublishStatus](https://docs.byteplus.com/docs/byteplus-vod/reference-updatemediapublishstatus)API to modify the publish status of audio and video assets.

<span id="ac028bf1"></span>
### Using the Server SDKs

We recommend that you use the Server SDKs to call APIs to modify the publish status of audio and video assets. For details, refer to the following documents:


* [Java SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-java-sdk)

* [Python SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-python-sdk)

* [PHP SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-php-sdk)

* [Go SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-go-sdk)


<span id="106dded0"></span>
## Auto\-publishing after uploading

<span id="dfb930c3"></span>
### Method 1: Set video status automatically


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. In the left navigation bar, click **System settings \> Post\-upload actions**.

3. Click **Modify**.

4. Set **Auto\-publishing** to **Publish**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9da3bf705f804dc58f99a82bca39ca14~tplv-goo7wpa0wc-image.image) </span>


<span id="97b2cbb9"></span>
### Method 2: Configure and automatically trigger default workflow


1. When creating a workflow, select the **Auto publishing** task.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52b6252b8dca41f999f40068968d7e21~tplv-goo7wpa0wc-image.image) </span>

2. In **System settings \> Post\-upload actions**, go to the **Default settings** section and set the workflow that contains the auto publishing task as the default workflow.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5db19ab3d24245c993453e29532cee55~tplv-goo7wpa0wc-image.image) </span>

3. In **System settings \> Post\-upload actions**, go to the **Automatic actions** section and enable **Default workflow trigger**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b75dd62ca74445c2bbbfd6b7cc3df3ee~tplv-goo7wpa0wc-image.image) </span>
