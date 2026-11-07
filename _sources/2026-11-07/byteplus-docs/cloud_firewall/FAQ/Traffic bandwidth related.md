---
title: "Traffic bandwidth related"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Bandwidth-related-FAQs"
---

<span id="bef0a118"></span>
### How is the traffic bandwidth protected by the cloud firewall defined? The bandwidth of the cloud firewall is independent of the bandwidth of other network products, so the bandwidth of the cloud firewall needs to be purchased separately.


* **Year and month**

   * Internet boundary firewall: Peak outbound bandwidth or peak inbound bandwidth for all region EIPs.

   * VPC boundary firewall: Peak outbound bandwidth + inbound bandwidth of VPC boundary firewall.

   * NAT boundary firewall: Peak outbound bandwidth + inbound bandwidth of NAT boundary firewall.

* **Pay on demand**

   * Internet boundary firewall: Peak outbound + inbound bandwidth for all region EIPs.

   * VPC boundary firewall: Peak outbound bandwidth + inbound bandwidth of VPC boundary firewall.

   * NAT boundary firewall: NAT boundary firewall outbound traffic + inbound traffic peak bandwidth.


<span id="业务流量超出云防火墙支持的带宽规格怎么办？"></span>
### What should I do if the traffic exceeds the bandwidth specifications supported by the cloud firewall? 

When the business traffic exceeds the protective bandwidth specifications of the internet boundary firewall, the cloud firewall cannot guarantee the security effectiveness, which may cause network throttling and packet loss. If you need larger traffic processing bandwidth, please scale up in a timely manner.

<span id="bbf343c1"></span>
### Is the purchased VPC/NAT boundary traffic processing capacity supported by each firewall instance or shared among firewall instances? 

The VPC/NAT boundary traffic processing capacity you purchased will be shared by all added VPC/NAT firewall instances. For example, if you selected 500 Mbps VPC boundary traffic processing capacity when purchasing, and then added 3 VPC firewalls, these 3 VPC firewalls will share the 500 Mbps bandwidth, and you can customize the traffic allocation for different firewall instances.

<span id="3912a801"></span>
### How to handle receiving traffic limit alerts? 

When you receive any boundary (internet boundary, VPC boundary, or NAT boundary) traffic bandwidth limit alert, please follow these steps to handle it:


1. To confirm the actual traffic situation, visit the overview page of the cloud firewall console where you can view the detailed traffic trend chart of each boundary firewall:

   * Internet boundary: displays the specific traffic trends of each asset IP

   * VPC boundary: shows the traffic trends of each VPC under each VPC firewall

   * NAT boundary: presents the traffic trends of each NAT firewall

2. Evaluate the handling plan; if you find that the actual business traffic has exceeded the current purchased protection traffic peak, network throttling or packet loss may occur. It is recommended that you promptly expand the bandwidth capacity to ensure normal business operations.
