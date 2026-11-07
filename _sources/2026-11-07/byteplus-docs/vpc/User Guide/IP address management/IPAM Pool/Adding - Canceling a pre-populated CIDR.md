---
title: "Adding/Canceling a pre-populated CIDR"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Adding-Canceling-a-pre-populated-CIDR"
---

## Scenarios

The address pool owner can add or remove pre\-populated CIDRs to/from the IPAM address pool. The CIDR blocks allocated to the IPAM address pool are made available for business accounts to use. When business accounts create network resources through the IPAM instance, they can only use IP addresses that fall within the ranges of these pre\-populated CIDRs.

> **tip**

> Shared consumers of the IPAM address pool do not have the permissions to add or remove pre\-populated CIDRs.

## Add pre\-populated CIDR

### Instructions

If the pool is a sub\-pool, the entered CIDR must be a subset of its parent pool.

### Procedure

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the top menu bar, select the Region.

3. In the left navigation pane, select **IPAM Address Pool**.

4. Click the name of the target address pool.

5. On the **Pre\-populated CIDR** tab, click **Add Pre\-populated CIDR**.

6. Enter the pre\-populated CIDR, such as 10.0.0.0/8.

7. Click **OK** to complete the action.

## Cancel pre\-populated CIDR

### Prerequisites

* The pre\-populated CIDR must not have been used to create any sub pools. If used, delete the sub pool first. For actions, see [Deleting an IPAM pool](https://docs.byteplus.com/en/docs/vpc/Managing-IPAM-pools).

* The CIDR must not be occupied by any custom\-allocated CIDR. If it is occupied, delete the custom\-allocated CIDR first. For the procedures, see [Deleting a custom-allocated CIDR](https://docs.byteplus.com/en/docs/vpc/Creating-Deleting-a-custom-allocated-CIDR).

* The CIDR must not be in use by any VPC. If in use, [Delete VPC](https://docs.byteplus.com/en/docs/vpc/Deleting-a-VPC) first or [Ignore](https://docs.byteplus.com/en/docs/vpc/Ignoring-Unignoring-the-VPC-CIDR) on the VPC.

### Procedure

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the top menu bar, select the Region.

3. In the left navigation pane, select **IPAM Address Pool**.

4. Click the name of the target address pool.

5. Click **Cancel Pre\-populated** to the right of the target CIDR.

6. Click **OK** to complete the action.

## Related documents

* [ProvisionIpamPoolCidr](https://docs.byteplus.com/en/docs/vpc/ProvisionIpamPoolCidr): Add pre\-populated CIDR to the pool.

* [DeprovisionIpamPoolCidr](https://docs.byteplus.com/en/docs/vpc/DeprovisionIpamPoolCidr): Remove pre\-populated CIDR from the pool.
