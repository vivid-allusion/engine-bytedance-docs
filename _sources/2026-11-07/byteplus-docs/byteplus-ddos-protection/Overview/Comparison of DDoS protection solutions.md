---
title: "Comparison of DDoS protection solutions"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/Comparison_of_DDoS_protection_solutions"
---

Based on different use cases, BytePlus DDoS Protection offers three distinct protection products: DDoS Basic Protection, DDoS Advanced Protection, and Cloud DDoS Protection, to meet various customer business needs and provide a diverse range of protection solutions.

<span id="ca01ca90"></span>
## DDoS Basic Protection

The DDoS basic service leverages the protection bandwidth of the native BytePlus network to provide free DDoS protection of up to 2 Gbps for public network resources such as cloud servers and load balancers on BytePlus. It offers real\-time attack monitoring and response within seconds, meeting the requirements of daily security operations.

<span id="ea564f72"></span>
## Advanced DDoS Protection

DDoS advanced protection is a paid service launched to address situations where public network resources of internet businesses experience large\-scale DDoS attacks, resulting in user service unavailability. After enabling anti\-DDoS protection, users can configure their service DNS to resolve to the anti\-DDoS IP address, redirecting public network traffic to the scrubbing center. The scrubbing center filters and blocks attack traffic, then forwards clean service traffic to the origin server to ensure stable and reliable service.

<span id="afd70774"></span>
## Cloud DDoS Protection

Cloud DDoS Protection is based on a cloud\-native network and provides BytePlus cloud users with the highest terabit\-level DDoS protection. Users do not need to change their business structure or modify proxy configurations, and can directly enable protection for cloud\-based public IPs (EIPs). The product's native multidimensional defense algorithms and efficient scrubbing systems can mitigate the business impact of DDoS attacks, ensuring normal operation without requiring changes to the business architecture.

<span id="786fdf69"></span>
## Comparison


|**Item** |**DDoS Basic Protection** |**Advanced DDoS Protection** |**Cloud DDoS Protection** |
|---|---|---|---|
|Description |Protection for a BytePlus EIP automatically takes effect without needing to change the IP address. |By configuring DNS or an anti\-DDoS IP, traffic is redirected to the BytePlus anti\-DDoS data center, and the change takes effect immediately. |Based on cloud\-native networking capabilities, full protection capability takes effect for BytePlus cloud EIP (when the security protection type is set to **default** during EIP instance creation), without the need to change the IP address. |
|Purchasing |Free to use |Flexible billing is available. The "Minimum Guarantee plus Elastic Protection" model is supported, and the elastic protection portion is billed based on actual traffic. |Supports expanding the number of protected IP addresses and the scale of business operations while maintaining full protection. |
|Integration |Takes effect immediately. |Uses BGP protected routes to reduce cross\-network access latency. |Takes effect in real time. |
|Change IP addresses |No |Is |No |
|Maximum protection capabilities |No more than 2 Gbps; upgrades are not supported. |Provides terabit\-level BGP protection for a single customer. |Provides comprehensive protection that can be shared by multiple EIPs within an instance. |
|Types of attacks |* Malformed packet attacks, such as Land, Winnuke, Smurf, Fraggle, malformed fragmented packets, TCP packets that do not comply with protocol specifications, UDP packets with empty payloads, and many others.<br><br>* Resource exhaustion attacks, such as ACK Flood, SYN Flood, and similar attacks.<br><br>* Common volumetric attacks, such as UDP Flood and many others.<br><br>* Reflection and amplification\-based high\-volume bandwidth attacks, such as DNS reflection and more. |* Malformed packet attacks, such as Land, Winnuke, Smurf, Fraggle, malformed fragmented packets, TCP packets that do not conform to protocol specifications, UDP packets with empty payloads, and many others.<br><br>* Common volumetric attacks, such as ICMP Flood, UDP Flood, and many others.<br><br>* Reflection amplification attacks, such as DNS reflection and others.<br><br>* Resource consumption attacks, such as ACK Flood, SYN Flood, and so on.<br><br>* Application resource attacks, such as CC attacks. |* Malformed packet attacks, such as Land, Winnuke, Smurf, Fraggle, malformed fragmented packets, TCP packets that do not comply with protocol specifications, UDP packets with empty payloads, and more.<br><br>* Common traffic bandwidth attacks, such as UDP Flood, ICMP Flood, IGMP Flood, and more.<br><br>* Large\-scale reflection\-based bandwidth attacks, such as DNS reflection, NTP reflection, SNMP reflection, and more.<br><br>* Resource consumption attacks, such as SYN Flood and more. |
|Use cases |* The business is deployed in the BytePlus cloud environment.<br><br>* Scenarios with low traffic that require high service availability but have a low likelihood of being attacked. |* The business is deployed in a multi\-cloud environment or outside the BytePlus cloud.<br><br>* Use cases that require protection against high\-volume attacks, need urgent recovery after an attack, or must hide the origin server. |* The business is deployed in the BytePlus cloud environment.<br><br>* Requires high service performance without changes to the business architecture, and can defend against small and medium\-sized traffic attacks. |
