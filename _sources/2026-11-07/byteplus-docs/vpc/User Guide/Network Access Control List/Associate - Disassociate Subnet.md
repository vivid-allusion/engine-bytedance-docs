---
title: "Associate/Disassociate Subnet"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-with-subnet-with-a-network-ACL"
---

## Scenarios

When traffic to and from cloud resources within a subnet requires monitoring and control, you can associate the subnet with a Network ACL. By configuring Network ACL rules, you can manage the inbound and outbound traffic for the subnet.

> **tip**

> Once a subnet is associated with a Network ACL, all cross\-subnet connections for the cloud resources within it—both existing and newly established—will be governed by the Network ACL rules. Please thoroughly evaluate the potential impact on live services and proceed with extreme caution.

## Associate a subnet

### Limitations

A Network ACL can only be associated with subnets within its own VPC, and each subnet can be associated with only one Network ACL.

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Network ACL**.

3. In the top menu bar, select the target project and region.

4. Click **Associate Subnet** on the right side of the target Network Access Control List.

5. Click **Add Association​** .

6. Check one or more subnets.

7. Click **Migrate** to complete the action.

## Dissociate subnet

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Network ACL**.

3. In the top menu bar, select the target project and region.

4. Click the target Network Access Control List name.

5. Click **Disassociate** on the right side of the subnet.

6. Click **Migrate** to complete the action.

## Related documents

* [AssociateNetworkAcl](https://docs.byteplus.com/en/docs/vpc/AssociateNetworkAcl)

* [DisassociateNetworkAcl](https://docs.byteplus.com/en/docs/vpc/DisassociateNetworkAcl)
