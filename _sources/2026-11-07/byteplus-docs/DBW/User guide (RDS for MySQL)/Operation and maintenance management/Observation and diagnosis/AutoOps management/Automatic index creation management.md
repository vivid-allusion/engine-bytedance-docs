---
title: "Automatic index creation management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Automatic_index_creation_management_MySQL"
---

DBW provides the automatic index creation feature for RDS for MySQL. When slow logs diagnose slow SQL queries, DBW automatically generates index creation suggestions and automatically creates indexes for slow SQL queries using Online DDL supported by RDS for MySQL to improve SQL retrieval efficiency.

<span id="U91rzQ1s"></span>
## Function introduction

DBW disables the automatic index creation feature for RDS for MySQL instances by default. If you want to use this feature, manually enable it. After the automatic index creation feature is enabled, when the slow log diagnosis provides index creation suggestions and the index creation protection and space protection conditions are met, DBW automatically creates a data change ticket for the RDS for MySQL instance using the dbw_bot system account. After the ticket is approved, the ticket can be executed to create an index for the instance.

DBW automatically creates indexes for slow SQL queries using Online DDL natively supported by the RDS for MySQL kernel. Therefore, it will not cause table locking. When index creation is triggered, DBW automatically creates an index only when the index creation protection and space protection conditions are met. The details are as follows:


|**Condition** |**Description** |
|---|---|
|Index creation protection |* Index exclusive filtering: Ensure that the effects of other indexes are not affected.<br><br>* Validity: Acceleration ratio of 2x or more, and the number of executions per day \> 10. |
|Space protection |Disk space: The safe level is less than 80%, and the remaining space is greater than two times the operating tablespace. |


<span id="2FpS3ruV"></span>
## Prerequisites


* An instance for RDS for MySQL has been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* The target instance has security control enabled, and the current account has the operation and maintenance read\-only or read/write permissions of the target instance. For more information, refer to [Enabling instance security control (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql), and [Applying for operation permissions (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket).


<span id="AAc2hF1D"></span>
## Precautions


* DBW disables the automatic index creation feature by default. If you want to use this feature, manually enable it.

* You can enable the automatic index creation feature only for instances that have security control enabled.

* We recommend that you select an off\-peak hour for creating indexes.


<span id="IICsDuiQ"></span>
## Enable the automatic index creation rule


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Index created automatically** under **Configure AutoOps rules**.

6. In the **Index created automatically** control panel, configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Feature switch** |Click **Enable** to enable automatic index creation for the current instance. After enabling automatic index creation, DBW automatically creates a Online DDL data change ticket for the current instance using the dbw_bot system account. After the ticket is approved, the ticket can be executed to automatically create an index for the current instance. |
   |**Index creation time** |Set the time to create an index based on the execution ticket as needed.<br><br><br>* **Execute now**: Execute the ticket to create an index immediately after approval.<br><br>* **Specified time period**: After approval, tickets can be executed at the specified time to create indexes.<br><br>* **Maintainable time period**: After approval, tickets can be executed during the O&M period to create indexes. For details about the maintenance window, refer to [Configuring maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">We recommend that you create indexes during off\-peak hours.</div><br> |
   |**Specific time period** |You only need to set the time period for executing SQL statements to create indexes when **Index creation time** is set to **Specified time period**.<br><br>When setting a **Specified time period**, the end time must be later than the start time.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">We recommend that you create indexes during off\-peak hours.</div><br> |
   

7. Click **OK**.


<span id="yhujeNjr"></span>
## View automatic index creation events


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, select the **Index created automatically** sub\-tab.

   Set the time range for query events as required. The target events to be viewed include **Event** **ID**, **Scheduled execution time**, **Trigger condition**, **Index statement**, **Ticket link**, **Ticket status**, **Creation time**, and **Last operation time**.

   Click **View Details** in the Actions column to go to the ticket details page, where you can view details about index creation.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bff450e8bff7fd97155cfd824f7efd56.jpg) </span>


<span id="EpWilCrX"></span>
## Modify the automatic index creation rule


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Index created automatically** under **Configure AutoOps rules**.

6. In the **Index created automatically** control panel, configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Feature switch** |Click **Enable** to enable automatic index creation for the current instance. After enabling automatic index creation, DBW automatically creates a data change ticket for the current instance using the dbw_bot system account. After the ticket is approved, the ticket can be executed to automatically create an index for the current instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">DBW uses the Online DDL natively supported by the RDS for MySQL kernel to automatically create indexes for slow SQL queries, which causes table locking.</div><br> |
   |**Index creation time** |Set the time to create an index based on the execution ticket as needed.<br><br><br>* **Execute now**: Execute the ticket to create an index immediately after approval.<br><br>* **Specified time period**: After approval, tickets can be executed at the specified time to create indexes.<br><br>* **Maintainable time period**: After approval, tickets can be executed during the O&M period to create indexes. For details about the maintenance window, refer to [Configuring maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period).<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default">We recommend that you create indexes during off\-peak hours.   </div><br>    |
   |**Specific time period** |You only need to set the time period for executing SQL statements to create indexes when **Index creation time** is set to **Specified time period**.<br><br>When setting a **Specified time period**, the end time must be later than the start time.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">We recommend that you create indexes during off\-peak hours.</div><br> |
   

7. Click **OK**.


<span id="oNAnhU8t"></span>
## Disable the automatic index creation rule


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **AutoOps**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **AutoOps** tab, click **Index created automatically** under **Configure AutoOps rules**.

6. On the **Index created automatically** control panel, click **Disable** switch.

7. Click **OK**.
