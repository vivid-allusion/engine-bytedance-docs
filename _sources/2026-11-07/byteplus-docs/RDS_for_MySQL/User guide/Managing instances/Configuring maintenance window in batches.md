---
title: "Configuring maintenance window in batches"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_maintainable_window_in_batches"
---

This topic introduces how to configure maintainable time periods for batch RDS for MySQL instances.

<span id="background"></span>
## Background

To protect the stability of cloud databases, the back\-end system will perform maintenance on instances irregularly. To ensure business stability during maintenance and reduce the impact on business, RDS for MySQL supports configuring maintainable time periods. The maintainable time period can be configured on a weekly cycle, and one or more days of the week can be selected as maintainable days. Within a maintainable day, a specific time period can be selected as the maintainable time period.

<span id="precautions"></span>
## Precautions


* To protect the stability of cloud databases, the back\-end system will perform maintenance on instances irregularly. It is recommended to set the maintainable time period during business off\-peak periods to avoid impacting business.

* Within the maintainable time period, the instance may experience 1 to 2 connection flickers. Please ensure that the application has an automatic reconnection mechanism.

* After submitting a task to be executed during the maintainable time period, the instance status will change to **Changing**. After the task execution is completed, the instance status will change to **Running**. During this period, operations that require the instance status to be **Running** cannot be performed on the instance. For specific details, please refer to the prerequisites of each operation. To avoid affecting your business, it is recommended to initiate a maintainable time period task after full estimation.

* When upgrading an instance, it will be evaluated according to the maintainable time period set for the instance. If the upgrade cannot be completed in the nearest maintainable time period, it will be postponed to the next maintainable time period.

* A maximum of 10 instances can be set with maintainable time periods at the same time.


<span id="prerequisites"></span>
## Prerequisites

The status of all instances to be batch\-configured with maintainable time periods is **Running**.

<span id="steps"></span>
## Steps


1. Log on to the [RDS for MySQL Console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region to which the instance belongs.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project to which the instance belongs has not been set, for this operation, you should select the project as <strong>All Resources</strong>.   </div>
   

3. Click **Instances** on the left navigation bar.

4. On the **Instances** page, select the instances for which you want to set the maintainable window.

5. Click  **... \> Modify maintainable window** below the instance list to enter the **Modify maintainable window** page.

6. On the popped\-up **Modify maintenance window** page, select **Maintainable day** and **Maintainable window** respectively, and after checking **I have read the above reminder and agree to the operations**, click **Confirm**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The minimum time interval for the maintainable time period is 2 hours, and the maximum time interval is 24 hours. Selecting a maintainable time period across days is not allowed.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The default maintainable time period is a random value. Please adjust and confirm this time period setting according to your business needs. It is recommended to specify business off\-peak periods as the maintenance time period to reduce the impact of change operations on business.   </div>
   


<span id="related-apis"></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyDBInstanceMaintenanceWindow](https://www.volcengine.com/docs/6313/1131818) |Call the ModifyDBInstanceMaintenanceWindow interface to modify the maintainable time period of a specified MySQL instance. |
