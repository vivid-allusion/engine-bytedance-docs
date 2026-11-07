---
title: "Configuring maintenance window"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Configuring_maintenance_window"
---

This topic describes the procedure for configuring the maintenance window for RDS for PostgreSQL instances.

<span id="gkCToWpP"></span>
## Background information

To ensure database stability, the backend system periodically maintains instances. To ensure service stability and reduce the impact on your business during maintenance, RDS for PostgreSQL allows you to configure a maintenance window. After configuring the maintenance window, the backend will choose the maintenance window period to maintain the instance. You can configure a weekly maintenance window and select one or more days of the week as maintenance days. Within the selected maintenance days, you can select a specific time period as the maintenance window.

<span id="W8Lfilk1"></span>
## Precautions


* Set the maintenance window during off\-peak hours to avoid impacting your services.

* During the maintenance window, the instance may experience 1 to 2 brief connection interruptions. Ensure that your application is equipped with an automatic reconnection mechanism.

* Currently, upgrading instances is only supported within the maintenance window. If the upgrade can not be completed within the nearest maintainable window, it will be postponed to the next maintainable window.


<span id="bot0wwjL"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click **Instances** in the left navigation bar.

4. Click the name of the target instance on the **Instances** page to go to the **Summary** page.

5. On the **Summary** tab, in the **Summary** section, click the **Edit** button to the right of **Maintenance window**.

6. In the pop\-up **Maintenance window**, set the **Maintainable day** and **Maintenance window**, and then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">At least one day and up to seven days per week can be set as maintainable days.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The maintenance window can only be set from 00:00 to 05:59 (UTC+08:00).   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The minimum duration for the maintenance window is 2 hours and the maximum is 6 hours; cross\-day selection of the maintenance window is not allowed.   </div>
   


<span id="U6X4bY1P"></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyDBInstanceMaintenanceWindow](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstancemaintenancewindow) |Call the ModifyDBInstanceMaintenanceWindow API to modify the maintenance window of a specified PostgreSQL instance. |
