---
title: "Concurrent stream limit"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/Concurrent_stream_limit"
---

To manage your streaming resources and prevent overload, you can set a concurrent stream limit for a domain name for stream pushing. This topic describes how to configure a concurrent stream limit and an alert threshold in the BytePlus MediaLive console.

<span id="b7189901"></span>
## Application scope

Domain name for stream pushing

<span id="68819e6d"></span>
## Feature overview

BytePlus MediaLive supports concurrent stream limits and stream alert thresholds for a domain name for stream pushing.

When the number of concurrent streams exceeds the configured alert threshold, alerts are sent by SMS and in\-app notifications. When the number of concurrent streams exceeds the configured limit, new stream push requests are denied.

<span id="b645d265"></span>
## Prerequisites

You have added a domain name for stream pushing. For more information, see [Adding a domain name](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain).

<span id="3e1fe063"></span>
## Procedure


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live/main/domain/list).

2. In the left\-side navigation pane, click **Domains**.

3. On the **Domains** page, click **Settings** to the right of the target domain name for stream pushing.

4. On the **Advanced settings** tab, in the **Concurrent stream limit** section, turn on the switch or click **Edit**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7388689701f4c98810dd919dcad118f~tplv-goo7wpa0wc-image.image) </span>

5. In the **Stream pushing Limit** dialog box that appears, complete the following settings and then click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8d22985d9ad4fce9f1575167ef6e5d6~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Description |
   |---|---|
   |Stream pushing Limit |Turn on the switch. |
   |Restrict number of streams |Enter the concurrent stream limit for stream pushing.<br><br>When the number of concurrent streams for stream pushing exceeds the configured value, BytePlus MediaLive denies new stream push requests. The valid value range is [10,200000]. |
   |Alert threshold |Enter the alert threshold for stream pushing.<br><br>When the number of concurrent streams for stream pushing exceeds the configured value, BytePlus MediaLive sends alerts by SMS and in\-app notifications. The valid value range is [10,200000], and the alert threshold must be less than or equal to the configured stream limit. |
