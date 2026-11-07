---
title: "Block requests with specific protocol"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/Block_requests_with_specific_protocol"
---

Protocol blocking allows you to restrict access from specific protocol types, such as UDP or ICMP, to defend against targeted attacks like flood attacks. When Cloud DDoS Protection detects an attack, it automatically discards requests of the blocked protocol type to reduce your business exposure. This guide explains common protocol\-based attacks and provides step\-by\-step instructions for configuring protocol blocking rules.

<span id="6239213c"></span>
## Common protocol attack types


* **ICMP flood attack**: The attacker overwhelms the target server by continuously sending a large number of ICMP requests (e.g., `ping` command), preventing it from responding to legitimate traffic.

* **UDP flood attack**: Utilizing the characteristic of the UDP protocol that does not require connection establishment, the attacker can quickly send a large number of UDP packets with spoofed source addresses, consuming the target server's processing power and bandwidth resources.

* **SYN flood attack**: The attacker abuses the TCP three\-way handshake mechanism by continuously sending a large number of forged SYN connection requests, causing the server to maintain a large number of half\-open connections and ultimately depleting system resources.


<span id="9c83b479"></span>
## **Applicable scenarios**


* **Block specific protocol attacks**: When you identify that the attack traffic primarily targets a specific protocol (such as UDP or ICMP), you can block that protocol to stop the attack traffic.

* **Minimize protocol exposure**: If your business only uses specific protocols (such as TCP), you can block other unnecessary protocols to reduce unnecessary exposure.


<span id="743bafa2"></span>
## **Important notes**


* **Protection trigger mechanism**: When the Cloud DDoS Protection detects an attack, it blocks the request traffic of the specified protocol.

* **Rule priority**: If the blocked protocol request comes from an IP address on an allowlist, the request will be allowed.


<span id="674ed813"></span>
## Prerequisites

You have purchased and activated the Cloud DDoS Protection service. Related operations can refer to [Step 1: Create a Cloud DDoS Protection instance](https://docs.byteplus.com/docs/byteplus-ddos-protection/Get_started_with_Cloud_DDoS_Protection#f147827f).

<span id="e35e8161"></span>
## **Steps**


1. Log in to the [Cloud DDoS Protection Console](https://console.byteplus.com/ddos-protection/).

2. In the left navigation pane, select  **Cloud DDoS Protection** ** \> ** **Protection policy**.

3. From the protection policy list, find your target rule group. To open its settings, click the rule group's name or click **Set rules** in the **Actions** column.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2d4128bdd43940f5ab94402e70d5f3a0) </span>


&nbsp;


&nbsp;

4. Select **Protocol filtering** and turn on the switch for the protocol that needs to be blocked.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f0dc4281984945278d7118df8af03a30) </span>


&nbsp;

&nbsp;
