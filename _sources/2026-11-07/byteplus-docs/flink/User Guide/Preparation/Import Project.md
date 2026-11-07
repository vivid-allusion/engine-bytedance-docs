---
title: "Import Project"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Import_Project"
---

The projects in the BytePlus Flink console are integrated with the projects in BytePlus.

Projects are a way of managing resources provided by BytePlus, allowing for grouped management of cloud resources used by different businesses or projects. Based on project\-level IAM authorization, it is beneficial for maintaining resource independence and data security; you can also view resource consumption bills from the project perspective, making it easier to calculate the cost of cloud resource usage.

<span id="bbf6d6f4"></span>
## Precautions

Only the **main account** can create projects in the project console and import projects in the BytePlus Flink console. Projects are isolated and independent from each other. Before preparing, it is necessary to complete service initialization and user permission authorization, you can refer to [Service Initialization](https://docs.byteplus.com/docs/flink/Service_Initialization).

<span id="54a9947c"></span>
## Step One: Create a Project

The main account must first create a project in the project console.


1. Main account login [project console](https://console.byteplus.com/iam/resourcemanage/project).

2. In the left navigation bar, select **Resource management \> Projects**, then click **Create Project**.

3. In the **Create Project** dialog box, set the project name, display name, and remarks, then click **OK**.

   After the project is created, the main account can import the project into the Flink console. In the project console, the main account can also move cloud resources in or out of the project.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e024a64ea174c328929774314b3dbd9~tplv-goo7wpa0wc-image.image) </span>

<span id="83400c27"></span>
## Step Two: Import Project

After the project creation is complete, the main account can import the project into the Flink console and then create resources, develop tasks, etc., within the project.


1. Main account login [BytePlus Flink console](https://console.byteplus.com/flink).

2. Select the target region in the top menu bar.

3. In the left navigation bar of the console, select **Project Management**, then click **Import Project**.

4. In the **Import Project** dialog, enter the project name keyword to search and select the target project, then set the project manager, and click **OK**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09a8d02d8eeb4af183efbe0e5c311589~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Description** |
|---|---|
|Project Name |Search for projects based on keywords in the project name, then select the target project. |
|Description |Descriptive statement of the project, not editable. |
|Project Manager |Select a BytePlus IAM user as the project manager for the BytePlus Flink project, who will have all permissions for the project. |
