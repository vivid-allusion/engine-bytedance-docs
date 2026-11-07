---
title: "Selecting Network Access Authentication Methods"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/selecting-network-access-authentication-methods"
---

When building an enterprise network access control system with SealSuite, selecting the appropriate authentication protocol is key to balancing security and user experience. SealSuite currently supports two mainstream network access control protocols: **802.1X authentication** and **Portal authentication**.

This document explains the working principles, architecture components, and applicable scenarios of the two protocols, helping you choose the best option based on your business requirements.

<span id="b3feb57f"></span>
## 802.1X Authentication

802.1X is a port\-based network access control standard widely used in enterprise wired office networks, such as switch access, and wireless office networks, such as Wi\-Fi access. Unlike scenarios where all employees share the same Wi\-Fi password or can access the network simply by plugging in a network cable, 802.1X requires each employee to use independent identity credentials for network access. Access permissions are centrally managed by the authentication server, enabling "one person, one credential" and traceable identities.

<span id="a57b911a"></span>
### Applicable Scenarios


* **Managed office computer access**: Company\-issued laptops that require long\-term, stable, and seamless intranet connectivity.

* **High security control requirements**: Core departments such as R&D and Finance, where identity verification is required and endpoint compliance checks, such as antivirus software running status, must be performed through the SealSuite client.

* **Dynamic network authorization**: Different VLAN or ACL permissions need to be automatically assigned during network access based on employee identity, such as department or role.


<span id="9b07440c"></span>
### Core Components and Roles

The SealSuite 802.1X architecture includes the following four core roles:


* **Endpoint device**: The employee’s office device. **The SealSuite client usually needs to be installed on the device**, except in manual configuration scenarios such as Windows AD domain authentication. The client is used to initiate EAP authentication requests, submit identity information, and perform environment security checks.

* **Network access device**: Network hardware that has access control capabilities and authentication enabled, such as a wired switch, wireless controller (AC), or wireless access point (AP). Before authentication succeeds, it intercepts all business traffic and acts as a relay to forward authentication information to the authentication server.

* **SealSuite RADIUS node**: The authentication access component of SealSuite. It is responsible for communicating with network access devices, processing identity verification requests, and returning authentication results to network access devices.

* **SealSuite Admin Console**: The control center of the system. It is responsible for storing user information, maintaining access policies, performing identity verification, and issuing the final access decision.


<span id="f63a3022"></span>
### Network Architecture and Data Flow

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/558b41deea8d487dbd3a414ea0f60f49~tplv-goo7wpa0wc-image.image) </span>

<span id="536b1324"></span>
### Workflow


1. **Connection and interception**: The endpoint device connects to the office Wi\-Fi or plugs in a wired network cable. The network access device detects the new connection. Before authentication succeeds, it only allows the endpoint to transmit authentication\-related traffic, such as EAP packets, and intercepts other business packets.

2. **Request forwarding**: The endpoint initiates a network access request through the SealSuite client. The network access device encapsulates the request into standard RADIUS packets and forwards it to the preconfigured SealSuite RADIUS node.

3. **Identity verification**: The SealSuite RADIUS node works with SealSuite Server to verify the validity of the user account, password, or certificate, and matches the corresponding access policy.

4. **Access decision delivery**: After verification is completed, SealSuite sends an Access\-Accept or Access\-Reject instruction to the network access device.

5. **Dynamic authorization**: While allowing access, SealSuite can dynamically instruct the network access device to assign the endpoint to the corresponding VLAN, or apply the corresponding ACL policy, based on the user’s role. This enables fine\-grained network isolation.


<span id="349a59f1"></span>
### Solution Advantages


* **Layer 2 physical interception**: Illegal traffic is intercepted at the data link layer, providing higher security than Portal authentication based on Layer 3 redirection.

* **Dynamic network switching (CoA)** : The system can perceive the security status of an endpoint in real time during runtime. Once a device becomes non\-compliant, it can be dynamically switched to an isolation VLAN without requiring disconnection and reconnection.

