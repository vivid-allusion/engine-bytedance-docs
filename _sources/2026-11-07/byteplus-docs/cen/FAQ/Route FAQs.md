---
title: "Route FAQs"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Route-entries-faq"
---

## How do I add Cloud Enterprise Network (CEN) routes?

When a CEN instance loads network instances, it automatically learns and advertises routes. Manual addition is not required.

## How do I modify CEN routes?

Direct modification is not supported. You can go to the network instance page and modify the subnet address to adjust the route entries in the routing table.

## If the destination CIDR blocks of loaded network instances within the same CEN instance conflict, how is traffic forwarded?

Depending on the types of conflicting network instances, the behavior is divided into the following three scenarios:

* VPC vs. VPC route conflict: Routes are forwarded based on the order in which the VPCs were attached. The route from the first\-attached VPC is used. The route from the later\-attached VPC is marked as **Conflict** and does not take effect.

* VPC vs. Direct Connect Gateway route conflict: **VPC routes \> Direct Connect routes**. VPC routes take precedence over Direct Connect routes. The VPC route is used, and the Direct Connect Gateway route status is set to **Available**.

* Direct Connect Gateway vs. Direct Connect Gateway route conflict: The priority is **Direct Connect static routes \> Direct Connect BGP routes \> ECMP routes**. The highest priority route is used, and the other routes are set to **Available**.
