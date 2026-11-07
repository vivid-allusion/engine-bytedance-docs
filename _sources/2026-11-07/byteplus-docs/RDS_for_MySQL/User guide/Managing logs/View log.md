---
title: "View log"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_and_downloading_logs"
---

This topic describes how to view the switchover log and error log.

## **Precautions**

Only monitoring information from the past 30 days can be viewed, and the maximum time range for each query is 7 days.

## Procedure

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the project and region for the instance.

   > **tip**

   > If the project to which the instance belongs is not set, this operation should select the project as **All resources**.

3. Click **Instances** in the left\-side navigation bar.

4. On the **Instances** page, click the target instance name.

5. At the top of the page, click the **Logs** tab to view the Switchover log and Error log for the instance.

   > **tip**

   * > The **Switchover log** tab displays the **New primary node**, **Old primary node**, **Switch time, Type/Source, Switch reason, and Bind task**. Click a task in the **Bind task** column to go to the **Task center** to view the task details.

   * > The **Error log** tab displays the **Collection time** and **Log details**.

## Related API

|API |Description |
|---|---|
|[DescribeFailoverLogs](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describefailoverlogs) |Call the DescribeFailoverLogs API to query the primary\-secondary switchover logs of a MySQL instance. |
