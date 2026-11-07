---
title: "About operation and maintenance events"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/about_operation_and_maintenance_events"
---

The operation and maintenance events of the RDS for MySQL refer to database software upgrades, hardware maintenance and upgrades and other events. In order to facilitate the management and maintenance of instances and make reasonable business arrangements, the operation and maintenance events of the RDS for MySQL console list the planned operation and maintenance events. In the operation and maintenance event list, you can view the instance ID, event ID, event operation, event type, event status, planned execution time, latest deferrable time, business impact and operation and other information related to the operation and maintenance event.

## Notification rules for operation and maintenance events

RDS for MySQL will send notifications for operation and maintenance events at least one week in advance via SMS, email, and internal messages, and initiate operation and maintenance events for instances in the console. You can find the specific event type, region, event cause, business impact, affected instances, and scheduled execution time in the notification or the operation and maintenance event in the console. To give you enough time to coordinate your business and minimize or eliminate the business impact of version upgrade operation and maintenance events, RDS for MySQL initiates these events one week in advance.

## Rules for postponing the execution time of operation and maintenance events

The execution time of RDS for MySQL operation and maintenance events supports postponement. When postponing the execution time of operation and maintenance events, the following rules need to be met:

* The execution time is allowed to be postponed or postponed multiple times, but not later than the latest deferrable time of the event.

* Postponement is not allowed when the planned execution time is less than 24 hours.Advance execution time is not allowed.

> **warning**

> If the instance's maintenance window is advanced after the instance receives a maintenance event (i.e., a pending maintenance event in the instance's list of maintenance events), RDS for MySQL adjusts the execution time of the planned maintenance event by selecting the most recent execution of the maintenance event in the adjusted maintenance window.

## Causes and effects of operation and maintenance events

The event causes and business impacts of operation and maintenance events for RDS for MySQL are described in the table below.

|**Event type** |**Event cause** |**Business impact** |
|---|---|---|
|Version upgrade |Routine version upgrades and iterations to fix known issues and release new features.<br><br> |During the switching process, there may be a flash disconnection in seconds. It is recommended to set up an automatic retry and reconnection mechanism for the program to avoid affecting the business. |
|SSL certificate update |The certificate used by the instance SSL function is about to expire. To ensure the normal operation of the function, the validity period of the certificate is extended. ||
|Host operation and maintenance |The instance host hardware is aging abnormally and needs maintenance, or the host module needs to be upgraded. ||
|Temporary upgrade expiration restoration |Restoration due to temporary upgrade expiration. ||
|Node reconstruction |Rebuilt the node |Rebuilding a node will affect the endpoint associated with the node, which may cause the connection through the endpoint to be disconnected in seconds. It is recommended to set an automatic reconnection mechanism for the program to avoid the impact. |
|Startup of stopped instance |Restoration due to stopped instance expiration.<br><br> |None. |
