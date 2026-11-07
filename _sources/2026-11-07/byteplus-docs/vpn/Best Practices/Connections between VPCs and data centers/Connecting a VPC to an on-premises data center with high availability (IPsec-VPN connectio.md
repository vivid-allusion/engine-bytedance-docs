---
title: "Connecting a VPC to an on-premises data center with high availability (IPsec-VPN connection with dynamic routing)"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-data-center-with-high-availability-communication-dynamic-route"
---

This topic desctibes high availability networking solutions and configuration instructions between a Virtual Private Cloud (VPC) and an on\-premises data center (IDC) through VPN Connect in dynamic route mode.

* High availability for primary and secondary links: Configure dynamic routes with the same Destination CIDR and different AS\-PATH lengths through VPN\-IPsec, or configure static routes with different Destination CIDR Block mask sizes. This document uses dynamic routes as an example.

* Dual\-link high availability: Configure routes with the same Destination CIDR Block through TR\-IPsec.

## Enable primary\-secondary link connectivity by associating VPN gateway via IPsec\-VPN

### Networking scenario

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9fdc0fca3f15c1ff6e1ae864900ec1c3.png)

### Prerequisites

* Create a VPC and its subnet. For specific actions, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* The IDC has a static Elastic IP Address (EIP) and supports BGP route protocol.

* The IDC subnet does not overlap with the private subnet of the VPC.

### Configuration instructions

> **tip**

> Only necessary parameters for high availability scenarios are introduced; other parameters should remain at their default values.

1. Create one VPN gateway. For detailed steps, see [Creating a VPN gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-VPN-gateway-2). Parameter descriptions are shown in the table below.

   |**Parameter** |**Description** |**Sample value** |
   |---|---|---|
   |**Basic information** |||
   |Protocol type |Select the protocol type of the VPN gateway. |IPsec\-VPN connection |
   |Billing method |The billing method of the VPN gateway. |Subscription |
   |Regions |Select the region where the VPN gateway resides. It must be the same region as the VPC. |China (Beijing) |
   |Name |Name of the VPN gateway. |VPNGW\-test |
   |Tunnel mode |The tunnel mode of the VPN gateway. |Single tunnel |
   |IP address type |The IP address type used to interconnect the VPN gateway and the client. In single\-tunnel mode, only IPv4 addresses are supported. |IPv4 |
   |Protocol type |The protocol type of VPN gateway tunnels. All tunnels attached to the VPN gateway use the same type. For single\-tunnel VPN gateways, only IPv4 addresses are supported. |IPv4 |
   |**Network Configuration** |||
   |BGP ASN |Set the ASN (Autonomous System Number) for the VPN gateway; it must not duplicate the BGP ASN of the customer gateway. |65000 |

   > **tip**

   > After successfully creating the VPN gateway VPNGW\-test, the system assigns the gateway's egress IP as 180.XX.XX.91.

2. Create two customer gateways. For detailed steps, see [Creating a ustomer gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-customer-gateway1). Parameter descriptions are shown in the table below.

   |**Parameter** |**Description** |**Sample value (Customer gateway 1)**  |**Sample value (Customer gateway 2)**  |
   |---|---|---|---|
   |Regions |Select the user gateway's region; it must match the VPN gateway VPNGW\-test's region. |China (Beijing) |China (Beijing) |
   |Name |Set the name for the customer gateway. |CGW\-01 |CGW\-02 |
   |IP Address |Type the static EIP address of the IDC's gateway. |27.XX.XX.42 |22.XX.XX.8 |
   |BGP ASN |Set the ASN (Autonomous System Number) for the customer gateway. Only the IPsec\-VPN connection using dynamic route propagation mode requires configuring the customer gateway BGP ASN. This parameter must be configured for this solution.<br><br><br>* The valid range for the customer gateway BGP ASN is 1 to 4294967294. The values 137718, 65535, and 150436 are unavailable.<br><br>* The customer gateway BGP ASN must not duplicate the VPN gateway BGP ASN or another customer gateway BGP ASN. |64001 |64002 |

