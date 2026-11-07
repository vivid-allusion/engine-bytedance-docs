---
title: "IPv6 Origin Fetch"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/origin_ip_preference_en"
---

This document introduces the "IPv6 Origin Fetch" feature in BytePlus CDN.

<span id="overview"></span>
## Overview

The IPv6 Origin Fetch feature in BytePlus CDN allows you to control whether the CDN prioritizes IPv4 or IPv6 when resolving your origin's domain name. By default, the CDN attempts to match the IP version of the end\-user's request. This feature gives you the flexibility to override this default behavior, ensuring that origin requests follow your preferred IP version for routing or compatibility purposes.

For origins that are domain names, when the CDN requests content from the origin, it resolves the domain name to an IP address using DNS. By default, the CDN attempts to obtain an IP address for the origin that has the same version (IPv4 or IPv6) as the user's request. That is to say:


* If a user connects with an IPv6 address, the CDN first attempts to resolve an IPv6 address for the origin. If that fails, it falls back to resolving an IPv4 address.


If you want CDN to prioritize obtaining a specified type of IP address during DNS resolution, you can configure the "IPv6 Origin Fetch" feature.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This feature is not applicable to origins configured with an IP address.</div>


* <div data-tips="true" data-tips-type="tip">To allow users to connect to the CDN over IPv6, you must first <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs-ipv6">enable IPv6</a> in the domain name configuration.</div>



<span id="steps"></span>
## Steps


1. Open the **IPv6 Origin Fetch** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Select one of the following **Origin IP Version** options:

   * **Match Request**: The CDN attempts to retrieve an IP address for the origin that matches the IP version of the user's request. This is the default setting.

   * **Prioritize IPv6**: The CDN always attempts to resolve an IPv6 address for the origin first. If that fails, it falls back to resolving an IPv4 address.

   * **Prioritize IPv4**: The CDN always attempts to resolve an IPv4 address for the origin first. If that fails, it falls back to resolving an IPv6 address.

3. After making the changes, click **Save** at the bottom right of the page.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b62a08af03e5272321a79cf9a396a90a.png) </span>
