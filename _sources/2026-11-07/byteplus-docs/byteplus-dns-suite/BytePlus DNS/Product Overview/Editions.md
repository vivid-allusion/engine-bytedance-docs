---
title: "Editions"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-editions"
---

This document introduces the editions of a domain in BytePlus DNS.

<span id="editions"></span>
## Editions

In BytePlus DNS, each domain has an edition. Supported features for each edition are as follows:


|Edition/Feature |Free |Professional |Enterprise |Ultimate |Exclusive |
|---|---|---|---|---|---|
|TTL |600 seconds to 86400 seconds |300 seconds to 86400 seconds |60 seconds to 86400 seconds |1 second to 86400 seconds |1 second to 86400 seconds |
|Line |* Geolocation line: Chinese mainland, Global (excluding Chinese mainland).<br><br>* Line group: Allows you to add lines supported by the free edition.<br><br>* ISP Line: China Telecom, China Unicom, and China Mobile.<br><br><br>See [Supported Lines](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-supported-lines). |* Geolocation line: Precise to regions in Chinese mainland and continents globally (excluding Chinese mainland).<br><br>* Line group: Allows you to add lines supported by the professional edition.<br><br>* ISP Line: China Telecom, China Unicom, China Mobile, and more.<br><br><br>See [Supported Lines](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-supported-lines). |* Geolocation line: Precise to regions/provinces in Chinese mainland, precise to continents/countries or regions globally (excluding Chinese mainland).<br><br>* Cloud vendor line: Volcengine, Alibaba Cloud, Tencent Cloud, Baidu Cloud, and Huawei Cloud.<br><br>* Line group: Allows you to add lines supported by the enterprise edition.<br><br>* ISP Line: China Telecom, China Unicom, China Mobile and more, precise to regions/provinces.<br><br><br>See [Supported Lines](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-supported-lines). |* Geolocation line: Precise to regions/provinces in Chinese mainland, precise to continents/countries or regions/Regions or states of the United States/Provinces of Vietnam globally (excluding Chinese mainland).<br><br>* Cloud vendor line: Volcengine, Alibaba Cloud, Tencent Cloud, Baidu Cloud, Huawei Cloud, precise to regions/provinces.<br><br>* IP\-based line: Set IP segments as lines.<br><br>* Line group: Allows you to add lines supported by the ultimate edition<br><br>* ISP Line: Global (Excluding Chinese mainland) ISPs including ATT and more. Chinese mainland ISPs including China Telecom, China Unicom, China Mobile and more, precise to regions/provinces.<br><br>* Secondary ISP Line: Chinese mainland ISPs including China Dr. Peng and more.<br><br><br>See [Supported Lines](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-supported-lines). |* Geolocation line: Precise to regions/provinces in Chinese mainland, precise to continents/countries or regions/Regions or states of the United States/Provinces of Vietnam globally (excluding Chinese mainland).<br><br>* Cloud vendor line: Volcengine, Alibaba Cloud, Tencent Cloud, Baidu Cloud, and Huawei Cloud, precise to regions/provinces.<br><br>* IP\-based line: Set IP segments as lines.<br><br>* Line group: Allows you to add lines supported by the exclusive edition.<br><br>* ISP Line: Global (Excluding Chinese mainland) ISPs including ATT and more. Chinese mainland ISPs including China Telecom, China Unicom, China Mobile and more, precise to regions/provinces.<br><br>* Secondary ISP Line: Chinese mainland ISPs including China Dr. Peng and more, precise to regions/provinces.<br><br><br>See [Supported Lines](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-supported-lines). |
|Load balancing |Up to 10 record values can be load balanced in one record set. Weight range is 1 to 100. |Up to 100 record values can be load balanced in one record set. Weight range is 1 to 100. |Up to 100 record values can be load balanced in one record set. Weight range is 1 to 100. |Up to 100 record values can be load balanced in one record set. Weight range is 1 to 100. |No limit on the number of record values in a record set. Weight range is 1 to 1000. |
|Subdomain levels |Cannot exceed 5 levels. |Cannot exceed 20 levels. |Cannot exceed 20 levels. |Cannot exceed 20 levels. |No limit. |
|DNS query metrics |Statistics by root domain. |Statistics by root domain, subdomain, DNS response, record type. |Statistics by root domain, subdomain, DNS response, record type, ISP (including cloud vendors). |Statistics by root domain, subdomain, DNS response, record type, ISP (including cloud vendors), geolocation. |Statistics by root domain, subdomain, DNS response, record type, ISP (including cloud vendors), geolocation, ISP (including cloud vendors) + geolocation. |
|DNS backup |Not supported. |Not supported. |Not supported. |Supported. |Supported. |
|DNSSEC |Not supported. |Not supported. |Supported. |Supported. |Supported. |
|Alias record |Not supported. |Supported. |Supported. |Supported. |Supported. |


<span id="view-the-edition-of-a-domain"></span>
## View the edition of a domain

You can view the edition of a domain in the console or via API.

<span id="view-the-edition-in-the-console"></span>
### View the edition in the Console

Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns). You can see the edition of each domain name in the **Edition** column on the **Domain management** page.

<span id="view-the-edition-via-api"></span>
### View the edition via API

After calling the QueryZone API or ListZones API, you can see the edition of the domain in the `TradeCode` parameter in the response.

<span id="upgrade-the-edition-of-a-domain"></span>
## Upgrade the edition of a domain

When you create a domain, the edition of the domain defaults to the free edition. You can upgrade the edition of the domain in the console.


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns).

2. On the **Domain management** page, find the domain you need to upgrade. Click **Upgrade** in the **Actions** column.

3. On the **Upgrade** page, select the edition you need to upgrade to, set the purchase duration, and check the agreement. Click **Submit order**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <strong>Auto renewal</strong> option is checked by default. When auto\-renewal is enabled, BytePlus DNS will start deducting fees on the seventh day before the resource expires, and the renewal duration is one year. You can cancel auto\-renewal at any time. You can check or uncheck <strong>Auto renewal</strong> according to your needs.   </div>
   

4. On the **Confirm order information** page, click **Next**.

5. On the **Submit payment information** page, select the payment method and click **Pay**.

6. After the payment is completed, you can find the upgraded domain name on the **Domain management** page.


<span id="feature-changes-after-downgrading-from-paid-edition-to-free-edition"></span>
## Feature changes after downgrading from paid edition to free edition

If your paid edition is downgraded to the free edition, the DNS record configuration of the original paid edition cannot be changed. Related features supported only by the paid edition will be unavailable. The following table lists the feature changes after downgrading.


|Feature |After downgrade |
|---|---|
|TTL |TTL exceeding the free edition limits cannot be changed |
|Line |Lines exceeding the free edition limits cannot be changed |
|Load balancing |Weight values exceeding the free edition limits cannot be changed<br><br>Record sets exceeding the free edition limits:<br><br><br>* Records cannot be added or updated<br><br>* Records can be deleted, but if the number of records after deletion still exceeds the free edition limits, the changes cannot be saved |
|Subdomain levels |Record sets exceeding the free edition limits:<br><br><br>* Records cannot be added or updated<br><br>* Records can be deleted, but if the number of records after deletion still exceeds the free edition limits, the changes cannot be saved |
|DNS query metrics |Downgraded to free edition limits |
|DNS Backup |Unavailable |
