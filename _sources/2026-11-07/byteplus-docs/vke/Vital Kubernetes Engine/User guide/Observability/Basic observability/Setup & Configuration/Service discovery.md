---
title: "Service discovery"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Service-discovery"
---

Service discovery integrates application metric endpoints in VKE clusters with VMP to collect custom metrics. This topic describes the service discovery methods supported by VKE clusters, the configuration steps, and how to verify metric collection.

<span id="lJM1rdCj"></span>
## Background

Prometheus primarily uses the pull method to scrape the monitoring endpoints exposed by target services. Therefore, you need to configure service discovery rules in the cluster to specify scraping targets. In this way, you can collect data and write it to the workspace of VMP.

VKE clusters support the following CRD resources for configuring custom metric collection. The following table describes the concepts and use cases of the resources.


|Resource type |Description |Application scenario |
|---|---|---|
|ServiceMonitor |Use a namespace and label to specify the Service to monitor, and use the Service ** ** to discover backend Pods. |Components or applications that expose metrics through a Service. Examples include CoreDNS, control plane services, and business applications. |
|PodMonitor |Use a namespace and label to directly specify the Pods to monitor. |Components that do not expose metrics through a Service or whose metrics must be scraped directly from Pods. An example is a CSI component. |
|VMNodeScrape |Directly scrape Kubernetes node\-level metrics without routing them through a Service or Pod. |Metrics of node\-level components such as node\-exporter, kubelet, and cadvisor. |
|Service/Pod annotation |Configure the specified annotations on a Service or Pod to enable service discovery. |The use cases are the same as those for ServiceMonitor and PodMonitor. However, adding the specified annotation fields when deploying resource objects enables quick integration when many resource objects exist. |


<span id="fEWeeBfz"></span>
## Prerequisites


