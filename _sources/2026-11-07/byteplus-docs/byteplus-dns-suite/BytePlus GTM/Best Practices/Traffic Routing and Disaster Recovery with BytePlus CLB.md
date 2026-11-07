---
title: "Traffic Routing and Disaster Recovery with BytePlus CLB"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/Traffic_Routing_and_Disaster_Recovery_with_BytePlus_CLB"
---

If your IDCs are distributed across multiple regions and your service require traffic distribution, high reliability, cross\-AZ disaster recovery, and so on, you can use [BytePlus Load Balancer (CLB)](https://www.byteplus.com/en/product/clb) to achieve traffic routing and disaster recovery across different regions.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5b7b4caf86bd789e493c6c257732104e.jpeg) </span>

<span id="traffic-routing"></span>
### Traffic routing

Users access ALB instances in each region based on geolocation. BytePlus GTM offers routing policies based on various factors such as geolocation, ISP, and latency.


* **Automatic traffic routing based on latency**: GTM instances can automatically return the server address with the lowest latency.

* **Load balancing**: GTM instances distribute traffic to different CLB instances based on their traffic capacity, assigning traffic to each CLB instance according to weight. CLB instances accept access traffic and forward requests to backend servers in multiple AZs within the same region, achieving balanced traffic routing.


<span id="disaster-recovery"></span>
### Disaster Recovery

BytePlus GTM combined with Load Balancer CLB can achieve disaster recovery both within the same region (intra\-city disaster recovery) and between regions (inter\-region disaster recovery).


* **Intra\-city disaster recovery**: CLB instances can perform health checks on backend servers. When the primary AZ fails due to network issues, access traffic can be distributed through the load balancer deployed in the backup AZ.

* **Inter\-region disaster recovery**: When a CLB instance in one region is unavailable, or all backend servers of the CLB instance are unavailable, BytePlus GTM automatically ignores the public IP address of the CLB instance, ensuring that traffic is routed to a CLB instance that is still providing services.


<span id="steps"></span>
## Steps

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9c2ff57a2b4745c10df1e589a86f9717.jpeg) </span>

The above scenario shows how GTM instances combined with CLB instances achieve cross\-region traffic routing and disaster recovery.


* Users access the GTM instance's routing domain, and the GTM instance resolves the user's DNS query to the public IP address of the CLB instance. You can set weights for the public IP addresses of different CLB instances based on their capacity.

* CLB instances forward traffic to backend servers in multiple AZs within the same region according to the load balancing algorithm.


You can refer to the following steps to achieve this scenario using BytePlus CLB and BytePlus GTM.

<span id="step-1-achieve-cross-az-load-balancing-and-disaster-recovery-based-on-clb-instances"></span>
### Step 1: Achieve cross\-AZ load balancing and disaster recovery based on CLB instances

Create the following two CLB instances in region A and region B respectively:


* Region A CLB instance: Load balancing and disaster recovery for backend servers in AZ1 and AZ2 in region A.

* Region B CLB instance: Load balancing and disaster recovery for backend servers in AZ1 and AZ2 in region B.


This document assumes that the traffic capacity ratio of backend servers in the region A CLB instance to the region B CLB instance is 4:1.

<span id="step-2-achieve-cross-region-traffic-routing-and-disaster-recovery-based-on-gtm-instances"></span>
### Step 2: Achieve cross\-region traffic routing and disaster recovery based on GTM instances

Create a GTM instance, and under the GTM instance, create a rule and a pool set. The pool set includes the following pools:


* Region A pool: The address is the public IP address of the region A CLB instance, with a weight of 80.

* Region B pool: The address is the public IP address of the region B CLB instance, with a weight of 20.


In this way, the GTM instance can perform cross\-region traffic routing and disaster recovery for the region A CLB instance and the region B CLB instance.
