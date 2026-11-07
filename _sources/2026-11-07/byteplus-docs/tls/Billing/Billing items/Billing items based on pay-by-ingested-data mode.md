---
title: "Billing items based on pay-by-ingested-data mode"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Billing_items_based_on_pay-by-ingested-data_mode"
---

This topic introduces the billing items and calculation formulas for pay\-by\-ingested\-data billing mode of Torch Log Service (TLS).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Pay by ingested data volume</strong> is a beta feature. If you have relevant need, contact your account manager for allowlist access.</div>


<span id="2056b2dd"></span>
## Price details

For price details of TLS billing items, see [Pricing details](https://www.byteplus.com/en/pricing?product=TLS&tab=1).

<span id="6653ee06"></span>
## Notes


* TLS supports changing the billing mode. However, only the change from pay\-by\-ingested\-data mode to pay\-by\-feature mode is supported.

* Under pay\-by\-ingested\-data mode, data transformation and log shipping do not generate extra fees but have quota limits. If the data exceeds the quota, fees are generated based on pay\-by\-feature mode.

   
   |**Quota limits** |**Quota requirements** |
   |---|---|
   |Data transformation volume |The free data transforming volume that each topic supports per month is 100TB. |
   |Data shipping volume |The free data shipping volume that each topic supports per month is 100TB. |
   |Data consumption volume |The free data consumption volume that each topic supports per month is 100TB. |
   


<span id="edcc384f"></span>
## Billing item


|Billing item |Description |Calculation formula |
|---|---|---|
|Raw write data volume |When uploading data to TLS, the raw write data is calculated based on the amount of data transmitted (uncompressed). |Daily cumulative raw write traffic (GiB) × price per GiB |
|Storage fee |After the data are stored over 30 days, the corresponding data volume occupies log storage space and generates fees accordingly. Storage volume is calculated cumulatively daily. For details, refer to [Storage billing scenarios](https://docs.byteplus.com/docs/tls/Billing_examples_based_on_pay-by-ingested_data_mode#5b7ef763).<br><br><br>* Log storage space (compressed) can be categorized into the following three types. Based on unit prices from high to low, their sorting is as follows:<br><br>   * Standard storage<br><br>   * Infrequent access storage<br><br>   * Archive storage<br><br>* Index storage space (uncompressed) can be categorized into the following three types. Based on unit prices from high to low, their sorting is as follows:<br><br>   * Index \- Standard storage<br><br>   * Index \- Infrequent access storage<br><br>   * Index \- Archive storage |Daily storage volume (GiB) × price per GiB |
|Outbound traffic |Reading data from the public network domain interface of the log service (compressed) generates external network read traffic. |Daily cumulative external network traffic × price per GiB |
