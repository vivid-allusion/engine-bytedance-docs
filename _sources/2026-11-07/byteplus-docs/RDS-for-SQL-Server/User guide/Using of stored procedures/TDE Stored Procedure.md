---
title: "TDE Stored Procedure"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/TDE_Stored_Procedure"
---

This topic describes how to use stored procedures to query, enable, and disable the Transparent Data Encryption (TDE) feature for a specific database, as well as how to remove encryption certificates.

<span id="ynj8Cinw"></span>
## Prerequisite

The SQL Server instance is connected. For more information, see [Connecting an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connect-instance).

<span id="tGHZLyKm"></span>
## Background information

Execute the stored procedure  `master.dbo. rds_db_tde` to operate the Transparent Data Encryption (TDE) function of the Database. The specific Parameters are described as follows:


* `@db_name`: Specify the target Database name. To operate all Databases, use `null`.

* `@tde_action`: Specifies the TDE Operation type, the specific value is as follows:

   * `0`:Query Database Encryption Status.

   * `1`:Enable Database Encryption.

   * `2`:Disable Database Encryption.

   * `3`:Remove the Database Encryption Certificate.


<span id="Hh847Qwh"></span>
## Operation steps

<span id="0sXIEish"></span>
### Query Database TDE Encryption Status

```SQL
-- Query the specified DB encryption
exec master.dbo.rds_db_tde @db_name= 'db1', @tde_action= 0
-- Query all DB encryption
exec master.dbo.rds_db_tde @db_name= NULL , @tde_action= 0
```


<span id="JJDECog2"></span>
### Enable Database TDE Encryption

```SQL
-- Enable specified DB encryption
exec master.dbo.rds_db_tde @db_name= 'db1' , @tde_action= 1
-- Enable all DB encryption
exec master.dbo.rds_db_tde @db_name= NULL , @tde_action= 1
```


<span id="OKKYWx2j"></span>
### Disable Database TDE Encryption

```SQL
-- Disable specified DB encryption
exec master.dbo.rds_db_tde @db_name= 'db1' , @tde_action= 2
-- Disable all DB encryption
exec master.dbo.rds_db_tde @db_name= NULL , @tde_action= 2
```


<span id="mVE2jL8v"></span>
### Removing Database Encryption Certificates

```SQL
-- Remove the specified DB encryption certificate
exec master.dbo.rds_db_tde @db_name= 'db1' , @tde_action= 3
Remove all DB encryption certificates
exec master.dbo.rds_db_tde @db_name= NULL , @tde_action= 3
```
