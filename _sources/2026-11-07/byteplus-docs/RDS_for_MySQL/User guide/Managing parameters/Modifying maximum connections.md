---
title: "Modifying maximum connections"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_maximum_connectio"
---

This topic describes how to modify the max connections for an RDS for MySQL instance.

<span id=".6IOM5pmv"></span>
## Background

For services that require high concurrency, set a sufficient number of connections to prevent users from being unable to access the database. Therefore, RDS for MySQL instances support modifying max connections through the console and API to accommodate an increase in connection demands.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Supported versions: MySQL 5.7, MySQL 8.0, and MySQL 8.4.

* The default max connections vary depending on the instance specifications. Therefore, when you change the specifications of a primary/standby or read\-only node, the max connections value changes accordingly. However, if you previously modified the max connections, the value will remain unchanged after a specification change. In this case, you must manually adjust the max connections to a reasonable value. If you do not modify the value, the previously reasonable max connections value will be too high after you downgrade the specifications, which may cause a memory overflow.


<span id=".5Y-Y5pu05b2x5ZON"></span>
## Impact

Database connections use memory and CPU resources. The more connections you have, the more resources are consumed. When setting the max connections, consider the availability of database resources and set the value carefully. If `max_connections` is set too high, it can easily cause out\-of\-memory errors. Therefore, we recommend using the default max connections value for the MySQL instance to prevent performance degradation and instability caused by improper configuration.

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description


|Parameter |Description |
|---|---|
|**max_connections** |The maximum number of connections to the entire database is the sum of connections from all database accounts, regardless of the user. he default maximum number of connections varies based on the instance specifications. For details, refer to [Product specifications](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications). If the total number of connections exceeds the upper limit, the system reports an error, and new connections cannot be established.<br><br>Values are as follows:<br><br><br>* For MySQL 5.7 instances:<br><br>   * For instances with MySQL 5.7.44_20260415 and earlier kernel minor versions, the value range is [100\-100000].<br><br>   * For instances with MySQL 5.7.44_20260415 and above kernel minor versions, the value range is [100\-200000].<br><br>* For MySQL 8.0 instances:<br><br>   * For instances with MySQL 8.0.43_20260415 and earlier kernel minor versions, the value range is [100\-100000].<br><br>   * For instances with MySQL 8.0.43_20260415 and above kernel minor versions, the value range is [100\-200000].<br><br>* For MySQL 8.4 instances: MySQL 8.4.7_20260415 and above kernel minor versions, the value range is [100\-200000]. |
|**max_user_connections** |The maximum number of connections for each database user. The default value is `0`, which indicates no limit. If the number of connections for the same account exceeds the upper limit, the system reports an error, and new connections cannot be established.<br><br>Values are as follows:<br><br><br>* For MySQL 5.7 instances:<br><br>   * For instances with MySQL 5.7.44_20260415 and earlier kernel minor versions, the value range is [0\|100\-100000].<br><br>   * For instances with MySQL 5.7.44_20260415 and above kernel minor versions, the value range is [0\|100\-200000].<br><br>* For MySQL 8.0 instances:<br><br>   * For instances with MySQL 8.0.43_20260415 and earlier kernel minor versions, the value range is [0\|100\-100000].<br><br>   * For instances with MySQL 8.0.43_20260415 and above kernel minor versions, the value range is [0\|100\-200000].<br><br>* For MySQL 8.4 instances: MySQL 8.4.7_20260415 and above kernel minor versions, the value range is [0\|100\-200000]. |


<span id=".5L-u5pS55pa55byP"></span>
## Modification method


* Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql) and modify the max connections on the **Parameter configuration** tab. For detailed steps, refer to [Modify parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters).

* Call the API to modify the max connections. For detailed steps, refer to [ModifyDBInstanceParameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstanceparameters).


After making the changes, you can check the **Records of MySQL parameter modification** tab to see if the modified maximum connection count parameter value has taken effect.
