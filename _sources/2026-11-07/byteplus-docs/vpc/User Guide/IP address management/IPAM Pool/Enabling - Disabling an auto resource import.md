---
title: "Enabling/Disabling an auto resource import"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Enabling-Disabling-an-auto-resource-import"
---

## Scenarios

After enabling resource auto\-import for an IPAM address pool, VPCs not created through the IPAM address pool will be automatically imported into the corresponding address pool for management if their CIDRs match the address pool range, with the same effect as VPCs created through the IPAM address pool.

## Instructions

* Address pools without a selected effective region do not support enabling resource auto\-import.

* After resource auto\-import is enabled, the system will continuously search for resources that fall within the CIDR range of the current address pool and automatically import them into your IPAM instance.

   * If multiple CIDRs discovered by IPAM overlap, IPAM will only automatically import the CIDR with the largest address block.

   * If IPAM discovers multiple identical CIDRs, IPAM instance will randomly import one of them.

* After resource auto\-import is disabled, already imported VPC resources are not affected.

## Procedure

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the top menu bar, select the region.

3. In the left navigation pane, select **IPAM Address Pool**.

4. Click the target pool name.

5. On the **Overview** tab, click the switch next to **Automatic Resource Import**, click **OK** to complete the action.

## Related documents

[ModifyIpamPool](https://docs.byteplus.com/en/docs/vpc/ModifyIpamPool): Modify IPAM pool information.
