---
title: "Set Application Permissions"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Set_Application_Permissions"
---

Setting permissions for data resources controls users’ access to protect data security and privacy, preventing unauthorized access and operations. This feature lets you configure access permissions for resources, including authority owners, confidentiality levels, application restrictions, and renewal rule settings. The following provides a detailed introduction on how to configure resource application permissions.

<span id="_1-配置申请权限"></span>
## Constraints

Only authority owners for database, table, row, and column resources can view and configure access rights for those resources.

<span id="d70944bf"></span>
## Prerequisites

The supported data sources have completed the corresponding metadata ingestion; for related operating instructions, refer to [Metadata Ingestion](https://docs.byteplus.com/docs/dataleap/Metadata_Ingestion).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After ByteHouse CE metadata ingestion, existing data synchronizes to <strong>data security</strong> on T+1 day; incremental data synchronizes in real time.</div>


* <div data-tips="true" data-tips-type="tip">After LAS Catalog metadata ingestion, synchronization to <strong>data security</strong> requires T+1 day.</div>



<span id="3c397258"></span>
## **Set Database Permissions**


1. Log in to the DataLeap console.

2. Select **Overview \> Security \> Authorization Management \> Authority Settings \> Database** to enter the **Database** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be016fe8ad784bb89e33522603242a84~tplv-goo7wpa0wc-image.image) </span>

