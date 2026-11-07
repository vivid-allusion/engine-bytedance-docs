---
title: "Step 3: Business account creates VPC"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Step-3-Business-account-creates-VPC"
---

## Scenarios

When the business account creates a VPC and allocates a CIDR from the IPAM address pool, IPAM will uniformly plan, allocate, and track the IP addresses. This effectively prevents issues such as address resource fragmentation, CIDR conflicts, and decentralized management.

## Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the top menu bar, select the target region.

3. Click **Create VPC**.

4. Configure parameters based on the table below.

   |Parameters |Notes |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Region |Select the region of the VPC. |China (Beijing) |
   |Name |Enter the name of the VPC. |VPC\-A1 |
   |**CIDR block** |||
   |IPv4 CIDR |Configure the IPv4 CIDR assignment method.<br><br><br>* Manual Assignment: Enter the IPv4 CIDR directly.<br><br>* **IPAM Assignment: Select an address pool from the dropdown and choose the netmask length.**  |**Assigned by IPAM**<br><br> **/16** |
   |**Subnet** |||
   |Zone |Select an Availability Zone. |AZ\-A |
   |Name |Type the name of the subnet. |Subnet\-A |
   |IPv4 CIDR |Configure the subnet CIDR block, which must fall within the VPC's address range. |10.1.1.0/24 |

5. Click **Create** to complete the action.

Once the VPC is created, the IPAM delegated administrator can [review Resource Discovery](https://docs.byteplus.com/en/docs/vpc/IPAM-Viewing-resource-discovery) to gain insight into the utilization of the IPAM address pool.
