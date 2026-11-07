---
title: "Viewing an event"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Viewing_an_event"
---

RDS for PostgreSQL supports viewing the monitoring information of PostgreSQL instances in the event center of Cloud monitor (VCM). This topic describes the procedure for viewing RDS for PostgreSQL events in the Cloud monitor event center.

<span id="5Of4Bpqb"></span>
## **Background information**

The Cloud Monitor event center provides fault monitoring for cloud products. When an event occurs for a cloud product, information such as the event time, event source, event name, and event details are saved to the event center. By viewing cloud product events, you can identify and resolve problems in a timely manner. RDS for PostgreSQL supports monitoring the following events in the Cloud monitor event center. When these events occur on an RDS for PostgreSQL instance, the Cloud monitor event center records and displays them. Events are saved for 30 days by default.


|Event type |Event |Event |
|---|---|---|
|Maintenance |rds_postgresql:Maintenance:InstanceSwitchover |Switching between primary and secondary nodes (task switching) |
|Exception |rds_postgresql:Exception:InstanceFailover |Switching between primary and secondary nodes (Failover) |
|Exception |rds_postgresql:Exception:InstanceBackupFailure |Instance backup failed |
|Exception |rds_postgresql:Exception:InstanceStatusAbnormal |Exception of instance state |


<span id="KFO1KSSa"></span>
## **Procedure**


1. Log on to the [Cloud Monitor console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left navigation bar, select **Event center**\>**Cloud product events**.

3. On the **Cloud product events** page, select **RDS for PostgreSQL** from the cloud product dropdown list.

   * You can filter events by specifying a time range and event type.

      * By default, events from the last hour are displayed.

      * The specified time range is accurate to the minute, with the seconds value defaulting to 00.

   * In the **Actions** column for a specific event, click **Details** to view its details. The information is displayed in JSON format.


<span id="ECCIzJvX"></span>
## Next steps

[Creating event policy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule)

<span id="cZXWz5gY"></span>
## **Related document**

[Viewing cloud product events](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-cloud-service-events)
