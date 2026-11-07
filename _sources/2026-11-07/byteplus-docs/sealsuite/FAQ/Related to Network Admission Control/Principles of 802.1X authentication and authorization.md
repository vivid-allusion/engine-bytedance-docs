---
title: "Principles of 802.1X authentication and authorization"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/8021x-authentication-and-authorization"
---

SealSuite verifies employee identity when employees access Wi\-Fi and wired networks through 802.1X, and delivers the corresponding permissions to network devices. This article introduces the protocols involved in authentication, packet interaction flow, authorization rule matching, and common RADIUS attributes. It helps you understand the authentication process together with packet capture results.

## Basic concepts

IEEE 802.1X is a port\-based network access control standard that works at the data link layer. SealSuite uses this protocol to verify employee identity when employees access Wi\-Fi or wired networks.

802.1X uses controlled ports and uncontrolled ports to separate service traffic from authentication traffic. Both are logical ports that share the same physical link:

* **Uncontrolled port**: Always remains open bidirectionally and allows only EAPOL (EAP over LAN) authentication\-related packets to pass. It does not block authentication interaction traffic at any point, ensuring that an endpoint can complete the full identity negotiation process with the authenticator before authentication is complete.

* **Controlled port**: Initially stays in the **unauthorized state** and restricts service data packets. It switches to the **authorized state** only after the endpoint completes identity authentication and passes verification. Then it opens normal network access and can also apply granular control policies delivered by the authentication server.

After authentication succeeds, the network device can apply authorization policies delivered by the authentication server, such as dynamic VLAN, ACL, and session duration.

802.1X provides two port control modes for different access scenarios. Confirm the default control mode with each network vendor:

* **Port\-based control mode**: After a single endpoint connected to the port is authenticated successfully, all endpoints connected to this physical port can obtain network access. This mode applies to high\-security wired scenarios where only one endpoint connects to the port.

* **MAC\-based control mode**: Each endpoint connected to the port must complete identity authentication independently, and permissions do not affect each other. This is the mainstream mode for wireless LANs and scenarios where multiple endpoints connect to one port.

### EAP

Defined by RFC 3748, EAP is the authentication core of 802.1X. It is a general authentication framework and is not bound to a specific authentication algorithm. It supports flexible extension of authentication methods to adapt to access scenarios with different security levels. Core packet types include:

* EAP\-Request: An identity or verification request packet initiated by the authenticator.

* EAP\-Response: An authentication response packet returned by the supplicant.

* EAP\-Success: A notification packet indicating final authentication success.

* EAP\-Failure: A notification packet indicating final authentication failure.

### EAPOL

Defined by the IEEE 802.1X standard, EAPOL is the dedicated encapsulation protocol for EAP over Layer 2 LAN links. Its Ethernet type is `0x888E`. It transfers authentication\-related packets between the endpoint and the authenticator. Core frame types include:

* EAPOL\-Start: A trigger packet in which the endpoint actively initiates authentication.

* EAPOL\-Packet: The main frame that carries core EAP authentication packets.

* EAPOL\-Logoff: A request packet in which the endpoint actively goes offline.

* EAPOL\-Key: A key negotiation packet in wireless LAN scenarios.

### EAP over RADIUS

EAP over RADIUS transfers EAP packets between network devices and authentication servers. For the related encapsulation rules, see RFC 3579. RADIUS authentication, authorization, and accounting are defined by RFC 2865 and RFC 2866. Core characteristics include:

* Based on UDP transport. SealSuite uses **wireless 802.1X authentication port 1812 and accounting port 1813** by default, and **wired 802.1X authentication port 2812 and accounting port 2813** by default.

* Encapsulates complete EAP packets through the `EAP-Message` attribute, enabling end\-to\-end transparent transmission of EAP between the authenticator and the authentication server (EAP over RADIUS).

* Natively supports integrated authentication, authorization, and accounting to complete authentication, authorization, and accounting for Network Access Control (NAC).

