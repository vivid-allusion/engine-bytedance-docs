---
title: "Configuring maintenance window"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Configuring_maintenance_window"
---

To protect the stability of cloud databases, the backend system will maintain the instances within the maintenance period. To ensure the stability of business during maintenance and reduce the impact on business, you can set the maintenanceable time period at the business peak according to business rules. This article describes how to configure a maintainable time period for instance.

<span id="MIQK3fre"></span>
## Precautions


* The default maintenance window for new instances is 02:00–05:59 (UTC+08:00) daily. You can also change this setting when creating an instance. Existing instances do not have a default maintenance window and must be configured manually on the **Summary** page.

* Operations performed during the maintenance window are displayed in the operation and maintenance events list. For more details, see [Viewing operation and maintenance events](https://docs.byteplus.com/en/docs/HBase/Viewing_operation_and_maintenance_events).

* During the execution of a task set within a maintainable time period, instances cannot undergo operations such as configuration changes or billing type changes. Therefore, it is recommended to set the maintenance time period during the business off\-peak period to avoid affecting the business.

* Within the maintainable time period, the instance may experience 1 to 2 connection flickers.


<span id="Lvu7MrkX"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the instance name of the target instance to enter the **Summary** page.

4. In the **Basic Information** area, click **Edit** after the **Maintenance window**.

5. In the dialog box that appears, select a **Maintainable day** and **Maintenance window**, and click **OK**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The minimum time interval for the maintainable time period is 2 hours, and the maximum time interval is 24 hours.   </div>
