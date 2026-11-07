---
title: "Connecting an on-premises data center to a VPC via dual Direct Connects with static routes (active-standby redundancy)"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Best-Practices-8"
---

To avoid single\-link failures and improve disaster recovery, typically deploy dual active\-standby Direct Connect (DC) Connections to connect your on\-premises data center and Virtual Private Cloud (VPC) for failover redundancy. This section describes how to design a dual\-line architecture with active\-standby redundancy, configure its routing, and provision sufficient bandwidth, ensuring seamless failover during faults.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Dual\-line is a specific form of multi\-line. The architectural solution and limits provided in this section also apply to multi\-line access scenarios.</div>


<span id=".6IOM5pmv5LuL57uN"></span>
## Background

A company needs to migrate some key services from its on\-premises data center (private CIDR block: `192.168.1.0/24`) in Beijing to VPC1 (private CIDR block: `172.16.1.0/24`) in the same region, ensuring interconnectivity via DC Connection. Due to the service's large user base and the critical impact of potential failures, the solution is to apply for two DC Connections (DAS201_port01_conn and DAS201_port02_conn) from different line operators, connect them to separate switches, and establish the connection between the on\-premises data center and the VPC using a dual\-line active\-standby redundancy​ architecture with static routing.

In the dual\-line active\-standby redundancy setup, all daily traffic is forwarded through the primary line, while the standby line remains in a hot\-standby state. If the primary line fails, traffic automatically fails over to the standby line to ensure business continuity. To ensure smooth path failover and uninterrupted business operations, plan your deployment considering the following three dimensions:


* **Architectural redundancy**:​ The two DC Connections should terminate at different access points to ensure availability in case of port, link, device, or access point failures.

* **Active\-standby routing and health check**: The two DC Gateways must be configured to form an active\-standby routing relationship **using specific and summary routes**. Specifically, the gateway for the primary line​ should be configured with a more specific route (longer prefix mask), while the gateway for the standby line​ should be configured with a summary route (shorter prefix mask) covering the entire destination CIDR block. After the DC Gateways are attached to the Cloud Enterprise Network (CEN), CEN will select the path based on the Longest Prefix Match​ principle, giving higher priority to the route with the longer mask. This establishes the active\-standby relationship between the two lines. Since static routes lack the automatic failure detection capability of BGP, you must configure line detection (e.g., BFD) for the lines. This enables rapid failure detection, route withdrawal for the affected path, and traffic switchover to the healthy line.

* **Bandwidth capacity**: To achieve high availability with dual\-line active\-standby redundancy, the standby line must have sufficient bandwidth to carry the entire business traffic when the primary line fails. Therefore, the standby line should use the same bandwidth specification​ as the primary line. Additionally, sufficient daily bandwidth headroom must be maintained on the primary line to prevent peak traffic from approaching the physical bandwidth cap.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Your dual\-line active\-standby redundancy solution must be deployed to meet all three dimensions above to ensure effective protection for your business traffic during failure scenarios.</div>



* <div data-tips="true" data-tips-type="warning">Architectural redundancy alone without primary/standby route or line detection configuration prevents traffic from automatically failing over to the healthy line during failure.</div>


* <div data-tips="true" data-tips-type="warning">Even if the architecture and routing are properly configured, packet loss may still occur after a failover if​ the healthy line lacks sufficient bandwidth capacity.</div>



**Network planning**


