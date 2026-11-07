---
title: "Attaching a network instance"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Loading-a-network-instance"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

You can attach the network instances, namely the Virtual Private Cloud (VPC) and Direct Connect Gateway, to the same Cloud Enterprise Network (CEN) instance to enable network interconnection between the VPC and the Direct Connect Gateway.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A CEN instance named CEN\-123 has been created, and the target VPC for communication, VPC\-123, has been attached to it. For specific operations, see [Creating a CEN instance](https://docs.byteplus.com/en/docs/cen/CEN-instances-01).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway).

2. In the top menu bar, select the region: China (Beijing).

3. In the left\-side navigation pane, select Quick Link \> CEN.

4. Click the name of the created CEN instance.

5. On the details page of the CEN instance, select **Network Instances** tab.

6. Click **Attach Network Instance**. Configure the network instance by referring to the following table.

   
   |Parameters |Description |Sample value |
   |---|---|---|
   |Account |Select the account to which the target Direct Connect Gateway instance belongs. |My account |
   |Regions |Select the region to which the target Direct Connect Gateway instance belongs. |China (Beijing) |
   |Instance type |Select the DC Gateway type. |DC Gateway |
   |Network Instances |Select the created DC Gateway. |dcgw\-123 (dcg\-2feqv4p59gp68s9\*\*\*\*) |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Example values are for reference only and have no practical significance.   </div>
   

7. Click **Install** to complete the action.

   At this point, the Direct Connect Gateway dcgw\-123 can communicate with the VPC\-123 via the CEN\-123.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next


* [Configure on-premises routing and test connectivity](https://docs.byteplus.com/en/docs/directconnect/Configuring-a-local-route-and-testing-connectivity)
