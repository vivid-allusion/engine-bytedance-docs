---
title: "Automatic index creation management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Automatic_index_creation_management"
---

DBW provides the automatic index creation feature for NDB for MySQL. When slow logs diagnose slow SQL queries, DBW automatically generates index creation suggestions and automatically creates indexes for slow SQL queries using Online DDL supported by RDS for MySQL to improve SQL retrieval efficiency.

## Function introduction

DBW disables the automatic index creation feature for veDB for MySQL instances by default. If you want to use this feature, manually enable it. After the automatic index creation feature is enabled, when the slow log diagnosis provides index creation suggestions and the index creation protection and space protection conditions are met, DBW automatically creates a data change ticket for the veDB for MySQL instance using the dbw_bot system account. After the ticket is approved, the ticket can be executed to create an index for the instance.

DBW automatically creates indexes for slow SQL queries using Online DDL natively supported by the RDS for MySQL kernel. Therefore, it will not cause table locking. When index creation is triggered, DBW automatically creates an index only when the index creation protection and space protection conditions are met. The details are as follows:

|**Condition** |**Description** |
|---|---|
|Index creation protection |* Index exclusive filtering: Ensure that the effects of other indexes are not affected.<br><br>* Validity: Acceleration ratio of 2x or more, and the number of executions per day \> 10. |
|Space protection |Disk space: The safe level is less than 80%, and the remaining space is greater than two times the operating tablespace. |

## Prerequisite

* An NDB for MySQL instance have been created, and the Instance state is Running. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, refer to [Enabling instance security control (veDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control), and [Applying for operation permissions (veDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket).

## Precautions

* Currently, the automatic index creation feature is supported only for instances with kernel versions 3.0.x.x and 2.0.x.x.

* DBW disables the automatic index creation feature by default. If you want to use this feature, manually enable it.

* You can enable the automatic index creation feature only for instances that have security control enabled.

* We recommend that you select an off\-peak hour for creating indexes.

## Enable the automatic index creation rule

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the drop\-down list in the upper\-right corner of the page, select the **NDB for MySQL** database type.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Index created automatically** under **Configure AutoOps rules**.

6. In the **Index created automatically** control panel, configure the following parameters.

   |**Parameter** |**Description** |
   |---|---|
   |**Feature switch** |Click **Enable** to enable automatic index creation for the current instance. After enabling automatic index creation, DBW automatically creates an online DDL data change ticket for the current instance using the dbw_bot system account. After the ticket is approved, the ticket can be executed to automatically create an index for the current instance. |
   |**Index creation time** |Set the time to create an index based on the execution ticket as needed.<br><br><br>* **Execute now**: Execute the ticket to create an index immediately after approval.<br><br>* **Specified time period**: After approval, tickets can be executed at the specified time to create indexes.<br><br>* **Maintainable time period**: After approval, tickets can be executed during the O&M period to create indexes. For details about the maintenance window, see [Configuring maintenance window](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Configuring_maintenance_window).<br><br>   > **tip**<br>   <br><br>   > We recommend that you create indexes during off\-peak hours.<br>    |
   |**Specific time period** |You only need to set the time period for executing SQL statements to create indexes when **Index creation time** is set to **Specified time period**.<br><br>When setting a **Specified time period**, the end time must be later than the start time.<br><br>> **tip**<br><br><br>> We recommend that you create indexes during off\-peak hours.<br> |

7. Click **OK**.

   After enabling this function, viewing configuration content on the list page is not supported yet. You need to go to the configuration item to view details. The operation and maintenance event records page will display the event only after it is successfully triggered.

## View automatic index creation events

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the drop\-down list in the upper\-right corner of the page, select the **NDB for MySQL** database type.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, select the **Index created automatically** sub\-tab.

   Set the time range for query events as required. The target events to be viewed include **Event ID**, **Scheduled execution time**, **Trigger condition**, **Index statement**, **Ticket link**, **Ticket status**, **Creation time**, and **Last operation time**.

   Click **View Details** in the Actions column to go to the ticket details page, where you can view details about index creation.

## Modify the automatic index creation rule

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the drop\-down list in the upper\-right corner of the page, select the **NDB for MySQL** database type.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Index created automatically** under **Configure AutoOps rules**.

6. In the **Index created automatically** control panel, configure the following parameters.

   |**Parameter** |**Description** |
   |---|---|
   |**Feature switch** |Click **Enable** to enable automatic index creation for the current instance. After enabling automatic index creation, DBW automatically creates a data change ticket for the current instance using the dbw_bot system account. After the ticket is approved, the ticket can be executed to automatically create an index for the current instance.<br><br>> **tip**<br><br><br>> DBW uses the Online DDL natively supported by the RDS for MySQL kernel to automatically create indexes for slow SQL queries, which causes table locking.<br> |
   |**Index creation time** |Set the time to create an index based on the execution ticket as needed.<br><br><br>* **Execute now**: Execute the ticket to create an index immediately after approval.<br><br>* **Specified time period**: After approval, tickets can be executed at the specified time to create indexes.<br><br>* **Maintainable time period**: After approval, tickets can be executed during the O&M period to create indexes. For details about the maintenance window, see [Configuring maintenance window](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Configuring_maintenance_window).<br><br>   > **tip**<br>   <br><br>   > We recommend that you create indexes during off\-peak hours.<br>    |
   |**Specific time period** |You only need to set the time period for executing SQL statements to create indexes when **Index creation time** is set to **Specified time period**.<br><br>When setting a **Specified time period**, the end time must be later than the start time.<br><br>> **tip**<br><br><br>> We recommend that you create indexes during off\-peak hours.<br> |

7. Click **OK**.

## Disable the automatic index creation rule

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the drop\-down list in the upper\-right corner of the page, select the **NDB for MySQL** database type.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Index created automatically** under **Configure AutoOps rules**.

6. On the **Index created automatically** control panel, click **Disable** switch.

7. Click **OK**.
