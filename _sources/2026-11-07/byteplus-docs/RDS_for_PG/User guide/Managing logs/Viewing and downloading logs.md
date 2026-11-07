---
title: "Viewing and downloading logs"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/viewing_and_downloading_logs"
---

This topic describes how to view and download logs.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

The RDS for PostgreSQL console displays **switchover logs**, **slow logs**, and **error logs**. Before using the slow log, you need to understand the following information.

Slow SQL refers to SQL queries whose execution time exceeds the set threshold. The slow log is the log file that records these slow queries. In RDS for PostgreSQL, the default SQL query execution time threshold is 1s, set by the log_min_duration_statement parameter. This parameter is a modifiable parameter provided by RDS for PostgreSQL and can be adjusted according to your business needs. For detailed information on modifying parameters, please refer to [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_parameters).

RDS for PostgreSQL also provides the modifiable parameter log_duration to control whether to print the execution time of each statement. This parameter can be set to `on` or `off`. When set to `on`, all user SQL statements are recorded as slow logs; when set to `off`, only SQL statements with execution time greater than log_min_duration_statement are recorded as slow logs. `off` is the default value.

To record only SQL statements with execution time greater than log_min_duration_statement in the logs, ensure log_duration is set to `off` and set the log_min_duration_statement parameter as needed.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL](https://console.byteplus.com/db/rds-pg) console.

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click on the target instance name.

4. View and download log information.



<Tabs>
<Tab zoneid="GxpwBI5SDG" title="Slow log">
<TabTitle>Slow log</TabTitle>

1. At the top of the page, click **Database Workshop**.

2. click the **Slow log** sub\-tab to view the **log collection time**, **SQL statement**, **client IP**, **database**, and **execution time (s)**  of slow logs. Database Workbench provides more comprehensive slow log analysis functions. For details on usage, refer to [Slow log analysis management](https://docs.byteplus.com/en/docs/DBW/slow-log-analysis-management-for-PG).

3. in the **Slow SQL List area,**  click the right side of the page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_83dcbb59826165298df9dedeff4dc52b.png) </span>\> **Export slow log** to download slow log details locally.


</Tab>
<Tab zoneid="AiUwX81Scb" title="Error log">
<TabTitle>Error log</TabTitle>

Error logs can be viewed and downloaded from two entries: the **Database Workshop** tab and the **Logs** tab; choose either method.

<span id="VjHcZULE"></span>
### **Database Workshop**


1. At the top of the page, click **Database Workshop**.

2. On the **Error log details** sub\-tab, view the **Log collection time**, **Log level**, and **Log content** of error logs. Common types of error logs can be found in [List of common error logs](https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_common_error_logs).

3. Click on the right side of the page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_10ee7902f39a3f940a40c69c9dc89d3e.png) </span>\> **Export log** to download error log details locally.


<span id="6be80tE3"></span>
### **Logs**


1. Click on the **Logs** tab on top of the page.

2. On the **Error log** sub\-tab, view the **Log collection time**, **Log level,**  and **Log content** of error logs. Common types of error logs can be found in [List of common error logs](https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_common_error_logs).

3. Click on the right side of the page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0f2c85cadf92234b12a4cd4133f6a943.png) </span>, to download error log details locally.


</Tab>
<Tab zoneid="Lbn7obM7HC" title="Switchover log">
<TabTitle>Switchover log</TabTitle>

1. Click on the **Logs** tab on top of the page.

2. The **Switchover log** sub\-tab displays the **New primary node**, **Old primary node**, **Switch type**, and **Switch time** of primary/secondary switchover logs.

3. Click on the right side of the page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6b242cca90f5d9f171a91c6060cee607.png) </span>, to download error log details locally.


</Tab>
</Tabs>
