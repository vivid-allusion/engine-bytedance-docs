---
title: "Origin Protocol"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/origin-protocol_en-us"
---

This topic describes how to configure the protocol that BytePlus CDN uses when sending requests to your origin.

The Origin Protocol setting is always enabled and cannot be disabled. You must select an origin protocol.

<span id="procedure"></span>
## Steps


1. Open the **Origins** tab. For instructions, see [Domain Name Configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Locate **Origin Protocol**.

3. Select the protocol for origin requests. For details about each option, see [Origin Protocol Options](https://docs.byteplus.com/en/docs/18/118283#origin-protocol-options).

4. Click **Save**.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260814061945-1444531854512.png) </span>

<span id="origin-protocol-options"></span>
## Origin Protocol Options


|Setting |Description |
|---|---|
|Origin Protocol |Select the protocol that BytePlus CDN uses when sending requests to your origin:<br><br>&nbsp;<br><br>\* **Follow Request**: Uses HTTP or HTTPS for the origin request based on the protocol of the incoming client request.<br><br>\* **HTTP**: Always uses HTTP for origin requests.<br><br>\* **HTTPS**: Always uses HTTPS for origin requests. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Your origin must support each applicable protocol on its configured port. For example, if you select <strong>HTTP</strong> and set the HTTP origin port to <code>8080</code>, the origin must accept HTTP requests on port <code>8080</code>. Otherwise, requests to the origin will fail.</div>
