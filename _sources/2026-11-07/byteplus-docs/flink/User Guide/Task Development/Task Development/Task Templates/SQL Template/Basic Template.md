---
title: "Basic Template"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Basic_Template"
---

During the Flink SQL task development process, developers often need to spend time and effort writing code. The console now offers a rich selection of preset SQL code templates for various scenarios, ready for task development.

<span id="cc738621"></span>
## View SQL Templates


1. Log in to the [BytePlus Flink Console](https://console.byteplus.com/flink).

2. Select the target region in the top menu bar.

3. In the left navigation bar, select **Project Management**, then click on the project block to enter the project.

4. In the left navigation bar of the project, select **Task Development \> Jupyter Lab**.

5. On the **Template Management** page, select **SQL Templates \> Basic Template** and view the template.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de591de6a702423f8b59c00bee6a5315~tplv-goo7wpa0wc-image.image) </span>

6. View template contents, use cases, and supported engine versions.

   
   |**Template Name** |**Use Case** |**Engine Version** |
   |---|---|---|
   |Window Top\-N |If you need to calculate the data currently ranked in the top or bottom within a certain time frame, you can use Window Top\-N. |* Flink 1.11\-byted<br><br>* Flink 1.16\-byted |
   |Create Temporary Table |If you only need to use certain tables in the current session or SQL script, you can use temporary tables. |Flink 1.16\-byted |
   |Create Temporary View |If you need to reuse code, organize extensive queries, or SQL scripts to simplify development in the Flink SQL development process, you can use temporary views. |Flink 1.16\-byted |
   |Rolling Window Aggregation |If you need to group time\-series data and perform aggregation analysis on each group, you can use rolling windows. |* Flink 1.11\-byted<br><br>* Flink 1.16\-byted |
   |Sliding Window Aggregation |If you need to update the data within a window at regular intervals, you can use sliding windows. |* Flink 1.11\-byted<br><br>* Flink 1.16\-byted |
   |Session Window Aggregation |If you need real\-time statistics on user data during an active session, you can use session windows. |* Flink 1.11\-byted<br><br>* Flink 1.16\-byted |
   |Cascading Window Aggregation |If you need to aggregate data from the same stream across different time dimensions (such as 1min, 5min, 30min, 1h), you can use cascading windows. |Flink 1.16\-byted |
   |Pattern Detection (CEP) |In data stream scenarios, if you need to search for a set of event patterns, you can use the MATCH_RECOGNIZE syntax. |* Flink 1.11\-byted<br><br>* Flink 1.16\-byted |
   |Deduplication |If you need to remove duplicate data from the data stream, you can use deduplication syntax. |* Flink 1.11\-byted<br><br>* Flink 1.16\-byted |
   |Temporal Table Join |If you need each piece of data in the stream table to be associated with the corresponding time version data from other tables, you can use Temporal Table Join. |Flink 1.16\-byted |
   |Dimension Table Join |If you need to associate data on a static dimension table, you can use the dimension table Join. |* Flink 1.11\-byted<br><br>* Flink 1.16\-byted |
   |GROUP BY |If you need to perform real\-time aggregation analysis on data, you can use the GROUP BY statement. |* Flink 1.11\-byted<br><br>* Flink 1.16\-byted |
   |INSERT INTO |If you need to write query results into a table in an external storage system, thereby providing them for downstream applications, you can use the INSERT INTO syntax. |* Flink 1.11\-byted<br><br>* Flink 1.16\-byted |
   |Interval Join |If you need to associate data within a specified time range from a table, you can use the Interval Join syntax. |* Flink 1.11\-byted<br><br>* Flink 1.16\-byted |
   |Over Window Aggregation |If you need to perform statistical analysis on each element within a window, you need to use the OVER window. |* Flink 1.11\-byted<br><br>* Flink 1.16\-byted |
   |Regular Join |If you need to perform calculations by associating data from other stream tables, you can use the Regular Join syntax. |* Flink 1.11\-byted<br><br>* Flink 1.16\-byted |
   |Top\-N |If you need to calculate data that ranks among the top or bottom according to business requirements, you can use the Top\-N syntax. |* Flink 1.11\-byted<br><br>* Flink 1.16\-byted |
   |WATERMARK |If you want BytePlus Flink to handle out\-of\-order data correctly, you must use a Watermark.<br><br>You can create a Watermark in the table creation DDL by defining a Watermark generation expression on an existing field, marking it as a time attribute field. |* Flink 1.11\-byted<br><br>* Flink 1.16\-byted |
