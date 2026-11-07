---
title: "Storage type"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Storage_Type"
---

Log Service provides tiered data storage through different storage types, suitable for storing log data with varying access frequencies. This document introduces Log Service's storage types and their applicable scenarios.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Archive storage is a beta feature. If you have relevant need, contact your account manager for allowlist access.</div>


<span id="abbc0519"></span>
## Storage type

Log Service supports the following storage types:


|Storage type |Activation requirements |Description |
|---|---|---|
|Standard storage |None |Standard Storage is the general storage solution provided by Log Service. By default, log data is stored in Log Service using Standard Storage. The Standard Storage solution offers high performance and high throughput, suitable for storing logs that are frequently accessed, such as those requiring frequent query and analysis.<br><br>Standard Storage features include:<br><br><br>* Supports real\-time access to log data, providing millisecond\-level log query and analysis capabilities.<br><br>* Standard storage duration is unlimited, supporting permanent storage.<br><br>* Standard storage supports migration to low\-frequency storage or archive storage. |
|Infrequent Access Storage |The standard storage duration is 7 days or more. |Low\-frequency storage is a low\-cost long\-term storage solution. Log data in low\-frequency storage also supports query and analysis, visualization, data processing, delivery, and consumption. However, log reading performance is slightly lower than standard storage, making it suitable for storing logs accessed less frequently, such as logs rarely queried or analyzed.<br><br>Low\-frequency storage has the following characteristics:<br><br><br>* Infrequent Access Storage supports near real\-time access to log data, providing second\-level log query and analysis capabilities.<br><br>* The minimum storage duration for Infrequent Access Storage is 30 days, and the maximum is permanent storage. |
|Archive storage |Meets any of the following conditions:<br><br><br>* Standard storage duration is 30 days or more.<br><br>* Standard storage duration of 7 days or more and infrequent access storage duration of 30 days or more. |Archive storage offers a lower\-cost long\-term data storage solution based on standard or infrequent access storage. Archive storage provides minute\-level query and analysis capabilities, suitable for data auditing scenarios.<br><br>Archive storage has the following features:<br><br>The minimum storage duration for archive storage is 60 days, with a maximum of permanent storage. |


<span id="55bcecbd"></span>
## Type comparison

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the query and analysis scope includes standard storage, infrequent access storage, and archive storage, the concurrency limit of archive storage applies.</div>



|Storage type ||Standard storage |Infrequent Access Storage |Archive storage |
|---|---|---|---|---|
|Applicable scenarios ||* Frequently accessed log data<br><br>* High\-performance query and analysis |* Logs with infrequent access<br><br>* Security compliance and root cause analysis scenarios |* Log data that is rarely queried and can tolerate long\-delay query results<br><br>* Data audit scenarios |
|Cost ||0.0115 USD/GB/day |0.005 yuan/GB/day |0.0025 RMB/GB/day |
|Performance |Latency (billions of data) |Millisecond\-level query |Query by second |Query by minute |
||Operation concurrency |* Concurrent count under a single Project<br><br>   * Query: 100<br><br>   * Analysis: 100<br><br>* Concurrent count under a single Topic<br><br>   * Query: 15<br><br>   * Analysis: 15 |Concurrent count under a single Project<br><br><br>* Query: 10<br><br>* Analysis: 2 |Concurrent count under a single Project<br><br><br>* Query: 2<br><br>* Analysis: 2 |
|Activation Conditions ||None. |Standard storage duration is 7 days or more. |Meet any of the following conditions:<br><br><br>* Standard storage duration of 30 days or more.<br><br>* Standard storage duration of 7 days or more and infrequent access storage duration of 30 days or more. |
|Minimum storage duration ||The minimum retention period for Standard Storage is 1 day |Minimum storage duration for archive storage is 30 days. |The minimum storage duration for archive storage is 60 days. |


<span id="5e75b860"></span>
## Function comparison


|Feature |Standard storage |Infrequent Access Storage |Archive storage |
|---|---|---|---|
|Query |✓ |✓ |✓ |
|Query and analysis |✓ |✓ |✓ |
|Context query |✓ |✓ |✓ |
|Rebuild index |✓ |✓ |× |
|dashboard |✓ |✓ |× |
|Data transformation |✓ |✓ |× |
|Data consumption |✓ |✓ |× |
|log shipping |✓ |✓ |× |
|Alarm |✓ |✓ |× |
|Scheduled SQL analysis |✓ |✓ |× |


<span id="27a1a7f3"></span>
## Set storage type

When creating or modifying a log topic, you can set the log data storage type in Log Service by enabling **log retention configuration**. For details, refer to [Log Topic](https://docs.byteplus.com/docs/tls/Managing_topics).

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e2fe2b9020227a9e6d49afd079bbae4f.png) </span>


* Standard storage

   Standard Storage must be enabled.

* Infrequent Access Storage

   After enabling Infrequent Access Storage, log data is first stored in the Standard Storage layer for a set period, which must be longer than 7 days. After this period, log data automatically moves to the Infrequent Access Storage layer for further retention and is deleted automatically once the retention expires.

* Archive storage

   * If only Archive Storage is enabled without Infrequent Access Storage, log data stays in Standard Storage for a set period, which must be longer than 30 days, before automatically moving to Archive Storage. After this period, log data automatically moves to the Archive Storage layer for further retention and is deleted automatically once the retention expires.

   * After enabling infrequent access and archive storage, log data automatically converts from standard storage to infrequent access storage after being stored for a period, then converts from infrequent access storage to archive storage after another period. You need to first set the retention period for log data in the standard storage layer, which should be longer than 7 days, then set the retention period in the infrequent access storage layer, which should be longer than 30 days. After exceeding the set duration, log data automatically moves down the storage layers for continued retention, until it is automatically deleted when storage time expires.
