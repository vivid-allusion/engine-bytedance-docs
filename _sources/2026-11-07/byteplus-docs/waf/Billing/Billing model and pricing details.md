---
title: "Billing model and pricing details"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/docs-billing-model-and-pricing-details"
---

BytePlus Web Application Firewall (WAF) service provides you with a set of robust security tools for the BytePlus CDN domains under protection. WAF supports two types of instances: edge cloud instances, aimed at services deployed on BytePlus CDN; and center cloud instances, aimed at public internet services deployed on or outside BytePlus Cloud. This article introduces the billing details for both instance types.

<span id="f1cbd129"></span>
## WAF instances for CDN domains

WAF instances for CDN domains take effect on businesses deployed on CDN, which means that your domain must first be added to BytePlus CDN to use such WAF instances for protection.

<span id="b338840c"></span>
### Billing model

A WAF instance for CDN domain uses the pay\-as\-you\-go billing model. You are charged based on your WAF resource usage. Fees are deducted from the balance of your BytePlus account after your bill is generated at the end of each service cycle.

<span id="0a4556df"></span>
### Specifications

A WAF instance for CDN domain offers a complete web application security solution for your websites or app services on BytePlus CDN, which includes the following protection capabilities.


* HTTP and HTTPS request protection

* Web vulnerability attack protection

* Blocklist/allowlist access control

* Location\-based access control

* Bot management and custom bot rules .

* Custom response page

* API protection


<span id="b9d5d28f"></span>
### Log service

You can enable TLS (Torch Log Service) to collect log data of web attacks and requests for protected resources. Log service allows you to query and analyze massive log data in real time. It can perform SQL analysis and calculations based on query results and display the results in charts, enabling you to promptly address security problems.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is noted that enabling the log service will automatically create an IAM service role (role name: ServiceRoleForWaf). This role authorizes WAF to access other cloud resources.</div>


WAF queries the used log capacity hourly. At the end of each month, you will be charged for the sum of used log capacity at every hour.

<span id="7ddcc891"></span>
### Pricing details

You are charged monthly for the WAF security functions and rules provided by the WAF instance (WAF functionality fee), the requests your instance process (request processing fee), and the TLS log volume you use (TLS fee) during every service cycle, all of which are billed hourly.


|**Item** |**Pricing (USD)**  |**Unit** |**Billing Cycle** |**Note** |
|---|---|---|---|---|
|WAF functionality fee |$0.14 |Per hour |An hour |About $100 per month. |
|Request processing fee |$0.75 |Per million requests |An hour |\-\- |
|TLS fee |$0.04 |Per TB per hour |An hour |\-\- |


<span id="26dda0c2"></span>
### Pricing example

User A accessed the WAF service at 8:00 a.m. on June 16th and was charged till the end of the month.

The user had 1,000,000,000 requests for BytePlus CDN processed by the WAF service.


* WAF functionality charges = $0.14 \* (17 hours + 14 days \* 24 hours) = $49.42.

* Request processing charges = $0.75 \* 1,000,000,000/1,000,000 = $750.


Below is an example of TLS usage for each hour from 09:00 a.m. to 12:00 p.m. on June 16th.


|**Time** |**TLS usage** |
|---|---|
|09:00 |1 TB |
|10:00 |2 TB |
|11:00 |2 TB |
|12:00 |1 TB |


The total usage during this time is the sum of all these 4 values, which is calculated as 6 TB. Therefore, the TLS fee for these four hours is $0.04 \* 6 TB = $0.24. To calculate the cost of the log service for User A in June, it is required to add up the used log capacity for each hour from June 16th to June 30th.

<span id="01b0b985"></span>
## Cloud WAF instances

Cloud WAF instances are not limited by the location of business deployment. They can protect businesses deployed on BytePlus as well as those deployed outside of BytePlus cloud. This offers a broader scope of application.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also check the latest specifications and pricing details on <a href="https://www.byteplus.com/en/pricing?product=WAF&tab=2">BytePlus Pricing Calculator</a>. If there is any inconsistency, please refer to the pricing calculator for accuracy.</div>


<span id="3a6fb2e5"></span>
### Billing model

A cloud WAF instance supports an annual or monthly prepaid billing model. You are charged based on the selected basic specifications, extension packages, and log capacity. The package specification is required while the extension packages and log capacity are optional.

<span id="2616bb6a"></span>
### Billable items


