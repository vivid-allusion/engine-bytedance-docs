---
title: "Configuring maintenance window"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/configuring-maintenance-window"
---

This article describes how to set the maintainable time period for an instance in the SQL Server Edition console of a cloud database.

<span id="background-information"></span>
## Background information

To safeguard the stability of the cloud database, the backend system will maintain the instance from time to time. In order to ensure business stability and reduce business impact during maintenance, RDS for SQL Server supports configuring maintainable time periods.

<span id="precautions"></span>
## Precautions


* Currently, only changing the maintenance period of the master instance is supported, and setting the maintenance period of the read\-only instance is not supported for the time being.

* The maintainable time period is recommended to be set during the low peak period of the business to avoid affecting the business.

* During the maintainable time period, the instance may experience one or two connection flash breaks. Please ensure that the application has an automatic reconnection mechanism.

* When a task is submitted for execution during a maintainable time period, the instance state changes to **Changing**, and when the task finishes, the instance state changes to **Running**. During this time, it is not supported to perform operations on the instance that require the instance state to be **running**. For details, please refer to the prerequisites for each operation. To avoid disrupting your business, it is recommended to initiate the Set maintainable time period task after a full estimate.

* When an instance is upgraded, it is evaluated based on the maintainable time period set for the instance. If the upgrade cannot be completed within the last maintainable time period, it is postponed to the next maintainable time period.


<span id="prerequisite"></span>
## prerequisite

The [instance was created ](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide)and the instance state is **running**.

<span id="operation-steps"></span>
## Operation steps


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the top menu bar, select Project and Region.

3. In the left navigation bar, click Instance List.

4. On the instance list page, click the name of the target instance.

5. On the Instance Info tab, in the Instance Info area, click Edit after maintainable time period.

6. In the Modify maintainable time period dialog box, after setting the **maintainable time period**, click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The minimum maintenance time interval is 1 hour, and the maximum time interval is 24 hours.   </div>
