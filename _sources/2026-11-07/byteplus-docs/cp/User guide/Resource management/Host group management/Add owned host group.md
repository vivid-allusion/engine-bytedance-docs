---
title: "Add owned host group"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Add_owned_host_group"
---

A host group is a collection of host instances. Typically, a host group corresponds to a release environment of an application or a specific task execution environment in a pipeline. This article introduces operations related to host group management.

<span id=".5re75Yqg6Ieq5Li75Li75py6"></span>
## Add independent host

You can manage a group of third party hosts outside BytePlus ECS in Code Pipeline.


1. Log in to the [Code Pipeline Console ](https://console.byteplus.com/cp).

2. In the left navigation bar, select **Resource management**.

3. On the **Resource management** page, switch to the **host group** tab.

4. On the **host group** tab, click **Add host group**.

5. On the Add host group page, fill in the parameters as required.

   
   |Parameter |Description |
   |---|---|
   |Host group name |Customize the display name of the host group. |
   |Host group identifier |Fill in the host group identifier according to the interface prompts. The host group identifier is the unique identifier of the host group and cannot be changed after creation. |
   |Type |Choose **custom host**. |
   |Hosts |Enter the IP address and login information required to connect to Hosts. |
   |Sharing scope |Host groups support controlling the visible Shared Workspace.<br><br><br>* **Specify workspace**: The host group is only visible to the specified workspace. Only pipelines in the specified workspace can use this host group.<br><br>* **All workspaces**: The host group is visible to all workspaces. Pipelines in all workspaces can use this host group. There is a risk of granting overly broad permissions; please use this solution with caution. |
   

6. Click **Confirm** to finish adding the host group.


<span id=".5p-l55yL5Li75py657uE5LiL6LWE5rqQ"></span>
## View resources in the host group

You can view basic information such as the host group's name, identifier, source, creator, and creation time. You can view the host instances included in the host group, and perform create, read, update, and delete operations on host instances within the host group.


1. On the **host group** tab, you can view all added host group resources.

2. Click the target host group name to view the host instances included in the target host group.

   
   |Feature |Description |
   |---|---|
   |Modify authentication information |Click **Modify authentication information** to reset the host login credentials. |
   |Delete host |Click **Delete** to delete the target host instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Host instances associated with managed applications cannot be deleted.</div><br> |
   


<span id=".57yW6L6R5Li75py657uE"></span>
## Edit host group

You can modify the host group name and Shared Workspace.


1. On the **host group** tab, select the target host group and click the **Actions** column's **Edit.** 

2. On the Edit host group page, modify the ConfigMap as needed.

3. After modification, click **Confirm**.


<span id=".5Yig6Zmk5Li75py657uE"></span>
## Delete host group

You can delete host group resources that are no longer used.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Host groups associated with managed applications cannot be deleted.</div>



1. On the **host group** tab, select the target host group and click the **Actions** column's **Delete.** 

2. In the pop\-up confirmation box, confirm the host group information again, then click **Delete** after confirmation.
