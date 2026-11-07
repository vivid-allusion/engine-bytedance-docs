---
title: "Query logs"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/querying-logs"
---

Cloud Search provides log query functionality. You can select nodes, set log type, log level, keywords, and other filters as needed to quickly locate the instance log content you want to query, facilitating instance maintenance. This topic describes how to query logs.

<span id="dc1b94fe"></span>
## Precautions

Logs are retained for up to 7 days. Within the retention period, you can view historical logs at any point in time.

<span id="5f8ef222"></span>
## Procedure


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click the target instance name.

4. Select **Observability \> Log query** in the left navigation pane of the instance details.

5. On the **Log query** page, select nodes as needed, set log type, log level, keywords, and other filters. The system automatically queries the logs.

   * Supports viewing logs of Data, Master, and Kibana nodes.

   * Supports **Go to bottom** and **Go to top** functions.


<span id="uGnM55HR"></span>
## More operations


* You can export the currently queried logs for local saving.

   1. Select **Log download \> Download logs** in the upper right corner of the **Log query** page.

   2. In the **Download logs** dialog, configure the following parameters, then click **OK**.

      
      |Parameter |Description |
      |---|---|
      |Export format |Select the export log format. Valid values: **CSV** and **JSONL**. |
      |Log sorting |Select the order for exporting logs. Valid values: **ascending** and **descending**. |
      |Compression type |Select the compression type for exporting the log file. Valid values: **no compression**, **gzip**, and **zip**. |
      

   3. In the **export history** info box, wait for the file to generate, then click **download** in the **actions** column.

* You can view the export log history and download previously exported log files.

   Select **Logs download \> export history** at the top right of the **log query** page.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The generated log file is retained by default for 1 day and then automatically deleted. Download it promptly.</div>
