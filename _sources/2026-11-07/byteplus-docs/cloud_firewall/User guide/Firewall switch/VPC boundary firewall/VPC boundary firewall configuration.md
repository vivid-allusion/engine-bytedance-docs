---
title: "VPC boundary firewall configuration"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/VPC_boundary_firewall_configuration"
---

This article describes how to enable, disable, and edit the VPC boundary firewall.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This article contains important tips that require your attention; ignoring this information may affect your business, so please read carefully.</div>


<span id="3ceb9842"></span>
## Requirements


* The cloud firewall enterprise edition or flagship edition has been activated.

* The TR transit router has been purchased, and the network interconnection between VPCs or between VPC and VPN, or between VPC and dedicated line has been completed using the transit router. For specific operations, please refer to [achieving interconnection and isolation between specified VPCs](https://docs.byteplus.com/en/docs/transitrouter/Best-Practices-01), [achieving independent interconnection between different VPCs and IDC](https://docs.byteplus.com/en/docs/transitrouter/Realize-the-Optimization-of-Different-Subnets-in-VPC-to-Access-IDC).


<span id="1930f883"></span>
## Usage restrictions


* When there are static routes within `100.64.0.0/10` in the routing table of the transit router, diversion configuration is not supported.

* Routing conflict diversion configuration for VPC network instances is not supported, including routing conflicts between VPC network instances and routing conflicts between VPC network instances and firewall VPC; otherwise, network interruption will occur after the configuration of automatic diversion scenarios. It is recommended to reasonably plan the firewall VPC subnet and VPC network instance subnet based on business needs.

* Automatic diversion mode does not support IPsec\-VPN instances.

* VPC firewall currently does not support IPv6 scenarios.


<span id="4f55b11c"></span>
## Precautions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">In automatic diversion mode, enabling and disabling the VPC border firewall has no impact on the service.</div>


2. <div data-tips="true" data-tips-type="tip">In manual diversion mode, enabling and disabling the VPC border firewall requires users to configure the correct routing table and fallback routing table.</div>


3. <div data-tips="true" data-tips-type="tip">When the diversion instance has a dedicated line gateway, closing the cloud firewall may cause a few seconds of network delay and may result in service interruption; it is recommended to perform these actions during off\-peak hours for the business.</div>



<span id="8527e1e3"></span>
## Overview of transit router protection


1. Log in to [the cloud firewall console](https://console.byteplus.com/firewall/overview), and click **Firewall Switch** in the left navigation bar.

2. On the **Firewall Switch** page, click **VPC Border Firewall**.

3. View the current overview of transit router protection, where one TR transit router instance corresponds to one VPC border firewall.

   
   |**Parameter** |**Note** |
   |---|---|
   |Unprotected |Displays the number of TR transit router instances without a created VPC firewall. |
   |Protected/instance authorization specifications |Protected: Number of VPC firewalls that have been created. \nInstance authorization specifications: The specifications of the VPC firewall instances you have currently purchased. |
   |Protected bandwidth specifications/bandwidth authorization specifications |Protected bandwidth specifications: The total of the protection bandwidth specifications configured by the VPC firewall. Bandwidth authorization specifications: The VPC firewall bandwidth authorization specifications you are currently purchasing. |
   


<span id="f16d9d8b"></span>
## Create a VPC boundary firewall


1. Select the transit router that needs protection in the VPC firewall table and click 【**Create Cloud Firewall**】.

2. Refer to the table below to configure the related parameters and click the "Submit Next" button to complete the operation.


<span id="3df3209e"></span>
### Select the diversion mode


|Parameter |Description |
|---|---|
|Automatic traffic diversion (recommended) |* You only need to select the VPC and dedicated line instances that need to divert traffic, and the cloud firewall will automatically link the TR transit router to configure the routing table to complete the traffic diversion.<br><br>* Automatic traffic diversion mode does not support IPsec\-VPN instances. |
|Manual Drainage |* You need to manually configure the traffic diversion policy on the TR transit router based on your business needs to redirect traffic to the cloud firewall. |


<span id="35a014b4"></span>
### Create a new VPC boundary firewall


1. After selecting the diversion mode, you need to configure the firewall creation.

   
   |**Parameter** |**Note** |**Value example** |
   |---|---|---|
   |Firewall name |Customize the VPC firewall name based on actual business conditions for identifying the VPC firewall instance. |IDC \- Volcano Firewall |
   |Protection bandwidth specifications |You need to allocate protective bandwidth for the VPC firewall based on the actual business traffic size. When the business traffic bandwidth exceeds the protective bandwidth, the cloud firewall will send SMS, email, and internal message alert notifications. |500Mbps |
   |Firewall VPC segment |* Configure the VPC network segment and subnet segment where the VPC firewall is located. The firewall subnet is used to deploy firewall instances; the larger the traffic, the more instances deployed, which occupies more IPs.<br><br>* The recommended mask for the three subnet segments of the cloud firewall in VPC is less than or equal to 28 bits and should not conflict with the planned network segments. The cloud firewall subnet is used for traffic redirection and backup disaster recovery. |192.168.0.0/24 |
   |VPC subnet 1 network segment ||192.168.0.16/28 |
   |VPC subnet 2 network segment ||192.168.0.32/28 |
   |VPC subnet 3 segment ||192.168.0.48/28 |
   |Name of the project to which the domain belongs. |Select the project to which the VPC firewall belongs. For more project details, please refer to [Project Overview](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Overview).<br><br><br>* If you select all resources of the account in the top navigation bar before entering the creation page, you can drop down to select an existing project.<br><br>* If you select the target project in the top navigation bar before entering the creation page, only the target project can be selected. |default (default project) |
   |Tag |Add one or more user tags to the on\-demand firewall. For more tag details, please see [tag overview](https://docs.byteplus.com/en/docs/resourcemanagement/Tag_Overview). The tag consists of two parts: the tag key (Key) and the tag value (Value), used for marking and classifying the public NAT gateway. Click **add tag** to add multiple tags, with a maximum of 20 tags added at the same time. |Tag key: cfw\-key\nTag value: cfw\-test |
   

2. Click the "Submit Next" button to proceed with the diversion configuration. If you choose "Manual Diversion Configuration," you will need to manually configure the routing on the TR transit router for diversion.


<span id="c8ba3d0a"></span>
### Cloud Firewall Diversion Configuration (Automatic Diversion)


1. After the cloud firewall is created, diversion configuration needs to be performed.

   
   |**Configuration item** |**Configuration Description** |**Configuration Parameter** |
   |---|---|---|
   |**Drainage Scenario Name** |Define the name of the traffic diversion scenario. This name is used to label the type of traffic diversion scenario; it is recommended that you enter a meaningful name based on the actual situation of the business. |IDC and business VPC drainage |
   |**Drainage scenario selection** |Select the traffic redirection scenario type based on the protection requirements of the network instances (VPC, dedicated line, VPN).<br><br><br>* **Point\-to\-point**: The traffic between two network instances is controlled by the cloud firewall. Applicable to simple network topology environments.<br><br>* **Point\-to\-multipoint**: The traffic between one network instance and multiple network instances is controlled by the cloud firewall. Applicable to star network topology environments; the left network instance can have its traffic with the multiple instances on the right controlled by the cloud firewall, while the traffic between the multiple instances on the right does not pass through the cloud firewall.<br><br>* **Multipoint interconnection**: The traffic between multiple network instances is controlled by the cloud firewall. Applicable to **FullMesh** mesh network topology environments. |Multi\-point interconnection |
   |**Instance selection** |Configure the network instances that require traffic redirection (multiple interconnections). |Business VPC\nIDC |
   

2. Click the "Submit Next" button to complete the traffic diversion configuration. Creating the traffic diversion process takes longer, estimated at around 10 minutes (the more routing entries, the longer it takes). Once completed, traffic protection between the network instances connected to the transit router can be achieved.

3. After completing the traffic diversion configuration, the cloud firewall will create the following resources in the TR transit router.

   * A new network instance connection named "CFW_system_please do not edit" is added to the TR transit router, which is a VPC firewall instance.

   * Several routing tables named "CFW_system_please do not edit" are added to the routing table, associating forwarding with network instances and VPC firewalls for traffic pulling between the firewall and network instances.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">Please do not edit the VPC firewall network instance connection and related routing tables in TR, as this may lead to traffic interruption.</div>


2. <div data-tips="true" data-tips-type="warning">When the cloud firewall switch is turned off or the service expires, the system will automatically forward the traffic of the VPC instances to the system routing table. To ensure normal business operation, please make sure to configure the corresponding fallback routes in the system routing table.</div>



<span id="614dd10c"></span>
## Edit or delete the VPC firewall.

<span id="c43be293"></span>
### Edit or delete the traffic diversion scenario.


1. Select the transit router that needs protection in the VPC firewall table and click 【Details】.

2. **Edit and delete diversion scenarios**.

   * Edit: Select the corresponding diversion scenario, click the 【Edit】 button at the top right corner of the diversion scenario card to perform delete, modify, and other operations on the diversion instance.

   * Delete: Select the corresponding diversion scenario and click the 【Close】 button at the top right corner of the diversion scenario card. After the diversion scenario is closed, click the 【Delete】 button at the top right corner of the diversion scenario card to complete the deletion operation.


<span id="1913d489"></span>
### Edit or delete VPC boundary firewall


1. Select the corresponding VPC boundary firewall in the table below and click 【Details】.

2. **Edit and delete cloud firewalls.** 

   * Edit: You can modify the “firewall name,” “protection bandwidth specification,” “tags” of the VPC boundary firewall.

   * Delete: After deleting the cloud firewall, business traffic will not be subject to access control by the cloud firewall, please delete with caution.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To avoid business interruption, please pay attention to the following items before deleting the VPC cloud firewall instance:</div>



* <div data-tips="true" data-tips-type="warning">In manual mode, you need to delete the routes pointing to the VPC boundary firewall in advance, and then delete the firewall instance.</div>


* <div data-tips="true" data-tips-type="warning">In automatic mode, if the firewall is in an enabled state, you need to delete all traffic diversion scenarios before deleting the firewall instance.</div>



<span id="c1ff1957"></span>
## Best Practices


* [Access control for traffic between VPCs (automatic diversion configuration)](https://docs.byteplus.com/en/docs/cloud_firewall/Access_control_for_traffic_between_VPCs)

* [Traffic access control between VPC and dedicated line (automatic steering configuration)](https://docs.byteplus.com/en/docs/cloud_firewall/Access_control_for_traffic_between_a_VPC_and_an_instance)

* [Traffic access control between VPC and VPN (manual steering configuration)](https://docs.byteplus.com/en/docs/cloud_firewall/Access_control_for_traffic_between_a_VPC_and_a_VPN)

* [Traffic access control between VPN and dedicated line (manual steering configuration)](https://docs.byteplus.com/en/docs/cloud_firewall/Access_control_for_traffic_between_a_VPN_and_an_instance)
