---
title: "Batch stopping and starting instances"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Batch_stopping_and_starting_instances"
---

This topic describes how to batch stop and start RDS for MySQL instances.

## Precautions

* Only pay\-as\-you\-go instances can be stopped.

* When an instance is stopped or started, its billing items are adjusted. Your account balance must be 100 USD or more, or you cannot pause or start an instance. To top up your account, refer to the [recharging instructions for details](https://docs.byteplus.com/en/docs/6269/100434). For more information on placing orders, refer to [Order Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-orders).

* Disaster recovery instances cannot be stopped.

* Instances with blue\-green deployment cannot be stopped.

* An instance can be stopped for a maximum of 30 days. After an instance is stopped for more than 30 days, it automatically starts and billing resumes. If an instance does not meet the startup conditions, the stop period is automatically extended.

* While an instance is stopped:

   * The instance becomes inaccessible, and in the RDS for MySQL console, you can only view its Summary, Connectivity, and Backups pages. Except for starting the instance, downloading backups, restoring to a new instance, and modifying the instance backup policy, no other actions are supported while the instance is stopped.

   * The allowlists associated with the instance cannot be modified or deleted. The instance's original allowlist configuration is restored when it starts.

   * The instance will no longer provide external services, and its monitoring data may become abnormal, which can trigger alarm policies. In this case, you need to manually deactivate the alarm policies. Before stopping the instance, deactivate its alarm policies and re\-enable them after starting the instance to avoid excessive alarm noise.

   * The basic backup storage space provided for the instance remains free of charge. If we start charging for this storage space, we will make an announcement one month in advance.

* If server resources are insufficient when you restart a suspended instance, the system automatically migrates the instance and then starts it. No manual intervention is required.

* Starting a suspended instance requires data migration. The startup duration depends on the amount of data to migrate. You can view the startup progress in the Task center.

* After a stop instance operation is initiated, the system creates a full backup for the instance before stopping the instance. When a stopped instance is released due to overdue payments, its backups are retained according to the "Backup retention policy after instance release" set for the instance.

* If the account is in arrears during the instance suspension period, after recharging, the instance will still be in **Stopped**.

## Prerequisites

* To stop an instance, its state must be **Running** and its billing method must be Pay\-as\-you\-go.

* To start an instance, its state must be **Stopped**.

## Stop an instance

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the project and region for the instance.

   > **tip**

   > If the project of the instance has not been set, the project should be selected as **All resources**.

3. Click **Instances** in the left navigation bar.

4. On the **Instances** page, select the instance that you want to stop, and then click  **…**  \> **Stop instance**.

5. In the **Batch stop instances** dialog box, read the prompt, select the checkbox, and click **Confirm Stop**.

## Start an instance

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the project and region for the instance.

   > **tip**

   > If the project of the instance has not been set, the project should be selected as **All resources**.

3. Click **Instances** in the left navigation bar.

4. On the **Instances** page, select the instance that you want to start, and then click  **...**  \> **Start instance**.

5. In the **Batch start instances** dialog box, read the prompt and select the checkbox, then click **Confirm Start**.
