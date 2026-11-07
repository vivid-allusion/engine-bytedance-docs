---
title: "Quick start"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Quick-start"
---

<span id=".6YCJ5oup5o6l5YWl54K5"></span>
## Scenarios

This topic describes how to quickly build a Direct Connect (DC) with BGP route for network connectivity between a Virtual Private Cloud (VPC) and an on\-premises data center.

<span id=".6YCJ5oup5o6l5YWl54K5"></span>
## Select an access point

An access point is the geographical location where a DC Connection connects to cloud services. BytePlus access points support DC Connections from multiple line operators. Confirm your access point before applying for a DC Connection. For more information, see [Direct Connect access points](https://docs.byteplus.com/en/docs/directconnect/Direct-Connect-access-point).

You can select the most suitable access point from the following aspects.


1. Region of the access point

   When selecting an access point, follow the "proximity principle"; that is, select the access point which is closest to your data center. The closer your data center is to the access point, the lower the network latency. For example, if your local data center is in Beijing, you should select the access point in China (Beijing).

2. Line operator

   Different access points may support different line operators. After confirming the region of the access point, consult your BytePlus account manager to learn which line operators each access point supports in that region. Select an appropriate line operator by comprehensively considering all aspects, such as prices and network performance.

3. Port Spec

   Specify your port specification. Different access points support different specifications. Port Spec determines the port rate. Default options are single\-mode optical ports of 1 Gbps and 10 Gbps. BytePlus includes one compatible optical module for your cloud port at no additional charge. For further details, please consult your BytePlus account manager.

   * BytePlus provides free optical modules of 1 Gbps and 10 Gbps supporting transmission distances of up to 10 km.

   * For optical modules of 40 Gbps, 100 Gbps, and 400 Gbps or optical modules of 1 Gbps and 10 Gbps supporting transmission distances over 10 km, you need to purchase them separately.


<span id=".5o6l5YWl5YmN5YeG5aSH"></span>
## Preparations before access

Complete the following preparations before using DC.


* Complete real\-name authentication for your account. The total value of your available balance and coupons applicable to DC must be no less than USD 0.

* Create a Virtual Private Cloud (VPC) and subnets for communication. For specific procedure, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC). The VPC in this example is VPC\-123 (CIDR block: 192.168.1.0/24).

* Create a Cloud Enterprise Network (CEN) and load the created VPC. For specific procedure, see [Creating a CEN instance](https://docs.byteplus.com/en/docs/cen/CEN-instances-01). The CEN in this example is CEN\-123, with VPC\-123 loaded.


<span id=".6YWN572u5LiT57q_6L-e5o6l"></span>
## Configure a DC connection


1. [Create a DC Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection).

2. [Create a DC Gateway](https://docs.byteplus.com/en/docs/directconnect/Creating-a-Direct-Connect-gateway).

3. [Create a Virtual Interface](https://docs.byteplus.com/en/docs/directconnect/Creating-a-virtual-interface).

4. [Load a network instance](https://docs.byteplus.com/en/docs/directconnect/Loading-a-network-instance).

5. [Configure on-premises routing and test connectivity](https://docs.byteplus.com/en/docs/directconnect/Configuring-a-local-route-and-testing-connectivity).
