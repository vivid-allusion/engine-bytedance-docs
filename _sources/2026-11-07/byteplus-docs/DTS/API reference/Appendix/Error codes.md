---
title: "Error codes"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/error_codes"
---

This topic summarizes the error codes that may occur in Database Transmission Service (DTS).


|**Type** |**Error codes** |**HTTPCode** |**Description** |
|---|---|---|---|
|Common error |InternalError |500 |Internal error. |
||MissingParameter |400 |The `{parameter1}` parameter is missing. |
||InvalidParameter |400 |The parameter `{parameter1}` value is invalid. |
|Quota |QuotaExceeded.Task |400 |Exceed the task quantity quota limit. |
||QuotaExceed.Tag |400 |The task tag quantity exceeds the quota limit. |
|Actions |OperationDenied.IncrMigrationNotSet |400 |The task does not contain increments. This operation can not be performed. |
||OperationDenied.IncrementNotSet |400 |The task has not been configured for increments. This operation can not be performed. |
||OperationDenied.TaskStatusNotSupport |400 |The current task status does not support this operation. |
||OperationDenied.ObjectNameChanged |400 |The object has been renamed. This operation can not be completed.` {parameter1}` should be renamed to `{parameter2}`. |
||OperationDenied.TaskNotInIncrStatus |400 |The task is not in the incremental state and can not perform this operation. |
||OperationDenied.TaskInChangingStatus |400 |The task is being changed and can not be executed. |
||OperationDenied.SyncObjectChanging |400 |The synchronization object is changing. This operation can not be performed. |
||OperationDenied.SyncObjectNotChange |400 |The synchronization objects have not changed, and this operation can not be performed. |
||OperationDenied.SubTaskUnchangeable |400 |Modifying subtasks is not allowed. |
||OperationDenied.SystemBusy |400 |The system is busy. Try again later. |
||OperationDenied.ChangeRunningTaskIncrStartPosition |400 |A started task is not allowed to modify the incremental starting point. |
||OperationDenied.DatabaseVersionTooLow |400 |The database version is earlier than `{parameter1}`. This operation can not be performed. |
||OperationDenied.NoBetaQualification |400 |The user is not qualified for public testing and can not perform this operation. |
||OperationDenied.InvalidChargeStatus |400 |Invalid billing status. This operation can not be performed. |
||OperationDenied.ExistRunningDataValidationTask |400 |A running verification task already exists. This operation can not be performed. |
||OperationDenied.TaskStatusUnsupported |400 |The task status is not supported. This operation can not be performed. |
||OperationDenied.DatabaseMappingNotFound |400 |`{parameter1}` can not be mapped to the destination. |
||OperationDenied.SubscriptionTypeConflict |400 |Full and incremental subscriptions can not be specified at the same time. |
||OperationDenied.OnlySupportIncrSubscription |400 |Only incremental subscription is supported. This operation can not be performed. |
||OperationDenied.IncrSubscriptionNotSet |400 |Incremental subscription is not set. This operation can not be performed. |
||OperationDenied.TaskNotPaid |400 |The task is unpaid, and this operation can not be performed. |
||Operationdenied.HasInProgressOrder |400 |The current instance has an ongoing order. End the order before trying again. |
||OperationDenied.TemporaryWhitelist |400 |The temporary allowlist is being applied for. Retry later. |
||OperationDenied.InstanceOverdue |400 |The instance is in arrears. This operation can not be performed. |
|Task |InvalidParameter.TaskNameMalformed |400 |The length must be between 1 and 64 characters. It must start with a Chinese character or a letter, and can only contain Chinese characters, letters, numbers, underscores, and hyphens. Empty values are not allowed. |
||InvalidParameter.DatabaseNameMalformed |400 |The length must be between 1 and 64 characters, and can not contain emojis. |
||InvalidParameter.Unsupported |400 |The `{parameter1}` parameter is not supported. |
||InvalidParameter.BPS |400 |BPS can not exceed {parameter1}. |
||InvalidParameter.RPS |400 |RPS can not exceed `{parameter1}`. |
||InvalidParameter.MongoDeploymentType |400 |The Mongo architecture {parameter1} does not match the actual one. |
||InvalidParameter.DataSourceCertificate |400 |The server certificate verification failed. Check whether the certificate is correct. |
||InvalidParameter.NetworkAddress |400 |Invalid IP address. |
||InvalidParameter.MigrateQueue |400 |The message queue does not exist or is not ready. |
||InvalidParameter.ShouldBeEmpty |400 |The parameter `{parameter1}` should be empty. |
||InvalidParameter.TagKeyDuplicate |400 |Duplicate Tag Keys are included. |
||InvalidParameter.ExceedTagResourceLimit |400 |The number of resources for adding or removing tags exceeds the maximum allowed at one time. |
||InvalidParameter.ExceedTagLimit |400 |The maximum number of tags added and deleted at one time is exceeded. |
||InvalidParameter.Tag |400 |The tag contains an invalid `key/value`. |
||InvalidPreCheckResult.NotFound |400 |The pre\-check results do not exist. |
||InvalidDatabase.NotFound |404 |The database ` {parameter1}` does not exist. |
||InvalidTaskId.NotFound |404 |Task ID does not exist. |
||InvalidDataValidationResult.NotFound |404 |The data verification report does not exist. |
||InvalidFunction.Overlap |400 |The target address is the same as the source address and contains identical functions. |
||InvalidView.Overlap |400 |The target address is the same as the source address and contains identical views. |
||InvalidAddress.Overlap |400 |Target address and source address. |
||InvalidProcedure.Overlap |400 |The target address is the same as the source address, and contains identical stored procedures. |
||InvalidTable.Overlap |400 |The target address is the same as the source address and contains identical tables. |
||InvalidConsumerGroupUser.AlreadyExists |400 |The user is already in the consumer group. |
||InvalidConsumerGroup.AlreadyExists |400 |The consumer group already exists. |
||InvalidTaskOrder.AlreadyExists |400 |The task order already exists. |
||InvalidConnection.AuthenticationFailed |400 |Connection authentication failed. Check if the username and password are correct. |
||InvalidConnection.Refused |400 |Remote connection refused. Check whether the IP address and port are enabled. |
||InsufficientSchedulableResources |200 |Insufficient schedulable resources. Task creation failed. [Submit a ticket ](https://console.byteplus.com/workorder/create/)to contact technical staff for support. |
|Network |InvalidNetworkAddress.Unavaiable |400 |The IP address `{parameter1}` is unavailable. |
||InvalidVpcId.NotFound |404 |Subnet ID does not exist. |
||InvalidConnection.CheckConnectionFailed |400 |Connection authentication failed. Check the network. |
|Account |Insufficient.Balance |400 |Insufficient account balance. |
||InvalidAccountPrivillege.Insufficient |400 |Failed to obtain the source database schema information. Confirm that the account has permissions for the system database. |
||OperationDenied.UnauthenticatedAccount |400 |The account has not completed real\-name verification. |
