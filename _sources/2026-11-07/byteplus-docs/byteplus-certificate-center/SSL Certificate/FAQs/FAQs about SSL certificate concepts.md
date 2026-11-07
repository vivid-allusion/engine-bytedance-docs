---
title: "FAQs about SSL certificate concepts"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-faqs-about-concepts"
---

<span id="why-do-i-need-an-ssl-certificate"></span>
## Why do I need an SSL certificate?

If you want to enable HTTPS to secure your website's traffic from being monitored, tampered with, or hijacked, you need an SSL certificate.

<span id="what-types-of-ssl-certificates-are-there"></span>
## What types of SSL certificates are there?

SSL certificates are divided into the following types:


* DV (Domain Validation) certificate: The Certificate Authority (CA) only verifies the applicant's ownership of the domain. DV certificates do not include information about the organization or company to which the certificate belongs.

* OV (Organization Validation) certificate: In addition to verifying the applicant's ownership of the domain, the CA also verifies the authenticity of the organization or company information provided by the applicant.

* EV (Extended Validation) certificate: In addition to verifying the applicant's ownership of the domain, the CA relies on third\-party databases to extensively review the organization or company information provided by the applicant, including identity confirmation and verification of relevant documents (such as lawyer letters).


<span id="which-type-of-ssl-certificate-should-i-choose"></span>
## Which type of SSL certificate should I choose?

Different types of SSL certificates have different levels of trust: DV provides a medium level, OV provides a high level, and EV provides the highest level.

Here are some recommendations for certificate selection:


* For personal or non\-commercial websites, it is recommended to choose a DV certificate.

* For public\-facing commercial websites, it is recommended to choose an OV certificate.

* For websites handling sensitive information such as e\-commerce and finance, it is recommended to choose an EV certificate.


<span id="how-many-domains-can-i-secure-with-an-ssl-certificate"></span>
## How many domains can I secure with an SSL certificate?


* Single domain certificate: A single domain certificate can secure only one fully qualified domain name (FQDN) or an IP address. The domain can be either a root domain (e.g., `example.com`) or a subdomain (e.g., `anything.example.com`).

* Wildcard domain certificate: A wildcard domain certificate can secure multiple subdomains at the same level. For instance, a certificate issued to `*.example.com` can secure `a.example.com`, `b.example.com`, etc., but cannot secure `a.b.example.com`.
