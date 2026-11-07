---
title: "Error log management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Error_log_management"
---

This topic describes how to view and download error logs on the Database Workshop (DBW) console.

<span id="ok1fZDjY"></span>
## Prerequisites


* An instance and account for RDS for MySQL have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts#.5Yib5bu66LSm5Y-3).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, refer to [Enabling instance security control (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql), and [Applying for operation permissions (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket).


<span id="UbPmXlow"></span>
## Precautions


* When you access the Log management tab through Operation observability on the left navigation bar, error log information about the first instance in the Instance list is viewed by default.

* When downloading error logs, note the following:

   * A single download supports up to 10,000 log entries.

   * Downloaded error log files are retained for 1 day by default. Expired files will be automatically deleted. Save the downloaded files to your computer promptly.

   * You can view and export downloaded error log files in the export history.


<span id="TPGEBs8x"></span>
## Query an error log


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

3. On the top menu bar, select the project and region.

4. In the upper\-right corner of the **Observation and diagnosis** page, select RDS for MySQL. Click the drop\-down icon next to the instance name and select the target instance.

5. On the **Observation and diagnosis** page, click **Log management**.

6. Click the **Error log details** sub\-tab and select a node in the instance to view the error log information of the node, including **Collection time**, **Log level**, and **Log content**. You can also filter the target error logs by time and keyword.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can filter error logs within a specified time range as needed. When selecting a time range, the query end time must be later than the start time.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Fuzzy queries are supported when you use keywords to search for error logs.   </div>
   


<span id="5GigzINW"></span>
## Download an error log

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">A single download supports up to 10,000 log entries.</div>


* <div data-tips="true" data-tips-type="warning">Downloaded error log files are retained for 1 day on the DBW console by default. Expired files will be automatically deleted. Save the downloaded files to your computer promptly.</div>


* <div data-tips="true" data-tips-type="warning">View and export the download file of error log in export history.</div>


* <div data-tips="true" data-tips-type="warning">Downloading error logs downloads the data in the error log list to the local device. Therefore, before downloading error logs, filter the logs to be downloaded in the error log list first.</div>


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, switch the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. In the upper\-left corner of the **Observation and diagnosis** page, click the drop\-down icon next to the instance name and select the target instance.

5. On the target instance page, click **Log management**

6. Click the **Error log details** sub\-tab, and filter the target error log in the error log list as required.

7. Click Download <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_79fd9094eb01b1e0f325f9af1f38225b.jpg) </span> chart, and select **Export log**.

8. In the **Export error log details** dialog box, select the format of the exported file as required, and click **OK**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The exported file format supports <code>csv</code> and <code>json</code> formats.   </div>
   

9. In the **Export history** dialog box, select the target task with **Status** as **Generated**, and click **Download file** in the **Actions** column to download the exported file locally.
