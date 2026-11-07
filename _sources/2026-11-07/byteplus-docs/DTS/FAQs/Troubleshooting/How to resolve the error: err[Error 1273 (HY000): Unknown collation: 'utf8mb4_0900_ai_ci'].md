---
title: "How to resolve the error: err[Error 1273 (HY000): Unknown collation: 'utf8mb4_0900_ai_ci']?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/what_should_I_do_if_an_authentication_failure_error_occurs"
---

If you encounter the error `err[Error 1273 (HY000): Unknown collation: 'utf8mb4_0900_ai_ci']`, follow the steps below to troubleshoot and resolve the issue.

<span id="ijc11WJR"></span>
### Reason

This error is due to incompatible database versions. This usually occurs when migrating or synchronizing data from MySQL 8.0 (source end) to MySQL 5.7 or lower (destination), because `utf8mb4_0900_ai_ci` is the default sort rule introduced in MySQL 8.0, which is unrecognized by the lower version destination database, causing table creation to fail.

<span id="SVmnHJUB"></span>
### Solutions


* #### Solution 1: Modify the destination collation (for scenarios where upgrading the destination database is not possible) <span id="KGth06Fl"></span>

   For destination instances running MySQL 5.7 or earlier, manually modify the table schema's collation to a format compatible with older versions, (e.g., `utf8mb4_general_ci`.

   1. **Check the source rule**:

      Run `SHOW CREATE TABLE d_live_server_paas.t_user_watch_record_2025_4_0;` on the source database to confirm whether the source table's collation is `utf8mb4_0900_ai_ci`.

   2. **Adjust destination structure**:

      * **Manual table creation**: Create the table structure manually in the destination database by replacing `utf8mb4_0900_ai_ci` with `utf8mb4_general_ci` in the SQL.

      * **Configure task**: Recreate data synchronization or migration task, selecting only **Full initialization**/**Full migration** and **Incremental synchronization**/**Incremental migration**.

* #### Solution 2: Upgrade the target database version (recommended) <span id="iGKHECBq"></span>

   Since target databases running MySQL 8.0 or higher natively support `utf8mb4_0900_ai_ci`, no configuration or code changes are required, ensuring optimal compatibility and data consistency. if the architecture allows, upgrading the target database to MySQL 8.0 or above is recommended.
