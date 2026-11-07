---
title: "Integrate VKE cluster"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Integrate_VKE_cluster"
---

Code Pipeline supports connecting to  [VKE](https://docs.byteplus.com/en/docs/vke/What-is-Vital-Kubernetes-Engine), enabling you to deploy applications to VKE clusters through pipelines or application delivery. Before deployment, you must first integrate the VKE cluster to be deployed. This article describes how to integrate a VKE cluster.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* VKE has been activated.

* The VKE cluster has been created. For specific operations, refer to [Create cluster ](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* For first\-time integration, cross\-service authorization must be completed. For specific operations, refer to [Cross-service authorization](https://docs.byteplus.com/en/docs/cp/Cross-service_authorization).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Code Pipeline Console ](https://console.byteplus.com/cp).

2. In the left navigation bar, click **Resource management \> ** **Deploy resources ** .

3. Click **Create deployment resource**.

4. In the **Create deployment resource** dialog box, configure the deployment resource information as required.

   
   |Parameter |Description |
   |---|---|
   |Deployment resource name |Customize the name of the resource to be deployed. The name must not be duplicated under the same account. |
   |Description |Optional. Enter description information such as the purpose of this deployment resource. |
   |Connection type |Select **VKE**. |
   |Authorized account |Displays the account name that has obtained cross\-service authorization. |
   |Region |Select the region where the Vital Kubernetes Engine VKE cluster is located.<br><br>For currently supported regions, please refer to [VKE server-launching region](https://docs.byteplus.com/en/docs/vke/Regions-and-Availability-Zones). |
   |Deploy cluster |You can select a Vital Kubernetes Engine cluster accessible to the current account from the drop\-down list. Only VKE clusters with the status Running, Changing, or Upgrading are displayed. |
   |Shared Workspace |Deployment resources support controlling the visible workspace scope.<br><br><br>* Specify workspace (recommended): The deployment resource is only visible to the specified workspace. Only pipelines and application delivery modules under the specified workspace can use and release this deployment resource.<br><br>* All workspaces: The deployment resource is visible to all workspaces. Pipelines and application delivery modules under all workspaces can use and release this deployment resource.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Selecting all workspaces for the sharing scope poses a risk of excessive permissions. Please use this solution with caution.</div><br> |
   

6. Click **Confirm** to successfully create the deployment resource.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next


* Use the Kubernetes deployment capability in the pipeline to deploy to the VKE cluster.

* Release the application to the target environment (the bound and integrated VKE cluster) through application delivery.

* Manage deployment resources.
