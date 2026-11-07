---
title: "Backup and recovery"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/backup-and-recovery-faq"
---

This topic summarizes the FAQs related to the backup and recovery of Cache for Redis.

<span id=".5Zyo5o6n5Yi25Y-w5omn6KGM5LqG5riF6Zmk5pWw5o2u5pON5L2c5ZCO77yM5pWw5o2u6L-Y6IO95oGi5aSN5ZCX77yf"></span>
### Can data be restored after performing data clearing on the console?

After clearing the data, all business data in the current Redis instance is erased immediately and cannot be retrieved. Online business will be affected as a result. Please proceed with caution.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">We recommend that you manually back up the data in a primary\-secondary instance of Redis before clearing the data. For manual backup method, refer to <a href="https://docs.byteplus.com/en/docs/redis/manual-backup">Manual backup</a>.</div>


* <div data-tips="true" data-tips-type="tip">A single\-node instance does not support backup and recovery, so data cannot be recovered after being cleared. Please proceed with caution.</div>



<span id=".57yT5a2Y5pWw5o2u5bqTLXJlZGlzLeeJiOiHquWKqOWkh-S7veeahOaXtumXtOauteaYr-S7gOS5iOaXtuWAme-8nw=="></span>
### What is the time period for automatic backup of Cache for Redis?

After a Redis instance of primary\-secondary type is created successfully, if you do not modify the automatic backup policy, the system will select any one hour from 00:00 to 06:59 by default (such as 02:00 to 02:59) for backup every day. The backup is retained for 7 days by default. You can also modify the automatic backup policy according to business needs. For the modification method, refer to [Modifying automatic backup policy](https://docs.byteplus.com/en/docs/redis/automatic-backup).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Single\-node instances do not support backup and restore functionality, so automatic backup cannot be performed. For details about the feature differences between the two instance types, refer to <a href="https://docs.byteplus.com/en/docs/redis/feature-faq">Feature differences</a>.</div>


<span id=".5piv5ZCm6IO95oGi5aSN6K-v5pON5L2c5Yig6Zmk55qE5a6e5L6L77yf"></span>
### Can I recover an instance deleted by mistake?

When deleting instances, Redis provides different backup policies for different types of instances. Among them:


* Primary\-secondary instance: The default backup policy is **Create a final backup**.

   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">danger   </div>
   

   * <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">A final backup will be created by default before deleting the instance, and it will be retained for 7 days after successful creation. We recommend that you download and save it locally, because the data will be <strong>completely cleared</strong> after the instance is deleted, and cannot be recovered. Please proceed with caution.   </div>
   

   * <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">If you have deleted a primary\-secondary instance by accident, view and download the backup for the deleted instance on the <strong>Backups</strong> page. Recover the instance based on the backup. For more details, refer to <a href="https://docs.byteplus.com/en/docs/redis/restore-deleted-instance">Restoring deleted instance</a>.   </div>
   

* Single\-node instance: The default backup policy is **Do not create a final backup**.

   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">danger   </div>
   

   <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">A single\-node instance does not support persistence and backup. No backup is created when deleting data by default. The instance data is <strong>completely cleared</strong> after being deleted. Please proceed with caution. For more details about single\-node instances, refer to <a href="https://docs.byteplus.com/en/docs/redis/product-component-architecture">Product architecture</a>.   </div>
   

<span id=".5piv5ZCm5pSv5oyB5bCG5aSW6YOo5pWw5o2u5a-85YWlLXJlZGlzLeWunuS-i-S4re-8nw=="></span>
### Can I import external data into Cache for Redis?

You can use the database transfer service (About DTS) to smoothly migrate or synchronize external data online to Cache for Redis. For specific procedures to migrate or synchronize data, refer to [Creating Redis data migration tasks](https://docs.byteplus.com/en/docs/DTS/creating_redis_data_migration_tasks).

<span id=".57yT5a2Y5pWw5o2u5bqTLXJlZGlzLeeJiOaYr-WQpuaUr-aMgS1hb2Yt5oyB5LmF5YyW562W55Wl77yf6IO95ZCm6K6-572uLWFvZi3mjInnp5LokL3nm5jvvJ8="></span>
### Does Redis support the AOF persistence strategy? Can AOF be set to be written to disk every second?

The primary\-secondary instance of Cache for Redis by default enables the AOF persistence strategy. You can turn off the AOF persistence function through the `appendonly-switch` parameter, but currently customizing the AOF persistence strategy (such as setting AOF to be written to disk every second) is not supported. For more details about the `appendonly-switch` parameter, refer to [Supported parameters](https://docs.byteplus.com/en/docs/redis/supported-parameter).

In addition, the Cache for Redis also provides RDB snapshot storage and data flashback functions to achieve persistence:


* RDB snapshot storage periodically creates and generates RDB snapshot files based on the memory data at a specified time. During backup, it will not affect the performance of data access. For more details, refer to [Data backup](https://docs.byteplus.com/en/docs/redis/backup-recovery-intro#.5pWw5o2u5aSH5Lu9).

* After enabling the data flashback function, the system will archive AOF increments, which can be used for second\-level recovery and improve the convenience of operation and maintenance. For more details, refer to [Setting data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback).


<span id=".5Li65LuA5LmI5a6e5L6L5YWo6YeP5aSH5Lu957uT5p2f5ZCO77yMcmVkaXMtZXhwb3J0ZXIt5LiK5Lya5Ye6546wLXJlZGlzLWluc3RhbmNlLWxvc3QtYS1zbGF2ZS3miqXplJnvvJ8="></span>
### Why does the error "Redis instance lost a slave" appear on the Redis Exporter after the full backup of the instance is completed?

After a Redis instance is created successfully, if you do not modify the automatic backup policy, the system will default to select any one hour between 00:00 and 06:59 every day (such as 02:00 to 02:59) for full backup. During the full backup process, the system will treat this backup link as a separate slave node and synchronize data with the slave node of the server. After the backup is completed, this backup task link will be automatically disconnected.

Therefore, some monitoring tools (such as Redis Exporter) may display an error message like `Redis instance lost a slave` or similar. You do not need to handle the above error as it will not have any impact on the normal operation of the instance or backup tasks.

For more information about Redis automatic backup, refer to [Modifying automatic backup policy](https://docs.byteplus.com/en/docs/redis/automatic-backup).
