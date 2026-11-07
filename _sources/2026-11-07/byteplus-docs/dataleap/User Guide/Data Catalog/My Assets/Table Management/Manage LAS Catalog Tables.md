---
title: "Manage LAS Catalog Tables"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Manage_LAS_Catalog_Tables"
---

Table management provides unified management for metadata creation, editing, and permission ownership. This article explains how to manage LAS Catalog tables.

<span id="_1-前提条件"></span>
## **Prerequisites**

A LAS Catalog database has been created. For related instructions, see [Manage LAS Catalog DB](https://docs.byteplus.com/docs/dataleap/Manage_LAS_Catalog_DB).

<span id="_2-操作步骤"></span>
## Operation Steps


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> My Assets \> Table Management** to enter the Table Management page.

3. Click the **LAS Catalog** tab to enter the LAS Catalog management page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bfe2f8f381f84ee2aadbbfeabe2ced55~tplv-goo7wpa0wc-image.image) </span>

4. The following actions can be performed:

   * Create a new LAS Catalog table

      Supports visual table creation and DDL table creation.

      * Click the **New LAS Catalog Table** button to directly enter the visual table creation page. Fill in the table information and click the **Table Creation Check** button to verify compliance with the table creation standard. After confirmation, click the **Submit** button to complete the LAS Catalog table creation. Refer to [Data Warehouse Table Creation Specification](https://docs.byteplus.com/docs/dataleap/data_warehouse_table_creation_specification) for related instructions on table creation standards.

      * Click the **New LAS Catalog Table \> DDL Table Creation** button to enter the DDL table creation page. Write the DDL statement, then click the **Parse** button to display field information. Fill in other form information and click the **Table Creation Check** button to verify compliance with the table creation standard. After confirmation, click the **Submit** button to complete the LAS Catalog table creation.

      
      |Parameters |Description |
      |---|---|
      |**DDL information** ||
      |\*DDL statement |Write DDL table creation statements.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Currently, primary key types only support basic types: string, int, bigint, double. Setting other types as primary keys may cause unexpected problems when data is inserted.</div><br> |
      |**Basic information** ||
      |* THE NAMES |LAS Catalog is the data directory name on the engine side used to store databases and tables.<br><br>Select from the dropdown of created data directories; once set, it cannot be changed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">LAS Catalog supports three data directory types: Hive, Iceberg, and Lance; currently, DataLeap only supports selecting Hive or Iceberg data directories.</div><br> |
      |\*LAS Catalog DB name |The name of the database under the LAS Catalog data directory. Select from the drop\-down list of created databases. Once set, it cannot be changed. |
      |Managing Business Line |The business line the data table belongs to. Select from the drop\-down list of created business lines.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is recommended that each business line establish a standardized modeling system to ensure the naming conventions of table creation. For related instructions, see <a href="https://docs.byteplus.com/docs/dataleap/Create_Business_Line">Create Business Line</a>.</div><br> |
      |Data layer |The layer where the data table is located. Supports the following options and can be selected from the drop\-down list. Supports quick selection by searching keywords in the layer name.<br><br><br>* Operational Data Store (ods)<br><br>* Data Integration Layer (dwi)<br><br>* Basic Dimensions<br><br>* Detailed data layer<br><br>* Intermediate data layer<br><br>* Data Warehouse Service<br><br>* Data warehouse application layer<br><br>* Data Market Layer<br><br>* Application Service Layer<br><br>* Application layer<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you select <strong>Managing Business Line</strong>, only the data hierarchy options included in that business line will be displayed.</div><br> |
      |Canonical Modeling Category |Category classification of offline business model specifications. Drop down to select the data classification of the created model specification category. Please refer to [Category Management](https://docs.byteplus.com/docs/dataleap/Category_Management) for the relevant operation instructions for creating model specification category data classification.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After selecting the managing business line and its associated data layer, you can set this parameter.</div><br> |
      |\*LAS Catalog table name |Create a data table name under the selected database; once set, it cannot be changed.<br><br>Only supports numbers, lowercase English letters, and underscores.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">After selecting the data layer and model specification category, the corresponding table name prefix and suffix will be filled in automatically; please avoid adding duplicates.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When multiple data classifications are associated, even if a classification with mandatory table naming exists, the classification abbreviation will not be automatically added to the table name prefix; please add it manually.</div><br> |
      |Chinese name |Chinese name of the data table. |
      |LAS Catalog table type |New data table types support three options: **hive**, **paimon**, and **iceberg**, selectable from the dropdown. Table type cannot be changed once set.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If no table type is selected, a <strong>hive</strong> table will be created by default.</div><br> |
      |\*Storage format |Data storage format supports three options: **parquet**, **text**, and **orc**, selectable from the dropdown. |
      |\*Partition type |Whether the data table is partitioned; supports **partition table** and **non\-partitioned table** options.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When selecting a <strong>partition table</strong>, set the displayed partition fields in the field info <strong>partition fields in the field info</strong> section. It is recommended to use string type for partition fields and avoid date, double, boolean, and other types to prevent type conversion failures and precision loss.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Partition tables are not supported when the <strong>LAS Catalog table type</strong> is set to <strong>iceberg</strong>.</div><br> |
      |Description |Description of the data table to facilitate later management. |
      |**Field info (visual table creation)**  ||
      |Entry method |Choose to fill in **Form** or **Excel**. |
      |Primary key |The primary key is one or more fields in a table whose value uniquely identifies a record in the table.<br><br>If it is a composite primary key, multiple fields must be selected. |
      |\*English name |The English name of the field, only lowercase English letters, numbers, and underscores are supported. |
      |\*Field type |Fill in according to the actual situation, multiple types supported, selectable from the dropdown. |
      |\*Field description |Description of the field for subsequent management, required field.<br><br>Supports AI generation. After setting the field's English name, descriptions can be generated as follows:<br><br><br>* Click the **AI Generation** button for this parameter to quickly generate descriptions for each corresponding field. Existing field descriptions will be ignored.<br><br>* Click the **field description** next to a field’s **AI Generation** icon to quickly generate the description for that field. If a description already exists for this field, it will be overwritten directly. |
      |Custom tag |Tags set for the field, supporting the following two methods:<br><br><br>* Select existing tags from the dropdown, supporting quick selection by searching tag keywords.<br><br>* Set tags manually: enter the tag manually, then select it from the dropdown list. |
      |Business Line Tags |Business line tags assigned to the field; select from already created tags in the business line dropdown. Multiple tags can be set.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can only select the tags created under the corresponding business line after choosing the <strong>business line</strong>.</div><br> |
      |**Security Information** ||
      |\*Confidentiality Level |The table's security level, with four options from low to high: L1, L2, L3, and L4.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The table's classification level cannot exceed that of its DB.</div><br> |
      |\*Table Authority Owner |The data security owner of the table; automatically filled with the current user, editable, and supports multiple entries. |
      |**Development information** ||
      |Data Development Project |The data table's project, selectable from a drop\-down list of created projects bound to the LAS Catalog service. |
      |**Portal information** ||
      |Portal Business Line |The asset portal business line to which the data table belongs. Dropdown options include created business lines, multiple selections allowed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The portal business line primarily provides data classification and management from a business perspective. An asset can belong to multiple portal business lines and multiple data classifications.</div><br> |
      |Business Classification |Data classification under the business line; select from the dropdown among created data classifications; multiple selections allowed. Refer to [Category Management](https://docs.byteplus.com/docs/dataleap/Category_Management) for operating instructions on creating data classifications.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The parameter can only be set after selecting the business line.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can only select the data classification of the <strong>model specification category</strong> after choosing the business line and the associated data layer.</div><br> |
      |Data Album |The data table's album, selectable from created **custom directory** or **fixed directory** albums in the drop\-down.<br><br>Can be quickly added to albums you manage. |
      |Status |The current status of the table, supports the following options, selectable from the drop\-down.<br><br><br>* Test: a table used for debugging and testing, not for actual production development.<br><br>* Temporary: Used to temporarily save some data during testing or development; will be cleared regularly.<br><br>* Active: Valid tables used in user production and development.<br><br>* Deprecated: Tables that are no longer used for production or testing.<br><br>* Pending Deactivation: Tables about to be taken offline, no longer used in production or development.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, the status options are for labeling only and have no functional effect.</div><br> |
      |Core or not |You can choose whether to mark the table as core. |
      |Custom Tags |Tags assigned to tables, supporting the following two settings:<br><br><br>* Select from existing tags in the dropdown, support quick selection by searching tag keywords.<br><br>* Set tags manually: after entering tags, select the tag from the dropdown list. |
      |Business Line Tags |Set business line tags for the table. Select from created tags in the dropdown. Multiple selections allowed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can select tags created under the corresponding business line only after choosing a <strong>business line</strong>.</div><br> |
      |Business glossary |Business glossary terms associated with the table. Select from created terms in the dropdown.<br><br>Supports quick selection by searching business glossary term keywords. |
      |Business domain |The business domain the table belongs to. Select from created domains in the dropdown. Supports quick selection by searching business domain keywords.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This metadata tag is pending deactivation; custom labels or business line tags are recommended as replacements.</div><br> |
      |Product line |Specifies the product line the table belongs to. Select from the created product lines in the dropdown. Supports quick selection by searching product line name keywords.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This metadata tag is pending deactivation; custom labels or business line tags are recommended as replacements.</div><br> |
      |Theme |Specifies the theme the table belongs to. Select from the created themes in the dropdown. Supports quick selection by searching theme name keywords.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This metadata tag is pending deactivation; custom labels or business line tags are recommended as replacements.</div><br> |
      

   * Set search criteria to search the list of matching information.

      When multiple search criteria are set, the query will use the intersection of all conditions.

   * Click the **Manage** button in the **Action** column of a data table record in the list to modify the metadata tag information of that table.

   * Click the **Edit** button in the **Action** column of a table info in the list to modify the table info.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Data type has compatibility issues. When editing table fields, type conversion succeeds only if compatible. Compatibility instructions are as follows:      </div>
      

         1. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If the field type is within the range {“string”, “varchar”, “char”}, they can be converted to each other and all can be converted to double type.      </div>
      

         2. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If the field type is within the range {“tinyint”, “smallint”, “int”, “bigint”, “float”, “double”, “decimal”}, types with smaller length can convert to types with larger length, for example, int converting to bigint is compatible, but bigint converting to int is not compatible.      </div>
      

         3. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If the field type is within the range {“date”, “datetime”, “timestamp”, “timestamp with time zone”}, they can be converted to {“string”, “varchar”, “char”} types.      </div>
      

         4. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Except for the above cases, all others are incompatible.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If the table is a datasource table, editing table field information here is not supported.      </div>
      

   * Click the  **...**   **\> Transfer** button in the **Action** column of a table info in the list to change the table owner and transfer the authority owner roles at the same time.

   * Click the  **... \> Permission Settings** button in the **Action** column of a table info in the list to go to **Permission management \> Permission Settings** for approval process setup.

   * Click the  **...**   **\> Delete** button in the **Action** column of a table info in the list, and in the pop\-up confirm deletion dialog, click the **Confirm** button to delete the table.

   * Select one or multiple table infos to perform batch transfer, batch delete, or batch management operations.
