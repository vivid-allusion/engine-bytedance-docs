---
title: "Feature comparison by version"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/version-function-comparison"
---

To ensure security when you use RDS for SQL Server, RDS for SQL Server has limitations on compatible versions. This topic also provides recommendations to enhance your user experience.


|**Feature** |**Standard edition**<br><br><br>* SQL Server 2019 Standard Edition<br><br>* SQL Server 2022 Standard Edition |**Enterprise Edition**<br><br><br>* SQL Server 2019 Enterprise Edition<br><br>* SQL Server 2022 Enterprise Edition |**Web edition**<br><br><br>* SQL Server 2019 Web Edition<br><br>* SQL Server 2022 Web Edition |
|---|---|---|---|
|Specification limit |24 Cores 192 GiB |64 Cores 256 GiB |16 Cores 64 GiB |
|High Availability |Always On Basic |Always On |None |
|[Maximum number of databases](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/version-function-comparison?lang=en#r4aJSqgk)<br><br>(Limited by instance type and specification) |* High availability: 50 to 300<br><br>* Single node edition: 100 to 400 |* High availability: 50 to 300<br><br>* Single node edition: 100 to 400 |Single node edition: 100 to 400 |
|Read\-only node |Unsupports |Supports |Unsupports |
|Maximum number of database accounts |Unlimited |Unlimited |Unlimited |
|Create a user, LOGIN, or database |Supports |Supports |Supports |
|Database\-level DDL triggers |Supports |Supports |Supports |
|Database authorization permissions |Supports |Supports |Supports |
|Permission to terminate threads |Supports |Supports |Supports |
|Linked Server |Supports |Supports |Supports |
|Change tracking |Supports |Supports |Supports |
|Data compression |Supports |Supports |Unsupports |
|SQL Profiler |Supports |Supports |Unsupports |
|Change Data Capture (CDC) |Supports |Supports |Unsupports |
|Online DDL |Unsupports |Supports |Unsupports |
|Distributed transaction |Supports<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This feature is available on an allowlist basis. To request access, <a href="https://console.byteplus.com/workorder/create">Submit a ticket</a> to contact the SQL Server technical team.</div><br> |Supports<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This feature is available on an allowlist basis. To request access, <a href="https://console.byteplus.com/workorder/create">Submit a ticket</a> to contact the SQL Server technical team.</div><br> |Supports<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This feature is available on an allowlist basis. To request access, <a href="https://console.byteplus.com/workorder/create">Submit a ticket</a> to contact the SQL Server technical team.</div><br> |
|Optimization advisor |Unsupported |Unsupported |Unsupports |
|Common Language Runtime (CLR) integration |Partially supported (Secure mode) |Partially supported (Secure mode) |Partially supported (Secure mode) |
|Replication feature |Partial support (Subscriber side) |Partial support (Subscriber side) |Unsupports |
|Windows domain account login |Unsupports |Unsupports |Unsupports |
|Email feature ||||
|SQL Server Integration Services (SSIS) ||||
|SQL Server Analysis Services (SSAS) ||||
|SQL Server Reporting Services (SSRS) ||||
|R language service ||||
|Asynchronous message communication ||||
|Policy management ||||


<span id="r4aJSqgk"></span>
## Maximum number of databases

The maximum number of databases for an SQL Server instance is limited by its instance type and the number of CPU cores in its instance specification. The following section lists the maximum number of databases for different instance types and numbers of CPU cores:


|**CPU Cores** |Instance type |||
|---|---|---|---|
||High availability |Cluster edition |Single node edition |
|2 Cores |50 |50 |100 |
|4 Cores |100 |100 |200 |
|8 Cores |100 |100 |200 |
|16 Cores |200 |200 |400 |
|32 Cores |250 |250 |400 |
|64 Cores |300 |300 |400 |


The detailed formula for calculating the maximum number of databases for different instance types and instance specifications is as follows:


* **High availability edition** or **Cluster edition**


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2682c6d6e7c6e1a16ef1a344a06e4726.png) </span>


That is, take the square root of the number of CPU cores, round down to the nearest integer, and multiply by 50. If the resulting value is X, the maximum number of databases is the **minimum value** between X and 300. For example, a High availability instance (2 cores 16 GiB) compatible with SQL Server 2022 Enterprise Edition supports a maximum of 50 databases.

* **Single node edition**


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_064943ef5c68e1694cba8bab84c91366.png) </span>


