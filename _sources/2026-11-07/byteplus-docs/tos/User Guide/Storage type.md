---
title: "Storage type"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-storage-type"
---

This topic explains the different types of storage supported by TOS, including when they are used and how they are different.

<span id="9cc05640"></span>
## Use cases


|**Storage type** |**Use cases** |
|---|---|
|Standard Storage |High availability, reliability, and performance, suitable for frequently accessed data. |
|Infrequent Access Storage |Designed for infrequently accessed data, with a minimum storage duration of 30 days. |
|Intelligent Tiering |Designed for data with unpredictable access patterns. It automatically moves data between storage types based on how often it's accessed to reduce storage costs. |
|Flashback Archive |Designed for rarely accessed data, with a minimum storage duration of 90 days. It retrieves data instantly and moves it to another storage type, allowing you to read it directly without having to restore it first. |
|Archive |Designed for long\-lived, rarely accessed data, with a minimum storage duration of 90 days. You must first restore archived data before you can access it.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Cross\-region replication or same\-region replication of archived objects is not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Append operations are not supported for archived objects.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Multi\-AZ redundancy is not available for archived objects.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you want to use CopyObject, GetObject, SetObjectMeta, or UploadPartCopy APIs to manage archived objects, or if you want to move, rename, or download them, you must first restore the objects.</div><br> |
|Cold Archive |Designed for cold data that is long\-lived and rarely accessed. Data must be stored for at least 180 days. You must first restore cold archived data before you can access it.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Cold Archive is only supported in China (Beijing), China (Shanghai), and China (Guangzhou).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Cross\-region replication or same\-region replication of cold archived objects is not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Append operations are not supported for cold archived objects.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Multi\-AZ redundancy is not available for cold archived objects.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you want to use CopyObject, GetObject, SetObjectMeta, or UploadPartCopy APIs to manage cold archived objects, or if you want to move, rename, or download them, you must first restore the objects.</div><br> |
|Deep Cold Archive |Designed for extremely cold data with ultra\-long retention needs. Data must be stored for at least 180 days. You must first restore deep cold archived data before you can access it.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Deep Cold Archive is only supported in China (Beijing), China (Shanghai), and China (Guangzhou). Deep Cold Archive is currently in closed beta. Please contact your account manager for access.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Cross\-region replication or same\-region replication of deep cold archived objects is not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Append operations are not supported for deep cold archived objects.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Multi\-AZ redundancy is not available for deep cold archived objects.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you want to use CopyObject, GetObject, SetObjectMeta, or UploadPartCopy APIs to manage deep cold archived objects, or if you want to move, rename, or download them, you must first restore the objects.</div><br> |


<span id="7154fc59"></span>
## Supported regions


* ✅: Supported.

* ✔️: Available for closed beta.

* ❌: Not supported.



|**Region** |**Standard Storage** |**Infrequent Access Storage** |**Intelligent ** Tiering |**Flashback Archive** |**Archive** |**Cold Archive** |**Deep Cold Archive** |
|---|---|---|---|---|---|---|---|
|China (Beijing) |✅ |✅ |✅ |✅ |✅ |✅ |✔️ |
|China (Shanghai) |✅ |✅ |✅ |✅ |✅ |✅ |✔️ |
|China (Guangzhou) |✅ |✅ |✅ |✅ |✅ |✅ |✔️ |
|China (Hong Kong) |✅ |✅ |✅ |✅ |✅ |❌ |❌ |
|Asia Pacific (Johor) |✅ |✅ |✅ |✅ |✅ |❌ |❌ |
|Asia Pacific (Jakarta) |✅ |✅ |✅ |✅ |✅ |❌ |❌ |


<span id="7405d9eb"></span>
## Comparing storage types


