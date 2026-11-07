---
title: "DDoS protection overview"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DDoS_protection_overview"
---

<span id="what-is-a-ddos-attack"></span>
## What is a DDoS attack?

A Distributed Denial of Service (DDoS) attack is a type of network attack. Attackers utilize multiple compromised devices, such as computers, to flood a target server with an overwhelming amount of packets or requests. These DDoS attacks rapidly deplete the target server's resources including bandwidth, CPU, and memory, making it unable to handle legitimate traffic or respond to legitimate requests.

DDoS attacks typically occur at the network layer (Layer 3), transport layer (Layer 4), and application layer (Layer 7) of the OSI model:


* Network layer attacks

   * Attackers use a large number of spoofed IP addresses to send a massive amount of packets to the target server, exhausting its network bandwidth and preventing it from processing legitimate network traffic.

* Transport layer attacks

   * Attackers use a large number of spoofed IP addresses to send numerous TCP or UDP connection requests to the target server, consuming its connection resources and preventing it from handling normal connection requests.

* Application layer attacks

   * Attackers use a large number of forged requests to send numerous HTTP requests to the target server, consuming its resources such as CPU and memory, causing it unable to respond to genuine requests.


DDoS attacks can cause significant business disruptions, often resulting in substantial financial losses. Internet applications and network infrastructure in industries such as gaming, e\-commerce, and finance are the main targets of DDoS attacks.

<span id="ddos-protection-provided-by-byteplus-cdn"></span>
## DDoS protection provided by BytePlus CDN

BytePlus CDN (hereafter referred to as CDN) offers a comprehensive defense against DDoS attacks through its DDoS protection and Web Application Firewall (WAF) features. The DDoS protection feature intercepts attacks at the network and transport layers, while the WAF feature safeguards against application layer attacks. By implementing these multi\-layered security measures, CDN effectively mitigates DDoS\-related risks, ensuring the security and uninterrupted operation of your origin server and business.

<span id="network-layer-and-transport-layer-ddos-protection"></span>
### Network layer and transport layer DDoS protection

By leveraging CDN to distribute your web content, your origin server gains an additional layer of protection as it is shielded behind the CDN infrastructure and safeguarded from direct attacks.

Nevertheless, attackers may still attempt to target either your domain or CDN's service IP addresses associated with your domain. If large\-scale DDoS attacks are launched on some of these IP addresses, the affected IP addresses may be disabled temporarily, leading to service disruptions. As a consequence, your business continuity may be impacted.

CDN provides different levels of protection against DDoS attacks at the network and transport layers:


* Standard DDoS Protection: Utilizes a self\-built DDoS protection system integrated into CDN edge nodes to mitigate DDoS attacks. Standard DDoS Protection provides basic DDoS protection capabilities and can defend against common\-scale DDoS attacks.

* Advanced DDoS Protection: Leverages globally distributed, high\-capacity scrubbing centers to mitigate DDoS attacks. Advanced DDoS Protection provides higher DDoS protection capabilities and can defend against large\-scale DDoS attacks. Advanced DDoS Protection is recommended when Standard DDoS Protection cannot provide sufficient protection against large\-scale or complex DDoS attacks for your business.


For more information about these services, see [Comparison between Standard DDoS Protection and Advanced DDoS Protection](https://docs.byteplus.com/en/docs/byteplus-cdn/DDoS_protection_levels#comparison-between-standard-ddos-protection-and-advanced-ddos-protection).

<span id="application-layer-ddos-protection"></span>
### Application layer DDoS protection

Application layer DDoS attacks targeting domains have two key characteristics:


* The attack traffic is often difficult to distinguish from legitimate client traffic.

* As a result, the attack traffic may reach an origin server, posing a serious threat to origin security and potentially leading to high CDN bills.


To mitigate the threat, CDN offers the WAF feature with capabilities of application layer DDoS protection. WAF supports both preset and custom protection policies to identify and filter out attack traffic. For detailed information about WAF, see [WAF protection](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-web-application-firewall-waf-).
