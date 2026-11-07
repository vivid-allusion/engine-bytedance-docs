---
title: "Creating a subnet"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet"
---

## Scenarios

A subnet is a segment of a VPC CIDR block allocated within a specific Availability Zone, providing private IP addresses for cloud resources (e.g., ECS instances and Load Balancers.).

> **tip**

> VPC's IPv6 is currently in Beta stage. If you need a trial, please contact your account manager.

## Action notes

* In the same VPC, the CIDR blocks of different subnets cannot overlap.

* After a subnet is created, it is automatically associated with the system route table.

* When creating a subnet, it is not supported to specify a project for it; its project defaults to the same as the VPC it belongs to. Change project of the VPC, the subnet's project affiliation does not automatically update. To enable synchronous updates, you must Resource transfer in for both the VPC and its subnets.

## Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation tree, select **Subnet**.

3. In the top menu bar, select the target project and region.

4. Click **Create Subnet**.

5.  Configure parameters based on the table below.

   |Parameters |Notes |Sample value |
   |---|---|---|
   |VPC |Select the VPC for the subnet. |vpc\-01\|192.168.0.0/16 |
   |CIDR |Select the CIDR block for the subnet. By default, resources use the primary CIDR block. You can switch to a [Secondary CIDR](https://docs.byteplus.com/en/docs/vpc/Managing-secondary-CIDR-blocks) if needed. |192.168.0.0/16 (primary CIDR block) |
   |Zone |Availability Zones (AZs) are physically isolated locations within the same region, with independent power and network infrastructure. Within the same VPC, availability zones can communicate over the private network.<br><br>When deploying subnets in a VPC, there are two strategies:<br><br><br>* Distributed deployment across different availability zones enables disaster recovery and enhances business stability.<br><br>* Centralized deployment in the same availability zone reduces network latency and meets low\-latency business requirements. |AZ\-A |
   |Name |Enter the name of the subnet. |subnet\-05 |
   |IPv4 CIDR |Set the subnet's CIDR block.<br><br><br>* The subnet CIDR block must fall within the VPC's address range, and CIDR blocks of different subnets must not overlap.<br><br>* The first two and the last IP address in each subnet's CIDR block are reserved for system use. These are designated as the network address, gateway address, and broadcast address, respectively. For a subnet with CIDR `192.168.1.0/24`, the system reserves addresses `192.168.1.0`, `192.168.1.1`, and `192.168.1.255`, which are unavailable for use.<br><br><br>> **warning**<br><br><br>> After the Subnet is created, the CIDR block cannot be modified.<br> |192.168.5.0/24 |
   |IPv6 CIDR |If the VPC is dual\-stack, you can choose whether to enable IPv6 for the subnet.<br><br><br>* Once enabled, the subnet IPv6 CIDR defaults to a /64 mask. You can customize the last 8 bits of the subnet IPv6 CIDR by entering a decimal value between 0 and 255. Disabled by default.<br><br>* The first two and the last IP addresses of each subnet are reserved by the system: the first is used as the network address, the second as the gateway address, and the last is the subnet's maximum address. These addresses cannot be assigned to resources. For example, for the subnet 2001:XX::/64, the system\-reserved addresses are` 2001:XX::`, `2001:XX::1`, and `2001:XX::ffff:ffff:ffff:ffff`.<br><br><br>> **warning**<br><br><br>> After the Subnet is created, the CIDR block cannot be modified.<br> |Not selected |

6. Click  **+Add subnet**. Configure each subnet following the same pattern as the previous step, creating multiple subnets in a single action.

7. Click the add icon (+), then enter the tag key and value to assign tags to the newly created subnet(s), facilitating subnet categorization and search.

8. Click **Create** to complete the configuration.

## What to do next

After creating subnets, you can [Create instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) within the subnets and [Deploy related services](https://docs.byteplus.com/en/docs/ecs/Self-service_website_creation) on those ECSs.

## Related documents

[CreateSubnet](https://docs.byteplus.com/en/docs/vpc/CreateSubnet)
