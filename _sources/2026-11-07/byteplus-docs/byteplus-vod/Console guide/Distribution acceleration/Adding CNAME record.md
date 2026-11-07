---
title: "Adding CNAME record"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-configuring-cname"
---

After you add a domain name in the BytePlus VOD console, a corresponding BytePlus VOD domain name is automatically assigned. You can find this assigned domain name in the **CNAME** column of the domain name list.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6e43d107c1f407ea2b0c0ba56507ca3~tplv-goo7wpa0wc-image.image) </span>

To use the BytePlus VOD service, you must add a CNAME record for your domain name to point to the assigned BytePlus VOD domain name.

<span id="bb17558e"></span>
### Prerequisites


* A domain name whose status is **Disabled** or **Enabled**.

* No CNAME record is configured for the domain name, that is, a yellow exclamation point (!) icon is displayed in the **CNAME** column.


<span id="0eb92281"></span>
### Configuring a CNAME record

This topic describes a common method to configure a CNAME record. The procedure is for reference only. If you cannot configure a CNAME record after taking the following steps, contact the domain service provider for more information.


1. Log in to the console of your domain service provider.

2. Select the domain name that you want to manage.

3. On the page that appears, configure the following parameters to add a CNAME record.

   * Host record: Enter the prefix of the subdomain name. For example, if the domain name is `example.vod.com`, enter `example` as the host record.

   * Record type: Select **CNAME**.

   * Line type: Select the default line type.

   * Record value: Enter the corresponding CNAME address of the domain name. You can find the CNAME address in the domain name list of the BytePlus VOD console.

   * TTL: We recommend that you enter 600s.

4. Save the configuration and wait for the configuration to take effect. After the configuration takes effect, a green check mark (✓) icon is displayed in the **CNAME** column in the domain name list.
