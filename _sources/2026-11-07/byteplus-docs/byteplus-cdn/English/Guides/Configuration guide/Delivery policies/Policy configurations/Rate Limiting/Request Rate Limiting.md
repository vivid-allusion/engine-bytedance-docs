---
title: "Request Rate Limiting"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/rate-limiting_en-us"
---

This document describes the Request Rate Limiting feature in BytePlus CDN. This feature lets you limit the queries per second (QPS) from individual client IP addresses.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use this feature, please <a href="https://console.byteplus.com/workorder/create">submit a ticket</a>.</div>


<span id="overview"></span>
## Overview

For a client IP address, QPS is the number of requests sent from that IP address to a domain per second. QPS is counted at edge points of presence (PoPs).

If your domain is subject to a CC attack, it may generate a large amount of traffic in a short period, resulting in high charges. To reduce this risk, you can enable **Request Rate Limiting**.

After Request Rate Limiting is enabled, if the QPS of requests from an IP address exceeds the configured threshold, BytePlus CDN rejects newly received requests from that IP address and returns a `403` status code.

<span id="configure-an-appropriate-qps-threshold"></span>
## Configure an Appropriate QPS Threshold

A threshold that is too low may prevent legitimate users from accessing your site. However, a threshold that is too high defeats the purpose of configuring a QPS threshold.

You can view a domain’s historical QPS on the [Edge Report](https://docs.byteplus.com/en/docs/byteplus-cdn/bWlzDn) page in the CDN console and use the data to estimate an appropriate QPS threshold. Pay particular attention to QPS peaks and determine whether they align with your expected traffic patterns.

<span id="steps"></span>
## Steps


1. Open the **Request Rate Limiting** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to **Enable**.

3. Set **Threshold** to an appropriate QPS value. The supported range is `1` to `1,000,000`.

4. In the lower\-right corner of the page, click **Save**.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260814092608-295763184606.png) </span>
