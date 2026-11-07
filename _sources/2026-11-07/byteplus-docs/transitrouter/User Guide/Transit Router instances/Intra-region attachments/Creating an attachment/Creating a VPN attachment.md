---
title: "Creating a VPN attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpn"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

Establish a connection between a Virtual Private Network (VPN) and a Transit Router (TR), enabling intercommunication between the VPN\-connected and TR's networks.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Ensure you have created a TR instance. For procedure, see [Creating a Transit Router instance](https://docs.byteplus.com/docs/transitrouter/TransitRouter-instances-01).

* Before creating a cross\-account intra\-region attachment, ensure you have [accepted a sharing invitation](https://docs.byteplus.com/docs/transitrouter/Cross-account-Transit-Router-sharing#kFuWwFWD). The target TR instance is not suspended due to overdue payment.


<span id=".5pON5L2c6K-05piO"></span>
## Instructions

By default, a single TR instance supports a maximum of 10 VPN attachments. If this quota is insufficient, you can request an increase through the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=Auto_Scaling), up to an absolute upper limit of 50 attachments.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the section below **Basic information**, select the **Intra\-region attachment** tab.

4. Click **Create attachment**, and complete the basic configuration based on the table below.

   
   |Parameters ||Description |Example |
   |---|---|---|---|
   |**Basic information** ||||
   |TR ||Defaults to the selected TR instance. No manual configuration is required. |tr01 |
   |Region ||Defaults to the same region as the TR instance. No manual configuration is required. |China (Beijing) |
   |Fee payer ||Defaults to the same fee payer as the TR instance. No manual configuration required. This parameter is displayed only when the TR instance is shared. |Network instance account |
   |Name ||The name of the network instance attachment to be created. |attach\-vpn01 |
   |**Attachment** ||||
   |Attachment type ||Select the type of network instance. This example only demonstrates configuration parameters for VPN attachments. |VPN |
   |VPN ||Select the IPsec\-VPN connection to be attached based on the project.<br><br><br>* **Use existing**: The ASN of the customer gateway associated with the IPsec\-VPN connection must differ from the ASN of the TR instance.<br><br>* Select **Create a VPN connection**: Configure the parameters for the new IPsec\-VPN connection, see [Creating a VPN Connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1). |Use existing; ipsec01<br><br> |
   |Configure the new IPsec\-VPN connection |**Basic information** |||
   ||Region |Defaults to the same region as the TR instance. No manual configuration is required. |China (Beijing) |
   ||Name |The name of the IPsec\-VPN connection to be created. |ipsec01 |
   ||Affiliated project |The project to which the IPsec\-VPN connection belongs. After a project is selected, newly created IPsec\-VPN connections can only be used by users with permissions for that project. |default |
   ||**Connection information** |||
   ||Specification |Select the specification for the IPsec\-VPN connection, with options of **Default**, **Large**, and **Super large**. Different specifications incur different IPsec instance fees.<br><br><br>* **Default** IPsec\-VPN connection has a bandwidth cap of 200 Mbps.<br><br>* **Large** IPsec\-VPN connection has a bandwidth cap of 1 Gbps.<br><br>* **Super large** IPsec\-VPN connection has a bandwidth cap of 3 Gbps.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The IPsec\-VPN connections in <strong>large</strong> and <strong>super large</strong> specifications are in the beta stage. To request a trial, please contact your account manager.   </div><br>    |default |
   ||Routing |Select a routing mode.<br><br><br>* Destination Routing Mode: Routing and forwarding are based on destination IP, without filling in the Local Subnet and Remote Subnet for negotiation.<br><br>* Protected Data Flows: Routing and forwarding are based on destination IP, requiring filling in the Local Subnet and Remote Subnet for negotiation. |Destination routing |
   ||Local Subnet |This parameter appears only in the **Protected Data Flows** mode. It is only for IPsec negotiation.<br><br>Type a subnet CIDR block of the local VPC that uses the VPN Connect for communication. |192.168.1.0/24 |
   ||Remote Subnet |This parameter appears only in the **Protected Data Flows** mode. It is only for IPsec negotiation.<br><br>Type the CIDR block of the peer data center or VPC that uses the VPN Connect for communication. |192.168.2.0/24 |
   ||Negotiate instantly |Specify whether the IPsec\-VPN connection takes effect immediately after configuration.<br><br><br>* Yes: The system proactively initiates the negotiation instantly upon the completion of IPsec\-VPN connection configuration.<br><br>* No: The system does not initiate negotiation after the IPsec\-VPN connection configuration is completed. Negotiation is triggered passively when traffic passes through. |Yes |
   ||Route propagation mode |Select the routing propagation mode for the IPsec\-VPN connection, supporting static and dynamic routing.<br><br><br>* **Static routing**: In static routing propagation mode, you need to manually configure the VPN gateway route after the IPsec\-VPN connection is created. For procedures, see [Adding a VPN gateway route](https://docs.byteplus.com/en/docs/vpn/Adding-a-VPN-gateway-route).<br><br>* **Dynamic routing**: In the dynamic routing propagation mode, routes are automatically published and forwarded. Manual configuration is not required.<br><br>   * In dynamic routing mode, we recommend using Destination Routing Mode. If the routing mode is Protected Data Flows and Dynamic routing is selected, only dynamic routes within the Protected Data Flows CIDR block take effect. Routes outside this block are ignored.<br><br>   * **To use dynamic routing, ensure different Autonomous System Numbers (ASNs) are assigned to the same IPsec\-VPN connection's associated resource (a VPN gateway or TR) and the selected customer gateway.** <br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For IPsec\-VPN connections using dynamic routing, we recommend avoiding the use of 65535 and 4294967295 as any ASN. If the AS_PATH contains 65535 or 4294967295, the related route will be discarded.   </div><br>    |Static route |
   ||Customer Gateway |Select your target customer gateway.<br><br><br>* To use dynamic routing propagation, ensure that the BGP ASN has been configured for the customer gateway. If not, refer to [Creating a Customer Gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-customer-gateway1) to recreate it. |cgw01 |
   ||Pre\-shared key |Type the key for IKE negotiation between VPN devices on both sides. Ensure the configuration on both sides of the VPN Connect is identical.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Identical Pre\-Shared Keys must be configured for both local and peer ends of the IPsec\-VPN connection. Otherwise, the connection cannot be initiated. The example value is for reference only. The key has no special meaning.</div><br> |We!08sr@D\*\*\*\* |
   ||Confirm key |Type the Pre\-Shared Key again. |We!08sr@D\*\*\*\* |
   ||Agreement |Follow the console guidance to review and accept the legal terms. |Check |
   |Availability Zone<br><br> ||Specify the availability zone for the IPsec\-VPN connection. We recommend choosing the same availability zone as the VPC to be connected via TR for lower latency |Availability Zone A |
   

5. Complete the route configuration and advanced options based on the table below.

   
   |Parameters |Description |Example |
   |---|---|---|
   |**Route configuration** |||
   |Association forwarding |Specify whether to enable association forwarding for this attachment.<br><br><br>* Enable: Select the TR route table. This means traffic from the specified IPsec\-VPN connection will be forwarded according to routes in this TR route table.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When a Recipient creates a cross\-account attachment and enables association forwarding, the only option is the target TR instance’s system route table by default. To modify this, contact the Owner.   </div><br>   <br><br>* Disable: After the attachment creation is completed, you also need to specify the TR route table that forwards traffic for this attachment by seeing [Create an association forwarding rule](https://docs.byteplus.com/docs/transitrouter/Route-tables-07). Otherwise, the TR will be unable to forward traffic from the attachment. |Enable |
   |Route learning |Specify whether to enable route learning for this attachment.<br><br><br>* Enable: Select the TR route table. The route table will automatically learn data center's routes by the BGP capabilities of the IPsec\-VPN connection.<br><br>   * IPsec\-VPN connections with **BGP** routing: The TR route table automatically generates routes. Destination CIDR blocks match the data center's, with the next hop set as this VPN attachment.<br><br>      * IPsec\-VPN connection with **Static** routing: The route learning is disabled. You need to manually add routes with the next hop set as this VPN attachment by seeing [Create a static route](https://docs.byteplus.com/docs/transitrouter/Route-tables-05).<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When a Recipient creates a cross\-account attachment and enables route learning, the only option is the target TR instance’s system route table by default. To modify this, contact the Owner.   </div><br>   <br><br>* Disable: The TR route table will not automatically learn data center's routes through the IPsec\-VPN connection. After the attachment creation is completed, add a route whose next hop is this VPN attachment by seeing [Create a route learning rule](https://docs.byteplus.com/docs/transitrouter/Route-tables-06) or [Create a static route](https://docs.byteplus.com/docs/transitrouter/Route-tables-05). |Enable |
   |**Advanced options** |||
   |Tag |A tag consists of a key\-value pair and is used for categorizing and searching resources. [Learn more](https://docs.byteplus.com/docs/transitrouter/Tags)<br><br>Click **Add tag**, and type the tag key and tag value to tag the attachment. |* Tag key: attach\-k1<br><br>* Tag value: attach\-v1 |
   

6. Click **Buy now** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[CreateTransitRouterVpnAttachment](https://docs.byteplus.com/docs/transitrouter/CreateTransitRouterVpnAttachment): Create a VPN attachment.
