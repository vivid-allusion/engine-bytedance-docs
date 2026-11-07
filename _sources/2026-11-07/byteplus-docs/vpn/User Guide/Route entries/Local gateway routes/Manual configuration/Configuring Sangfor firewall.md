---
title: "Configuring Sangfor firewall"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Configuring_a_Sangfor_firewall"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

After configuring the cloud VPN gateway, customer gateway, and IPsec\-VPN connection, you also need to configure the VPN connection on the Sangfor firewall in your data center.

<span id=".5Y-C5pWw6YWN572u"></span>
## Argument configuration


* CIDR block information

   The CIDR block of the Virtual Private Cloud (VPC) is 192.168.1.0/24, and the public IP address of the VPN gateway is 23.XX.XX.18. The private CIDR block of the data center is 10.0.0.0/24, and the static EIP of the gateway device is 110.XX.XX.64.

   > The EIP of a VPN gateway is automatically assigned when the VPN gateway is created. It serves as the egress IP address of the VPN gateway. Unlike separately purchased EIP instances, the EIP cannot be independently owned, and shares the same lifetime as the VPN gateway.   
   

* IPsec\-VPN connection

   * Pre\-Shared Key: test@1234

   * NAT traversal: On

   * IKE Config

      
      |Strategy |Value |
      |---|---|
      |Authentication algorithm |sha256 |
      |Encryption algorithm |aes |
      |DH algorithm |group14 |
      |Negotiation |aggressive |
      |Version |ikev2 |
      |Lifecycle |86400 |
      

   * IPsec Config

      
      |Strategy |Value |
      |---|---|
      |Authentication algorithm |sha256 |
      |Encryption algorithm |aes |
      |DH algorithm |group14 |
      |Lifecycle |86400 |
      


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

> This article only describes necessary arguments. For other arguments, you can set them as needed. Different versions of the Sangfor firewall may have different interfaces and ingress points. You can consult the firewall vendor for details.



1. Log in to the Web page of Sangfor firewall locally. In the left\-side navigation pane, select VPN \> IPsec\-VPN \> Third\-Party Interfacing \> Phase 1.

2. Configure the Sangfor firewall Phase 1 according to the IKE Config of the IPsec\-VPN connection.

   At the top of the right\-side page, select Line Out and then click New to create a new connection.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Device name |Enter the device name. |VPN0001 |
   |Device address type |Select Fixed Remote IP. |Fixed Remote IP |
   |Fixed IP |Enter the IP address of the cloud VPN gateway. |23.XX.XX.18 |
   |Authentication |Select Pre\-Shared Key. |Pre\-shared key |
   |Pre\-shared key |The Pre\-Shared Key set when creating the IPsec\-VPN connection. |test@1234 |
   |Enable device |Checked by default. |Check |
   |Enable active connection |Checked by default. |Check |
   

3. Click Advanced for the advanced settings of the connection, and then click OK when completed.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |ISAKMP lifetime |The ISAKMP lifetime must be consistent with the IKE lifecycle set when you create the IPsec\-VPN connection. |86400 |
   |Retry attempts |Number of connection retries. |10 |
   |Mode |On the Sangfor firewall, select Aggressive mode for NAT traversal to correspond to the IKE Negotiation mode of IPsec\-VPN connection. |Aggressive |
   |DH group |Select MOOP group1024 (3). |MOOP group1024 (3) |
   |Local ID type |Select IPv4 address (IPv4 ADDR). |IPv4 address (IPv4 ADDR) |
   |Local ID |IP address of the local gateway. |110.XX.XX.64 |
   |Remote ID type |Select IPv4 Address (IPv4 ADDR). |IPv4 address (IPv4 ADDR) |
   |Remote identity ID |IP address of the cloud VPN gateway. |23.XX.XX.18 |
   |Enable Dead Peer Detection |Unchecked in this example. |Unchecked |
   |Enable NAT traversal |Check this example. |Check |
   |Authentication algorithm |Select authentication algorithm. |SHA256 |
   |Encryption algorithm |Select the encryption algorithm. |AES |
   

4. In the left\-side navigation pane, select VPN \> IPsec\-VPN \> Third\-Party Interfacing \> Phase 2.

5. Configure the inbound policy based on the CIDR block information.

   On the Inbound Policy tab, click New to create a new inbound policy, and then click OK after completion.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Policy name |Enter a name for the inbound policy. |testin |
   |Source IP type |Select Subnet+Mask. |subnet + mask |
   |Subnet |Enter the subnet of the VPC. |192.168.1.0 |
   |Mask |Enter the mask of the subnet. |255.255.255.0 |
   |Peer device |Select the phase one configuration device name. |VPN0001 |
   |Inbound service |Select allowed services. |All services |
   |Security options |Specify security settings. |Default security settings |
   |Enable this policy |Check to enable. |Check |
   

6. Configure the outbound policy based on the CIDR block information.

   On the Outbound Policy tab, click New to create a new outbound policy.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Policy name |Name the policy. |testout |
   |Source IP type |Select the type of source IP. |Subnet + mask |
   |Subnet |Enter local subnet. |10.0.0.0 |
   |Mask |Enter local mask. |255.255.255.0 |
   |Peer device |Select the device name for Stage 1 configuration. |VPN0001 |
   |Outbound service |Select allowed services. |All services |
   |Security options |Specify security settings. |Default security settings |
   |Enable this policy |Check to enable. |Check |
   

7. In the left\-side navigation pane, select VPN \> IPsec\-VPN \> Third\-Party Interfacing \> Security Setting.

8. Configure security settings based on the IPsec Config of the IPsec\-VPN connection.

   Click Add, configure the security settings on the pop\-up page, and then click OK after completion.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Name |Custom name. |test connection |
   |Protocol |Phase 2 authentication protocol, ESP in this example. |ESP |
   |Encryption algorithm |The encryption algorithm configured for the IPsec\-VPN connection. |SHA256 |
   |Authentication algorithm |The authentication algorithm configured for the IPsec\-VPN connection. |AES |
   

9. Configure routes and ACLs of the data center to allow traffic accessing VPC into the VPN communication tunnel.
