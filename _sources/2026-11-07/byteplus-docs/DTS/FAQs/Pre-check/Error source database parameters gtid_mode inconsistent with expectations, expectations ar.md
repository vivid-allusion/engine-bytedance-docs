---
title: "Error source database parameters gtid_mode inconsistent with expectations, expectations are: ON, but set to: OFF, how to do?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Error_source_database_parameters_gtid_mode"
---

## Possible causes

Since GTID is a new feature introduced in MySQL 5.6, this problem exists in MySQL 5.6 and later versions. DTS only supports `gtid_mode` values of `ON` and `OFF`, so it is recommended to set `gtid_mode` to `ON`, otherwise the DTS task will report an error when creating a pre\-check.

GTID (Global Transaction Identifier) is a mechanism introduced in MySQL 5.6 and later versions to identify and coordinate transactions. It assigns a globally unique identifier to each transaction, making it easier and more reliable to manage} and track primary/secondary synchronization in a GTID\-based replication environment.

## Solutions

When you encounter this error during the pre\-check, you need to modify the value of the parameter `gtid_mode` to `ON`.

To ensure system consistency and prevent potential errors, the `gtid_mode` parameter provides values including `OFF`, `OFF_PERMISSIVE`, `ON_PERMISSIVE`, and `ON`:

* `OFF`: Closes the GTID mode, that is, GTID is not used for transaction management.

* `OFF_PERMISSIVE`: The system accepts both transactions without GTID and transactions with GTID, but does not allow transactions with only GTID. This is a transitional state that allows a gradual transition from closing the GTID mode to opening the GTID mode.

* `On_permissive`: the system generates a GTID and attaches it to a new transaction, but still accepts transactions without a GTID. This is also a transitional state that allows a gradual transition from closing the GTID mode to enabling the GTID mode.

* `On`: fully enables GTID `mode`, only accepts transactions with GTIDs, and rejects transactions without GTIDs.

Note that, to modify the `gtid_mode` parameter from `off` to `on`, you need to modify it step by step in sequence. The value levels of the `gtid_mode` parameter are `off`<\-\>`off_permissive`<\-\>`on_permissive`<\-\>`on` in order. The detailed operations are as follows:

1. Log in to the source database instance.

2. Modify the parameter value of `gtid_mode`.

   1. On both sides of the primary\-secondary copy structure, modify the `gtid_mode` parameter value from `off` to `off_permissive`:

      For versions prior to MySQL 5.7.6, you need to modify the `my.cnf` configuration file and restart the `database` to take effect. for MySQL 5.7.6 and later versions, `modify` it through global naming without restarting the `database`, but you need to reset all business connections.

      ```sql
      SET GLOBAL gtid_mode = OFF_PERMISSIVE;
      ```

   2. On both sides of the primary\-secondary copy structure, modify the `gtid_mode` parameter value from `OFF_PERMISSIVE` to `ON_PERMISSIVE`:

      ```sql
      SET GLOBAL gtid_mode = ON_PERMISSIVE;
      ```

   3. Run the following command on each instance node to check whether the anonymous transaction has been consumed:

      ```sql
      SHOW VARIABLES LIKE '%ONGOING_ANONYMOUS_TRANSACTION_COUNT%';
      ```

      The expected execution result is as follows:

      > **tip**

      > If the return result is 0, it means that the anonymous transaction has been consumed.

      ```sql
      mysql> SHOW VARIABLES LIKE '%ONGOING_ANONYMOUS_TRANSACTION_COUNT%';
      +-------------------------------------+-------+
      | Variable_name                       | Value |
      +-------------------------------------+-------+
      | Ongoing_anonymous_transaction_count | 0     |
      +-------------------------------------+-------+
      1 row in set (0.00 sec)
      ```

   4. On both sides of the primary\-secondary copy structure, `modify` the gtid_mode parameter value from `ON_PERMISSIVE` to `ON`:

      ```sql
      SET GLOBAL gtid_mode = ON;
      ```

   5. Add the following content to the `my.cnf` file, and then restart the `database` for the initial value to take effect:

      > **tip**

      > The default path of the my.cnf configuration file is `/etc/my.cnf`, and the actual situation on site shall prevail.

      ```sql
      gtid_mode = on
      enforce_gtid_consistency = on
      ```

   6. Re\-run the pre\-check task.
