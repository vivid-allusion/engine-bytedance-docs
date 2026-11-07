---
title: "Resource Discovery overview"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Resource-Discovery-overview"
---

## Overview

Resource Discovery automatically identifies and continuously tracks the network segment usage of resources such as VPCs and subnets in a region, providing data support for centralized resource management, IP address planning, and allocation.

## Classification

|Category |Description |
|---|---|
|Default resource discovery |When a user creates an IPAM instance, it is created with the IPAM instance and deleted with the IPAM instance. |
|Custom resource discovery |A custom Resource Discovery is manually created by the user. |

## Recognition scope

|Create principal |Resource discovery identification scope |
|---|---|
|IPAM delegated admin |VPC resources of member accounts within the enterprise organization that have not created a separate Resource Discovery |
|Accounts that are not IPAM delegated admins or have not joined the enterprise organization are excluded from the scope |Only VPC resources within the current account |

### Limits

* The default Resource Discovery is automatically associated with the IPAM instance to which it belongs; no manual association is required.

* The default resource discovery cannot be disassociated.

* Deleting default resource discovery is not supported.

## Default resource discovery vs Custom resource discovery

|**Dimension** |**Default resource discovery** |**Custom resource discovery** |
|---|---|---|
|Creation timing |Automatically created when IPAM is created |Manually created by user |
|Operating regions |Always consistent with the IPAM effective region; cannot be modified separately |Effective regions can be freely added or removed |
|Cross\-account sharing |Sharing not supported |Supports cross\-account sharing via Resource Access Management (RAM) and association with the target IPAM |
|Home Region constraint |Same as IPAM primary region |When shared with the target IPAM, the primary region must match the target IPAM's primary region |
|Owner |IPAM instance owner |Custom discovery creator |

## Configuration procedures

* Same enterprise organization

   [View Resource Discovery](https://docs.byteplus.com/en/docs/vpc/Viewing-the-resource-discovery): IPAM instance owners can use the default Resource Discovery to view CIDR usage information of members within the same enterprise organization.

* Cross\-enterprise organization

   1. [Create Custom Resource Discovery](https://docs.byteplus.com/en/docs/vpc/IPAM-Viewing-resource-discovery): Create a custom Resource Discovery for accounts that need to be managed by an IPAM instance.

   2. [Share Resource Discovery](https://docs.byteplus.com/en/docs/vpc/Sharing-Resource-Discovery): Share the custom Resource Discovery with the IPAM instance owner.

   3. [Accept Shared Resource Discovery](https://docs.byteplus.com/en/docs/vpc/Sharing-Resource-Discovery): The IPAM instance owner accepts the sharing of the Resource Discovery.

   4. [Associate with IPAM Instance](https://docs.byteplus.com/en/docs/vpc/Associating-Disassociating-the-resource-discovery): The IPAM instance owner associates the shared custom Resource Discovery with the IPAM instance.

   5. [View Resource Discovery](https://docs.byteplus.com/en/docs/vpc/Viewing-the-resource-discovery): The IPAM instance owner can then view the information identified by the custom Resource Discovery.
