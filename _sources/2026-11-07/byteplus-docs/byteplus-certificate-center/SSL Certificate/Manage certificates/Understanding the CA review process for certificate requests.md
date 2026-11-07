---
title: "Understanding the CA review process for certificate requests"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-understanding-the-review-process-for-certificate-requests"
---

After you submit a certificate request to the CA, the CA will review your certificate request. Only when the certificate request passes the CA's review process, will the CA issue a certificate for you. This article introduces the review process for different types of certificates and what you need to pay attention to.

<span id="overview"></span>
## Overview

The review process for different types of certificates varies, and the time required to issue different certificates also varies.


|Certificate type |Review process |Time required for issuance |
|---|---|---|
|DV Certificate |DV stands for Domain Validation.<br><br>CA only verifies that the applicant has administrative control over the domain, and will issue DV certificates. |CA generally implements domain validation through automated methods, so DV certificates can be issued within a few hours. |
|OV Certificate |OV stands for Organization Validation.<br><br>In addition to verifying that the applicant has administrative control over the domain, the CA also verifies that the organization applying for the certificate actually exists and has no abnormal business issues, and confirms that the applicant has the authorization to order certificates for the organization.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Please ensure that your organization has no abnormal business issues, otherwise you will not be able to obtain OV and EV certificates.</div><br> |Organization validation requires manual involvement. This means that OV certificates generally take 3 to 5 working days to be issued.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Some CAs retain the organization information that has been verified (i.e., the organization information template you used when submitting the certificate request) to expedite the issuance of OV/EV certificates for the organization. For more information, see <a href="https://docs.byteplus.com/en/docs/29/8580#simplified-review-process-for-ov-ev-certificate-requests">Simplified review process for OV/EV certificate requests</a>.</div><br> |
|EV Certificate |EV stands for Extended Validation.<br><br>In addition to domain validation and organization validation, the validation process for EV certificates may involve investigations by professional legal personnel and confirmation by independent auditors. |Due to the complexity of the review process, EV certificates generally take 7 to 10 working days to be issued. |


<span id="checking-order-progress"></span>
## Checking order progress

You can keep track of the progress of your order and get updates on the status of your certificate request. The order progress information is located in the certificate details.

Follow these steps to check the order progress:


1. Log on to the [BytePlus Certificate Center console](https://console.byteplus.com/certificate-center).

2. In the left navigation pane, select **SSL Certificate** \> **Certificates**.

3. On the **Certificate management** page, click the ID of the certificate.

   If the CA is reviewing your certificate request, the status of the certificate will be **Validating**.

4. On the right side of the certificate details page, view the **Order progress** of the certificate.


You can obtain domain validation requirements and other related information through the order progress.

<span id="review-process"></span>
## Review process

Different CAs have different specific review processes. The following content mainly introduces the general matters that you need to cooperate with the CA to complete during the certificate request review process. If you want to learn about the detailed review processes of different CAs, it is recommended that you visit the official websites of the CAs.

<span id="domain-validation"></span>
### Domain validation

Domain validation means that the CA verifies that you have administrative control over the domain for which the certificate is issued. You can choose the domain validation method when submitting a certificate request. The domain validation methods include:


* DNS validation: This method requires you to modify the DNS records of the domain as required, such as adding a TXT or CNAME record. The CA checks if the specified DNS record exists to complete the validation.

* File validation: This method requires you to add the specified file to the server corresponding to the domain. The CA checks if the specified file exists to complete the validation.


<span id="what-do-i-need-to-do"></span>
#### What do I need to do


1. After submitting a certificate request in the [BytePlus Certificate Center console](https://console.byteplus.com/certificate-center), please wait patiently for 5 minutes to obtain the domain validation requirements in the **Order progress**.

2. After completing the validation configuration according to the domain validation requirements, you can click **Check** to check if your configuration is correct. For specific steps of domain validation, please refer to [Demonstrating control over domain](https://docs.byteplus.com/byteplus-certificate-center/docs/conducting-domain-validation).

3. After confirming that you have completed the validation configuration as required, please wait patiently for the CA to check your configuration.


<span id="what-should-i-do-next"></span>
#### What should I do next


* For DV certificate requests

   After the CA verifies the accuracy of your configuration, the certificate will be issued to you. This process usually takes about 5 minutes.

* For OV and EV certificate requests

   After completing the domain validation configuration as required, you also need to cooperate with the CA to complete the [Organization validation](https://docs.byteplus.com/en/docs/29/8580#organization-validation).


<span id="organization-validation"></span>
### Organization validation

For OV and EV certificate requests, the CA will perform organization validation to confirm the following:


* The organization applying for the certificate exists and has no abnormal business issues.

   For example, the CA may verify the organization's records in the local government's business registration, and check if it is not listed in the local government's restricted entity list.

* You (the certificate applicant/contact person) have the authorization to order the certificate for the organization.

   The CA will search for certified and publicly listed organization phone numbers, and then use the certified phone number to contact the organization's representative (such as the organization contact person or technical contact person) to verify your authorization to order the certificate. If other representatives cannot be contacted, the CA may contact you.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The organization's phone number must come from a third party or an independent list. For example, the phone number registered on Google Maps, the phone number registered with Dun & Bradstreet, etc.</div>


<span id="what-do-i-need-to-do"></span>
#### What do I need to do

You must cooperate with the CA to complete the phone verification.


* (Recommended) Answer the CA's call to confirm your authorization.

   * After submitting the certificate request, please ensure that the organization contact person, technical contact person, and the front desk of your company are aware that you have ordered a certificate, and any of them can answer the CA's call.

   * Please inform them of the following:

      * The CA may call within 24 hours.

      * Be prepared to answer several questions about you and your position in the company.

   * The certificate cannot be issued to you until your authorization is confirmed.

* Respond to the organization consent message

   * If the CA verification personnel cannot contact you or someone who represents you through the verified and publicly listed organization phone number, they will leave a message with a callback number and verification code.

   * Make sure that you, the front desk, the organization contact person, or the technical contact person reply to the message and provide the verification code to the CA.

* Schedule a call


If the CA verification personnel cannot contact someone who represents you through the verified and publicly listed organization phone number, you may also receive an email to schedule a call and complete the verification.

<span id="what-should-i-do-next"></span>
#### What should I do next


* For OV certificate requests

   After the CA completes the organization validation, the certificate will be issued to you.

* For EV certificate requests

   You also need to cooperate with the CA to complete the [Extended validation](https://docs.byteplus.com/en/docs/29/8580#extended-validation).


<span id="extended-validation"></span>
### Extended validation

For EV certificate (or some brands of OV certificate) requests, the CA may require you to provide additional confirmation or provide other supporting documents. For example, an application form with the organization's official seal and a signed user agreement with the official seal, basic deposit account information, scanned copies of the personal identification card of the organization contact person (front and back), lawyer's letter, etc.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the following cases, the CA may require you to provide a lawyer's letter:</div>



* <div data-tips="true" data-tips-type="tip">The subject of the certificate application has been established for less than three years.</div>



<div data-tips="true" data-tips-type="tip">Please refer to the CA's notification for specific requirements.</div>


The CA will send an email to the certificate contact person's email address to explain the supporting documents you need to provide. Some CAs may inform you of the supporting documents required during the organization validation process through a phone call.

<span id="what-do-i-need-to-do"></span>
#### What do I need to do

Check the email using the email address provided in the certificate request information, confirm and prepare the supporting documents required by the CA, and reply to the email as required. If you need assistance, you can contact the after\-sales support staff of the BytePlus Certificate Center.

<span id="what-should-i-do-next"></span>
#### What should I do next

After the CA completes the extended validation, the certificate will be issued to you.

<span id="simplified-review-process-for-ov-ev-certificate-requests"></span>
## Simplified review process for OV/EV certificate requests

When you submit an OV/EV certificate request, you need to select an organization information template. The CA will verify the information in the organization information template and record the verified organization information template. If you use a verified organization information template to apply for an OV/EV certificate again, the certificate request review process will be simplified.

The simplification process is reflected in the following two aspects: no organization validation and no domain validation.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If a field (except for the <strong>Template name</strong>) in the verified organization information template is changed, and you use the modified template to submit an OV/EV certificate request, the CA will perform organization validation and domain validation again.</div>


<div data-tips="true" data-tips-type="warning">The following only describes the simplified review process of DigiCert. Different CAs may have different verification strategies. Please refer to the official information of the CA for specific details.</div>



|Type |Description |Applicable certificate brands |
|---|---|---|
|No organization validation |* If the organization information template you used when applying for an OV certificate has been verified by the CA, and you use the same organization information template to apply for an OV certificate from the same CA within the next 13 months, you do not need to undergo organization validation.<br><br>> Example:<br><br>> Suppose you have successfully applied for a DigiCert SecureSite OV certificate. If you continue to use the same organization information template to apply for a DigiCert SecureSite OV certificate, you do not need to undergo organization validation.<br><br><br>* If the organization information template you used when applying for an EV certificate has been verified by the CA, and you use the same organization information template to apply for an EV or OV certificate from the same CA within the next 13 months, you do not need to undergo organization validation. |* DigiCert SecureSite<br><br>* DigiCert SecureSite Pro<br><br>* DigiCert GeoTrust |
|No domain validation |If you have successfully applied for an OV/EV certificate for a domain using an organization information template, you do not need to undergo domain validation when applying for a certificate for the same domain using the same organization information template within the next 13 months.<br><br>No domain validation is also applicable in the following scenarios where the domains are different:<br><br><br>* If the root domain (e.g., `example.com`) has been validated, the corresponding subdomains (e.g., `www.example.com`, `abc.www.example.com`, etc.) can be exempted from validation.<br><br>* If the subdomain with the www prefix (e.g., `www.example.com`) has been validated, the corresponding root domain (e.g., `example.com`) and other subdomains (e.g., `abc.example.com`, `abc.www.example.com`, etc.) can be exempted from validation. ||