Account\-based network access uses EAP\-PEAP: a TLS encrypted tunnel is first established through the server certificate, and user identity authentication is then completed inside the tunnel. The following sections use account authentication for employee Wi\-Fi and wired networks as examples.

## Authentication flow

The following section uses endpoint\-initiated EAP\-PEAP authentication as an example to describe interactions between components. The network device forwards authentication packets between the endpoint and the RADIUS server through EAP relay. The following table describes the roles and responsibilities involved in authentication.

|Role |Function |Core responsibilities |
|---|---|---|
|endpoint device (Supplicant) |Authentication requester |802.1X client. Initiates authentication, processes EAP packets, and completes the TLS handshake and MSCHAPv2 authentication. |
|Network device (Authenticator) |Authentication relay |In the EAP relay mode used in this example, the switch or wireless access device encapsulates and forwards packets between EAPOL and RADIUS. After authentication succeeds, it controls endpoint access based on the delivered authorization information. |
|RADIUS server |Authentication server |EAP authentication termination point. Processes the TLS tunnel and MSCHAPv2 authentication logic, and connects to the identity source. |
|SealSuite server |Identity source / authorization source |Stores keys, passwords, and permission information for endpoints and users, and provides identity data and audit capabilities required for authentication. |

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/review-20261021/8021x-flow-en.png)

The overall interaction process includes 4 core stages:

### Stage 1: Start authentication and identify the Endpoint

After the endpoint initiates authentication, the network device queries the endpoint identity and forwards EAP packets to the RADIUS server to prepare identity information for establishing the PEAP tunnel. The following table lists the interaction steps for starting authentication, transferring identity information, and initiating TLS negotiation in order.

|No. |Packet direction |Packet name |Detailed purpose and protocol description |
|---|---|---|---|
|1 |endpoint → network device |EAPOL\-Start |The trigger packet for 802.1X authentication. Based on the EAPOL Layer 2 protocol, the endpoint actively initiates an authentication request to the network device and notifies the authenticator to start the access process. |
|2 |Network device → endpoint |EAP\-Request(Identity) |After receiving the start request, the network device initiates an identity query to the endpoint according to the EAP standard.<br><br>Protocol: EAPOL encapsulates the EAP packet. EAP Code=1 (Request), Type=1 (Identity), requiring the endpoint to provide an identity. |
|3 |endpoint → network device |EAP\-Response(Identity) |The endpoint responds to the identity request. The packet carries its identity, such as hostname, MAC address, or username.<br><br>Protocol: EAPOL encapsulates the EAP packet. EAP Code=2 (Response), Type=1 (Identity). |
|4 |Network device → RADIUS server |Access\-Request |As a RADIUS client, the network device encapsulates the endpoint's EAP\-Response packet into the RADIUS EAP\-Message attribute. It also carries the NAS device identifier and port information, then sends the packet to the RADIUS server to complete EAP\-to\-RADIUS relay.<br><br>Protocol: RADIUS, packet Code=1 (Access\-Request). |
|5 |RADIUS server → SealSuite server |Client Query |The RADIUS server extracts network device information from the packet and initiates a query to the SealSuite server over HTTP/HTTPS to verify the network device information.<br><br>When HTTPS is used, this interaction is encrypted. |
|6 |SealSuite server → RADIUS server |Client Info(Secret) |The SealSuite server returns the query result, and the RADIUS server completes preparation before authentication.<br><br>When HTTPS is used, this interaction is encrypted. |
|7 |RADIUS server → network device |Access\-Challenge(tls\-start) |The RADIUS server starts the PEAP process and returns a RADIUS challenge packet to the network device. The packet encapsulates EAP\-Request(TLS Start) and notifies the endpoint to start establishing the PEAP outer TLS tunnel.<br><br>Protocol: RADIUS, Code=11 (Access\-Challenge), carrying an EAP\-Message that encapsulates the TLS start instruction. |
|8 |Network device → endpoint |EAP\-Request(tls\-start) |The network device decapsulates the EAP packet from the RADIUS packet and sends it to the endpoint through EAPOL, notifying the endpoint to start the PEAP TLS handshake process.<br><br>Protocol: EAPOL encapsulates the EAP packet. EAP Code=1 (Request), Type=25 (PEAP). |

