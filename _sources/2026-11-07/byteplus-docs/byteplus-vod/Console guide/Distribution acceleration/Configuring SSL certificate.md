---
title: "Configuring SSL certificate"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-configuring-ssl-certificates"
---

To use HTTPS for encrypted data transmission with your BytePlus VOD domain names, you must configure an SSL certificate. This guide provides step\-by\-step instructions on how to first add your certificate in the BytePlus Certificate Center and then associate it with a specific domain name within the VOD console.

<span id="8931bb30"></span>
## Prerequisites

Purchase a certificate from BytePlus Certificate Center or upload your own certificate to the BytePlus Certificate Center. See the following documents for details:


* [Creating an SSL Certificate Order](https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-creating-certificate-order)

* [Uploading an SSL certificate](https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-uploading-an-ssl-certificate)


<span id="1c21ccdd"></span>
## Configuring the SSL certificate for a domain name

To configure the SSL certificate for a domain name in the BytePlus VOD console, follow these steps:


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter the target space.

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Find the target domain name in the domain name list and click **Configure** in the **SSL certificate** column.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e547d31654f4b8997f0378c37d16f38~tplv-goo7wpa0wc-image.image) </span>

4. In the dialog box that appears, do the following:

   1. Enable HTTPS mode.

   2. Select a certificate from BytePlus Certificate Center.

   3. Click **OK**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f922645a91a04ba8b1577807eb857b4f~tplv-goo7wpa0wc-image.image) </span>

5. After the certificate configuration is completed, you can check the status and expiration time of the certificate. Here are the detailed explanations of the certificate statuses:

   * **Certificate running fine**: Indicates that there are more than 30 days remaining until the expiration date.

   * **Certificate about to expire**: Indicates that there are less than 30 days remaining until the expiration date.

   * **Certificate has expired**: Indicates that the certificate has already expired.
