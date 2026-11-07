---
title: "Tutorial Overview"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/S1LBKo"
---

This tutorial introduces how to use BytePlus GTM to route user traffic according to your business scenario.

BytePlus GTM supports basic routing policies and intelligent routing policies. Different policies have different applicable scenarios and steps.


* **Basic routing**: Traffic routing policy based on geolocation and weight. Both the standard edition and the ultimate edition support basic routing policies. When a user sends a DNS query to a recursive DNS server, BytePlus GTM will return the address that matches the user's ISP and is closest to the user's geolocation. If you want user requests to be allocated proportionally based on the capacity of the pool or address, you can enable load balancing for the basic routing policy.

* **Intelligent routing**: Traffic routing policy based on latency, capacity, and load feedback. Only the ultimate edition supports intelligent routing policy. You can set the intelligent routing policy to any of the following routing modes. Unlike basic routing, in the intelligent routing policy, you do not need to manually add routing rules based on ISPs and geolocations. BytePlus GTM will automatically generate routing rules based on your traffic targets and routing modes.

   * **Performance**: When a user sends a DNS query to a recursive DNS server, BytePlus GTM will return the address with the lowest access latency. You cannot set capacity limits for addresses based on traffic capacity, so it is recommended to choose performance when the traffic capacity of all data centers is sufficient. If you want user requests to be distributed proportionally based on the traffic capacity of the addresses, you can choose capacity or load feedback mode.

   * **Capacity**: When a user sends a DNS query to a recursive DNS server, BytePlus GTM will return the address with the lowest access latency, subject to the capacity limit of the address. If you want user requests to be distributed proportionally based on the traffic capacity of the addresses, you can choose capacity mode.


<span id="example-business-scenario-one"></span>
## Example business scenario A

Your website domain name is `www.example.com`, and the DNS service provider is BytePlus DNS. The website servers are deployed in multiple data centers. The geolocations and access point IP addresses of these data centers are shown in the following table.


|**Data center geolocation** |**Data center IP address** ||ISP |
|---|---|---|---|
|Shanghai |`203.0.113.1` |`203.0.113.2` |China Telecom |
|Zhejiang |`203.0.113.3` |`203.0.113.4` |China Mobile |
|Beijing |`203.0.113.5` |`203.0.113.6` |BGP |


The traffic capacity of the data centers is as follows:


* The traffic capacity of the data centers with IP addresses `203.0.113.1`, `203.0.113.2`, `203.0.113.3`, `203.0.113.4`, and `203.0.113.6` are the same.

* The traffic capacity of the IDC with IP address `203.0.113.5` is twice that of the IDC with IP address `203.0.113.6`.


Your business requirements are as follows:


* User requests from the China Telecom / Shanghai are all allocated to the Shanghai IDC.

* User requests from the China Mobile / Zhejiang are all allocated to the Zhejiang IDC.

* User requests from other ISPs and geolocations are all allocated to the Beijing IDC.

* User requests are allocated to different data centers in proportion to their traffic capacity.


<span id="using-basic-routing-to-implement-example-business-scenario-one"></span>
### Use basic routing to implement example business scenario A

This tutorial uses basic routing to implement example business scenario A. You will complete the following tasks:


1. [Create a GTM instance](https://docs.byteplus.com/docs/byteplus-dns-suite/A5PoZE).

2. [Configure the GTM Instance (Basic Routing)](https://docs.byteplus.com/docs/byteplus-dns-suite/ItJU_b)

3. [Validate traffic](https://docs.byteplus.com/docs/byteplus-dns-suite/RWiva6).


<span id="example-business-scenario-two"></span>
## Example business scenario B

Your website domain name is `www.example.com`, and the DNS service provider is BytePlus DNS. The website servers are deployed in multiple data centers. The geolocations and access point IP addresses of these data centers are shown in the following table. The capacity of all data centers is sufficient.


|Data center geolocation |Data center IP address ||ISP |
|---|---|---|---|
|Shanghai |`203.0.113.1` |`203.0.113.2` |China Telecom |
|Zhejiang |`203.0.113.3` |`203.0.113.4` |China Mobile |
|Beijing |`203.0.113.5` |`203.0.113.6` |BGP |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The IP addresses in the documentation are for example purposes only and do not represent real IP addresses.</div>


Your business requirement is to reduce the latency for users accessing your website as much as possible.

<span id="using-the-performance-priority-mode-of-intelligent-routing-to-implement-example-business-scenario-two"></span>
### Use the performance mode of intelligent routing to implement example business scenario B

This tutorial uses the performance routing mode of intelligent routing to implement example business scenario two. You will complete the following tasks:


1. [Create a GTM instance](https://docs.byteplus.com/docs/byteplus-dns-suite/A5PoZE).

2. [Configure the GTM Instance (Intelligent Routing, Performance Mode)](https://docs.byteplus.com/docs/byteplus-dns-suite/FT4Bjd)

3. [Validate traffic](https://docs.byteplus.com/docs/byteplus-dns-suite/RWiva6).


<span id="example-business-scenario-three"></span>
## Example business scenario C

Your website domain name is `www.example.com`, and the DNS service provider is BytePlus DNS. The website servers are deployed in multiple data centers. The geolocations, access point IP addresses, and capacities of these data centers are shown in the following table.


|Data center geolocation |Data center IP address |ISP |Capacity |
|---|---|---|---|
|Shanghai |`203.0.113.1` |China Telecom |100 |
||`203.0.113.2` ||100 |
|Zhejiang |`203.0.113.3` |China Mobile |100 |
||`203.0.113.4` ||100 |
|Beijing |`203.0.113.5` |BGP |200 |
||`203.0.113.6` ||100 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Capacity is used to represent the IDC's traffic capacity, which can be set based on indicators such as bandwidth and concurrent connections. In this tutorial, capacity values are set for each IDC based on bandwidth.</div>


* <div data-tips="true" data-tips-type="tip">The IP addresses in the documentation are for example purposes only and do not represent real IP addresses.</div>



Your business requirement is to reduce the latency for users accessing your website as much as possible, while not exceeding the IDC capacity.

<span id="using-the-capacity-priority-mode-of-intelligent-routing-to-implement-example-business-scenario-three"></span>
### Use the capacity mode of intelligent routing to implement example business scenario C

This tutorial uses the capacity routing mode of intelligent routing to implement example business scenario three. You will complete the following tasks:


1. [Create a GTM instance](https://docs.byteplus.com/docs/byteplus-dns-suite/A5PoZE).

2. [Configure the GTM Instance (Intelligent Routing, Capacity Mode)](https://docs.byteplus.com/docs/byteplus-dns-suite/zHuTsr)

3. [Validate traffic](https://docs.byteplus.com/docs/byteplus-dns-suite/RWiva6).
