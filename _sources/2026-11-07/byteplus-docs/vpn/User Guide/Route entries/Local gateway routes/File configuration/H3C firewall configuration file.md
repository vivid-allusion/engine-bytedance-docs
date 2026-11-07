---
title: "H3C firewall configuration file"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/H3C-firewall-configuration-file"
---

This topic describes how to configure IPsec configuration file locally when the user's on\-premises VPN gateway is an H3C firewall.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Configuration files may vary among different models from the same vendor. This article provides examples for reference only. Please consult the firewall vendor for details. The Pre\-Shared Keys used in this article are for demonstration purposes only. For actual operations, configure more secure Pre\-Shared Keys.</div>


<span id=".5LqR5LiKSVBzZWPov57mjqXphY3nva7lj4LmlbA="></span>
## Cloud IPsec\-VPN connection configuration parameters


* Pre\-Shared Key: test@1234

* Routing mode: Protected Data Flows

* Local Network: `1.1.1.1/32`, `172.1.1.1/32`

* Remote Network: `2.2.2.2/32`, `3.3.3.3/32`, `4.4.4.4/32`

* IKE Config

   
   |Strategy |Value |
   |---|---|
   |Authentication algorithm |md5 |
   |Encryption algorithm |aes192 |
   |DH algorithm |group1 |
   |Negotiation |main |
   |Version |ikev2 |
   |Lifecycle |86400 |
   |Local ID |119.XX.XX.94 |
   |Remote ID |180.XX.XX.137 |
   

* IPsec Config

   
   |Strategy |Value |
   |---|---|
   |authentication algorithm |md5 |
   |Encryption algorithm |aes192 |
   |DH algorithm |group1 |
   |Lifecycle |3600 |
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This is the configuration on the cloud: local (including the uppercase 'Local') refers to the VPN side on the cloud, while peer (including the uppercase 'Remote') refers to the user’s local VPN side. In the configuration file, it is the opposite: local (including the uppercase 'Local') refers to the user’s local VPN side, while peer (including the uppercase 'Remote') refers to the VPN side on the cloud.</div>


<span id=".6YWN572u5paH5Lu2"></span>
## Configuration file

```Plain Text
VPC utilizes unique identifiers to manipulate the configuration of
 a VPN Connection. Each VPN Connection is assigned an identifier and is
 associated with Virtual Private Gateway Identifier and User Gateway IP.

 Your VPN Connection ID : 37315  # ID of the IPsec-VPN connection on your local firewall
 Your Virtual Private Gateway ID : 23850 #ID of your local VPN gateway
 Your User Gateway IP : 180.XX.XX.137 255.255.255.255 180.XX.XX.137/32 0.0.0.0 #用户本地VPN网关的IP地址



 To configure an IKEv2-based IPsec tunnel, perform the following tasks:

 1. Internet Key Exchange (IKEv2) Configuration

 A policy is established for the supported ISAKMP encryption,
 authentication, Diffie-Hellman and key parameters.

 An IKEv2 proposal defines a set of attributes describing how IKEv2 negotiation in
 phase 1 should take place.
 By default, there is an IKEv2 proposal that is used as the default IKEv2 proposal.
 The default IKEv2 proposal parameters are as follows:
 Authentication Authentication Encryption Diffie-Hellman Duration
 method algorithm algorithm group (seconds)
 ------------------------------------------------------------------
 PRE-SHARED-KEY SHA1 DES-CBC Group 1 86400

 Create an IKEv2 keychain to use the pre-shared key for authentication.

ikev2 keychain keychain1   # Configure key information
peer peer1
address 119.XX.XX.94   #Identifier of the VPN gateway, which is the default egress IP address of the cloud VPN gateway.
pre-shared-key plaintext test@1234   #Pre-shared key
quit


ikev2 proposal 1   #Configure encryption settings
encryption aes-cbc-192   #Encryption algorithm
integrity md5   #Authentication algorithm
dh group1   #DH algorithm
quit


ikev2 policy unique
proposal 1
match local address 180.XX.XX.137  #User local VPN gateway identifier

 An IKEv2 profile is intended to provide a set of parameters for IKEv2
 negotiation. IKEv2 negotiation mode for phase 1 uses Main mode.   # Negotiation modes: main, aggressive.
 Uses the IP address of the user gateway as the local ID. Uses the WAN IP
 address of the VPN gateway as the remote ID.

ikev2 profile profile1
authentication-method local pre-share
authentication-method remote pre-share
keychain keychain1


identity local address 180.XX.XX.137  # User's local VPN gateway identifier
match remote identity address 119.XX.XX.94 #Cloud VPN Gateway Identifier
quit




 The invalid SPI recovery feature enables the receiving peer to set up an IKE
 SA with the originator so that an SPI invalid notification can be sent. Upon
 receiving the notification, the originator deletes the IPsec SA that has the
 invalid SPI. If the originator has data to send, new SAs will be set up.
 
ike invalid-spi-recovery enable


 2. IPsec Configuration

 By default, the time-based IPsec SA lifetime is 3600 seconds.

 The IPsec transform set defines the encryption, authentication, and IPsec
 mode parameters.
 The default IPsec transform-set parameters are as follows:
 Security protocol Encapsulation mode PFS feature
 ----------------------------------------------------
 ESP tunnel disabled

ipsec transform-set transform-set1
esp authentication-algorithm md5
esp encryption-algorithm aes-cbc-192


pfs dh-group1

quit


 IPsec uses ACLs to identify the traffic to be protected. Configure an IPv4
 advanced ACL to identify data flows.

 acl advanced 3001 #Configure client policy entries, where the source IP address is the user's local network segment and the destination IP address is the cloud network segment

rule permit ip source 2.2.2.2 0.0.0.0 destination 1.1.1.1 0.0.0.0
rule permit ip source 2.2.2.2 0.0.0.0 destination 172.1.1.1 0.0.0.0
rule permit ip source 3.3.3.3 0.0.0.0 destination 1.1.1.1 0.0.0.0
rule permit ip source 3.3.3.3 0.0.0.0 destination 172.1.1.1 0.0.0.0
rule permit ip source 4.4.4.4 0.0.0.0 destination 1.1.1.1 0.0.0.0
rule permit ip source 4.4.4.4 0.0.0.0 destination 172.1.1.1 0.0.0.0




 ACL for VPN connection probe




 The IPsec policy references the IPsec transform set, ACL and IKE profile.
 Configure the remote address for the IPsec tunnel in the IPsec policy policy1.



ipsec policy policy1 1 isakmp
transform-set transform-set1
security acl 3001
remote-address 119.XX.XX.94 # Remote address is the identifier of the cloud VPN gateway

ikev2-profile profile1

sa duration time-based 3600
quit

 Enable sending ICMP destination unreachable messages. The device sends ICMP
 destination unreachable message when the received packet cannot be sent to
 the destination.

ip unreachables enable


 3. Interface Configuration
 Apply the IPsec policy to an interface. All traffic routed to the interface
 will be encrypted and transmitted to the VPC. Traffic from the VPC will be
 received on this interface.  #Apply IPsec policy to the interface. All traffic routed to the interface will be encrypted and transmitted to the cloud VPC, and traffic from the cloud VPC will be delivered and received on this interface
 Finally, use the command 'ip address' to assign an IP address to the interface. 

interface myporttest1  # Local port name of the user
port link-mode route
ipsec apply policy policy1
quit
```
