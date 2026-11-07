---
title: "Configuring node check and self-healing"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/NodePool-health-check-and-auto-repair"
---

The operation status of nodes, as the infrastructure of clusters, is critical to users. The VKE team provides the self\-developed node check and self\-healing feature for common failure detection and self\-healing for nodes. This topic describes how to configure the node check and self\-healing feature.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is available only to enterprises. If you cannot view the corresponding page in the console, make sure that your account has completed enterprise verification.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The node\-problem\-detector add\-on has been installed. For details, see [node-problem-detector](https://docs.byteplus.com/en/docs/vke/node-problem-detector-add-on).

* (Optional) A Vital Managed Service for Prometheus (VMP) workspace has been created.

* (Optional) To use the custom failure detection feature, make sure that you have configured custom failure check items. For details, see [Custom node check items](https://docs.byteplus.com/en/docs/vke/node-problem-detector-add-on).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u5qOA5p-l6Ieq5oSI6KeE5YiZ"></span>
### Step 1: Configure a check and self\-healing rule


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster to go to the cluster management page.

4. In the left navigation pane of the cluster management page, click **Check and self\-healing**. Then, click **Create check and self\-healing rules**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When you configure check and self\-healing rules, if multiple check items are selected and their self\-healing rules differ, the system will automatically split them into multiple rules.   </div>
   

   
   |Parameter |Description |
   |---|---|
   |Rule name |Specify a name for the check and self\-healing rule. The rule name must be unique in the same cluster. |
   |**Rules** ||
   |Failure type |Select the type of failures to be checked. Supported failure types include **GPU failures**, **XID exception, Node failure, System and add\-on failures**, and **custom fault**. |
   |Check item |Select one or more items to be checked for the specified failure type. Different types of failures support different check items. For details, see [Check and self-healing overview](https://docs.byteplus.com/en/docs/vke/Check_and_self-healing_overview). |
   |Event listening |When the **Failure type** is **Node failure** , and the **check item** is **ECS failure**, specific events can be selected for listening.  <br><br><br>* **All events**: Listens to all events.<br><br>* **Specified events**: Listens to specified events. Multiple selection allowed. For event details, see [Check and self-healing overview](https://docs.byteplus.com/en/docs/vke/Check_and_self-healing_overview). |
   |Failure handling approach |Select an automatic failure handling method. Valid values:<br><br><br>* **Anomaly prompt**: Only includes the **Anomaly prompt** process.<br><br>* **Cordon nodes**: Includes **Anomaly prompt**, **Process intervention (optional)** , and **Cordon nodes**.<br><br>* **Drain nodes**: Includes **Anomaly prompt**, **Process intervention (optional)** , **Cordon nodes**, and **Node draining**.<br><br>* **Auto recovery**: Includes **Anomaly prompt**, **Process intervention (optional)** , **Cordon nodes**, **Node draining**, **Auto recovery**, and **Uncordon (optional)** .<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <strong>Failure type</strong> is set to <strong>custom fault</strong>, only the <strong>Auto recovery</strong> failure handling approach is supported.</div><br> |
   

6. Configure the troubleshooting process.

   * **Anomaly prompts**: When a node fails, the system converts failure information into metrics. You can use the cloud\-native observability feature to obtain metrics and view them in the VMP console.

   * **Process intervention**: After you enable this feature, the system will add the specified labels to nodes after the preceding steps are complete, to identify failed nodes. You can filter specified nodes by label to perform manual intervention and troubleshooting.

   * **Cordon nodes**: When a node fails, the NoSchedule taint will be added to the node to prevent new pods from being scheduled to the node.

   * **Node draining**: When a node fails, add the NoExecute taint to the node and evict all pods on it.

      
      |Parameter |Description |
      |---|---|
      |Prohibit scheduling |Specify the time period before a node starts evicting pods after the node is cordoned. Multiple time periods are available, such as immediately, 15 minutes, 30 minutes, 1 hour, 2 hours, 3 hours, 6 hours, 12 hours, 24 hours, 36 hours, 2 days, 3 days, 4 days, 5 days, 6 days, and 7 days.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Before node draining, the system checks whether one of the following workloads is running on the nodes. You need to make sure that these workloads do not exist on the nodes. Otherwise, node draining will not be performed.</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">ingress\-controller Pods</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Workloads that are strongly bound to the nodes</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Single\-replica workloads</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Static pods</div><br><br><br><br><div data-tips="true" data-tips-type="warning">Node draining does not guarantee the termination or eviction of workloads on a node. If a workload cannot be evicted and no manual intervention is performed, the next self\-healing operation will not be performed until the node is forcibly restarted at the specified time.</div><br> |
      

   * **Auto recovery**: When you enable this feature, the system will attempt to fix node failures to achieve self\-healing after node draining.

      
      |Parameter |Description |
      |---|---|
      |Reboot ECS nodes if necessary |Automatic fixing operations vary by failure type. If you select this option, the node will be automatically restarted regardless of whether it is drained or not. The node will not be automatically restarted unless it is automatically fixed.<br><br>Specify the waiting period before a node restarts after it has been drained, such as immediately, 30 minutes, 1 hour, 2 hours, 3 hours, and 6 hours. |
      

   * **Uncordon**: Specify whether to automatically uncordon a node after the node restarts and its failure is fixed. When the feature is enabled, the system will perform health checks again after the node restarts. If all check items pass the checks, the node will be uncordoned.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The system can only make sure that no exceptions occur in the existing check items. If a failure occurs beyond the scope of node check items, the operation of training or inference tasks may become abnormal. If issues persist after the self\-healing process is complete, <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210">submit a ticket</a> to obtain technical support.      </div>
      

7. (Optional) Click **Add rules** to add multiple rules.

8. After the configuration is complete, carefully read **Considerations**, select **I acknowledge and consent to**, and then click **Confirm** to save the configurations.


<span id=".5q2l6aqk5LqM77ya6IqC54K55rGg57uR5a6a5qOA5p-l6Ieq5oSI6KeE5YiZ"></span>
### Step 2: Associate a node pool with the check and self\-healing rule

You can associate the check and self\-healing rule with a node pool when creating it, or with an existing node pool. This topic provides an example of how to associate the check and self\-healing rule with a node pool when you create the node pool.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only managed node pools can be associated with check and self\-healing rules. If your node pool is a normal node pool, you need to enable hosting for the node pool first and then associate a check and self\-healing rule with the node pool.</div>



1. In the left navigation bar of the cluster management page, click **Nodes** \> **Node pool**. On the page that appears, click **Create node pool**. In the pop\-up dialog box, select **Managed mode pool**.

2. When configuring node pool details, enable the **Check and self\-healing** feature under **Operation and maintenance configuration** and bind self\-healing rules.

   
   |**Parameter** |**Description** |
   |---|---|
   |Check and self\-healing |Specify whether to enable the node check and self\-healing feature.<br><br><br>* **Enable**: After you configure node self\-healing rules, the system will automatically check node status and promptly handle node failures to recover nodes.<br><br>* **Disable:**  Does not enable this feature. This is the default setting. |
   |Check and self\-healing rules |Configure a check and self\-healing rule. Valid values:<br><br><br>* **Recommendation rule**: Use the system default recommended rule. For details, see [Recommended rules](https://docs.byteplus.com/en/docs/vke/Creating-a-managed-NodePool#.5o6o6I2Q6KeE5YiZ).<br><br>* **Custom rule**: To use your custom rules, select a configured check and self\-healing rule from the drop\-down list. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more configurations of node pools, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-managed-NodePool">Creating node pools</a>.   </div>
   

3. Click **Confirm** to complete the binding.


<span id=".5q2l6aqk5LiJ77ya77yI5Y-v6YCJ77yJ5byA5ZCv5LqR5Y6f55Sf6KeC5rWL"></span>
### Step 3: (Optional) Enable cloud\-native observability

If you need to use node failure metrics to obtain node status, enable the cloud\-native observability feature. The steps are as follows:


1. Bind the cluster to a VMP workspace, install the prometheus\-agent add\-on, and enable cloud\-native observability. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

2. Enable check and self\-healing observability. For details, see [Check and self-healing observability](https://docs.byteplus.com/en/docs/vke/Check_Self-healing_Observation).


<span id=".57uT5p6c6aqM6K-B"></span>
## Validate results

<span id=".5p-l55yL5qOA5p-l6Ieq5oSI6KeE5YiZ"></span>
### Viewing the check and self\-healing rule


1. In the left navigation pane of the cluster management page, click **Health check & auto recovery**.

2. In the self\-healing rule list, click the name of the target self\-healing rule to view its details.


<span id=".5p-l55yL6Ieq5oSI5Lu75Yqh6K-m5oOF"></span>
### Viewing self\-healing task details

After self\-healing is complete for a failed node, you can view the self\-healing task list and details on the Node details page.


1. In the left navigation bar of the cluster management page, click **Nodes \> Node**.

2. Click the name of the target node to go to the Node details page.

3. Click the **Self\-healing from failure** tab to view the list of failure self\-healing tasks for the current node.

4. Click the name of the target self\-healing task to view the self\-healing details for the current node.


<span id=".5p-l55yL5qOA5p-l6Ieq5oSI6KeC5rWL"></span>
### Viewing check and self\-healing observability data

You can view check and self\-healing observability data on the cloud\-native observability dashboard and configure the corresponding alerts. For details, see [Check and self-healing observability](https://docs.byteplus.com/en/docs/vke/Check_Self-healing_Observation).

<span id=".5p-l55yL5ZGK6K2m6KeE5YiZ6K-m5oOF"></span>
### Viewing alert rule details

After you configure check and self\-healing alerts, you can view the details of the corresponding alert rule in the VMP console.


1. Log in to the [VMP console](https://console.byteplus.com/prometheus).

2. Click **Alert Center \> Alert rule** in the left navigation bar. Click the **Alert rule group** tab. On this tab, you can view the configured check and self\-healing alert rule groups.

3. Click the name of the target alert rule group to go to its details page. Then, click the **Alert rule list** tab to view the alert rule details.


<span id=".5YW25LuW5pON5L2c"></span>
## Other operations

<span id=".57uI5q2i5qOA5p-l6Ieq5oSI5rWB56iL"></span>
### Terminating the self\-healing process

During the execution of a check and self\-healing task, you can manually terminate the self\-healing process at any time.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After the self\-healing process is terminated, the step in progress will continue until completion, but subsequent steps will not be performed. You need to manually resolve the remaining issues. No troubleshooting will be performed on the node again until it is uncordoned.</div>



1. In the left navigation bar of the cluster management page, click **Nodes \> Node**.

2. Click the name of the target node to go to the Node details page.

3. Click the **Self\-healing from failure** tab and then find the target self\-healing task in the failure self\-healing task list.

4. Click the name of the self\-healing task to go to its details page. Click **Stop failure processing** to terminate the self\-healing task.
