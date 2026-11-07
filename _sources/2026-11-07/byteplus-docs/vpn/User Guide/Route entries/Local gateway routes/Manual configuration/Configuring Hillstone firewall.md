---
title: "Configuring Hillstone firewall"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Configuring_a_Hillstone_firewall"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

If the on\-premises data center uses Hillstone firewall, after configuring the cloud VPN gateway, customer gateway, IPsec\-VPN connection, and other actions, you also need to configure the VPN connection on the Hillstone firewall.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="tip">Different models and versions of Hillstone firewalls may have variations in configuration operations and interface displays. This document demonstrates configuration using the Hillstone SG\-6000\-VM01 model firewall with SG6000\-CloudEdge\-5.5R7P9 version. You can refer to the firewall documentation or consult the third\-party firewall vendor for specific configuration details based on your firewall model and version.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have completed procedures for [creating a VPN gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-VPN-gateway-2), [creating a customer gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-customer-gateway1), [creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1), and [adding a VPN gateway route](https://docs.byteplus.com/en/docs/vpn/Adding-a-VPN-gateway-route).

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description


* Virtual Private Cloud

   * The CIDR block is 192.168.2.0/24, and the Elastic IP Address (EIP) of the VPN gateway is 22.XX.XX.10.

      > The EIP of a VPN gateway is automatically assigned when the VPN gateway is created. It serves as the egress IP address of the VPN gateway. Unlike separately purchased EIP instances, the EIP cannot be independently owned, and shares the same lifetime as the VPN gateway.      
      

   * cloud IPsec\-VPN connection

      * Pre\-Shared Key (PSK): test@1234

      * IKE Config

         
         |Strategy |Value |
         |---|---|
         |Authentication algorithm |sha256 |
         |Encryption algorithm |aes192 |
         |DH algorithm |group14 |
         |Negotiation |main |
         |Version |ikev1 |
         |Lifecycle |86400 |
         

      * IPsec Config

         
         |Strategy |Value |
         |---|---|
         |Authentication algorithm |sha256 |
         |Encryption algorithm |aes192 |
         |DH algorithm |group14 |
         |Lifecycle |86400 |
         |Security protocol |esp |
         

* Data Center: The private CIDR block is 10.1.1.0/24. The gateway device’s static public IP address is 122.XX.XX.64. The outbound public network interface is vlan100.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

> This article only describes necessary arguments. For other arguments, you can set them as needed.



1. Log in locally to the Hillstone firewall web page.

2. Select **Network** from the top navigation bar, then select **VPN \> IPsec\-VPN** from the left navigation pane. On the **IKE VPN Configuration** page, click the **P1 Proposal** tab, then click **New** under the **P1 Proposal** tab.

3. Configure the IKE negotiation phase on the **Stage 1 Proposal Configuration** page, then click **OK** when done.

   
   |Parameter |Value |
   |---|---|
   |Policy name |P1 |
   |Authentication |Pre\-share |
   |Verification algorithm |SHA\-256 |
   |Encryption algorithm |AES\-192 |
   |DH group |Group14 |
   |Lifetime |86400 |
   

4. On the **IKE VPN Configuration** page, click the **P2 Proposal** tab, then click **New**. Configure the IPsec negotiation phase on the **Stage 2 Proposal Configuration** page, then click **OK** when finished.

   
   |Parameter |Value |
   |---|---|
   |Proposal name |P2 |
   |Protocol |ESP |
   |Authentication algorithm |SHA\-256 |
   |Encryption algorithm |AES\-192 |
   |Compression |None |
   |PFS group |Group14 |
   |Lifetime |86400 |
   

5. On the **IKE VPN Configuration** page, click the **VPN Peer List** tab, then click **New**. Create a peer VPN named **hs_to_vpc** and configure the VPN peer details under the **Basic Configuration** tab. Click **OK** when completed.

   If NAT traversal is required, enable it by clicking **Enable** under the **Advanced Configuration** tab. Click **OK** once all configurations are complete.

   
   |Parameter |Description |Value |
   |---|---|---|
   |Authentication mode |The **negotiation mode** corresponding to the IPsec\-VPN connection in the VPC. Main Mode corresponds to main, Aggressive Mode corresponds to aggressive. |main |
   |Type |Public IP address type of the cloud VPN gateway. |Static IP |
   |Peer IP |The EIP of the VPN gateway. |22.XX.XX.10 |
   |Local ID |Type of local ID. |IPv4 |
   |Local IP |The public IP address on the on\-premises data center side. |122.XX.XX.64 |
   |Peer ID |Type of local ID. |IPv4 |
   |Peer IP |The public IP address of the cloud VPN gateway. |22.XX.XX.10 |
   |Proposal 1 |P1 proposal configured in step 2. |P1 |
   |Pre\-shared key |The shared key must match the one used for the IPsec\-VPN connection with the VPC. |test@1234 |
   

6. On the **IKE VPN Configuration** page, click **IKE VPN List**, then click **New**. Refer to the following table to configure the IKE VPN under the **Basic Configuration** tab. After configuration, click **OK**, then go to the **Advanced Configuration** tab and check **Auto Connect** and **Enable**.

   
   |Parameter |Description |Value |
   |---|---|---|
   |**Peer** |||
   |Peer option |Select the name of the VPN peer created in step 5. |hs_to_vpc |
   |**Tunnel** |||
   |Name |Name of the VPN tunnel. |hs_to_vpc |
   |Mode |VPN tunnel mode. |tunnel |
   |P2 proposal |Select the P2 proposal created in step 4. |P2 |
   |Proxy ID |Select the method to configure the proxy ID |manual |
   |Local IP/mask |Enter the private network segment of the on\-premises data center. |10.1.1.0/24 |
   |Remote IP/mask |Enter the private CIDR block of the Virtual Private Cloud. |192.168.2.0/24 |
   |Service |Select the service mode, then click the **Add** button to save. |any |
   

7. Click **Security Domain** in the left navigation tree, then click **New**. Configure the security domain under the **Basic Configuration** tab. After configuration, click **OK**.

   
   |Parameter |Description |Value |
   |---|---|---|
   |Security domain name |Set the name of the security domain |sec_01 |
   |Type |Select the type of security domain. |Layer 3 security domain |
   |Virtual router |Select the virtual route of the on\-premises data center |trust_vr |
   

8. Click **Interface** in the left navigation pane, then click **New \> Tunnel Interface**. Configure the tunnel interface under the **Tunnel Interface** section’s **Basic Configuration** tab. After configuration, click **OK**.

   If you need to configure MUT and Keep\-alive IP, do so under the **Tunnel Interface** section’s **Properties** tab.

   
   |Parameter |Description |Value |
   |---|---|---|
   |**Basic configuration** |||
   |Interface name |Enter the tunnel interface name in the fixed format: `tunnel number`, where the number ranges from 1 to 64. |tunnel100 |
   |Attach security domain |Select the type of security domain to attach. |Layer 3 security domain |
   |Security domain |Select the security domain created in step 7 |sec_01 |
   |**Tunnel binding configuration** |||
   |Tunnel type |Fixed as **IPsec\-VPN**. |IPsec\-VPN |
   |VPN name |Select the VPN tunnel name from step 6, then click the **Add** button to save. |hs_to_vpc |
   

9. Select **Policy** in the top menu bar, then click **Policy** in the left navigation tree and click **New**. Configure the upstream and downstream security policies.

   1. Add an upstream security policy.

      Security policy direction from the on\-premises data center to the VPC.

      
      |Parameter |Description |Value |
      |---|---|---|
      |**Source information** |||
      |Security domain |Select the source security zone, corresponding to the name of the **virtual router** in step 7. |trust_vr |
      |Address |Select any here. |any |
      |**Purpose** |||
      |Security domain |Select the destination security domain created in step 6. |sec_01 |
      |Address |Select "any" here. |any |
      |Actions |Set the execution action of this security policy to allow or deny access. |Allow |
      

   2. Add downlink security policy.

      Security policy from VPC to on\-premises data center.

      
      |Parameter |Description |Value |
      |---|---|---|
      |**Source information** |||
      |Security domain |Select the source security domain, which is the name of the security domain created in step 6. |sec_01 |
      |address |Select any here. |any |
      |**Purpose** |||
      |Security domain |Destination source security domain, which is the name of the **virtual router** in step 6. |trust_vr |
      |Address |Select any here. |any |
      |Actions |Set the enforcement action for this security policy to allow or deny access. |Allow |
      

10. Select **Network** in the top navigation bar, then click **Route** in the left navigation pane, and click **Create** to add uplink and downlink routes.

   1. Uplink route

      Route from on\-premises data center to VPC.

      
      |Parameter |Description |Value |
      |---|---|---|
      |Associated virtual router |Select the virtual route of the on\-premises data center in step 6. |trust_vr |
      |Destination |Private network segment of the Virtual Private Cloud |192.168.2.0 |
      |Subnet mask |Mask of CIDR block. |24 |
      |Next Hop |Select the Next Hop type. |Interface |
      |Interface |Select the name of the newly created interface in step 8. |tunnel100 |
      

   2. Downlink route: configure the route for the firewall’s downlink interface yourself. If the firewall downlink interface IP address belongs to the on\-premises data center’s private network segment, there is a direct local route, and no need to configure the downlink route again.
