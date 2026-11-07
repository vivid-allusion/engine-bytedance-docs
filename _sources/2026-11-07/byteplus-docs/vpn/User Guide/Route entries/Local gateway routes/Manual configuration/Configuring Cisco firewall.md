---
title: "Configuring Cisco firewall"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Configuring-a-Cisco-firewall"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

In the scenario that the Cisco firewall is applying to your local data center, after configuring the cloud VPN gateway, customer gateway, and IPsec\-VPN connection, you also need to configure the VPN connection on the Cisco firewall.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="tip">Commands in the article are examples. Adapt them to your specific environment. For more information on Cisco firewall configurations, consult third\-party vendors. This article offers a general guide only.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have completed procedures for [creating a VPN gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-VPN-gateway-2), [creating a customer gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-customer-gateway1), [creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1), and [adding a VPN gateway route](https://docs.byteplus.com/en/docs/vpn/Adding-a-VPN-gateway-route).

<span id=".5Y-C5pWw6YWN572u"></span>
## Argument configuration


* Virtual Private Cloud (VPC): The CIDR block is 192.168.2.0/24, and the Elastic IP Address (EIP) of the VPN gateway is 22.XX.XX.10.

* Data center: The private CIDR block is 10.1.1.0/24, and the static EIP of the gateway device is 122.XX.XX.64.

   > The EIP of a VPN gateway is automatically assigned when the VPN gateway is created. It serves as the egress IP address of the VPN gateway. Unlike separately purchased EIP instances, the EIP cannot be independently owned, and shares the same lifetime as the VPN gateway.   
   

<span id=".SUtFdjHniYjmnKw="></span>
## IKEv1 version

<span id=".54Gr5bGx5byV5pOOSVBzZWMg5Y-C5pWw6YWN572u"></span>
### IPsec argument configuration


* IPsec\-VPN connection

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
      |DH algorithm |group14<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the on\-premises firewall does not support the PFS feature or has no Diffie\-Hellman (DH) algorithm configured, set the value to disable.</div><br> |
      |lifecycle |86400 |
      


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Run an SSH command to log in to the configuration interface of the on\-premises Cisco firewall.

   ```Plain Text
   ssh -p admin@110.XX.XX.32  #Use the SSH command to log in to Cisco firewall.
   User Access Verification   #Input username and password to enter user mode.
   Username: admin 
   Password: ***  #The password is encrypted in this example. Enter your own password during operation.
   Type help or '?' for a list of available commands.
   ```
   

2. Enter the global configuration mode of Cisco firewall.

   ```Plain Text
   ASA>  
   ASA> en  
   Password:    #Input enable and its password to enter privileged mode, where you can only view settings.
   ASA  #conf t   
   ASA(config)#   #Input config ter to enter global mode, where you can configure firewall.
   ```
   

3. Configure a firewall interface for the VPC in global configuration mode.

   ```Plain Text
   interface GigabitEthernet0/0
   nameif outside    #Define the secure domain name for the port.
   security-level 0  #Define the security level for the port.
   ip address 122.XX.XX.64 255.255.255.255  #Input the public IP address of the on-premises data center.
   ```
   

4. Configure isakmp policy.

   ```Plain Text
   crypto ikev1 policy 1  #Set IKEv1 Phase 1 proposal number to 1 (range: 1–65535; lower number = higher priority).
   authentication pre-share  #Set the authentication method to Pre-Shared Key.
   encryption aes  #Set Phase 1 encryption algorithm to aes.
   hash sha  #Set the IKE authentication algorithm to sha.
   group 14  #Set the IKE DH group to group 14。
   lifetime 86400  #Set the IKE lifetime to 86,400 seconds.
   ```
   

5. Configure the pre\-shared key for establishing the IPsec\-VPN connection.

   ```Plain Text
   crypto isakmp key test@1234 address 22.XX.XX.10  #Enter the pre-shared key, which must match the pre-shared key used to create the IPsec-VPN connection. 22.XX.XX.10 is the public IP address of the VPN gateway.
   ```
   

6. Configure the IPsec protocol.

   ```Plain Text
   crypto ipsec transform-set ipsecpro64 esp-aes esp-sha-hmac mode tunnel  #Set the encryption algorithm and authentication algorithm for IPsec phase 2 negotiation.
   ```
   

7. Configure an ACL policy.

   ```Plain Text
   access-list 100 permit ip 10.1.1.0 0.0.0.255 192.168.2.0 0.0.0.255  # Configure ACL policy to capture data flows in the VPN tunnel. If the local gateway device has multiple network segments, you need to add an ACL policy for each segment separately.
   ```
   

8. Configure the IPsec policy.

   ```Plain Text
   crypto map ipsecpro64 10 ipsec-isakmp
   set peer 22.XX.XX.10  #Set the cloud gateway IP — use the VPN Gateway's EIP.
   set transform-set ipsecpro64  #Set the encryption map entry to use IKEv1.
   set pfs group14  #Set the DH group for the IPsec policy.
   match address 100  #Reference the traffic captured by the ACL.
   ```
   

9. Start the IPsec policy.

   ```Plain Text
   interface g0/0
   crypto map ipsecpro64
   ```
   

10. Configure a static route.

   ```Plain Text
   ip route 192.168.2.0 255.255.255.0 22.XX.XX.10
   ```
   

11. Test the connectivity between the VPC and the on\-premises data center.

   Log in to the ECS in the VPC associated with the VPN gateway, and execute the ping command. If the IP address of the local data center can be pinged, it indicates that the IPsec communication tunnel is established.


<span id=".SUtFdjLniYjmnKw="></span>
## IKEv2

<span id=".54Gr5bGx5byV5pOOSVBzZWMg5Y-C5pWw6YWN572u"></span>
### IPsec argument configuration


* IPsec\-VPN connection

   * Pre\-Shared Key: test@1234

   * NAT traversal: On

   * IKE Config

      
      |Strategy |Value |
      |---|---|
      |Authentication algorithm |sha256 |
      |Encryption algorithm |aes256 |
      |DH algorithm |group14 |
      |Negotiation |main |
      |Version |ikev2 |
      |Lifecycle |86400 |
      

   * IPsec Config

      
      |Strategy |Value |
      |---|---|
      |Authentication algorithm |sha256 |
      |Encryption algorithm |aes |
      |DH algorithm |group14<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the on\-premises firewall does not support the PFS feature or has no Diffie\-Hellman (DH) algorithm configured, set the value to disable.</div><br> |
      |Lifecycle |86400 |
      


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Follow steps 1 to 3 in the above **IKEv1 Version** procedures to log in to the local Cisco firewall configuration interface.

2. Configure arguments in IKE Phase 1.

   ```Plain Text
   crypto ikev2 proposal daemon 
   integrity sha256  #Set authentication algorithm for IKE policy to sha256.
   encryption aes-cbc-192  #Set encryption algorithm for Phase 1 negotiation to aes192.
   group 14  #Set DH algorithm for IKE policy to group 14.
   lifetime 86400  #Set lifecycle to 86400s.
   ```
   

3. Configure an IKEv2 policy.

   ```Plain Text
   crypto ikev2 policy ipsecpro64_v2  #Set IKEv2 policy.
   proposal daemon  #Apply proposal.
   ```
   

4. Configure the Pre\-Shared Key.

   ```Plain Text
   crypto ikev2 keyring ipsecpro64_v2 
   peer vpngw 
   address 22.XX.XX.10  
   pre-shared-key 0 test@1234 #Input the pre-shared key. It must match the PSK configured when creating the IPsec connection.
   ```
   

5. Configure the identity authentication information.

   ```Plain Text
   crypto ikev2 profile ipsecpro64_v2
   match identity remote address 22.XX.XX.10 255.255.255.255  #Cloud gateway IP — use the VPN Gateway's EIP.
   identity local address 10.1.1.1 #Input the IP address of local gateway.
   authentication remote pre-share     
   authentication local pre-share 
   keyring local ipsecpro64_v2
   ```
   

6. Configure the IPsec Protocol.

   ```Plain Text
   crypto ipsec transform-set ipsecpro64_v2 esp-aes esp-sha-hmac mode tunnel  #Set the encryption algorithm and authentication algorithm for IPsec Phase 2 negotiation.
   ```
   

7. Configure an ACL policy.

   ```Plain Text
   access-list 100 permit ip 10.1.1.0 0.0.0.255 192.168.2.0 0.0.0.255  #Configure ACL policy to capture data flows of VPN tunnels. If the local gateway device has multiple network segments, you need to add ACL policies for each segment separately.
   ```
   

8. Configure the IPsec policy.

   ```Plain Text
   crypto map ipsecpro64_v2 10 ipsec-isakmp
   set peer 22.XX.XX.10  #The IP address of the cloud gateway to which IPsec-protected traffic is forwarded. In this case, use the public IP address of the VPN Gateway.
   set transform-set ipsecpro64_v2  #Set the encryption mapping entry to use the IKEv2 protocol.
   set pfs group14  #Set DH group for IPsec policy.
   match address 100  #Reference the traffic captured by the ACL.
   ```
   

9. Start the IPsec policy.

   ```Plain Text
   interface g0/0
   crypto map ipsecpro64_v2
   ```
   

10. Configure a static route.

   ```Plain Text
   ip route 192.168.2.0 255.255.255.0 22.XX.XX.10
   ```
   

11. Test the connectivity between the VPC and the on\-premises data center.

   Log in to the ECS in the VPC associated with the VPN gateway, and execute the ping command. If the IP address of the local data center can be pinged, it indicates that the IPsec communication tunnel is established.
