---
title: "Add ECS host group"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Add_ECS_host_group"
---

A host group is a collection of host instances. Typically, a host group corresponds to a release environment of an application or a specific execution environment for a job in a pipeline. This article describes operations related to host group management.

<span id=".5re75YqgLWVjcy3kuLvmnLrnu4Q="></span>
## Add ECS host group

You can import a group of ECS instances into a host group in Code Pipeline for management.


1. Log in to the [Code Pipeline Console ](https://console.byteplus.com/cp).

2. In the left navigation bar, select **Resource management**.

3. On the **Resource management** page, switch to the **Host group** tab.

4. On the **Host group** tab, click **Add host group**.

5. On the Add host group page, fill in the parameters as required.

   
   |Parameter |Description |
   |---|---|
   |Host group name |Customize the display name of the host group. |
   |Host group identifier |Fill in the host group identifier as prompted by the interface. The host group identifier is the unique identifier of the host group and cannot be changed after creation. |
   |Type |Type of host group to be added; currently, only **ECS (Elastic Compute Service)**  is supported. |
   |Region |Select the region to which the current host group belongs. |
   |VPC |All ECS instances in a host group must be within the same VPC. |
   |Hosts |Select the ECS instances to add to the current host group from the host list. Multiple ECS instances can be added.<br><br><br>* Only ECS instances running Linux are supported.<br><br>* ECS instances must have the batch job agent installed in advance; otherwise, they cannot be added to the host group. For specific operations, refer to [Install batch job agent](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client).<br><br>* If the ECS instance state is **Abnormal**, click the status label to navigate to the cloud server console and confirm whether the agent is installed. |
   |Shared Workspace |The host group supports controlling the visible workspace scope.<br><br><br>* **Specify workspace**: The host group is only visible to the specified workspace. Only pipelines under the specified workspace can use this host group.<br><br>* **All workspaces**: The host group is visible to all workspaces. Pipelines under all workspaces can use this host group. There is a risk of excessive permissions; please use this solution with caution. |
   

6. Click **Confirm** to complete adding the host group.


<span id=".5p-l55yL5Li75py657uE5LiL6LWE5rqQ"></span>
## View resources in the host group

You can view basic information such as the host group's name, identifier, source, creator, and creation time. You can view the host instances included in the host group, and perform create, read, update, and delete operations on host instances within the host group.


1. On the **Host group** tab, you can view all added host group resources.

2. Click the target host group name to view the host instances included in the target host group.

   
   |Feature |Description |
   |---|---|
   |Add host |Click **Add host** to add a new host instance to the current host group. |
   |Delete host |Click **Delete** to delete the target host instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Host instances associated with managed applications cannot be deleted.</div><br> |
   


<span id=".57yW6L6R5Li75py657uE"></span>
## Edit host group

You can modify the host group name and sharing scope.


1. On the **Host group** tab, select the target host group and click the **Actions** column's **Edit** button.

2. On the Edit host group page, modify the configuration items as needed.

3. After modification, click **Confirm**.


<span id=".5Yig6Zmk5Li75py657uE"></span>
## Delete host group

You can delete host group resources that are no longer in use.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Host groups associated with managed applications cannot be deleted.</div>



1. On the **Host group** tab, select the target host group and click the **Actions** column's **Delete** button.

2. In the pop\-up confirmation box, confirm the host group information again, then click **Delete**.
