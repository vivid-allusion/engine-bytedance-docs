---
title: "Tenant guide"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Tenant-operation-guide"
---

This topic guides tenants, as users of the shared Direct Connect (DC), on how to connect their on\-premises data center to the cloud via Shared Line.

<span id=".5pON5L2c6ZmQ5Yi2"></span>
## Limits


* Tenants cannot view monitoring data of the Shared Line.

* After accepting the Shared Line, tenants can only create one Virtual Interface for this line. That is, the ratio between the Shared Line and the Virtual Interface is 1:1.

* Tenants cannot modify the VLAN ID of the Shared Line. When creating a Virtual Interface for the Shared Line, the tenant cannot modify the VLAN ID for the interface instance, which is inherited from the Shared Line.

* Tenants cannot directly modify the bandwidth of the Shared Line. To modify, tenants must contact the line operator who supports the Shared Line.

* The QoS policy feature is unavailable for Shared Lines under a tenant account, but available for Dedicated Lines under this account.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permission notes

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The accepted Shared Line belongs to the tenant account's <strong>default</strong> project by default. You can transfer the Shared Line into another project based on your requirements. For procedure, see <a href="https://docs.byteplus.com/en/docs/6649/94337">Project resource management</a>.</div>


* <div data-tips="true" data-tips-type="warning">Non\-global IAM users (who do not have full permissions) cannot view Virtual Interfaces. Configure a custom policy to authorize the IAM user. For procedure, see <a href="https://docs.byteplus.com/en/docs/directconnect/Common-system-default-policies">Custom policy examples</a>.</div>



<span id=".55u45YWz5pON5L2c"></span>
## Related actions

<span id=".5o6l5Y-X5YWx5Lqr5LiT57q_5bm25pSv5LuY56uv5Y-j5Y2g55So6LS5"></span>
### Accept a Shared Line and pay the port occupancy fee

<span id=".5YmN5o-Q5p2h5Lu2"></span>
#### Prerequisites

The line operator has created a Shared Line for your account.

<span id=".5pON5L2c5q2l6aqk"></span>
#### Procedure


