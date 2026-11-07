---
title: "Nodes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Node-monitoring-1"
---

Node resource retrieval provides the monitoring information of nodes in clusters, including the node list and node details. This topic describes how to view the node list and details.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Cloud\-native observability has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* Full\-stack observability has been enabled. For details, see [Enabling full-stack observability](https://docs.byteplus.com/en/docs/vke/Network-and-application-observability).


<span id=".6IqC54K55YiX6KGo"></span>
## Node list


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the cluster list page, click the target cluster.

4. In the left navigation bar of the cluster management page, click **Monitoring center** \> **Resource explorer**.


<span id=".5p-l55yL6IqC54K55YiX6KGo"></span>
### Viewing the node list

In the **Resource type** panel, select **Node** to view the node list. The node list displays basic information for cluster nodes, including the node name, status, Kubelet version, running status, schedulability, pod, label, CPU usage, and memory usage.

You can perform the following operations in the node list:


* Click the name of the target node to go to the node details page to view the details of the node.

* Click the number in the **Pods** column to go to the Pod page and view the information about all pods for the node.


<span id=".6IqC54K5562b6YCJ"></span>
### Filtering nodes

In the node list, you can filter nodes by node IP address, status, running status, label, or annotation. This helps you quickly locate the target node.


1. Select the information to be retrieved from the **Node**, **Status**, and **Operation status** drop\-down lists.

2. Click **Add label/annotation** to configure the labels or annotations for the node.

   
   |Parameters |Description |
   |---|---|
   |Type |Select Label or Annotation to filter nodes. |
   |Name |Enter the name of the label or annotation in string format. |
   |Operator |Configure the operator. Valid values:<br><br><br>* **Include**: Indicates that the label and annotation contain the specified value.<br><br>* **Not equal to**: Indicates that the label and annotation do not contain the specified value. |
   |Value |Specify the value of the label or the annotation in string format. You can enter multiple values by pressing the spacebar. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can add multiple labels or annotations for retrieval.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Multiple values are in the <strong>AND</strong> relationship, which means the node must contain all values.   </div>
   

3. Click **Search** to retrieve the node.


<span id=".6IqC54K56IGa5ZCI"></span>
### Aggregating nodes

You can aggregate nodes by **Status** and **Operation status** in the node list.


1. Select the target node aggregation dimension from the **Aggregation dimension** drop\-down list.

2. Click **Search** to aggregate nodes.


<span id=".6IqC54K56K-m5oOF"></span>
## Node details

Click the name of the target node in the node list to go to the node details page. You can view node details, including the basic information, performance overview, and YAML.

<span id=".5Z-656GA5L-h5oGv"></span>
### Basic information

In the **Basic information** section, view the basic information about the node, such as the Kubelet version, specification, operation duration, label, and annotation.

<span id=".5a655Zmo57uE5YiX6KGo"></span>
### Pods

In the Pods section, view the list of pods and their information on the node, such as the pod name, status, number of ready pods, number of restarted pods, namespace, QPS, P90 request latency, and error rate.

<span id=".5Z-656GA6LWE5rqQ6KeC5rWL"></span>
### Basic observability

Click the **Basic observability** tab to view the resource monitoring information of the node, such as CPU monitoring information, memory monitoring information, disk monitoring information, network monitoring information, and GPU monitoring information. You can query resource usage by time period and set the information refresh mode to manual or automatic refresh.

<span id=".eWFtbC3kv6Hmga8="></span>
### YAML

Click the **YAML** tab to view the YAML file content of the node.
