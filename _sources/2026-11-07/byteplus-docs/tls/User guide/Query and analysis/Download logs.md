---
title: "Download logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Download-logs-2"
---

When you query and analyze logs collected by the server, you can download either the raw log data or the query and analysis results for local viewing or further analysis.

<span id=".6LS555So6K-05piO"></span>
## Billing description

The log download feature is in public beta and is currently free of charge.

<span id="f9f7c674"></span>
## Limits

When downloading logs, the download task has the following data volume limits:

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div>



* <div data-tips="true" data-tips-type="default">If the data volume is large, we recommend narrowing the query time range and downloading in multiple batches.</div>


* <div data-tips="true" data-tips-type="default">When the download task is running, if you modify the index used in the query statement, download may fail.</div>




|Actions |Description |
|---|---|
|Query or preview logs only |* You can download up to 20 million log entries that meet the query condition at one time, with a maximum data volume of 20 GiB. If limits are exceeded, only the first 20 million log entries or the first 20 GiB of data will be downloaded.<br><br>* When data exceeds 20 GiB, the **Export history** page will show **File generation interrupted**. |
|Query and analyze logs |You can download up to 1 million query and analysis results at one time, with a maximum data volume of 2 GiB. If limits are exceeded, only the first 1 million data entries or the first 2 GiB of data will be downloaded. |


<span id=".5LiL6L295pel5b-X5pWw5o2u"></span>
## Step 1 Create download task

You can download log data via console or API. This topic takes downloading via the console as an example to show the related steps.


1.  Log in to[ TLS console](https://console.byteplus.com/tls).

2. Select the region where log service is located from the top navigation bar.

3. On the left navigation bar, select **Common Features** \> **Query and analysis**.

4. On **Query and analysis** page and in the list of left pane, select the specified project and topic. 

5. On the query and analysis page for the specified log topic, set the time range and enter the query statement.

6. Download log data.

   * Download after query: In the top right corner of the **Raw logs** tab, select **Download Log \> Download Log**.

   * Download after analysis: In the top right corner of the **Chart analysis** tab, select **Download log \> Download log**.

7. Fill out the basic settings for the log download task, and then click **OK**.

   * Offline download

      Create a log offline download task based on the specified query condition. After the task is created successfully, download the log files according to step 2.

      
      |Configuration |Description |
      |---|---|
      |Download method |The log download method, select **Offline download**. |
      |Task name |The name of the log download task, i.e., the name of the log compressed file.<br><br>The download task name can not be duplicated within the same project. |
      |Time range |The time range for the log query. If you need modify them, go back to the **query and analysis** page and run the query again. |
      |Query statements |Log query statements or query and analysis statements. If you need modify them, go back to the **query and analysis** page and run the query again. |
      |Log quantity |The data volume involved in this download. It also means the whole data volume that meets the filter conditions or the data volume of custom download. |
      |Download imprecise query results |Downloading may fail if the query results are imprecise. When enabled, the system continues to download the logs that have been retrieved as imprecise results. |
      |Fully accurate |Determines whether to download result logs based on exact queries only. For details about exact queries, see [Log analysis](https://docs.byteplus.com/docs/tls/Analyze-logs-2).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div><br><br><br><div data-tips="true" data-tips-type="default">This feature is in closed beta. If you have relevant business needs, you can contact your account manager to enable the allowlist.</div><br> |
      |Export format |File format for export. Supports CSV, JSON, and JSONL. |
      |Log sorting |The sort order when only querying without analysis. Supports ascending or descending order. |
      |Compression type |Compression type for exported files. Supports none, zip, and gzip.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div><br><br><br><div data-tips="true" data-tips-type="default">After downloading to your device, use an appropriate decompression tool to decompress the file.</div><br> |
      

   * Save results as

      Save the current page's query results directly to your local device. The downloaded data includes the logs currently loaded.

      
      |Configuration |Description |
      |---|---|
      |Download method |Log download method: choose **Save result as**. |
      |Time range |The time range for the log query. If you need modify them, go back to the **query and analysis** page and run the query again. |
      |Query statements |Log query statements or query and analysis statements. If you need modify them, go back to the **query and analysis** page and run the query again. |
      |Log quantity |The data volume involved in this download. It also means the whole data volume that meets the filter conditions or the data volume of custom download. |
      |Fully accurate |Determines whether to download result logs based on exact queries only. You can refer to [Log analysis](https://docs.byteplus.com/docs/tls/Analyze-logs-2) for details of fully accurate queries.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div><br><br><br><div data-tips="true" data-tips-type="default">This feature is in closed beta. If you have relevant business needs, you can contact your account manager to enable the allowlist.</div><br> |
      |Export format |File format for export. Supports CSV, JSON, and JSONL. |
      |Compression type |Compression type for exported files. Supports none, zip, and gzip.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div><br><br><br><div data-tips="true" data-tips-type="default">After downloading to your device, use an appropriate decompression tool to decompress the file.</div><br> |
      


&nbsp;

<span id="a10c6948"></span>
## Step 2 Download log files


1. Select **Download log \> Export history.** 

2. In the export history list, locate the target download task and click **Download** under **Actions** column.


<span id="76ba9af8"></span>
## Related operations

<span id="aa29d337"></span>
### View download history

After creating a download task, you can select **Download log \> Export history** to view the history of exported logs.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div>



* <div data-tips="true" data-tips-type="default">Download tasks are executed in the order of creation time. If multiple new tasks exist, tasks will be executed one by one.</div>


* <div data-tips="true" data-tips-type="default">You can view log export records from the past day. Log export record and its corresponding file that lasts longer than one day will be automatically deleted.</div>



The export record includes basic information about the download task, such as file name, file size, number of log entries, and compression format.

<span id="9e9f8e8c"></span>
### View download status

After creating a log download task, you can select **Download log\> Export history** to check the file status for each download task. Description of each status is as follows:


|Status |Description |
|---|---|
|File is being generated |The compressed file for the download task is being generated.  |
|File generation interrupted |When exporting data from TLS, if the log volume exceeds the limit, only part of the log data can be downloaded. The excess data can not be exported.<br><br>If the data volume is large, we recommend narrowing the query time range and downloading in multiple batches. |
|File generated successfully |The specified log data has been successfully exported by TLS. You can download the file at any time. |
|Waiting |This topic has download tasks that are in **file generation in progress** status. The download takes a while. |
|Failed |If you encounter network fluctuation, index closure, topic deletion, or other exceptions, log export fails and the file will be marked as **Failed**. |


<span id="c728a331"></span>
### Cancel download task

After creating a download task, you can cancel the download.


1. Select **Download log \> Export history.** 

2. In the export history list, locate the target download task and click **Cancel** in **Actions** column.
