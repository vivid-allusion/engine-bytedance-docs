---
title: "Creating a VPN gateway"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Creating-a-VPN-gateway-2"
---

When you need to achieve communication between a Virtual Private Cloud (VPC) and an on\-premises data center or another VPC via VPN Connect, you must create a VPN gateway first.

<span id="0EqNKYp0"></span>
## Instructions


* Multiple VPN gateways within the same VPC cannot be interconnected via IPsec\-VPN connection.

* For disaster recovery scenarios, it is recommended to use a dual\-tunnel mode VPN connection. A dual\-tunnel mode VPN connection includes both a primary and a secondary tunnel, and these two tunnels are distributed across different Availability Zones. If the primary tunnel fails, traffic can be transmitted through the secondary tunnel.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The dual\-tunnel mode is in the beta stage. If you need a trial, please contact your account manager.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Dual\-tunnel VPN gateways do not support configuring the SSL feature.   </div>
   


<span id="FJ7ErjAx"></span>
## Prerequisites


* Creating a VPN gateway will occupy IP addresses of the subnet where the VPN gateway is located. Reserve sufficient IP addresses.

   * A VPN gateway in single\-tunnel mode occupies three IP addresses within the subnet.

   * A VPN gateway in dual\-tunnel mode occupies one IP address each within both the primary subnet and the secondary subnet.

* Deploy the primary and secondary tunnels of a dual\-tunnel VPN gateway in different availability zones. Ensure the target VPC contains subnets with two or more availability zones.

* A Subscription VPN gateway will be suspended at 12:00:00 UTC on the day after it expires. If renewal is not completed within the 15\-day grace period, the VPN gateway will be released. Release is an irreversible action. A released VPN gateway cannot be restored, with all associated data being unrecoverable.


<span id="Fqxu8WxI"></span>
## Procedure


