---
title: "Connecting an on-premises data center to a VPC across accounts and regions"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Best-Practices-9"
---

Virtual Private Clouds (VPCs) in different accounts and regions are isolated from on\-premises data center networks. This section describes how to enable network connectivity between an on\-premises data center and a VPC across accounts and regions.

<span id=".6IOM5pmv5LuL57uN"></span>
## Background introduction

A data center in Beijing is connected to the cloud via a Direct Connect (DC) Connection in the nearest region. Now, you want to access from the data center to resources in a VPC in a different region and account via DC Connection.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have created a VPC (name: vpc\-test) and its subnet in China (Shanghai) under Account B (account ID: 200\*\*\*\*02), and purchased an Elastic Compute Service (ECS) instance within that VPC. For procedures, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5o6l5YWl54mp55CG5LiT57q_"></span>
### Step 1: Create a DC Connection

In this example, the creation of DC Connection is completed. The DC Connection under the current account (Account B, ID: 200\*\*\*\*01) is marked as "Opened". For procedure, see [Creating a Direct Connect Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1). DAS230_port01_conn is the DC Connection in China (Beijing).

<span id=".5q2l6aqk5LqM77ya5Yib5bu65LiT57q_572R5YWz"></span>
### Step 2: Create a DC Gateway


1. Use Account A to log in to [the Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway).

2. Click **Create DC Gateway** to create a DC Gateway with the following configuration.

   
   |Parameters |Description |Value |
   |---|---|---|
   |Regions |Select the region where the DC Gateway is deployed. It must match the region of the DC Connection. |China (Beijing) |
   |Name |Set a name for the DC Gateway. |dcg\-test |
   |ASN |Set an ASN for the DC Gateway. This example does not require a custom ASN and directly uses the BytePlus ASN. |137718 |
   |IPv6 |Enable IPv6 as needed. |Disable |
   |Affiliated project |Select the project to which the new DC Gateway belongs. |Project\-test |
   |Agreement |Follow the console guidance to review and accept Legal. |Check |
   

3. Click **Buy now** to complete the action.

4. Click **Go to console** to return to the Direct Connect Gateway console. You can view the new DC Gateway  **(dcg\-test)**  in the DC Gateway list.


<span id=".5q2l6aqk5LiJ77ya5Yib5bu66Jma5ouf5o6l5Y-j"></span>
### Step 3: Create a Virtual Interface


