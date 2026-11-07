---
title: "Introduction to VPC Boundary Firewall"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Enabling-VPC-firewall"
---

<span id="81906d6b"></span>
## What is VPC Boundary Firewall? 

The VPC Boundary Firewall supports access control for traffic between private networks (VPCs) and between VPCs and local data centers (via VPN or dedicated line), as well as between VPCs and third\-party clouds (via VPN or dedicated line gateway), ensuring business isolation and effectively blocking unauthorized access between internal networks.

<span id="fb15ecad"></span>
## VPC Boundary Firewall Traffic Redirection Principle

The cloud firewall directs traffic through a customized routing approach using TR transfer routers. The working principle of the cloud firewall's traffic redirection is introduced using the following scenario as an example.

> A company has deployed a development VPC (192.168.1.0/24, 192.168.2.0/24) and a testing VPC (172.16.1.0/24, 172.16.2.0/24), and these VPCs have been bi\-directionally connected through TR transfer routers. Now, it is necessary to redirect traffic between VPCs to the cloud firewall.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b2297ad16952be3ba83f293599d667c8.png) </span>

<span id="de35500c"></span>
### Firewall Traffic Redirection Configuration


1. Log in to [Cloud Firewall Console](https://console.byteplus.com/firewall/overview), and in the left navigation bar, click **Firewall Switch**.

2. On the **Firewall Switch** page, click **VPC Boundary Firewall**.

3. Select the transfer router that needs protection from the table below, click 【**New Cloud Firewall**】, and select 【**Automatic Redirection**】 in the redirection mode.

4. Create firewall configuration.

   
   |**Parameter** |**Note** |**Example of value** |
   |---|---|---|
   |Firewall name |Customize the VPC firewall name based on actual business conditions for identifying VPC firewall instances. |Development \- Testing \- Business Firewall |
   |Protection bandwidth specifications |You need to allocate protection bandwidth for this VPC firewall based on the actual business traffic size. When the business traffic bandwidth exceeds the protection bandwidth, the cloud firewall will send SMS, email, and site message alert notifications. |200Mbps |
   |Firewall VPC subnet |* Configure the VPC network segment and subnet segment where the VPC firewall is located. The firewall subnet is used to deploy firewall instances. The larger the traffic, the more instances deployed and the more IPs occupied.<br><br>* It is recommended that the mask of the three subnets of the cloud firewall VPC be less than or equal to 28 bits and not conflict with the planned network segments. The cloud firewall subnet is used for traffic diversion and backup disaster recovery. |192.168.10.0/24 |
   |VPC subnet 1 network segment ||192.168.10.16/28 |
   |VPC subnet 2 network segment ||192.168.0.32/28 |
   |VPC subnet 3 segment ||192.168.0.48/28 |
   |Project |Select the project to which the VPC firewall belongs.<br><br><br>* If you select "All resources" of the account in the top navigation bar before entering the creation page, you can choose from existing projects.<br><br>* If you select the target project in the top navigation bar before entering the creation page, only the target project can be selected. |default (default project) |
   |Label |Add one or more user tags as needed for the firewall. \nTags consist of two parts: tag key (Key) and tag value (Value), used to mark and classify public NAT gateways. Click **Add tag** to add multiple tags, with a maximum of 20 tags added simultaneously. |Label key: cfw\-key\nLabel value: cfw\-test |
   

5. Configure diversion scenarios.

   
   |**Traffic diversion scenario name** |Define the name of the steering scenario. This name is used to label the type of steering scenario, and it is recommended that you enter a meaningful name based on the actual business situation. |Business VPC traffic diversion |
   |---|---|---|
   |**Flow diversion scenario selection** |Select the diversion scenario type based on the protection requirements of network instances (VPC, dedicated line, VPN).<br><br><br>* **Point to point**: Traffic between two network instances is controlled by the cloud firewall. Suitable for simple network topology environments.<br><br>* **Point to multipoint**: Traffic between one network instance and multiple network instances is controlled by the cloud firewall. Applicable to star topology network environments; traffic between the left network instance and the right multiple instances can go through the cloud firewall, while traffic between the right multiple instances does not go through the cloud firewall.<br><br>* **Multi\-point interconnection**: Traffic between multiple network instances is controlled by the cloud firewall. Applicable to **FullMesh** mesh network topology environments. |Point to point |
   |**Instance selection** |Configure the network instances that need to be redirected |Develop VPC\nTest VPC |
   


<span id="4ddc6bc5"></span>
### Introduction to firewall diversion routing

The cloud firewall diversion architecture diagram is shown below, **the development VPC** accessing **the testing VPC** is as follows.


1. The development VPC forwards request traffic to the cloud firewall for inspection: **the development VPC** \-\> TR transit router \-\> VPC boundary firewall.

2. The cloud firewall forwards the inspected traffic to the testing VPC: VPC boundary firewall \-\> TR transit router \-\> **the testing VPC**.

3. The testing VPC forwards response traffic to the cloud firewall for inspection: **the testing VPC** \-\> TR transit router \-\> VPC boundary firewall.

4. The cloud firewall forwards the inspected traffic to the development VPC: VPC boundary firewall \-\> TR transit router \-\> **the development VPC**.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_444754c0537c70b0568789842dadac97.png) </span>


<span id="57d470f7"></span>
## Best practices:


* [Access control for traffic between VPCs (automatic diversion configuration)](https://docs.byteplus.com/en/docs/cloud_firewall/Access_control_for_traffic_between_VPCs)

* [Traffic access control between VPC and dedicated line (automatic steering configuration)](https://docs.byteplus.com/en/docs/cloud_firewall/Access_control_for_traffic_between_a_VPC_and_an_instance)

* [Traffic access control between VPC and VPN (manual steering configuration)](https://docs.byteplus.com/en/docs/cloud_firewall/Access_control_for_traffic_between_a_VPC_and_a_VPN)

* [Traffic access control between VPN and dedicated line (manual steering configuration)](https://docs.byteplus.com/en/docs/cloud_firewall/Access_control_for_traffic_between_a_VPN_and_an_instance)
