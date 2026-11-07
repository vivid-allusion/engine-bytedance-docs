---
title: "Ignoring/Unignoring the VPC CIDR"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Ignoring-Unignoring-the-VPC-CIDR"
---

## Scenarios

IPAM supports ignoring special address ranges that do not require IPAM attention. The system no longer validates the hosting status, compliance status, or overlap of ignored address ranges.

## Instructions

* A VPC CIDR that has been actively ignored remains within the scope.

* After the CIDR used by a VPC is ignored, the associated IPAM address pool reclaims that range, and the reclaimed addresses can be allocated to other resources.

* After a VPC's CIDR is unignored, IPAM cannot manage it if the original IPAM address pool has not enabled automatic resource import, or if the CIDR has already been allocated. To manage the VPC's CIDR, first enable automatic resource import for the original IPAM address pool; if it is still not managed, you can change the scope.

## Procedure

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the top menu bar, select the region.

3. In the left navigation pane, select **IPAM Scope**.

4. Click the target scope name.

5. On the **Resource details** page, click **Ignore** or **Unignore**.

6. Click **OK** to complete the action.

## Related documents

[ModifyIpamResourceCidr](https://docs.byteplus.com/en/docs/vpc/ModifyIpamResourceCidr): Modifies the scope or monitoring status of a resource CIDR.

##
