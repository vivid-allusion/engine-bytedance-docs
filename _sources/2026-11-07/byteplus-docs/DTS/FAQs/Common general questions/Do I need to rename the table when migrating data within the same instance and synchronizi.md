---
title: "Do I need to rename the table when migrating data within the same instance and synchronizing data from table A to the empty table B in the database?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/do_I_need_to_rename_the_table_"
---

Yes. You need to modify the name of the empty database table B when creating a migration task configuration data migration object. Otherwise, the source database will also be refreshed.
