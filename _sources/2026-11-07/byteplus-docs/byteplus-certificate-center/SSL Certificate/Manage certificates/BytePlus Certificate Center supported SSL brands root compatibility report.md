---
title: "BytePlus Certificate Center supported SSL brands root compatibility report"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/compatibility-test-report-for-brand-ssl-certificate-root-certificates"
---

<span id="csiahw9G"></span>
## Overview

When your certificate appears as untrusted or shows an incomplete certificate chain in certain environments, you can refer to this document to look up the support status of each brand's root certificates on platforms such as Windows, macOS, iOS, Android, and Java, and download or upload an adapted certificate chain accordingly.

All SSL certificates currently offered by **BytePlus Certificate Center**—including **RapidSSL**, **Secure Site**, **Secure Site Pro**, and **GeoTrust**—are issued under the **DigiCert root ecosystem**.


* **No action is required for most web scenarios**: For websites accessed through web browsers, root and intermediate certificates are already pre\-installed in the operating system or browser. You only need to deploy the complete certificate chain provided via the BytePlus console.

* **Special attention is required for non\-browser scenarios**: Environments such as Java clients, IoT/embedded devices, custom trust stores, and certificate pinning may require manual installation of root/intermediate certificates or replacement with compatible certificate chains.

* **DigiCert ecosystem**: Since 2023\-03\-08, the default issuance chain has been G2 / G3 and remains fully trusted. The legacy G1 root has been removed from the trust store by Chrome / Firefox starting 2026\-04\-15, which only affects custom chains still anchored on G1.


This report is maintained by BytePlus Certificate Center. Data sources include official root certificate compatibility statements from DigiCert and announcements from browser root programs like Chrome and Mozilla. For specific compatibility, validity periods, and distrust schedules, please refer to the actual certificate chains delivered by the console.

<span id="FMzfyKo3"></span>
## Certificate Chain and Compatibility Differences

A complete SSL/TLS trust chain consists of three parts, which the client validates from bottom to top:


* **End\-entity certificate (server certificate)** : Bound to your domain and deployed on the web server.

* **Intermediate certificate (Intermediate CA / ICA)** : Issued by the CA using the root private key, used to isolate and protect the root key while bridging the upper and lower layers.

* **Root certificate (Root CA)** : The final anchor of trust (trust anchor), preinstalled in trust stores of operating systems, browsers, JDKs, etc.


Whether a client can trust a certificate depends on whether the root certificate at the top of the chain is pre\-installed in its trust store. Compatibility differences arise because different operating systems, browser versions, JDK versions, mobile systems, and IoT firmware have varying pre\-installed root certificate lists and update strategies. Legacy systems may lack newer root certificates, and self\-maintained trust stores may not incorporate new roots promptly.

