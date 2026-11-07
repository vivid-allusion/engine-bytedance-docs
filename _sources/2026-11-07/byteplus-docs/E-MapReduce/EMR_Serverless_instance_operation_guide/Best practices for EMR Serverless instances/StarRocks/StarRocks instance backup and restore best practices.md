---
title: "StarRocks instance backup and restore best practices"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/StarRocks_instance_backup_and_restore_best_practices"
---

<span id="d53fa054"></span>
## Back up data

StarRocks supports full backups at the granularity of databases, tables, or partitions.

When a table contains a large amount of data, it is recommended to perform backups by partition to reduce the probability of failure. To perform regular data backups, it is recommended to set a [dynamic partition](https://docs.starrocks.io/zh/docs/table_design/data_distribution/dynamic_partitioning/) policy when creating tables, so that only newly added partitions need to be backed up periodically during later maintenance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Backup and restore functionality is currently unavailable for StarRocks with storage and compute separation.</div>


<span id="206dee84"></span>
### Create a repository

A repository is used to store backup files in a remote storage system. Before backing up data, you need to create a repository in StarRocks based on the path of the remote storage system. You can create multiple repositories within the same cluster. For detailed usage, refer to [CREATE REPOSITORY](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/backup_restore/CREATE_REPOSITORY/).


* Create a repository in an HDFS cluster.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The following example is for creating the repository <code>test_repo</code> in an Apache™ Hadoop® cluster.   </div>
   

   ```SQL
   CREATE REPOSITORY test_repo
   WITH BROKER
   ON LOCATION "hdfs://<hdfs_host>:<hdfs_port>/repo_dir/backup"
   PROPERTIES(
       "username" = "<hdfs_username>",
       "password" = "<hdfs_password>"
   );
   ```
   

* Create a repository in TOS.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can use IAM user credentials (Access Key and Secret Key) as security credentials to access TOS.   </div>
   

   **Example**

   Use IAM user credentials as security credentials to create the repository `test_repo` in the `bucket_tos` TOS bucket.

   ```SQL
   CREATE REPOSITORY test_repo
   WITH BROKER
   ON LOCATION ""s3a://bucket_tos/backu"
   PROPERTIES(
       "aws.s3.region"="cn-beijing",
       "aws.s3.endpoint" = "tos-cn-beijing.ivolces.com",
       "aws.s3.access_key" = "XXXXXXXXXXXXXXXXX",
       "aws.s3.secret_key" = "yyyyyyyyyyyyyyyyyyyyyyyy"
       
   );
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For the regions and access domain names (S3 Endpoint) supported by VolcEngine TOS, please refer to <a href="https://www.volcengine.com/docs/6349/107356#%E5%9C%B0%E5%9F%9F%E5%8F%8A%E8%AE%BF%E9%97%AE%E5%9F%9F%E5%90%8D%E8%AF%B4%E6%98%8E">Region and Access Domain Name</a>.   </div>
   

After the repository is created, you can use [SHOW REPOSITORIES](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/backup_restore/SHOW_REPOSITORIES/) to view the repositories that have been created. After completing backup and restore operations, you can use the [DROP REPOSITORY](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/backup_restore/DROP_REPOSITORY/) statement to delete the repository in StarRocks. However, currently, you cannot directly delete snapshot data stored in the remote storage system via StarRocks. You need to manually delete the snapshot path in the remote storage system.

<span id="8ff347b4"></span>
### Back up data snapshots

After creating a data repository, you can use the [BACKUP](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/backup_restore/BACKUP/) command to create a data snapshot and back it up to the remote repository.

**Example**

Create the data snapshot `sr_member_backup` for the table `sr_member` in the database `sr_hub` and back it up to the repository `test_repo`.

```SQL
BACKUP SNAPSHOT sr_hub.sr_member_backup
TO test_repo
ON (sr_member);
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">StarRocks supports backup and restore operations at the following granularities:</div>



* <div data-tips="true" data-tips-type="tip">Partition level: You need to specify the partition name in the ON clause in the following format <code>ON (<table_name> PARTITION (<partition_name>, ...))</code>.</div>


* <div data-tips="true" data-tips-type="tip">Table level: You need to specify the table name in the ON clause <code>ON (<table_name>)</code>.</div>


* <div data-tips="true" data-tips-type="tip">Database level: You do not need to specify the ON clause. This will back up or restore the entire database.</div>



Data backup is an asynchronous operation. You can use the [SHOW BACKUP](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/backup_restore/SHOW_BACKUP/) statement to view the status of backup jobs, or use the [CANCEL BACKUP](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/backup_restore/CANCEL_BACKUP/) statement to cancel backup jobs.

<span id="b5a78e67"></span>
## Restore or migrate data

You can restore data snapshots backed up to a remote repository to the current or another StarRocks cluster to complete data recovery or migration.

<span id="efb678c3"></span>
### View database snapshots

Before starting recovery or migration, you can use [SHOW SNAPSHOT](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/backup_restore/SHOW_SNAPSHOT/) to view information about data snapshots in a specific repository.

**Example**

View data snapshot information in the `test_repo` repository.

```Plain
mysql> SHOW SNAPSHOT ON test_repo;
+------------------+-------------------------+--------+
| Snapshot         | Timestamp               | Status |
+------------------+-------------------------+--------+
| sr_member_backup | 2023-02-07-14-45-53-143 | OK     |
+------------------+-------------------------+--------+
1 row in set (1.16 sec)
```


<span id="2b47f214"></span>
### Restore data snapshots

Use the [RESTORE](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/backup_restore/RESTORE/) statement to restore data snapshots from a remote repository to the current or another StarRocks cluster to recover or migrate data.

**Example**

Restore the data snapshot `sr_member_backup` from the `test_repo` repository as the table `sr_member`, restoring only one data replica.

```SQL
RESTORE SNAPSHOT sr_hub.sr_member_backup
FROM test_repo
ON (sr_member)
PROPERTIES (
    "backup_timestamp"="2023-02-07-14-45-53-143",
    "replication_num" = "1"
);
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">StarRocks supports backup and restore operations at the following granularities:</div>



* <div data-tips="true" data-tips-type="tip">Partition level: You need to specify the partition name in the ON clause in the following format <code>ON (<table_name> PARTITION (<partition_name>, ...))</code>.</div>


* <div data-tips="true" data-tips-type="tip">Table level: You need to specify the table name in the ON clause <code>ON (<table_name>)</code>.</div>


* <div data-tips="true" data-tips-type="tip">Database level: You do not need to specify the ON clause. This will back up or restore the entire database.</div>



Data restoration is an asynchronous operation. You can use the [SHOW RESTORE](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/backup_restore/SHOW_RESTORE/) statement to check the status of the restore job, or use the [CANCEL RESTORE](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/backup_restore/CANCEL_RESTORE/) statement to cancel the restore job.

<span id="8368bec3"></span>
## Configure related parameters

You can accelerate backup or restore jobs by modifying the following configuration items.


|Configuration items |Note |
|---|---|
|make_snapshot_worker_count |The maximum number of threads for snapshot tasks on BE nodes, used for backup jobs. Default value: 5. Increasing the value of this configuration item can increase the parallelism of snapshot tasks. |
|release_snapshot_worker_count |The maximum number of threads for releasing snapshot tasks on BE nodes, used for exception cleanup in backup jobs. Default value: 5. Increasing the value of this configuration item can increase the parallelism of releasing snapshot tasks. |
|upload_worker_count |The maximum number of threads for upload tasks on BE nodes, used for backup jobs. Default value: 0. 0 means the number of threads is set to the number of CPU cores on the machine where the BE node is located. Increasing the value of this configuration item can increase the parallelism of upload tasks. |
|download_worker_count |The maximum number of threads for download tasks on BE nodes, used for restoring jobs. Default value: 10. When the effective value is 0, the number of threads is set to the number of CPU cores on the machine where the BE node is located. Increasing the value of this configuration item can improve the parallelism of download tasks. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If your actual configuration parameters differ from the descriptions in the table above, please contact Volcano Engine technical support by <a href="https://console.volcengine.com/workorder/create/">submitting a ticket</a>.</div>


<span id="d8d95855"></span>
## Backup and restore of materialized views

During the backup or restore of table data, StarRocks automatically backs up or restores the [synchronous materialized views](https://docs.starrocks.io/zh/docs/using_starrocks/Materialized_view-single_table/) contained in the table.

Starting from StarRocks version 3.2.3, when performing backup and restore operations on a database, you can also back up and restore [asynchronous materialized views](https://docs.starrocks.io/zh/docs/using_starrocks/async_mv/Materialized_view/) in the database.

During database backup and restore, StarRocks performs the following operations.


* **BACKUP**

1. Traverse the database to collect information on all tables and asynchronous materialized views.

2. Adjust the order of tables in the backup and restore queue to ensure that the base tables of materialized views are placed before the materialized views:

   * If the base table exists in the current database, StarRocks adds the table to the queue.

   * If the base table does not exist in the current database, StarRocks prints a warning log and continues the backup operation without blocking the process.

3. Execute backup tasks in the order of the queue.

* **RESTORE**

1. Restore tables and materialized views in the order of the backup and restore queue.

2. Rebuild the dependency relationship between materialized views and their base tables, and resubmit the refresh task scheduling.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">During the backup and restore operations for materialized views, the backup and restore process will not stop or be interrupted regardless of any errors encountered. You can use the <a href="https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/backup_restore/SHOW_BACKUP/">SHOW BACKUP</a> statement to view the backup job status, and use the <a href="https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/backup_restore/SHOW_RESTORE/">SHOW RESTORE</a> statement to view the restore job status.</div>


After the operation is complete, you can use [SHOW MATERIALIZED VIEWS](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/materialized_view/SHOW_MATERIALIZED_VIEW/) to check the status of the materialized views.


* If a materialized view is in the Active state, it can be used directly.

* If a materialized view is in the Inactive state, it may be because its base table has not yet been restored. After restoring all base tables, you can use [ALTER MATERIALIZED VIEW](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/materialized_view/ALTER_MATERIALIZED_VIEW/) to reactivate the materialized view.


<span id="95d934a3"></span>
## important notes


* Different permissions are required to perform global, database\-level, table\-level, and partition\-level backup and restore operations. For more details, please refer to [基于使用场景创建自定义角色](https://docs.byteplus.com/docs/E-MapReduce/109139#%E5%9F%BA%E4%BA%8E%E4%BD%BF%E7%94%A8%E5%9C%BA%E6%99%AF%E5%88%9B%E5%BB%BA%E8%87%AA%E5%AE%9A%E4%B9%89%E8%A7%92%E8%89%B2).

* Only one backup job or one restore job can be executed at a time within a single database. Otherwise, StarRocks will return an error message.

* Because backup and restore operations consume certain system resources, it is recommended to perform these operations during off\-peak periods for cluster workloads.

* Currently, StarRocks does not support using compression algorithms when backing up data.

* Because data backup is completed in the form of snapshots, any data imported after the current snapshot is generated will not be backed up. Therefore, any data imported during the period from snapshot generation to completion of the restore (migration) job must be re\-imported into the cluster. It is recommended to import data in parallel to both the old and new clusters for a period after migration is completed. After verifying the correctness of the data and workloads, migrate the workloads to the new cluster.

* The table being restored cannot be operated on until the restore job is completed.

* Primary Key tables cannot be restored to StarRocks clusters running versions earlier than v2.5.

* There is no need to create the tables to be restored in the new cluster before the restore job. The restore job will automatically create the table.

* If the table being restored has the same name as an existing table, StarRocks will first identify the Schema of the existing table. If the Schema is the same, StarRocks will overwrite the existing table. If the Schema is different, the restore job will fail. You can use the `AS` keyword to rename the table being restored, or delete the existing table and then initiate the restore job again.

* If the restore job is an overwrite operation (restoring data to an existing table or partition), then starting from the COMMIT phase of the restore job, the overwritten data in the current cluster may no longer be recoverable. If the restore job fails or is canceled at this point, previous data may be corrupted and become inaccessible. In this case, you can only execute the restore operation again and wait for the job to complete. Therefore, we recommend that you do not use the overwrite method to restore data unless it is necessary and you have confirmed that the current data is no longer in use. The overwrite operation checks whether the metadata of the snapshot and the existing table or partition are identical, including information such as Schema and Rollup. If they differ, the restore operation cannot be performed.

* Currently, StarRocks does not support backup and restore for logical views.

* Currently, StarRocks does not support backup and restore for user, permission, and resource group configuration data.

* StarRocks does not support backup and restore for Colocate Join relationships between tables.
