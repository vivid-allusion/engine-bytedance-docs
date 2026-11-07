---
title: "Creating a VPC"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC"
---

## Scenarios

For user convenience, the platform provides a default VPC. If the default VPC does not meet your requirements, you may create a custom VPC by following this topic.

> Notes

> VPC's IPv6 is currently in Beta stage. If you need a trial, please contact your account manager.

## Action notes

The following resources are automatically created along with a VPC upon its creation:

* A default security group. For details, see [Default security group](https://docs.byteplus.com/en/docs/vpc/Default-Security-Group).

* A system route table. For details, see [Route table overview](https://docs.byteplus.com/en/docs/vpc/Route-table-overview).

## Procedures

1. Log in to [VPC console](https://console.byteplus.com/vpc/vpc).

2. Click **Create VPC**.

3.  Configure basic information and CIDR block according to the table below.

   |**Parameters** |**Notes** |**Sample value** |
   |---|---|---|
   |Region |Select Region where the VPC resides. VPCs are isolated across regions by default. Select a region closer to your business operations to reduce network latency and improve access speed. |China (Beijing) |
   |Name |Type in the name for the VPC. |vpc\-01 |
   |IPv4 CIDR |Set the IPv4 CIDR block for the VPC. **Once a VPC is created, its CIDR block cannot be modified**. Supported CIDR blocks are as follows:<br><br><br>* **10.0.0.0/8~28** (up to 16,777,213 IPs available in the VPC)<br><br>* **172.16.0.0/12~28** (up to 1,048,573 IPs available in the VPC)<br><br>* **192.168.0.0/16~28** (up to 65533 IPs available in the VPC) |192.168.0.0/16 |
   |IPv6 CIDR |Select whether to enable the IPv6 CIDR block as needed. After enabling, the following occurs:<br><br><br>* The system automatically assigns an IPv6 CIDR block with a `/56` mask to the VPC, and IPv6 addresses support VPC communication. Additionally, the system automatically creates an IPv6 gateway, which can be used to enable internet bandwidth for IPv6 addresses, allowing IPv6 addresses to communicate with the internet. |Enable<br><br>2408:XXXX:0:a600::/56 |

4. When creating a VPC in the console, you must create at least one subnet. Configure the subnet parameters according to the table below.

   |**Parameters** |**Notes** |**Sample value** |
   |---|---|---|
   |Zone |Select the subnet's Availability Zone. Within the same VPC, different Availability Zones can communicate with each other over the private network. Deploying subnets of a VPC across different availability zones enables cross\-AZ resource disaster recovery; deploying them within the same availability zone reduces network latency. |AZ\-A |
   |Name |Enter the subnet name. |subnet\-01 |
   |IPv4 CIDR |Set the subnet's CIDR block.<br><br><br>* The subnet CIDR block must fall within the VPC's address range, and CIDR blocks of different subnets must not overlap.<br><br>* The first two and the last IP address in each subnet's CIDR block are reserved for system use. These are designated as the network address, gateway address, and broadcast address, respectively. For a subnet with CIDR `192.168.1.0/24`, the system reserves addresses `192.168.1.0`, `192.168.1.1`, and 192.168.1.255, which are unavailable for use.<br><br><br>> **warning**<br><br><br>> After the Subnet is created, the CIDR block cannot be modified.<br> |192.168.1.0/24 |
   |IPv6 CIDR |If you enable the IPv6 CIDR block during VPC creation, you can choose whether or not to enable IPv6 for subnets.<br><br><br>* Once enabled, the subnet IPv6 CIDR defaults to a /64 mask. You can customize the last 8 bits of the subnet IPv6 CIDR by entering a decimal value between 0 and 255. Disabled by default.<br><br>* The first two and the last IP addresses of each subnet are reserved by the system: the first is used as the network address, the second as the gateway address, and the last is the subnet's maximum address. These addresses cannot be assigned to resources. For example, for the subnet 2001:XX::/64, the system\-reserved addresses are` 2001:XX::`, `2001:XX::1`, and `2001:XX::ffff:ffff:ffff:ffff`.<br><br><br>> **warning**<br><br><br>> After the Subnet is created, the CIDR block cannot be modified.<br> |Enable |

   Click  **+Add Subnet ** to create more than one subnet at the same time. A maximum of 3 subnets can be created at once. The subnet CIDR block must fall within the VPC's address range and must not overlap with existing subnets.

5. Configure projects and tags according to the table below.

   |**Parameters** |**Notes** |**Sample value** |
   |---|---|---|
   |Belongs to Project |Select VPC and its subnets' project. For more information, see [Project management](https://docs.byteplus.com/en/docs/vpc/Managing-projects). |default |
   |Tag |Add one or more custom tags to the VPC and its associated subnets as needed. A tag consists of a key\-value pair and is used for categorizing and searching resources More information is available in [Tag management](https://docs.byteplus.com/en/docs/vpc/Managing-tags).<br><br>Click the "Add" icon, enter a tag key and value, and then add the tag to the VPC instance. |* Tag key: vpc\-key<br><br>* Tag value: vpc\-v1 |

6. Click **Create** to complete configuration.

## What to do next

After creating the VPC, you can [create an ECS](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) within its subnet and [deploy the required services](https://docs.byteplus.com/en/docs/ecs/Self-service_website_creation) on those instances.

## Related documents

[CreateVpc](https://docs.byteplus.com/en/docs/vpc/CreateVpc)
