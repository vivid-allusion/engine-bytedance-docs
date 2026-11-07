---
title: "Viewing error logs"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-error-logs"
---

This article describes the steps to view the error log.

<span id="background-information"></span>
## Background information

The error log records the error information during the running of the instance. By analyzing the error log, the running status of the instance can be known in time.

<span id="operation-steps"></span>
## **Operation steps**


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **instance list** page, click the target instance name to go to the **instance information** tab.

4. At the top of the page, click the **Log Management** tab, and then click the **Error Log** subtab to view the list of error logs.

   * In the error log list, the generation time, information source, and log details of the error log are shown.

   * Error logs are displayed in reverse order according to generation time, with a maximum of 10,000 error log messages displayed. The log can be filtered by setting the start date and end date, and the error log of the last 24 hours will be displayed by default when not filtered.

   * Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4bbccf23366725216a366304b4c35433.png) </span> button in the target error log details column to copy the log details.
