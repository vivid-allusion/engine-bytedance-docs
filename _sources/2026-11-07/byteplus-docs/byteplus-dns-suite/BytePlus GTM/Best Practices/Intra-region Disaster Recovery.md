---
title: "Intra-region Disaster Recovery"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/5qftVh"
---

This document introduces the intra\-region disaster recovery solution based on BytePlus GTM.

<span id="overview"></span>
## Overview

The distance between IDCs in the same region is relatively short, and the impact of traffic switching on user network latency is minimal. Therefore, disaster recovery can be achieved through DNS\-based traffic switching between IDCs. This is known as intra\-region disaster recovery. For example:


* Disaster recovery between multiple AZs within the same region in public cloud services;

* Disaster recovery through traffic switching between multiple geographically adjacent on\-premise IDCs.


Assume your service is deployed in multiple AZs within a region of a public cloud service. When a service failure occurs in one AZ, you can perform automatic or manual failover according to the disaster recovery plan, switching user traffic to other AZs to ensure uninterrupted service or quick recovery.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f89ca724737dcc6fd38191e3590b359c.jpeg) </span>

BytePlus GTM supports health checks, failover, proximity access, load balancing, and other functions. BytePlus GTM can achieve various DNS\-based intra\-region disaster recovery modes with low cost, convenient deployment, and non\-intrusive methods to ensure uninterrupted service or quick recovery during failures. You can achieve the following intra\-region disaster recovery modes through BytePlus GTM:


* Cold standby mode

* Hot standby mode

* Active\-active mode


<span id="cold-standby-mode"></span>
## Cold standby mode

Two AZs in the same region adopt a primary\-backup mode, where the primary AZ handles normal traffic, and the backup AZ does not handle traffic. When the primary AZ fails, traffic switches to the backup AZ.

This mode is simple to deploy but has the following disadvantages:


* Resource waste under normal conditions.

* Since there is no traffic under normal conditions, it is impossible to know whether the backup AZ is ready in case of a primary failure (including backend configuration, capacity, and system status).

* Attention is needed for the capacity of the backup AZ.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0004a33eb7679ef7638a5cfbb35d62bc.jpeg) </span>

<span id="steps"></span>
### Steps

Follow the steps below to implement the cold standby mode shown in the figure above in BytePlus GTM.


