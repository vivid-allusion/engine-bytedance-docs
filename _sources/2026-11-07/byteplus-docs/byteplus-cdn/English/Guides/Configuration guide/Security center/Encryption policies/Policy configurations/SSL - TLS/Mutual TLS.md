---
title: "Mutual TLS"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/mtls_en-us"
---

This document describes how to configure Mutual TLS for a domain name in BytePlus CDN. Mutual TLS is suitable for scenarios that require strict identity verification, such as enterprise internal applications, where CDN allows only clients presenting an approved certificate to access the service. This further strengthens the security of communication between clients and CDN.

When this feature is enabled, CDN validates the client certificate during the SSL handshake. If the client certificate is not issued by the root CA certificate that you configured, CDN rejects the request.

To enable Mutual TLS, you must configure a root CA certificate in CDN. Both Single Certificate and Dual Certificate modes are supported.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In Dual Certificate mode, you can configure two root CA certificates that use different key algorithms, but the two certificates cannot share the same fingerprint.</div>


<span id="prerequisites"></span>
## Prerequisites

To enable Mutual TLS, you must have uploaded a root CA certificate to CDN\-hosted storage. For details, see [CDN-Hosted Certificates](https://docs.byteplus.com/en/docs/byteplus-cdn/cdn-cert-hosting_en-us).

<span id="steps"></span>
## Steps


1. Open the **Mutual TLS** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Toggle **Status** on.

3. Select **Source**. Only **CDN\-Hosted** is currently supported.

4. Set **Mode**.

   * **Single Certificate**: Configure one root CA certificate.

   * **Dual Certificate**: Configure two root CA certificates that use different key algorithms.

5. In the **Select CA Certificate** drop\-down list, select the root CA certificate you want to use. If the certificate you need is not in the list, click **Upload Certificate** below the drop\-down to upload one.

6. Click **Save**.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Any of the following situations causes the <strong>configuration to fail</strong>:</div>



* <div data-tips="true" data-tips-type="warning">HTTPS is not enabled for the domain name.</div>


* <div data-tips="true" data-tips-type="warning">The Mutual TLS mode does not match the server certificate mode. For example, Mutual TLS is in Dual Certificate mode while the server certificate is in Single Certificate mode.</div>


* <div data-tips="true" data-tips-type="warning">The key algorithms of the CA certificates configured for Mutual TLS do not cover the key algorithms of the server certificates. For example, both CA certificates configured for Mutual TLS use RSA, while the server certificates include one RSA and one ECC certificate — ECC traffic then has no matching CA certificate.</div>



<div data-tips="true" data-tips-type="warning">Under the following condition, <strong>client certificate validation fails</strong>:</div>



* <div data-tips="true" data-tips-type="warning">The certificate chain depth of the configured root CA certificate exceeds three levels. For example, the chain is <code>rootCA > iCA1 > iCA2 > client certificate</code>, where iCA1 and iCA2 are intermediate CAs.</div>



<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260604125708-264765382111.png) </span>
