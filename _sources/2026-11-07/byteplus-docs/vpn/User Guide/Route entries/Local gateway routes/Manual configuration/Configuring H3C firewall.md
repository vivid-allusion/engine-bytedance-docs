---
title: "Configuring H3C firewall"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Configuring-an-H3C-firewall"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

In the scenario that the H3C firewall is applying to your local data center, after configuring the cloud VPN gateway, customer gateway, and IPsec\-VPN connection, you also need to configure the VPN connection on the H3C firewall.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="tip">Configurations and interface layout may differ among different models and versions of H3C firewalls. You can refer to the corresponding documentation or consult the third\-party firewall vendor for specific configuration based on the firewall model you use.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have completed procedures for [creating a VPN gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-VPN-gateway-2), [creating a customer gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-customer-gateway1), [creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1), and [adding a VPN gateway route](https://docs.byteplus.com/en/docs/vpn/Adding-a-VPN-gateway-route).

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description


* Virtual Private Cloud (VPC)

   * The CIDR block is 192.168.2.0/24, and the Elastic IP Address (EIP) of the VPN gateway is 22.XX.XX.10.

      > The EIP of a VPN gateway is automatically assigned when the VPN gateway is created. It serves as the egress IP address of the VPN gateway. Unlike separately purchased EIP instances, the EIP cannot be independently owned, and shares the same lifetime as the VPN gateway.      
      

   * cloud IPsec\-VPN connection

      * Pre\-Shared Key: test@1234

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
         |security protocol |esp |
         

* Data center: The private CIDR block is 10.1.1.0/24, and the EIP of the gateway device is 122.XX.XX.64. The interface used by the gateway device to connect to the internet is Reth1.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

> This topic only describes necessary arguments. For other arguments, you can set them as needed.



1. Log in to the Web page of the H3C firewall locally.

2. Create a new IPsec policy.

   1. In the left\-side navigation pane, click Network \> VPN \> IPsec \> Policy.

   2. On the Create IPsec Policy page, configure an on\-premises IPsec policy. Ensure the local IPsec policy matches the IPsec\-VPN connection configuration created in the VPC.

   3. The configuration parameters of the cloud IPsec\-VPN connection are shown in the parameter description. The necessary local parameter configurations are listed in the table. Save the configuration after completing the setup.

      
      |Parameter |Description |Value |
      |---|---|---|
      |**Basic configuration** |||
      |Interface |The gateway device interface connected to the internet. |Reth1 |
      |IP address type |The type of IP address. |IPv4 |
      |pattern |Select **peer/branch node**. |Peer/branch node |
      |Peer IP address/hostname |Public IP address of the cloud VPN gateway. |22.XX.XX.10 |
      |Negotiation |During the IKE authentication phase, the negotiation modes are as follows: Main mode corresponds to "main" on the cloud; Aggressive mode corresponds to "aggressive" on the cloud. |main |
      |Authentication |Select Pre\-Shared Key. |Pre\-shared key |
      |Pre\-shared key |The Pre\-Shared Key is set when creating the IPsec\-VPN connection. |test@1234 |
      |Type Pre\-Shared Key again. |Confirm pre\-shared key. |test@1234 |
      |Peer ID |The public IP address of the cloud VPN gateway. |22.XX.XX.10 |
      |Local ID |Public IP address of the local VPN gateway. |122.XX.XX.64 |
      |**Protected data flow** |||
      |Source IP address |Private network segment of the local data center. |10.1.1.0/24 |
      |Destination IP address |CIDR block of the cloud communication VPC. |192.168.2.0/24 |
      

3. In the left navigation tree, click **Network \> VPN \> IPsec \> IKE Config**, then click **New** to add an IKE configuration. Click **OK** when finished.

   The IKE configuration here must match the IKE configuration in the cloud IPsec\-VPN connection.

   
   |Parameter |Value |
   |---|---|
   |Priority |10 |
   |Authentication |Pre\-shared key |
   |Authentication algorithm |SHA256 |
   |Encryption algorithm |AES\-CBC\-192 |
   |DH |DH group 14 |
   |IKE SA lifecycle |86400 |
   

4. In the left navigation tree, click **Network \> VPN \> IPsec \> Policy**, find the policy created in step 2, add an IPsec Config under **Advanced configuration**, then click **OK** after finishing the configuration.

   The IPsec Config here must match the IPsec Config in the cloud IPsec\-VPN connection.

   
   |Parameter |Value |
   |---|---|
   |Encapsulation pattern |Tunnel mode |
   |Security protocol |ESP |
   |ESP authentication algorithm |SHA256 |
   |ESP encryption algorithm |AES\-CBC\-192 |
   |PFS |Group_14 |
   |IPsec SA lifetime (time\-based) |86400 |
   |Local IP address |122.XX.XX.64 |
   

5. In the left navigation tree, click **Network \> VPN \> IPsec \> Policy \> Security Policy \> Create** to create outbound and inbound security policies respectively.

   * Outbound security policy

      Security policy from the local data center to the cloud Virtual Private Cloud.

      
      |Parameter |Description |Value |
      |---|---|---|
      |Name |Enter the name of this uplink security policy. |h3c_to_vpc |
      |Source security zone |Select source security domain. |Trust |
      |Destination security domain |Select the destination security domain. |Untrust |
      |Type |Select the IP type. |IPv4 |
      |Actions |Set the execution action of this security policy to allow or deny access. |Allow |
      |Source IP address |Private CIDR block of the on\-premises data center. |10.1.1.0/24 |
      |Destination IP address |CIDR block of the Virtual Private Cloud (VPC) |192.168.2.0/24 |
      

   * Inbound security policy

      Security policy from the cloud Virtual Private Cloud to the local data center.

      
      |Parameter |Description |Value |
      |---|---|---|
      |Name |Enter the name of this outbound security policy. |vpc_to_h3c |
      |Source security domain |Select source security zone. |Untrust |
      |Destination security domain |Select the destination security domain. |Trust |
      |Type |Select the IP type. |IPv4 |
      |Actions |Set the execution action of this security policy to allow or deny access. |Allow |
      |Source IP address |The CIDR block of the VPC. |192.168.2.0/24 |
      |Destination IP address |Private CIDR block of the local data center. |10.1.1.0/24 |
      

6. Click **Network \> Route \> Static Route** in the left navigation tree to enter the **Create IPv4 Static Route** page. Add a static route from the on\-premises data center to the VPC, then click **OK**.

   * Uplink route

      Route from on\-premises data center to VPC.

      
      |Parameter |Description |Value |
      |---|---|---|
      |VRF |Select the type of VRF. |Internet |
      |Destination IP address |Enter the destination IP address. |0.0.0.0 |
      |Mask length |Enter mask length. |0 |
      |**Next Hop** |||
      |VRF to which the next hop belongs |Select the **VRF of the next hop** and choose **internet**. |Check, internet |
      |Next Hop IP address |Enter the IP address of the next hop. |22.XX.XX.10 |
      

   * Downlink route

      Route from VPC to on\-premises data center. Since this operation uses direct routes, configuring downlink routes is not required. You can also configure related static route entries based on actual network conditions.