1. Log in to the [VPN gateway console](https://console.byteplus.com/vpn/vpnGateway). 

2. In the top menu bar, select the target region and project to which the resource belongs.

3. Click **Create VPN Gateway** and configure the VPN gateway parameters based on the table below.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The features supported by a VPN gateway depend on its version. The table below lists the parameters available for the latest version. To access the latest functionality, upgrade your VPN gateway. For procedure, see <a href="https://docs.byteplus.com/en/docs/vpn/Upgrading-a-VPN-gateway">Upgrading a VPN gateway</a>.   </div>
   

   
   <Tabs>
   <Tab zoneid="hwlETzCRue" title="Single-tunnel VPN gateway">
   <TabTitle>Single-tunnel VPN gateway</TabTitle>
   
   
   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Billing method |The billing method for the VPN gateway. Supports **Subscription** and **Pay\-as\-you\-go**. |Subscription |
   |Regions |By default, select the region in the top menu bar before entering the Create VPN Gateway page. Private networks in different regions are isolated. We recommend selecting a region closest to your business for lower network delays and faster access. |China (Beijing) |
   |Name |Name of the VPN gateway. |VPNGW\-a3cs |
   |Tunnel mode |The tunnel mode of the VPN gateway.<br><br><br>* **Single tunnel**: Only one encrypted tunnel. Tunnel failure may cause network interruption.<br><br>* **Dual tunnels**: Two encrypted tunnels in primary\-secondary mode. If the primary tunnel fails, traffic can be switched to the secondary tunnel for normal transmission. Deploy two encrypted tunnels in different availability zones, enabling disaster recovery at the availability zone level. |Single tunnel |
   |IP address type |The IP address type for the connection between the VPN gateway and the client. A single\-tunnel mode VPN gateway only supports the IPv4 address type. |IPv4 |
   |Protocol type |The protocol type used within the VPN gateway tunnels. All tunnels associated with the VPN gateway will use the same protocol type. A single\-tunnel mode VPN gateway only supports the IPv4 address type. |IPv4 |
   |**Network Configuration** |||
   |Bandwidth |Set the bandwidth cap of the VPN gateway. This limit restricts the bandwidth cap for both outbound and inbound directions of VPC. For more bandwidth limits, see [VPN gateway bandwidth limits](https://docs.byteplus.com/en/docs/vpn/Limits#.VlBO572R5YWz5bim5a696ZmQ5Yi2).<br><br><br>* This value is the bandwidth shared for all IPsec\-VPN connections and SSL\-VPN connections created on this VPN gateway. That is, the total bandwidth of IPsec\-VPN and SSL\-VPN connections cannot exceed the bandwidth of the VPN gateway.<br><br>* After the VPN gateway is created, you can adjust Bandwidth of the VPN gateway as needed. For more information, see [Modifying VPN gateway configurations](https://docs.byteplus.com/en/docs/vpn/Modifying-VPN-gateway-configurations).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The bandwidth limit applies to encapsulated encrypted packets. To configure alarm strategies in Cloud Monitor to monitor VPN gateway metrics, select monitoring metrics including packet encapsulation overhead for trigger conditions, such as VPN gateway outbound/inbound bandwidth usage.</div><br> |20Mbps |
   |VPC |Select the VPC where the VPN gateway resides. Only VPCs within the current project are selectable. |VPC1 \| 10.1.0.0/16 |
   |Subnet |Select the subnet where the VPN gateway resides. The VPN gateway occupies three IPv4 addresses in the subnet. Reserve sufficient IPv4 addresses. |subnet \| 10.1.0.0/24 \| China (Beijing) A |
   |BGP ASN |Set the Autonomous System Number (ASN) for the VPN gateway. If the IPsec\-VPN connection uses dynamic routing propagation mode, configure a BGP ASN for the VPN gateway. If static routing is used, BGP ASN is not required.<br><br><br>* Once configured, the BGP ASN of the VPN gateway cannot be modified.<br><br>* Valid ranges of BGP ASN: 64512 to 65534 and 4200000000 to 4294967294.<br><br>* If this VPN gateway is later used to create an IPsec\-VPN connection with dynamic routing, ensure that different ASNs are assigned to the VPN gateway and the customer gateway attached to the same IPsec\-VPN connection. |65024 |
   |**Function configuration** |||
   |IPsec\-VPN connection |Enable IPsec\-VPN connectivity: When enabled, the IPsec\-VPN functionality becomes available. For single\-tunnel mode gateways, the SSL\-VPN connectivity can be enabled simultaneously.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The billing items vary depending on the enabled connection capability. For more information, see <a href="https://docs.byteplus.com/en/docs/vpn/Billing-overview">Billing</a>.</div><br> |Check |
   |SSL connection |Enable SSL\-VPN connectivity as needed. After enabling, you can use the SSL\-VPN feature and can enable IPsec\-VPN connectivity concurrently. |Check |
   |SSL Max Connections |This parameter appears only if you enable SSL\-VPN connectivity. Select the maximum number of clients that can be connected concurrently for the SSL\-VPN connection. |10 |
   |**Billing cycle** |||
   |Duration |The ​​validity period​​ for which the VPN gateway is subscribed. |1 month |
   |Automatic renewal |Enable automatic renewal as needed. If automatic renewal is enabled, the renewal length is one month and the number of renewals is unlimited. You can manually disable automatic renewal or visit the **Billing center** to modify the number of renewals. For detailed actions, see [Automatic renewal](https://docs.byteplus.com/en/docs/byteplus-platform/docs-auto-renewal-rules). For VPN gateways that you rely on for the long term, we recommend checking Automatic renewal to prevent any disruption when they expire. |Disabled |
   |Affiliated Project |Select the project to which the new VPN gateway belongs. A project refers to a task in your daily work. You can create multiple projects under the same account and create or purchase cloud resources for each project. Cloud resources cannot be shared between different projects.<br><br><br>* After the project is selected, the created VPN gateway can only be used by users with permissions for that project.<br><br>* If you have selected **All Resources** in the top menu bar, the created VPN gateway belongs to the default project by default. You can modify the project as needed.<br><br>* If you have selected a specific project in the top menu bar, the new VPN gateway belongs to that project. You can modify the project in the top menu bar.<br><br>* If no projects are available, click **Create project** on the right to create a new project.<br><br>* After a VPN gateway is added to a project, you can transfer the VPN gateway out of the project based on your business needs. For details, see [Project resource management](https://docs.byteplus.com/en/docs/6649/94337).<br><br>* VPN gateway routes are sub\-resources of the VPN gateway. They can only be transferred along with the VPN gateway and cannot be transferred separately between projects. |default |
   |**Advanced option** |||
   |Tags |A tag consists of a tag key (Key) and a tag value (Value). It can be used to classify and search for customer gateways. [Prerequisite](https://docs.byteplus.com/en/docs/vpn/Tag-management)<br><br><br>* Click **Add tag** to add multiple tags as needed. You can add up to 20 tags per action, and add up to 50 tags for a single VPN gateway.<br><br>* The Keys of multiple tags for the same VPN gateway must be unique. Each Key has only one Value.<br><br>* The Key and the Value are case\-sensitive. For example, the Key=tag and the Key=Tag are two different Keys. |key:test |
   
   
   
   
   
   </Tab>
   <Tab zoneid="lt7oZHsKRR" title="Dual-tunnel VPN gateway">
   <TabTitle>Dual-tunnel VPN gateway</TabTitle>
   
   
   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Billing method |The billing method for the VPN gateway. Supports **Subscription** and **Pay\-as\-you\-go**. |Subscription |
   |Region |By default, select the region in the top menu bar before entering the Create VPN Gateway page. Private networks in different regions are isolated. We recommend selecting a region closest to your business for lower network delays and faster access. |China (Beijing) |
   |Name |Name of the VPN gateway. |VPNGW\-a3cs |
   |Tunnel mode |The tunnel mode of the VPN gateway.<br><br><br>* **Single tunnel**: Only one encrypted tunnel. Tunnel failure may cause network interruption.<br><br>* **Dual tunnels**: Two encrypted tunnels in primary\-secondary mode. If the primary tunnel fails, traffic can be switched to the secondary tunnel for normal transmission. Deploy two encrypted tunnels in different availability zones, enabling disaster recovery at the availability zone level.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When creating a dual\-tunnel VPN gateway for the first time, please complete cross\-service authorization according to the guidance.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When creating a dual\-tunnel VPN gateway in a region that only supports single\-availability zone deployment for VPN Connect, you must configure both tunnels within the same zone.   </div><br>    |Dual tunnel |
   |IP address type |Select the IP address type for the connection between the VPN gateway and clients. Both IPv4 and IPv6 address types are supported, with IPv4 set as the default. The IP address type of a VPN gateway cannot be modified after creation. Please choose carefully.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The IPv6 protocol type is currently in beta stage. If you need a trial, please contact your account manager.</div><br> |IPv4 |
   |Protocol type |Select the protocol type used within the VPN gateway tunnels. All tunnels associated with the VPN gateway will use the same protocol type. The protocol type of a VPN gateway cannot be modified after creation. Please choose carefully.<br><br><br>* Supports 3 protocol types: IPv4, IPv6, and dual\-stack. When selecting, the IP address type must match the **that** of the VPN gateway.<br><br>* The dual\-stack protocol type is compatible with all IP address types. |IPv4 |
   |**Network Configuration** |||
   |Bandwidth |Set the bandwidth cap of the VPN gateway. This limit restricts the bandwidth cap for both outbound and inbound directions of VPC. For more bandwidth limits, see [VPN gateway bandwidth limits](https://docs.byteplus.com/en/docs/vpn/Limits#.VlBO572R5YWz5bim5a696ZmQ5Yi2).<br><br><br>* This value is the bandwidth shared for all IPsec\-VPN connections and SSL\-VPN connections created on this VPN gateway. That is, the total bandwidth of IPsec\-VPN and SSL\-VPN connections cannot exceed the bandwidth of the VPN gateway.<br><br>* After the VPN gateway is created, you can adjust Bandwidth of the VPN gateway as needed. For more information, see [Modifying VPN gateway configurations](https://docs.byteplus.com/en/docs/vpn/Modifying-VPN-gateway-configurations).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The bandwidth limit applies to encapsulated encrypted packets. To configure alarm strategies in Cloud Monitor to monitor VPN gateway metrics, select monitoring metrics including packet encapsulation overhead for trigger conditions, such as VPN gateway outbound/inbound bandwidth usage.</div><br> |20Mbps |
   |VPC |Select the VPC where the VPN gateway resides. Only VPCs within the current project are selectable. |VPC1 \| 10.1.0.0/16 |
   |Primary subnet |Select the primary subnet where the VPN gateway is located. The VPN gateway occupies one IP address within this subnet. Reserve sufficient IP addresses.<br><br><br>* The subnet must contain a CIDR block that matches the VPN gateway's protocol type. For example, a VPN gateway with an IPv4 protocol type can select a subnet containing an IPv4 CIDR block or a dual\-stack subnet.<br><br>* If the VPN gateway protocol type is dual\-stack, only subnets of the dual\-stack protocol type are supported.<br><br>* The VPN gateway occupies one IP address within this subnet. Reserve sufficient IP addresses. |subnet01 \| 10.1.0.0/24 \| Availability Zone  A |
   |Secondary subnet |Select the subnet where the VPN gateway resides. To enable availability zone disaster recovery, select a subnet in an availability zone ​​other than that of​​ the primary subnet as the secondary subnet.<br><br><br>* The subnet must contain a CIDR block that matches the VPN gateway's protocol type. For example, a VPN gateway with an IPv4 protocol type can select a subnet containing an IPv4 CIDR block or a dual\-stack subnet.<br><br>* If the VPN gateway protocol type is dual\-stack, only subnets of the dual\-stack protocol type are supported.<br><br>* The VPN gateway occupies one IP address within this subnet. Reserve sufficient IP addresses. |subnet02 \| 10.1.1.0/24 \| Availability Zone B |
   |BGP ASN |Set the Autonomous System Number (ASN) for the VPN gateway. If the IPsec\-VPN connection uses dynamic routing propagation mode, configure a BGP ASN for the VPN gateway. If static routing is used, BGP ASN is not required.<br><br><br>* Once configured, the BGP ASN of the VPN gateway cannot be modified.<br><br>* Valid ranges of BGP ASN: 64512 to 65534 and 4200000000 to 4294967294.<br><br>* If you later use this VPN gateway to create an IPsec\-VPN connection with dynamic routing: Assign different ASNs to the VPN gateway and the customer gateway for that connection. |65024 |
   |**Function configuration** |||
   |IPsec\-VPN connection |Enable IPsec\-VPN connectivity: When enabled, the IPsec\-VPN functionality becomes available. This is enabled by default for dual\-tunnel mode. |Check |
   |**Billing cycle** |||
   |Duration |The ​​validity period​​ for which the VPN gateway is subscribed. |1 month |
   |Automatic renewal |Enable automatic renewal as needed. If automatic renewal is enabled, the renewal length is one month and the number of renewals is unlimited. You can manually disable automatic renewal or visit the **Billing center** to modify the number of renewals. For detailed actions, see [Automatic renewal](https://docs.byteplus.com/en/docs/byteplus-platform/docs-auto-renewal-rules). For VPN gateways that you rely on for the long term, we recommend checking Automatic renewal to prevent any disruption when they expire. |Disabled |
   |Affiliated Project |Select the project to which the new VPN gateway belongs. A project refers to a task in your daily work. You can create multiple projects under the same account and create or purchase cloud resources for each project. Cloud resources cannot be shared between different projects.<br><br><br>* After the project is selected, the created VPN gateway can only be used by users with permissions for that project.<br><br>* If you have selected **All Resources** in the top menu bar, the created VPN gateway belongs to the default project by default. You can modify the project as needed.<br><br>* If you have selected a specific project in the top menu bar, the new VPN gateway belongs to that project. You can modify the project in the top menu bar.<br><br>* If no projects are available, click **Create project** on the right to create a new project.<br><br>* After a VPN gateway is added to a project, you can transfer the VPN gateway out of the project based on your business needs. For details, see [Project resource management](https://docs.byteplus.com/en/docs/6649/94337).<br><br>* VPN gateway routes are sub\-resources of the VPN gateway. They can only be transferred along with the VPN gateway and cannot be transferred separately between projects. |default |
   |**Advanced option** |||
   |Tags |A tag consists of a tag key (Key) and a tag value (Value). It can be used to classify and search for customer gateways. [Prerequisite](https://docs.byteplus.com/en/docs/vpn/Tag-management)<br><br><br>* Click **Add tag** to add multiple tags as needed. You can add up to 20 tags per action, and add up to 50 tags for a single VPN gateway.<br><br>* The Keys of multiple tags for the same VPN gateway must be unique. Each Key has only one Value.<br><br>* The Key and the Value are case\-sensitive. For example, the Key=tag and the Key=Tag are two different Keys. |key:test |
   
   
   
   
   
   </Tab>
   </Tabs>
   

5. After the configuration is completed, click **Confirm order**.

6. Confirm the information to complete the purchase. Follow the console guidance to review and accept the legal terms, and then click **Buy now**. 

   * **Pay\-as\-you\-go**: Follow the console guidance to review and accept the legal terms, and then click **Buy now** to complete the action.

   * **Subscription**:

      1. Follow the console guidance to review and accept the legal terms, and then click **Buy now**.

      2. Click **Next**, select a payment method, and click **Pay**.

      3. Make the payment by the selected method. After submitting the payment information, complete the payment within the specified time. Otherwise, the order will be canceled.


<span id="hMpPDiII"></span>
## Results

After the VPN gateway is successfully created, the system automatically assigns a gateway egress IP address. You can view this egress IP in the **IP Address** column of the VPN gateway list.


* One gateway egress IP address is assigned to the single\-tunnel VPN gateway.

* Two gateway egress IP addresses, primary and secondary, are assigned to the dual\-tunnel VPN gateway.


<span id="mDMdx33Z"></span>
## What to do next

[Create a customer gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-customer-gateway1): After the VPN gateway is created, you also need to create a customer gateway to register the information of your gateway on the premises.

<span id="Tx9PnTmZ"></span>
## Related documents

[CreateVpnGateway](https://docs.byteplus.com/en/docs/vpn/CreateVpnGateway): Create a VPN gateway.
