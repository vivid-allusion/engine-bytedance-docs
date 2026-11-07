---
title: "Viewing operation and maintenance events"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/view_operation_and_maintenance_events"
---

This topic describes how to view the information related to the RDS for PostgreSQL operation and maintenance events in the console.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

RDS for PostgreSQL operation and maintenance events refer to planned events initiated to perform necessary upgrades and adjustments to the software, hardware and network that the instance depends on. In the RDS for PostgreSQL console operation and maintenance event list, the operation and maintenance events in the current region are listed. In the operation and maintenance event list, you can view the instance name, instance ID, event ID, event type, event status, planned execution time, planned switching time period, event cause, business impact, latest postponed time related and supported actions.

<span id=".6L-Q57u05LqL5Lu255qE6YCa55-l6KeE5YiZ"></span>
### Notification rules for operation and maintenance events

RDS for PostgreSQL will send notifications for operation and maintenance events via SMS, email or internal message at least 3 natural days in advance. You can learn the specific event type, region, event cause, business impact and planned execution time in the notification.

<span id=".6L-Q57u05LqL5Lu255qE5Y6f5Zug5LiO5b2x5ZON"></span>
### Causes and impacts of operation and maintenance events

RDS for PostgreSQL operation and maintenance events currently support two types: Version upgrade and Host offline. The business impact and description of these two operation and maintenance events are shown in the following table.


|Event type |Business impact |Impact statement |
|---|---|---|
|Version upgrade |Transient instance interruption |The connection may be broken in seconds during the switching process. It is recommended that the program set an automatic retry and reconnect mechanism to avoid the impact of the event. |
|Host offline |||


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

To ensure the stability of the database cloud service and continue to provide a high\-quality experience, we may initiate operation and maintenance events to perform necessary upgrades and adjustments to the software, hardware and network that the instance depends on. In order to minimize the impact on your business, we remind you to ensure that the business system has implemented the disconnection and reconnection mechanism, and please pay attention to the following important matters:


* Some operation and maintenance events enter the pre\-preparation stage before entering the planned execution time. During this process, the normal data access of the database itself will not be affected, but other configuration change operations on the instance will be prohibited before the overall change is completed.

* Operation and maintenance events will perform operations that affect database IO during the planned execution time period, and usually there will be flash disconnections. Please ensure that the business has a disconnection and reconnection mechanism. We will take the best solution for each specification to minimize the duration of the flash outage. The flash outage duration of large\-size instances may be slightly longer than that of small\-size instances.

* If the operation and maintenance event is not completed due to network blocking or rescheduling, the system will automatically cancel or adjust the relevant operation and maintenance event.


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. In the left\-side navigation pane, click ** Operation and maintenance event** to go to the **Operation and maintenance event** list.

4. In th**e Operation and maintenance events** list, the instance name, instance ID, event ID, event type, event status, planned execution time, planned switching time period, event cause, business impact, latest postponed time related and supported actions are displayed. You can filter and view target events on demand, and you can also filter and display the operation event list.

   1. Filter view: Support search and filter operation and maintenance events by instance name, instance ID, event ID, planned execution time period, and planned switching time period.

   2. Filtered view: Support for filtered view of operational events by event type and event status.


<span id=".55u45YWzIEFQSQ=="></span>
## Related APIs


|API |Note |
|---|---|
|[DescribePlannedEvents](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribePlannedEvents) |Call DescribePlannedEvents API to query the operation and maintenance events in the current region. |


&nbsp;
