---
title: "SealSuite Deployment Guide"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/deployment_guide"
---

 &nbsp;

<span id="i.-introduction-to-basic-deployment"></span>
### I. Introduction to basic deployment

 &nbsp;

<span id="introduction-to-deployment-method"></span>
## Introduction to Deployment Method

Formal delivery methods are divided into standardized delivery and customized delivery. **This article introduces the deployment process of standardized delivery** .

**Standardized delivery** : 5 types of mirroring or installation packages are provided by default, namely SealSuite Server, VPN Server, RADIUS Server, AGW Server, and Storage Server. Provide customers with the corresponding number of nodes according to the actual procurement contract.

**Customized delivery** : Customized deployment of functional modules and components based on actual user needs, which affects standard mirroring functions or delivery forms. Provide corresponding delivery solutions to customers according to actual procurement contracts.

 &nbsp;

<span id="sealsuite-architecture-overview"></span>
## SealSuite Architecture Overview

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0cab6d3c9d6439cbf95982600867b37~tplv-goo7wpa0wc-topic.webp) </span>

 &nbsp;

<span id="standardized-delivery-mirroring-instructions"></span>
## Standardized delivery mirroring instructions

The following is a brief introduction to the functions of each component.


* SealSuite Server: provides the SealSuite portal, admin console configuration, and O&M platform management capabilities, and comes with a VPN Server node and a RADIUS node.

* VPN Server: Provides the ability to expand VPN nodes and can form a cluster with nodes provided by SealSuite Server.

* RADIUS Server: Provides the ability to extend RADIUS nodes and can form a master\-slave relationship with nodes provided by SealSuite Server.

* AGW Server: Provides application gateway nodes for Layer 7 reverse proxy access in clientless scenarios.

* Storage Server: Provides storage capacity, mainly providing storage resources for services with large storage needs. For example, leak files for data leakage prevention, leak event alarm logs, anti\-virus alarm logs, etc.


 &nbsp;

<span id="ii.-prepare-resources-for-deployment"></span>
# II. Prepare resources for deployment

 &nbsp;

<span id="server-level-resource-requirements"></span>
## Server level resource requirements

 &nbsp;

<span id="virtualization-platform-requirements"></span>
### Virtualization platform requirements

SealSuite provides virtual machine mirroring in OVA, OVF, and QCOW2 formats by default, supporting deployment on virtualization platforms based on KVM and VMware. Public Cloud environment supports Alibaba Cloud, Tencent Cloud, AWS, Huawei Cloud, etc.

 &nbsp;

<span id="number-of-virtual-machines-and-configuration-recommendations"></span>
### Number of virtual machines and configuration recommendations

SealSuite 2.1.10 version is officially delivered with 5 components, namely SealSuite Server, RADIUS Server, VPN Server, AGW Server and Storage Server.

&nbsp;


|**Components** |**Type** |**Resource** |**Size** |**Amount** |**Users** |
|---|---|---|---|---|---|
|SealSuite Server |Image |Minimum 4C 8G, recommended configuration 8C 16G |300G |Default is 1<br><br>According to the number of contracts signed |Provide system services such as management background capabilities, system operation and maintenance platforms, database services, and web services |
|RADIUS Server |Software package |determined according to the RADIUS reference table |200G |N, according to the number of contracts signed |For wireless AP/AC and switch access authentication |
|VPN Server |Software package |determined according to the VPN reference table |200G |N, according to the number of contracts signed |Used for VPN high availability and accessing different targets and other demand scenarios |
|AGW Server |Software package |determined according to the VPN reference table |200G |N, according to the number of contracts signed |Used for seven\-layer web proxy access scenarios |
|vCPE Server |Software package |determined according to the vCPE reference table |100G |N, according to the number of contracts signed |Used as an egress point for the SD\-WAN function. |
|Storage Server/MDM |Image |8C 16G |2T |1 is provided by default. |Used to store endpoint data leakage prevention (DLP) related forensic files, screenshots, etc. |


 &nbsp;

<span id="sealsuite-server-resource-configuration-reference-table"></span>
### SealSuite Server Resource Configuration Reference Table

&nbsp;


|**Specifications** |**BytePlus ECS** |**Supported amount** |
|---|---|---|
|4C 8G |ecs.c3al.xlarge |1\-500 devices |
|8C 16G |ecs.c3al.2xlarge |500\-3000 devices |
|16C 32G |ecs.c3al.4xlarge |5000\-20000 devices |


 &nbsp;

<span id="vpn-server-resource-configuration-reference-table"></span>
### VPN Server Resource Configuration Reference Table

&nbsp;


|**Specifications** |**BytePlus ECS** |**Recommended concurrency** |**Maximum concurrency** |
|---|---|---|---|
|4C 4G |ecs.c3a.xlarge |500 |1000 |
|8C 8G |ecs.c3a.2xlarge |1000 |2000 |
|16C 16G |ecs.c3a.4xlarge |2000 |4000 |


