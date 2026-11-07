---
title: "Traffic Routing and Disaster Recovery with BytePlus ALB"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/Traffic_Routing_and_Disater_Recovery_with_BytePlus_ALB"
---

If your IDCs are distributed across multiple regions, and your service requires traffic distribution for application\-layer websites or audio/video applications, you can combine [BytePlus ALB](https://www.byteplus.com/en/product/alb) to achieve traffic routing and disaster recovery switching across different regions.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_840185e36e9c6e4299bce9d95cf7e72b.jpeg) </span>

<span id="traffic-routing"></span>
### Traffic routing

Users access ALB instances in each region based on geolocation. BytePlus GTM offers routing policies based on various factors such as geolocation, ISP, and latency.


* **Automatic traffic routing based on latency**: GTM instances can automatically return the server address with the lowest latency.

* **Load balancing**: GTM instances distribute traffic to different ALB instances according to their capacity. ALB instances accept incoming traffic and forward requests to backend servers across multiple AZs within the same region, achieving balanced traffic routing.


<span id="disaster-recovery"></span>
### Disaster recovery

The combination of BytePlus GTM and BytePlus ALB can simultaneously achieve disaster recovery across AZs within the same region (intra\-region disaster recovery) and aross regions (inter\-region disaster recovery).


* **Intra\-region disaster recovery**: ALB instances can perform health checks on backend servers. When a public IP in an AZ of an ALB instance becomes unavailable, that public IP and its backend servers are shielded, and the system redistributes incoming traffic to the remaining available servers according to the proportions set in the balancing algorithm.

* **Inter\-region disaster recovery**: When an ALB instance in a region becomes unavailable, or all backend servers of an ALB instance are unavailable, BytePlus GTM automatically shields the domain name of that ALB instance, ensuring that traffic is routed to ALB instances that are providing normal service.


<span id="steps"></span>
## Steps

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e366ed3d9a5ade541708d911baa46a43.jpeg) </span>

The above diagram shows a scenario where GTM instances and ALB instances are combined to achieve cross\-region traffic routing and disaster recovery switching.


* When users access the routing domain of a GTM instance, the GTM instance resolves the routing domain to the domain name of an ALB instance. You can set weights for the domain names of different ALB instances based on their capacity.

* ALB instances distribute traffic to backend servers across multiple AZs within the same region, based on BytePlus ALB's load balancing and health check features.


You can follow these steps to implement this scenario by combining BytePlus ALB and BytePlus GTM.

<span id="step-1-implement-cross-az-load-balancing-and-disaster-recovery-based-on-alb-instances"></span>
### Step 1: Implement cross\-AZ load balancing and disaster recovery based on ALB instances

Create the following two ALB instances in region A and region B respectively:


* Region A ALB instance: Performs load balancing and disaster recovery for backend servers in AZ1 and AZ2 in Region A.

* Region B ALB instance: Performs load balancing and disaster recovery for backend servers in AZ1 and AZ2 in Region B.


This article assumes that the traffic capacity ratio of backend servers for the region A ALB instance to the region B ALB instance is 4:1.

<span id="step-2-implement-cross-region-load-balancing-and-disaster-recovery-based-on-gtm-instances"></span>
### Step 2: Implement cross\-region load balancing and disaster recovery based on GTM instances

Create a GTM instance, and under this GTM instance, create one rule and one pool set. The pool set includes the following pools:


* Region A pool: The address is the domain name of the region A ALB instance, with a weight of 80.

* Region B pool: The address is the domain name of the region B ALB instance, with a weight of 20.


This way, the GTM instance can perform cross\-region load balancing and disaster recovery for the region A ALB instance and the region B ALB instance.
