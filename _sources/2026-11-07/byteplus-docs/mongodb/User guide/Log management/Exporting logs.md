---
title: "Exporting logs"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/export-log"
---

Document Database for MongoDB supports logs management. You can export slow logs, error logs, and running logs that meet query conditions from the console to your local device for management. This topic describes how to export logs.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* You can view and export log details within the last 7 days.

* The amount of log data that can be exported in a single operation is subject to the following constraints:

   * Maximum 20 MiB of log data per export.

   * Maximum 1,000 records per export.

   If the exportable log data within your selected time range exceeds 20 MiB or 1,000 records, please narrow the query time range and export in batches.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Slow logs, error logs, and running logs are exported in the same way. This topic describes the procedure for exporting slow logs as an example.</div>



1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **Logs** tab.

6. Under the **Slow log** sub\-tab, click <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_79fd9094eb01b1e0f325f9af1f38225b.jpg) </span> icon.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can first specify the query time range, component, or node ID in the upper\-left corner of the list to filter the log results you need, and then export them.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To export error logs or running logs, first navigate to the corresponding log sub\-tab, then click <img src="https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_79fd9094eb01b1e0f325f9af1f38225b.jpg" width="14px" /> icon to export.   </div>
   

7. In the dialog box that pops up, select the target log information (such as query statements and execution start time of slow logs) based on the business requirements and then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After clicking <strong>OK</strong>, the instance list information will be exported as a CSV file and automatically downloaded to your local device via the browser. You can view the file using a text editor.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Log details that can be exported vary with log types. The specific information is subject to the console.   </div>
