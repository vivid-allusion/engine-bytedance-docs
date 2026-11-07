---
title: "Revoking an SSL certificate"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-revoking-an-ssl-certificate"
---

Revoking an SSL certificate means invalidating it before its scheduled expiration date. Once an SSL certificate is revoked, it cannot be used anymore. This article describes the methods for revoking an SSL certificate.

<span id="use-cases"></span>
## Use cases

During the validity period of an SSL certificate, if you have the following needs, it is recommended to submit a certificate revocation request to the Certificate Authority (CA). This can help prevent insecure situations such as certificate theft.


* The certificate request information is incorrect, but the certificate has been issued and you need to resubmit the certificate request.

* The certificate has been issued, but you need to replace the domain protected by the certificate.

* You no longer need to use the issued certificate.

* Due to security reasons (such as the private key of the certificate being compromised), the issued certificate is no longer used.


<span id="restrictions"></span>
## Restrictions

In the BytePlus Certificate Center console, you can only revoke certificates purchased through BytePlus Certificate Center. You cannot revoke certificates that you have uploaded.

<span id="precautions-before-operation"></span>
## Precautions before operation


* Once an SSL certificate is revoked, it cannot be used anymore. It is recommended to revoke the certificate only after confirming that it is no longer in use.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If your service is still using a revoked certificate, the service will be affected. For example, users will not be able to access your service or they will receive a "Not Secure" warning when accessing the service.   </div>
   

* Revoked SSL certificates cannot be restored. Please proceed with caution.


<span id="operation-steps"></span>
## Operation steps


1. Log on to the [BytePlus Certificate Center console](https://console.byteplus.com/certificate-center).

2. In the left navigation pane, choose **SSL Certificate** \> **Certificates**.

3. On the **Certificate management** page, find the certificate you plan to revoke, click the  **...**  in the **Actions** column, and then click **Revoke**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <strong>Revoke</strong> button only appears when the certificate status is <strong>Issued</strong>.   </div>
   

4. In the pop\-up dialog box, enter a revocation reason, and then click **Revoke**.

5. Follow the on\-screen instructions to complete the Account Protection verification.

   **Account protection** is a security measure for BytePlus accounts that requires you to perform a second identity verification when conducting sensitive operations. Revoking an SSL certificate is a sensitive operation. If you have enabled **Account protection**, you need to complete the second identity verification according to the on\-screen instructions.

   The methods for second identity verification include phone number verification, MFA verification, etc. The specific method used depends on the Security Settings of your account.


After you have completed the above steps, BytePlus Certificate Center will submit the certificate revocation request to the CA. At this time, the status of the corresponding certificate will change to **Revoking**.

After receiving the revocation request, the CA will revoke the corresponding SSL certificate. You can check the status of the certificate in the BytePlus Certificate Center console later. When the status of the certificate changes to **Revoked**, it means that the SSL certificate has been successfully revoked.