3. You can perform the following operations:

   * Search database

      Search for database resources that meet the criteria by setting resource type, confidentiality level, database, authority owner, parameter filtering, and other conditions. When multiple search conditions are set, the intersection of all conditions is used for the query.

   * Configure a single database

      1. Click the **Settings** button in the **Action** column of a database entry to enter that database’s permission settings page.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b57b628d4bb44a0bca695937d0c6960~tplv-goo7wpa0wc-image.image) </span>

      2. You can modify the related permission parameters.

         
         |Parameters |Description |
         |---|---|
         |**Basic Settings** ||
         |\*Authority Owner |The authority owner of the database supports setting as an individual or role group.<br><br><br>* Individual: selectable from the dropdown, multiple selections supported. You can delete the current owner or add a new owner by entering the tenant account keyword and selecting from the dropdown list.<br><br>   After adding or deleting at least one authority owner, the parameter **Increase or decrease application to sub\-level?**  will be displayed. You can choose whether to modify sub\-level resources at the same time.<br><br>   * Yes, modify sub\-level resources simultaneously: the person will be added or removed from the owner settings of all sub\-level resources. For example, if authority owner A is removed at the table level, A will be removed from the row\-column (if any) hierarchy and the default owners of newly added row enumerations under that table.<br><br>   * No, applied only at this level: changes related to the authority owner apply only to the current resource.<br><br>* Role group: select from created role groups in the dropdown. For instructions on creating role groups, see [Set Automatic Approval Rules](https://docs.byteplus.com/docs/dataleap/Set_Automatic_Approval_Rules).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After the authority owner changes, the approvers of pending work orders update synchronously.</div><br> |
         |Confidentiality level |Database security confidentiality levels, from low to high: L1, L2, L3, and L4, selectable from the dropdown.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the classification changes, the approval process will change to the corresponding classification approval flow. For special needs, configure it at <a href="https://docs.byteplus.com/docs/dataleap/Set_Approval_Flow">Set Approval low</a> this location.</div><br> |
         |Confidentiality level escalation permission processing |You can choose whether to revoke permissions from the original grantee.<br><br><br>* Recycle all: all permissions of this type held by the original grantee will be revoked, and the original grantee must reapply as needed. Warehouse manager and table owner permissions remain unaffected.<br><br>* Do not recycle: retain the original grantee’s permissions.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter appears when the <strong>confidentiality level</strong> increases.</div><br> |
         |Renewal Rule |Set whether renewal is allowed.<br><br><br>* Allow: permit the grantee to renew.<br><br>   When renewing, only provide the reason for renewal; no approval is required to obtain permissions. For renewal operations, see [Manage Valid Permissions](https://docs.byteplus.com/docs/dataleap/Manage_Current_Permissions).<br><br>* Block: prohibit the grantee from renewing. Selecting this option requires providing a reason for disallowing renewal. |
         |Request Settings |Choose whether to open database access permission applications, supporting fine\-grained settings including **read\-only**, **read\-write**, and **create table**<br><br>When **block** is selected, provide a reason for the prohibition; when **allow** is selected, set the types of prohibited applications, including Multiple, Individual, and User Group options, supporting multiple selections<br><br><br>* Read\-only: allows only "read" operations on the resource, such as Select<br><br>* Read\-write: allows all operations on the resource, such as Insert, Select, etc.<br><br>* Create table: allows creating tables in the database where this permission is applied By default, you have read\-write permission to create new tables but cannot access other tables without permission in the database |
         |Application Q&A |You can choose whether to enable application Q&A for the resource; it is off by default When enabled, applicants must answer custom questions before submitting the application<br><br><br>* Scope of application: supports two options, **Only at this level** and **Resources at this level and below**.<br><br>* Title setting: add questions and customize problems, multiple questions can be added.<br><br>   * \*Topic: question type, supports three options: Q&A, single choice, and multiple choice.<br><br>   * \*Question: customize the question to be answered, no more than 512 characters.<br><br>   * \*Options: options for single\-choice or multiple\-choice questions, at least two options per question.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If <strong>resources at this level and below</strong> are selected at the database/table level, custom questions must be answered when applying for resources under that database/table. If applying for multiple resources under the same database/table, the questions only need to be answered once.</div><br> |
         |**Add default settings for table** (applies to newly added tables in the database after configuration) ||
         |default confidentiality level |confidentiality level of new tables in this database, selectable from dropdown.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The classification of a table cannot be higher than the classification of its database.</div><br> |
         |default authority owner |Authority owner responsible for new tables under this database. After entering tenant account keywords, selectable options appear in the dropdown; multiple entries are supported. |
         |Renewal rule |You can set whether the access rights of new tables under this database allow renewal. |
         |Request Settings |Permission application configuration can be selected for new tables under this database. |
         

      3. Click the **Save** button to complete the settings.

   * Batch modify permission owners

      When changes occur, such as work relation adjustments, requiring a change of database permission owners, this operation allows quick completion.

      1. After selecting one or more options, click the **Edit Authority Owner** button to open the **Edit Authority Owner** window.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f413202c4bbe46749c50f5bfd06768fc~tplv-goo7wpa0wc-image.image) </span>

      2. After setting the permission owner information as needed, click the **Confirm** button to complete the batch modification.

         
         |Parameters |Description |
         |---|---|
         |Change method |You can choose any one of the following change methods and select the Authority Owner from the dropdown list.<br><br><br>* Cover as: means replacing the existing Authority Owner with the selected person.<br><br>   For example, if the original Authority Owners are **A**, **B**, and **C**, and you choose to overwrite with **D**, the Authority Owner changes to **D**.<br><br>* Add to existing: means adding the selected person to the current owners.<br><br>   For example, if the original Authority Owners are **A**, **B**, and **C**, and you add **C** and **D** to existing, the final Authority Owners become **A**, **B**, **C**, and **D**.<br><br>* Find and delete: means removing the selected person if they are an existing owner.<br><br>   For example, if the original Authority Owners are **A**, **B**, and **C**, and you choose to find and delete **B** and **C**, the final Authority Owner is **A**.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If not found, do not delete.   </div><br>   <br><br>* Find and replace: means replacing the found owner with the person selected in the **replace with** dropdown if the found person is an existing owner.<br><br>   For example, if the original Authority Owners are **A**, **B**, and **C**, and you find **A** to replace with **D**, the final Authority Owners become **B**, **C**, and **D**.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If not found, do not replace.   </div><br>    |
         |Do you apply this modification to the subordinate (if any) resource? |You can choose whether to apply this modification to lower\-level resources. The default is no.<br><br><br>* Yes, modify subordinate resources at the same time<br><br>* No, only apply to this resource |
         

   * Batch modify confidentiality levels

      After selecting one or more options, click the **Edit Confidentially Level** button. In the popped\-up window, set the confidentiality level, then click the **Confirm** button.

   * Batch configure entire database application restrictions

      After selecting one or more options, select **Entire DBRequest Settings** from the **More Settings** dropdown. In the popped\-up window, set the application restrictions, then click the **OK** button.

   * Batch configure new table default settings

      After selecting one or more options, select **Add default settings for table** from the **More Settings** dropdown. In the pop\-up window, set the table's classification and authority owner, then click the **OK** button.

   * Batch modify renewal configuration

      After selecting one or more options, select **Set Renewal Rule** from the **More Settings** dropdown. In the pop\-up window, select whether to renew, then click the **OK** button.

   * Batch set application Q&A

      After selecting one or more options, select **Set Application Q&A** from the **More Settings** dropdown. In the pop\-up window, set the application Q&A information, then click the **OK** button.


<span id="_1-2-数据表配置"></span>
## **Set Data Table Permissions**

Use the data table permission settings feature to set access rights for the entire table, columns, and row\-level restrictions as required.


1. Log in to the DataLeap console.

2. Select **Overview \> Security \> Authorization Management \> Authority Settings \> Table** to enter the **Table** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02aad5feabd8445ca22c832bc81ce06a~tplv-goo7wpa0wc-image.image) </span>

