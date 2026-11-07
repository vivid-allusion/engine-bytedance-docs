---
title: "Adding a CNAME record"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-adding-a-cname-record"
---

After you add a domain name in the BytePlus MediaLive console, a BytePlus MediaLive domain name will be automatically assigned to your domain name, and you can find it in the **CNAME** column in the domain name list.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/921578252bd64ce5b8cdba2a4952cb4d~tplv-goo7wpa0wc-image.image) </span>

To use the BytePlus MediaLive service, you must add a CNAME record for your domain name to point to the assigned BytePlus MediaLive domain name.

<span id="78110c72"></span>
### Prerequisites


* A domain name whose status is **Offline** or **Online**.

* No CNAME record is configured for the domain name, that is, a yellow exclamation point (!) icon is displayed in the **CNAME** column.


<span id="a9099180"></span>
### Procedure

This topic describes a common method to configure a CNAME record. The procedure is for reference only. If you cannot configure a CNAME record after taking the following steps, contact the domain service provider for more information.


1. Log in to the console of your domain service provider.

2. Select the domain name that you want to manage.

3. On the page that appears, configure the following parameters to add a CNAME record.

   * Host record: Enter the prefix of the subdomain name. For example, if the domain name is example.live.com, enter `example` as the host record.

   * Record type: Select **CNAME**.

   * Line type: Select the default line type.

   * Record value: Enter the corresponding CNAME address of the domain name. You can find the CNAME address in the domain name list of the BytePlus MediaLive console.

   * TTL: We recommend that you enter 600s.

4. Save the configuration and wait for the configuration to take effect. After the configuration takes effect, a green check mark (✓) icon is displayed in the **CNAME** column in the domain name list.
