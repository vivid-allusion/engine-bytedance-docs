---
title: "Error code"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/error-codes"
---

This article introduces the error codes that may appear in Database Workshop (DBW).


|**HTTPCode** |**Error code** |**Description** |
|---|---|---|
|500 |CurrentUserNotDbwUser |The current user is not a DBW user |
|500 |SecurityRuleCheckFailed |Security rule verification failed. |
|500 |NotSupportInstanceType |The instance type is not supported. |
|500 |CheckConnectionFailed |Verification connection failed. |
|500 |AlreadyEnableInstanceManagement |The current instance has enabled security control. |
|500 |TenantNotFound |Tenant information not found. |
|500 |EmptyInputSql |SQL text is empty. |
|500 |UnsupportIputSqlType |The entered SQL type is not supported. |
|500 |InputSqlNumExceedLimit |The number of SQL statements exceeds the maximum limit. |
|500 |ExecuteTypeNotSupport |Unsupported ticket execution type. |
|500 |CreateDdlSqlChangeTicketError |Failed to create DDL ticket. |
|500 |InternalError |Internal error. |
|500 |ParamError |Parameter error |
|500 |CreateSessionError |Failed to create session. |
|500 |TooManyConnectionsError |Too many connections. |
|500 |SessionNotExistError |Session timed out or does not exist. |
|500 |CreateSessionConnectionError |Failed to create connection. |
|500 |CommandTooLarge |Command is too long. |
|500 |ExplainCommandError |Unable to parse command. |
|500 |ConnectionBusy |Connection occupied. |
|500 |InvalidConnection |Disconnected. |
|500 |CommandNotFound |Command does not exist. |
|500 |DataSourceOpFail |Failed to read/write data source. |
|500 |CancelCommandFail |Cancel command failed. |
|500 |ConnectionFailed |Failed to connect to data source. |
|500 |ConnectionNotExist |Connection does not exist. |
|400 |ListAccountFail |Query account failed |
|400 |ModifyTaskNotAllowed |Modifying tasks is not allowed. |
|400 |TaskNotPaid |Task not paid. |
|400 |ChargeTypeInvalid |The order type is incorrect. |
|400 |DataValidationResultNotFound |Data validation report does not exist. |
|500 |ChargeStatusInvalid |Illegal payment status |
|500 |SyncConfigChangeForbidden |This synchronized configuration item does not allow changes. |
|500 |OrderExist |Order for instance already exists. |
|500 |AccountNotReal |Unfinished identity verification. |
|500 |AccountBalanceLack |Insufficient account balance |
|500 |CreateOrderFailed |Failed to create order. |
|500 |ProductTypeInvalid |Failed to create order. |
|500 |ResourceNotFoundInvalid |No relevant resources were found. |
|500 |RepeatCreateResourceError |Resources cannot be created repeatedly |
|500 |RdsStatusNotRunning |RDS instance status is abnormal |
|500 |MetaDBQueryError |Query metadata library failed. |
|500 |BillServiceCallFail |Query billing service failed. |
|500 |InstanceAlreadyCreating |Instance is already being created |
|404 |InstanceNotFound |Instance does not exist. |
|500 |NotSupportSsl |SSL encrypted database instance is temporarily not supported. |
|500 |NotSupportMultiTasks |Instance does not support running multiple import or export tasks simultaneously. |
|500 |SqlRuleKeyWordsRepeatedErr |SQL throttling rule keywords cannot be repeated. |
|500 |SqlRuleMaxNumsErr |The maximum number of SQL rate limiting rules is 128. |
|500 |SqlRuleNotRunning |The rate limiting rule is running. |
|500 |ProxyModeDisabled |The Instance is not enabled Proxy. |
|500 |NotSupportAction |The current status does not support this operation. |
|500 |NotSupportSymbol |There are unsupported characters. |
|500 |NotSupportInstanceType |The instance type is not supported. |
|500 |NotSupportSqlLevelKeyWord |Rate limiting keywords of SQL type are not supported. |
|500 |CheckConnectionFailed |Connection failed. Check the username and password. |
|500 |UserMgmtPermissionDeny |User management is only available to administrators. |
|500 |TicketStatusNotCompleted |This instance has a ticket in workflow. |
|500 |UserIsExisted |Joined users cannot be added again. |
|500 |TicketIsNotExisted |Unable to find ticket information. |
|500 |TicketStatusNotSatisfy |Ticket status does not meet execution conditions. |
|500 |RecordNotFound |Query record does not exist. |
|500 |AlreadyEnableInstanceManagement |This instance is under Security Control. |
|500 |ExecuteCommandFailed |Run command error. |
|500 |PrivilegeMaxEffectTimeErr |The maximum effective time for permissions is 1 year. |
|500 |UserNotJoinUserMgmt |The user has not joined User management. |
|500 |SqlDurationMaxNumsErr |The maximum SQL rate limiting duration is 10000 minutes. |
|500 |InstanceStatusNotSatisfy |Instance status does not meet the conditions, check whether security control is enabled for the instance. |
|500 |PrivilegesNotFound |Permission does not exist. |
|400 |SessionIdParamError |SessionID should not be empty. |
|400 |InstanceIdParamError |InstanceID should not be empty |
|400 |InstanceTypeParamError |InstanceType should not be empty. |
|400 |TaskIdParamError |TaskID should not be empty. |
|400 |ObjectNameParamError |Object name should not be empty. |
|400 |TimeRangeError |The execution time must be later than the creation time and is only valid within the last 24 hours. |
|400 |ExportContentParamError |The CSV format cannot export any structure content. |
|500 |GetTempCredentialFailed |Failed to obtain temporary credentials. |
|500 |GetAvailableDaysFailed |Failed to obtain available time. |
|500 |GetLatestDiskUsageFailed |Failed to get disk usage. |
|500 |GetStorageSpaceFailed |Failed to get instance details. |
|500 |ModifyInstanceAllowListFailed |Failed to modify instance allowlist. |
|500 |AddPrivilegeToDBFailed |Failed to add permissions to database. |
|400 |PaginationParamError |Paging parameter error. |
|400 |QueryTimeRangeError |Query time range error. |
|500 |GetMonitorDataFailed |Failed to obtain CloudTrail data. |
|400 |IntervalParamError |Interval must be greater than 0. |
|400 |InvalidEndpoint |Invalid end point.Invalid end point |
|400 |InvalidDatabase |Invalid database. |
|400 |InputParamError |Request parameter `{parameter1}` error. |
|500 |CommandSetExecuteTimeout |Run command set timeout. |
|400 |CommandSetEmpty |Command set is empty. |
|400 |CheckSessionFailed |Failed to verify SessionID. |
|403 |NotSupportUseTheFunction |This feature does not support tenants |
|400 |InstanceTypeNotSupport |This feature does not support this instance type. |
|500 |InspectionCronCreateError |Failed to create automatic inspection Cron task |
|400 |WaitForRetryError |Retry later. |
|400 |SqlParseFailed |Check whether the SQL syntax is correct or compatible |
|200 |OK |Succeeded |
|400 |ParamError |Parameter error |
|404 |ResourceNotFoundInvalid |No relevant resources were found. |
|500 |InternalError |System internal error. |
