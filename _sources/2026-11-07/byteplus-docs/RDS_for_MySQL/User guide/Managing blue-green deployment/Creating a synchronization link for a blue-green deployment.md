---
title: "Creating a synchronization link for a blue-green deployment"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Creating_a_synchronization_link_for_a_blue-green_deployment"
---

This topic describes how to create a synchronization link between the blue and green instances for a blue\-green deployment.

<span id="MKy616VU"></span>
## Fee

Data Transmission Service (DTS) provides the data synchronization feature for blue\-green deployments. For more information about synchronization link fees, refer to [Billing of data synchronization tasks](https://docs.byteplus.com/en/docs/DTS/billing_items).

<span id="4AtlJ6Cp"></span>
## Prerequisites

A blue\-green deployment is created. For more information, refer to [Create a blue-green deployment](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Creating_a_blue-green_deployment).

<span id="nXqjj665"></span>
## Precautions


* You can create a synchronization link for both the blue and green instances.

* Only one unidirectional synchronization link can be created for blue and green instances.

* Only pay\-as\-you\-go synchronization links can be created.

* Only the accounts of the blue instance can be synchronized when the synchronization link is created.

* The data synchronization task starts automatically after the synchronization link is created and cannot be terminated or paused.

* During DTS synchronization, do not write data from sources other than DTS to the target database. Otherwise, this will cause data inconsistency between the source and target databases. For example, if data from sources other than DTS is written to the target database, performing online DDL changes with DBW may cause data loss in the target database.

* During synchronization link creation, database and table structure initialization, and full initialization, do not perform DDL operations that change the database or table structure. Otherwise, the synchronization task will fail.

* When performing DDL operations with an online DDL tool, ensure that the synchronization object is the entire database. Otherwise, the DDL operation will fail because temporary tables cannot be synchronized. During synchronization, do not use online DDL tools to perform lightweight DDL operations, such as adding fields to small tables. Otherwise, the DDL synchronization may fail because the DDL temporary table is too short\-lived.

* Tables to be synchronized must have a primary key or a unique non\-null constraint, and the fields must have unique values. Otherwise, data inconsistency may occur.

* Binlogs must be retained for at least 24 hours. We recommend retaining them for more than seven days. Otherwise, the task may fail and data loss may occur because DTS cannot obtain the logs.

* Tables with foreign key dependencies must be synchronized simultaneously. Otherwise, data synchronization will fail.

* Synchronization tasks do not support trigger and event objects.

* After you create the synchronization link, modify the following parameters of the primary instance with caution to avoid affecting the synchronization link:

   * lower_case_table_names

   * collation_server

   * transaction_isolation

   * innodb_strict_mode

   * sql_mode

   * innodb_large_prefix

   * default_time_zone

* After the synchronization link is created, it is recommended to create a data validation for the corresponding synchronization task to ensure data consistency. For more information about data validation, refer to [Introduction to data validation](https://docs.byteplus.com/en/docs/DTS/introduction_to_data_validation) and [Configure data validation](https://docs.byteplus.com/en/docs/DTS/configuring_data_validation).


<span id="HUzbBERg"></span>
## Procedure


1. (Optional) If you have just created the blue\-green deployment for the target instance and are still on the **Create green instance** page, click the Create synchronization link button on the page to go to the **Create blue\-green synchronization task** page and proceed directly to step 7.

2. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

3. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

4. In the left\-side navigation pane, click **Instances** to view the list of instances for RDS for MySQL.

5. On the **Instances** page, click the name of the target blue or green instance to go to the **Summary** tab.

6. Click the **Connectivity** tab, and in the **Instance topology** area, click **Create synchronization link** on the blue\-green deployment relationship line to go to the **Create blue\-green synchronization task** page.

7. On the **Create disaster recovery synchronization task** page, complete the following settings.

   1. On the **Configure source and destination databases** page, complete the following configurations and click **Next step: Configure synchronization objects** to go to the **Configure synchronization objects** page.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Task name**<br><br> |(Optional) Customize the synchronization task name. Naming rules are as follows:<br><br><br>* Must start with a letter.<br><br>* The length must be no more than 64 characters.<br><br>* It can only contain letters, numbers, underscores (_), and hyphens (\-). |
      |**Link specification** |Select the link Specification for the synchronization task. **Compact** and **Standard** are the supported options.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The link Specification cannot be modified after the task is successfully created. Refer to <a href="https://docs.byteplus.com/en/docs/DTS/product_specifications">Product Specifications</a> for details about link Specifications.</div><br> |
      |**Synchronization topology** |Select the synchronization topology based on your business requirements. Currently, only **Unidirectional synchronization** is supported. |
      |**Blue and green instances** |Confirm the information for the blue and green instances. |
      |**Project** |(Optional) Select the task's affiliated project from the drop\-down list. The default is **default (Default project)** . You can also click **Create new project** to create a new project. For details, refer to [Creating a project](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">To grant a sub\-user permission to access resources in a specific project, refer to <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Project_Permission_Management">Modifying project permissions</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After a task is successfully created, if you need to modify the instance's affiliated project, for example, by moving the task from the current project to another, you can move the resource to the specified project.</div><br><br><br>* <div data-tips="true" data-tips-type="default">A project is a virtual concept that includes a set of resources, users, and roles. A project allows you to view and manage a group of resources in a unified manner and control the permissions of users and roles to these resources.</div><br> |
      |**Tag** |(Optional) Click **Add Tag** to add a tag to the instance. Tags can help you classify cloud resources, control access to them, and allocate bills and costs. A tag is a key\-value pair that identifies a cloud resource. You can use tags to classify resources with the same characteristics from different dimensions, such as purpose and owner, to simplify filtering, aggregation, and resource management. For more information about tags, see [Tag Overview](https://docs.byteplus.com/en/docs/resourcemanagement/Tag_Overview). The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, digits, spaces, or symbols (_.:/=+\-@).<br><br>   * It is case\-sensitive, and the length must be between 1 and 128 characters.<br><br>   * Uses Unicode format with UTF\-8 encoding.<br><br>   * The key cannot start with volc: in any form (e.g., Volc:, VOLC:, etc.).<br><br>* (Optional) Value<br><br>   * Supports any language, characters, digits, spaces, or symbols (_.:/=+\-@).<br><br>   * Case\-sensitive, with a length of 0 to 256 characters.<br><br>   * Use Unicode format with UTF\-8 encoding.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Bind up to 20 Tags to a task at a time. A single task can have a maximum of 50 Tags.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The Tag Key for a resource must be unique, and each Tag Key can have only one Value.</div><br> |
      |**Billing method** |Select a billing method. Currently, only **Pay\-as\-you\-go** is supported. |
      

   2. On the **Configure synchronization objects** page, complete the following configurations and click **Pre\-check** to initiate the pre\-check and go to the **Pre\-check** page.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Synchronization type** |Select the synchronization type as needed. By default, all four synchronization types are selected: **User initialization**, **Schema initialization**, **Full initialization**, and **Incremental synchronization**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Synchronization tasks do not support synchronizing trigger and event objects.</div><br> |
      |**Migration user** |Select the target Accounts as needed and set new passwords in the **New password (optional)**  column. When migrating multiple Users, Click **Batch modify password** to modify the passwords of the Accounts to be migrated. If not modified, the Account passwords in the target Database will be the same as in the source Database.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This configuration is supported when <strong>Synchronization type</strong> is set to <strong>User Initialization</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">During Database Synchronization, User and Privilege Synchronization must be handled separately. If some Accounts in the source Database do not support Synchronization, Firstly, ensure that your business is not impacted by the absence of the Accounts that need to be synchronized.</div><br> |
      |**Synchronization object** |Select the objects to be synchronized. You can only select **the entire instance** as the synchronization object. |
      |**Error retry time** |If a synchronization task fails due to a disconnection between the source and destination databases, it will immediately retry the connection multiple times within the specified time. Value range: 600 to 86400, in seconds (s). The default value is 600 seconds. |
      |**Full synchronization rate** |Set the rate for full synchronization as needed. To avoid impacting source database performance due to a high synchronization rate, adjust the following parameters based on the read/write pressure of the source and target databases:<br><br><br>* **Rows to synchronize per second**: Enable and set the number of rows to synchronize per second as needed. The default value is 100,000, and the value range is 1 to 100,000.<br><br>* **Data volume to synchronize per second**: Enable and set the data volume to synchronize per second as needed. The default value is 25,000, the value range is 1 to 25,000, and the unit is KB. |
      

   3. After the pre\-check is complete, the **Pre\-check** page displays the check result for each check item. If the pre\-check passes, click **Confirm order** to create the blue\-green deployment synchronization task.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">For detailed descriptions of the pre\-check, refer to <a href="https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_mysql">Pre\-check items</a>.   </div>
   


<span id="SoYFwL5w"></span>
## Related document

For more information on creating data synchronization tasks, refer to [Synchronize from BytePlus for MySQL to BytePlus for MySQL](https://docs.byteplus.com/en/docs/DTS/synchronizing_to_byteplus_rds_for_mysql_rdsmysql).
