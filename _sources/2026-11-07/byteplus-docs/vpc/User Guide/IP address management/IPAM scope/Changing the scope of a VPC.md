---
title: "Changing the scope of a VPC"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Changing-the-scope-of-a-VPC"
---

## Scenarios

Change a VPC CIDR to a target scope for management as needed, for example, from the default VPC scope to a custom VPC scope.

## Instructions

Only unmanaged or ignored VPC CIDRs support scope changes. If it is already managed, please perform the ignore operation first.

## Procedure

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the top menu bar, select the Region.

3. In the left navigation pane, select **IPAM Scope**.

4. Click the target scope name.

5. On the **Resource details** page, click **Change scope**.

6. Drop down to select a new scope, click **OK** to complete the operation.

## Related documents

[ModifyIpamResourceCidr](https://docs.byteplus.com/en/docs/vpc/ModifyIpamResourceCidr): Modifies the scope or monitoring status of a resource CIDR.