### Stage 2: Establish the PEAP outer TLS tunnel

This stage first establishes the PEAP outer TLS encrypted tunnel, and then performs user identity authentication inside the tunnel. The endpoint confirms the server identity by verifying the server certificate. The following table uses TLS 1.2 as an example to describe version and cipher suite negotiation, certificate verification, key exchange, and handshake confirmation. Actual handshake messages depend on the negotiated cipher suite.

|No. |Packet direction |Packet name |Detailed purpose and protocol description |
|---|---|---|---|
|9 |endpoint → network device |EAP\-Response(Client Hello) |After receiving the TLS start instruction, the endpoint initiates the first step of the TLS handshake and generates a Client Hello packet. The packet carries core parameters such as the TLS versions supported by the endpoint, cipher suite list, client random number (Client Random), and session ID.<br><br>Protocol: EAPOL encapsulates the EAP packet. EAP Code=2 (Response), Type=25 (PEAP), and the data segment is TLS Client Hello. |
|10 |Network device → RADIUS server |Access\-Request |The network device encapsulates the EAP packet that contains Client Hello into a RADIUS Access\-Request and continues relay forwarding.<br><br>Protocol: RADIUS, Code=1, carrying the EAP\-Message attribute. |
|11 |RADIUS server → network device |Access\-Challenge(tls\-handshake) |The RADIUS server processes Client Hello, generates TLS server handshake packets, and encapsulates them into a RADIUS challenge packet. The following lists the related contents in a TLS 1.2 handshake. Specific messages depend on the negotiated cipher suite:<br><br><br>1. Server Hello: Confirms the TLS version and cipher suite, and generates the server random number (Server Random).<br><br>2. Server digital certificate: The X.509 certificate of the RADIUS server, used by the endpoint to verify the server identity.<br><br>3. Server Key Exchange (when applicable): Server key exchange parameters used for premaster secret negotiation.<br><br>4. Server Hello Done: Notifies the endpoint that the server has finished sending initial handshake packets.<br><br>   Protocol: RADIUS, Code=11. |
|12 |Network device → endpoint |Server Hello&Cert&Server Key Exchange&Server Hello Done |After decapsulation, the network device sends TLS server packets to the endpoint through EAPOL. After receiving the packets, the endpoint first verifies the validity of the server certificate, including the CA trust chain, validity period, and domain name match. After certificate verification succeeds, it extracts the server public key and key exchange parameters.<br><br>Protocol: EAPOL encapsulates the PEAP EAP packet. |
|13 |endpoint → network device |Client Key Exchange, Change Cipher Spec, Finished |After verifying the server certificate, the endpoint participates in key exchange through Client Key Exchange, and then sends Change Cipher Spec and Finished. The key exchange content depends on the negotiated cipher suite. Finished is used to verify the handshake process. Protocol: EAPOL encapsulates the PEAP EAP packet. |
|14 |Network device → RADIUS server |Access\-Request |The network device encapsulates the endpoint's TLS response packet into a RADIUS Access\-Request and forwards it to the RADIUS server.<br><br>Protocol: RADIUS, Code=1. |
|15 |RADIUS server → network device |Access\-Challenge |The RADIUS server processes and verifies the endpoint's TLS handshake message, and returns the server's Change Cipher Spec and Finished through Access\-Challenge. Protocol: RADIUS, Code=11. |
|16 |Network device → endpoint |Change Cipher Spec, Finished |The network device forwards the server's TLS message to the endpoint. After both parties exchange and verify Finished messages, the TLS handshake is complete. Subsequent inner identity authentication is performed in the encrypted tunnel. |
|17 |endpoint → network device |EAP\-Response(ack) |The endpoint sends a PEAP response and continues subsequent authentication interactions. Protocol: EAPOL encapsulates the EAP packet. |
|18 |Network device → RADIUS server |Access\-Request |The network device encapsulates the endpoint's PEAP response into a RADIUS Access\-Request and forwards it to continue subsequent authentication interactions.<br><br>Protocol: RADIUS, Code=1. |

