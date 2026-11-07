---
title: "How to set the definer of a database object after the MySQL structural migration or structure initialization is complete?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/How_to_set_the_DEFINER_of_database_objects_during_MySQL_schema_migration_or_initialization"
---

When exporting the structure of MySQL database objects (such as views, stored structures, functions, etc.), DTS will automatically change the value of `SQL SECURITY` (security verification method) in objects to be migrated, such as views, stored procedures, triggers, and functions from `DEFINER` to `INVOKER`, and set the `DEFINER` to the target database account used in the migration task.

After the migration is complete, to ensure the security of the database objects, it is recommended that you manually modify the value of `SQL SECURITY` back to `DEFINER` and set the `DEFINER` to the account actually used by the business.
