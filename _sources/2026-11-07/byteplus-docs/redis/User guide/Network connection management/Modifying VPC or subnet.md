---
title: "Modifying VPC or subnet"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modify-vpc-or-subnet"
---

Cache for Redis supports modifying network information of instances, including Virtual Private Cloud (VPC) and subnets. You can easily adjust instances to the target network (such as the network of ECS instances) according to business needs. The private networks between Redis instances and ECS instances can be interconnected.

## Prerequisite

* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

* Target private network and subnets are already created. For specific procedures, refer to [Creating VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Creating subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).

## Background information

The network environment of Cache for Redis consists of two parts: VPC and subnet, where:

* The VPC creates an isolated and autonomously configured virtual network environment for cloud resources. Within the VPC, you can customize network features such as CIDR blocks, security groups, and route entry to efficiently and securely manage cloud resources. VPC communication is supported between different availability zones within the same region.

* Subnets are segments of IP addresses allocated within a private network in an availability zone, providing private IP addresses for cloud resources (such as ECS instance and Cloud Load Balancer). You can allocate one or more subnets for a VPC as needed. Subnets inherently support VPC communication and demonstrate availability zone properties. You can create multiple subnets in different availability zones within the same VPC to deploy multiple replicas of a service system, ensuring disaster recovery across availability zones.

   For more details, refer to [What is VPC](https://docs.byteplus.com/en/docs/vpc/What-is-VPC).

## Operation impact

* During network configuration changes (including modifications to private networks or subnets), all connection addresses (such as private addresses, direct connect addresses, and public addresses) may experience 1\-2 temporary disconnections. Please proceed with caution. It is recommended to perform changes during off\-peak business hours and ensure the business has an automatic reconnection mechanism.

* Modifying private networks and subnets will not change the private address or direct connect address domain names, but their corresponding IP addresses will change. Ensure that the business uses domain names for connections and that the network environment where the business resides can communicate with the newly configured network environment.

* Promptly clear the client cache, or else read/write exceptions may occur.

* Modifying private networks and subnets will temporarily affect the use of database ecosystem products such as DTS and DBW.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. In the **Basic information** pane under the **Summary** tab, click on the![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png)icon behind the availability zone name.

5. In the pop\-up dialog box, confirm the address or domain information that will be affected by the modification, and configure as follows.

   |Parameters |Description |
   |---|---|
   |Project<br><br> |Select the project for the target VPC and subnet from the drop\-down list. By default, the project to which the instance currently belongs is displayed.<br><br>> **tip**<br><br><br>> If you modify the Redis VPC and subnet through IAM user, you can only see the VPC and subnet information under the projects that have been authorized for the current IAM user. For more details, refer to [Using Redis with IAM user](https://docs.byteplus.com/en/docs/redis/using_redis_with_subusers).<br> |
   |Virtual private cloud |Select the target VPC from the drop\-down list.<br><br>> **tip**<br><br><br><br>* > We recommend that you connect Redis instances to ECS instances in the same VPC. Otherwise, they cannot achieve optimal communication performance.<br><br><br>* > Both instances and VPCs have project attributes, and you can only select a VPC that belongs to the already selected project.<br> |
   |Subnet |Select the target subnet from the drop\-down list.<br><br>> **tip**<br><br><br>> Subnets possess availability zone properties. The drop\-down list only shows subnets that belong to the same availability zone as the instance in the current VPC.<br> |
   |Old IP address release policy |Select the old IP address release time from the drop\-down list. You can choose **Release right now**, **Release after 1 day**, **Release after 2 days**, **Release after 3 days**, or **Release after 7 days**.<br><br>> **tip**<br><br><br>> Modifying VPCs and subnets does not change the domain names of VPC addresses or direct addresses. But their corresponding IP addresses will change. It is recommended to clear the client cache promptly before the old IP address is released; otherwise, read/write exceptions may occur.<br> |
   |Risk confirmation |Click![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_68f09ee3d71a500d15692275712e7f67.png)icon on the right, carefully read the relevant database risk details and check **I have been informed and understand the relevant data risks**. |

## Relevant APIs

|API |Description |
|---|---|
|[ModifyDBInstanceSubnet](https://docs.byteplus.com/en/docs/redis/modifydbinstancesubnet) |Call the ModifyDBInstanceSubnet API to associate the target Redis instance to a specified subnet. |