|DC interconnection |One DC Connection (Virtual Interface |Another DC Connection (Virtual Interface 2) |
|---|---|---|
|Cloud gateway peer IP |`10.0.0.1/30` |`10.0.0.5/30` |
|Your gateway peer IP |`10.0.0.2/30` |`10.0.0.6/30` |
|VLAN ID |10 |20 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Cloud gateway peer IP is the interconnect IP of the VPC, and Your gateway peer IP is the interconnect IP of your on\-premises data center.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created a VPC named VPC1 (private CIDR block: `172.16.1.0/24`) and its subnet. For procedure, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* You have created an Elastic Compute Service (ECS) instance (private IP address: `172.16.1.12`) within VPC1. For procedure, see [Buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id=".57qm5p2f6ZmQ5Yi2"></span>
## Limits


* The route type must be Static.

* Static routes with different priorities must be configured for both lines in the DC Gateway to distinguish the active and standby paths.

* When configuring a Virtual Interface, you must enable line detection and set the detection method to BFD (Bidirectional Forwarding Detection).

* Consider the following limits when connecting DC Connections:

   * Connect the two different DC Connections to switches at separate access points.

   * If connecting the two different DC Connections to separate switches, you must create two separate DC Gateways to associate with respective DC Connections.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5o6l5YWl54mp55CG5LiT57q_"></span>
### Step 1: Create a DC Connection

Activate two DC Connections, and connect them to separate switches. For procedure, see [Creating a Direct Connect Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1).  This example uses two DC Connections in China (Beijing): DAS201_port01_conn and DAS201_port02_conn, setting DAS201_port01_conn as Primary and DAS201_port02_conn as Secondary.

<span id=".5q2l6aqk5LqM77ya5Yib5bu65LiT57q_572R5YWz"></span>
### Step 2: Create a DC Gateway


1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway).

2. In the top menu bar, select the region: **China (Beijing)** .

3. Click **Create DC Gateway**.

4. Configure the DC Gateway based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Region |The region where the DC Gateway is deployed. It must match the region of the DC Connection. |China (Beijing) |
   |Name |Set the name for the DC Gateway. |Dcg\-01 |
   |ASN |Set an ASN for the DC Gateway. This example does not require a custom ASN and directly uses the BytePlus ASN. |137718 |
   |IPv6 |Enable IPv6 as needed. |Disable |
   |Project |Select the project to which the new DC Gateway belongs. |Project\-test |
   |Agreement |Follow the console guidance to review and accept the legal terms. |\- |
   

5. After confirming all parameters are correct, click **Buy now** to complete the action.

6. Click **Go to console** to return to the Direct Connect Gateway console. You can view the new DC gateway (Dcgw\-01) in the DC Gateway list.

7. Repeat steps 1\-5 to create another DC Gateway (Dcg\-02).


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
   |Name |Set the name for the Virtual Interface. |VIF\-01 |
   |DC Connection |Filter the DC Connection by project to associate with the Virtual Interface. |Project\-test\|DAS201_port01_conn |
   |DC Gateway |Filter the DC Gateway by project to associate with the Virtual Interface. |Project\-test\|Dcg\-01 |
   |Bandwidth limit |Enable bandwidth limit as needed. |Disable |
   |**Interconnection information** |||
   |IPv4 interconnect IP |Set the IPv4 IP for interconnection.<br><br><br>* Cloud gateway peer IP: Set an IPv4 address and mask for the cloud DC gateway. You may customize the interconnect IP according to network planning, but confirm that the cloud gateway peer IP and your gateway peer IP are in the same CIDR block without duplication. Use a private IP address that does not conflict with cloud or on\-premises IP addresses.<br><br>* Your gateway peer IP: Set an IPv4 address and mask for the gateway on your on\-premises data center. You may customize the interconnect IP according to network planning, but confirm that the cloud gateway peer IP and your gateway peer IP are in the same CIDR block without duplication. Use a private IP address that does not conflict with cloud or on\-premises IP addresses. |* Cloud gateway IP: 10.0.0.1/30​​<br><br>* Your gateway IP: 10.0.0.2/30​​ |
   |IPv6 interconnect IP |Enable IPv6 IP for interconnection as needed. |Disable |
   |VLAN ID |Set a VLAN ID for connecting to the data center. Confirm that this VLAN ID is unoccupied. Range: 0–2999.<br><br><br>* 0: The DC Connection's switch port operates in Layer 3 routing mode with no VLAN configured. This mode supports only a single untagged Virtual Interface per DC Connection.<br><br>* 1–2999: The DC Connection's switch port operates in Layer 3 sub\-interface mode. Each sub\-interface has a unique VLAN ID mapped to a separate Virtual Interface. This mode supports multiple Virtual Interfaces per DC Connection. |10 |
   |**Routing information** |||
   |Route type |Support two route types: BGP and Static. This example uses static routes. |Static |
   |BFD mode |Select the mode for the BFD detection. We recommend using BFD control packet. |BFD control packet |
   |Detect interval |The time interval for sending and receiving BFD packets. |1000 |
   |Detect multiplier |The number of BFD detection attempts. If a BFD session fails to receive the defined number of consecutive packets, the system declares a route failure. |3 |
   

4. After configuration, click **Create** to complete the creation.

5. Repeat steps 1\-4 to create another Virtual Interface with configurations listed in the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Virtual Interface owner |Select the account to which the Virtual Interface belongs. |My account |
   |Region |The region where the Virtual Interface is deployed. It must be the same region as the DC Connection and the DC Gateway. |China (Beijing) |
   |Name |Set the name for the Virtual Interface. |VIF\-02 |
   |DC Connection |Filter the DC Connection by project to associate with the Virtual Interface. |Project\-test\|DAS201_port02_conn |
   |DC Gateway |Select the DC Gateway to be associated with the Virtual Interface. |Dcg\-02 |
   |Bandwidth limit |Enable bandwidth limit as needed. |Disable |
   |**Interconnection information** |||
   |IPv4 interconnect IP |Set the IPv4 IP for interconnection.<br><br><br>* Cloud gateway peer IP: Set an IPv4 address and mask for the cloud DC gateway.<br><br>* Your gateway peer IP: Set an IPv4 address and mask for the gateway on your on\-premises data center. |* Cloud gateway peer IP: `10.0.0.5/30`<br><br>* Your gateway peer IP: `10.0.0.6/30` |
   |IPv6 interconnect IP |Enable IPv6 for interconnection as needed. |Disable |
   |VLAN ID |Set a VLAN ID for connecting to the data center. Confirm that this VLAN ID is not occupied. |20 |
   |**Routing information** |||
   |Route type |Select the route type. |Static |
   |BFD mode |Select the mode for the BFD detection. We recommend using BFD control packets. |BFD control packet |
   |Detect interval |The time interval for sending and receiving BFD packets. |1000 |
   |Detect multiplier |The number of BFD detection attempts. If a BFD session fails to receive the defined number of consecutive packets, the system declares a route failure. |3 |
   


<span id=".5q2l6aqk5Zub77ya5re75Yqg6Z2Z5oCB6Lev55Sx"></span>
### Step 4: Add a static route


1. Back to [the Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway), and click the name of the target DC Gateway  **(Dcg\-01)**  in the DC Gateway list.

2. Select the **Routing Information** tab.

3. Click **Add static route entry**, and configure the route.

   
   |Parameter |Value |
   |---|---|
   |Network type |IPv4 |
   |Destination CIDR |A destination CIDR block is the CIDR block of the on\-premises data center that needs to communicate with the VPC. In this example, it is `192.168.1.0/24`. |
   |Next Hop type |Virtual Interface |
   |Next Hop |VIF\-01 |
   

4. Click **Create** to complete configuration.

5. Back to the DC Gateway list, and click the name of the target DC Gateway  **(Dcg\-02)** .

6. Select the **Routing Information** tab.

7. Click **Add static route entry**, and configure the route.

   
   |Parameter |Value |
   |---|---|
   |Network type |IPv4 |
   |Destination CIDR |A destination CIDR block is the CIDR block of the on\-premises data center that needs to communicate with the VPC. In this example, it is `192.168.0.0/20`. |
   |Next Hop type |Virtual Interface |
   |Next Hop |VIF\-02 |
   

8. Click **Create** to complete configuration.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To form active\-standby redundancy on multi\-POP links, configure the two DC Gateways to advertise routes with different specificities (more specific and less specific). After attaching the gateways to a CEN, the system will utilize these routes to form primary and secondary paths within the CEN. In this example, one connection is configured as <code>192.168.1.0/24</code>, and another connection as <code>192.168.0.0/20</code>. Since CEN follows the <strong>longest prefix match</strong> principle to prioritize routes (where routes with longer subnet masks take precedence), one connection becomes the primary path while another connection serves as the secondary.</div>


<span id=".5q2l6aqk5LqU77ya5Yib5bu65LqR5LyB5Lia572R5bm25Yqg6L29572R57uc5a6e5L6L"></span>
### Step 5: Create a CEN and load a network instance


1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. Click **Create CEN**.

3. Configure the CEN based on the table below and load **VPC\-01**.

   
   |Parameter |Value |
   |---|---|
   |**Basic information** ||
   |Name |Cen\-test |
   |**Network Instances** ||
   |Attach Network Instance |Enable |
   |Region |China (Beijing) |
   |Instance type |VPC |
   |Network Instances |Project\-test\|VPC1 |
   |**More information** ||
   |Project |Project\-test |
   

4. Click **Create** to complete the action.

5. In the CEN instance list, click the name of the target instance  **(Cen\-test)** .

6. In the **Network Instances** tab, click **Attach Network Instance**.

7. The Attach Network Instance window pops up. Configure the information of the DC Gateway instance to be loaded, and then click **Attach** to complete the action.

   
   |Parameter |Value |
   |---|---|
   |Account |My account |
   |Region |China (Beijing) |
   |Instance type |DC Gateway |
   |Network Instances |Dcg\-01 |
   

8. Repeat steps 5\-7 to load another DC Gateway  **(Dcg\-02)** .


<span id=".5q2l6aqk5YWt77ya5ZyoRUNT5omA5bGe5a6J5YWo57uE5re75Yqg5a6J5YWo57uE6KeE5YiZ"></span>
### Step 6: Add a rule to the ECS security group


1. Log in to [the ECS console](https://console.byteplus.com/ecs/dashboard).

2. In the top menu bar, select the region: **China (Beijing)** .

3. In the left\-side navigation pane, click **Instances**. On the instance page, choose **Main private IP address** from the dropdown in the search box, and type `172.16.1.12` to search for the target ECS.

4. Click the name of the target ECS, and then click the **Security Group** tab.

5. Click the security group name. In the **Access rules** tab, click **Add rule** under the **Inbound rule** tab.


<span id=".5q2l6aqk5LiD77ya6YWN572u5pys5Zyw6Lev55Sx5ZKMTlFB5qOA5rWL"></span>
### Step 7: Configure on\-premises routing and BFD

Considering that two switches are connected separately to two switches at the on\-premises data center side, configurations must be applied on both switches. See the following code examples to configure routes at the data center side.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Configuration commands are vendor\-specific. These commands are for reference only. Adjust commands based on your device model. For details, consult your device vendor or see <a href="https://docs.byteplus.com/en/docs/directconnect/Configuration_examples_for_on-premises_data_centers_in_static_routing">Data center configuration reference</a>.</div>


**Reference commands**

Configuration command for switch 1 on primary line:

```Plain Text
# Configure static routes 
ip route 10.0.0.1 255.255.0.0 10.0.0.2 

# Enable BFD
bfd

# Configure BFD
interface HGE1/1/1
bfd detect-multiplier 3
bfd min-transmit-interval 1000
bfd min-receive-interval 1000
```


Configuration command for switch 2 on standby line:

```Plain Text
# Configure static routes 
ip route 10.0.0.5 255.255.0.0 10.0.0.6 

# Enable BFD
bfd

# Configure BFD
interface HGE1/1/1
bfd detect-multiplier 3
bfd min-transmit-interval 1000
bfd min-receive-interval 1000
```


<span id="izcGdqcF"></span>
### Step 8: Test connectivity


1. Run the `ping` command in the data center to verify connectivity to the DC Gateway network.

   * Ping Cloud gateway peer IP of the primary connection. In this example, `ping 10.0.0.1`.

   * Ping Cloud gateway peer IP of the secondary connection. In this example, `ping 10.0.0.5`.

   **Expected result**: Ping successful. The data center can communicate with the DC Gateway through the primary connection.

2. Execute the `ping` command in the data center to ping the private IP address of an ECS within the VPC. In this example, `ping 172.16.1.12` to verify connectivity to the ECS within the VPC.

   **Expected result**: Ping successful. The data center can access the ECS in the VPC through the primary connection.

3. Disconnect the primary connection to simulate a failure, and then execute the `ping` command in the data center to ping the private IP address of an ECS within the VPC. In this example, `ping 172.16.1.12` to verify connectivity to the ECS within the VPC.

   **Expected result**: Ping successful. Upon primary connection failure, traffic automatically switches to the secondary connection. The data center can access the ECS in the VPC through the secondary connection.
