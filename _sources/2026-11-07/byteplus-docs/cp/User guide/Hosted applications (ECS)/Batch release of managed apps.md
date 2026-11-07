---
title: "Batch release of managed apps"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Release_managed_applications_in_batches"
---

In distributed scenarios, it is necessary to deploy the same app to different hosts. Continuous Delivery supports the batch deployment feature. After the app is successfully deployed to a subset of cloud services, it is then deployed to the other cloud services, reducing the maintenance cost of deployment failures. This document describes how to deploy apps in batches.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations

Only **Managed Apps** support batch release. **K8s YAML Apps** are not supported for this feature.

<span id=".5L2_55So5Zy65pmv"></span>
## Application scenarios

Suppose you need to deploy the same app to 3 different hosts. Using the batch release policy, you can deploy the app to 1 cloud server in the first batch. After the first batch of apps is deployed successfully, manually trigger the start of the next batch in the console to deploy the app to the 2 cloud servers in the second batch.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The JAR/WAR package for the app has been prepared.

* The ECS instances to be deployed (**2 or more**) have been connected. For specific operations, see [Add ECS host group](https://docs.byteplus.com/en/docs/cp/Add_ECS_host_group#.5re75YqgLWVjcy3kuLvmnLrnu4Q=).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the app management page.

   1. Log in to the [Continuous Delivery console](https://console.byteplus.com/cp).

   2. In the left navigation bar, select **Workspace**.

   3. Click the target workspace name to enter the current workspace.

   4. In the left navigation bar, select **App Delivery \> App Management**.

2. On the app management page, click **Create App**.

3. On the create app page, select **Managed App**, and fill in the required configuration information for the app as prompted. This section focuses on how to fill in the parameters related to batch release. For other parameter descriptions, see [Create and Deploy Managed Apps (Java technology stack)](https://docs.byteplus.com/en/docs/cp/Create_and_deploy_managed_applications_ECS?lang=en).

   1. In **App Information**, after filling in the information, click **Next: Environment Configuration**.

      
      |Parameter |Description |
      |---|---|
      |App deployment type |Select **Hosts**. |
      |App technology stack |Select **Java**. |
      

   2. In **Deployment Configuration**, after filling in the information, click **Next: Advanced Settings**.

      
      |Parameter |Description |
      |---|---|
      |Package Update Strategy |Option **Batch release**. |
      |Batch quantity |Total release batches. In this scene, set **batch count** to **2**, **Batch 1** to **1**, and **Batch 2** to **2**. |
      |Suspend policy |Determine whether to suspend before each batch release. In this scene, select **Suspend each batch**. After the previous batch is successfully deployed, manually trigger the start of the next batch deployment in the Console. |
      

   5. Click **Confirm** to start deploying the app. You can view the deployment progress of the app on the environment tab.


<span id=".5pON5L2c57uT5p6c"></span>
## Subsequent operations

**Deploy subsequent batches**

Click **Continue** in the **environment \> change log \> details** section of the App Details page to trigger the start of subsequent batches.
