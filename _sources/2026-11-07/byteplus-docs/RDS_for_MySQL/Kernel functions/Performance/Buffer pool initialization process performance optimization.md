---
title: "Buffer pool initialization process performance optimization"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Buffer_pool_initialization_process_performance_optimization"
---

This topic describes the buffer pool initialization process performance optimization feature of RDS for MySQL.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

A restart is required when upgrading MySQL or modifying certain parameters. When MySQL restarts, it runs a series of processes, such as buffer pool initialization. MySQL becomes available for service only after these processes are complete. Therefore, the performance of the buffer pool initialization process is crucial to the availability of the MySQL instance. This feature speeds up the buffer pool initialization process, reduces MySQL startup time, and enhances the availability of MySQL instances.

<span id=".5pSv5oyB54mI5pys"></span>
## Supported version


* MySQL 5.7 version, and the kernel version is MySQL 5.7.32_20250415 and above.

* MySQL 8.0 version, and the kernel version is MySQL 8.0.32_20250415 and above.

* MySQL 8.4, with a kernel minor version of MySQL 8.4.7_20260415 or later.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can view the kernel minor version of an instance by <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details">Viewing instance information</a>. If the kernel minor version of your instance is not within the supported kernel minor version range, you can <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version">Manually upgrading the instance kernel minor version</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance has been created and the state of the instance is **Running**.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Modify the running value of the loose_buffer_pool_lazy_block_locks_init parameter to `ON` to enable performance optimization for the buffer pool initialization process.


|Parameter name |Default value |Does it need instance restart to take effect? |Value range |Scope |Parameter description |
|---|---|---|---|---|---|
|loose_buffer_pool_lazy_block_locks_init |OFF |Yes |[ON\|OFF] |Global |Enables or disables performance optimization for the buffer pool initialization process. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is not open for modification. To modify it, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical support.</div>


<span id=".5oCn6IO95rWL6K-V"></span>
## Performance test

The test environment is a MySQL 5.7 instance. For instances of different specifications, the elapsed time of the buffer pool initialization process before and after this feature is enabled is as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0ccbbbff15fc8924563fe2b56870c6bc.png) </span>
