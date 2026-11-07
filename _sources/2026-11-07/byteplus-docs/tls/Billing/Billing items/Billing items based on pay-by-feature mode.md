---
title: "Billing items based on pay-by-feature mode"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Billing_items_based_on_pay-by-feature_mode"
---

This topic introduces the billing items and calculation formulas for pay\-by\-feature billing mode of Torch Log Service (TLS).

<span id="33bd0521"></span>
## Price details

For the price details of each TLS billing item, refer to [Pricing details](https://www.byteplus.com/en/pricing?product=TLS&tab=1).

<span id="e70a11d6"></span>
## Billing items

<span id=".5a2Y5YKo6LS555So"></span>
### Storage space

TLS calculates the storage volume at every full hour (UTC+8). The daily storage volume is the average of the hourly storage volumes that are recorded over 24 hours of the day.

The retention period of log data and index data is the log storage period that you set in log topic. Log data that exceeds retention period is no longer counted in storage volume. TLS deletes expired data at the next full hour.

TLS automatically compresses data once the data is collected. The compression ratio is `20%~30%`.

Data volume calculation methods are categorized into the following two types:


* Calculated based on compressed raw data volume: log storage space, infrequent access\-log storage space, archive\-log storage space.

* Calculated based on uncompressed raw data volume: index storage space, infrequent access\-index storage space, archive\-index storage space.



|Billing items |Description |Calculation formula |
|---|---|---|
|Log storage space |After TLS collects data, the corresponding data volume (compressed) occupies standard storage space and generates accordingly.<br><br>For example, if the collected raw data volume is 10 GiB with a compression rate of 20%, the daily storage volume for this data is 2 GiB. |Daily storage volume (GiB) × price per GiB |
|Infrequent access\-log storage space |The data volume (compressed) occupies IAS storage space and generates fees accordingly.<br><br>When IAS storage is enabled, log storage converts to IAS storage if log storage time exceeds the standard storage period. Accordingly, fees are calculated based on IAS billing standard. |Daily storage volume (GiB) × price per GiB |
|Archive\-log storage space |The data volume (compressed) occupies archive storage space and generates fees accordingly.<br><br>When archive storage is enabled, log storage converts to archive storage if log storage time exceeds the standard storage period or IAS storage period. Accordingly, fees are calculated based on archive billing standards. |Daily storage volume (GiB) × price per GiB |
|Index storage space |After the data is indexed, index data volume (uncompressed) occupies standard storage space and generates fees accordingly.<br><br>For example, if the original collected data volume is 10 GiB and only full\-text indexing is enabled, the daily index storage size for this data is 10 GiB. |Daily storage volume (GiB) × price per GiB |
|IAS\-index storage space |After data is indexed, indexed data volume (uncompressed) occupies infrequent access storage(IAS) space and generates fees.<br><br>When IAS storage is enabled, log storage converts to IAS storage if log storage time exceeds the standard storage period. Accordingly, fees are calculated based on IAS billing standard. |Daily storage volume (GiB) × price per GiB |
|Archive \- index storage space |After data is indexed, indexed data volume (uncompressed) occupies archive storage space and generates fees.<br><br>When archive storage is enabled, log storage converts to archive storage if log storage time exceeds the standard storage period or IAS storage period. Accordingly, fees are calculated based on archive billing standards. |Daily storage volume (GiB) × price per GiB |


<span id=".5rWB6YeP6LS555So"></span>
### Traffic

Data volume calculation methods are categorized into the following two types:


* Calculated based on compressed raw data volume: write traffic, private network read traffic, and public network read traffic.

* Calculated based on uncompressed raw data volume: index traffic, data shipping traffic, data transformation traffic.



|Billing items |Description |Calculation formula |
|---|---|---|
|Write traffic |During log collection, the collected data volume (compressed) generates write traffic fees. |Daily cumulative write traffic (GiB) × unit price per GiB |
|Private network read traffic |When the data are collected through TLS private network domain name, the corresponding data volume generates downstream traffic fees.<br><br><br>* Downloading logs and consuming logs via private network generates private network read traffic.<br><br>* Querying and analyzing logs via the console or API does not generate read traffic or fees. |Daily cumulative private network read traffic (GiB) × unit price per GiB |
|Public network read traffic |When the data are collected through TLS public network domain name, the corresponding data volume generates downstream traffic fees.<br><br><br>* Downloading logs or consuming logs via public network programs generates public network read traffic.<br><br>* Querying and analyzing logs via the console or API does not generate read traffic or fees. |Daily cumulative public network read traffic (GiB) × unit price per GiB |
|Index traffic |When data is indexed or reindexed, index traffic volume (uncompressed) generates traffic fees. For index traffic details, refer to [Index traffic description](https://docs.byteplus.com/docs/tls/Billing_items_based_on_pay-by-feature_mode#145d6599).<br><br>If a field is configured with both full\-text and key\-value indexes, the index traffic fee is calculated only once.<br><br>For example, when the collected raw data volume is 10 GiB:<br><br><br>* If only the full\-text index is enabled, the index traffic is 10 GiB.<br><br>* If only a key\-value index is enabled on a field with 2 GiB of data, the index traffic is 2 GiB.<br><br>* If the full\-text index is enabled first, and then a key\-value index is enabled on a 2 GiB data field, the index traffic remains 10 GiB. |Daily data volume (GiB) × unit price per GiB |
|Data shipping traffic |Traffic fees are generated by the amount of data that are shipped (uncompressed) to TOS or Kafka. |Daily cumulative shipping data volume (GiB) × price per GiB |
|Data transformation traffic |Traffic fees generated by the volume of data transformed (uncompressed) during data transformation. |Daily cumulative transformed data (GiB) × unit price per GiB |


<span id="145d6599"></span>
### Index traffic description

The index is created based on fields. The size of index traffic relates to the number, length, and values of the indexed fields.


|Index type |Description |
|---|---|
|Full\-text index |Both field names and field values are stored as text types and both generate index traffic. |
|Key\-value index |* Text type: Both field name and field value generate index traffic.<br><br>* Numeric types: Field names of long type and double type do not generate index traffic. The index traffic that each field value occupies is 8 bytes.<br><br>* JSON type: Both field names and field values (including subfields) generate index traffic.<br><br>   * If no index is created for a JSON subfield, the subfield is categorized as the value of a JSON type field, and index traffic is calculated based on text type.<br><br>   * When JSON subfield is indexed, TLS calculates index traffic based on the data type of subfield, such as text, long, and double type. |
|Reserved field index |TLS automatically builds indexes for reserved fields. A small amount of index traffic will be generated accordingly. For more information, refer to [Reserved fields](https://docs.byteplus.com/docs/tls/Reserved-fields-2). |


<span id=".5YW25LuW6LS555So"></span>
### Other billing items


|Billing items |Description |Calculation formula |
|---|---|---|
|Service request count |The number of requests that users call read\-write interface through LogCollector, Open API, or SDK. Fees are calculated based on the number of requests.<br><br><br>* Charges are based on the total number of read and write requests received by TLS, including both successful and failed requests.<br><br>* Interface calls that are triggered via the management console are not included. |Daily cumulative read/write requests (million) × unit price per million requests |
|Number of log shards |Fees are calculated based on the number of log shards according to the read/write status.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, TLS is running a promotion that offers a certain quota of free log shards. During the promotion, each log topic is offered with 2 free log shards per day.</div><br> |Number of shards in read/write state (count) × unit price |
