---
title: "Cisco firewall configuration file"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Cisco-firewall-configuration-file"
---

This topic introduces how to configure the local IPsec connection profile when the user's local VPN gateway uses a Cisco firewall.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Configuration profiles may vary among different models from the same vendor. This topic is only an example. Please consult the firewall vendor for specific details. The pre\-shared keys used in this topic are for illustrative purposes only. In actual operations, configure more secure pre\-shared keys.</div>


&nbsp;

<span id=".5LqR5LiKSVBzZWPov57mjqXphY3nva7lj4LmlbA="></span>
## Cloud IPsec\-VPN connection configuration parameters


* Pre\-Shared Key: test@1234

* Routing mode: Protected Data Flows

* Local Network: `1.1.1.1/32`, `172.1.1.1/32`

* Remote Network: `2.2.2.2/32`, `3.3.3.3/32`, `4.4.4.4/32`

* IKE configuration

   
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
   

* IPsec configuration

   
   |Strategy |Value |
   |---|---|
   |Authentication algorithm |md5 |
   |Encryption algorithm |aes192 |
   |DH algorithm |group1 |
   |Lifecycle |3600 |
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This is the cloud configuration: Local refers to the cloud VPN, and Remote refers to the user's on\-premises VPN. In the configuration file, it is reversed: Local refers to the user's on\-premises VPN side, and Remote refers to the cloud VPN side.</div>


<span id=".6YWN572u5paH5Lu2"></span>
## Configuration file

<span id=".Y3Ny54mI5pys"></span>
### csr version

```Plain Text
crypto ikev2 proposal ikev2proposal  #IKE version
encryption aes  #Encryption algorithm
integrity md5  #Authentication algorithm
group 1  #DH algorithm
lifetime 86400 #Lifecycle in Phase 1 negotiation


crypto ikev2 policy ikev2policy
proposal ikev2proposal


crypto ikev2 keyring keys  #Configure key
peer strongswan
address 119.XX.XX.94  #Identifier of Cloud VPN gateway
pre-shared-key local test@1234  #Pre-shared key of local IPsec-VPN connection
pre-shared-key remote test@1234  #Pre-shared key of Cloud IPsec-VPN connection


crypto ikev2 profile ikev2profile
identity local address 180.XX.XX.137   #Identifier of customer gateway
match identity remote address 119.XX.XX.94    #Identifier of Cloud VPN gateway (119.XX.XX.94)
authentication remote pre-share
authentication local pre-share
keyring local keys


crypto ipsec transform-set vsr esp-aes esp-md5-hmac


#User-side policy entries require a one-to-one match between the local CIDR blocks and the cloud CIDR blocks
access-list 101 permit ip 2.2.2.2 0.0.0.0 1.1.1.1 0.0.0.0
access-list 101 permit ip 2.2.2.2 0.0.0.0 172.1.1.1 0.0.0.0
access-list 101 permit ip 3.3.3.3 0.0.0.0 1.1.1.1 0.0.0.0
access-list 101 permit ip 3.3.3.3 0.0.0.0 172.1.1.1 0.0.0.0
access-list 101 permit ip 4.4.4.4 0.0.0.0 1.1.1.1 0.0.0.0
access-list 101 permit ip 4.4.4.4 0.0.0.0 172.1.1.1 0.0.0.0




crypto map cmap 10 ipsec-isakmp
set peer 119.XX.XX.94  #Identifier of Cloud VPN gateway
set transform-set TS
set ikev2 -profile ikev2profile
match address 101 
set pfs group1  #Configure the DH key exchange algorithm for the IPsec Policy



set security-association lifetime seconds 3600  #IPsec SA lifecycle (s)



interface myport1
ip address 180.XX.XX 255.255.255.0 #IP address of user's on-permises VPN gateway
crypto map cmap




#Configure local entries (local firewall to Cloud)
ip route 172.1.1.1 255.255.255.255 119.91.131.94
ip route 1.1.1.1 255.255.255.255 119.91.131.94


```


<span id=".aW9z54mI5pys"></span>
### ios version

