---
title: "Data verification overview"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/introduction_to_data_validation"
---

Database Transmission Service (DTS) provides the data verification feature, which can verify and check the source and target difference data without downtime to help you identify inconsistent data or schema and other issues in time. This topic introduces the advantages, costs, and how to manage data verification.

## Background

The data verification feature can improve the data quality and reliability of the database and reduce data errors and abnormalities. At the same time, data verification is also an important means to protect database security and data integrity.

## Advantages

* Data verification supports verification without downtime.

* The data verification algorithm uses table\-based chunks for comparison and has high performance.

* Data verification tasks support field verification of row\-level data of full data at the source and target.

* If there is any data inconsistency during the execution of the task, DTS will check the abnormal data again after a certain period of time to ensure that the exception is not caused by an incremental delay.

## Billing

For billing information about the data verification task, refer to [Billing method for data verification task](https://docs.byteplus.com/en/docs/DTS/Data_verification_billing_method).

## Precautions

* Since full validation and schema verification are real\-time verifications of data, the verification needs to start when the expected data is consistent. Therefore, full validation or schema verification can be enabled only after the full migration/synchronization (if any) task is completed, and the delay time is 0 for incremental migration/synchronization.

* Increment validation is to verify the new data on the source and target ends. Therefore, increment validation can be started only when the delay time of incremental migration/synchronization is 0.

* Since full validation is a real\-time verification of the data, if the data changes frequently during verification, temporarily inconsistent data may be verified, resulting in an inaccurate data verification task result.

* Before performing the verification task, you need to evaluate the source database and target database performance. It is recommended that you perform data verification during off\-peak hours (for example, the CPU load of the source database and target database is below 30%). Because DTS will occupy certain read resources of the source database and target database during data verification, which may cause the database load to increase. In the case of poor database performance, low specifications, or large business volume, it may increase the pressure on the database, or even cause the database service to be unavailable.

* For MySQL\-to\-MYSQL single\-table data verification, DTS supports identifying up to 100,000 rows of differing data. If the number of differing rows exceeds 100,000, DTS will not perform data validation. The console page does not display the diff data; to view it, you can download the data locally. For detailed operations, refer to [Download data verification results](https://docs.byteplus.com/en/docs/DTS/viewing_data_validation?lang=en#.5LiL6L295pWw5o2u5qCh6aqM57uT5p6c). This feature is available on an allowlist basis. To use it, [Submit tickets](https://console.byteplus.com/workorder/create).

* The single table data verification feature from MySQL to MySQL displays up to 2,000 rows of difference data by default; the overall verification limit per table is 100,000 rows. Beyond this threshold, verification will be skipped automatically (no Diff results generated). The console page shows only partial diff data. To view the complete verification result, download the local file. For detailed steps, refer to [Download verification result](https://docs.byteplus.com/en/docs/DTS/viewing_data_validation?lang=en#.5LiL6L295pWw5o2u5qCh6aqM57uT5p6c). This feature is available on an allowlist basis. To use it, [Submit tickets](https://console.byteplus.com/workorder/create).

* In MongoDB data validation, the source database serves as the reference. The validation only checks whether the selected synchronized or migrated data from the source exists and is consistent in the target database; it cannot detect extra data present in the target database that is not in the source.

## Supported verification method

The data verification task supports three methods for checking data discrepancies between the source and target ends: full data verification, full row verification, and schema verification. The specific differences between the three verification methods are shown in the following table:

|**Verification method** |**Full verification** |||**Schema verification** |**Increment verification** |
|---|---|---|---|---|---|
||**Content verification** |**Row verification** |**Primary key verification** |||
|**Description** |This verification method can compare all or part of the data content between two databases or data entities. The full data verification process can ensure data consistency, and the accuracy and integrity of the data is guaranteed. |The validation method can simply compare whether the total number of rows in the source database and the target database is the same. The verification method is fast and effective, and can quickly detect problems such as data loss or duplicate addition. |This verification method can verify whether the primary keys are consistent between the source and target. |This verification method can check the consistency of the data schema, such as whether the columns, data type, primary key, and index of the table are the same. This verification method ensures schema consistency between the source and target databases. |This verification method can verify whether all increment data at the source and target are consistent after the incremental task is enabled. |
|**Limits** |* If the table to be validated has no primary key and no unique index, DTS will not perform data validation.<br><br>* MySQL supports verifying up to 100,000 rows of different data per single table; beyond 100,000 rows, DTS will not perform data verification.<br><br>* For other types of databases, data validation for a single table supports identifying at most 100 rows of differing data; if the number of differing rows exceeds 100, DTS will not perform data validation.<br><br>* The single table default verification limit for RDS for PostgreSQL data verification tasks is 100 rows. To verify data exceeding 100 rows, [Submit tickets](https://console.byteplus.com/workorder/create).<br><br>* Data validation is not supported if ETL rules are configured in the data synchronization task.<br><br>* Do not perform DDL operations on the source during the validation process, as this may result in inconsistent validation task results. |* If the table to be validated has no primary key and no unique index, DTS will not perform data validation.<br><br>* Data validation is not supported if ETL rules are configured in the data synchronization task.<br><br>* Do not perform DDL operations on the source during the validation process, as this may result in inconsistent validation task results. |* A maximum of 100 rows of different data can be verified in a single table. If this limit is exceeded, Database Transmission Service (DTS) will not perform data verification.<br><br>* Do not perform DDL operations on the source during the validation process, as this may result in inconsistent validation task results. |* Data validation is not supported if ETL rules are configured in the data synchronization task.<br><br>* Do not perform DDL operations on the source during the validation process, as this may result in inconsistent validation task results. |* A maximum of 10,000 different data entries can be verified.<br><br>* Data validation is not supported if ETL rules are configured in the data synchronization task.<br><br>* GTID is enabled for both the source and target database instances.<br><br>* Verification of tables without a primary key is not supported. |
|**Timing to start the verification task** |Start the data verification task (full validation, schema verification, or incremental validation) when the full migration/synchronization (if any) task is completed, and the delay time of incremental migration/synchronization is 0. |||||
|**Supported database types** |* MySQL<br><br>* veDB MySQL<br><br>* PostgreSQL<br><br>* MongoDB<br><br>* RDS for SQL Server<br><br>* Redis |* MySQL<br><br>* veDB MySQL<br><br>* MongoDB<br><br>* RDS for SQL Server<br><br>* PostgreSQL |* MongoDB |* MySQL<br><br>* veDB MySQL |* MySQL<br><br>* veDB MySQL<br><br>* MongoDB |

## Operation document

* [Configure data verification](https://docs.byteplus.com/en/docs/DTS/configuring_data_validation)

* [View data verification](https://docs.byteplus.com/en/docs/DTS/viewing_data_validation)
