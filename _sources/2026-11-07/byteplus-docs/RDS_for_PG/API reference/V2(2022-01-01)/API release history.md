---
title: "API release history"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/api_release_notes"
---

## October 2026

|API |Release date |Change log |Related functions |
|---|---|---|---|
|新增 [CreateSQLConcurrencyControlRule](https://docs.byteplus.com/en/docs/6438/2692657) |2026\-10\-15 |New API. |SQL throttling |
|新增 [ModifySQLConcurrencyControlRule](https://docs.byteplus.com/en/docs/6438/2692658) ||||
|新增 [DescribeSQLConcurrencyControlRules](https://docs.byteplus.com/en/docs/6438/2692659) ||||
|新增 [SwitchSQLConcurrencyControlRule](https://docs.byteplus.com/en/docs/6438/2692660) ||||
|新增 [DeleteSQLConcurrencyControlRule](https://docs.byteplus.com/en/docs/6438/2692661) ||||
|更新 [CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/CreateDBInstance) ||Updated the value range of request parameter DBEngineVersion, adding `PostgreSQL_18`. |[CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/CreateDBInstance?lang=en) |
|更新 [DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/describebackups) ||Updated the return parameter DBEngineVersion value range to include `PostgreSQL_18`. |[DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/describebackups?lang=en) |
|更新 [DescribeDetachedBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/describedetachedbackups) |||[DescribeDetachedBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/describedetachedbackups?lang=en) |
|更新 [DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstanceparameters) |||[DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstanceparameters?lang=en) |
|更新 [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances) |||[DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances?lang=en) |
|更新 [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancedetail) |||[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancedetail?lang=en) |
|更新 [DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancespecs) ||Updated the value range of request parameter DBEngineVersion, adding `PostgreSQL_18`. |[DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancespecs?lang=en) |
|更新 [DescribeDBInstanceProxyParameters](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeDBInstanceProxyParameters) ||Updated the return parameter DBEngineVersion value range to include `PostgreSQL_18`. |[DescribeDBInstanceProxyParameters](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeDBInstanceProxyParameters?lang=en) |
|新增 [DescribeDBEngineVersionParameters](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeDBEngineVersionParameters) ||Updated the value range of request parameter DBEngineVersion, adding `PostgreSQL_18`. |[DescribeDBEngineVersionParameters](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeDBEngineVersionParameters?lang=en) |
|新增 [CreateParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/CreateParameterTemplate) |||[CreateParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/CreateParameterTemplate?lang=en) |
|新增 [ListParameterTemplates](https://docs.byteplus.com/en/docs/RDS_for_PG/ListParameterTemplates) |||[ListParameterTemplates](https://docs.byteplus.com/en/docs/RDS_for_PG/ListParameterTemplates?lang=en) |
|新增 [DescribeParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeParameterTemplate) |||[DescribeParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeParameterTemplate?lang=en) |
|更新 Common structure \- BasicInfoObject ||Updated the parameter DBEngineVersion value range, adding `PostgreSQL_18`. |\- |
|更新 Common structure \- InstanceInfoObject ||||
|更新 Common structure \- InstanceObject ||||
|更新 Common structure \- InstanceSpecObject ||||

## June 2026

|API |Release date |Change log |Related functions |
|---|---|---|---|
|更新 [CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/CreateDBInstance) |2026\-06\-03 |Added request parameters `TDEEnable` and `KMSTrn`. |Managing instances |
|更新 [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancedetail) ||Add response parameters `TDEEnable` and `KMSTrn`. ||

## April 2026

|API |Release date |Change log |Related functions |
|---|---|---|---|
|更新 [CreateAllowList](https://docs.byteplus.com/en/docs/RDS_for_PG/createallowlist) |2026\-04\-16 |Updated the description of request parameters UserAllowList and AllowList, adding explanations on the validity of values when both are passed simultaneously. |Data security |

## March 2026

|API |Release date |Change log |Related functions |
|---|---|---|---|
|更新 [CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/CreateDBInstance) |2026\-03\-30 |Update the description of parameter StorageSpace due to different specification supporting storage space ranges |Managing instances |
|更新 [DescribeDBInstancePriceDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancepricedetail) ||||
|更新 [DescribeDBInstancePriceDifference](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancepricedifference) ||||
|更新 [ModifyDBInstanceSpec](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbinstancespec) ||||
|更新 [RestoreToNewInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/restoretonewinstance) |||Backup and recovery |
|更新 Common structure \- InstanceSpecObject ||Added parameters StorageSpaceMax and StorageSpaceMin to specify the maximum and minimum storage space supported by the current specification respectively. |\- [DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancespecs) |

## January 2026

|API |Release date |Change log |Related functions |
|---|---|---|---|
|更新 [ModifyDBInstanceParameters](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbinstanceparameters) |2026\-01\-09 |Updated the request type of the API from "Sync request" to "Async request". |Managing connections |
|更新 [ModifyDBEndpointReadWriteFlag](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbendpointreadwriteflag) |||Managing parameters |
|更新 [CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/CreateDBInstance) ||Added the request parameter `MaintenanceWindow`. |Managing instances |
|更新 [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances) ||Added return parameter `MaintenanceWindow`. ||
|更新 [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancedetail) ||||
|更新 [ModifyDBInstanceSpec](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbinstancespec) ||Added the request parameters `SwitchType`, `SwitchType`, and `SpecifiedSwitchEndTime`. ||
|更新 [RestoreToNewInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/restoretonewinstance) ||Added the request parameter `MaintenanceWindow`. |Backup and recovery |
|新增 [ModifyPlannedEventExecuteTime](https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyPlannedEventExecuteTime) ||New API. |Event management |
|新增 [ModifyTask](https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyTask) |||Managing tasks |

## December 2025

|API |Release date |Change log |Related functions |
|---|---|---|---|
|新增 [DescribeWALLogBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeWALLogBackups) |2025\-12\-02 |Added a new API: `DescribeWALLogBackups` to retrieve the list of backed\-up WAL logs for a specified instance. |Backup and recovery |
|更新 [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances) ||Added `PrivateNetworkVpcId` parameter for filtering instances using the specified virtual private cloud. |Managing instances |
|更新 [DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstanceparameters) ||Added return parameter `NoneKernelParameters` to return the current parameter configuration of the instance (non\-kernel parameters). |Managing parameters |

## October 2025

|API |Release date |Change log |Related functions |
|---|---|---|---|
|更新 [DescribeBackupPolicy](https://docs.byteplus.com/en/docs/RDS_for_PG/describebackuppolicy) |2025\-10\-13 |* Added return parameter `DataIncrBackupPeriods` to describe the backup frequency for the backup method as normal frequency, with a prompt that if the instance does not enable incremental backup, this field will not be returned.<br><br>* Added return parameter `HourlyIncrBackupEnable` to describe whether the high frequency backup function is enabled.<br><br>* Modified the return parameter `IncrementBackupFrequency` description, add the `12` value for high frequency incremental backup frequency, and explain that this parameter only takes effect when `HourlyIncrBackupEnable` is set to `true`. |Backup and recovery |
|更新 [ModifyBackupPolicy](https://docs.byteplus.com/en/docs/RDS_for_PG/modifybackuppolicy) ||* Added to the prompt of the `FullBackupPeriod` parameter: choose at least one day each week for full backup.<br><br>* Added parameter `DataIncrBackupPeriods`: sets the backup frequency for incremental backups with normal frequency. Values must not overlap with the full backup schedule, and up to six days per week can be selected for incremental backup.<br><br>* Added parameter `HourlyIncrBackupEnable`: controls whether to enable high\-frequency backup.<br><br>* Modified the description of the `IncrementBackupFrequency` parameter: added value `12` and clarified this applies only when `HourlyIncrBackupEnable` is `true`. ||
|更新 [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances) |October.14 2025 |* The `StorageType` parameter is added to the body parameter of `DescribeDBInstances` API to specify the instance storage type, and the fixed value `LocalSSD` (local SSD disk) is used.<br><br>* The `CrossRegionDomain` parameter is added to the `AddressObject` structure to indicate the private network address accessible across regions. This field is not returned if no such address exists.<br><br>* The `DomainVisibilitySetting` parameter is added to the `AddressObject` structure to indicate the private network address type. The values are `LocalDomain` (local domain name) or `CrossRegionDomain` (cross\-region accessible domain name). |Managing instances |
|更新 [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancedetail) ||* Added `CrossRegionDomain` parameter in `AddressObject` to describe private network addresses accessible across regions.<br><br>* Added `DomainVisibilitySetting` parameter in `AddressObject` to describe private network address types, including local domain names and cross\-region accessible domain names. ||
|更新 [DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancespecs) |2025\-10\-13 |* Added `StorageType` request parameter to specify instance storage type, fixed value `LocalSSD` (local SSD disk).<br><br>* Added `StorageType` field to the returned parameter `InstanceSpecObject` to return the instance storage type information, with a fixed value of `LocalSSD` (local SSD disk). ||
|更新 [ModifyDBInstanceSpec](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbinstancespec) ||* Added `EstimateOnly` parameter to initiate configuration adjustment evaluation. When set to `true`, it returns `EstimationResult`, which describes the impact of this configuration adjustment.<br><br>* Added `EstimationResult` field to the returned parameters to describe the estimated impact on the instance based on the current configuration change.<br><br>* Added description to the `OrderId` field in the returned parameters. When `EstimateOnly` is set to `true`, this field returns empty.<br><br>* Added `ModifyDBInstanceSpecEstimationResult` object, containing `Plans` and `Effects` fields, which describe the impact on the instance and read/write connections after the modification. ||
|新增 [DescribeDBInstanceSSL](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeDBInstanceSSL) ||Added `DescribeDBInstanceSSL` API to query the SSL settings of the specified instance. This API supports querying the following information:<br><br><br>* Protected address<br><br>* Force encryption status<br><br>* SSL certificate validity<br><br>* SSL function enabled status<br><br>* SSL certificate expiration time<br><br>* Supported TLS versions |Data security |
|新增 [ModifyDBInstanceSSL](https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyDBInstanceSSL) ||Added the `ModifyDBInstanceSSL` interface to modify the SSL configuration of the specified instance. This interface supports the following functions:<br><br><br>* Enabled or disabled SSL encryption (via `SSLEnable` parameter)<br><br>* Updated SSL certificate validity period (via `ReloadSSLCertificate` parameter)<br><br>* Enabled or disabled SSL force encryption (via `ForceEncryption` parameter)<br><br>* > Updating the SSL certificate validity and force encryption features only take effect when the instance has the SSL encryption feature enabled.<br><br><br>* > It does not support passing `ReloadSSLCertificate` and `SSLEnable` parameters at the same time;<br> ||
|新增 [DownloadSSLCertificate](https://docs.byteplus.com/en/docs/RDS_for_PG/DownloadSSLCertificate) ||Added the `DownloadSSLCertificate` interface to download the SSL certificate of the specified instance. This API requires an instance ID as a mandatory parameter and returns a compressed certificate package. ||
|新增 [DescribeTasks](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeTasks) ||Added `DescribeTasks` API to query task information. This API supports querying task details by task ID or task time range and returns the execution status, duration, creation time, and other information of the task. |Managing tasks |

## August 2025

|API |Release date |Change log |Related functions |
|---|---|---|---|
|更新 [DescribeAllowListDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describeallowlistdetail) |2025\-08\-26 |\- Added return parameter `AssociatedInstanceNum`. |[Viewing allowlist details](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Viewing_allowlist_details) |

## July 2025

|API |Release date |Change log |Related functions |
|---|---|---|---|
|更新 [CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/CreateDBInstance) |2025\-07\-31 |\- Added `AllowListIds` parameter for associating allowlists. Support associating multiple allowlists, separated by English commas. A single instance can associate up to 100 allowlists. |[Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance) |
|更新 [DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/describebackups) ||\- Added `AllowListIds` parameter in `InstanceInfoObject` to describe the allowlist information associated with the backup instance. |\- |
|更新 [DescribeDetachedBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/describedetachedbackups) ||\- Added `AllowListIds` parameter in the `InstanceInfoObject` structure to describe the allowlists bound to the instance to which the backup belongs. ||
|更新 [RestoreToNewInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/restoretonewinstance) ||\- Added `AllowListIds` parameter for associating with allowlists. Supports binding multiple allowlists, up to 100 allowlists can be associated. |[Restoring to a new instanceRestoring to new instance](https://docs.byteplus.com/en/docs/RDS_for_PG/recovery_from_a_backup_set) |
|更新 [DescribePlannedEvents](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribePlannedEvents) ||\- Added `MaxDelayTime` parameter to indicate the latest postponed time of operation and maintenance events, formatted as `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time). |[Viewing operation and maintenance events](https://docs.byteplus.com/en/docs/RDS_for_PG/view_operation_and_maintenance_events) |
|更新 [DescribeAllowLists](https://docs.byteplus.com/en/docs/RDS_for_PG/describeallowlists) ||* Added request parameter `AllowListCategory` to specify allowlist category, with values including `Ordinary` (ordinary allowlist) and `Default` (default allowlist), defaulting to `Ordinary`.<br><br>* Added request parameter `AllowListDesc` for fuzzy search of allowlists by description.<br><br>* Added request parameter `AllowListId` for querying by allowlist ID.<br><br>* Added request parameter `AllowListName` for querying by allowlist name.<br><br>* Added request parameter `IPAddress` to support querying allowlists by IP address. Multiple IP addresses can be separated by commas.<br><br>* Added request parameter `PageNumber` to specify the current page number. The default value is 1.<br><br>* Added request parameter `PageSize` to specify the number of records per page. No default value.<br><br>* Added return parameter `Total` to indicate the total number of allowlists.<br><br>* Added field `AllowListCategory` in `AllowListObject` to indicate the allowlist category.<br><br>* Added field `SecurityGroupBindInfos` in `AllowListObject` to indicate security group binding information for allowlists, including security group ID, name, IP list, and association mode.<br><br>* Added data structure `SecurityGroupBindInfo` to describe security group binding information, including fields such as `IpList`, `BindMode`, `SecurityGroupId`, and `SecurityGroupName`. |\- |
|更新 [DescribeAllowListDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describeallowlistdetail) ||* Added return parameter `AllowListCategory` to identify the allowlist category, with values including `Ordinary` (ordinary allowlist) and `Default` (default allowlist). The default value is `Ordinary`.<br><br>* Added return parameter `SecurityGroupBindInfos` to describe the security group list bound to the allowlist, including IPs in the security group, associated security group mode, security group ID, and security group name.<br><br>* Added the return parameter `UserAllowList` to describe IP addresses or CIDR\-formatted IP address segments outside the security groups that need to be added to the allowlist. ||
|更新 [CreateAllowList](https://docs.byteplus.com/en/docs/RDS_for_PG/createallowlist) ||* `AllowList` parameter changed from required to optional, with a new prompt: this field cannot be used simultaneously with `UserAllowList`.<br><br>* Added `AllowListCategory` parameter to specify allowlist category, optional values: `Ordinary` (ordinary allowlist) and `Default` (default allowlist), default value is `Ordinary`.<br><br>* Added `SecurityGroupBindInfos` parameter to bind security group information to the allowlist, including subparameters `IpList`, `BindMode`, `SecurityGroupId`, and `SecurityGroupName`.<br><br>* Added `UserAllowList` parameter to specify IP addresses to be added to the allowlist outside the security group, this field cannot be used simultaneously with `AllowList`.<br><br>* Added `SecurityGroupBindInfo` data structure including fields `IpList`, `BindMode`, `SecurityGroupId`, and `SecurityGroupName`. |[Creating an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/adding_an_ip_address_allowlist) |
|更新 [ModifyAllowList](https://docs.byteplus.com/en/docs/RDS_for_PG/modifyallowlist) ||* Added warning in `ModifyMode` parameter description: if the allowlist to be modified is bound to a security group, or if binding a security group when modifying the allowlist is required, then `ModifyMode` can only take the value `Cover`.<br><br>* Added `AllowListCategory` parameter to specify the allowlist category, with values `Ordinary` (ordinary allowlist) or `Default` (default allowlist). The default value is `Ordinary`.<br><br>* Added `SecurityGroupBindInfos` parameter to provide information for associating security groups with the allowlist, including `IpList`, `BindMode`, `SecurityGroupId`, and `SecurityGroupName`.<br><br>* Added `UpdateSecurityGroup` parameter to control whether to update the security groups bound to the allowlist, with values `true` (update) or `false` (no update). The default value is `false`.<br><br>* Added `UserAllowList` parameter to specify IP addresses to add to the allowlist outside of security groups, supporting both individual IP addresses and CIDR\-format IP address ranges.<br><br>* Added `SecurityGroupBindInfo` structure to describe security group binding information, including `IpList`, `BindMode`, `SecurityGroupId`, and `SecurityGroupName`. |[Modifying an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_an_allowlist) |

## June 2025

|API |Release date |Change log |Related functions |
|---|---|---|---|
|新增 [CloneDatabase](https://docs.byteplus.com/en/docs/RDS_for_PG/CloneDatabase) |2025\-06\-04 |New API. |[Cloning a database](https://docs.byteplus.com/en/docs/RDS_for_PG/Clone) |
|新增 [CloneParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/CloneParameterTemplate) |||[Managing parameter template](https://docs.byteplus.com/en/docs/RDS_for_PG/Managing_a_parameter_template) |
|新增 [CreateParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/CreateParameterTemplate) |||[Creating a parameter template](https://docs.byteplus.com/en/docs/RDS_for_PG/Creating_a_parameter_template) |
|新增 [DeleteBackup](https://docs.byteplus.com/en/docs/RDS_for_PG/DeleteBackup) |||[Deleting data backup](https://docs.byteplus.com/en/docs/RDS_for_PG/Deleting_a_data_backup) |
|新增 [DeleteParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/DeleteParameterTemplate) |||[Managing parameter template](https://docs.byteplus.com/en/docs/RDS_for_PG/Managing_a_parameter_template) |
|新增 [DescribeApplyParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeApplyParameterTemplate) |||[Apply parameter template](https://docs.byteplus.com/en/docs/RDS_for_PG/Applying_a_parameter_template) |
|新增 [DescribeDBEngineVersionParameters](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeDBEngineVersionParameters) |||\- |
|新增 [DescribeParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeParameterTemplate) |||[Managing parameter template](https://docs.byteplus.com/en/docs/RDS_for_PG/Managing_a_parameter_template) |
|新增 [DownloadBackup](https://docs.byteplus.com/en/docs/RDS_for_PG/DownloadBackup) |||[Downloading data backup files](https://docs.byteplus.com/en/docs/RDS_for_PG/Downloading_a_data_backup) |
|新增 [GetBackupDownloadLink](https://docs.byteplus.com/en/docs/RDS_for_PG/GetBackupDownloadLink) ||||
|新增 [ListParameterTemplates](https://docs.byteplus.com/en/docs/RDS_for_PG/ListParameterTemplates) |||[Managing parameter template](https://docs.byteplus.com/en/docs/RDS_for_PG/Managing_a_parameter_template) |
|新增 [ModifyParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyParameterTemplate) ||||
|新增 [RestoreToExistedInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/RestoreToExistedInstance) |||[Restoring to existing instance](https://docs.byteplus.com/en/docs/RDS_for_PG/Restoring_to_an_existing_instance) |
|新增 [SaveAsParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/SaveAsParameterTemplate) |||[Exporting parameter configuration as parameter template](https://docs.byteplus.com/en/docs/RDS_for_PG/Exporting_parameter_configuration_as_a_parameter_template) |
|更新 [CreateBackup](https://docs.byteplus.com/en/docs/RDS_for_PG/createbackup) ||* Added request parameters BackupScope, BackupMethod, BackupDescription, BackupMeta.<br><br>* Added the return parameter BackupId. |[Creating a data backup](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_manual_backup) |
|更新 [DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/describebackups) ||* Added request parameters DownloadStatus, BackupMethod, BackupDatabaseName, BackupDescription, CreateType, and BackupScope.<br><br>* Added return parameter BackupId. |\- |
|更新 [ModifyDBEndpointReadWeight](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbendpointreadweight) ||Updated the description of the request parameter WriteNodeHaltWriting. ||
|更新 [ModifyDBEndpointReadWriteFlag](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbendpointreadwriteflag) ||||
|新增 Common structure \- BackupMetaObject ||Add a new struct. |* [CreateBackup](https://docs.byteplus.com/en/docs/RDS_for_PG/createbackup)<br><br>* [DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/describebackups) |
|更新 Common structure \- BackupObject ||* Added parameters BackupDataSize, BackupDescription, BackupMeta, BackupMethod, BackupScope, and DownloadStatus.<br><br>* Updated value ranges for parameters BackupStatus, BackupType, and CreateType. |* [DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/describebackups) |

## April 2025

|API |Release date |Change log |Related functions |
|---|---|---|---|
|新增 [ModifyDBEndpointProxyConfig](https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyDBEndpointProxyConfig) |2025\-04\-22 |New API. |[Editing connection endpoints](https://docs.byteplus.com/en/docs/RDS_for_PG/editing_connection_endpoints) |
|新增 [DescribeDBInstanceProxyParameters](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeDBInstanceProxyParameters) |||\- |
|新增 [DescribePlannedEvents](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribePlannedEvents) |||[Viewing operation and maintenance events](https://docs.byteplus.com/en/docs/RDS_for_PG/view_operation_and_maintenance_events) |
|更新 [CreateDatabase](https://docs.byteplus.com/en/docs/RDS_for_PG/createdatabase) ||Updated the description of the request parameter Owner to include the restriction that Owner cannot be designated as a super account with disabled DDL permission or a normal account with disabled DDL permission. |[Creating a database](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_a_database) |
|更新 [CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/CreateDBInstance) ||Updated the value range of request parameter DBEngineVersion, adding `PostgreSQL_17`. |[Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance) |
|更新 [CreateDBAccount](https://docs.byteplus.com/en/docs/RDS_for_PG/createdbaccount) ||Added optional request parameter NotAllowPrivileges. |[Creating an account](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_and_managing_an_account) |
|更新 [CreateSchema](https://docs.byteplus.com/en/docs/RDS_for_PG/createschema) ||Updated the description of the request parameter Owner to include the restriction that Owner cannot be designated as a super account with disabled DDL permission or a normal account with disabled DDL permission. |[Creating a schema](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_a_schema) |
|更新 [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances) ||Updated the value range of request parameter DBEngineVersion, adding `PostgreSQL_17`. |\- |
|更新 DescribeDBInstanceSpecs ||||
|更新 DescribeDBInstanceParameters ||Updated the return parameter DBEngineVersion value range to include `PostgreSQL_17`. ||
|更新 [ModifyDatabaseOwner](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydatabaseowner) ||Updated the description of the request parameter Owner to include the restriction that Owner cannot be designated as a super account with disabled DDL permission or a normal account with disabled DDL permission. |[Modifying the database owner](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_the_database_owner) |
|更新 [ModifyDBEndpointReadWeight](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbendpointreadweight) ||Added the request parameter WriteNodeHaltWriting. |[Setting read-write separation weight](https://docs.byteplus.com/en/docs/RDS_for_PG/setting_read-write_splitting_weights) |
|更新 [ModifyDBEndpointReadWriteFlag](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbendpointreadwriteflag) ||* Updated the descriptions of the request parameters ReadOnlyNodeMaxDelayTime and ReadOnlyNodeDistributionType.<br><br>* Add request parameters ReadWriteProxyConnection and WriteNodeHaltWriting. ||
|更新 [ModifySchemaOwner](https://docs.byteplus.com/en/docs/RDS_for_PG/modifyschemaowner) ||Updated the description of the request parameter SchemaInfoObject \> Owner, adding the restriction that Owner cannot be set as a super account or normal account with DDL permissions disabled. |[Modifying schema owner](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_schema_owner) |
|新增 Common structure \- PlannedEventsObject ||New common structure. |[DescribePlannedEvents](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribePlannedEvents) |
|更新 Common structure \- AccountObject ||Added parameter NotAllowPrivileges. |[DescribeDBAccounts](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbaccounts) |
| 更新 Common structure \- BasicInfoObject ||Updated the parameter DBEngineVersion value range, adding `PostgreSQL_17`. |[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancedetail) |
|更新 Common structure \- ChargeInfoObject ||Updated the parameter Number's value range. |* [CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/CreateDBInstance)<br><br>* [DescribeDBInstancePriceDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancepricedetail)<br><br>* [DescribeDBInstancePriceDifference](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancepricedifference)<br><br>* [RestoreToNewInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/restoretonewinstance) |
|更新 Common structure \- DatabaseObject ||Modified the description of parameter Owner. Added information that super accounts with DDL privileges disabled or normal accounts with DDL privileges disabled cannot be used as database owners. |[DescribeDatabases](https://docs.byteplus.com/en/docs/RDS_for_PG/describedatabases) |
|更新 Common structure \- EndpointObject ||Added parameters ReadWriteProxyConnection and WriteNodeHaltWriting. |* [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances)<br><br>* [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancedetail) |
| 更新 Common structure \- InstanceInfoObject ||* Updated the parameter DBEngineVersion value range, adding `PostgreSQL_17`.<br><br>* Added parameter Endpoints. |* [DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/describebackups)<br><br>* [DescribeDetachedBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/describedetachedbackups) |
|更新 Common structure \- InstanceObject ||Updated the parameter DBEngineVersion value range, adding `PostgreSQL_17`. |[DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances) |
|更新 Common structure \- InstanceSpecObject |||[DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancespecs) |
|更新 Common structure \- SchemaObject ||Modified the description of parameter Owner. Added information that super accounts with DDL privileges disabled or normal accounts with DDL privileges disabled cannot be used as schema owners. |* [DescribeSchemas](https://docs.byteplus.com/en/docs/RDS_for_PG/describeschemas)<br><br>* [ModifySchemaOwner](https://docs.byteplus.com/en/docs/RDS_for_PG/modifyschemaowner) |

## February 2025

|API |Release date |Change log |Related functions |
|---|---|---|---|
|更新 [CreateDatabase](https://docs.byteplus.com/en/docs/RDS_for_PG/createdatabase) |2025\-02\-19 |Updated request parameter Ctype to CType. |[Creating a database](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_a_database) |
|更新 [DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/describebackups) ||Updated return parameter StorageSpace type to Integer. |\- |
|更新 [DescribeDetachedBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/describedetachedbackups) ||||
|更新 [DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstanceparameters) ||* Updated the sample value of the request ParameterName.<br><br>* Updated the API return example.<br><br>* Added the descriptionZH field to the return parameters data structure. ||
|更新 [ModifyDBInstanceParameters](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbinstanceparameters) ||Removed the checkingCode, defaultValue, description, restart instance and type fields from the request parameter parameters data structure. |[Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_parameters) |
|更新 [DescribeSlots](https://docs.byteplus.com/en/docs/RDS_for_PG/describeslots) ||* Added the request parameter IPAddress.<br><br>* Added the IPAddress field to the return parameter ReplicationSlots data structure. |[Viewing replication slot list](https://docs.byteplus.com/en/docs/RDS_for_PG/view_replication_slot_list) |
|更新 [DeleteSlot](https://docs.byteplus.com/en/docs/RDS_for_PG/deleteslot) ||Updated interface precautions. |[Deleting replication slot](https://docs.byteplus.com/en/docs/RDS_for_PG/delete_replication_slot) |

## December 2024

|API |Release date |Change log |Related functions |
|---|---|---|---|
|更新 [CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/CreateDBInstance) |2024\-12\-11 |Updated request parameter DBEngineVersion value range, adding `PostgreSQL_15` and `PostgreSQL_16`. |[Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance) |
|更新 [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances) ||* Added notes to the API.<br><br>* Updated request parameter DBEngineVersion value range, adding `PostgreSQL_15` and `PostgreSQL_16`. |\- |
|更新 [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancedetail) ||Updated the value range of return parameter DBEngineVersion to include `PostgreSQL_15` and `PostgreSQL_16`. ||
|更新 [DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancespecs) ||* Added notes to the API.<br><br>* Updated request parameter DBEngineVersion value range, adding `PostgreSQL_15` and `PostgreSQL_16`. ||
|更新 [RestartDBInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/restartdbinstance) ||Updated the description of the request parameters ApplyScope and CustomNodeIds. |[Restarting an instance or read-only node(s)](https://docs.byteplus.com/en/docs/RDS_for_PG/restarting_an_instance) |
|更新 [DescribeDBInstancePriceDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancepricedetail) ||Updated description information for the parameter NodeOperateType. |\- |
|更新 [DescribeDBInstancePriceDifference](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancepricedifference) ||||
|更新 [ModifyDBInstanceChargeType](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbinstancechargetype) ||Updated the description of request parameter Period. |[Switch to Subscription](https://docs.byteplus.com/en/docs/RDS_for_PG/switching_to_subscription) |
|更新 [RemoveTagsFromResource](https://docs.byteplus.com/en/docs/RDS_for_PG/removetagsfromresource) ||Updated the description of the request parameter All. |[Disassociating a tag](https://docs.byteplus.com/en/docs/RDS_for_PG/disassociating_a_tag) |
|更新 [CreateDatabase](https://docs.byteplus.com/en/docs/RDS_for_PG/createdatabase) ||Updated the description of request parameter Owner. |[Creating a database](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_a_database) |
|更新 [DescribeDatabases](https://docs.byteplus.com/en/docs/RDS_for_PG/describedatabases) ||Updated the description for the DBName parameter. |\- |
|更新 [DescribeDBAccounts](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbaccounts) ||Updated the description for the AccountName field. ||
|更新 [DescribeSchemas](https://docs.byteplus.com/en/docs/RDS_for_PG/describeschemas) ||Updated the description for the DBName parameter. ||
|更新 [CreateDBEndpoint](https://docs.byteplus.com/en/docs/RDS_for_PG/createdbendpoint) ||Updated the description for the EndpointName parameter. |[Creating a connection endpoint](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_connection_endpoints) |
|更新 [ModifyDBInstanceConfig](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbinstanceconfig) ||Updated the description for the GlobalReadOnly parameter. |[Enabling global read-only](https://docs.byteplus.com/en/docs/RDS_for_PG/enabling_global_read-only) |
|更新 [ModifyDBEndpointReadWeight](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbendpointreadweight) ||Updated the value range of the ReadOnlyNodeDistributionType request parameter. |[Setting read-write separation weight](https://docs.byteplus.com/en/docs/RDS_for_PG/setting_read-write_splitting_weights) |
|更新 [ModifyDBEndpointReadWriteFlag](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbendpointreadwriteflag) ||Updated the description of the request parameter ReadWriteSpliting. ||
|更新 [ModifyDBEndpointAddress](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbendpointaddress) ||Added notes to the API. |* [Modifying private network access port](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_private_ports)<br><br>* [Modifying private network address prefix](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_a_private_address_prefix) |
|更新 [DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstanceparameters) ||* Updated the description of the request parameter ParameterName.<br><br>* Updated the value range of return parameter DBEngineVersion to include `PostgreSQL_15` and `PostgreSQL_16`. |\- |
|更新 [ModifyDBInstanceParameters](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbinstanceparameters) ||Updated the descriptions of the request parameter Type's value range and sample value. |[Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_parameters) |
|更新 [DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/describebackups) ||* Updated the descriptions of the request parameters BackupId, BackupStartTime, BackupEndTime, BackupStatus, and BackupType.<br><br>* Updated the value range of return parameter DBEngineVersion to include `PostgreSQL_15` and `PostgreSQL_16`. |\- |
|更新 [ModifyBackupPolicy](https://docs.byteplus.com/en/docs/RDS_for_PG/modifybackuppolicy) ||Updated description for request parameters BackupRetentionPeriod, FullBackupTime, FullBackupPeriod, IncrementBackupFrequency, and WALLogSpaceLimitEnable. |[Customizing backup policies](https://docs.byteplus.com/en/docs/RDS_for_PG/customizing_backup_policies) |
|更新 [DescribeDetachedBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/describedetachedbackups) ||Updated description for request parameters InstanceId, InstanceName, BackupStartTime, BackupEndTime, ProjectName, BackupStatus, BackupType. |\- |
|更新 [RestoreToNewInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/restoretonewinstance) ||Updated description information for the parameter NodeOperateType. |[Restoring to a new instanceRestoring to new instance](https://docs.byteplus.com/en/docs/RDS_for_PG/recovery_from_a_backup_set) |
|更新 [DescribeSlots](https://docs.byteplus.com/en/docs/RDS_for_PG/describeslots) ||Updated the description of the request parameters SlotName, SlotType, Plugin, Database, Temporary, SlotStatus. |\- |
|更新 [DeleteSlot](https://docs.byteplus.com/en/docs/RDS_for_PG/deleteslot) ||Updated the description of the request parameter All. |[Deleting replication slot](https://docs.byteplus.com/en/docs/RDS_for_PG/delete_replication_slot) |
|更新 [DescribeFailoverLogs](https://docs.byteplus.com/en/docs/RDS_for_PG/describefailoverlogs) ||Updated descriptions of request parameters QueryStartTime, QueryEndTime, and Context. ||
|更新 [CreateAllowList](https://docs.byteplus.com/en/docs/RDS_for_PG/createallowlist) ||Updated description information for request parameters AllowListName and AllowListDesc. |[Creating an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/adding_an_ip_address_allowlist) |
|更新 [ModifyAllowList](https://docs.byteplus.com/en/docs/RDS_for_PG/modifyallowlist) ||Updated description information for request parameters AllowListName, AllowListDesc, AllowList, ModifyMode, ApplyInstanceNum. |[Modifying an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_an_allowlist) |
|更新 [UnifyNewAllowList](https://docs.byteplus.com/en/docs/RDS_for_PG/unifynewallowlist) ||Updated description information for request parameters AllowListName and AllowListDesc. |[Merging allowlists](https://docs.byteplus.com/en/docs/RDS_for_PG/unifying_allowlists) |

## October 2024

|API |Release date |Change log |Related functions |
|---|---|---|---|
|更新 [DescribeBackupPolicy](https://docs.byteplus.com/en/docs/RDS_for_PG/describebackuppolicy) |2024\-10\-24 |Added return parameter WALLogSpaceLimitEnable. |[Configuring local remaining available space protection](https://docs.byteplus.com/en/docs/RDS_for_PG/configuring_local_remaining_space_protection) |
|更新 [ModifyBackupPolicy](https://docs.byteplus.com/en/docs/RDS_for_PG/modifybackuppolicy) ||Added request parameter WALLogSpaceLimitEnable. |[Customizing backup policies](https://docs.byteplus.com/en/docs/RDS_for_PG/customizing_backup_policies) |

## August 2024

|API |Release date |Change log |Related functions |
|---|---|---|---|
|更新 [CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/CreateDBInstance) |2024\-08\-28 |Updated descriptions of parameters VpcId and SubnetId, adding restrictions on value ranges. |[Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance) |
|更新 [RestoreToNewInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/restoretonewinstance) |||[Restore to new instance](https://docs.byteplus.com/en/docs/RDS_for_PG/recovery_from_a_backup_set) |

## July 2024

|API |Release date |Change log |Related functions |
|---|---|---|---|
|新增 [DescribeSlots](https://docs.byteplus.com/en/docs/RDS_for_PG/describeslots) |2024\-07\-30 |New API. |[Viewing replication slot list](https://docs.byteplus.com/en/docs/RDS_for_PG/view_replication_slot_list) |
|新增 [DeleteSlot](https://docs.byteplus.com/en/docs/RDS_for_PG/deleteslot) |||[Deleting replication slot](https://docs.byteplus.com/en/docs/RDS_for_PG/delete_replication_slot) |
|更新 [CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/CreateDBInstance) ||Updated the valid range for the parameter DBEngineVersion. |[Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance) |
|更新 [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances) |||\- |
|更新 [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances) ||||
|更新 [DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstanceparameters) ||Updated the return parameter DBEngineVersion value range. ||
|更新 [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancedetail) ||Updated the value range of parameter DBEngineVersion. ||
|更新 [DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/describebackups) ||||
|更新 [DescribeDetachedBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/describedetachedbackups) ||||

## June 2024

|API |Release date |Change log |Related functions |
|---|---|---|---|
|更新 ModifyDBEndpointAddress |2024\-06\-20 |Updated API to add usage restrictions. |* [Modifying private network address prefix](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_a_private_address_prefix)<br><br>* [Modifying private network access port](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_private_ports) |
|更新 RestartDBInstance |2024\-06\-12 |Updated API to add fields related to restarting specified read\-only nodes. |[Restarting an instance or read-only node(s)](https://docs.byteplus.com/en/docs/RDS_for_PG/restarting_an_instance) |

## April 2024

|API |Release date |Change log |Related functions |
|---|---|---|---|
|新增 DescribeAllowLists |2024\-04\-25 |New API. |[Managing allowlists (new version)](https://docs.byteplus.com/en/docs/RDS_for_PG/Allowlist_management) |
|新增 DescribeAllowListDetail ||||
|新增 CreateAllowList |||[Creating an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/adding_an_ip_address_allowlist) |
|新增 ModifyAllowList |||[Modifying an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_an_allowlist) |
|新增 AssociateAllowList |||[Associating with an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/associating_an_allowlist) |
|新增 DisassociateAllowList |||[Disassociating with allowlists](https://docs.byteplus.com/en/docs/RDS_for_PG/disassociating_an_allowlist) |
|新增 DeleteAllowList |||[Deleting an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/deleting_an_allowlist) |
|新增 UnifyNewAllowList |||[Merging allowlists](https://docs.byteplus.com/en/docs/RDS_for_PG/unifying_allowlists) |
|新增 UpgradeAllowListVersion |||[Upgrading allowlist](https://docs.byteplus.com/en/docs/6438/1182632) |
