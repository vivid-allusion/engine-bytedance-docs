---
title: "Manage ByteHouse CE Tables"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Manage_ByteHouse_CE_Tables"
---

Table management provides unified handling of metadata creation, editing, and authorization ownership. This article introduces how to manage ByteHouse CE tables.

<span id="2c44a956"></span>
## Constraints

Only the main account or sub\-accounts with **ByteHouseCEStandardAccess** permission can correctly create and edit data tables. Sub\-account authorization activation requires the following steps; see [Bytehouse Enterprise Documentation](https://docs.byteplus.com/en/docs/bytehouse/getting-started#_3-import-users) for details.


1. The main account grants **ByteHouseCEStandardAccess** permission to sub\-accounts via the Console.

2. The sub\-account logs into the **ByteHouse CE Console** once.


<span id="_1-前提条件"></span>
## Prerequisites

A ByteHouse CDW database has been created. For related operating instructions, refer to [Manage ByteHouse CE DB](https://docs.byteplus.com/docs/dataleap/Manage_ByteHouse_CE_Database).

<span id="_2-操作步骤"></span>
## Operation Steps


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> My Assets \> Table Management** to enter the Table Management page.

3. Click the **ByteHouse CE** tab to enter the ByteHouse CE management page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d06d78c7de94d4aaa8be6f2927acbef~tplv-goo7wpa0wc-image.image) </span>

4. The following operations can be performed:

   * Create a new ByteHouse CE table

      Click the **Create ByteHouse CE Table** button to enter the create table page, fill in the table information, then click the **Table creation check** button to verify compliance with creation standards. After confirmation, click the **Submit** button to complete the ByteHouse CE table creation. For related operating instructions on creation standards, please refer to [Data Warehouse Table Creation Specification](https://docs.byteplus.com/docs/dataleap/data_warehouse_table_creation_specification).

      The related parameters for creating a ByteHouse CE table are shown in the table below. Parameters marked with \* are required; those without \* are optional.

      
      |Parameters |Description |
      |---|---|
      |**Basic information** ||
      |\*Cluster |ByteHouse CE cluster name, dropdown to select from created clusters. |
      |\*Database name |ByteHouse CE database name, select from the dropdown of created databases. |
      |Manage business line |The business line the data table belongs to, select from the dropdown of created business lines.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is recommended that each business line establish a standardized modeling system to ensure naming standards for table creation. Refer to <a href="https://docs.byteplus.com/docs/dataleap/Create_Business_Line">Create Business Line</a> for related operating instructions.</div><br> |
      |Data layer |The layer where the data table resides, supports the following options, selectable from the dropdown. Supports quick selection by searching for keywords in the layer name.<br><br><br>* Operational data store (ods)<br><br>* Data integration layer (dwi)<br><br>* Basic Dimensions (dim)<br><br>* Detailed data layer (dwd)<br><br>* Intermediate data layer (dwm)<br><br>* Data Warehouse Service (dws)<br><br>* Data warehouse application layer (dwa)<br><br>* Data Market Layer (dm)<br><br>* Application Service Layer (ads)<br><br>* application layer (app) |
      |Canonical Modeling Category |Below the business line, model specification category classification, dropdown to select data classification of the created model specification category. Refer to [Category Management](https://docs.byteplus.com/docs/dataleap/Category_Management) for related operation instructions on creating model specification category data classification.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can set this parameter only after selecting the business line and the associated data hierarchy.</div><br> |
      |\*Table name |Name of the data table created under the selected database, cannot be changed once set.<br><br>Only supports numbers, lowercase English letters, and underscores.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After selecting the data hierarchy and canonical modeling category, corresponding table name prefixes and suffixes are automatically filled. Avoid adding duplicates.</div><br> |
      |Chinese name |Chinese name of the data table. |
      |Description |Description of the data table to facilitate subsequent management. |
      |**Field Info** ||
      |Entry method |You can fill in using either form or Excel methods. |
      |Primary Key |The primary key consists of one or more fields that uniquely identify a record in the table.<br><br>If it is a composite primary key, multiple fields must be selected. |
      |\*English Name |The English name of the field, which must start with a letter or underscore, followed by letters, numbers, or underscores. |
      |\*Field Type |Fill in according to the actual situation. Multiple types are supported and selectable from the dropdown. |
      |Can be empty |You can choose whether to allow this field to be empty. |
      |\*Field Description |Description of the field for future management; required field. |
      |\*Sort Key |Used to determine the physical storage order of data in the database.<br><br>Select from filled and non\-empty fields in the dropdown; up to 5 sort keys can be set without duplication. |
      |Partition Key |Used to determine the data partition each table row belongs to, dividing large tables into smaller parts.<br><br>Select from filled and non\-empty fields in the dropdown; up to 5 can be set.<br><br>Only fields of type **Date** or **Datetime** can be partitioned by day, month, or year. |
      |TTL |Table lifecycle settings.<br><br>This parameter can only be set after defining a partition key of type Date or Datetime. |
      |\*Primary Key |Used to organize data files and enforce uniqueness for each record in the table.<br><br>The primary key dropdown options depend on the order of the sort key. |
      |Sampling Key |Use the sampling key to obtain sample data from certain parts.<br><br>Choose from **field type** as **UInt** for the **sort key** and **primary key** in the dropdown list. |
      |\*table engine |Supports two engine options: HaMergeTree and HaUniqueMergeTree.<br><br>When selecting **HaUniqueMergeTree**, choose the unique key and its validity scope. |
      |\*unique key |Ensures uniqueness of data in the corresponding fields. The unique key provides an UPSERT function to ensure users can query the latest unique key value.<br><br>The dropdown lists filled and non\-empty fields; up to 10 can be set. Supports two levels to determine unique value granularity: **partition range** and **data table range**.<br><br>This parameter must be set when the **table engine** is set to **HaUniqueMergeTree**. |
      |unique key version field |Ensure that data with the same unique key only updates when **the current value ≥ the existing value**.<br><br>Dropdown selectable, only supports fields of type **UInt**, **Date**, or **DateTime** that are not nullable. |
      |**Security Information** ||
      |\*Confidentiality Level |The table’s security level, with options L1, L2, L3, and L4 in ascending order.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The classification level of the table cannot be higher than that of its DB.</div><br> |
      |\*Table Authority Owner |The data security authority owner of the table, auto\-filled, editable, supports multiple entries. |
      |**Portal Information** ||
      |Portal Business Line |The portal business lines to which the data table belongs. Select from created business lines in the dropdown. Multiple selections are supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The portal business line mainly provides data classification and management from a business perspective. One asset can belong to multiple portal business lines and multiple data classifications.</div><br> |
      |Business Classification |The business classification to which the data table belongs. Select from created comprehensive or custom data classifications in the dropdown.<br><br>This classification is the directory name under the specified business line in the "Asset Catalog," used for asset portal construction.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can set this parameter only after selecting the <strong>portal business line</strong>.</div><br> |
      |Data Album |The album to which the data table belongs. Select from created **custom directories** or **fixed directories** in the dropdown.<br><br>Can be quickly added to the albums you manage. |
      |Status |Shows the current life cycle status of the table. The following options are supported and selectable from the dropdown.<br><br><br>* Test: A table for test and debugging purposes, not used in actual production development.<br><br>* Temporary: Used for temporarily saving some data during testing or development; regularly cleaned up.<br><br>* Online: A valid table for user production development.<br><br>* Deprecated: A table that is no longer used for production or testing.<br><br>* Pending Deactivation: A table that will be deactivated soon and is no longer used for production development.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, status options are used for labeling only and have no functional effect.</div><br> |
      |Core or not |Optionally set the table as core. |
      |custom label |Tags set for the table support the following two methods:<br><br><br>* Select existing tags from the dropdown, with keyword search to quickly find tags.<br><br>* Set tags manually: after entering a tag manually, select it from the dropdown list. |
      |Business line tags |Set business line tags for the table; select multiple existing tags from the dropdown.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Select <strong>portal business line</strong> first before choosing tags created under the corresponding business line.</div><br> |
      |Business glossary |Business glossary terms associated with the table; select created business glossary terms from the dropdown.<br><br>Supports keyword search on business glossary term names for quick selection. |
      |Business domain |The table's business domain. Select from the dropdown of created business domains. Supports quick selection by searching business domain name keywords.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This metadata tag will soon go offline. It is recommended to use custom labels or business line tags instead.</div><br> |
      |Product line |The table's product line. Select from the dropdown of created product lines. Supports quick selection by searching product line name keywords.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This metadata tag will soon go offline. It is recommended to use custom labels or business line tags instead.</div><br> |
      |Theme |The table's theme. Select from the dropdown of created themes. Support quick selection by searching theme name keywords.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This metadata tag will soon go offline. It is recommended to use custom labels or business line tags instead.</div><br> |
      

   * Set search criteria to list information that matches the conditions.

      When multiple search criteria are set, the query returns the intersection of all conditions.

   * Click the **Manage** button in the **Action** column of a table record to modify its metadata tag information.

   * Click the **Edit** button in the **Action** column of a table record to modify the table information.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If the <strong>ByteHouse CE</strong> table structure has been modified through DataLeap’s SQL jobs but <strong>metadata ingestion</strong> has not yet been performed in the Data Catalog, modifying the table information will cause an exception. In this case, manually ingest metadata first to sync the table structure to the Data Catalog, then modify the table information.      </div>
      

   * Click the  **...**   **\> Transfer** button in the **Action** column of a table record to proceed, allows changing the table owner and transferring the authority owner role simultaneously.

   * Click the  **...**   **\> Copy table** button in the **Action** column of a table record to proceed, lets you duplicate the table information and open the Create Table page to create a new table as needed.

   * Click the  **...**   **\> Permission Settings** button in the **Action** column for a data table entry in the list, lets you go to **Permission Management \> Permission Settings** to set up the approval process.

   * Click the  **...**   **\> Delete** button in the **Action** column for a data table entry in the list, opens a confirmation dialog; click the **OK** button to delete the table.

   * Select one or more data table entries to perform batch transfer, batch delete, or batch management operations.
