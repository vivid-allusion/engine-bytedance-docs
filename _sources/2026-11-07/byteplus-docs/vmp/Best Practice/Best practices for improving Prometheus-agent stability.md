---
title: "Best practices for improving Prometheus-agent stability "
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Best_practices_for_improving_Prometheus-agent_stability_"
---

Prometheus\-agent is a collector add\-on that allows Vital Managed Service for Prometheus (VMP) to collect information from Vital Kubernetes Engine (VKE) clusters. The stability of Prometheus\-agent affects cluster observability results and quality. This topic describes how to improve the stability of Prometheus\-agent in practical scenarios.

<span id="4PhjOUqX"></span>
## Background

For enhanced performance and stability, a newer version of the Prometheus\-agent add\-on may be available in your VKE cluster. We recommend reviewing the release notes and upgrading to the latest version. For details, see [Add-on release notes](https://docs.byteplus.com/en/docs/vke/prometheus-agent).

An increase in cluster size can cause performance issues, which can lead to unexpected faults, such as metric loss. You are also advised to perform the following common operations to mitigate the risk and improve the stability of the Prometheus\-agent add\-on.

<span id="CNtjvDML"></span>
## Common operations

<span id="lmRxAAoC"></span>
### Upgrading the version

We recommend that you upgrade the Prometheus\-agent add\-on in your cluster to the latest version. For details, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Prometheus\-agent V2.8.0 has a new capability: add\-on self\-monitoring metrics collection, which enables the use of cloud\-native VKE observability to monitor the metrics and status of the add\-on itself.</div>



* <div data-tips="true" data-tips-type="warning">If the add\-on version is earlier than v2.8.0, upgrade it to the latest version.</div>


* <div data-tips="true" data-tips-type="warning">If upgrading is not feasible, configure add\-on self\-monitoring for data collection based on the instructions in Step 2.</div>



Ensure that Prometheus\-agent in your VKE cluster is deployed using the standard method. Otherwise, you may not be able to upgrade it in the VKE console. To deploy it in the standard way, perform the following steps:


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview). 

2. In the left navigation bar, click **Cluster**. In the cluster list, click the name of the target cluster.

3. In the left navigation bar of the cluster management page, click **Addons**. On the Addons page, click the **Monitoring** tab****.

4. Find the Prometheus\-agent card, and in the upper right corner, click `...` \> **Install**. For a detailed description of configuration items for the installation, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on)


If you want to collect basic metrics of containers in the clusters, enable cloud native observability and basic observability. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability) and [Basic observability](https://docs.byteplus.com/en/docs/vke/Basic-observability).

<span id="lHMJcx40"></span>
### Creating self\-monitoring collection configurations

If the Prometheus\-agent add\-on in your cluster is earlier than V2.8.0 and cannot be upgraded, you can follow the steps below to create a self\-monitoring collection configuration by using a ServiceMonitor.


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview). 

2. In the left navigation pane, click **Cluster**. In the cluster list on the right side, find the target cluster.

3. Click the name of the cluster to go to the cluster configuration page.

4. In the left navigation bar, click **Workload \> Resource Explorer**. Click **Create with Yaml** to configure service discovery through ServiceMonitor.

   * Select **Custom** from the **Type** drop\-down menu.

   * Enter the YAML configuration in the **Yaml** editor.


```YAML
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  labels:
    volcengine.vmp: "true"
  name: prometheus-agent
  namespace: kube-system
spec:
  endpoints:
  - bearerTokenSecret:
      key: ""
    interval: 15s
    path: /metrics
    port: http
    scheme: http
    scrapeTimeout: 10s
  namespaceSelector:
    matchNames:
    - kube-system
  selector:
    matchLabels:
      app.kubernetes.io/instance: prometheus-agent
      app.kubernetes.io/name: vmagent
      managed-by: vm-operator
```


<span id="3uuvTFBQ"></span>
### Enabling autoscaling

As the cluster scales and the number of metrics being collected grows, Prometheus\-agent may face insufficient resource capacity, leading to issues like OOM (Out of Memory), restricted metric collection, or even data loss in severe cases. To prevent these problems, we recommend enabling the autoscaling feature , which allows the system to automatically adjust the replica count of the collector add\-on based on its real\-time resource usage.

You can enable add\-on autoscaling when or after you deploy the add\-on. This topic describes how to enable the feature after the add\-on is deployed.


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview). 

2. In the left navigation bar, click **Cluster**. In the cluster list, click the name of the target cluster.

