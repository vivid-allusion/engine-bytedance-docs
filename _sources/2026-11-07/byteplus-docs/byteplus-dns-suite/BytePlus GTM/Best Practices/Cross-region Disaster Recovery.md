---
title: "Cross-region Disaster Recovery"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/jEzSkh"
---

This document introduces the cross\-region active\-active solution based on BytePlus GTM.

<span id="overview"></span>
## Overview

For performance, redundancy, and disaster recovery considerations, large\-scale internet services typically have multiple centers. Therefore, when deploying services in multiple regions, you need to implement cross\-region disaster recovery to ensure that services can quickly recover or continue to operate in the event of a region\-level failure. Due to the significant latency between IDCs across regions, traffic switching has a considerable impact on the network latency of user requests, leading to performance and cost issues.

In such cases, we can implement traffic management and cross\-region disaster recovery under region\-level failures through a cross\-region active\-active architecture. For example, active\-active setups between multiple regions in public clouds, or disaster recovery and service active\-active setups between multiple on\-premise IDCs that are geographically distant. The cross\-region active\-active architecture supports disaster recovery both within a single region across multiple Availability Zones (AZs) and across regions. In case of an AZ failure, traffic can be switched to other AZs in the same region through load balancing.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a0a86b051f63847899dfd2f587785a95.jpeg) </span>

<span id="steps"></span>
## Steps

The following diagram illustrates a solution that implements load balancing and cross\-region disaster recovery under region\-level failures in Region A and Region B regions through a cross\-region active\-active architecture.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_cf298ac78edc77a28ff6f0332e486f4f.jpeg) </span>

In this diagram, `regiona.alb.example.com` and `regionb.alb.example.com` are the CNAMEs of the load balancers in Region A and Region B, respectively. You can also use the Virtual IP (VIP) addresses of the load balancers.

Follow these steps to implement the cross\-region active\-active solution shown in the diagram above.


1. [Create a GTM instance](https://docs.byteplus.com/docs/byteplus-dns-suite/k_FIn3).

2. [Configure the GTM instance you created](https://docs.byteplus.com/docs/byteplus-dns-suite/5qftVh). You need to:

   * Select basic routing

   * Enable health checks

   * [Create two pools](https://docs.byteplus.com/docs/byteplus-dns-suite/RmUweJ). The addresses included in each pool are as follows:

   
   |Pool |Address |
   |---|---|
   |Region A |regiona.alb.example.com |
   |Region B |regionb.alb.example.com |
   

   The weight of the address `regiona.alb.example.com` is 80; the weight of the address `regionb.alb.example.com` is 20.

   * [Create a rule](https://docs.byteplus.com/docs/byteplus-dns-suite/snlUdP). In the rule, add **Pool set A**, which includes the **Region A** and **Region B** pools.

3. [Start the GTM instance](https://docs.byteplus.com/docs/byteplus-dns-suite/U5nvpy). Once the GTM instance is successfully started, the cross\-region active\-active solution described in the diagram above is implemented.