1. Use Account A to log in to [the DC Virtual Interface console](https://console.byteplus.com/dc/VirtualInterface).

2. Click **Create DC Virtual Interface**.

3. Configure the Virtual Interface based on the table below.

   
   |Parameters |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Resource ownership |Select the account to which the Virtual Interface belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The feature of creating a Shared Virtual Interface for another account is currently in the beta stage. If you need a trial, please contact your account manager.</div><br> |My account |
   |Regions |Select the region where the Virtual Interface is deployed. It must be the same as the region of the DC Connection and the DC Gateway. |China (Beijing) |
   |Name |Set a name for the Ethernet Virtual Interface. |VIF\-weo4 |
   |DC Connection |Filter the DC Connection by project to associate with the Virtual Interface. |Project\-test\|DAS230_port01_conn |
   |Direct Connect Gateway |Filter the DC Gateway by project to associate with the Virtual Interface. |Project\-test\|dcg\-test |
   |Bandwidth limit |Enable bandwidth limit as needed. |Disable |
   |**Interconnection information** |||
   |IPv4 interconnect IP |Set the IPv4 IP for interconnection.<br><br><br>* Cloud gateway peer IP: Set an IPv4 address and mask for the cloud DC gateway. You may customize the interconnect IP according to network planning, but confirm that the cloud gateway peer IP and your gateway peer IP are in the same CIDR block without duplication. Use a private IP address that does not conflict with cloud or on\-premises IP addresses.<br><br>* Your gateway peer IP: Set an IPv4 address and mask for the gateway on your on\-premises data center. You may customize the interconnect IP according to network planning, but confirm that the cloud gateway peer IP and your gateway peer IP are in the same CIDR block without duplication. Use a private IP address that does not conflict with cloud or on\-premises IP addresses. |* Cloud gateway peer IP: 10.0.0.1/30​​<br><br>* Your gateway IP: 10.0.0.2/30​​ |
   |IPv6 interconnect IP |Enable IPv6 IP for interconnection as needed. |Disable |
   |VLAN ID |Set a VLAN ID for connecting to the data center. Confirm that this VLAN ID is unoccupied. |10 |
   |**Routing information** |||
   |Route type |Support two route types: BGP and Static. This example uses BGP routes. |BGP |
   |Peer ASN |Set the ASN for the IPv4 BGP Peer. The valid range for ASN is 1 to 4294960000. The ASN of the BGP Peer can neither be the same as that of the DC Gateway, nor be the BytePlus ASN (137718). |483600 |
   |BGP key |Type the key for the IPv4 BGP Peer. |00300 |
   |Detection method |Select a detection method for the line.<br><br>After enabling BFD, periodic packets are sent between BytePlus and on\-premises devices to detect the link status. This enables rapid switching to the secondary connection upon failure and completing route convergence in the from\-cloud direction. |BFD |
   |BFD mode |Select a mode for the BFD detection. The mode is BFD control packet in this example. |BFD control packet |
   |Detect interval |The time interval for BFD to send consecutive packets. |2000 |
   |Detect multiplier |The number of BFD detection attempts. If a BFD session fails to receive the defined number of consecutive packets, the system declares a route failure. |8 |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In this example, a BGP Peer is established along with the creation of the Virtual Interface. Once established, the BGP information (Peer ASN and BGP key) cannot be modified.   </div>
   

4. Click **Create** to complete the action.

5. Configure data center routing. For reference commands, see [Configure the routing for a data center](https://docs.byteplus.com/en/docs/directconnect/Best-Practices-3#.5q2l6aqk5YWt77ya6YWN572u5pys5ZywSURD6Lev55Sx).


<span id=".5q2l6aqk5Zub77ya5Yib5bu65LqR5LyB5Lia572R"></span>
### Step 4: Create a Cloud Enterprise Network


1. Use Account A to log in to [the CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. Click **Create CEN**.

3. Configure the CEN based on the table below.

   
   |Parameters |Value |
   |---|---|
   |**Basic information** ||
   |Name |cen\-01 |
   |Main account |A parameter that only appears on the O&M\-side. Select the account of the resource. |
   |**Network Instances** ||
   |Attach Network Instance |Disable |
   |**More information** ||
   |Project |Project\-test |
   

4. Click **Create** to complete the action. The ID of the new CEN is cen\-rrhx580\*\*\*\*1ri7. Record this ID, which is required for cross\-account authorization.


<span id=".5q2l6aqk5LqU77ya5Li66Leo6LSm5Y-35LqR5LyB5Lia572R5o6I5p2D"></span>
### Step 5: Authorize cross\-account CEN


1. Use Account B to log in to [the Virtual Private Cloud console](https://console.byteplus.com/vpc/vpc).

2. In the VPC list, click the name of the target VPC: **vpc\-test**.

3. Click the **CEN cross\-account authorization** tab, and then click **CEN cross\-account authorization**.

4. In the pop\-up dialog box, type the information of the CEN under another account.

   
   |Parameters |Value |
   |---|---|
   |Owner account ID |200\*\*\*\*01 |
   |Peer CEN instance ID |cen\-rrhx580\*\*\*\*1ri7 |
   

5. After completion, click **Attach**.


<span id=".5q2l6aqk5YWt77ya5LqR5LyB5Lia572R5Yqg6L29572R57uc5a6e5L6L"></span>
### Step 6: Load a network instance to the CEN

<span id=".5Yqg6L296Leo6LSm5Y-356eB5pyJ572R57uc"></span>
#### Load a VPC of another account


1. Use Account A to log in to [the CEN console](https://console.byteplus.com/cen/EnterpriseNetwork). In the CEN instance list, click the name of the target instance: **cen\-01**.

2. In the **Network Instances** tab, click **Attach Network Instance**.

3. The Attach Network Instance window pops up. Configure the information of the DC Gateway to be loaded.

   
   |Parameters |Value |
   |---|---|
   |Account |Cross\-account |
   |Owner account ID |200\*\*\*\*02 |
   |Regions |China (Shanghai) |
   |Instance type |Virtual Private Cloud (VPC) |
   |Network Instances |vpc\-test |
   


<span id=".5Yqg6L295pys6LSm5Y-35LiT57q_572R5YWz"></span>
#### Load a DC Gateway of my account


1. Use Account A to log in to [the CEN console](https://console.byteplus.com/cen/EnterpriseNetwork). In the CEN instance list, click the name of the target instance: **cen\-01**.

2. In the **Network Instances** tab, click **Attach Network Instance**.

3. The Attach Network Instance window pops up. Configure the information of the DC Gateway to be loaded.

   
   |Parameters |Value |
   |---|---|
   |Account |My account |
   |Regions |China (Beijing) |
   |Instance type |DC Gateway |
   |Network Instances |dcg\-test |
   


<span id=".5q2l6aqk5LiD77ya6LSt5Lmw5bim5a695YyF5bm25YiG6YWN5Z-f6Ze05bim5a69"></span>
### Step 7: Purchase a bandwidth package and allocate inter\-region bandwidth.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This example is accessing resources in a VPC across accounts and regions. Cross\-region access requires purchasing a CEN bandwidth package. If you are accessing resources in a VPC across accounts but in the same region, you can skip this step.</div>



1. Use Account A to log in to [the CEN console](https://console.byteplus.com/cen/EnterpriseNetwork). In the left\-side navigation pane, click **Bandwidth Package**.

2. Click **Create BWP**, and configure the bandwidth package based on the table below.

   
   |Parameters |Value |
   |---|---|
   |**Basic information** ||
   |Billing method |Subscription |
   |Name |package\-test |
   |**Bandwidth configuration** ||
   |CEN |Project\-test\|cen\-01 |
   |Interoperability area |Chinese mainland \- Chinese mainland |
   |Bandwidth |300Mbps |
   |Duration |1 month |
   |**More information** ||
   |Affiliated project |Project\-test |
   

3. Click **Confirm order**. After confirming the order is correct on its details page, follow the console guidance to review and accept the legal terms.

4. Click **Buy now** to complete the bandwidth package creation.

5. In the left\-side navigation pane, click **CEN Instances**.

6. Click the CEN Instance name  **(cen\-01)** , and then click the **Inter\-region bandwidth** tab in the details page.

7. In the **Inter\-region bandwidth** zone, click **Allocate inter\-region bandwidth**. Allocate bandwidth across regions based on the table below.

   
   |Parameters |Value |
   |---|---|
   |Bandwidth package |package\-test |
   |Interconnected regions |China (Beijing) \- China (Shanghai) |
   |Bandwidth |200Mbps |
   

8. Click **Create** to complete configuration.


<span id=".5q2l6aqk5YWr77ya6YWN572u5pys5Zyw6Lev55Sx5ZKMQkZE"></span>
### Step 8: Configure local routing and BFD

Configure routing and BFD on a local switch.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Configuration commands are vendor\-specific. These commands are for reference only. Adjust commands based on your device model. For details, consult your device vendor.</div>


**Reference commands**

```Plain Text
bgp 483600
peer 10.0.0.1 as-number 137718
peer 10.0.0.1 password simple 00300
peer 10.0.0.1 bfd
network 192.168.2.0 255.255.255.0

interface HGE1/1/1
bfd detect-multiplier 8
bfd min-transmit-interval 2000
bfd min-receive-interval 2000
```


<span id=".5q2l6aqk5Lmd77ya5rWL6K-V6L-e6YCa5oCn"></span>
### Step 9: Test connectivity


1. Log in to any server within 192.168.1.0/24 of your on\-premises data center.

2. Run the following command. A successful Ping indicates the data center is properly connected to the VPC network across accounts and regions.

   `ping 192.168.2.10`
