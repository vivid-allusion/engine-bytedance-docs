---
title: "Creating a VPN gateway"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Creating-a-VPN-gateway-1"
---

This topic describes how to quickly create an available VPN gateway. This configuration example only provides required parameters. For more parameters and descriptions, see [Creating a VPN gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-VPN-gateway-2).

## Procedure

1. Log in to the [VPN gateway console](https://console.byteplus.com/vpn/vpnGateway).

2. In the top menu bar, select the target project and region.

3. Click **Create VPN Gateway** to enter the Create VPN Gateway page.

4. Configure Basic information for the VPN gateway based on the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |Protocol type |Select the protocol type of the VPN gateway. |SSL connection |
   |Billing method |The billing method of the VPN gateway. |Subscription |
   |Region |Select the region where the VPN gateway is located. Keep it consistent with the region of VPC2.​ |China (Beijing) |
   |Name |The name of the VPN gateway. |VPNGW\-SSL |
   |Tunnel mode |The tunnel mode of the VPN gateway. Currently, only single\-tunnel mode is supported. |Single tunnel |
   |IP address type |The IP address type for the connection between the VPN gateway and the client. A single\-tunnel mode VPN gateway only supports the IPv4 address type. |IPv4 |
   |Protocol type |The protocol type used within the VPN gateway tunnels. All tunnels associated with the VPN gateway will use the same protocol type. A single\-tunnel mode VPN gateway only supports the IPv4 address type. |IPv4 |

5. Configure Network information for the VPN gateway based on the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |Bandwidth |Set the bandwidth cap for the VPN gateway. This limit applies to the public bandwidth in both the outbound and inbound VPC directions.​ For more details, see [VPN gateway bandwidth limits](https://docs.byteplus.com/en/docs/vpn/Limits#.VlBO572R5YWz5bim5a696ZmQ5Yi2).<br><br><br>* This value is the bandwidth shared for all IPsec\-VPN connections and SSL\-VPN connections created on this VPN gateway. That is, the total bandwidth of IPsec\-VPN and SSL\-VPN connections cannot exceed the bandwidth of the VPN gateway.<br><br>* After the VPN gateway is created, you can adjust Bandwidth of the VPN gateway as needed. For more information, see [Modifying configuration for VPN gateway](https://docs.byteplus.com/en/docs/vpn/Modifying-VPN-gateway-configurations).<br><br><br>> **tip**<br><br><br>> The bandwidth limit applies to encapsulated encrypted packets. To configure alarm strategies in Cloud Monitor to monitor VPN gateway metrics, select monitoring metrics including packet encapsulation overhead for trigger conditions, such as VPN gateway outbound/inbound bandwidth usage.<br> |20Mbps |
   |SSL Max Connections |Set the maximum number of clients that can connect to the SSL VPN at the same time.​ |10 |
   |VPC |Select the VPC where the VPN gateway resides. Only VPCs within the current project are selectable. |VPC1 \| 10.1.0.0/16 |
   |Subnet |Select the subnet where the VPN gateway resides. The VPN gateway occupies three IPv4 addresses in the subnet. Reserve sufficient IPv4 addresses. |subnet \| 10.1.0.0/24 \| Availability Zone A |
   |BGP ASN |Set the Autonomous System Number (ASN) for the VPN gateway. If the IPsec\-VPN connection uses dynamic routing propagation mode, configure a BGP ASN for the VPN gateway. If static routing is used, BGP ASN is not required.<br><br><br>* Once configured, the BGP ASN of the VPN gateway cannot be modified.<br><br>* Valid ranges of BGP ASN: 64512 to 65534 and 4200000000 to 4294967294.<br><br>* If this VPN gateway is later used to create an IPsec\-VPN connection with dynamic routing, ensure that different ASNs are assigned to the VPN gateway and the customer gateway attached to the same IPsec\-VPN connection. |65024 |

6. Configure Feature information for the VPN gateway based on the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |Purchase duration |The ​​validity period​​ for which the VPN gateway is subscribed. |1 month |
   |Automatic renewal |Specify whether to enable automatic renewal. If automatic renewal is enabled, the renewal length is one month and the number of renewals is unlimited. You can manually disable automatic renewal or visit the **Billing center** to modify the number of renewals. For procedure, see [Automatic renewal](https://docs.byteplus.com/en/docs/byteplus-platform/docs-auto-renewal-rules). For VPN gateways that you rely on for the long term, we recommend checking Automatic renewal to prevent any disruption when they expire. |Disable |
   |Affiliated project |Select the project to which the new VPN gateway belongs. A project refers to a task in your daily work. You can create multiple projects under the same account and create or purchase cloud resources for each project. Cloud resources cannot be shared between different projects.<br><br><br>* After the project is selected, the created VPN gateway can only be used by users with permissions for that project.<br><br>* If you have selected **All Resources** in the top menu bar, the created VPN gateway belongs to the default project by default. You can modify the project as needed.<br><br>* If you have selected a specific project in the top menu bar, the new VPN gateway belongs to that project. You can modify the project in the top menu bar.<br><br>* If no projects are available, click **Create project** on the right to create a new project.<br><br>* After a VPN gateway is added to a project, you can transfer the VPN gateway out of the project based on your business needs. For details, see [Project resource management](https://docs.byteplus.com/en/docs/6649/94337).<br><br>* VPN gateway routes are sub\-resources of the VPN gateway. They can only be transferred along with the VPN gateway and cannot be transferred separately between projects. |default |
   |Tags |A tag consists of a tag key and a tag value. It can be used to classify and search VPN gateways. [Learn more](https://docs.byteplus.com/en/docs/vpn/Tag-management)<br><br><br>* Click **Add tag** to add multiple tags as needed. You can add up to 20 tags per action, and add up to 50 tags for a single VPN gateway.<br><br>* The keys of multiple tags for the same VPN gateway must be unique. Each key can have only one value.<br><br>* The key and value are case\-sensitive. For example, Key=tag and Key=Tag are two different keys. |key:test |

8. Click **Confirm order**. Follow the console guidance to review and accept the legal terms, and then click **Buy now**.

9. After confirming that the order information is correct, proceed with payment according to the guidance.

   After the VPN gateway is created, the system assigns an egress IP address: 180.XX.XX.232. It is displayed in the **IP Address** column of the VPN gateway list.

## What to do next

* [Create an SSL-VPN server](https://docs.byteplus.com/en/docs/vpn/Creating-an-SSL-server)

* [Create an SSL-VPN client and download certificate](https://docs.byteplus.com/en/docs/vpn/Creating-and-downloading-an-SSL-client-certificate)

* [Configure a client](https://docs.byteplus.com/en/docs/vpn/Configuring-the-client)

* [Test connectivity](https://docs.byteplus.com/en/docs/vpn/Testing-connectivity1)
