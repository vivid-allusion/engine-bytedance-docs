---
title: "PostgreSQL kernel"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/PostgreSQL_kernel"
---

This topic summarizes the issues and suggestions related to the core features of the RDS for PostgreSQL.

<span id=".UG9zdGdyZVNRTCBYSUQg5L2_55So55u45YWz5bu66K6u"></span>
#### PostgreSQL XID usage suggestions

As one of the PostgreSQL kernel resources, the transaction ID (XID) will be gradually consumed (wrap\-up) during the execution of the transaction. The kernel continuously recovers the consumed stock transaction IDs in the background through Vacuum to avoid exhaustion. When a single table is too large, the data space of a single instance is too large, or the instance is under high\-frequency insert, delete, and update operations for a long time, the speed of Vacuum recovering transaction IDs will be lower than the rate at which the instance consumes transaction IDs through insert, delete, and update. This will lead to transaction ID exhaustion and cause the instance to be unable to write. To avoid this situation, the recommendations are:


1. When a single table is larger than 1TB or the TPS of the entire instance is frequently greater than 1,000, you can design sharding according to the business situation.

2. Pay attention to the "Database maximum age XIDs" monitor item daily and configure related alarm policies. If an alarm is received, you can [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000179) or contact Volcano technical support for assistance in troubleshooting and resolution.
