---
title: "FAQ about Advanced DDoS protection"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-FAQ-BytePlus-Advanced-DDoS-protection"
---

This section details the frequently asked questions about BytePlus Advanced DDoS protection.

<span id="59906b1e"></span>
## What are the common types of attacks?


* Network layer attacks: These include, but are not limited to, malformed packet attacks, common bandwidth attacks, reflection/amplification attacks, and resource consumption attacks. These attacks aim to consume server bandwidth and connection resources, ultimately leading to a denial of service.

* Application layer attacks: These include DNS Flood attacks, HTTP Flood attacks, and CC attacks. These attacks intend to consume server resources to deny service.


<span id="ddd8e6c8"></span>
## Can the platform issue alerts for attacks?

The BytePlus Advanced DDoS Protection platform sends notifications via platform messages or email when events occur, such as a DDoS attack starting or ending, or your service being blackholed or unblackholed.

<span id="61953d14"></span>
## **What types of protocols are supported by BytePlus Advanced DDoS Protection**?


* Non\-website protection (port forwarding) supports TCP and UDP protocols.

* Website protection (for domain names) supports the HTTP, HTTPS, and WebSocket protocols. When you configure HTTP, WebSocket is also enabled. Similarly, enabling HTTPS also enables WebSocket.


<span id="a09cddf7"></span>
## How many ports and domains can be protected by **BytePlus Advanced DDoS Protection**?


* Each instance provides a quota of 50 ports and 50 domains, and this number can be expanded as needed. Every additional 5 ports or domains incurs additional costs.

* Up to 1000 ports or domains can be protected.


<span id="d8b2cfe7"></span>
## How many IP addresses can be added to the allowlist or blocklist?


* Up to 1000 IP addresses can be added to the allowlist.

* Up to 1000 IP addresses can be added to the blocklist.


<span id="63675dfa"></span>
## How is traffic distributed when a forwarding rule is associated with multiple origin servers?

The service uses IP hashing to load balance traffic among origin servers.

<span id="24d68f40"></span>
## What does full protection mean?

Full protection means that we provide the total protection capacity of all scrubbing centers. When a DDoS attack's magnitude exceeds a scrubbing center's bandwidth limit, incoming traffic to the protected service may be temporarily blocked to prevent the center from becoming unavailable.
