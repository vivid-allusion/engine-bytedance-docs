---
title: "Creating an SSL certificate order"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-creating-certificate-order"
---

This article introduces the method of creating an SSL certificate order through the BytePlus Certificate Center.

<span id="background-information"></span>
## Background information

The SSL certificate service of the Certificate Center allows you to order SSL certificates from mainstream certificate authorities (CAs). To obtain an SSL certificate, you must first create an SSL certificate order and submit the certificate request to the CA. After the CA approves your certificate request, they will issue the certificate to you.

<span id="prerequisites"></span>
## Prerequisites

You have registered a BytePlus account.

<span id="procedure"></span>
## Procedure


1. Log on to the [BytePlus Certificate Center console](https://console.byteplus.com/certificate-center).

2. In the left navigation pane, select **SSL Certificate** \> **Certificates**.

3. Click **Purchase certificate**.

4. On the **Purchase certificate** page, complete the relevant configurations according to the [Configuration instructions](https://docs.byteplus.com/en/docs/29/8584#configuration-instructions), and then click **Buy now**.

5. Confirm your order and complete the payment.


After creating the order, you can view the corresponding certificate instance on the **Certificate management** page.

<span id="configuration-instructions"></span>
## Configuration instructions


|Category |Configuration item |Description |
|---|---|---|
|**Certificate information** |**Certificate type** |Select the type of the certificate. Options:<br><br><br>* **DV \| Domain Validation**: DV certificates have a medium level of trust and are suitable for personal and non\-commercial websites.<br><br>   For DV SSL certificate requests, the CA only verifies the ownership of the domain by the applicant. DV certificates are usually issued within a few hours.<br><br>* **OV \| Organization Validation**: OV certificates have a higher level of trust and are suitable for public\-facing commercial websites.<br><br>   For OV SSL certificate requests, the CA verifies not only the ownership of the domain by the applicant but also the authenticity of the organization. OV certificates are usually issued within 3 to 5 business days.<br><br>* **EV \| Extended Validation**: EV certificates have the highest level of trust and are suitable for websites handling sensitive information, such as e\-commerce or financial websites.<br><br>   For EV SSL certificate requests, the CA verifies not only the ownership of the domain by the applicant but also conducts a thorough examination of the organization. This examination includes checking relevant documents of the organization, confirming the identity of the applicant, and verifying the information through third\-party databases. EV certificates are usually issued within 7 to 10 business days. |
||**Certificate brand** |Select a certificate brand. Options:<br><br><br>* **RapidSSL**: A DV brand from DigiCert.<br><br>* **SecureSite**: An OV/EV brand from Digicert.<br><br>* **SecureSite Pro**: A high\-end OV/EV brand from Digicert.<br><br>* **GeoTrust**: A cost\-effective DV/OV/EV brand from Digicert.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Some brands only appear when you select specific <strong>Certificate type</strong>. If you don't find an option for a certain brand, it means that the brand does not provide certificates for the current <strong>Certificate type</strong>.</div><br> |
||**Domain type** |Select the type of domain protected by the certificate. Options:<br><br><br>* **Single domain (FQDN)** : Indicates that the certificate is used to protect a specific domain or an IP address. Examples: `example.com`, `www.example.com`, `1.XX.XX.1`.<br><br>* **Wildcard domain**: Indicates that the certificate is used to protect a wildcard domain. Example: `*.example.com`.<br><br>   A wildcard domain can match all subdomains of a domain. For example, `*.example.com` can match `a.example.com`, `b.example.com`, etc., but cannot match `a.b.example.com`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The hierarchy of the domain cannot exceed 100 levels. For the meaning of hierarchy, please refer to the following examples: The level of <code>example.com</code> is 2, and the level of <code>www.example.com</code> is 3.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Only some certificate brands support IP as the protected object.</div><br> |
||**Service duration** |Select the duration of your subscription to the SSL certificate service. Option: **199 days**.<br><br>Starting from February 10, 2026, all CAs will gradually stop accepting public TLS certificate requests with a validity greater than 199 days. For more details, see [Reduction in SSL Certificate Validity Period](https://docs.byteplus.com/en/docs/byteplus-certificate-center/notice-on-shortening-of-ssl-certificate-validity-period). |
||**Purchase method** |Select a purchase method. Options:<br><br><br>* **By domain**: Indicates that the certificate request is automatically submitted to the CA after the order is created.<br><br>   If you choose this method, you need to continue filling in the certificate request information on the current page. With this method, you can only order one certificate at a time, but the certificate issuance speed is faster.<br><br>* **By quantity**: Indicates that the certificate request will not be submitted to the CA automatically after the order is created.<br><br>   If you choose this method, you can select the quantity of certificates to make a bulk order. After completing the payment, you can go to the BytePlus Certificate Center console to manually submit certificate requests.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The certificate request information includes the <strong>Key algorithm</strong>, <strong>CSR from</strong>, <strong>Domain name</strong>, <strong>Information template</strong>, and <strong>Domain validation method</strong>. These configuration items only appear when the <strong>Purchase method</strong> is <strong>By domain</strong>. For more information on configuring the certificate request information, see <a href="https://docs.byteplus.com/byteplus-certificate-center/docs/requesting-a-certificate">Requesting an SSL certificate</a></div><br> |
||**Quantity** |Enter the quantity of certificates to order.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This configuration item only appears when the <strong>Purchase method</strong> is <strong>By quantity</strong>.</div><br> |
||**Remark** |Add a note to the certificate for future management. |
|**More options** |**Project** |Assign a [Resource project](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Overview) to the certificate(s). If your order contains multiple certificates, the project you specify will apply to all of them.<br><br>If you have never created any projects or modified the default project, the only option available for **Project** will be **default (Default project)** . |
||**Tag** |Add one or more tags (in key\-value pairs) to the certificate. Tags allow you to categorize, search, and control access to certificates from various dimensions, enhancing the flexibility of your resource management. |
|**Service agreement** |**Agreement** |Select this option to indicate that you have read and agree to the service terms of BytePluse Certificate Center. |
