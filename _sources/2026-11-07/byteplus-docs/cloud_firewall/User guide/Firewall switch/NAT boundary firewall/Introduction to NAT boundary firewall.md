---
title: "Introduction to NAT boundary firewall"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Introduction_to_NAT_boundary_firewall"
---

<span id="23f73e8b"></span>
## What is a NAT firewall? 

NAT firewall policy configuration supports access control for traffic from private IP of the NAT gateway to the public network, effectively intercepting unauthorized access from the internal network to the public network. The architecture diagram of the NAT firewall is as follows.

<div style="text-align: center">
<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b7a7f1137d829a028fa453c4462dcd37.png" /></div>


<span id="5d19fece"></span>
## NAT firewall drainage principle

This article describes how to drain NAT gateway traffic to the cloud firewall, using the following scenario to illustrate the working principle of cloud firewall drainage.

> A certain enterprise has deployed a development VPC (192.168.1.0/24, 192.168.2.0/24) and has external software calling requirements in the daily development environment. Now it is necessary to drain NAT gateway traffic to the cloud firewall.


<div style="text-align: center">
<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8ae004614776bb0ed79b9e84b5cd96fa.png" /></div>


<span id="72620f0c"></span>
### Create NAT firewall


1. Log in to [cloud firewall console](https://console.byteplus.com/firewall/overview), in the left navigation bar, click **firewall switch**.

2. On the **firewall switch** page, click **NAT firewall**.

3. Select the NAT gateway that needs protection in the table below and click 【**Create Cloud Firewall**】. When creating the firewall, the creation conditions for the NAT gateway will be checked, and the following conditions must be met to create a cloud firewall.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The VPC subnet where the NAT gateway is located cannot contain any other service resources.</div>


* <div data-tips="true" data-tips-type="tip">The route table of the VPC subnet where the NAT gateway is located cannot contain other task service subnets.</div>


* <div data-tips="true" data-tips-type="tip">The route table of the subnet where the NAT gateway is located cannot be a system route table; it must be a custom route table.</div>


4. After passing the checks, click next to configure the firewall creation.

   
   |**Parameter** |**Note** |**Sample values** |
   |---|---|---|
   |Firewall name |Customize the NTA firewall name based on actual servic needs, used to identify the NAT firewall instance. |Development firewall |
   |Protection bandwidth specifications |You need to allocate protection bandwidth for this NAT firewall based on the actual service traffic size. When the service traffic bandwidth exceeds the protection bandwidth, the cloud firewall will send SMS, email, and onsite message alert notifications. |200Mbps |
   |Firewall subnet segment |Configure the subnet segment for the NAT firewall, the suggested mask for the subnet segment is 29 bits. |192.168.10.0/29 |
   |Name of the project to which the domain belongs. |Select the project that the NAT firewall belongs to.<br><br><br>* If you select "All Resources" in the top navigation bar before entering the creation page, you can pull down to choose an existing project.<br><br>* If you select the target project in the top navigation bar before entering the creation page, only the target project can be selected. |default (default item) |
   |Label |Add one or more user tags as needed for the firewall. Tags consist of two parts: tag key (Key) and tag value (Value), used to mark and classify the public NAT gateways. Click **Add Tag** to add multiple tags; you can add up to 20 tags at the same time. |Tag key: cfw\-key\nTag value: cfw\-test |
   


<span id="5e01e6f0"></span>
### NAT Firewall Drainage Configuration

The architecture diagram of the cloud firewall drainage is shown below, and the entire process of the service subnet accessing the NAT gateway is as follows.


1. The service subnet forwards the request traffic to the cloud firewall for inspection: service ** Subnet** \-\> NTA Firewall.

2. The cloud firewall forwards the inspected traffic to the NAT gateway: NAT Firewall \-\> **NAT Gateway**.

3. The NAT gateway forwards the response traffic to the cloud firewall for inspection: **NAT Gateway** \-\> NAT Firewall.

4. The cloud firewall forwards the inspected traffic to the service subnet: NAT  Firewall \-\> service ** Subnet**.


<div style="text-align: center">
<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8df90d3db3b915f51efb2c83743db31b.png" /></div>


&nbsp;

<span id="4f4d74aa"></span>
## Best practices:

[Private IP ](https://docs.byteplus.com/en/docs/6516/1338062)[outbound](https://docs.byteplus.com/en/docs/6516/1338062)[ traffic access control](https://docs.byteplus.com/en/docs/cloud_firewall/Private_network_IP_outbound_traffic_access_control)

[Private IP inbound traffic access control](https://docs.byteplus.com/en/docs/6516/1338061)