The above table is the configuration resource reference for a single node, and indicates the number of concurrent users that a single node can support.

Recommended concurrency: Recommended single\-node concurrency capacity, which can ensure the low\-load operation of VPN Server CPU and memory under this concurrency capacity

Maximum concurrency: the maximum single\-node concurrency carrying capacity, under which the VPN server runs under high CPU and memory load

 &nbsp;

<span id="radius-server-resource-configuration-reference-table"></span>
### RADIUS Server Resource Configuration Reference Table

&nbsp;


|**Specifications** |**BytePlus ECS** |**QPS** |
|---|---|---|
|2C 2G |ecs.t2\-c1m1.large |300/s |
|4C 4G |ecs.c3a.xlarge |600/s |
|8C 8G |ecs.c3a.2xlarge |1200/s |


QPS : The number of authenticated users per second, QPS is 300/s, that is, 300 users are authenticated per second. If there are 400 users, 100 users will queue up for authentication in the next second, and will not disconnect or displace already authenticated users.

 &nbsp;

<span id="agw-server-resource-configuration-reference-table"></span>
### AGW Server Resource Configuration Reference Table

&nbsp;


|**Specifications** |**BytePlus ECS** |**Recommended Concurrency** |**Maximum Concurrency** |
|---|---|---|---|
|4C 4G |ecs.c3a.xlarge |500 |1000 |
|8C 8G |ecs.c3a.2xlarge |1000 |2000 |
|16C 16G |ecs.c3a.4xlarge |2000 |4000 |


 &nbsp;

<span id="vcpe-server-resource-configuration-reference-table"></span>
### vCPE Server Resource Configuration Reference Table

&nbsp;


|**Specifications** |**BytePlus ECS** |**Recommended OS** |**BandWidth** |
|---|---|---|---|
|4C 4G |ecs.c3a.xlarge |Debian 11<br><br>CentOS 7/8<br><br>Ubuntu 20/22 |0\-100Mb |
|8C 8G |ecs.c3a.2xlarge ||100\-200Mb |
|16C 16G |ecs.c3a.4xlarge ||200\-500Mb |


 &nbsp;

<span id="network-requirements"></span>
## Network requirements

 &nbsp;

<span id="ip-address-requirements"></span>
### IP Address Requirements

The internal IP of SealSuite Server and VPN Server can be mapped to a fixed public IP through the public network NAT , and open services to the public network.

&nbsp;


|**Component** |**Exposed to public** |**IP Address** |**Amount** |**Remarks** |
|---|---|---|---|---|
|SealSuite Server |Yes |201.23.10.1 (public external) |1 is provided by default. |Fixed public ip address |
||No |192.168.1.1 |1 is provided by default. |Fixed intranet ip address |
|VPN Server |Yes |201.23.10.2 (public external) |N, according to the number of contracts signed |Fixed public ip address |
||No |192.168.1.2 |N, according to the number of contracts signed |Fixed intranet ip address |
|RADIUS Server |No |201.23.10.3 (public external)<br><br>/192.168.1.3 |N, according to the number of contracts signed |Fixed public/intranet ip address |
|AGW Server |Yes |201.23.10.4 (public external) |N, according to the number of contracts signed |Fixed public ip address |
||No |192.168.1.4 |N, according to the number of contracts signed |Fixed intranet ip address |
|Storage Server |No |192.168.1.5 |1 is provided by default. |Fixed intranet ip address |


 &nbsp;

<span id="network-port-opening-requirements"></span>
### Network port opening requirements

The following table of network open requirements applies to deploying SealSuite on an enterprise intranet.

<div style="text-align: center">
\*\*Extended nodes refer to VPN Server, RADIUS Server, AGW Server, Storage Server\*\*</div>


&nbsp;


