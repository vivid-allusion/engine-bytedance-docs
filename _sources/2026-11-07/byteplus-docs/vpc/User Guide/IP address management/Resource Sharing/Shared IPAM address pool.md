---
title: "Shared IPAM address pool"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Sharing-IPAM-Pool"
---

## Scenarios

The IPAM address pool owner must share the pool with the business accounts. Only then can these business accounts use the CIDR blocks within the pool to create VPCs.

> **warning**

> After an IPAM address pool is shared with a business account, to ensure IP traceability, IPAM must first have the capability to monitor the IP usage of the business account. Only then can the business account allocate CIDR blocks from the shared pool to create VPCs. If the business account's VPC resources cannot be automatically discovered by IPAM, the business account must share its own Resource Discovery with the IPAM owner. For more information, see [Managing a resource discovery,](https://docs.byteplus.com/en/docs/vpc/IPAM-Viewing-resource-discovery)[Shared resource discovery](https://docs.byteplus.com/en/docs/vpc/Sharing-Resource-Discovery).

## Shared IPAM address pool

### Action notes

Shared consumers of an IPAM address pool are only permitted to view and use the CIDRs within the shared pool. They are not allowed to modify or delete the IPAM address pool, add or remove pre\-populated CIDRs, create child address pools, or re‑share the pool.

### Procedures

1. Log in to the [Resource Sharing console](https://console.byteplus.com/resourcemanager/region:resource-manager+cn-beijing/resource_share/owned) using the IPAM pool owner account.

2. In the left navigation tree, select **Resource sharing \> Shared by me**.

3. In the top menu bar, select the Region.

4. On the **Shared unit** tab, click **Create shared unit**.

5. Configure parameters based on the table below.

   |Parameters |Notes |Example A |
   |---|---|---|
   |Unit name |Type in a name for the shared unit. |Shared address pool\-A |
   |Region |Select the region where the address pool resides. |China (Beijing) |
   |Product |Select VPC \- IPAM pool. |VPC \- IPAM Pool |
   |Resource ID |Select (check) the IDs of the IPAM address pools to be shared. |Select the ID of the IPAM pool |
   |Shared policy name |Defaults to and only supports IPAMPoolDefaultPermission. |IPAMPoolDefaultPermission |
   |Resource user |Supports **Allow sharing with any account** and **Allow sharing only within the same enterprise organization.** <br><br><br>* **Allow sharing with any account:**  The resource can be shared with any root user. If the account is part of an enterprise organization, sharing can also be extended to the entire organization, departments, or member accounts.<br><br>* **Allow sharing only within the same enterprise organization**: The account must be a member of an enterprise organization, and resources can only be shared with the entire organization, departments, or member accounts. |Allow sharing with any account |
   |Add by business organization |Enable the **Add via enterprise organization** feature and select the member accounts from the enterprise organization. Note that this feature can only be enabled by an enterprise organization admin. |Do not enable |
   |User type and user ID |Select root user as the type and enter the Account ID of the consumer. |Root user 210005\*\*\*\* |

6. Click **Next**, confirm everything is correct, then click **Confirm** to complete the actions.

### Accept the shared IPAM address pool

### Action notes

* If the shared consumer and the IPAM address pool owner are in the same enterprise organization, the share is automatically accepted by default.

* If the shared consumer and the IPAM address pool owner are not in the same enterprise organization, the share must be accepted manually. The sharing invitation is valid for 14 days; if not accepted within this period, it will be automatically rejected by default.

### Procedures

1. Use the IPAM address pool consumer account to log in to the [Resource Sharing console](https://console.byteplus.com/resourcemanager/region:resource-manager+cn-beijing/resource_share/owned).

2. In the left navigation pane, select **Resource sharing \> Share with me**.

3. Click **Accept** on the right side of the shared unit for the target address pool to complete the operation.

###
