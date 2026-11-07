---
title: "DDoS protection levels"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DDoS_protection_levels"
---

BytePlus CDN offers varying levels of DDoS protection based on the value\-added services or subscription plans you use.

Value\-added services include CDN Advanced DDoS Protection and WAF Protection. Subscription plans include CDN\-Security\-Plan Standard Edition and CDN\-Security\-Plan Advanced Edition.

<span id="45f02e26"></span>
## Network layer and transport layer DDoS protection


|**Service Type** |**Protection Capability** |**Applicable to** |
|---|---|---|
|CDN Native Protection |* Minimum protection capability: Not guaranteed<br><br>* Maximum protection capability: 10 Gbps (adjusted based on platform capacity) |All users |
|CDN Standard DDoS Protection |* Minimum protection capability: 50 Gbps<br><br>* Maximum protection capability: Adjusted based on platform capacity |* Users who subscribe to CDN\-Security\-Plan Standard Edition<br><br>* Users who separately apply for CDN Standard DDoS Protection |
|CDN Advanced DDoS Protection |* Minimum protection capability: 100 Gbps<br><br>* Maximum protection capability: Tbps\-level (best effort) |* Users who subscribe to CDN\-Security\-Plan Advanced Edition<br><br>* Users who separately purchase CDN Advanced DDoS Protection |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Concepts:</strong></div>



* <div data-tips="true" data-tips-type="tip">Protection capability (measured by bandwidth): The maximum inbound anomalous traffic that the CDN platform can handle in a single attack event. Anomalous traffic targeting all domain names under your account is included in this calculation.</div>


* <div data-tips="true" data-tips-type="tip">Minimum protection capability: The stable protection capability provided by the CDN platform.</div>


* <div data-tips="true" data-tips-type="tip">Maximum protection capability: The highest protection capability that the CDN platform can achieve through dynamic scheduling. <strong>It is a reference value.</strong></div>



<div data-tips="true" data-tips-type="tip"><strong>Notes:</strong></div>



* <div data-tips="true" data-tips-type="tip">When using CDN Advanced DDoS Protection, ensure that the protection feature has been enabled for relevant domain names. For related operations, see <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/Manage_protected_domains#add-domains">Add domain names to an Advanced DDoS Protection instance</a>.</div>


* <div data-tips="true" data-tips-type="tip">If attack traffic exceeds the CDN platform's capacity and threatens its stability, protective measures including blackholing, domain name removal from CDN, and service suspension will be triggered. This potentially interrupts your business. To minimize disruptions, we recommend the following:</div>


   * <div data-tips="true" data-tips-type="tip">Subscribe to value\-added services in advance to upgrade your security protection.</div>


   * <div data-tips="true" data-tips-type="tip">After the attack subsides, <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000735">submit a ticket</a> to have restrictions lifted.</div>



<span id="d8f9a0fe"></span>
## **Application layer DDoS protection**


|**Service Type** |**Protection Capability** |**Applicable to** |
|---|---|---|
|CDN Native Protection |* Minimum protection capability: Not guaranteed<br><br>* Maximum protection capability: 100,000 QPS (adjusted based on platform capacity) |All users |
|Application Layer DDoS Protection with Edge WAF |* Minimum protection capability: 500,000 QPS<br><br>* Maximum protection capability: 3,000,000 QPS (adjusted based on platform capacity) |* Users who subscribe to BytePlus Edge WAF<br><br>* Users who subscribe to CDN\-Security\-Plan Standard Edition<br><br>* Users who subscribe to CDN\-Security\-Plan Advanced Edition |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Concepts:</strong></div>



* <div data-tips="true" data-tips-type="tip">Protection capability (measured by QPS): The total number of anomalous requests that the CDN platform can handle in a single attack event. Anomalous requests for all domain names under your account will be included in the calculation.</div>


* <div data-tips="true" data-tips-type="tip">Minimum protection capability: The stable protection capability provided by the CDN platform.</div>


* <div data-tips="true" data-tips-type="tip">Maximum protection capability: The highest protection capability that the CDN platform can achieve through dynamic scheduling. <strong>It is a reference value.</strong></div>



<div data-tips="true" data-tips-type="tip"><strong>Notes:</strong></div>



* <div data-tips="true" data-tips-type="tip">When using Application Layer DDoS Protection with Edge WAF, ensure that the protection feature has been enabled for relevant domain names and that security policies are configured as needed. For related operations, see <a href="https://docs.byteplus.com/en/docs/waf/Adding_a_CDN_domain_name_to_a_WAF_instance">Add a CDN domain name to a WAF instance</a> and <a href="https://docs.byteplus.com/en/docs/waf/docs-configuring-rate-limit-policies">Configure rate limiting policies</a>.</div>


* <div data-tips="true" data-tips-type="tip">If attack traffic exceeds the CDN platform's capacity and threatens its stability, protective measures such as sandboxing, forced rate limiting, domain name removal from CDN, and service suspension will be triggered. This potentially interrupts your business. To minimize disruptions, we recommend the following:</div>


   * <div data-tips="true" data-tips-type="tip">Subscribe to value\-added services in advance to upgrade your security protection.</div>


   * <div data-tips="true" data-tips-type="tip">After the attack subsides, <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000735">submit a ticket</a> to have restrictions lifted.</div>