|**Category** |**Standard Storage** |**Infrequent Access Storage** |**Intelligent Tiering** |**Flashback Archive** |**Archive** |**Cold** **Archive** |**Deep Cold Archive** |
|---|---|---|---|---|---|---|---|
|Designed data durability (single\-AZ) |99.999999999% (11 nines) |99.999999999% (11 nines) |99.999999999% (11 nines) |99.999999999% (11 nines) |99.999999999% (11 nines) |99.999999999% (11 nines) |99.999999999% (11 nines) |
|Designed data durability (multi\-AZ) |99.9999999999% (12 nines) |99.9999999999% (12 nines) |99.9999999999% (12 nines) |99.9999999999% (12 nines) |Not applicable |Not applicable |Not applicable |
|Designed service availability (single\-AZ) |99.99% |99.00% |Uses the access tier of the object before the transition |99.00% |99.00% (after you restore data) |99.00% (after you restore data) |99.00% (after you restore data) |
|Designed service availability (multi\-AZ) |99.995% |99.5% |Uses the access tier of the object before the transition |99.5% |Not applicable |Not applicable |Not applicable |
|Minimum billable object size |64 KiB<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For objects in a given region that are smaller than 64 KiB: if the number of such objects reaches or exceeds 1 billion, each object will be billed as 64 KiB. If the number remains below 1 billion, the objects are charged at their actual size.</div><br> |64 KiB<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Objects smaller than 64 KiB are charged as 64 KiB, and objects equal to or larger than 64 KiB are charged at actual size.</div><br> |None |64 KiB<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Objects smaller than 64 KiB are charged as 64 KiB, and objects equal to or larger than 64 KiB are charged at actual size.</div><br> |64 KiB<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Objects smaller than 64 KiB are charged as 64 KiB, and objects equal to or larger than 64 KiB are charged at actual size.</div><br> |64 KiB<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Objects smaller than 64 KiB are charged as 64 KiB, and objects equal to or larger than 64 KiB are charged at actual size.</div><br> |64 KiB<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Objects smaller than 64 KiB are charged as 64 KiB, and objects equal to or larger than 64 KiB are charged at actual size.</div><br> |
|Minimum storage duration |None |30 days |Same as Intelligent Tiering rules |90 days |90 days |180 days |180 days |
|Storage cost |Standard |Lower |Based on the access frequency |Lower |Lower |Very low |Extremely low |
|Request cost |Standard |Higher |Higher, with additional object monitoring fees charged. |Higher |Higher |Higher |Higher |
|Data retrieval cost |None |Per\-GiB retrieval fees apply. |None |Per\-GiB retrieval fees apply. |Per\-GiB retrieval fees apply. |Per\-GiB retrieval fees apply. The price of each unit depends on the restoration options chosen. |Per\-GiB retrieval fees apply. The price of each unit depends on the restoration options chosen. |
|Data access |Real\-time access with millisecond latency. |Real\-time access with millisecond latency. |Real\-time access with millisecond latency. |Real\-time access with millisecond latency. |You need to restore objects before reading them. Retrieval time is within one minute. |You need to restore objects before reading them. Restoration options are as follows:<br><br><br>* Quick: 1–5 minutes<br><br>* Standard: 2–5 hours<br><br>* Batch: 5–12 hours |You need to restore objects before reading them. Restoration options are as follows:<br><br><br>* Standard: Within 12 hours<br><br>* Batch: Within 48 hours |
|Use cases |Designed for various social and media\-sharing platforms for images, audio, and video, large\-scale websites, big data analytics, and similar use cases such as software download services and mobile applications. |Designed for infrequently accessed data (once or twice a month), such as hot backup data and surveillance video data. |Designed for data with unpredictable access patterns, such as video logs. |Designed for long\-lived, rarely accessed data, such as archives. |Designed for long\-lived, rarely accessed data, such as medical imaging data. |Designed for rarely accessed data with ultra\-long retention needs, such as archives. |Designed for business needs that require storing data for a really long time. Some examples are storing raw data in the big data and artificial intelligence fields, keeping media archives for good, storing data for legal and compliance reasons, and replacing tapes. |
|Parameter value |STANDARD |IA |INTELLIGENT_TIERING |ARCHIVE_FR |ARCHIVE |COLD_ARCHIVE |DEEP_COLD_ARCHIVE |
