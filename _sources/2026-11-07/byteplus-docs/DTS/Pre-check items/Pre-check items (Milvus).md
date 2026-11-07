---
title: "Pre-check items (Milvus)"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/pre-check-items-milvus"
---

Database Transmission Service (DTS) performs various checks on databases before creating or configuring synchronization tasks for Milvus. This topic introduces the details of check items.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The pre\-check result levels include Error and Warning, as detailed below:</div>



* <div data-tips="true" data-tips-type="default">Error: indicates an error\-level check result. When this type of error occurs during task creation pre\-check, it can not be ignored. Relevant information must be modified according to the prompts before re\-running the pre\-check.</div>


* <div data-tips="true" data-tips-type="default">Warning: indicates a prompt\-level pre\-check result. When this type of error occurs during task creation pre\-check, it can be ignored.</div>




|**Item** |Link |**Check scope** |**Level** |**Check content** |**Remarks** |
|---|---|---|---|---|---|
|Environment detection. |MySQL2Milvus |* Full initialization<br><br>* Schema initialization |Error |Environment detection. |None |
||Milvus2Milvus |Full initialization ||||
|Source end connectivity check |MySQL2Milvus |* Full initialization<br><br>* Schema initialization |Error |Check whether DTS can connect to the source and target Milvus databases.<br><br> |None |
|Milvus source database connectivity check |Milvus2Milvus |Full initialization ||||
|Source database version detection |MySQL2Milvus |* Full initialization<br><br>* Schema initialization |Error<br><br> |Check whether the source database version is supported |The source database versions are all greater than MySQL 5.5. |
|Source Milvus database version detection |Milvus2Milvus |Full initialization |Error |Check whether the source Milvus database version is supported |The supported database engine versions are 2.5 and 2.6. |
|Database connection and architecture wildcard rule check<br><br> |MySQL2Milvus<br><br> |* Full initialization<br><br>* Schema initialization |Error<br><br> |Check the database and schema wildcard rules. |None<br><br> |
||Milvus2Milvus |Full initialization ||||
|Source table/database existence check |MySQL2Milvus |* Full initialization<br><br>* Schema initialization |Error |Check whether the specified tables/databases exist in the source database |None |
|Milvus target database connectivity check |MySQL2Milvus<br><br> |* Full initialization<br><br>* Schema initialization |Error |Check whether the data transmission server can connect to the target Milvus database. |None |
||Milvus2Milvus |Full initialization ||||
|Target Milvus database version detection<br><br> |MySQL2Milvus<br><br> |* Full initialization<br><br>* Schema initialization |Error |Check whether the target Milvus database version is supported. |The supported database engine versions are 2.5 and 2.6. |
||Milvus2Milvus |Full initialization ||||
