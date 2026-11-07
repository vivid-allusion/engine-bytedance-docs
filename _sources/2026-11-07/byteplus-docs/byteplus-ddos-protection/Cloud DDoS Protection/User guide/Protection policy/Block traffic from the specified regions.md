---
title: "Block traffic from the specified regions"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/Block_traffic_from_the_specified_regions"
---

Regional blocking is a location\-based access control policy that prevents business disruptions by intercepting or rate\-limiting traffic from specific areas. It is ideal for scenarios such as defending against region\-specific attacks, restricting access from non\-business areas, or meeting legal compliance requirements. This document will guide you through the steps to configure regional blocking rules to protect your services.

<span id="3253e38d"></span>
## Applicable scenarios


* **Defend** ** against** ** attacks from specific regions**: When you identify that attack traffic originates primarily from one or more regions, you can block IP addresses from those regions to mitigate the attacks.

* **Restrict access from non\-business areas**: If your services are only available in specific regions, you can block IP addresses from other regions to reduce exposure risk.

* **Meet compliance requirements**: Certain businesses may need to prohibit access from users in specific countries/regions due to legal and regulatory restrictions.


<span id="9e813fc0"></span>
## Important notes


* Regional blocking rules support IPv4 addresses. IPv6 addresses are not currently supported.

* If an IP from a blocked region is added to the IP allowlist, requests from that IP will be allowed.

* Protection actions, such as blocking traffic or applying rate limits, are triggered only after Cloud DDoS Protection detects an attack.


<span id="3e155aa8"></span>
## Actions

Regional blocking supports two types of actions:


* **Block**: After an attack is detected, Cloud DDoS Protection blocks all request traffic from the specified regions. This action is ideal for mitigating attacks or blocking malicious behavior.

* **Rate limit**: After detecting an attack, Cloud DDoS Protection applies rate limits to request traffic from the specified regions. Requests within the configured packet rate threshold are allowed, while packets exceeding the threshold are discarded.


<span id="a5e6c914"></span>
## Steps


1. Log in to the [Cloud DDoS Protection Console](https://console.byteplus.com/ddos-protection/).

2. In the left navigation pane, select  **Cloud DDoS Protection** ** \> ** **Protection policy**.

3. From the protection policy list, find your target rule group. To open its settings, click the rule group's name or click **Set rules** in the **Actions** column.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2d4128bdd43940f5ab94402e70d5f3a0) </span>


&nbsp;


&nbsp;

4. Select **Regional blocking** and click **Add region**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/790f4265ee4248b7b0fd5d070ea6c662) </span>

5. Select the regions to block.

   * Single selection: Select regions individually.

   * Quick filter: Select all of **Mainland China** or all regions **Outside** ** mainland China** with one click.

6. Set the action for the selected regions.

   * Block: Blocks requests from the selected regions when an attack is detected.

   * Rate limit: Limits the rate of requests from the selected regions when an attack is detected. Set a packet rate threshold between 1 and 10,000,000 pps. For example, if you set the threshold to `1,000,000` pps, any packets from the selected regions that exceed this rate during an attack are discarded.
