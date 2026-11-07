---
title: "Error codes"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes"
---

This topic lists error code you may encounter when using NDB for MySQL.


|Type |Error code |Message |HttpCode |
|---|---|---|---|
|Public |InvalidParameterFormat |The input parameter is not valid. |400 |
||InvalidParameter |The specified parameter %s is not valid. |400 |
||InvalidPageNumber |PageNumber must greater or equal to 1. |400 |
||InvalidPageSize |PageSize must be between 1\-%s. |400 |
||MissingParameter |The input parameter %s that is mandatory for processing this request is not supplied. |400 |
||MissingParameter.AtLeastOneParameter |At least one parameter in the given array %v is mandatory. |400 |
||InvalidParameter.AtMostOneParameter |At most one parameter in the given array %v is mandatory. |400 |
||InternalError |The request processing has failed with internal server error. |500 |
||ServiceUnavailable |The request has failed due to a temporary failure of the server. |503 |
|Instance |InvalidNodeSpec |The NodeSpec is not invalid. Supported options are: %v. |400 |
||InvalidInstanceName |Length must be between 1\-128, must start with a letter or a Chinese character, contains only alphabets, numbers, '\-', '_' Chinese charactors or empty string. |400 |
||InvalidInstanceStatus |The Instance Status is not invalid. |400 |
||InvalidParameter.TimeZoneMalformed |Accepted Time Zone format should be like 'UTC \-12:00', 'UTC +10:00'. |400 |
||InvalidInstanceStatus.NotRunning |The specified instance is not running. |400 |
||InvalidInstanceStatus.Closed |The specified instance has closed. |400 |
||InvalidInstanceId.NotFound |The specified instance does not exist. |404 |
||InvalidNode.NotFound |Instance [%s] in Cluster [%s] is not exist. |404 |
||InvalidInstanceId.Duplicate |The specified instance already exists. |400 |
||OperationDenied.DeletionProtectionPolicyNotMatch |The operation is not permitted due to the instance enabled deletion protection. |400 |
|Allowlists |InvalidParameter.AllowListNameMalformed |Length must be between 1\-128, must start with a letter or a Chinese character, contains only alphabets, numbers, "\-", "_" and Chinese characters. |400 |
||InvalidAllowListName.Duplicate |The specified AllowList already exists. |400 |
||InvalidParameter.AllowListDescMalformed |Length must be less than 200. |400 |
||QuotaExceeded.AllowListIP |The IPs in the AllowList cannot exceed %v. |400 |
||InvalidAllowListIPList.InvalidIPList |The specified IPList exists duplicate IP address. |400 |
||QuotaExceeded.AllowList |The AllowLists in region cannot exceed %v |400 |
||InvalidAllowListId.NotFound |The specified AllowList does not exist. |404 |
||InvalidAllowListIPList.IPDuplicate |The specified IPList exists duplicate IP address. |400 |
||InvalidParameter.Unsupported |The specified %s is not supported. |400 |
||OperationDenied.ApplyInstanceNumConflict |The input parameter ApplyInstanceNum is s%, but there are v% instances applying this AllowList. |400 |
||OperationDenied.AllowListIdInuse |The operation is not permitted due to the specified AllowList is associated by instance. |400 |
||QuotaExceeded.AllowListAssociation |The specified AllowList exceeds the association limit. |400 |
||QuotaExceeded.InstanceAllowList |The specified instance exceeds the association limit. |400 |
||QuotaExceeded.InstanceAllowListIP |The IP addresses of the AllowLists associated with the specified instance exceeds the limit. |400 |
|Database |InvalidParameter.DatabaseNameMalformed |Length must be between 2\-64, must start with a low case letter, contains only low case letter, numbers, '_', '\-', and can't contains keywords, and end with a low case letter or number. |400 |
||InvalidDatabaseType |The Database Type is not invalid. |400 |
||InvalidCharacterSet |The Character Set is only support: utf8, ascii, latin1, utf8mb4. |400 |
||InvalidDatabaseName.Duplicate |The specified database name already exists. |400 |
||InvalidDatabaseName.NotFound |The specified database name does not exist. |404 |
|Backups |InvalidBackupPeriod |The Backup Period is only support: Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday. |400 |
||OperationDenied.BackupAmountOverTheLimit |The operation is not permitted due to backup amount over the limit. |400 |
||OperationDenied.BackupJobExists |The operation is not permitted due to exist running backup job. |400 |
||InvalidSnapShot.NotFound |The specified Snap Shot does not exist. |404 |
||InvalidBackupWindow |The backup windows is preferred to be 2 hours. |400 |
||OperationDenied.SnapshotNotReady |The specified snapshot %s is not ready. |400 |
||InvalidBackupId |The specified BackupId is invalid. |400 |
||InvalidParameter.ProjectMismatch |The backup does not belong to the srcproject. |400 |
|Billing |InvalidChargeType |The Charge Type is only support %v . |400 |
|Maintenance |InvalidMaintainWindow |Maintain Window should be as format 00:00 to 02:00 and duration should be 2 to 4 hours. |400 |
|Account |InvalidPrivilegeType |The Privilege Type is only support: ReadWrite ReadOnly DDLOnly DMLOnly Custom. |400 |
||InvalidPrivilegeDetail |Only custom read and write permissions are supported. |400 |
||InvalidAccountName.Duplicate |The specified Account Name already exists. |400 |
||InvalidAccountName.NotFound |The specified Account Name does not exist. |400 |
||InvalidDatabasePrivilege.Repetitive |The Database %s , Privilege %s is repetitive. |400 |
||InvalidUserPrivilege.Repetitive |The User %s , Privilege %s is repetitive. |400 |
||InvalidAccountType |The specified account type is not valid. |400 |
||InvalidParameter.UserNameMalformed |Length must be between 2\-32, must start with a low case letter, contains only low case letter, numbers, '_', and can't contains keywords, and end with a low case letter or number. |400 |
||InvalidParameter.PasswordMalformed |Length must be between 8\-32, contain at least any three of uppercase letters, lowercase letters, numbers, or special characters. |400 |
|Actions |OperationDenied.UnsupportedOperation |The operation is unsupported for the specified instance. |400 |
||OperationDenied.InvalidNode |Instance [%s] in Cluster [%s] is not reachable. |400 |
||OperationDenied.StatusNotReady |The required reboot is not allowed now. |400 |
||OperationDenied.InstanceLockMode |The operation is not permitted due to lock of instance. |403 |
||OperationDenied.InstanceMaintaining |The operation is not permitted due to the instance being maintained. |400 |
|Network connection |InvalidVpcId.NotFound |The specified VPC ID does not exist. |404 |
||InvalidSubnetId.Unavailable |The specified SubnetId is unavailable. |400 |
||InvalidEipId.Unavailable |The specified EipId is unavailable. |400 |
||EndpointLimitExceed |The custom endpoints of specified instance exceed its limit. |400 |
||InvalidEndpointId.NotFound |The specified EndpointId does not exist. |400 |
||InvalidEndpointId.NotAllowed |The specified EndpointId is not allowed. |400 |
||OperationDenied.InvalidEndpointStatus |The operation is not allowed because the specified endpoint %s needs at least one node. |400 |
||InvalidParameter.DnsConflict |Dns is already used, connection address:%s. |400 |
||InvalidParameter.DomainPrefixMalformed |The domain prefix does not conform to the specification. |400 |
||InvalidParameter.PortMalformed |Port must be between 1000\-65534. |400 |
