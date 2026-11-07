---
title: "API History"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/API_release_history"
---

This topic summarizes the API changes for Database Workshop (DBW).

## November 2026

|API |Release time |Change log |Associated feature |
|---|---|---|---|
|新增[AnalyzeTrxAndLock](https://docs.byteplus.com/en/docs/dbw/analyzetrxandlock?lang=en) |2026\-11\-03 |Call the AnalyzeTrxAndLock API to create a transaction and lock analysis task. |* [Transaction and lock management](https://docs.byteplus.com/en/docs/DBW/lock-analysis-management-for-mysql?lang=en) (MySQL)<br><br>* [Transaction and lock management](https://docs.byteplus.com/en/docs/DBW/Transaction_and_lock_management?lang=en) (NDB MySQL)<br><br>* [Transaction and lock management](https://docs.byteplus.com/en/docs/DBW/transaction-and-lock-management?lang=en) (PostgreSQL) |
|新增[DescribeTrxAndLockAnalysisTasks](https://docs.byteplus.com/en/docs/dbw/describetrxandlockanalysistasks?lang=en) |2026\-11\-03 |Call the DescribeTrxAndLockAnalysisTasks API to query the transaction and lock analysis task list. ||
|新增[DescribeTrxAndLockAnalysisTaskResults](https://docs.byteplus.com/en/docs/dbw/describetrxandlockanalysistaskresults?lang=en) |2026\-11\-03 |Call the DescribeTrxAndLockAnalysisTaskResults API to query the transaction and lock analysis results that meet the query conditions. ||

## October 2026

|API |Release time |Change log |Associated feature |
|---|---|---|---|
|新增[DescribeInstanceDasSnapShotCollectionStatus](https://docs.byteplus.com/en/docs/DBW/DescribeInstanceDasSnapShotCollectionStatus?lang=en) |2026\-10\-10 |Call the DescribeInstanceDasSnapShotCollectionStatus API to query the session snapshot collection status and backoff policy status of the specified database instance. |* [MySQL session management](https://docs.byteplus.com/en/docs/DBW/session-management-for-mysql?lang=en)<br><br>* [NDB MySQL session management](https://docs.byteplus.com/en/docs/DBW/Session_management?lang=en)<br><br>* [PostgreSQL session management](https://docs.byteplus.com/en/docs/DBW/session-management?lang=en)<br><br>* [MongoDB session management](https://docs.byteplus.com/en/docs/DBW/MongDB_Session_management?lang=en) |
|新增[ModifyInstanceDasSnapshotCollectionSwitch](https://docs.byteplus.com/en/docs/DBW/ModifyInstanceDasSnapshotCollectionSwitch?lang=en) |2026\-10\-10 |Call the ModifyInstanceDasSnapshotCollectionSwitch API to modify the session snapshot collection feature. ||
|新增[DescribeSqlKeywords](https://docs.byteplus.com/en/docs/DBW/DescribeSqlKeywords?lang=en) |2026\-10\-10 |Call the DescribeSqlKeywords API to generate SQL throttling keywords based on the original SQL statement. |* [MySQL rate limiting management](https://docs.byteplus.com/en/docs/DBW/preview-sql-throttle-task-management-for-mysql?lang=en)<br><br>* [NDB MySQL rate limiting management](https://docs.byteplus.com/en/docs/DBW/SQL_throttling_management?lang=en) |
|新增[CreateSqlConcurrencyControlRule](https://docs.byteplus.com/en/docs/DBW/CreateSqlConcurrencyControlRule?lang=en) |2026\-10\-10 |Call the CreateSqlConcurrencyControlRule API to create a SQL throttling task. ||
|新增[DescribeSqlConcurrencyControlRules](https://docs.byteplus.com/en/docs/DBW/DescribeSqlConcurrencyControlRules?lang=en) |2026\-10\-10 |Call the DescribeSqlConcurrencyControlRules API to query all SQL throttling tasks of the database instance. ||
|新增[StopSqlConcurrencyControlRule](https://docs.byteplus.com/en/docs/DBW/StopSqlConcurrencyControlRule?lang=en) |2026\-10\-10 |Call the StopSqlConcurrencyControlRule API to stop the SQL throttling task. ||
|新增[RestartSqlConcurrencyControlRule](https://docs.byteplus.com/en/docs/DBW/RestartSqlConcurrencyControlRule?lang=en) |2026\-10\-10 |Call the RestartSqlConcurrencyControlRule API to enable a suspended SQL throttling task. ||
|新增[DeleteSqlConcurrencyControlRule](https://docs.byteplus.com/en/docs/DBW/DeleteSqlConcurrencyControlRule?lang=en) |2026\-10\-10 |Call the DeleteSqlConcurrencyControlRule API to delete a SQL throttling task. ||

## September 2026

|API |Release time |Change log |Associated feature |
|---|---|---|---|
|新增[AutoScale](https://docs.byteplus.com/en/docs/DBW/AutoScale?lang=en) |2026\-09\-04 |Call the AutoScale API to configure scaling rules. |[Storage space expansion management](https://docs.byteplus.com/en/docs/DBW/Storage_expansion_management_pg?lang=en) |
|新增[DescribeAutoScaleEvents](https://docs.byteplus.com/en/docs/DBW/DescribeAutoScaleEvents?lang=en) |2026\-09\-04 |Call the DescribeAutoScaleEvents API to query scaling events for the specified instance. ||
|新增[DescribeAutoScaleRules](https://docs.byteplus.com/en/docs/DBW/DescribeAutoScaleRules?lang=en) |2026\-09\-04 |Call the DescribeAutoScaleRules API to query Automatic Or Scheduled scaling configurations for an instance. ||
|新增[PreCheckCreateFullSql](https://docs.byteplus.com/en/docs/DBW/PreCheckCreateFullSql?lang=en) |2026\-09\-01 |Call the PreCheckCreateFullSql operation to enable Full SQL insight. |* MySQL [Database audit](https://docs.byteplus.com/en/docs/DBW/database-audit-management-for-mysql?lang=en) and [SQL insights and auditing](https://docs.byteplus.com/en/docs/DBW/full-SQL-explorer?lang=en)<br><br>* <br><br>* NDB MySQL [Database audit](https://docs.byteplus.com/en/docs/DBW/Database_audit_management?lang=en) and [SQL insights and auditing](https://docs.byteplus.com/en/docs/DBW/Full_SQL_insight_management?lang=en) |
|新增[CreateTerminateFullSqlOrder](https://docs.byteplus.com/en/docs/DBW/CreateTerminateFullSqlOrder?lang=en) |2026\-09\-01 |Call the CreateTerminateFullSqlOrder API to create a termination order for the specified full SQL instance. ||
|新增[CreateFullSqlOrder](https://docs.byteplus.com/en/docs/DBW/CreateFullSqlOrder?lang=en) |2026\-09\-01 |Call the CreateFullSqlOrder API to create a full SQL subscription order for the specified instance. ||
|新增[DescribeFullSqlStatus](https://docs.byteplus.com/en/docs/DBW/DescribeFullSqlStatus?lang=en) |2026\-09\-01 |Call the DescribeFullSqlStatus API to query the full SQL enablement status, feature status, and subscription configuration of the specified instance. ||
|新增[DescribeFullSQLFingerprintExample](https://docs.byteplus.com/en/docs/DBW/DescribeFullSQLFingerprintExample?lang=en) |2026\-09\-01 |Call the DescribeFullSQLFingerprintExample operation to query full SQL detail samples based on SQL fingerprints. ||
|新增[DescribeSqlTemplatesContrast](https://docs.byteplus.com/en/docs/DBW/DescribeSqlTemplatesContrast?lang=en) |2026\-09\-01 |Call the DescribeSqlTemplatesContrast API to query the aggregated indicator comparison of full SQL templates in two time periods. ||
|新增[DescribeSQLExecItemMetric](https://docs.byteplus.com/en/docs/DBW/DescribeSQLExecItemMetric?lang=en) |2026\-09\-01 |Call the DescribeSQLExecItemMetric API to query the metric curve of a single execution indicator for a specific SQL fingerprint within a specified time range. ||

## August 2026

|API |Release time |Change log |Associated feature |
|---|---|---|---|
|新增[DescribeDialogDetailSnapshot](https://docs.byteplus.com/en/docs/DBW/DescribeDialogDetailSnapshot?lang=en) |2026\-07\-29 |Call the DescribeDialogDetailSnapshot API to query the details of session information in a session snapshot. |* [MySQL session management](https://docs.byteplus.com/en/docs/DBW/session-management-for-mysql?lang=en)<br><br>* [NDB MySQL session management](https://docs.byteplus.com/en/docs/DBW/Session_management?lang=en)<br><br>* [PostgreSQL session management](https://docs.byteplus.com/en/docs/DBW/session-management?lang=en)<br><br>* [MongoDB session management](https://docs.byteplus.com/en/docs/DBW/MongDB_Session_management?lang=en) |
|新增[DescribeDialogSnapshots](https://docs.byteplus.com/en/docs/DBW/DescribeDialogSnapshots?lang=en) |2026\-07\-29 |Call the DescribeDialogSnapshots API to query the list of session snapshot time points. ||
|新增[DescribeEngineStatusSnapShot](https://docs.byteplus.com/en/docs/DBW/DescribeEngineStatusSnapShot?lang=en) |2026\-07\-29 |Call the DescribeEngineStatusSnapShot API to query session snapshot engine status details. ||

## July 2026

|API |Release time |Change log |Associated feature |
|---|---|---|---|
|新增[GetFullSqlInstanceCorrespondence](https://docs.byteplus.com/en/docs/DBW/GetFullSqlInstanceCorrespondence?lang=en&type=preview) |2026\-07\-01 |New API. Call the GetFullSqlInstanceCorrespondence API to query the instance mapping relationship for FullSQL. |[Viewing billing information](https://docs.byteplus.com/en/docs/DBW/Viewing_fee_information?lang=en) |
|更新[DescribeAuditLogDetail](https://docs.byteplus.com/en/docs/DBW/describeauditlogdetail?lang=en) |2026\-07\-01 |Updated the API notes. Distinguish the version of the database Log when calling Database audit. |* [MySQL database audit management](https://docs.byteplus.com/en/docs/DBW/database-audit-management-for-mysql?lang=en)<br><br>* [NDB MySQL Database audit management](https://docs.byteplus.com/en/docs/DBW/Database_audit_management?lang=en)<br><br>* [PostgreSQL database audit management](https://docs.byteplus.com/en/docs/DBW/database-audit-management-for-PG?lang=en)<br><br>* [Redis database audit management](https://docs.byteplus.com/en/docs/DBW/database-audit-management?lang=en)<br><br>* [MongoDB database audit management](https://docs.byteplus.com/en/docs/DBW/database-audit-management____?lang=en&type=preview) |

## June 2026

|API |Release time |Change log |Associated feature |
|---|---|---|---|
|更新[DescribeAggregateSlowLogs](https://docs.byteplus.com/en/docs/DBW/describeaggregateslowlogs?lang=en) |2026\-06\-05 |Updated the API notes.<br><br><br>* API is deprecated.<br><br>* Updated the data structure `AggregateSlowLogs` in the API. |* [Slow log diagnosis management](https://docs.byteplus.com/en/docs/DBW/Slow_log_diagnosis_management)<br><br>* [NDB for MySQL slow log management](https://docs.byteplus.com/en/docs/DBW/Slow_log_diagnosis?lang=en)<br><br>* [PostgreSQL slow log management](https://docs.byteplus.com/en/docs/DBW/slow-log-analysis-management-for-PG?lang=en)<br><br>* [MongoDB slow log management](https://docs.byteplus.com/en/docs/DBW/slow-query-log-management?lang=en) |
|新增[UpdateInstanceManagementConfig](https://docs.byteplus.com/en/docs/DBW/UpdateInstanceManagementConfig?lang=en) |2026\-06\-04 |Updated the API notes. The `SecurityRuleId` and `ApprovalConfigId` parameters are changed from required to optional when calling the API. |* [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql) [(RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql)<br><br>* [Enabling security control (veDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control)<br><br>* [Enabling security control (NDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control)<br><br>* [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-control) [(RDS for](https://docs.byteplus.com/en/docs/DBW/enabling-security-control) [PostgreSQL](https://docs.byteplus.com/en/docs/DBW/enabling-security-control)[)](https://docs.byteplus.com/en/docs/DBW/enabling-security-control)<br><br>* [Enabling security control ](https://docs.byteplus.com/en/docs/DBW/MongoDB_Enabling_security_control)[(](https://docs.byteplus.com/en/docs/DBW/MongoDB_Enabling_security_control)[Document Database for MongoDB](https://docs.byteplus.com/en/docs/DBW/MongoDB_Enabling_security_control)[)](https://docs.byteplus.com/en/docs/DBW/MongoDB_Enabling_security_control) |

## March 2026

|API |Release time |Change log |Associated feature |
|---|---|---|---|
|新增[DescribePreCheckDetail](https://docs.byteplus.com/en/docs/DBW/describePreCheckDetail?lang=en) |2026\-03\-05 |New API. Call the DescribePreCheckDetail API to query the pre\-check results of the ticket. |* [Managing data change tickets (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/ticket-management-for-mysql)<br><br>* [Managing data change tickets (NDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/Managing_data_change_tickets)<br><br>* [Managing data change tickets (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/Managing_data_change_ticket)<br><br><br><br><br> |

## January 2026

|API |Release time |Change log |Associated feature |
|---|---|---|---|
|新增[CreateSqlKillRule](https://docs.byteplus.com/en/docs/DBW/createSqlKillRule?lang=en) |2026\-01\-14 |New API. Call the CreateSqlKillRule API to create persistent Kill tasks. |* [Persistent Kill MySQL tasks](https://docs.byteplus.com/en/docs/DBW/session-information-management-for-mysql?lang=en#.a2lsbC3kvJror50=)<br><br>* [Persistent Kill NDB MySQL tasks](https://docs.byteplus.com/en/docs/DBW/Session_information_management?lang=en#.a2lsbC3kvJror50=) |
|新增[StopSqlKillRule](https://docs.byteplus.com/en/docs/DBW/stopsqlkillrule?lang=en) |2026\-01\-14 |New API. Call the StopSqlKillRule API to stop persistent Kill tasks. ||
|新增[DeleteSqlKillRule](https://docs.byteplus.com/en/docs/DBW/deletesqlkillrule?lang=en) |2026\-01\-14 |New API. Call the DeleteSqlKillRule API to delete persistent Kill tasks. ||
|新增[DescribeSqlKillRules](https://docs.byteplus.com/en/docs/DBW/describesqlkillrules?lang=en) |2026\-01\-14 |New API. Call the DescribeSqlKillRules API to query persistent Kill tasks. ||

## December 2025

|API |Release time |Change log |Associated feature |
|---|---|---|---|
|新增[AgreeUserProtocol](https://docs.byteplus.com/en/docs/DBW/AgreeUserProtocol?lang=en) |2025\-12\-30 |New API for agreeing to the Database Workshop DBW user agreement. |\- |

## November 2025

|**API** |**Release time** |**Change log** |**Associated feature** |
|---|---|---|---|
|新增[ExecuteSQL](https://docs.byteplus.com/en/docs/DBW/ExecuteSQL) |2025\-11\-28 |New API for executing SQL statements. |\- |
|新增[ListDatabases](https://docs.byteplus.com/en/docs/DBW/ListDatabases) |2025\-11\-28 |New API for querying the database list of a database instance. |\- |
|新增[ListTables](https://docs.byteplus.com/en/docs/DBW/ListTables) |2025\-11\-28 |New API for querying the list of tables in the database of a database instance. |\- |
|新增[GetTableInfo](https://docs.byteplus.com/en/docs/DBW/GetTableInfo) |2025\-11\-28 |New API for querying table metadata of database instances. |\- |

## October 2025

|**API** |**Release time** |**Change log** |**Associated feature** |
|---|---|---|---|
|更新[GenerateSQLFromNL](https://docs.byteplus.com/en/docs/DBW/GenerateSQLFromNL) |2025\-10\-15 |Modify the API to generate SQL statements from natural language. |* [Natural language to SQL (RDS for MySQL & NDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/natural-language-to-sql-conversion-for-mysql) |

## September 2025

|**API** |**Release time** |**Change log** |**Associated feature** |
|---|---|---|---|
|新增[DescribeSecurityGroups](https://docs.byteplus.com/en/docs/DBW/DescribeSecurityGroups) |2025\-09\-26 |Added an API for querying the Security rule set. |* [Security rule set management (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/security-rule-set-management-for-mysql)<br><br>* [Security rule set management (NDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/Security_rule_set_management)<br><br>* [Security rule set management (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/Security_rule_set_management)<br><br>* [Security rule set management (Document Databse for MongoDB)](https://docs.byteplus.com/en/docs/DBW/security-rule-set-management_____)<br><br>* [Security rule set management (SQL Server)](https://docs.byteplus.com/en/docs/DBW/security-rule-set-management__) |
|新增[ListApprovalFlowConfig](https://docs.byteplus.com/en/docs/DBW/ListApprovalFlowConfig) |2025\-09\-26 |New API for querying the approval workflow list. |[Approval workflow management](https://docs.byteplus.com/en/docs/DBW/Approval_workflow_management) |
|新增[ListApprovalNode](https://docs.byteplus.com/en/docs/DBW/ListApprovalNode) |2025\-09\-26 |New API for querying approval nodes. |[Approval node management](https://docs.byteplus.com/en/docs/DBW/Approval_node_management) |
|新增[DescribeManagedUsers](https://docs.byteplus.com/en/docs/DBW/DescribeManagedUsers) |2025\-09\-26 |New API for querying user information. |[Personal user management](https://docs.byteplus.com/en/docs/DBW/Personal_user_management) |
|新增[EnableInstanceManagement](https://docs.byteplus.com/en/docs/DBW/EnableInstanceManagement) |2025\-09\-26 |New API for enabling security control. |* [ (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql)[ (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql)<br><br>* [for MySQL)](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control)[for MySQL)](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control)[for MySQL)](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control)[for MySQL)](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control)<br><br>* [SQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-control)[SQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-control)[SQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-control)[SQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-control)<br><br>* [)](https://docs.byteplus.com/en/docs/DBW/MongoDB_Enabling_security_control)[)](https://docs.byteplus.com/en/docs/DBW/MongoDB_Enabling_security_control)[)](https://docs.byteplus.com/en/docs/DBW/MongoDB_Enabling_security_control)[)](https://docs.byteplus.com/en/docs/DBW/MongoDB_Enabling_security_control) |
|新增[UpdateInstanceManagementConfig](https://docs.byteplus.com/en/docs/DBW/UpdateInstanceManagementConfig) |2025\-09\-26 |New API for modifying security control information. ||
|新增[DisableInstanceManagement](https://docs.byteplus.com/en/docs/DBW/DisableInstanceManagement) |2025\-09\-26 |New API for disabling security control. ||
|新增[CreateDmlSqlChangeTicket](https://docs.byteplus.com/en/docs/DBW/CreateDmlSqlChangeTicket) |2025\-09\-19 |New API for creating DML data change tickets. |* [Creating a regular SQL change ticket (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/creating-a-normal-sql-change-ticket-for-mysql)<br><br>* [Creating a regular SQL change ticket (NDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/Creating_a_regular_SQL_change_ticket)<br><br>* [Creating a regular SQL change ticket (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/Create_a_regular_SQL_change_ticket) |
|新增[CreateDdlSqlChangeTicket](https://docs.byteplus.com/en/docs/DBW/CreateDdlSqlChangeTicket) |2025\-09\-19 |New API for creating DDL schema change tickets. |* [Creating a lock-free schema change ticket (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/creating-a-lock-free-structural-change-ticket-onlineddl-ticket-for-mysql)<br><br>* [Creating a lock-free schema change ticket (NDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/creating-a-lock-free-schema-change-ticket-OnlineDDL) |
|新增[DescribeTickets](https://docs.byteplus.com/en/docs/DBW/DescribeTickets) |2025\-09\-19 |New API for batch querying tickets. |* [Managing data change tickets (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/ticket-management-for-mysql)<br><br>* [Managing data change tickets (NDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/Managing_data_change_tickets)<br><br>* [Managing data change tickets (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/Managing_data_change_ticket)<br><br><br><br><br> |
|新增[DescribeTicketDetail](https://docs.byteplus.com/en/docs/DBW/DescribeTicketDetail) |2025\-09\-19 |New APIs for querying single Ticket details. ||
|新增[DescribeWorkflow](https://docs.byteplus.com/en/docs/DBW/DescribeWorkflow) |2025\-09\-19 |New API for querying the approval ticket details. ||
|新增[WorkflowAction](https://docs.byteplus.com/en/docs/DBW/WorkflowAction) |2025\-09\-19 |New APIs for approval ticket ||
|新增[ManualExecuteTicket](https://docs.byteplus.com/en/docs/DBW/ManualExecuteTicket) |2025\-09\-19 |New API for manually executing tickets. ||

## August 2025

|**API** |**Release time** |**Change log** |**Associated feature** |
|---|---|---|---|
|新增[GenerateSQLFromNL](https://docs.byteplus.com/en/docs/DBW/GenerateSQLFromNL) |2025\-08\-12 |New API for generating SQL statements from natural language. |[Natural language to SQL](https://docs.byteplus.com/en/docs/DBW/natural-language-to-sql-conversion-for-mysql) |

## June 2025

|**API** |**Release time** |**Change log** |**Associated feature** |
|---|---|---|---|
|更新[DescribeSlowLogs](https://docs.byteplus.com/en/docs/DBW/describeslowlogs) |2025\-06\-14 |Modify the API. |[Slow log details management](https://docs.byteplus.com/en/docs/DBW/slow-log-management-for-mysql) |
|新增[ListSlowQueryAdviceApi](https://docs.byteplus.com/en/docs/DBW/ListSlowQueryAdviceApi) |2025\-06\-29 |New API for getting the slow log diagnosis details. |[Slow log diagnosis management](https://docs.byteplus.com/en/docs/DBW/Slow_log_diagnosis_management) |
|新增[SlowQueryAdviceTaskHistoryApi](https://docs.byteplus.com/en/docs/DBW/SlowQueryAdviceTaskHistoryApi) |2025\-06\-29 |New API for getting slow log diagnosis history. ||

## May 2024

|**API** |**Release time** |**Change log** |**Associated feature** |
|---|---|---|---|
|新增[DataExecCommandSetAsync](https://docs.byteplus.com/en/docs/DBW/dataexeccommandsetasync) |2024\-05\-16 |New API. Execute command sets asynchronously through the DataExecCommandSetAsync interface. |\- |
|新增[DataGetCommandSetResult](https://docs.byteplus.com/en/docs/DBW/datagetcommandsetresult) |2024\-05\-16 |New API. Call the DataGetCommandSetResult API to query the execution results of the asynchronous execution command set. |\- |
