---
title: "Context search"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Context-search-2"
---

When you query logs, Torch Log Service (TLS) allows you to view the context of logs in the log source file.

<span id="Limits"></span>
## Limits


* Only logs collected using LogCollector 1.0.6 or later support the context search. Log data uploaded by calling PutLogs through an SDK or using other methods does not support the context search.

* Before you use the context search feature, configure indexes for logs. For more information on how to configure indexes, refer to [Configure indexes](https://docs.byteplus.com/docs/tls/Configure-indexes-2).


<span id="6879adb9"></span>
## Background

When you use the query feature of TLS to query logs, you often want to query the context of a log in the specified file on the specified server. For example, if access fails or an exception occurs, you want to view the related log information based on the event occurrence time, including logs recorded earlier and later than the exception log.

TLS offers the context search feature for you to quickly locate an abnormal log in the console. In addition, TLS visualizes the context information of the log in the specified source file on the specified server. The context search feature is suitable for quickly locating exceptions and failures. The feature helps O&M personnel view peripheral information related to failures and locate problems for troubleshooting.

<span id="4ab559c6"></span>
## Procedure


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. Select the region where torch log service is located from the top navigation bar.

3. In the left navigation pane, select **Common functions** \> **Query and analysis**.

4. On **Query and analysis** page, a list is displayed in the left area. Select the specified project and topic.

5. On the query and analysis page for the specified log topic, enter the query statement and set the time range.

6. On the **Raw Log** tab, locate the specified log and click the search icon.

7. Scroll up or down to view the contextual information of the specified log.

   You can view more information in the following ways:

   * View context in **raw** logs or **table** format.

      By default, the page displays log data in raw log format and positions to the specified log with a serial number of 0. Scroll up to view logs collected before the specified log, with serial numbers as decreasing negative values indicating the number of logs prior to the specified log. Scroll down to view logs collected after the specified log, with serial numbers as increasing positive values indicating the number of logs following the specified log.

   * View log data in **raw** log or **table** format.

   * Use **field configuration** to view only specified log fields.

   * Highlight specified log field values using the **highlight** feature. After setup, this string will appear highlighted in teal in the **log content** column.

   * Filter logs in context by field values containing specified strings using **filter conditions**. After setup, this string will appear highlighted in yellow in the **log content** column.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88067e685ac84a93ae3f9994da8dca8e~tplv-goo7wpa0wc-image.image) </span>

8. Download context query results.

   1. Select **Download \> Download logs** after the filter conditions.

   2. Enter a task name, verify log details, configure the following parameters, and then click **OK**.

      
      |Parameters |Description |
      |---|---|
      |Time range |Select the time range for downloading query logs. |
      |Export format |Select the export format for downloading logs. Supported formats: CSV, JSON, JSONL. |
      |Compression type |Select the compression type for downloading logs. Supported types: No compression, gzip, zip. |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">Notice      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Files are automatically deleted after 1 day by default. Please download the relevant files promptly.      </div>
      

   3. Select **Download \> Export history**.

   4. In the export history list, locate the target download task and click **Download** under **Actions**.