3. Create two IPsec\-VPN connections. For detailed steps, see Creating an IPsec\-VPN connection. The parameter descriptions are shown in the table.

   |**Parameter** |**Description** |**Sample value (primary)**  |Sample value (secondary) |
   |---|---|---|---|
   |**Basic information** ||||
   |Regions |Select the region where the IPsec\-VPN connection is located. It must be the same region as the VPNGW\-test. |China (Beijing) |China (Beijing) |
   |Name |Name of the IPsec\-VPN connection. |IPsecVPN\-01 |IPsecVPN\-02 |
   |**Associate resources** ||||
   |Attach Type |Select the resource type associated with the new IPsec\-VPN connection.<br><br><br>* VPN gateway: Associate the IPsec\-VPN connection with a VPN gateway.<br><br>* TR: Associate the IPsec\-VPN connection to a Transit Router (TR).<br><br>* Associate to TR later: Associate the IPsec\-VPN connection with a TR later. |VPN gateway |VPN gateway |
   |VPN gateway |Select VPN gateway VPNGW\-test created under VPC. |VPNGW\-test |VPNGW\-test |
   |**Connection information** ||||
   |Routing mode |Select a routing mode. |Destination Routing Mode |Destination Routing Mode |
   |Negotiate instantly |Specify whether the IPsec\-VPN connection takes effect immediately after configuration. |Yes |Yes |
   |Routing propagation mode |Select a routing propagation mode. |Dynamic |Dynamic |
   |Customer gateway |Select the customer gateway. |CGW\-01 |CGW\-02 |
   |Tunnel CIDR block |The CIDR block where the local and peer tunnel IPs reside. A tunnel CIDR block must meet all three of the following requirements:<br><br><br>* Must be within 169.254.0.0/16 CIDR block and not within 169.254.255.0/24 CIDR block.<br><br>* Its subnet mask must be `/30`. |169.254.1.0/30 |169.254.2.0/30 |
   |Local Tunnel IP |The local tunnel IP is the BGP address configured on the VPN gateway. |169.254.1.1 |169.254.2.1 |
   |Peer Tunnel IP |The peer tunnel IP is the BGP address configured on the user device. |169.254.1.2 |169.254.2.2 |
   |Pre\-shared key |Type the key used for IKE negotiation between VPN devices on both sides.<br><br>> **warning**<br><br><br>> This information is crucial. Keep it secure.<br> |test@123 |test@123 |
   |Confirm key |Type the Pre\-Shared Key again. |test@123 |test@123 |
   |**Advanced configuration** ||||
   |Health check |Select whether to enable IPsec\-VPN connection health check.<br><br>After enabling health check, the VPN gateway probes IPsec tunnel connectivity based on your health check settings and displays the status.<br><br><br>* **Source IP**: The IP address on the local VPC side accessible through the IPsec connection from the IDC or peer VPC. **The IP address within the VPC in this context.** <br><br>* **Destination IP**: The IP address of the peer IDC or peer VPC accessible through the IPsec connection from the local VPC. **This exampled refers to IP addresses in the IDC.** <br><br>* **Detect interval**: The time interval for performing health checks.<br><br>* **Response timeout**: The time to wait for a health check response. The response timeout must not be longer than the probe interval.<br><br>* **Healthy threshold**: The number of successful health checks required to mark the status as healthy. Default value: 3.<br><br>* **Unhealthy threshold**: The number of retries for health checks. Default value: 3.<br><br><br>> **tip**<br><br><br>> If you cannot configure health checks, your VPN gateway may not be the latest version. Please [upgrade the VPN gateway](https://docs.byteplus.com/en/docs/vpn/Upgrading-a-VPN-gateway).<br> |Enable and add the following probe IPs:<br><br><br>* Source IP: 192.168.1.10<br><br>* Destination IP: 192.168.2.10<br><br>* Probe interval, response timeout, healthy threshold, and unhealthy threshold keep their default values |Enable and add the following probe IPs:<br><br><br>* Source IP: 192.168.1.20<br><br>* Destination IP: 192.168.2.20<br><br>* Probe interval, response timeout, healthy threshold, and unhealthy threshold remain at their default values |

4. Configure VPN for the gateway device of an IDC. For detailed steps, see [File transfer overiew](https://docs.byteplus.com/en/docs/vpn/Overview-1).

   > **warning**

   > When configuring the local gateway route, the AS\-PATH length of the gateway on the primary link should be less than that of the secondary link.

### Result verification

After the above steps are completed, the route will automatically propagate between the VPC and the local IDC using the BGP route protocol, and the local IDC and VPC can communicate normally.

1. Log in to the Elastic Compute Service in the VPC. For login procedures, see [Login to Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Login to Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Run the command `ping` to connect to the server in the IDC and verify connectivity.

3. Check the monitoring data of the IPsec\-VPN connection to verify the traffic path.

   * Under normal conditions, traffic reaches the IDC via the primary link (IPsecVPN\-01).

   * If the primary link is disconnected, traffic routes to the IDC via the secondary link (IPsecVPN\-02).

## Achieve dual\-link load balancing by attaching TR via IPsec\-VPN

### Networking scenario

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_82d191b199f4864f79a1092b4e684792.png)

### Prerequisites

* Create a VPC and its subnet. For specific actions, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* The IDC has a static EIP and supports BGP routing protocol.

* The IDC network segment does not overlap with the VPC private network segment.

### Configuration instructions

> **tip**

> Only key parameters for the high availability scenario are introduced; other parameters remain default or can be selected as needed.

1. Create a Transit Router (TR) instance. For detailed steps, see [Creating a Transit Router instance](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1). Parameter description is shown in the following table.

   |**Parameter** |**Description** |**Sample value** |
   |---|---|---|
   |Regions |Select the region where the Transit Router instance belongs; it must be the same as the VPC region to connect. |China (Beijing) |
   |Name |Type the name for the TR instance to be created. |tr01 |
   |ASN |Specify a BGP ASN for the TR instance. Valid range: 64512\-65534 or 4200000000\-4294967294.<br><br>The ASN assigned here will be automatically prepended to the AS_Path attribute of routes propagated to other network instances. |64512 |

2. Create two customer gateways. For detailed steps, see Creating a customer gateways. The parameters are described in the table below.

   |**Parameter** |**Description** |**Sample value (Customer gateway 1)**  |**Sample value (Customer gateway 2)**  |
   |---|---|---|---|
   |Region |Select the region where the customer gateway resides. It must be the same region as the VPN gateway VPNGW\-test. |China (Beijing) |China (Beijing) |
   |Name |Set the name for the customer gateway. |CGW\-01 |CGW\-02 |
   |IP Address |Type the static EIP address of the IDC's gateway. |27.XX.XX.42 |22.XX.XX.8 |
   |BGP ASN |Set the ASN (Autonomous System Number) for the customer gateway. Only IPsec\-VPN connections using dynamic route propagation mode require configuration of the customer gateway BGP ASN. This parameter must be configured for this solution.<br><br><br>* The valid range for the customer gateway BGP ASN is: 1 to 4294967294. The values 137718, 65535, and 150436 are unavailable.<br><br>* The customer gateway BGP ASN must not overlap with the BGP ASN of the TR or with another customer gateway BGP ASN. |64001 |64002 |

3. Create two IPsec\-VPN connections. For detailed steps, see [Creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1). The parameter descriptions are shown in the table.

   |**Parameter** |**Description** |**Sample value (primary)**  |Sample value (secondary) |
   |---|---|---|---|
   |**Basic information** ||||
   |Region |Select the region of the IPsec connection, which must match the region of VPNGW\-test. |China (Beijing) |China (Beijing) |
   |Name |Name of the IPsec\-VPN connection. |IPsecVPN\-01 |IPsecVPN\-02 |
   |**Associate resources** ||||
   |Attach type |Select the resource type associated with the new IPsec\-VPN connection.<br><br><br>* VPN gateway: Associate the IPsec\-VPN connection with a VPN gateway.<br><br>* TR: Associate the IPsec\-VPN connection to a Transit Router (TR).<br><br>* Associate to TR later: Associate the IPsec\-VPN connection with a TR later. |Transit Router |Transit Router |
   |Transit Router |Select the created TR tr01. |tr01 |tr01 |
   |Availability zone |Select the Availability Zone where the TR provides services. |Availability Zone A |Availability Zone A |
   |**Connection information** ||||
   |Routing mode |Select a routing mode. |Destination routing |Destination Routing Mode |
   |Negotiate instantly |Specify whether the IPsec\-VPN connection takes effect immediately after configuration. |Yes |Yes |
   |Routing propagation mode |Select a routing propagation mode. |Dynamic |Dynamic |
   |Customer gateway |Select the customer gateway. |CGW\-01 |CGW\-02 |
   |Tunnel CIDR block |The CIDR block where the local and peer tunnel IPs reside. The tunnel subnet must meet the following requirements:<br><br><br>* Must be within 169.254.0.0/16 CIDR block and not within 169.254.255.0/24 CIDR block.<br><br>* Its subnet mask must be `/30`. |169.254.1.0/30 |169.254.2.0/30 |
   |Local Tunnel IP |The local tunnel IP is the BGP address configured on the VPN gateway. |169.254.1.1 |169.254.2.1 |
   |Peer tunnel IP |The peer tunnel IP is the BGP address configured on the user device. |169.254.1.2 |169.254.2.2 |
   |Pre\-shared key |Type the key used for IKE negotiation between VPN devices on both sides.<br><br>> **warning**<br><br><br>> This information is crucial. Keep it secure.<br> |test@123 |test@123 |
   |Confirm the key |Type the Pre\-Shared Key again. |test@123 |test@123 |
   |**Advanced configuration** ||||
   |Health check |Select whether to enable the health check feature for the IPsec\-VPN connection.<br><br>After enabling health check, the VPN gateway probes IPsec tunnel connectivity based on your health check settings and displays the status.<br><br><br>* **Source IP**: refers to the IP address on the local VPC side accessed by the IDC or peer VPC via IPsec\-VPN connection. **This refers to the IP address within the VPC.** <br><br>* **Destination IP**: The IP address of the IDC or peer VPC accessed by the local VPC via IPsec\-VPN connection. **This refers to the IP address in the IDC.** <br><br>* **Detect interval**: The time interval to perform the health check.<br><br>* Response Timeout: The time to wait for a health check response. The response timeout must not be longer than the probe interval.<br><br>* **Healthy threshold**: The number of health checks to determine a normal status. Default value: 3.<br><br>* **Unhealthy threshold**: The number of health check retries. Default value: 3.<br><br><br>> **tip**<br><br><br>> If you cannot configure the health check, it may be because your VPN gateway is not up to date. Please [upgrade the VPN gateway](https://docs.byteplus.com/en/docs/vpn/Upgrading-a-VPN-gateway).<br> |Turn on and add the following detection IPs:<br><br><br>* Source IP: 192.168.1.10<br><br>* Destination IP: 192.168.2.10<br><br>* Probe interval, response timeout, healthy threshold, and unhealthy threshold keep default values |Turn on and add the following probe IPs:<br><br><br>* Source IP: 192.168.1.20<br><br>* Destination IP: 192.168.2.20<br><br>* Probe interval, response timeout, healthy threshold, and unhealthy threshold keep default values |

   > **tip**

   > After the IPsec\-VPN connection is created and the TR is successfully associated, the system automatically allocates an Elastic IP Address (EIP) as the egress IP address for the cloud. You can retrieve this Elastic IP Address from the Associate resource area on the IPsec\-VPN connection details page.

4. Configure VPN for the gateway device of an IDC. For detailed steps, see [File transfer overiew](https://docs.byteplus.com/en/docs/vpn/Overview-1).

### Result verification

After the above steps are completed, the route will automatically propagate between the VPC and the local IDC using the BGP route protocol, and the local IDC and VPC can communicate normally.

1. Log in to the ECS instance in the VPC. For login steps, see [Login to Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Login to Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Execute the command `ping` to connect to the server in the IDC and verify connectivity.

3. By checking the IPsec\-VPN connection monitoring data, you can see that the traffic is evenly distributed across the two links.
