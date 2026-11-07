---
title: "Viewing event"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-event"
---

RDS for SQL Server supports viewing monitoring information for SQL Server events in the cloud\-monitored Event Center. This article describes the steps to view events for a RDS for SQL Server.

<span id="background-information"></span>
## Background information

The Cloud Monitoring Event Center provides the ability to monitor failures in cloud products. When an event occurs in a cloud product, information such as the event time, event source, event name, and event details are saved to the event center. By reviewing cloud product events, you can identify and resolve issues in a timely manner.

RDS for SQL Server supports monitoring the following four types of events in the Cloud Monitoring Event Center. When these events occur in an instance of RDS for SQL Server, the Cloud Monitoring Event Center will record and display these events. Events are saved for 30 days by default.


|event type |event |event name |
|---|---|---|
|Exception |rds_mssql:Exception:InstanceBackupFailure |instance backup failed |
|Exception |rds_mssql:Exception:InstanceFailover |Active and standby switching (failover) |
|Exception |rds_mssql:Exception:InstanceStatusAbnormal |instance state exception |
|Maintenance |rds_mssql:Maintenance:InstanceSwitchover |Active and standby switching (task switching) |


<span id="operation-steps"></span>
## Operation steps


1. Log in to [the cloud monitoring console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left navigation bar, select **Event Center** \> **Cloud Product Events** .

3. On the **Cloud Product Events** page, select **RDS for SQL Server** in the Cloud Product drop\-down list.

   * Support setting time period and event type to filter event information.

      * The default query is for event information within the last hour.

      * The specified time period is accurate to the minute level, and the number of seconds defaults to 00.

   * In the **Actions** column for a specific event, click **Details** to view the details for that event. The information is displayed in JSON format.


<span id="next-steps"></span>
## Next steps

[Create event rules](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule)

<span id="related-documentation"></span>
## Related Documentation

[View cloud product events](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-cloud-service-events)
