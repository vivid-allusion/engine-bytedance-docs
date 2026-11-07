---
title: "Managing CronHPA"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Managing-CronHPAs"
---

If a Cron Horizontal Pod Autoscaler (CronHPA) has been created in a cluster, you can go to the CronHPA management page to perform related operations. This topic describes the scenarios, impacts, and procedures of CronHPA\-related operations.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">CronHPA applies only to Deployments and StatefulSets. This topic takes Deployments for example.</div>


<span id=".5pu05paw5a6a5pe25Ly457yp"></span>
## Updating CronHPA

You can modify CronHPA configurations. Once modified, the new configurations take effect. Follow the steps below to complete the configuration:


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Cluster**. On the page that appears, click the name of the target cluster to go to the management page of the cluster.

3. In the left navigation bar of the cluster management page, click **Workload** \> **Deployment** to go to the deployment configuration page.

4. Click the name of the target workload for which you want to configure a CronHPA to go to the workload details page. Click the **Autoscaling** tab and then click the **CronHPA** tab.

5. In the CronHPA list, find the CronHPA for which the configurations need to be updated, and click `... `\> **Update** in the Actions column.

6. Modify the configuration of the CronHPA based on your business requirements. For details, see [Creating CronHPA](https://docs.byteplus.com/en/docs/vke/Creating-a-CronHPA).


<span id=".5Yig6Zmk5a6a5pe25Ly457yp"></span>
## Deleting CronHPA

You can delete a CronHPA configuration. To do so, follow the steps below:


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Cluster**. On the page that appears, click the name of the target cluster to go to the management page of the cluster.

3. In the left navigation bar of the cluster management page, click **Workload** \> **Deployment** to go to the deployment configuration page.

4. Click the name of the target workload for which you want to configure a CronHPA to go to the workload details page. Then, click the **Autoscaling** tab and then click the **CronHPA** tab.

5. In the CronHPA list, find the CronHPA that you want to delete, and in the **Actions** column, click `...` \> **Delete**.

6. Click **Confirm** in the confirmation dialog box to delete the configurations.
