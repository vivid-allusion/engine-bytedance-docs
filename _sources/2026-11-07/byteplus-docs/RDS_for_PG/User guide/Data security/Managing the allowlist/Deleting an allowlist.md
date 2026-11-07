---
title: "Deleting an allowlist"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/deleting_an_allowlist"
---

This topic describes the procedure for deleting an allowlist.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Existing allowlist.

* Confirmed that the IP addresses or IP address segments in the allowlist to be deleted no longer need access to the instance, and the allowlist is unbound from the instance.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Deleting allowlists associated to instances is not supported.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper left corner of the top menu bar, select the region to which the allowlist belongs.

3. Click **Allowlists** on the left navigation bar.

4. Click **Actions** in the target allowlist’s  **...**  column \> **Delete**, then click **OK** in the popped\-up dialog.


<span id=".55u45YWzIEFQSQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DeleteAllowList](https://docs.byteplus.com/en/docs/RDS_for_PG/deleteallowlist) |Call DeleteAllowList API to delete an allowlist. |
