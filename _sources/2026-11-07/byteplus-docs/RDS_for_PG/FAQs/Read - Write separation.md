---
title: "Read/Write separation"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/read-write_splitting"
---

This topic summarizes frequently asked questions about RDS for PostgreSQL read/write splitting.

**Why does an error occur when choosing read/write separation?** 

Before enabling read/write separation, confirm a read\-only node is created. If you encounter errors with read/write separation, troubleshoot using the following suggestions:


* Confirm that the PostgreSQL instance is in the **Running** state.

* Confirm that you've created a read\-only node for the instance and the instance is in the **Running** status.


If errors with read/write separation persist after troubleshooting, you can [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support.

**What happens when read/write separation is enabled?** 

After read/write splitting is enabled, the PostgreSQL instance can be accessed by the read/write splitting address, and requests can be automatically forwarded to the read\-only nodes. If a transaction contains both read and write requests, they are sent to the primary node for execution. For more information, refer to [Enabling or disabling read/write separation](https://docs.byteplus.com/en/docs/RDS_for_PG/enabling_or_disabling_read-write_splitting).

**What is global read\-only?** 

Once global read\-only is enabled, you can set the PostgreSQL instance to read\-only, so that write requests will not be forwarded to the instance.

**Does enabling global read\-only override account privileges?** 

After global read\-only is enabled, only read permission is available.
