---
title: "Creating an operation permission ticket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket__"
---

This topic describes how to create an operation permission ticket for applying for a Document Database for MongoDB instance on the Database Workshop (DBW) console.

## Prerequisite

Your account is already assigned a DBW role. For detailed steps, refer to the guide for accounts that [have been added as](https://docs.byteplus.com/en/docs/DBW/Personal_user_management) or [applied to become a DBW role](https://docs.byteplus.com/en/docs/DBW/role-permission-request).

## Precautions

* Only normal users in DBW can apply for instance operation permissions.

* All administrators in DBW can approve DBW role application tickets.

* The maximum validity period for permissions is 1 year.

* Approvers for operation permission tickets are set in the approval workflow when security control is enabled.

* Currently, only creating instance authorization tickets for Document Database for MongoDB is supported.

## Procedure

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Permission application** tab, click **Create ticket**.

5. In the dialog box that appears, select the required information for authorization.

   |Parameter |Description |
   |---|---|
   |**Applicant** |Defaults to the currently logged\-in account and can not be modified. |
   |**Application type** |Default is **Authorize instance** and cannot be modified. |
   |**Database type** |From the drop\-down list, select **Document Database for MongoDB**. |
   |**Authorize instance** |Check the instance to be authorized from the drop\-down list. Multiple selections are supported. |
   |**Permission type** |Check the permission type as needed. Currently, the following options are supported.<br><br><br>* **SQLchange**: Refers to operations that add, modify, or delete data in the database.<br><br>* **SQL query**: Refers to the operation of retrieving the required data from the database.<br><br>* **Structural change**: Represents operations that can modify, add, or delete a database structure.<br><br>* **Operation and maintenance read\-only**: Refers to read\-only permissions for operation and maintenance management capabilities, such as viewing real\-time sessions and database audit logs.<br><br>* **Operation and maintenance read/write**: Refers to full permissions for operation and maintenance management capabilities, such as Kill sessions.<br><br><br>> **tip**<br><br><br>> **SQL change**, **SQL query**, and **Schema change** can be checked or unchecked together, but not individually.<br> |
   |**Effective time** |Select the validity period of the authorization from the drop\-down list, with options including **1 month** (default), **3 months**, **6 months**, and **1 year**. Additionally, custom days can be set as the validity period, with a default of 1 day and a range of [1, 365]. |
   |**Business background** |Fill in the business reason and use case for creating the ticket as needed, so approvers can quickly understand the ticket's purpose, reduce communication costs, and support future audits. |

6. Click **Submit application**.
