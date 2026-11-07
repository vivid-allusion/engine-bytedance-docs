---
title: "Pre-check items (Kafka & RocketMQ)"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_kafka"
---

Database Transmission Service (DTS) performs various checks on the database before subscribing messages to its own middleware Kafka or RocketMQ. This topic introduces the details of check items.

<span id="YEcp6Ztm"></span>
# Kafka subscription


|**Item** |**Database type** |**Check scope** |**Level** |**Check content** |**Remarks** |
|---|---|---|---|---|---|
|Environment detection. |Target database |Data subscription |Warning |Environment detection. |None |
|Kafka ACL permission detection |Target database |Data subscription |Warning |Check whether the specified user has write permission for the given Topic. |None |
|Source end system time check |Source database |Data subscription |Warning |check whether the system time at the source end differs from the standard time by more than 1 minute |Check the actual time when data changes occur in the source database. |
|RocketMQ ACL check |Target database |Data subscription |Warning |Check whether the specified user has write permission for the given Topic. |None |


<span id="TfkEUeyn"></span>
# RocketMQ subscription


|**Item** |**Database type** |**Check scope** |**Level** |**Check content** |**Remarks** |
|---|---|---|---|---|---|
|Environment detection. |Target database |Data subscription |Warning |Environment detection. |None |
|PreCheck_SolutionPGCheckMsLvlLatencyAvailability_Name |Target database |Data subscription |Warning |PreCheck_SolutionPGCheckMsLvlLatencyAvailability_Desc |Check whether the source end PostgreSQL database meets the basic conditions to support millisecond\-level low latency data synchronization (CDC). |
|RocketMQ ACL check |Target database |Data subscription |Warning |Check whether the specified user has write permission for the given Topic. |None |
