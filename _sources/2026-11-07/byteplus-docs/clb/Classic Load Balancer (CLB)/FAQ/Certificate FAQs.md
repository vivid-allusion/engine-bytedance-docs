---
title: "Certificate FAQs"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Certificate-faq"
---

<span id=".6K-B5Lmm5Yy65YiG5Zyw5Z-f5ZCX77yf"></span>
## Are certificates region\-specific?

BytePlus Certificate Center (recommended): Not region\-specific.

CLB\-side certificate management module (not recommended): Region\-specific. If the same certificate is to be used in multiple regions, you need to upload it separately in each region.

<span id=".5aaC5L2V5LiK5Lyg6K-B5Lmm77yf"></span>
## How to upload a certificate?

To facilitate unified certificate management, please upload certificates to the Certificate Center console. 

In the Certificate Center, you can perform certificate purchase, upload, renewal, and deletion in one stop.

<span id=".6LSf6L295Z2H6KGh5pSv5oyB5ZOq5Lqb57G75Z6L55qE6K-B5Lmm77yf"></span>
## What types of certificates does CLB support?

Currently, CLB only supports server certificates in PEM format, including both RSA and EC types.

If the server certificate format does not meet the requirements, you can convert it to the required PEM format by referring to the table below.


|Certificate format |Conversion instructions |
|---|---|
|CER/CRT |Then directly change the file extension to .pem (e.g., rename server.crt to server.pem).<br><br>For example: Rename the certificate file `server.crt` to `server.pem`. |
|PFX |PFX format certificates are often used on Windows Server. You can use the OpenSSL tool to convert to PEM format.<br><br><br>* Public key certificate: `openssl pkcs12 -in certname.pfx -nokeys -out publickey.pem`<br><br>* Private key certificate: `openssl pkcs12 -in certname.pfx -nocerts -out privatekey.pem -nodes` |
|P7B |P7B format certificates are often used on Windows Server and Tomcat servers. You can use the OpenSSL tool to convert to CER format, then simply change the file extension to .pem. <br><br>For both public key certificate and private key certificate, use the command: `openssl pkcs7 -print_certs -in incertificate.p7b -out outcertificate.cer`. |
|DER |DER format certificates are often used on Java platforms. You can use the OpenSSL tool to convert to PEM format.<br><br><br>* Public key certificate: `openssl x509 -inform der -in certname.der -out publickey.pem`<br><br>* Private key certificate: `openssl rsa -inform DER -outform PEM -in certname.der -out privatekey.pem` |


<span id=".6LSf6L295Z2H6KGh5pyN5Yqh5piv5ZCm5pSv5oyB5rOb5Z-f5ZCN6K-B5Lmm77yf"></span>
## Does the CLB service support wildcard domain certificates?

Supported. Just upload a wildcard domain certificate.

Pay attention to the wildcard rules for domain certificates. For example, a wildcard certificate for \*.support.com supports a.support.com and b.support.com, but does not support a.a.support.com. To support that, you would need to apply for a wildcard certificate for \*.a.support.com.

<span id=".5Li65LuA5LmI6YWN572u6K-B5Lmm5ZCO5LuN5Ye6546w5LiN5a6J5YWo5o-Q56S677yf"></span>
## Why does an insecure prompt still appear after configuring a certificate?

Possible causes:


* The domain name recorded in the certificate does not match the domain name accessed by the user. It is recommended to check the domain name recorded in the certificate.

* The domain name level does not match the certificate level, e.g., the domain name is at level 5 while the certificate is at level 4.

* The domain name is not registered.

* The certificate has expired.


For other cases, you can use the curl command (`curl` *accessed domain*) to troubleshoot based on the error message returned by the system.

<span id=".5L-u5pS55LiD5bGC55uR5ZCs5Zmo55qE6K-B5Lmm5Lya5a-86Ie05Lia5Yqh5Lit5pat5ZCX77yf"></span>
## Does modifying the certificate of a layer\-7 listener cause service interruption?

No. After modifying the certificate for a layer\-7 listener, the change takes effect immediately. Existing connections continue to use the original certificate, and business is unaffected; new connections use the new certificate.

<span id=".6K-B5Lmm6ZyA6KaB5LiK5Lyg5Yiw5ZCO56uv5pyN5Yqh5Zmo5ZCX77yf"></span>
## Do certificates need to be uploaded to backend servers?

No. The certificate is used to encrypt access requests between the client and the CLB, and does not need to be uploaded to backend servers.

<span id="ZMHQ5Cyj"></span>
## How to view the resources associated with a certificate?


* Certificates from the Certificate Center:

   1. Log in to the [Certificate Center console.](https://console.byteplus.com/certificate-center/ssl/certificate?showUploadCertDrawer=false)

   2. Click the name of the target certificate to go to the certificate details page, where you can view the resources associated with the certificate.

* Certificates managed by CLB certificate management

   * Log in to the [CLB Certificate Management console](https://console.byteplus.com/clb/region:clb+cn-beijing/Certificate?projectName=default).

   * Obtain the listeners associated with the certificate from the Associated Listener column on the right side of the target certificate.


<span id=".6K-B5Lmm6L-H5pyf5LqG5oCO5LmI5Yqe77yf"></span>
## What should I do if the certificate expires?

After a certificate expires, please replace it by following the instructions in [Modifying a listener certificate](https://docs.byteplus.com/en/docs/clb/Modifying-the-listener-certificate).

<span id=".6K-B5Lmm5Yiw5pyf5Lya6YCa55-l5ZCX77yf"></span>
## Will I be notified when a certificate expires?

There are differences between the BytePlus Certificate Center and the CLB\-side certificate management module:


* Certificate Center (recommended): Requires you to configure notifications. 

* CLB\-side certificate management module (not recommended): By default, sends notifications at 10:00 Beijing time on 30, 15, 7, and 1 day(s) before expiration, as well as on the expiration day itself, via in‑site messages, email, and SMS. Please update your certificate promptly after receiving the notification. If the certificate expires between 00:00 and 10:00 Beijing time, no notification will be sent on the expiration day.


<span id=".5aaC5L2V5Y-W5raI6K-B5Lmm5Yiw5pyf5o-Q6YaS77yf"></span>
## How to cancel certificate expiration reminders?

There are differences between the BytePlus Certificate Center and the CLB\-side certificate management module:


* Certificate Center (recommended): Supports managing expiration alerts for specific certificates. 

* CLB\-side certificate management module (not recommended): Subscribes you to certificate expiration reminders by default. If you do not wish to receive reminder messages, you can go to the Message Center console → Basic Message Reception Configuration, and remove notification methods for **Product expiration notification** as needed. 

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Product Expiration Notification includes expiration events for products other than CLB. Unsubscribing will disable such expiration notifications for all products. Please operate with caution.   </div>
