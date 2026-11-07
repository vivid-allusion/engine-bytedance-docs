---
title: "Managing data lake connections"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_a_connection"
---

AI Native Database Platform provides data lake capabilities for workspaces using the PostgreSQL engine, supporting data read and write operations from Object Storage TOS. This topic introduces the procedure for creating and managing data lake connections for branches.

<span id="9kGRGc1X"></span>
## Prerequisites


* A workspace is created and its status is **Running**.

* The target branch status is **Running**.

* The branch's main compute has AP acceleration enabled, or DuckDB compute has been created for the branch.


<span id="uZEwxwB1"></span>
## Procedure

<span id="NbSQcDD4"></span>
### Creating a connection


1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page.

5. On the **Branch overview** page under the **DuckDB** tab, click **Create connection** to enter the **Create connection** page.

6. On the **Create connection** page, complete the configuration below, then click **Create**.

   
   |**Configuration item** |**Required** |**Decscription** |
   |---|---|---|
   |Connection name |Yes |Set the name of the connection. Connection name must follow the rules below:<br><br><br>* Can only contain uppercase and lowercase letters, digits, and underscores (_),<br><br>* Must be 1 to 64 characters in length. |
   |Type |No |No setting required, currently only supports setting as TOS |
   |Database |Yes |Select the database for which you want to create a data lake connection. |
   |Account |Yes |Select an account to use database connections. |
   |Access Key ID |Yes |Enter the access key ID used to access the Object Storage TOS service. |
   |Secret Access Key |Yes |Enter the access key Secret used to access the Object Storage TOS service. |
   |Endpoint |No<br><br> |No need to set, the value is automatically taken based on the Region of the workspace.<br><br><br>* North China 2 (Beijing), the value for this configuration is tos\-cn\-beijing.volces.com.<br><br>* East China 2 (Shanghai), the value for this configuration is tos\-cn\-shanghai.volces.com.<br><br>* Asia Pacific Southeast (Johor), the value for this configuration is tos\-ap\-southeast\-1.volces.com. |
   |Scope |No |Specify the bucket used for the TOS service of the data lake.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If not specified, all buckets under the TOS service are used for the data lake connection.</div><br> |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">During the data lake connection creation, the <a href="https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pg_duckdb">pg_duckdb</a> plugin will be installed for the database.   </div>
   

<span id="Ey328h79"></span>
### Test connection


1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page.

5. On the **Branch overview** page under the **DuckDB** tab, you can filter connections by databases with created data lake connections in the dropdown list or search connections by connection Name.


<span id="mpeqSx6f"></span>
### Delete connection

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Database connections cannot be recovered after deletion. Proceed with caution.</div>



1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page.

5. On the **Branch overview** page, under the **DuckDB** tab, click  **...**  \> **Delete** on the target connection row.

6. On the pop\-up **Confirm delete connection?**  page, click **OK** to delete the connection


<span id="AsNmrFoi"></span>
## Related APIs


|API |Decscription |
|---|---|
|[CreateDataLakeSecretConnection](https://docs.byteplus.com/docs/aidap/CreateDataLakeSecretConnection) |Call CreateDataLakeSecretConnection API to create a data lake connection. |
|[DeleteDataLakeSecretConnection](https://docs.byteplus.com/docs/aidap/DeleteDataLakeSecretConnection) |Call DeleteDataLakeSecretConnection API to delete a data lake connection. |
|[DescribeDataLakeSecretConnection](https://docs.byteplus.com/docs/aidap/DescribeDataLakeSecretConnection) |Call the DescribeDataLakeSecretConnection API to query the data lake connection. |
|[CheckDataLakeSecretConnection](https://docs.byteplus.com/docs/aidap/CheckDataLakeSecretConnection) |Invoke CheckDataLakeSecretConnection to verify the connectivity of the data lake connection. |
|[ListDatabasesDataLakeSecretConnection](https://docs.byteplus.com/docs/aidap/ListDatabasesDataLakeSecretConnection) |Call ListDatabasesDataLakeSecretConnection API to query databases with data lake connections. |


<span id="SUbkpeyS"></span>
##
