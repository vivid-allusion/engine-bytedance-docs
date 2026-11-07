---
title: "Creating a database"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_a_database"
---

This topic describes how to create a database for a branch.

<span id="t787l4Ug"></span>
## Prerequisites


* A workspace is created and its status is **Running**.

* The target branch status is **Running**.

* An account with database creation permission is created under the target branch.


<span id="s1RTuswB"></span>
## Procedure


1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page.

5. On the **Branch overview** page's **Database** tab, click **Create database** to access the ** Create database** page.

6. On the **Create database** page, complete the following configuration and click **Create** to finish creation.

   
   |**Configuration item** |**Decscription** |
   |---|---|
   |Database name |Set the database name. The database name must follow these rules:<br><br><br>* Unique within the branch.<br><br>* Must start with a letter and end with a letter or number.<br><br>* Can only contain letters, numbers, underscores (_), and hyphens (\-).<br><br>* Must be 2 to 63 characters in length.<br><br>* Cannot use certain reserved words. For forbidden reserved words, refer to [List of reserved words](https://docs.byteplus.com/en/docs/330/Reservation_word_list). |
   |Associated account |In the drop\-down list, specify the associated account for the new database. |
   


<span id="1JmDTiho"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[CreateDatabase](https://docs.byteplus.com/en/docs/330/CreateDatabase) |Call the CreateDatabase API to create a database for a branch. |