3. Perform the following actions:

   * Search tables

   * Set table permissions

   * Set column permissions

   * Set row permissions


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When setting a single table, you can set both row and column permissions simultaneously.</div>


* <div data-tips="true" data-tips-type="tip">ByteHouse CDW tables do not support row permission configuration.</div>



<span id="b7744440"></span>
### Search Tables

This feature supports both ordinary and batch search methods to help you quickly find tables to configure. Among them, **batch search** addresses batch settings in scenarios where users lack clear resource filtering rules, reducing data scraping costs.


* Ordinary search

   Use filters such as resource type, confidentiality level, database, permission owner, and parameters to query matching table resources. When setting multiple search criteria, the intersection of all conditions will be used for the query.

* Batch Search

   1. Click the **Search in bulk** button to open the batch search window for the data table.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df8f7be13e7a4328b189da1503dd76b7~tplv-goo7wpa0wc-image.image) </span>

   2. Download and fill in the template as instructed.

   3. After selecting the data source and uploading the completed file, click the **Search** button to view the results.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Please enter the names of resources for which you are the Authority Owner (Owner or permission responsible), following the template instructions. For detailed format guidelines and examples, refer to the template content.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Fill in the resources corresponding to the selected datasource type on the current tab; otherwise, they will be filtered out.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The maximum parse limit is 1000 entries; it is recommended not to exceed 1000 entries per search.   </div>
   


<span id="d7c66ea6"></span>
### Set Table Permissions