|**Destination IP** |**Destination port** |**Protocol** |**Source IP** |**Can it be modified** |**Remarks** |
|---|---|---|---|---|---|
|SealSuite Server IP |8443 |TCP |Allow access to the IP range of the SealSuite management background, such as the administrator's computer |Yes |Admin Console Portal<br><br>Open intranet access |
||10443 |TCP |any |Yes |User access portal |
||49901 |TCP |Allow access from the IP range of the SealSuite O&M platform |No |Operation and maintenance management portal |
||49900 |TCP |VPN Server IP<br><br>RADIUS Server IP<br><br>AGW Server IP<br><br>Storage Server IP |No |Component control port<br><br>Open intranet access<br><br>Open internet access if required to communicate with internet resources |
|SealSuite public IP addresses |10443 |TCP |any |Yes |User access portal<br><br>Open internet access |
|VPN Server public IP |443 |TCP |any |Yes |VPN control port<br><br>Configure server mapping on egress routing devices |
||80 |TCP<br><br>UDP |any |Yes |VPN data port<br><br>Configure server mapping on egress routing devices |
|AGW Server public IP |443 |TCP |any |Yes |Service port of the application gateway |
|RADIUS Server IP |1812 |UDP |Wireless controller |Yes |Employee Wi\-Fi authentication port<br><br>Open intranet access<br><br>Open internet access if RADIUS server is deployed in internet |
||1813 |UDP |Wireless controller |Yes |Employee Wi\-Fi billing port<br><br>Open intranet access<br><br>Open internet access if RADIUS server is deployed in internet |
||2812 |UDP |Wired switch |Yes |Wired network authentication port<br><br>Open intranet access<br><br>Open internet access if RADIUS server is deployed in internet |
||2813 |UDP |Wired switch |Yes |Wired network billing port<br><br>Open intranet access<br><br>Open internet access if RADIUS server is deployed in internet |
||3812 |UDP |Wireless controller |Yes |Guest Wi\-Fi authentication port<br><br>Open intranet access<br><br>Open internet access if RADIUS server is deployed in internet |
||3813 |UDP |Wireless controller |Yes |Guest Wi\-Fi billing port<br><br>Open intranet access<br><br>Open internet access if RADIUS server is deployed in internet |
|Storage Server IP |49903 |TCP |SealSuite Server |No |Reserved port for ops operation and maintenance platform |
||7070 |TCP |SealSuite Server |No |Data leak prevention and anti virus module logs, backup files, screenshots and other information storage |
|Third party OSS |443 |TCP |SealSuite Server IP |No |Leaked file storage service<br><br>If you plan to use third\-party Public Cloud Object Storage, it can be integrated with the standard OSS services from BytePlus, Alibaba Cloud, and Tencent Cloud |
|CPE server IP |53 |UDP |DNS server IP |No |DNS Resolution |
|CPE server IP |49905 |TCP |SealSuite Server IP |No |gRPC connection to SealSuite Server |
|CPE server IP |49920<br><br>443<br><br>80 |TCP |SealSuite SaaS Resources |No |gPRC<br><br>api/https<br><br>api/http |
|CPE server IP |53 |TCP<br><br>UDP |SealSuite SaaS Resources |No |DNS (if no custom DNS server has been setup) |
|CPE server IP |5000\-40000 |TCP<br><br>UDP |SealSuite SaaS Resources |No |WireGuard tunnel |


Note: The yellow background part indicates that the public network needs to be mapped.

SealSuite SaaS Resources

