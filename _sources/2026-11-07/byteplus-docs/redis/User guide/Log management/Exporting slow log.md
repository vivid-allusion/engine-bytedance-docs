---
title: "Exporting slow log"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/export-slow-log"
---

Cache for Redis supports log management, allowing you to view or export details of slow logs (such as slow query statements and execution time) within a specified time period. This topic contains instructions on how to check slow logs. This topic describes how to export slow log.

## Limits

* You can view and export slow log details within the last 3 days.

* You can export up to 10,000 logs at a time. If the logs to be exported exceed 10,000, you need to perform multiple exports.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, select the **Logs** tab.

5. On the **Slow logs** sub\-tab, click ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_79fd9094eb01b1e0f325f9af1f38225b.jpg) icon in the upper right corner of the list.

   > **tip**

   > You can specify the query time range on the upper\-left corner of the list, or use node ID to filter out and export the relevant slow log query results in the list.

6. Click **OK**.

   > **tip**

   * > After clicking **OK**, the slow log information will be exported as a CSV file and automatically downloaded to your local device via your browser. You can view the file using a text editor.

   * > You can export up to 10,000 logs at a time. If there are more than 10,000 log entries to be exported, you need to wait for the previous 10,000 log entries to finish exporting, then click **OK** again to export the remaining log entries.

   * > The exported query results will display the slow request's **Node ID**, **Execution start time**, **Execution time (μs)**, **Statement**, as well as the involved **Database name**, **Client IP address**, and **Accounts** details.
