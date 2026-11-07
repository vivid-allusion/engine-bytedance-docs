---
title: "Creating/Deleting an IPAM pool"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Managing-IPAM-pools"
---

## Scenarios

An IPAM address pool is a collection of IP address blocks (CIDRs). Top\-level address pools can be created within a scope, and these top\-level pools can act as parent pools to create multiple Sub\-pools. Additionally, IPAM address pools can serve as the CIDR source for VPC creation, and can be directly used to create VPCs.

## Create address pool

You can see this procedure to create **Top\-level pools** and **Sub\-pools**.

### Before you begin

The scope to which the pool belongs must have been created first. For the steps, see [Creating a scope](https://docs.byteplus.com/en/docs/vpc/Managing-IPAM-scopes).

### Instructions

A single IPAM private network scope supports a maximum of 50 address pools (including both top\-level and sub address pools).

### Procedure

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the top menu bar, select the Region.

3. In the left navigation pane, select **IPAM Address Pool**.

4. Click **Create Address Pool**.

5. Configure relevant parameters based on the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |**Basic information** |||
   |Name |Enter the name of the pool. |IpamPool\-A |
   |IPAM scope |Select the IPAM scope from the dropdown list. |IpamScope\-A |
   |**Address pool hierarchy** |||
   |Address pool source |Based on the [IPAM pool plan](https://docs.byteplus.com/en/docs/vpc/IPAM-address-planning), select either a top\-level pool or a sub pool.<br><br><br>* Top\-level pool: Choose **IPAM Scope** as the pool source.<br><br>* Sub pool: Choose **IPAM Address Pool** as the source, and choose an address pool within the corresponding scope as the parent address pool for this pool. |IPAM Scope |
   |Operating regions |Select the operating region for the Pool as needed.<br><br><br>* Each pool can have at most 1 effective region selected.<br><br>* If no effective region is selected for the pool, the pool cannot be used to create a VPC.<br><br>* If the parent address pool has an effective region configured, the child address pool's effective region must match that of the parent address pool. | |
   |Automatic resource import |Enable resource auto\-import. If no effective region is selected for the address pool, automatic resource import cannot be enabled.<br><br><br>* When enabled, the system will continuously discover resources within the CIDR range of this pool and automatically import them as allocations into your IPAM instance.<br><br>   * If multiple CIDRs discovered by IPAM overlap, IPAM will only automatically import the CIDR with the largest address block.<br><br>   * If IPAM discovers multiple identical CIDRs, IPAM instance will randomly import one of them.<br><br>* If this option is not enabled now, you can edit the address pool later and enable automatic resource import as needed. |Enable |
   |**Pre\-populated CIDR** |||
   |CIDR |Enter the CIDR as needed.<br><br><br>* You can click Add CIDR to add pre‑provisioned CIDR blocks. Up to 50 CIDR blocks can be added.<br><br>* If the address pool is a sub\-pool, the entered CIDR must be a subset of its parent address pool. |10.0.0.0/8 |
   |**Allocation rules** |||
   |Allocation rule settings |Enable the allocation rule settings as needed. |Enable |
   |Allocate mask |Configure the allocation mask. This parameter is only configurable after enabling the Allocation Rule Settings.<br><br>Enter the **Minimum netmask length**, **Default netmask length**, and **Maximum netmask length** for resources allocated within the address pool. |8 16 24 |
   |**More information** |||
   |Project |Select a project for the IPAM Pool. For more information, see [Project management](https://docs.byteplus.com/en/docs/vpc/Managing-projects). |default |
   |**Advanced options** |||
   |Tag |Add one or more custom tags to the IPAM pool as needed.<br><br>A tag consists of a key\-value pair and is used for categorizing and searching resources. For more information, see [Tag management](https://docs.byteplus.com/en/docs/vpc/Managing-tags). |* Tag key: IpamPool\-key<br><br>* Tag value: IpamPool\-v1 |

6. Click **Create** to complete the action.

### What to do next

Share the created IPAM address pool with business accounts. For actions, see [Shared IPAM pool](https://docs.byteplus.com/en/docs/vpc/Resource-sharing-overview).

## Delete address pool

### Prerequisites

* The Pool contains no sub\-pools. If any exist, delete sub\-pools first.

* The Pool has not allocated any CIDRs to a VPC. If any have been allocated, [Delete VPC](https://docs.byteplus.com/en/docs/vpc/Deleting-a-VPC) first or [Ignore](https://docs.byteplus.com/en/docs/vpc/Ignoring-Unignoring-the-VPC-CIDR) on the VPC.

* The Pool contains no pre\-populated CIDRs. If any exist, first [Cancel pre-populated CIDR](https://docs.byteplus.com/en/docs/vpc/Managing-IPAM-pools).

### Procedure

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the top menu bar, select the Region.

3. In the left navigation pane, select **IPAM Address Pool**.

4. Click **Delete** to the right of the target Pool.

5. Click **Delete** to complete the action.

## Related documents

* [CreateIpamPool](https://docs.byteplus.com/en/docs/vpc/CreateIpamPool): Create IPAM Pool.

* [DeleteIpamPool](https://docs.byteplus.com/en/docs/vpc/DeleteIpamPool): Delete IPAM Pool.
