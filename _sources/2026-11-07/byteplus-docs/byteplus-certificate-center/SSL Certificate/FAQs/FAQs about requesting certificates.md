---
title: "FAQs about requesting certificates"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-faqs-about-requesting-certificates"
---

<span id="how-to-obtain-an-ssl-certificate"></span>
## How to obtain an SSL certificate?

To obtain an SSL certificate, you need to order an SSL certificate from the BytePlus Certificate Center and submit a certificate request to the Certificate Authority (CA). Once the CA receives your certificate request, they will review the information in your request. After the review is complete, the CA will issue the certificate for you. Once the certificate is issued, you can download it from the BytePlus Certificate Center console and start using it to protect your website.

<span id="how-long-does-it-take-to-obtain-an-ssl-certificate"></span>
## How long does it take to obtain an SSL certificate?


* For DV certificate requests, the CA will issue the certificate to you within a few hours after you complete domain validation.

* For OV and EV certificate requests, the processing time for your certificate request will be longer due to the complex manual verification involved in organization validation. You may need to wait for several days to weeks to obtain the certificate.


<span id="what-is-csr"></span>
## What is CSR?

CSR (Certificate Signing Request) represents the file used to request a certificate signing. The CSR contains the public key and the distinguished name, which is a set of certificate\-related information such as domain name and organization information.

To obtain an SSL certificate, you need to generate a CSR and submit it to the CA. The CA will review the information in the distinguished name and then issue the certificate for you. Specifically, the CA uses its root certificate's private key to sign your CSR and generate the certificate issued to you.

<span id="what-is-an-information-template"></span>
## What is an information template?

An information template represents a template for certificate request information. When you request multiple certificates separately, you may need to enter repetitive information such as contact name, contact phone number, and company information. With an information template, you can save the certificate request information for reuse when requesting certificates in the future. When requesting a certificate, you only need to select the information template to use the saved information.

<span id="will-changing-the-content-of-an-information-template-affect-existing-certificate-requests"></span>
## Will changing the content of an information template affect existing certificate requests?

No, it will not. The information template is only for your convenience in quickly entering information when requesting a certificate and is not associated with already submitted certificate requests.

<span id="what-is-the-difference-between-dns-validation-and-file-validation"></span>
## What is the difference between DNS validation and file validation?

DNS validation and file validation are two methods of domain validation.


* DNS validation: It means that the CA verifies that the certificate applicant has the authority to manage the domain's DNS. This method requires you to log in to the DNS service provider's system and create a DNS TXT/CNAME record for the domain. The CA periodically checks if the specified record exists. When the CA confirms the existence of the specified record, the DNS validation will be completed.

* File validation: It means that the CA verifies that the certificate applicant has the authority to manage the server where the domain is located. This method requires you to add the specified validation file to the specified path on the web server. The CA periodically checks if the specified file can be accessed. When the CA confirms that the specified file can be accessed, the file validation will be completed.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The CA only supports sending validation requests to port 80 or 443. Before choosing this method, please make sure that your web server has opened port 80 or 443.   </div>
   

<span id="how-do-i-cooperate-with-the-ca-to-complete-the-certificate-request-information-validation"></span>
## How do I cooperate with the CA to complete the certificate request information validation?

You need to follow the CA's requirements to complete the following operations:


1. Complete domain validation.

2. If you request an OV or EV certificate, you also need to cooperate with the CA to complete organization validation.

3. If you request an EV certificate, you also need to cooperate with the CA to complete extended validation.


Different CAs may have different methods for organization validation or extended validation. Usually, the CA will notify you of the validation method through the provided phone or email. Please keep your phone accessible and check your email. For more information, please refer to the [Review process for certificate requests](https://docs.byteplus.com/byteplus-certificate-center/docs/understanding-the-review-process-for-certificate-requests).

<span id="why-is-the-status-of-the-certificate-instance-always-validating"></span>
## Why is the status of the certificate instance always "Validating"?

Please first confirm if you have completed domain validation.

If you request an OV or EV certificate, after completing domain validation, you also need to wait for the CA to verify the identity of your organization. The validation process may take 3 to 5 days. Please be patient.

<span id="i-have-completed-the-configuration-for-domain-validation-but-the-order-progress-has-been-stuck-at-pending-domain-validation-for-a-long-time-what-should-i-do"></span>
## I have completed the configuration for domain validation, but the order progress has been stuck at "Pending domain validation" for a long time. What should I do?

When the CA processes your certificate request, in addition to verifying your ownership of the domain, it also checks the CAA (Certification Authority Authorization) records of the domain. If your domain has CAA records configured, only the CA specified in the CAA records is allowed to issue a certificate for your domain.

When the CA finds that it does not have the authority to issue a certificate for your domain, it will stop processing the certificate request. In this case, you will see the order status stuck at the "Pending domain validation" stage in the BytePlus Certificate Center.

**Checking CAA Records**

If you have completed the configuration for domain validation but the certificate request is still stuck at the "Waiting for domain validation" stage for a long time, you can verify if the domain validation failed due to CAA record check by following these steps:

Run the `dig caa <your_domain_name>` command to check if the domain has CAA records configured and if the CAA records include the CA you requested the certificate from.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The CAA records of the root domain apply to all subdomains. For example, if you have a CAA record for <code>example.com</code>, it will apply to all subdomains of <code>example.com</code>.</div>


Take the following image as an example. The returned result includes a CAA record. This record indicates that only GlobalSign is allowed to issue a certificate for your domain.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_3b3d781ef7a2b92587b72913b97f4cd4.png) </span>

**Resolving CAA Record Check Failure**

If you confirm that the domain validation failed due to CAA record check, you can choose one of the following methods to resolve the issue:


* Modify the CAA records of the domain and add the CA you requested the certificate from to the values of the CAA records.

   The method to modify CAA records varies depending on the DNS service provider.

   After adding the specified CA to the values of the CAA records, please wait patiently for about 5 minutes. The CA will periodically check the domain validation configuration and CAA records. If both meet the requirements, the domain validation will pass.

* Cancel the original certificate request in the [BytePlus Certificate Center console](https://console.byteplus.com/certificate-center) and submit a new certificate request to the CA authorized by the CAA records.


<span id="why-did-my-certificate-request-fail"></span>
## Why did my certificate request fail?

If the CA determines that the certificate request information you provided does not match your identity information, or if you fail to complete domain validation within 30 calendar days after submitting the certificate request, the CA will reject your certificate request.
