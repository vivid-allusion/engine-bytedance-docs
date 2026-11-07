---
title: "Configuring maintenance window"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period"
---

This topic describes how to configure the maintenance window for RDS for MySQL.

<span id="background"></span>
## Background

To guarantee the stability of RDS, the backend system maintains the instances from time to time. To ensure business stability and reduce the impact on business during maintenance, RDS for MySQL supports the configuration of the maintenance period. You can configure the maintenance period on a weekly basis by specifying one or more days of the week as maintenance days. On the maintenance days, you can designate a specific period as the maintenance period.

<span id="precautions"></span>
## Precautions


* We recommend that the maintenance period be set to off\-peak hours to avoid any impact on business.

* The instance may temporarily disconnect once or twice in the maintenance period. Please make sure that the application has an automatic reconnection mechanism.

* After the task to be executed in the maintenance period is submitted, the instance status changes to **Modifying**. After the task is executed, the instance status changes to **Running**. During this period, the following operations cannot be performed on instances. To avoid affecting your business, we recommend that you initiate a maintenance period task only after ample consideration.

   * Modifying the instance configuration

   * Availability Zone Migration

   * Switching the billing method

   * Restarting an Instance

   * Deleting an instance

   * Connection endpoint management

   * Creating manual data backups

   * Data security management

   * Modifying Parameters

* An instance upgrade is evaluated based on the maintenance period set for the instance. If the upgrade cannot be completed within the current maintenance period, it is postponed to the next maintenance period.


<span id="procedure"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">If no project is set, you should select the option <strong>Account's all resource</strong> at this step.</div>



3. Click **Instance list** in the left\-side navigation bar.

4. Go to the **Instance list** page and click on the target instance name to open the **Instance information** page.

5. Click **Edit** to the right of **Maintenance window** in the **Instance information** area under the **Instance information** tab.

6. Select **Maintainable day** and **Maintenance window** in the pop\-up **Maintainable time** window, and click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">说明   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The maintenance period has a minimum time interval of 2 hours and a maximum time interval of 24 hours. You cannot select periods across multiple days.   </div>
   

<span id="relevant-apis"></span>
## Relevant APIs


|API |**Description** |
|---|---|
|[ModifyDBInstanceMaintenanceWindow](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstancemaintenancewindow) |Call ModifyDBInstanceMaintenanceWindow to modify the maintenance period of the specified MySQL instance. |