|Billing Items |Required |Description |
|---|---|---|
|Basic specifications |Yes |* Cloud WAF instance includes basic specifications: Basic, Advanced, Enterprise, and Ultimate editions.<br><br>* Different basic specifications offer varying levels of protection, and you can choose the package that suits your actual protection needs. For specific differences between different basic specifications, please refer to [Details of different instance packages](https://docs.byteplus.com/docs/waf/docs-billing-model-and-pricing-details#11299bb0). |
|Domain extension package |No |* On top of the protection domain quotas included in the selected instance package, additional protection domain quotas are provided. Within the validity period of the instance specifications, you can upgrade the number of domain extension packages according to your needs.<br><br>* A single\-domain extension package includes protection quotas for 10 domains (limited to one main domain).<br><br>* Each instance can have up to 1000 domain extension packages. |
|QPS extension package |No |* On top of the protection domain quotas included in the selected instance package, additional protection domain quotas are provided. Within the validity period of the instance specifications, you can upgrade the quantity of QPS extension packages based on your needs.<br><br>* Each instance can have up to 20 QPS expansion packages. |
|Log service |No |* The log service provides capabilities such as collection, retrieval analysis, alerting, and downloading of attack and access logs for the domains under the protection of WAF, based on the purchased log service capabilities. Within the validity period of the instance specification, you can enable or upgrade the log service capability according to your needs.<br><br>* The log service supports a minimum capacity of 1 TiB and a maximum of 500 TiB per instance. |


<span id="11299bb0"></span>
### Details of different instance packages

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Log service is available for all specification editions, and you can purchase log storage capacity as needed.</div>


<span id="3986877f"></span>
#### Protection capabilities


|**Specifications** |**Basic Edition** |**Advanced Edition** |**Enterprise Edition** |**Ultimate Edition** |
|---|---|---|---|---|
|Number of protected domains |10 (1 main domain) |20 (2 main domains) |30 (3 main domains) |50 (5 main domains) |
|Supported ports |* HTTP: 80<br><br>* HTTPS: 443 |* HTTP: 80<br><br>* HTTPS: 443<br><br>* Other ports |* HTTP：80<br><br>* HTTPS：443<br><br>* Other ports |* HTTP：80<br><br>* HTTPS：443<br><br>* Other ports |
|Normal request peak |200 QPS |2000 QPS |5000 QPS |10000 QPS |


<span id="1367baba"></span>
#### Protection policies


|**Type** |**Feature** |**Basic Edition** |**Advanced Edition** |**Enterprise Edition** |**Ultimate Edition** |
|---|---|---|---|---|---|
|Vulnerability protection |OWASP TOP 10 threat protection |Supported |Supported |Supported |Supported |
||Automatic updates for the latest vulnerability protection rules |Supported |Supported |Supported |Supported |
|Access control |IP allowlist/blocklist based on advanced conditions |10 rules per instance |100 rules per instance |500 rules per instance |1000 rules per instance |
|Geo\-blocking |Geographic blocking based on global locations |Not supported |Supported |Supported |Supported |
|Custom response page ||Not supported |Not supported |50 rules per instance |100 rules per instance |
|Rate limiting |Custom rate\-limiting (based on IP, custom Args, custom Header, Cookie, Session, etc.) |10 rules per instance |200 rules per instance |600 rules per instance |1500 rules per instance |
||Intelligent rate\-limiting |Not supported |Supported (Time\-limited free trial) |Supported (Time\-limited free trial) |Supported (Time\-limited free trial) |
|API protection |Custom API protection |Not supported |Not supported |600 rules per instance |1500 rules per instance |
||API auto\-discovery |Not supported |Not supported |Supported (Time\-limited free trial) |Supported (Time\-limited free trial) |
|Bot management |Managed bot rules |Not supported |Supported |Supported |Supported |
||Custom bot rules |Not supported |Not supported |50 rules per instance |100 rules per instance |
||Rate\-limiting protection against bot |Not supported |Support (Time\-limited free trial) |Support (Time\-limited free trial) |Support (Time\-limited free trial) |
||Statistical protection against bot |Not Supported |Support (Time\-limited free trial) |Support (Time\-limited free trial) |Support (Time\-limited free trial) |
|Sensitive data leakage prevention (including mobile phone number, ID card, bank card, and other private data) ||Not Supported |Supported |Supported |Supported |
|Web tamper protection ||Not Supported |20 rules per instance |50 rules per instance |100 rules per instance |


<span id="5e99204a"></span>
### Pricing details

Below introduces the pricing details of different billable items.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Product specifications and prices are subject to change. For detailed costs, please refer to the actual calculators and orders in your console.</div>



|**Item** ||**Pricing (USD)**  |**Unit** |**Note** |
|---|---|---|---|---|
|Basic specifications |Basic edition |$160 |Per month |* Select one edition from the 4 editions.<br><br>* The cost of the log service is not included. |
||Advanced edition |$560 |Per month ||
||Enterprise edition |$1,400 |Per month ||
||Ultimate edition |$3,800 |Per month ||
|Domain extension package ||$100 |Per package per month |* One package includes 10 domains, and these 10 domains should be subject to one main domain.<br><br>* You can purchase up to 1,000 domain extension packages. |
|QPS extension package ||$400 |Per package per month |* One package includes 1,000 QPS.<br><br>* You can purchase up to 1,000 QPS extension packages. |
|Log service ||$90 |Per TB per month |Available range: 1 to 500 TB. |


<span id="0815c4bc"></span>
### Pricing example

Let's assume that you buy one WAF instance of center cloud for one month. The billable items are as follows.


|**Item** |**Specification** |
|---|---|
|Basic specification |Advanced edition |
|Domain extension package |5 |
|QPS extension package |5 |
|Log service |5 TB |
|Total combined charges |\-\- |



* Basic specification charges = $560

* Domain extension package charges = $100 \* 5 = $500

* QPS extension package charges = $400 \* 5 = $2,000

* Log service charges = $90 \* 5 = $450


Total combined charges = $560 + $500 + $2,000 + $450 = $3,510