[SealSuite SaaS Resources for cpe](https://bytedance.sg.larkoffice.com/sheets/I6LRs8LEKhyczNtYAHClx9g3gDf)

 &nbsp;

<span id="sealsuite-internet-access-requirements"></span>
### SealSuite Internet access requirements

In order to ensure the normal use of SealSuite 's functions, the following public network resources need to be reserved for SealSuite:

&nbsp;


|**Request destination address** |**Request source** |**Whether it is necessary to** |**Usage scenarios** |
|---|---|---|---|
|[https://corplink.isealsuite.com](https://corplink.isealsuite.com) |SealSuite Client |Yes |Client Login Access to Enterprise Information, SealSuite Privacy Policy, Software Distribution Public Key, |
||SealSuite Server |No |When using the data leakage prevention module, it is used to update the application library and sensitive data templates at the server level. |
|[https://cdn.isealsuite.com](https://oss-s3.ifeilian.com/) |SealSuite Server |No |Default virus library update address, dynamic control IP library update address, patch management update address |
|[https://corplink.isealsuite.com](https://corplink.isealsuite.com) |SealSuite Server |No |Default virus library license update address, data leakage prevention policy model update address |


 &nbsp;

<span id="domain-name-requirements-and-certificate-requirements"></span>
### Domain name requirements and certificate requirements

&nbsp;


|**Resource name** |**Purpose** |**Example** |**Remarks** |
|---|---|---|---|
|Portal domain name |User web page access address, client and server level connection address |sealsuite.xxx.com |A domain name is required for a formal launch. For PoC testing, you can use the public IP address |
|Portal domain certificate and private key |HTTPS encryption for portal domain access |SealSuite.xxx.com CRT file<br><br>SealSuite.xxx.com key file |Must have. Support self\-signed domain name certificate. If it is a self\-signed domain name certificate, the issued RootCA certificate needs to be provided |
|Self\-signed RootCA certificate |The portal domain name uses a self\-issued certificate. When the client requests the portal domain name through the enterprise identification code, the RootCA certificate is downloaded to the client and the client trust is configured |XXCA.pem file |Only when using a self\-issued domain name certificate, it is required to provide |
|Software signing public key |When the client fills in the enterprise identification code activation, it pulls the public key from the Volcengine to sign and decrypt the software package distributed by the software |Xxx.public.key file |This item is only required when enabling security checks for software distribution |


**Limitations of using a self\-signed certificate**:


* Third\-party login (such as Feishu, WeCom) is not available

   * Reason: Third\-party software will verify the public network certificate, and the self\-signed certificate is not trusted

* Third\-party IM (such as Feishu, WeCom) view OTP not available

   * Reason: The third\-party Client will verify the public network certificate, and the self\-signed certificate is not trusted

* Browsers such as visitor Wi\-Fi and Client download pages may prompt security issues, and some lower version system browsers of visitor Wi\-Fi may not pop up

   * Reason: Self\-signed document browser is not trusted

   * Suggestion: Click Trust to continue access when prompted with security issues, and directly access any webpage with a browser when the visitor Wi\-Fi does not pop up.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip"><strong>Notes</strong> :</div>


<div data-tips="true" data-tips-type="tip"><strong>1. If the external mapping SealSuite Server's IP address and SealSuite Server's outbound address after NAT are unified addresses, and the portal domain name is configured, the portal domain name A record needs to be added to the intranet DNS server or modify the local hosts file, otherwise there will be an exception when accessing the management background after connecting to the intranet</strong></div>


<div data-tips="true" data-tips-type="tip"><strong>2. The export mapping port is consistent with the SealSuite custom port, such as the public IP address is 100.10.10.1, and the 8001 port is open, which needs to be mapped to the 8001 port 192.168.10.1 the internal IP address</strong></div>


<div data-tips="true" data-tips-type="tip"><strong>3. Ensure that the SealSuite server level can access the Internet, otherwise it will affect some functions, such as importing third\-party data sources and third\-party authorized login</strong></div>


 &nbsp;

<span id="iii.-sealsuite-server-deployment-configuration"></span>
# III. SealSuite Server Deployment Configuration

 &nbsp;

<span id="image-initialization-configuration"></span>
## Image initialization configuration


1. Login to Console: After importing the mirroring configuration, start the system. You can connect to the machine through VNC or SSH , enter the initialization account password: pilot /pilot2048, **the first connection will prompt to change the default pilot password** , **the pilot password is at least 8 digits, it is recommended to set a high\-strength password with characters and uppercase and lowercase letters** . After changing and confirming the password, log in to the system and enter the Console. The homepage displays the current product version number and deployment mode information.


<div style="text-align: center">
<strong>Tab key to switch text boxes, Enter key on the button to perform the operation, Esc to return to the left menu</strong></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5bb6bfe7b6584bffa1d35c1862459be5~tplv-goo7wpa0wc-image.image" width="1708px" /></div>



2. Network Configuration: Enter Network Setup to configure IP, support static IP and DHCP two modes, default is DHCP automatically obtains IP, it is recommended to configure static IP to prevent IP changes from causing the system to be inaccessible, and you can also configure DNS Server IP in DNS Setup. After the network configuration is completed, you need to restart the machine. **It is recommended to configure it to static mode.** 


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99b068f19a054464b7def59849ed395f~tplv-goo7wpa0wc-image.image" width="1572px" /></div>



3. Configure DNS : Enter DNS Setup to support configuring primary and secondary DNS.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/445ab4b878094bd48e0ce0e91b15a670~tplv-goo7wpa0wc-image.image" width="1570px" /></div>



4. Configure NTP : Enter NTP Setup, the default is Alibaba Cloud Ali Cloud Aliyun's NTP, which can be modified to NTP in the enterprise intranet. It is recommended to use the public network NTP server.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b490bf301ea4354a512947607b67ad1~tplv-goo7wpa0wc-image.image" width="1562px" /></div>


Restart the machine: Enter Reboot, enter y or yes, and press Enter to complete the machine restart

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95429ac9a7c346c7a42da0e518ffa147~tplv-goo7wpa0wc-image.image" width="1568px" /></div>



6. Platform Initialization: Enter Initialize, follow the prompts to confirm the initialization process, and you can see the execution result in the output window. Get the operation and maintenance platform account password (account is ops @SealSuite.local) and the management platform account password (account is admin@SealSuite.local) and record it. **After completing the initialization, obtain the Secret Key through the "cluster" page to connect the Storage node later.** 

   **Note: Please remember the output account password! If you forget the password, please contact the SealSuite delivery team to check** .


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9224fef302f843f1bae8b373586bf266~tplv-goo7wpa0wc-image.image" width="1708px" /></div>


 &nbsp;

<span id="authorized-license"></span>
## Authorized license


1. After completing the initialization configuration, enter the address in the browser **https://< SealSuite Server_ip \>: 49901** to access the SealSuite operation and maintenance platform, trust the domain name certificate and continue to access, enter the default account password to log in to the system.

* Default administrator account: **ops@SealSuite.local** , password: **password randomly generated in the mirroring initialization configuration**


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a09ef78bc9544078f5912de0b19774b~tplv-goo7wpa0wc-image.image" width="2216px" /></div>



2. After successful login, enter the SealSuite operation and maintenance platform page, select  **"System Configuration" \- "Rights Center"**  to enter the license management page


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d32139c8ab6148679fe7c13124768c2c~tplv-goo7wpa0wc-image.image" width="2750px" /></div>



3. Click Copy to send the device fingerprint and related License information to the implementer. The implementer generates a License and sends it to the customer. Click Edit to fill in the License and refresh the current page to see the complete system functions. **After entering the License, the status of the License is displayed as "Activated", and the authorization information can be viewed.** 


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e314099a29214f9b850f73f000311e36~tplv-goo7wpa0wc-image.image" width="2790px" /></div>


 &nbsp;

<span id="domain-name-configuration"></span>
## Domain name configuration

In the SealSuite operation and maintenance platform  **"System Configuration" \- "Enterprise Configuration"**  Click Edit to configure the portal domain name and certificate, management domain name and certificate respectively. The **portal domain name** and certificate are recommended as **public domain name and public CA certificate, supporting self\-signed certificate files** . **The management domain name and certificate can be consistent with the portal domain name.**  The management domain name is the access address of the current management background. From a security perspective, it is recommended to use an intranet domain name or IP, and it is not open to the public network. (The default port of the portal site is 10443, and the default port of the management background is 8443. Customization is allowed, but the port cannot be duplicated. After customization and modification, contact the implementation personnel for enterprise portal domain name registration)

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d4ecfa696a8491cad9fbf16a99b81e7~tplv-goo7wpa0wc-image.image" width="2802px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b44e87c9b544d55a09e8a360395bd35~tplv-goo7wpa0wc-image.image" width="482px" /></div>


After the configuration is completed, you can use the new management domain https://< admin_domain \>: 8443 to access the management background. The login account of the management background is admin@SealSuite.local (the password is the password obtained in the mirroring initialization process). After entering the management background, you can add a new administrator in " **System Configuration" \- \> "Administrator Permissions", delete the default administrator account or modify the default administrator password on the portal page** .

 &nbsp;

<span id="client-configuration"></span>
## Client configuration


1. After completing the domain configuration, use the new management domain https://< admin_domain \>: 8443 to access the management background

* Default administrator account: **admin@SealSuite.local** , password: **password randomly generated in the mirroring initialization configuration**

2. After entering the management background page, click "Version Release" in the left navigation bar to enter the Client version management page. If there is no "Version Release", you can pin the relevant tags through the "All Features" in the navigation bar.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ab8624bf9a149e0a4094610cfab572e~tplv-goo7wpa0wc-image.image" width="2822px" /></div>



2. After clicking "New Version", fill in the basic information according to the prompt, upload the Client installation package or download link, and open "Online Status" to make the version of Client visible to users.


<div style="text-align: center">
<strong>(Please contact SealSuite delivery team for Client installation package)</strong></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ece5620a47b4073bc750b00868deb30~tplv-goo7wpa0wc-image.image" width="1440px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e14d1efbecc545ca921837136f6bfadd~tplv-goo7wpa0wc-image.image" width="2388px" /></div>



3. Enter the "System Configuration" \- "Enterprise Configuration" page in the management background, copy the self\-installation method link, and send it to the user for self\-service Client download.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10d747c7733242589d08bfb653eaa155~tplv-goo7wpa0wc-image.image" width="2348px" /></div>


The effect after opening the link is as follows:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/955c30a55ca04fad824fe0a33c76cead~tplv-goo7wpa0wc-image.image" width="2820px" /></div>


 &nbsp;

<span id="iv.-vpn-server-image-deployment-configuration"></span>
# IV. VPN Server image deployment configuration


1. Go to SealSuite Admin Console , click "VPN Management" \- "Node Management" \- "Create Node", and complete the relevant information configuration as required


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14710648fa944e6182cae0f318d2d204~tplv-goo7wpa0wc-image.image" width="2792px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b40033025a8420f85e2d25af33e6744~tplv-goo7wpa0wc-image.image" width="1528px" /></div>



* **Node name** : The name that the node displays to the user

* **DNS IP** : DNS address issued by the VPN node, generally fill in the internal DNS address, support configuration **primary and secondary**

* **Intranet IP : The** internal IP address of the VPN node

* **Public IP : The** public IP address mapped by the VPN node

* **Control port** : Client exploration, configuration issued, recommended 8001, can be modified

* **Data port** : VPN data connection, recommended 8002, can be modified

* **Whether Network Address Translation ( NAT ) is enabled:** 

   **Enable:**  Use virtual IP address pool, the IP address pool can be set to the intranet unplanned network segment, for example, the intranet IP range is 192.168.0.0/16 segment, you can set the IP address pool to 10.10.10.0/24.

   **Not enabled:**  Do not use the virtual IP Address pool. The address of the IP Address needs to be set to the network segment planned by the internal network and not used. For example, if the original network plan is 192.168.10.0/24 segment, then the IP Address pool can be set to 192.168.20.0/24. At this time, it is necessary to configure the next hop to access the 192.168.20.0/24 network segment on the enterprise intranet switch as the intranet IP of the VPN node.

* **IP pool** : Cannot conflict with the existing address range of the enterprise intranet.

2. After the configuration is completed, click "Next" to obtain the VPN Server installation package, and follow the prompts to install the VPN Server in the prepared Linux virtual machine.

   1. Use the wget command to download the VPN Server installation package link in the prepared Linux virtual machine. **If SealSuite Server uses a self\-signed certificate, you need to execute wget \-\-no\-check\-certificate to skip certificate verification**


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a14f6062334d461a9b424f599a598226~tplv-goo7wpa0wc-image.image" width="1634px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e10038a74b2a4cf69b2e8c4ae67ef4f4~tplv-goo7wpa0wc-image.image" width="2014px" /></div>



2. Complete the installation package decompression and installation according to the background instructions. **If the administrator operates through the root account, remove the sudo command**


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2f5d500a7e24839847de0408822900d~tplv-goo7wpa0wc-image.image" width="1624px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e5ebfb7b6e04fae86581984ba19feac~tplv-goo7wpa0wc-image.image" width="1932px" /></div>



3. During the installation process, the system prompts that you need to enter "app_id" and "app_secret". Please copy "Component ID" and "Component secret" from the SealSuite Admin Console to the virtual machine for execution to complete the final installation. Note: Only one node can be configured for each set of Component ID and secret. Please get it again when adding a new node.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc0a7b0748824630b24f746a4e70ca6e~tplv-goo7wpa0wc-image.image" width="1506px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/612d225c7a85498fad23593558047f75~tplv-goo7wpa0wc-image.image" width="1960px" /></div>



3. After installation is complete, click "Next" to enter the "Connectivity Test" page, click "Start Testing" to ensure that the connectivity is normal


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7aa7fa4ca29c4310aa348f939e27907d~tplv-goo7wpa0wc-image.image" width="1548px" /></div>



4. After completing the "Connectivity Check", click "Finish" to complete the entire installation process of the node


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10efaf702af34d7e8caaef5f69b03c2d~tplv-goo7wpa0wc-image.image" width="1560px" /></div>



5. After completing the installation of the VPN node, the node will enter the "Testing" state by default. You need to go through the "Node Management" in the SealSuite management background, click "Change Status", adjust the node to "Online", and complete the entire deployment process of the VPN extension node.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a44b5979fa0c4a85ad92a9cfa0e73119~tplv-goo7wpa0wc-image.image" width="2406px" /></div>


 &nbsp;

<span id="v.-radius-server-image-deployment-configuration"></span>
# V. RADIUS Server image deployment configuration


1. Go to the SealSuite Admin Console , click "Wi\-Fi Management" \- "Configuration", and follow the prompts to complete the relevant information configuration


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ea5affb470c4b49bde34b8c8dee01d8~tplv-goo7wpa0wc-image.image" width="2756px" /></div>



* RADIUS name: Custom RADIUS name

* IP address: You can fill in the internal network address or public network address.

   * Fill in the internal network address: Ensure that SealSuite Server and RADIUS Server can communicate on the internal network

   * Fill in the public network address: Ensure that the RADIUS Server is open to the external network and the port is reachable

* Employee Wi\-Fi authentication port: 1812 is recommended and can be modified

* Employee Wi\-Fi billing port: 1813 is recommended and can be modified

* Wired network authentication port: recommended 2812, can be modified

* Wired network billing port: recommended 2813, can be modified

* Guest Wi\-Fi authentication port: 3812 recommended, can be modified

* Guest Wi\-Fi billing port: 3813 recommended, can be modified

2. After the configuration is completed, click "Next" to obtain the RADIUS Server installation package, and install RADIUS Server in the prepared Linux virtual machine according to the prompts

   1. Download the RADIUS Server installation package link in the prepend Linux virtual machine through the wget command. **If SealSuite Server uses a self\-signed certificate, you need to execute wget \-\-no\-check\-certificate to skip certificate verification**


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb822dc2a3ed4325b9bd980f1134dca0~tplv-goo7wpa0wc-image.image" width="1514px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81d19b9e228e48cf8891d61e024b4d3f~tplv-goo7wpa0wc-image.image" width="2018px" /></div>



2. Complete the installation package decompression and installation according to the background instructions. **If the administrator operates through the root account, remove the sudo command**


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44a3d808899844e8ab8420b135f18ee9~tplv-goo7wpa0wc-image.image" width="1512px" /></div>



3. During the installation process, the system prompts that you need to enter "app_id" and "app_secret". Please copy "Component ID" and "Component secret" from the SealSuite Admin Console to the virtual machine for execution to complete the final installation. Note: Only one node can be configured for each set of Component ID and secret. Please get it again when adding a new node.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e02f8be084f14a6398b9ff4220d6b1ac~tplv-goo7wpa0wc-image.image" width="1506px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/17f3f03ca477464eae6b854ca6125af1~tplv-goo7wpa0wc-image.image" width="1994px" /></div>



3. After installation is complete, click "Next" to enter the "Connectivity Test" page, click "Start Testing" to ensure that the connectivity is normal


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57f929afe4994072a72ef2301c5b84f5~tplv-goo7wpa0wc-image.image" width="1560px" /></div>



4. After completing the "Connectivity Check", click "Finish" to complete the entire installation process of the node


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b67ce41bb9d44e55be479d3a522313d6~tplv-goo7wpa0wc-image.image" width="1606px" /></div>



3. Configure wireless controller, wired switch related information, **if temporarily unable to configure, directly click Next** .


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31182e377f2b4bb5a8a1a2ca29a09957~tplv-goo7wpa0wc-image.image" width="2784px" /></div>



4. Add the SSID configured on Wi\-Fi, which is currently required. You can fill in a value at will and modify it according to the actual situation later.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/345258a629a8473cac7c75e1e615593e~tplv-goo7wpa0wc-image.image" width="1531px" /></div>


 &nbsp;

<span id="vi.-agw-server-image-deployment-configuration"></span>
# VI. AGW Server image deployment configuration


1. Go to the SealSuite admin console , click "Application Management" \- "Gateway Management" \- "Create Node", and follow the prompts to complete the relevant information configuration


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf67ac8ebd864568b1de9d76a6693a28~tplv-goo7wpa0wc-image.image" width="2288px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c27e6ea87cf49ffa1867e5c665d21ed~tplv-goo7wpa0wc-image.image" width="1410px" /></div>



* Node name: Custom gateway node name

* IP Address: You can fill in the internal network address or public network address.

   * Fill in the internal network address: Ensure that SealSuite Server and AGW Server can communicate within the internal network

   * Fill in the public network address: Ensure that the AGW Server is open to the external network and the port is reachable

* DNS server: AGW DNS service for resolving domain names, generally fill in the DNS address of the intranet, support configuration **primary and secondary**

2. After the configuration is completed, click "Next" to obtain the AGW Server installation package, and install AGW Server in the Linux virtual machine prepared according to the prompts

   1. Download the AGW Server installation package link in the prepend Linux virtual machine through the wget command. **If SealSuite Server uses a self\-signed certificate, you need to execute wget \-\-no\-check\-certificate to skip certificate verification**


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fda4617b57443b9ac15b84811c8c3c8~tplv-goo7wpa0wc-image.image" width="1372px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0df9b4830cf64aff995db563d3edb0a3~tplv-goo7wpa0wc-image.image" width="1944px" /></div>



2. Complete the installation package decompression and installation according to the background instructions. **If the administrator operates through the root account, remove the sudo command**


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f8792ab284b4491a7888faef4ec55d1~tplv-goo7wpa0wc-image.image" width="1512px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5eedda900188412089ad34339b5750e6~tplv-goo7wpa0wc-image.image" width="1922px" /></div>



3. During the installation process, the system prompts that you need to enter "app_id" and "app_secret". Please copy "Component ID" and "Component secret" from the SealSuite Admin Console to the virtual machine for execution to complete the final installation. Note: Only one node can be configured for each set of Component ID and secret. Please get it again when adding a new node.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a1336a9e97342b4880d773b4622760f~tplv-goo7wpa0wc-image.image" width="1506px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3276d7852ef845ecaad080bd860774a7~tplv-goo7wpa0wc-image.image" width="1934px" /></div>



3. After installation is complete, click "Next" to enter the "Connectivity Test" page, click "Start Testing" to ensure that the connectivity is normal


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e6852c31b3d43a6a964d9b7379142a3~tplv-goo7wpa0wc-image.image" width="1432px" /></div>



4. After completing the "Connectivity Check", click "Finish" to complete the entire installation process of the node


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c8529d05479474a8d15f51276d3f04a~tplv-goo7wpa0wc-image.image" width="1422px" /></div>



5. After clicking "Finish", the node is completed and officially launched.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38f837039c3f46ae90fd556feaf47967~tplv-goo7wpa0wc-image.image" width="2830px" /></div>


 &nbsp;

<span id="viii.-storage-server-image-deployment-configuration"></span>
# VIII. Storage Server image deployment configuration


1. Login/ssh to mirroring through corplink account, **account is corplink, password is corplink2021$** 


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00c3b781af9d4cc7b9f5ef6b15884183~tplv-goo7wpa0wc-image.image" width="839px" /></div>



2. After logging into the system, enter the command pilot , press Enter, and enter the Storage Server homepage


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6e22746af6454ce69523c0de9b713145~tplv-goo7wpa0wc-image.image" width="1054px" /></div>



3. Go to the Network Setup page and configure Storage mirroring IP Address, Subnet mask, and Gateway


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5fc6eb3c100f43eca137dd9608e5c0ae~tplv-goo7wpa0wc-image.image" width="1744px" /></div>



4. Go to the Initialize page and set the Manager IP Address to SealSuite Server address


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6534fb3f1658465097b6c28c00296e18~tplv-goo7wpa0wc-image.image" width="1054px" /></div>



5. Go to the DNS Setup page, set DNS , support setting primary and secondary DNS


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d55abfc8a92f48668e4bad1d0825fd55~tplv-goo7wpa0wc-image.image" width="1804px" /></div>



6. Go to the NTP Setup page, set up the NTP server, you can keep the default NTP server


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68542e4c9c134018875244a0d311671a~tplv-goo7wpa0wc-image.image" width="1862px" /></div>



7. After completing the configuration, log in to the ops operation and maintenance platform to view the host list and confirm the online status of the node


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/862d70851acf48faae0ec1933254f34a~tplv-goo7wpa0wc-image.image" width="1280px" /></div>



8. Log in to the SealSuite web page management background, check the "File Service" in the "System Configuration" of the data leakage prevention module to confirm that it has been updated to the Store node IP


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12d3bb2cbe234d3dbe08b51c4508ce3b~tplv-goo7wpa0wc-image.image" width="3356px" /></div>


 &nbsp;

<span id="ix.-mdm-server-image-deployment-configuration"></span>
# IX. MDM Server image deployment configuration

We provide below versions of images that work with SealSuite Server 3.0.6+

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7fe793aea6945cda25975a67449d4cf~tplv-goo7wpa0wc-image.image" width="1280px" /></div>


 &nbsp;

<span id="login-image-via-ssh"></span>
## login image via ssh


1. Account: corplink，password: veC0rplinK.5ec


 &nbsp;

<span id="key-in-"pilot"-to-enter-configuration-panel:"></span>
## Key in "pilot" to enter configuration panel:


1. Obtain the Shared Secret Key from SealSuite Server Ops portal and initialize with the server IP and this key.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5d12fae973d47a7811a640915ba9b93~tplv-goo7wpa0wc-image.image" width="2054px" /></div>



2. Setup Network and DNS related config and then Exit


 &nbsp;

<span id="configure-mdm-device-number-for-allocating-memory:-sudo-/opt/corplink/tool/reconfig_mdm.sh"></span>
## Configure MDM device number for allocating memory: sudo /opt/corplink/tool/reconfig_mdm.sh

 &nbsp;

<span id="navigate-to-sealsuite-server-pilot-user,-point-the-mdm-service-to-this-server-using-the-command-below:"></span>
## Navigate to SealSuite Server Pilot user, point the MDM service to this server using the command below:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/942a73be57994e6586743276ab1d37ef~tplv-goo7wpa0wc-image.image" width="930px" /></div>


[addr] = SealSuiteServerIP:8140

 &nbsp;

<span id="x.-console-function-description"></span>
# X. Console Function Description

SealSuite Console is the operating platform for SealSuite mirroring, used for daily operation and troubleshooting by administrators. It integrates functions such as initialization, network settings, DNS settings, NTP server settings, commonly used tools, system upgrades, and machine restarts/shutdowns.

 &nbsp;

<span id="shortcut"></span>
## Shortcut


* Left Menu: Enter to enter the selected menu item

* Right Description/Output: arrow keys up/down, scroll to view

* Any window on the right:

   * Enter Esc to return to the Left Menu

   * Enter Tab to switch between different windows on the right

* Initialize/Network Setup/DNS Setup：

   * Text box Enter or Tab to switch to the next control

   * Press the Enter button to perform the corresponding action

* Tool：

   * After entering the command, Enter triggers execution.

   * Ctrl + K interrupts the current command execution

* Exit Console: Ctrl + Q


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5330e6b3e9b54ee88003a33553e6b0a2~tplv-goo7wpa0wc-image.image" width="1121px" /></div>


 &nbsp;

<span id="common-tools"></span>
## **Common tools**

Console supports some commonly used tool commands for setting up and troubleshooting network issues, etc. The supported commands mainly include:


* Ping < ip \> Detect IP connectivity

* Nc < ip \> < port \> Detect IP specified port connectivity

* Traceroute < ip \> Traces the routing path of network packets

* ARP view/set ARP cache table information

* Ifconfig view/set network interface card information

* Route View/set route information

* IP configuration network

* Date View system date and time

* Uptime view system running time and load


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/822947c2ac3044229c84b1a0e646cb24~tplv-goo7wpa0wc-image.image" width="1630px" /></div>
