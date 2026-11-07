---
title: "Route overview"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Overview"
---

After creating an IPsec\-VPN connection, you must also configure a route on both the cloud gateway and the on\-premises gateway. This ensures bidirectional traffic flow between the cloud and on\-premises networks, enhancing rapid route convergence and network communication quality.


* Cloud gateway route: On the VPN gateway or Transit Router (TR) associated with the IPsec\-VPN connection, configure routes for the connection peer (an on\-premises data center or another VPC).

* On\-premises gateway route: To connect an on\-premises data center with a Virtual Private Cloud (VPC) via VPN Connect, configure VPN\-specific settings on the data center gateway.

   > Due to the wide variety of on\-premises firewall models and their varying configurations, this documentation covers only the VPN configuration for common models.   
   

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Route configuration is not required for SSL\-VPN connections.</div>


<span id="iec9oYtX"></span>
## Cloud gateway routes

<span id=".6Lev55Sx57G75Z6L6K-05piO"></span>
### Route types

IPsec\-VPN connections support both static and dynamic routing propagation modes. Choose the mode that best suits your scenario.


|Comparison |Static routes |Dynamic |
|---|---|---|
|Application scenarios |Applicable to scenarios where the routes of the IPsec\-VPN connection peer are limited in number and frequently remain unchanged. |Applicable to scenarios where the routes of the IPsec\-VPN connection peer are numerous and frequently modified. |
|Modification cost |Relatively high. If the routes of the IPsec\-VPN connection peer change, you must manually update route configuration in route tables of the VPN gateway/TR and the VPC. |Low. Dynamic routing uses the Border Gateway Protocol (BGP). If routes change on the peer side of the IPsec\-VPN connection, the VPN gateway/TR automatically learns these routes and publishes them to the VPC side without manual configuration. |
|Peer device requirements |No requirements |The peer gateway must support BGP |
|Recommended type |Support both Destination Routing Mode and Protected Data Flows. Choose one based on your specific scenario. |Destination Routing Mode is recommended. If **the routing mode** for the IPsec\-VPN connection is **Protected Data Flows** and Dynamic routing is selected, only dynamic routes within the Protected Data Flows CIDR block take effect. Routes outside this block are ignored. |
|Route selection priority |* Static routes take precedence over dynamic routes.<br><br>* Longest prefix match (LPM) principle: When traffic matches a route table, and the destination IP address falls within destination CIDR blocks of multiple routes, the system will select an entry with the longest mask (i.e., the highest priority) based on the LPM principle.<br><br>* Shortest AS_PATH match principle: For dynamic routes with the same destination, the shorter the AS_PATH length, the higher the priority of the route. ||


<span id=".6Lev55Sx5LyY5YWI57qn6K-05piO"></span>
### Route recommendations and limits


<Tabs>
<Tab zoneid="HPSlpv0Guo" title="IPsec-VPN connection via VPN gateway">
<TabTitle>IPsec-VPN connection via VPN gateway</TabTitle>

<span id="MZaqvd9I"></span>
### Recommendations


* In dynamic routing mode, we recommend using **Destination Routing Mode**. If **the routing mode** for the IPsec\-VPN connection is **Protected Data Flows** and Dynamic routing is selected, only dynamic routes within the Protected Data Flows CIDR block take effect. Routes outside this block are ignored.

* In the scenario where multiple IPsec\-VPN connections are created on the same VPN gateway, we recommend using the same propagation mode for all connections under this VPN gateway. That is, use either all static or all dynamic routing for all IPsec\-VPN connections.

* Avoid propagating the following types of routes, as they will consume the route quota of the VPN gateway and may be rejected by VPC.

   * Dynamic routes with a destination CIDR of 0.0.0.0/n, including 0.0.0.0/0.

   * Dynamic routes that have the same CIDR block as the subnet range of the VPN gateway's host VPC.


<span id="nemR7xik"></span>
### Limits


* Avoid propagating loop routes with AS_PATH containing the VPN gateway's ASN.

* The VPN gateway supports only dynamic equal\-cost multi\-path routing (ECMP) routes, but not static ECMP routes.

