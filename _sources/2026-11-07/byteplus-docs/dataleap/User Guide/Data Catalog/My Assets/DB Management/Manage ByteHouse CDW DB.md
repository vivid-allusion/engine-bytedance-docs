---
title: "Manage ByteHouse CDW DB"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Manage_ByteHouse_CDW_DB"
---

DB management provides unified creation, editing, and authorization ownership of metadata. This article introduces how to manage the ByteHouse CDW DB.

<span id="_1-约束限制"></span>
## Constraints

Users can only manage databases where they are DB owners.

<span id="_2-前提条件"></span>
## Prerequisites

The collector has been created, and ByteHouse CDW metadata has been ingested into the Data Catalog. Related instructions can be found in [Metadata Ingestion](https://docs.byteplus.com/docs/dataleap/Metadata_Ingestion).

<span id="_3-操作步骤"></span>
## Operation Steps


1. Log in to the DataLeap console.

2. Choose **Overview \> Catalog \> My Assets \> DB Management** to enter the DB Management page.

3. Click the **ByteHouse CDW** tab to enter the ByteHouse CDW page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/074ef519f70f433a8a4789996aa2b916~tplv-goo7wpa0wc-image.image) </span>

4. The following operations can be performed:

   * Click the **Create ByteHouse CDW DB** button. In the pop\-up create DB window, fill in the information, then click the **OK** button to create a new ByteHouse CDW DB.

      The related parameters for creating a ByteHouse CDW DB are explained in the following table.

      
      |Parameter |Description |
      |---|---|
      |\*Cluster |The cluster for creating the database; you can select from clusters with existing collectors in the dropdown. Refer to [Metadata Ingestion](https://docs.byteplus.com/docs/dataleap/Metadata_Ingestion) for operations related to creating collectors. |
      |\*Database name |The name of the database to be created; once set, it cannot be changed.<br><br>Only supports lowercase English letters, numbers, and underscores, starting with a lowercase letter, up to 50 characters in length. |
      |\*DB owners |Database administrators with a development focus, responsible for daily operation and maintenance of the DB.<br><br><br>* When creating a DB, it automatically fills in with the current user. Supports multiple entries and dropdown selection of created tenant accounts. Owners can be changed, but one cannot remove themselves.<br><br>* Can choose to synchronize to the database authority owner. |
      |\*Database authority owner |Security management role that manages all resources under the DB (authorize revocation, classification settings, approval flow configuration, etc.), decides whether data can be used openly, and directly participates in the overall DB permission approval.<br><br>When the **DB owners** uncheck **synchronize to the database authority owner**, this option becomes editable and supports multiple selections. |
      |Description |Explanation information describing the scope, usage, etc., of the database to facilitate subsequent management. |
      |\*DB usage |There are two options: production environment and test environment. |
      |\*Confidentiality Level |The database security level ranges from low to high as L1, L2, L3, L4, selectable from the dropdown. |
      

   * Enter a name or description keyword to search for matching databases in the list.

   * Click the **Edit** button in the **Action** column of a database entry in the list. In the pop\-up edit window, you can modify the basic information of the DB. Click the **Go to settings** button in the row of the **Permission Settings** parameter to go to the permission management module and set DB permissions and the approval process.

      Please refer to [Set Application Permissions](https://docs.byteplus.com/docs/dataleap/Set_Application_Permissions) for related instructions on permission management operations.

   * Click the **Delete** button in the **Action** column of a database entry in the list. In the pop\-up confirm deletion dialog, click the **Confirm** button to delete the DB.


<span id="00db8d91"></span>
## Subsequent Operations

After creating the database, go to the **Table Management** page to create the required tables under the database. Refer to [Manage ByteHouse CDW Tables](https://docs.byteplus.com/docs/dataleap/Manage_ByteHouse_CDW_Tables) for instructions related to creating tables.
