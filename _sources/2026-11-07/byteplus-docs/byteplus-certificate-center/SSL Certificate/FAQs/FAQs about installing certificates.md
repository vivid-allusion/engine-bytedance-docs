---
title: "FAQs about installing certificates"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-faqs-about-installing-certificates"
---

<span id="how-to-install-an-ssl-certificate"></span>
## How to install an SSL certificate

You can download the SSL certificate from the BytePlus Certificate Center console and then install the downloaded SSL certificate on the corresponding server. When downloading the certificate, you can choose the format of the certificate according to the type of server (such as Nginx, IIS, etc.). For more information, see [Downloading an SSL certificate](https://docs.byteplus.com/en/byteplus-certificate-center/docs/downloading-certificates).

<span id="why-does-the-browser-display-a-not-secure-warning-when-users-browse-my-website"></span>
## Why does the browser display a "Not Secure" warning when users browse my website?

There are several possible reasons for this issue:


* Your website does not have an installed SSL certificate, so the client's browser cannot establish a secure HTTPS connection with the website server.

* Your website has an incorrect or expired certificate. A correct and valid certificate must meet the following requirements:

   * The certificate is not expired or revoked.

   * The certificate authority is trusted.

   * The certificate protects the domain that matches your website's domain.

   * The certificate is installed correctly.


<span id="after-installing-a-new-certificate-following-the-expiration-of-the-old-certificate-why-does-the-browser-still-display-a-not-secure-warning"></span>
## After installing a new certificate following the expiration of the old certificate, why does the browser still display a "Not Secure" warning?

Once a certificate expires, it becomes invalid, and the browser no longer trusts the certificate, resulting in a "Not Secure" warning. If you have installed a new certificate on your website and the browser still displays a "Not Secure" warning, it is recommended to clear the browser cache and then revisit the website.

If your issue is not resolved, please check if you have correctly installed the new certificate.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">It is recommended to request a new certificate and complete the certificate replacement process within 30 days before the old certificate expires to prevent any impact on your business.</div>
