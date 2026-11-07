---
title: "Downloading an SSL certificate"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-downloading-certificates"
---

After the CA issues an SSL certificate for you, you can download the issued certificate from the BytePlus Certificate Center console and then install the certificate in the environment where you want to use it. For example, you can install the certificate on a web server. Only when the SSL certificate is installed correctly, HTTPS can be enabled.

<span id="prerequisites"></span>
## Prerequisites

You have completed one of the following operations:


* You have submitted an SSL certificate request through BytePlus Certificate Center, and the SSL certificate has been issued. For relevant operations, please refer to [Requesting an SSL certificate](https://docs.byteplus.com/byteplus-certificate-center/docs/requesting-a-certificate).

* You have uploaded an SSL certificate from a third\-party certificate platform to BytePlus Certificate Center. For relevant operations, please refer to [Uploading an SSL certificate](https://docs.byteplus.com/en/byteplus-certificate-center/docs/uploading-an-ssl-certificate).


<span id="procedure"></span>
## Procedure


1. Log on to the [BytePlus Certificate Center console](https://console.byteplus.com/certificate-center).

2. In the left navigation pane, choose **SSL Certificate** \> **Certificates**.

3. In the certificate list, find your certificate and click **Download** in the **Actions** column.

4. In the **Download** dialog box, click the corresponding **Download** button based on the type of your web server.

   Different web servers have different requirements for certificate formats. To facilitate certificate installation, BytePlus Certificate Center provides multiple download options. You can find the corresponding download button based on your server type. The downloaded certificate is in a format that meets the requirements of the corresponding server. For more information, please refer to [Certificate format description](https://docs.byteplus.com/en/docs/29/8587#certificate-format-description).

5. Follow the on\-screen instructions to complete the Account Protection verification.

   Account Protection is a security measure for BytePlus accounts that requires you to perform a second identity verification when conducting sensitive operations. Downloading an SSL certificate is a sensitive operation. If you have enabled **Account protection**, you need to complete the second identity verification according to the on\-screen instructions.

   The methods for second identity verification include phone number verification, MFA verification, etc. The specific method used depends on the Security Settings of your account.

   After you complete the above steps, the certificate package will be automatically downloaded to the default download path of your browser.

6. Extract the downloaded certificate package.

   After extraction, you will obtain the corresponding certificate files.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the following cases, the certificate package contains the private key file:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You selected to generate the CSR automatically when submitting the certificate request.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You uploaded the private key to BytePlus Certificate Center when uploading the certificate.   </div>
   


<span id="installing-the-certificate-on-a-web-server"></span>
## Installing the certificate on a web server

After obtaining the SSL certificate, you need to install the certificate in the corresponding environment for it to take effect. The requirements and configurations for installing the certificate on different environments are different.

We recommend that you consult the official documentation of the corresponding service to find out how to implement SSL/TLS.

<span id="certificate-format-description"></span>
## Certificate format description

You can download certificate packages compatible with the following servers from the BytePlus Certificate Center console:


|Server type |Certificate package contents |
|---|---|
|**Apache** |Certificate chain (.crt) and certificate (.crt). |
|**Nginx** |Certificate (.pem). The certificate file contains the complete certificate chain. |
|**IIS** |Certificate (.pfx). The certificate is password protected. |
|**Tomcat (PFX format)**  |Certificate (.pfx). The certificate is password protected. |
|**Tomcat (JKS format)**  |Certificate (.jks). The certificate is password protected. |
|**Other** |Certificate (.pem) and certificate (.crt). The certificate file contains the complete certificate chain. |
|**Root certificate** |Root certificate (.crt). |
