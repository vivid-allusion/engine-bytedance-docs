---
title: "Requesting a free SSL certificate"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-request-free-ssl-certificate"
---

This article describes how to request a free certificate in the BytePlus Certificate Center.

<span id="background-information"></span>
## Background information

BytePlus Certificate Center provides you with free certificates from DigiCert EE.


* Free certificates are suitable for scenarios such as testing and personal websites. In formal environments, it is suggested to use a [paid certificate.](https://byteplus-console.byteintl.net/certificate-center/ssl/certificate/buy)

* Each BytePlus account can get a maximum of 20 free SSL certificates from DigiCert EE per calendar year.

* DigiCert EE free certificates can only be associated with a fully qualified domain name (FQDN).

* Free certificates do not support some domain name suffixes, including but not limited to .edu, .gov, .org, .jp, .pay, .bank, .live, and .nuclear, etc.


<span id="procedure"></span>
## Procedure

<span id="step-1-submitting-a-free-certificate-request"></span>
### Step 1: Submitting a free certificate request


1. Log on to the [BytePlus Certificate Center console](https://console.byteplus.com/certificate-center).

2. In the left navigation pane, select **SSL Certificate** \> **Certificates**.

3. On the **Certificate management** page, click **Request free certificate**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you hover over the <strong>Request free certificate</strong> button, you can view the number of free certificate quotas you currently have.   </div>
   

4. On the **Request free certificate** page, complete the parameter settings and click **Request**.

   For detailed descriptions of configuration items, refer to [Requesting an SSL certificate](https://docs.byteplus.com/byteplus-certificate-center/docs/requesting-a-certificate).


After you submit a free certificate request, BytePlus Certificate Center will automatically create a certificate instance. You can view the newly created certificate instance on the **Certificate management** page. The **Status** of the certificate instance is **Validating**.

Next, you need to complete domain ownership verification.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you choose <strong>DNS validation</strong> as the <strong>Domain validation method</strong> and your domain is using BytePlus DNS Suite for DNS service, the domain ownership verification will be automatically completed. You just need to wait patiently for the certificate to be issued. Free certificates are usually issued within a few hours.</div>


<span id="step-2-completing-domain-ownership-verification"></span>
### Step 2: Completing domain ownership verification


1. On the **Certificate management** page, find your certificate instance and click on its name.

2. In the **Order progress** section on the right side of the certificate details page, follow the instructions in the **Pending domain validation** section to complete the required configurations.

   For more information about domain ownership verification, refer to [Demonstrating control over domain](https://docs.byteplus.com/byteplus-certificate-center/docs/conducting-domain-validation).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the <strong>Pending domain validation</strong> section does not appear in <strong>Order progress</strong>, please wait for 5 minutes.   </div>
   

3. In the **Check your configuration** section, click **Check** to manually check if your configuration is accurate.


After confirming that your configuration is accurate, please wait patiently. The CA will periodically check your configuration. Once the CA confirms that you have completed the required configurations, the certificate will be issued. Free certificates are usually issued within a few hours.
