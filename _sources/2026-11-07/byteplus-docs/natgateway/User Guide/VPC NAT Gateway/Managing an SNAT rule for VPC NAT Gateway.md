---
title: "Managing an SNAT rule for VPC NAT Gateway"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Managing-SNAT-rules-vpcnat"
---

This topic describes how to create, modify, and delete an SNAT rule for a VPC NAT Gateway.

## Create an SNAT rule

### Before you begin

* The CIDR block of a new SNAT rule must not be the same as that of an existing SNAT rule.​

* When CIDR blocks of multiple SNAT rules overlap, the system matches SNAT rules based on the longest prefix match (LPM) principle. The longer the subnet mask of the CIDR block, the higher the priority. For example, an SNAT rule at granularity of Elastic Compute Service (ECS) has a `/32` subnet mask, which is the longest and has the highest priority.​

### Instructions

* A single NAT gateway supports up to 40 SNAT rules. If the default quota is insufficient, go to [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=NATGW) to increase the quota.​

* A single SNAT rule supports up to 1 associated NAT IP.​

### Procedure

1. Log in to the [VPC NAT Gateway console](https://console.byteplus.com/nat/vpcNat).

2. In the top menu bar, select the target region and project.

3. In the VPC NAT Gateway list, click **Configure SNAT rule** to the right of the target VPC NAT Gateway.

4. In the **SNAT rules** tab, click **Create SNAT rule**.

5. Configure relevant parameters based on the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |Name |Enter the name of the SNAT rule. |snat\-1 |
   |Granularity |Set the granularity of the SNAT rule. In this granularity, all ECS instances can access resources outside the VPC over the private network.<br><br><br>* Subnet: Select a subnet from the dropdown. The subnet must belong to the VPC of the VPC NAT Gateway.<br><br>* VPC: Select the VPC to which the VPC NAT Gateway belongs.<br><br>* ECS: Select an ECS from the dropdown. The ECS must belong to the VPC of the VPC NAT Gateway.<br><br>* Custom CIDR: Set a custom CIDR block as needed. |Subnet<br><br>subnet\-1\|192.XX.XX.0/24 |
   |NAT IP |Select the NAT IP address for the VPC NAT Gateway.<br><br>> **tip**<br><br><br>> If a DNAT rule and an SNAT rule are associated with the same NAT IP, traffic contention may occur. We recommend associating them with different NAT IPs.​<br> |natip\-1 |

6. Click **Create** to complete the action.

## Edit an SNAT rule

After an SNAT rule is created, you can modify its name and NAT IP.​

### Instructions

Modifying the NAT IP disconnects existing SNAT connections. ECSs must re\-initiate requests to establish new connections. Proceed with caution.​

### Procedure

1. Log in to the [VPC NAT Gateway console](https://console.byteplus.com/nat/vpcNat).

2. In the top menu bar, select the target region and project.

3. In the VPC NAT Gateway list, click **Configure SNAT rule** to the right of the target VPC NAT Gateway.

4. On the **SNAT rules** tab, click **Edit** to the right of the target SNAT rule to modify the name and NAT IP address.

5. Click **Save** to complete the action.

## Delete an SNAT rule

After an SNAT rule is created, you can delete it if it is no longer needed.​

### Instructions

Deleting an SNAT rule prevents the associated ECS instances from accessing resources outside the VPC over the private network. Proceed with caution.​

### Procedure

1. Log in to the [VPC NAT Gateway console](https://console.byteplus.com/nat/vpcNat).

2. In the top menu bar, select the target region and project.

3. In the VPC NAT Gateway list, click **Configure SNAT rule** to the right of the target VPC NAT Gateway.

4. In the **SNAT rules** tab, click **Delete** to the right of the target SNAT rule.

5. Click **Delete** to complete the action.

## Related documentation

* [CreateSnatEntry](https://docs.byteplus.com/en/docs/natgateway/CreateSnatEntry): Create an SNAT rule.

* [ModifySnatEntryAttributes](https://docs.byteplus.com/en/docs/natgateway/ModifySnatEntryAttributes): Modify the name and associated NAT IP address of an SNAT rule.

* [DeleteSnatEntry](https://docs.byteplus.com/en/docs/natgateway/DeleteSnatEntry): Delete an SNAT rule.
