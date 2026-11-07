---
title: "Bandwidth limit"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/Bandwidth_limit"
---

To prevent sudden traffic spikes from causing network congestion and affecting user experience, you can configure bandwidth limits for your domain name for stream pulling. This topic describes how to configure a bandwidth limit and an alert threshold in the BytePlus MediaLive console.

<span id="35916e45"></span>
## Application scope

Domain name for stream pulling

<span id="701951c3"></span>
## Feature overview

Bandwidth is part of network resources. A sudden increase in traffic to a domain name for stream pulling may cause network congestion and affect the user experience. Configuring bandwidth limits helps allocate bandwidth resources based on actual needs.

BytePlus MediaLive supports bandwidth limits and bandwidth alert thresholds for a domain name for stream pulling. When peak downstream bandwidth exceeds the configured alert threshold, alerts are sent by SMS and in\-app notifications. When peak downstream bandwidth exceeds the configured limit, new stream pull requests are denied.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, bandwidth limits can be configured only for RTM, FLV, and RTMP stream pulling. The configuration does not take effect for HLS or CMAF stream pulling.</div>


<span id="07acdeb4"></span>
## Prerequisites

You have added a domain name for stream pulling. For more information, see [Adding a domain name](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain).

<span id="d52fbb7a"></span>
## Procedure


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live/main/domain/list).

2. In the left\-side navigation pane, click **Domains**.

3. On the **Domains** page, click **Settings** to the right of the target domain name for stream pulling.

4. On the **Advanced settings** tab, in the **Bandwidth limit** section, turn on the switch or click **Edit**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98ea53b5cbb64fac87f5d7e7e1cb0832~tplv-goo7wpa0wc-image.image) </span>

5. In the **Bandwidth Limit** dialog box that appears, complete the following settings and then click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dca8dfccc941458ea9cc671eaedf95f2~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Description |
   |---|---|
   |Bandwidth Limit |Turn on the switch. |
   |Restrict quota |Enter the bandwidth limit for stream pulling. Available units are Mbps, Gbps, and Tbps.<br><br>When the peak downstream bandwidth exceeds the configured value, BytePlus MediaLive denies new stream pull requests. The valid value range is [1,10000]. |
   |Alert threshold |Enter the bandwidth alert threshold for stream pulling. Available units are Mbps, Gbps, and Tbps.<br><br>When the peak downstream bandwidth exceeds the configured value, BytePlus MediaLive sends alerts by SMS and in\-app notifications. The valid value range is [1,10000], and the alert threshold must be less than or equal to the bandwidth limit. |
