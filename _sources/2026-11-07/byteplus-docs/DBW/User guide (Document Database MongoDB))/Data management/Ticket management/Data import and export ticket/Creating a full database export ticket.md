---
title: "Creating a full database export ticket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/creating-a-full-database-export-ticket-for-mongodb"
---

This topic describes how to create a full database export ticket for Document Database for MongoDB on the Database Workshop (DBW) console.

## Prerequisite

* A Document Database for MongoDB instance and account have been created, and the account has the `readWrite` permission and `dbAdmin` permission of the business database, and the instance is in the running status. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/mongodb/create-instance) and [Creating an account](https://docs.byteplus.com/en/docs/mongodb/create-account).

* The instance has enabled security control. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/MongoDB_Enabling_security_control).

* A user has been added as an administrator of DBW. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/Personal_user_management#.5re75Yqg55So5oi3). Alternatively, to apply for DBW administrator privileges, refer to [Role permission application](https://docs.byteplus.com/en/docs/DBW/role-permission-request).

* The BytePlus IAM user added as a DBW role has been granted relevant permissions. For detailed steps, refer to [Permission management](https://docs.byteplus.com/en/docs/DBW/Granting_operation_permissions_for_system_roles?lang=en).

## Precautions

* Exporting data from Document Database for MongoDB cloud disk instances is currently not supported.

* To minimize impact on primary database performance, DBW performs MongoDB data exports on secondary nodes by default.

* DBW uses the mongoexport tool for MongoDB data exports, currently supporting only JSON format files.

* DBW imposes a row limit of 100,000 rows for MongoDB data exports. When data volume exceeds 100,000 rows, the system automatically truncates at the 100,000th row.

* MongoDB exports only support UTF\-8 character set.

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
||**Database type** |This topic describes how to create a full database export ticket for the Document Database for MongoDB. Therefore, select **Database type** as **Document Database for MongoDB**. |
||**Ticket type** |Select **Full database export**. |
||**Execution method** |Defaults to **Automantic execution after approval**, meaning full database export tickets will run automatically once approved. This parameter can not be modified. |
|**Data import/export configuration**<br><br> |**Instance** |From the drop\-down list, select the target instance for full database export. |
||**Database** |From the drop\-down list, select the target database for full database export. |
||**File type** |Currently, only JSON format file content is supported for export. |
||**Target collection** |From the drop\-down list, select the target collection for full database export. |
||**Character set** |Currently, only the **utf8** character set is supported. |
||**Query condition** |Set filter conditions for exporting documents from the collection as needed. The format is`{"key":"value"}`。 |
||**Business background** |Fill in the business reason and usage scenario for creating the ticket as needed, so that the approver can quickly understand the purpose of the ticket, reduce communication costs, and use it for subsequent audits. |

7. Click **Next step: Pre\-check**.

8. On the **Ticket pre\-check** configuration wizard of the **Create data import/export ticket** control panel, you can view the **Permission check** pre\-check item.

   > **tip**

   > If pre\-check fails, you can click **View details** in the **Result details** column of the check item to review the specific reasons for the failure. After making corrections, recreate the ticket.

9. Click **OK**.
