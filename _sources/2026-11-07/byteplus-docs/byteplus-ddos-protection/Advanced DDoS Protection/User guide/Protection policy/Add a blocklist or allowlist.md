---
title: "Add a blocklist or allowlist"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-configuring-an-allowlist-or-blocklist"
---

To precisely control traffic to your services, you can configure a blocklist and an allowlist for your Advanced DDoS Protection instance. This guide provides step\-by\-step instructions on how to add IPs to a blocklist to deny access or to an allowlist to grant access, ensuring you can effectively manage requests from specific sources.

<span id="08b65ffc"></span>
## Limitations


* The blocklist or allowlist only applies to a single Advanced DDoS Protection instance. If you need to set up a blocklist or allowlist for multiple instances, please set them up separately.

* An IP address cannot be on the blocklist and the allowlist at the same time.

* Up to 1,000 IP addresses can be added to a blocklist or allowlist.


<span id="3aa9c7c0"></span>
## Before you begin

Ensure you have an active BytePlus Advanced DDoS Protection instance.

<span id="f4eb6086"></span>
## Procedure


1. Log in to the [BytePlus Advanced DDoS Protection Console](https://console.byteplus.com/ddos-protection/advance/instances).

2. In the left\-side navigation pane, choose **Advanced DDoS Protection** \> **Protection policy**.

3. Choose **DDoS attack protection** tab, and select an instance to configure.

4. Choose **Blocklist** or **Allowlist** tab, and click **Add**.

5. Enter the IP addresses. You can use spaces or line breaks to separate IP addresses.

6. Click **OK**.


<span id="ffe2a7d5"></span>
## Related operations

On the **Blocklist/Allowlist settings** page, you can also perform the following actions.


* Click **Download** to download the blocklist or allowlist of the current instance to check all the IP addresses in the list.

* Click **Delete** to remove a specific IP address.

* Click **Clear** **all** to delete all the IP addresses in the blocklist or allowlist.
