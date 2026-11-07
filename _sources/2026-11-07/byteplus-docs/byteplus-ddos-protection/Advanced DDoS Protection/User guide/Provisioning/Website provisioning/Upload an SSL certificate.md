---
title: "Upload an SSL certificate"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-uploading-an-ssl-certificate"
---

To enable HTTPS for your domain names protected by Advanced DDoS Protection, you must upload an SSL certificate. This guide provides step\-by\-step instructions on how to upload your certificate through the console.

<span id="2bffb44f"></span>
## Background information

An SSL certificate is a data file hosted in a website's origin server. It enables SSL/TLS encryption and contains the website's public key, identity, and associated information. Clients attempting to communicate with the origin server use this file to access the public key and authenticate the server's identity. The corresponding private key remains confidential and secure.

<span id="9cbbae72"></span>
## Before you begin


* Add one or more domain name forwarding rules and HTTPS is set as the protocol type.

* A valid certificate file in PEM format.


<span id="8cd18b1b"></span>
## Precautions

Please be aware of the expiration date of your certificate. If the certificate you have uploaded is nearing its expiration, it is crucial to update it promptly. Once updated, apply the renewed certificate to the respective domain name through the Advanced DDoS Protection console. This will prevent any potential business disruptions caused by expired certificates.

<span id="04f4563d"></span>
## Procedure


1. Log in to the [BytePlus Advanced DDoS Protection Console](https://console.byteplus.com/ddos-protection/advance/instances).

2. In the left\-side navigation pane, choose **Advanced DDoS Protection** \> **Provisioning**.

3. Choose **Website config** tab, and click **Certificate management**.

4. Click **Upload certificate**, and enter your certificate information.

   
   |Configuration |Description |
   |---|---|
   |Certificate name |The certificate name should contain 5 to 100 characters. It cannot start with a digit or dash (\-), and can only contain letters, digits, underscores (_), and dashes (\-). |
   |Certificate description |The certificate description supports no more than 255 characters. It cannot start with a digit or dash (\-), and can only contain letters, digits, underscores (_), and dashes (\-). |
   |Public key certificate |The certificate file procured from your Certificate Authority (CA) typically includes your public key certificate and the intermediate CA's certificate. These two components collectively form what is known as the "certificate chain". When uploading the certificate, it is imperative to upload the entire certificate chain to ensure proper functionality.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">There should be no blank lines between certificates.</div><br><br><br><br>* Format requirements<br><br>   ```Plain```<br>```   -----BEGIN CERTIFICATE-----```<br>```   Public key certificate of your server (BASE64 encoding)```<br>```   -----END CERTIFICATE-----```<br>```   -----BEGIN CERTIFICATE-----```<br>```   Public key certificate of intermediate CA (BASE64 encoding)```<br>```   ----BEGIN CERTIFICATE-----```<br>```   ```<br>   <br><br>* Example<br><br>   ```Plain```<br>```   -----BEGIN CERTIFICATE-----```<br>```   ****gjCCA2qgAwIBAgIQC5x5K4Yr3DdZJVClIoMOfjANBgkqhkiG9w0BAQsFADBu```<br>```   ****CQYDVQQGEwJVUzEVMBMGA1UEChMMRGlnaUNlcnQgSW5jMRkwFwYDVQQLExB3```<br>```   ****ZGlnaWNlcnQuY29tMS0wKwYDVQQDEyRFbmNyeXB0aW9uIEV2ZXJ5d2hlcmUg```<br>```   -----END CERTIFICATE-----```<br>```   -----BEGIN CERTIFICATE-----```<br>```   ****qjCCA5KgAwIBAgIQDeD/te5iy2EQn2CMnO1e0zANBgkqhkiG9w0BAQsFADBh```<br>```   ****CQYDVQQGEwJVUzEVMBMGA1UEChMMRGlnaUNlcnQgSW5jMRkwFwYDVQQLExB3```<br>```   ****ZGlnaWNlcnQuY29tMSAwHgYDVQQDExdEaWdpQ2VydCBHbG9iYWwgUm9vdCBH```<br>```   ----BEGIN CERTIFICATE-----```<br>```   ```<br>    |
   |Private key certificate |The format of private key certificates is as follows, there should be no blank lines between certificates.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">There should be no blank lines between certificates.</div><br><br><br><br>* Format requirements<br><br>   ```Plain```<br>```   -----BEGIN RSA PRIVATE KEY-----```<br>```   Certificate private key (BASE64 encoding)```<br>```   -----END RSA PRIVATE KEY-----```<br>```   ```<br>```   Or```<br>```   ```<br>```   -----BEGIN RSA PRIVATE KEY-----```<br>```   Certificate private key (BASE64 encoding)```<br>```   -----END RSA PRIVATE KEY-----```<br>```   ```<br>   <br><br>* Example<br><br>   ```Plain```<br>```   -----BEGIN RSA PRIVATE KEY-----```<br>```   ****owIBAAKCAQEAummRpZTzEY+BmqDOoUJBXEjH3vrS3REgWyh05YD+F9xxLBn1```<br>```   ****++DTx/uQIIe/cm/tCQVTgI0/McxNRSb1gNp8rrDW2MJ7mgW7JLlgWkmjdHXZ```<br>```   ****i5weOm2xIQ4CXz4heroNGlgJZB46uM+EeJ+ZdfRYA6h612xra0v7JcCiAgkc```<br>```   -----END RSA PRIVATE KEY-----```<br>```   ```<br>    |
   

5. Click **Save**.


<span id="3a525eff"></span>
## Related operations

On the **Certificate management** page, you can also conduct the following operations.


* Check the associated domain name and expiration time of your certificate.

* Click **View** to examine your certificate's details.

* Click **Edit** to modify the **Certificate description**, **Public key certificate**, or **Private key certificate**.

* Click **Delete** to remove the certificate you do not need anymore.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Removing the certificate being applied may disrupt the resolution of the associated domain's HTTPS service. Prior to deletion, it is advisable to replace the certificate assigned to the corresponding domain to prevent potential issues.   </div>
