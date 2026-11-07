---
title: "Scope overview"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Scope-overview"
---

## Overview

An IPAM scope is the top\-level container in IPAM, where each scope represents an independent IP address space. CIDRs are completely independent between different scopes.

## Category

|Category |Description |
|---|---|
|Default scope |Created with the IPAM instance. |
|Custom scope |User\-created scope. |

## Status of a VPC within a scope

IPAM Resource Discovery automatically identifies all VPCs and subnets within its discovery range and associates them with the corresponding IPAM scope. When creating a VPC, if an IPAM address pool is selected, the VPC is associated with the scope to which the address pool belongs; otherwise, the VPC is associated with the default scope (subnets are associated with the same scope as their VPC). For the recognition range of resource discovery, see [Resource Discovery overview](https://docs.byteplus.com/en/docs/vpc/Resource-Discovery-overview).

The following are the various states of a VPC within its scope:

|Category |Value |Description |Advice |
|---|---|---|---|
|Managed status |Managed |Indicates that the VPC's CIDR has been incorporated into an address pool. |\-\- |
||Unmanaged |Indicates that the VPC's CIDR is not incorporated into any address pool.<br><br>For example: The VPC's CIDR does not match the address pool's preset CIDR, or the address pool does not have resource auto\-import enabled. |Change the scope of a VPC's CIDR, or enable resource auto\-import for an address pool. |
||Ignored |For specific VPCs that do not require management by IPAM, users can actively ignore them. The system will then no longer validate the managed status, compliance, or IP overlap for these VPCs. |\-\- |
|Compliance status |Compliant |Indicates that after the VPC's CIDR is managed, it complies with the allocation rules of its address pool. |\-\- |
||Non\-compliant |Indicates that after the VPC's CIDR is managed, it does not comply with the allocation rules of its pool. |Modify the allocation rules or change its scope. |
||Unmanaged |Indicates that compliance is not validated. |\-\- |
||Ignored |For specific VPCs that do not require management by IPAM, users can actively ignore them. The system will then no longer validate the managed status, compliance, or IP overlap for these VPCs. |\-\- |
|Overlap status |Overlap |Indicates that the VPC's CIDR overlaps with the CIDR of another VPC. |Change the scope for any unmanaged VPC among them. |
||Non\-overlapping |Indicates that the VPC's CIDR does not overlap with any other VPC's CIDR. |\-\- |
||Ignored |For specific VPCs that do not require management by IPAM, users can actively ignore them. The system will then no longer validate the managed status, compliance, or IP overlap for these VPCs. |\-\- |

### Limits

|Limits |Max |Adjustable |
|---|---|---|
|Maximum number of scopes per IPAM instance |5 |No |
