---
title: "FAQs"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/adYtyw"
---

This document lists common questions about using the BytePlus Global Traffic Manager (GTM).

<span id="what-is-the-difference-between-byteplus-gtm-and-byteplus-dns"></span>
## What is the difference between BytePlus GTM and BytePlus DNS?

BytePlus DNS is an authoritative DNS service, primarily used for managing DNS records, and also provides simple traffic routing capabilities. BytePlus DNS supports DNS\-based routing based on the user's line and DNS\-level load balancing.

BytePlus GTM is a DNS\-based traffic routing service, which expands the traffic routing functions of BytePlus DNS by adding health check and failover capabilities.

<span id="how-is-the-load-balancing-function-of-byteplus-gtm-different-from-byteplus-load-balancer-clb-and-byteplus-application-load-balancer-alb"></span>
## How is the load balancing function of BytePlus GTM different from BytePlus Load Balancer (CLB) and BytePlus Application Load Balancer (ALB)?

BytePlus GTM directs user requests to the target address at the DNS level. Users directly access the target address, so the user traffic does not pass through BytePlus GTM.

BytePlus CLB and BytePlus ALB distribute traffic to different backend servers by proxying user access requests. User traffic goes through BytePlus CLB or BytePlus ALB.

<span id="why-can-t-i-see-the-health-check-tasks-of-my-gtm-instance"></span>
## Why can't I see the health check tasks of my GTM instance?

Your GTM instance's health check tasks might not be activated. Ensure the following conditions are met:


* Routing is started in the GTM instance. See [Start or Stop Routing](https://docs.byteplus.com/en/docs/byteplus-dns-suite/U5nvpy).

* The policy has health checks enabled. See [Update Policy](https://docs.byteplus.com/en/docs/byteplus-dns-suite/YCZRHw).

* Routing rules have health checks enabled. See [Create a Rule](https://docs.byteplus.com/en/docs/byteplus-dns-suite/snlUdP). If you use intelligent routing policy and you do not customize routing rules, the health check settings of the routing rules are the same as the routing policy.

* In the routing rules, at least one pool's **Address availability mode** is set to **Automatic**. Refer to [Create a Pool](https://docs.byteplus.com/en/docs/byteplus-dns-suite/RmUweJ).
