---
title: "Viewing migration task configuration"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/view-migration-task-configuration"
---

This topic describes how to view migration task configuration on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A data migration task has been created. For details, refer to Creating a data migration task. For more information, refer to [Migration solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_migration_solutions#.6L-B56e75pa55qGI5qaC6KeI).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. On the **Data migration list** page, click the target task name.

4. On the target instance list page, click **Task configuration**.

5. On the **Task configuration** tab, you can view the following information:

   * View the basic configuration of the task, as shown below:

      * **Migration data type**: View the migration type selected when creating the migration task, such as user migration, schema migration, full migration, or incremental migration.

      * **Migration starting point**: View the migration starting point selected when creating the migration task, such as system default, specified GTID, specified GTID_EXECUTED, or specified timestamp.

      * **Whether to enable foreign key check?** : View whether foreign key check was enabled when creating the migration task.

      * **Migration object**: Click **View migration object**. In the **Migration object** dialog box, view details of the migration object.

   * View the advanced configuration of the task, as shown below:

      * **Enable transaction merging?** : View whether transaction merge is enabled for the migration task.

      * **Migration preferences**: View the preferences of the migration task, such as space first or performance first.

      * **Enable ETL configuration**: View whether ETL configuration is enabled for the task. If the task has ETL enabled, you can click **Edit** to modify the task’s ETL rules. For detailed steps, refer to [Modifying ETL configuration in existing synchronization or subscription tasks](https://docs.byteplus.com/en/docs/DTS/configuring_etl_in_dts_synchronization_task#.5Zyo5bey5pyJ5ZCM5q2l5oiW6K6i6ZiF5Lu75Yqh5Lit5L-u5pS5LWV0bC3phY3nva4=).

      * **Error retry time**: You can view the error retry time configured in the migration task.

      * **Whether to skip post\-migration**: You can check if the migration task skips post\-migration.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Task configuration depends on the options and database type selected during the migration task setup. Therefore, the task configuration you see may not fully match the descriptions above.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Only when the source instance is RDS for MySQL, the corresponding migration task supports such configurations as enabling ETL configuration, enabling transaction merging?, and setting migration preferences.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Only when the source instance for migration is RDS for PostgreSQL, the corresponding migration task supports configuring whether to skip post\-migration.      </div>
      


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

When the migration task status is **To be started**, you can modify the migration object as needed. For details, refer to [Configuring a migration task](https://docs.byteplus.com/en/docs/DTS/configuring_a_migration_task).
