---
title: "Associating a cloud resource"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Associating-Cloud-Resources-with-an-EIP"
---

After applying for an Elastic IP Address (EIP) successfully, you can associate the EIP with Elastic Compute Service (ECS), Classic Load Balancer (CLB), Internet NAT Gateway, secondary network interface (ENI), High\-Availability Virtual IP Address (HAVIP), and other cloud resources to meet diverse internet requirements. This topic describes how to associate an EIP with a cloud resource.

<span id=".5pON5L2c6K-05piO"></span>
## Instructions

After associating an EIP with an ECS instance, their relationship is as follows:


* The EIP acts as a sub\-resource of the ECS instance, just like the system disk, data disk, and primary network interface. If the ECS instance changes its project, the EIP's project changes accordingly.

* When renewing or unsubscribing a subscription EIP, you can choose to renew or unsubscribe the associated subscription ECS instance together, and vice versa.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [EIP console](https://console.byteplus.com/eip/eips).

2. In the top menu bar, select the region and project of your target EIP.

3. In the EIP list, click **Associate** to the right of the target EIP.

4. Supported cloud resources: ECS, CLB, NAT Gateway, secondary network interface, IP address, and HAVIP. Select a cloud resource and configure relevant parameters based on the table below.

   
   <Tabs>
   <Tab zoneid="a2zFMkZZ4T" title="ECS, Secondary ENI">
   <TabTitle>ECS, Secondary ENI</TabTitle>
   
   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Instance type |Select an ECS or a secondary network interface. |ECS |
   |Project |Select the project to which the target cloud resource belongs. |default |
   |EIP Direct |Specify whether to enable EIP Direct.<br><br><br>* Check: Enable EIP Direct, allowing viewing the EIP on the Elastic Compute Service's network interface. After attaching an EIP to a cloud resource, you also need to [configure and run the EIP Direct script](https://docs.byteplus.com/en/docs/eip/Set-up-EIP-Pass-through-Mode#.5byA5ZCv55u06YCa) on the Elastic Compute Service.<br><br>* Uncheck: Do not enable EIP Direct at this time. After attaching an EIP to a cloud resource, you can [enable EIP Direct in the console](https://docs.byteplus.com/en/docs/eip/Set-up-EIP-Pass-through-Mode) based on your actual business needs.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The EIP Direct feature is in the beta stage. To request a trial, please contact your account manager.</div><br> |Unchecked |
   |Release request |Check to release with the instance as needed. This parameter applies only when a Pay\-as\-you\-go EIP is associated with an ECS.<br><br>If checked, the following applies:<br><br><br>* When the system automatically recovers (24 hours after unsubscription, expiration recovery, or arrears recovery) or when calling [DeleteInstance](https://docs.byteplus.com/en/docs/ecs/DeleteInstance) to release the ECS, the EIP is released together with it.<br><br>* When manually releasing the ECS in the console, the release of EIP is subject to your setting. |Unchecked |
   |Select instance |Select the cloud resource to be associated.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the instance type is <strong>secondary network interface</strong> and EIP Direct is enabled, only secondary network interfaces already associated with Elastic Compute Service can be selected.</div><br> |CS\-ik9\*\*\*\* |
   
   
   
   
   
   </Tab>
   <Tab zoneid="ANDG7bXndG" title="CLB, NAT Gateway, HAVIP">
   <TabTitle>CLB, NAT Gateway, HAVIP</TabTitle>
   
   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Instance type |Select a Classic Load Balancer, NAT Gateway, or High\-Availability Virtual IP Address. |Classic Load Balancer |
   |Project |Select the project to which the target cloud resource belongs. |default |
   |Select instance |Select the cloud resource to be associated. |CLB\-pr2\*\*\*\* |
   
   
   
   
   
   </Tab>
   <Tab zoneid="P0E8Yhe1nX" title="IP">
   <TabTitle>IP</TabTitle>
   
   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Instance type |Select an IP address.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The IP Address instance type is in the beta stage. To request a trial, please contact your account manager.</div><br> |IP |
   |Project |Select the project to which the target cloud resource belongs. |default |
   |VPC |Only Virtual Private Clouds with attached IPv4 gateways are supported. |VPC\-01 |
   |IP |Type in an IP Address.<br><br><br>* Currently, you can only type in the IPv4 address. The CIDR block of the IP address must have a route entry for internet access.<br><br>* You cannot associate an IP address with multiple EIPs that are associated with the same VPC.<br><br>* You cannot type in the IP addresses of an ECS's primary and secondary network interfaces that are associated with the EIP. |10.XX.XX.86 |
   
   
   
   
   
   </Tab>
   </Tabs>
   

5. Click **Associate** to complete the action.


<span id=".55u45YWz5pON5L2c"></span>
## Related actions


* After an ECS instance is assoicated with an EIP, see [Why can't an ECS instance still connect to Internet after associating an EIP](https://docs.byteplus.com/en/docs/eip/EIP-FAQs#.5Li65LuA5LmI5LqR5pyN5Yqh5Zmo5a6e5L6L57uR5a6a5YWs572RSVDku43nhLbml6Dms5Xov57mjqXkupLogZTnvZHvvJ8=) if it cannot access the internet.

* To associate EIPs with secondary private IPs of primary and secondary network interfaces, see [Network interface > Associate an EIP](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-an-EIP#.57uR5a6a5YWs572RSVA=).


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[AssociateEipAddress](https://docs.byteplus.com/en/docs/eip/AssociateEipAddress): Associate an EIP to a cloud resource.
