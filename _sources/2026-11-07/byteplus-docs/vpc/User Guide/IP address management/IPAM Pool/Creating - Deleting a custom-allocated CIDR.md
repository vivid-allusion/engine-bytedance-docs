---
title: "Creating/Deleting a custom-allocated CIDR"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Creating-Deleting-a-custom-allocated-CIDR"
---

## Scenarios

Custom\-allocated CIDR refers to a CIDR block that users can manually reserve within an IPAM address pool to pre‑allocate addresses in advance for scenarios such as hybrid cloud, multi‑cloud, and data migration.

## Create custom\-allocated CIDR

### Instructions

* The custom‑allocated CIDR must be an unallocated CIDR block within the IPAM pool.

* The custom‑allocated CIDR is counted toward the used capacity of the IPAM pool.

### Procedure

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the top menu bar, select the region.

3. In the left navigation pane, select **IPAM Address Pool**.

4. Click the target pool name to enter the details page.

5. On the **CIDR allocated** tab, click **Create custom allocation**.

6. Enter the CIDR and click **OK** to complete the action.

## Delete custom\-allocated CIDR

### Instructions

* The resource owner of a pool can release all custom‑allocated CIDRs within the pool.

* Shared consumers of the pool can only release the custom‑allocated CIDRs that they created themselves.

### Procedure

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the top menu bar, select the region.

3. In the left navigation pane, select **IPAM Address Pool**.

4. Click the target pool name to enter the details page.

5. On the **CIDR allocated** tab, click **Delete** to the right of the target custom allocation.

6. After confirming the information is correct, click **Delete** to complete the action.

## Related documents

* [CreateIpamPoolAllocation](https://docs.byteplus.com/en/docs/vpc/CreateIpamPoolAllocation): Create custom\-allocated CIDR.

* [ReleaseIpamPoolAllocation](https://docs.byteplus.com/en/docs/vpc/ReleaseIpamPoolAllocation): Release custom\-allocated CIDR.
