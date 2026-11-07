---
title: "Constraints and limits"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Constraints_and_limits"
---

After purchasing the NDB for MySQL product series, you do not need to do basic database operation and maintenance, but in order to improve the stability and security of the instance, there are some fixed restrictions on its use. This topic describes the usage constraints of NDB for MySQL instances.

<span id="igb7l89B"></span>
## **DBEngine limits**

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">NDB for MySQL is highly compatible with MySQL. Here we only describe the limitations that differ from MySQL. All other aspects remain consistent.</div>



* NDB for MySQL only supports the InnoDB engine. Other engines are converted to InnoDB by default.

* The maximum data capacity of a single table/partition is 64 TiB.

* MySQL native compression capabilities are not supported. If you set compression when executing SQL statements, NDB for MySQL will automatically ignore the corresponding settings.


<span id="YMMBNJkh"></span>
## Instance usage limits


|Constraint |Limitation |
|---|---|
|Instance parameter |Most instance parameters can be modified using the console or API, but for security and stability reasons, some parameters do not support modification. For more information, see [Modifying parameters](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_parameters). |
|Database root privileges |Does not provide root privileges. |
|Database backup |Backups are limited to the console or API. The maximum number of manual backups is 10, and the optional range of automatic backup retention days is 7 to 365 days. |
|Database recovery |Restore only through the console or API. Supports cross\-availability zone recovery, where new and original instances can be selected in different availability zones. |
|Storage engine |Currently only the InnoDB engine is supported. |
|Database replication |Currently only 2 to 16 nodes are supported, of which up to 15 are read\-only nodes, and the data on each node is exactly the same as the primary node. |
|Instance change |Changes can only be made through the console or API. You can delete the instance, change the configuration, switch the primary node, account management, database management, allowlist management and other operations. |
|Database access |If the instance does not have public network access, the instance must be in the same VPC (Virtual Private Cloud) as the cloud host elastic computing service to access each other. |
|View backup |The backup file for the instance is stored on the TOS service and is not visible to the server. Only the backup file list can be viewed on the console. |
|Deploy |None of the servers deployed by the instance are visible, allowing applications to access the database only through connection or IP addresses. |
