---
title: "Backups"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Backups_faq"
---

<span id=".dmVkYi1teXNxbC3mgaLlpI3lupPooajmmK_lnKjlrp7kvovkuIrmlrDliJvlu7rkuIDkuKrlupPvvIzkuKTkuKrmlbDmja7lupPlkIzml7blrZjlnKjvvIzov5jmmK_kvJropobnm5bljp_mnaXnmoTlupPlkaLvvJ8="></span>
### Does NDB for MySQL recoverable database table create a new database alongside the original one, or overwrite the existing database?

Create a new database while preserving the original, with no impact on existing database tables in the instance. For details, refer to [Database & table recovery by backup sets](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Recovering_database_and_table_by_backup_set).

<span id="D1qra3VQ"></span>
### What tools are used to perform backups for NDB for MySQL?

The backup of NDB for MySQL is a physical backup, which is done using the xtrabackup tool.
