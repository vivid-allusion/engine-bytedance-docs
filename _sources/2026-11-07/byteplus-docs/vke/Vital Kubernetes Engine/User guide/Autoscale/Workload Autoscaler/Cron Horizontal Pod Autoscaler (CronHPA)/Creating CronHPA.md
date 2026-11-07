---
title: "Creating CronHPA"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-CronHPA"
---

CronHPA‌ enables ‌time\-triggered autoscaling‌ by executing predefined scaling rules at scheduled intervals. It automatically ‌scales pod replicas horizontally‌ to accommodate workload fluctuations, optimizing resource utilization and cost efficiency for business operations.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

CronHPA applies only to Deployments and StatefulSets. This topic uses a Deployment as an example.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The cronhpa add\-on has been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.Y3JvbmhwYS3nu4Tku7Y=).

* A Deployment or StatefulSet has been created. For details, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment) and [Creating StatefulSets](https://docs.byteplus.com/en/docs/vke/Creating-a-StatefulSet).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Cluster**.

3. In the cluster list, click the target cluster.

4. In the left navigation bar of the cluster management page, click **Workload** \> **Deployment**.

5. Click the name of the target workload for which you want to configure a CronHPA to go to the workload details.

6. Click the **Autoscaling** tab and then click the **CronHPA** tab.

7. Click **Create CronHPA** to start configuration.

   
   |**Parameters** |**Description** |
   |---|---|
   |**Basic information** ||
   |Name |Enter a CronHPA name that complies with the displayed naming rules. The name must be unique under the same workload. |
   |Description |Provide a description for the CronHPA. The description can be related to the purposes and use cases of the CronHPA. |
   |**Policy configuration** ||
   |Repeat regularly |You can configure scheduled scaling at a specific time every hour, day, week, or month, or by using a Cron expression. For information about how to configure it by using a Cron expression, see [Cron](https://docs.byteplus.com/en/docs/vke/Cron-expressions). |
   |Execution policy |The CronHPA automatically adjusts the number of workload replicas to the specified value at the scheduled time. |
   |Add policy |Click **Add policy** to add a new policy. Ensure that multiple policies do not conflict with each other. |
   |Delete |Click **Delete** to delete a policy.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you create a CronHPA, at least one policy is required. When there is only one policy, the <strong>Delete</strong> button is disabled.</div><br> |
   

8. Click **Confirm** to finish configuration.
