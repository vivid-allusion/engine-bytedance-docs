---
title: "Certificate overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Certificate-Overview"
---

When configuring an HTTPS listener, you need to attach a certificate to the listener. ALB supports uploading server certificates and CA certificates to the console for separate management of uploaded certificates. When configuring an HTTPS listener, you can easily select an uploaded certificate from a dropdown menu.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">ALB supports uploading certificates purchased on <a href="https://docs.byteplus.com/en/docs/6638/118049">BytePlus</a> and certificates issued by third parties.</div>


<span id=".6K-B5Lmm57G75Z6L"></span>
## Certificate type

ALB supports two types of certificates, as detailed below:


* Server certificate: In HTTPS one\-way authentication, the listener must attach a server certificate for the client to verify the server's trustworthiness.

* CA certificate: In HTTPS mutual authentication, the listener attaches both the server certificate and a CA certificate. This means that in addition to the client verifying the server, the server also verifies the client’s trustworthiness. mutual authentication provides higher data transmission security.


<span id=".6K-B5Lmm5qC85byP"></span>
## certificate format

The ALB console only supports uploading certificates and private keys in PEM format. When creating a certificate, you can directly enter the certificate content or upload the certificate file.

<span id=".5YWs6ZKl6K-B5Lmm5qC85byP"></span>
### public key certificate format

**basic format**


* Starts with “\-\-\-\-\-BEGIN CERTIFICATE\-\-\-\-\-” and ends with “\-\-\-\-\-END CERTIFICATE\-\-\-\-\-.”

* 64 characters per line, with no more than 64 characters on the last line.

* No blank lines are allowed between certificates.


**certificate chain**

The certificate file obtained from the certificate authority usually includes your certificate and certificates issued by intermediate authorities, which together form the certificate chain. When uploading certificates, ensure the complete certificate chain is uploaded.


* Open all \*.PEM format certificate files with a text editor, placing the server certificate first, followed by the intermediate certificates.

* No blank lines are allowed between certificates.

* Please refer to the intermediate agency's certificate rules description.


The common formats for public key certificates are shown below:

<span id=".56eB6ZKl6K-B5Lmm5qC85byP"></span>
### Private key certificate format

**Basic format**


* Starts with “\-\-\-\-\-BEGIN RSA PRIVATE KEY\-\-\-\-\-” and ends with “\-\-\-\-\-END RSA PRIVATE KEY\-\-\-\-\-.”

* Each line contains 64 characters, except the last line which has fewer than 64 characters.

* No blank lines are allowed between private keys.


Common formats of private key certificates are shown in the figure below:

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The HTTP listener does not support one\-way authentication or mutual authentication.

* Certificates uploaded to the ALB console can be attached to multiple ALB instance listeners during listener configuration.

* ALB supports PEM format certificates. Other certificate formats must be converted to PEM format before uploading to the ALB console.

* ALB checks the validity period of certificates. Before expiration, the system sends notifications through internal messages, email, and SMS. Please check them carefully.
