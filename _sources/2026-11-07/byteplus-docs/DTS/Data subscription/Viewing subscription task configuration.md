---
title: "Viewing subscription task configuration"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/view-subscription-task-configuration"
---

This topic describes how to view subscription task configuration on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A data subscription task has been created. Refer to [Overview](https://docs.byteplus.com/en/docs/DTS/overview_of_subscription_solutions#.6K6i6ZiF5pa55qGI5qaC6KeI) for detailed operations.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data subscription**.

4. On the **Data subscription list** page, click the target task name.

5. On the target task name page, click **Task configuration**.

6. On the **Task configuration** tab, you can view the following information:

   * View the basic configuration of the task, as shown below:

      * **Subscription format**: In the **basic configuration** area, you can view the subscription format selected when creating the data subscription task. For details on data subscription, refer to [Data subscription format](https://docs.byteplus.com/en/docs/DTS/data_subscription_format).

      * **Subscription data type**: In the **basic configuration** area, you can view the subscription type selected when creating the subscription task, such as database and table schema subscription, incremental subscription, or full subscription.

      * **Starting timestamp**: In the **basic configuration** area, you can view the starting timestamp selected when creating the subscription task, such as the system default, specified GTID, specified GTID_EXECUTED, or specified GTID_EXECUTED.

      * **Subscription object**: In the **basic configuration** area, click **View subscription object** to see the subscription object in the **Subscription object** dialog box.

         * Click **View subscription object** to view the subscription object in the dialog box.

         * Click **View custom Topic** to view the custom Topic in the dialog box.

         * Click **View database & table automatic delivery rules** to see the database & table automatic delivery rules in the dialog box. If the information is blank, it indicates that the database & table automatic delivery rules have not been enabled.

      * **Delivery policy**: View the delivery policy selected in the subscription task, for example, unified delivery to Partition 0.

   * View the advanced configuration of the task

      In the **Advanced configuration** area, you can view the advanced configuration items of the task, as shown below.

      * **Enable ETL configuration**: View whether ETL configuration is enabled for the task. Check whether ETL configuration is enabled. If the task has ETL enabled, you can click **Edit** to modify the task’s ETL rules. For detailed steps, refer to [Modifying ETL configuration in existing synchronization or subscription tasks](https://docs.byteplus.com/en/docs/DTS/configuring_etl_in_dts_synchronization_task#.5Zyo5bey5pyJ5ZCM5q2l5oiW6K6i6ZiF5Lu75Yqh5Lit5L-u5pS5LWV0bC3phY3nva4=).

      * **Subscribe Begin/Commit**: Check whether to subscribe to Begin/Commit.

      * **Subscribe to all fields**: View whether to subscribe to all fields.

      * **Error retry time**: View the error retry time configured in the subscription task. The default value is 600 seconds.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Configuration information for the subscription task is related to the options and database type selected during task configuration. If you can not find certain information as shown above, it may be because that type was not selected or the subscribed database does not support it.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Only subscription tasks with the access method set to RDS for MySQL or veDB for MySQL support configuring ETL rules.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The viewing of subscribe to all fields parameters is supported only when <strong>Instance type</strong> is <strong>MySQL</strong>, the access method for the middleware is <strong>Message Queue for Kafka</strong> or <strong>Kafka connected over express network</strong>, and the <strong>Subscription format</strong> is <strong>Canal JSON</strong>.      </div>
      


<span id=".55u45YWz5paH5qGj"></span>
## Related document

For subscription tasks in progress, you can modify the subscription object as needed. For detailed steps, refer to [Changing a subscription object](https://docs.byteplus.com/en/docs/DTS/changing_subscription_objects).
