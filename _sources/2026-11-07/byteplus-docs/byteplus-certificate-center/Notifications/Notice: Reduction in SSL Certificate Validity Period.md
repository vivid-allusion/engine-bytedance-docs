---
title: "Notice: Reduction in SSL Certificate Validity Period"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/notice-on-shortening-of-ssl-certificate-validity-period"
---

Dear BytePlus Users,

In accordance with the latest voting results from the CA/Browser Forum (Ballot [SC-081v3](https://cabforum.org/2025/04/11/ballot-sc081v3-introduce-schedule-of-reducing-validity-and-data-reuse-periods/)), the maximum validity period for SSL/TLS certificates worldwide will be progressively shortened. To enhance network security and follow industry standards, BytePlus Certificate Center will adjust its certificate validity policies in alignment with the specific execution strategies of global Certificate Authorities (CAs).

> The Certification Authority Browser Forum (CA/Browser Forum) is the global authoritative standards organization for the digital certificate industry. To be publicly trusted by major browsers and operating systems, a CA must comply with the Baseline Requirements (BR) established by the CA/B Forum.


<span id="NqQ7Ralq"></span>
## Background

Starting in 2026, the maximum validity period for SSL/TLS certificates will be reduced in stages from the current 398 days to 47 days. This change is designed to mitigate risks like private key compromise by increasing the frequency of certificate rotation.

Maximum validity period of public TLS/SSL in the CA/Browser Forum:


|**Certificate issued** |**Maximum certificate validity** |
|---|---|
|Before March 15, 2026 |398 days |
|Between March 15, 2026, and March 15, 2027 |200 days |
|Between March 15, 2027, and March 15, 2029 |100 days |
|After March 15, 2029 |47 days |


<span id="ch0s6Fcz"></span>
## What do I need to do?

To ensure a smooth transition of platform policies and issuance workflows, BytePlus Certificate Center will adjust the validity rules for public SSL/TLS certificates starting **February 10, 2026**, based on the CA/B Forum Baseline Requirements and individual CA execution timelines. While all brands fall under this unified transition scope starting February 10, the specific validity and pricing rules remain subject to the final execution strategy of each CA.


|Certificate Brand |From |Order Date |Issuance Date |Validity Period |Pricing Details |
|---|---|---|---|---|---|
|DigiCert |Paid Certificate |Before Feb 10, 2026 |Before Feb 24, 2026 |1 year |See [DigiCert Pricing Adjustment Details](https://docs.byteplus.com/en/docs/byteplus-certificate-center/notice-digicert-certificate-pricing-adjustment#tlBkgnnL). |
|||Before Feb 10, 2026 |On or After Feb 24, 2026 |199 days ||
|||On or After Feb 10, 2026 |Any |199 days ||
|Others |BytePlus Certificate Center expects to adjust issuance rules for other brands starting March 15, 2026. Specific effective dates and validity periods will depend on CA policies. Please refer to the [Purchase certificate](https://console.byteplus.com/certificate-center/ssl/certificate/buy?) page in the console for updated validity and pricing information. |||||


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note on Key Dates</div>



* <div data-tips="true" data-tips-type="default"><strong>February 10, 2026:</strong> BytePlus Certificate Center begins implementing validity and pricing adjustments for DigiCert certificates.</div>


* <div data-tips="true" data-tips-type="default"><strong>February 24, 2026:</strong> The deadline for DigiCert to accept requests for certificates with validity exceeding 199 days. Per <a href="https://knowledge.digicert.com/alerts/public-tls-certificates-199-day-validity">DigiCert’s official announcement</a>, certificates exceeding 199 days will no longer be issued after this date.</div>



<span id="Jcb7UsCd"></span>
## Recommendations

As validity periods shorten, manual certificate management will become increasingly complex. To avoid service disruptions or access issues caused by certificate expiration, we recommend the following:


* Embrace automation: We strongly advise adopting automated certificate management tools. BytePlus Certificate Center is continuously enhancing our automation capabilities to help you streamline renewals and reduce the risk of manual errors.

* Audit your inventory: Review your currently deployed certificates and note those expiring after early 2026 to plan for the new shorter renewal cycles.

* Stay informed: We will continue to monitor CA/Browser Forum updates and provide timely notifications regarding further changes or specific brand policies.


BytePlus Certificate Center is committed to providing you with secure and reliable services. If you have any questions, please feel free to contact our support team.

Thank you for your continued trust in BytePlus!
