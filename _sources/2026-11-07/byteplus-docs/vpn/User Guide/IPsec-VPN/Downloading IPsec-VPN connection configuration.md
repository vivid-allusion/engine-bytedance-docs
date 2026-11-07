---
title: "Downloading IPsec-VPN connection configuration"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Downloading-IPsec-VPN-connection-configurations"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

After creating the IPsec\-VPN connection, you can directly download the IPsec\-VPN connection configuration file and save it to your local device for configuring the peer VPN gateway in special cases (for example, no local network environment).

<span id=".5pON5L2c6ZmQ5Yi2"></span>
## Limits

You cannot download configuration files for IPsec\-VPN connections in **Creating** or **Deleting ** status.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the VPN Connection console](https://console.byteplus.com/vpn/vpnConnect).

2. In the top menu bar, select the target project and region.

3. In the IPsec Config list, check the checkbox on the left for the IPsec Config you want to download the configuration file for.

4. Click **Download IPsec Config** at the bottom of the list.

5. In the interface that pops up on the right, click **Download**.

   The downloaded configuration file format example is as follows:

   ```Plain Text
   {
           "Local": "10.XX.XX.240",
           "Remote": "10.XX.XX.74",
           "LocalSubnet": "192.XX.XX.0/24,192.XX.XX.0/24",
           "RemoteSubnet": "172.XX.XX.0/24",
           "IkeConfig": {
               "version": "ikev1",
               "psk": "R0U17****",
               "dhGroup": "group2",
               "mode": "main",
               "encAlg": "aes",
               "authAlg": "sha1",
               "lifetime": 86400,
               "localId": "10.XX.XX.240",   
               "remoteId": "10.XX.XX.74"
               
           },
           "IpsecConfig": {
               "encAlg": "aes",
               "authAlg": "sha1",
               "lifetime": 86400,
               "dhGroup": "group2"
           },
           "natTraversal": false,
           "dpdAction": "clear",
           "negotiateInstantly": false,
           "LogEnabled": false
       }
         
   } 
   ```
   

   
   |**Parameter** |**Description** |
   |---|---|
   |Local |The local VPN gateway egress IP address. |
   |Remote |The egress IP address of the peer VPN gateway. |
   |LocalSubnet |The local subnet. |
   |RemoteSubnet |Remote Subnet. |
   |IkeConfig |IKE Config, including LocalId, RemoteId, Version, Mode, EncAlg, AuthAlg, Lifetime, DhGroup, and Psk. |
   |version |The version of the IKE protocol. |
   |psk |The Pre\-Shared Key for identity authentication between the VPN gateway and the customer gateway in Phase 1. |
   |dhGroup |The DH key exchange algorithm for Phase 1 negotiation. |
   |mode |The negotiation mode for Phase 1. |
   |encAlg |The encryption algorithm for Phase 1 negotiation. |
   |authAlg |The authentication algorithm for Phase 1 negotiation. |
   |lifetime |The SA lifetime for Phase 1 negotiation. When the lifetime expires, a renegotiation is initiated. |
   |localId |The identifier of the VPN gateway for Phase 1 negotiation. |
   |remoteId |The identifier of the customer gateway for Phase 1 negotiation. |
   |IpsecConfig |IPsec Config includes DhGroup, EncAlg, AuthAlg, Lifetime. |
   |encAlg |The encryption algorithm for Phase 2 negotiation. |
   |authAlg |The authentication algorithm for Phase 2 negotiation. |
   |lifetime |The SA lifetime for Phase 2 negotiation. When the lifetime expires, a renegotiation is initiated. |
   |dhGroup |The DH key exchange algorithm for Phase 2 negotiation. |
   |natTraversal |NAT traversal feature.<br><br><br>* true: NAT traversal is enabled.<br><br>* false: NAT traversal is not enabled. |
   |dpdAction |DPD feature.<br><br><br>* clear: DPD enabled. After DPD timeout, the IPsec VPN tunnel is cleared.<br><br>* false: DPD not enabled.<br><br>* hold: DPD enabled. After DPD timeout, the tunnel remains unchanged until new data enters the tunnel, then attempts reconnection.<br><br>* restart: DPD is enabled. Reconnect immediately after DPD timeout.<br><br>* none: DPD is not enabled. |
   |negotiateInstantly |Negotiate instantly after IPsec\-VPN connection configuration completes.<br><br><br>* true: The system proactively negotiates instantly upon the completion of IPsec\-VPN connection configuration.<br><br>* false: The system does not initiate negotiation after the IPsec\-VPN connection configuration completes. Negotiation is triggered passively when traffic passes through. |
   |LogEnabled |The status of the IPsec\-VPN connection.<br><br><br>* true: Enabled.<br><br>* false: Disabled. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In Protected Data Flows mode, <code>localId</code> and <code>remoteId</code> may be in the form of a domain name.   </div>
