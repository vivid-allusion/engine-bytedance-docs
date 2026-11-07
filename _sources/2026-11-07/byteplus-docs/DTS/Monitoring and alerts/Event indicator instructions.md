---
title: "Event indicator instructions"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Event_indicator_instructions"
---

Database Transfer Service (DTS) supports the monitoring of events and anomalies during data transmission, and can set up alarm rules. During data transmission, you will be notified immediately once an event reaches the set trigger rules, so that you can take timely measures to ensure the normal operation of the business.

<span id=".5LqL5Lu25oyH5qCH6aG5"></span>
## Event indicator item


|**Event name** |**Description** |
|---|---|
|**The migration task is abnormal** |During the data migration task, when an abnormality occurs in the task (excluding scenarios where you actively pause, terminate, or delete task), an alarm notification will be triggered. |
|**Incremental start of a migration task** |During the data migration task, an alert notification is triggered when an incremental migration is initiated. |
|**Migration task recovery** |If a task changes from migration failure to progress, an alarm notification will be triggered. |
|**Abnormal synchronization task** |During the data synchronization task, when an exception occurs in the task (excluding scenarios where you actively pause, terminate, or delete the task), an alarm notification is triggered. |
|**Incremental start of a synchronization task** |During the data synchronization task, when incremental synchronization starts, an alarm notification is triggered. |
|**Recovery of synchronization task** |If a task changes from synchronization failure to in progress, an alarm notification will be triggered. |
|**Subscription task is abnormal** |During the data subscription task, when an exception occurs in the task (excluding scenarios where you actively pause, terminate, or delete the task), an alarm notification is triggered. |
|**Recovery of subscription task** |When a task changes from subscription fails to progress, an alarm notification is triggered. |
|**Failed to delete the PG logical replication slot** |When a PostgreSQL database migration or synchronization task is terminated, the system detects whether there are logical replication slots in the source PostgreSQL database. If logical replication slots are detected or the detection fails due to network connection issues, an alarm notification will be triggered. |


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* Database Transfer Service (DTS) can monitor key metrics, trigger an alarm when the metrics reach a set threshold, and notify users to take action in a timely manner. For details about monitoring metrics, refer to [Monitoring metrics](https://docs.byteplus.com/en/docs/DTS/monitoring_metrics).

* For details on how to create event rules, see [Configuring event alarm](https://docs.byteplus.com/en/docs/DTS/Configuring_DTS_event_alarm).
