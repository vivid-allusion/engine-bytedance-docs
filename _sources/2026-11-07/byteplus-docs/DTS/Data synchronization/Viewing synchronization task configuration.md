---
title: "Viewing synchronization task configuration"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/view-synchronization-task-configuration"
---

This topic describes how to view the task configuration of a synchronization task on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A synchronization task has been created. Refer to [Overview](https://docs.byteplus.com/en/docs/DTS/overview_of_synchronization_solutions#.5ZCM5q2l5pa55qGI5qaC6KeI) for detailed operations.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data synchronization**.

4. On the **Data synchronization list** page, click the target task name.

5. On the target task name page, click **Task configuration**.

6. On the **Task configuration** tab, you can view the following information:

   * View the basic configuration of the task, as shown below:

      * **Synchronization type**: You can view the synchronization type selected when creating a synchronization task, such as user initialization, schema initialization, full initialization, or incremental synchronization.

      * **Synchronization starting point**: View the synchronization starting point selected when creating the synchronization task, such as system default, specified GTID, specified GTID_EXECUTED, or specified timestamp.

      * **Whether to enable foreign key check?** : View whether foreign key check was enabled when creating the synchronization task.

      * **Synchronization objects**: Click **View synchronized objects**, and in the **Synchronization objects** dialog box, view the synchronization objects.

         If synchronization objects were modified, the names before and after modification are displayed.

      * **Write mode**: You can view the write mode selected when creating a synchronization task, such as `Upsert` or `Insert`.

   * View the advanced configuration of the task, as shown below:

      * **Enable transaction merging?** : View whether transaction merge is enabled for the synchronization task.

      * **Synchronization preferences**: View the preferences of the synchronization task, such as space first or performance first.

      * **Enable ETL configuration**: View whether ETL configuration is enabled for the task. If the task has ETL enabled, you can click **Edit** to modify the task’s ETL rules. For detailed steps, refer to [Modifying ETL configuration in existing synchronization or subscription tasks](https://docs.byteplus.com/en/docs/DTS/configuring_etl_in_dts_synchronization_task#.5Zyo5bey5pyJ5ZCM5q2l5oiW6K6i6ZiF5Lu75Yqh5Lit5L-u5pS5LWV0bC3phY3nva4=).

      * **Error retry time**: You can view the error retry time configured in the synchronization task.

      * **Whether to skip post\-migration**: You can check if the synchronization task skips post\-migration.

      * **Post\-schema synchronization**: You can view whether post\-schema synchronization is enabled for the synchronization task.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Only when the source instance for synchronization is MySQL, the synchronization task supports configuring ETL rules, whether to open transaction merge, synchronization preference configuration, and post\-schema synchronization.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Only when the source instance for synchronization is RDS for PostgreSQL, the corresponding synchronization task supports configuring whether to skip post\-synchronization.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Only when the source instance for synchronization is Milvus, the corresponding synchronization task supports configuring write mode.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Task configuration depends on the options and database type selected during the synchronization task setup. Therefore, the task configuration you see may not fully match the descriptions above.      </div>
      


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

If a Synchronization task is in progress, you can modify the synchronization object as needed, and you can view the record of changing the synchronization object. For details, refer to [Managing synchronized objects.](https://docs.byteplus.com/en/docs/DTS/managing_synchronization_objects#.5Y-Y5pu05ZCM5q2l5a-56LGh)