```Plain Text
 VPC utilizes unique identifiers to manipulate the configuration of
 a VPN Connection. Each VPN Connection is assigned an identifier and is
 associated with Virtual Private Gateway Identifier and User Gateway IP.

 Your VPN Connection ID : 37315   #IPsec-VPN connection ID for user's local firewall
 Your Virtual Private Gateway ID : 23850   #VPN gateway ID for user's local firewall
 Your User Gateway IP : 180.XX.XX.137   #IP of user's on-permises gateway, corresponding to Remote ID configured in the IPsec-VPN connection on the console

 To configure an IKE-based IPsec tunnel, perform the following tasks:

 #1: Internet Key Exchange (IKE) Configuration #IKE configuration

 A policy is established for the supported ISAKMP encryption,
 authentication, Diffie-Hellman and key parameters. 

 An IKE proposal defines a set of attributes describing how IKE negotiation in
 phase 1 should take place.
 By default, there is an IKE proposal that is used as the default IKE proposal.
 The default IKE proposal parameters are as follows:
 Authentication Encryption Diffie-Hellman Duration
 algorithm algorithm group (seconds)
 --------------------------------------------------------
 SHA DES Group 1 86400

crypto isakmp policy 1
authentication pre-share
encryption esp-aes 192   #Encryption algorithm
hash esp-md5-hmac   #Authentication algorithm
group 1    #DH algorithm
lifetime 86400   #IPsec SA lifecycle (s)


 The ISAKMP keyring stores the pre-shared key used to authenticate the
 tunnel endpoints.

crypto keyring 1
pre-shared-key address 119.XX.XX.94 key test@1234  #Identifier and pre-shared key of Cloud VPN gateway


 An ISAKMP profile is used to associate the keyring with a particular
 endpoint. IKE negotiation mode for phase 1 uses Main mode.   #Negotiation mode: main, aggressive
 Uses the IP address of the user gateway as the local ID. Uses the WAN IP
 address of the VPN gateway as the remote ID.

crypto isakmp profile 1
keyring 1
self-identity address 180.XX.XX.137  #Identifier of User's on-permises VPN gateway

match identity address 119.XX.XX.94  #Identifier of Cloud VPN gateway



no initiate mode




 #2: IPsec Configuration
 
 By default, the time-based IPsec SA lifetime is 3600 seconds.

 The IPsec transform set defines the encryption, authentication, and IPsec
 mode parameters. IP packets are encapsulated in tunnel mode.

crypto ipsec transform-set vsr esp-aes 192 esp-md5-hmac #IPsec encryption and authentication algorithms


 IPsec uses access lists to identify the traffic to be protected. Configure
 the access list to identify data flows.



#Policy entries require a one-to-one match between the local CIDR blocks and the cloud CIDR blocks.
access-list 101 permit ip 2.2.2.2 0.0.0.0 1.1.1.1 0.0.0.0
access-list 101 permit ip 2.2.2.2 0.0.0.0 172.1.1.1 0.0.0.0
access-list 101 permit ip 3.3.3.3 0.0.0.0 1.1.1.1 0.0.0.0
access-list 101 permit ip 3.3.3.3 0.0.0.0 172.1.1.1 0.0.0.0
access-list 101 permit ip 4.4.4.4 0.0.0.0 1.1.1.1 0.0.0.0
access-list 101 permit ip 4.4.4.4 0.0.0.0 172.1.1.1 0.0.0.0



 ACL for VPN connection probe



 The IPsec crypto map references the IPsec transform set, the ISAKMP profile
 and the access list. The PFS feature is disabled for the IPsec crypto map.

crypto map 1 1 ipsec-isakmp
set peer 119.XX.XX.94  #IPsec peer
set transform-set vsr
set isakmp-profile 1
match address 101


set pfs group1  #DH algorithm for IPsec phase



set security-association lifetime seconds 3600 #Lifecycle (s)



 #3: Interface Configuration

 Apply the IPsec crypto map to an interface. All traffic routed to the
 interface will be encrypted and transmitted to the VPC. Traffic from the VPC
 will be received on this interface.

interface myporttest1
ip address 180.XX.XX.137 255.255.255.0  #Configure the user-side VPN gateway. All traffic routed to this gateway will be encrypted and transmitted to the cloud VPC. Traffic from the cloud VPC will be delivered to and received by this gateway.
crypto map 1


 #4: Routing Configuration 

 Configure static routing or a routing protocol for interconnections between the
 Virtual Private Gateway and your User Gateway.

ip route 172.1.1.1/32 119.XX.XX.94
ip route 1.1.1.1/32 119.XX.XX.94
```
