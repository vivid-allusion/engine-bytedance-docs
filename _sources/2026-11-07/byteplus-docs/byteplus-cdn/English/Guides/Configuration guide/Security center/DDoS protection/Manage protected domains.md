---
title: "Manage protected domains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Manage_protected_domains"
---

This document describes how to manage protected domains in the BytePlus CDN management console, including adding and deleting domains.

<span id="add-domains"></span>
## Add domains

After you create an Advanced DDoS Protection instance, Advanced DDoS Protection is not automatically enabled for domains added to CDN under your BytePlus account. You need to manually add the domains to be protected to this instance. Once a domain is added, Advanced DDoS Protection is enabled for it.

<span id="limitations"></span>
### Limitations

By default, an Advanced DDoS Protection instance can protect up to 50 domains. If more domains need to be protected, additional fees will be charged. For billing information, see [Pricing details](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-pricing).

<span id="precautions"></span>
### Precautions


* Enabling Advanced DDoS Protection for a domain incurs fees for secure traffic. The fees are calculated based on the amount of data transferred from CDN to clients. For more information, see [Pricing details](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-pricing).

* After enabling Advanced DDoS Protection for a domain, you do not need to modify the DNS resolution configuration for the domain. However, DNS will stop resolving the domain name to an IPv6 address even if you have enabled IPv6 in your CDN policy. All traffic is directed to the corresponding IPv4 address dedicated to DDoS protection.

* Enabling Advanced DDoS Protection may introduce additional latency in domain name access. The extent of this latency depends on client locations and network environment.


For more information, see [Considerations when using Advanced DDoS Protection](https://docs.byteplus.com/en/docs/byteplus-cdn/DDoS_protection_levels#considerations-when-using-advanced-ddos-protection).

<span id="steps"></span>
### Steps


1. Log in to the [BytePlus CDN management console](https://console.byteplus.com/cdn).

2. In the left navigation pane, choose **Security center** \> **DDoS protection**.

3. In the **Protected domains** section on the **DDoS protection** page, click **Add domain**.

4. In the list of all domains, select the domains to be protected and click **Confirm**.

   The quota of domains that can be protected by the instance and the number of domains currently being protected are displayed above the list. The number of domains you can select is the difference between the preceding two values. For example, if the quota of domains is 50 and the number of domains currently being protected is 45, you can add up to 5 more domains.


<span id="54419edd"></span>
### More information

<span id="b5dc4328"></span>
#### Protection mode

Advanced DDoS Protection instances support the following protection modes:


* **Dynamic Switch**: Under normal conditions, your domain resolves directly to a CDN service IP address for optimal performance. If the system detects a sudden traffic surge, it automatically reroutes traffic by resolving your domain to the IP address of the Advanced DDoS Protection instance. This DNS update may take several minutes to take effect. This mode is ideal for domains that require a balance between performance and security.

* **Always On**: Your domain always resolves to the IP address of the Advanced DDoS Protection instance. This mode provides constant protection and is recommended for domains that are frequently targeted by attacks.


When you add a domain to an Advanced DDoS Protection instance, the **Dynamic Switch** mode is enabled for the domain by default. If your domain is frequently attacked, we recommend that you manually switch its protection mode to **Always On**.

<span id="513048c9"></span>
#### Protection status

In **Dynamic Switch** mode, your domain may have one of the following protection status:


* Monitoring: Under normal conditions without attacks, your domain resolves to a CDN service IP address, leveraging widely distributed nodes for high\-quality performance. In this case, the protection status is displayed as "Monitoring."

* Running: If a sudden traffic surge is detected, your domain will resolve to the IP address of the Advanced DDoS Protection instance, and the protection status changes to "Running." During this period, the network\-layer DDoS protection service analyzes traffic for threats.

* Scrubbing: If the DDoS protection service identifies attack traffic, it automatically begins traffic scrubbing. The protection status then changes to "Scrubbing."

   Once the attack traffic ceases, the system enters a default waiting period to ensure that the threat is completely neutralized. The protection status then reverts to "Monitoring," and traffic is routed back to the CDN service IP address. If you need to restore the original routing sooner, please submit a ticket.


In **Always On** mode, your domain's protection status will be either "Running" or "Scrubbing".

<span id="delete-a-domain"></span>
## Delete a domain

If a domain no longer needs Advanced DDoS Protection, you can remove it from the list of protected domains to free up the corresponding domain quota.

<span id="precautions"></span>
### Precautions

After you remove a domain from the list of protected domains, Advanced DDoS Protection for that domain is disabled.

<span id="steps"></span>
### Steps


1. Log in to the [BytePlus CDN management console](https://console.byteplus.com/cdn).

2. In the left navigation pane, choose **Security center** \> **DDoS protection**.

3. In the **Protected domains** section on the **DDoS protection** page, find the domain you want to delete, and click **Delete** in the **Actions** column.

4. In the dialog box that appears, click **OK**.
