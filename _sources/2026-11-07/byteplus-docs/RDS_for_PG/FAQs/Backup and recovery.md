---
title: "Backup and recovery"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/faqs_of_backup_and_recovery"
---

This topic summarizes frequently asked questions about RDS for PostgreSQL backup and recovery.

<span id=".5Li65LuA5LmI5peg5rOV6L-b6KGM5aSH5Lu95pON5L2c77yf"></span>
#### **Why can't I perform a backup?** 

If you are unable to perform a backup operation, check the following:


* Confirm whether the PostgreSQL instance is in **Running** state.

* Confirm that no DDL operations are ongoing during the backup period to avoid table locks that may cause a backup failure.


If the problem persists, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support.

<span id=".5aSH5Lu957G75Z6L5piv5ZCm5pSv5oyB6YC76L6R5aSH5Lu977yf"></span>
#### **Does the backup type support logical backup?** 

Currently, only physical backups are supported; logical backups are not supported.

<span id=".5Y-v5Lul5a-55Y-q6K-76IqC54K56L-b6KGM5aSH5Lu95ZCX77yf"></span>
#### **Is it possible to back up the read\-only node?** 

Because the primary node already has backups, read\-only nodes currently do not support backup settings or manual backup initiation.
