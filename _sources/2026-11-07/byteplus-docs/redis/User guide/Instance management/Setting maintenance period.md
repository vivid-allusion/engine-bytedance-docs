---
title: "Setting maintenance period"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/set-maintenance-period"
---

After a Redis instance is successfully created, the system will default to setting the maintainable time period of the instance to any 2 hours between 00:00 and 05:59 (such as 02:00 ~ 03:59). You can set the maintainable time period during the business low peak according to business patterns to avoid or reduce the impact of the maintenance process on business.

## Application scenarios

The maintenance period refers to the time period during which Redis instances are allowed to perform maintenance operations. You can choose to perform certain actions during the maintenance period. Currently, the following actions can be executed within the maintenance period:

* [Restart instance](https://docs.byteplus.com/en/docs/redis/restart-instance)

* Modifying instance specifications (including [Modifying node specifications](https://docs.byteplus.com/en/docs/redis/modify-node-spec), [Modifying number of node](https://docs.byteplus.com/en/docs/redis/modify-node-number), [Modifying number of shard](https://docs.byteplus.com/en/docs/redis/modify-shard--number), [Enabling sharding cluster](https://docs.byteplus.com/en/docs/redis/modify-sharding-cluster-config), [Switching to primary-secondary instance](https://docs.byteplus.com/en/docs/redis/switch_to_high_availability_instance))

* [Modifying availability zone](https://docs.byteplus.com/en/docs/redis/modify-az)

* [Upgrading minor version](https://docs.byteplus.com/en/docs/redis/upgrade-minor-version)

> **tip**

> Operations performed within the maintenance period will be automatically added to the list of scheduled events. For more details on scheduled events, refer to [Managing planned events](https://docs.byteplus.com/en/docs/redis/manage-planned-event).

## Precautions

* If the relevant operations listed in [Application scenarios](https://docs.byteplus.com/en/docs/redis/set-maintenance-period#.5bqU55So5Zy65pmv) are performed within the maintenance period, the instance may experience a brief connection interruption. It is recommended to set the maintenance period during the off\-peak hours of the business and ensure that the application has an automatic reconnection mechanism.

* **If you choose to perform some database O&M operations (such as changing configuration) within the maintenance period, the instance status will immediately change (for example, to** **`Scaling`** **) and this status will persist until the task is complete, but the actual execution time of the operation task will still be within the maintenance period**.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. In the **Basic Information** area under the **Summary** tab, click **Modify** next to maintenance period.

5. In the pop\-up dialog box, select the appropriate time period in the **Maintenance period**, and then click **OK**.

   > **tip**

   > To ensure tasks proceed normally within the maintenance period, the duration of the maintenance period must be between 2 and 24 hours.

   > For example, if the maintenance period starts at 01:00, the selectable range for the end time is from 02:59 on the same day to 00:59 on the next day.

## Relevant APIs

|API |Description |
|---|---|
|[ModifyMaintenanceTime](https://docs.byteplus.com/en/docs/redis/modifymaintenancetime) |Call the ModifyMaintenanceTime API to modify the maintenance period of the target Redis instance. |
