---
title: "Control panel audit log"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/control-plane-auditing"
---

The Cloud Search service has been integrated with the Volcengine Operation Audit service. Operation events related to Cloud Search will be recorded through the Operation Audit service for future query, audit, and traceability.

Currently, Cloud Search provides control panel and data plane audit logs. Only control panel logs are recorded in the Operation Audit service.

<span id="13addde2"></span>
## Precautions

Only ES instances of `version 7.10.2` currently support the security audit feature.

<span id="6d941e50"></span>
## View control panel audit logs

Control panel audit is enabled by default, recording instance changes, queries, and other operations to the Operation Audit service. You can directly access the Operation Audit console to view audit logs.


1. Log on to the[Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click the target instance name to enter the instance details page.

4. In the left navigation bar of the instance details, select **Observability \> Security audit**, then click **View event log** in the **Control panel auditing** area to automatically jump to the [Operation Audit Service Console](https://console.byteplus.com/cloudtrail).

5. In the Operation Audit Console, enter **Cloud Search** in the **Event source** filter box to filter related events of Cloud Search under the current account.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also quickly filter logs for the past 1 hour, 1 day, and 1 week, or select an exact time in the time picker to filter logs.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Operation audit provides access logs within 180 days only.   </div>
   

6. Click the event occurrence time to view event details.


<span id="45b90bb7"></span>
## Audit event description

Operation audit records management events generated when users operate cloud resources via OpenAPI or console. The following table lists the events supported by Cloud Search.


|**Event name** |**Event description** |
|---|---|
|ModifyIpWhitelist |Modify allowlist IP address. |
|CreateInstanceInOneStep |Create an instance in one step. |
|ModifyNodeSpecInOneStep |Update instance node specification step by step |
|ModifyChargeCode |Change the billing method, only supporting conversion from pay\-as\-you\-go to subscription. |
|DescribeGASLogs |Query GAS logs. |
|GetGMSUserToken |Get user Token and UUID. |
|InnerCreateInstance |Create instance. |
|ModifyWhiteList |Modify whitelist. |
|ModifyESNetworkSetting |Modify ES network configuration. |
|ModifyKibanaNetworkSetting |Modify Kibana network configuration. |
|ModifyMaintenanceSetting |Modify maintainable time configuration. |
|ModifyEndpointAddress |Modify instance private network address. |
|ModifyInstanceChargeType |Modify instance billing type. |
|ModifyDeletionProtection |Modify instance anti\-deletion configuration. |
|StopTransferNode |Stop data migration. |
|ReleasePublicAddress |Turn off instance public address. |
|CreateInstance |Create instance |
|ReleaseInstance |Delete instance. |
|ModifyTransportProtocol |Change the instance transport protocol type. |
|ModifyPrivateDomainPublic |Change private network to public network resolution configuration. |
|CreatePublicAddress |Enable public network access for the instance. |
|ScaleInstance |Scale instance capacity. |
|TransferNode |Data migration. |
|ModifyResourceTag |Update resource tags. |
|DescribeInstancePrice |Query instance configuration price. |
|CheckReduceCapacity |Validate volume shrinkage and change specification. |
|AdminDescribeInstances |Admin resource pool query list. |
|DescribeAdminInstances |Administrator resource pool query list. |
|DescribeRegions |Get the Region list. |
|DescribeZones |Get the Zone list. |
|DescribeInstances |Get the instance list. |
|DescribeInstance |Get instance details. |
|DescribeNodeAvailableSpecs |Get the list of available node configurations. |
|RenameInstance |Rename instance. |
|ResetAdminPassword |Reset the instance administrator password. |
|UploadCustomPlugins |Upload user\-defined plugin. |
|DescribeTransferCostEvalution |Estimate the time consumed for data migration. |
|ModifyInstanceSettings |Modify ES configuration. |
|DeleteBackup |Delete backup records and data. |
|DeleteCustomPlugins |Delete user\-defined plugin. |
|UninstallCustomPlugins |Uninstall user\-defined plugin. |
|EnableS3Backup |Enable backup. |
|EnableAudit |Enable data plane audit log. |
|DetailBackupHistory |Details of backup history. |
|InstallCustomPlugins |Install user\-defined plugins. |
|EnableManualBackup |Turn on manual backup. |
|EnableBackupRestore |Turn on manual recovery. |
|ExistSameSnapshot |Whether the manually backed\-up snapshot has a duplicate name. |
|SuspendFiles |Batch disable external files. |
|DeleteTosFiles |Batch delete external files saved in TOS. |
|DeleteFiles |Batch delete external files. |
|ApplyFiles |Batch enable external files. |
|UpdateInstancePlugins |Update instance plugin. |
|DescribeAuditEnabled |View data plane audit log status |
|ListBackupHistory |Query backup history. |
|ListInstanceIndice |Query the index list of the instance. |
|DescribeTransferProgress |Query data migration progress. |
|DescribeAccountPermission |Query user permissions. |
|ListCustomPlugins |Query user\-defined plugin list. |
|DisableS3Backup |Disable backup. |
|DisableAudit |Disable data plane audit log. |
|DescribeInstanceSettings |Get the list of ES configurations. |
|DescribeS3Buckets |Get S3 bucket list. |
|GetFileUploadInfo |Get external file upload information. |
|GetFileDownloadInfo |Get external file download information. |
|DescribeFiles |Get instance external file list |
|DescribeInstancePlugins |Get instance plugin list. |
|DescribeS3BackupConfig |Get the instance's S3 backup configuration. |
|GetInstanceStats |Get instance statistics. |
|DescribeInstanceNodes |Get list of instance nodes. |
|DescribeAccountAccess |Obtain the tenant's platform access method. |
|RestartInstance |Restart instance. |
|RestartNode |Restart node |
|ForecastBackupTime |Estimate backup time consumption. |
|ForecastRestoreTime |Estimate recovery time. |
