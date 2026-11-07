---
title: "Manually cleaning self-built resources for PostgreSQL data transmission tasks"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Manually_cleaning_self-built_resources_for_PostgreSQL_data_transmission_tasks"
---

After using BytePlus DTS for PostgreSQL database data migration or data synchronization, if a DTS task is terminated abnormally, the methods described in this topic can be used to manually clean up the resources created by the migration or synchronization tasks in the PostgreSQL database.

<span id="iU6CRrSn"></span>
## Background

When BytePlus DTS performs PostgreSQL database data migration or data synchronization, it automatically creates the following 5 types of resources in the PostgreSQL Source database.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The <code>{task_id}</code> placeholder in the naming format <code>column</code> in the following table is the DTS <code>task</code> ID.</div>



|**DTS self\-built resources** |**Usage in data transmission** |**Naming format** |
|---|---|---|
|Event Trigger |It is used to capture DDL (Data Definition Language) operations, such as `CREATE TABLE` and `ALTER TABLE`. DTS creates two event triggers, which are triggered before and after a DDL event occurs, respectively. |`dts_ddl_command_trigger_{task_id}` and `dts_publication_ddl_command_trigger_{task_id}` |
|Function |It is called by the Event Trigger to record details about DDL events into a table created by DTS. |`public.dts_ddl_command_func_{task_id}()` and `public.dts_publication_ddl_command_func_{task_id}()` |
|Table |It is used to store detailed information about DDL events. |`public.dts_ddl_command_table_{task_id}` |
|Publication |It is used to define which table changes (`INSERT`, `UPDATE`, `DELETE`, `TRUNCATE`) need to be sent to the subscription through logical replication. |`dts_logical_replica_{task_id}` |
|Replication Slot |Logical replication slot, which ensures that the database does not delete the relevant WAL (Write\-Ahead Logging) logs before the subscriber consumes the data.<br><br>Failure to clean up core resources of replication slots over an extended period may lead to the database's disk space being fully occupied. |`dts_logical_replica_{task_id}` |


Under normal circumstances, after the data transmission task is completed, DTS will automatically delete the above 5 types of created resources in the Source database. However, in the following scenarios, DTS can not automatically delete the above 5 types of resources. In this case, you need to manually clean the above resources.


|**Scenario** |**Description** |**Actions** |
|---|---|---|
|DTS can not connect to the source database |Before BytePlus DTS normally ends the task, DTS is abnormally unable to connect to the PostgreSQL source database for other reasons. For example, before terminating the DTS Task, removing DTS from the source database allowlist will cause DTS to be unable to connect to the PostgreSQL source database, and the above five types of resources can not be deleted. |Manually delete the Event Trigger, Function, Table, Publication, and Replication Slot in the source database. |
|Migrate self\-built resources in the DTS source database to the target database |Before BytePlus DTS normally terminates the task, if you use a third\-party migration tool to migrate the data in the PostgreSQL source database (including the above 5 types of resources automatically created by DTS) to the target database. At this time, you also need to manually clean up the above 5 types of resources at the destination. |Manually delete the Event Trigger, Function, Table, Publication, and Replication Slot in the target database. |


<span id="CtuISKlO"></span>
## Prerequisites


* A PostgreSQL database data migration or data synchronization task has been started in BytePlus DTS, and DTS can not automatically delete the self\-built resources (Event Triggers, Functions, Tables, Publications, and Replication Slots) in the PostgreSQL source or target database.

* You have the Superuse permission of the PostgreSQL database.


<span id="kzt9Ehnr"></span>
## Precautions


* After a DTS transfer task ends abnormally, if the self\-built resources of DTS are not cleaned up, the data within these resources will continue to accumulate, occupying database space and affecting database performance.

* When cleaning up DTS self\-built resources, be sure to follow the order in the cleanup steps to Delete Event Trigger \> Function \> Table \> Publication \> Replication Slot in sequence.

* If the deletion sequence of resources is incorrect and results in the database being unable to perform DDL operations normally, execute the DROP EVENT TRIGGER command to restore the availability of DDL operations in the database.


