---
title: "Renewing an SSL certificate"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-renew-ssl-certificate"
---

SSL certificates have a validity period of [199 days](https://docs.byteplus.com/en/docs/byteplus-certificate-center/notice-on-shortening-of-ssl-certificate-validity-period). After the SSL certificate expires, it will no longer protect your website, resulting in users being prompted with a site security warning when accessing the website. Therefore, you must request a new certificate (commonly known as "certificate renewal") and replace the old certificate installed on the server before the old certificate expires. This will ensure that your website continues to be protected by the new SSL certificate.

<span id="renewal-restrictions"></span>
## Renewal restrictions


* Only SSL certificates purchased through BytePlus Certificate Center support renewal.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Free certificates and SSL certificates that you upload to Certificate Center do not support renewal.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When a free certificate expires, you can apply for a new free certificate to replace the old one.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When an uploaded certificate expires, you can purchase a new certificate from BytePlus Certificate Center.   </div>
   

* Renewal can only be performed within 30 days before the certificate expires.

   Within 30 days before certificate expiration, you can perform the **Renew** operation for the certificate in the BytePlus Certificate Center console. This operation means ordering a new certificate based on the information from the old certificate.

   * When you request a new certificate, BytePlus Certificate Center automatically fills in the same request information as the old certificate, so you don't need to fill it in again.

   * The CA supports transferring the remaining valid time from the old certificate to the new certificate.

   > Example:

   > Suppose the old certificate expires on February 28, 2025. You ordered a renewal certificate on February 10, and the new certificate was issued on the same day. In this case, the new certificate will be valid until September 14, 2025.   
   

<span id="operation-steps"></span>
## Operation steps


1. Log on to the [BytePlus Certificate Center console](https://console.byteplus.com/certificate-center).

2. In the left navigation pane, select **SSL Certificate** \> **Certificates**.

3. Above the certificate list, click the **Expire soon (within 30 days)**  card, then use the **Certificate Instance** filter to find certificates of type **Paid certificate**.

4. Locate the certificate to be renewed and click **Renew** in the **Actions** column.

5. On the **Renew certificate** page, review the certificate information and click **Submit**.

6. Confirm the order and complete the payment.

   After you complete the payment, a new certificate will appear in the certificate list.

   The new certificate obtained through renewal is associated with the old certificate. You can click the **View associated certificates** button in the **Actions** column of the old certificate to view the association between the certificates.

7. Click the ID of the new certificate and follow the prompts in the **Order progress** section to complete the verification of certificate request information. For more information, please refer to [Demonstrating control over domain](https://docs.byteplus.com/byteplus-certificate-center/docs/conducting-domain-validation).


After the new certificate is issued, you need to replace the old certificate with the new certificate, such as installing the new certificate on your web server or deploying it to your BytePlus cloud services.

<span id="related-faq"></span>
## Related FAQ

<span id="why-can-t-i-directly-order-a-certificate-with-a-validity-period-of-multiple-years"></span>
### Why can't I directly order a certificate with a validity period of multiple years?

Due to the policies of Apple and Google root stores, as well as the latest baseline requirements from the CA/Browser Forum, the maximum validity period for SSL certificates issued by publicly trusted CAs (such as DigiCert, GlobalSign, etc.) has been progressively shortened. Currently, the validity for certain SSL certificates has been adjusted from 1 year to 199 days, with further reductions expected in the future. For detailed information, please refer to the [Notice on SSL Certificate Validity Shortening](https://docs.byteplus.com/en/docs/byteplus-certificate-center/notice-on-shortening-of-ssl-certificate-validity-period).

<span id="how-can-i-view-the-validity-period-of-a-certificate"></span>
### How can I view the validity period of a certificate?

You can query the validity period of a certificate in the following ways:


* Method 1: Query through the console

   You can log in to the [BytePlus Certificate Center console](https://console.byteplus.com/certificate-center) and view the validity period of the certificate in the **Certificate management** list.

* Method 2: Access the website for querying

   If you have already installed the certificate on the server, you can use a browser to access the website and view the validity period of the certificate through the browser's certificate viewer.

   Taking Chrome browser as an example, the query steps are as follows:

   1. Enter the domain name in the address bar and access the website.

   2. Click the connection icon, and then click **Connection is secure**.

   3. Click **Certificate is valid**.

   4. Click the **Details** tab, and then view the **Validity** information in the **Certificate Fields**.

      The value of **Not After** represents the expiration time of the certificate.

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c52345f1b7121fdbc5763b1bf2717b29.png) </span>
