---
title: "Creating a customer gateway"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Creating-a-customer-gateway1"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

After creating the VPN gateway, you also need to create a customer gateway. The customer gateway is a collection and abstraction of information from your on\-premises gateway side. Through the customer gateway, you can register your on\-premises gateway's information into the VPC. A single customer gateway can connect to multiple VPN gateways.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Customer Gateway console](https://console.byteplus.com/vpn/vpnClient). 

2. In the top menu bar, select the target region and project to which the resource belongs.

3. Click **Create Customer Gateway**, and configure the customer gateway based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Regions |Defaults to the region selected in the top navigation bar. Resources are isolated between regions. Selecting a region closer to your users can reduce latency and improve access speed. |China (Beijing) |
   |Name |Set the name for the customer gateway. |CGW\-sj2x |
   |IP address type |Select the IP address type for the Customer Gateway. Both IPv4 and IPv6 addresses are supported. In IPv6 communication scenarios, please ensure that all link configurations support the IPv6 protocol type.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The IPv6 address type for customer gateway is currently in Beta stage. If you need a trial, please contact your account manager.</div><br> |IPv4 |
   |IP Address |Enter the static public IP address of your on\-premises data center gateway or the Elastic IP Address (EIP) of the peer VPC's VPN gateway.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If this EIP is implemented through NAT, you must enable the NAT traversal function when <a href="https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1">creating an IPsec\-VPN connection</a>, and simultaneously configure NAT traversal on the local VPN gateway device.</div><br> |22.XX.XX.16 |
   |BGP ASN |Set the ASN (Autonomous System Number) for the customer gateway. If the IPsec connection uses dynamic routing propagation mode, you need to configure the customer gateway BGP ASN. If the IPsec connection uses the static routing propagation mode, configuring the customer gateway BGP ASN is not required.<br><br><br>* The customer gateway BGP ASN cannot be modified after configuration.<br><br>* The valid range for the customer gateway BGP ASN is: 1 to 4294967294. The values 137718, 65535, and 150436 are unavailable.<br><br>* If this customer gateway is later used to create an IPsec connection with dynamic routing propagation mode, ensure that the ASN of the customer gateway is different from the ASN of the associated VPN gateway or transit router. |65000 |
   |Affiliated Project |Select the project to which the new customer gateway belongs. A project refers to a task in your daily work. You can create multiple projects under the same account and create or purchase cloud resources for each project. Cloud resources cannot be shared between different projects.<br><br><br>* If no projects are available, click **Create project** on the right to create a new project.<br><br>* After a customer gateway is added to a project, you can move it out of the project based on actual business needs. For details, see Project resource management. |default |
   |**Advanced option** |||
   |Tags |A tag consists of a Key and a Value, and can be used to categorize and search for customer gateways. [Learn more](https://docs.byteplus.com/en/docs/vpn/Tag-management)<br><br><br>* Click **Add tag** to add multiple tags as needed. A single operation allows you to add up to 20 tags, and an individual customer gateway can have a maximum of 50 tags.<br><br>* For a single Customer Gateway, the Tag Keys for multiple tags cannot be duplicated, and each Tag Key can only have one Tag Value.<br><br>* The Key and the Value are case\-sensitive. For example, the Key=tag and the Key=Tag are two different Keys. |key:test |
   

5. Click **Create** to complete configuration.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

[Create an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1): Create an IPsec\-VPN connection and configure Phase 1 and Phase 2 authentication information for the IPsec communication tunnel.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateCustomerGateway](https://docs.byteplus.com/en/docs/vpn/CreateCustomerGateway): Create a customer gateway.
