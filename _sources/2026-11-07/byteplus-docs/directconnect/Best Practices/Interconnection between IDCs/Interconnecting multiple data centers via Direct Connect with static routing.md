---
title: "Interconnecting multiple data centers via Direct Connect with static routing"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Best-Practices-10"
---

This section describes how to implement interconnection between different on\-premises data centers via Direct Connect (DC) with static routing.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The feature of multi\-data center interconnection via Direct Connect is currently in the beta stage. If you need a trial, please contact your account manager.

* All data centers to be interconnected have available DC Connections. For procedure, see [Creating a Direct Connect Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1).

* All data centers to be interconnected must have gateway devices supporting static routing.


<span id=".5pON5L2c6ZmQ5Yi2"></span>
## Limits

Data centers intended for interconnection must have non\-overlapping CIDR blocks.

<span id=".5pON5L2c6IOM5pmv"></span>
## Background

A large enterprise has on\-premises data centers in both Beijing and Shanghai, which can be connected to BytePlus via DC. Then adding DC Gateways for the two DCs to the same Cloud Enterprise Network (CEN) enables network interconnection between the two data centers across regions.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5o6l5YWl54mp55CG5LiT57q_"></span>
### Step 1: Create a DC Connection

Deploy DC Connections in China (Beijing) and China (Shanghai) to connect respective data centers to BytePlus. For procedure, see [Creating a Direct Connect Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1). In this example, DAS\-246\-3_port1330\-conn is the DC Connection in China (Beijing) and DAS\-246\-2_port1320\-conn is the DC Connection in China (Shanghai).

<span id=".5q2l6aqk5LqM77ya5Yib5bu65LiT57q_572R5YWz"></span>
### Step 2: Create a DC Gateway


1. Log in to [the Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway).

2. Click **Create DC Gateway** to create a DC Gateway for the Beijing data center (IDC1) with the following configuration.

   
   |Parameter |Description |Value |
   |---|---|---|
   |Regions |Select the region where the DC Gateway is deployed. It must match the region of the DC Connection. |China (Beijing) |
   |Name |Set a name for the DC Gateway. |DCGW1 |
   |ASN |Set an ASN for the DC Gateway. The ASN of the DC Gateway applies only to BGP routing. Keep the default (137718) for static routing. |137718 |
   |IPv6 |Enable IPv6 as needed. |Disable |
   |Project |Select the project to which the new DC Gateway belongs. |Project\-test01 |
   |Agreement |Follow the console guidance to review and accept the legal terms. |Check |
   

3. After configuration, click **Create** to complete the creation.

4. Click **Go to console** to return to the Direct Connect Gateway console. You can view the new DC Gateway (DCGW1) in the DC Gateway list.

5. Repeat steps 2\-4 to create a DC Gateway for the Shanghai data center (IDC2), using the parameter values listed in the table below.

   
   |Parameter |Description |Value |
   |---|---|---|
   |Regions |Select the region where the DC Gateway is deployed. It must match the region of the DC Connection. |China (Shanghai) |
   |Name |Set a name for the DC Gateway. |DCGW2 |
   |ASN |Set an ASN for the DC Gateway. The ASN of the DC Gateway applies only to BGP routing. Keep the default (137718) for static routing. |137718 |
   |IPv6 |Enable IPv6 as needed. |Disabled |
   |Project |Select the project to which the new DC Gateway belongs. |Project\-test02 |
   |Agreement |Follow the console guidance to review and accept the legal terms. |Check |
   


<span id=".5q2l6aqk5LiJ77ya5Yib5bu66Jma5ouf5o6l5Y-j"></span>
### Step 3: Create a Virtual Interface


