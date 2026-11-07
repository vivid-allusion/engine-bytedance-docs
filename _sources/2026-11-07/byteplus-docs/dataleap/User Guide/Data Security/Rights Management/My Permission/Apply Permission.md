---
title: "Apply Permission"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Apply_Permission"
---

If you need to use data resources developed by others, you must apply for permission to access those resources. This article explains how to apply for resource permissions.

<span id="256a2292"></span>
## Prerequisites


* Supported data sources have completed corresponding metadata ingestion; see [Metadata Ingestion](https://docs.byteplus.com/docs/dataleap/Metadata_Ingestion) operating instructions for details.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After ByteHouse CE metadata ingestion, existing data synchronizes to <strong>Data Security</strong> on T+1 day, while incremental data syncs in real time.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After LAS Catalog metadata ingestion, it takes T+1 day to synchronize to <strong>Data Security</strong>.   </div>
   

* The requested resource has open access permissions. For resource permission settings, see [Set Application Permissions](https://docs.byteplus.com/docs/dataleap/Set_Application_Permissions) operating instructions.


<span id="_2-申请权限"></span>
## **Operation Steps**


1. Log in to the DataLeap console.

2. Select **Overview \> Security \> Authorization Management \> My Authorizations** to enter the **My Authorizations** page.

3. Click the **Apply** button to enter the **Apply** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59e1e8251a994ab4af48c70bdbdd60b1~tplv-goo7wpa0wc-image.image) </span>

4. After setting the application information below, click the **Submit** button to enter the preview page, confirm the information, then click the **Submit** button to complete the permission application.

   1. Select the grantee.

   2. Select the resources to apply for.

      Click the **Add Request Resources** button. In the pop\-up window, select the resources and click the **Confirm** button to add them to the resource list. Then you can perform the following actions:

      * Click a request resource name to view its details.

      * Click the **Edit** icon in the **Action** column to adjust the permission type and validity period for the request.

      * Click the **Preview Approval Flow** icon in the **Action** column to preview the approval flow for the resource.

      * Click the **Delete** icon in the **Action** column. After confirmation, you can remove the requested resource.

      * Select one or more entries to batch delete resources or modify their validity periods.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Permission owners can restrict applications for entire databases, tables, sensitive columns, row\-level access, or resource packages. If the resource is not open for application, the system will prompt “Application permission not yet open” with the reason and the permission owner.      </div>
      

   3. Enter the reason for the application.

      The parameters related to permission applications are explained in the table below. Parameters marked with \* are required; those without \* are optional.

   
   |Parameters |Description |
   |---|---|
   |**Select grantee** ||
   |\*Grantee Type |There are two grantee application options: **Individual** and **User Group**, with **Individual** selected by default. |
   |\*Grantee |The individual or user group granted resource permissions.<br><br><br>* When **Grantee Type** is set to **Individual**, the current logged\-in account is the default grantee. You can enter tenant account keywords to select other accounts from the dropdown for application, supporting multiple selections.<br><br>* When **Grantee Type** is set to **User Group**, you can select from the dropdown of already created user groups.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The tenant primary account automatically has all data access rights and does not require application.</div><br> |
   |**Request Resources** ||
   |\*Datasource |Datasource types supported include ByteHouse CE, ByteHouse CDW, and LAS Catalog. |
   |\*Content |Resource applications include three options: database, table, and package.<br><br><br>* Database: apply for database permissions by selecting cluster and database.<br><br>* Table: apply for table permissions by selecting cluster, database, and table in order.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The LAS Catalog options refer to the data directories on the engine side. LAS Catalog data directories support three types: <strong>Hive</strong>, <strong>Iceberg</strong>, and <strong>Lance</strong>. Currently, DataLeap supports selecting only <strong>Hive</strong> and <strong>Iceberg</strong> types.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Database permissions and table permissions are independent and do not affect each other. For example, having database permission alone does not grant access rights to the tables within that database.</div><br> |
   |\*Level |The scope of permission application is displayed after selecting a table from the dropdown. Supports **Table** or **Row\-level**.<br><br><br>* Table: apply for full table permission, including row\-level restrictions.<br><br>* Row\-level: apply only for row\-level restricted permissions when row restrictions exist.<br><br>   * Row\-level restriction: after choosing **Row\-level**, set the row restriction information for the permission application. The dropdown supports selecting multiple enumerated values.<br><br>* Column\-level application: select the required **columns** (including sensitive and regular columns) to apply for column permissions separately. After selecting **column\-level application**, choose the application items from the displayed **column** dropdown.<br><br>* Column: when the table contains **sensitive columns**, column permissions must be applied separately. Select the application items from the displayed **column** dropdown.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When <strong>application content</strong> selects <strong>table</strong>, this parameter must be set.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only <strong>ByteHouse CDW</strong> and <strong>ByteHouse CE</strong> data sources support <strong>column\-level application</strong> for access rights to all columns; other data sources only require applying for access rights to <strong>sensitive columns</strong>.</div><br> |
   |Access type |Access permissions granted to the grantee include three options: read\-write, read\-only, and create table.<br><br><br>* Read\-write: allows all operations on the resource, such as Insert and Select.<br><br>* Read Only: allows only read operations on the resource, such as Select.<br><br>* Create Table: allows creating tables under the database with this permission. By default, you have read\-write permission to create new tables, but cannot access other tables in the database without permission.<br><br><br>The permission types available differ across resource levels, as detailed below:<br><br><br>* Database: supports read\-write, read\-only, create table.<br><br>* Table: supports read\-write, read\-only.<br><br>* Row\-level restrictions/sensitive columns: support read\-only. |
   |Validity Period |The validity period for resource permissions can be selected from the dropdown or entered manually. The validity period depends on the request type as follows:<br><br><br>* Troubleshooting support is valid for 1 to 30 days.<br><br>* Index calculation support is valid for 1 to 180 days.<br><br>* Other request types support validity from 1 day to permanent. |
   |**Reason for Application** ||
   |\*Request Type |The reason category for applying resource permissions includes options such as troubleshooting, index calculation, and data mining analysis, selectable from the dropdown list. |
   |\*Description |Detailed explanation for applying resource permissions.<br><br>Different request types provide corresponding fill\-in templates. |
   |\*Application Q&A |Custom questions to answer when applying for resource permissions.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter appears only when applying for permission after setting a custom problem for the resource. Refer to <a href="https://docs.byteplus.com/docs/dataleap/Set_Application_Permissions">Set Application Permissions</a> for instructions on setting custom problems.</div><br> |
   


<span id="c85ca709"></span>
## Operation Result


* After applying for permission, you can use the My Applications feature to view all your submitted tickets, including application details and status. You can also withdraw or expedite your tickets. For related operating instructions, refer to [Manage My Applications](https://docs.byteplus.com/docs/dataleap/Manage_My_Applications).

* After applying for permission, the system sends an email with a link to the approver, allowing quick access to the approval page for efficient processing.