1. Use a tenant account to log in to the BytePlus [Direct Connect Connection console](https://console.byteplus.com/dc/PhysicalConnection).

2. On the **Direct Connect Connection** page, you can view the Shared Line created by the line operator for the current tenant account. The status of Shared Line is **Pending acceptance**.

3. Click **Accept** in the **Actions** column of the Shared Line to be accepted.

4. In the pop\-up dialog box, confirm the details (such as the region and bandwidth) are correct, and then click **Accept**.

5. In the **Pay Port Occupancy Fee** dialog box that pops up after you accept the Shared Line, configure the parameters based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Billing method |Billing method of Shared Line port resources. Supports only Subscription. |Subscription |
   |Duration |Usage duration of Shared Line port resources. |1 month |
   |Automatic renewal |Enable automatic renewal as needed. If automatic renewal is enabled, the renewal length is one month and the number of renewals is unlimited. You can manually disable automatic renewal or access **the Billing center** to modify the number of renewals. For port resources that you rely on for the long term, we recommend checking Automatic renewal to prevent any disruption when they expire. |Disable |
   

6. Follow the console guidance to review and accept the Legal, and click **Pay now**.

7. Click **Next step**, select a payment method, and then click **Pay**.

8. Make the payment by the selected method. After submitting the payment information, complete the payment within the specified time. Otherwise, the order will be canceled.

9. Once the payment is complete, the DC Connection status becomes **Opened**. The DC Connection is available for use.


<span id=".5Yib5bu65LiT57q_572R5YWz"></span>
### Create a DC Gateway

The procedure to create a DC Gateway for a Shared Line is the same as for the Dedicated Line. For details, see [Creating a Direct Connect Gateway](https://docs.byteplus.com/en/docs/directconnect/Creating-a-Direct-Connect-gateway-1).

<span id=".5Yib5bu66Jma5ouf5o6l5Y-j"></span>
### Create a Virtual Interface

<span id=".5pON5L2c6K-05piO"></span>
#### Instructions


* You can only create Virtual Interfaces for accepted Shared Lines.

* You can only create a Virtual Interface per Shared Line.


<span id=".5pON5L2c5q2l6aqk"></span>
#### Procedure


1. Use a tenant account to log in to the BytePlus [DC Virtual Interface console](https://console.byteplus.com/dc/VirtualInterface).

2. In the top menu bar, select your target region.

3. Click the name of the target Shared Line.

4. Select the **DC Virtual Interface** tab, and then click **Create DC Virtual Interface**.

5. Configure the Virtual Interface based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Resource ownership |Select the account to which the Virtual Interface belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The feature of creating a Shared Virtual Interface for another account is currently in the beta stage. If you need a trial, please contact your account manager.</div><br> |My account |
   |Regions |The region for the Virtual Interface, which is fixed to the region of the current Shared Line. |China (Beijing) |
   |Name |Set a name for the Ethernet Virtual Interface. |VIF\-sg2x |
   |DC Connection |Fixed to the current Shared Line. |DAS\-26\-3_port10\-conn\-12 |
   |DC Gateway |Filter the target DC Gateway by project to associate with the Virtual Interface.<br><br>If no DC Gateways are available, click **Create DC Gateway** to create a new DC Gateway. |Project\-01\|Dcg\-test |
   |Bandwidth limit |Limit outbound traffic of the Virtual Interface. This feature is enabled by default and cannot be modified. |Check |
   |Bandwidth cap |Fixed to the bandwidth of the current Shared Line. Cannot be modified. |100 Mbps |
   |**Interconnection information** |||
   |IPv4 interconnect IP |Type the IPv4 interconnect IP.<br><br><br>* **Cloud gateway peer IP**: Set an IPv4 address and mask for the cloud DC gateway. You may customize the interconnect IP according to network planning, but confirm that the cloud gateway peer IP and your gateway peer IP are in the same CIDR block without duplication.<br><br>   * We recommend using a private IP address which does not conflict with IP addresses both on the cloud and on\-premises. For more interconnect IP restrictions, see [Direct Connect Virtual Interface FAQs](https://docs.byteplus.com/en/docs/directconnect/Virtual-interface).<br><br>   * Unsupported CIDR blocks: `0.0.0.0/8`, `127.0.0.0/8`, `169.254.0.0/16`, `255.255.255.255`, `224.0.0.0` \- `239.255.255.255`, and `240.0.0.0` \- `255.255.255.254`.<br><br>* **Your gateway peer IP**: Set an IPv4 address and mask for the gateway on your on\-premises data center. You may customize the interconnect IP according to network planning, but confirm that the cloud gateway peer IP and your gateway peer IP are in the same CIDR block without duplication. Use a private IP address that does not conflict with cloud or on\-premises IP addresses. |* Cloud gateway IP: 10.0.0.1/30​​<br><br>* Your gateway IP: 10.0.0.2/30​​ |
   |IPv6 interconnect IP |Specify whether to enable IPv6 interconnect IP. If enabled, you must configure the Cloud gateway peer IPv6 and Your gateway peer IPv6. Once enabled, disabling is unsupported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To enable IPv6 interconnect IP, you must confirm that the Virtual Interface's associated <strong>DC Gateway</strong> has IPv6 enabled. To enable IPv6 for a DC Gateway, see <a href="https://docs.byteplus.com/en/docs/directconnect/turn-on-dc-gateway-ipv6">Enabling IPv6</a>.</div><br><br><br><br>* **Cloud gateway peer IPv6**: Enable parameters of IPv6 interconnect IP, set an IPv6 address and mask for the DC Gateway on the cloud. Type the correct IPv6 address. For more peer IP restrictions, see [Direct Connect Virtual Interface FAQs](https://docs.byteplus.com/en/docs/directconnect/Virtual-interface).<br><br>* **Your gateway peer IPv6**: Enable parameters of IPv6 interconnect IP, set an IPv6 address and mask for the gateway on your on\-premises data center. Type the correct IPv6 address.<br><br>* Unsupported CIDR blocks: `FC01:A9FE::0/64` and `FE80:0:0:0:A9FE::/80`. |Disable |
   |VLAN ID |The VLAN ID to connect an on\-premises data center. It is fixed to the VLAN ID of the selected Shared Line and cannot be modified. |10 |
   |**Routing information** |||
   |Route type |Support two route types: BGP (recommended) and Static.<br><br><br>* **BGP**: BGP routes, for which you need to configure BGP information (such as Peer ASN and BGP key) and establish a BGP Peer.<br><br>   * If the BGP information (Peer ASN and BGP key) is configured, a BGP Peer will be established along with the creation of the Virtual Interface. Once created, the BGP information cannot be modified.<br><br>   * If you do not configure BGP information (Peer ASN and BGP key), only the Virtual Interface will be created without establishing a BGP Peer. After successful creation of the Virtual Interface, you need to configure the BGP Peer separately. For procedure, see [Adding a BGP Peer](https://docs.byteplus.com/en/docs/directconnect/Adding-a-BGP-peer).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To create a Shared Virtual Interface for another account, create a BGP Peer under the account who uses the shared Virtual Interface. For procedure, see <a href="https://docs.byteplus.com/en/docs/directconnect/Adding-a-BGP-peer">Adding a BGP Peer</a>.   </div><br>   <br><br>* **Static**: Static routes. After successful creation of the Virtual Interface, go to the detail page of the DC Gateway associated with the Virtual Interface. In the Routing information tab, configure the static route to the data center. For procedure, see [Adding a static route](https://docs.byteplus.com/en/docs/directconnect/Adding-a-static-route-entry).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To create a Shared Virtual Interface for another account, configure the static route under the account who uses the shared Virtual Interface. For procedure, see <a href="https://docs.byteplus.com/en/docs/directconnect/Adding-a-static-route-entry">Adding a static route</a>.   </div><br>    |BGP |
   |Peer ASN |This parameter appears only for **BGP routes**. Type the ASN of the BGP Peer. In the BGP protocol, each independent AS has a globally unique ASN.<br><br><br>* Type the ASN of the BGP Peer. Valid range: 1 to 4294960000.<br><br>* The ASNs of the BGP Peer and the DC Gateway must be different.<br><br>* The ASN of the BGP Peer must not be 137718, which is the BytePlus ASN.<br><br>* If IPv6 interconnect IP capability is enabled, type in Peer ASNs for IPv4 and IPv6 separately.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the DC Gateway uses the BytePlus ASN (137718), confirm the Peer ASN is different from 137718.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the DC Gateway uses a custom ASN, the Peer ASN must be neither the custom ASN nor 137718.</div><br> |45999 |
   |BGP key |A parameter that appears only when the route type is **BGP**. Type your BGP Peer password.<br><br><br>* If the IPv6 interconnect IP capability is enabled, type in BGP keys for IPv4 and IPv6 separately.<br><br>* The BGP key is a sensitive credential. Store it securely to avoid compromise or disclosure. |E0g5\*\*\*\*8go1 |
   |Detection method |Set the method for line detection. Different detection methods vary in different route types. **BGP routes support BFD, and static routes support BFD and NQA**.<br><br><br>* **Disable**: Do not enable line detection.<br><br>* [BFD](https://docs.byteplus.com/en/docs/directconnect/Virtual-interface#.5LuA5LmI5pivQkZE5qOA5rWL77yf): Enable BFD as the detection method.<br><br>* [NQA](https://docs.byteplus.com/en/docs/directconnect/Virtual-interface#.5LuA5LmI5pivTlFB5qOA5rWL77yf): Enable NQA as the detection method.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When using static routing, you can enable either BFD or NQA for detection, but not both simultaneously.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The NQA feature is currently in the beta stage. If you need a trial, please contact your account manager. For details of BFD and NQA, see <a href="https://docs.byteplus.com/en/docs/directconnect/Detection_methods">Connection health detection mode</a>.</div><br> |BFD |
   |BFD mode |A parameter that appears only when the detection method is **BFD**, supporting the following two modes:<br><br><br>* BFD control packet (default): Send BFD control packets to detect bidirectional path reachability between network devices. The data center must establish a BFD session and exchange packets.<br><br>* BFD echo packet: BytePlus sends BFD echo packets, and the data center returns them to quickly detect reachability between network devices. The data center only forwards echo packets.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The BFD echo packet feature is currently in the beta stage. If you need a trial, please contact your account manager.</div><br> |BFD control packet |
   |Detect interval |Set the detection interval. This parameter appears only when using **BFD** or **NQA**. Including the sending and receiving intervals of probe packets. |1000 |
   |Detect multiplier |Set the detection count. This parameter is displayed only when using **BFD** or **NQA**. Set a number for detection attempts. If a session fails to receive the defined number of consecutive packets, the system declares a route failure. |8 |
   |**Advanced option** |||
   |Tags |A tag consists of a Tag key (Key) and a Tag value (Value), and can be used to classify and search Virtual Interfaces.<br><br><br>* Click the <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_745f4ea6f3f698cebd9adc96c9240260.png) </span> icon to add multiple tags. You can add up to 20 tags per action, and up to 50 tags for a single Virtual Interface.<br><br>* The Keys of multiple tags for the same Virtual Interface must be unique. Each Key can have only one Value.<br><br>* The Key and the Value are case\-sensitive. For example, the Key=tag and the Key=Tag are two different Keys. For more information, see [Tag management](https://docs.byteplus.com/en/docs/directconnect/Tag-management). |key:test |
   

6. Click **Create** to complete the action.


<span id=".5Y-Y6YWN5YWx5Lqr5LiT57q_"></span>
### Modify specification for a Shared Line

As your business evolves, the port bandwidth of a Shared Line may no longer meet your current business needs. You can apply to the line operator to modify the port bandwidth for the Shared Line. For the specific procedure, see [Modifying specifications](https://docs.byteplus.com/en/docs/directconnect/Modification-of-instance-specification).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You cannot initiate modification to the port bandwidth for a Shared Line by yourself. To modify, contact the line operator who supports the Shared Line.</div>


<span id=".5Yig6Zmk5YWx5Lqr5LiT57q_"></span>
### Delete a Shared Line

<span id=".5YmN5o-Q5p2h5Lu2"></span>
#### Prerequisites

Tenants can delete unused Shared Lines under their accounts. Deletion supports only Shared Lines with unpaid or expired port occupancy fee.


* If the Shared Line to be deleted is not expired, unsubscribe the Shared Line first. For procedure, see [Unsubscription](https://docs.byteplus.com/en/docs/6269/81013).

* If the Shared Line to be deleted has associated Virtual Interfaces, delete the virtual interfaces first. For procedure, see [Deleting a Direct Connect Virtual Interface](https://docs.byteplus.com/en/docs/directconnect/Deleting-the-virtual-interface).


<span id=".5pON5L2c5q2l6aqk"></span>
#### Procedure


1. Use a tenant account to log in to the BytePlus [Direct Connect Connection console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the DC Connection list on the **Direct Connect Connection** page, click **Delete** in the **Actions** column of the target Shared Line.

3. In the pop\-up dialog box, confirm the information is correct, and click **Delete** to complete the action.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After deleting a Shared Line, dependent configurations will be deleted accordingly and are unrecoverable.   </div>
   

<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [ConfirmDirectConnectConnection](https://docs.byteplus.com/en/docs/directconnect/ConfirmDirectConnectConnection): Confirm accepting the Shared Line created by the line operator.

* [CreateDirectConnectGateway](https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectGateway): Create a DC Gateway.

* [CreateDirectConnectVirtualInterface](https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectVirtualInterface): Create a Virtual Interface.

* [DeleteDirectConnectConnection](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectConnection): Delete the specified DC Connection.