1. [Create a GTM instance](https://docs.byteplus.com/docs/byteplus-dns-suite/k_FIn3).

2. [Configure the GTM instance you created](https://docs.byteplus.com/docs/byteplus-dns-suite/5qftVh). You need to:

   * Select basic routing

   * Enable health checks

   * [Create two pools](https://docs.byteplus.com/docs/byteplus-dns-suite/RmUweJ). The addresses included in each pool are as follows:

      
      |Pool |Address |
      |---|---|
      |Region A \- 1 |203.0.113.1<br><br>203.0.113.2 |
      |Region A \- 2 |203.0.113.3<br><br>203.0.113.4 |
      

   * [Create a rule](https://docs.byteplus.com/docs/byteplus-dns-suite/snlUdP). Create two pool sets in the rule, where:

      * Pool set A includes the **Region A \- 1** pool.

      * Pool set B includes the **Region A \- 2** pool.

      * Ensure that the priority of pool set A is higher than that of pool set B, i.e., A is ordered before B.

3. [Start the GTM instance](https://docs.byteplus.com/docs/byteplus-dns-suite/U5nvpy). When the GTM instance is running, you have implemented the cold standby mode.


<span id="hot-standby-mode"></span>
## Hot standby mode

Two AZs in the same region adopt a primary\-backup mode. The primary AZ handles the main traffic, while the backup AZ handles secondary traffic to verify the availability of most functions of the backup AZ.

The hot standby mode solves the problem of not being able to determine whether the backup AZ is ready in case of a primary AZ failure, but it still cannot solve the problem of resource waste under normal conditions. Additionally, the backup AZ may also face capacity issues during failover.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_62c994634f1cb5a6b87c0202f90b8fe8.jpeg) </span>

<span id="steps"></span>
### Steps

Follow the steps below to implement the hot standby mode shown in the figure above in BytePlus GTM.


1. [Create a GTM instance](https://docs.byteplus.com/docs/byteplus-dns-suite/k_FIn3).

2. [Configure the GTM instance you created](https://docs.byteplus.com/docs/byteplus-dns-suite/5qftVh). You need to:

   * Select basic routing

   * Enable load balancing and health checks

   * [Create two pools](https://docs.byteplus.com/docs/byteplus-dns-suite/RmUweJ). The addresses included in each pool are as follows:

      
      |Pool |Address |
      |---|---|
      |Region A \- 1 |203.0.113.1<br><br>203.0.113.2 |
      |Region A \- 2 |203.0.113.3<br><br>203.0.113.4 |
      

   * [Create a rule](https://docs.byteplus.com/docs/byteplus-dns-suite/snlUdP). Add an pool set in the rule, including the **Region A \- 1** and **Region A \- 2** pools. The total weight of all addresses in **Region A \- 1** is 90; the total weight of all addresses in **Region A \- 2** is 10.

3. [Start the GTM instance](https://docs.byteplus.com/docs/byteplus-dns-suite/U5nvpy). When the GTM instance is running, you have implemented the hot standby mode.


<span id="active-active-mode"></span>
## Active\-active mode

Two AZs in the same region work simultaneously. When one AZ fails, traffic switches to the non\-failing AZ. Since multiple AZs work simultaneously under normal conditions, there is no issue of whether the backup AZ is ready. You only need to pay attention to the remaining capacity of the AZ to which the traffic is switched.

There can also be more than two AZs within a region, reducing the remaining capacity that each AZ needs to reserve. However, multiple AZs also increase the burden of data and configuration synchronization.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5d7b920aa59a37e3c6c7eada090a2a64.jpeg) </span>

Under normal conditions, the IDCs in Region A \- 1 and Region A \- 2 are in active\-active mode. The IDCs in Region A \- 1 and Region A \- 2 each handle 50% of the traffic. Additionally, this solution includes the following plans:


* **Switch to pool set B**: When the IDC in Region A \- 2 fails, all traffic from the Region A \- 2 IDC switches to the Region A \- 1 IDC.

* **Switch to pool set C**: When the IDC in Region A \- 1 fails, all traffic from the Region A \- 1 IDC switches to the Region A \- 2 IDC.


<span id="steps"></span>
### Steps

Follow the steps below to implement the active\-active mode shown in the figure above in BytePlus GTM.


1. [Create a GTM instance](https://docs.byteplus.com/docs/byteplus-dns-suite/k_FIn3).

2. [Configure the GTM instance you created](https://docs.byteplus.com/docs/byteplus-dns-suite/5qftVh). You need to:

   * [Create two pools](https://docs.byteplus.com/docs/byteplus-dns-suite/RmUweJ). The addresses included in each pool are as follows:

      
      |Pool |Address |
      |---|---|
      |Region A \- 1 |203.0.113.1<br><br>203.0.113.2 |
      |Region A \- 2 |203.0.113.3<br><br>203.0.113.4 |
      

   * [Create a rule](https://docs.byteplus.com/docs/byteplus-dns-suite/snlUdP). Create three pool sets in the rule, where:

      * Pool set A includes the **Region A \- 1** and **Region A \- 2** pools. The total weight of all addresses in **Region A \- 1** is 50; the total weight of all addresses in **Region A \- 2** is 50. Pool set A has the highest priority.

      * Pool set B includes the **Region A \- 1** pool.

      * Pool set C includes the **Region A \- 2** pool.

3. [Start the GTM instance](https://docs.byteplus.com/docs/byteplus-dns-suite/U5nvpy). When the GTM instance is running, you have implemented the active\-active mode.
