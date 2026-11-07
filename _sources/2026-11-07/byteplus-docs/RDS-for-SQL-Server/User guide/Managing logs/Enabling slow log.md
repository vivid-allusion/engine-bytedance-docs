---
title: "Enabling slow log"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/enabling-slow-log"
---

This article describes the steps to enable the slow logging function.

<span id="background-information"></span>
## Background information

Slow logging records statements that take longer than the slow logging threshold `long_query_time`(default is 1 second). By analyzing the slow log, you can identify statements that are inefficient to execute and make targeted optimizations.

<span id="precautions"></span>
## Precautions


* Turning on the slow logging feature will have a certain impact on instance performance.

* Only turn on the slow log switch and turn off the slow log switch once per minute.

* The slow logging threshold is supported to be set to 1 to 10 seconds, and only integer values are supported. After modifying the slow logging threshold, you need to restart the slow logging function to take effect.

* When the slow logging feature is turned on, RDS for SQL Server starts generating slow log files.

   * A single slow log file can be up to 50MB. After turning off and restarting the slow log function, a new slow log file will be automatically generated.

   * Keep up to 20 slow log files. When the number of slow log files reaches the maximum, the system deletes the oldest file. If necessary, you can download the slow log file and save it locally. For more information, see [Download slow logs](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-and-download-slow-logs).


<span id="operation-steps"></span>
## **Operation steps**


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **instance list** page, click the target instance name to go to the **instance information** tab.

4. At the top of the page, click the **Log Management** tab, and then click the **Slow Log** subtab.

5. In the **Slow Logging** subtab, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9aed8d19dc25944e92bc4ac004faabec.png) </span> to enable slow logging.

6. (Optional) Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c5f388c2c9e5bf78356c9d2a53d829ff.png) </span> to adjust the slow logging threshold.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The new slow logging threshold will take effect after the slow logging feature is restarted.</div>
