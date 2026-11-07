---
title: "NAT boundary firewall configuration"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/NAT_boundary_firewall_configuration"
---

This article describes how to enable, disable, and edit the NAT boundary firewall.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This article contains important precautionary information that you need to pay attention to. Ignoring this information may impact your business, so please read it carefully.</div>


<span id="8c347a0b"></span>
## Requirements


* The cloud firewall service has been activated, and a sufficient number of NAT boundary firewall licenses have been purchased.

* A public NAT gateway has been created. For detailed operations, please refer to [Creating a Public NAT Gateway](https://docs.byteplus.com/en/docs/natgateway/Creating-an-Internet-NAT-gateway).


<span id="78db3ad0"></span>
## Precautions

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The NTA firewall only supports protection for one VPC and one NAT gateway. If two or more NAT gateways are deployed within a VPC, it is not recommended to use the NAT firewall to avoid routing errors that may damage your business.</div>


* <div data-tips="true" data-tips-type="warning">To enable and disable the NAT boundary firewall, users need to configure the correct routing table.</div>


* <div data-tips="true" data-tips-type="warning">Ensure that all the regions where your network resources are located are supported by the NAT boundary firewall; otherwise, it may lead to the inability to enable the VPC boundary firewall. For specific information, please refer to <a href="https://docs.byteplus.com/en/docs/cloud_firewall/Region_and_Availability_Zones">regions and availability zones</a>.</div>



<span id="97dd3091"></span>
## NAT gateway instance overview


1. Log in to [Cloud Firewall Console](https://console.byteplus.com/firewall/overview), click on **Firewall Switch** in the left navigation bar.

2. On the **Firewall Switch** page, click **NAT**. **Border Firewall**.

3. View the current NAT gateway protection overview. One NAT gateway instance corresponds to one NAT border firewall.

   
   |**Parameter** |**Note** |
   |---|---|
   |Unprotected |Display the number of NAT gateway instances that have not created a NAT firewall. |
   |Protected/Instance authorization specifications |Protected: The number of NAT boundary firewalls that have already been created. Instance authorization specifications: The NAT editing firewall instance specifications you have currently purchased. |
   |Protected bandwidth specifications/Bandwidth authorization specifications |Protected bandwidth specifications: The total of the protection bandwidth specifications that the NAT boundary firewall has configured. \nBandwidth authorization specifications: The bandwidth authorization specifications you are currently purchasing. |
   


<span id="f3c77df2"></span>
## Create NAT border firewall


1. Select the NAT gateways that need protection in the table below and click 【**New Cloud Firewall**】.

2. When creating the firewall, the conditions for creating the NAT gateway will be checked, and the following conditions must be met to create a cloud firewall.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The VPC subnet where the NAT gateway is located cannot contain any other business resources.</div>


* <div data-tips="true" data-tips-type="tip">The route table of the VPC subnet where the NAT gateway is located cannot contain any other task business subnets.</div>


* <div data-tips="true" data-tips-type="tip">The route table of the subnet where the NAT gateway is located cannot be a system route table; it must be a custom route table.</div>


3. After passing the inspection, refer to the table below to configure the related parameters and click the "Submit Next" button to complete the operation.

   
   |**Parameter** |**Note** |**Sample values** |
   |---|---|---|
   |Firewall name |Customize the NAT firewall name according to actual business needs for identification of the NAT firewall instance. |Develop NAT firewall |
   |Protection bandwidth specifications |You need to allocate protective bandwidth for this NAT firewall based on the actual business traffic size. When the business traffic bandwidth exceeds the protective bandwidth, the Cloud Firewall will send SMS, email, and internal message alert notifications. |500Mbps |
   |Firewall subnet configuration |Configure subnet segments for the NAT firewall, with a suggested subnet mask of 29 bits. |192.168.0.0/29 |
   |Name of the project |Select the project to which the VPC firewall belongs. For more project details, please refer to [Project Overview](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Overview).<br><br><br>* If you select All Resources of the Account in the top navigation bar before entering the creation page, you can scroll down to choose an existing project.<br><br>* If you select the Target Project in the top navigation bar before entering the creation page, only the target project can be selected. |default (Default Project) |
   |Tags |Add one or more user tags for on\-demand firewall. For more tag details, please refer to [tag overview](https://docs.byteplus.com/en/docs/resourcemanagement/Tag_Overview). Tags consist of two parts: tag key (Key) and tag value (Value), used for marking and classifying the public NAT gateway. Click **add tags** to add multiple tags, with a maximum of 20 tags that can be added simultaneously. |Label key: cfw\-key<br\>Label value: cfw\-test |
   


<span id="9aa9cefc"></span>
## Traffic diversion configuration

You need to manually customize the route in the VPC route table based on your business to redirect traffic to the NAT perimeter firewall. For more traffic diversion details, please refer to


* [The introduction to the NAT perimeter firewall](https://docs.byteplus.com/en/docs/6516/1477143)

* [Private IP outbound](https://docs.byteplus.com/en/docs/6516/1338062)[ traffic access control](https://docs.byteplus.com/en/docs/cloud_firewall/Private_network_IP_outbound_traffic_access_control)

* [Private IP inbound traffic access control](https://docs.byteplus.com/en/docs/6516/1338061)


<span id="1a9323b3"></span>
## Edit and delete the NAT perimeter firewall


1. Select the corresponding NAT boundary firewall in the table below and click 【Details】.

2. **Edit cloud firewall.** 

   * You can modify the "firewall name," "protection bandwidth specifications," and "tags" of the NAT boundary firewall.

3. **Delete cloud firewall.** 

   * Select the corresponding NAT boundary firewall in the table below and click 【Delete】 to complete the deletion.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before deleting the NAT firewall, you need to complete the flow cut configuration in the VPC, diverting the business traffic away from the firewall before shutting it down, to avoid affecting the business.</div>
