---
title: "Collecting control plane add-on logs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Collecting-control-plane-add-on-logs"
---

VKE supports collecting logs from clusters' control plane components, helping you troubleshoot operational anomalies of core components such as kube\-apiserver, kube\-scheduler, and etcd. This topic describes how to enable log collection for control plane components and view the collection results.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Related fees will be incurred after you enable control plane add\-on logs. For detailed billing instructions, see <a href="https://docs.byteplus.com/en/docs/tls/Billing_items_based_on_pay-by-feature_mode">TLS billing</a>.</div>


<span id=".5o6n5Yi26Z2i57uE5Lu25LuL57uN"></span>
## Background

<span id="xjqXTnA9"></span>
### Supported components

VKE supports log collection for multiple control plane components, helping you understand the runtime status of key control plane components and providing a reference for cluster troubleshooting. The currently supported components are listed in the following table.


|Add\-ons |Description |
|---|---|
|kube\-apiserver |kube\-apiserver is a control plane add\-on that exposes the Kubernetes APIs. All resource requests and calls are implemented through this add\-on. For details, see the [official documentation](https://kubernetes.io/docs/concepts/overview/components/#kube-apiserver). |
|kube\-scheduler |The kube\-scheduler add\-on primarily schedules resources for the entire cluster. For details, see the [official documentation](https://kubernetes.io/docs/concepts/overview/components/#kube-scheduler). |
|kube\-controller\-manager |The kube\-controller\-manager add\-on is the management and automation control center of a cluster, which is used for managing multiple types of controllers in the cluster, such as the Node Controller and Replication Controller. For details, see the [official documentation](https://kubernetes.io/docs/concepts/overview/components/#kube-controller-manager). |
|etcd |etcd is the storage service of Kubernetes, which is used to store important information of the cluster. For details, see the [official documentation](https://kubernetes.io/docs/concepts/overview/components/#etcd). |
|cluster\-autoscaler |The cluster\-autoscaler component is a node autoscaler that implements cluster resource autoscaling. For details, see [Node autoscaling (Cluster AutoScaler)](https://docs.byteplus.com/en/docs/vke/Creating-a-Cluster-Autoscaler?lang=en). |
|karpenter |The Karpenter component is a just\-in\-time node autoscaler that implements autoscaling of cluster resources. For details, see [Just-in-time node autoscaling (Karpenter)](https://docs.byteplus.com/en/docs/vke/Configure_node_instant_autoscaler_Karpenter?lang=en). |


<span id="Ofy2ebAu"></span>
### Automatically generated log topics

After log collection is enabled for control plane components, the system automatically generates a log topic for each component. Understanding the naming format of log topics for each component helps you quickly locate the target topic and query related logs in TLS. The following table describes the naming format of the log topic for each component.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">By default, control plane add\-on logs are stored in topics for 30 days, and the number of log shards is 2. In addition, automatic log shard splitting is enabled by default. For more information about log topics, see <a href="https://docs.byteplus.com/en/docs/tls/Managing_topics">Log topics</a>.</div>


* <div data-tips="true" data-tips-type="tip">After you delete the cluster, the corresponding log topics will not be deleted. To delete the log topics, manually delete them in the <a href="https://console.byteplus.com/tls">TLS console </a>.</div>




|Add\-ons |Auto\-generated log topic name |
|---|---|
|kube\-apiserver |vke\-apiserver\-<your_clusterid\>\-xxxxxx |
|kube\-scheduler |vke\-scheduler\-<your_clusterid\>\-xxxxxx |
|kube\-controller\-manager |vke\-kcm\-<your_clusterid\>\-xxxxxx |
|etcd |vke\-etcd\-<your_clusterid\>\-xxxxxx |
|cluster\-autoscaler |vke\-ca\-<your_clusterid\>\-xxxxxx |
|Karpenter |vke\-ka\-<your_clusterid\>\-xxxxxx |


<span id="Toaezzzn"></span>
## Prerequisites


* TLS has been activated. To activate this service, log in to the [TLS console](https://console.byteplus.com/tls) and activate the service based on the on\-screen prompts.

* (Optional) A **log project** has been created in TLS. For detailed instructions, see [Log projects](https://docs.byteplus.com/en/docs/tls/Managing_projects).


<span id=".6YWN572u5pel5b-X6YeH6ZuG"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, select **Log management**, and then select the **Control Plane addon log** tab.

4. Click **Settings** to configure control plane component log collection.

   
   |**Parameter** |**Description** |
   |---|---|
   |Control plane add\-on log |Specify the control plane components whose logs need to be collected.<br><br><br>* **Checked**: Collect the logs of the component. If you select a component, specify the log project in which you want to store its logs.<br><br>* **Not checked**: The logs of this component will no longer be collected, but the generated log topic will not be deleted and may still incur billing. If you no longer need the topic, manually delete the topic in the [TLS console](https://console.byteplus.com/tls). For detailed instructions, see [Deleting log topics](https://docs.byteplus.com/en/docs/tls/Managing_topics#.5Yig6Zmk5pel5b-X5Li76aKY).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">After log collection is enabled for a component, the system automatically generates a log topic for the component. For details, see <a href="https://docs.byteplus.com/en/docs/90/21526#Ofy2ebAu">Automatically generated log topics</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The cluster\-autoscaler and karpenter components are mutually exclusive and cannot be installed in the same cluster simultaneously. Therefore, when collecting component logs, you cannot enable log collection for both components simultaneously.</div><br> |
   |Log usage type |Select the type of logs that you need to use. Valid values:<br><br><br>* **Use existing log projects**: Use a created log project in TLS. Add\-on logs will be written to this project.<br><br>* **Automatically create new log projects**: Automatically create a log project. Add\-on logs will be written to the created project.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If you change the log project for cluster control plane add\-on logs, the log project for cluster audit logs will also change. Proceed with caution. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Cluster-auditing">Cluster auditing</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The system automatically creates a log project, which is named <code>vke-k8s-log-{clusterId}</code>.</div><br> |
   |Project |Select the project to which the logs belong from the drop\-down list. For details, see [Project management](https://docs.byteplus.com/en/docs/vke/Project-management). |
   |Log project |Select the log project to which the control plane add\-on logs are written from the drop\-down list. You can also select **Create log project** from the drop\-down list to create a log project. For details, see [Log projects](https://docs.byteplus.com/en/docs/tls/Managing_projects) of . |
   

5. Click **Confirm** to finish.


<span id=".5p-l55yL5pel5b-X"></span>
## Validate results

After you configure the control plane add\-on log collection feature, you can view the information about the collected logs on the configuration page.


1. On the **Log management** page, click the **Control Plane addon log** tab.

2. Select the control plane add\-on for which you want to view logs from the drop\-down list to view the relevant log information.

   * If the logs of the selected component are already displayed on the page, log collection for the control plane component has taken effect.

   * If no logs are displayed, wait a few minutes and refresh the page to check again.
