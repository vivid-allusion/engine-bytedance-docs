---
title: "SDK release history"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/sdk_release_notes"
---

<span id=".XzIwMjUtMDItMDfvvIjmlrDlop7vvIk="></span>
## June 2026

Released SDKs for Python (v5.0.36), GO (v1.2.37), and Java (v2.0.14). This release includes the following updates:


|**Change type** |**API** |**Change log** |
|---|---|---|
|Modify |[CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbinstance1) |* Added the optional request parameter AutoUpgradeMinorVersion.<br><br>* Updated the description for the request parameter DBEngineVersion.<br><br>* Updated the description of the return parameter DBEngineVersion. |
|Modify |[DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) |* Updated the description for the request parameter DBEngineVersion.<br><br>* Updated the description of the return parameter DBEngineVersion. |
|Modify |[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancedetail) |Updated the description of the return parameter DBEngineVersion. |
|Modify |[DescribeDBInstanceAttribute](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBInstanceAttribute) |Updated the description of the return parameter DBEngineVersion. |
|Modify |[DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancespecs) |* Updated the description for the request parameter DBEngineVersion.<br><br>* Updated the description of the return parameter DBEngineVersion. |
|Modify |[DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstanceparameters) |Added the response parameters TemplateId, TemplateName, and TemplateSource. |
|Modify |[DescribeDBInstanceParametersLog](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstanceparameterslog) |Added the response parameters TemplateId, TemplateName, and TemplateSource. |
|Modify |[ModifyDBInstanceChargeType](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstancechargetype) |Updated the description of request parameter InstanceId, supplemented the limit that a maximum of 20 instance IDs can be filled in. |
|Modify |[DeleteDBNodes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedbnodes)<br><br> |* Updated the description of request parameter DBNodeIds, added the first note.<br><br>* Updated the descriptions of the request parameters SwitchType, SpecifiedSwitchStartTime, and SpecifiedSwitchEndTime. |
|Modify |[ModifyDBInstanceType](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstancetype) |* Updated the description of request parameter TypeConvertPath, added the value SingleToDouble: convert single\-node instance type to double\-node instance.<br><br>* Updated the description of parameter NodeOperateType in the request structure NodeInfoObject, added the third note. |
|Modify |[UpgradeDBInstanceEngineMinorVersion](https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgradedbinstanceengineminorversion) |* Updated the description of request parameter SpecifiedSwitchStartTime, added the second note.<br><br>* Updated the description of request parameter SpecifiedSwitchEndTime, added the third note. |
|Modify |[CreateDrDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdrdbinstance) |* Added notes for calling the API to create disaster recovery instances.<br><br>* Added the optional request parameter AutoUpgradeMinorVersion. |
|Modify |[UpgradeDBInstanceEngineMajorVersionPrecheck](https://docs.byteplus.com/en/docs/RDS_for_MySQL/UpgradeDBInstanceEngineMajorVersionPrecheck) |* Updated the example value and description of request parameter TargetMajorVersion (8.0.32 → 8.0.43).<br><br>* Updated the descriptions of the request parameters SwitchType, SpecifiedSwitchStartTime, and SpecifiedSwitchEndTime. |
|Modify |[DescribeUpgradeEngineMajorVersionPrecheckResult](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeUpgradeEngineMajorVersionPrecheckResult) |Updated the example value and description of response parameter TargetMajorVersion (8.0.32 → 8.0.43).<br><br> |
|Modify |[StopDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/stopdbinstance) |Added notes for calling the API to stop instances. |
|Modify |[DescribeDBInstanceNodes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancenodes) |* Updated the description of response parameter NodeStatus, added the value InOperation: under maintenance lock.<br><br>* Updated the description of response parameter SpaceUsedPercentage, added notes. |
|Modify |[CreateDBBlueGreenInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/CreateDBBlueGreenInstance) |* Added notes for calling the API to create blue\-green instances.<br><br>* Added the optional request parameter AutoUpgradeMinorVersion.<br><br>* Updated the description of request parameter InstanceName, added notes.<br><br>* Updated the description of request parameter DBParamGroupId, added notes.<br><br>* Updated the description of request parameter ProxyNodeCustom, added the second and third notes. |
|Modify |[SwitchDBPrecheckBlueGreen](https://docs.byteplus.com/en/docs/RDS_for_MySQL/SwitchDBPrecheckBlueGreen) |Updated the request type of the API from "Sync request" to "Async request". |
|Modify |[DeleteDBBlueGreenRelation](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DeleteDBBlueGreenRelation) |Updated the request type of the API from "Sync request" to "Async request". |
|Modify |[CreateDBEndpoint](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbendpoint) |* Added notes for the API: multi\-node instances only support creating 3 custom read\-write direct endpoints.<br><br>* Updated the description of request parameters ConnectionPoolType, ReadWriteSpliting, ReadOnlyNodeDistributionType, ReadOnlyNodeWeight, ReadOnlyNodeMaxDelayTime, MultiStatementsMode, OverloadProtection, MasterProtectorTimeout, MasterNodeRouting, ImplicitTransSplit and EnableConnectionPersistent, added notes. |
|Modify |[ModifyDBEndpoint](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbendpoint) |* Added notes for the API.<br><br>* Updated the description of request parameter Description, supplemented the field length limit. |
|Modify |[DescribeDBProxyConfig](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbproxyconfig) |Updated the description of response parameter DBProxyStatus, added the value Updating: proxy is being modified. |
|Modify |[DeleteDBEndpoint](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedbendpoint) |Updated interface precautions. |
|Modify |[ModifyReadOnlyNodeDelayReplicationTime](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifyreadonlynodedelayreplicationtime) |Updated the notes for the API, added the second note. |
|Modify |[ModifyDBProxy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbproxy) |* Updated the notes for the API, added the fourth note.<br><br>* Updated the request parameter EnableDBProxy to be required. |
|Modify |[ModifyDBProxySpec](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbproxyspec) |* Updated the notes for the API, added the second note.<br><br>* Updated the descriptions of the request parameters SwitchType, SpecifiedSwitchStartTime, and SpecifiedSwitchEndTime. |
|Modify |[AddDiagnosticsEntity](https://docs.byteplus.com/en/docs/RDS_for_MySQL/adddiagnosticsentity) |Updated the description of request parameters EcsInstanceIds and PublicIpAddresses, added the second note. |
|Modify |[CreateBackup](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createbackup1) |* Updated interface precautions.<br><br>* Updated the descriptions of the request parameters BackupMethod, BackupType, and BackupMeta. |
|Modify |[RestoreToNewInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/restoretonewinstance) |* Updated interface precautions.<br><br>* Added the optional request parameter AutoUpgradeMinorVersion. |
|Modify |[RestoreToExistedInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/restoretoexistedinstance) |Added notes for the API. |
|Modify |[DeleteDataBackup](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedatabackup) |Added notes for the API. |
|Modify |[DescribeResourcePackageDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeResourcePackageDetail) |Updated the description of request parameter QueryStartTime, added notes. |
|Modify |[CreateResourcePackage](https://docs.byteplus.com/en/docs/RDS_for_MySQL/CreateResourcePackage) |* Added notes for the API.<br><br>* Updated the request parameters PeriodUnit and Period to be required. |
|Modify |[ListResourcePackages](https://docs.byteplus.com/en/docs/RDS_for_MySQL/ListResourcePackages) |Updated the descriptions of the request parameters PageSize and OrderBy. |
|Modify |[ModifyDBInstanceSpec](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstancespec1) |Updated the descriptions of the request parameters SwitchType, SpecifiedSwitchStartTime, and SpecifiedSwitchEndTime. |
|Modify |[ModifyDBNodeTemporarySpec](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbnodetemporaryspec) |Updated the descriptions of the request parameters SwitchType, SpecifiedSwitchStartTime, and SpecifiedSwitchEndTime. |
|Modify |[ModifyDBNodeSpec](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbnodespec) |Updated the descriptions of the request parameters SwitchType, SpecifiedSwitchStartTime, and SpecifiedSwitchEndTime. |
|Modify |[CreateDBNodes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbnodes) |Updated the descriptions of the request parameters SwitchType, SpecifiedSwitchStartTime, and SpecifiedSwitchEndTime. |
|Modify |[MigrateToOtherZone](https://docs.byteplus.com/en/docs/RDS_for_MySQL/migratetootherzone) |Updated the descriptions of the request parameters SwitchType, SpecifiedSwitchStartTime, and SpecifiedSwitchEndTime. |
|Modify |[RestartDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/restartdbinstance1) |Updated the descriptions of the request parameters SwitchType, SpecifiedSwitchStartTime, and SpecifiedSwitchEndTime. |
|Modify |[SwitchDBBlueGreen](https://docs.byteplus.com/en/docs/RDS_for_MySQL/SwitchDBBlueGreen) |Updated the descriptions of the request parameters SwitchType, SpecifiedSwitchStartTime, and SpecifiedSwitchEndTime. |
|Modify |[ModifyDBProxySpec](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbproxyspec) |Updated the descriptions of the request parameters SwitchType, SpecifiedSwitchStartTime, and SpecifiedSwitchEndTime. |
|Modify |[ModifyDBInstanceSSL](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstancessl) |Updated the descriptions of the request parameters SwitchType, SpecifiedSwitchStartTime, and SpecifiedSwitchEndTime. |
|Modify |[ModifyDBInstanceTDE](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstancetde) |Updated the descriptions of the request parameters SwitchType, SpecifiedSwitchStartTime, and SpecifiedSwitchEndTime. |


<span id="iGK96jKM"></span>
## March 2026

Released SDKs for Python (v5.0.19), GO (v1.2.21), and Java (v1.0.16). This release includes the following updates:


|**Change type** |**API** |**Change log** |
|---|---|---|
|Create |[DescribeNonWhiteSessionList](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeNonWhiteSessionList) |Add an API. |
|Create |[CleanNonWhiteSession](https://docs.byteplus.com/en/docs/RDS_for_MySQL/CleanNonWhiteSession) |Add an API. |
|Create |[RebuildDBGreenInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/RebuildDBGreenInstance) |Add an API. |
|Modify |[CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbinstance1) |Added the optional request parameter PrivateIpAddress. |
|Modify |[RebuildDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/rebuilddbinstance) |Added the optional request parameter PrivateIpAddress. |
|Modify |[CreateDrDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdrdbinstance) |Added the optional request parameter PrivateIpAddress. |
|Modify |[CreateDBBlueGreenInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/CreateDBBlueGreenInstance) |Added the optional request parameter PrivateIpAddress. |
|Modify |[RestoreToNewInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/restoretonewinstance) |Added the optional request parameter PrivateIpAddress. |
|Modify |[DescribeDBInstanceHAConfig](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBInstanceHAConfig) |Added the response parameter AutoStorageScalingConfig. |
|Modify |[CreateDBAccount](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbaccount) |Added the optional request parameter AuthenticationType. |
|Modify |[DescribeAllowLists](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeallowlists1) |Updated the description of the DescribeAllowLists request parameter. |
|Modify |[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeallowlistdetail1) |Added the response parameter ProjectName. |
|Modify |[DescribeBackupPolicy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackuppolicy) |Added the response parameter LockDDLTimeSecond. |
|Modify |[ModifyBackupPolicy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifybackuppolicy) |* Added the request parameter LockDDLTimeSecond.<br><br>* Added the response parameter LockDDLTimeSecond.<br><br>* Updated the description of the request parameter LockDDLTime. |
|Modify |[ModifyDBInstanceParameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstanceparameters) |Added the request parameter TemplateId. |
|Modify |[SaveAsParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_MySQL/saveasparametertemplate1) |* Added the request parameter ProjectName.<br><br>* Added the response parameter TemplateId. |
|Create |Common structure \- AutoStorageScalingConfigObject |Add a new struct. |
|Modify |Common structure \- AccountObject |Added the AuthenticationType parameter. |
|Modify |Common structure \- TemplateInfoObject |Adds the parameter ProjectName. |
|Modify |Public struct \- AllowListObject |Adds the parameter ProjectName. |


<span id="0LPK3fne"></span>
## December 2025

Released SDKs for Python (v4.0.42), Go (v1.1.54), and Java (v0.2.53). This release includes the following updates:


|**Change type** |**API** |**Change log** |
|---|---|---|
|Modify |[CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbinstance1) |* Updated the description of the StorageSpace request parameter (GB \> GiB).<br><br>* Added the request parameters EnableExternalReplication and EngineType. |
|Modify |[DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) |Added the request parameter EngineType. |
|Modify |[DescribeResourceUsage](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeResourceUsage) |Updated the descriptions of the response parameters BackupFreeQuotaSize, BackupUse, StorageSpace, and StorageUse (GB \> GiB). |
|Modify |[DescribeDBInstancePriceDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancepricedetail) |Updated the descriptions of the response parameters BackupFreeQuotaSize, BackupUse, StorageSpace, and StorageUse (GB \> GiB). |
|Modify |[ModifyDBNodeSpec](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbnodespec) |Updated the descriptions of the response parameters BackupFreeQuotaSize, BackupUse, StorageSpace, and StorageUse (GB \> GiB). |
|Modify |[ModifyDBInstanceType](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstancetype) |Added a note: changing a single\-node instance to a double\-node instance. |
|Modify |[RestartDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/restartdbinstance1) |Added the request parameter RestartWithProxy. |
|Modify |[RebuildDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/rebuilddbinstance) |Updated the description of the request parameter StorageSpace (GB \> GiB). |
|Modify |[CreateDrDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdrdbinstance) |Updated the description of the request parameter StorageSpace (GB \> GiB). |
|Modify |[CreateDBAccount](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbaccount) |* Updated the description for the request parameter AccountPassword (updated special characters).<br><br>* Updated the description of the request parameter DryRun (added a second note). |
|Modify |[ResetDBAccount](https://docs.byteplus.com/en/docs/RDS_for_MySQL/resetdbaccount) |Updated the description for the request parameter AccountPassword (updated special characters). |
|Modify |[GrantDBAccountPrivilege](https://docs.byteplus.com/en/docs/RDS_for_MySQL/grantdbaccountprivilege) |Updated the description of the request parameter DryRun (added a second note). |
|Modify |[DeleteDatabase](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedatabase1) |Added the request parameter KeepAccountPrivileges. |
|Modify |[DescribeAllowLists](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeallowlists1) |Updated the description of the request parameter RegionId with additional explanations. |
|Modify |[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeallowlistdetail1) |* Added the response parameter ProjectName.<br><br>* Updated the description of the response parameter SecurityGroupBindInfos (added new descriptive content). |
|Modify |[DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackups) |* Updated the description of the request parameter StorageSpace (GB \> GiB).<br><br>* Added the request parameter EnableExternalReplication. |
|Modify |[DescribeRecoverableTime](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describerecoverabletime1) |Updated the description of the returned parameter RecoverableTimeInfo (+0800 \> UTC time). |
|Modify |[DescribeBackupPolicy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackuppolicy) |* Updated the description of the return parameter BinlogSpaceLimitEnable (GB \> GiB).<br><br>* Updated the description of the return parameter DataKeepDaysAfterReleased (deleted the content related to "Currently, only a value of `7` is supported.").<br><br>* Updated the description of the return parameter LockDDLTime (deleted the description).<br><br>* Added the new return parameter LockDDLTimeSecond. |
|Modify |[ModifyBackupPolicy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifybackuppolicy) |* Updated the description of the `BinlogSpaceLimitEnable` request parameter (GB \> GiB).<br><br>* Updated the description of the `LockDDLTime` request parameter (deleted the descriptive content).<br><br>* Added the `LockDDLTimeSecond` request parameter.<br><br>* Updated the description of the `BinlogSpaceLimitEnable` response parameter (GB \> GiB).<br><br>* Updated the description of the `DataKeepDaysAfterReleased` response parameter (deleted content related to "Currently, only the value `7` is supported.").<br><br>* Added the `LockDDLTimeSecond` response parameter. |
|Modify |[ModifyDBInstanceParameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstanceparameters) |* Updated the description of the TemplateId request parameter.<br><br>* Added an example value for the request parameter TemplateId. |
|Modify |[CreateParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createparametertemplate1) |Added the request parameter EngineType. |
|Modify |[ListParameterTemplates](https://docs.byteplus.com/en/docs/RDS_for_MySQL/listparametertemplates1) |Added the request parameter EngineType. |
|Modify |[SaveAsParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_MySQL/saveasparametertemplate1) |* Added the request parameter ProjectName.<br><br>* Changed the display status of the return parameter from hidden to displayed. |
|Modify |[CreateResourcePackage](https://docs.byteplus.com/en/docs/RDS_for_MySQL/CreateResourcePackage) |Updated the description of the request parameter EffectiveTime (added format content). |
|Modify |Common structure \- InstanceInfoObject |* Updated the description of the StorageSpace parameter (GB \> GiB).<br><br>* Added the EngineType parameter. |
|Modify |Common structure \- DBInstanceAttribute |* Updated the description of the Memory parameter (GB \> GiB).<br><br>* Updated the description of the StorageSpace parameter (GB \> GiB).<br><br>* Added the EngineType parameter. |
|Modify |Common structure \- AutoStorageScalingConfigObject |Updated the description for the StorageUpperBound parameter (GB \> GiB). |
|Modify |Common structure \- NodeDetailInfoObject |Updated the description of the Memory parameter (GB \> GiB). |
|Modify |Public structure \- InstanceSpecsInfoObject |Updated the descriptions for the Memory, StorageMax, StorageMin, and StorageStep parameters (GB \> GiB). |
|Modify |Common structure \- AutoStorageScalingConfig |Updated the description of the request parameter StorageUpperBound (GB \> GiB). |
|Modify |Common structure \- ChargeItemPriceObject |Updated the description of the parameter ChargeItemValue (GB \> GiB). |
|Modify |Common structure \- NodeDetailInfoObject |* Updated the description of the Memory parameter (GB \> GiB).<br><br>* Updated the description of the UpdateTime parameter (added a time format). |
|Modify |Public struct \- AllowListObject |* Updated the example value for the `ProjectName` parameter (from empty to default) and added new information to its description.<br><br>* Added new information to the description of the `SecurityGroupBindInfos` parameter. |
|Modify |Common structure \- BackupObject |Added the EngineType parameter. |
|Modify |Common structure \- RecoverableTimeInfoObject |* Updated the description of the `EarliestRecoverableTime` parameter: changed +0800 to UTC time and added format content.<br><br>* Updated the description of the `LatestRecoverableTime` parameter: changed +0800 to UTC time and added format content. |
|Modify |Common structure \- UsageStat |Updated the description of the StatTime parameter (added format details). |
|Modify |Common structure \- DeletedDBInstanceInfo |* Updated the description of the parameter BackupExpirationTime (added format content).<br><br>* Updated the description of the parameter DeletionTime (added format content).<br><br>* Updated the description of the parameter StorageSpace (GB \> GiB). |
|Modify |Common structure \- ParameterTemplateInfo |* Updated the description of the CreateTime parameter to include format information.<br><br>* Updated the description of the ProjectName parameter by adding explanatory notes.<br><br>* Added the request parameter EngineType. |
|Modify |Common structure \- TaskInfoObject |* Updated the description for the CreateTime parameter to include format information.<br><br>* Updated the description for the FinishTime parameter to include format information. |


<span id="sd5Y6Of4"></span>
## September 2025

Released SDKs for Python (v4.0.21), Go (v1.1.35), and Java (v0.2.35). This release includes the following updates:


|**Change type** |**API** |**Change log** |
|---|---|---|
|Create |[DescribeDBInstanceAttribute](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBInstanceAttribute) |Add an API. |
|Create |[DescribeDBInstanceEndpoints](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBInstanceEndpoints) |Add an API. |
|Create |[DescribeResourceUsage](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeResourceUsage) |Add an API. |
|Create |[DescribeDBInstanceChargeDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBInstanceChargeDetail) |Add an API. |
|Create |[DescribeDBInstanceHAConfig](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBInstanceHAConfig) |Added a new API. |
|Create |[DescribeDBProxy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBProxy) |Add an API. |
|Create |[DescribeDBDisasterRecoveryInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBDisasterRecoveryInstances) |Add an API. |
|Create |[StopDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/stopdbinstance) |Added a new API. |
|Create |[StartDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/startdbinstance) |Add API. |
|Create |[ModifyBackupName](https://docs.byteplus.com/en/docs/RDS_for_MySQL/ModifyBackupName) |Added the ModifyBackupName API to modify the name of a data backup. This API includes the following required parameters:<br><br><br>* InstanceId: Instance ID<br><br>* BackupId: The ID of the data backup<br><br>* BackupName: The backup name. The naming rules are as follows:<br><br>   * Cannot start with a hyphen (\-)<br><br>   * Can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-)<br><br>   * The length must be between 1 and 128 characters |
|Modify |[CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbinstance1) |* Added the SingleNode option to the InstanceType parameter, and provided an explanation on selecting `Blue instance` and `Green instance` types.<br><br>* Added an explanation for the StorageType parameter: when InstanceType is set to SingleNode, StorageType can only be CloudESSD_FlexPL or CloudESSD_PL0.<br><br>* Added an explanation for the NodeSpec parameter in NodeInfoObject: if the value of StorageType is CloudESSD_FlexPL or CloudESSD_PL0, NodeSpec must be of the `General type`.<br><br>* Added a note to the description of the ProxyNodeCustom parameter indicating that it does not take effect for instances of the SingleNode type. |
|Modify |[DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) |* Added a restriction to the StorageType parameter: when InstanceType is set to SingleNode, StorageType can only be CloudESSD_FlexPL or CloudESSD_PL0.<br><br>* Added SingleNode (Single node type) as a value for the InstanceType parameter and added a prompt for instance type selection.<br><br>* Added the EipLocked parameter to AddressObject to indicate whether the EIP used by the connection endpoint is shut down due to overdue payments. |
|Modify |[DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancespecs) |* Added the SingleNode (single\-node type) option to the InstanceType parameter and added instructions for selecting instance types for blue and green instances.<br><br>* Added a restriction to the StorageType parameter: when InstanceType is set to SingleNode, StorageType can only be CloudESSD_FlexPL or CloudESSD_PL0.<br><br>* Removed the reference to the CreateDBBlueGreenInstance API from the restrictions of the StorageType parameter. |
|Modify |[DescribeDBInstancePriceDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancepricedetail) |* Added CloudESSD_FlexPL (Cloud ESSD FlexPL) and CloudESSD_PL0 (Cloud ESSD PL0) to the value range of the StorageType parameter, and provided details about the value rules of this parameter for different API operations.<br><br>* Added the response parameter HidePriceInfo to control whether to hide price information. When set to true, price information is displayed as \*\*\*.<br><br>* Added a restriction to the StorageType parameter: If InstanceType is set to SingleNode, StorageType can only be CloudESSD_FlexPL or CloudESSD_PL0.<br><br>* Added a restriction to the NodeSpec parameter: if StorageType is CloudESSD_FlexPL or CloudESSD_PL0, NodeSpec can only be a general type.<br><br>* Removed the restriction on the StorageType parameter of the CreateDBBlueGreenInstance API. |
|Modify |[ModifyDBNodeTemporarySpec](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbnodetemporaryspec) |Added a prompt to the description of the NodeSpec parameter in NodeInfoObject: If StorageType is set to CloudESSD_FlexPL or CloudESSD_PL0, only the General type can be passed for NodeSpec. |
|Modify |[ModifyDBNodeSpec](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbnodespec) |* Added CloudESSD_FlexPL and CloudESSD_PL0 to the value range of the StorageType parameter, and detailed the usage restrictions and change rules across different interfaces.<br><br>* Expanded the description of the StorageType parameter from "Instance storage type. The value is LocalSSD (local SSD disk)" to an explanation that includes multiple storage types and detailed usage rules.<br><br>* A new restriction is added to the StorageType parameter: When InstanceType is set to SingleNode, StorageType can only be set to CloudESSD_FlexPL or CloudESSD_PL0.<br><br>* A new restriction is added to the NodeSpec parameter: If StorageType is set to CloudESSD_FlexPL or CloudESSD_PL0, NodeSpec only supports specifications of the general type. |
|Modify |[CreateDBNodes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbnodes) |A new restriction is added to the NodeSpec parameter: If StorageType is set to CloudESSD_FlexPL or CloudESSD_PL0, NodeSpec only supports specifications of the general type. |
|Modify |[MigrateToOtherZone](https://docs.byteplus.com/en/docs/RDS_for_MySQL/migratetootherzone) |Added a restriction on the storage type to the description of the NodeSpec parameter: when StorageType is set to CloudESSD_FlexPL or CloudESSD_PL0, NodeSpec can only be set to the general type. |
|Modify |[RestartDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/restartdbinstance1) |Added the ForceRestartMaster parameter to control whether to perform a force restart. When the instance is a single\-node instance, this parameter must be set to true. |
|Modify |[RebuildDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/rebuilddbinstance) |* The description of the StorageType parameter is updated, its value range is expanded to include CloudESSD_FlexPL and CloudESSD_PL0, and the usage rules for different APIs are specified in detail.<br><br>* Added a restriction to the StorageType parameter: If InstanceType is set to SingleNode, StorageType can only be CloudESSD_FlexPL or CloudESSD_PL0.<br><br>* Added a restriction to the NodeSpec parameter: If you set StorageType to CloudESSD_FlexPL or CloudESSD_PL0, you can specify only the general type for NodeSpec. |
|Modify |[DeleteDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedbinstance1) |* Added the KeepCrossBackupEnableAfterReleased parameter to control whether to retain cross\-regional backups. The value can be true or false. Volume instances do not support this feature.<br><br>* Added the value range to the description of the DataKeepDays parameter. The value can range from 7 to 3650 days, with a default of 7 days. |
|Modify |[UpgradeDBInstanceEngineMinorVersion](https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgradedbinstanceengineminorversion) |* Added the ObservationHours parameter to set the observation duration after an instance upgrade. The value can be an integer from 0 to 72. The unit is hours. The default value is 0.<br><br>* Removed the information about the impact of the EstimateOnly value from the description of the PreparedMinutes parameter. |
|Modify |[CreateDrDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdrdbinstance) |* Added the StorageType parameter to specify the instance storage type. Valid values are LocalSSD (local disk), CloudESSD_FlexPL (Cloud ESSD FlexPL), or CloudESSD_PL0 (Cloud ESSD PL0). This parameter is required when setting StorageSpace and has different value ranges and usage limits across different APIs.<br><br>* Removed the AutoStorageScalingConfig parameter. Configuring automatic storage expansion for instances is no longer supported.<br><br>* Added a note to the description of the NodeSpec parameter in NodeInfoObject. If StorageType is set to CloudESSD_FlexPL or CloudESSD_PL0, NodeSpec can only be set to the general type. |
|Modify |[DescribeDBProxyPriceDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbproxypricedetail) |* Added the return parameter HidePriceInfo to control whether to hide price information. When this parameter is set to true, the price information is replaced with \*\*\*.<br><br>* Added the StoragePackage billing item type to the ChargeItemType parameter of ChargeItemPriceObject to indicate a storage plan.<br><br>* Updated the description of the ChargeItemValue parameter of ChargeItemPriceObject to include the StoragePackage type, which indicates the resource plan size in GB. |
|Modify |[CreateDBEndpoint](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbendpoint) |* Added the CustomRouteStrategy parameter to set the SQL forwarding rules for the connection endpoint.<br><br>* Added a prompt to the description of the ConnectionPoolType parameter: Single\-node instances do not support this feature.<br><br>* Added a prompt to the description of the ReadOnlyNodeDistributionType parameter: Single\-node instances do not support this feature.<br><br>* Added a prompt to the description of the MultiStatementsMode parameter: Single\-node instances do not support this feature. |
|Modify |[ModifyDBEndpoint](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbendpoint)<br><br> |* Added the CustomRouteStrategy parameter for customizing forwarding rules. It includes the KeywordRouteStrategy sub\-parameter, which supports setting keywords and target nodes for SQL forwarding rules.<br><br>* Added a note to the prompt for the AutoAddNewNodes parameter: This feature is not supported for single\-node instances.<br><br>* Added a note to the prompt for the ReadWriteSpliting parameter: This feature is not supported for single\-node instances.<br><br>* Added a note to the prompt for the ReadOnlyNodeDistributionType parameter: This feature is not supported for single\-node instances.<br><br>* Added a note to the prompt for the IdleConnectionReclaim parameter: This feature is not supported for single\-node instances.<br><br>* Added a note to the prompt for the ConnectionPoolType parameter: This feature is not supported for single\-node instances.<br><br>* Added a note to the prompt message for the MultiStatementsMode parameter: This feature is not supported for single\-node instances.<br><br>* Added a note to the prompt message for the OverloadProtection parameter: This feature is not supported for single\-node instances.<br><br>* Added a note to the prompt message for the MasterNodeRouting parameter: This feature is not supported for single\-node instances. |
|Modify |[ModifyDBEndpointConnectionMode](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbendpointconnectionmode) |* Added the CustomRouteStrategy parameter for setting SQL forwarding rules for connection endpoints.<br><br>* Added the KeywordRouteStrategy parameter to define the configurations for SQL forwarding rules, including targets and keyword settings. |
|Modify |[CreateBackup](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createbackup1) |* Updated the description of the BackupMethod parameter to specify that only Snapshot backup is supported when the instance storage type is Volume and to differentiate the backup types for local disks and Volumes.<br><br>* Updated the description of the BackupType parameter to specify that the backup method can only be Full when the backup type is Snapshot, and to further clarify the backup methods that correspond to different backup types.<br><br>* Added the BackupName parameter to set the backup name. Naming rules are as follows:<br><br>   * Cannot start with a hyphen (\-).<br><br>   * It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>   * The length must be between 1 and 128 characters.<br><br>   * If a backup name is not set, the backup ID is used as the backup name. |
|Modify |[DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackups) |* Added Snapshot as a value for the BackupMethod parameter, which indicates the snapshot backup type.<br><br>* Added the Snapshot value to the BackupMethod parameter in BackupObject for consistency with the request parameter.<br><br>* A new request parameter, BackupName, is added to query backups by a specified name.<br><br>* A new field, BackupName, is added to the BackupObject response parameter to return the name of the backup. |
|Modify |[RestoreToNewInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/restoretonewinstance) |* Added CloudESSD_FlexPL and CloudESSD_PL0 to the value range of the StorageType parameter and detailed its value range restrictions across different interfaces.<br><br>* Added rules for the StorageType parameter regarding storage type changes. This specifies that changes are not supported if the original instance's storage type is LocalSSD or CloudESSD_FlexPL, and outlines the changeable options if the storage type is CloudESSD_PL0.<br><br>* Added a restriction to the description of the StorageType parameter for when InstanceType is set to SingleNode: When InstanceType is set to SingleNode, StorageType can only be set to CloudESSD_FlexPL or CloudESSD_PL0.<br><br>* A restriction is added to the description of the NodeSpec parameter for when StorageType is set to CloudESSD_FlexPL or CloudESSD_PL0: if StorageType is set to CloudESSD_FlexPL or CloudESSD_PL0, NodeSpec can only be set to the general type. |
|Modify |[DescribeBackupPolicy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackuppolicy) |* Added the HighFrequencySnapshotBackupEnable parameter to control the status of the high\-frequency incremental snapshot backup feature for volume instances.<br><br>* Added the HighFrequencySnapshotBackupSecondPeriod parameter to set the frequency of high\-frequency incremental snapshot backups in seconds.<br><br>* Added the prompt "This feature is not currently supported for volume instances" to the description of the DataBackupEncryptionEnabled parameter.<br><br>* The description of the DataBackupRetentionDay parameter is expanded to differentiate the number of days to retain backups for local disk instances (7 to 3650 days) and volume instances (currently only 7 days).<br><br>* The description of the DataIncrBackupPeriods parameter is updated to include "local disk instances".<br><br>* The description of the HourlyIncrBackupEnable parameter is updated to include "local disk instances".<br><br>* The description of the IncrBackupHourPeriod parameter is updated to include "local disk instances".<br><br>* The description of the LogBackupRetentionDay parameter has been expanded to specify different ranges for the number of days to retain backups for local disk and cloud volume instances: 7 to 3650 days for local disk instances and 7 to 720 days for cloud volume instances.<br><br>* The prompt for the HighFrequencySnapshotBackupSecondPeriod parameter is modified to: "When the value of HighFrequencySnapshotBackupEnable is false, the value of this field is 0".<br><br>* Added the return parameter KeepCrossBackupEnableAfterReleased to control whether to retain the cross\-regional backup when releasing an instance. Values include true (Yes) and false (No). |
|Modify |[ModifyBackupPolicy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifybackuppolicy) |* Updated the descriptions for the IncrBackupHourPeriod and LockDDLTime request parameters.<br><br>* Added the HighFrequencySnapshotBackupEnable parameter to control whether to enable the high\-frequency incremental snapshot backup feature.<br><br>* Added the HighFrequencySnapshotBackupSecondPeriod parameter to set the frequency (in seconds) for high\-frequency incremental snapshot backups. Valid values are 3600 (Every 1 hour), 7200 (Every 2 hours), 10800 (Every 3 hours), 14400 (Every 4 hours), 19200 (Every 6 hours), 28800 (Every 8 hours), and 38400 (Every 12 hours).<br><br>* Updated the description of the DataBackupRetentionDay parameter to differentiate the range for the number of days to retain backups for local disk instances and volume\-based instances:<br><br>   * Local disk instances: 7 to 3650 days.<br><br>   * Cloud disk instances: 7 days only.<br><br>* Updated the description of the LogBackupRetentionDay parameter to clarify the different ranges for log backup retention days on local and cloud disk instances:<br><br>   * Local disk instances: 7 to 3650 days.<br><br>   * Cloud disk instances: 7 to 720 days.<br><br>* Updated the description of the HourlyIncrBackupEnable parameter to clarify that this feature applies only to local disk instances.<br><br>* Updated the description of the IncrBackupHourPeriod parameter to clarify that this feature applies only to local disk instances.<br><br>* Updated the descriptions for the DataBackupEncryptionEnabled and BinlogBackupEncryptionEnabled parameters to include a note that this feature is not supported for cloud disk instances.<br><br>* Added the KeepCrossBackupEnableAfterReleased parameter to specify whether to retain cross\-regional backups. This feature is currently available only for instances that use local disks.<br><br>* Added the KeepCrossBackupEnableAfterReleased field to the response parameters to display the retention status of cross\-regional backups. |
|Modify |[DescribeCrossBackupPolicy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifybackupencryptionpolicy) |* Modified the description of the BackupEnabled parameter from "Whether to enable cross\-regional backup" to "Indicates whether cross\-regional backup is enabled. Valid values:", and added the descriptions for its values.<br><br>* Added the response parameter CrossBackupAllRetention, which indicates whether to retain the cross\-regional backups until the instance is released. The value can be true or false.<br><br>* Extended the value range for the Retention parameter from 7–1825 days to 7–3650 days, and added a note that the value returned for this parameter is invalid when CrossBackupAllRetention is true. |
|Modify |[CreateDBEndpoint](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbendpoint) |Added the request parameter EnableConnectionPersistent first. |
|Modify |[ModifyDBEndpoint](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbendpoint) |Added the request parameter EnableConnectionPersistent first. |
|Modify |[CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbinstance1) |* Added two new storage types for the StorageType parameter: CloudESSD_FlexPL and CloudESSD_PL0, and detailed the usage restrictions in different APIs.<br><br>* Improved the description of the StorageSpace parameter to clarify that the value range for storage space varies based on the storage type and specification. |
|Modify |[DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) |* Added CloudESSD_FlexPL and CloudESSD_PL0 to the value range of the StorageType parameter, and specified the usage restrictions in different interfaces.<br><br>* Added rules for the value range of the StorageType parameter in different interfaces to its description, including:<br><br>   * In the CreateDBBlueGreenInstance interfaces, the value of StorageType can only be LocalSSD.<br><br>   * In the RebuildDBInstance, RestoreToNewInstance, and ModifyDBNodeSpec interfaces, the value of StorageType depends on the storage type of the original instance. |
|Modify |[DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancespecs) |* The description of the StorageType parameter has been updated with new storage type options (CloudESSD_FlexPL and CloudESSD_PL0) and detailed value range limitations for different interfaces.<br><br>* The description of the StorageType parameter in the InstanceSpecsInfoObject response parameter is updated with new storage type options and interface restriction notes. |
|Modify |[DescribeDBInstanceAttribute](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBInstanceAttribute) |Added CloudESSD_FlexPL (Cloud ESSD FlexPL) and CloudESSD_PL0 (Cloud ESSD PL0) to the value range of the StorageType parameter. |
|Modify |[DescribeDeletedDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedeleteddbinstances) |Two new storage types are added to the StorageType parameter: CloudESSD_FlexPL and CloudESSD_PL0, which represent Cloud ESSD FlexPL and Cloud ESSD PL0 respectively. |
|Modify |[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancedetail) |Added a note: This API is deprecated. |
|Modify |[DescribeAllowLists](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeallowlists1) |* Added the request parameter WithIpList to control whether to return the list of IP addresses and IP address segments included in the allowlists. If the value is true, the list is returned. If the value is false or no value is passed, the list is not returned by default.<br><br>* Added the IpList field to the return parameter AllowListObject to return the list of IP addresses and IP address segments included in the allowlists. This field is returned only if the request parameter WithIpList is set to true; otherwise, null is returned. |
|Modify |Common structure \- EndpointsObject |Added the parameter EnableConnectionPersistent. |


<span id="FmSNneaC"></span>
## June 2025

Released SDKs for Python (v3.0.15), GO (v1.1.18), and Java (v0.2.18). This release includes the following updates:


|Change type |API |Change log |
|---|---|---|
|Create |[CreateDrDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdrdbinstance) |Add an API. |
|Create |[DescribeDBAccountTableColumnInfo](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbaccounttablecolumninfo) |Add an API. |
|Create |[DescribeDBInstanceNodes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancenodes) |Add an API. |
|Create |[DescribeDBNodeParameterDifferences](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbnodeparameterdifferences) |Add an API. |
|Create |[DescribeDBProxyPriceDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbproxypricedetail) |Add an API. |
|Create |[DescribeDisasterRecoveryRegions](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedisasterrecoveryregions) |Add an API. |
|Create |[DescribeTaskDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describetaskdetail) |Add an API. |
|Create |[ifyDBInstanceDeletionProtectionPolicy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstancedeletionprotectionpolicy) |Add an API. |
|Create |[ModifyBackupPublicAccessPolicy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifybackuppublicaccesspolicy) |Add an API. |
|Create |[ModifyDBEndpointConnectionMode](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbendpointconnectionmode) |Add an API. |
|Create |[RebuildDrInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/rebuilddrinstance) |Add an API. |
|Create |[SwitchDrInstanceToMaster](https://docs.byteplus.com/en/docs/RDS_for_MySQL/switchdrinstancetomaster) |Add an API. |
|Create |[SyncAllowList](https://docs.byteplus.com/en/docs/RDS_for_MySQL/syncallowlist) |Add an API. |
|Create |Public structure \- ColumnPrivilegeObject |Add a new struct. |
|Create |Public structure \- AccountTableColumnPrivilegeObject |Add a new struct. |
|Create |Common structure \- AutoStorageScalingConfigObject |Add a new struct. |
|Create |Common structure \- DescribeDBInstancePriceDetailStrObject |Add a new struct. |
|Create |Public structure \- DisasterRecoveryInstanceObject |Add a new struct. |
|Create |Public struct \- MasterInstance |Add a new struct. |
|Create |Public structure \- NodeDifferentParameterObject |Add a new struct. |
|Create |Common structure \- NodeParameterValueDetailObject |Add a new struct. |
|Create |Common structure \- TableInfoObject |Add a new struct. |
|Create |Common structure \- TablePrivilegeObject |Add a new struct. |
|Modify |[CreateAllowList](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createallowlist1) |Added restriction information for AllowList, UserAllowList, SecurityGroupIds, and SecurityGroupBindInfos. |
|Modify |[CreateBinlogBackup](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createbinlogbackup) |Added the return parameters InstanceId and BackupId. |
|Modify |[CreateDBEndpoint](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbendpoint) |* Added notes to the API.<br><br>* Added the request parameters MasterNodeRouting, ImplicitTransSplit, OverloadProtection, and MasterProtectorTimeout.<br><br>* Updated the value range for the request parameter ReadOnlyNodeDistributionType. |
|Modify |[CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbinstance1) |* Add the request parameter ProxyNodeCustom. Update the value range of the request parameter InstanceType. Update the description of the request parameter InstanceName.<br><br>* Modify the description of the value range for StorageSpace. Added the request parameters DeletionProtection for deletion protection and AutoStorageScalingConfig for automatic storage expansion. |
|Modify |[CreateDBNodes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbnodes) |Updated the value range of the request parameter SwitchType for multiple node instances. |
|Modify |[CreateParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createparametertemplate1) |The request parameters TemplateType and TemplateTypeVersion are now optional. |
|Modify |[DeleteDBEndpoint](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedbendpoint) |Added notes to the API. |
|Modify |[DeleteDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedbinstance1) |Added the DataKeepDays request parameter. Updated the value range of the DataKeepPolicy request parameter. |
|Modify |[DeleteDBNodes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedbnodes) |Updated the value range of the request parameter SwitchType for multiple\-node instances. Updated the value range of the DBNodeIds request parameter for multiple\-node and double\-node instances. |
|Modify |[DeleteParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleteparametertemplate1) |Added the response parameter TemplateId. |
|Modify |[DescribeBackupPolicy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackuppolicy) |Added the return parameter PublicDownloadEnable. Updated the value range of the return parameter DescribeBackupPolicy. |
|Modify |[DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackups) |Updated the value range of the PageSize request parameter. |
|Modify |[DescribeDatabases](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedatabases) |Updated the value range of the PageSize request parameter. |
|Modify |[DescribeDBAccounts](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbaccounts) |Updated the value range of the PageSize request parameter. |
|Modify |[DescribeDBInstanceParametersLog](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstanceparameterslog) |Updated the value range of the PageSize request parameter. |
|Modify |[DescribeDBInstancePriceDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancepricedetail) |Added the `ProxyNodeCustom` request parameter. Added the `DescribeDBInstancePriceDetailStrObject` response parameter. Removed the `BillingMethod`, `Chargeltem Prices`, `CouponAmount`, `Currency`, `DiscountPrice`, `OriginalPrice`, `PayablePrice`, `Quantity`, and `RefundAmount` response parameters. |
|Modify |[DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) |* Added the request parameter StorageType. Added the response parameter DisasterRecoveryInstances.<br><br>* Updated the value range of the PageSize request parameter. |
|Modify |[DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancespecs) |Updated the value range of the request parameter InstanceType. |
|Modify |[DescribeTagsByResource](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describetagsbyresource) |Updated the descriptions of the request parameters PageNumber and PageSize. |
|Modify |[ListParameterTemplates](https://docs.byteplus.com/en/docs/RDS_for_MySQL/listparametertemplates1) |Added the request parameter TemplateName. |
|Modify |[MigrateToOtherZone](https://docs.byteplus.com/en/docs/RDS_for_MySQL/migratetootherzone) |Added notes for the API. |
|Modify |[ModifyAllowList](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifyallowlist1) |Added restrictions for the SecurityGroupIds and SecurityGroupBindInfos parameters. |
|Modify |[ModifyBackupPolicy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifybackuppolicy) |Added the response parameter PublicDownloadEnable. Updated the value range of the request parameter DataKeepPolicyAfterReleased. |
|Modify |[ModifyDBEndpoint](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbendpoint) |* Updated the descriptions for the request parameters: Nodes, AutoAddNewNodes, ReadOnlyNodeDistributionType, OverloadProtection, MasterProtectorTimeout, MasterNodeRouting, ConnectAllSlaveNodes, and ConnectionMode.<br><br>* Added the request parameters: MasterNodeRouting, ImplicitTransSplit, OverloadProtection, and MasterProtectorTimeout.<br><br>* Updated the value range for the request parameter ReadOnlyNodeDistributionType. |
|Modify |[ModifyDBInstanceParameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstanceparameters) |Updated the description of the request parameter ParamApplyScope. |
|Modify |[ModifyDBInstanceSSL](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstancessl) |Added the request Parameters SwitchType, SpecifiedSwitchStartTime, and SpecifiedSwitchEndTime. |
|Modify |[ModifyDBNodeSpec](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbnodespec) |Update the description of the request parameter StorageSpace. |
|Modify |[ModifyDBProxy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbproxy) |* Added the request parameter ConvertDefaultEndpoint.<br><br>* Added notes for the API. |
|Modify |[ModifyDBProxySpec](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbproxyspec) |Removed notes on API deprecation. Added the return Parameter OrderId. |
|Modify |[ModifyParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifyparametertemplate1) |Added the response parameter TemplateId. |
|Modify |[ModifyReadOnlyNodeDelayReplicationTime](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifyreadonlynodedelayreplicationtime) |Added notes to the API. |
|Modify |[ModifyTask](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifytask) |Added notes on canceling tasks for the API. |
|Modify |[RebuildDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/rebuilddbinstance) |Added the request parameters ProxyNodeCustom, BackupId, StorageType, StorageSpace, VpcId, InstanceName, DBParamGroupId, ChargeInfo, NodeInfo, SubnetId, InstanceTags, AllowListIds, Port, AutoStorageScalingConfig, and DeletionProtection. Added InstanceId and OrderId. |
|Modify |[RestoreToExistedInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/restoretoexistedinstance) |Added the request parameter FastMode. |
|Modify |[RestoreToNewInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/restoretonewinstance) |Added the `ProxyNodeCustom` request parameter. |
|Modify |[SaveAsParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_MySQL/saveasparametertemplate1) |Added the response parameter TemplateId. |
|Modify |[CopyParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_MySQL/copyparametertemplate1)<br><br> |Added the request parameter CopyParameterTemplate. Added the response parameter TemplateId. |
|Modify |Common structure \- AccountPrivilegeObject |Updated the descriptions of the DBName, AccountPrivilege, and AccountPrivilegeDetail fields. Updated the value ranges for AccountPrivilege and AccountPrivilegeDetail. |
|Modify |Public structure \- AccountsObject |Added the parameter HasTableColumnPrivilegeDBNames. |
|Modify |Common structure \- BackupInfoObject |Added the parameter DBEngineVersion. |
|Modify |Common structure \- BasicInfoObject |* Added the DeletionProtection parameter.<br><br>* Added parameters related to the disaster recovery instance feature: DrDtsTaskId, MasterRegion, DrDtsTaskName, DrDtsTaskStatus, MasterInstanceId, MasterInstanceName, and DrSecondsBehindMaster.<br><br>* Updated the value range of the InstanceType parameter. |
|Modify |Common structure \- DeletedDBInstanceInfoObject |Update the value range of the parameter InstanceType. |
|Modify |Common structure \- EndpointsObject |* Added new parameters: ConnectionInfoTags, MasterNodeRouting, ImplicitTransSplit, OverloadProtection, and MasterProtectorTimeout.<br><br>* Updated the value range of the ReadOnlyNodeDistributionType field. |
|Modify |Common structure \- InstanceInfoObject |* Update the value range of the parameter InstanceType.<br><br>* Added the DeletionProtection parameter for the deletion protection feature. Added the parameters DrDtsTaskId, MasterInstance, and DisasterRecoveryInstances for the disaster recovery instance feature. |
|Modify |Public structure \- NodeInfoObject |Update the descriptions for the parameters NodeType, NodeSpec, NodeOperateType, and ZoneId. |
|Modify |Common struct \- ProxyNodeCustomObject |Updated the value range of the CpuNum parameter for multiple\-node and double\-node instances. |
|Modify |Common struct \- ReadOnlyNodeWeightObject |Modified the description and value range of the `NodeType` parameter. |
|Modify |Common structure \- TagFilterObject |Added the new parameter Values. |


<span id=".XzIwMjUtMDItMDfvvIjmlrDlop7vvIk="></span>
## **2025\-03\-06**

Released SDKs for Python (v1.0.128), GO (v1.0.185), and Java (v0.1.155). This release includes the following updates:


|API |Change log |
|---|---|
|[AddDiagnosticsEntity](https://docs.byteplus.com/en/docs/RDS_for_MySQL/adddiagnosticsentity) |Add an API. |
|[CreateDBNodes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbnodes) ||
|[CreateDiagnosticsTask](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creatediagnosticstask) ||
|[DeleteDBNodes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedbnodes) ||
|[DescribeBackupStats](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackupstats) ||
|[DescribeDBInstanceEngineMinorVersions](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstanceengineminorversions) ||
|[DescribeDeletedDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedeleteddbinstances) ||
|[DescribeDiagnosticsInfos](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describediagnosticsinfos) ||
|[ModifyDBInstanceAutoUpgradeEngineMinorVersion](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstanceautoupgradeengineminorversion) ||
|[ModifyDBInstanceGlobalReadOnly](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstanceglobalreadonly) ||
|[ModifyDBNodeSpec](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbnodespec) ||
|[ModifyDBNodeTemporarySpec](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbnodetemporaryspec) ||
|[ModifyDBProxy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbproxy) ||
|[ModifyDBProxySpec](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbproxyspec) ||
|[RemoveDiagnosticsEntity](https://docs.byteplus.com/en/docs/RDS_for_MySQL/removediagnosticsentity) ||
|[UpgradeDBInstanceEngineMinorVersion](https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgradedbinstanceengineminorversion) ||
|Public structure \- BackupExtraOptionObject |Add a new struct. |
|Common struct \- CheckModifyDBProxyAllowedV2Object ||
|Common structure \- CRBackupServingInstanceInfoObject ||
|Common structure \- DeletedDBInstanceInfoObject ||
|Common structure \- DiagnosticsEcsInfoObject ||
|Common structure \- DiagnosticsEndpointInfo ||
|Common structure \- DiagnosticsInfoObject ||
|Common structure \- DiagnosticsItemInfoObject ||
|Public structure \- DiagnosticsPublicAddressInfoObject ||
|Public structure \- ProxyInfoObject ||
|Common struct \- ProxyNodeCustomObject ||
|Common data structure \- ProxyResourceInfoObject ||
|Common structure \- UsageStatObject ||
|[CopyParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_MySQL/copyparametertemplate1) |Add the optional request parameter ProjectName. |
|[CreateAllowList](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createallowlist1) ||
|[CreateDBAccount](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbaccount) |* Added the request parameter `DryRun`.<br><br>* Added the response parameter CreateAccountSQL.<br><br>* Updated the description of the request parameter AccountName and added value rules. |
|[CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbinstance1) |* The request parameter StorageSpace is changed from optional to required.<br><br>* Updated the description of the request parameter InstanceTags. |
|[CreateDBEndpoint](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbendpoint) |* Added the following request parameters:<br><br>   * ConnectionMode<br><br>   * ConnectionPoolType<br><br>   * IdleConnectionReclaim<br><br>   * MultiStatementsMode<br><br>   * ReadOnlyNodeDistributionType<br><br>   * ReadOnlyNodeMaxDelayTime<br><br>   * ReadOnlyNodeWeight<br><br>   * ReadWriteSpliting<br><br>* Updated the descriptions of the following request parameters:<br><br>   * ReadWriteMode |
|[CreateParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createparametertemplate1) |Add the optional request parameter ProjectName. |
|[DeleteAllowList](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleteallowlist1) ||
|[DeleteDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedbinstance1) |Updated the value range of the DataKeepPolicy request parameter. |
|[DeleteParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleteparametertemplate1) |Add the optional request parameter ProjectName. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeallowlistdetail1) ||
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeallowlists1) |* Added the request parameter QueryDefault.<br><br>* Add the optional request parameter ProjectName.<br><br>* Added the request parameter IPAddress. |
|[DescribeBackupPolicy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackuppolicy) |* Added the following response parameters:<br><br>   * BinlogBackupAllRetention<br><br>   * BinlogBackupEnabled<br><br>   * BinlogBackupEncryptionEnabled<br><br>   * DataBackupAllRetention<br><br>   * DataBackupEncryptionEnabled<br><br>   * DataFullBackupStartUTCHour<br><br>   * DataKeepDaysAfterReleased<br><br>   * DataKeepPolicyAfterReleased<br><br>   * HourlyIncrBackupEnable<br><br>   * IncrBackupHourPeriod<br><br>   * RetentionPolicySynced<br><br>* Updated the descriptions for the following response parameters:<br><br>   * DataBackupRetentionDay<br><br>   * DataFullBackupTime<br><br>   * DataIncrBackupPeriods<br><br>   * LogBackupRetentionDay<br><br>* Updated the value ranges for the following response parameters:<br><br>   * DataBackupRetentionDay<br><br>   * LogBackupRetentionDay<br><br>* Update the return example. |
|[DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackups) |* Updated the optionality of the request parameter InstanceId and modified its description.<br><br>* Added the request parameter Option.<br><br>* Updated the description of the response parameter DBTableInfos.<br><br>* Updated the descriptions of the request parameters BackupStartTime and BackupEndTime. |
|[DescribeBinlogFiles](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebinlogfiles) |* Added the request parameter ResultSorter.<br><br>* Updated the request parameter Context to optional. |
|[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancedetail) |Added the return parameter ProxyDetail. |
|[DescribeDBInstancePriceDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancepricedetail) |Add the optional request parameter ProjectName. |
|[DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) |* Added the request parameters PrivateNetworkIpAddress, KernelVersion, and PrivateNetworkVpcId.<br><br>* Updated the value range of the request parameter InstanceStatus.<br><br>* Updated the descriptions of the request parameters PageNumber and PageSize. |
|[DescribeDBProxyConfig](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbproxyconfig) |* Added the return parameters CheckModifyDBProxyAllowedV2 and ProxyResourceInfo.<br><br>* Updated the descriptions for the return parameters BinlogDump, DBProxyStatus, and CheckModifyDBProxyAllowed. |
|[DescribeParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeparametertemplate1) |Add the optional request parameter ProjectName. |
|[DescribePlannedEvents](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeplannedevents) |* Added the optional request parameter ProjectName.<br><br>* Updated the value range of the request parameter Status. |
|[DescribeRecoverableTime](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describerecoverabletime1) |Updated the description of the request parameter RestoreType. |
|[DescribeTasks](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describetasks) |Updated the value ranges of the TaskStatus and TaskCategory request parameters. |
|[GetBackupDownloadLink](https://docs.byteplus.com/en/docs/RDS_for_MySQL/getbackupdownloadlink) |Updated the type of the request parameter BackupFileSize from Integer to Long. |
|[GrantDBAccountPrivilege](https://docs.byteplus.com/en/docs/RDS_for_MySQL/grantdbaccountprivilege) |* Added the request parameter `DryRun`.<br><br>* Added the return parameter CreateAccountSQL. |
|[ListParameterTemplates](https://docs.byteplus.com/en/docs/RDS_for_MySQL/listparametertemplates1) |Add the optional request parameter ProjectName. |
|[MigrateToOtherZone](https://docs.byteplus.com/en/docs/RDS_for_MySQL/migratetootherzone) |* Modified the description of the `SwitchType` request parameter.<br><br>* Added the `SpecifiedSwitchStartTime` and `SpecifiedSwitchEndTime` request parameters. |
|[ModifyAllowList](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifyallowlist1) |* Add the request parameter IgnoreInstanceStatus.<br><br>* Add the optional request parameter ProjectName. |
|[ModifyBackupPolicy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifybackuppolicy) |* Added the following request parameters:<br><br>   * DataFullBackupStartUTCHour<br><br>   * BinlogBackupAllRetention<br><br>   * BinlogBackupEnabled<br><br>   * BinlogBackupEncryptionEnabled<br><br>   * DataBackupAllRetention<br><br>   * DataBackupEncryptionEnabled<br><br>   * DataKeepDaysAfterReleased<br><br>   * DataKeepPolicyAfterReleased<br><br>   * HourlyIncrBackupEnable<br><br>   * IncrBackupHourPeriod<br><br>   * RetentionPolicySynced<br><br>* Update the descriptions for the following request parameters:<br><br>   * DataFullBackupPeriods<br><br>   * DataBackupRetentionDay<br><br>   * DataFullBackupTime<br><br>   * DataIncrBackupPeriods<br><br>   * BinlogFileCountsEnable<br><br>   * BinlogLimitCount<br><br>   * BinlogLocalRetentionHour<br><br>   * BinlogSpaceLimitEnable<br><br>   * BinlogStoragePercentage<br><br>   * LogBackupRetentionDay<br><br>* Updated the value range for the following request parameters:<br><br>   * DataBackupRetentionDay<br><br>   * LogBackupRetentionDay<br><br>* Added the following response parameters:<br><br>   * BinlogBackupAllRetention<br><br>   * BinlogBackupEnabled<br><br>   * BinlogBackupEncryptionEnabled<br><br>   * DataBackupAllRetention<br><br>   * DataBackupEncryptionEnabled<br><br>   * DataFullBackupStartUTCHour<br><br>   * DataKeepDaysAfterReleased<br><br>   * DataKeepPolicyAfterReleased<br><br>   * HourlyIncrBackupEnable<br><br>   * IncrBackupHourPeriod<br><br>   * RetentionPolicySynced<br><br>* Updated the descriptions for the following return parameters:<br><br>   * DataFullBackupTime<br><br>   * DataIncrBackupPeriods<br><br>   * LogBackupRetentionDay<br><br>* Updated the request and response examples for the API. |
|[ModifyDBEndpoint](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbendpoint) |* Added the following request parameters:<br><br>   * ConnectionMode<br><br>   * MultiStatementsMode<br><br>* Modified the description of the following request parameters:<br><br>   * ReadWriteMode |
|[ModifyDBInstanceSpec](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstancespec1) |Added a note that this API is deprecated. |
|[ModifyParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifyparametertemplate1) |Add the optional request parameter ProjectName. |
|[ModifyPlannedEventExecuteTime](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifyplannedeventexecutetime) |* Added the optional request parameters ProjectName and TaskEventOperation.<br><br>* Added the required request parameter InstanceId.<br><br>* Modify the request parameters ModifyBeginTime and ModifyEndTime to be optional. |
|[ModifyTask](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifytask) |* Added the request parameters TaskEventOperation, ModifyBeginTime, ModifyEndTime, and ProjectName.<br><br>* Removed the request parameters ModifyType and SwitchTime. |
|[RebuildDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/rebuilddbinstance) |* Added the request parameter RequestSource.<br><br>* Updated the description of the request parameter ProjectName. |
|[RestartDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/restartdbinstance1) |* Modified the description of the `SwitchType` request parameter.<br><br>* Added the `SpecifiedSwitchStartTime` and `SpecifiedSwitchEndTime` request parameters. |
|[RestoreToExistedInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/restoretoexistedinstance) |Updated the description of the request parameter RestoreType. |
|[RestoreToNewInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/restoretonewinstance) |Updated the descriptions of the request parameters StorageType and InstanceTags. |
|Public structure \- AccountsObject |Added fields AccountPrivilegesSQL and GlobalAccountPrivileges. |
|Common structure \- AccountPrivilegesObject |Updated the description for the DBName field. |
|Public struct \- AllowListObject |Modify the description of the AllowListCategory field. |
|Common structure \- AssociatedInstanceObject |Added the fields InstanceStatus and IsLatest. |
|Common structure \- BasicInfoObject |* Added the parameters BasicBackupBinlogSize, BasicBackupDataSize, BackupFreeQuotaSize, CurrentKernelVersion, and AutoUpgradeMinorVersion.<br><br>* Updated the description of the parameter InstanceStatus. |
|Public struct \- BackupExtraOption |Added the request parameter ResultSorter. |
|Public structure \- ChargeInfo |Modify the descriptions for the ChargeType, AutoRenew, PeriodUnit, Period, and Number fields. |
|Common structure \- EndpointObject |Added the following fields:<br><br><br>* ConnectionMode<br><br>* ConnectionPoolType<br><br>* MultiStatementsMode<br><br>* ReadOnlyNodeDistributionType<br><br>* ReadOnlyNodeMaxDelayTime |
|Common structure \- InstanceInfoObject |\- CurrentKernelVersion field. |
|Public structure \- InstanceSpecsInfoObject |Updated the description for the value of the SpecFamily field (instance specification type name updated). |
|Public structure \- NodeInfoObject |Updated the descriptions for the NodeId, ZoneId, NodeType, and NodeOperateType fields. |
|Common structure \- NodeObject |Added fields DelayReplicationTime and SyncDelay. |
|Common structure \- PlannedEvent |* Added the PlannedSwitchBeginTime and PlannedSwitchEndTime fields.<br><br>* Removed the IsUrgent field. |
|Common structure \- RegionObject |Updates the example value of the RegionName field. |
|Public structure \- TableMetaObject |Update the description of the NewDBName field and add its value rules. |
|Common structure \- TagObject |Updated the descriptions of the `Key` and `Value` fields. |
|Common structure \- TableObject |Updated the description for the NewTableName field and added value rules. |
|Common structure \- TaskInfoObject |* Added the fields ScheduledExecuteEndTime, ScheduledExecuteStartTime, ScheduledSwitchEndTime, and ScheduledSwitchStartTime.<br><br>* Updated the value range for the fields TaskCategory and TaskStatus.<br><br>* Removed the ConfigInfos field. |


<span id="_2024-10-31"></span>
## 2024\-10\-31

Released SDKs for Python (v1.0.107), GO (v1.0.163), and Java (v0.1.134). This release includes the following updates:


|API |Change log |
|---|---|
|DescribeBackupPolicy |Updated the example value of the DataFullBackupTime return parameter in the return parameter list. |
|DescribeDBInstanceTDE |Removed from the SDK. |
|ModifyDBInstanceTDE |Removed from the SDK. |
|CreateParameterTemplate |* Added the response parameter TemplateId.<br><br>* Modified the value of the request parameter TemplateType to `Mysql`.<br><br>* Update the return example. |
|ModifyDBEndpoint |Added the request parameter IdleConnectionReclaim. |
|CreateDBInstance |Modify the description for the request parameter VpcId to add a restriction for unsupported shared VPCs. |
|RestoreToNewInstance |Modify the description for the request parameter VpcId to add a restriction for unsupported shared VPCs. |
|Data structure \- InstanceParamObject |Added the parameters ExpectValue and Expression. |
|Data structure \- ParameterChangeLogObject |Added the new `CustomNodeIds` and `ParamApplyScope` fields to the response of the `DescribeDBInstanceParametersLog` API. |
|Data structure \- ParametersObject |Removed the fields CheckingCode, ForceRestart, ParameterDefaultValue, ParameterDescription, and Expression. |
|Data structure \- InstanceParametersObject |Updated the structure associated with the Parameters response parameter of the DescribeDBInstanceParameters API to InstanceParametersObject. |
|Data structure \- EndpointObject |Added the IdleConnectionReclaim parameter to the EndpointObject returned by the DescribeDBInstanceDetail API. |
|Data structure \- NodeInfoObject |Updated the descriptions of the NodeSpec and ZoneId parameters of NodeInfoObject. |


&nbsp;

<span id="_2024-08-08"></span>
## 2024\-08\-08

Released Python (v1.0.95), GO (v1.0.151), and Java (v0.1.123) SDKs. This release includes the following updates:


|API |Change log |
|---|---|
|ModifyAllowList |Modified the ApplyInstanceNum request parameter to be conditionally required. |
|RestoreToExistedInstance |Changed the request parameters RestoreType and TableMeta from optional to required. |
|ModifyBackupEncryptionPolicy |Add an API. |
|DescribeBackupEncryptionStatus |Add an API. |
|DescribeBackupDecryptionKey |Add an API. |


<span id="_2024-07-25"></span>
## 2024\-07\-25

Released Python (v1.0.94), GO (v1.0.150), and Java (v0.1.122) SDKs. This release includes the following API updates:


|API |Change log |
|---|---|
|AssociateAllowList |Updated the descriptions of the request parameters InstanceIds and AllowListIds and added quantity limit information. |
|CreateBackup |* Added `Logical` as a value for the BackupMethod parameter.<br><br>* Added `DumpAll` as a value for the BackupType parameter and updated relevant descriptions.<br><br>* Added prerequisites, mutual exclusion conditions, and quantity limits for the BackupMeta parameter.<br><br>* Added examples for creating a logical backup for a full database backup and a database & table backup.<br><br>* Updated the response parameters. |
|CreateDBAccount |Updated the value range of the request parameter AccountPassword. |
|CreateDBEndpoint |Modify the value of the EndpointType request parameter by removing the value Primary. |
|CreateDBInstance |* Added the request parameter MaintenanceWindow and updated the request example.<br><br>* Updated the value range for the parameter SuperAccountPassword. |
|DeleteDataBackup |Removed the usage restrictions for this API. |
|DescribeBackups |* Added the `CreateType` request parameter.<br><br>* Added the value `Logical` for the `BackupMethod` request parameter and updated the request example.<br><br>* Added the value `DumpAll` for the `BackupType` request parameter and updated the related description.<br><br>* Added descriptions about the default values for the `BackupId`, `BackupStatus`, `BackupMethod`, and `BackupType` request parameters.<br><br>* Update the return example. |
|DescribeDBInstanceParameters |Add request parameter NodeId. |
|DescribeDBInstances |* Added the request parameters InstanceType, NodeSpec, and TagFilters.<br><br>* Update the return example. |
|DescribeDBInstanceSSL |Added the response parameter Address and updated the response example. |
|DescribeFailoverLogs |Added request parameters EndTime and StartTime. |
|DescribeReadOnlyNodeDelay |Modify the type of the returned parameter DelayReplicationTime to Long. |
|GetBackupDownloadLink |* Modified the data type of the response parameter DownloadProgress to Long.<br><br>* Updated the API notes.<br><br>* Updated the description of the request parameter BackupId.<br><br>* Added the response parameter InnerBackupDownloadLink.<br><br>* Updated the descriptions of the response parameters BackupFileName and BackupId.<br><br>* Updated the unit of the response parameter BackupFileSize.<br><br>* Updated the response example. |
|ModifyAllowList |Add the request parameter UpdateSecurityGroup. |
|ModifyDBInstanceParameters |Added the request parameters ParamApplyScope and CustomNodeIds. |
|ModifyReadOnlyNodeDelayReplicationTime |Modify the type of the request parameter DelayReplicationTime to Long. |
|ResetDBAccount |Updated the value range of the request parameter AccountPassword. |
|RestoreToExistedInstance |Updated the description of the request parameter BackupId. |
|RestoreToNewInstance |Updated the description of the request parameter BackupId. |
|Data structure \- BackupMetaObject |Added the `TableNames` parameter. |
|Data structure \- BackupObject |* Adds the IsEncrypted parameter.<br><br>* Modifies the type of the BackupFileSize parameter to Long.<br><br>* Adds the value `DumpAll` for the BackupType parameter. |
|Data structure \- BasicInfoObject |* Modified the type of the StorageSpace parameter to Long.<br><br>* Added the value `ChargeTypeChanging` for the InstanceStatus parameter: billing method changing.<br><br>* Added a value for the parameter InstanceStatus: `NetWorkChanging` (Network changing).<br><br>* Added the following values for InstanceStatus:<br><br>   * `Recycled`: Recycled.<br><br>   * `TDEUpdating`: TDE modifying.<br><br>   * `Closed`: shut down.<br><br>   * `Maintaining`: maintaining.<br><br>   * `CreateFailed`: failed to create.<br><br>   * `Closing`: Shutting down.<br><br>   * `SSLUpdating`: SSL modifying.<br><br>   * `AllowListMaintaining`: Allowlist modifying.<br><br>   * `Unknown`: Unknown.<br><br>   * `ProxyCreating`: Proxy is enabling.<br><br>   * `ProxyDeleting`: Proxy is disabling.<br><br>   * Update the description for the value `MasterChanging`. |
|Data structure \- BinlogFilesObject |* Added the IsEncrypted parameter.<br><br>* Modified the type of the FileSize parameter to Long. |
|Data structure \- ChargeItemPriceObject |Modified the type of the parameter ChargeItemValue to Long. |
|Data structure \- ConfigItemPriceObject |Modified the type of the Quantity parameter to Long. |
|Data structure \- EndpointObject |* Removed Primary and Cluster from the valid values for the EndpointType parameter.<br><br>* Modified the example value and description for the Description parameter.<br><br>* Modified the example value for the EndpointName parameter. |
|Data structure \- InstanceObject |* Added the value `NetWorkChanging` (Network changing) to the InstanceStatus parameter.<br><br>* Updated the description of the ZoneId parameter.<br><br>* Added the NodeCPUUsedPercentage, NodeMemoryUsedPercentage, and NodeSpaceUsedPercentage parameters.<br><br>* Added the Tags and ZoneIds parameters.<br><br>* Added the following values to the InstanceStatus parameter:<br><br>   * `Recycled`: Recycled.<br><br>   * `TDEUpdating`: TDE modifying.<br><br>   * `Closed`: shut down.<br><br>   * `Maintaining`: maintaining.<br><br>   * `CreateFailed`: failed to create.<br><br>   * `Closing`: Shutting down.<br><br>   * `SSLUpdating`: SSL modifying.<br><br>   * `AllowListMaintaining`: Allowlist modifying.<br><br>   * `Unknown`: Unknown.<br><br>   * `ProxyCreating`: Proxy is enabling.<br><br>   * `ProxyDeleting`: proxy is disabling.<br><br>   * `ChargeTypeChanging`: billing method changing.<br><br>   * Update the description for the value `MasterChanging`. |
|Data structure \- MaintenanceWindowObject |Deleted the DayOfMonth Parameter. |
|Data structure \- ParameterTemplateInfoObject |Modified the type of the ParameterNum parameter to Long. |
|Data structure \- TaskInfoObject |Modified the type of the CostTimeMS parameter to Long. |


<span id="_2024-05-23"></span>
## 2024\-05\-23

Released Python (v1.0.83), GO (v1.0.137), and Java (v0.1.111) SDKs. This release includes the following API updates:


|API |Change log |
|---|---|
|CreateDatabase |Modified the description of the request field DBName. |
|CreateDBAccount |Modified the description of the request field AccountName. |
|CreateDBInstance |* Added the Port request field and updated the request example.<br><br>* Updated the example values and descriptions for the VpcId and SubnetId request fields.<br><br>* Modified the description for the SuperAccountName request field. |
|DescribeBinlogFiles |* Updated the sample value for the returned field BinlogFiles.<br><br>* Updated the returned sample to add a NodeId for each returned BinlogFilesObject.<br><br>* Modified the upper limit for the BackupFileNumber field. |
|ModifyDBEndpointAddress |* Add notes to the interface description.<br><br>* Add a note to the description of the request field Port. |
|ModifyDBInstanceChargeType |* Modified the API description.<br><br>* Modified the request fields PeriodUnit and Period to be optional. |
|ModifyDBInstanceName |Updated the description of the InstanceNewName request parameter. |
|ModifyTask |* Add the request field InstanceId.<br><br>* Update request and response examples. |
|RestoreToNewInstance |* Added the Port request field and updated the request example.<br><br>* Updated the example values and descriptions for the VpcId and SubnetId request fields. |
|Data structure \- BinlogFilesObject |Added the NodeId field. |
|Data structure \- NodeInfoObject |Added a description for the `ZoneId` field. |


<span id="_2024-04-11"></span>
## 2024\-04\-11

Released SDKs for Python (v1.0.74), Go (v1.0.131), and Java (v0.1.105). This release includes the following API updates:


|APIAPI |Change log |
|---|---|
|ModifyDBEndpointAddress |Modified the API usage description (supports modifying the public network port) and the description of the Port request parameter. |
|CreateAllowList |Add the request parameters SecurityGroupBindInfos, AllowListCategory, and UserAllowList. |
|ModifyAllowList |Add the request parameters SecurityGroupBindInfos, AllowListCategory, and UserAllowList, and modify the usage limits of the API. |
|DescribeAllowLists |Updated the response examples in the API documentation. |
|DescribeAllowListDetail |Added the return parameters AllowListCategory, SecurityGroupBindInfos, and UserAllowList. |
|DescribePlannedEvents |Added the value HostOffline for the request parameter EventType. |
|CreateParameterTemplate |Updated the value of the request parameter TemplateTypeVersion and the API request example. |
|ModifyParameterTemplate |Updated the description of the request parameter TemplateParams to add instructions. |
|DescribeParameterTemplate |Updated the API request example. |
|ListParameterTemplates |Updated the value of the request parameter TemplateTypeVersion. |
|Data structure \- InstanceParamObject |Added descriptions and the DefaultValue, Description, Restart, and ValueRange fields. |
|Data structure \- ParameterTemplateInfoObject |Added an example value for the TemplateParams field. |


&nbsp;

<span id="_2024-03-14"></span>
## 2024\-03\-14

Released SDKs for Python (v1.0.69), Go (v1.0.125), and Java (v0.1.101). The changes in this version are as follows:

<span id=".5paw5aKe"></span>
### Create

This SDK version adds the following APIs:


|API |Change log |
|---|---|
|MigrateToOtherZone |Call the MigrateToOtherZone API to migrate nodes of a specified instance to another availability zone within the same region. |
|DescribeReadOnlyNodeDelay |Call the DescribeReadOnlyNodeDelay API to query the delayed replication configuration of a read\-only node. |
|ModifyReadOnlyNodeDelayReplicationTime |Call the ModifyReadOnlyNodeDelayReplicationTime API to configure the delayed replication feature for a read\-only node. |
|ModifyDBAccountHost |Call the ModifyDBAccountHost API to modify the IP address from which a regular database account can access the database. |
|DownloadSSLCertificate |Call the DownloadSSLCertificate API to download the SSL certificate of a specified MySQL instance. |
|DeleteDataBackup |Call the DeleteDataBackup API to delete manual backup files for a specified MySQL instance. |
|ListParameterTemplates |Call the ListParameterTemplates API to query the parameter template list of a MySQL instance. |
|DescribeTasks |Call the DescribeTasks API to query tasks. |
|ModifyTask |Call the ModifyTask API to edit the task. |
|DescribePlannedEvents |Call the DescribePlannedEvents API to query the list of planned events. |
|ModifyPlannedEventExecuteTime |Call the ModifyPlannedEventExecuteTime API to change the execution of scheduled operations events. |
|DescribeFailoverLogs |Call the DescribeFailoverLogs API to query the primary\-secondary switchover logs of a MySQL instance. |


<span id=".5L-u5pS5"></span>
### Modify

This SDK version modifies the following APIs:


|API |Change log |
|---|---|
|CopyParameterTemplate |Updated the request Parameter TemplateName to be a required option. |
|CreateAllowList |Update the request parameter AllowList to be optional. |
|CreateBackup |The update returns an empty parameter. |
|CreateDBAccount |* Added the required request parameter AccountType.<br><br>* Updated the request parameters AccountName and AccountPassword to be required.<br><br>* Deleted the request parameter AccountPrivilegesInfo. |
|CreateDBEndpoint |Updates the request parameter EndpointType to a required option. |
|CreateDBInstance |Made the request parameters DBEngineVersion, StorageSpace, StorageType, SubnetId, and VpcId required. |
|CreateDatabase |* The request parameter DBName is now required.<br><br>* Deleted the request parameter DatabasePrivilegesInfo. |
|CreateParameterTemplate |Updated the request Parameter TemplateName to be a required option. |
|DescribeAllowLists |Updated the request parameter RegionId to be required. |
|DescribeAvailabilityZones |The request parameter RegionId is deleted. |
|DescribeAvailableCrossRegion |Updated the request parameter RegionId to be required. |
|DescribeBinlogFiles |The request parameters `EndTime`, `InstanceId`, and `StartTime` are now required. |
|DescribeCrossBackupPolicy |The request parameter `InstanceId` is now required. |
|DescribeDBAccounts |* The AccountsInfo field has been deleted from the response parameter.<br><br>* The AccountPrivilegesInfo field has been deleted from the Accounts nested object of the response parameter. |
|DescribeDBInstanceDetail |Deleted ConnectionInfo and NodeDetailInfo from the return parameter structure. |
|DescribeDBInstancePriceDetail |Update the request parameters ChargeType, StorageSpace, and StorageType to be required. |
|DescribeDBInstanceTDE |Added the required parameter InstanceId. |
|DescribeDBInstances |Remove the return parameter InstancesInfo. |
|DescribeDBProxyConfig |The request parameter `InstanceId` is now required. |
|DescribeDatabases |The request parameter `InstanceId` is now required.<br><br>Deleted the `DatabasesInfo` field from the response parameters. |
|DescribeParameterTemplate |Deleted the Description field from the TemplateParams parameter in the returned TemplateInfo parameter. |
|DownloadBackup |The request Parameter BackupId is now required. |
|GetBackupDownloadLink |The request Parameter BackupId is now required. |
|ModifyBackupPolicy |The request parameter `InstanceId` is now required. |
|ModifyCrossBackupPolicy |The request parameter `InstanceId` is now required. |
|ModifyDBEndpointAddress |Updated the request parameters EndpointId and NetworkType to be required. |
|ModifyDBInstanceChargeType |Updated the request parameters ChargeType, Period, and PeriodUnit to be required. |
|ModifyDBInstanceMaintenanceWindow |Updated the request parameter MaintenanceTime to required. |
|ModifyDBInstanceParameters |The response parameters are now empty. |
|ModifyDBInstanceSyncMode |The request parameter SyncMode is now required. |
|ModifyDBInstanceTDE |Updated the request parameter TDEStatus to be required. |
|ModifyParameterTemplate |Updated the request Parameter TemplateName to be a required option. |
|ResetDBAccount |The request parameter AccountPassword is now required. |
|RestoreToExistedInstance |The request parameter SourceDBInstanceId is now required. |
|SaveAsParameterTemplate |Updated the request Parameter TemplateName to be a required option. |
|SwitchDBInstanceHA |Updated the request parameter NodeId to be a required option. |
