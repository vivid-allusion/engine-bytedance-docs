---
title: "Convert certificate format"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Converting-certificate-formats"
---

ALB only supports uploading PEM format certificates; other formats must be converted to PEM format certificates. This article introduces common methods to convert other certificate formats to PEM format certificates.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The common third\-party conversion tool is OpenSSL; use it as needed.</div>


<span id=".Y2VyLWNydC3moLzlvI_or4HkuabovazmjaLkuLotcGVtLeagvOW8jw=="></span>
## Convert CER / CRT format certificates to PEM format

You can convert CER and CRT format certificates to PEM format by modifying the certificate file extension. For example, rename the `server.crt` certificate file to `server.pem`.

<span id=".cGZ4LeagvOW8j-ivgeS5pui9rOaNouS4ui1wZW0t5qC85byP"></span>
## Convert PFX format certificates to PEM format

PFX format certificates usually appear on Windows Server servers; you can use the OpenSSL tool to convert PFX format certificates to PEM format.


* Certificate conversion: convert `certname.pfx` to `cert.pem` file.

   ```json
    openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
   ```
   

* Private key conversion: Convert `certname.pfx` to `key.pem` file.

   ```json
   openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">certname.pfx: PFX format certificate file.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">cert.pem: public key file.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">key.pem: private key file.   </div>
   

<span id=".cDdiLeagvOW8j-ivgeS5pui9rOaNouS4ui1wZW0t5qC85byP"></span>
## Convert P7B format certificate to PEM format

P7B format certificates are usually found on Windows Server and Tomcat servers. You can use the OpenSSL tool to convert the certificate format. The steps are as follows:


1. Convert P7B format certificate to CER format certificate.

   ```json
   openssl pkcs7 -print_certs -in incertificate.p7b -out outcertificate.cer
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">incertificate.p7b: P7B format certificate file.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">outcertificate.cer: CER format certificate file.   </div>
   

2. Retain the certificate content in the CER file starting with "\-\-\-\-\-BEGIN CERTIFICATE\-\-\-\-\-" and ending with "\-\-\-\-\-END CERTIFICATE\-\-\-\-\-".

3. Rename the modified `outcertificate.cer` certificate file extension directly to `outcertificate.pem`.


<span id=".ZGVyLeagvOW8j-ivgeS5pui9rOaNouS4ui1wZW0t5qC85byP"></span>
## Convert DER format certificate to PEM format

Certificates in DER format usually appear on the Java platform. You can convert DER format certificates to PEM format using the OpenSSL tool.


* Certificate conversion: convert `certificate.der` to `certificate.pem` file.

   ```json
    openssl x509 -inform der -in certificate.der -out certificate.pem
   ```
   

* Private key conversion: convert `privatekey.der` to `privatekey.pem` file.

   ```json
   openssl rsa -inform DER -outform PEM -in privatekey.der -out privatekey.pem
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">certificate.der: DER format certificate file.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">certificate.pem: public key file.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">privatekey.pem: private key file.   </div>
