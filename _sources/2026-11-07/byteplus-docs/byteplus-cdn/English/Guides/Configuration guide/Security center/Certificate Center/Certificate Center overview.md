---
title: "Certificate Center overview"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-certificate-center-overview"
---

The Certificate Center page on the BytePlus CDN console integrates the functionality of the BytePlus Certificate Center. You can purchase certificates, upload existing ones, view certificates information, and associate your domain names with certificates on this page.

<span id="usage-scenarios"></span>
## Usage Scenarios

If you need to bind an encryption policy to a domain name, you must first associate that domain name with a certificate issued to it.


* If you have already purchased the certificate from another certificate service provider, you need to upload it to the **Certificate Center** page and then associate it with the domain name.

* If you have not yet purchased such a certificate, you can purchase one on the **Certificate Center** page and then associate it with the domain name.


<span id="service-authorization"></span>
## Service Authorization

If this is your first time visiting the **Certificate Center** page, you need to authorize CDN to access BytePlus Certificate Center by granting the `ServiceRoleForCDN` role to CDN. Click **Authorize Access** and follow the prompts on the page to proceed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only the primary account can authorize CDN to access BytePlus Certificate Center. IAM users cannot perform this operation.</div>


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_577784dd9d5d54962a9f7bdd5a1a6e47.png) </span>

<span id="page-introduction"></span>
## Page Introduction

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c83c7ef6b08c46829b809f21d20ea0e6~tplv-goo7wpa0wc-image.image) </span>

The **Certificate Center** includes the following sections:


* [Purchase Certificates](https://docs.byteplus.com/en/docs/18/6606#purchase-certificates)

* [Upload Certificates](https://docs.byteplus.com/en/docs/18/6606#upload-certificates)

* [View Certificates](https://docs.byteplus.com/en/docs/18/6606#view-certificates)


<span id="purchase-certificates"></span>
### Purchase Certificates

If you do not have a certificate issued to your domain name, you can purchase one on the Certificate Center page. The page offers two purchase options:


* Purchase Certificate: Purchase a paid certificate for official commercial sites. When you click **Purchase Certificate**, the CDN console opens the **Purchase Certificate** page of BytePlus Certificate Center. Refer to the Certificate Center's [Order Certificate](https://docs.byteplus.com/en/byteplus-certificate-center/docs/creating-certificate-order) documentation for steps.

* Get Free Certificate: Get a free certificate issued by DigiCert, suitable for personal websites or testing HTTPS requests. When you click Get **Free Certificate**, the CDN console opens the Request **Free Certificate** page of BytePlus Certificate Center. Refer to the Certificate Center's [Request Free Certificate](https://docs.byteplus.com/en/byteplus-certificate-center/docs/request-free-ssl-certificate) documentation for steps.


<span id="upload-certificates"></span>
### Upload Certificates

See [Upload Certificates](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-upload-certificates-certfiicate-center).

<span id="view-certificates"></span>
### View Certificates

The certificates listed on the **Certificate Center** page meet the following criteria:


* These certificates are from the BytePlus Certificate Center.

* These certificates are for domain names that have been added to CDN.


The page has four tabs:


* **Total**: Lists all your uploaded or purchased certificates.

* **Issued**: Lists valid certificates. A certificate is considered valid if its expiration date is more than a month away.

* **Expiring**: Lists certificates that are less than one month away from the expiration date. Please renew these certificates promptly to avoid expiration.

* **Expired**: Lists expired and revoked certificates. Browsers will flag access to accelerated domain names associated with these certificates as insecure. Please renew your expired certificates as soon as possible.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the certificate needing renewal is already associated with a domain name, see <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs-associate-domain-name-with-certificate#52a3b9d4">Steps after Renewing a Certificate</a>.</div>


Each tab lists the corresponding certificates. The following table describes the fields on the tabs.


|**Field** |**Description** |
|---|---|
|Certificate ID |The unique ID of the certificate in the BytePlus Certificate Center. |
|Issued To |Lists all the domains issued to the certificate. |
|Status |Indicates the status of the certificate, which can be one of the following:<br><br><br>* Issued<br><br>* Expiring<br><br>* Expired |
|Hosted At |Shows the location where the certificate is stored. For certificates from the BytePlus Certificate Center, this field is **Certificate Center**. |
|Associable Domains |Indicates the domain names in the CDN that can be associated with the certificate. |
|Associated Domains |Indicates the domain names in the CDN that have been associated with the certificate. |
|Remark |Indicates the remark of the certificate. |
|Issued On |Indicates the issuance date of the certificate. |
|Expire On |Indicates the expiration date of the certificate. |
|Actions |Lists the actions that can be performed on the certificate. Available actions include:<br><br><br>* **Associate Domains**: Associate the certificate with one or more domain names. The domain names that can be associated are displayed in the **Associable Domains** field. See [Associate Certificates with Domain Names](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-associate-domain-name-with-certificate).<br><br>* **View Details**: View the details of the certificate in the BytePlus Certificate Center. |
