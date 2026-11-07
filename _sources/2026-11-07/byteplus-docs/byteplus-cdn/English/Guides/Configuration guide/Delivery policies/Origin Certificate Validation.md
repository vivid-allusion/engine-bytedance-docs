---
title: "Origin Certificate Validation"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/origin-cert-verification_en-us"
---

The Origin Certificate Validation feature enhances security for HTTPS communication between BytePlus CDN and your origin server. By default, CDN does not validate the origin's certificate, creating a vulnerability for man\-in\-the\-middle attacks. When you enable this feature, CDN verifies the certificate's legitimacy, including its issuer, revocation status, and domain match. If validation fails after a retry, CDN blocks the request and returns a 504 error, ensuring content is only retrieved from a verified and secure origin. To use this feature, please [submit a ticket](https://console.byteplus.com/workorder/create).

By default, when CDN uses HTTPS to request files from an origin server, it does not validate the origin server's certificate. Although the communication between CDN and the origin server is encrypted, man\-in\-the\-middle attacks cannot be prevented.

If you have high security requirements for communication between CDN and the origin server, you can enable the "Origin Certificate Validation" feature. After you enable this feature, CDN validates the origin server certificate by checking criteria such as whether it has been revoked, was issued by a trusted CA, and matches the origin server domain. CDN has built\-in root certificates from common trusted CAs. If the origin server certificate fails validation, CDN performs an [origin request retry](https://docs.byteplus.com/en/docs/byteplus-cdn/origin_retry-en). If the certificate still fails validation on retry, CDN considers the origin server unreachable and responds to the user request with a 504 status code.

<span id="procedure"></span>
## Procedure


1. Open the **Origin Certificate Validation** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. In the **Origin Certificate Validation** module, enable the feature.

3. After completing the configuration, click **Submit**.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_96dacb06bffe1e5c162093f3e4bde4b7.png) </span>
