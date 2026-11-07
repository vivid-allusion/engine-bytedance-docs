---
title: "Viewing an event"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_an_event"
---

RDS for MySQL supports viewing the monitoring information of MySQL instances in the event center of Cloud Monitor. This topic describes the procedure for viewing RDS for MySQL events in the Cloud Monitor event center.

## **Background**

The Cloud Monitor event center provides fault monitoring for cloud products. When an event occurs for a cloud product, information such as the event time, event source, event name, and event details are saved to the event center. By viewing cloud product events, you can identify and resolve problems in a timely manner. For the RDS for MySQL events monitored in the Cloud Monitor event center, refer to [Appendix: MySQL events supported for viewing in the Cloud Monitor event center](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_an_event?lang=en#er4zjy7a).

## Precautions

Events are saved for 30 days by default.

## **Procedure**

1. Log on to the [Cloud Monitor console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left navigation bar, select **Event center**\>**Cloud product events**.

3. On the **Cloud Service Event** page, select **RDS for MySQL** from the cloud service drop\-down list.

   * You can filter events by specifying a time range and event type.

      * By default, events from the last hour are displayed.

      * The specified time range is accurate to the minute, with the seconds value defaulting to 00.

   * In the **Actions** column for a specific event, click **Details** to view its details. The information is displayed in JSON format.

## Subsequent steps

[Creating event policy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Creating_event_policy)

## **Related document**

* [Viewing cloud product events](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-cloud-service-events)

* [Creating event policy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule)

## Appendix: MySQL events supported for viewing in the Cloud Monitor event center

|**Event type** |**Event name** |**Event description** |
|---|---|---|
|Exception |rds_mysql:Exception:EipStatusException |Abnormal Eip state |
|Exception |rds_mysql:Exception:InstanceBackupFailure |Instance backup failed |
|Exception |rds_mysql:Exception:InstanceFailureStart |Abnormal instance state start |
|Exception |rds_mysql:Exception:InstanceFailureEnd |Abnormal instance state ended |
|Exception |rds_mysql:Exception:InstanceBackupFailure |Instance backup failed |
|Exception |rds_mysql:Exception:InstanceOOMException |Abnormal instance OOM |
|Exception |rds_mysql:Exception:InstanceBlueGreenDtsRebuildTaskFailed |Abnormal DTS task after blue\-green switch |
|Exception |rds_mysql:Exception:InstanceStorageAutoScalingFailed |Instance storage automatic expansion failed |
|Maintenance |rds_mysql:Maintenance:InstanceFailover |Switching between primary and secondary nodes (Failover) |
|Maintenance |rds_mysql:Maintenance:InstanceSwitchover |Switching between primary and secondary nodes (task switching) |
|Maintenance<br><br> |rds_mysql:Maintenance:ReadOnlyNodeDrained |Read\-only nodes are drained due to replication lag<br><br>> **tip**<br><br><br>> Instances with MySQL 8.4.7_20260815, MySQL 8.0.43_20260815, MySQL 5.7.44_20260815 and above support this event.<br> |
|Maintenance |rds_mysql:Maintenance:ReadOnlyNodeRejoined |Read\-only node drain recovery<br><br>> **tip**<br><br><br>> Instances with MySQL 8.4.7_20260815, MySQL 8.0.43_20260815, MySQL 5.7.44_20260815 and above support this event.<br> |
|BackupRecoveryManagement<br><br> |* rds_mysql:BackupRecoveryManagement:DeleteDateBackup.Initiated<br><br>* rds_mysql:BackupRecoveryManagement:DeleteDateBackup.Completed<br><br>* rds_mysql:BackupRecoveryManagement:DeleteDateBackup.Failed |* Delete backup initiated<br><br>* Delete backup completed<br><br>* Delete backup failed |
|DatabaseAdminManagement |* rds_mysql:DatabaseAdminManagement:DeleteDBAccount.Initiated<br><br>* rds_mysql:DatabaseAdminManagement:DeleteDBAccount.Completed<br><br>* rds_mysql:DatabaseAdminManagement:DeleteDBAccount.Failed |* Delete account initiated<br><br>* Delete account completed<br><br>* Delete account failed |
|DatabaseAdminManagement<br><br> |* rds_mysql:DatabaseAdminManagement:DeleteDatabase.Initiated<br><br>* rds_mysql:DatabaseAdminManagement:DeleteDatabase.Completed<br><br>* rds_mysql:DatabaseAdminManagement:DeleteDatabase.Failed |* Delete database initiated<br><br>* Delete database completed<br><br>* Delete database failed |
|DatabaseAdminManagement |* rds_mysql:DatabaseAdminManagement:RevokeDatabasePrivilege.Initiated<br><br>* rds_mysql:DatabaseAdminManagement:RevokeDatabasePrivilege.Completed<br><br>* rds_mysql:DatabaseAdminManagement:RevokeDatabasePrivilege.Failed |* Revoke database permissions initiated<br><br>* Revoke database permissions completed<br><br>* Failed to revoke database permissions |
|HighAvailability<br><br> |* rds_mysql:HighAvailability:SwitchDBInstanceHA.Initiated<br><br>* rds_mysql:HighAvailability:SwitchDBInstanceHA.Completed<br><br>* rds_mysql:HighAvailability:SwitchDBInstanceHA.Failed |* Switching between primary and secondary nodes initiated<br><br>* Switching between primary and secondary nodes completed<br><br>* Switching between primary and secondary nodes failed |
|InstanceManagement<br><br> |* rds_mysql:InstanceManagement:DeleteDBInstance.Initiated<br><br>* rds_mysql:InstanceManagement:DeleteDBInstance.Completed<br><br>* rds_mysql:InstanceManagement:DeleteDBInstance.Failed |* Delete instance initiated<br><br>* Delete instance completed<br><br>* Delete instance failed |
|InstanceManagement |* rds_mysql:InstanceManagement:DeleteDBNodes.Initiated<br><br>* rds_mysql:InstanceManagement:DeleteDBNodes.Completed<br><br>* rds_mysql:InstanceManagement:DeleteDBNodes.Failed |* Delete node initiated<br><br>* Delete node completed<br><br>* Delete node failed |
|InstanceManagement |* rds_mysql:InstanceManagement:MigrateToOtherZone.Initiated<br><br>* rds_mysql:InstanceManagement:MigrateToOtherZone.Completed<br><br>* rds_mysql:InstanceManagement:MigrateToOtherZone.Failed |* Migrate node pool initiated<br><br>* Migrate node pool completed<br><br>* Migrate node pool failed |
|InstanceManagement<br><br> |* rds_mysql:InstanceManagement:ModifyDBInstanceSpec.Initiated<br><br>* rds_mysql:InstanceManagement:ModifyDBInstanceSpec.Completed<br><br>* rds_mysql:InstanceManagement:ModifyDBInstanceSpec.Failed |* Modify instance specification initiated<br><br>* Modify instance specification completed<br><br>* Modify instance specification failed |
|InstanceManagement |* rds_mysql:InstanceManagement:ModifyDBNodeSpec.Initiated<br><br>* rds_mysql:InstanceManagement:ModifyDBNodeSpec.Completed<br><br>* rds_mysql:InstanceManagement:ModifyDBNodeSpec.Failed |* Modify node specification initiated<br><br>* Modify node specification completed<br><br>* Modify node specification failed |
|InstanceManagement |* rds_mysql:InstanceManagement:RestartDBInstance.Initiated<br><br>* rds_mysql:InstanceManagement:RestartDBInstance.Completed<br><br>* rds_mysql:InstanceManagement:RestartDBInstance.Failed |* Restart instance initiated<br><br>* Restart instance completed<br><br>* Restart instance failed |
|InstanceManagement |* rds_mysql:InstanceManagement:StartDBInstance.Initiated<br><br>* rds_mysql:InstanceManagement:StartDBInstance.Completed<br><br>* rds_mysql:InstanceManagement:StartDBInstance.Failed |* Start instance initiated<br><br>* Start instance completed<br><br>* Start instance failed |
|InstanceManagement |* rds_mysql:InstanceManagement:SwitchDBBlueGreen.Initiated<br><br>* rds_mysql:InstanceManagement:SwitchDBBlueGreen.Completed<br><br>* rds_mysql:InstanceManagement:SwitchDBBlueGreen.Failed |* Blue\-green switch initiated<br><br>* Blue\-green switch completed<br><br>* Blue\-green switch failed |
|NetworkManagement |* rds_mysql:NetworkManagement:DeleteDBEndpoint.Initiated<br><br>* rds_mysql:NetworkManagement:DeleteDBEndpoint.Completed<br><br>* rds_mysql:NetworkManagement:DeleteDBEndpoint.Failed |* Delete endpoint initiated<br><br>* Delete endpoint completed<br><br>* Delete endpoint failed |
|NetworkManagement |* rds_mysql:NetworkManagement:DeleteDBEndpointPublicAddress.Initiated<br><br>* rds_mysql:NetworkManagement:DeleteDBEndpointPublicAddress.Completed<br><br>* rds_mysql:NetworkManagement:DeleteDBEndpointPublicAddress.Failed |* Disable public network access completed<br><br>* Disable public network access failed<br><br>* Disable public network access initiated |
|SecurityManagement<br><br> |* rds_mysql:SecurityManagement:AssociateAllowList.Initiated<br><br>* rds_mysql:SecurityManagement:AssociateAllowList.Completed<br><br>* rds_mysql:SecurityManagement:AssociateAllowList.Failed |* Associated allowlist initiated<br><br>* Associated allowlist completed<br><br>* Associated allowlist failed |
|SecurityManagement |* rds_mysql:SecurityManagement:DisassociateAllowList.Initiated<br><br>* rds_mysql:SecurityManagement:DisassociateAllowList.Completed<br><br>* rds_mysql:SecurityManagement:DisassociateAllowList.Failed |* Disassociating allowlists initiated<br><br>* Disassociating allowlists completed<br><br>* Disassociating allowlists failed |
|SystemMaintainManagement |* rds_mysql:SecurityManagement:ModifyPlannedEventExecuteTime.Initiated<br><br>* rds_mysql:SecurityManagement:ModifyPlannedEventExecuteTime.Completed<br><br>* rds_mysql:SecurityManagement:ModifyPlannedEventExecuteTime.Failed |* Modify maintenance window initiated<br><br>* Modify maintenance window completed<br><br>* Modify maintenance window failed |
|VersionUpgrade<br><br> |* rds_mysql:VersionUpgrade:UpgradeDBInstanceEngineMinorVersion.Initiated<br><br>* rds_mysql:VersionUpgrade:UpgradeDBInstanceEngineMinorVersion.Completed<br><br>* rds_mysql:VersionUpgrade:UpgradeDBInstanceEngineMinorVersion.Failed |* Upgrade instance kernel version initiated<br><br>* Upgrade instance kernel version completed<br><br>* Upgrade instance kernel version failed |
