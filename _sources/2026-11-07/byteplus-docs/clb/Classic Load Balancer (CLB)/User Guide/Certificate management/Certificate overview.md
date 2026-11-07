---
title: "Certificate overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Certificate-management-01"
---

When configuring an HTTPS listener, you need to attach an SSL certificate to the listener for SSL handshake negotiation, applicable to HTTPS one\-way authentication scenarios.

You can use either a self\-signed certificate or one issued by a third party. Advice is to use certificates issued by authoritative organizations, as self\-signed certificates may pose security risks.

## Upload SSL certificate

When creating an HTTPS listener in CLB, you can obtain SSL certificates from the BytePlus Certificate Center or CLB Certificate Management module.

|Name |Explanation |Certificate expiration notification |
|---|---|---|
|**BytePlus Certificate Center (recommended)**  |* To facilitate unified management of certificates for users, CLB has integrated with the Certificate Center. We recommend you upload the certificate via the [Certificate Center console](https://console.byteplus.com/certificate-center/ssl/overview?projectName=default).<br><br>* In the Certificate Center, you can perform one\-stop operations such as purchasing, uploading, renewing, and deleting certificates. |* The Certificate Center sends an expiration reminder 30, 15, 7, and 3 days before SSL certificate expiration.<br><br>* You can turn off expiration reminders for specified certificates. |
|CLB Certificate Management Module (not recommended) |* You can upload certificates to the CLB Certificate Management module.<br><br>* If the same certificate is used in multiple regions, upload it separately in each region. |* system default sends expiration reminders at 10:00 Beijing time 30, 15, 7, 1 day(s) before expiration and on the expiration day.<br><br>* If the expiration time is between 00:00 and 10:00 Beijing time, no notification will be sent on the expiration day.<br><br>* Turning off expiration reminders for specific certificates is not supported.  |

> Explanation

> The certificate management module on the CLB side operates independently from the Certificate Center, and SSL certificates do not synchronize automatically.

## Certificate requirements

CLB supports only PEM format certificates; please convert other formats to PEM. Before uploading, ensure your certificate, certificate chain, and private key comply with PEM format requirements.

**Certificate chain**: refers to the certificate file obtained from your certificate provider, which typically includes your own certificate and intermediate issuing authority certificates.

### Public key format requirements

**Certificates issued by root certificate authorities**

If your certificate is issued by a root certificate authority, the certificate you receive is unique. No additional certificates are required, and the configured site will be recognized as trusted by browsers and other access devices.

#### Certificate format

* Beginning with\-\-\-\-\-BEGIN CERTIFICATE\-\-\-\-\- and ending with\-\-\-\-\-END CERTIFICATE\-\-\-\-\-.

* Each line contains 64 characters, with the last line possibly shorter than 64 characters.

* Certificate content must not include spaces or empty lines.

**Certificates issued by intermediate authorities**

If your certificate is issued by an intermediate CA, the certificate file you receive will contain multiple certificates that need to be combined and uploaded together.

#### Certificate chain format

* The SSL certificate should be placed first, followed by the intermediate certificate, with no empty lines in between.

* Certificate content must not contain spaces.

* 64 characters per line. No blank lines or spaces are allowed between certificates.

#### Certificate chain example

```Plain Text
-----BEGIN CERTIFICATE-----
服务器公钥证书(BASE64编码) 
-----END CERTIFICATE----- 
-----BEGIN CERTIFICATE-----
中级签发机构公钥证书(BASE64编码)
-----END CERTIFICATE-----
```

### Private key format requirements

When creating an SSL certificate, you also need to upload the certificate's private key.

**RSA private key format requirements**

* Start with \-\-\-\-\-BEGIN RSA PRIVATE KEY\-\-\-\-\-and end with\-\-\-\-\-END RSA PRIVATE KEY\-\-\-\-\-.

* Each line contains 64 characters. There must be no blank lines between private keys. The last line can contain fewer than 64 characters.

If your private key format differs, convert it to a usable private key as follows:

```JSON
openssl rsa -in old_server_key.pem -out new_server_key.pem
```

**EC private key format requirements**

* Start with\-\-\-\-\-BEGIN EC PARAMETERS\-\-\-\-\- and end with\-\-\-\-\-END EC PARAMETERS\-\-\-\-\-.

* Each line contains 64 characters. Private keys must not have empty lines or spaces between them. The last line can be shorter than 64 characters.

If your private key format differs, convert it to an available private key as follows:

```JSON
openssl ec -in old_server_key.pem -out new_server_key.pem
```

#### EC private key example

```Plain Text
-----BEGIN EC PARAMETERS-----
证书私钥(BASE64编码)
-----END EC PARAMETERS-----
-----BEGIN EC PRIVATE KEY-----
证书私钥(BASE64编码)
-----END EC PRIVATE KEY-----
```
