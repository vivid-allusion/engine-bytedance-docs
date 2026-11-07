---
title: "Distribution settings"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-domain-name-settings"
---

To customize how your video content is delivered in BytePlus VOD, this guide shows you how to configure the main distribution protocol and the distribution rule. You can change the default protocol for preview URLs and set a specific domain for distribution instead of using random routing.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08eee146e1e14ecfa92aae96b8778220~tplv-goo7wpa0wc-image.image) </span>

<span id="316eed95"></span>
## Configuring the main distribution protocol

In BytePlus VOD, the default main distribution protocol is HTTP. This configuration affects the URLs for previewing videos and subtitles in the VOD console.

To change the main distribution protocol, follow these steps:


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration \> Distribution settings** on the left navigation bar.

3. Click the **Modify** button at the bottom of the page.

4. Under **Main distribution protocol**, select the protocol that you want.

5. Click **Save**.


<span id="82ce8a60"></span>
## Configuring the distribution rule

If you have added multiple domain names in a space, requests are distributed randomly by default.

To change the distribution rule, follow these steps:


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration \> Distribution settings** on the left navigation bar.

3. Click the **Modify** button at the bottom of the page.

4. Under **Distribution rule**, click **Distribute based on the default domain name** and select a default domain name.

5. Click **Save**.
