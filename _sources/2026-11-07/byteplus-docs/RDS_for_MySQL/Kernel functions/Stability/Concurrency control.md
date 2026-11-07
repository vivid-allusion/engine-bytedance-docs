---
title: "Concurrency control"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Concurrency_control"
---

The performance of MySQL can degrade when it encounters burst traffic and resource\-intensive statements. RDS for MySQL limits concurrency for burst traffic and special types of SQL to improve database stability.

<span id=".6YCC55So5Zy65pmv"></span>
## Use cases

The system has sudden high concurrency and resource\-intensive SQL queries. A typical scenario is when the absence of proper indexes causes numerous full table scans, leading to a sharp decline in database performance.

<span id=".5pSv5oyB54mI5pys"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.32_20231015 and above.

* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.32_20231015 and above.

* MySQL 8.4 version, and the kernel minor version is MySQL 8.4.7_20260415 and above.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can view the kernel minor version of an instance by <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details">Viewing instance information</a>. If the kernel minor version of your instance is not within the supported kernel minor version range, you can <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version">Manually upgrading the instance kernel minor version</a>.</div>


<span id=".5L2_55So6K-05piO"></span>
## Instructions

For details about how to use SQL throttling, refer to [SQL throttling](https://docs.byteplus.com/en/docs/DBW/preview-sql-throttle-task-management-for-mysql).
