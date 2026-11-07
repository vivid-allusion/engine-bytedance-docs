---
title: "API overview"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/api-overview"
---

This topic summarizes the APIs provided by Database Workshop (DBW).

## Compliance Agreement

|API |Description |
|---|---|
|[AgreeUserProtocol](https://docs.byteplus.com/en/docs/DBW/AgreeUserProtocol?lang=en) |Call the AgreeUserProtocol API to agree to the Database Workshop DBW user agreement. |

## Instance access

|**API** |**Description** |
|---|---|
|[DataConnectInstance](https://docs.byteplus.com/en/docs/DBW/dataconnectinstance) |Call the DataConnectInstance API to connect to the instance. |

## SQL Task

|**API** |**Description** |
|---|---|
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands API to execute the command set synchronously. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive API to keep an SQL session alive. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession API to close an SQL session. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Call the DataCancelExec interface to cancel SQL execution. |
|[DataExecCommandSetAsync](https://docs.byteplus.com/en/docs/DBW/dataexeccommandsetasync) |Call the DataExecCommandSetAsync API to asynchronously execute a set of commands. |
|[DataGetCommandSetResult](https://docs.byteplus.com/en/docs/DBW/datagetcommandsetresult) |Call the DataGetCommandSetResult API to query the execution results of the asynchronous execution command set. |
|[DataDescribeCommandSet](https://docs.byteplus.com/en/docs/DBW/DataDescribeCommandSet) |Call the DataDescribeCommandSet to query the execution status of the command set. |
|[GenerateSQLFromNL](https://docs.byteplus.com/en/docs/DBW/GenerateSQLFromNL) |Call the GenerateSQLFromNL API to generate SQL statements from natural language. |
|[ExecuteSQL](https://docs.byteplus.com/en/docs/DBW/ExecuteSQL) |Call the ExecuteSQL API to execute SQL statements. |
|[ListDatabases](https://docs.byteplus.com/en/docs/DBW/ListDatabases) |Call the ListDatabases API to query the database list of the instance. |
|[ListTables](https://docs.byteplus.com/en/docs/DBW/ListTables) |Call the ListTables API to query the table list in the database of the instance. |
|[GetTableInfo](https://docs.byteplus.com/en/docs/DBW/GetTableInfo) |Call the GetTableInfo API to query table metadata of the database instance. |

## Persistent Kill

|API |Description |
|---|---|
|[CreateSqlKillRule](https://docs.byteplus.com/en/docs/DBW/createSqlKillRule?lang=en) |Call the CreateSqlKillRule API to create persistent Kill tasks. |
|[StopSqlKillRule](https://docs.byteplus.com/en/docs/DBW/stopsqlkillrule?lang=en) |Call the StopSqlKillRule API to stop persistent Kill tasks. |
|[DeleteSqlKillRule](https://docs.byteplus.com/en/docs/DBW/deletesqlkillrule?lang=en) |Call the DeleteSqlKillRule API to delete persistent Kill tasks. |
|[DescribeSqlKillRules](https://docs.byteplus.com/en/docs/DBW/describesqlkillrules?lang=en) |Call the DescribeSqlKillRules API to query persistent Kill tasks. |

## Operation and maintenance management

|API ||Description |
|---|---|---|
|SQL throttling |[DescribeSqlKeywords](https://docs.byteplus.com/en/docs/DBW/DescribeSqlKeywords?lang=en) |Call the DescribeSqlKeywords API to generate SQL throttling keywords based on the original SQL statement. |
||[CreateSqlConcurrencyControlRule](https://docs.byteplus.com/en/docs/DBW/CreateSqlConcurrencyControlRule?lang=en) |Call the CreateSqlConcurrencyControlRule API to create a SQL rate limiting task. |
||[DescribeSqlConcurrencyControlRules](https://docs.byteplus.com/en/docs/DBW/DescribeSqlConcurrencyControlRules?lang=en) |Call the DescribeSqlConcurrencyControlRules API to query all SQL throttling tasks for the database instance. |
||[StopSqlConcurrencyControlRule](https://docs.byteplus.com/en/docs/DBW/StopSqlConcurrencyControlRule?lang=en) |Call the StopSqlConcurrencyControlRule API to stop the SQL throttling task. |
||[RestartSqlConcurrencyControlRule](https://docs.byteplus.com/en/docs/DBW/RestartSqlConcurrencyControlRule?lang=en) |Call the RestartSqlConcurrencyControlRule API to enable a suspended SQL throttling task. |
||[DeleteSqlConcurrencyControlRule](https://docs.byteplus.com/en/docs/DBW/DeleteSqlConcurrencyControlRule?lang=en) |Call the DeleteSqlConcurrencyControlRule API to delete SQL throttling tasks. |
|Audit log management |[DescribeAuditLogDetail](https://docs.byteplus.com/en/docs/DBW/describeauditlogdetail?lang=en) |Calls the DescribeAuditLogDetail API to query the detailed information of audit logs. |
|Slow log and optimization suggestions |[DescribeSlowLogs](https://docs.byteplus.com/en/docs/DBW/describeslowlogs) |Call the DescribeSlowLogs API to query slow log information. |
||[DescribeAggregateSlowLogs](https://docs.byteplus.com/en/docs/DBW/describeaggregateslowlogs?lang=en) |Call the DescribeAggregateSlowLogs API to get the aggregation information of slow logs. |
||[ListSlowQueryAdviceApi](https://docs.byteplus.com/en/docs/DBW/ListSlowQueryAdviceApi) |Call the ListSlowQueryAdviceApi API to get detailed slow log diagnosis information. |
||[SlowQueryAdviceTaskHistoryApi](https://docs.byteplus.com/en/docs/DBW/SlowQueryAdviceTaskHistoryApi) |Call the SlowQueryAdviceTaskHistoryApi API to obtain historical slow log diagnosis information. |
|Transactions and locks |新增[AnalyzeTrxAndLock](https://docs.byteplus.com/en/docs/dbw/analyzetrxandlock?lang=en) |Call the AnalyzeTrxAndLock API to create a transaction and lock analysis task. |
||新增[DescribeTrxAndLockAnalysisTasks](https://docs.byteplus.com/en/docs/dbw/describetrxandlockanalysistasks?lang=en) |Call the DescribeTrxAndLockAnalysisTasks API to query the transaction and lock analysis task list. |
||新增[DescribeTrxAndLockAnalysisTaskResults](https://docs.byteplus.com/en/docs/dbw/describetrxandlockanalysistaskresults?lang=en) |Call the DescribeTrxAndLockAnalysisTaskResults API to query transaction and lock analysis results that meet the query conditions. |
|Diagnostics and Snapshots |[DescribeDialogDetailSnapshot](https://docs.byteplus.com/en/docs/DBW/DescribeDialogDetailSnapshot?lang=en) |Call the DescribeDialogDetailSnapshot API to query the details of session information in a session snapshot. |
||[DescribeDialogSnapshots](https://docs.byteplus.com/en/docs/DBW/DescribeDialogSnapshots?lang=en) |Call the DescribeDialogSnapshots API to query the list of session snapshot time points. |
||[DescribeEngineStatusSnapShot](https://docs.byteplus.com/en/docs/DBW/DescribeEngineStatusSnapShot?lang=en) |Call the DescribeEngineStatusSnapShot API to query session snapshot engine status details. |
||[DescribeInstanceDasSnapShotCollectionStatus](https://docs.byteplus.com/en/docs/DBW/DescribeInstanceDasSnapShotCollectionStatus?lang=en) |Call the DescribeInstanceDasSnapShotCollectionStatus API to query the session snapshot collection state and backoff policy state of the specified database instance. |
||[ModifyInstanceDasSnapshotCollectionSwitch](https://docs.byteplus.com/en/docs/DBW/ModifyInstanceDasSnapshotCollectionSwitch?lang=en) |Call the ModifyInstanceDasSnapshotCollectionSwitch API to modify the session snapshot collection feature. |
|SQL insights and auditing |[PreCheckCreateFullSql](https://docs.byteplus.com/en/docs/DBW/PreCheckCreateFullSql?lang=en) |Call the PreCheckCreateFullSql API to enable full SQL insight. |
||[CreateTerminateFullSqlOrder](https://docs.byteplus.com/en/docs/DBW/CreateTerminateFullSqlOrder?lang=en) |Call the CreateTerminateFullSqlOrder API to create a termination order for the specified full SQL instance. |
||[CreateFullSqlOrder](https://docs.byteplus.com/en/docs/DBW/CreateFullSqlOrder?lang=en) |Call the CreateFullSqlOrder API to create a full SQL subscription order for the specified instance. |
||[GetFullSqlInstanceCorrespondence](https://docs.byteplus.com/en/docs/DBW/GetFullSqlInstanceCorrespondence?lang=en) |Call the GetFullSqlInstanceCorrespondence API to query the instance mapping relationship for FullSQL. |
||[DescribeFullSqlStatus](https://docs.byteplus.com/en/docs/DBW/DescribeFullSqlStatus?lang=en) |Call the DescribeFullSqlStatus API to query the full SQL enablement status, feature status, and subscription configuration of a specified instance. |
||[DescribeFullSQLFingerprintExample](https://docs.byteplus.com/en/docs/DBW/DescribeFullSQLFingerprintExample?lang=en) |Call the DescribeFullSQLFingerprintExample operation to query full SQL detail samples based on SQL fingerprints. |
||[DescribeSqlTemplatesContrast](https://docs.byteplus.com/en/docs/DBW/DescribeSqlTemplatesContrast?lang=en) |Call the DescribeSqlTemplatesContrast API to query the aggregated indicator comparison of full SQL templates in two time periods. |
||[DescribeSQLExecItemMetric](https://docs.byteplus.com/en/docs/DBW/DescribeSQLExecItemMetric?lang=en) |Call the DescribeSQLExecItemMetric API to query the metric curve of a single execution indicator for a specific SQL fingerprint within a specified time range. |
|AutoOps |[AutoScale](https://docs.byteplus.com/en/docs/DBW/AutoScale?lang=en) |Call the AutoScale API to configure scaling rules. |
||[DescribeAutoScaleEvents](https://docs.byteplus.com/en/docs/DBW/DescribeAutoScaleEvents?lang=en) |Call the DescribeAutoScaleEvents API to query scaling events for the specified instance. |
||[DescribeAutoScaleRules](https://docs.byteplus.com/en/docs/DBW/DescribeAutoScaleRules?lang=en) |Call the DescribeAutoScaleRules API to query Automatic Or Scheduled scaling configurations for an instance. |

## Ticket management

|**API** |Description |
|---|---|
|[CreateDmlSqlChangeTicket](https://docs.byteplus.com/en/docs/DBW/CreateDmlSqlChangeTicket) |Call the CreateDmlSqlChangeTicket API to create a DML data change ticket. |
|[CreateDdlSqlChangeTicket](https://docs.byteplus.com/en/docs/DBW/CreateDdlSqlChangeTicket) |Call the CreateDdlSqlChangeTicket API to create a DDL structural change ticket. |
|[DescribeTickets](https://docs.byteplus.com/en/docs/DBW/DescribeTickets) |Call the DescribeTickets API to query tickets in batch. |
|[DescribeTicketDetail](https://docs.byteplus.com/en/docs/DBW/DescribeTicketDetail) |Call the DescribeTicketDetail API to query the details of a single ticket. |
|[DescribeWorkflow](https://docs.byteplus.com/en/docs/DBW/DescribeWorkflow) |Call the DescribeWorkflow API to query approval ticket details. |
|[WorkflowAction](https://docs.byteplus.com/en/docs/DBW/WorkflowAction) |Call the WorkflowAction API to approve a ticket. |
|[ManualExecuteTicket](https://docs.byteplus.com/en/docs/DBW/ManualExecuteTicket) |Call the ManualExecuteTicket API to manually execute the ticket. |
|[DescribePreCheckDetail](https://docs.byteplus.com/en/docs/DBW/describePreCheckDetail?lang=en) |Call the DescribePreCheckDetail API to query the pre\-check results of a ticket. |

## Security control

|**API** |Description |
|---|---|
|[DescribeSecurityGroups](https://docs.byteplus.com/en/docs/DBW/DescribeSecurityGroups) |Call the DescribeSecurityGroups API to query security rule sets. |
|[ListApprovalFlowConfig](https://docs.byteplus.com/en/docs/DBW/ListApprovalFlowConfig) |Call the ListApprovalFlowConfig API to query the approval workflow list. |
|[ListApprovalNode](https://docs.byteplus.com/en/docs/DBW/ListApprovalNode) |Call the ListApprovalNode API to query approval nodes. |
|[DescribeManagedUsers](https://docs.byteplus.com/en/docs/DBW/DescribeManagedUsers) |Call the DescribeManagedUsers API to query user information. |
|[EnableInstanceManagement](https://docs.byteplus.com/en/docs/DBW/EnableInstanceManagement) |Call the EnableInstanceManagement API to enable security control for the database instance. |
|[UpdateInstanceManagementConfig](https://docs.byteplus.com/en/docs/DBW/UpdateInstanceManagementConfig) |Call the UpdateInstanceManagementConfig API to modify security control information. |
|[DisableInstanceManagement](https://docs.byteplus.com/en/docs/DBW/DisableInstanceManagement) |Call the DisableInstanceManagement API to disable security control. |
