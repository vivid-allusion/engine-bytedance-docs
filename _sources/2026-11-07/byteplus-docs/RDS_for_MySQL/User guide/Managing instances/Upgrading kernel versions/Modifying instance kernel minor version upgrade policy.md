---
title: "Modifying instance kernel minor version upgrade policy"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Modifying_instance_kernel_minor_version_upgrade_policy"
---

This topic describes how to modify the instance kernel minor version upgrade policy.

## Prerequisites

An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

## Precautions

The maintenance cycle for RDS for MySQL kernel minor versions is six months. If the kernel minor version of an instance exceeds its maintenance cycle, the system temporarily ignores the upgrade policy, automatically upgrades the kernel minor version, and notifies you through internal messages. The automatic upgrade of an instance's kernel version depends only on its current kernel version, not its creation time. For detailed information about the kernel version maintenance cycle, refer to [Kernel minor version release note](https://docs.byteplus.com/en/docs/RDS_for_MySQL/kernal_version_release_notes).

During the instance kernel minor version upgrade, the system upgrades the kernel components and proxy components of the instance.

## Procedure

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the project and region for the instance.

   > **tip**

   > If the project to which the instance belongs is not set, this operation should select the project as **All resources**.

3. On the Instances page, click the target instance name.

4. On the **Summary** tab, in the **Configuration** section, click Edit next to **Kernel version upgrade policy**.

5. In the **Kernel version upgrade policy settings** dialog box, set the kernel version upgrade method and click **OK**. You can choose:

   * Manual upgrade: Manually upgrade the instance kernel version on the Summary page. For details, refer to [Upgrading instance kernel minor version manually](https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version).

   * Automatic upgrade: if the kernel minor version of an instance exceeds its maintenance cycle, the system notifies you through internal messages, and it is automatically upgraded to the latest minor version during the maintenance window of the instance.

   > **tip**

   > If you choose to upgrade within the maintenance window, you need to confirm the instance's maintenance window.

   * > You can click **Edit** to modify the maintenance window of the instance. For detailed rules on setting maintenance window, see [Configuring maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period).

   * > After a task is initiated, you can still modify the instance's maintenance window, but the execution time of the initiated task will not be automatically adjusted with the modification of the maintenance window. If you need to adjust the execution time of a task, you need to manually schedule and adjust it at Task center. For more information about modifying tasks execution time, see [Changing the execution time of a task](https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_the_execution_time_of_a_task).

## Related API

|API |Description |
|---|---|
|[ModifyDBInstanceAutoUpgradeEngineMinorVersion](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstanceautoupgradeengineminorversion) |Call the ModifyDBInstanceAutoUpgradeEngineMinorVersion API to modify the upgrade strategy for the instance's kernel minor version. |
