---
title: "Connecting an on-premises data center to a VPC via a single Direct Connect with BGP"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Best-Practices-3"
---

The networks of the Virtual Private Cloud (VPC) and the on\-premises data center are isolated and cannot mutually communicate. This section describes how to achieve interconnection between a data center and Elastic Compute Service (ECS) within a VPC via Direct Connect (DC) using BGP.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created a VPC (named VPC\-02) and its subnets. For procedure, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The subnet CIDR block of the VPC must not overlap or conflict with that of the data center. All existing route entries must not conflict with subnet routes after adding to a DC Connection   </div>
   

* You have created an ECS instance within VPC\-02. For procedure, see [Purchasing an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* The gateway devices on the data center side support Border Gateway Protocol (BGP).


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

An enterprise has the following configuration: For the VPC, the CIDR block of the subnet is 192.168.2.0/24, the IP address of the gateway is 10.0.0.5, and the private IP address of the ECS is 192.168.2.7. For the on\-premises data center, the CIDR block of the subnet is 172.16.2.0/24, the IP address of the gateway is 10.0.0.6, and the IP address of an active server is 172.16.2.10. Now, the enterprise wants its on\-premises data center to access the ECS within the VPC through Direct Connect.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5o6l5YWl54mp55CG5LiT57q_"></span>
### Step 1: Create a DC Connection

Activate one DC Connections. For procedure, see [Creating a Direct Connect Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1). In this example, the DC Connection used is DAS336_port100_conn under Project\-test in China (Beijing).

<span id=".5q2l6aqk5LqM77ya5Yib5bu65LiT57q_572R5YWz"></span>
### Step 2: Create a DC Gateway


1. Log in to [the Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway).

2. Click **Create DC Gateway** to enter the creation page, and create a DC Gateway based on the following configuration.

   
   |Parameter |Description |Value |
   |---|---|---|
   |Regions |Select the region where the DC Gateway is deployed. It must match the region of the DC Connection. |China (Beijing) |
   |Name |Set a name for the DC Gateway. |dcg\-test |
   |ASN |Set an ASN for the DC Gateway. This example does not require a custom ASN and directly uses the BytePlus ASN. |137718 |
   |IPv6 |Enable IPv6 as needed. |Disable |
   |Project |Select the project to which the new DC Gateway belongs. |Project\-test |
   |Agreement |Follow the console guidance to review and accept the legal terms. |\- |
   

3. Click **Buy now** to complete the action.


<span id=".5q2l6aqk5LiJ77ya5Yib5bu66Jma5ouf5o6l5Y-j"></span>
### Step 3: Create a Virtual Interface


1. Log in to [the DC Virtual Interface console](https://console.byteplus.com/dc/VirtualInterface).

2. Click **Create DC Virtual Interface**.

3. Configure the Virtual Interface based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Resource ownership |Select the account to which the Virtual Interface belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The feature of creating a Shared Virtual Interface for another account is currently in the beta stage. If you need a trial, please contact your account manager.</div><br> |My account |
   |Regions |Select the region where the Virtual Interface is deployed. It must be the same as the region of the DC Connection and the DC Gateway. |China (Beijing) |
   |Name |Set a name for the Ethernet Virtual Interface. |VIF\-dsq3e |
   |DC Connection |Filter the DC Connection by project to associate with the Virtual Interface. |Project\-test\|DAS336_port100_conn |
   |Direct Connect Gateway |Filter the DC Gateway by project to associate with the Virtual Interface. |Project\-test\|dcg\-test |
   |Bandwidth limit |Enable bandwidth limit as needed. |Disable |
   |**Interconnection information** |||
   |IPv4 interconnect IP |Set the IPv4 IP for interconnection.<br><br><br>* Cloud gateway peer IP: Set an IPv4 address and mask for the cloud DC gateway. You may customize the interconnect IP according to network planning, but confirm that the cloud gateway peer IP and your gateway peer IP are in the same CIDR block without duplication. Use a private IP address that does not conflict with cloud or on\-premises IP addresses.<br><br>* Your gateway peer IP: Set an IPv4 address and mask for the gateway on your on\-premises data center. You may customize the interconnect IP according to network planning, but confirm that the cloud gateway peer IP and your gateway peer IP are in the same CIDR block without duplication. Use a private IP address that does not conflict with cloud or on\-premises IP addresses. |* Cloud gateway peer IP: 10.0.0.5/30<br><br>* Your gateway peer IP: 10.0.0.6/30 |
   |IPv6 interconnect IP |Enable IPv6 IP for interconnection as needed. |Disable |
   |VLAN ID |Set a VLAN ID for connecting to the data center. Confirm that this VLAN ID is unoccupied. Range: 0–2999.<br><br><br>* 0: The DC Connection's switch port operates in Layer 3 routing mode with no VLAN configured. This mode supports only a single untagged Virtual Interface per DC Connection.<br><br>* 1–2999: The DC Connection's switch port operates in Layer 3 sub\-interface mode. Each sub\-interface has a unique VLAN ID mapped to a separate Virtual Interface. This mode supports multiple Virtual Interfaces per DC Connection. |10 |
   |**Routing information** |||
   |Route type |Support two route types: BGP and Static. This example uses BGP routes. |BGP |
   |Peer ASN |Set the ASN for the IPv4 BGP Peer. The valid range for ASN is 1 to 4294960000. The ASN of the BGP Peer can neither be the same as that of the DC Gateway, nor be the BytePlus ASN (137718). |42949 |
   |BGP key |Type the key for the IPv4 BGP Peer. |00300 |
   |Detection method |Select a detection method to check the line health. |Uncheck |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In this example, a BGP Peer is established along with the creation of the Virtual Interface. Once established, the BGP information (Peer ASN and BGP key) cannot be modified.   </div>
   

4. Click **Create** to complete the action.


<span id=".5q2l6aqk5Zub77ya6YWN572u5LqR5LyB5Lia572R"></span>
### Step 4: Configure Cloud Enterprise Network


1. Log in to [the CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. Click **Create CEN**.

3. Configure the CEN based on the table below and load **VPC\-02**.

   
   |Parameter |Value |
   |---|---|
   |**Basic information** ||
   |Name |cen\-test02 |
   |**Network Instances** ||
   |Attach Network Instance |Enable |
   |Regions |China (Beijing) |
   |Instance type |VPC |
   |Network Instances |VPC\-02 |
   |**More information** ||
   |Project |Project\-test |
   

4. Click **Create** to complete the action.

5. In the list of CEN Instances, click the name of the target instance  **(cen\-test02)** .

6. In the **Network Instances** tab, click **Attach Network Instance**.

7. The Attach Network Instance window pops up. Configure the information of the DC Gateway instance to be loaded.

   
   |Parameter |Value |
   |---|---|
   |Account |My account |
   |Regions |China (Beijing) |
   |Instance type |DC Gateway |
   |Network Instances |dcg\-test |
   


<span id=".5q2l6aqk5LqU77ya5ZyoRUNT5omA5bGe5a6J5YWo57uE5re75Yqg5a6J5YWo57uE6KeE5YiZ"></span>
### Step 5: Add a rule to the ECS security group


1. Log in to [the ECS console](https://console.byteplus.com/ecs/dashboard).

2. In the top menu bar, select the region: China (Beijing).

3. In the left\-side navigation pane, click **Instances**. On the instance page, choose **Main private IP address** from the dropdown in the search box, and type 192.168.2.7 to search for the target ECS.

4. Click the name of the target ECS, and then click the **Security Group** tab.

5. Click the security group name. In the **Access rules** tab, click **Add rule** under the Inbound rule tab.

   See the figure below to add an inbound rule that allows the CIDR block of the data center to access.


<span id=".5q2l6aqk5YWt77ya6YWN572u5pys5ZywSURD6Lev55Sx"></span>
### Step 6: Configure routing for an on\-premises data center

After Direct Connect is configured in the BytePlus console, you must also configure the private network routing locally to truly achieve network interconnection between a data center and a VPC.

```Plain Text
bgp 42949
peer 10.0.0.5 as-number 137718
peer 10.0.0.5 password simple 00300
network 172.16.2.0 255.255.255.0
```


Parameter description:


* 42949: The BGP ASN of the on\-premises data center.

* 137718: The ASN of BytePlus.

* 10.0.0.5: The local interconnect IP (cloud gateway peer IP) filled in when creating the VPC.

* 00300: The BGP key of the data center.

* 172.16.2.0: The private CIDR block of the on\-premises data center.

* 255.255.255.0: The mask of the IP address for the data center.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Configuration commands may vary across different devices. Adopt according to your specific device during actual operation. For details, please consult your device vendor.</div>


<span id=".5q2l6aqk5LiD77ya5rWL6K-V6L-e6YCa5oCn"></span>
### Step 7: Test connectivity

<span id=".5rWL6K-V5LiT57q_6L-e6YCa5oCn"></span>
#### Test DC connectivity

In the command window of the on\-premises data center, execute the `ping` command to ping Cloud gateway peer IP typed at the creation of the DC Gateway. In this example, ping 10.0.0.5 to verify connectivity to the DC gateway network.

Expected result: Ping successful. The on\-premises data center is properly connected to the DC Gateway network.

<span id=".5rWL6K-V5LqR5pyN5Yqh5Zmo6L-e6YCa5oCn"></span>
#### Test ECS connectivity

After confirming the DC communicates properly, execute the `ping` command in the command window of the on\-premises data center, ping the private IP address of an ECS within the VPC. In this example, ping 192.168.2.7 to verify connectivity to the ECS within the VPC.

Expected result: Ping successful. The data center is properly connected to the ECS network.
