---
title: "Database management"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Database_Management"
---

## **Query Database List**

1. Log in to the LAS console.

2. Menu selection: **Catalog**.

3. Click the required data catalog name \> database name in sequence to enter the **Database List** page.

## Create Database

1. Log in to the LAS console.

2. Menu selection: **Catalog**.

3. Select the data catalog and click **Create Database.**  in the upper right corner.

4. In the **Create Database** popup, fill in the database name, storage location, and remarks, then click **Confirm** to complete database creation.

## Edit Database

> **说明**

> Users can only edit databases for which they have permission.

1. Log in to the LAS console.

2. Menu selection: **Catalog**.

3. Select the data catalog, then in the **Database List**, click the edit button to the right of the database name to be edited, and modify the storage location and remarks.

## Delete Database

1. Log in to the LAS console.

2. Menu selection: **Catalog**.

3. Select the data catalog, then in the **Database List**, click the delete button to the right of the database name to be deleted and confirm deletion.

> **说明**

* > When deleting a DB, tables/functions under the DB will be deleted first, followed by the DB itself.

* > When deleting a table/DB, metadata will be deleted first, then the file directory corresponding to the storage location. The actions of deleting metadata and deleting files do not guarantee transactional consistency; that is, metadata may be deleted successfully while the file directory still exists. In other words, the DB/table may not be found, but the corresponding file directory remains.

* > When deleting a database, files will also be deleted. However, currently file deletion does not have a recycle bin function; once deleted, it cannot be restored. To recover mistakenly deleted data, multi\-version control must be enabled in TOS. For detailed instructions, please refer to: [Version Control](https://www.volcengine.com/docs/6349/145534).

* > When deleting a DB, tables will be deleted first. If an error occurs while deleting a table, the tables already deleted will not be rolled back. Users can refresh the page to continue deleting tables that have not yet been deleted.