* Configure a single data table

   Click the **Settings** button in the **Action** column of a data table entry to access its permission settings page. Here, you can modify the table\-level authority owner, confidentiality level, application restrictions, renewal rule, and more.

   
   |Parameters |Description |
   |---|---|
   |\*Column\-level |You can choose whether to enable apply by column permission.<br><br><br>* When **enabled**, applicants can select access rights by column when applying for resources.<br><br>* When **disabled**, authorized subjects will not lose permissions; only new permission requests will be affected. If disabled, a reason for disabling is required.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter only needs to be configured for ByteHouse CE and ByteHouse CDW.</div><br> |
   |Inherited application Q&A |If higher\-level resources have application Q&A settings, the resource will inherit this Q&A. To modify the Q&A information, contact the higher\-level resource owner. |
   |other parameters |see [Set Database Permissions](https://docs.byteplus.com/docs/dataleap/Set_Application_Permissions#3c397258) part for other parameter details. |
   

* Batch configure data tables

   You can batch modify the authority owner, confidentiality level, entire table application restrictions, renewal rule, and more. For details, see [Set Database Permissions](https://docs.byteplus.com/docs/dataleap/Set_Application_Permissions#3c397258).


<span id="183b9409"></span>
### Set Column Permissions


1. Click the **Settings** button in the **Action** column of a data table entry to access the permission settings page for that data table.

2. Click the **Column Settings** tab to open the column permissions setting page.

3. After setting the column permission parameters, click the **Save** button to complete the settings.

   
   |parameter |description |
   |---|---|
   |**sensitive column configuration** ||
   |How to deal with the rights of the original authorized party for the newly added sensitive column |after clicking the  **+ sensitive column** button to add sensitive column configurations, select whether the original grantees need to reapply for the newly added permissions.<br><br><br>* Full authorization: all original “database and table” grantees will be authorized.<br><br>* Not authorized: original “database and table” grantees must reapply for “sensitive column” permissions as needed; permissions of original column grantees, DBAs, and table owners remain unaffected.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Regardless of which option is chosen, the database manager and table owner will be granted permanent permissions for sensitive columns.</div><br> |
   |Sensitive column |Field name to be set as a sensitive column. Select from existing fields in the table using the dropdown. |
   |Confidentiality level |Confidentiality level of the sensitive column. Select from the dropdown.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The confidentiality level of sensitive columns is not restricted by the table classification and can be set independently.</div><br> |
   |Column Authority Owner |Authority Owner of the sensitive column. After entering tenant account keywords, select from the dropdown.<br><br>The Authority Owner of the column can be set independently. The Authority Owner of this sensitive column has the right to configure permissions for this column, including approval flows, auto approval rules, Authority Owner settings, confidentiality level, renewal rules, application restrictions, and other configurations. The Authority Owner will also act as the "Authority Owner" node in the approval flow to review work orders related to column permission applications. |
   |Description |Description information for this field. It is displayed automatically and cannot be manually maintained.<br><br>This information comes from the **field description** of this field. To modify it, go to the Data Catalog platform. Related instructions can be found in the [Retrieve Data](https://docs.byteplus.com/docs/dataleap/Search_Data) document for the corresponding type of data table. |
   |**Column default settings** (ByteHouse CE, ByteHouse CDW) ||
   |\*Inherit the table settings |You can choose whether to inherit the parent table's permission settings.<br><br><br>* Yes, column default settings will inherit table settings: column permissions automatically inherit the table's permission settings. This is selected by default.<br><br>* No, custom column default settings: do not inherit the table's permission settings. You can configure parameters such as **Confidentiality Level**, **Authority Owner**, and **Request Settings** in the column default settings section.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When a field classification is set higher than the table classification, the table classification will automatically upgrade to that level.</div><br> |
   |**Column settings** (ByteHouse CE, ByteHouse CDW) ||
   |Use column default settings |Edit the permissions of the column as needed via the **edit** button on the column field, and choose whether to use the column default settings.<br><br><br>* Yes: automatically inherit the **column default settings**, selected by default.<br><br>* No: do not inherit the **column default settings**, and manually configure parameters such as the column's **confidentiality level**, **authority owner**, and **request settings**. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only ByteHouse CE and ByteHouse CDW tables support configuration of all column permissions, with no distinction between sensitive and ordinary columns.   </div>
   

<span id="d10f9bd4"></span>
### Set Row Permissions


1. Click the **Settings** button in the **Action** column of a data table entry to access the permission settings page for that data table.

2. Click the **Row Settings** tab to open the row permission setting page.

3. After setting the parameters for row restrictions, click the **Save** button to complete the settings.

   
   |Parameters |Description |
   |---|---|
   |Row default settings |Provide default basic settings for subsequently added enumerated values (including Authority Owner additions and manual user applications), including confidentiality level, default Authority Owner, renewal configuration, and application configuration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>1. <div data-tips="true" data-tips-type="tip">If the new enumerated value default is not empty, the configuration here takes effect; if empty, it follows the table’s basic settings by default.</div><br><br><br>2. <div data-tips="true" data-tips-type="tip">After configuring, the restriction on newly added rows in the table (including those added by applicants) takes effect. Existing row restrictions require maintenance in the <strong>Settings</strong> section of the corresponding resource’s permission settings page.</div><br> |
   |**Row settings** ||
   |Row\-level |Choose whether to enable row\-level access application.<br><br><br>* Enable: activate row\-level access application for the table, allowing users to apply by row. Users can choose to apply by entire table or by row on the application page. **Enabling this does not affect users who already have table permissions.** <br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When accompanying row filter conditions, the confidentiality level judgment rule is as follows:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For tables accompanied by rows (applied by row), the resource confidentiality level is based on the row confidentiality level (if multiple rows are applied, the highest applies).   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When columns accompany rows, ordinary columns follow the row confidentiality level, while sensitive columns take the higher level (the higher of the sensitive column and row confidentiality levels).   </div><br>   <br><br>* Disable: Off by default, meaning the table does not allow row\-level access applications, only whole table applications. If previously enabled and then disabled, **only new applicants cannot apply by row,**  while **users with existing row permissions** can still manage their current row permissions. |
   |Manually add row enum |You can choose whether to allow manual addition of enumerated values.<br><br>If disabled, applicants cannot manually add new enumerated values on the application page and can only select from preset values.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When <strong>Row\-level</strong> is set to <strong>Enable</strong>, this parameter must be configured.</div><br> |
   |Controlled fields |Field to control access conditions. You can select controlled fields from the dropdown by clicking the **Add column field** button.<br><br>Controlled fields can have multiple enumerated values, each including the following parameters:<br><br><br>* \*Enumerated value: Manually input row\-level access enumerated values, such as Beijing, Shanghai.<br><br>* Confidentiality level: confidentiality level of the row, selectable from the dropdown. The row confidentiality level cannot exceed the table confidentiality level.<br><br>* Row authority owner: the authority owner for the row restriction; after entering tenant account keywords, select from the dropdown.<br><br>   The row authority owner has the power to set permissions independently, such as approval flows, auto approval rules, column authority owners, confidentiality levels, renewal configurations, application restrictions, and more. Simultaneously, the row authority owner acts as the "authority owner" node in the approval flow to approve column application tickets.<br><br>* Description: add a description for this enumerated value to facilitate maintenance and help applicants identify the application content.<br><br><br>Support adding enumerated values one by one or by bulk import.<br><br><br>* Add one by one: click **Add column field**, choose the controlled field from the dropdown, then click the  **+Enumeration value** button to set row restriction information.<br><br>* Bulk import: **Download batch template**, open the template and set the row restriction information, then **upload enumeration value file**.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Because the database includes tables and table permissions include rows, database admins and table Owners do not require permanent permissions restricted by row\-level access.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When batch adding enumerated values, the downloaded file contains the enumerated values already set in the current table configuration. Uploading the file will overwrite the enumerated value information in the list.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Deleting already set enumerated values is supported. After deletion, the corresponding row permissions of the original grantee will be revoked without affecting the entire table permissions.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Supports deleting controlled fields. After deletion, the row permissions of the original grantee will be revoked, which may affect the normal operation of data development tasks. Handle with care!</div><br> |
   


<span id="_1-3-敏感列-行限制配置"></span>
## **Set Column/Row Permissions**

You can configure and manage both column and row permissions simultaneously when configuring a data table. For detailed operations, refer to [Set Data Table Permissions](https://docs.byteplus.com/docs/dataleap/Set_Application_Permissions#_1-2-%E6%95%B0%E6%8D%AE%E8%A1%A8%E9%85%8D%E7%BD%AE) Part.

After adding data column/row restrictions, you can also modify or delete them individually. Follow these steps:


1. Log in to the DataLeap console.

2. Select **Overview \> Security \> Authorization Management \> Authority Settings \> Table** to enter the **Table** page.

3. The following operations can be performed:

   * Click the **Data column** tab to enter the sensitive column permission settings page, where you can manage sensitive column information.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec90b44fb5284b369ae804031750d112~tplv-goo7wpa0wc-image.image) </span>

      * Search for data columns

         * Use resource type, confidentiality level, database, authority owner, parameter filtering, and other criteria to search for sensitive column resources that meet the conditions. When multiple search criteria are set, their intersection will be used for the query.

         * Click the **Search in bulk** button. In the popup window, download and fill in the template as instructed, then upload the completed file for batch searching. For detailed instructions, see [Search Tables](https://docs.byteplus.com/docs/dataleap/Set_Application_Permissions#b7744440).

      * Manage a single data column

         Click the **Settings** button in the **Action** column of a data column to modify its authority owner, confidentiality level, application configuration, and renewal rule.

      * Batch operation

         After selecting one or more options, modify the authority owner, confidentiality level, sensitive column application configuration, renewal rule, and more in batch.

      * Delete column configuration

         Click the **Delete** button in the **Action** column of a data column, then click **Confirm** in the pop\-up confirmation dialog to delete the column's permission.

   * Click the **Row Filters** tab to enter the row\-level\-access settings page and manage row\-level\-access information.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/192fc6036fc243e697fd44c76c6b89c8~tplv-goo7wpa0wc-image.image) </span>

      * Search row\-level\-access

         * Search for row\-level\-access resources that match the criteria by setting resource type, confidentiality level, database, authority owner, parameter filters, and more. When multiple search criteria are set, the query returns the intersection of all conditions.

         * Click the **Batch Search** button, then in the pop\-up window, download and fill out the template as instructed, and upload the completed file to perform batch search. For detailed instructions, see [Search Tables](https://docs.byteplus.com/docs/dataleap/Set_Application_Permissions#b7744440).

      * Manage single row\-level\-access restriction

         Click the **Settings** button in the **Action** column of a row\-level\-access restriction entry to modify the authority owner, confidentiality level, application configuration, and renewal rule for that single restriction.

      * Batch Operate

         After selecting one or more options, you can batch modify the authority owner, confidentiality level, row\-level\-access application configuration, renewal rule, and more.

      * Delete row\-level\-access configuration

         Click the **Delete** button in the **Action** column of a row\-level\-access restriction entry. In the confirmation dialog that appears, click **Confirm** to delete the restriction.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Deleting row restrictions will affect users who have obtained row restriction permissions and may impact normal operation of multiple tasks like data development, so proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">For specific operations on managing data column/row restrictions, see <strong>setting database permissions</strong> and <strong>setting table permissions</strong>.</div>



<span id="8f8cc52e"></span>
## Subsequent Actions

After configuring data access permissions, you must get approval before accessing the corresponding data. For instructions on permission applications, see [Apply Permission](https://docs.byteplus.com/docs/dataleap/Apply_Permission) and [Auth Management](https://docs.byteplus.com/docs/dataleap/Auth_Management).