### Stage 3: Verify user identity inside the TLS tunnel

After the TLS tunnel is established, the endpoint and the RADIUS server perform inner identity authentication through EAP\-MSCHAPv2. They use challenge\-response verification and do not directly transmit the user password. The following table describes the interaction sequence for identity query, challenge response, result verification, and reporting.

|No. |Packet direction |Packet name |Detailed purpose and protocol description |
|---|---|---|---|
|19 |RADIUS server → network device |Access\-Challenge |Inside the encrypted tunnel, the RADIUS server initiates another EAP identity request and encapsulates it into a RADIUS challenge packet.<br><br>Protocol: RADIUS, Code=11. EAP\-Message is the encrypted EAP\-Request (Identity). |
|20 |Network device → endpoint |EAP\-Request(Identity) |After decapsulation, the network device sends the encrypted identity request to the endpoint. The endpoint decrypts the request inside the TLS tunnel.<br><br>Protocol: The inner EAP packet with Type=1 (Identity) is carried inside the TLS tunnel, and the outer layer is transmitted through EAPOL. |
|21 |endpoint → network device |EAP\-Response(Identity) |The endpoint responds to the identity request inside the encrypted tunnel and carries the user's username identifier. The entire process is encrypted to prevent identity leakage.<br><br>Protocol: The inner EAP packet with Type=1 (Identity) is carried inside the TLS tunnel, and the outer layer is transmitted through EAPOL. |
|22 |Network device → RADIUS server |Access\-Request |The network device encapsulates the encrypted identity response into a RADIUS Access\-Request and forwards it.<br><br>Protocol: RADIUS, Code=1. |
|23 |RADIUS server → network device |Access\-Challenge |After decrypting and obtaining the username, the RADIUS server initiates an MSCHAPv2 challenge. It generates a 16\-byte server random challenge, encapsulates it as an EAP\-MSCHAPV2_CHALLENGE packet, and places it in the RADIUS challenge packet.<br><br>Protocol: RADIUS, Code=11. EAP\-Message is the encrypted EAP\-MSCHAPv2 challenge packet. |
|24 |Network device → endpoint |EAP_MSCHAPV2_CHALLENGE |After decapsulation, the network device sends the challenge packet to the endpoint. The endpoint decrypts it inside the tunnel and obtains the server challenge.<br><br>Protocol: The inner EAP packet with Type=26 (EAP\-MSCHAPv2) is carried inside the TLS tunnel, and the outer layer is transmitted through EAPOL. |
|25 |endpoint → network device |EAP_MSCHAPV2_RESPONSE |After receiving the challenge, the endpoint performs the core MSCHAPv2 calculation:<br><br><br>1. Generates a 16\-byte client random number (Peer Challenge).<br><br>2. Combines the username, user password hash, server challenge, and client random number to generate a 24\-byte NT\-Response hash.<br><br>3. Encapsulates the random number and response value into the response packet and sends it, without directly transmitting the user password.<br><br>   Protocol: The inner EAP packet with Type=26 (EAP\-MSCHAPv2) is carried inside the TLS tunnel, and the outer layer is transmitted through EAPOL. |
|26 |Network device → RADIUS server |Access\-Request |The network device encapsulates the MSCHAPv2 response packet into a RADIUS Access\-Request and forwards it.<br><br>Protocol: RADIUS, Code=1.<br><br>Inner authentication content is transmitted encrypted in the TLS tunnel. |
|27 |RADIUS server → SealSuite server |User Query |The RADIUS server decrypts and obtains the username and MSCHAPv2 response, then initiates a user query to the SealSuite server over HTTP/HTTPS to obtain the user's password hash and access permission information.<br><br>When HTTPS is used, this interaction is encrypted. |
|28 |SealSuite server → RADIUS server |User Info(Password&Permission) |The SealSuite server returns the user's NT password hash and access authorization policies, such as VLAN and ACL. The RADIUS server uses them to verify the validity of the MSCHAPv2 response.<br><br>When HTTPS is used, this interaction is encrypted. |
|29 |RADIUS server → network device |Access\-Challenge |The RADIUS server completes authentication verification. There are two scenarios:<br><br>Authentication success: The server uses the user password hash and challenge parameters to calculate the expected NT\-Response and compares it with the endpoint response. After verification succeeds, it returns the success result and the server authentication response for the endpoint to verify.<br><br>Authentication failure: If response verification fails, the server returns an inner authentication failure result and informs the endpoint of the failure reason.<br><br>Protocol: RADIUS, Code=11.<br><br>Inner authentication content is transmitted encrypted in the TLS tunnel. |
|30 |Network device → endpoint |Authentication success or failure result inside the tunnel |After decapsulation, the network device sends the authentication result packet to the endpoint. The endpoint decrypts it inside the tunnel: Authentication failure: The endpoint receives the failure notification and ends the authentication process. Authentication success: The endpoint verifies the server authentication response, confirms that the server identity is valid, and completes mutual authentication.<br><br>Protocol: EAPOL encapsulates the EAP\-MSCHAPv2 packet, with TLS encryption. |
|31 |endpoint → network device |endpoint response to the inner authentication result |The endpoint responds to the server with the authentication result:<br><br>Authentication failure: The endpoint processes the failure notification according to the inner authentication method. The authenticator notifies the endpoint of final authentication failure through EAP\-Failure.<br><br>Authentication success: The endpoint confirms the inner authentication result and continues to complete PEAP authentication.<br><br>Protocol: EAPOL encapsulates the EAP packet, with TLS encryption. |
|32 |Network device → RADIUS server |Access\-Request |The network device encapsulates the endpoint's final response into a RADIUS packet and forwards it:<br><br><br>1. Authentication failure: Encapsulates it into Access\-Request, and the RADIUS server finally returns Access\-Reject.<br><br>2. Authentication success: Encapsulates it into Access\-Request and enters the authorization process.<br><br>   Inner authentication content is transmitted encrypted in the TLS tunnel. |
|33 |RADIUS server → SealSuite server |Connect Report |The RADIUS server reports the authentication result, endpoint information, failure reason, and more to the SealSuite server, and the SealSuite server records audit logs.<br><br>When HTTPS is used, this interaction is encrypted. |