<span id="c12ea1bc"></span>
## More information

<span id="ec4bf4b4"></span>
### Comparison between Standard DDoS Protection and Advanced DDoS Protection

CDN offers Standard DDoS Protection and Advanced DDoS Protection to mitigate network layer and transport layer DDoS attacks. Compared to Standard DDoS Protection, Advanced DDoS Protection provides higher DDoS protection capabilities.

The following table lists the specific differences between Standard DDoS Protection and Advanced DDoS Protection.


| |**Standard DDoS Protection** |**Advanced DDoS Protection** |
|---|---|---|
|**Service scope** |* Applicable to : Users who subscribe to CDN\-Security\-Plan Standard Edition or separately apply for CDN Standard DDoS Protection.<br><br>* Service region : Global (excluding Chinese Mainland) |* Applicable to : Users who subscribe to CDN\-Security\-Plan Advanced Edition or subscribe to CDN Advanced DDoS Protection.<br><br>* Service region : Global (excluding Chinese Mainland) |
|**Subscription and pricing** |If you subscribe to CDN\-Security\-Plan Standard Edition or separately apply for CDN Standard DDoS Protection, Standard DDoS Protection will be automatically enabled for your domain name after it is added to CDN. No additional configuration or payment is required. |* Subscribe to CDN\-Security\-Plan Advanced Edition<br><br>   The system will automatically create an Advanced DDoS Protection instance. You do not need to pay separately for Advanced DDoS Protection.<br><br>* Separately purchase Advanced DDoS Protection<br><br>   You need to create an Advanced DDoS Protection instance and pay for its usage. The cost of Advanced DDoS Protection includes:<br><br>   * Instance fees (prepaid)<br><br>   * Fees for secure traffic (postpaid)<br><br>   * Fees for domain names exceeding the default quota of 50 (prepaid)<br><br>      Fees for secure traffic are calculated based on the amount of data transmitted from CDN to clients. For more information, see [Pricing details](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-pricing). |
|**Technical implementation** |Standard DDoS Protection is implemented based on the self\-built DDoS protection system that is integrated into CDN's distributed nodes. This system uses protection plugins based on eXpress Data Path (XDP) technology, capable of handling high\-concurrency traffic. |CDN utilizes a global network of high\-capacity scrubbing centers to intercept and filter out DDoS attack traffic before it reaches your origin server.<br><br>When a DDoS attack occurs, attack traffic is dispersed to scrubbing centers via Anycast IP. Dedicated DDoS scrubbing engines intercept and filter the traffic. Then, only legitimate traffic is forwarded to CDN and your origin server. |
|**Protection capability** |Standard DDoS Protection provides the following protection capabilities:<br><br><br>* Defends against common\-scale DDoS attacks at network and transport layers. |Advanced DDoS Protection provides the following protection capabilities:<br><br><br>* Defends against large\-scale DDoS attacks at network and transport layers.<br><br>* Provides Terabit\-level protection bandwidth.<br><br>* Offers an exclusive IP address dedicated to DDoS protection.<br><br>* Protects a maximum of 50 domains per instance by default. If more domains need to be protected, you can pay extra to increase the domain quota. |
|**Protection scope** |Standard DDoS Protection can protect against common attacks, including SYN Flood, ACK Flood, RST Flood, Empty Connection, TCP Malformed Packet, and LAND attacks. |Advanced DDoS Protection can protect against common attacks, including SYN Flood, ACK Flood, RST Flood, RST/FIN Flood, SYN\-ACK Flood, UDP Flood, UDP Fragmentation Flood, UDP Reflection, ICMP Fragmentation Flood, ICMP Flood, Ping of Death, Smurf, Teardrop, IP Options, and LAND attacks. |
|**Monitoring and alerting** |Standard DDoS Protection does not support attack monitoring and alerting features. For suspected service restrictions due to large\-scale attacks, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000735) for assistance. |Advanced DDoS Protection supports attack monitoring and alerting features. You can view real\-time monitoring data of your Advanced DDoS Protection instance on the dashboard page. When attack traffic reaches the threshold, the platform will send you alert notifications. For more information, see [View monitoring data](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-viewing-ddos-attack-protection-information). |


<span id="ab639ead"></span>
### Considerations when using Advanced DDoS Protection

When using Advanced DDoS Protection, pay attention to the following points:


* IPv6

   After enabling Advanced DDoS Protection for a domain, you do not need to modify the DNS resolution configuration for the domain. However, DNS will stop resolving the domain name to an IPv6 address even if you have enabled IPv6 in your CDN policy. All traffic is directed to the IPv4 address dedicated to DDoS protection.

* Performance impact

   Enabling Advanced DDoS Protection may introduce additional latency in domain access. The extent of this latency depends on client locations and network environment.

* Service region

   * DDoS protection is not available for Chinese Mainland.

      * For domains with "Global" acceleration:

         * Scrubbing centers are only available outside Chinese Mainland.

         * Only traffic from non\-Chinese Mainland areas passes through these scrubbing centers.

      * For domains with "Chinese Mainland" acceleration:

         * DDoS protection cannot be enabled.

   * After you enable Advanced DDoS Protection for a domain, the acceleration region for the domain cannot be modified.
