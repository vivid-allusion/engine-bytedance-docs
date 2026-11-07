---
title: "Log query"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/log_query"
---

Log query enables individual queries of log details collected through the App's monitoring function based on DID, UUID, SSID, or UserID.

<span id=".5pON5L2c5q2l6aqk"></span>
## Operation Procedure


1. Log in to [Application Performance Full Trace Edition Console](https://console.byteplus.com/observe/apmplus-client/console/overview).

2. On the top navigation bar, select the target region.

3. In the left\-side menu, select **Client monitoring**, then locate and click the target application name.

4. Click **App Monitoring** under the target application.

5. In the upper left corner of the console, select **All features** \> **Log query**.

6. On the **log query** page, perform the relevant configuration.

   
   |**Parameters** |**DescriptionS** |
   |---|---|
   |Query dimensions |* **DID**：Device ID。<br><br>* **UUID**: Universally Unique Identifier, a universally unique identification code.<br><br>* **SSID**: Service Set Identifier, service set identifier.<br><br>* **UserID**: The user's UserID. |
   |time |* **Recent**: The recent period, ranging from 1 to 24 hours.<br><br>   For example, if you select 24, the system will display logs from the current time forward within the next 24 hours by default.<br><br>* **Date**: The specific date. You can select a date and specific time.<br><br>   For example, if you select 2022\-09\-20 11:40:30, by default logs from the 8 hours preceding the selected time will be displayed. |
   |Log attributes |* All<br><br>* Crash log, lag log, start log, crash protection log, custom error log, network analytics, event analytics, page load, frame rate, frame loss, memory metric, memory log<br><br>* Battery analytic, power consumption factors, battery exception<br><br>* CPU metric, thread CPU metric, and CPU anomaly<br><br>* JavaScript error, AJAX request, session performance, Dart exception<br><br>* Slow functions, slow messages, MetricKit log, Metric performance log, application exit cause<br><br>* disk metrics, disk anomaly, directory analytic, traffic metric, traffic anomaly<br><br>* user session duration, background usage duration |
   

7. Display log query results.

   Query results description:

   * **log** area

      * You can select **load the previous 8 hours of data** and **load the next 8 hours of data** to view the log context.

      * You can filter by event types and logs.

         
         |**Parameters** |**DescriptionS** |
         |---|---|
         |Event types |Supports filtering by event type, including all event types found in the queried log. |
         |Log filter |Supports entering keywords to filter titles and detailed reports. |
         

   * **Details** area

      * Click **Show custom dimension parameters** to view the parameters and values of the custom dimension.

      * Click **Download log file** to download the `.json` file and view the original log.

   * **Detailed reporting** area

      * Click **view issue details**, and you will be redirected to the crash details page for that issue.