Calculate by taking the square root of the number of CPU cores, rounding down, and multiplying by 100. Let this value be Y. The maximum number of databases is the **minimum** of Y and 400. For example, a Single node edition instance (2 cores 4 GiB) compatible with SQL Server 2022 Web Edition supports a maximum of 100 databases.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<span id="7QB6UhwO"></span>
## <div data-tips="true" data-tips-type="default">In the formulas above, min refers to the minimum value within a data range. For example, min{100, 300} is 100.</div>


<span id="CgrFqWKG"></span>
## Recommendations


|**Type** |**Limitations** |
|---|---|
|**Instance** |* Domain\-joined instance: for a domain\-joined instance, the domain controller is on the user side, and the user has elevated permissions. The domain controller's group policy configuration affects machines that join the domain. Modifying domain control rules on the user's side increases security risks related to the permissions of the database instance. Therefore, creating domain\-joined instances is not recommended.<br><br>* Restart instance: performance may degrade if an instance runs for a long time. Restart the instance every three months during off\-peak hours. |
|**Database** |* Number of databases: Do not exceed 100 databases per single instance. The number of databases a single instance can support depends on its specification. Too many databases will degrade instance performance and consume resources like Worker Threads.<br><br>* System database operations: Do not create tables in system databases. Storing data in system databases is insecure, so create a custom database to store data.<br><br>* `Auto Close` property: Although a database's `Auto Close` property can be enabled, this may cause issues such as being unable to establish replication relationships and preventing normal database operation. It is strongly recommended to not enable the `Auto Close` property.<br><br>* Database mode: Do not set the database mode to `Single User`. Since `Single User` mode only allows one `Session` to access the database, it can prevent other `Sessions` from accessing it, leading to operational problems for the cloud database. Therefore, change databases set to `Single User` mode to `Multi User` mode as soon as possible.<br><br>* Database shrink: Over time, database usage can prevent physical space from being released promptly. Perform a database shrink operation to release this physical space. Monitor the size of log and physical files. If you notice file expansion, shrink the database promptly during off\-peak business hours.<br><br>* Database name:<br><br>   * The length must be between 2 and 60 characters.<br><br>   * Start with a letter and end with a letter or digit.<br><br>   * The database name must contain digits, uppercase and lowercase letters, hyphens (\-), and underscores (_).<br><br>   * You can not use reserved words, such as `master`, `msdb`, `model`, `tempdb`,`resource`, `rdsadmin`, and `distribution`.<br><br>* Database recovery model:<br><br>   Do not set the database's recovery model to `simple`. The `full` model is recommended. The reasons are as follows:<br><br>   * The `simple` model does not perform incremental backups, so the database can not be restored to a specific point in time.<br><br>   * For primary/secondary or cluster instances, setting the database recovery model to `simple ` prevents a high\-availability relationship from being established. This blocks operations like primary/secondary switchovers and specification changes. Therefore, use the `simple ` model with caution. |
|**Permission** |* veyun_user account: A super account that is created for each instance upon creation and cannot be deleted.<br><br>* System Admin account: An account with the System Admin role has super administrator permissions. Improper use will compromise the security and stability of the database. Therefore, RDS for SQL Server grants super administrator permissions through an allowlist. To enable super administrator permissions, [submit a ticket](https://console.byteplus.com/workorder/create) and contact the SQL Server technical team for allowlist access. |
|**Others** |* Slow query log: A slow query log can help with slow SQL analysis, but keeping it enabled for a long time will degrade performance. Disable the slow query log when you do not need to track and analyze SQL issues.<br><br>* Index: A database may develop significant index fragmentation over time, which degrades database access performance. Rebuild indexes periodically. We recommend creating an SQL Agent job to rebuild indexes monthly.<br><br>* Statistics: Regularly updating database statistics improves database performance. We recommend creating an SQL Agent job to update statistics weekly.<br><br>* Max degree of parallelism: This parameter affects CPU utilization. The default value of 0 allows a session to use all CPUs. However, a problematic SQL query could prevent the CPU from being allocated to other sessions. We recommend setting this value based on your instance specifications, such as the number of Cores divided by two.<br><br>* Parameters: To modify RDS for SQL Server parameters, use the console. Modifying parameters by executing SQL commands is unsupported.<br><br>* Backup and restore: Perform backup and restore operations through the management console, or by calling an API or SDK. You cannot perform these operations directly through SSMS or by executing SQL. |
