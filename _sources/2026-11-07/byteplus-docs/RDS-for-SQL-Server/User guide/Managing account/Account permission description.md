---
title: "Account permission description"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/account-permissions-description"
---

This topic describes the account types and permissions for RDS for SQL Server instances.

<span id=".6LSm5Y-357G75Z6L"></span>
## **Account types**

RDS for SQL Server instances support three database account types: Normal account, Super account, and System Admin account.


|**Account types** |**Description** |
|---|---|
|**Normal account** |* They can be created and managed through the console, API, or SQL statements.<br><br>* An instance can support multiple normal accounts, and the specific number depends on the instance's kernel.<br><br>* You need to manually grant permissions for specific databases to normal accounts.<br><br>* Normal accounts cannot create or manage other accounts, nor can they disconnect other accounts. |
|**Super account** |* You must create a super account when creating an instance.<br><br>* Each instance can have only one super account, which manages all normal accounts and databases.<br><br>* More permissions are available to meet personalized and fine\-grained permission management needs, such as assigning query permissions for different tables to users.<br><br>* Has permissions for all databases in the instance.<br><br>* Can disconnect any account. |
|**System Admin account** |* You can create only one database account with SA permissions (System Admin permission) for each instance. After the account is created, you can enable or disable it through the console.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The Super account feature is available on an allowlist basis. To request access, <a href="https://console.byteplus.com/workorder/create">Submit a ticket</a> to contact the SQL Server technical team.   </div><br>   <br><br>* This account has all permissions for all databases. |


<span id=".6LSm5Y-35p2D6ZmQ5YiX6KGo"></span>
## **Account permission list**


|**Account types** |**Authorization type** |**Role** |Permission |
|---|---|---|---|
|**System Admin account** |Owner |sysadmin |All permissions. |
|**Super account** |Owner |* Server\-level role<br><br>   * public<br><br>   * processadmin<br><br>   * setupadmin<br><br>* Database level role<br><br>   * public<br><br>   * db_owner |* Server\-level permission<br><br>   * CONNECT SQL<br><br>   * CREATE ANY DATABASE<br><br>   * ALTER ANY LOGIN<br><br>   * ALTER ANY LINKED SERVER<br><br>   * ALTER ANY CONNECTION<br><br>   * ALTER TRACE<br><br>   * VIEW ANY DATABASE<br><br>   * VIEW SERVER STATE<br><br>   * ALTER SERVER STATE<br><br>   * CREATE SERVER ROLE<br><br>   * ALTER ANY SERVER ROLE<br><br>* Database\-level permissions<br><br>   * CREATE DATABASE<br><br>   * CONNECT<br><br>   * SHOWPLAN<br><br>   * KILL DATABASE CONNECTION<br><br>   * VIEW ANY COLUMN ENCRYPTION KEY DEFINITION<br><br>   * VIEW ANY COLUMN MASTER KEY DEFINITION<br><br>   * VIEW DATABASE STATE<br><br>   * VIEW DEFINITION<br><br>   * CONNECT<br><br>   * SHOWPLAN<br><br>   * ALTER ANY USER<br><br>   * SELECT<br><br>   * KILL DATABASE CONNECTION<br><br>   * VIEW ANY COLUMN ENCRYPTION KEY DEFINITION<br><br>   * VIEW ANY COLUMN MASTER KEY DEFINITION<br><br>   * VIEW DATABASE STATE<br><br>   * VIEW DEFINITION<br><br>   * CREATE TABLE<br><br>   * CREATE VIEW<br><br>   * CREATE PROCEDURE<br><br>   * CREATE FUNCTION<br><br>   * CREATE RULE<br><br>   * CREATE DEFAULT<br><br>   * BACKUP DATABASE<br><br>   * BACKUP LOG<br><br>   * CREATE TYPE<br><br>   * CREATE ASSEMBLY<br><br>   * CREATE XML SCHEMA COLLECTION<br><br>   * CREATE SCHEMA<br><br>   * CREATE SYNONYM<br><br>   * CREATE AGGREGATE<br><br>   * CREATE ROLE<br><br>   * CREATE MESSAGE TYPE<br><br>   * CREATE SERVICE<br><br>   * CREATE CONTRACT<br><br>   * CREATE REMOTE SERVICE BINDING<br><br>   * CREATE ROUTE<br><br>   * CREATE QUEUE<br><br>   * CREATE SYMMETRIC KEY<br><br>   * CREATE ASYMMETRIC KEY<br><br>   * CREATE EXTERNAL LANGUAGE<br><br>   * CREATE EXTERNAL LIBRARY<br><br>   * CREATE FULLTEXT CATALOG<br><br>   * CREATE CERTIFICATE<br><br>   * CONNECT<br><br>   * CONNECT REPLICATION<br><br>   * CHECKPOINT<br><br>   * SUBSCRIBE QUERY NOTIFICATIONS<br><br>   * SHOWPLAN<br><br>   * ALTER ANY USER<br><br>   * ALTER ANY ROLE<br><br>   * ALTER ANY APPLICATION ROLE<br><br>   * ALTER ANY COLUMN ENCRYPTION KEY<br><br>   * ALTER ANY COLUMN MASTER KEY<br><br>   * ALTER ANY SCHEMA<br><br>   * ALTER ANY ASSEMBLY<br><br>   * ALTER ANY DATABASE SCOPED CONFIGURATION<br><br>   * ALTER ANY DATASPACE<br><br>   * ALTER ANY EXTERNAL DATA SOURCE<br><br>   * ALTER ANY EXTERNAL FILE FORMAT<br><br>   * ALTER ANY EXTERNAL LIBRARY<br><br>   * ALTER ANY EXTERNAL LANGUAGE<br><br>   * ALTER ANY MESSAGE TYPE<br><br>   * ALTER ANY CONTRACT<br><br>   * ALTER ANY SERVICE<br><br>   * ALTER ANY REMOTE SERVICE BINDING<br><br>   * ALTER ANY ROUTE<br><br>   * ALTER ANY FULLTEXT CATALOG<br><br>   * ALTER ANY SYMMETRIC KEY<br><br>   * ALTER ANY ASYMMETRIC KEY<br><br>   * ALTER ANY CERTIFICATE<br><br>   * ALTER ANY SECURITY POLICY<br><br>   * SELECT<br><br>   * INSERT<br><br>   * UPDATE<br><br>   * DELETE<br><br>   * REFERENCES<br><br>   * EXECUTE<br><br>   * ALTER ANY DATABASE DDL TRIGGER<br><br>   * ALTER ANY DATABASE EVENT NOTIFICATION<br><br>   * ALTER ANY DATABASE AUDIT<br><br>   * ALTER ANY DATABASE EVENT SESSION<br><br>   * KILL DATABASE CONNECTION<br><br>   * VIEW ANY COLUMN ENCRYPTION KEY DEFINITION<br><br>   * VIEW ANY COLUMN MASTER KEY DEFINITION<br><br>   * VIEW DATABASE STATE<br><br>   * VIEW DEFINITION<br><br>   * TAKE OWNERSHIP<br><br>   * ALTER<br><br>   * ALTER ANY MASK<br><br>   * UNMASK<br><br>   * EXECUTE ANY EXTERNAL SCRIPT<br><br>   * ADMINISTER DATABASE BULK OPERATIONS<br><br>   * ALTER ANY SENSITIVITY CLASSIFICATION<br><br>   * VIEW ANY SENSITIVITY CLASSIFICATION<br><br>   * CONTROL |


&nbsp;
