---
title: "How to resolve the \"PrecheckFailed_DiskSpaceInsufficient\" error when creating a ticket?"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/PrecheckFailed_DiskSpaceInsufficient"
---

**Issue Analysis**: The DBW ticket pre\-check failed due to insufficient disk space. During online DDL execution, a large amount of binlog is generated. Therefore, the disk space must meet the following condition when creating a ticket: (Total space \- Used space \- Binlog reserved space) \> (Table space × 1.2).

**Solution**:


* Check disk space and expand capacity. Consider configuring [Automatic operation and maintenance management](https://docs.byteplus.com/en/docs/DBW/automatic-expansion-management) to quickly respond and expand capacity when disk space is insufficient.

* Reduce binlog reserved space. Adjust the maximum storage usage rate to a lower value by [Modifying backup policy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_data_backup_policies).
