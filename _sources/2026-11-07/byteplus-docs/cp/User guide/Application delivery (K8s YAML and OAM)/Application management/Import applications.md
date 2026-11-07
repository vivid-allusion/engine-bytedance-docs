---
title: "Import applications"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Import_applications"
---

Bulk import of existing applications from Kubernetes clusters to make it easier to integrate users' existing cluster applications and improve application creation efficiency. This article explains how to import an application.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, only K8s YAML applications can be imported. The system uses the default K8s YAML deployment strategy, and one environment instance for each category—development (Dev), test (Test), and production (Prod)—is pre\-provisioned.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A workspace has been created. For detailed actions, please refer to [Create a workspace](https://docs.byteplus.com/en/docs/cp/Create_a_workspace).

* The Kubernetes cluster where the application to be imported is located has been connected. For detailed instructions, see [Deploy resource](https://docs.byteplus.com/en/docs/cp/Deploy_resource_management).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the application management page.

   1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

   2. In the left navigation bar, select **workspace**.

   3. Click the target workspace name to enter the current workspace.

   4. Select **Application Delivery \> Application Management** in the left navigation bar.

2. On the application management page, click **Import application**.

3. On the import application page, fill in the required basic configuration for the application.

   
   |Configuration Item |Descriptions |
   |---|---|
   |deploy resource |Select the Kubernetes cluster where the application to be imported is located. |
   |Namespace |Select the namespace where the application to be imported is located. |
   

4. Click **Add application**, and fill in the information for each application as required. You can add up to 20 applications at a time.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Resources |Select the types of resources included in the current application. Deployment, Service, and ConfigMap resource types are supported. An application can add up to 10 resources.<br><br><br>* Deployment: Select the Deployment to import. Currently, an application only supports adding one resource of the Deployment type.<br><br>* Service: Select the Service to import. Supports adding multiple items.<br><br>* ConfigMap: Select the ConfigMap to import. Multiple items can be added. |
   

5. After filling in the required information, click **OK** to import the application.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

Arrange imported applications as needed. For specific actions, see [application orchestration](https://docs.byteplus.com/en/docs/cp/Application_orchestration).
