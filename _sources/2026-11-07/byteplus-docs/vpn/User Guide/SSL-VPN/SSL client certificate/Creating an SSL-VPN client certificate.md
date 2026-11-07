---
title: "Creating an SSL-VPN client certificate"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Creating-an-SSL-client-certificate"
---

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have created an SSL\-VPN server. For procedure, see [Creating an SSL-VPN server](https://docs.byteplus.com/en/docs/vpn/Creating-an-SSL-server-1).

<span id=".5pON5L2c6K-05piO"></span>
## Action description

The SSL\-VPN client certificate is a sub\-resource of the SSL\-VPN server. A new SSL\-VPN client certificate belongs to the same project as the SSL\-VPN server, which is selected at creation. You can only migrate the SSL\-VPN client certificate to another project with the SSL\-VPN server, but not migrate it separately.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the SSL VPN Client Certificates console](https://console.byteplus.com/vpn/sslClient). 

2. In the top menu bar, select a target region and project.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After selecting a project, you can only select an SSL\-VPN server from the specified project when creating an SSL\-VPN client certificate.   </div>
   

3. Click **Create SSL Client Certificate**. In the pop\-up dialog box, configure the SSL\-VPN client certificate.

   
   |Parameters |Explanation |Sample value |
   |---|---|---|
   |Name |Set the name for the SSL\-VPN client certificate. |Client\-01 |
   |SSL server |Select the SSL\-VPN server that you want to associate the SSL\-VPN client certificate with. |Server\-01 |
   |**Advanced option** |||
   |Tags |A tag consists of two parts: a tag key (Key) and a tag value (Value), which can be used to classify and search the SSL\-VPN client certificate. [Learn more](https://docs.byteplus.com/en/docs/vpn/Tag-management)<br><br><br>* Click **Add tag** to add multiple tags as needed. You can add up to 20 tags per action. Each SSL\-VPN client certificate can have up to 50 tags.<br><br>* Keys of multiple tags on the same SSL\-VPN client certificates must be unique, and each Key can have only one Value.<br><br>* The Key and the Value are case\-sensitive. For example, the Key=tag and the Key=Tag are two different Keys. |key:test |
   

4. After configuration, click **OK** to complete the action.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

[Download the SSL-VPN client certificate](https://docs.byteplus.com/en/docs/vpn/Downloading-an-SSL-client-certificate): Download the SSL\-VPN client certificate file to your local folder to initiate a connection.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateSslVpnClientCert](https://docs.byteplus.com/en/docs/vpn/CreateSslVpnClientCert): Create an SSL\-VPN client certificate.
