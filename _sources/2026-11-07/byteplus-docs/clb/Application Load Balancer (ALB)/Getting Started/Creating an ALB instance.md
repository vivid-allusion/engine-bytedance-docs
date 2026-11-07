---
title: "Creating an ALB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Creating-an-ALB-instance"
---

Application Load Balancer (ALB) is a load balancer service oriented towards the application layer. Before using the ALB service, you need to create an ALB instance. The ALB service is an overall concept, while the ALB instance is the specific load balancer that you can configure and manage in practice.

The ALB instance receives requests from clients and distributes them according to the forwarding rules and load balancing algorithms you set.

## Prerequisites

* Before creating an instance, you need to select the region closest to the majority of your users based on their geographical distribution to reduce access latency.

* Prepare the [VPC](https://docs.byteplus.com/en/docs/vpc/What-is-VPC) and [Backend ECS](https://docs.byteplus.com/en/docs/ecs/Instance-overview) instances required for subsequent configuration in the selected region in advance.

## Procedures

1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. In the left navigation tree, select **Instance**.

4. Click **Create instance**.

5. configure relevant parameters based on the table below. The following table only lists the required configuration items. For all other configuration items, default values will be applied. For more information, see [Creating an instance](https://docs.byteplus.com/docs/clb/Creating-an-instance).

   |**Configuration item** ||**Description** |**Example** |
   |---|---|---|---|
   |Basic information |Regions |Select the region to which the ALB instance belongs. It must be in the same region as the prepared VPC. |China (Beijing） |
   ||Name |Set the name of ALB instance |alb\-1 |
   ||Instance edition |Select the instance edition. Compared to Basic Edition instances, Standard Edition instances provide more abundant features. For details, see [Instance edition comparison](https://docs.byteplus.com/docs/clb/Comparison-between-instance-editions). |Standard |
   |Network Configuration |IP type |Select the IP type of ALB instance. |IPv4 |
   ||Network type |Set the network type of ALB instance. The system will assign IP addresses to the ALB instance based on your selection.<br><br><br>* **Public**: A public ALB instance has both an elastic IP address (EIP) and a private IP address. A public ALB instance can be accessed via the internet or through a private network. When using an EIP, you will incur relevant charges. For billing details, see [EIP billing](https://docs.byteplus.com/docs/eip/Pay-as-you-go).<br><br>* **Private**: A private ALB instance only has a private IP address and can only be accessed via the private network. |Internet |
   ||VPC |Select the VPC where the instance resides. Only server groups and backend servers within the same VPC can be bound to the corresponding ALB instance. |ALB\-VPC2 |
   ||Availability zone |Select the availability zones in the current region. At least one availability zone must be selected. When multiple availability zones exist, it is recommended to select at least two availability zones for deploying the ALB instance to further improve overall system availability. |Availability zone A, availability zone B |
   ||Subnet |Select the subnet under the availability zone. |AZ\-A: Subnet is alb\-vpc2\-aza<br><br>AZ\-B: Subnet is alb\-vpc2\-azb |
   |EIP configuration |ISP |Select the ISP type for the EIP. |BGP (multi\-ISP) |
   ||Metering method |Select the metering method for the EIP.<br><br><br>* **Pay\-by\-bandwidth**: Fees are calculated based on the duration of bandwidth usage, regardless of the actual traffic generated. This billing method is suitable for services with stable bandwidth requirements.<br><br>* **Pay\-by\-data\-transfer**: Fees are calculated based on the actual outbound internet traffic generated, regardless of the duration of bandwidth usage. This billing method is suitable for services with unstable or unpredictable bandwidth requirements.<br><br><br>For EIP, both **Pay\-by\-bandwidth** and **Pay\-by\-data\-transfer** belong to the Pay\-As\-You\-Go billing method. For billing details, see [Pay-as-you-go](https://docs.byteplus.com/docs/eip/Pay-as-you-go). |Pay\-by\-bandwidth\-cap |
   ||Bandwidth cap |Set the bandwidth cap of the EIP. Unit: Mbps.<br><br>Value range:<br><br><br>* When the metering method is **Pay\-by\-bandwidth**, the bandwidth cap value ranges from 1 to 500 Mbps.<br><br>* When the metering method is **Pay\-by\-data\-transfer**, the bandwidth cap value ranges from 1 to 200 Mbps.<br><br><br>After creating a public network instance, you can adjust the EIP bandwidth cap as needed. |100 Mbps |

6. Follow the console guidance to review and accept the Legal. Click **Submit order** to complete creation.

7. Return to the **Instance** page in the console. You will see that the newly created instance has been added to the instance list.
