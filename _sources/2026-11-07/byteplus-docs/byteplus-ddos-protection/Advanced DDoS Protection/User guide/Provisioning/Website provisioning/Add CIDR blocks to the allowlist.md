---
title: "Add CIDR blocks to the allowlist"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/adding-CIDR-blocks-to-the-allowlist"
---

To ensure the back\-to\-origin requests can be properly forwarded to your origin server, you should add the CIDR blocks to the allowlist of the firewall, access control list (ACL), or any other security software.

<span id="b87b2d74"></span>
## Background information

After adding your service to Advanced DDoS Protection, all requests are redirected to your origin server from the back\-to\-origin CIDR blocks of the Advanced DDoS Protection instance. Consequently, the volume of requests from each back\-to\-origin IP might increase, which can trigger blocking or rate limiting by your security policies. Therefore, you must add our back\-to\-origin CIDR blocks to your allowlist.

If your origin server uses a firewall or other security software, add the back\-to\-origin CIDR blocks to its allowlist. This ensures that your security policies do not block traffic from the back\-to\-origin IP addresses.

<span id="8f768029"></span>
## Before you begin

Add a domain name to your Advanced DDoS Protection instance.

<span id="35e92263"></span>
## Procedure


1. Log in to the [BytePlus Advanced DDoS Protection Console](https://console.byteplus.com/ddos-protection/advance/instances).

2. In the left\-side navigation pane, choose **Advanced DDoS Protection** \> **Provisioning**.

3. On the **Website config** tab, click **View back\-to\-origin CIDR blocks**.

4. Click **Copy all**.

5. Add all the CIDR blocks to the allowlist of the firewall, access control list (ACL), or any other security software.


<span id="652363e6"></span>
## What to do next

If you selected HTTPS as the protocol type, you must upload an SSL certificate and add it to your domain name. For more details, see [Uploading an SSL certificate](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-uploading-an-ssl-certificate) and [Setting an SSL certificate for domain name](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-setting-an-SSL-certificate-for-domain-name).
