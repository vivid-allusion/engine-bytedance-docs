---
title: "Viewing and download slow logs"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-and-download-slow-logs"
---

This article describes the steps for viewing and downloading slow logs.

<span id="background-information"></span>
## Background information

Slow logging records statements that take longer than the slow logging threshold `long_query_time` (default is 1 second). By analyzing the slow log, you can identify statements that are inefficient to execute and make targeted optimizations.

<span id="view-slow-log"></span>
## **View slow log**


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **instance list** page, click the target instance name to go to the **instance information** tab.

4. At the top of the page, click the **Log Management** tab, and then click the **Slow Log** subtab to view the list of slow log files.

5. Connect to the target instance through the SQL Server client side and get the name of the slow log file. For specific operations on connection instances, see [Connection Instances](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connecting-an-instance).

6. After obtaining the slow log file name, execute the following SQL command to view the slow log details.

   ```sql
   Select * from:: fn_trace_gettable ('D: SQLTrace audit < slow log filename >', default)
   ```
   


<span id="download-slow-log"></span>
## Download slow log


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **instance list** page, click the target instance name to go to the **instance information** tab.

4. At the top of the page, click the **Log Management** tab, and then click the **Slow Log** subtab.

   Check the **Slow Log** subtab to view the list of slow log files. The list of slow log files is sorted in reverse order according to the file update time, and the slow log can be filtered by setting the start date and end date.

5. Click the Download button in the Target Slow Log File Action column to download the log file locally.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the slow log is downloaded locally, you can use SSMS to connect to the local database and then execute the following SQL command to view the slow log details.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">   ```sql
   Select * from:: fn_trace_gettable ('< local address for storing slow log files >', default)
   ```
      </div>
