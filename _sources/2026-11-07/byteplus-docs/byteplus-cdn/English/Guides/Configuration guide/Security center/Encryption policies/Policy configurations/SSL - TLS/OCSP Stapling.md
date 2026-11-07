---
title: "OCSP Stapling"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-ocsp-stapling-1"
---

OCSP Stapling is a feature provided by BytePlus CDN that improves TLS handshake efficiency and enhances user experience by allowing the server to cache the certificate's status. This document explains the concept, its benefits, and guides you through enabling it for your domain.

<span id="what-is-ocsp-stapling"></span>
## What is OCSP Stapling

OCSP stands for Online Certificate Status Protocol. During the TLS handshake phase, after obtaining a certificate, the client queries the CA (Certificate Authority) for the status of that certificate. The CA sends an OCSP response to the client.

Because each client queries the CA for the certificate's status after receiving it, this process can generate a high volume of queries to the CA. If the CA's response is slow, it can increase the TLS handshake time. To avoid this problem, OCSP Stapling was introduced. OCSP Stapling allows servers to periodically query the CA for the certificate status and cache this status. When the server sends the certificate to the client, it also sends the OCSP response for that certificate. The OCSP response is signed by the CA and therefore cannot be forged.

<span id="the-pros-and-cons-of-ocsp-stapling"></span>
## The Pros and Cons of OCSP Stapling

OCSP stapling significantly reduces the number of queries that clients send to CAs and also reduces the TLS handshake time. The downside is that the certificate status obtained by the client may not always be the latest. However, this can be mitigated by configuring the interval at which the server queries the CA for the certificate status.

<span id="enabling-ocsp-stapling"></span>
## Enabling OCSP Stapling

BytePlus CDN offers the "OCSP Stapling" feature, which can improve TLS handshake efficiency and enhance user experience.

<span id="prerequisites"></span>
### Prerequisites

To enable this configuration, your domain name must have Encryption enabled and [associated with a certificate](https://docs.byteplus.com/en/byteplus-cdn/docs/associate-domain-name-with-certificate).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a9c8d525b754c7e84bf44ba4fc7c2c9~tplv-goo7wpa0wc-image.image) </span>

<span id="steps"></span>
## Steps


1. Open the **OCSP Stapling** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to **Enable**.

3. Configure the setting as shown in the image.

4. After the configuration is complete, click **Save**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/425a4f64567847fca3eed055d9429e4b~tplv-goo7wpa0wc-image.image) </span>
