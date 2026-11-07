---
title: "Modifying maintenance periods in batches"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modifying_maintainable_periods_in_batches"
---

Cache for Redis supports batch modification of the maintainable period. You can batch set the same maintainable period for instances with consistent or similar business off\-peak periods, avoiding or reducing the impact on the business during the maintenance process while improving the efficiency of instance management. This topic describes how to batch modify maintenance periods.

## Prerequisite

The instance status that needs to modify maintenance periods in batches is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Precautions

* Cache for Redis supports setting the execution time of certain instance maintenance operations (such as modifying instance configurations) within the maintainable period. When performing these operations during the maintainable period, the instance may experience connection disruptions. It is recommended to set the maintainable period during the business off\-peak period and ensure that the application has an automatic reconnection mechanism. For details on operations that can be performed during the maintenance period, refer to [Use cases](https://docs.byteplus.com/en/docs/redis/set-maintenance-period#.5bqU55So5Zy65pmv).

* **If you choose to perform database O&M operations (such as changing the configuration) during the maintenance period, the instance status will immediately change (such as changing to ** **`Scaling`** **) and this status will persist until the task is completed, but the actual execution time of the operation task is still within the maintainable period**.

* You can select a maximum of 10 instances simultaneously to batch modify the maintainable period.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, select the instances for which you want to set maintenance periods.

   > **tip**

   > You can select a maximum of 10 instances simultaneously to batch modify the maintainable period.

4. Below the instance list, click **Modify maintainable period**.

5. In the pop\-up **control** panel, first confirm the information of the instances that need to have the maintainable period batch modified (such as instance name, ID, version) in the **Selected instances** area, and then set the following configurations according to your business needs in the **Maintenance period** area.

   |Parameter |Description |
   |---|---|
   |Cycle |Fixed as **By week**, no need to set. |
   |Maintainable |Fixed as Monday to Sunday (that is, every day of the week can be maintained), no need to set. |
   |Maintenance period |The default maintainable time period is from 02:00 to 03:59 every day. You can select the appropriate start time and end time from the drop\-down box according to the actual needs of your business.<br><br>> **tip**<br><br><br>> To ensure that the task can be carried out normally within the maintainable period, when batch modifying the maintainable period, the minimum interval between the start and end times is 2 hours, the maximum interval is 24 hours, and it is not allowed to select the maintainable period across days. For example, if the start time point for batch modifying the maintainable period is 01:00, then the selectable value range for the end time point is from 02:59 to 23:59.<br> |

6. In the lower\-left corner of the page, check **I have read the above reminder and agree to proceed the operation**, then click **OK** in the lower\-right corner.
