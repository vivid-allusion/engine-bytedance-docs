---
title: "Resource sharing overview"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Resource-sharing-overview"
---

## Overview

Resource sharing refers to sharing the resources owned by your account with other accounts at the granularity of specific operations \- for example, allowing other accounts to view or manage the resource. Once the sharing configuration takes effect, resource consumers can directly reuse the shared resources without needing to recreate them. This effectively reduces resource redundancy in multi\-account environments and lowers overall operational and maintenance costs.

## Terms

|Term |Notes |
|---|---|
|Resource owner |The Resource Owner is the party that initiates the sharing of an IPAM address pool or a Resource Discovery. |
|Shared user |The Resource Consumer is the account that is invited to use the shared resources. After accepting the share, it can use the resources directly without having to recreate them. |

## IPAM application scenarios

|Resource |Scenario description |Related documents |
|---|---|---|
|IPAM Pool |The IPAM address pool owner must share the pool with the business accounts. Only then can these business accounts use the CIDR blocks within the pool to create VPCs. |[Shared IPAM address pool](https://docs.byteplus.com/en/docs/vpc/Sharing-IPAM-Pool) |
|Custom resource discovery |For a consumer to use an IPAM address pool, its VPC resources must be identifiable by the IPAM address pool owner. If the resources cannot be identified, Resource Discovery must be shared as well. |[Shared resource discovery](https://docs.byteplus.com/en/docs/vpc/Sharing-Resource-Discovery) |
