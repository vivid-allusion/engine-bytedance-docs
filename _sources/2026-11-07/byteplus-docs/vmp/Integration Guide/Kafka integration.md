---
title: "Kafka integration"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Kafka_Integration"
---

Vital Managed Service for Prometheus (VMP) allows you to monitor Kafka instances that are deployed in Vital Kubernetes Engine (VKE) clusters and Elastic Compute Service (ECS) instances, or Message Queue for Kafka instances. This topic describes how to monitor Kafka instances that are deployed in different environments.

<span id="hlpBpeaV"></span>
## Background

As a high\-throughput, distributed streaming platform, Apache Kafka is used for building real\-time data pipelines and streaming applications. With the publish/subscribe pattern at its core, Apache Kafka supports massive data persistence and horizontal scaling, which is used in scenarios such as log collection and event sourcing.

You can use VMP to monitor Kafka instances that are deployed in VKE clusters and ECS instances, or [Message Queue for Kafka](https://docs.byteplus.com/en/docs/kafka/what-is-message-queue-for-kafka) instances to achieve key metric alerting and optimization.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If you want to monitor the instances of Message Queue for Kafka, we recommend using the <a href="https://docs.byteplus.com/en/docs/vmp/Monitoring-cloud-services">Cloud Monitor integration</a> feature in the integration center. The feature supports the collection of cloud service metrics with a few clicks.</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e27539e482c1ae0f5853b50dd2ff47c8.png) </span>

&nbsp;

<span id="KyLPgl93"></span>
## Prerequisites


* VMP

   * A VMP workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* Elastic Compute Service (ECS)

   * A BytePlus root user has been created, and ECS has been activated.

   * The Kafka application is deployed in an ECS instance.

* Vital Kubernetes Engine (VKE)

   * VKE has been activated.

   * A cluster has been created. For details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   * The Kafka application is deployed in the VKE cluster.

   * The cloud native observability feature is enabled, and prometheus\-agent is installed in the cluster. For more details, refer to [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* Message Queue for Kafka

   * A BytePlus root user has been created, and Message Queue for Kafka has been activated.

   * A Message Queue for Kafka instance has been created. For more details, see [Creating instances](https://docs.byteplus.com/en/docs/kafka/creating-instance).

   * The endpoint address of the Message Queue for Kafka instance is obtained. For more details, refer to [Viewing endpoints](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The VMP workspace and the monitoring targets (ECS instance, VKE cluster, and Message Queue for Kafka instance) must be deployed in the same region.</div>


<span id="roLJNDQ3"></span>
## Integration methods

<span id="GnYQjZQa"></span>
### Method 1: integration center (recommended)


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. In the left navigation pane, click **Access Center \> Components**. On the page that appears, click **Kafka** and configure the integration task.

4. Specify the deployment environment of the collector.

   * When the monitoring target is deployed in the ECS instance, click **Hosting environment**.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8803dd7b651c48048137dc547b28382c.png) </span>

   * When the monitoring target is a Message Queue for Kafka instance or a self\-built Kafka instance that is deployed in the VKE cluster, click **VKE environment**.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f2683fd28dc1b38148cf47c8c4765671.png) </span>

5. Click **Create Integration Task** to specify the details of the integration task.

   * **Basic information**

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c12b487ae442fc63b2555eab65e3b4eb.png) </span>

      
      |Parameter |Description |
      |---|---|
      |Task name |Configure the name of the integration task. |
      |workspace |Select a created VMP workspace. |
      

   * **Scrape configuration**

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d764f7150456da1dfaee8bb0b0cc895f.png) </span>

      
      |Parameter |Description |
      |---|---|
      |JobLabel |Configure the label of the collection job. If this parameter is not specified, the ID of the integration task will be used as the metric by default. |
      |Metric scraping interval |Configure the collection interval of the collector. |
      |ECS VPC |Select the virtual private cloud (VPC) where the ECS instance is deployed. This parameter is required only when the monitoring target is **deployed** in the **hosting environment**. |
      |Subnet |Select the subnet of the VPC. This parameter is required only when the **monitoring target is deployed** in the **hosting environment**. |
      |Service addresses |Specify the server (broker) address for the Kafka instance. The address varies based on different environments.<br><br><br>* When the monitoring target is deployed in the ECS instance, the service address is in the format of ECS instance IP address + port number. Example: `192.168.1.10:9092`.<br><br>* When the monitoring target is deployed in the VKE cluster, you can access the Kafka instance by using ClusterIP or NodePort. For example, when you use a ClusterIP service, the address is `kafka-demo.kafka.svc.cluster.local:9092`. For more details, refer to [ClusterIP](https://docs.byteplus.com/en/docs/vke/ClusterIP) and [NodePort](https://docs.byteplus.com/en/docs/vke/NodePort).<br><br>* When the monitoring target is a Message Queue for Kafka instance, the service address is the domain name or IP address of the endpoint for the instance such as `192.168.1.10:9092`. For more details, refer to [Viewing endpoints](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints). |
      |Versions |Specify the version of the Kafka instance such as `3.9.1`. |
      |Topic Regular Filtering |Use a regular expression to collect topic metrics that meet the filter rules in the Kafka instance. |
      |Group Regular Filtering |Use a regular expression to collect group metrics that meet the filter rules in the Kafka instance. |
      |Enable SASL |Specify whether to enable Simple Authentication and Security Layer (SASL). After SASL is enabled, you need to configure the following authentication information:<br><br><br>* **SASL username**: Specify the username for SASL authentication.<br><br>* **SASL password**: Specify the password for SASL authentication.<br><br>* **SASL method**: Configure the SASL authentication method. Valid values: **PLAIN**, **SCREAM\-SHA256**, and **SCREAM\-SHA512**. |
      

6. Click **Confirm** to complete the configuration.


<span id="D2V52vNQ"></span>
### Method 2: custom deployment

You can also deploy kafka\-exporter in the VKE cluster to monitor the Kafka instance.

<span id="2A8Dt10e"></span>
#### Step 1: Deploy kafka\-exporter


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the left navigation pane, click **Cluster**. In the cluster list on the right side, find the target cluster.

3. Click the name of the cluster to go to the cluster details page.

4. Click **Workload \> Deployment** in the left navigation pane. Click **Create with Yaml** to deploy kafka\-exporter.


```Yaml
apiVersion: apps/v1
kind: Deployment
metadata: 
  name: kafka-exporter # Specify the name of the exporter.
  namespace: volcano-metrics # Specify the namespace of the exporter.
  labels: 
    app-name: kafka-exporter # Configure the labels of the exporter.
spec: 
  replicas: 1 # Specify the number of replicas for the exporter.
  selector: 
    matchLabels: 
      app-name: kafka-exporter # Change the name based on your business requirements. It is recommended to add information about the Kafka instance.
  template: 
    metadata: 
      labels: 
        app-name: kafka-exporter # Change the name based on your business requirements. It is recommended to add information about the Kafka instance.
    spec: 
      containers: 
      - args: 
        - --kafka.server=x.x.x.x:9092 # Specify the address and port number of the Kafka instance.
        image: danielqsj/kafka-exporter:latest # Pull the exporter image from Docker Hub.
        imagePullPolicy: IfNotPresent
        name: kafka-exporter # Specify the container name.
        ports:
        - containerPort: 9308 # Specify the container port number.
          name: metric-port # Specify the container port name.
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      terminationGracePeriodSeconds: 30
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For detailed parameters of kafka\-exporter, refer to <a href="https://github.com/danielqsj/kafka_exporter">kafka\-exporter</a>.</div>


<span id="PlmaUIuW"></span>
#### Step 2: Configure service discovery


1. Click **Workload \> Resource Explorer** in the left navigation pane.

2. Click **Create with Yaml** to configure service discovery by using PodMonitor.

   * Select **Custom** from the **Type** drop\-down menu.

   * Enter the YAML configuration in the **Yaml** field.


```Yaml
apiVersion: monitoring.coreos.com/v1
kind: PodMonitor
metadata:
  name: kafka-exporter # Specify the name of PodMonitor.
  namespace: volcano-metrics # Specify the namespace of PodMonitor.
  labels: 
    volcengine.vmp: "true" # Configure the labels for PodMonitor to allow the labels to be identified by prometheus-agent.
spec:
  podMetricsEndpoints:
  - interval: 30s
    port: metric-port # Specify the container port name of the exporter.
    path: /metrics # Specify the URI path for metric exposure. The value is /metrics by default if it is not specified.
    relabelings: # Configure metric relabeling. This parameter can be omitted if it is not required.
    - action: replace
      sourceLabels:
      - instance
      regex: (.*)
      targetLabel: instance
      replacement: 'kafka-xxxxxx' # Specify the ID of the Kafka instance.
  namespaceSelector:
    matchNames: 
    - volcano-metrics # Specify the namespace where the exporter is located.
  selector: 
    matchLabels:
      app-name: kafka-exporter # Specify the label value of the exporter to locate and select the target pod.
```


<span id="D2V52vNQ"></span>
## Validate results

<span id="VbdEnDmO"></span>
### View the integration task

After the configuration is complete, you can view the status and details of the task. Check whether the integration task is running as expected.


1. In the left navigation pane, click **Access Center \> access task**.

2. Click **Hosting environment** or **VKE environment.**  You can view the status of integration tasks in the task list.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ef065ce29ebc53b1bdf27ad111449493.png) </span>

After the integration task is created, you can perform the following O&M operations:


* Click the **name of the task** to go to the task details page.

* Click **Edit** in the **Actions** column to edit the task.

* Click **Suspend task** in the **Actions** column to suspend the task.

* Click **Delete** in the **Actions** column to delete the corresponding integration task.


<span id="yGZci6Hm"></span>
### Query task metrics

Click **Explore** in the left navigation pane. On the page that appears, use the `up` statement to view the status of collection jobs for the integration task. In this example, the statement is `up{job="kafka_job"}`. When the metric value is 1, it indicates that the collector is created and working as expected.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_072dc7ced2e17b6f00af90e74cfd431a.png) </span>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">当 Kafka 部署在 VKE 集群中时，采集任务的名称为<code>kafka-exporter-***</code>. You can use <code>up{job="kafka-exporter-***"}</code> to view the status of collection jobs.</div>


<span id="q4yNfLkF"></span>
## Monitoring information

<span id="4wXSEdQ8"></span>
### Query metrics

You can quickly query and display metric data by using the Explore feature of VMP. For more details, refer to [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a5b60fa728a359119eaa27c69743b2be.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For common Kafka metrics, refer to the <a href="https://kafka.apache.org/documentation/">official documentation</a>.</div>


<span id="qwdFYGIl"></span>
### Build dashboards

You can install Grafana in a VKE cluster or an ECS instance and then use Grafana to view metrics and create dashboards.


* [Deploying Grafana in a VKE cluster and accessing workspaces](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster)

* [Deploying Grafana on an ECS instance and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/Deploying_Grafana_on_an_ECS_instance_and_integrating_Grafana_with_a_workspace)


<span id="qSWY68xs"></span>
### Configure alerts

You can configure alerts for the Kafka instance in the alerting center of VMP. For details, see [Creating alert rules](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules).
