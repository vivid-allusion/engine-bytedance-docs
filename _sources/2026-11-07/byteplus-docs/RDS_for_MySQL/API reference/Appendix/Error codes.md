---
title: "Error codes"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code"
---

This topic lists error code you may encounter when using RDS for MySQL.


|HTTP status code |Error Codes |**Description** |
|---|---|---|
|400 |AccountNotExist |The account was not found. |
|400 |AccountNumExceedLimit |The number of accounts in the current instance exceeds the maximum. |
|400 |AccountPrivilegeInsufficient |Insufficient account permissions. |
|400 |BackupAmountOverTheLimit |The number of databases or tables exceeds the maximum. |
|400 |ChangeNodeIsMaster |The current node is the primary node. |
|400 |ChargeOrderExists |A billing order already exists. |
|400 |DatabaseNotExist |The database was not found. |
|400 |InstanceCPUTooSmall |Instance CPU cannot be smaller than %s core. |
|400 |InstanceHasClosed |The current instance has been shut down. |
|400 |InstanceIsNotRunning |The current instance status is not running. |
|400 |InstanceMemoryTooSmall |The instance memory cannot be less than %s GB. |
|400 |InstanceNameDuplicate |The instance name already exists. |
|400 |InstanceSpecLessThanMaster |Parameter %s value is invalid. It cannot be less than the primary instance value. |
|400 |InstanceStorageSpaceTooLarge |The instance storage space cannot be greater than %s GB. |
|400 |InstanceStorageSpaceTooSmall |The instance storage space cannot be less than %s GB. |
|400 |InstanceUnchangeable |The current instance cannot be changed in the current period. |
|400 |InsufficientBalance |The account balance is insufficient. |
|400 |InvalidAccountName_Duplicate |This account name already exists. |
|400 |InvalidAccountName_Keyword |An account name cannot be a reserved keyword. |
|400 |InvalidAccountPassword_Weak |The account password is too weak. |
|400 |InvalidAccountType_Duplicate |The privileged account already exists. |
|400 |InvalidDBName_Duplicate |The database already exists. |
|400 |InvalidDBName_Keyword |A database name cannot be a reserved keyword. |
|400 |InvalidParameter |Parameter %s value is invalid. |
|400 |InvalidParameterFormat |Abnormal parameter. |
|400 |InvalidSecurityIPList |An invalid IP address exists. |
|400 |InvalidSecurityIPList_Duplicate |An allowlist already exists. |
|400 |InvalidSecurityIPList_IPExist |Duplicate IP addresses exist in the current allowlist. |
|400 |InvalidSecurityIPList_IPGroupExceedLimit |The number of allowlists of the current instance exceeds the maximum. |
|400 |InvalidSecurityIPList_IPNumExceedLimit |The number of IP addresses in the current allowlist array exceeds the maximum. |
|400 |InvalidSubnetId |The subnet parameter value is invalid or not in the same availability zone as the node. |
|400 |InvalidTemplateName_Duplicate |The parameter template name already exists. |
|400 |MaintainTime_ConflictWith_BackupTime |The maintenance period cannot be within automatic backup period %s. |
|400 |MissingParameter |Missing %s parameter. |
|400 |NameDuplicate |Name %s already exists. |
|400 |NotSatisfiedMasterChangeCondition |The conditions for a primary node switch are not satisfied. Please try again later. |
|400 |OperationDenied_AddressExists |The current endpoint already has an address of the same type, so this operation cannot be performed. |
|400 |OperationDenied_BackupJobExists |The current instance is executing a backup task, so the operation cannot be performed. |
|400 |OperationDenied_ChargeDisabled |The billing service is not enabled, so the operation cannot be performed. |
|400 |OperationDenied_DiskSpaceInsufficient |The disk space is insufficient. |
|400 |OperationDenied_DownloadBackupJobExists |The current instance is executing a backup download task, so the operation cannot be performed. |
|400 |OperationDenied_ExistLargeDelaySlaveNode |The delay time of the secondary node is long, so the operation cannot be performed. |
|400 |OperationDenied_ImportJobExists |The current instance is executing a data import task, so the operation cannot be performed. |
|400 |OperationDenied_IncrBackupUnsupportRecovery |The operation cannot be performed for incremental backup. |
|400 |OperationDenied_InstanceClosed |The current instance is shut down, so the operation cannot be performed. |
|400 |OperationDenied_InstanceIsNotRecycled |The current instance status is not "reclaiming". |
|400 |OperationDenied_InstanceMaintaining |The current instance is in maintenance, so the operation cannot be performed. |
|400 |OperationDenied_InstancePrepaid |The billing method of the current instance is pre paid, so the operation cannot be performed. |
|400 |OperationDenied_KMSDisabled |KMS service is not enabled, so the operation cannot be performed. |
|400 |OperationDenied_MgrBusy |Other tasks are being executed, so the operation cannot be performed. |
|400 |OperationDenied_NotExistLowDelaySlaveNode |No secondary node with a short delay time exists, so the operation cannot be performed. |
|400 |OperationDenied_NotExistRunningReadOnlyInstance |No running read\-only instance exists in the current instance, so the operation cannot be performed. |
|400 |OperationDenied_NotExistRunningReadOnlyNode |No running read\-only node exists in the current instance, so the operation cannot be performed. |
|400 |OperationDenied_OnlineDDLJobExists |The current instance is executing an Online DDL task, so the operation cannot be performed. |
|400 |OperationDenied_OnlineDDLJobFinished |The current task has been completed, so the operation cannot be performed. |
|400 |OperationDenied_SystemGroup |The current allowlist is the default for the system, so the operation cannot be performed. |
|400 |OperationDenied_SystemTemplate |The current parameter template is a system parameter template, so the operation cannot be performed. |
|400 |OperationDenied_TDEEnabled |The TDE function has been enabled, so the operation cannot be performed. |
|400 |OperationUnsupported |Operation not supported. |
|400 |OperationUnsupported_MySQL56 |The operation is not supported by MySQL 5.6 version. |
|400 |OperationUnsupported_MySQL80 |The operation is not supported by MySQL 8.0 version. |
|400 |PrecheckFailed_CannotConnectMysql |Database connection failed. |
|400 |PrecheckFailed_DbNotExists |The destination database does not exist. |
|400 |PrecheckFailed_DiskSpaceInsufficient |The disk space is insufficient. |
|400 |PrecheckFailed_DryRunFailed |Pre\-execution failed. |
|400 |PrecheckFailed_DuplicateKeyOrColumn |Duplicate indexes or columns exist. |
|400 |PrecheckFailed_KeyOrColumnNotExists |Indexes or columns do not exist. |
|400 |PrecheckFailed_NoPrimaryKey |A table must have a primary key or a unique index. |
|400 |PrecheckFailed_SQLSyntaxError |Incorrect or unsupported SQL syntax. |
|400 |PrecheckFailed_SQLUnsupported |SQL statement not supported. |
|400 |PrecheckFailed_TableNotExists |The destination table does not exist. |
|400 |ReadOnlyInstanceNotExists |No read\-only instance exists in the current instance, so the operation cannot be performed. |
|400 |ReadOnlyInstanceNumExceedLimit |The number of read\-only instances in the current instance exceeds the maximum. |
|400 |ReadOnlyNodeNotExists |No read\-only node exists in the current instance, so the operation cannot be performed. |
|400 |RunningOrderNumExceedLimit |The number of tasks currently running exceeds the maximum. |
|400 |SQLSyntaxErrorOrUnsupported |The current SQL statement has syntax errors, or is not supported. |
|400 |UnsupportedParameter |%s parameter not supported. |
|400 |UserBackupAmountOverTheLimit |The number of manual backups exceeds the maximum. |
|400 |OperationUnsupported_MySQL55 |This operation is not supported in MySQL version 5.5. |
|400 |OperationUnsupported_Instance |The current instance does not support this operation: %s. |
|400 |OperationDenied_JobExists |The current instance has the same unfinished task and the operation cannot be performed. |
|400 |OperationDenied_SomeParamsMustBeAppliedToAllNodes |There is a parameter that must be applied to all nodes: %s, the operation cannot be performed. |
|400 |InvalidSecurityGroupId |The specified security group %s is invalid. |
|400 |InvalidSecurityGroupId_SGNumExceedLimit |The number of specified security groups cannot exceed %s. |
|400 |DownloadFileSizeExceedLimit |The current download file size exceeds the upper limit. |
|400 |DownloadTaskNotExists |The current file download task does not exist. |
|400 |OperationDenied_Unexpired_Data_Backup |This operation cannot be performed for unexpired data backup. |
|400 |OperationDenied_System_Data_Backup |System data backup does not support this operation. |
|400 |OperationDenied_TempModify_ChargeTypeUnsupported |The current charging type does not support this operation. |
|400 |OperationDenied_TempModify_ReduceNodeUnsupported |Read\-only nodes cannot be deleted/downgraded during temporary upgrade. |
|400 |OperationDenied_TempModify_ReduceStorageUnsupported |Storage space cannot be reduced during temporary upgrade. |
|400 |OperationDenied_TempModify_ReduceSpecUnsupported |Specifications cannot be reduced during temporary upgrade. |
|400 |OperationDenied_TempModify_InstanceDeleteUnsupported |The instance cannot be unsubscribed during the temporary upgrade. |
|400 |OperationDenied_TempModify_InstanceReclaimTimeLimit |The restore time cannot be greater than the expiration time. |
|400 |OperationDenied_TempModify_InstanceContinueTimeLimit |The restore time must be greater than the current restore time. |
|400 |OperationDenied_TempModify_InstanceDurationTimeLimit |The temporary upgrade duration is too long. |
|400 |InvalidAccountName_SuperOnly |The account name can only be used as a high\-privilege account. |
|400 |OperationDenied_NotExistDatabase |The database table information does not exist in the current instance and the operation cannot be performed. |
|400 |OperationDenied_CaseSensitiveDatabase |The database name is in uppercase. Only when the parameter lower_case_table_names is 0, deletion of this database is supported. |
|400 |InstancesExceeded_BindTags |The number of instances of single binding tags exceeds %s. |
|400 |TagsExceeded_BindTags |The number of tags bound at a time exceeds %s. |
|400 |InvalidCCLRule_Duplicate |The current limiting rule already exists. |
|400 |OperationDenied_CCLRule_CCLClosed |The current limiting rule has been closed and the operation cannot be performed. |
|400 |ReadOnlyNodeBindEndpointWithOtherNode |This read\-only node has bound a terminal to other nodes, please unbind it first |
|400 |ReadOnlyNodeHasOpenDelayRepl |The read\-only node has enabled delayed replication and is not allowed to bind terminals to other nodes |
|400 |OperationUnsupported_SameNetworkConfig |The network configuration is the same, no switching is required |
|400 |InvalidParameterValue_NonBlockSizeMultiple |The value of parameter %s needs to be a multiple of %s. |
|400 |OperationDenied_ControlComponentUpgrading |The platform component is being upgraded, but the instance is still running normally. Please try again later. |
|400 |OperationDenied_ExistMaintainTask |The instance operation and maintenance task already exists. |
|400 |InvalidParameterValue_ExpressionUnsupported |Parameter %s does not support custom expressions. |
|400 |InvalidParameterValue_InvalidExpressionFormat |The expression %s is malformed. |
|400 |OperationDenied_AddNodeNumExceedLimit |The number of nodes that can be added at a time exceeds the upper limit. |
|400 |OperationDenied_DefaultAllowListDelete |The default allowlist prohibits deletion. |
|403 |Forbidden_Authentication |The account has not completed real\-name authentication. |
|403 |OperationDenied_InstanceLockMode |Instance lock conflict, please try again later. |
|403 |OperationDenied_ResourceSoldOut |The current availability zone has insufficient resources. |
|403 |QuotaExceeded_CreateInstance |Quota limit exceeded. |
|404 |AddressNotFound |No address of this network type is found. |
|404 |BackupNotFound |No available backup records found. |
|404 |EndpointNotFound |No endpoint found. |
|404 |InstanceNotFound |The instance was not found. |
|404 |ProjectNotFound |The project was not found. |
|404 |SecurityIPListGroupNotFound |The allowlist array was not found. |
|404 |SubnetIDNotFound |Subnet ID was not found. |
|404 |TemplateNotFound |The parameter template was not found. |
|404 |TemplateTypeNotMatch |No match for the current parameter template type. |
|404 |VpcIDNotFound |The VpcId was not found. |
|429 |OperationDenied_QpsRateLimit |Frequent operations, please try again later. |
|500 |InternalError |Internal error. |
|500 |ServiceBusy |The system is busy, please try again later. |
|500 |InternalServiceError |Service internal error: %s. |
|503 |ServiceUnavailable |The current service is temporarily unavailable. |
