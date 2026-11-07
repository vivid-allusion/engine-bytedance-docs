---
title: "Download logs and view export history"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Download_logs_and_view_export_history"
---

After completing the query analysis, you can download the original log data or chart analysis results to your local machine for centralized log information viewing and data analysis.

<span id="db0263df"></span>
## Download logs


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/region:waf+cn-beijing/overview?).

2. Select the region where the instance belongs in the top bar.

3. In the left navigation, select **Log Management** to enter the log management page.

4. Select **Download logs \> Download logs**.

   * If you need to download the queried logs: select **Download logs** at the top right corner of the **Original Logs** tab.

   * If you need to download the search analysis logs: select **Download logs** at the top right corner of the **Chart Analysis** tab.

5. Set the parameters for downloading logs.

   
   |Configuration |Note |
   |---|---|
   |Task name |The name of the log download task, which will be applied to the log compressed file name. |
   |Time range |Time range for log retrieval. If modification is needed, please return to the retrieval analysis page and re\-retrieve. |
   |Retrieval statement |Log query statement or retrieval analysis statement. If modifications are needed, please return to the retrieval analysis page to search again. |
   |Log quantity |The number of logs involved in this download task.<br><br><br>* All logs: The total amount of data currently meeting the filtering conditions.<br><br>* Custom log quantity: Supports downloading up to 1000 retrieval analysis results at a time, and 1 million query results. |
   |Export format |The file format for export, supports CSV file format or JSON format. |
   |Log sorting |Sorting method for exported logs, supports ascending or descending order. |
   |Compression type |The compression type of the exported file currently supports gzip format. |
   


<span id="a4db2473"></span>
## View log export history

After creating a download task, you can view the historical records and information of log exports in the export history interface.


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/region:waf+cn-beijing/overview?).

2. Select the instance's region from the top bar.

3. Select **Log Management** from the left navigation to enter the log management page.

4. Select **Download Log \> Export History**.

5. View the export history.

   It includes basic information about download tasks, such as file name, file size, number of log entries, compression format, creation time, file format, file description, and status. You can click **Download** in the action column to download the corresponding file.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Download tasks are executed in order based on creation time. If there are multiple new tasks, please be patient while the tasks are being executed.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Supports viewing the log export records of the last 1 day; log export records and corresponding log files older than 1 day will be automatically cleared.   </div>
   

   The status of each downloaded file is described as follows:

   
   |Status |Description |
   |---|---|
   |File generation in progress |The compressed file corresponding to the download task is being generated, please be patient. |
   |File generation interrupted |When exporting data from the log service, if the log volume exceeds the limit, only part of the log data can be downloaded, and the excess data cannot be successfully exported. When the data volume is large, it is recommended to narrow the query time range and download in multiple batches. |
   |The file has been generated |The log service has successfully exported the specified log data, and the file can be downloaded. |
   |Waiting |There are download tasks in progress for files in this Topic, please be patient. |
   |Failed |Log export failed due to network fluctuations, index closure, Topic deletion, or other exceptional circumstances. Please try downloading again. |
