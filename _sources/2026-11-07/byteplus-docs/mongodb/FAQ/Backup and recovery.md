---
title: "Backup and recovery"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/Backup_and_recovery"
---

This topic summarizes backup and recovery FAQs for Document Database for MongoDB.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">A recovery task creates a new instance and does not overwrite the original instance. The original instance can continue to provide read and write services normally during recovery and is not affected.</div>


* <div data-tips="true" data-tips-type="default">Time\-series collections currently do not support data recovery or database and table rollback. If the original instance contains time\-series data, data inconsistency may occur after recovery.</div>



<span id="7XfrFZ7O"></span>
## In the backup list, the "Restore to a new instance" button is grayed out and cannot be clicked. What should I do?

Based on your instance architecture type, refer to the table below to identify the cause and resolve the issue. For more information about instance architecture, refer to [Product architecture](https://docs.byteplus.com/en/docs/mongodb/about-mongodb?lang=en#.5Lqn5ZOB5p625p6E).


|**Instance architecture type** |**Reason and solution** |
|---|---|
|Sharding cluster instance |This architecture currently does not support recovery from backup files. Instead, use recovery by point in time (i.e., rollback) **.**  For detailed steps, refer to [Recovery by point in time](https://docs.byteplus.com/en/docs/mongodb/recovery-by-time-point?lang=en). |
|Replica set instance |If a log backup is selected, you must first generate a data backup using point\-in\-time recovery, then use the "Restore to a new instance" feature. For detailed steps, refer to [Recovery by point in time](https://docs.byteplus.com/en/docs/mongodb/roll-back-data). For more information on log backup and data backup, see [Overview](https://docs.byteplus.com/en/docs/mongodb/backup-overview?lang=en#.5aSH5Lu95a-56LGh). |


<span id="v97m17dE"></span>
## Is it necessary to manually create a new instance before performing point\-in\-time recovery?

No. After selecting the recovery time, the system will automatically guide you to the recovery instance configuration page. Once you confirm the configuration and cost, you can create a new instance and complete the recovery immediately, without requiring any preliminary operations

<span id="yW3PGMhg"></span>
## Can point\-in\-time recovery be accurate to the minute?

Yes. During the backup retention period, you can specify any minute\-level point for recovery in the console's time selection window. The most recent selectable point is 1 minute before the current time. For details, refer to [Recovery by point in time.](https://docs.byteplus.com/en/docs/mongodb/recovery-by-time-point?lang=en).

<span id="KsiDCppo"></span>
## What factors influence the time required for point\-in\-time recovery?

The principle of point\-in\-time recovery is to restore data to your specified time point by sequentially replaying all incremental oplog logs generated after the most recent full backup.

Therefore, the volume of oplog logs that need to be replayed directly determines the recovery time. The further the recovery time is from the last full backup, the more logs accumulate, leading to longer recovery times. Conversely, shorter distances result in faster recovery.

<span id="FoKFKBfB"></span>
## How to handle slow or stalled recovery progress?

Recovery slowdown is usually caused by the following factors:


* Large time span: The recovery point is far from the last full backup, requiring a large volume of logs to be replayed.

* High write pressure: The original instance experienced frequent writes or changes during that period, generating a large number of oplog entries.

* Low new instance specifications: CPU might become a bottleneck, affecting log replay speed.


You can select appropriate handling methods based on your actual scenario.


|**Solution** |**Applicable scenarios and descriptions** |
|---|---|
|Wait until the task is complete |In most cases, this is normal and requires no intervention. |
|Re\-initiate recovery, shorten time span |Selecting a recovery point within the last 7 days can significantly reduce the oplog replay volume. |
|Re\-initiate recovery and upgrade instance specifications |Selecting instances with higher CPU/memory specifications can significantly improve replay speed. Multiple restore tasks can be executed in parallel without affecting each other. |
|Only restore the full backup |If your business does not require point\-in\-time recovery to the second, you can directly use a full physical backup for restoration, skipping the oplog replay step, which is the fastest method. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In daily use, it is recommended to prioritize selecting a recovery point closer to the current time, which can effectively shorten recovery time.</div>


<span id="L0xtXFZs"></span>
## During the recovery process, if the original instance status changes to "Recovering," will it affect online services?

No. This status indicates that the instance is performing a data recovery task. During this period, the original instance can continue to provide read/write services, and you are not required to take any action.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When the instance is in the "Recovering" status, change\-type operations (e.g., upgrading, downgrading, modifying parameters) are temporarily not supported. Wait for the recovery task to complete before proceeding.</div>


<span id="0v5CfOZc"></span>
## Can multiple recovery tasks be initiated simultaneously for the same instance?

Yes. As long as the original instance is in the "Running" or "Recovering" status, you can submit multiple recovery tasks simultaneously. Each task executes independently, without affecting each other or slowing down each other's progress.

<span id="2yZAHEIT"></span>
## Database and table rollback failed due to insufficient storage space. What should I do?

First, expand the instance's storage space. The expanded capacity must be ≥ 1.2 times the currently used space. Then, you can re\-initiate the rollback task. For the specific procedure on storage space expansion, refer to [Modifying instance specifications](https://docs.byteplus.com/en/docs/mongodb/change-instance-config?lang=en).

<span id="1invmS0N"></span>
## Accidentally deleted a table or some data, what's the easiest way to recover?

Select the corresponding recovery method based on your MongoDB version.


|**MongoDB version** |**Recommended practice** |
|---|---|
|Version 4.0 |The database and table rollback feature is currently in grayscale release. [Submit a ticket](https://console.byteplus.com/workorder/create/) to apply for activation. If not yet enabled, you can first use point\-in\-time recovery to restore data to a new instance, then use Database Transmission Service (DTS) to migrate the required collections back to the original instance. For the specific procedure, refer to [Migrating to BytePlus MongoDB](https://docs.byteplus.com/en/docs/DTS/migrating_to_byteplus_documentdb_for_mongodb_mongodb?lang=en). |
|Non\-4.0 versions |Directly use the database and table rollback feature in the console. The system will automatically generate a replica table with a timestamp suffix in the source database (e.g., if the source table is `test`, a new `test_bak_backup_timestamp` table will be created after rollback), which will not overwrite or affect existing online data. For operation guidance, refer to [Rolling back database and table data](https://docs.byteplus.com/en/docs/mongodb/roll-back-data?lang=en). |


<span id="nq1m8OpZ"></span>
## After an instance is released, how long are my manually created backups retained?

Manual backups are uniformly retained for 7 days after an instance is released. After this period, the system automatically deletes them, and they cannot be recovered.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For important business data, it is recommended to download backup files to local storage before the instance is released. For the specific procedure, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/manage-backup-file?lang=en#OQemzRNR">Downloading backup file</a>.</div>


<span id="sYbG0laM"></span>
## After an instance is deleted, can my backup data still be retained long\-term?

Backups of deleted instances are only retained for 7 days and cannot be extended. To retain long\-term, refer to the following methods:


* Method 1 (Recommended): While the instance is still in use, retain or manually create a common data backup. Use the **Obtain backup file** feature in the console to download the backup to local or self\-owned storage (e.g., TOS) for long\-term retention. For specific procedures, refer to [Downloading backup file](https://docs.byteplus.com/en/docs/mongodb/manage-backup-file?lang=en#OQemzRNR).

* Method 2: After exporting data using the `mongodump`, archive it to long\-term storage services such as TOS.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The automatic backup retention period for common instances can be set to 7\-365 days, but this setting <strong>cannot change</strong> the limitation that backups are fixed for only 7 days after an instance is deleted.</div>


* <div data-tips="true" data-tips-type="default">Backup files <strong>cannot be directly</strong> restored to MongoDB instances in the cloud. To restore, you must first restore the backup file to a locally managed MongoDB environment and then migrate the data to a cloud instance.</div>
