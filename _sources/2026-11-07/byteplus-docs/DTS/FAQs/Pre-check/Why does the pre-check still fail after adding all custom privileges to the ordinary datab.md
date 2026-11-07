---
title: "Why does the pre-check still fail after adding all custom privileges to the ordinary database account?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/why_does_pre-check_fail_after_I_added_all_custom_permissions_to_general_account"
---

When using Database Transmission Service (DTS) for data migration or synchronization, if the database account is an ordinary account, the pre\-check may fail even if the account has all custom privileges.

**Reason:** 

If the database account of the target database is an ordinary account and there is no database to be migrated or synchronized in the target database, the pre\-check will report an error during the migration or synchronization process because the ordinary account does not have the permission to automatically create the same database in the target database.

**Solution:** 

In this case, you need to manually create the same database in the target database before creating a data migration or synchronization task. Otherwise, the pre\-check will fail.

Refer to [Account privileges Instructions ](https://docs.byteplus.com/en/docs/RDS_for_MySQL/account_permissions1) for details about high\-privilege accounts and ordinary accounts in the instance.
