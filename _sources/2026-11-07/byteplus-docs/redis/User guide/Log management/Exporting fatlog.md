---
title: "Exporting fatlog"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/export-fat-log"
---

Cache for Redis supports logs management, allowing you to view or export fatlog details (such as query statements and statement length) within a specified time range on the console. This topic describes how to export fatlogs.

## Limits

* You can view and export fatlog details for the last 3 days.

* You can export up to 10,000 logs at a time. If the logs to be exported exceed 10,000, you need to perform multiple exports.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, select the **Logs** tab.

5. On the **Fatlogs** sub\-tab, select the node type as needed (**server node** or **proxy node**), then click the top\-right corner of the list.![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_79fd9094eb01b1e0f325f9af1f38225b.jpg)icon on the right of the tags.

   > **tip**

   > You can specify the query time range on the upper\-left corner of the list, or use node ID to filter out and export the relevant fatlog query results in the list.

6. Click **OK**.

   > Description

   * > After clicking **OK**, the fatlog information will be exported as a CSV file and automatically downloaded to your local device via your browser. You can view the file using a text editor.

   * > You can export up to 10,000 logs at a time. If there are more than 10,000 log entries to be exported, you need to wait for the previous 10,000 log entries to finish exporting, then click **OK** again to export the remaining log entries.

   * > The exported query results display details of fatlog query requests, including **Node ID**, **Execution start time**, **Statement**, **Statement length**, and **Client IP address**.
