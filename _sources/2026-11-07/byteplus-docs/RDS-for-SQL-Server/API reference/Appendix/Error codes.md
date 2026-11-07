---
title: "Error codes"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/error-codes"
---

This article summarizes the error codes that can occur in SQL Server editions of cloud databases.


|**error code** |**HTTPCode** |**describe** |
|---|---|---|
|InternalError |500 |Internal error. |
|TosRestoreTaskNumExceedLimit |500 |There are too many tasks in progress. Please submit them later. |
|InvalidParameterFormat |400 |Exception parameters. |
|InvalidParameter |400 |The parameter `{parameter1}` value is invalid. |
|TosRestoreTaskDbVerifyFailed |400 |DB validation failed due to `{parameter1}`. |
|InvalidDBName_Duplicate |400 |The database already exists. |
|MissingParameter |400 |Missing `{parameter1}` parameter. |
|OperationDenied_IncrBackupUnsupportRecovery |400 |Incremental backup cannot perform this operation. |
|OperationDenied_ImportJobExists |400 |The current instance is performing a data import task and cannot perform the operation. |
|InstanceIsNotRunning |400 |The current instance state is not running. |
|OperationUnsupported |400 |Operation is not supported. |
|OperationDenied_BackupJobExists |400 |The current instance is performing a backup task and cannot perform the operation. |
|UserBackupAmountOverTheLimit |400 |The number of manual backups exceeded the limit. |
|OperationDenied_ResourceSoldOut |403 |The current Availability Zone is under\-resourced. |
|QuotaExceeded_RestoreDB |403 |The recovery database exceeded the quota limit. |
|BackupNotFound |404 |No available backup records were found. |
|InstanceNotFound |404 |The instance was not found. |
