---
title: "Editions"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/8cqTK1"
---

This document introduces the editions and features of BytePlus GTM instances.

<span id="editions-and-features"></span>
## Editions and features

In BytePlus GTM, each GTM instance has an edition. The features of each edition are as below:


|Features |Standard edition |Ultimate edition |
|---|---|---|
|**Supported lines** |* ISP Line: ISPs in Chinese Mainland, including China Telecom, China Unicom, and China Mobile, accurate to provinces<br><br>* Geolocation line: Chinese Mainland, global (excluding Chinese Mainland) accurate to continent/country or region |* ISP Line: ISPs in Chinese Mainland, including China Telecom, China Unicom, China Mobile, China Education and Research Network (CERN), and China Broadnet, accurate to region/province<br><br>* Secondary ISP Lines: China Dr. Peng, China Great Wall Broadband Network, China Wasu Group, China Founder Group, China Science & Technology Network, China Guangzhou Zhujiang Digital Group, accurate to region/province<br><br>* Geolocation line: Chinese Mainland accurate to major region/province, global (excluding Chinese Mainland) accurate to continent/country or region<br><br>* IP\-based Line: IP ranges as DNS lines |
|**Health check interval** |1 minute |1 minute or 15 seconds |
|**TTL (Time to Live)**  |60 seconds ~ 3600 seconds |1 second ~ 3600 seconds |
|**Policy** |Basic routing |Basic or intelligent routing |
|**Limit on number of routing rules within a GTM instance** |20 |200 |
|**Limit on number of pool sets within a rule** |10 |10 |
|**Limit on number of pools within a pool set** |10 |20 |
|**Limit on number of pools within a GTM instance** |20 |50 |
|**Limit on number of addresses within a pool** |20 |50 |
|**Limit on number of addresses within a GTM instance** |500 |2000 |
|**Address weight range** |1 ~ 10 |1 ~ 100 |
|**Weight range for pools within a pool set** |Not Supported |1 ~ 100 |
|**Weight range for rules** |1 ~ 10 |1 ~ 100 |


Different editions are billed differently. For billing details, refer to [Billing](https://docs.byteplus.com/en/docs/byteplus-dns-suite/R4Anoj).

<span id="view-the-edition-of-a-gtm-instance"></span>
## View the edition of a GTM instance

You can view the edition of a GTM instance via the BytePlus GTM console or through APIs.

<span id="view-from-the-console"></span>
### View from the console

Open [Instance management](https://console.byteplus.com/dns-suite/gtm/instances). The edition for each GTM instance can be viewed in the **Edition** column on the **Instance management** page.

<span id="view-through-the-api"></span>
### View through the API

After calling the GetGtm API or ListGtms API, the edition of the GTM instance can be found in the API response.

<span id="upgrade-the-edition-of-a-gtm-instance"></span>
## Upgrade the edition of a GTM instance

If your GTM instance edition is standard edition, you can upgrade it to the ultimate edition. Downgrading from the ultimate edition back to the standard edition is not supported.

Open [Instance management](https://console.byteplus.com/dns-suite/gtm/instances). You can start the upgrade by clicking **Upgrade** in the **Action** column of the **Instance management** page.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Upgrade operations take effect at 00:00 on the following day. During the upgrade period, deleting instances is temporarily unsupported.</div>
