---
title: "Viewing master and standby switch log"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-master-and-standby-switch-log"
---

This article describes the steps to view the active and standby switch log.

<span id="background-information"></span>
## Background information

The active and standby switch log shows the active and standby node switching process during the running of the instance. Since the main and standby node switching generally takes 30~60 seconds to complete, during which each database will have 1~2 flash breaks, by viewing the main and standby switching log, you can have a more accurate and comprehensive understanding of the instance operation.

<span id="operation-steps"></span>
## **Operation steps**


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **instance list** page, click the target instance name to go to the **instance information** tab.

4. At the top of the page, click the **Log Management** tab, and then click the **Master and Standby Switch Logs** subtab to view the list of master and standby switch logs.

   In the primary and standby switching log list, the new and old primary nodes, switching type and switching time information are displayed after the primary and standby switching. There are two types of switching: **user** and **system**. You can filter the log by setting the start date and end date, and display the full amount of switching logs by default when not filtering.
