---
title: "What is Direct Connect"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/What-is-Direct-Connect"
---

<span id=".566A5LuL"></span>
## Overview

Direct Connect (DC) is an exclusive, stable, secure, high\-speed, and low\-latency connection channel that links your on\-premises data center to a Virtual Private Cloud (VPC). Compared to common cloud access methods, such as Virtual Private Networks (VPNs), Elastic IP Addresses (EIPs), and Internet NAT gateways, DC offers high bandwidth, low latency, and enhanced privacy, supporting private network interconnection between the on\-premises data centers and multiple VPCs.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1244e68f9c455438b076ea8921578fa2.png) </span>

<span id=".5Z-65pys57uE5oiQ"></span>
## Basic components


|Component |Notes |
|---|---|
|Direct Connect Access Point |An access point is the geographical location where a DC Connection connects to cloud services. BytePlus access points support DC Connections from multiple line operators. |
|DC Connection |A DC Connection is a private physical link that connects your on\-premises data center to a BytePlus access point. Physically, it is implemented as a fiber optic cable. |
|DC Gateway |A DC Gateway is an access router that acts as the logical access gateway for a DC Connection to access a VPC. It requires no physical hardware on the cloud platform. When using DC, you can connect multiple DC Connections through one DC Gateway. |
|DC Virtual Interface |A DC Virtual Interface is a logical interface created on a DC Connection. It links the DC connection to a DC gateway, enabling your on\-premises data center to communicate with multiple VPCs. Supports both static and BGP routing modes. |


<span id="3P9xlwiU"></span>
## Benefits


* **High reliability**: Supports multi\-line disaster recovery across regions, and capabilities of automatic fault detection and link auto\-switching, with an SLA up to 99.95%, ensuring stable communication.

* **High security**: The DC Connection is exclusively owned by the user and transmits data between the cloud and the on\-premises through a private network, enhancing security and meeting the strict requirements of government, financial, and other industries.

* **Low latency**: Achieve data transmission via a private network with fixed routing paths, resulting in low and stable transmission latency.

* **Strong scalability**: Based on the Cloud Enterprise Network (CEN), you can associate multiple VPCs and multiple IDCs at any time with immediate effect, enabling flexible and scalable hybrid cloud deployment.

* **High bandwidth**: A single DC connection supports bandwidth of up to 400 Gbps. You can add multiple connections to achieve higher overall bandwidth, thereby enhancing transmission performance.


<span id=".6K6_6Zeu5pa55byP"></span>
## Access method comparison


|Comparison |Dedicated Line |Shared Line |
|---|---|---|
|Connection solution |A Dedicated line offers an exclusive port from BytePlus, establishing an exclusive, stable, secure, high\-speed, and low\-latency connection channel between your data center and a VPC. |A Shared line directly uses a DC Connection of a line operator that is connected to the BytePlus access point. The tenant only needs to connect the network between the data center and the line operator's DC access point. Share the DC Connection created by the line operator to use DC capabilities.<br><br> |
|Port type |Exclusive port |Shared port |
|Overall construction scope |Requires you contact a line operator to implement a physical link from your data center to the BytePlus access point. |Only requires connecting the network between your data center and the DC access point of the line operator. |
|Overall construction period |2\-3 months |Within 1 month |
|BytePlus billing items |* Port occupancy fee: Charge by the port specification of the Delicated line.<br><br>* Outbound traffic fee: Charge by the total traffic from the cloud egressing through the DC Gateway. |* Port occupancy fee: Charge the Shared line's actual user (tenant) based on the port specification of the Shared line.<br><br>* Outbound traffic fee: Charge the Shared line's actual user (tenant) based on the total traffic from the cloud egressing through the DC Gateway. |
|Recommended bandwidth |1 Gbps\-400 Gbps |<1 Gbps |


<span id=".6K6_6Zeu5pa55byP"></span>
## Access method


|Access methods |Notes |
|---|---|
|Console access |You can log in to [the Direct Connect Connection console](https://console.byteplus.com/dc/PhysicalConnection) to manage directly through the web page. |
|API access |You can use either HTTP or HTTPS to request online API calls or custom development. For details, see [API reference](https://docs.byteplus.com/en/docs/directconnect/Overview-2). |
|SDK access |You can use the SDK to call APIs more conveniently for creating and managing resources. For details, see [SDK Overview](https://docs.byteplus.com/en/docs/directconnect/DC_SDK_Overview). |


<span id="pqZ1c4Xy"></span>
##
