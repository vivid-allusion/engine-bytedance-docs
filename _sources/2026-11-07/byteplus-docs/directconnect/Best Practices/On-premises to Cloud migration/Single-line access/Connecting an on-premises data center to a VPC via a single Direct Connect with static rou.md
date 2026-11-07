---
title: "Connecting an on-premises data center to a VPC via a single Direct Connect with static routing"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Best-Practices-4"
---

The networks of the Virtual Private Cloud (VPC) and the on\-premises data center are isolated and cannot mutually communicate. This section describes how to achieve interconnection between a data center and Elastic Compute Service (ECS) within a VPC via Direct Connect (DC) using static routes.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created a VPC (named vpc) and its subnets. For procedure, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The subnet CIDR block of the VPC must not overlap or conflict with that of the data center. All existing route entries at the data center side must not conflict with subnet routes after being added to a DC Connection   </div>
   

* You have created an ECS instance within **vpc**. For procedure, see [Purchasing an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* The data center to be interconnected has gateway devices supporting static routes.


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

An enterprise wants its on\-premises data center to access an ECS within a VPC through Direct Connect.


* Data center configuration: The subnet CIDR block is 172.16.1.0/24, the interconnect IP is 10.0.0.2, and the IP address of an active server is 172.16.1.10.

* VPC configuration: The subnet CIDR block is 192.168.1.0/24, the interconnect IP is 10.0.0.1, and the private IP address of the ECS is 192.168.1.10.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5o6l5YWl54mp55CG5LiT57q_"></span>
### Step 1: Create a DC Connection

Activate one DC Connection. For procedure, see [Creating a Direct Connect Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1). In this example, the DC Connection used is DAS237_port101_conn under Project\-test in China (Beijing).

<span id=".5q2l6aqk5LqM77ya5Yib5bu65LiT57q_572R5YWz"></span>
### Step 2: Create a DC Gateway


1. Log in to [the Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway).

2. Click **Create DC Gateway** to create a DC Gateway with the following configuration.

   
   |Parameter |Description |Value |
   |---|---|---|
   |Regions |Select the region where the DC Gateway is deployed. It must match the region of the DC Connection. |China (Beijing) |
   |Name |Set a name for the DC Gateway. |dcg\-01 |
   |ASN |Set an ASN for the DC Gateway. This example does not require a custom ASN and directly uses the BytePlus ASN. |137718 |
   |IPv6 |Enable IPv6 as needed. |Disable |
   |Project |Select the project to which the new DC Gateway belongs. |Project\-test |
   |Agreement |Follow the console guidance to review and accept Legal. |Check |
   

3. Click **Buy now** to complete the action.

4. Click **Go to console** to return to the Direct Connect Gateway console. You can view the new DC Gateway (dcg\-01) in the DC Gateway list.


<span id=".5q2l6aqk5LiJ77ya5Yib5bu66Jma5ouf5o6l5Y-j"></span>
### Step 3: Create a Virtual Interface


1. Log in to [the DC Virtual Interface console](https://console.byteplus.com/dc/VirtualInterface).

2. In the top menu bar, select your target region.

3. Click **Create DC Virtual Interface**.

4. Configure the Virtual Interface based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Resource ownership |Select the account to which the Virtual Interface belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The feature of creating a Shared Virtual Interface for another account is currently in the beta stage. If you need a trial, please contact your account manager.</div><br> |My account |
   |Regions |Select the region where the Virtual Interface is deployed. It must be the same as the region of the DC Connection and the DC Gateway. |China (Beijing) |
   |Name |Set a name for the Ethernet Virtual Interface. |VIF\-uad8h |
   |DC Connection |Filter the DC Connection by project to associate with the Virtual Interface. |Project\-test\|DAS237_port101_conn |
   |Direct Connect Gateway |Filter the DC Gateway by project to associate with the Virtual Interface. |Project\-test\|dcg\-01 |
   |Bandwidth limit |Enable bandwidth limit as needed. |Disable |
   |**Interconnection information** |||
   |IPv4 interconnect IP |Set the IPv4 IP for interconnection.<br><br><br>* Cloud gateway peer IP: Set an IPv4 address and mask for the cloud DC gateway. You may customize the interconnect IP according to network planning, but confirm that the cloud gateway peer IP and your gateway peer IP are in the same CIDR block without duplication. Use a private IP address that does not conflict with cloud or on\-premises IP addresses.<br><br>* Your gateway peer IP: Set an IPv4 address and mask for the gateway on your on\-premises data center. You may customize the interconnect IP according to network planning, but confirm that the cloud gateway peer IP and your gateway peer IP are in the same CIDR block without duplication. Use a private IP address that does not conflict with cloud or on\-premises IP addresses. |* Cloud gateway IP: 10.0.0.1/30​​<br><br>* Your gateway IP: 10.0.0.2/30​​ |
   |IPv6 interconnect IP |Enable IPv6 IP for interconnection as needed. |Disable |
   |VLAN ID |Set a VLAN ID for connecting to the data center. Confirm that this VLAN ID is unoccupied. |10 |
   |**Routing information** |||
   |Route type |Support two route types: BGP and Static. This example uses static routes. |Static routes |
   |Detection method |Select a detection method to check the line health. |Uncheck |
   

5. Click **Create** to complete the action.


<span id=".5q2l6aqk5Zub77ya5re75Yqg6Z2Z5oCB6Lev55Sx"></span>
### Step 4: Add a static route


1. Back to [the Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway), and click the name of the target DC Gateway  **(dcg\-01)**  in the DC Gateway list.

2. On the details page, select the **Routing information** tab.

3. Click **Add static route entry**, and configure the route.

   
   |Parameter |Value |
   |---|---|
   |Network type |IPv4 |
   |Destination CIDR |A destination CIDR block is the CIDR block of the on\-premises data center that needs to communicate with the VPC. In this example, it is 172.16.1.0/24. |
   |Next Hop type |Virtual Interface |
   |Next Hop |VIF\-uad8h |
   

4. Click **Add** to complete configuration.


<span id=".5q2l6aqk5LqU77ya5Yib5bu65LqR5LyB5Lia572R"></span>
### Step 5: Create a Cloud Enterprise Network


1. Log in to [the CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. Click **Create CEN**.

3. Configure the CEN based on the table below and load **vpc**.

   
   |Parameter |Value |
   |---|---|
   |**Basic information** ||
   |Name |cen\-test |
   |**Network Instances** ||
   |Attaching a network instance |Enable |
   |Regions |China (Beijing) |
   |Instance type |Virtual Private Cloud (VPC) |
   |Network Instances |Project\-test\|vpc |
   |**More information** ||
   |Project |Project\-test |
   

4. Click **Create** to complete the action. The ID of the new CEN is **cen\-rr9sri7\*\*\*\*1hx58031**.


<span id=".5q2l6aqk5YWt77ya5LqR5LyB5Lia572R5Yqg6L295LiT57q_572R5YWz"></span>
### Step 6: Load the DC Gateway to the CEN


1. In the list of [the CEN console](https://console.byteplus.com/cen/EnterpriseNetwork), click the name of the target instance  **(cen\-test)** .

2. In the **Network Instances** tab, click **Attach Network Instance**.

3. The Attach Network Instance window pops up. Configure the relevant parameters

   
   |Parameter |Value |
   |---|---|
   |Account |My account |
   |Regions |China (Beijing) |
   |Instance type |Direct Connect Gateway |
   |Network Instances |dcg\-01 |
   


<span id=".5q2l6aqk5LiD77ya5ZyoRUNT5omA5bGe5a6J5YWo57uE5re75Yqg5a6J5YWo57uE6KeE5YiZ"></span>
### Step 7: Add a rule to the ECS security group


1. Log in to [the ECS console](https://console.byteplus.com/ecs/dashboard).

2. In the top menu bar, select the region: **China (Beijing)** .

3. In the left\-side navigation pane, click **Instances**. On the instance page, choose **Main private IP address** from the dropdown in the search box, and type 192.168.1.10 to search for the target ECS.

4. Click the name of the target ECS, and then click the **Security Group** tab.

5. Click the security group name. In the **Access rules** tab, click **Add rule** under the Inbound rule tab.

   See the figure below to add an inbound rule that allows access from the CIDR block of the data center.


<span id=".5q2l6aqk5YWr77ya6YWN572u5pys5ZywSURD6Lev55Sx"></span>
### Step 8: Configure routing for the data center

In the data center, configure a route from the data center to the VPC, which means setting the destination address as the VPC and the next hop as the cloud gateway peer IP (10.0.0.1) for the route.

Log in to the on\-premises gateway (the gateway IP is 10.0.0.2) and configure a route from the on\-premises data center to the VPC based on the following commands.

```Plain Text
ip route 192.168.1.0 255.255.255.0 10.0.0.1   
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If your testing device is not the same as your on\-premises gateway device, you need to configure routing between them.</div>


* <div data-tips="true" data-tips-type="tip">Routing configuration commands may vary for gateway devices from different vendors. For specific configurations, consult your device vendor.</div>



<span id=".5q2l6aqk5Lmd77ya5rWL6K-V6L-e6YCa5oCn"></span>
### Step 9: Test connectivity


* Test DC connectivity

   In the command window of the on\-premises data center, execute the `ping` command to ping Cloud gateway peer IP typed at the creation of the DC Gateway. In this example, ping 10.0.0.1 to verify connectivity to the DC gateway.

* Test ECS connectivity

   After confirming the DC communicates properly, execute the `ping` command in the command window of the on\-premises data center, ping the IP address of an ECS within the VPC. In this example, ping 192.168.1.10 to verify connectivity to the ECS within the VPC.
