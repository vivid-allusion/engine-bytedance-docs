---
title: "Creating IHPA"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Create_an_Intelligent_Horizontal_Pod_Autoscaler"
---

Intelligent Horizontal Pod Autoscaler (IHPA) predicts scaling targets based on data, provides fine\-grained management on the number of workload replicas, and reduces the impact of native HPA scaling delay on business operations.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features">Beta·Apply for Trial</a>]: This feature is currently at the beta stage. Submit an application if you need to use it.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A cluster has been created, and the cluster version meets the following requirements:

   * Clusters of v1.24 need to be upgraded to v1.24.15\-vke.13 or later.

   * Clusters of v1.26 need to be upgraded to v1.26.10\-vke.13 or later.

   * Clusters of v1.28 need to be upgraded to v1.28.3\-vke.15 or later.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the version of your cluster does not meet the requirements, you can upgrade the cluster. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster">Upgrading clusters</a>.   </div>
   

* Cloud native observability has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5a6J6KOF57uE5Lu2"></span>
### Step 1: Install an add\-on

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the katalyst add\-on is installed in your cluster, you need to upgrade the add\-on to v0.5.6\-vke.6 or later. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading add\-ons</a>.</div>



1. Log in to [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Cluster**.

3. On the cluster list page, click the cluster you want to configure.

4. On the cluster management page, select **Addons** in the left navigation bar.

5. Click the **Scheduling** tab. Move the pointer over the katalyst add\-on card and then click **Deploy**.

6. Select **IHPA**.

7. Click **Confirm** to install the add\-on.


<span id=".5q2l6aqk5LqM77ya5Yib5bu65by55oCn5Ly457yp562W55Wl"></span>
### Step 2: Create a scaling policy


1. In the left navigation bar on the cluster management page, click **Autoscaling** \> **IHPA**. On the page that appears, click **Create IHPA** to create a scaling rule in the console.

   * **Basic information**

      
      |Parameter |Description |
      |---|---|
      |Name |Specify the name of the IHPA, which must be unique within the cluster. |
      |Prediction model |Configure the prediction mode of the IHPA. Valid values:<br><br><br>* **Preview**: only previews workload scaling based on the configured IHPA policy. The number of workload replicas is not increased or decreased.<br><br>* **Automatic**: Workload autoscaling can be performed based on the configured IHPA policy. |
      |Namespace |Select the namespace to which the scaling policy belongs. We recommend that you select a custom namespace or the system default namespace named **default**. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
      |Label |It corresponds to the label in Kubernetes and is used to identify the scaling policy. Click **Add new** and then enter a **key**\-**value** pair that complies with the on\-screen requirements. |
      |Annotation |It corresponds to the annotation in Kubernetes, which is used to attach non\-identifying metadata to the scaling policy for efficient metadata retrieval. Annotations can contain characters that are not permitted in **labels**. Click **Add annotation** and then enter a **key**\-**value** pair that complies with the on\-screen requirements. |
      

   * **Scaling policy**

      
      |Parameters |Description |
      |---|---|
      |Scalable object |Specify a workload to be scaled. Select the type of workload and the specific workload from the drop\-down lists. For workload types, you can select **Deployment** or **StatefulSet**. |
      |Monitoring metrics |Click **Add monitoring metrics** to configure the metrics for workload autoscaling. The system determines whether scaling is required based on the metrics. The following metrics are available:<br><br><br>* **CPU usage**: Specify the CPU utilization as a metric, which is the proportion of `the total CPU usage of all pod instances` to `the total CPU requests of all pod instances`. When CPU utilization reaches this value, scaling is triggered.<br><br>* **Memory usage**: Specify the memory utilization as a metric, which is the proportion of the `total memory usage of all pod instances` to the `total memory requests of all pod instances`. When memory utilization reaches this value, scaling is triggered. |
      |Minimum number of instances |Specify the minimum number of instances during scaling. When the policy is triggered, workload instances will scale within the configured minimum and maximum instance limits. |
      |Maximum number of instances |Specify the maximum number of instances during scaling. When the policy is triggered, workload instances will scale within the configured minimum and maximum instance limits. |
      |Prediction percentiles |A predictive quantile that indicates the probability of the actual metric value not reaching the specified target value. A larger value indicates a more conservative scaling policy. The value needs to be a positive integer. Valid values: 1 to 100. Recommended values: 90 to 99. |
      |Cold start time |The time required for a pod to reach the Ready state. |
      

   * **Scaling rule**

      
      |Parameters |Description |
      |---|---|
      |Scaling policy |Select **Scale\-out policy** and **Scale\-in policy** to configure the workload scale\-in and scale\-out behavior. |
      |Silence time |Specify the silence time of the scale\-out policy or scale\-in policy. The value is an integer. Unit: seconds.<br><br>After the system completes scaling, the scaling policy will not be executed again during the silence time. This prevents frequent changes in the number of workload replicas that lead to system instability. |
      |Policy type |Specify the policy type. Valid values:<br><br><br>* **Maximum value**: executes the policy that has the most impact on pod count.<br><br>* **Minimum value**: executes the policy that has the least impact on pod count.<br><br>* **Disable**: disables the scale\-out policy or scale\-in policy. |
      |Policy |Configure specific scaling policy operations. Valid values:<br><br><br>* **Type**: Specify the type of scaling policy behavior.<br><br>   * **Pod**: performs scaling based on the number of pods.<br><br>   * **Percentage**: performs scaling based on the percentage of pods.<br><br>* **Threshold**: Specify the threshold for scaling. This parameter needs to be used together with **Type**. For example, if you set the **Type** parameter to **Pod** and the threshold to 10, it indicates that 10 replicas will be scaled out or scaled in within the **time interval**.<br><br>* **Time interval**: Specify the interval at which scaling is performed. The value is an integer. Valid values: 1 to 1800. Unit: seconds. |
      

   * **Effective period**

      
      |Parameters |Description |
      |---|---|
      |Start time |Specify the time when the IHPA starts to take effect, which is accurate to seconds. |
      |End time |Specify the end time of the IHPA. Valid values:<br><br><br>* **Permanent**: indicates that the IHPA never expires.<br><br>* Select a date: Specify the time when the IHPA ends, which is accurate to seconds. The end time needs to be not earlier than the start time. |
      |CronHPA policy |Configure the CronHPA policy. Valid values:<br><br><br>* **Repeat regularly**: You can select **By hour**, **By day**, **By week**, or **Monthly** to perform scheduled scaling at a specific time point. You can also enter a Cron statement to specify the time. For configuration methods, see [Cron statements](https://docs.byteplus.com/en/docs/vke/Cron-expressions).<br><br>* **Minimal instances**: Specify the minimum number of instances during scheduled scaling.<br><br>* **Maximum instances**: Specify the maximum number of instances during scheduled scaling. |
      

2. Click **Confirm** to complete the configuration.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation

<span id=".5p-l55yL5qaC6KeI"></span>
### Viewing overview


1. In the left navigation bar on the cluster management page, click **Autoscaling** \> **IHPA**. On the IHPA page, click the name of the policy to go to the details page of the policy.

2. Click the **Overview** tab to view the configuration details of the intelligent scaling policy.


<span id=".5p-l55yL5LqL5Lu2"></span>
### Viewing events


1. In the left navigation bar on the cluster management page, click **Autoscaling** \> **IHPA**. On the IHPA page, click the name of the policy to go to the details page of the policy.

2. Click the **Event** tab to view the event details of the intelligent scaling policy.
