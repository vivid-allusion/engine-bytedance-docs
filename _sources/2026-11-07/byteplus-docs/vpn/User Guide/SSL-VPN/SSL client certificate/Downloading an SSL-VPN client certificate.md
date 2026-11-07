---
title: "Downloading an SSL-VPN client certificate"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Downloading-an-SSL-client-certificate"
---

You must load SSL\-VPN client certificates to your SSL\-VPN clients before connecting SSL\-VPN. This topic describes how to download an SSL\-VPN client certificate.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Create an SSL\-VPN client certificate. For procedure, see [Creating an SSL-VPN client certificate](https://docs.byteplus.com/en/docs/vpn/Creating-an-SSL-client-certificate).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the SSL VPN Client Certificates console](https://console.byteplus.com/vpn/sslClient).

2. In the top menu bar, select a target region and project.

3. In the SSL\-VPN client certificate list, click **Download configuration** in the **Actions** column of the target SSL\-VPN client certificate.

4. In the pop\-up dialog box, select the format of the SSL\-VPN client certificate, supporting .zip and .ovpn formats.

   *  **.zip (default)** 

      * A `.zip` package containing the SSL\-VPN client configuration and certificate collection.

      * If the downloaded certificate is used for SSL\-VPN connections on a MAC client, a Windows client, or a Linux client, this format is recommended.

      * After downloading, you can find a .zip file prefixed with certs_vsc on the lower\-left corner of the page. That is the client certificate. The .zip file of client certificate contains four files.

   *  **.ovpn**

      * A file merging the SSL\-VPN client configuration and certificate information.

      * If the downloaded certificate is used for SSL\-VPN connections on an iOS or Android client, this format is recommended. After downloading, you can directly use the certificate on an iOS client to initiate an SSL\-VPN connection.

&nbsp;

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you need to use the downloaded .zip file for an iOS or Android client, you can merge the certificate files and then use the merged file on the iOS client. For specific actions, see <a href="https://docs.byteplus.com/en/docs/vpn/Merging-client-certificates">Merging client certificates</a>.   </div>
   

<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next


* [Configure a client](https://docs.byteplus.com/en/docs/vpn/Configuring-the-client): After obtaining the SSL\-VPN client certificate, you can use it to configure your client device.

* [Modify an SSL-VPN client certificate](https://docs.byteplus.com/en/docs/vpn/modify-the-ssl-client-certificate): If you are using the Pritunl client to connect, you need to modify the downloaded configuration file before initiating the connection.
