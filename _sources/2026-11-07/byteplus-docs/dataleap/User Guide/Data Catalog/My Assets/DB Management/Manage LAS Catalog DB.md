---
title: "Manage LAS Catalog DB"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Manage_LAS_Catalog_DB"
---

Database management provides unified creation, editing, and permission ownership of metadata. This article introduces how to manage the LAS Catalog database.

<span id="_1-约束限制"></span>
## **Constraints**

Users can only manage databases where they are database owners.

<span id="_2-前提条件"></span>
## **Prerequisites**

The collector has been created and the metadata from the LAS Catalog cluster has been ingested into the Data Catalog. See related operation instructions in [Metadata Ingestion](https://docs.byteplus.com/docs/dataleap/Metadata_Ingestion).

<span id="_3-操作步骤"></span>
## Operation Steps


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> My Assets \> DB Management** to enter the DB Management page.

3. Click the **LAS Catalog** tab to enter the LAS Catalog page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9edebff8cf6f4da5b074d9e27796c709~tplv-goo7wpa0wc-image.image) </span>

4. You can perform the following operations:

   * Click the **Create LAS Catalog DB** button, fill in the information in the pop\-up creation window, then click the **OK** button to create a new LAS Catalog DB.

      
      |Parameters |Description |
      |---|---|
      |\*directory |LAS Catalog engine\-side data directory name, used to store databases and tables.<br><br>Dropdown to select created data directories; once set, it cannot be changed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">LAS Catalog supports three types of data directories: Hive, Iceberg, and Lance. Currently, DataLeap only supports selecting Hive and Iceberg types of data directories.</div><br> |
      |\*database name |Name of the created database; once set, it cannot be changed.<br><br>Only supports lowercase English letters, numbers, and underscores; must start with a lowercase letter, within 50 characters. |
      |\*DB owners |Database admin, a develop role responsible for the DB’s daily operation and maintenance.<br><br><br>* Automatically fills with the current user when creating a DB. Supports setting multiple users and selecting from created tenant accounts in the dropdown. The owner can be replaced, but you cannot remove yourself.<br><br>* Option to sync to the database authority owner. |
      |\*Database authority owner |A security management role that manages all resources under the DB (authorization retrieval, classification settings, approval flow configuration, etc.). Responsible for deciding whether data can be opened and directly participates in the overall DB permission approval.<br><br>When the **DB owners** uncheck **synchronize to the database authority owner**, this parameter becomes editable and supports multiple selections. |
      |Description |Information that explains the DB’s range, usage, etc., to aid future management. |
      |\*DB usage |There are two options: production environment and test environment. |
      |\*Confidentiality Level |The database security level ranges from low to high as L1, L2, L3, and L4, selectable from the dropdown. |
      

   * Enter a name or description keyword to search the list of databases that match the criteria.

   * Click the **Edit** button in the **Action** column for a database entry in the list to modify its information.

   * Click the **Delete** button in the **Action** column for a database entry in the list. In the pop\-up confirmation dialog, click the **OK** button to delete the database.


<span id="bb492dba"></span>
## Subsequent Operations

After creating the database, proceed to the **Table Management** page to create the required tables under the database. For instructions on creating tables, please refer to [Manage LAS Catalog Tables](https://docs.byteplus.com/docs/dataleap/Manage_LAS_Catalog_Tables).
