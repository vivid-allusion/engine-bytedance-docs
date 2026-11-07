---
title: "Creating a Virtual Interface"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Creating-a-virtual-interface-1"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

After creating the Direct Connect (DC) Connection and Direct Connect Gateway, you need a Virtual Interface to associate the DC Connection with the DC Gateway.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic describes how to create and configure a Virtual Interface. For the procedure and configurations of a Shared Virtual Interface, log in using an account ​​with an active trial​ and see <a href="https://docs.byteplus.com/en/docs/directconnect/Create-shared-Direct-Connect-Virtual-Interface">Creating a Shared Virtual Interface</a> (this documentation is unavailable for accounts without trial activation).</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [DC Virtual Interface console](https://console.byteplus.com/dc/VirtualInterface).

2. In the top menu bar, select your target Region.

3. Click **Create DC Virtual Interface**.

4. Configure the Virtual Interface based on the table below.

   * **Basic information**

      
      |Parameter |Description |Sample value |
      |---|---|---|
      |Resource ownership |Select the account to which the Virtual Interface belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The feature of creating a Shared Virtual Interface for another account is currently in the beta stage. If you need a trial, please contact your account manager.</div><br> |My account |
      |Regions |Select the region for the Virtual Interface. It must be the same as the region to which the DC Connection and DC Gateway belong. |China (Beijing) |
      |Name |Set a name for the Virtual Interface. |VIF\-ad3hu |
      |DC Connection |Filter the target DC Connection by project to associate with the Virtual Interface. |default\|DAS\-236\-3_port1330\-conn |
      |Direct Connect Gateway |Filter the target DC Gateway by project to associate with the Virtual Interface.<br><br>If no DC Gateways are available, click "Create DC Gateway" to create a new DC Gateway. |default\|Dcg\-123 |
      |Bandwidth limit |Enable bandwidth limit as needed. If the VLAN ID of the Virtual Interface is 0, the outbound and inbound bandwidth caps for the virtual interface equal the bandwidth of the associated DC Connection regardless of whether bandwidth limit is enabled.<br><br><br>* Enable: Set limits on the Virtual Interface’s outbound and inbound bandwidths (from a VPC to a data center and from a data center to a VPC).<br><br>* Disable: Do not set limits on outbound and inbound bandwidths (from a VPC to a data center and from a data center to a VPC).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the associated DC Connection requires a QoS policy, do not enable bandwidth limit on the Virtual Interface.</div><br> |Check |
      |Bandwidth cap |The maximum bandwidth after enabling bandwidth limit. The maximum bandwidth for the Virtual Interface cannot exceed the bandwidth of the associated DC Connection. Reasonably allocate bandwidth based on service needs. |10 Mbps |
      

   * **Interconnection information**

      
      |Parameter |Description |Sample value |
      |---|---|---|
      |IPv4 interconnect IP |Type the IPv4 interconnect IP.<br><br><br>* Cloud gateway peer IP: Set an IPv4 address and mask for the cloud DC gateway. You may customize the interconnect IP according to network planning, but confirm that the cloud gateway peer IP and your gateway peer IP are in the same CIDR block without duplication.<br><br>   * We recommend using a private IP address which does not conflict with IP addresses both on the cloud and on\-premises. For more interconnect IP restrictions, see [Virtual Interface FAQs](https://docs.byteplus.com/en/docs/directconnect/Virtual-interface#.5Yib5bu66Jma5ouf5o6l5Y-j5pe25pys56uvSVDjgIHlr7nnq69JUOaYr-WQpuaciemZkOWItu-8nw==).<br><br>   * Unsupported CIDR blocks: `0.0.0.0/8`, `127.0.0.0/8`, `169.254.0.0/16`, `255.255.255.255`, `224.0.0.0` \- `239.255.255.255`, and `240.0.0.0` \- `255.255.255.254`.<br><br>* Your gateway peer IP: Set an IPv4 address and mask for the gateway on your on\-premises data center. You may customize the interconnect IP according to network planning, but confirm that the cloud gateway peer IP and your gateway peer IP are in the same CIDR block without duplication. Use a private IP address that does not conflict with cloud or on\-premises IP addresses. |* Cloud gateway peer IP: 10.0.0.1/30<br><br>* Your gateway IP: 10.0.0.2/30​​ |
      |IPv6 interconnect IP |Specify whether to enable IPv6 interconnect IP. Once enabled, it cannot be disabled. To enable IPv6 interconnect IP, you must confirm that the Virtual Interface's associated DC Gateway has IPv6 enabled.<br><br><br>* Cloud gateway peer IPv6: Enable parameters of IPv6 interconnect IP, set an IPv6 address and mask for the DC Gateway on the cloud. Type the correct IPv6 address. For more peer IP restrictions, see [Virtual Interface FAQs](https://docs.byteplus.com/en/docs/directconnect/Virtual-interface#.5Yib5bu66Jma5ouf5o6l5Y-j5pe25pys56uvSVDjgIHlr7nnq69JUOaYr-WQpuaciemZkOWItu-8nw==).<br><br>* Your gateway peer IPv6: Enable parameters of IPv6 interconnect IP, set an IPv6 address and mask for the gateway on your on\-premises data center. Type the correct IPv6 address.<br><br>* Unsupported CIDR blocks: `FC01:A9FE::0/64` and `FE80:0:0:0:A9FE::/80`. |* Cloud gateway peer IPv6: 2408:4004:cc:400::1/56<br><br>* Your gateway peer IPv6: 2408:4004:cc:400::2/56 |
      |VLAN ID |Set the VLAN ID for connecting to the data center. Range: 0–2999.<br><br><br>* 0: The DC Connection's switch port operates in Layer 3 routing mode with no VLAN configured. This mode supports only a single untagged Virtual Interface per DC Connection.<br><br>* 1–2999: The DC Connection's switch port operates in Layer 3 sub\-interface mode. Each sub\-interface has a unique VLAN ID mapped to a separate Virtual Interface. This mode supports multiple Virtual Interfaces per DC Connection.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For the scenario where the DC Connection associated with a Virtual Interface is a Dedicated Line, ensure that the VLAN trunking feature for your specific VLAN tag is enabled on all Layer 2 and Layer 3 devices along the entire path. This path includes the line operator's DC connection, the DC Gateway, and your on\-premises data center. That is, all related devices can identify your VLAN tag and allow traffic without VLAN translation.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Each DC Connection on the same switch must have a unique VLAN ID.</div><br> |10 |
      

   * **Routing information**

      
      |Parameter |Description |Sample value |
      |---|---|---|
      |Route type |Support two route types: BGP (recommended) and Static.<br><br><br>* **BGP**: BGP routes, for which you need to configure BGP information (such as Peer ASN and BGP key) and establish a BGP Peer.<br><br>   * If the BGP information (Peer ASN and BGP key) is configured, a BGP Peer will be established along with the creation of the Virtual Interface. Once created, the BGP information cannot be modified.<br><br>   * If you do not configure BGP information (Peer ASN and BGP key), only the Virtual Interface will be created without establishing a BGP Peer After successful creation of the Virtual Interface, you need to configure the BGP Peer separately. For procedure, see [Adding a BGP Peer](https://docs.byteplus.com/en/docs/directconnect/Adding-a-BGP-peer).<br><br>* **Static**: Static routes. After successful creation of the Virtual Interface, go to the detail page of the **DC Gateway** associated with the Virtual Interface. In the **Routing information** tab, configure the static route to the data center. For procedure, see [Adding a static route](https://docs.byteplus.com/en/docs/directconnect/Adding-a-static-route-entry). |BGP |
      |Peer ASN |This parameter appears only for **BGP routes**. Type the ASN of the BGP Peer. In the BGP protocol, each independent AS has a globally unique ASN.<br><br><br>* Type the ASN of the BGP Peer. Valid range: 1 to 4294960000.<br><br>* The ASNs of the BGP Peer and the DC Gateway must be different.<br><br>* The ASN of the BGP Peer must not be 137718, which is the BytePlus ASN.<br><br>* If IPv6 interconnect IP capability is enabled, type in Peer ASNs for IPv4 and IPv6 separately.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the DC Gateway uses the BytePlus ASN (137718), confirm the Peer ASN is different from 137718.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the DC Gateway uses a custom ASN, the Peer ASN must be neither the custom ASN nor 137718.</div><br> |46000 |
      |BGP key |A parameter that appears only when the route type is **BGP**. Type your BGP Peer password.<br><br><br>* Must be 6\-80 characters in length. May include numbers, lowercase and uppercase letters, and symbols: ` \| ! ~ @ # $ % ^ ( ) \- _ + = [ ] { } , . / : ;，<br><br>* If the IPv6 interconnect IP capability is enabled, type in BGP keys for IPv4 and IPv6 separately.<br><br>* The BGP key is a sensitive credential. Store it securely to avoid compromise or disclosure. |E0g5\*\*\*\*d8go1 |
      |Detection method |Set the method for line detection. Different detection methods vary in different route types. **BGP routes support BFD, and static routes support BFD and NQA**.<br><br><br>* **Disable**: Do not enable line detection.<br><br>* [BFD](https://docs.byteplus.com/en/docs/directconnect/Virtual-interface#.5LuA5LmI5pivQkZE5qOA5rWL77yf): Enable BFD as the detection method.<br><br>* [NQA](https://docs.byteplus.com/en/docs/directconnect/Virtual-interface#.5LuA5LmI5pivTlFB5qOA5rWL77yf): Enable NQA as the detection method.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The NQA feature is currently in the beta stage. If you need a trial, please contact your account manager. For details of BFD and NQA, see <a href="https://docs.byteplus.com/en/docs/directconnect/Detection_methods">Detection methods</a>.</div><br> |BFD |
      |BFD mode |A parameter that appears only when the detection method is **BFD**, supporting the following two modes:<br><br><br>* BFD control packet (default): Send BFD control packets to detect bidirectional path reachability between network devices. The data center must establish a BFD session and exchange packets.<br><br>* BFD echo packet: BytePlus sends BFD echo packets, and the data center returns them to quickly detect reachability between network devices. The data center only forwards echo packets.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The BFD echo packet feature is currently in the beta stage. If you need a trial, please contact your account manager.</div><br> |BFD control packet |
      |Detect interval |Set the detect interval, including the sending and receiving intervals of probe packets. |1000 |
      |Detect multiplier |Set a number for detection attempts. If a session fails to receive the defined number of consecutive packets, the system declares a route failure. |8 |
      

   * **Advanced option**

      
      |Parameter |Description |Sample value |
      |---|---|---|
      |Tags |A tag consists of a Tag key (Key) and a Tag value (Value), and can be used to classify and search Virtual Interfaces.<br><br><br>* Click the <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_745f4ea6f3f698cebd9adc96c9240260.png) </span> icon to add multiple tags. You can add up to 20 tags per action, and up to 50 tags for a single Virtual Interface.<br><br>* The Keys of multiple tags for the same Virtual Interface must be unique. Each Key can have only one Value.<br><br>* The Key and the Value are case\-sensitive. For example, the Key=tag and the Key=Tag are two different Keys. For more information, see [Tag management](https://docs.byteplus.com/en/docs/directconnect/Tag-management). |key:test |
      

5. Click **Create** to complete the action.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next


|Documentation |Action description |
|---|---|
|[Adding a static route](https://docs.byteplus.com/en/docs/directconnect/Adding-a-static-route-entry) |If the Virtual Interface uses **static routes**, you also need to configure static routes on your data center for the DC Gateway associated with the Virtual Interface. |
|[Adding a BGP Peer](https://docs.byteplus.com/en/docs/directconnect/Adding-a-BGP-peer) |If the Virtual Interface uses **BGP routes** without configuring BGP parameters at its creation, you also need to establish a BGP Peer on your data center for the DC Gateway associated with the Virtual Interface. |
|[Configuring on-premises routing and test connectivity](https://docs.byteplus.com/en/docs/directconnect/Configuring-a-local-route-and-testing-connectivity) |According to the actual line route type, configure the route on the switch in a data center and perform a connectivity test. For more examples of local route configurations, see the **Data center configuration samples** section under [Best Practices](https://docs.byteplus.com/en/docs/directconnect/best-practices-overview) in this documentation. |


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateDirectConnectVirtualInterface](https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectVirtualInterface): Create a Virtual Interface.