### Stage 4: Deliver permissions and report accounting information

After authentication succeeds, the RADIUS server delivers permissions to the network device. The network device allows the endpoint to access the network and reports accounting information. The following table describes the authorization process and the accounting session startup process. If authentication fails, the authenticator returns `EAP-Failure`, and the network device denies the network access attempt.

|No. |Packet direction |Packet name |Detailed purpose and protocol description |
|---|---|---|---|
|34 |RADIUS server → SealSuite server |User Approved |The RADIUS server confirms the user's final authorization policy with the SealSuite server, and the SealSuite server returns access permission rules.<br><br>When HTTPS is used, this interaction is encrypted. |
|35 |RADIUS server → network device |Access\-Accept with Authorization |The RADIUS server returns an authentication success packet to the network device. The packet includes:<br><br><br>1. The encapsulated EAP\-Success packet. 2. RADIUS authorization attributes: Tunnel\-Private\-Group\-ID (assigned VLAN), Filter\-ID (ACL rule), and more. The packet instructs the network device to allow the authenticated user to access the network and apply the corresponding authorization policy.<br><br>   Protocol: RADIUS, Code=2 (Access\-Accept). |
|36 |Network device → endpoint |EAP\-Success |The network device decapsulates the EAP\-Success packet and sends it to the endpoint through EAPOL, notifying the endpoint that 802.1X PEAP authentication is complete and normal network access is available. Protocol: EAPOL encapsulates the EAP packet, Code=3 (Success). |
|37 |Network device → RADIUS server |Accounting\-Request |After the user successfully accesses the network, the network device sends an accounting start request to the RADIUS server. The request carries information such as username, session ID, access time, and endpoint IP address, and starts the accounting session.<br><br>Protocol: RADIUS, Code=4 (Accounting\-Request), Acct\-Status\-Type=Start. |
|38 |RADIUS server → SealSuite server |User Accounting |The RADIUS server reports the user's access accounting and session information to the SealSuite server for audit, reports, and session management.<br><br>When HTTPS is used, this interaction is encrypted. |
|39 |RADIUS server → network device |Accounting\-Response |The RADIUS server confirms the accounting session and returns an accounting response packet. The network device subsequently sends periodic accounting update packets and sends an accounting termination packet when the user goes offline, completing full lifecycle management.<br><br>Protocol: RADIUS, Code=5 (Accounting\-Response). |

