---
title: "Common error code"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/error-code"
---

This topic summarizes the error codes that may occur in Cache for Redis.

|Error code |HTTP status code |Error description |
|---|---|---|
|AccountAbnormal |400 |The operation is not allowed because the account does not have real\-name authentication or the account balance is less than 100RMB. |
|AccountDescriptionTooLong |400 |The account description is too long. |
|AccountExist |400 |The specified account already exists. |
|AccountFlowLimitExceeded |429 |Request was rejected because the request speed of this OpenAPI exceeds the current flow control limit. |
|AccountModifyConfigForbidden |400 |The account is forbidden to modify this parameter. |
|AccountNotExist |400 |The specified account does not exist. |
|AccountNotVerified |400 |The account is not verified. |
|AccountOfInstanceExceedUpper |400 |The number of accounts belonging to the specified instance exceeds the limit. |
|AccountRoleInvalid |400 |The specified account role does not exist. |
|ActionCanceled |400 |The action is canceled. |
|ActionExcuteTimeout |500 |The specified task execution times out. |
|ActionRollingBack |400 |The specified task is rolling back. |
|AddressPrefixAlreadyExists |400 |The specified connection address prefix already exists. |
|AddressPrefixInvalid |400 |The specified connection address prefix is invalid. |
|AddressTypeNotFound |400 |The specified connection address type does not exist. |
|AllowListBindEntInstanceExceedUpper |400 |The number of bound enterprise instances in the specified allowlist exceeds the limit. |
|AllowListBindInstanceCannotDelete |400 |The operation is not allowed because allowlist already binds to instance. |
|AllowListBindInstanceExceedUpper |400 |The number of bound instances in the specified allowlist exceeds the limit. |
|AllowListConfiguredWildcardAddress |400 |The operation is not allowed because the allowlist has been configured with 0.0.0.0/0. |
|AllowListCountPerRequestExceedUpper |400 |The operation is not allowed because the number of allowlists per request is exceeded. |
|AllowListIPsExceedEntInstanceUpper |400 |The number of ips exceed the limit of enterprise instance. |
|AllowListNeedAtLeastOneIPs |400 |The operation is not allowed because the allowlist contains at least one IP address or IP address segment. |
|AllowListNotExist |400 |The specified allowlist does not exist. |
|AllowListOfAccountExceedUpper |400 |The number of allowlists belonging to the specified account exceeds the limit. |
|ApplyAccountToInstanceFailed |500 |Failed to apply account change to instance. |
|AvailableZoneNumberExceeded |400 |The number of available zone exceeds the limit. |
|AzFailOverTaskNotExist |400 |Az failover task not exist. |
|AZNotExist |400 |The specified available zone does not exist. |
|BackupFileGetFailed |400 |Failed to get the specified backup file. |
|BackupFileNotExist |400 |The specified backup file does not exist. |
|BackupInstanceFailed |500 |Failed to create backup files. |
|BackupNotSupportForCache |400 |The operation is not allowed because the Standalone instance does not support backup. |
|BackupNotSupportForStandalone |400 |The operation is not allowed because the Standalone instance does not support backup. |
|BackupPointExistInDatabase |400 |The specified backup point already exists in the database. |
|BackupPointGetFromAbaseChannelFailed |400 |Failed to get backup point from Abase channel. |
|BackupPointHandleMutex |400 |The operator is not allowed because the backup point is being handled by other request. |
|BackupPointInfoCheckFailed |400 |The specified backup point does not match. |
|BackupPointIsAlreadyExpired |400 |The specified backup point has already expired. |
|BackupPointIsNotReady |400 |The operation is not allowed because the backup point is not ready. |
|BackupPointIsUnavailable |400 |The specified backup point is unavailable. |
|BackupPointNotComplete |400 |The operation is not allowed because the backup point information is incomplete. |
|BackupPointNotFoundFromAbaseChannel |400 |The specified backup point does not exist on the Abase channel. |
|BackupPointNotFoundFromDatabase |400 |The specified backup point does not exist in the database. |
|BackupPointNotSupportForDelete |400 |The specified backup point cannot be deleted. |
|BackupPointNotSupportForRestore |400 |The specified backup point cannot be used to restore instance. |
|BackupPointTaskCreateOnAbaseChannelFailed |400 |Failed to create backup point task on Abase channel. |
|BackupPointTaskDeleteFromAbaseChannelFailed |400 |Failed to delete backup point task from Abase channel. |
|BackupPointTaskGetFromAbaseChannelFailed |400 |Failed to get backup point task from Abase channel. |
|BackupPointTaskNotFoundFromAbaseChannelByChannelId |400 |The specified backup point task cannot be found on the Abase channel by ChannelId. |
|BackupPointTaskNotFoundFromAbaseChannelByInstanceId |400 |The specified backup point task cannot be found on the Abase channel by InstanceId. |
|BackupPointTaskStartOrEndTimeNotRight |400 |Failed to get backup point information due to incorrect StartTime or FinishTime. |
|BackupPointTaskStatusIsBad |400 |The specified backup point task status is bad. |
|BackupPointTaskTypeNotSupport |400 |The operation is not allowed because the specified backup point task type is not supported. |
|BackupPointUpdateFailed |400 |Failed to update backup point information. |
|BackupPolicyExist |400 |The specified backup policy already exists in the database. |
|BackupPolicyIncCreateRefused |400 |The specified instance does not support incremental backup policy creation. |
|BackupPolicyMutex |400 |The operation is not allowed because a backup policy is being handled by another request. |
|BackupRecordNotFound |400 |The specified backup record does not exist. |
|BackUpSystemInternalError |400 |The request processing failed with an internal backup system error. |
|BackupTaskNotExist |400 |The selected backup task was not found. |
|BlueGreenDeploymentConflict |400 |The instance is already in blue green deployment. |
|BlueGreenDeploymentNotFound |404 |SourceInstanceId does not refer to an existing blue green deployment. |
|BlueGreenDeploymentStatusNotMatch |400 |The operation is not allowed because the blue green deployment status does not match. |
|BlueGreenDeploymentUnsupported |400 |Blue green deployment is not supported for this instance. |
|BroadcastFailed |500 |Failed to broadcast. |
|CancelPlannedEventNotSupport |400 |The specified event does not support cancellation. |
|CannotCreateSelectVersionInstance |400 |The operation is not allowed because the account cannot create the specified version instance. |
|CannotModifyCacheInstance |400 |The operation is not allowed because the Cache instance specification is no longer supported. |
|CanNotModifyDefaultAccountRole |400 |Modifying the default account role is not supported. |
|CannotModifyVpc |400 |Modifying the VPC is not supported. |
|CannotRecover |400 |The instance cannot be recovered to the specified time. |
|CanNotRunningAnotherTask |400 |The operation is not allowed because a task is running in the specified instance. |
|CannotUseDirectConnect |400 |The account cannot use direct connect. |
|CannotUseModule |400 |The account cannot use module. |
|CapacityNoChange |400 |当前实例容量已经是该值 |
|CheckAllowListFailed |500 |Failed to check allowlist. |
|ClearDataExecuteFailed |500 |Failed to execute the data clearing command. |
|ClusterNotMatch |400 |The parameter cluster is invalid. |
|ClusterStorageTypeCheckSupportIsFailed |400 |Failed to check cluster storage type. |
|ClusterUnsupportedModifyShardCapacity |400 |The operation is not allowed because the Cluster instance does not support node spec modification. |
|ClusterUnsupportedReductionShardCapacity |400 |The operation is not allowed because the Cluster instance does not support node spec degradation. |
|CombineUrlFailed |400 |Failed to get the download link for the backup file. |
|ConfByteDriveVersionUpdateFailed |400 |Failed to update ByteDrive version. |
|ConfigCanNotEdit |400 |The operation is not allowed because the specified configuration item is not editable. |
|ConfigIsTestingCallOMModify |400 |The parameter is currently in the testing phase. Please contact customer support for further information and assistance. |
|ConfigItemIsConflict |400 |The configuration items conflict. Please check your configuration item modification. |
|ConfigNameNotExist |400 |The specified parameter name does not exist. |
|ConfigNotSupported |400 |The specified parameter cannot be modified. |
|ContinuousBackupAppendonlyOFFMutex |400 |ContinuousBackup and AppendonlyOFF are mutually exclusive. Cannot do %s with %s. |
|CpuSizeOutOfLimit |400 |The operation is not allowed because the CPU exceeds the limit. |
|CreateBackupTaskFailed |500 |Failed to create a backup task. |
|CreateDtsInstanceFailed |500 |Failed to create the DTS instance. |
|CreateK8sStorageClassFailed |500 |Failed to create K8s storage class. |
|CreateOrderFailed |500 |Failed to create order. |
|CreateRestorTaskFailed |500 |Failed to create a restore task. |
|CrossRegionBackupFailed |400 |The cross\-region backup failed. |
|CrossRegionBackupNotSupport |400 |Cross\-region backup is not supported. Please contact the administrator. |
|DataBaseOperateFailed |500 |Failed to access the specified database. |
|DefaultAllowListCannotDelete |400 |The operation is not allowed because the default allowlist cannot be deleted. |
|DeleteDefaultAccount |400 |Deleting the default account is not supported. |
|DeleteDefaultIpGroup |400 |The default IP group cannot be deleted. |
|DeleteDtsInstanceFailed |500 |Failed to delete the DTS instance. |
|DeleteSystemParamGroupForbidden |400 |The operation is not allowed because the system parameter group cannot be deleted. |
|DeletionProtectionPolicyNotMatch |400 |The operation is not allowed because the deletion protection policy has been enabled. |
|DirectModeAlreadyDisabled |400 |Direct mode is already disabled. |
|DirectModeAlreadyEnabled |400 |Direct mode is already enabled. |
|DirectModeDisabled |400 |The operation is not allowed because direct mode is disabled. |
|DirectModeEnabled |400 |The operation is not allowed because direct mode is enabled. |
|DirectModeUnsupported |400 |Direct mode is not supported for this instance. |
|DownsizeIsNotAllowed |400 |The operation is not allowed because the capacity would be insufficient after the downgrade. |
|DtsClusterIsNotReady |400 |The operation is not allowed because the DTS Instance is not ready. |
|DuplicatedFilterNameAndFilterKey |400 |The filter name and filter key already exist. |
|EipNotAvailable |400 |The operation is not allowed because the specified EIP is unavailable. |
|EipNotExist |400 |The specified EIP does not exist. |
|EipPreempted |409 |The operation is not allowed because the specified EIP is preempted by other Redis instance[%s]. |
|EngineVersionTooLowForRestore |400 |The instance engine version is too low to restore. |
|EntInstanceBindAllowListExceedUpper |400 |The number of bound allowlists in the specified enterprise instance exceeds the limit. |
|ExtraPLBExist |400 |The operation is not allowed because extra PLB exists. Please contact technical support. |
|FlowLimitExceeded |429 |Request was rejected because the request speed of this OpenAPI exceeds the current flow control limit. |
|ForbidEmptyPassword |400 |The operation is not allowed because an empty password is prohibited. |
|GetBackupPointFailed |500 |Failed to get the backup point. |
|GetBackupTaskFailed |400 |Failed to get backup task information. |
|GetChannelInfoFailed |400 |Failed to get channel information. |
|GetDTSProcessFailed |500 |Failed to get the DTS process. |
|GetIncRestoreIntervalNotReady |400 |The operation is not allowed because the incremental backup is not ready. |
|GetInstanceProductInfoFailed |400 |Failed to get Instance product information. |
|GetInstanceSpecFailed |500 |Failed to get instance spec. |
|GetInstanceTagsFailed |500 |Failed to get instance tags. |
|GetVisitAddressFailed |500 |Failed to get instance visit addresses. |
|HotKeyCacheDisabled |400 |The operation is not allowed because hot key Cache mode is disabled. |
|InnerAllowListCannotCreate |400 |The operation is not allowed because the inner allowlist cannot be created. |
|InstanceBackupPolicyNotFound |400 |The specified backup policy does not exist. |
|InstanceBindAllowListExceedUpper |400 |The number of bound allowlists in the specified instance exceeds the limit. |
|InstanceBindIPsExceedUpper |400 |The number of bound allowlist IP or IP segment the specified instance exceeds the limit. |
|InstanceBRClusterNotReady |400 |The selected instance backup/restore cluster is not ready. |
|InstanceCanNotModify |400 |The operation is not allowed because the status of the specified instance is not running. |
|InstanceCountPerRequestExceedUpper |400 |The operation is not allowed because the number of instances per request is exceeded. |
|InstanceHasDTSEvent |400 |The operation is not allowed because the instance already has a DTS task running. |
|InstanceHasNoSubnet |400 |The operation is not allowed because the specified instance does not have a subnet. |
|InstanceKubeClusterNameGetFailed |400 |The Instance failed to get kube cluster name. |
|InstanceNotExist |400 |The specified instance does not exist. |
|InstanceNotSupportBanKeys |400 |The operation is not allowed because the proxy version does not support ban keys. |
|InstanceNotSupportHotKeyHosting |400 |The operation is not allowed because the Proxy version does not support hot key hosting. |
|InstanceNotSupportModule |400 |The operation is not allowed because the instance does not support modules. |
|InstanceStatusNotMatch |400 |The operation is not allowed because the specified instance status does not match. |
|InstanceVersionTooLow |400 |The operation is not allowed because the instance version is low. |
|InternalError |500 |The request processing failed with an internal server error. |
|InternalError4ErrCodeMapping |500 |Internal error: error code mapping not found. Please contact technical support. |
|InvalidAccountName |400 |The account name format is invalid. |
|InvalidAllowListVersion |400 |The allowlist version is invalid. |
|InvalidArchType |400 |The specified arch type is invalid. |
|InvalidBackupSchedule |400 |The specified backup schedule is invalid. |
|InvalidBatchCount |400 |The operation is not allowed because the batch count exceeds the limit. |
|InvalidChargeType |400 |The operation is not allowed because the charge type is invalid. |
|InvalidConfigValue |400 |The specified parameter value is invalid. |
|InvalidConnectionMode |400 |The connection mode is invalid. |
|InvalidDescVersion |400 |The desc version is invalid. |
|InvalidEngineVersion |400 |The specified engine version is invalid. |
|InvalidEngineVersionDowngrade |400 |Downgrade engine version is not allowed. |
|InvalidEntModule |400 |The modules are invalid. |
|InvalidExecuteMode |400 |The specified execution mode is invalid. |
|InvalidFilter |400 |The filter name and filter key do not exist. |
|InvalidInstanceClass |400 |The specified instance class is invalid. |
|InvalidInstanceName |400 |The specified instance name is invalid. |
|InvalidInstanceSpec |400 |The specified instance spec does not exist. |
|InvalidInstanceType |400 |The specified instance type is invalid. |
|InvalidInternetProtocol |400 |The specified internet protocol is invalid. |
|InvalidIpAddressPattern |400 |The IP address format is invalid. |
|InvalidMaintenanceTimeScope |400 |The specified maintenance time scope format is invalid. |
|InvalidMinorVersionDowngrade |400 |Downgrade minor version is not allowed. |
|InvalidName |400 |The name is invalid. |
|InvalidNetworkType |400 |The specified network type is invalid. |
|InvalidNetworkVersion |400 |The operation is not allowed because the specified Proxy version is not supported. |
|InvalidOperator |400 |The operation is not supported. |
|InvalidPassword |400 |The account password format is invalid. |
|InvalidPort |400 |The specified port is invalid. |
|InvalidProjectName |400 |The value for ProjectName is invalid. |
|InvalidPurchaseMonths |400 |The purchase months is invalid. |
|InvalidRegion |400 |The specified region is invalid. |
|InvalidReplicas |400 |The value for Replicas is invalid. |
|InvalidSecurityIpGroupName |400 |The security IP group name is invalid. |
|InvalidShardedCluster |400 |The operation is not allowed because the specified instance is already a Sharded Cluster instance. |
|InvalidTagValue |400 |The value for the specified tag is invalid. |
|InvalidZone |400 |The specified zone is invalid. |
|JobAlreadyRunning |400 |The related job is already running. |
|JobNotExist |400 |The specified job does not exist. |
|JsonMarshalFailed |400 |Failed to marshal JSON structure. |
|JsonUnMarshalFailed |400 |Failed to unmarshal JSON structure. |
|K8sResourceDeleteFailed |500 |Failed to delete K8s resource. |
|K8sResourceGetFailed |500 |Failed to get K8s resource. |
|K8sResourceUpdateFailed |500 |Failed to update K8s resource information. |
|KeyAnalysisNotSupportForStandalone |400 |The operation is not allowed because the Standalone instance does not support RDB analysis. |
|KeyScanJobExist |400 |There is a key scan job running. |
|KeyScanJobStatusCannotBeInterrupted |400 |The key scan job is neither creating nor running. Cannot be interrupted. |
|ListBackupPointEmpty |400 |The operation is not allowed because the list of backup point is empty. |
|MaintenanceApiFailed |400 |The maintenance API failed. |
|MemorySizeOutOfLimit |400 |The operation is not allowed because the memory exceeds the limit. |
|MgrConfLoadFailed |500 |Failed to load the Mgr configuration. |
|MigrateInstancePodFailed |500 |Instance migration of the server or Proxy pod failed. |
|MigratingInstanceOperationForbidden |400 |The operation is not allowed because the instance is migrating. |
|ModifyActiveCrossRegionPolicyNotSupport |400 |Modifying the active cross\-region policy is not supported. Please close the current policy and reopen it. |
|ModifyAZConfigureNotSupportForStandalone |400 |The operation is not allowed because the Standalone instance does not support changing available zone. |
|ModifyBandwidthNotSupport |400 |The operation is not allowed because the specified instance does not support modifying bandwidth. |
|ModifyEnterpriseDataLayoutNotSupport |400 |Modifying the enterprise instance data layout is not supported. |
|ModifyNodeNumberNotSupportForStandalone |400 |The operation is not allowed because the Standalone instance does not support node number modification. |
|ModifyPlannedEventExecuteTimeNotSupport |400 |The specified event does not support modifying execution time. |
|ModifyShardNumberExceedUpperDirectLink |400 |The operation is not allowed because the specified instance has direct link enabled. |
|ModifyStorageNotSupportForCache |400 |The operation is not allowed because the Standalone instance does not support modifying storage. |
|NexInvalidRollback |400 |Nex invalid rollback. |
|NodeIdsTooLong |400 |The operation is not allowed because the length of NodeIds is invalid. |
|NodeNumberNoChange |400 |The operation is not allowed because the node number for each shard does not change. |
|NodePoolNotExist |400 |The node pool does not exist. |
|NoDirectLink |400 |The operation is not allowed because the instance has no direct link. |
|NotAllowedModifyOperator |400 |Modifying the storage class is not supported. |
|NotSupportModifyAppendOnlySwitch |400 |The operation is not allowed because the standalone instance does not support modifying appendonly switch. |
|NotSupportModifyReadDistributionStrategy |400 |The operation is not allowed because the Standalone instance does not support modifying read distribution strategy. |
|OffsetOutOfRange |400 |The value for Offset is invalid. |
|OK |200 |OK. |
|OnlyOneAllowListOrOneInstance |400 |The operation is not allowed because only one allowlist or instance is accepted per request. |
|OpenDirectLinkShardNumberExceedUpper |400 |The operation is not allowed because the number of instance shards exceeds the limit. |
|OperatorBdNotReady |500 |Storage class is not ready. |
|OrderByInvalid |400 |The value for OrderBy is invalid. |
|OrderTypeInvalid |400 |The value for OrderType is invalid. |
|ParamError |400 |The request processing failed with a parameter error. |
|ParamGroupCountExceedUpper |400 |The number of parameter templates exceeds the limit. |
|ParamGroupNotExists |400 |The specified parameter template does not exist. |
|PasswordWrong |500 |The operation is not allowed because the password is wrong. |
|PlannedEventNotExist |400 |The specified event does not exist. |
|PlannedEventStatusNotMatch |400 |The operation is not allowed because the specified event status does not match. |
|PrePaidInstanceCanNotModifySpec |400 |The operation is not allowed because the charge type of the specified instance is PrePaid. |
|PrePaidInstanceCanNotRelease |400 |The operation is not allowed because the charge type of the specified instance is PrePaid. |
|PrivateAddressNotExist |400 |The operation is not allowed because the private address does not exist. |
|ProjectNameIsNeeded |400 |The specified ProjectName parameter is missing. |
|ProjectNameNotExist |400 |The specified ProjectName does not exist. |
|ProxyModeAlreadyDisabled |400 |Proxy mode is already disabled. |
|ProxyModeAlreadyEnabled |400 |Proxy mode is already enabled. |
|ProxyModeDisabled |400 |The operation is not allowed because Proxy mode is disabled. |
|PublicAddressForPrivateAlreadyCreate |400 |The operation is not allowed because the private address has already been resolved to a public address. |
|PublicAddressForPrivateNotCreate |400 |The operation is not allowed because the private address has not been resolved to a public address. |
|PublicConnectionAlreadyExist |400 |The operation is not allowed because the public connection has been enabled for the specified instance. |
|PublicConnectionNotExist |400 |The operation is not allowed because the public connection has been disabled for the specified instance. |
|PublicZoneEnabled |400 |The operation is not allowed because the specified instance has public zone visit enabled. |
|PublicZoneVisitEnabled |400 |Open all ip addresses is not allowed because the specified instance %s has public zone visit enabled. |
|PublicZoneVisitEnabledCannotOpenNoAuthMode |400 |The instance enabled public zone visit. Cannot open no auth mode. |
|QuotaNotEnough |400 |The operation is not allowed because the quota for instance amount is insufficient. |
|ReadDistributionStrategyCannotSupport |400 |The operation is not allowed because the read distribution strategy of the current instance is not supported. |
|RegionAliasNotSet |400 |The operation is not allowed because the region alias is Initializing. |
|ResourceCheckFailed |500 |Failed to check resource. |
|ResourceIDFilterMissing |400 |The Resource ID is missing in the specified Filter parameter. |
|ResourceNotEnough |500 |The operation is not allowed because the specified resource is insufficient. |
|ResourceNotExist |400 |The specified resource does not exist. |
|RestoreInstanceFailed |500 |Failed to restore the specified instance. |
|RestoreNotSupportForStandalone |400 |The operation is not allowed because the Standalone instance does not support restore. |
|RoleAclRuleInvalid |400 |The ACL rule format for the role is invalid. |
|RoleExist |400 |The specified role already exists. |
|RoleNameInvalid |400 |The role name format is invalid. |
|RoleOfInstanceExceedUpper |400 |The number of roles belonging to the specified instance exceeds the limit. |
|SealZoneVisitDisabled |400 |The operation is not allowed because the instance does not enable sale\-zone visit. |
|SecurityIpGroupAlreadyExist |400 |The specified security IP group already exists. |
|SecurityIpGroupNotExist |400 |The specified security IP group does not exist. |
|ServerError |500 |The request failed due to a temporary failure of the server. |
|ServerVersionAppendonlyOFFMutex |400 |The server version is too low; please first set the appendonly\-switch to on. |
|ServerVersionDegradeNotSupported |400 |The server version is too low to degrade. Please use higher server version. |
|ServiceRoleForRedisNotExist |400 |The ServiceRoleForRedis role does not exist. |
|ShardCapacityNoChange |400 |The operation is not allowed because the capacity of each shard does not change. |
|ShardNumberNoChange |400 |The operation is not allowed because the shard number does not change. |
|SSLEnabled |400 |The operation is not allowed because SSL is enabled. |
|StandardClusterNotSupportDirectLink |400 |The Standard Cluster instance does not support the direct link. |
|StandardUnsupportedModifyShardNumber |400 |The operation is not allowed because it is not a Sharded Cluster instance. |
|StorageClassCheckFailed |500 |Failed to check the storage class. |
|StorageClassNameCombineFailed |500 |Failed to get the storage class name. |
|StorageClassNotExist |500 |The specified storage class does not exist. |
|StorageClassRebuildFailed |500 |Failed to rebuild the storage class. |
|SubnetAvaiableIPNotEnough |400 |The operation is not allowed because the available subnet IP is insufficient. |
|SubnetIdIsNeeded |400 |The specified SubnetId parameter is missing. |
|SubnetIPv6CidrBlockNotExist |400 |The subnet has no IPv6 address. |
|SubnetNotExist |400 |The specified subnet does not exist. |
|SubnetZoneMismatch |400 |The specified zone of the subnet does not match that of the instance. |
|SwitchOverNotSupportForStandalone |400 |The operation is not allowed because the Standalone instance does not support switch over. |
|SystemBusy |500 |The operation is not allowed because the system is busy. |
|SystemMaintenance |500 |The system is under maintenance. |
|TagNotExist |400 |The specified tag does not exist. |
|TemporaryModifyCannotSupport |400 |The operation is not allowed because the PostPaid instance does not support temporary upgrade. |
|TemporaryModifyRollbackTimeOutOfRange |400 |The operation is not allowed because the rollback time exceeds the limit. |
|TimeFormatInvalid |400 |The specified time format is invalid. |
|TimeIntervalInvalid |400 |The specified time interval is invalid. |
|TimeOutOfRange |400 |Time out of range. |
|TimeSpanExceeded |400 |The operation is not allowed because the time span is exceeded. |
|TimeSpanInvalid |400 |The specified time span is invalid. |
|TosBucketNotExist |500 |The specified TOS bucket does not exist. |
|TosCallFunctionFailed |500 |Failed to call the TOS interface. |
|TosInvalidParam |500 |The specified TOS bucket parameter value is invalid. |
|TradeOrderOperationFailed |400 |Trade order operation failed. |
|UnexpectedStartTime |400 |The operation is not allowed because StartTime is later than EndTime. |
|UnsupportedClusterStorageTypeForConfig |400 |The configuration items are not supported for this cluster. Please contact the administrator. |
|UnsupportedLogType |400 |The log type is not supported. |
|UnsupportedModule |400 |The requested module is not supported. |
|UnsupportedOperatorInTemporaryModify |400 |The operation is not allowed because instance is in the temporary upgrade period. |
|UnsupportedServerVersionForConfig |400 |The configuration value cannot be set for the instance server version. Please update the server version first. |
|UnsupportedSpecReductionInTemporaryModify |400 |The operation is not allowed because temporary upgrades do not support degrading instance spec. |
|UnsupportedSubNamespace |400 |The value for SubNamespace is invalid. |
|UnsupportedTargetName |400 |The value for TargetName is invalid. |
|UpdateConfigFailed |500 |Failed to update the configuration. |
|UpdatingShardCountExceedLimit |400 |The operation is not allowed because the number of instances that modify the shard amount exceeds the limit. |
|VisitAddressNoChange |400 |The operation is not allowed because the connection address or port number does not change. |
|VpcAuthModeOpened |400 |The operation is not allowed because the specified instance %s has VPC auth mode enabled. |
|VpcIdIsNeeded |400 |The specified parameter VpcId is missing. |
|VpcIPv6CidrBlockNotExist |400 |The VPC has no IPv6 address. |
|VpcNotExist |400 |The specified VPC does not exist. |
|ZoneSoldOut |400 |The operation is not allowed because the specified available zone has been sold out. |