* **Automated network access**: When used with the SealSuite client, silent connection is supported, eliminating the need to manually configure complex parameters such as SSID, protocol, and certificates.


<span id="da5df37a"></span>
## Portal Authentication

Portal authentication, also known as Web authentication, is a clientless network access method. After a user connects to Wi\-Fi, traffic is intercepted by the network access device and redirected to an authentication web page, also known as the Portal page. The user can access the internet after completing identity verification on the web page.

<span id="68c686d5"></span>
### Applicable Scenarios


* **Visitor access**: External users such as partners and interview candidates do not need to install any software. They can connect and use the network immediately through QR code scanning or SMS verification codes.

* **Mobile office (BYOD)** : Employees use personal phones or tablets to connect to Wi\-Fi and access non\-core resources, where fast and convenient access is prioritized.

* **Temporary or special endpoint access**: Smart endpoints that cannot install a client but have browser capabilities, or temporary emergency internet access channels used when the client on an employee's computer fails.


<span id="d13471ae"></span>
### Core Components and Roles

The SealSuite Portal architecture mainly includes the following core roles:


* **Endpoint device**: The device used by an employee or visitor. The SealSuite client does not need to be installed. A standard web browser, such as a PC browser or mobile H5 browser, is sufficient.

* **Network access device**: Network hardware with HTTP redirection capabilities, such as a wireless controller (AC), wireless access point (AP), or wired switch. It intercepts user HTTP requests before authentication and forcibly redirects them to the authentication page. After receiving the final "authentication successful" instruction, it releases network permissions.

* **Portal module**: The component responsible for receiving identity credentials submitted from the endpoint web page and initiating an authentication handshake request to the network access device. Depending on the selected solution, it can be deployed in either of the following forms:

   * **Built into the network access device (corresponding to Solution 1)** : Integrated into the network access device (AC). The endpoint directly submits the credential form to the network access device, which then directly triggers subsequent RADIUS verification.

   * **Independently hosted by SealSuite (corresponding to Solution 2)** : SealSuite provides an independent protocol processing component in the backend. It receives the endpoint form on behalf of the network access device, encapsulates it into a standard Portal authentication request packet, and forwards it to the network access device. It also receives the authentication result from the network access device and pushes the final page to the endpoint.

* **SealSuite Server**: The control center of the SealSuite system. It provides web pages for employee or visitor authentication, identifies network access devices, delivers the specified address for receiving authentication information, and serves as the database for verifying the validity of accounts and passwords.


<span id="4295dea9"></span>
## Technical Implementation Modes

To adapt to network access devices from different vendors and models, SealSuite Portal authentication provides two technical implementation modes. The main difference between the two modes lies in the path through which the account and password are passed to the network access device (AC) after the endpoint user clicks "Log in" on the web page.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following modes use employee Portal authentication as an example. The underlying logic of visitor authentication is the same. During actual deployment, the system differentiates parameters such as the authentication page, for example SMS or QR code authentication, credential receiving address, and RADIUS port based on user identity, enabling fine\-grained isolation of business policies.</div>


<span id="99cf5a60"></span>
### Solution 1: Use Built\-in Portal Authentication on the AC (Recommended)

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1bf58850bd424f3db70d71d75f44607d~tplv-goo7wpa0wc-image.image) </span>

In this mode, the network access device (AC) has complete web form receiving capabilities, and the endpoint directly interacts with the AC.


* **Data flow**: The endpoint clicks Log in ➔ the account and password are sent directly to the AC device ➔ the AC sends them to the backend RADIUS/SealSuite Server for verification. After the password is verified, the AC device directly pushes the "authentication successful" page to the endpoint.

* **Advantages**: The communication link is the shortest, there are fewer interaction steps, and authentication is the fastest. The solution fully relies on the mature standard RADIUS protocol, with clear configuration logic.