## Authorization matching and permission delivery

SealSuite matches authorization rules based on RADIUS request packets and the EAP authentication process. A request must meet all conditions configured in a rule before the corresponding permission group is delivered.

### Permission types

* Employee Wi\-Fi: Distinguished by destination port 1812 in RADIUS packets

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/8021x-principles-20261009/802-migration-1.png)

* Employee wired network: Distinguished by destination port 2812 in RADIUS packets

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/8021x-principles-20261009/802-migration-2.png)

### Authentication method

SealSuite account authentication uses `EAP-PEAP`, which corresponds to the authorization rule for account\-based network access.

### Applicable entities

* Employee authorization (department, role): View the permissions of the user in the IAM module based on user information in the Identity field exchanged in EAP packets

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/8021x-principles-20261009/802-migration-3.png)

* Device authorization (device, group): Match device ID information based on the endpoint MAC address in Calling\-Station\-Id. **Mobile Endpoints may fail to provide MAC addresses, or clients may enable random MAC addresses. In these cases, device IDs cannot be matched by MAC address and permissions cannot be obtained. Use the IP address (Framed\-IP\-Address) reported through RADIUS accounting for permission matching and updates.**

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/8021x-principles-20261009/802-migration-4.png)

### Advanced configuration

* RADIUS server: The RADIUS server that receives RADIUS authentication request packets

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/8021x-principles-20261009/802-migration-5.png)

* Network device: The network device matched based on the source IP address in RADIUS authentication request packets

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/8021x-principles-20261009/802-migration-6.png)

* SSID: The SSID obtained based on the Called\-Station\-Id field in RADIUS authentication request packets. This field is the NAS device identifier, usually device MAC address + SSID in wireless scenarios

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/8021x-principles-20261009/802-migration-7.png)

* RADIUS attribute: Performs access matching based on configured RADIUS attribute values. The corresponding permission group is delivered only when user attributes meet the configured conditions. If multiple attribute values are configured, all conditions must be met for the rule to take effect.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/8021x-principles-20261009/802-migration-8.png)

### Permission group policy

After authentication succeeds, SealSuite delivers permissions to the network device through an Access\-Accept packet:

* Network\-based: Tunnel\-Pvt\-Group\-ID Usually corresponds to the VLAN ID on the network device. Enter a number only, such as 123.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/8021x-principles-20261009/802-migration-9.png)

