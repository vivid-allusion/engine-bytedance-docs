---
title: "Creating an SSL-VPN server"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Creating-an-SSL-server-1"
---

You can establish site\-to\-site connections with the SSL\-VPN feature only after creating an SSL\-VPN server.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Before you begin

Before creating an SSL\-VPN server, ensure a VPN gateway with SSL\-VPN connectivity is created.


* If you need to create a new VPN gateway with SSL\-VPN enabled, see [Creating a VPN gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-VPN-gateway-2) for procedure.

* If you already have a VPN gateway without SSL\-VPN connectivity, you can enable it. For procedure, see [Modifying configuration for VPN gateway](https://docs.byteplus.com/en/docs/vpn/Modifying-VPN-gateway-configurations).

* Two\-Factor Authentication is only available on VPN gateway version 3.4 and later. If your gateway version does not apply, upgrade it on the instance details page first.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Two\-Factor Authentication is in the beta stage. To request a trial, please contact your account manager.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fde97ca0c5f9e5bf10100b29406146e0.png) </span>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [SSL VPN Server console](https://console.byteplus.com/vpn/sslServer). 

2. In the top menu bar, select a target region and project.

3. Click **Create SSL Server**, and configure the SSL\-VPN server parameters based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Name |Set the name for the SSL\-VPN server. |Server\-01 |
   |VPN gateway |Select a VPN gateway to which the SSL\-VPN server you want to create is associated. |VPNGW\-01 |
   |Local Subnet |In an SSL\-VPN connection, Local Subnet refers to the address ranges that clients are allowed to access through the SSL\-VPN tunnel. This can include subnet CIDRs within your VPC, CIDRs of on\-premises data centers connected to VPC via Direct Connect, and cloud service address ranges (e.g., Torch Object Storage, Cloud Database).<br><br><br>* Recommended mask for Local Subnet: `/8` to `/32`.<br><br>* The local subnet must not conflict with the client IP pool.<br><br>* Up to **5** local subnets can be configured. |172.XX.1.0/24, 172.XX.2.0/24 |
   |Client IP Pool |In SSL\-VPN, Client IP pool refers to the CIDR blocks assigned by an SSL\-VPN server to client devices for communication. It is not the local CIDR blocks of client devices. When a client connects through the SSL\-VPN connection, the VPN gateway assigns an IP address from this client IP pool to the client.​<br><br><br>* Mask for client IP pool: `/16` to `/28`.<br><br>* The client IP pool must not conflict with the local subnet.<br><br>* The client IP pool must not be the same as the VPN gateway route.<br><br>* The client IP pool must not conflict with any routes in the VPN gateway's default route table.<br><br>* The client IP pool must not overlap with `100.64.0.0/10`, `169.254.0.0/16`, `127.0.0.0/8`, `224.0.0.0/4`, or `240.0.0.0/4`.<br><br>* **The available IP count in the client IP pool must be at least four times the SSL Max Connections value configured when creating the VPN gateway**. For example, if the SSL Max Connections is set to 10, the client IP pool must contain more than 40 available IP addresses. |192.XX.0.0/16 |
   |Protocol |Select the protocol used for SSL\-VPN connection. **TCP** (default) and **UDP** are supported.​ |TCP |
   |Encryption algorithm |Select the encryption algorithm for the SSL\-VPN connection. Supported options: AES\-128\-CBC (default), AES\-192\-CBC, AES\-256\-CBC, no encryption. |AES\-128\-CBC |
   |Authentication algorithm |Select the authentication algorithm for the SSL\-VPN connection. Supported options: SHA1 (default), MD5, no encryption. |SHA1 |
   |Data compression |Specify whether to compress data during encrypted transmission. Default: **No**. |No |
   |Port |The port used by the SSL\-VPN server. Port range: **1\-65535**. Default: **1194**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Unsupported ports: 22, 68, 179, 323, 500, and 4500.</div><br> |1194 |
   |Affiliated project |Select the project to which the new SSL\-VPN server belongs. A project refers to a task in your daily work. You can create multiple projects under the same account and create or purchase cloud resources for each project. Cloud resources cannot be shared between different projects.<br><br><br>* After you select a project, the created SSL\-VPN server can only be used by users who have permissions for that project.<br><br>* If you have selected **All Resources** in the top menu bar before entering the creation page, the new SSL\-VPN server belongs to the default project. You can change the project on the Create SSL Server page.<br><br>* If you have selected a specific project in the top menu bar before entering the creation page, the new SSL\-VPN server belongs to that specific project. You cannot change the project on the Create SSL Server page. To change the project, exit the creation page, select the project again, then create the SSL\-VPN server.<br><br>* If no projects are available, click **Create project** on the right to create a new project.<br><br>* After adding the SSL\-VPN server to a project, you can transfer the SSL\-VPN server out of the project based on your actual business needs. For details, see [Project resource management](https://docs.byteplus.com/en/docs/6649/94337).<br><br>* SSL\-VPN Client Certificate is a sub\-resource of SSL\-VPN Server. A certificate can only be transferred between projects along with its server. It cannot be transferred alone. |default |
   |**Advanced option** |||
   |Certificate reuse |Specify whether to enable certificate reuse. Default: **Yes**.<br><br><br>* Enable: A certificate created by the SSL\-VPN server supports multiple clients connecting simultaneously.<br><br>* Disable: A certificate created by the SSL\-VPN server supports only one client at a time. Other clients will take over the current connection when logging in. |Yes |
   |SSL connection log |Specify whether to enable connection log for the SSL\-VPN server.<br><br><br>* Enable: Connection logs are delivered to [Torch Log Service](https://docs.byteplus.com/en/docs/tls/What_is_TLS)[ (TLS)](https://docs.byteplus.com/en/docs/tls/What_is_TLS). You can locate issues by searching log keywords. For more information, see [How to troubleshoot common errors by checking the SSL-VPN connection logs](https://docs.byteplus.com/en/docs/vpn/SSL-VPN-connection-FAQs#Hk1WXWBa)<br><br>* Disable: Logging is not enabled. You can [enable connection log](https://docs.byteplus.com/en/docs/vpn/Viewing-IPsec-VPN-connection-logs#.5q2l6aqk5LqM77ya5byA5ZCvSVBzZWPov57mjqXml6Xlv5c=) later from the instance list after the SSL\-VPN server is created.<br><br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">SSL\-VPN Connection Log is in the invite\-only beta stage. To request a trial, please contact your account manager.</div><br> |Enable |
   |DNS server IP |SSL\-VPN connections use the BytePlus DNS server by default. You can also specify a custom DNS server IP. Once set, the custom DNS server address is uniformly distributed to all SSL\-VPN connections.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Custom DNS is in the invite\-only beta stage. To request a trial, please contact your account manager.</div><br><br><br>* <div data-tips="true" data-tips-type="default">DNS server IP only supports IPv4 addresses. Add <code>100.64.0.0/10</code> to the local subnet when using a custom DNS server. Otherwise, BytePlus cloud services may not be accessible.</div><br> |114.XX.XX.8 |
   |DNS resolution domain |Set the domain to be resolved by the custom DNS server. This takes effect only after the DNS server IP is configured. Domains not set here are resolved by BytePlus DNS server by default. |\*.dns.com |
   |Two\-factor authentication |Two\-factor authentication is a security mechanism that verifies identity using two different types of credentials. VPN Connect provides SAML\-based user SSO for this purpose.<br><br><br>* Enable:​ Users must pass both certificate authentication and identity authentication before establishing an SSL\-VPN connection.<br><br>* Disable:​ Users only need to pass certificate authentication to establish an SSL\-VPN connection.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Changing the two\-factor authentication status (enabled/disabled) will interrupt all existing SSL\-VPN connections under this SSL\-VPN server. Proceed with caution.</div><br> |Disable |
   |SAML metadata |This parameter is only required when two\-factor authentication is enabled. You need to provide an XML metadata file for the identity provider (IdP) and service provider to exchange authentication and authorization data.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The SAML metadata exported from the IdP must include the IdP login URL, IdP entity ID, and a valid X.509 certificate. This information is used for subsequent SAML SSO security validation.</div><br><br><br>* <div data-tips="true" data-tips-type="default">SAML metadata from one IdP can be used for multiple SSL\-VPN servers' two\-factor authentication.</div><br><br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Changing SAML metadata will interrupt all existing SSL\-VPN connections under this SSL\-VPN server. Proceed with caution.</div><br> |\- |
   |Tag |A tag consists of a tag key (Key) and a tag value (Value), which can be used to classify and search the SSL\-VPN server. [Learn more](https://docs.byteplus.com/en/docs/vpn/Tag-management)<br><br><br>* Click **Add tag** to add multiple tags as needed. You can add up to 20 tags per action. Each SSL\-VPN server can have up to 50 tags.<br><br>* Keys of multiple tags on the same SSL\-VPN server must be unique, and each Key can have only one Value.<br><br>* The Key and the Value are case\-sensitive. For example, Key=tag and Key=Tag are two different Keys. |key:test |
   

5. Click **OK** to complete the action.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next


* [Create SSL-VPN client certificate](https://docs.byteplus.com/en/docs/vpn/Creating-an-SSL-client-certificate): Create an SSL\-VPN client certificates for initiating client connections.

* [Modify SSL-VPN server](https://docs.byteplus.com/en/docs/vpn/Modify-an-SSL-server): After the SSL\-VPN server is created, you can modify its configuration.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[CreateSslVpnServer](https://docs.byteplus.com/en/docs/vpn/CreateSslVpnServer): Create an SSL\-VPN server.
