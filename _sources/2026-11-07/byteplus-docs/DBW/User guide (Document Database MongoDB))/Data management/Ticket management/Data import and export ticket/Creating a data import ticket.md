---
title: "Creating a data import ticket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/creating-a-data-import-ticket_for_mongodb"
---

This topic explains how to create a data import ticket for a Document Database for MongoDB instance on the Database Workshop (DBW) console.

## Background

To ensure controllability and consistency during data import, MongoDB uses the mongoimport tool, with the import mode set to INSERT. Additionally, mongoimport reads and parses the input JSON file contents using a single thread on the client side and sends the data to the MongoDB server in batches. The server can process write requests concurrently, ensuring that data is parsed sequentially while improving overall throughput efficiency.

## Prerequisite

* A Document Database for MongoDB instance and account have been created, and the account has the `readWrite` permission and `dbAdmin` permission of the business database, and the instance is in the running status. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/mongodb/create-instance) and [Creating an account](https://docs.byteplus.com/en/docs/mongodb/create-account).

* The instance has enabled security control. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/MongoDB_Enabling_security_control).

* A user has been added as an administrator of DBW. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/Personal_user_management#.5re75Yqg55So5oi3). Alternatively, to apply for DBW administrator privileges, refer to [Role permission application](https://docs.byteplus.com/en/docs/DBW/role-permission-request).

* The BytePlus IAM user added as a DBW role has been granted relevant permissions. For detailed steps, refer to [Permission management](https://docs.byteplus.com/en/docs/DBW/Granting_operation_permissions_for_system_roles?lang=en).

## Precautions

* Only one import task can be created at a time. Concurrent imports are not supported.

* System databases do not support data imports.

* Importing data to Document Database for MongoDB cloud disk instances is currently unsupported.

* Before importing data, verify that the source and target table structures match, including column names, data types, lengths, and order. If structures differ, manually adjust or convert the data to avoid data loss, truncation, or task failure.

* Currently, only JSON files are supported for upload, with a maximum size of 1 GiB. Excel files are not supported.

* An import task may fail under the following conditions:

   * Insufficient database account permissions.

   * The target database or table is deleted or renamed during import.

   * Target instance restart or configuration change during import.

   * The character set of the import file is not UTF\-8.

## Procedure

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, click **Data import/export**.

5. On the **Data import/export** tab, click **Create data import/export ticket**.

6. On the **Fill in the ticket** configuration wizard of the **Create data import/export ticket** control panel, configure the following parameters.

|**Parameter** ||**Description** |
|---|---|---|
|**Basic information**<br><br> |**Creator** |Defaults to the currently logged\-in account and can not be modified. |
||**Database type** |This document describes how to create a data import ticket for Document Database for MongoDB. Therefore, **Database type** should be set to **Document Database for MongoDB**. |
||**Ticket type** |Select **Data import**. |
||**Execution method** |Defaults to **Automantic execution after approval**, meaning data import tickets will run automatically once approved. This parameter can not be modified. |
|**Data import/export configuration**<br><br> |**Instance** |From the drop\-down list, select the target instance for data import. |
||**Database** |From the drop\-down list, select the target database for data import. |
||**File type** |Currently, only the JSON file is supported for import. |
||**Target collection** |From the drop\-down list, select the target collection for data import. |
||**Upload file** |Click **Upload file** to upload a JSON file with a maximum size of 1GiB. |
||**Write method** |Currently, only **INSERT_INTO** format is supported for writing. |
||**Character set** |Currently, only the **utf8** character set is supported. |
||**Exception error** |Optional. Check whether to ignore errors in case of exceptions. Unchecked by default.<br><br><br>* Checked: Skip the current erroneous statement and continue execution in case of exceptions.<br><br>* Unchecked: Terminate the import task immediately upon any error. |
||**Business background** |Fill in the business reason and usage scenario for the ticket as needed, so that the approver can quickly understand the purpose of the ticket, reduce communication costs, and use it for subsequent audits. |

7. Click **Next step: Pre\-check**.

8. On the **Ticket pre\-check** configuration wizard of the **Create data import/export ticket** control panel, you can view the **Permission check** pre\-check item.

> **tip**

> If pre\-check fails, you can click **View details** in the **Result details** column of the check item to review the specific reasons for the failure. After making corrections, recreate the ticket.

9. Click **OK**.
