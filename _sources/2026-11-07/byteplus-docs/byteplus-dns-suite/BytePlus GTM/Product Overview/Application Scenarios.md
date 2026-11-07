---
title: "Application Scenarios"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/ibFPum"
---

This document introduces the common usage scenarios of BytePlus Global Traffic Management (GTM).

<span id="788ff481"></span>
## **Traffic distribution and failover during migration over cloud services**

During the process of migrating your business from one public cloud to another, you need to conduct A/B testing and grey release. A/B testing and grey release require control over the traffic distribution ratio during migration. Furthermore, when there's an IDC failure, business traffic needs to be switched to an available IDC to ensure business continuity.

BytePlus GTM can improve user access speed during the business migration process, assist in rational traffic distribution, and perform timely disaster recovery switching through health checks.

<span id="e6248659"></span>
## Geo\-based routing, load balancing and failover

<span id="Geo-based routing"></span>
### Geo\-based routing

The network quality worldwide (excluding Chinese mainland) has the following characteristics:


* The network quality for users accessing IP addresses within the same continent is better than accessing IP addresses across different continents.

* The network quality for users accessing IP addresses within the same country or region is better than accessing IP addresses across different countries or regions.


The network quality within Chinese mainland has the following characteristics:


* The network quality when users access IP addresses within the same ISP is better than that when accessing IPs across different ISPs.

* The network quality when users access IPs within the same province is better than that when accessing IPs across provinces.

* The network quality when users access IPs across the same ISP but in different provinces is better than that when accessing IPs across different ISPs within the same province.


Therefore, you need to route user traffic to the nearest IDC based on their geographical location. At the same time, it's necessary to prevent user traffic from crossing ISPs to access the IDC.

<span id="Load Balancing"></span>
### Load balancing

The incoming traffic of an IDC is limited by the following factors:


* Bandwidth of various ISPs and BGP

* Parameters of the load balancer such as QPS and the maximum number of concurrent connections


Based on these factors, the capacity of an IDC and the corresponding water level response can be defined as a numerical value. For example, the capacity of an IDC can be set at 1000, corresponding to the QPS or the maximum number of connections of a load balancer. The capacities of different IDCs can then serve as weights for load balancing.

<span id="Failover"></span>
### Failover

Traffic should be switched in the following failover scenarios:


* Single address failure: redirect the traffic of the failed address to other addresses in the same IDC and ISP.

* Single ISP failure in an IDC: redirect the traffic of the failed ISP to addresses of the same ISP in other IDCs.

* Total failure of an IDC: redirect all traffic of the failed IDC to the addresses of the same ISP in other IDCs.
