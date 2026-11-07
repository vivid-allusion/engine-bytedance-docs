---
title: "Managing schema"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Managing_schema"
---

This topic introduces how to visually create, edit, and delete modes in the AI Native BaaS for Supabase to achieve full lifecycle management of modes.

<span id="C4XyJxXR"></span>
## Prerequisites

Workspace, database, and account have been created. For detailed operations, please refer to [Creating a workspace](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_a_workspace), [Creating a database](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_a_database), and [Creating an account](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_an_account).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The account you create must have the corresponding permissions for querying and modifying the corresponding database.</div>


<span id="c0BO2mZ9"></span>
## Precautions


* A deleted schema cannot be recovered. In addition, deleting a schema requires the database to process a large number of files, which may block the processing of other transactions and degrade database performance. Exercise caution when performing this operation.

* The creation, deletion, and other operations you perform may affect the online business operation. It is recommended to perform them during off\-peak hours.


<span id="5tgTpMZk"></span>
## Create schema


1. Log in to the [AI Native BaaS for Supabase](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. Go to the **SQL query** page of the target database. Click<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_906ef41b4eb1b26873ff9c3cc9ddbc6d.png)<sub> </sub></span>**SQL query** in the center navigation bar on the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name, branch name, and database name on the top left of the page in turn to select the target workspace, target branch, and target database from the drop\-down list respectively to enter the **SQL query** page of the target database.

4. On the **SQL query** page in the schema list, create schema by either of the following two methods:

   * Method one: Right\-click the target schema and select **Create schema**.

   * Method two: Click the icon <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_81d578b34d80e5c7df4d90b257017379.png)<sub> </sub></span> to the right of the target schema, select **Create schema**.

5. In the **Create schema** dialog box, configure the schema name. The rules for schema names are as follows:

   * The schema name is unique within the database.

   * The length must be between 2 and 63 characters.

   * The name must start with a letter and end with a letter or a digit.

   * It consists of letters, numbers, underscores (_), or hyphens (\-).

   * It can not start with `pg_` and can not use reserved keywords.

6. Click **OK**.


<span id="F6rKCmha"></span>
## Edit schema name


1. Log in to the [AI Native BaaS for Supabase](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. Go to the **SQL query** page of the target database. Click in the middle navigation bar of the page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_906ef41b4eb1b26873ff9c3cc9ddbc6d.png)<sub> </sub></span>**SQL query**, then click the workspace name, branch name, and database name on the upper left of the page, and the area to the right of each<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span>In the drop\-down list that appears, select the target workspace, target branch, and target database respectively to enter the **SQL query** page of the target database.

4. On the **SQL query** page's schema list, edit the schema by either of the following two methods:

   * Method 1: Right\-click the target schema and select **Edit schema**.

   * Method 2: Click the icon behind the target schema and select **Edit schema**.

4. In the **Edit schema** dialog box, modify the schema name. The rules for schema name are as follows:

   * The schema name is unique within the database.

   * The length must be between 2 and 63 characters.

   * The name must start with a letter and end with a letter or a digit.

   * It consists of letters, numbers, underscores (_), or hyphens (\-).

   * It can not start with `pg_` and can not use reserved keywords.

5. Click **OK**.


<span id="aeRaenGJ"></span>
## Delete schema


1. Log in to the [AI Native BaaS for Supabase](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. Go to the **SQL query** page of the target database. Click the middle navigation bar on the page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_906ef41b4eb1b26873ff9c3cc9ddbc6d.png)<sub> </sub></span>**SQL query**, then click the Workspace name, branch name, and the icon to the right of the database name in the top left corner of the page in sequence<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span>, select the target Workspace, target branch, and target database respectively in the pop\-up drop\-down list to enter the **SQL query** page of the target database.

4. On the **SQL query** page in the schema list, delete the schema by either of the following two methods:

   * Method one: right\-click the target mode, and select **Delete schema**.

   * Method two: click the icon after the target mode, and select **Delete schema**.

4. In the **Delete schema** dialog box, confirm the SQL statement to be executed.

5. Click **Execute**.
