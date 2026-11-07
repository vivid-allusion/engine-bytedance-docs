---
title: "Creating an ALB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Creating-an-instance"
---

## Prerequisites

* You have registered a BytePlus account and completed real\-name authentication. For detailed steps, see Account registration and Real\-name authentication.

* Before creating an ALB instance, you should have identified the region and availability zones where the ALB instance will be deployed. For guidance on selecting regions and availability zones, see [Regions and Availability Zones](https://docs.byteplus.com/docs/clb/Regions-and-Availability-Zones).

* You should have created the Virtual Private Cloud (VPC) where the ALB instance will be deployed. For detailed actions, see [Creating a VPC](https://docs.byteplus.com/docs/vpc/Creating-a-VPC).

## Procedures

1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. In the left\-side navigation pane, select **Instances**.

4. On the instance list page, click **Create instance**.

5. configure relevant parameters based on the table below.

   |Parameter |Explanation |Example |
   |---|---|---|
   |**Basic information** |||
   |Regions |Select the region where the ALB instance resides. The region cannot be changed after the instance is created. |China (Beijing） |
   |Name |Enter the name of the ALB instance. Naming rules are as follows:<br><br><br>* Allows English letters, Chinese characters, numbers, and special characters `._-`.<br><br>* Must start with an English letter or a Chinese character.<br><br>* A maximum of 128 characters is allowed. |ALB\-X |
   |Instance edition |Select the instance edition: Basic Edition or Standard Edition.<br><br><br>* Compared to Basic Edition instances, Standard Edition instances provide more abundant features. For details, see [Instance edition comparison](https://docs.byteplus.com/docs/clb/Comparison-between-instance-editions).<br><br>* Standard Edition and Basic Edition instances follow the same billing standards. It is recommended to use Standard Edition instances to access richer product features and more flexible configuration options. |Standard edition |
   |Description |Optional. Enter the description of the ALB instance. The description must meet the following requirements:<br><br><br>* Allows letters, Chinese characters, numbers, spaces, and special characters `,._=-，。`.<br><br>* Must start with a letter or Chinese character.<br><br>* A maximum of 255 characters are allowed. |\-\- |
   |**Network Configuration** |||
   |IP type |Select the ALB IP type:<br><br><br>* **IPv4**: Only IPv4 is supported.<br><br>* **IPv4 & IPv6 dual\-stack**: Both IPv4 and IPv6 are supported.<br><br><br>> **tip**<br><br><br>> The IPv4&IPv6 dual\-stack ALB instance is in beta stage. If you need a trial, please contact your account manager or [Submit ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000645) to apply.<br> |IPv4 |
   |Network type |Select the network type for the ALB instance. The system will assign IP addresses to the ALB instance based on your selection.<br><br><br>* **Public**: A public ALB can be accessed from both the public network and the private network.<br><br>* **Private**: A private ALB instance only has a private IP address and can only be accessed via the private network. |Internet |
   |VPC |Select the VPC to which the ALB instance belongs. |VPC\-A |
   |Availability zone |Select one or more availability zones. If your services require high reliability, it is recommended to select two or more Availability Zones. |Availability zone\-A<br><br>Availability zone\-B |
   |Subnet |Select the subnet to which the ALB instance belongs. The private IP address of the ALB instance will be allocated from the CIDR block of the selected subnet. |Subnet\-A<br><br>Subnet\-B |
   |**IPv4 EIP configuration (This parameter is only available when the ALB network type is set to public)**  |||
   |ISP |The ISP of the EIP. Only BGP (multi\-line) is supported by default. |BGP (multi\-ISP) |
   |Metering method |Select the metering method for the EIP.<br><br><br>* **Pay\-by\-bandwidth**: Fees are calculated based on the duration of bandwidth usage, regardless of the actual traffic generated. This billing method is suitable for services with stable bandwidth requirements.<br><br>* **Pay\-by\-data\-transfer**: Fees are calculated based on the actual outbound internet traffic generated, regardless of the duration of bandwidth usage. This billing method is suitable for services with unstable or unpredictable bandwidth requirements.<br><br><br>For more billing details, see [Pay-as-you-go](https://docs.byteplus.com/docs/eip/Pay-as-you-go). |Pay\-by\-bandwidth\-cap |
   |Bandwidth cap |Set the bandwidth cap of the EIP. Unit: Mbps. Value range:<br><br><br>* When the metering method is **Pay\-by\-bandwidth**, the bandwidth cap value ranges from 1 to 500 Mbps.<br><br>* When the metering method is **Pay\-by\-data\-transfer**, the bandwidth cap value ranges from 1 to 200 Mbps.<br><br><br>After creating a public network instance, you can adjust the EIP bandwidth cap as needed. |100 |
   |Add to Bandwidth Package |Add the EIP to a [Bandwidth Package](https://docs.byteplus.com/en/docs/bandwidthpackage/What-is-Bandwidth-Package).<br><br><br>* To add an EIP to a Bandwidth Package, the following conditions must be met:<br><br>   * Both are in the same region.<br><br>   * Internet egress for both is the same.<br><br>   * Both have the same protection type.<br><br>   * The EIP uses pay\-as\-you\-go billing (i.e., Pay\-by\-bandwidth or Pay\-by\-data\-transfer as described in this document).<br><br>* After adding to a Bandwidth Package, the metering method and bandwidth cap configured here become ineffective. The EIP will share the bandwidth resources of the Bandwidth Package. If the EIP is later removed from the Bandwidth Package, the metering method and bandwidth cap configured here will be fully restored.<br><br>* If not added now, it can be [Added to a Bandwidth Package](https://docs.byteplus.com/en/docs/eip/Adding-an-EIP-to-a-Bandwidth-Package) later as needed. |Do not add |
   |**IPv6 EIP configuration (This parameter is only available when the ALB network type is set to public and the IP type is IPv4&IPv6)**  |||
   |ISP |The ISP of IPv6 Internet bandwidth. By default, only BGP (Multi\-ISP) is supported. |BGP (multi\-ISP) |
   |Metering method |Select the metering method for IPv6 Internet bandwidth.<br><br><br>* **Pay\-by\-bandwidth**: Fees are calculated based on the duration of bandwidth usage, regardless of the actual traffic generated. This billing method is suitable for services with stable bandwidth requirements.<br><br>* **Pay\-by\-data\-transfer**: Fees are calculated based on the actual outbound internet traffic generated, regardless of the duration of bandwidth usage. This billing method is suitable for services with unstable or unpredictable bandwidth requirements.<br><br><br>For more billing details, see [Pay-as-you-go](https://docs.byteplus.com/en/docs/IPv6/Pay-as-you-go). |Pay\-by\-bandwidth\-cap |
   |Bandwidth cap |Set the maximum bandwidth for IPv6 Internet bandwidth. Unit: Mbps. Value range:<br><br><br>* When the metering method is **Pay\-by\-bandwidth**, the bandwidth cap value ranges from 1 to 500 Mbps.<br><br>* When the metering method is **Pay\-by\-data\-transfer**, the bandwidth cap value ranges from 1 to 200 Mbps.<br><br><br>After creating a public ALB instance, you can adjust the EIP bandwidth cap as needed. |100 |
   |Add to Bandwidth Package |Add IPv6 Internet Bandwidth to a [Bandwidth Package](https://docs.byteplus.com/en/docs/bandwidthpackage/What-is-Bandwidth-Package).<br><br><br>* To add an IPv6 Internet bandwidth to a Bandwidth Package, the following conditions must be met:<br><br>   * Both are in the same region.<br><br>   * Internet egress for both is the same.<br><br>   * Bandwidth Packages support IPv6.<br><br>* After adding, the metering method and bandwidth cap configured on this page become ineffective. The IPv6 Internet bandwidth will share the bandwidth resources of the Bandwidth Package. If the IPv6 Internet bandwidth is later removed from the Bandwidth Package, the metering method and bandwidth cap configured on this page will be restored.<br><br>* If not added now, it can be [Added to a Bandwidth Package](https://docs.byteplus.com/en/docs/IPv6/Manage_Shared_Bandwidth_Package) later as needed. |Do not add |
   |**More configurations** |||
   |Delete protection |Enable the **Delete protection** feature. When this feature is enabled, the ALB instance cannot be deleted. If you need to delete the ALB instance later, please disable this feature first. |No |
   |Project |Select the project the ALB belongs to. For more information, see [Project management](https://docs.byteplus.com/en/docs/clb/Projects-Overview). |default |
   |Tags |A tag consists of a key\-value pair and is used for categorizing and searching resources [Prerequisite](https://docs.byteplus.com/en/docs/clb/Tag-Overview)<br><br>Click the add icon, enter the tag key and tag value to add a tag to the ALB. |* Tag key: alb\-key<br><br>* Tag value: alb\-test |

6. Follow the console guidance to review and accept Legal.

7. Click **Submit order** to complete the action.

###