**Order of Precedence** (in case of conflicts, from highest to lowest): ① Latest official CA statements / compatibility reports → ② [Latest change announcements from BytePlus Certificate Center](https://docs.byteplus.com/en/docs/byteplus-certificate-center/TiGoiX) → ③ Actual certificate chain files delivered by the console → ④ This report.

<span id="YyDDwDEo"></span>
## Compatibility Quick Reference Matrix

The following table summarizes the current / target root system, key intermediates, and official references for each brand currently offered by the Certificate Center.


|**Brand** |**Support level / algorithms** |**Current / target root system** |**Key intermediate certificates** |**Official compatibility report** |**Root certificate download** |
|---|---|---|---|---|---|
|**Secure Site** |OV / EV · RSA / ECC |DigiCert Global Root G2 (RSA) / G3 (ECC) |DigiCert Global G2 TLS RSA SHA256 2020 CA1; G3 TLS ECC SHA384 2020 CA1; EV RSA CA G2 |[DigiCert Compatibility](https://knowledge.digicert.com/general-information/compatibility-of-digicert-trusted-root-certificates) |[DigiCert Root Library](https://www.digicert.com/kb/digicert-root-certificates.htm) |
|**Secure Site Pro** |OV / EV · RSA / ECC |DigiCert Global Root G2 (RSA) / G3 (ECC)<br><br> |Issuing CAs in the DigiCert Pro family (subject to what the console actually delivers) |[DigiCert Compatibility](https://knowledge.digicert.com/general-information/compatibility-of-digicert-trusted-root-certificates) |[DigiCert Root Library](https://www.digicert.com/kb/digicert-root-certificates.htm) |
|**GeoTrust** |DV / OV / EV · RSA / ECC |Follows the DigiCert ecosystem (G2 / G3) |GeoTrust TLS RSA CA G1; GeoTrust EV RSA CA G2 |[DigiCert Compatibility](https://knowledge.digicert.com/general-information/compatibility-of-digicert-trusted-root-certificates) |[DigiCert Root Library](https://www.digicert.com/kb/digicert-root-certificates.htm) |
|**RapidSSL** |DV · RSA / ECC |Follows the DigiCert ecosystem (G2 / G3) |RapidSSL TLS DV RSA Mixed SHA256 2020 CA\-1, etc. |[DigiCert Compatibility](https://knowledge.digicert.com/general-information/compatibility-of-digicert-trusted-root-certificates) |[DigiCert Root Library](https://www.digicert.com/kb/digicert-root-certificates.htm) |


<span id="jvAedrks"></span>
## Per\-Brand Root Certificate Compatibility Details

<span id="NYGjeVwJ"></span>
### DigiCert family (Secure Site / Secure Site Pro / GeoTrust / RapidSSL)

Brands in the DigiCert family share the DigiCert root hierarchy. According to the [official DigiCert statement](https://knowledge.digicert.com/general-information/compatibility-of-digicert-trusted-root-certificates), its trusted root certificates are compatible with all mainstream browsers and platforms. Since **2023\-03\-08**, the default issuance hierarchy for public TLS certificates has switched to the second\-generation G2 / G3 root and intermediate hierarchy; G1 certificates that were issued before that and are still within their validity period remain trusted until expiration.


|**Root certificate** |**Algorithm** |**Validity** |**Role** |**Status / Notes** |
|---|---|---|---|---|
|DigiCert Global Root G2 |RSA 2048 |2013 — 2038 |Current RSA trust anchor |✅ Default RSA issuance trust anchor, widely preinstalled in mainstream environments |
|DigiCert Global Root G3 |ECC P\-384 |2013 — 2038 |Current ECC trust anchor |✅ Default ECC issuance trust anchor |
|DigiCert Global Root CA (G1) |RSA 2048 |2006 — 2031 |Legacy DV / OV trust anchor |🔴 Removed from Chrome / Firefox trust stores starting 2026\-04\-15 |
|DigiCert High Assurance EV Root CA (G1) |RSA 2048 |2006 — 2031 |Legacy EV trust anchor |🔴 Distrusted on 2026\-04\-15 in sync with other G1 roots |


**Typical certificate chain (current):**  User domain certificate → DigiCert Global G2 TLS RSA SHA256 2020 CA1 (RSA) / DigiCert Global G3 TLS ECC SHA384 2020 CA1 (ECC) → corresponding G2 / G3 root.

**Compatibility tips:**  Standard web deployments using the complete chain from the console are unaffected by the G1 distrust. What needs special verification are scenarios where the certificate chain is still anchored on the legacy G1 root, or where G1 is hardcoded in a custom trust store or pinning configuration — these should switch to chains terminating at G2 / G3 before 2026\-04\-15. See [DigiCert root strategy](https://knowledge.digicert.com/alerts/digicert-root-strategy-aligning-with-industry-standards) and the [Cloudflare G1 distrust guide](https://developers.cloudflare.com/ssl/reference/migration-guides/digicert-g1-distrust/) for details.

In addition, DigiCert enabled two dedicated new public TLS roots on 2021\-01\-15: **DigiCert TLS RSA4096 Root G5** (RSA 4096) and **DigiCert TLS ECC P384 Root G5** (ECC P\-384), valid until 2046\-01\-14. The default issuance chain in BytePlus Certificate Center for the DigiCert family is currently still G2 / G3, with G5 positioned as the future migration target for public TLS. Customers focused on long\-term evolution or self\-maintained trust stores can take note in advance.

**Official references:**  [Compatibility statement](https://knowledge.digicert.com/general-information/compatibility-of-digicert-trusted-root-certificates) | [Root certificate download](https://www.digicert.com/kb/digicert-root-certificates.htm)

<span id="RpvlDARk"></span>
## Root Certificate Upgrade and Distrust Timeline

The following table summarizes root upgrade and distrust events for each brand in chronological order, with status evaluated as of the current date **2026\-06\-29**. All browser distrust events listed are public TLS trust policy changes that affect chains still anchored on the corresponding legacy roots; the current chains delivered by BytePlus Certificate Center by default are not affected.


|**Date** |**Brand / system** |**Event** |**Status** |
|---|---|---|---|
|2023\-03\-08 |DigiCert family |Default issuance chain upgraded to the G2 / G3 hierarchy |✅ In effect |
|From 2024\-11\-11 |Entrust |Chrome / Apple / Mozilla progressively stop trusting newly issued Entrust public TLS certificates |✅ In effect |
|2025\-05\-12 |DigiCert legacy compatibility anchor |Baltimore CyberTrust Root has expired |🔴 Expired |
|2026\-04\-15 |DigiCert family |G1 legacy roots (Global Root CA, High Assurance EV Root, etc.) removed from Chrome / Firefox trust stores |✅ In effect |


Compatibility versions, validity periods, and distrust timelines in this report all come from official CA statements and browser root program announcements, and will be updated continuously as the official sources are updated. For exact details, please refer to the latest official statements from the corresponding brand and to the certificate chain actually delivered by the console. If you need further confirmation, you can [submit a ticket](https://console.byteplus.com/workorder/create) to contact us.
