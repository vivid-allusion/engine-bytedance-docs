---
title: "Creating and initiating a migration task"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_and_initiating_a_migration_task"
---

Database transmission service (DTS) provides a variety of database migration services. This topic describes how to use DTS to create and initiate a data migration task, using the migration of a self\-hosted MySQL in a VPC to BytePlus RDS for MySQL as an example.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A BytePlus account has been registered with real name authentication completed. For account creation methods and real\-name authentication,     please refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account) and [Real-name authentication](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).

* Meet the supported database types and constraints for migration. For more Details, refer to [Usage restrictions](https://docs.byteplus.com/en/docs/DTS/limits_mysql_as_source_database).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [DTS console](https://console.byteplus.com/dts).

2. In the upper\-left corner of the top menu bar, select the target region.

3. Click Create task in the Migration task list.

4. Configure the following parameters on the Create a migration task page.

   
   |Parameter ||Description |
   |---|---|---|
   |Task name ||Enter a task name. This is required. The name must meet the following conditions:<br><br><br>* Must start with a letter.<br><br>* It must contain no more than 32 characters.<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-). |
   |Link specification ||DTS supports four different links to meet business requirements of different levels. For more details about link specifications, refer to [Product specification](https://docs.byteplus.com/en/docs/DTS/product_specifications). |
   |Source database information |Instance type |Currently, only "MySQL" is supported. |
   ||Access method |The currently supported access methods are "BytePlus RDS", "self\-managed MySQL in the VPC", and "PublicMySQL".<br><br>**Description**:<br><br>This topic uses "self\-managed MySQL in the VPC" as an example. |
   ||MySQL instance |Select the source MySQL instance from the drop\-down list.<br><br>**Note**:<br><br>This configuration is supported only when "BytePlus RDS" is used as the access method. |
   ||Host address |Enter the host address of the source self\-managed instance.<br><br>**Note**:<br><br>This configuration is supported only when "self\-managed MySQL in the VPC" or "PublicMySQL" is used as the access method. |
   ||Port |Enter the port number of the source self\-hosted instance.<br><br>**Note**:<br><br>This configuration is supported only when "self\-managed MySQL in the VPC" or "PublicMySQL" is used as the access method. |
   ||VPC |Select the VPC network of the source instance from the drop\-down list.<br><br>**Note**:<br><br>This configuration is supported only when 'self\-managed MySQL in the VPC' is used as the access method. |
   ||Database account |Enter the database account for the source instance. |
   ||Database password |Enter the password for the source instance database account.<br><br>**Note**:<br><br><br>* After entering the password, you can click Test connection, and then perform subsequent configuration after the test is passed.<br><br>* If access restrictions are set for your instance, you should grant access permissions for the DTS CIDR block so that you can continue the migration task.You can click \\View DTS IP segment\\\* to view and copy the CIDR block. You can click \\View DTS IP segment\\\* to view and copy the CIDR block. |
   |Target database information |Instance type |Currently, only "MySQL" is supported. |
   ||Access method |The currently supported access methods are "BytePlus RDS", "self\-managed MySQL in the VPC", and "PublicMySQL".<br><br>**Note**:<br><br>This topic uses "RDS for MySQL" as an example. |
   ||MySQL instance |Select the target MySQL instance from the drop\-down list.<br><br>**Note**:<br><br>This configuration is supported only when "BytePlus RDS" is used as the access method. |
   ||Host address |Enter the localhost of the target self\-managed instance.<br><br>**Note**:<br><br>This configuration is supported only when "self\-managed MySQL in the VPC" or "PublicMySQL" is used as the access method. |
   ||Port |Enter the port number of the target self\-hosted instance.<br><br>**Note**:<br><br>This configuration is supported only when "self\-managed MySQL in the VPC" or "PublicMySQL" is used as the access method. |
   ||VPC |Select the VPC for the target instance from the drop\-down list.<br><br>**Note**:<br><br>This configuration is supported only when 'self\-managed MySQL in the VPC' is used as the access method. |
   ||Database account |Enter the database account of the target instance. |
   ||Database password |Enter the password corresponding to the database account of the target instance.<br><br>**Note**:<br><br><br>* After entering the password, you can click Test connection, and then perform subsequent configuration after the test is passed.<br><br>* If access restrictions are set for your instance, you should grant access permissions for the DTS CIDR block so that you can continue the migration task.You can click \\View DTS IP segment\\\* to view and copy the CIDR block. You can click \\View DTS IP segment\\\* to view and copy the CIDR block. |
   

5. Click Next step: configure migration object.

6. Configure the following parameters on the Configure migration objects page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you do not currently need to initiate the migration task, you can click Save in the lower\-right corner of the page after the migration objects are configured.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After saving, it jumps back to the Migration task list page. For configuration instructions, refer to <a href="https://docs.byteplus.com/en/docs/DTS/configuring_a_migration_task">Configure migration task</a>.   </div>
   

   
   |Parameter |Description |
   |---|---|
   |Migration type |Select the migration type based on your business needs:<br><br><br>* If you only need full migration, select Structural migration and Full migration at the same time.<br><br>* If you must perform non\-stop migration, you select Structural migration, Full migration, and Incremental migration at the same time.<br><br><br>&nbsp;<br><br>**Note**:<br><br>If Incremental migration is not selected, do not write new data to the source instance during data migration to ensure data consistency. |
   |Migration object |Select the objects to be migrated in the Migration objects box, and you can confirm the migration objects in the Selected objects box on the right.<br><br>**Note**:<br><br><br>* If a migration object is not an entire database, OnlineDDL is not supported, and automatic migration of new objects and relevant modifications are not supported for incremental migration.<br><br>* Migration objects can be selected at the database or table level. If a migration object selected is a table, other objects (such as views, triggers, functions, and stored procedures) will not be moved to the destination database. |
   

7. Click Pre\-check and start.

   You can perform the following operations based on the precheck result:

   * Click Details in the Action column of the precheck result to view the detailed alert information and modify the database and table based on the alert information.

   * Click Ignore in the Action column to ignore the alert and continue to initiate the migration task.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you choose to Ignore the alert and initiate the migration task, it can cause data inconsistencies and business risks.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For details about pre\-check items, refer to <a href="https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_mysql">Pre\-check items</a>.   </div>
   

8. Read and check the service agreement in the lower\-left corner, and click Start task in the lower\-right corner.

   After the task is created, you can return to the console and view the progress of the migration task in the Migration task list.


<span id="LXBpu7ng"></span>
## FAQ

<span id="eKmEZaEv"></span>
### Why do some GROUP BY queries fail after migrating a MySQL 5.6 instance to RDS for MySQL?

RDS for MySQL is compatible with MySQL 5.7 and 8.0. In MySQL 5.7 and later versions, the ONLY_FULL_GROUP_BY mode is enabled by default, which applies stricter validation to GROUP BY syntax, causing some non\-standard GROUP BY queries to fail.
