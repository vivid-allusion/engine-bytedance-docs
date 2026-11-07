---
title: "Subscription solution overview"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/overview_of_subscription_solutions"
---

Through data subscription, you can obtain incremental data from the source database (such as public network MySQL, RDS MySQL, veDB MySQL, public network PostgreSQL, PostgreSQL) in real time and freely consume incremental data as needed. This is suitable for scenarios such as business asynchronous decoupling. This topic introduces the source database types, versions, access methods, and supported data types for subscription supported by BytePlus Database Transmission Service (DTS).

## Subscription type instructions

|**Subscription type** |**Description** |
|---|---|
|**Full subscription** |Fully reads the source table contents and converts them into a ProtoBuf structure. Currently, it supports **BytePlus Proto**, **Canal Proto**, **Canal JSON**, **Avro format**, and **Debezium JSON format**, and pushes them to the corresponding message queue. |
|**Incremental subscription** |Resolves the incremental logs of the source database and converts them into a ProtoBuf structure. Currently, it supports **BytePlus Proto**, **Canal Proto**, **Canal JSON**, **Avro format**, and **Debezium JSON format**, and pushes them to the corresponding message queue. |
|**Database and table schema subscription** |Converts the source database and table schema into a ProtoBuf structure. Currently, it supports **BytePlus Proto**, **Canal Proto**, **Canal JSON**, and **Avro format**, and pushes them to the message queue. |

## Subscription state instructions

|**Task status** |**Description** |
|---|---|
|**To be started** |The task enters this state after you complete object configuration or pre\-check and choose to save during subscription task creation. |
|**In progress** |Subscription tasks in progress. |
|**Failed** |State entered when the task is interrupted or abnormal due to issues or failures during subscription. |
|**Completed** |Task status after the following operations:<br><br><br>* State after the subscription task is complete.<br><br>* Terminate tasks that are in progress. The task status will first change to “terminating”, then to “completed”. |

## Subscription solution overview

including:

* **Data update**: Refers to database manipulation language, namely DML, which performs insert, delete, and modify operations on table data, such as `INSERT`, `DELETE`, or `UPDATE`.

* **Schema update**: Refers to data definition language, namely DDL, which creates, deletes, or modifies tables, such as `CREATE`, `DROP`, or `ALTER`.
