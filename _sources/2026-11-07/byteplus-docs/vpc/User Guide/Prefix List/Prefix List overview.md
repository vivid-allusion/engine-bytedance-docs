---
title: "Prefix List overview"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Prefix-list-overview"
---

<span id=".566A5LuL"></span>
## Overview

A prefix list is a collection of CIDR blocks that can be referenced by multiple types of network resources. When a prefix list is modified, all resources associated with it are updated synchronously, making operations and maintenance easier.

The resources that can reference a prefix list are as follows:


|Product |Supported resources for referencing |Related documents |
|---|---|---|
|Virtual Private Cloud (VPC) |Security group rule |[Adding a security group rule](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules) |
||Route entry |[Adding a route](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry) |
|Transit Router (TR) |Route entry |[Managing a static route](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05) |
||Route policy |[Creating a route policy](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-routing-policy) |


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

When modifying the contents of a prefix list, all configuration constraints of the network resources that reference it must be met simultaneously.

<span id="NVGbWiKT"></span>
## Configuration procedures


1. [Create a prefix list](https://docs.byteplus.com/en/docs/vpc/Creating-a-prefix-list)

2. [Add a prefix list entry](https://docs.byteplus.com/en/docs/vpc/Managing-entries-in-the-prefix-list#.5re75Yqg5YmN57yA5YiX6KGo5p2h55uu)

3. Usage:

   * Security Group: [Add a security group rule](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules), and select the prefix list as the Destination/Source address parameter.

   * VPC route table: [Add a route](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry), and select the prefix list as the Destination CIDR parameter.

   * TR route table: [Create a static route](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05), select the prefix list as the destination CIDR block.

   * Route policy: [Create a route policy](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-routing-policy), then select the prefix list as the route prefix in the match condition.
