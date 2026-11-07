---
title: "About replication slots"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/about_replication_slot"
---

Replication slot is a unique mechanism of PostgreSQL database, which is used to avoid data loss or duplicate replication in streaming replication and improve the reliability of data replication.


* Types of replication slots

   Replication slots are divided into physical replication slots and logical replication slots according to their types.Replication slots are divided into physical replication slots and logical replication slots based on their type.

   * Physical replication slots are generally used in conjunction with streaming replication to prevent WAL logs required by the standby database from being deleted in the primary database, ensuring that the primary database will not delete WAL logs before all standby databases receive WAL logs. The primary database will confirm the WAL logs that are no longer needed based on the information returned by the standby database, and then clean them up.

   * Logical replication slot is a WAL parsing function provided by PostgreSQL itself, which is used to record and switch transactions to ensure that transactions are not lost or resent.

* Status of replication slot

   Replication slots have two states: ACTIVE and INACTIVE. When there are too many inactive logical replication slots due to not being cleaned up in time, WAL logs will continue to accumulate, occupying a large amount of storage space, and may even fill up the disk, causing the instance to be locked and unable to write data, thus affecting the business. RDS for PostgreSQL supports deleting inactive replication slots through the console or Open API to reduce the disk space occupied by WAL logs. For more details on cleaning up replication slots, see [Deleting replication slots](https://docs.byteplus.com/en/docs/RDS_for_PG/delete_replication_slot). RDS for PostgreSQL supports viewing replication slots under instances via the console or Open API. For more details on viewing instance replication slots, refer to [Viewing the replication slot list](https://docs.byteplus.com/en/docs/RDS_for_PG/view_replication_slot_list).
