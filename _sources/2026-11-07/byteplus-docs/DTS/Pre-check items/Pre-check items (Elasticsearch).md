---
title: "Pre-check items (Elasticsearch)"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/pre-check-items-elasticsearch"
---

Database Transmission Service (DTS) performs various checks on databases before creating or configuring migration or synchronization tasks for Elasticsearch. This topic introduces the details of check items.


|**Item** |**Database type** |**Check scope** |**Level** |**Check content** |**Remarks** |
|---|---|---|---|---|---|
|Data connectivity |Target database |All synchronization |Error |Check if connecting to the target database Elasticsearch succeeds. |None |
|Elasticsearch instance version |Target database |All synchronization |Error |Check whether the Elasticsearch instance version is greater than or equal to 6.0. If it is less than 6.0, the pre\-check fails. |None |
|Target database index |Target database |All synchronization |Warn |Check whether the indexes already exist in the target database Elasticsearch. |None |
|Elasticsearch health status |Target database |All synchronization |Error |Check the health status of the target database Elasticsearch. If the state is Red, pre\-check fails. |None |
