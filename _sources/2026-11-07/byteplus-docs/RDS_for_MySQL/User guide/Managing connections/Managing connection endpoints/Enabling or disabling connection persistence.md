---
title: "Enabling or disabling connection persistence"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_connection_persistence"
---

This topic describes the steps to configure connection persistence for an RDS for MySQL instance.

<span id="VcOyuPvb"></span>
## Background

When you use RDS for MySQL, performing a switchover operation on an instance causes a brief interruption in the connection between the application and the database proxy. This can impact your business. To address this, RDS for MySQL provides the connection persistence feature, which ensures stable connections, improves product availability, and reduces operation costs.

<span id="FsMJANKQ"></span>
## Precautions


* The connection persistence feature cannot maintain connections when prepare is enabled.

* The connection persistence feature cannot maintain connections when you restart the entire instance, which means the restart scope is set to All nodes.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For multiple\-node instances, selecting a restart scope is not supported. You can only restart the entire instance.   </div>
   

* The connection persistence feature will take effect within 10 minutes when it is enabled or diabled.

* Connections for which the MySQL server has not completely returned data packets. For example, for a 100 MB result set, only 50 MB has been returned, and the remaining result set is still being transmitted.

* Uncommitted transactions exist.

* Unparsed statements have been used on the connection.

* LOAD DATA statements have been used on the connection.

* Temporary collections exist.

* Connections that subscribe to Binlog through the database proxy address.

* Calls to the `FOUND_ROWS`, `ROW_COUNT`, and `LAST_INSERT_ID` functions are not supported. Although these functions can be called successfully, the accuracy of the results cannot be guaranteed. `SELECT FOUND_ROWS()` has been deprecated by MySQL. It is recommended to replace `SELECT FOUND_ROWS()` with `SELECT COUNT(*) FROM tb1` for queries. For details, refer to [FOUND_ROWS()](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_found-rows).

* Because connections may reconnect, the thread ID of the current connection returned by `SELECT CONNECTION_ID()` may change.

* Because connections are re\-established, the Internet protocol address and port displayed in `SHOW PROCESSLIST` or **SQL Insight** may not match those of the client.

* If a connection contains user\-defined variables, the connection can be maintained, but the variables will become invalid.


<span id="fAiOKoZ9"></span>
## Prerequisites


* An instance has been created, and its state is **Running**. For more details, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* The database proxy feature is enabled for the instance. For details about enabling the database proxy, refer to [Enable database proxy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enable_database_agent).


<span id="RwmUMjRE"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. In the left navigation bar, choose **MySQL** \> **Instances**.

4. On the **Instances** page, click the target instance name.

5. Click the **Connectivity** tab at the top of the page.

6. On the **Connectivity** page, in the **Endpoints** list, click **Edit** in the **Actions** column for the target connection endpoint to open the **Modify endpoint** page.

7. On the **Modify endpoint** page, enable or disable connection persistence, and then click **OK**.


<span id="nmrOUwRi"></span>
## **Feature test**

This topic only tests the active switchover scenario.

<span id="cKf2Osrd"></span>
### **Test Environment**


* The MySQL instance for the test is as follows:

   * MySQL 8.0 version, High\-availability architecture.

   * The instance specification is 8\-core 16 GB dedicated type (rds.mysql.d1.8c16g).

* Test tool: Sysbench.

* The test data is as follows:

   * 100 tables, each with 40,000 rows of data.

   * The number of concurrent threads is 128.


<span id="4lHaUGJ9"></span>
### **Test methods**

In different operation scenarios, test the connection persistence rate of the MySQL instance (the ratio of connections maintained before and after the operation).

**Execute test statement**:

```Shell
sysbench --db-driver=mysql --mysql-host=mysqlb469bxxxx.rds.ivolces.com --mysql-port=3306 --mysql-user=username --mysql-password='' --tables=100 --table-size=40000 --threads=128 --mysql-db=sbtest --report-interval=5  --time=600 oltp_read_write run
```


**Parameter description**

The parameters in the statement are described as follows:


* db\-driver: database engine, the value must be mysql.

* mysql\-host: the database proxy address, which must be replaced with your actual value.

* tables: the number of tables in the database.

* table\-size: the number of records in each table.

* threads: the number of concurrent threads.

* time: the test time is measured in seconds.


<span id="iOIJyJ9j"></span>
### **The test results are as follows.** 

In the following tested operation scenarios, the MySQL instance maintains a 100% connection persistence rate.


|**Active switch scenario** |**Connection persistence rate** |
|---|---|
|Active switching between primary and secondary nodes |100% |
|Modify parameters that require a restart |100% |
