---
title: "Notice: Let's Encrypt root certificate update"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/-notice-lets-encrypt-root-certificate-update"
---

Dear BytePlus Certificate Center Users,

Let's Encrypt's original cross\-sign root certificate IdenTrust will expire on **September 30, 2024**, and its self\-signed root certificate ISRG Root X1 will become the only trusted root certificate for RSA certificates.

If your application is using Let's Encrypt certificates, we strongly recommend that you check the compatibility of ISRG Root X1 with the client platform in a timely manner. Since ISRG Root X1 is not yet widely used, if the client platform does not trust ISRG Root X1, HTTPS services may become unavailable.

For example, the following common systems are **compatible** with ISRG Root X1 only in certain versions and above:


* **Android ≥ 7.1.1**

* **Windows ≥ XP SP3, Server 2008** (unless **Automatic Root Certificate Updates** have been disabled)

* **Java ≥ 7u151, 8u141, 9+** 


For more information, see [Let's Encrypt Documentation - Platforms that Trust ISRG Root X1](https://letsencrypt.org/docs/certificate-compatibility/#platforms-that-trust-isrg-root-x1).

For client platform incompatibility issues, you can take the following measures:


*  **(Recommended) Upgrade to a paid certificate**: For higher protection, it is recommended that you upgrade your current Let's Encrypt certificate to a paid certificate. Paid certificates have wider compatibility and are valid for one year, which greatly saves certificate maintenance costs compared to Let's Encrypt certificates that are only valid for 90 days.

* Upgrade client truststore: If you want to continue using Let's Encrypt certificates, you must upgrade the truststore of clients connecting to your website or application to include the self\-signed ISRG Root X1 to prevent impact.

* Pay attention to user feedback: It is recommended that you monitor support channels for any feedback related to certificate warnings or access issues.


Thank you for your support and attention to BytePlus Certificate Center. Should you have any questions, please feel free to communicate with us at any time.
