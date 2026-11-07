---
title: "Origin Host"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/origin-hostname_en-us"
---

This topic describes how to configure the global Origin Host value that BytePlus CDN includes in the `Host` header of requests to your origin.

The global Origin Host setting is always enabled and cannot be disabled. You must set the global Origin Host to either the CDN domain or a custom domain. If your origin server hosts multiple websites, configuring the correct Origin Host ensures that BytePlus CDN retrieves content from the intended virtual host.

<span id="configuration-priority"></span>
## Configuration Priority

BytePlus CDN provides the following Origin Host settings:


* **Global Origin Host**: Applies to all origins in the distribution policy.

* **Per\-origin Origin Host**: Applies to a specific origin. You can configure a different Origin Host for each origin. A per\-origin Origin Host takes precedence over the global Origin Host. If you do not specify a per\-origin value, BytePlus CDN uses the global value. For configuration instructions, see [Standard Origins](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-configurations).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The global Origin Host does not apply to object storage origins. For these origins, BytePlus CDN uses either the Origin Host specified in the origin settings or a predefined Host header value for the cloud provider.</div>


<span id="procedure"></span>
## Steps


1. Open the **Origins** tab. For instructions, see [Domain Name Configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Locate **Origin Host**.

3. Select one of the following options for the global Origin Host:

   * **CDN Domain**: Uses the current CDN domain as the global Origin Host.

   * **Custom Domain**: Enter the hostname of the website hosted on the origin server. The Origin Host value can contain up to 1,024 characters.

4. Click **Save**.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260814062022-210497174568.png) </span>
