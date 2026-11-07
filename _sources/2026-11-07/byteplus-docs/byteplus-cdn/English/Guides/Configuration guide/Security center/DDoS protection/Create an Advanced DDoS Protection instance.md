---
title: "Create an Advanced DDoS Protection instance"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Create_an_Advanced_DDoS_Protection_instance"
---

This document describes how to create an Advanced DDoS Protection instance on the **DDoS protection** page in the BytePlus CDN management console. Once an Advanced DDoS Protection instance is created, your BytePlus account subscribes to and activates the Advanced DDoS Protection service.

<span id="background-information"></span>
## Background information

For network and transport layer DDoS attacks, CDN provides Standard DDoS Protection and Advanced DDoS Protection. For more information, see [Comparison between Standard DDoS Protection and Advanced DDoS Protection](https://docs.byteplus.com/en/docs/byteplus-cdn/DDoS_protection_levels#comparison-between-standard-ddos-protection-and-advanced-ddos-protection).

To use Advanced DDoS Protection, you need to subscribe to CDN\-Security\-Plan Advanced Edition or create an Advanced DDoS Protection instance.

<span id="limitations"></span>
## Limitations


* To use the Advanced DDoS Protection feature, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000735).

* Only one Advanced DDoS Protection instance can be created under a single BytePlus account.


<span id="precautions"></span>
## Precautions


* Fees for secure traffic apply if you enable Advanced DDoS Protection for a domain without a subscription to CDN\-Security\-Plan Advanced Edition. The fees are calculated based on the amount of data transferred from CDN to clients. For billing information, see [Pricing details](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-pricing).

* After enabling Advanced DDoS Protection for a domain, you do not need to modify the DNS resolution configuration for the domain. However, DNS will stop resolving the domain name to an IPv6 address even if you have enabled IPv6 in your CDN policy. All traffic is directed to the corresponding IPv4 address dedicated to DDoS protection.

* Enabling Advanced DDoS Protection may introduce additional latency in domain access. The extent of this latency depends on client locations and network environment.


For more information, see [Considerations when using Advanced DDoS Protection](https://docs.byteplus.com/en/docs/byteplus-cdn/DDoS_protection_levels#considerations-when-using-advanced-ddos-protection).

<span id="steps"></span>
## Steps


1. Log in to the [BytePlus CDN management console](https://console.byteplus.com/cdn).

2. In the left navigation pane, choose **Security center** \> **DDoS protection**.

3. In the **Instance management** section on the **DDoS protection** page, click **Create instance**.

4. On the **Create Advanced DDoS Protection instance** page, configure the following parameters:

   * **Number of protected domains**: Set the number of domains to be protected. The number of domains should not be less than 50 and must be a multiple of 5.

      By default, an Advanced DDoS Protection instance can protect up to 50 domains. If more domains need to be protected, additional fees will be charged. For billing information, see [Pricing details](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-pricing).

   * **Duration**: Specify the subscription duration.

      Other parameters on this page are system\-specified and cannot be manually modified. Explanations for these parameters are as follows:

   * **Region**: The region where Advanced DDoS Protection provides services. Currently, Advanced DDoS Protection can only be used in areas outside Chinese mainland.

   * **Provisioning mode**: The provisioning mode of Advanced DDoS Protection. The Advanced DDoS Protection service of CDN is deployed in **CDN interaction** mode.

   * **Reserved resources**: Reserved exclusive IP address. When you subscribe to Advanced DDoS Protection, CDN will allocate you an exclusive IP address dedicated to DDoS protection.

   * **Protection capability**: The protection capability provided by Advanced DDoS Protection. The fixed value is **Full protection**. **Full protection** means that the maximum protection capacity of scrubbing centers will be used to protect against DDoS attacks.

   * **Data transfer fees**: The fees for secure traffic. The fees are calculated based on the amount of data transferred from CDN to clients.

5. After confirming that the configuration is correct, check **I have read and agree to Service Specific Terms,**  **Service Level Agreement,Customer Agreement**, and then click **Create**.

6. Complete the payment as prompted on the page. The created instance will be displayed in the instance list on the **DDoS protection** page.


<span id="next-steps"></span>
## Next steps


1. [Add domains](https://docs.byteplus.com/en/docs/byteplus-cdn/Manage_protected_domains#add-domains): After creating an Advanced DDoS Protection instance, you need to manually add the domains to be protected.

2. (Optional) [View monitoring data](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-viewing-ddos-attack-protection-information): You can view DDoS protection data such as attack traffic, attack frequency, traffic sent to your origin server from CDN, traffic sent from CDN to clients, and attack events on the dashboard page.