1. Log in to [the DC Virtual Interface console](https://console.byteplus.com/dc/VirtualInterface).

2. Click **Create DC Virtual Interface**.

3. Configure the Virtual Interface based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Resource ownership |Select the account to which the Virtual Interfacelongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The feature of creating a Shared Virtual Interface for another account is currently in the beta stage. If you need a trial, please contact your account manager.</div><br> |My account |
   |Regions |Select the region where the Virtual Interface is deployed. It must be the same as the region of the DC Connection and the DC Gateway. |China (Beijing) |
   |Name |Set a name for the nterface. |VIF\-01 |
   |DC Connection |Filter the DC Connection by project to associate with the Virtual Interface. |Project\-test01\|DAS\-246\-3_port1330\-conn |
   |DC Gateway |Filter the DC Gateway by project to associate with the Virtual Interface. |Project\-test01\|DCGW1 |
   |Bandwidth limit |Enable bandwidth limit as needed. |Disable |
   |**Interconnection information** |||
   |IPv4 interconnect IP |Set the IPv4 IP for interconnection.<br><br><br>* Cloud gateway peer IP: Set an IPv4 address and mask for the cloud DC gateway. You may customize the interconnect IP according to network planning, but confirm that the cloud gateway peer IP and your gateway peer IP are in the same CIDR block without duplication. Use a private IP address that does not conflict with cloud or on\-premises IP addresses.<br><br>* Your gateway peer IP: Set an IPv4 address and mask for the gateway on your on\-premises data center. You may customize the interconnect IP according to network planning, but confirm that the cloud gateway peer IP and your gateway peer IP are in the same CIDR block without duplication. Use a private IP address that does not conflict with cloud or on\-premises IP addresses. |* Cloud gateway IP: 10.0.0.1/30​​<br><br>* Your gateway IP: 10.0.0.2/30​​ |
   |IPv6 interconnect IP |Enable IPv6 IP for interconnection as needed. |Disable |
   |VLAN ID |Set a VLAN ID for connecting to the data center. Confirm that this VLAN ID is unoccupied. |10 |
   |**Routing information** |||
   |Route type |Support two route types: BGP and Static. This example uses static routes. |Static routes |
   |Detection method |Select a detection method to check the line health. |Disable |
   

4. Click **Create** to complete the creation of the Virtual Interface for IDC1.

5. Repeat steps 2\-4 to create a Virtual Interface for IDC2, using the parameter values listed in the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Resource ownership |Select the account to which the Virtual Interface belongs. |My account |
   |Regions |Select the region where the Virtual Interface is deployed. It must be the same as the region of the DC Connection and the DC Gateway. |China (Shanghai) |
   |Name |Set a name for the Virtual Interface. |VIF\-02 |
   |DC Connection |Filter the DC Connection by project to associate with the Virtual Interface. |Project\-test02\|DAS\-246\-2_port1320\-conn |
   |DC Gateway |Filter the DC Gateway by project to associate with the Virtual Interface. |Project\-test02\|DCGW2 |
   |Bandwidth limit |Enable bandwidth limit as needed. |Disable |
   |**Interconnection information** |||
   |IPv4 interconnect IP |Set the IPv4 IP for interconnection.<br><br><br>* Cloud gateway peer IP: Set an IPv4 address and mask for the cloud DC gateway.<br><br>* Your gateway peer IP: Set an IPv4 address and mask for the gateway on your on\-premises data center. |* Cloud gateway peer IP: 10.0.0.5/30<br><br>* Your gateway peer IP: 10.0.0.6/30 |
   |IPv6 interconnect IP |Enable IPv6 IP for interconnection as needed. |Disable |
   |VLAN ID |Set a VLAN ID for connecting to the data center. Confirm that this VLAN ID is unoccupied. |10 |
   |**Routing information** |||
   |Route type |Support two route types: BGP and Static. This example uses static routes. |Static routes |
   |Detection method |Select a detection method to check the line health. |Disabled |
   


<span id=".5q2l6aqk5Zub77ya5re75Yqg6Z2Z5oCB6Lev55Sx"></span>
### Step 4: Add a static route


1. In the gateway list of [the Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway), click the name of the target DC Gateway  **(DCGW1)** .

2. Select the **Routing Information** tab.

3. Click **Add static route entry**, and configure the route.

   
   |Parameter |Value |
   |---|---|
   |Network type |IPv4 |
   |Destination CIDR |The destination CIDR block is the CIDR block of IDC1. In this example, it is 192.168.0.0/24. |
   |Next Hop type |Direct Connect Virtual Interface |
   |Next Hop |VIF\-01 |
   

4. Click **Create** to complete configuration.

5. Repeat steps 1\-4 to add a static route for DCGW2, using the parameter values listed in the table below.

   
   |Parameter |Value |
   |---|---|
   |Network type |IPv4 |
   |Destination CIDR |The destination CIDR block is the CIDR block of IDC2. In this example, it is 172.16.0.0/24. |
   |Next Hop type |Virtual Interface |
   |Next Hop |VIF\-02 |
   


<span id=".5q2l6aqk5LqU77ya5Yib5bu65LqR5LyB5Lia572R"></span>
### Step 5: Create a Cloud Enterprise Network


1. Log in to [the CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. Click **Create CEN**.

3. Configure the CEN based on the table below, and load the DC Gateway (DCGW1).

   
   |Parameter |Value |
   |---|---|
   |**Basic information** ||
   |Name |Cen\-connect |
   |**Network Instances** ||
   |Attaching a network instance |Enable |
   |Regions |China (Beijing) |
   |Instance type |DC Gateway |
   |Network Instances |DCGW1 |
   |**More information** ||
   |Project |Project\-test |
   

4. Click **Create** to complete the action.


<span id=".5q2l6aqk5YWt77ya5LqR5LyB5Lia572R5Yqg6L295LiT57q_572R5YWz"></span>
### Step 6: Load the DC Gateway to the CEN


1. In the instance list of [the CEN console](https://console.byteplus.com/cen/EnterpriseNetwork), click the name of the target instance  **(Cen\-connect)** .

2. In the **Network Instances** tab, click **Attach Network Instance**.

3. The Attach Network Instance window pops up. Configure the information of the DC Gateway instance to be loaded.

   
   |Parameter |Value |
   |---|---|
   |Account |My account |
   |Regions |China (Shanghai) |
   |Instance type |DC Gateway |
   |Network Instances |DCGW2 |
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you also need to connect with a Virtual Private Cloud (VPC), just attach your target VPC to the same CEN.</div>


<span id=".5q2l6aqk5LiD77ya6LSt5Lmw5bim5a695YyF5bm25YiG6YWN5Z-f6Ze05bim5a69"></span>
### Step 7: Purchase a bandwidth package and allocate inter\-region bandwidth.

In this scenario, to implement intercommunication between data centers across regions, you need to purchase a CEN bandwidth package for cross\-region access. If connecting data centers in the same region, you can skip this step.


1. Log in to [the CEN console](https://console.byteplus.com/cen/EnterpriseNetwork) and click **Bandwidth Package** in the left\-side navigation pane.

2. Click **Create BWP**, and configure the bandwidth package based on the table below.

   
   |Parameter |Value |
   |---|---|
   |**Basic information** ||
   |Billing method |Subscription |
   |Name |Package\-cen |
   |**Bandwidth configuration** ||
   |Cloud Enterprise Network |Project\-test\|Cen\-connect |
   |Interoperability area |China \- China |
   |Bandwidth |300Mbps |
   |Duration |1 month |
   |**More information** ||
   |Project |Project\-test |
   

3. Click **Confirm order**, and follow the console guidance to review and accept the legal terms.

4. Click **Buy now** to complete the bandwidth package creation.

5. In the left\-side navigation pane, click **CEN Instances**.

6. Click the CEN Instance name  **(Cen\-connect)** , and then click the **Inter\-region bandwidth** tab in the details page.

7. In the **Inter\-region bandwidth** section, click **Associate BWP**, select the target bandwidth package (Package\-cen), and click **Associate**.

8. Click **Allocate inter\-region bandwidth**. Allocate bandwidth across regions based on the table below.

   
   |Parameter |Value |
   |---|---|
   |Bandwidth package |Package\-cen |
   |Interconnected regions |China (Beijing) \- China (Shanghai) |
   |Bandwidth |200Mbps |
   

9. Click **Create** to complete configuration.


Now, you have completed all the necessary configuration steps in the console.

<span id=".5q2l6aqk5YWr77ya6YWN572u5pys5ZywSURD6Lev55Sx"></span>
### Step 8: Configure routing for the data center

Configure routes in both on\-premises IDC1 and IDC2 for communication with the interconnected VPC. For procedure, see [Configure routing for a data center](https://docs.byteplus.com/en/docs/directconnect/Best-Practices-3#.5q2l6aqk5YWt77ya6YWN572u5pys5ZywSURD6Lev55Sx).

<span id=".5q2l6aqk5Lmd77ya5rWL6K-V572R57uc6IGU6YCa5oCn"></span>
### Step 9: Test network connectivity


1. Log in to any server within 192.168.0.0/24 of IDC1.

2. Ping any IP address within 172.168.0.0/24 of IDC2. A successful response indicates that network connectivity from IDC1 to IDC2 is established.

   ```Plain Text
   ping 172.168.0.21
   ```
   

3. Similarly, ping the IP address of IDC1 in any server of IDC2. A successful response indicates that network connectivity from IDC2 to IDC1 is established. The interconnectivity between IDC1 and IDC2 is achieved.
