---
title: "Performance monitoring management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Performance_monitoring_management"
---

The Database Workshop (DBW) supports performance monitoring, providing a wide range of performance metrics. These metrics allow you to view the performance trends of database instances and promptly identify potential risks. This topic introduces the performance monitoring metrics and the steps to view them, helping you understand the operational status of your database instances.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A NDB for MySQL instance and account has been created, and the instance status is running. For detailed operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts#.5Yib5bu66LSm5Y-3).

* If the target instance has security control enabled, you need to apply for read\-only or read\-write operation permissions for the target instance for the current account. For more information, refer to  [Enabling instance security controls (NDB for MySQL)](https://bytedance.larkoffice.com/6956/1262771), and [Applying for operation permissions (NDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Do not modify the instance configurations during the use of performance monitoring, as it may prevent you from viewing the instance's performance monitoring information.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DBW Console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the Observation and diagnosis page, switch the instance type and ID.

   1. In the upper\-right corner of the Observation and diagnosis page, switch the instance type to NDB for MySQL.

   2. In the upper\-left corner of the Observation and diagnosis page, switch the target instance by instance ID or name.

5. On the Observation and diagnosis page, click Performance monitoring to view the instance's monitoring information.

   For detailed information on monitoring metrics, refer to the [Monitoring metrics description](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Monitoring_metrics).
