---
title: "Creating a Direct Connect Gateway"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Creating-a-Direct-Connect-gateway"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

A Direct Connect (DC) Gateway serves as an ingress to enable mutual access between the data center and the VPC. This topic describes how to quickly create a DC Gateway with basic functionality.​​

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway).

2. In the top menu bar, select the region: China (Beijing).

3. Click **Create DC Gateway** to open the **Create DC Gateway** dialog box for configuration.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Regions |Select the region where the DC Gateway is located. This must match the region of the associated DC Connection. |China (Beijing) |
   |ASN |Set an ASN for the DC Gateway. In this demonstration, the ASN can remain as the default value 137718, which is the BytePlus ASN. No modification is required here. |137718 |
   |IPv6 |Enable IPv6: Disabled by default. |Disable |
   |Affiliated project |Select the project to which the new DC Gateway belongs. |default |
   |Agreement |Follow the console guidance to review and accept Legal. |Check |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This example demonstrates only example values for required parameters. For more parameter details, see <a href="https://docs.byteplus.com/en/docs/directconnect/Creating-a-Direct-Connect-gateway-1">Creating a Direct Connect Gateway</a>. Example values are for reference only and have no practical significance.   </div>
   

4. Click **Buy now** to complete the action.

5. Click **Go to console** to return to the Direct Connect Gateway console.

   You can view the newly created dcgw\-123 in the Direct Connect Gateway list. At this point, the Direct Connect Connection DAS123_port308_conn and the dcgw\-123 have been successfully requested.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next


* [Creating a Virtual Interface](https://docs.byteplus.com/en/docs/directconnect/Creating-a-virtual-interface)

* [Attaching a network instance](https://docs.byteplus.com/en/docs/directconnect/Loading-a-network-instance)

* [Configure on-premises routing and test connectivity](https://docs.byteplus.com/en/docs/directconnect/Configuring-a-local-route-and-testing-connectivity)
