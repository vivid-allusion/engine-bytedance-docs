---
title: "Feature Overview"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/features-overview"
---

This topic describes the features supported by each edition of RDS for SQL Server. You can use this information to select an instance that meets your needs and view the features supported by your purchased instances.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The features supported by RDS for SQL Server may differ from those provided by Microsoft. For more information, see the <a href="https://learn.microsoft.com/zh-cn/sql/sql-server/editions-and-components-of-sql-server-2019?view=sql-server-ver16">official Microsoft documentation</a>.</div>



|**Module** |**Feature** |**Single node edition** |**High availability** |**Cluster Edition** |References |
|---|---|---|---|---|---|
|Lifecycle |Create an instance |Supports |Supports |Supports |[Create an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide) |
||Restart an instance |Supports |Supports |Supports |[Restart an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/restart-instance) |
||Automatic renewal. |Supports |Supports |Supports |[Renewal description](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/renewal-management) |
||Switch to subscription |Supports |Supports |Supports |[Switch to subscription](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/switching-to-yearly-or-monthly-subscription) |
||Change instance configuration |Supports |Supports |Supports |[Change instance configuration](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/changing-an-instance-configuration) |
||Delete instance |Supports |Supports |Supports |[Delete instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/deleting-pay-as-you-go-instance) |
||Create read\-only instance |Unsupports |Unsupports |Supports |[Create read-only instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-read-only-instance) |
|Instance information |View instancesInstances |Supports |Supports |Supports |[View instances](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-instance-details) |
||View instance information |Supports |Supports |Supports ||
||Reset Advanced Account Password |Supports |Supports |Supports |[Reset Advanced Account Password](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Reset_password) |
||Project management |Supports |Supports |Supports |[Project management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management) |
||Tag management |Supports |Supports |Supports |[Tag management](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/tag-management) |
|Database connection |Private network connection |Supports |Supports |Supports |[Connect to an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connecting-to-instance) |
||Public network connection |Supports |Supports |Supports ||
|Service availability |Same\-city disaster recovery |Unsupports |Supports |Supports |[Create an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide) |
||Primary/Secondary failover |Unsupports |Supports |Supports |[Switch to primary node](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/switching-master-node) |
|Backup and recovery |Full backup |Supports |Supports |Supports |[About Backups](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/about-backup) |
||Differential backup |Supports |Supports |Supports ||
||Log backup |Supports |Supports |Supports ||
||Customize backup policy |Supports |Supports |Supports |[Customize backup policy](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/custom-backup-policy) |
||Database\-level or instance\-level restore from a backup set |Supports |Supports |Supports |* [Restore to a new instance from a backup set](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/recovery-to-new-instances-by-using-backup-set)<br><br>* [Restore to an existing instance from a backup set](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/recovery-to-existing-instances-by-using-backup-set) |
||Database\-level or instance\-level point\-in\-time restore |Supports |Supports |Supports |* [Restore to a new instance by time in point](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/recovering-to-new-instance-by-time-point)<br><br>* [Restore to an existing instance by point in time](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/recovering-to-existing-instance-by-time-point) |
||Database\-level manual backup |Supports |Supports |Supports |[Create a manual backup](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-data-backup-manually) |
||Restore to the cloud from TOS backup files (full, differential, and log backups) |Supports |Supports |Supports |[Create TOS backup recovery task](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-tos-backup-recovery-task) |
|Monitoring and alerts |Resource monitoring |Supports |Supports |Supports |[Monitoring Metrics Description](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/monitoring-metrics) |
||Engine monitoring |Supports |Supports |Supports ||
|Parameter management |Parameter update |Supports |Supports |Supports |[Modify parameters](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/modifying-parameters) |
|Log management |Error log |Supports |Supports |Supports |[View error logs](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-error-logs) |
||Running log |Supports |Supports |Supports |[Running log](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/enabling-slow-log) |
||Primary and secondary failover log |Unsupports |Supports |Supports |[Primary and secondary failover log](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-master-and-standby-switch-log) |
|Data Security |Allowlist management |Supports |Supports |Supports |[Allowlist management](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/managing-allowlists?lang=en) |
||Distributed transaction allowlist |Supports |Supports |Supports |[Configure the distributed transaction allowlist](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Configure_the_distributed_transaction_allowlist?lang=en)<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This feature is available on an allowlist basis. To request access, <a href="https://console.byteplus.com/workorder/create">Submit a ticket</a> to contact the SQL Server technical team.</div><br> |
||TDE encryption |Supports |Supports |Unsupports |[Enable transparent data encryption (TDE).](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/Enable_transparent_data_encryption_TDE?lang=en)<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This feature is available on an allowlist basis. To request access, <a href="https://console.byteplus.com/workorder/create">Submit a ticket</a> to contact the SQL Server technical team.</div><br> |
||SSL encryption |Supports |Supports |Supports |[Set up SSL encryption](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/setting-ssl-encryption?lang=en) |
