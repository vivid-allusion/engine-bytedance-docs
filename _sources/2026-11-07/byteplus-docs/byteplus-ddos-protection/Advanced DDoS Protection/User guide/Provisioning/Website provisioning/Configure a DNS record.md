---
title: "Configure a DNS record"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-configuring-a-DNS-record"
---

To safeguard your website services, you must modify your domain's DNS record to use the CNAME provided by the Advanced DDoS Protection instance. This setup reroutes public network traffic through our scrubbing centers for filtering before forwarding it to your origin server, ensuring that only legitimate traffic reaches your service.

<span id="7f3a9c76"></span>
## Before you begin


* Add a domain name to be protected. For more details, see [Adding a domain name](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-adding-a-domain-name-to-the-instance).

* Add CIDR blocks to the allowlist. For more details, see [Adding CIDR blocks to the allowlist](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/adding-CIDR-blocks-to-the-allowlist).

* Set an SSL certificate for your domain name if your domain name uses the HTTPS protocol. For more details, see [Setting an SSL certificate for domain name](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-setting-an-SSL-certificate-for-domain-name).


<span id="4d42da8f"></span>
## Procedure


1. Log in to the [BytePlus Advanced DDoS Protection Console](https://console.byteplus.com/ddos-protection/advance/instances).

2. In the left\-side navigation pane, choose **Advanced DDoS Protection** \> **Provisioning**.

3. Choose **Website config** tab, and click the copy icon of the domain name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f733c3c84504c12b5e874cdbebf05c7~tplv-goo7wpa0wc-image.image) </span>

   The CNAME record of your domain name will be copied.

4. Go to your DNS provider, and add the CNAME record to redirect your service traffic to the instance of Advanced DDoS Protection.


<span id="2df697ad"></span>
## What to do next

We recommend confirming that the forwarding configuration is effective. This step helps prevent service interruptions that can result from an incorrect configuration.
