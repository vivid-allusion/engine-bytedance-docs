---
title: "Modifying an SSL-VPN server"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Modify-an-SSL-server"
---

After an SSL\-VPN server is created, you can modify its configuration. Modifying SSL\-VPN server may cause the original SSL\-VPN connection to be interrupted. You need to re\-download and install the SSL\-VPN client certificate or re\-establish the SSL\-VPN connection. This topic describes how to modify an SSL\-VPN server.

<span id=".5pON5L2c6ZmQ5Yi2"></span>
## Limits

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>Modifying the SSL\-VPN server information may lead to business disruption. Proceed with caution</strong>.</div>



|Configuration to be modified |Impact |Actions after modification |
|---|---|---|
|Local Subnet |All existing SSL\-VPN connections under this SSL\-VPN server will be interrupted. |Reconnect from the client after modification. |
|Client IP Pool |||
|Data compression |||
|Certificate reuse |||
|Two\-factor authentication |||
|SAML metadata |||
|Protocol |All existing SSL\-VPN connections under this server will be interrupted. SSL\-VPN client certificates created with this server will become invalid. |After modification, download the new SSL\-VPN client certificate. Then manually disconnect the existing connection on the client. Install the new certificate and initiate a new SSL\-VPN connection. |
|Encryption algorithm |||
|Authentication algorithm |||
|Port |||


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [SSL VPN Server console](https://console.byteplus.com/vpn/sslServer). 

2. In the top menu bar, select the target region and related project of the resource.

3. In the SSL\-VPN server list, click **Modify** in the **Actions** column of the target SSL\-VPN server.

4. On the **Modify SSL Server** page, modify the SSL\-VPN server configuration as needed.

5. After modification, click **OK** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[ModifySslVpnServer](https://docs.byteplus.com/en/docs/vpn/ModifySslVpnServer): Modify the name, description, local subnet, client IP pool, encryption algorithm, authentication algorithm, and other related information of an SSL\-VPN server.
