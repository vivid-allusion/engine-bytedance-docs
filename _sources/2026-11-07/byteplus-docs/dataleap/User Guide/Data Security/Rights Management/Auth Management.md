---
title: "Auth Management"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Auth_Management"
---

In this module, you can view the current authorization status of the resources you manage from the perspective of resources or grantees and perform related authorization operations.

<span id="_1-按资源查看"></span>
## **Constraints**


* Only access rights already opened for the resource can be authorized. For instructions on resource permission settings, refer to [Set Application Permissions](https://docs.byteplus.com/docs/dataleap/Set_Application_Permissions).

* Resource permissions for packages can only be granted to individuals.

* Batch operations support only the same type of data, as detailed below:

   * Batch authorization of the same type of resources for the same engine. For example, you can batch authorize multiple LAS table resources, but cannot batch authorize LAS table and row resources together.

   * Batch modify validity period and revoke permissions for the same grantee type.


<span id="029b3b97"></span>
## Prerequisites

Supported datasources have completed corresponding metadata ingestion; see [Metadata Ingestion](https://docs.byteplus.com/docs/dataleap/Metadata_Ingestion) for related instructions.

<span id="bdc6c05b"></span>
## View by Resource

From the resource perspective, view all authorizations of the resources you manage and perform management operations accordingly.


* Search resources

   Search for databases, tables, rows, and columns that match the criteria by setting resource type, resource level, and resource keywords. When multiple search criteria are set, the intersection of all conditions will be used for the query.

* View authorization details of databases, tables, rows, and columns.

* Grant authorization for resources proactively.

* Revoke or modify the validity period of permissions for authorized users.


<span id="_1-1-查看授权详情"></span>
### View Authorization Details


1. Log in to the DataLeap console.

2. Select **Overview \> Security \> Authorization Management \> Auth Management** to enter the resource\-based view page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73f94b0202c34ffc86761a155877c2b3~tplv-goo7wpa0wc-image.image) </span>

3. Click the **View Details** button in the **Action** column of a resource in the list to enter the authorization details page for that resource.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9dce1403049a40c9937cf92cf18d805f~tplv-goo7wpa0wc-image.image) </span>

4. Execute the following actions:

   * View auth details

      Set search information to view a list of resource authorization information that matches the criteria. When multiple search criteria are set, the intersection of all conditions will be queried.

   * View grantee access details

      Click the **Detail** button in the **Action** column of an authorization record to jump to the **View by Grantee** page, where you can view and manage all resource permissions the grantee has under this database.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">This operation is supported only for DB resources.      </div>
      

   * Download auth details

      Click the **Download auth details** button, select the required subordinate resources in the pop\-up window, then click **OK** to complete the download.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have DB resource permissions, you can view table, row, column, and package resource permissions in the DB authorization details; if you have table resource permissions, you can view DB, table, row, and column resource permissions in the table authorization details.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The download auth details function is only for permission convergence and inspection management.   </div>
   


<span id="_1-2-添加获权方"></span>
### Add Grantee


1. Log in to the DataLeap console.

2. Select **Overview \> Security \> Authorization Management \> Auth Management** to enter the resource view page.

3. Click the **View details** button in the **Action** column of an entry in the resource list to access the authorization details page of that resource.

4. Click the **Grant Access to** button to open the **Grant Access to** window.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a61036feae74a07961b48059c1c6a44~tplv-goo7wpa0wc-image.image) </span>