* A single TR instance or VPN gateway supports ECMP routing across up to 16 IPsec\-VPN connections.

* The VPN gateway can receive routes with an AS_PATH length up to 29 and send routes with an AS_PATH length up to 30.

* The VPN gateway's route table supports a ​​maximum of 200 routes​​ by default. Routes ​​exceeding this limit​​ will be discarded. If the default quota cannot satisfy your needs, go to the Quota center to increase the corresponding quota. For procedure, see [Quota management](https://docs.byteplus.com/en/docs/vpn/Quota-management).

* Sending a massive number of dynamic routes may cause the BGP session to drop. If the number of dynamic routes sent over an IPsec\-VPN connection exceeds 1,000 (via a VPN Gateway) or 5,000 (via a TR), the BGP session will terminate abruptly. It will not recover even after the excess routes are withdrawn. To send a massive number of dynamic routes, [submit a ticket](https://console.byteplus.com/workorder/create?step=3&SubProductID=P00000249&FlowKey=NGhBLLYotsiBMSgHMvCt).


</Tab>
<Tab zoneid="XEmKk5lXdS" title="IPsec-VPN connection via TR">
<TabTitle>IPsec-VPN connection via TR</TabTitle>

<span id="Jr14BmFl"></span>
### Recommendations


* In scenarios with a small number of instance routes, we recommend [configuring static routes](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05). You need to manually configure routes on the TR.

* In scenarios with a large number of instance routes, we recommend configuring [auto-learned routes.](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-06) The TR route table will automatically generate entries with the next hop of the network instance.

* Route match sequence: Static route \> Auto\-learned route. Among auto\-learned routes, prefer routes with the shortest AS_PATH length. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-01#.6Lev55Sx5LyY5YWI57qn)

* Avoid propagating the following routes that may be rejected by the TR:

   * A route whose destination CIDR block is exactly the same as that of an existing entry in the route table.

   * A route whose destination CIDR block is a multicast CIDR block (`224.0.0.0 to 239.255.255.255` or `FF00::/8`).

   * A route whose AS_PATH contains the ASN of this TR.

   * A route whose AS_PATH length exceeds 30.


<span id="cHeSmdIb"></span>
### Limits


* Each network instance attachment can be configured with only one associated forwarding route table.

* To configure association forwarding or route learning when creating a cross\-account attachment, you can select only the system route table. The TR route table can be modified by the Sharer solely.

* You can add a maximum of 2,000 routes to a single TR route table, and can create up to 20 tables (including the system route table) for a single TR instance. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Product-Overview-04#.6YWN6aKd6ZmQ5Yi2)


</Tab>
</Tabs>


<span id=".6Lev55Sx5LyY5YWI57qn6K-05piO"></span>
### Route propagation and configuration requirements


<Tabs>
<Tab zoneid="qBR0KK8pgs" title="IPsec-VPN connection via VPN gateway">
<TabTitle>IPsec-VPN connection via VPN gateway</TabTitle>


|Routing mode |Traffic direction |VPC |Local VPN gateway |Peer data center/VPC |
|---|---|---|---|---|
|Static routes |From cloud |* Single\-tunnel VPN gateway<br><br>   After a route is configured to the VPN gateway, the system automatically publishes this route as a custom route in **the system route table** of the gateway's host VPC. This directs traffic originating from the VPC towards the VPN gateway.<br><br>   * You do not need to configure routes for the system route table manually.<br><br>   * If the VPN gateway's host VPC has a custom route table in addition to the system route table, and the subnet associated with the custom route table needs to access the peer via VPN Connect, you must manually add the route to **the custom route table** in the VPC. For the new route, its destination CIDR block is the peer data center or the VPC CIDR block and its next hop type is **VPN gateway**. For procedure, see [Add a route entry](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry).<br><br>* Dual\-tunnel VPN gateway<br><br>   After a route is configured to the VPN gateway, the system automatically publishes this route as a system route in **all route tables (system and custom route tables)**  of the gateway's host VPC. This directs traffic originating from the VPC towards the VPN gateway. You do not need to configure routes for the VPC manually.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The dual\-tunnel mode is in the beta stage. If you need a trial, please contact your account manager.   </div><br>    |You need to add routes pointing to the peer data center or VPC into the VPN gateway. For procedure, see [Adding a VPN gateway route](https://docs.byteplus.com/en/docs/vpn/Adding-a-VPN-gateway-route).<br><br><br>* If the destination CIDR block of a VPN gateway route overlaps with that of a route in the VPC's system route table, the traffic will be forwarded based on the route with the longest mask.<br><br>* Neither the VPN gateway route nor the corresponding route entry in the VPC route table can be modified.<br><br>* When a route is deleted from the VPN gateway, ​​all corresponding system\-added routes​​ (with this VPN gateway as the next hop) ​​in the VPC route tables are automatically deleted​​. ​​Manually added routes remain unaffected​​.<br><br>* When the VPN gateway is deleted, ​​all corresponding system\-added routes​​ (with this VPN gateway as the next hop) ​​in the VPC route tables are automatically deleted​​. ​​Manually added routes remain unaffected​​. |No configuration required |
||To cloud |No configuration required |No configuration required |Configure an on\-premises gateway route on the peer data center or VPC side. For procedure, see [On-premises gateway routes](https://docs.byteplus.com/en/docs/vpn/Overview-1). |
|Dynamic |From cloud |No configuration required |No configuration required<br><br><br>* After the BGP session is established, the VPN gateway learns the BGP routes announced by the peer gateway, and publishes them as system routes into all route tables (system and custom route tables) of the gateway's host VPC.<br><br>* After the BGP session is established, the VPN gateway learns the routes from its VPC's system route table that point to the VPC's subnets and publishes them to the peer gateway. The VPN gateway does not learn CEN\-published routes or custom routes in the VPC route tables. |No configuration required<br><br><br>* After the BGP session is established, the peer gateway can automatically propagate its on\-premises routes to the VPN gateway.<br><br>* After the BGP session is established, the peer gateway can automatically learn VPC's routes from the VPN gateway. |
||To cloud |No configuration required |||





</Tab>
<Tab zoneid="LPKsCBQWkX" title="IPsec-VPN connection via TR">
<TabTitle>IPsec-VPN connection via TR</TabTitle>


|Routing mode |Traffic direction |VPC |Local TR |Peer data center/VPC |
|---|---|---|---|---|
|Static routes |From cloud |After creating a TR, connect it to a VPC instance and configure routes. The traffic within the VPC will be forwarded based on the routes in the TR's route table​​. |Add routes pointing to the peer data center or VPC into the TR. For procedure, see [Managing a static route](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05). |No configuration required |
||To cloud |No configuration required |No configuration required |Configure an on\-premises gateway route on the peer data center or VPC side. For procedure, see [On-premises gateway routes](https://docs.byteplus.com/en/docs/vpn/Overview-1). |
|Dynamic |From cloud |No configuration required |No configuration required<br><br>Specify the routing propagation mode as **dynamic routing** when creating an IPsec\-VPN connection. After the BGP session is established, the TR learns the BGP routes announced by the peer gateway. It then publishes these routes as system routes into all route tables (system and custom route tables) of the TR.<br><br><br>* To use dynamic routing, ensure different Autonomous System Numbers (ASNs) are assigned to the same IPsec\-VPN connection's TR and the selected customer gateway.<br><br>   * For IPsec\-VPN connections using dynamic routing, we recommend avoiding the use of 65535 and 4294967295 as any ASN. If the AS_PATH contains 65535 or 4294967295, the related route will be discarded. |No configuration required<br><br><br>* After the BGP session is established, the peer gateway can automatically propagate its on\-premises routes to the TR.<br><br>* After the BGP session is established, the peer gateway can automatically learn routes from the TR. |
||To cloud |No configuration required |||





</Tab>
</Tabs>


<span id=".6Lev55Sx5LyY5YWI57qn6K-05piO"></span>
### Route configuration guide


<Tabs>
<Tab zoneid="vUM6qQjB7N" title="IPsec-VPN connection via VPN gateway">
<TabTitle>IPsec-VPN connection via VPN gateway</TabTitle>

* [Adding a VPN gateway route](https://docs.byteplus.com/en/docs/vpn/Adding-a-VPN-gateway-route).

* [Deleting a VPN gateway route](https://docs.byteplus.com/en/docs/vpn/Deleting-a-VPN-gateway-route).


</Tab>
<Tab zoneid="SUvdP8VTYD" title="IPsec-VPN connection via TR">
<TabTitle>IPsec-VPN connection via TR</TabTitle>

TR route table consists of a series of route entries and supports associated forwarding, route learning, and static routing. This allows quick addition of routes and flexible control of traffic direction in and out of the TR. For more information, see [TR Route Table overview](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-01).


|Routing capability |Principle description |Configuration procedure |
|---|---|---|
|Custom route table |A route table manually created by the user. You can use multiple TR route tables to define different interconnectivity scopes for network instances. |[Create a route table](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-03) |
|Static routes |Used to manually configure routes on the TR instance side. Applicable to scenarios with a small number of routes. |[Create a static route](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05#.5Yib5bu66Z2Z5oCB6Lev55Sx) |
|Route propagation |Used to configure TR\-side routes by route learning. Applicable to scenarios with a large number of network instance routes.<br><br>After configuring route learning, the TR route table automatically generates routes with the next hop set to the attachment. |[Create a route learning rule](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-06#.5Yib5bu66Lev55Sx5a2m5Lmg) |
|Auto Publish Route |Used to configure routes on the network instance side by auto publishing.<br><br>After enabling auto\-publishing, the system automatically publishes routes from the TR associated forwarding route table of the target instance into the route table of that network instance. |[Enable auto publishing](https://docs.byteplus.com/en/docs/transitrouter/Attachments-04) |
|Route policy |Used to filter routes received and sent by the TR, which can change route propagation behavior and selection results.<br><br> |1. [Create a route policy](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-routing-policy)<br><br>2. [Configure route policy for a TR route table](https://docs.byteplus.com/en/docs/transitrouter/Binding-Unbinding-Modifying-routing-policy-for-TR-route-table) |
|Forwarding policy |Used to specify the TR route table for the TR instance to forward traffic of a CIDR block in the network instance. |1. [Create a forwarding policy](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-forwarding-policy)<br><br>2. [Configure forwarding policy for a network instance attachment](https://docs.byteplus.com/en/docs/transitrouter/Enabling-Disabling-Modifying-forwarding-policy) |





</Tab>
</Tabs>


<span id=".6Lev55Sx5LyY5YWI57qn6K-05piO"></span>
## On\-premises gateway route

<span id="OprMSgpy"></span>
### Prerequisites


* The gateway device in your on\-premises data center supports the IKE V1 or IKE V2 protocol.

* The gateway device in your data center has a static Elastic IP Address (EIP).

* The CIDR blocks of your data center must not overlap with those of the VPC where the VPN gateway to be communicated with is located.


<span id="cO2H6cV1"></span>
### Configuration examples

For your convenience, we introduce two configuration methods. You can select the one that best suits your scenario.


<Tabs>
<Tab zoneid="au7kgFcmmu" title="Manual configuration">
<TabTitle>Manual configuration</TabTitle>

* [Configuring the Sangfor firewall](https://docs.byteplus.com/en/docs/vpn/Configuring_a_Sangfor_firewall)

* [Configuring the Cisco firewall](https://docs.byteplus.com/en/docs/vpn/Configuring-a-Cisco-firewall)

* [Configuring the H3C firewall](https://docs.byteplus.com/en/docs/vpn/Configuring-an-H3C-firewall)

* [Configuring the Hillstone firewall](https://docs.byteplus.com/en/docs/vpn/Configuring_a_Hillstone_firewall)


</Tab>
<Tab zoneid="MofEtufHFu" title="File configuration">
<TabTitle>File configuration</TabTitle>

* [Cisco firewall configuration file](https://docs.byteplus.com/en/docs/vpn/Cisco-firewall-configuration-file)

* [H3C firewall configuration file](https://docs.byteplus.com/en/docs/vpn/H3C-firewall-configuration-file)


</Tab>
</Tabs>
