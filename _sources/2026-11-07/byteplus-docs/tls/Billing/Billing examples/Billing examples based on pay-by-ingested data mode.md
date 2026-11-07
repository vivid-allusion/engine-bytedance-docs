---
title: "Billing examples based on pay-by-ingested data mode"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Billing_examples_based_on_pay-by-ingested_data_mode"
---

This topic introduces the billing examples for pay\-by\-ingested\-data billing mode of Torch Log Service (TLS).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Pay by ingested data volume</strong> is a beta feature. If you have relevant need, contact your account manager for allowlist access.</div>


<span id="5b7ef763"></span>
## Storage billing scenario


|Storage time |Storage duration example |Billing example |
|---|---|---|
|Data storage period ≤ 30 days |7 days of standard storage + 10 days of infrequent access storage |No charge. |
||14 days of standard storage + 16 days of infrequent access storage |No charge. |
|Data storage time \> 30 days |Standard storage for 31 days |Standard storage costs 1 day. |
||31 days of standard storage + 20 days of infrequent access storage |* Day 31: 1 day of standard storage fee.<br><br>* Day 32: 1 day of standard storage fee + 1 day of infrequent access storage fee.<br><br>* Day 33: 1 day of standard storage fee + 2 days of infrequent access storage fee.<br><br>* And so on, up to day 51. |
||Standard storage 14 days + Infrequent access storage 20 days |4 days of infrequent access storage fee. |


<span id="e301a1d4"></span>
## Billing example

User A wrote 10 GiB of data per day, and the data was retained for 30 days. Details are shown in the table below:


|Billing item |explain |Daily Measurement |Unit price example |Daily billing example |
|---|---|---|---|---|
|Original Write Traffic |The logs were uploaded to the log service, with an initial write traffic of 10 GiB. |10 GiB |0.114555256 $/GiB |$ 1.14555256 |
|* Standard Log Storage<br><br>* Standard Index Storage |Data storage duration is 30 days. |You will enjoy free storage for 30 days after the data is written, with no charges incurred, based on the amount of data written. |* Standard Log Storage: 0.00279 $/GiB/Day<br><br>* Standard Index Storage: 0.00279 $/GiB/Day |$ 0 |
