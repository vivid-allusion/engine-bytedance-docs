---
title: "Modifying the execution time of operation and maintenance events"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Modifying_the_execution_time_of_operation_and_maintenance_events"
---

Table Storage for HBase supports modifying the execution time of some operation and maintenance events that are pending execution. This article describes the steps to modify the operation and maintenance event time.

<span id="BDkfQEX1"></span>
## Prerequisites


* The operation and maintenance event is in **Waiting for execution** state.

* The scheduled execution time of the operational event is more than 24 hours away.


<span id="YNx5l7i0"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/region:db+cn-beijing/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. In the left\-side navigation pane, select **Operation and maintenance event**.

4. On the **Operation and maintenance event** page, click **Change execution time** in the **Actions** column for the target maintenance event.

5. In the dialog box, select **Switching time** and **Specify time period**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Modification time must not be later than the current time.‌   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If execution cannot be completed within the specified time, it will continue to be executed in the next maintainable time period.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The scheduled execution time will be automatically specified based on the instance details and the selected time.   </div>
