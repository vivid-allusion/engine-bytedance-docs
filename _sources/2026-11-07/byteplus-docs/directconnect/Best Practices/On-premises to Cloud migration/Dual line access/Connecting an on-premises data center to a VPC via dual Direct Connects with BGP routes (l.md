---
title: "Connecting an on-premises data center to a VPC via dual Direct Connects with BGP routes (load redundancy)"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Best-Practices-5"
---

To avoid single\-link failures and improve disaster recovery, you can deploy dual active\-active Direct Connect (DC) Connections to connect your on\-premises data center and Virtual Private Cloud (VPC) for load redundancy. This topic describes how to design a dual\-line architecture with load redundancy, configure its routing, and provision sufficient bandwidth, ensuring seamless failover during faults.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Dual\-line is a specific form of multi\-line. The architectural solution and limits provided in this section also apply to multi\-line access scenarios.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

A company needs to migrate some key services from its on\-premises data center (private CIDR block: 192.168.1.0/24) in Beijing to VPC1 (private CIDR block: 172.16.1.0/24) in the same region, ensuring interconnectivity via DC Connection. Due to the large user base and potential serious impact of any failure, the solution is to apply for one DC Connection each from separate line operators, DAS225_port01_conn and DAS225_port02_conn, and connect them to different switches, connecting your on\-premises data center and VPC in load redundancy mode.

In the dual\-line load redundancy scenario, both DC Connections forward traffic simultaneously. If one line fails, the other assumes the full traffic load.​ To ensure smooth traffic failover and uninterrupted business operations, plan your deployment considering the following three dimensions:


* **Architectural redundancy**:​ The two DC Connections should terminate at different access points to ensure availability in case of port, link, device, or access point failures.

* **Equal\-cost routing**: The on\-premises data center must advertise equal\-cost routes to both Direct Connects via BGP (multi\-ISP). This enables the cloud VPC to load\-balance traffic evenly across the two links using ECMP. We also recommend enabling BFD detection to accelerate failure detection and route convergence, thereby reducing failover time.

* **Bandwidth capacity**: To achieve high availability with dual\-line load redundancy, the healthy line must have sufficient spare bandwidth to carry the entire business traffic when the other line fails. If the bandwidth utilization on both lines is excessively high during normal operation, the surviving line may not have enough capacity after failover, potentially causing packet loss. Therefore, we recommend that the bandwidth specification of each DC Connection be capable of independently handling the peak total business traffic. The daily bandwidth utilization for a single line should be kept below **50%**  of its upper limit.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Your dual\-line load redundancy solution must be deployed to meet all three dimensions above to ensure effective protection for your business traffic during failure scenarios.</div>



* <div data-tips="true" data-tips-type="warning">Architectural redundancy alone without equal\-cost routing prevents traffic from automatically switching to a healthy line during failure.</div>


* <div data-tips="true" data-tips-type="warning">Even if the architecture and routing are properly configured, packet loss may still occur after a failover if​ the healthy line lacks sufficient bandwidth capacity.</div>



**Network planning**


|DC interconnection |One DC Connection (Virtual Interface 1) |Another DC Connection (Virtual Interface 2) |
|---|---|---|
|Cloud gateway peer IP |`10.0.0.1/30` |`10.0.0.5/30` |
|Your gateway peer IP |`10.0.0.2/30` |`10.0.0.6/30` |
|VLAN ID |10 |20 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Cloud gateway peer IP is the interconnect IP of the VPC, and Your gateway peer IP is the interconnect IP of your on\-premises data center.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created a VPC named VPC1 (private CIDR block: 172.16.1.0/24) and its subnet. For procedure, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* You have created an Elastic Compute Service (ECS) instance (private IP address: 172.16.1.12) within VPC1. For procedure, see [Buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id=".57qm5p2f6ZmQ5Yi2"></span>
## Limits


* The route type must be BGP.

* Equal\-cost BGP routes must be advertised from the on\-premises data center to the VPC through the two DC Connections.

* The gateway device on the on\-premises data center supports BGP and Bidirectional Forwarding Detection (BFD).

* Consider the following limits when connecting DC Connections to switches:

   * Connect the two different DC Connections to switches at separate access points.

   * If connecting the two different DC Connections to separate switches, you must create two separate DC Gateways to associate with respective DC Connections.


<span id="yqfm6lNu"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5o6l5YWl54mp55CG5LiT57q_"></span>
### Step 1: Create a DC Connection

Activate two DC Connections, and connect them to separate switches. For procedure, see [Creating a Direct Connect Connection.](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1) This example uses DC Connections in China (Beijing): DAS225_port01_conn and DAS225_port02_conn.

<span id=".5q2l6aqk5LqM77ya5Yib5bu65LiT57q_572R5YWz"></span>
### Step 2: Create a DC Gateway

Since the two DC Connections are connected to separate switches, you need to create two DC Gateways.


1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway).

2. In the top menu bar, select the region: **China (Beijing)** .

3. Click **Create DC Gateway**.

4. Configure the DC Gateway based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Region |The region where the DC Gateway is deployed. It must match the region of the DC Connection. |China (Beijing) |
   |Name |Set the name for the DC Gateway. |dcg\-01 |
   |ASN |Set an ASN for the DC Gateway. This example does not require a custom ASN and directly uses the BytePlus ASN. |137718 |
   |IPv6 |Enable IPv6 as needed. |Disable |
   |Affiliated project |Select the project to which the new DC Gateway belongs. |Project\-test |
   |Agreement |Follow the console guidance to review and accept Legal. |Check |
   

5. After confirming all parameters are correct, click **Buy now** to complete the action.

6. Click **Go to console** to return to the Direct Connect Gateway console. You can view the new DC Gateway (dcg\-01) in the DC Gateway list.

7. Repeat steps 1 to 5 to create another DC Gateway (dcg\-02).


<span id=".5q2l6aqk5LiJ77ya5Yib5bu66Jma5ouf5o6l5Y-j"></span>
### Step 3: Create a Virtual Interface


1. Log in to the [DC Virtual Interface console](https://console.byteplus.com/dc/VirtualInterface).

2. Click **Create DC Virtual Interface**.

3. Configure the Virtual Interface based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Virtual Interface owner |Select the account to which the Virtual Interface belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The feature of creating a Shared Virtual Interface for another account is currently in the beta stage. If you need a trial, please contact your account manager.</div><br> |My account |
   |Region |The region where the Virtual Interface is deployed. It must be the same region as the DC Connection and the DC Gateway. |China (Beijing) |
   |Name |Set the name for the Virtual Interface. |VIF\-ds01 |
   |DC Connection |Filter the DC Connection by project to associate with the Virtual Interface. |Project\-test\|DAS225_port01_conn |
   |DC Gateway |Filter the DC Gateway by project to associate with the Virtual Interface. |Project\-test\|dcg\-01 |
   |Bandwidth limit |Enable bandwidth limit as needed. |Disable |
   |**Interconnection information** |||
   |IPv4 interconnect IP |Set the IPv4 IP for interconnection.<br><br><br>* Cloud gateway peer IP: Set an IPv4 address and mask for the cloud DC gateway. You may customize the interconnect IP according to network planning, but confirm that the cloud gateway peer IP and your gateway peer IP are in the same CIDR block without duplication. Use a private IP address that does not conflict with cloud or on\-premises IP addresses.<br><br>* Your gateway peer IP: Set an IPv4 address and mask for the gateway on your on\-premises data center. You may customize the interconnect IP according to network planning, but confirm that the cloud gateway peer IP and your gateway peer IP are in the same CIDR block without duplication. Use a private IP address that does not conflict with cloud or on\-premises IP addresses. |* Cloud gateway peer IP: 10.0.0.1/30​​<br><br>* Your gateway IP: 10.0.0.2/30​​ |
   |IPv6 interconnect IP |Enable IPv6 IP for interconnection as needed. |Disable |
   |VLAN ID |Set a VLAN ID for connecting to the data center. Confirm that this VLAN ID is unoccupied. Range: 0–2999.<br><br><br>* 0: The DC Connection's switch port operates in Layer 3 routing mode with no VLAN configured. This mode supports only a single untagged virtual interface per DC Connection.<br><br>* 1–2999: The DC Connection's switch port operates in Layer 3 sub\-interface mode. Each sub\-interface has a unique VLAN ID mapped to a separate virtual interface. This mode supports multiple virtual interfaces per DC Connection. |10 |
   |**Routing information** |||
   |Route type |Supports two route types: BGP and Static. This example uses BGP routes. |BGP |
   |BGP Peer ASN |Set the ASN for the IPv4 BGP Peer. The valid range for ASN is 1 to 4294960000. The ASN of the BGP Peer can neither be the same as that of the DC Gateway, nor be the BytePlus ASN (137718). |465000 |
   |BGP key |Type the key for the IPv4 BGP Peer. |123456 |
   |Detection method |Select a detection method for the line.<br><br><br>* After enabling BFD, the system establishes a BFD session between the on\-premises data center and BytePlus. Both ends send BFD packets periodically based on the set detect interval. If a BFD session misses a certain number of consecutive packets, the system immediately declares a route failure.<br><br>* In Direct Connect redundancy access mode, enabling Bidirectional Forwarding Detection (BFD) allows quick line switching when a route failure occurs.<br><br>* After enabling BFD, you must configure BFD synchronously for your data center, confirming that the detect interval and detect multiplier match those configured on BytePlus. |BFD |
   |BFD mode |Select a mode for the BFD detection. We recommend using BFD control packet. |BFD control packet |
   |Detect interval |The time interval for sending and receiving BFD packets. |1000 |
   |Detect multiplier |The number of BFD detection attempts. If a BFD session fails to receive the defined number of consecutive packets, the system declares a route failure. |3 |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In this example, a BGP Peer is established along with the creation of the Virtual Interface. Once established, the BGP information (Peer ASN and BGP key) cannot be modified.   </div>
   

4. Click **Create** to complete the action.

5. Repeat steps 1\-4 to create another Virtual Interface with configurations listed in the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Virtual Interface owner |Select the account to which the Virtual Interface belongs. |My account |
   |Region |The region where the Virtual Interface is deployed. It must be the same region as the DC Connection and the DC Gateway. |China (Beijing) |
   |Name |Set the name for the Virtual Interface. |VIF\-ds02 |
   |DC Connection |Filter the DC Connection by project to associate with the Virtual Interface. |Project\-test\|DAS225_port02_conn |
   |DC Gateway |Select the DC Gateway to be associated with the Virtual Interface. |dcg\-02 |
   |**Interconnection information** |||
   |IPv4 interconnect IP |Set the IPv4 IP for interconnection.<br><br><br>* Cloud gateway peer IP: Set an IPv4 address and mask for the cloud DC gateway.<br><br>* Your gateway peer IP: Set an IPv4 address and mask for the gateway on your on\-premises data center. |* Cloud gateway peer IP: 10.0.0.5/30<br><br>* Your gateway peer IP: 10.0.0.6/30 |
   |IPv6 interconnect IP |Enable IPv6 IP for interconnection as needed. |Disable |
   |VLAN ID |Set a VLAN ID for connecting to the data center. Confirm that this VLAN ID is not occupied. |20 |
   |**Routing information** |||
   |Route type |Select the routing mode. |BGP |
   |BGP Peer ASN |Type the ASN of the IPv4 BGP Peer. |465000 |
   |BGP key |Type the key for the IPv4 BGP Peer. |123456 |
   |Detection method |Select a detection method to check the line health.<br><br>After enabling BFD, you must configure BFD synchronously for your data center, confirming that the detect interval and detect multiplier match those configured on BytePlus. |BFD |
   |Detect interval |The time interval for sending and receiving BFD packets. |1000 |
   |Detect multiplier |The number of BFD detection attempts. If a BFD session fails to receive the defined number of consecutive packets, the system declares a route failure. |3 |
   


<span id=".5q2l6aqk5Zub77ya5Yib5bu65LqR5LyB5Lia572R5bm25Yqg6L29572R57uc5a6e5L6L"></span>
### Step 4: Create a CEN and load the network instance


1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. Click **Create CEN**.

3. Configure the CEN based on the table below and load **VPC\-01**.

   
   |Parameter |Value |
   |---|---|
   |**Basic information** ||
   |Name |cen\-test |
   |**Network Instances** ||
   |Attach Network Instance |Enable |
   |Region |China (Beijing) |
   |Instance type |VPC |
   |Network Instances |Project\-test\|VPC1 |
   |**More information** ||
   |Affiliated project |Project\-test |
   

4. Click **Create** to complete the action.

5. In the CEN Instance list, click the name of the target instance: **cen\-test**.

6. In the **Network Instances** tab, click **Attach Network Instance**.

7. The Attach Network Instance window pops up. Configure the information of the DC Gateway instance (dcg\-01) to be loaded, and then click **Attach** to complete the action.

   
   |Parameter |Value |
   |---|---|
   |Account |My account |
   |Region |China (Beijing) |
   |Instance type |DC Gateway |
   |Network Instances |dcg\-01 |
   

8. Refer to steps 5 to 7 to load another DC Gateway (dcg\-02).


<span id=".5q2l6aqk5LqU77ya5ZyoRUNT5omA5bGe5a6J5YWo57uE5re75Yqg5a6J5YWo57uE6KeE5YiZ"></span>
### Step 5: Add a rule to the ECS security group


1. Log in to [the ECS console](https://console.byteplus.com/ecs/dashboard).

2. In the top menu bar, select the region: China (Beijing).

3. In the left\-side navigation pane, click **Instances**. On the instance page, choose **Main private IP address** from the dropdown in the search box, and type 172.16.1.12 to search for the target ECS.

4. Click the name of the target ECS to its details page, and then click the **Security Group** tab.

5. Click the name of the security group to redirect to the security group details page.

6. Click the **Access rules** tab, and click **Add rule** under the Inbound rule tab.


<span id=".5q2l6aqk5YWt77ya6YWN572u5pys5Zyw6Lev55Sx5ZKMQkZE"></span>
### Step 6: Configure local routing and BFD

Configure routing and BFD on a local switch. Two switches are connected separately to two on\-premises data center switches (assumed as switch01 and switch02, private CIDR block: 192.168.1.0/24). Apply configurations on both switches to establish load redundancy over multi\-POP connections.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Configuration commands are vendor\-specific. These commands are for reference only. Adjust commands based on your device model. For details, consult your device vendor.</div>


**Reference commands**

Configuration command for on\-premises switch01:

```Plain Text
bgp 465000
peer 10.0.0.1 as-number 137718
peer 10.0.0.1 password simple 123456
peer 10.0.0.1 bfd
network 192.168.1.0 255.255.255.0

interface HGE1/1/1
bfd detect-multiplier 3
bfd min-transmit-interval 1000
bfd min-receive-interval 1000
```


Configuration command for on\-premises switch02:

```Plain Text
bgp 465000
peer 10.0.0.5 as-number 137718
peer 10.0.0.5 password simple 123456
peer 10.0.0.5 bfd
network 192.168.1.0 255.255.255.0

interface HGE1/1/1
bfd detect-multiplier 3
bfd min-transmit-interval 1000
bfd min-receive-interval 1000
```


Parameter description:


* 465000: BGP Peer ASN of the data center.

* 137718: ASN of the DC Gateway (i.e., BytePlus ASN).

* 10.0.0.1: Local (Cloud) gateway peer IP for one DC Connection.

* 10.0.0.5: Local (Cloud) gateway peer IP for another DC Connection.

* 123456: BGP key of the data center.

* 192.168.1.0: Private CIDR block of the data center.

* 255.255.255.0: Mask of the data center.

* HGE1/1/1: Direct Connect interface.

* 3: BFD detect multiplier.

* 1000: Minimum interval for sending and receiving single\-hop BFD control packets.


<span id=".5q2l6aqk5LiD77ya5rWL6K-V6L-e6YCa5oCn"></span>
### Step 7: Test connectivity


1. In the command window of the on\-premises data center, execute the `ping` command to ping Cloud gateway peer IPs of the two DC Connections. In this example, ping 10.0.0.1 and 10.0.0.5 to verify connectivity to the DC gateway network.

   Expected result: Ping tests for both connections are successful. The data center is properly connected to the DC Gateway network.

2. In the command window of the on\-premises data center, execute the `ping` command to ping the private IP address of an ECS within the VPC. In this example, ping 172.16.1.12 to verify connectivity to the ECS within the VPC.

   Expected result: Ping successful. The data center is properly connected to the ECS network.

3. Execute the `tracert -d` command to check whether the dual DC Connections are deployed in load redundancy mode.
