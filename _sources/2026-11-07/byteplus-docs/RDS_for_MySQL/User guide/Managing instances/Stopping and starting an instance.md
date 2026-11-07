---
title: "Stopping and starting an instance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/stopping_and_starting_an_instance"
---

This topic describes how to stop and start an RDS for MySQL instance.

## Background

Stopping an instance is a deactivation feature for RDS for MySQL. While an instance is stopped, it is inaccessible, but its data and network configuration are fully retained. You can start the instance when needed to quickly resume its operations. While an instance is stopped, you are only charged for its backup storage space and data storage space.

## Precautions

* Only pay\-as\-you\-go instances can be stopped.

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

3. Click **Instances** in the left\-side navigation bar.

4. On the **Instances** page, click  **...**  \> **Stop Instance** in the target instance **Action** column.

5. In the **Stop instance** dialog box that pops up, after reading and checking the prompt, click **OK**.

## Start an instance

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the project and region for the instance.

   > **tip**

   > If the project of the instance has not been set, the project should be selected as **All resources**.

3. Click **Instances** in the left\-side navigation bar.

4. On the **Instances** page, click **Start Instance** in the target Instance **Action** column.

5. In the **Start instance** dialog box that pops up, click **OK**.

## Related API

|API |Description |
|---|---|
|[StopDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/stopdbinstance) |Call the StopDBInstance API to pause the instance. |
|[StartDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/startdbinstance) |Call the StartDBInstance API to start the instance. |
