---
title: "Manage ByteHouse CDW Tables"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Manage_ByteHouse_CDW_Tables"
---

Table management provides unified management for metadata creation, editing, authorization, and ownership. This article explains how to manage ByteHouse CDW tables.

<span id="_1-前提条件"></span>
## Prerequisites

The ByteHouse CDW database has been created. For related instructions, see [Manage ByteHouse CDW DB](https://docs.byteplus.com/docs/dataleap/Manage_ByteHouse_CDW_DB).

<span id="_2-操作步骤"></span>
## Operation Steps


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> My Assets \> Table Management** to enter the Table Management page.

3. Click the **ByteHouse CDW** tab to enter the ByteHouse CDW management page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e567e1f22a264c1ba324b8303cd6e47c~tplv-goo7wpa0wc-image.image) </span>

4. Perform the following operations:

   * Create a ByteHouse CDW table

      Click the **Create ByteHouse CDW table** button to enter the table creation page. After filling in the table information, click the **Submit** button to complete the ByteHouse CDW table creation.

      The relevant parameters for creating a ByteHouse CDW table are explained in the following table. Parameters marked with \* before the name are required; those without \* are optional.

      
      |Parameters |Description |
      |---|---|
      |**DDL information** ||
      |\*DDL statement |Write DDL table creation statements.<br><br>Set this parameter only when **DDL table creation** is selected. |
      |**Basic information** ||
      |\*Cluster |The cluster where the database to be created is located; select from clusters with existing collectors. Refer to [Metadata Ingestion](https://docs.byteplus.com/docs/dataleap/Metadata_Ingestion) for collector creation operations. |
      |\*ByteHouse CDW database name |ByteHouse CDW database name; select from existing databases. |
      |Manage business line |The business line to which the data table belongs. Select from created business lines in the dropdown.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Suggest each business line establish a standardized modeling system to ensure consistent table naming. For related operating instructions, refer to <a href="https://docs.byteplus.com/docs/dataleap/Create_Business_Line">Create Business Line</a>.</div><br> |
      |Data Layer |The layer where the data table resides. Supported options are available in the dropdown. Supports quick selection by searching layer name keywords.<br><br><br>* Operational Data Store (ods)<br><br>* Data Integration Layer (dwi)<br><br>* Basic Dimensions (dim)<br><br>* Detailed data layer (dwd)<br><br>* intermediate data layer (dwm)<br><br>* data warehouse service layer (dws)<br><br>* data warehouse application layer (dwa)<br><br>* data market layer (dm)<br><br>* application service layer (ads)<br><br>* application layer (app) |
      |canonical modeling category |Model category classification under the business line. The dropdown allows selecting created model specification categories' data classifications. For related operating instructions on creating model specification category data classifications, see [Category Management](https://docs.byteplus.com/docs/dataleap/Category_Management).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can set this parameter only after selecting the business line and the associated data hierarchy.</div><br> |
      |\*ByteHouse CDW table name |Name of the data table created under the selected database. This cannot be changed once set.<br><br>Only numbers, lowercase letters, and underscores are supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After selecting data hierarchy and canonical modeling category, the corresponding table name prefixes and suffixes will fill automatically. Avoid adding duplicates.</div><br> |
      |Chinese name |Chinese name of the data table. |
      |Description |Description of the data table for later management. |
      |**Field info** ||
      |Entry method |Choose to fill in by form or Excel |
      |\*English Name |The English name of the field, only supports combinations starting with letters or underscore and including letters, numbers, and underscores. |
      |\*Field Type |Fill in according to actual situation, multiple types supported, selectable from dropdown. |
      |Field Description |Description of the field to assist subsequent management, required field. |
      |Default Value |Default value of the field, set by yourself.<br><br>The default value can be an expression or a constant. For String or Time type constants, please enclose the input value in single quotes, such as 'Hello Word' and '1970\-01\-01'. |
      |Can be empty |Choose whether to allow this field to be empty. |
      |**Advanced settings** (After creating the data table, sort keys and partition keys cannot be changed. Select carefully.) ||
      |\*Sort key |Used to determine the physical storage order of data in the database.<br><br>Select from filled and non\-empty fields in the dropdown. Up to 5 sort keys can be set, and duplicates are not allowed. |
      |Partition key |Used to determine the data partition each row belongs to, splitting large tables into smaller parts.<br><br>Select from filled and non\-empty fields in the dropdown. Up to 5 partition keys can be set.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the selected field is of type <strong>Date</strong>, <strong>Datetime</strong>, or <strong>Datetime64</strong>, partitioning can be done directly by day, month, or year.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For other field types, first specify the partitioning form as <strong>Date</strong>, <strong>Datetime</strong>, or <strong>Datetime64</strong>, then partition by day, month, or year.</div><br> |
      |Unique key |Used to ensure the uniqueness of data in the corresponding field. The dropdown allows selection of fields set as **partition keys**, with a maximum of 10.<br><br>Supports two levels for defining uniqueness granularity: **partition range** and **data table range**.<br><br>Unique keys enable Upsert (Update and Insert) functionality to ensure deduplication at the partition level and always retrieve the latest value for the corresponding unique key. |
      |Bucket key |For each table or partition, specifying the Cluster Key further subdivides data into buckets by hashing column data, enabling finer granularity partitioning and improving query and sampling efficiency. |
      |Primary key |Used to organize data files and uniquely identify each record in a data table.<br><br>The primary key dropdown options correspond to the order of the sort key. |
      |sampling key |Obtain sample data of certain parts by defining sampling keys.<br><br>Select from **Field Type** as **UInt** in **sort key** and **primary key**, dropdown optional. |
      |**Security Information** ||
      |\*confidentiality level |The table's security level has four options from low to high: L1, L2, L3, and L4.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The table classification cannot be higher than the database classification level.</div><br> |
      |\*table authority owner |The table's data security authority owner, auto\-filled, editable, and supports multiple entries. |
      |**portal information** ||
      |portal business line |The asset portal business line to which the table belongs. Select from created business lines in the dropdown; multiple selection supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The portal business line primarily provides data classification and management from a business perspective. An asset may belong to multiple portal business lines and multiple data classifications.</div><br> |
      |business classification |The business classification of the table. Select from created comprehensive or custom classification types in the dropdown.<br><br>In "Asset Catalog," this classification specifies the file directory name under the business line for asset portal construction.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only after selecting the <strong>portal business line</strong> can this parameter be set.</div><br> |
      |core or not |Select whether to set the table as core. |
      |custom label |Tags set for the table support the following two methods:<br><br><br>* Dropdown allows selecting existing tags, supporting quick selection by searching tag keywords.<br><br>* Set tags manually: after entering a tag manually, select it from the dropdown list. |
      |Business line tags |Business line tags set for the table, with a dropdown to select created tags; multiple selections are allowed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can select created tags under the corresponding business line only after choosing a <strong>Portal Business Line</strong>.</div><br> |
      |Business glossary |Business terms associated with the table, selectable from created business terms in a dropdown.<br><br>Supports quick selection by searching keywords in business term names. |
      |Business domain |The business domain the table belongs to. Select from the dropdown of created business domains. Supports quick selection by searching business domain name keywords.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This metadata tag is about to be taken offline. It is recommended to use custom labels or business line tags instead.</div><br> |
      |Product line |The product line the table belongs to. Select from the dropdown of created product lines. Supports quick selection by searching product line name keywords.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This metadata tag is about to go offline. It is recommended to use custom tags or business line tags as replacements.</div><br> |
      |Theme |The theme the table belongs to. Select from the dropdown of created themes. Supports quick selection by searching theme name keywords.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This metadata tag is about to go offline. It is recommended to use custom tags or business line tags as replacements.</div><br> |
      

   * Set search criteria to find matching records.

      When multiple search conditions are set, the query uses the intersection of all conditions.

   * Click the **Manage** button in the **Action** column of a data table in the list to edit the table's metadata tags.

   * Click the **Edit** button in the **Action** column of a data table in the list to modify the table information.

   * Click the  **...**   **\> Transfer** button in the **Action** column of a data table in the list to change the table owner and transfers the authority owner roles simultaneously.

   * Click the  **... \> Copy table** button in the **Action** column of a data table entry in the list to duplicate the table information and opens the create table page to create a new data table as needed.

   * Click the  **...**   **\> Permission Settings** button \*\*\*\* in the **Action** column of a data table entry in the list to navigate to **Permission Management \> Permission Settings** to configure the approval process.

   * Click the  **... \> Delete** button in the **Action** column of a data table entry in the list to open a confirmation dialog. Click the **OK** button to delete the table.

   * Select one or more data table entries to perform batch transfer, batch delete, or batch management operations.
