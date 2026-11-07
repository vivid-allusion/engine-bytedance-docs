---
title: "Big key analysis"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/big-key-analysis"
---

Cache for Redis supports performance analysis, allowing you to view the details of big keys and hot keys in the database in real time while using Redis. It also supports viewing historical details of big keys and hot keys. This topic describes how to use the big key analysis feature.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Performance analysis** tab.

5. On the **Big key analysis** sub\-tab, perform the following operations to view the big key distribution.

   |Console area |Supported operations |Description |
   |---|---|---|
   |Line chart area |In the **Used memory** area, specify the query time for memory usage. You can quickly identify time periods that may generate big keys based on the trend of the **Used memory** line chart. |* You can click the time query shortcut keys in the upper left corner of the line chart (such as **1 hour**, **3 hours**, etc.) to quickly specify the query time range.<br><br>* The data display granularity on the line chart is different when the query time range is different. For example, when the query time range is 1 day, the data display granularity is 30 minutes. The specific display granularity is subject to the console display.<br><br>* The **Used memory** line chart displays the memory usage information for the last 1 day by default. You can view the most recent memory usage information and big key details for up to 15 days. |
   |Big key list area |Click on any time point on the line chart of **Used memory** to view the detailed distribution of big keys in the corresponding time period, including specific key names, data types, memory usage, element numbers, and database names. |* If you do not click on any time point on the **Used memory** line chart, the big key list will by default display the big key distribution corresponding to the last monitoring point on the line chart. For example, if the time you specified in the previous step is from May 21, 2024, 00:00:00 to May 22, 2024, 00:00:00 (at this time, the data display granularity is 30 minutes), then the last monitoring point on the **Used memory** line chart is May 22, 2024, 00:00:00. If there is a big key in this time period, then the big key list will default to showing the big key distribution from May 21, 2024, 23:30:00 to May 22, 2024, 00:00:00.<br><br>* Related information about big keys is displayed in the list only when big keys exist in the database. For more information on how to determine big keys, refer to [Detection criteria](https://docs.byteplus.com/en/docs/redis/performance-issue-and-solution#.5Yik5pat5qCH5YeG).<br><br>* By default, the big key list displays details for the top 50 keys with the highest memory usage in the Redis instance at the specified time. You can also click **By Element Count** to display details for the top 50 keys with the most elements at the current time.<br><br>* By default, details of big keys are queried from all data types. You can also select the required data type from the **Data type** drop\-down box to filter and display the results. Currently supported data types for viewing are String, List, Set, Zset, Hash and Stream.<br><br>* Keys with different data types support different statistical information for display:<br><br>   * Keys of String type will display the specific memory usage in the **Memory usage(Bytes)**  column, while the **Number of element(s)**  column defaults to 1.<br><br>   * Keys of non\-String type will display specific numerical values in the **Number of element(s)**  column. At the same time, an estimated memory usage value will also be displayed in the **Memory usage(Bytes)**  column. This memory usage value is for reference only.<br><br>      > **tip**<br>      <br><br>      > Currently, only Redis 7.0 version instances support the above functions. In instances of Redis 6.0 and below versions, for keys of non\-String type, only the specific numerical values will be displayed in the **Number of element(s)** column, and the **Memory usage(Bytes)** column defaults to empty.<br>       |
   ||Click ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_79fd9094eb01b1e0f325f9af1f38225b.jpg) icon in the upper right corner of the big key list to download the current big key analysis result to the local for management. |The big key list information will be exported as a CSV file and automatically downloaded to the local device through the browser. You can view this file with a text editing tool. |

## Relevant APIs

|API |Description |
|---|---|
|[DescribeBigKeys](https://docs.byteplus.com/en/docs/redis/describebigkeys) |Call the DescribeBigKeys API to view the details of big Keys of target instance within specified time windows. |
