---
title: "Creating and downloading an SSL-VPN client certificate"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Creating-and-downloading-an-SSL-client-certificate"
---

This topic describes how to quickly create a client and download the client certificate locally.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have created a VPN gateway and an SSL server. For details, see [Creating a VPN gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-VPN-gateway-1) and [Creating an SSL-VPN server](https://docs.byteplus.com/en/docs/vpn/Creating-an-SSL-server).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5Yib5bu6U1NM5a6i5oi356uv6K-B5Lmm"></span>
### Creating an SSL VPN client certificate


1. Log in to [the SSL VPN Client Certificates console](https://console.byteplus.com/vpn/sslClient).

2. In the top menu bar, select a target region and project.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After selecting a project, you can only select an SSL VPN server from the specified project when creating an SSL VPN client certificate.   </div>
   

3. On the SSL client certificate page, click **Create SSL Client Certificate**, and configure the SSL client certificate in the pop\-up dialog box.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Name |Set the SSL client certificate name. |Client\-test |
   |Account |This parameter must be configured when logging in from the O&M\-side, but is not displayed on the tenant\-side. Select the account of the SSL VPN client certificate. The created VPN gateway can only be used by this account and cannot be migrated. |account1 |
   |SSL server |Select the SSL server to associate the SSL client certificate with. |Server\-test |
   

4. After configuration, click **OK** to complete the action.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The newly created SSL client certificate belongs to the same project as the selected SSL server during creation.   </div>
   

<span id=".5LiL6L295a6i5oi356uv6K-B5Lmm"></span>
### Download client certificate

After successfully creating the SSL client certificate, you can directly download the client certificate on the current page:


1. On the SSL client certificate page, in the SSL client certificate list, click **Download configuration** in the **Actions** column of the target SSL client certificate.

2. Select the certificate format to download according to the client.

   * `.zip` format: for Windows, Mac, Linux, and other clients. The `.zip` file starting with **certs_vsc** is the client certificate. Here, the downloaded client certificate is assumed to be named **certs_vsc\-2feuoxsyxxxxxybovbq.zip**.

   * `.ovpn` format: for clients such as iOS and Android, files starting with **certs_vsc** and ending with `.ovpn` are client certificates. Here, it is assumed the downloaded client certificate is named **certs_vsc\-2fen9va5qgpxxxxxx67cjgq.ovpn**.


<span id=".5ZCO572u5pON5L2c"></span>
## What to do next


* [Configure a client](https://docs.byteplus.com/en/docs/vpn/Configuring-the-client)

* [Test connectivity](https://docs.byteplus.com/en/docs/vpn/Testing-connectivity1)