* **Applicable scenario**: This is the recommended solution. It applies to enterprise network environments where network access devices have good performance, support standard built\-in integration capabilities, and may include mixed use of hardware from multiple brands.


<span id="67fd65f3"></span>
### Solution 2: Use SealSuite Portal Server Authentication

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e9cf3669450493a9083213b4d85cdfc~tplv-goo7wpa0wc-image.image) </span>

In this mode, the SealSuite system enables the "SealSuite Portal Server" module as an intermediate relay to receive the web form information sent from the endpoint on behalf of the AC.


* **Data flow**: The endpoint clicks Log in ➔ the account and password are first sent to SealSuite Portal Server ➔ SealSuite Portal Server packages and forwards them to the AC device ➔ the AC sends them to the backend RADIUS/SealSuite Server for verification. After the password is verified, the AC notifies SealSuite Portal Server, and SealSuite Portal Server pushes the "authentication successful" page to the endpoint.

* **Advantages**: Complex web information receiving work is handled by SealSuite, reducing requirements for the software, hardware performance, and capabilities of the network access device.

* **Applicable scenario**: This mode is used when your AC device has compatibility issues with receiving Portal web page data and requires an external Portal protocol handshake.

* **Limitations**: Since external Portal protocols, such as Portal 1.0/2.0, are mostly led by domestic vendors and are not international common standards, devices from international vendors such as Cisco and Aruba usually do not support this mode.


<span id="6cf5b9b4"></span>
### Workflow

Regardless of which implementation mode you select in the backend, the experience of Portal authentication is the same for endpoint users. Its underlying logic follows the following four phases:


1. **Pre\-connection and interception (common phase)** : The endpoint connects to the network and obtains an IP address. The network access device intercepts its internet access requests and only allows access to basic DNS and specified authentication\-free whitelist addresses.

2. **Web page triggering and routing instruction (common phase)** : When the endpoint initiates an HTTP request, it is forcibly redirected to the authentication web page provided by SealSuite Server. At this point, SealSuite Server instructs the browser, based on the backend configuration, to send the credentials entered later to the AC (Solution 1) or to SealSuite Portal Server (Solution 2).

3. **Credential submission and forwarding (differentiated phase)** : The user enters credentials and submits them. The data follows the path of the selected implementation mode, either directly to the AC or forwarded to the AC through SealSuite Portal Server. It finally converges at the network access device and is uniformly reported to the backend RADIUS/SealSuite Server.

4. **Verification and release (common phase)** : After the SealSuite backend verifies the credentials, it sends an Access\-Accept instruction to the network access device. The device releases the interception, the endpoint obtains full network permissions, and the authentication success page is displayed.


<span id="bdb7b8ed"></span>
## Authentication Protocol Comparison

You can use the following table to compare the differences between the two protocols.


|Dimension |802.1X Authentication |Portal Authentication |
|---|---|---|
|**Target users** |Enterprise employees with managed endpoints |Visitors, contractors, and employees’ personal devices |
|**Client requirement** |The SealSuite client must be installed |The SealSuite client is not required. Only a browser is needed. |
|**Security** |Very high: Layer 2 physical interception, CoA\-based dynamic network switching, and endpoint compliance checks |Medium: Layer 3 redirection and interception, focusing on identity verification |
|**Network access experience** |After the first login, the endpoint is automatically detected and connected in subsequent sessions |After authentication expires, the user must manually log in again on the page |
|**Permission control** |Strong: Supports dynamic VLAN/ACL and dynamic network switching |Medium: Usually releases access based on static network segments |
|**Hardware compatibility** |Very high: Based on standard RADIUS and supports mainstream vendors worldwide |AC built\-in mode: Highly compatible and supports mainstream domestic and international brands.<br><br>SealSuite\-hosted mode: Mainly supports domestic brands. |
|**Authentication methods** |SealSuite account, Windows AD authentication, and digital certificate |SealSuite account, third\-party QR code scanning, and SMS/email verification code |
