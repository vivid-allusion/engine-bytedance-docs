---
title: "[Important] Change in Let's Encrypt Certificate Chain"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/lets_encrypt_cert_chain_update_en"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In BytePlus CDN, if you have deployed a Let's Encrypt certificate for your domain to enable HTTPS access, please pay attention to this announcement.</div>


Dear BytePlus users,

The IdenTrust root certificate, which cross\-signs the intermediate certificate in Let's Encrypt's certificate chain, will expire on September 30, 2024. Additionally, starting from June 6, 2024, certificates issued by Let's Encrypt will rely solely on the self\-signed ISRG Root X1 as their trusted root certificate.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The validity period of Let's Encrypt certificates is 90 days.</div>


If your domain has deployed a Let's Encrypt certificate, only clients that trust ISRG Root X1, meaning the client's trust store includes ISRG Root X1, will be able to access your domain normally over HTTPS. Starting from September, we recommend that you monitor user feedback channels for any CDN access issues related to certificates.

The following common systems only trust ISRG Root X1 in specific versions:


* Android: Android 7.1.1 and above.

* Windows: Windows XP SP3 and above, Windows Server 2008 and above (except systems with automatic root certificate updates disabled).

* Java: Java SE 7u151, Java SE 8u141, Java SE 9 and above.

* macOS: macOS 10.12.1 Sierra and above.

* iOS: iOS 10.0 and above.


For a complete list of systems that trust ISRG Root X1, see the [Let's Encrypt Documentation - Platforms that Trust ISRG Root X1](https://letsencrypt.org/docs/certificate-compatibility/).

To resolve potential CDN access issues related to certificates, consider the following options:


*  **(Recommended) Deploy a paid certificate for the domain**: Paid certificates have broader compatibility and a validity period of one year, significantly reducing certificate maintenance costs compared to Let's Encrypt certificates, which are only valid for 90 days.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">BytePlus Certificate Center offers a variety of paid certificates for you to choose from, along with various purchasing discounts. <a href="https://www.byteplus.com/en/product/certificate-center">Learn more</a>.   </div>
   

* Upgrade the client's trust store: If the client's system version is old, it may not trust ISRG Root X1. To ensure the client can access your domain normally over HTTPS, upgrade the client's trust store to include the ISRG Root X1 certificate.


Thank you for your continued support. If you have any questions, please contact us.
