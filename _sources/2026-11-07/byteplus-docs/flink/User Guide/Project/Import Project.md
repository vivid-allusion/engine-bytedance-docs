---
title: "Import Project"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Import_Project_From_BytePlus"
---

The projects in the BytePlus Flink console integrate with the projects in BytePlus.

A project is a resource management method provided by BytePlus, allowing you to group manage cloud resources used by different businesses or projects. Based on project IAM authorization, it helps maintain resource independence and data security; meanwhile, it allows viewing resource consumption bills from the project perspective, facilitating the calculation of cloud resource usage costs.

<span id="14cf57fc"></span>
## Precautions

Only the **primary account** is supported to create projects on the project console and import projects in the BytePlus Flink console. Different projects are isolated and independent from each other.

<span id="4c5bbf7c"></span>
## Step One: Create Project

The primary account needs to first create a project on the project console.


1. Main account logs into the [Project Console](https://console.byteplus.com/iam/resourcemanage/project).

2. In the left navigation bar, select **Resource Management \> Projects**, then click **Create Project**.

3. In the **Create Project** dialog, set the project name, display name, and notes, then click **OK**.

   After the project is created, the main account can import the project into the Flink console. In the project console, the main account can also move cloud resources into or out of the project; for more information, see [Proect Resource Management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/628d5541033c4d22a75ff92ba407012d~tplv-goo7wpa0wc-image.image) </span>


<span id="5c4bbf1a"></span>
## Step Two: Import Project

After the project creation, the main account can import the project to the Flink console and then create resources, develop tasks, etc., within the project.


1. Main account logs into the [BytePlus Flink Console](https://console.byteplus.com/flink).

2. Select the target region in the top menu bar.

3. In the left navigation bar of the console, select **Project Management**, then click **Import Project**.

4. In the **Import Project** dialog, enter the project name keyword to search and select the target project, then set the project leader, and click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7fbe824d91004da1b66236d490725b92~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration** |**Description** |
   |---|---|
   |Project Name |Search for projects by fuzzy querying keywords based on project name, then select the target project. |
   |Description |The project's descriptive statement, not editable. |
   |Project Manager |Select IAM users of BytePlus as the project manager for the BytePlus Flink project, who will have all permissions for the project. |
   


<span id="67f04a6d"></span>
## More Actions

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ddf51f2c46e74103a693fdd908eeca21~tplv-goo7wpa0wc-image.image) </span>

After the project is created, it appears as cards on the project management page. You may perform the following actions as needed:


* View project details: Click **Details** to view information such as the project name, project ID, and project leader.

* Change project leader: Click **Change Project Leader** to reset the project leader.

* Delete project: Click **Delete** to remove the project.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When deleting a project, there must be no resource pools in the project, and they must be cleaned up before the project can be deleted. Once project data is deleted, it cannot be recovered and is an irreversible operation. Please proceed with caution.   </div>