<span id="98MuhhOZ"></span>
## Procedure

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You need to delete in the following order: Event Trigger \> Function \> Table \> Publication \> Replication Slot.</div>



1. Log in to the PostgreSQL database (Source end or destination).

2. Switch to the database to be migrated.

3. Delete Event Trigger.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace the<code> {task_id}</code> placeholder in the following command with the DTS task ID.   </div>
   

   1. Execute the following command to check whether the target event trigger exists.

      ```SQL
      SELECT evtname FROM pg_event_trigger WHERE evtname IN ('dts_ddl_command_trigger_{task_id}', 'dts_publication_ddl_command_trigger_{task_id}');
      ```
      

   2. If it exists, execute the following command to delete the target event trigger.

      ```SQL
      DROP EVENT TRIGGER IF EXISTS dts_ddl_command_trigger_{task_id};
      DROP EVENT TRIGGER IF EXISTS dts_publication_ddl_command_trigger_{task_id};
      ```
      

4. Delete Function.

   1. Execute the following command to check whether the target function exists.

      ```SQL
      SELECT proname FROM pg_proc WHERE proname IN ('dts_ddl_command_func_{task_id}', 'dts_publication_ddl_command_func_{task_id}');
      ```
      

   2. If it exists, execute the following command to delete the target function.

      ```SQL
      DROP FUNCTION IF EXISTS public.dts_ddl_command_func_{task_id}();
      DROP FUNCTION IF EXISTS public.dts_publication_ddl_command_func_{task_id}();
      ```
      

5. Delete Table.

   1. Execute the following command to check whether the target table exists.

      ```SQL
      SELECT to_regclass('public.dts_ddl_command_table_{task_id}');
      ```
      

   2. If it exists, execute the following command to delete the target table.

      ```SQL
      DROP TABLE IF EXISTS public.dts_ddl_command_table_{task_id};
      ```
      

6. Delete Publication

   1. Execute the following command to check whether the target publication exists.

      ```SQL
      SELECT pubname FROM pg_publication WHERE pubname = 'dts_logical_replica_{task_id}';
      ```
      

   2. If it exists, execute the following command to delete the target publication.

      ```SQL
      DROP PUBLICATION IF EXISTS dts_logical_replica_{task_id};
      ```
      

7. Delete Replication Slot

   1. Execute the following command to check whether the target replication slot exists.

      ```SQL
      SELECT slot_name FROM pg_replication_slots WHERE slot_name = 'dts_logical_replica_{task_id}';
      ```
      

   2. If it exists, make sure that no client is connected to the target replication slot, and then execute the following command to delete the target replication slot.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If a client is connecting to the target replication slot, interrupt the replication slot connection first. Otherwise, the deletion may fail.      </div>
      

      ```SQL
      SELECT pg_drop_replication_slot('dts_logical_replica_{task_id}');
      ```
      


<span id="ZuxotOLD"></span>
## FAQs

<span id="MqRf8TJg"></span>
#### Q1: After a DTS task ends, if DTS does not automatically clean up the event triggers, functions, tables, publications, and logical replication slot resources created for the transmission task, must they be cleaned up manually?


A: Yes, you must manually clean up the above five types of self\-built resources by DTS. If you do not manually clean up the above resources, these resources will continue to run in the database.

   * Publication and logical replication slots will always record the newly added data logs in the database. As time goes by, the amount of data in the publication and logical replication slots will become larger and larger, which will take up a lot of storage space and affect database performance.

   * Trigger, function, and table: The trigger will always capture DDL execution events and record the DDL execution data in the table through the function.


<span id="GE7ZUsJD"></span>
#### Q2: When manually cleaning up DTS self\-built resources, what impact will it have if the resources are not deleted according to the cleaning sequence?


As mentioned in the [Background](https://docs.byteplus.com/en/docs/DTS/Manually_cleaning_self-built_resources_for_PostgreSQL_data_transmission_tasks#iU6CRrSn), there is a dependency among DTS self\-built resources. If the order of deleting resources is incorrect, errors may occur and affect the database service operation. Be sure to delete the DTS self\-built resources according to the cleaning steps.
