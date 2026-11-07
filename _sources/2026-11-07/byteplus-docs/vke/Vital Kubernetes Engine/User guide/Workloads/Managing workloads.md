---
title: "Managing workloads"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Managing-Deployments"
---

Vital Kubernetes Engine (VKE) enables you to perform operations on created workloads based on your business requirements, such as updating and deleting workloads.

<span id="i8KA0vtf"></span>
## Prerequisites

A workload has been created. For detailed procedures, see [Creating workloads](https://docs.byteplus.com/en/docs/vke/Deployments).

<span id="gIohWWEC"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar of the cluster management page, click **Workload** and select the target workload type.

5. In the **Actions** column of the target workload, click the `...` icon and then click an option to perform the corresponding operation on the workload.

   
   |Action |Description |
   |---|---|
   |Update |Update the configurations of the workload in the console. For detailed configuration instructions, see the **Creating through the console** section in the [Creating workloads](https://docs.byteplus.com/en/docs/vke/Deployments) topic.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You cannot update the <strong>name</strong> and <strong>namespace</strong> of the workload.</div><br> |
   |Clone |You can perform this operation only on **Deployments**.<br><br>You can clone Deployments. By cloning a Deployment, you can easily provision multiple Deployments with similar configurations to meet different business requirements. On the **Clone Deployment** page, set the name, confirm the remaining configuration items, and click Confirm to clone the Deployment. To modify configurations, see [Workload configurations](https://docs.byteplus.com/en/docs/vke/Workload_configurations). |
   |Edit Yaml |Edit the YAML file to update the configuration information. For detailed configuration instructions, see the **Creating via kubectl command line** section in the [Creating workloads](https://docs.byteplus.com/en/docs/vke/Deployments) topic.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You cannot update the <strong>name</strong> and <strong>namespace</strong> of the workload. This means that you cannot update <code>metadata.name</code> and <code>metadata.namespace</code>.</div><br> |
   |Update number of instances |You can perform this operation only on **Deployments** and **StatefulSets**.<br><br>In the **Update number of instances** dialog box, enter the desired **number of instances** to update the quantity of pod instances in the workload. |
   |Redeploy |You can perform this operation only on **Deployments** and **StatefulSets**.<br><br>After you redeploy a deployment, all pods within the deployment will restart. We recommend that you perform this operation during off\-peak hours.<br><br>In addition to redeploying a single Deployment, you can also redeploy multiple Deployments at the same time in VKE. In the Deployment list, select the check boxes before the names of the target Deployments, and click **Redeploy** below the list. In the message that appears, confirm the workload information and click **Batch deployment** to redeploy multiple Deployments at the same time. |
   |Update parallel number |You can perform this operation only on **Jobs** and **CronJobs**.<br><br>In the running policy, use the **Number of successful runs** parameter to define how many times pods must run successfully for the Job. To run pods multiple times, use the **Parallel number** parameter to adjust the maximum number of concurrent pods and control the Job's progress. You can also update this limit on the console. |
   |Update image |You can perform this operation only on **Deployments**, **StatefulSets**, **DaemonSets**, and **CronJobs**.<br><br>You can quickly update the image and image tag used by a container in the workload in the console. |
   |Suspend |You can perform this operation only on **CronJobs**.<br><br>You can pause a CronJob to release some system resources and move it to the backend. When the CronJob is required, you can resume the CronJob from its last suspension point.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You cannot suspend executed Jobs. Jobs that are suspended during the scheduling period will be counted as missed Jobs. When a missed Job resumesby the execution deadline, it will be immediately executed.</div><br> |
   |Manually trigger |You can perform this operation only on **CronJobs**.<br><br>When you manually trigger a CronJob, the system will quickly create a Job with the same configuration and immediately execute the Job. This is primarily used to verify the accuracy of the CronJob configuration. |
   |View monitoring |After you enable the cloud native observability capability, you can view monitoring information about workload resources, including network traffic, disk I/O and replicas, CPU, and memory in **Monitoring Center**. To enable the cloud native observability capability, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability). |
   |Export |You can perform this operation only on **Deployments** and **StatefulSets**.<br><br>Export the YAML configuration file of the current workload. |
   |Delete |You can delete workloads that you no longer use based on your business requirements.<br><br>In addition to deleting a single workload, you can also delete multiple workloads at the same time in VKE. In the workload list, select the check boxes before the names of the target workloads, and click **Delete** below the list. In the message that appears, confirm the workload information and click **Delete** to delete multiple workloads at the same time.<br><br><div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div><br><br><br><div data-tips="true" data-tips-type="danger">After you delete a workload, the associated service may become unavailable. Proceed with caution.</div><br> |