* A VKE cluster has been created, and cloud\-native observability has been enabled for the cluster. For details, see [Enabling cloud-native observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* ServiceMonitor, PodMonitor, or other CRD resources have been created in the cluster. If these resources are not created, create them first as described in [How do I create CRD resources such as ServiceMonitor in a cluster](https://docs.byteplus.com/en/docs/vmp/How-do-I-create-Custom-Resource-Definition-resources-such-as-ServiceMonitor-in-a-cluster)?


<span id="3B4a8jds"></span>
## Implementing service discovery with ServiceMonitor

<span id="viGIHdmd"></span>
### Procedure

ServiceMonitor discovers backend Pods by matching Services. It is suitable for scenarios where an application exposes a metric port through a Service. After the configuration is complete, the system scrapes target metrics based on the port, path, and label rule settings defined in the ServiceMonitor. Procedure:


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, select **Cluster**. In the cluster list, find the target cluster.

3. Click the cluster name to go to the Cluster configuration page.

4. In the left navigation pane, click **Workload \> Resource Explorer**, click **Create with Yaml**, and configure service discovery through ServiceMonitor.

   * Select **Custom** from the **Type** drop\-down menu.

   * Edit the configurations in the **Yaml** box.


```YAML
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: service-discover # The name of the resource for service discovery.
  namespace: volcano-metrics # The namespace of the resource for service discovery.
  labels: 
    volcengine.vmp: "true" # The labels of the resource for service discovery so that the Agent can discover it.
spec:
  endpoints:
  - interval: 15s # The time interval for collection. The default interval is 15 seconds.
    scrapeTimeout: 10s # The collection timeout. The default interval is 15 seconds.
    port: metrics # The service port name. This port name must be explicitly declared in the container configuration.
    path: /metrics # The URI path where metrics are exposed. The default value is /metrics.
    scheme: http # The collection protocol. Supported protocols are HTTP and HTTPS. The default is HTTP.
    relabelings: # Configure metric relabeling. If this is not required, omit it. This example adds the fixed label environment="Production".
    - targetLabel: environment
      action: replace
      replacement: Production
  namespaceSelector: # The namespace where the target is located. If you do not specify a value, the current namespace is used.
    matchNames:
    - volcano-metrics 
  selector: # The label value for selecting the target service.
    matchLabels:
      app.kubernetes.io/name: ek8s-gpu-exporter 
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details of configuration items, see the <a href="https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#monitoring.coreos.com/v1.ServiceMonitor">documentation</a>.</div>



5. Click **Confirm** to finish.


<span id="FZ2WQv56"></span>
### View settings

After you create the CRD in VKE, you can follow the steps below to view, edit, or delete the configuration.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, select **Cluster**. In the cluster list, find the target cluster.

3. Click the cluster name to go to the Cluster configuration page.

4. In the left navigation pane, click **Workload \> Resource Explorer**. From the **Category** drop\-down list, select **CRD** to view created CRD resources.

5. Click **ServiceMonitor** to go to the details page.

6. Find the configuration you want to edit or delete. In the **Actions** column, click `...`, then select **Edit Yaml** or **Delete**.


<span id="zon8JsgZ"></span>
## Implementing service discovery with PodMonitor

<span id="VlSPyNXU"></span>
### Procedure

PodMonitor discovers scrape targets directly by Pod label. It is suitable for scenarios where target Pods do not expose metrics through a Service or when you want to scrape Pod metrics without using a Service. After the configuration is complete, the system scrapes target metrics based on the port, path, and label rule settings defined in the PodMonitor. Procedure:


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, select **Cluster**. In the cluster list, find the target cluster.

3. Click the cluster name to go to the Cluster configuration page.

4. In the left navigation pane, click **Workload \> Resource Explorer**, click **Create with Yaml**, and configure service discovery through PodMonitor.

   * Select **Custom** from the **Type** drop\-down menu.

   * Edit the configurations in the **Yaml** box.


```YAML
apiVersion: monitoring.coreos.com/v1
kind: PodMonitor
metadata:
  name: pod-discover # The name of the resource for service discovery.
  namespace: volcano-metrics # The namespace of the resource for service discovery.
  labels: 
    volcengine.vmp: "true" # The labels of the resource for service discovery so that the Agent can discover it.
spec: # The characteristics of the target pod of metric collection and the configuration of the collection task
  podMetricsEndpoints: # The Prometheus HTTP endpoint for the monitored object. Multiple endpoints can be configured.
  - interval: 15s # The time interval for collection. The default interval is 15 seconds.
    scrapeTimeout: 10s # The collection timeout. The default interval is 15 seconds.
    port: metric-port # The container port name. This port name must be explicitly declared in the container configuration.
    path: /metrics # The URI path where metrics are exposed. The default value is /metrics.
    scheme: http # The collection protocol. Supported protocols are HTTP and HTTPS. The default is HTTP.
    relabelings: # The metric relabeling configuration. Multiple relabeling rules can be configured. Multiple rules execute in order.
    - action: replace # The action to take on a matched label. Available actions include replace, keep, and drop.
      sourceLabels: # Source labels for relabeling.
      - instance
      regex: (.*) # Regular expression for matching the values of source labels.
      targetLabel: instance # When action is replace, specify the corresponding label name using target_label.
      replacement: 'kafka-xxxxxx' # When action is replace, use replacement to define the expression that will replace the matched value after regex matching.
  namespaceSelector: # The namespace where the target is located. If you do not specify a value, the current namespace is used.
    matchNames: 
    - volcano-metrics 
  selector: # The label value for selecting the target pod.
    matchLabels:
      app-name: kafka-exporter
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details of configuration items, see the <a href="https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api.md#monitoring.coreos.com/v1.PodMonitor">documentation</a>.</div>



5. Click **Confirm** to finish.


<span id="d3EqV2x2"></span>
### View settings

After you create the CRD in VKE, you can follow the steps below to view, edit, or delete the configuration.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, select **Cluster**. In the cluster list, find the target cluster.

3. Click the cluster name to go to the Cluster configuration page.

4. In the left navigation pane, click **Workload \> Resource Explorer**. From the **Category** drop\-down list, select **CRD** to view created CRD resources.

5. Click **PodMonitor** to go to the details page.

6. Find the configuration you want to edit or delete. In the **Actions** column, click `...`, then select **Edit Yaml** or **Delete**.


<span id="0oqIOLNU"></span>
## Enable service discovery through VMNodeScrape

<span id="Xc4JoFR9"></span>
### Procedure

You can configure service discovery for node\-level metrics through VMNodeScrape. This topic uses kubelet metric configuration as an example. Perform the following steps:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When configuring kubelet metrics, we recommend retaining the node discovery and TLS settings. Then, add the names of the additional metrics to collect, such as <code>kubelet_evictions</code>, to <code>metricRelabelConfigs</code>.</div>


* <div data-tips="true" data-tips-type="warning">Carefully select the scrape scope and metrics in custom collection rules. If your custom rules overlap with the cluster's default rules, metrics are scraped more than once, resulting in duplicate charges.</div>


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, select **Cluster**. In the cluster list, find the target cluster.

3. Click the cluster name to go to the Cluster configuration page.

4. In the left navigation pane, click **Workload \> Resource Explorer**, click **Create with Yaml**, and configure service discovery through VMNodeScrape.

   * Select **Custom** from the **Type** drop\-down menu.

   * Edit the configurations in the **Yaml** box.


```YAML
apiVersion: operator.victoriametrics.com/v1beta1
kind: VMNodeScrape
metadata:
  name: custom-kubelet # Custom service discovery name.
  namespace: kube-system # Namespace of the custom service discovery configuration.
  labels: 
    volcengine.vmp: "true" # The labels of the resource for service discovery so that the Agent can discover it.
spec:
  bearerTokenFile: /var/run/secrets/kubernetes.io/serviceaccount/token
  interval: 15s # Collection interval. The system scrapes metrics from all target nodes every 15 seconds.
  scheme: https # By default, kubelet exposes metrics over HTTPS on port 10250. Explicitly declare this port.
  selector: # Use a Kubernetes label selector to filter for the nodes to scrape.
    matchExpressions:
      - key: node.kubernetes.io/instance-type
        operator: NotIn
        values:
          - dcp-node
  tlsConfig: # Node TLS settings. Keep them consistent with those in the default rule configuration.
    caFile: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
    insecureSkipVerify: true
  relabelConfigs:
    - replacement: kubelet-custom # Rewrite the job label of the nodes to kubelet-custom, facilitating subsequent metric filtering by job="kubelet-custom".
      targetLabel: job
    - regex: (.+)
      sourceLabels:
        - __meta_kubernetes_node_name
      targetLabel: node
    - regex: volcengine://(.+)
      sourceLabels:
        - __meta_kubernetes_node_provider_id
      targetLabel: ecs
  metricRelabelConfigs: # Metric filtering configuration.
    - action: keep # Keep metrics.
      sourceLabels: # Filter by metric name. This example keeps only metrics that match the regular expression.
        - __name__
      regex: kubelet_running_pods|kubelet_node_name|kubelet_evictions # Specify the metric names to retain or the regular expression. This setting determines the metrics that this collection rule ultimately collects.
```



5. Click **Confirm** to finish.


<span id="H7q2yyGG"></span>
### View settings

After you create a custom configuration in VKE, perform the following steps to view, edit, or delete it.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, select **Cluster**. In the cluster list, find the target cluster.

3. Click the cluster name to go to the Cluster configuration page.

4. In the left navigation pane, click **Workload \> Resource Explorer**. Select **CRD** from the **Category** drop\-down list and search for `vmnodescrape` to view the configuration in the cluster.

5. Click the resource name to go to its details page.

6. Find the configuration you want to edit or delete. In the **Actions** column, click `...`, then select **Edit Yaml** or **Delete**.

   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">danger   </div>
   

   <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">Do not delete the default cluster configurations. Otherwise, cluster observability may not work as expected.   </div>
   

<span id="20RM4mUn"></span>
## Implementing service discovery with service or pod annotations

<span id="D1LmTL5V"></span>
### Background information

You can use a ServiceMonitor or PodMonitor to implement service discovery. However, if a cluster contains many services or pods, the monitoring configuration becomes especially complex as you need to manually create multiple ServiceMonitor or PodMonitor objects.

To address this issue, VMP provides another method for service discovery: using service or pod annotations. You can add specified annotations when deploying a service or pod to enable rapid service discovery.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Using service or pod annotations is a fast method for service discovery. However, it also has some disadvantages. For example, it does not support metric relabeling. You should evaluate whether this method can meet your actual requirements.</div>


* <div data-tips="true" data-tips-type="warning">Service discovery based on service or pod annotations is not supported in the kube\-system namespace. If necessary, we recommend using ServiceMonitor or PodMonitor.</div>



<span id="85Cqr8yy"></span>
### Overview

When configuring a service or pod in the cluster, you can enable service discovery for custom targets by adding the following annotations.

```YAML
prometheus.io/scrape: "true"   # Set the value to true to enable collection.
prometheus.io/port: "9400"     # The port number where the metrics are exposed.
prometheus.io/path: "/metrics" # The URI path where metrics are exposed. It is typically /metrics.
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you use <code>prometheus.io/port: "9400"</code> to specify the target port, explicitly declare the port in the container configuration as follows:</div>


<div data-tips="true" data-tips-type="tip">```YAML
...
    spec:
      containers:
        ports:
        - containerPort: 9400 # Explicitly declare the container port in the container configuration.
```
</div>


<span id="T7bmgqok"></span>
### Configuring service discovery based on service annotations

When configuring a service in the cluster, you can add annotations to enable service discovery. This enables the service to be easily integrated into a monitoring solution. To do so, follow these steps:


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster to go to the cluster management page.

4. In the left navigation bar, click **Services and Ingresses** \> **Service**. On the page that appears, click **Create with Yaml** to configure the service. During service configuration, add the annotations to enable easy service discovery.


```YAML
apiVersion: v1
kind: Service
metadata:
  name: golang-service-demo
  namespace: volcano-metrics # Specify the namespace where the service is located.
  labels: 
    app: golang-service-demo # Service labels.
  annotations: 
    prometheus.io/scrape: "true"  # Set the value to true to enable service discovery.
    prometheus.io/port: "2023"  # The port number where the metrics are exposed. This port number must be explicitly declared in the container configuration.
    prometheus.io/path: "/metrics" # The URI path where metrics are exposed. It is typically /metrics.
spec:
  selector:
    app: golang-demo
  ports:
    - protocol: TCP
      port: 2023
      targetPort: 2023
      name: metrics # The service port name.
  type: ClusterIP
```


<span id="vIWQtGdg"></span>
### Configuring service discovery based on pod annotations

When configuring a pod in the cluster, you can add annotations to enable service discovery. This enables the pod to be easily integrated into a monitoring solution. To do so, follow these steps:


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster to go to the cluster management page.

4. In the left navigation pane, click **Workload \> Deployment**. Click **Create with Yaml**. Deploy the application and add annotations to enable service discovery.


```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: golang-demo # Specify a name for the application.
  namespace: volcano-metrics # Specify the namespace where the application resides.
  labels:
    app: golang-demo # Specify application labels.
spec:
  replicas: 2 # The number of replicas for the application.
  selector:
    matchLabels:
      app: golang-demo
  template:
    metadata:
      labels:
        app: golang-demo
      annotations: 
        prometheus.io/scrape: "true"  # Set the value to true to enable service discovery.
        prometheus.io/port: "2023"  # The port number where the metrics are exposed. This port number must be explicitly declared in the container configuration.
        prometheus.io/path: "/metrics" # The URI path where metrics are exposed. It is typically /metrics.
    spec:
      containers:
      - name: golang-demo # The container name.
        image: doc-cn-beijing.cr.volces.com/vmp/golang-demo:1.0 # The address and version of the application image.
        ports:
        - containerPort: 2023 # The container port.
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This example uses a Deployment configuration for demonstration. For other workload types, the configuration is similar.</div>


* <div data-tips="true" data-tips-type="tip">The image address in this example is only for demonstration purposes. You need to replace it with your actual image address.</div>


* <div data-tips="true" data-tips-type="tip">Service discovery based on pod annotations does not support HTTP and HTTPS simultaneously.</div>



<span id="WWbWgutH"></span>
## What to do next

After configuring service discovery, you can use the Explore feature of VMP to confirm whether the expected service has been discovered. Procedure:


1. Log in to the [VMP console ](https://console.byteplus.com/prometheus).

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Explore** to go to the Explore page.

4. In the upper\-right corner, specify the **workspace** from which to query metrics. In the **Query** text box, enter a statement in the `up{job="xxx"}` format to check whether the corresponding service is discovered. A metric value of 1 indicates that the corresponding service is correctly discovered.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you still cannot view the expected metrics, see <a href="https://docs.byteplus.com/en/docs/vmp/unable-to-query-expected-metrics">Why do I fail to view the expected metrics?</a>   </div>
