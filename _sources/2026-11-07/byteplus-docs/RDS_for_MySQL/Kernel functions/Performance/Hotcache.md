---
title: "Hotcache"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Hotcache"
---

This topic describes the hotcache feature of RDS for MySQL.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

When MySQL restarts due to an upgrade or failure, the data cache in its BufferPool is cleared. This action prevents service requests from hitting the cache, which results in frequent disk I/O operations and significantly degrades the SQL performance of the database. To address this issue, RDS for MySQL places the BufferPool memory in shared memory. After a restart, it directly reuses the original memory, reducing service fluctuations in these scenarios.

<span id=".5Y-C5pWw6K-05piO"></span>
### Parameter description


|**Parameter name** |**Default value** |Does it need instance restart to take effect? |Value range |**Scope** |Parameter description |
|---|---|---|---|---|---|
|loose_buffer_pool_enable_hot_cache |off |Yes |[on\|off] |Global |Enables or disables the hotcache feature. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is not open for modification. To modify it, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical support.</div>


<span id=".5pSv5oyB54mI5pys"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.32_20241015 and above.

* MySQL 8.0, with a kernel minor version of MySQL 8.0.32_20241015 or later.

* MySQL 8.4, with a kernel minor version of MySQL 8.4.7_20260415 or later.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can view the kernel minor version of an instance by <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details">Viewing instance information</a>. If your instance is a version earlier than MySQL 5.7.32_20241015 or MySQL 8.0.32_20241015, you can <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version">Upgrade instance kernel minor version</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance has been created and the state of the instance is **Running**.

* The running Value of the loose_buffer_pool_enable_hot_cache Parameter is set to `on`.


<span id=".54q25oCB6K-05piO"></span>
## Status description

RDS for MySQL provides the following parameter to display the current state of hotcache:


|**Parameter name** |**Scope** |**Description** |
|---|---|---|
|Innodb_buffer_hot_cache_state |Global |State of Hotcache reuse:<br><br><br>* `uninit`: Hotcache is not used.<br><br>* `init`: A new hotcache is created.<br><br>* `reuse`: Reusing the previous hotcache. This is an intermediate state before MySQL starts.<br><br>* `reuse_init`: The previous hotcache is reused. |
|Innodb_buffer_hot_cache_state_code |Global |`Hotcache` reuse status code:<br><br><br>* `0`：uninit。<br><br>* `1`：init。<br><br>* `2`：reuse。<br><br>* `3`：reuse_init。 |
|Innodb_buffer_hot_cache_reused_pages |Global |The quantity of pages reused by Hotcache. |
