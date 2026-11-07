---
title: "Route configuration planning"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Route-tables-02"
---

When designing to use a Transit Router (TR) for forwarding cloud and on\-premises traffic, plan route configuration for the TR based on your scenario. This upfront planning is critical for an efficient and successful implementation.

<span id=".6KeE5YiS5Y6f5YiZ"></span>
## Planning principles

<span id=".6Lev55Sx6KGo5pWw6YeP6KeE5YiS"></span>
### Number of route tables

Each TR instance supports up to 20 TR route tables (including the TR system route table). The number of TR route tables you need depends on your specific networking scenario and its interconnectivity requirements. We recommend using the following principles to determine the minimum number needed.


* When using a TR to achieve full connectivity between cloud and on\-premises networks, only one TR route table is required per TR instance.

* When using a TR to achieve partial connectivity with isolation between certain networks, we recommend following the principles below to plan the number of route tables:

   In a single TR instance, multiple network instances with the identical access destination can share the same TR route table, while multiple network instances with different destinations must use separate TR route tables.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For inter\-region peering attachments, the TR instance on each end forwards traffic according to the TR route table associated with the attachment in its respective region.   </div>
   

<span id=".6Lev55Sx5p2h55uu6KeE5YiS"></span>
### Route entry planning

A TR forwards access traffic from network instances based on the route entries in the TR route table.

To forward cloud network traffic via a TR: Configure a route entry in the VPC route table with its next hop set to the TR to direct cloud traffic to the TR. Ensure a route is propagated into the TR route table to forward traffic to the destination network. Plan route entries in each TR route table as needed, and select the appropriate method to generate routes for the TR route table.

For details of route generation methods, see [List of routing capabilities](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-01#.6Lev55Sx6IO95Yqb).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When both route learning and static routing are supported, we recommend using route learning to generate routes for the TR route table, as this configuration is more convenient and faster.</div>


> In the table, a checkmark (✓) denotes supported, and **a cross (×)**  denotes not supported.



|TR resources ||Route propagation |Static routes |
|---|---|---|---|
|Network instance attachment |VPC |✓ |✓ |
||VPN | **×**  |✓ |
||DC Gateway |✓ |✓ |
|Inter\-region attachment ||✓ |✓ |


<span id=".6KeE5YiS56S65L6L"></span>
## Planning examples

These examples demonstrate route configuration planning for interconnecting Virtual Private Clouds (VPCs) via a TR, covering both intra\-region and inter\-region scenarios.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cc20190a20f76919e7710ad31069caf7.png) </span>

<span id=".5ZCM5Zyw5Z-f5Zy65pmv6Lev55Sx6KeE5YiS"></span>
### Route configuration planning for intra\-region scenarios

In the same region and account scenario, the specific route configuration for this example network setup is as follows:


* **Plan the number of TR route tables**: Since each VPC has a unique set of access destinations, each network instance attachment requires a separate route table for association forwarding. Therefore, 4 TR route tables are needed.

* **Plan the routes and configuration methods in TR route tables**: Each TR route table must contain a route with its destination set to the CIDR block of the target VPC and its next hop set to the corresponding network instance attachment. Since the TR supports learning routes from VPC attachments within the same region, route learning is selected to generate routes.

* **Plan the routes and configuration methods in VPC route tables**: Each VPC route table must contain a route with its destination set to the CIDR block of the target VPC and its next hop set to the TR.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1d303811614b5adf368920bb9fdd3f54.png) </span>

<span id=".6Leo5Zyw5Z-f5Zy65pmv6Lev55Sx6KeE5YiS"></span>
### Route configuration planning for inter\-region scenarios

In the inter\-region same\-account scenario, the specific route configuration for this example network setup is as follows:


* **Plan the number of TR route tables**: 6 TR route tables are needed for this networking scenario.

   Due to three distinct access destinations in Region A, three separate TR route tables are required:

   * vpc\-01 accesses vpc\-02 via tr\-01

   * vpc\-03 accesses vpc\-02 and vpc\-04 via tr\-01

   * Cross\-region traffic accesses vpc\-01 and vpc\-03 via tr\-01

   Similarly, Region B also requires three TR route tables to forward access traffic.

* **Plan the routes and configuration methods in TR route tables**:

   * Each route table associated with a network instance attachment must contain a route with its destination set to the CIDR block of the target VPC and its next hop set to the attachment. TR route tables support route learning for inter\-region attachments, so route learning is used to generate routes.

   * TR route tables on both ends of the inter\-region attachment must contain a route with its destination set to the CIDR block of the target VPC and its next hop set to the network instance attachment. TR route tables support route learning for intra\-region attachments, so route learning is used to generate routes.

* **Plan the routes in VPC route tables**: Each VPC route table must contain a route with its destination set to the CIDR block of the target VPC and its next hop set to the TR.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_712efe5169d563a6e2ed28f88a382916.png) </span>
