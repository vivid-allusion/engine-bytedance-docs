---
title: "Associate domain name with certificate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-associate-domain-name-with-certificate"
---

To enable HTTPS for your domain name, you must associate it with a valid certificate. This guide provides step\-by\-step instructions for associating a domain with a certificate for the first time, as well as how to update the association after renewing an existing certificate to ensure continuous service.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A domain name can only be associated with one certificate. A certificate can be associated with multiple domain names.</div>


<span id="steps"></span>
## Steps


1. Open the [Certificate Center](https://console.byteplus.com/cdn/cdn-bp/security/cert)[ page](https://console.byteplus.com/cdn/cdn-bp/security/cert).

2. Find the certificate to associate with your domain name.

   1. In the domain name search box at the top right of the certificate list, enter the domain name you need to associate with the certificate.

&nbsp;

      You must enter the complete domain name. After you enter the domain name, the list will display certificates that can be associated with that domain name.

   2. In the certificate list, find the certificate you want to associate.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3917d08ce6d4ebe8fc2021806073bc9~tplv-goo7wpa0wc-image.image) </span>

3. (Optional) Confirm whether your domain name is already associated with a certificate.

   1. In the certificate list, check if your domain name appears in the **Associated Domains** column.

   2. If it does not appear, your domain name is not yet associated with any certificate. Continue with the subsequent steps. If it does appear, confirm the following information:

      * Confirm whether the currently associated certificate is the correct one. If not, please continue with the subsequent steps to associate your domain name with a different certificate.

      * If it is correct, please confirm the status of the certificate. If the status is **Expired** or **Expiring**, renew the certificate promptly, and then refer to [Steps after Renewing a Certificate](https://docs.byteplus.com/en/docs/18/6608#steps-after-renewing-a-certificate).

4. In the **Actions** column for the certificate, click **Associate Domains.** 

5. On the **Associate Domain Names** page, refer to the following instructions to select your domain name, then click **OK**.

   * This page displays all domain names that can be associated with the certificate. These domains are organized into the following lists:

      * The **Associable Domain Names** list shows domain names that are not associated with any certificate. If your domain name is on this list, select your domain name to associate it with the certificate.

      * The **Domain Names Associated with a Certificate** list shows domain names that are already associated with a different certificate. If your domain name is on this list, select your domain name to associate it with this certificate and disassociate it from the previous one.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e8dcb07485c4c56b270266a6c93eae9~tplv-goo7wpa0wc-image.image" width="761px" /></div>


<span id="steps-after-renewing-a-certificate"></span>
## Steps after Renewing a Certificate

If the status of a certificate in the certificate list is **Expired** or **Expiring**, renew the certificate promptly.


* If you purchased the certificate from the BytePlus Certificate Center, you can also renew it there.

* If the certificate was uploaded to the BytePlus Certificate Center, you need to renew it at your certificate service provider.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Renewing a certificate does not extend the expiration date of the current one; instead, the CA will issue a new certificate to your domain name.</div>


* <div data-tips="true" data-tips-type="tip">If you renew your certificate at the BytePlus Certificate Center, the new certificate will appear in the certificate list. Otherwise, you need to export the new certificate from your certificate service provider and then import it on the <strong>Certificate Center</strong> page.</div>



After successful renewal, you need to associate your domain name with the new certificate.


1. On the **Certificate Center** page, find the new certificate.

2. In the **Actions** column for the certificate, click **Associate Domains**.

3. On the **Associate Domain Names** page, in the **Domain Names Associated with a Certificate** list, select your domain name, then click **OK**.