* Role\-based: Filter\-ID Usually corresponds to a preset role, user group, or ACL on the network device. Enter a combination of letters and numbers, such as Dev1. If you enter numbers only, it can correspond to an ACL ID.

* Custom: Delivers custom RADIUS AVP attribute values for special scenarios.

After authorization is complete and the delivered permissions meet expectations, issues such as DHCP failing to obtain an IP address, network access failure, slow access, or packet loss require troubleshooting on the network side. Contact the network vendor for assistance.

## RADIUS attributes

RADIUS transfers user identity, permission policies, accounting data, and security verification information through attribute\-value pairs (AVPs). When viewing packets, you can identify authentication requests, authorization results, and session status based on attribute names and values.

RADIUS attributes defined by RFC 2865 use the TLV (Type\-Length\-Value) structure and consist of three fields: type, length, and value. A single attribute can be up to 255 bytes. The following table describes each field.

|Field |Length |Specification definition and description |
|---|---|---|
|Type |1 byte |Identifies the attribute type. Vendor\-Specific uses Type 26. |
|Length |1 byte |The total byte length of the attribute, including Type, Length, and Value. The maximum is 255 bytes. EAP\-Message can carry longer EAP packets through multiple attributes. |
|Value |Variable length (maximum 253 bytes) |The specific service data of the attribute. Its format is defined by the attribute type, such as string, integer, address, or binary data. |

Common RADIUS attributes include standard attributes and vendor\-specific attributes (VSAs):

* Standard IANA attributes: Uniformly defined by the IETF through RFC specifications and assigned Type numbers by IANA. They are commonly supported by mainstream network devices and RADIUS servers and provide the basic functions of the RADIUS protocol.

* Vendor\-Specific Attribute (VSA): Corresponds to Type=26. It is an extension attribute specifically defined in RFC 2865 to address vendor\-specific requirements that standard attributes cannot cover, such as proprietary permission policies, customized accounting, and device\-specific features. It is the most common extension capability in enterprise Network Access Control (NAC) and wireless access scenarios.

### Authentication request attributes

Attributes in authentication requests identify users, endpoints, and network devices. The following table lists common attributes and their functions, and distinguishes PAP, CHAP, and PEAP scenarios to help you determine field purposes when viewing `Access-Request`.

|Attribute number |Attribute name |Core function |802.1X scenario description |
|---|---|---|---|
|1 |User\-Name |Identifies the user or endpoint to be authenticated. Supports formats such as "username@domain" and "endpoint MAC address". |When the network device receives EAP\-Response/Identity, it puts the identity information into the User\-Name attribute for processing by the RADIUS server. |
|2 |User\-Password |Encapsulates the user password for PAP authentication. It is encrypted with the RADIUS shared secret and is not plaintext. |Used only for PAP authentication. This attribute is not used in PEAP\-MSCHAPv2 scenarios. |
|3 |CHAP\-Password |Encapsulates the hash response value for CHAP authentication to prevent password transmission over the network. |Used in CHAP authentication scenarios. MSCHAPv2 inside the PEAP tunnel does not directly use this attribute. |
|4 |NAS\-IP\-Address |The IP address of the network device, such as switch or AP, that initiates the authentication request. The device is the NAS. |Used to identify the NAS device. For the basis of network device matching in SealSuite, see "Authorization matching and permission delivery". |
|5 |NAS\-Port |The physical port number of the NAS device accessed by the endpoint. It can carry information such as slot and VLAN. |Used to identify the physical access location of the endpoint and enforce port\-level access control. |
|30 |Called\-Station\-Id |The identifier of the NAS device, usually device MAC address + SSID in wireless scenarios. |Used to identify the AP and SSID for wireless access. |
|31 |Calling\-Station\-Id |Carries the MAC address used by the endpoint for this access, allowing the server to identify and match the endpoint. |A core attribute in 802.1X scenarios, used for endpoint identity verification and MAC allowlist access. |

### EAP authentication attributes

