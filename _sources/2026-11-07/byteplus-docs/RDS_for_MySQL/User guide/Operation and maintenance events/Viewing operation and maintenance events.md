---
title: "Viewing operation and maintenance events"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/view_operation_and_maintenance_events"
---

In addition to notifications by SMS, email, or internal messages, operation and maintenance events and emergency events for RDS for MySQL, such as instance migration and version upgrades, are also listed in the Operation and maintenance events menu of the RDS for MySQL console. This topic describes how to view information about operation and maintenance events in the console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

An instance has been created. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Host operation and maintenance is initiated for hardware maintenance on the host machine of the instance. If an instance undergoes operations such as configuration changes or migrating availability zones after a host operation and maintenance event is initiated, and has been migrated from the original host, the event is no longer required and is automatically canceled.

* Operation and maintenance events involve software, hardware, and network upgrades on physical devices. To avoid business impact, ensure that your services have an automatic reconnection mechanism.

* Before the scheduled execution time, the operation and maintenance event is in the **Not executed** state. During this period, normal data access to the related database is not affected.

* After the scheduled execution time, the operation and maintenance event enters the **Running** state. During an instance switchover, a transient connection interruption and a read\-only period of up to 30 seconds typically occur.

* After the operation and maintenance event is completed, the access point and usage of the database instance remain the same as the original instance, and the instance's availability zone, network, and migration tasks are unaffected.

* If the operation and maintenance event is not completed due to factors such as network freezes or rescheduling, RDS for MySQL automatically cancels the upgrade.

* If there are any **Not executed** or **Executing** operation and maintenance events in the current region, a corresponding prompt is displayed for the Operation and maintenance event item in the menu bar.


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

3. In the left\-side navigation pane, click ** Operation and maintenance event** to go to the **Operation and maintenance event** list.

4. In the **Operation and maintenance event** list, you can view information such as instance ID, event ID, event type, event state, scheduled execution time, latest postponed time, business impact, and operations.

   You can filter and view target events on demand, and you can also filter and display the operation event list.

   * Filter view: supports filtering operation and maintenance events by scheduled execution time, instance ID, and event ID.

   * Filtered view: supports filtering the operation and maintenance event list by event state.


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Note |
|---|---|
|[DescribePlannedEvents](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeplannedevents) |Call the DescribePlannedEvents API to query the list of planned events. |
