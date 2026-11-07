---
title: "How to migrate data from the third-party MySQL to Volcano Engine RDS for MySQL?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/How_to_migrate_data_from"
---

1. BytePlus's Data Transmission Service (DTS) supports migrating data from the third\-party MySQL to BytePlus RDS for MySQL using dedicated network lines or the public network.

2. Add the CIDR blocks of BytePlus DTS servers to the allowlist or security group of third parties' database by referencing [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

3. Determine the migration type. DTS supports full migration, incremental migration, and schema migration.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If performing incremental migration, the parameter configuration requirements for the source Binlogs are as follows.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Enable the Binlog function, and set the parameter <code>binlog_format</code> to <code>row</code> and <code>binlog_row_image</code> to <code>full</code>. Otherwise, pre\-check will report errors, and the data migration task can not be started successfully.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Binlogs must be retained for at least 24 hours, and a retention period of more than seven days is recommended. Otherwise, the DTS task may fail because it can not obtain the logs, potentially leading to data loss.   </div>
   

4. The essence of DTS data migration is to read data from the source and write it to the target. Therefore, before migration, carefully read the notes and limitations in the [source as public network MySQL migration to BytePlus MySQL](https://docs.byteplus.com/en/docs/DTS/migrating_to_byteplus_rds_for_mysql_publicmysql) or [source as MySQL connected over express network migration to BytePlus MySQL](https://docs.byteplus.com/en/docs/DTS/migrating_to_byteplus_rds_for_mysql_expressmysql) document, and try to ensure both the source and target meet the migration conditions.

5. Create a migration task by referencing [Migrating from MySQL connected over public network to BytePlus RDS for MySQL](https://docs.byteplus.com/en/docs/DTS/migrating_to_byteplus_rds_for_mysql_publicmysql) or [Migrating from MySQL connected over express network to BytePlus RDS for MySQL](https://docs.byteplus.com/en/docs/DTS/migrating_to_byteplus_rds_for_mysql_expressmysql) To verify data consistency between the source and target ends, you can configure a data verification task for the migration task.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Migration can be divided into full migration and incremental migration. After the full migration is completed, the incremental migration will continue until the data is consistent with the source end.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">During full migration, no downtime is required, and the source businesses remain unaffected.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Avoid performing DDL operations on the source database during incremental migration.   </div>
   

6. The duration of data migration depends on various factors such as data volume and network bandwidth. You can refer to the guide named [Adjusting the full migration rate](https://docs.byteplus.com/en/docs/DTS/adjusting_full_migration_rate) to improve migration speed and reduce the migration duration.

7. When the incremental migration delay reaches 0, start the data verification task to validate data consistency between the source and the destination.