3. In the left navigation bar of the cluster management page, click **Addons**. On the Addons page, click the **Monitoring** tab****.

4. Click **Configuration** on the Prometheus\-agent add\-on card. In the dialog box that appears, enable add\-on autoscaling and specify the maximum shard number. Then, click Confirm.



|Parameter |Description |
|---|---|
|Addon scaling |Specify whether to enable the automatic scaling feature for the vm\-agent collector and the kube\-state\-metrics agent.<br><br><br>* **Disable**: The number of shards for the agent is the specified initial number of shards. The agent will not be automatically scaled out as resource usage increases.<br><br>* **Enable**: You need to specify the maximum number of shards for the agent. The agent will be automatically scaled based on resource usage by the following rules:<br><br>   * **vm\-agent scale\-out**: vm\-agent is automatically scaled out when CPU or memory usage is greater than 70%.<br><br>   * **vm\-agent scale\-in**: vm\-agent is automatically scaled in when CPU and memory usage are less than 30%.<br><br>   * **kube\-state\-metrics scale\-out**: kube\-state\-metrics is automatically scaled out when CPU or memory usage is greater than 70%.<br><br>   * **kube\-state\-metrics scale\-in**: kube\-state\-metrics is automatically scaled in when CPU and memory usage are less than 70%.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The cooldown period of vm\-agent scaling is 30 minutes. kube\-state\-metrics is scaled through HorizontalPodAutoscaler.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">After you enable the automatic scaling feature for the agent, ensure that cluster resources are sufficient. Otherwise, the agent scale\-out may fail caused by insufficient resources.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When you scale out the vm\-agent collector and the kube\-state\-metrics agent, it is recommended to specify the number of shards for the kube\-state\-metrics agent as an integer multiple of the number of shards for the vm\-agent collector to ensure load balancing. For example, maintain a 1:1 or 2:1 ratio of the number of shards for the kube\-state\-metrics agent to the number of shards for the vm\-agent collector.<code></code><code></code><code></code><code></code></div><br> |


<span id="LkDhiJ66"></span>
### Configure alerts

VMP provides alert rule templates for the Prometheus\-agent add on. We recommend that you configure add\-on alert rules to detect add\-on exceptions in real time.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The default thresholds in these templates are strict. If the default thresholds cause too many unnecessary alerts, adjust these thresholds to meet your actual requirements.</div>



1. Log in to the [VKE console](https://console.byteplus.com/vke/overview). 

2. In the top navigation bar, select the target region.

3. In the left navigation bar, click **Alert center \> Alert rule template**. On the page that appears, select the **Preset template** tab.

4. On the **Preset template** page, find the **vmagent alert rule template**. Click **Apply template** in the **Actions** column.

5. Adjust thresholds for alert rules that you want to modify. For details, see [Creating alert rule groups](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rule-groups).


<span id="L5YSqhx8"></span>
### Viewing dashboards

<span id="HXQXJBGs"></span>
#### Built\-in dashboards

If a cluster has cloud native observability enabled[](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability), you can check the Prometheus\-agent monitoring dashboard.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When you check the dashboard, select the VMP workspace that is bound to the cluster.</div>



1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. In the left navigation bar, select **Monitor dashboard**. In the dashboard list, search for **vmagent**.


We recommend that you pay special attention to the following charts in the dashboard:


* **CPU** and **RSS memory % usage**: show the resource usage of the add\-on.

* **Persistent queue dropped**: reflects whether persistent queues have dropped data. If vmagent has performance issues or other exceptions, the corresponding metrics cannot be sent to the VMP workspace. If that happens, the add\-on stores metrics in a persistent queue and recovers metric sending when exceptions are fixed. If any metric is displayed in the chart, metric sending has encountered data losses.

* **RemoteWrite connection saturation**: shows the connection saturation. If the saturation is greater than 80%, relatively high latency is observed in sending of each packet. In this case, consider increasing the CPU limit for vmagent to increase the concurrency level.


<span id="BMwnkuPL"></span>
#### Custom dashboards

You can also create a Grafana dashboard and import it as the Prometheus\-agent dashboard. For details, see the following documents.


1. Deployment: [Deploying Grafana in a VKE cluster and accessing workspaces.](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster)

2. Dashboard: Import the following dashboard configuration file into Grafana:


<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_96919150d8c7ae35f9689b44722faa0e.json" name="vmagent-dashboard.json">vmagent-dashboard.json</Attachment>
