---
title: "Configuring maintenance window"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Configuring_maintenance_window"
---

To protect the stability of cloud databases, the backend system will maintain the instances within the maintenance period. To ensure the stability of business during maintenance and reduce the impact on business, you can set the maintenanceable time period at the business peak according to business rules. This article describes how to configure a maintainable time period for instance.

<span id="应用场景"></span>
## Application scenarios

Maintainable time period refers to the time period when an instance is allowed to perform maintenance operations. Currently, only the following operations support manual selection whether to perform within maintenanceable time:


* [Modify instance configuration](https://www.byteplus.com/en/docs/NDB_for_MySQL/Changing_node_specifications)

* [Modifying parameters](https://www.byteplus.com/en/docs/NDB_for_MySQL/Modifying_parameters)

* [Apply parameter template](https://www.byteplus.com/en/docs/NDB_for_MySQL/Apply_parameter_template)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Selecting an action that is performed during the maintenance period will be displayed in the planned event list. You can cancel or modify the execution time of the target event in the planned event list. For more information, see <a href="https://www.byteplus.com/en/docs/NDB_for_MySQL/Planned_events">Planned events</a>.</div>


<span id="注意事项"></span>
## Precautions


* During the execution of tasks set in the maintenance time period, the instance cannot be reconfigured, billing type changed, or connection endpoint managed. Therefore, it is recommended to set the maintenance time period during the business off\-peak period to avoid affecting the business.

* Within the maintainable time period, the instance may experience 1 to 2 connection flickers.


<span id="操作步骤"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the instance name of the target instance to enter the **Summary** page.

4. In the **Basic Information** area, click **Edit** after the **Maintenance window**.

5. In the dialog box that pops up, select the **Maintenance window** and click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The minimum time interval for the maintainable time period is 2 hours, and the maximum time interval is 24 hours.   </div>
