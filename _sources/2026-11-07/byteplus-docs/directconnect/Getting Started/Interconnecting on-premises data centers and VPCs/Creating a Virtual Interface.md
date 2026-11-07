---
title: "Creating a Virtual Interface"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Creating-a-virtual-interface"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

A Virtual Interface is a logical interface established over a Direct Connect (DC) Connection, enabling communication between your on\-premises data center (IDC) and different Virtual Private Clouds (VPCs). It supports two routing modes: static routing and BGP routing. This example uses BGP routing.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [DC Virtual Interface console](https://console.byteplus.com/dc/VirtualInterface).

2. Click **Create DC Virtual Interface**.

3. Configure the Virtual Interface based on the table below.

   * **Basic information**

      
      |Parameters |Description |Sample value |
      |---|---|---|
      |Resource ownership |Select the account to which the Virtual Interface belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The feature of creating a Shared Virtual Interface for another account is currently in the beta stage. If you need a trial, please contact your account manager.</div><br> |My account |
      |Regions |Select the region where the Virtual Interface is deployed. It must be the same as the region of the DC Connection and the DC Gateway. |China (Beijing) |
      |Name |Set a name for the Ethernet Virtual Interface. |VIF\-ds123 |
      |DC Connection |Select the DC Connection and the Project it belongs to, to associate with the virtual interface. |default\|DAS123_port308_conn |
      |Direct Connect Gateway |Select the Direct Connect Gateway and the Project it belongs to, to associate with the virtual interface. |default\|Dcg\-123 |
      |Bandwidth limit |Enable bandwidth limit as needed. Enabling Bandwidth limit restricts the bandwidth of the virtual interface. Disabling Bandwidth limit means the virtual interface's bandwidth is unrestricted. |Check |
      |Bandwidth cap |The maximum bandwidth after enabling bandwidth limit. The maximum bandwidth for the Virtual Interface cannot exceed the bandwidth of the associated DC Connection. Reasonably allocate bandwidth based on service needs. |10 Mbps |
      

   * **Interconnection information**

      
      |Parameters |Description |Sample value |
      |---|---|---|
      |IPv4 interconnect IP |Type the IPv4 interconnect IP. |\-\- |
      |Cloud gateway peer IP |Set an IPv4 address and mask for the cloud DC gateway. You may customize the interconnect IP according to network planning, but confirm that the cloud gateway peer IP and your gateway peer IP are in the same CIDR block without duplication. Use a private IP address that does not conflict with cloud or on\-premises IP addresses. |10.0.0.1/24 |
      |Your gateway IP |Set an IPv4 address and mask for the gateway on your on\-premises data center. You may customize the interconnect IP according to network planning, but confirm that the cloud gateway peer IP and your gateway peer IP are in the same CIDR block without duplication. Use a private IP address that does not conflict with cloud or on\-premises IP addresses. |10.0.0.2/24 |
      |VLAN ID |Set a VLAN ID for connecting to the data center. Confirm that this VLAN ID is unoccupied. |10 |
      

   * **Routing information**

      
      |Parameters |Description |Sample value |
      |---|---|---|
      |Route type |Supports two routing types: BGP routing and Static routing. This example uses BGP routing. BGP information (BGP Peer ASN, BGP key) cannot be modified after the virtual interface is successfully created. |BGP |
      |Peer ASN |Enter the ASN for the IPv4 BGP peer. The valid ASN range is 1 to 4294960000. It must not be the same as the Direct Connect Gateway's ASN, nor can it be BytePlus's ASN (137718). |46000 |
      |BGP key |Enter the BGP key for the IPv4 BGP Peer (This parameter only appears when the routing type is "BGP"). |E0g5\*\*\*\*8go1 |
      |Detection method |Select the detection method for the line. |Disable |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">This example demonstrates only example values for required parameters. For more parameter details, see <a href="https://docs.byteplus.com/en/docs/directconnect/Creating-a-virtual-interface-1">Creating a Virtual Interface</a>. Example values are for reference only and have no practical significance.      </div>
      

4. After configuration, click **Create** to complete the creation.

   At this point, the following resources have been requested: DC Connection DAS123_port308_conn, the Direct Connect Gateway dcgw\-123, and Virtual Interface VIF\-ds123. VIF\-ds123 has been associated with both DAS123_port308_conn and dcgw\-123.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next


* [Attach a network instance](https://docs.byteplus.com/en/docs/directconnect/Loading-a-network-instance)

* [Configure on-premises routing and test connectivity](https://docs.byteplus.com/en/docs/directconnect/Configuring-a-local-route-and-testing-connectivity)
