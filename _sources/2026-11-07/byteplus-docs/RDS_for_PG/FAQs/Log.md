---
title: "Log"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/logs"
---

This topic summarizes frequently asked questions about RDS for PostgreSQL logs.

<span id=".5oWi5pel5b-X5piO57uG5Y-v5L-d55WZ5aSa5LmF77yf"></span>
#### **How long can I store the slow log details?** 

Slow log details can be stored for 30 days.

<span id=".6buY6K6k6LaF6L-H5aSa5bCR5pe26Ze05bCx6KKr5a6a5LmJ5Li65oWi5pel5b-X77yf6IO95ZCm6Ieq5a6a5LmJ5oWi5pel5b-X55qE5pe26Ze077yf"></span>
#### **How long can I store the slow log details? Can I customize the slow log time?** 

By default, SQL statements exceeding 1 second are defined as a slow log; you can modify the `long_query_time` parameter in the parameter setting to customize the slow log time. For details, refer to [Modify parameters](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_parameters).

<span id=".5Li75aSH5YiH5o2i55qE5pel5b-X5Y-v5L-d55WZ5aSa5LmF77yf"></span>
#### **How long can primary/secondary switchover logs be stored?** 

Primary/secondary switchover logs can be stored for 30 days.

<span id=".5YiH5o2i5Li76IqC54K56ZyA6KaB5rOo5oSP5ZOq5Lqb5LqL6aG577yf"></span>
#### **What are the precautions for switching primary node?** 


* Please make sure that your applications have automatic reconnection mechanisms.

* If a read\-only node is mounted under the instance, the data of the read\-only node can be delayed for several minutes after primary/secondary switchover, because it must rebuild the replication link and synchronize the incremental data.

* Switchover can be completed within 5 seconds without a delay in primary/secondary replication.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Note for more details on primary/secondary switchover, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/switching_primary_nodes">Switching primary node</a>.</div>