EAP over RADIUS carries EAP packets through `EAP-Message` and verifies packet integrity through `Message-Authenticator`. The following table describes the roles of these two attributes in PEAP authentication.

|Attribute number |Attribute name |Core function |PEAP flow description |
|---|---|---|---|
|79 |EAP\-Message |Encapsulates EAP protocol packets and serves as the core carrier of EAP over RADIUS, as defined in RFC 3579. |All EAP packets in the full PEAP flow, including TLS handshake, MSCHAPv2 authentication, and EAP\-Success/Failure, are encapsulated and transmitted through this attribute. Oversized EAP packets are split into multiple fragments of this attribute. |
|80 |Message\-Authenticator |Used for integrity verification of RADIUS packets and generated based on the HMAC\-MD5 algorithm. |Access\-Request, Access\-Challenge, Access\-Accept, and Access\-Reject packets that contain EAP\-Message must include Message\-Authenticator and must be verified according to the specification. Packets with missing or failed verification must be discarded. |

### Authorization control attributes

After authentication succeeds, the RADIUS server returns authorization information to the network device through `Access-Accept`. The following table lists attributes related to service type, access control, VLAN assignment, and accounting update interval. Use them to check whether delivered results match the configuration.

|Attribute number |Attribute name |Core function |802.1X scenario description |
|---|---|---|---|
|6 |Service\-Type |Identifies the user's service type, such as Framed (2, Ethernet / PPP access) or Login (1, device management login). |Used to identify the access service type. |
|11 |Filter\-ID |Delivers the ACL access control rule name or number to control the endpoint's network access permissions. |Used to enforce granular access control based on users or endpoints, such as blocking access to high\-risk network segments or restricting internet access. |
|81 |Tunnel\-Private\-Group\-ID |Delivers the VLAN ID for endpoint access and implements dynamic VLAN assignment, as defined in RFC 2868. |The most common authorization attribute in 802.1X scenarios. After authentication succeeds, the endpoint port is automatically assigned to the specified VLAN, implementing network isolation for users with different permissions. |
|85 |Acct\-Interim\-Interval |Sets the sending interval for accounting update packets, in seconds. |Controls the NAS device to periodically report endpoint online status and traffic data, implementing real\-time session monitoring. |

### Accounting attributes

Accounting packets record the start, update, and end of endpoint sessions. The following table lists attributes such as session identifier, endpoint IP address, traffic, online duration, and offline reason. Use them to associate packets in the same session and view session status.

|Attribute number |Attribute name |Core function |Scenario description |
|---|---|---|---|
|8 |Framed\-IP\-Address |The public or private IPv4 address assigned to the endpoint. |Identifies the real endpoint IP address corresponding to the current accounting session, used for traffic tracing, online user locating, and abnormal access auditing. |
|40 |Acct\-Status\-Type |Accounting packet type. Core values include Start (session start), Interim\-Update (session update), and Stop (session end). |Identifies the service stage of an accounting packet. endpoint online, periodic update, and offline events correspond to these three packet types. |
|44 |Acct\-Session\-Id |The unique ID of the accounting session. Start/Update/Stop packets in the same session use the same ID. |Used to associate the complete access session of the endpoint and serves as the core identifier for audit and accounting reconciliation. |
|42 |Acct\-Input\-Octets |endpoint upstream traffic, in bytes. |Counts upstream traffic during endpoint access. |
|43 |Acct\-Output\-Octets |endpoint downstream traffic, in bytes. |Counts downstream traffic during endpoint access. |
|46 |Acct\-Session\-Time |endpoint online duration, in seconds. |Records the number of seconds that the session has lasted and can be reported in Stop and Interim\-Update accounting packets. |
|49 |Acct\-Terminate\-Cause |Session termination reason, such as user\-initiated offline, session timeout, port down, or authentication failure. |Used for troubleshooting and audit analysis to locate the root cause of endpoint disconnection. |
