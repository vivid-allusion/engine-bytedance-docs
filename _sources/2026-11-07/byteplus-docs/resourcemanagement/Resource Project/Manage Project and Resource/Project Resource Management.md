---
title: "Project Resource Management"
product: "Byteplus Resource Management"
product_code: "resourcemanagement"
source: "https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management"
---

This topic introduces how to manage resources within a project, including querying resources and transferring resources between projects.

> When you purchase or create cloud resources by using cloud service consoles or calling APIs, you can directly assign them to a specified project. You can also use the consoles and APIs to adjust the grouping of existing resources.


<span id="querying-project-resource"></span>
## **Querying project resource**


1. Log in to [Resource project > Project](https://console.byteplus.com/iam/resourcemanage/project).

2. Click the name of a project or the Manage resource button to go to the project details page.

3. You can filter resources in the list by attributes such as resource type, region, and tag.

4. If the project has a hierarchical structure, you can click Show sub\-project resources at the top of the resource list to display all resources from both the project and its sub\-projects.


<span id="transferring-resource-into-project"></span>
## **Transferring resource into project**


1. Log in to [Resource project > Project](https://console.byteplus.com/iam/resourcemanage/project).

2. Click the name of a project or the Manage resource button to go to the project details page.

3. Click Transfer in to go to the resource transfer page.

4. Select the resources to transfer. You can filter resources by project, resource type, region, tag, resource ID, or resource name. Then, click Next.

5. Confirm the transfer details and click OK.

6. On the result page, verify the transfer result. If the result is as expected, click Finish.

> Note:

> * Resources already in the current project cannot be selected for transfer\-in.

> * Resources with parent\-child relationships will be transferred together.

> * If some resources fail to transfer, you can click Retry.


<span id="transferring-resource-out-of-project"></span>
## **Transferring resource out of project**


1. Log in to [Resource project > Project](https://console.byteplus.com/iam/resourcemanage/project).

2. Click the name of a project or the Manage resource button to go to the project details page.

3. Select the resources to transfer. You can filter resources by resource type, region, tag, resource ID, or resource name.

4. Click Transfer out to go to the resource transfer page.

5. Select the target project for the transfer and click Next.

6. Confirm the transfer details and click OK.

7. On the result page, verify the transfer result. If the result is as expected, click Finish.

> Note:

> * You cannot select the current project as the target project.

> * Resources with parent\-child relationships will be transferred together.

> * If some resources fail to transfer, you can click Retry.