5. After setting the authorization information, click the **Add** button to add a new grantee.

   The information filled in during authorization is similar to that during permission application. See [Apply Permission](https://docs.byteplus.com/docs/dataleap/Apply_Permission) related parameters for details.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Authorization should follow the principle of minimizing data range and personnel scope to avoid unnecessary authorization and overly long validity periods.</div>


* <div data-tips="true" data-tips-type="tip">The main account has all data access rights by default and requires no authorization.</div>



<span id="_1-3-回收权限"></span>
### Modify Validity Period


1. Log in to the DataLeap console.

2. Select **Overview \> Security \> Authorization Management \> Auth Management** to enter the resource view page.

3. Click the **View details** button in the **Action** column of an entry in the resource list to access the authorization details page of that resource.

4. The following operations are available:

   * Modify the validity period of a single resource

      1. Click the **Edit Valid Days** button in the **Action** column of a permission entry in the list to open the **Edit Valid Days** window.

      2. Select the new expiration date and enter the reason for modification, then click the **OK** button to complete the modification.

   * Batch modify validity periods

      1. Click the filter icon of **Grantee Type**, select Individual or User Group, then click the **OK** button. The list will display authorization information with the same permission source.

      2. After selecting one or more options, click the **Batch Edit Valid Days** button to open the **Edit Valid Days** window.

      3. After setting the modification information, click the **OK** button to finish the modification.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If the grantee of a resource is the DB admin or table owner of that resource, they have all permissions on that resource by default, and its validity period cannot be modified.</div>


* <div data-tips="true" data-tips-type="tip">Higher\-level permissions cannot have their validity periods modified on the authorization details page of lower\-level permissions. For example, if you have certain DB permissions, you cannot modify the validity period of those permissions on the related data table authorization details page; you must modify it on the DB authorization details page.</div>


* <div data-tips="true" data-tips-type="tip">After the validity period is modified, the grantee will receive the related notification.</div>


* <div data-tips="true" data-tips-type="tip">The expiration date cannot be modified to the current day of the action.</div>



<span id="07389027"></span>
### Reclaim Permissions


1. Log in to the DataLeap console.

2. Select **Overview \> Security \> Authorization management \> Auth Management** to enter the resource view page.

3. Click the **View details** button in the **Action** column of an entry in the resource list to open the authorization details page for that resource.

4. The following operations are available:

   * Revoke permission for a single resource

      1. Click the **Revoke** button in the **Action** column of a permission entry in the list to open the **Revoke Permission** window.

      2. After setting the revocation details, click the **OK** button to open the confirmation dialog.

      3. Click the **Confirm** button to complete the revocation.

   * Batch revoke permissions

      1. Click the filter icon next to **Grantee Type**, select individual or user group, and then click the **Confirm** button. The list will show authorization information from the same permission source.

      2. After selecting one or more options, click the **Batch revoke** button to open the **Batch Revoke Permission** window.

      3. After setting the revocation details, click the **OK** button to open the confirmation dialog.

      4. Click the **OK** button to complete the reclamation.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">If the grantee of a resource is the resource's librarian or table owner, they by default have all permissions on that resource, and their permissions cannot be revoked.</div>


* <div data-tips="true" data-tips-type="warning">If a permission is associated with tasks, revoking it may cause some tasks (such as data development tasks) to fail to run. Please carefully check before revocation.</div>


* <div data-tips="true" data-tips-type="warning">Higher\-level permissions cannot be revoked on the authorization details page of lower\-level permissions. For example, if you have permission for a database, you cannot revoke it on that database’s data table authorization details page. You need to go to the database authorization details page to revoke it.</div>



<span id="_2-按获权方查看"></span>
## **View by Grantee**

From the grantee's perspective, query the permissions of a certain grantee in the resources you manage and reclaim them.


1. Log in to the DataLeap console.

2. Select **Overview \> Security \> Authorization management \> Auth Management \> View by grantee** to enter the view by grantee page.

3. After selecting an individual or user group, choose a grantee from the corresponding dropdown list.

4. Click the **Query** button, and then select **Datasource** to display the corresponding datasource type of resource permission information owned by the grantee.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/881713b417fb456d9715488e6df56612~tplv-goo7wpa0wc-image.image) </span>

5. You can perform the following actions:

   * Search resources

      Search for libraries, tables, rows, or columns that match the conditions by setting resource type, datasource type, resource keywords, and other search criteria. When setting multiple search criteria, the intersection of each condition will be used for the query.

   * Revoke permissions already obtained by a single grantee

      1. Click the **Revoke** button in the **Action** column of a permission item in the list to open the **Revoke Permission** window.

      2. After providing the reason for revocation, click the **OK** button to open the confirmation dialog for revocation.

      3. Click the **OK** button to complete the revocation.

   * Modify the validity period of the permissions obtained by the grantee

      1. Click the **Edit Valid Days** button in the **Action** column of a permission item in the list to open the **Edit Valid Days** window.

      2. Select a new expiration date and provide the reason for modification, then click the **OK** button to complete the update.

   * Batch revoke permissions or modify validity periods

      1. After selecting one or more options, click the **Batch revoke** or **Batch Edit Valid Days** button to open the corresponding window.

      2. After filling in the reason and other information, click the **OK** button. After a second confirmation, the batch operation is complete.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If a permission is associated with tasks, revoking it may cause some tasks (such as data development tasks) to fail to run. Please carefully check before revocation.</div>


* <div data-tips="true" data-tips-type="tip">After the validity period is modified, the grantee will receive a related notification.</div>


* <div data-tips="true" data-tips-type="tip">The expiration date cannot be modified to the current day of the action.</div>
