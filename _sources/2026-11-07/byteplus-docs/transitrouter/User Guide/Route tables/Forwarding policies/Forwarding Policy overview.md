---
title: "Forwarding Policy overview"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Overview-of-forwarding-policy"
---

<span id=".566A5LuL"></span>
## Overview​

A Forwarding Policy enables source\-and\-destination\-based routing. It can steer traffic from different address pairs within the same network instance through different Transit Router (TR) route tables, thereby creating distinct forwarding paths. For a single attachment, a forwarding policy takes precedence over association forwarding. For example, two subnets in a VPC run different services. Subnet A forwards traffic based on TR Route Table A. Subnet B forwards traffic to the destination CIDR block (172.16.1.0/24) based on TR Route Table B, while traffic from Subnet B to other destination CIDR blocks still forwards based on TR Route Table A. This can be achieved by configuring forwarding policies, as illustrated in the diagram below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c6390654ef7d7dbfaa256fade29cdbc9.png) </span>

<span id=".6L2s5Y-R562W55Wl5Yy56YWN5Y6f5YiZ"></span>
## Forwarding policy matching rules

A forwarding policy is a list including multiple policy entries. It determines the forwarding path of traffic based on the source and destination addresses.

The matching rules for the forwarding policy can be summarized as **ordered evaluation**, and **unique match**. The description of matching rules is shown below:


* **Ordered evaluation**: The policy processes all entries sequentially, from the highest to the lowest priority, matching access traffic against each entry.

   A lower priority value indicates a higher precedence for a policy entry.

* **Unique match**: Upon a successful match with a policy entry, the system forwards traffic according to the TR route table specified in that entry and ignores all subsequent entries. If no match is found in the forwarding policy, the system forwards traffic based on the TR route table associated with the network instance attachment.


<span id=".57qm5p2f6ZmQ5Yi2"></span>
## Limits

Forwarding policies are not currently supported on inter\-region attachments. For more about quotas and usage limits, see [Limits](https://docs.byteplus.com/en/docs/transitrouter/Product-Overview-04).
