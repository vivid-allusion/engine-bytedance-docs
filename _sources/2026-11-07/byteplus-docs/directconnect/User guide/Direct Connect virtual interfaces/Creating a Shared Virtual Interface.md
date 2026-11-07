---
title: "Creating a Shared Virtual Interface"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Create-shared-Direct-Connect-Virtual-Interface"
---

This topic describes how to create a Shared Virtual Interface.

<span id=".5LuA5LmI5piv5YWx5Lqr6Jma5ouf5o6l5Y-j"></span>
## What is a Shared Virtual Interface

BytePlus's Direct Connect (DC) service supports the capability to share Virtual Interfaces across BytePlus accounts. You can create a Shared Virtual Interface for another BytePlus account, enabling multiple accounts to share a single DC Connection. This reduces costs while allowing resource management by accounts.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In this documentation, <strong>an account</strong> is a BytePlus account.</div>


* <div data-tips="true" data-tips-type="tip"><strong>A Shared Virtual Interface</strong> is a Virtual Interface created by Account A for the exclusive use of Account B. Account A cannot use it. It does not allow multiple accounts to use the same virtual interface simultaneously.</div>


* <div data-tips="true" data-tips-type="tip">The Shared Virtual Interface is currently in the beta stage. If you need a trial, please contact your account manager.</div>



<span id=".57qm5p2f6ZmQ5Yi2"></span>
### Limits

The account that creates a Shared Virtual Interface (Account A) cannot use it. It is solely for another account (Account B).

<span id=".5Zy65pmv6K-05piO"></span>
### Scenario notes

In the Shared Virtual Interface scenario, resources involved are from two or more accounts. Many differences exist compared to the Dedicated Virtual Interface scenario, as shown in the table below:


|Difference |Account A (who creates the Shared Virtual Interface) |Account B (who uses the Shared Virtual Interface) |
|---|---|---|
|Resource ownership |DC Connection |* Direct Connect Gateway<br><br>* Shared Virtual Interface |
|Incurred fees |Pay the port occupancy fee of the DC Connection. For more details, see [Port occupancy fee](https://docs.byteplus.com/en/docs/directconnect/Billing-overview). |Pay the outbound traffic fee. For details, see [Outbound traffic fee](https://docs.byteplus.com/en/docs/directconnect/Billing-overview). |
|Owned quota |Account A creates a Shared Virtual Interface, which counts toward Account A's quota for **associated Virtual Interfaces per DC Connection**. The quota of Virtual Interfaces associated with a single DC Connection is 5 and non\-increasable. |* If Account B has not accepted a Shared Virtual Interface, it does not count toward Account B's quota.<br><br>* The Shared Virtual Interface accepted by Account B counts toward Account B's **quota for associated Virtual Interfaces per DC Gateway**. You can associate up to 8 Virtual Interfaces with a single DC Gateway. To increase the quota, see [Quota management](https://docs.byteplus.com/en/docs/directconnect/Quota_management) for details. |
|Resource management |* DC Connection: Full operational and management permissions<br><br>* Shared Virtual Interface:<br><br>   * Manage bandwidth limit, interconnect IP, VLAN ID, detection methods, and other settings of the Shared Virtual Interface.<br><br>   * Delete a Shared Virtual Interface unassociated with a DC Gateway, and remove all data of the Shared Virtual Interface. |* DC Gateway: Full operational and management permissions<br><br>* BGP Peer: Full operational and management permissions<br><br>* Static route: Full operational and management permissions<br><br>* Shared Virtual Interface:<br><br>   * Accept or reject a Shared Virtual Interface.<br><br>   * Deleting the Shared Virtual Interface on Account B does not remove it from Account A. |


<span id=".5Yib5bu65YWx5Lqr6Jma5ouf5o6l5Y-j"></span>
## Create a Shared Virtual Interface

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Before you go


* The account creating a Shared Virtual Interface (hereafter referred to as Account A) must have the Shared Virtual Interface feature enabled and an available DC Connection that has not reached its virtual interface limit. For the procedure, see [Creating a Direct Connect Connection](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1).

* Account A has obtained the account ID and region of Account B (which uses the Shared Virtual Interface). It has confirmed the configurations of the Shared Virtual Interface (such as network settings and bandwidth) with Account B.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The Shared Virtual Interface is currently in the beta stage. If you need a trial, please contact your account manager.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Use Account A to log in to the BytePlus [DC Virtual Interface console](https://console.byteplus.com/dc/VirtualInterface).

2. In the top menu bar, select your target region.

3. Click **Create DC Virtual Interface**.

4. Configure the Virtual Interface based on the table below.

   * **Basic information**

      
      |Parameter |Description |Sample value |
      |---|---|---|
      |Resource ownership |Select the account to which the Virtual Interface belongs. To create a Shared Virtual Interface, select **Another account**. |Another account |
      |Owner account ID |ID of the BytePlus account that uses the Shared Virtual Interface. |2100052\*\*\*\* |
      |Regions |Select the region for the Virtual Interface. It must be the same as the region to which the DC Gateway of the account using the Shared Virtual Interface belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Confirm the region with the account using the Shared Virtual Interface in advance. After creation, the user account can only use this Shared Virtual Interface in the currently selected region.</div><br> |China (Beijing) |
      |Name |Set a name for the Ethernet Virtual Interface. |VIF\-share01 |
      |DC Connection |Filter by project and select the new Shared Virtual Interface to associate with a DC Connection<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The DC Connection used for a Shared Virtual Interface does not support QoS policies.</div><br> |Project\-01\|DAS\-236\-3_port1330\-conn |
      |Bandwidth limit |Enable bandwidth limit as needed.<br><br><br>* Enable: Set limits on the Virtual Interface’s outbound and inbound bandwidths (from a VPC to a data center and from a data center to a VPC).<br><br>* Disable: Do not set limits on outbound and inbound bandwidths (from a VPC to a data center and from a data center to a VPC). |Check |
      |Bandwidth cap |The maximum bandwidth after enabling bandwidth limit. The maximum bandwidth for the Virtual Interface cannot exceed the bandwidth of the associated DC Connection. Reasonably allocate bandwidth based on service needs. |10 Mbps |
      

   * **Interconnection information**

      
      |Parameter |Description |Sample value |
      |---|---|---|
      |IPv4 interconnect IP |Type the IPv4 interconnect IP.<br><br><br>* Cloud gateway peer IP: Set an IPv4 address and mask for the cloud DC gateway. You may customize the interconnect IP according to network planning, but confirm that the cloud gateway peer IP and your gateway peer IP are in the same CIDR block without duplication.<br><br>   * We recommend using a private IP address which does not conflict with IP addresses both on the cloud and on\-premises. For more interconnect IP restrictions, see [Virtual Interface FAQs](https://docs.byteplus.com/en/docs/directconnect/Virtual-interface).<br><br>   * Unsupported CIDR blocks: `0.0.0.0/8`, `127.0.0.0/8`, `169.254.0.0/16`, `255.255.255.255`, `224.0.0.0` \- `239.255.255.255`, and `240.0.0.0` \- `255.255.255.254`.<br><br>* Your gateway peer IP: Set an IPv4 address and mask for the gateway on your on\-premises data center. You may customize the interconnect IP according to network planning, but confirm that the cloud gateway peer IP and your gateway peer IP are in the same CIDR block without duplication. Use a private IP address that does not conflict with cloud or on\-premises IP addresses. |* Cloud gateway peer IP: 10.0.0.1/30<br><br>* Your gateway peer IP: 10.0.0.2/30​​ |
      |VLAN ID |Set the VLAN ID for connecting to the data center. Range: 0–2999.<br><br><br>* 0: The DC Connection's switch port operates in Layer 3 routing mode with no VLAN configured. This mode supports only a single untagged Virtual Interface per DC Connection.<br><br>* 1–2999: The DC Connection's switch port operates in Layer 3 sub\-interface mode. Each sub\-interface has a unique VLAN ID mapped to a separate Virtual Interface. This mode supports multiple Virtual Interfaces per DC Connection.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Each DC Connection on the same switch must have a unique VLAN ID.</div><br> |10 |
      

   * **Routing information**

      
      |Parameter |Description |Sample value |
      |---|---|---|
      |Route type |Support two route types: BGP (recommended) and Static.<br><br><br>* **BGP**: BGP routes. After a Shared Virtual Interface is created, use the account using the virtual interface (Account B) to establish a BGP Peer. For procedure, see [Adding a BGP Peer](https://docs.byteplus.com/en/docs/directconnect/Adding-a-BGP-peer).<br><br>* **Static**: Static routes. After a Shared Virtual Interface is created, use the account using the virtual interface (Account B) to configure the static route to the data center. For procedure, see [Adding a static route](https://docs.byteplus.com/en/docs/directconnect/Adding-a-static-route-entry). |BGP |
      |Detection method |Set the method for line detection. Different detection methods vary in different route types. **BGP routes support BFD, and static routes support BFD and NQA**.<br><br><br>* **Disable**: Do not enable line detection.<br><br>* [BFD](https://docs.byteplus.com/en/docs/directconnect/Virtual-interface#.5LuA5LmI5pivQkZE5qOA5rWL77yf): Enable BFD as the detection method.<br><br>* [NQA](https://docs.byteplus.com/en/docs/directconnect/Virtual-interface#.5LuA5LmI5pivTlFB5qOA5rWL77yf): Enable NQA as the detection method.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The NQA feature is currently in the beta stage. If you need a trial, please contact your account manager. For details of BFD and NQA, see <a href="https://docs.byteplus.com/en/docs/directconnect/Detection_methods">Connection health detection mode</a>.</div><br> |BFD |
      |BFD mode |A parameter that appears only when the detection method is **BFD**, supporting the following two modes:<br><br><br>* BFD control packet (default): Send BFD control packets to detect bidirectional path reachability between network devices. The data center must establish a BFD session and exchange packets.<br><br>* BFD echo packet: BytePlus sends BFD echo packets, and the data center returns them to quickly detect reachability between network devices. The data center only forwards echo packets.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The BFD echo packet feature is currently in the beta stage. If you need a trial, please contact your account manager.</div><br> |BFD control packet |
      |Detect interval |Set the detect interval, including the sending and receiving intervals of probe packets. |1000 |
      |Detect multiplier |Set a number for detection attempts. If a session fails to receive the defined number of consecutive packets, the system declares a route failure. |8 |
      

   * **Advanced option**

      
      |Parameter |Description |Sample value |
      |---|---|---|
      |Tags |A tag consists of a tag key (Key) and a tag value (Value), and can be used to classify and search Virtual Interfaces.<br><br><br>* Click the <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_745f4ea6f3f698cebd9adc96c9240260.png) </span> icon to add multiple tags. You can add up to 20 tags per action, and up to 50 tags for a single Virtual Interface.<br><br>* The Keys of multiple tags for the same Virtual Interface must be unique. Each Key can have only one Value.<br><br>* The Key and the Value are case\-sensitive. For example, the Key=tag and the Key=Tag are two different Keys. For more information, see [Tag management](https://docs.byteplus.com/en/docs/directconnect/Tag-management).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Tags configured when creating a Shared Virtual Interface are only visible to the account creating the Shared Virtual Interface (Account A) and not to the account using it (Account B).</div><br> |share:01 |
      

5. Click **Create** to complete the action.


<span id=".5pON5L2c57uT5p6c"></span>
### Results

After creation, the Shared Virtual Interface appears in the DC Virtual Interface console for both accounts with different statuses: Pending confirmation for Account A and Pending acceptance for Account B.

<span id=".5ZCO57ut5pON5L2c"></span>
### What to do next

[Accept a Shared Virtual Interface](https://docs.byteplus.com/en/docs/directconnect/Accept-shared-Direct-Connect-Virtual-Interface): Account B accepts and uses a Shared Virtual Interface.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[AllocateDirectConnectVirtualInterface](https://docs.byteplus.com/en/docs/directconnect/AllocateDirectConnectVirtualInterface): Create a Shared Virtual Interface.
