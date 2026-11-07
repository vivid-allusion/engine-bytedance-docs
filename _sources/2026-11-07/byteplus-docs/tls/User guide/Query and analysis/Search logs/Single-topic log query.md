---
title: "Single-topic log query"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Query-logs-2"
---

After successfully collecting log data and correctly configuring the index, you can view the collected log data in real time on the Log Service console and query logs within a specified time range using search criteria.

This article describes the steps to query logs for a single topic.

## Precautions

The storage period of log data in Log Service is determined by the **log retention period** of the project. Logs that have expired and been deleted cannot be queried.

## Prerequisites

* The project and log topic have been created.

* Log data has been collected through LogCollector or other methods.

* You must enable the index before querying logs. For steps to enable the index, refer to [Configure Index](https://docs.byteplus.com/docs/tls/Configure-indexes-2).

## Procedure

1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, select **common functions** \> **query and analysis**.

4. In the left list of the **query and analysis** page, select the specified project and log topic.

5. On the query and analysis page for the log topic, specify the time range.

   The default time range is 5 minutes. You can also customize the search time range. Log data stored outside the specified query time range will not be retrieved.

6. Enter search conditions and click **search**.

   * For supported query methods, refer to the [query overview](https://docs.byteplus.com/docs/tls/Query-overview-2). For supported query syntax, refer to the [query syntax](https://docs.byteplus.com/docs/tls/Log-query-syntax-2).

   * If you only query logs without statistical analysis, just enter the query conditions.

   * An empty query means retrieving all logs within the specified time range.

## View query results

After querying logs, you can view the results in the **raw logs** tab.

Log data is reported approximately every minute. If there is no real\-time data in the **raw logs** tab, please wait one minute and refresh to try again.

### Log histogram

The log histogram shows the distribution of logs meeting the query conditions across different time periods. If you do not want to display the histogram, you can click **hide chart**.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bc463e10bea27e02a4161474f2144a74.png)

* Hover the mouse over a blue data block to view its time range, the number of logs matching the query in that period, and whether this query is precise.

* Click a blue data block to drill down and view the finer\-grained log distribution for that time period. The **raw logs** tab will also display the raw log information hit within the specified time range.

* If the **query results** are **precise**, it means all results matching the search criteria within the specified period have been returned.

   > **tip**

   > When the **query results** are **imprecise**, you can refer to [the prompt "query results are imprecise," how to resolve?](https://docs.byteplus.com/en/docs/tls/troubleshooting_query_and_analysis) Tackle the issue accordingly.

* Duration: displays the time taken for this search.

* Timeout: the data volume within the search range is too large, or the search syntax is complex with too many fields, exceeding the data processing capacity of each <shard\>. The page will display **timeout** in this case. It is recommended to narrow the time range and search again.

### Raw logs

The page defaults to showing log data collected within the last 5 minutes in **raw** format.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_02cff6a72884e8d0cf821b705785acb4.png)

|Number |Description |
|---|---|
|1 |Click **Raw** or **Table** to switch log formats.<br><br>The default log display is in **Raw** mode. |
|2 |* Time: supports sorting logs in ascending or descending order.<br><br>* Line break (raw format only): the system enables **line break** by default, displaying each log field on a separate line for clearer viewing.<br><br>* Compact layout (raw format only): when **compact layout** is selected, the system hides the **time** column and shows the log time within the **log content** column.<br><br>* Filter preset fields: selecting **filter preset fields** hides reserved fields from the logging service. For detailed说明about reserved fields, refer to [reserved fields](https://docs.byteplus.com/docs/tls/Reserved-fields-2).<br><br>* More settings:<br><br>   * Filter empty fields: selecting **filter empty fields** hides fields without values.<br><br>   * Use paginator for paging: selecting **use paginator for paging** allows page navigation via the paginator.<br><br>      By default, each query returns up to 100 logs. You can retrieve up to 100,000 logs through paging.<br><br>      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ea9e2d73382d35cf56875c1e36e28e72.png)<br><br>   * Table sorting (only for **table** format): after selecting **table sorting**, the table supports front\-end single\-page sorting.<br><br>   * Flat display of JSON fields: after selecting **flat display of JSON fields**, the system will display JSON fields in a flat format. The flat format uses KEY1.KEY2, for example `child_type.kind:"SERVER"`.<br><br>      Effective only for fields with JSON as the indexed data type.<br><br>   * Tree display of JSON fields: after selecting **tree display of JSON fields**, the system will display JSON fields in a tree structure.<br><br>      Effective only for fields with JSON as the indexed data type.<br><br>   * Force parse JSON fields: after selecting **force parse JSON fields**, the system will forcibly convert logs (json, arrays) into JSON format regardless of the index configuration. Highlighting in query results may fail.<br><br>   * Batch expand or collapse field values (only **raw** format): when a field value is too long, it will be collapsed by default. You can click **expand** in **more settings** to batch expand all currently collapsed field values. To collapse an expanded field value, click **collapse**. <br><br>      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fef89291dc077c5c839d6dc95b60dcfe.png) |
|3 |Click the **expand** icon before the log time to display the **raw log** area, where you can perform the following actions.<br><br>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8a1e1acc7509858acdac12a06c09b312.png)<br><br><br>* Show or hide specified fields<br><br>   Click the eye icon before the target field in the **raw log** area to show or hide the specified field in the raw log.<br><br>* Copy value<br><br>   Click the copy icon before the target field in the **raw log** area to copy the value of the specified field.<br><br>* Query<br><br>   Click the query icon before the target field in the **raw log** area; the system will use the field's value as the search condition.<br><br>* Add query<br><br>   Click the + icon before the target field in the **raw log** area. The system will add the key\-value pair as a search condition, joined by AND operators.<br><br>   For index data fields of JSON type, one\-click add query is supported only after checking **flatten JSON fields**.<br><br>* Exclude from query results<br><br>   Click the \- icon before the target field in the **original log** area. The system will use the key\-value pair as a query condition and append it to the query statement with the NOT operator.<br><br>   For fields with index data type JSON, enabling **flatten JSON fields** supports one\-click exclusion from query. |
|4 |* Context query: Click the **context query** icon corresponding to the target log to view the context information of the specified log in the log source file, including several log entries before and after the collection time. For details, refer to [Querying the context of specified logs](https://docs.byteplus.com/docs/tls/Context-search-2).<br><br>   > **tip**<br>   <br><br>   > Only logs collected by LogCollector version 1.0.6 and later support context query. Logs uploaded via the SDK putLogs interface or other methods do not support context query.<br>   <br><br>* Copy: Click the **copy** icon corresponding to the target log to copy a single log to the clipboard. The copied log text is in JSON format.<br><br>* Expand or collapse field values: Click the **expand** or **collapse** icon corresponding to the target log to expand or collapse the field values of this log entry. |
|5 |* Copy: supports copying the entire field value; if the field value is split by delimiters, copying the tokens is supported.<br><br>* Select a field value and click **Query** to add the field value to the query statement.<br><br>* Select a field value and click **Add to query condition** to add the key\-value pair as a query condition, connected by the AND operator.<br><br>* Select a field value and click **Exclude from query results** to add the key\-value pair to the query condition, connected by the NOT operator. |
|6 |* Download logs: Click **Download logs** to save the raw log data or query and analysis results locally for viewing or further analysis. For detailed instructions, refer to [Download logs](https://docs.byteplus.com/docs/tls/Download-logs-2).<br><br>* Schedule SQL analysis: Click **Save as schedule SQL analysis** to create a scheduled SQL analysis task. For details, refer to [Creating scheduled SQL analysis data storage in log project](https://docs.byteplus.com/docs/tls/create_a_scheduled_sql_task). |
|7 |* Quick analysis: Click a field name to quickly analyze the distribution of its values over a recent period. For detailed instructions, refer to [Quickly analyze specified log fields](https://docs.byteplus.com/docs/tls/Quick-analysis-2).<br><br>   If it is a JSON secondary field, setting the field index for the secondary field is required to display the secondary field list in the quick analysis area.<br><br>* Hide and show fields: click the **Show Fields** hide icon to the right of the field name to set the field as hidden in query and analysis results. Click the **Show** icon to the right of the field name in **Hidden Fields** to restore the field’s display.<br><br>* Set display order: drag fields with the mouse to customize their display order. If there are many fields, you can also quickly locate a specific field using the search box. |

### Sort logs by high\-precision timestamps

When collecting logs, enable the nanosecond time precision feature. Then, on the query and analysis log page, select **nanosecond query precision** to sort logs by nanosecond timestamps. For specific steps to enable nanosecond time precision during collection, refer to [enabling LogCollector high-precision time](https://docs.byteplus.com/docs/tls/Enable-LogCollector-high-precision-time).

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_55978381515bf1a5e0231c4ac6e20a4f.png)
