---
title: "Adding or deauthorizing a cross-account authorization"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Managing-CEN-cross-account-authorization"
---

## Scenarios

When private network connectivity is required between cross\-account VPCs, accounts without a Cloud Enterprise Network (CEN) must authorize their VPCs to the other party’s CEN instance. [Prerequisite](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-accounts-within-the-same-Region)

## Add cross\-account authorization

### Prerequisites

* Prior to authorizing your VPC to a CEN instance in another account, you must first obtain the other party's primary account ID and their CEN instance ID.

* A single VPC can be authorized to a maximum of 10 cross\-account CEN instances.

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the top menu bar, select the target project and region.

3. Click the name of target VPC.

4. In the **CEN cross\-account authorization** tab, click **CEN cross\-account authorization**.

5. Enter the account ID and CEN instance ID to authorize.

6. Click **Migrate** to complete the action.

### What to do next

Once authorization is successful, when attaching network instances to the CEN under the other account, the authorized VPC from your account will be available for selection. For instructions on how to attach network instances to CEN, see [Installing a network instance](https://docs.byteplus.com/en/docs/cen/Network-instances-01).

## Cancel a cross\-account authorization

**Prerequisites**

The VPC has not been attached to any authorized CEN instance yet. If it is attached, [Detach](https://docs.byteplus.com/en/docs/cen/Network-instances-02) it first.

**Procedures**

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the top menu bar, select the target project and region.

3. Click the name of target VPC.

4. In the **CEN cross\-account authorization** tab, click **Deauthorize** on the right side of the account to be deauthorized.

5. Click **Deauthorize** to complete the operation.

## Related documents

* [GrantInstanceToCen](https://docs.byteplus.com/en/docs/cen/GrantInstanceToCen)

* [RevokeInstanceFromCen](https://docs.byteplus.com/en/docs/cen/RevokeInstanceFromCen)

* [DescribeInstanceGrantedRules](https://docs.byteplus.com/en/docs/cen/DescribeInstanceGrantedRules)

* [DescribeGrantRulesToCen](https://docs.byteplus.com/en/docs/cen/DescribeGrantRulesToCen)
