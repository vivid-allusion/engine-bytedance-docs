---
title: "Integrate custom clusters"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Integrate_custom_clusters"
---

Supports deploying applications to third\-party Kubernetes clusters or self\-hosted Kubernetes clusters via pipeline or application delivery. Before deployment, you need to connect the custom cluster that will be deployed. This article explains how to integrate custom clusters.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The Kubeconfig file for the custom cluster has been obtained.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

2. In the left navigation bar, select **Resource management**.

3. On the Resource management page, switch to the **deploy resource** tab.

4. On the **Deploy Resource** tab, click **Create Deploy Resource**.

5. In the **Create deploy resource** dialog box, configure the deploy resource information as required.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Deploy resource name |Customize the name of the resource to be deployed. The name must be unique under the same account. |
   |Description |Optional. Enter a description for this deploy resource, such as its purpose. |
   |Connection Type |Select **Custom**. |
   |The Kubeconfig file |Kubeconfig serves as the credential for accessing a cluster. Please paste the Kubeconfig of the cluster you want to connect into this field. |
   |Sharing scope |Deploy resources support controlling which workspaces are visible.<br><br><br>* Specify workspace: Deployed resources are only visible to the specified workspace. Only the pipelines and application delivery modules within the specified workspace are permitted to use this deploy resource and perform publishing.<br><br>* All workspaces: Deployed resources are visible to all workspaces. All pipelines and application delivery modules under all workspaces can use this deploy resource for publishing. This poses a risk of excessive permissions. Please use this solution with caution. |
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the pipeline uses the public resource pool, you must ensure that the Server address of the custom cluster being connected is accessible via the Internet.   </div>
   

6. Click **OK**. The deployment resource was created successfully.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next


* Use the Kubernetes deployment feature in the pipeline to deploy to the custom cluster.

* Through application delivery, release the application to the target environment (a custom cluster that has already been associated and connected).

* Manage deployment resources.
