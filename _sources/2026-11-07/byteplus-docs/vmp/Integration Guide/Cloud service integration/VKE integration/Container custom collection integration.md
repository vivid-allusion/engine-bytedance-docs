---
title: "Container custom collection integration"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/service-discovery"
---

In addition to the default collection rules of the collection add\-on, you may also need to configure collection rules for custom metrics. This topic describes how to configure custom collection rules.

<span id=".5qaC6L-w"></span>
## Overview

Prometheus mainly uses a pull\-based model to scrape the monitoring endpoints exposed by target services. Therefore, you need to configure corresponding service discovery rules in the cluster to specify collection targets. In this way, data can be collected and written into the workspaces of Vital Managed Service for Prometheus (VMP).

The following table describes the types of service discovery supported by VMP.


|Service Discovery Type |Description |
|---|---|
|ServiceMonitor |In the Kubernetes cluster, namespaces and labels are used to specify the services that you need to monitor. |
|PodMonitor |In the Kubernetes cluster, namespaces and labels are used to specify the Pods that you need to monitor. |
|Service/Pod annotation |In the Kubernetes cluster, you can configure specific annotations for Services or Pods to achieve service discovery. |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* VMP

   * A VMP workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* VKE

   * A cluster is created, and cloud native observability is enabled. For more details, refer to [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

   * The CRD resources have been created in the cluster. For details, see [How do I create CRD resources such as ServiceMonitor in a cluster](https://docs.byteplus.com/en/docs/vmp/How-do-I-create-Custom-Resource-Definition-resources-such-as-ServiceMonitor-in-a-cluster).


<span id="96bIOcIA"></span>
## Configuration methods

<span id="iH82aQzR"></span>
### Method 1: integration center (recommended)


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. In the left navigation pane, click **Integration Center \> Component**. On the page that appears, click **Container custom collection** to configure the integration task.

4. Configure the deployment environment of the collector. Click **VKE environment** and select an associated cluster.

5. Click **Create Integration Task** to specify the details of the integration task.

   
   |Parameter |Description |
   |---|---|
   |**Basic information** ||
   |Task name |Specify the name of the integration task. |
   |**Scrape configuration** ||
   |JobLabel |You can select labels from the objects of the associated Kubernetes Service, and the label value will be used as the job label for all metrics. For example, if you set the JobLabel parameter to `foo` and the Service label is `foo: bar`, a `job="bar"` label will be added to all collected metrics. If this parameter is left empty or the specified label does not exist, the default job label for the metrics is the name of the associated Service. |
   |Metric scraping interval |Configure the collection interval of the collector. |
   |Namespace |Specify the namespace where the collection target is deployed in the cluster. Values:<br><br><br>* **arbitrary**: indicates that metrics of resources in any namespace in the cluster can be collected.<br><br>* **custom**: indicates that you can specify custom namespaces in the cluster, and only metrics of resources in the specified namespaces can be collected. For example, if you set the value to `default`, only metrics of resources in the default namespace can be collected. |
   |Metric acquisition port |Configure the metric port for the collection target. You can set the value to a port name or a port number. |
   |Metric acquisition path |Configure the metric path of the collection target. |
   | LabelSelector |The label selector used to select the Kubernetes Service object for which metrics are to be collected. |
   |**Advanced configuration** ||
   |Metric Relabel configuration |Configure metric relabeling. For more details, refer to [Metric relabeling](https://docs.byteplus.com/en/docs/vmp/Metric_relabel). |
   

6. Click **Confirm** to complete the configuration.


<span id="jBVWm5Y7"></span>
### Method 2: custom deployment

<span id=".6YCa6L-HIFNlcnZpY2VNb25pdG9yIOWunueOsOacjeWKoeWPkeeOsA=="></span>
#### Achieve service discovery by using ServiceMonitor

You can configure service discovery for custom targets through ServiceMonitor to collect the metrics of the custom targets.

Procedure:


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the left navigation pane, click **Cluster**. In the cluster list on the right side, find the target cluster.

3. Click the name of the cluster to go to the cluster configuration page.

4. In the left navigation bar, click **Workload \> Resource Explorer**. Click **Create with Yaml** to configure service discovery through ServiceMonitor.

   * Select **Custom** from the **Type** drop\-down menu.

   * Enter the YAML configuration in the **Yaml**field.


```YAML
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: service-discover # Configure the service discovery name.
  namespace: volcano-metrics # Specify the namespace of the service discovery.
  labels: 
    volcengine.vmp: "true" # Configure the labels for the service discovery to allow the labels to be identified by the agent.
spec:
  endpoints:
  - interval: 15s # Specify the collection interval. Default value: 15 seconds.
    scrapeTimeout: 10s # Specify the collection timeout. Default value: 10 seconds.
    port: metrics # Specify the service port name. The declaration of the port name must be displayed in the configurations of the container.
    path: /metrics # Specify the URI path for metric exposure. Default value: /metrics.
    scheme: http # Configure the collection protocol. HTTP and HTTPS are supported. Default value: HTTP.
    relabelings: # Configure metric relabeling. This parameter can be omitted if it is not required.
    - targetLabel: environment 
      action: replace # In this example, a fixed label is added: environment="Production"
      replacement: Production
  namespaceSelector: # Specify the namespace of the collection target. If you do not specify this parameter, it indicates that the current namespace is selected.
    matchNames:
    - volcano-metrics 
  selector: # Specify the label value of the Service to locate and select the target Service.
    matchLabels:
      app.kubernetes.io/name: ek8s-gpu-exporter 
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more configuration item descriptions, refer to the <a href="https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api-reference/api.md#servicemonitor">official documentation of GitHub</a>.</div>



5. Click **Confirm** to complete the configuration.


After you create CRD resources in the VKE console, you can perform the following steps to view, edit, or delete the configurations of the resources:


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the left navigation pane, click **Cluster**. In the cluster list on the right side, find the target cluster.

3. Click the name of the cluster to go to the cluster configuration page.

4. Click **Workload \> Resource Explorer** in the left navigation pane. Select **CRD** from the **Category** list to view created CRD resources.

5. Click **servicemonitor** to go to the details page.

6. Find the configuration item that you want to edit or delete and click the `...` icon in the **Actions** column. Then click **Edit Yaml** or **Delete** to edit or delete the configuration item.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aa9c85bcdf5d43f333ccb3f9fb799299.png) </span>


<span id=".6YCa6L-HIFBvZE1vbml0b3Ig5a6e546w5pyN5Yqh5Y-R546w"></span>
#### Achieve service discovery by using PodMonitor

You can configure service discovery through PodMonitor to collect the metrics of custom targets.

Procedure:


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the left navigation pane, click **Cluster**. In the cluster list on the right side, find the target cluster.

3. Click the name of the cluster to go to the cluster configuration page.

4. In the left navigation bar, click **Workload \> Resource Explorer**. Click **Create with Yaml** to configure service discovery by using PodMonitor.

   * Select **Custom** from the **Type** drop\-down menu.

   * Enter the YAML configuration in the **Yaml**field.


```YAML
apiVersion: monitoring.coreos.com/v1
kind: PodMonitor
metadata:
  name: pod-discover # Configure the service discovery name.
  namespace: volcano-metrics # Specify the namespace of the service discovery.
  labels: 
    volcengine.vmp: "true" # Configure the labels for the service discovery to allow the labels to be identified by the agent.
spec: # Describe the characteristics of the target Pod for collection and the configuration of the collection task.
  podMetricsEndpoints: # Configure the Prometheus HTTP endpoints of the monitoring target. You can configure multiple endpoints.
  - interval: 15s # Specify the collection interval. Default value: 15 seconds.
    scrapeTimeout: 10s # Specify the collection timeout. Default value: 10 seconds.
    port: metric-port # Specify the container port name. The declaration of the port name must be displayed in the configurations of the container.
    path: /metrics # Specify the URI path for metric exposure. Default value: /metrics.
    scheme: http # Configure the collection protocol. HTTP and HTTPS are supported. Default value: HTTP.
    relabelings: # Configure the metric relabeling feature. You can configure multiple relabeling rules, which are executed in order.
    - action: replace # The operation after label matching. Valid values: replace, keep, and drop.
      sourceLabels: # The original labels whose values are taken for relabeling.
      - instance
      regex: (.*) # The regular expression to match the values of source labels.
      targetLabel: instance # When action is set to replace, specify the corresponding label name by using target_label.
      replacement: 'kafka-xxxxxx' # When action is set to replace, define the expression to be replaced after regular expression matching through replacement.
  namespaceSelector: # Specify the namespace of the collection target. If you do not specify this parameter, it indicates that the current namespace is selected.
    matchNames: 
    - volcano-metrics 
  selector: # Specify the label value of the collection target to locate and select the target Pod.
    matchLabels:
      app-name: kafka-exporter
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more configuration item descriptions, refer to the <a href="https://github.com/prometheus-operator/prometheus-operator/blob/main/Documentation/api-reference/api.md#podmonitor">official documentation of GitHub</a>.</div>



5. Click **Confirm** to complete the configuration.


After you create CRD resources in the VKE console, you can perform the following steps to view, edit, or delete the configurations of the resources:


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the left navigation pane, click **Cluster**. In the cluster list on the right side, find the target cluster.

3. Click the name of the cluster to go to the cluster configuration page.

4. Click **Workload \> Resource Explorer** in the left navigation pane. Select **CRD** from the **Category** list to view created CRD resources.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5f3904c38f0aa9afa640e60b2d807e8e.png) </span>

5. Click **podmonitor** to go to the details page.

6. Find the configuration item that you want to edit or delete and click the `...` icon in the **Actions** column. Then click **Edit Yaml** or **Delete** to edit or delete the configuration item.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_180b5a7537c42430898988cfae28b65a.png) </span>


<span id=".6YCa6L-HIFNlcnZpY2UvUG9kIGFubm90YXRpb24g5a6e546w5pyN5Yqh5Y-R546w"></span>
#### Achieve service discovery by using Service or Pod annotations

As mentioned above, you can use ServiceMonitor or PodMonitor for service discovery. However, if a large number of services or pods exist in the cluster, you need to create multiple ServiceMonitor or PodMonitor objects for monitoring, which makes the configuration particularly complex.

To solve the preceding issues, VMP provides you with another type of service discovery, which is achieved through Service or Pod annotations. You can add the specified annotation field when you deploy Services or Pods to quickly integrate businesses.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Service or pod annotations can quickly achieve service discovery, but some issues also exist. For example, metric relabeling cannot be achieved. You need to choose an appropriate method based on your business requirements.</div>


* <div data-tips="true" data-tips-type="warning">You cannot use Service or Pod annotations for service discovery in the kube\-system namespace. It is recommended to use ServiceMonitor or PodMonitor.</div>



When you configure Services or Pods in the cluster, you can achieve service discovery for custom targets by adding the following annotations:

```YAML
prometheus.io/scrape: "true"   # Set the value to true, which indicates that collection is enabled.
prometheus.io/port: "9400"     # Configure the port number for exposing the metrics.
prometheus.io/path: "/metrics" # Specify the URI path for metric exposure. The value is /metrics by default.
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you use <code>prometheus.io/port: "9400"</code> to specify the port number of the target, the declaration of the port must be displayed in the configurations of the container, which is shown in the following sample code.</div>


<div data-tips="true" data-tips-type="tip">```YAML
...
    spec:
      containers:
        ports:
        - containerPort: 9400 # Display the declaration of the container port in the container configurations.
```
</div>



* **Service annotation configuration example**


When you configure services in the cluster, you can add annotations to achieve service discovery. This quickly integrates the services with monitoring. You can perform the following steps to configure service discovery by using Service annotations:


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. Click **Cluster** in the left navigation pane.

3. On the cluster list page, click the name of the target cluster to go to the cluster details page.

4. In the left navigation pane, click **Services and Ingresses** \> **Service**. On the page that appears, click **Create with Yaml** to configure a service and add annotations for service discovery.


```YAML
apiVersion: v1
kind: Service
metadata:
  name: golang-service-demo
  labels: 
    app: golang-service-demo # Configure the labels of the service.
  annotations: 
    prometheus.io/scrape: "true"  # Set the value to true, which indicates that service discovery is enabled.
    prometheus.io/port: "2023"  # Specify the port number for exposing the metrics. The declaration of the port number must be displayed in the configurations of the container.
    prometheus.io/path: "/metrics" # Specify the URI path for metric exposure. The value is /metrics by default.
spec:
  selector:
    app: golang-demo
  ports:
    - protocol: TCP
      port: 2023
      targetPort: 2023
      name: metrics # Specify the service port name.
  type: ClusterIP
```



* **Pod annotation configuration example**


When you configure Pods in the cluster, you can add annotations to achieve service discovery. This quickly integrates the Pods with monitoring. You can perform the following steps to configure service discovery by using Pod annotations:


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. Click **Cluster** in the left navigation pane.

3. On the cluster list page, click the name of the target cluster to go to the cluster details page.

4. In the left navigation pane of the cluster details page, click **Workload \> Deployment**. Click **Create with Yaml** to deploy the application and add annotations for service discovery.


```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: golang-demo # Specify the name of the application.
  labels:
    app: golang-demo # Configure the labels of the application.
spec:
  replicas: 2 # Specify the number of replicas for the application.
  selector:
    matchLabels:
      app: golang-demo
  template:
    metadata:
      labels:
        app: golang-demo
      annotations: 
        prometheus.io/scrape: "true"  # Set the value to true, which indicates that service discovery is enabled.
        prometheus.io/port: "2023"  # Specify the port number for exposing the metrics. The declaration of the port number must be displayed in the configurations of the container.
        prometheus.io/path: "/metrics" # Specify the URI path for metric exposure. The value is /metrics by default.
    spec:
      containers:
      - name: golang-demo # Specify the container name.
        image: doc-cn-beijing.cr.volces.com/vmp/golang-demo:1.0 # Specify the address and version of the application image.
        ports:
        - containerPort: 2023 # Specify the container port number.
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This example shows how to configure a Deployment. This method also applies to the configuration of other types of workloads.</div>


* <div data-tips="true" data-tips-type="tip">The image address in this example is used for illustration only. You need to replace it with the image address in your actual environment.</div>


* <div data-tips="true" data-tips-type="tip">When you use Pod annotations for service discovery, HTTP and HTTPS cannot both be supported.</div>



<span id="5Unr8Ty3"></span>
## Validate results

<span id="42mShVDs"></span>
### View the integration task

After the configuration is complete, you can view the status and details of the integration task to check whether the target Kafka integration task is running as expected.


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. In the left navigation bar, click **Integration Center \> Integration task**.

4. Click **VKE environment** **.**  You can view the status of the integration task in the task list.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3bcf65d7085f473892d6b98b06901389.png) </span>

