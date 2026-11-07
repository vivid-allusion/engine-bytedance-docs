---
title: "Download logs and view export history"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Download_logs_and_view_export_history"
---

After completing query analysis, you can download the raw log data or chart analysis results to your local device to view log information and analyze data in one place.

<span id="db0263df"></span>
## Download logs


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. In the top bar, select the region of the instance.

3. Select **Log details** from the left navigation.

4. Select **Download log \> Download log**.

   * To download the queried logs: In the upper right corner of the **Original** tab, select **Download log**.

   * To download retrieval analysis logs: In the upper right corner of the **Table** tab, select **Download log**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ea5176086caf4951809b9dadafee32fd) </span>

5. Set the parameters of the download log.

   
   |Configuration |Description |
   |---|---|
   |Task name |The task name is used as the filename for the compressed log file. |
   |Time range |The time range for log retrieval. To make changes, return to the search analysis page and perform a new search. |
   |Search statement |Log query statements or log search and analysis statements. To make changes, return to the search analysis page and perform the search again. |
   |Log quantity |The number of logs involved in this download task.<br><br><br>* All logs: The total amount of data currently meeting the filter criteria.<br><br>* Custom log quantity: Up to 100,000 search analysis results and 1,000,000 query results can be downloaded at one time. |
   |Export format |Supported export formats are CSV and JSON. |
   |Log sorting |Exported logs can be sorted in ascending or descending order. |
   |Compression type |Compression type for exported files. Currently, gzip and zip formats are supported. |
   


<span id="a4db2473"></span>
## View log export history

After creating a download task, you can view the history and information of log exports in the export history interface.


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. Select the instance's region from the top bar.

3. In the left navigation, select **Log details**.

4. Select **Download log \> Export history**.

5. View export history.

   Includes basic information about the download task, such as file name, file size, number of log entries, compression format, creation time, file format, file description, and status. You can click **Download** in the operation column to download the corresponding file.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Download tasks are performed sequentially according to their creation time. When multiple new tasks are present, please wait patiently while the tasks are being executed.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can view log export records from the past day.   </div>
   

   Descriptions of the status of each downloaded file are as follows:

   
   |Status |Description |
   |---|---|
   |File generation in progress |The compressed file for the download task is being generated. Please wait. |
   |File generation interrupted |If the number of logs to be exported exceeds the limit, the export is truncated, and only the logs within the limit are downloaded.<br><br>For large data volumes, we recommend narrowing the query time range and downloading the data in batches. |
   |A file has been generated |The specified log data has been successfully exported by the log service. You can now download the files. |
   |Waiting |Another download task is already in progress for this topic. Please wait. |
   |Failed |The log export failed due to network fluctuations, index closure, topic deletion, or other issues. Please try downloading again. |
