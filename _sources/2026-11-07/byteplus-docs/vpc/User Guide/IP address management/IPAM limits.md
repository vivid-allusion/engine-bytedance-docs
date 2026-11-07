---
title: "IPAM limits"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/ipam-constraint-restriction"
---

This topic introduces the limits of IP Address Manager (IPAM).

## **Quota limits**

|Limits |Max |Adjustable |
|---|---|---|
|Maximum number of IPAM instances per account per region |1 |No |
|Maximum number of scopes per IPAM instance |5 |No |
|Maximum number of pre\-populated CIDRs supported per address pool |50 |No |
|Maximum number of address pools per IPAM private scope (including top\-level and sub pools) |50 |No |
|Maximum number of Resource Discoveries that can be created per account per region |1 |No |
|Maximum number of Resource Discoveries that can be associated with a single IPAM (including the default) |5 |No |
|Maximum number of effective regions that can be configured per IPAM |10 |No |

## Limits

* A sub\-pool can also serve as a parent pool for other address pools. The maximum hierarchy depth for address pools is 10 levels.

* A sub\-pool is a subset of its parent address pool.

##