After the integration task is created, you can perform the following O&M operations:


* Click the **name of the task** to go to the task details page.

* Click **Edit** in the **Actions** column to edit the task.

* Click **Suspend task** in the **Actions** column to suspend the task.

* Click **Delete** in the **Actions** column to delete the corresponding integration task.


<span id="vPpiQeOf"></span>
### Query task metrics

Click **Explore** in the left navigation pane. On the page that appears, use the `up` statement to view the status of collection jobs for the integration task. In this example, the statement is `up{job="vmp-system/custom-***"}`. When the metric value is 1, it indicates that the collector is created and working as expected.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_106c141726aeaef9b173e91d372e43cb.png) </span>

<span id="AFeJMfS0"></span>
## Monitoring information

<span id="c3OicC41"></span>
### Query metrics

You can quickly query and display metric data by using the Explore feature of VMP. For more details, refer to [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9549a64840db2008e8fb0622c198a0b9.png) </span>

&nbsp;

<span id="HEHNQPQO"></span>
### Create dashboards

You can install Grafana in a VKE cluster or an ECS instance and then use Grafana to view metrics and create dashboards.


* [Deploying Grafana in a VKE cluster and accessing workspaces](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster)

* [Deploying Grafana on an ECS instance and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/Deploying_Grafana_on_an_ECS_instance_and_integrating_Grafana_with_a_workspace)


<span id="aP3o3hUY"></span>
### Configure alerts

You can configure alerts for monitoring targets in the Alert Center of VMP. For details, see [Creating alert rules](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules).
