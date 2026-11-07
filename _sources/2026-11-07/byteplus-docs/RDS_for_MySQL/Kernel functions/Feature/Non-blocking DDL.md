---
title: "Non-blocking DDL"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Non-blocking_DDL"
---

This topic describes the non\-blocking DDL feature of RDS for MySQL.

## Supported version

MySQL 8.0, and the kernel minor version of MySQL 8.0.43_20260815 and above.

> **tip**

> You can view the kernel minor version of an instance by [Viewing instance information](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details). If the kernel minor version of your instance is not within the supported kernel minor version range, you can [Manually upgrading the instance kernel minor version](https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version).

## Background

In MySQL, DDL operations must acquire the MDL lock on the target table to commit metadata changes and ensure metadata consistency. MDL locks are incompatible with locks of any other type. If the DDL thread enters the pending state because it cannot acquire the lock immediately, all subsequent accesses to the target table will be blocked, which may cause business system failures and unavailability.

## Feature description

After non\-blocking DDL is enabled, for DDL threads that need to upgrade to an MDL lock, the system attempts to acquire the lock through intermittent retries while waiting for the MDL lock and does not block continuously. Between two attempts to acquire the lock, business DDL operations can still continue to execute.

### Limitation

* Enabling the non\-blocking DDL feature reduces the priority of DDL. Therefore, the probability of DDL failures caused by the inability to acquire the MDL lock increases.

* Only ALTER TABLE, CREATE INDEX and DROP INDEX operations are currently supported.

* RENAME TABLE cannot be executed directly.

* It does not take effect in the slave_thread scenario.

## Instructions

You can enable and adjust the non\-blocking DDL feature through the loose_rds_nonblock_ddl_retry_interval and loose_rds_nonblock_ddl_lock_wait_timeout parameters.

|**Parameter name** |**Default value** |**Whether an instance restart is required for the change to take effect** |**Value range** |**Scope** |**Parameter description** |
|---|---|---|---|---|---|
|loose_rds_nonblock_ddl_retry_interval |0 |No |0~31536000 |GLOBAL / SESSION |The time interval for the DDL thread to retry when acquiring the MDL lock times out. The default value is 0, which means the non\-blocking DDL feature does not take effect. The unit is seconds. |
|loose_rds_nonblock_ddl_lock_wait_timeout |1 |No |1~31536000 |GLOBAL / SESSION |The timeout period for the DDL thread to intermittently acquire the MDL lock. The default value is 1, and the unit is second. |

## Performance test

### Test Environment

* Instance specification: RDS for MySQL 4C8G.

* Instance version: MySQL 8.0.

### Test steps

1. Create tables and insert data through sysbench.

```Shell
sysbench oltp_read_write \
  --db-ps-mode=auto \
  --percentile=95 \
  --mysql-socket=/var/run/mysqld/mysqld.sock \
  --mysql-user=user \
  --mysql-password=password \
  --mysql-db=test_demo \
  --tables=1 \
  --table-size=10000 \
  --threads=4 \
  prepare
```

2. Start the sysbench stress test to simulate online business.

```Shell
sysbench oltp_read_write \
  --db-ps-mode=auto \
  --percentile=95 \
  --mysql-socket=/var/run/mysqld/mysqld.sock \
  --mysql-user=user \
  --mysql-password=password \
  --mysql-db=test_demo \
  --tables=1 \
  --table-size=10000 \
  --threads=4 \
  --report-interval=1 \
  --time=100 \
  run
```

3. Start session 1 and open a long\-running transaction on the target table, to block subsequent DDL operations on this table.

```SQL
SELECT SLEEP(60) FROM test_demo LIMIT 1; 
```

4. Start another session 2 and execute the DDL operation with the non\-blocking DDL feature disabled.

```SQL
ALTER TABLE test_demo ENGINE = InnoDB;
```

5. Enable the non\-blocking DDL feature, and set the loose_rds_nonblock_ddl_retry_interval parameter to 6 and the loose_rds_nonblock_ddl_lock_wait_timeout parameter to 1. Execute the same DDL operation as in the previous step.

```SQL
ALTER TABLE test_demo ENGINE = InnoDB;
```

### **The test results are as follows.**

The following conclusions can be drawn from the comparison figure below:

* When the non\-blocking DDL feature is **disabled**, the DDL thread cannot acquire the MDL lock, and the session is fully blocked.

* When the non\-blocking DDL feature is **enabled**, the DDL thread can acquire the MDL lock intermittently, and the session is not fully blocked.

![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261016083311-1536567722422.png)

![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261016083324-293821145439.png)
