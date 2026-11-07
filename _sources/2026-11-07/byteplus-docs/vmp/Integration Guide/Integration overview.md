---
title: "Integration overview"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Monitoring-overview"
---

Vital Managed Service for Prometheus (VMP) features an excellent open source ecosystem affinity, supports cloud\-native monitoring, and supports various SDKs and exporters provided by the open source community for monitoring various environments, middleware, and custom applications. This topic describes how to integrate your business with VMP by using different methods.

<span id="N0D3VerW"></span>
## Feature modules and business processes

When your business is deployed in BytePlus, VMP provides comprehensive and user\-friendly features to help you quickly integrate your business. If you use a self\-built Internet data center (IDC) or an environment provided by a third\-party cloud provider, VMP also offers features such as collector deployment scripts and network connectivity to help you build a multi\-cloud platform for centralized metric observability with VMP at its core. The following section lists the common business deployment environments and integration steps.


* Businesses can be deployed in the following environments:

   * BytePlus

   * Self\-built IDC or third\-party cloud provider

* Businesses are integrated in the following steps:

   1. Deploy a collection agent.

   2. (Optional) Expose metrics.

   3. Configure collection.

   4. Query and use metrics.


The following figure shows the main feature modules and business processes of VMP. For business integration scenarios, the core features of VMP include:


* **VMP workspace**: The primary storage unit for metrics. You need to specify a specific workspace to send or query metrics. For more details, refer to [Selecting a workspace](https://docs.byteplus.com/en/docs/vmp/Selecting-a-workspace) and [Workspace type](https://docs.byteplus.com/en/docs/vmp/workspaces-types).

* **prometheus\-agent**: A collector that gathers infrastructure and business metrics of Vital Kubernetes Engine (VKE) clusters or self\-built Kubernetes clusters. The collected metrics can be sent to VMP workspaces.

* **Integration center**: The cloud service integration center provided by VMP for quick integration of  cloud services. For details, see [Integration center](https://docs.byteplus.com/en/docs/vmp/integration-center).


<span id="sbevmmvx"></span>
## Select an integration method based on the deployment environment

<span id="rGg74UZN"></span>
### VKE integration


1. Deploy a collection agent: Deploy the prometheus\-agent in a cluster and bind it to a workspace. For more details, refer to [VKE integration](https://docs.byteplus.com/en/docs/vmp/cluster-monitoring).

2. Expose metrics. Enable the monitoring feature for different resources in the cluster and expose the corresponding metrics based on your business requirements.



|Observability Object |References |
|---|---|
|Cluster observability |* For more details about collecting the metrics of Kubernetes resources such as nodes, workloads, and containers, refer to [Container Service Observation](https://docs.byteplus.com/en/docs/vke/VKE-observability).<br><br>* For more details about collecting the metrics of control plane agents such as APIServer, refer to [Control plane service observation](https://docs.byteplus.com/en/docs/vke/Control-plane-service-observability).<br><br>* For more details about collecting AI\-related metrics such as GPU and RDMA, refer to [AI resource observation](https://docs.byteplus.com/en/docs/vke/AI-resource-observability) and [Monitoring AI training jobs in VKE](https://docs.byteplus.com/en/docs/vmp/Monitoring-Artificial-Intelligence-training-jobs-in-Vital-Kubernetes-Engine).<br><br>* For more details about collecting other advanced VKE metrics, refer to the following topics:<br><br>   * [DNS service observability](https://docs.byteplus.com/en/docs/vke/DNS-service-observability)<br><br>   * [Ingress service observation](https://docs.byteplus.com/en/docs/vke/Ingress-observability)<br><br>   * [CNI network observation](https://docs.byteplus.com/en/docs/vke/CNI-network-observability)<br><br>   * [Image acceleration observability](https://docs.byteplus.com/en/docs/vke/Image-acceleration-observability)<br><br>   * [CR observability](https://docs.byteplus.com/en/docs/vke/Container-Registry-observability)<br><br>   * [CSI storage observation](https://docs.byteplus.com/en/docs/vke/CSI-storage-observability)<br><br>   * [Check self-healing observation](https://docs.byteplus.com/en/docs/vke/Check_Self-healing_Observation) |
|Business observability |For businesses deployed in the cluster, you can use the SDK provided by the Prometheus community to define business metrics during application development, and then monitor the internal status (including the number of requests and the number of queues) of the applications by using VMP. Supported monitoring scenarios include:<br><br><br>* Business count metrics: such as the number of requests and the number of queues<br><br>* Core logic latency: such as the time taken for external service requests<br><br><br>Refer to the following documentation:<br><br><br>* [Custom business integration](https://docs.byteplus.com/en/docs/vmp/custom-application-monitoring)<br><br>* [Go application integration](https://docs.byteplus.com/en/docs/vmp/Golang-application-access)<br><br><br>In addition, the Prometheus open source community supports SDKs for various development languages to allow you to select the appropriate SDK for business metric tracking and development. For more details, refer to the [official documentation of Github](https://prometheus.io/docs/instrumenting/clientlibs/). |
|Other observability |[Kafka integration](https://docs.byteplus.com/en/docs/vmp/Kafka_Integration) |
|Exporter observability |* If the self\-built middleware already exposes metrics in Prometheus format, you only need to configure [service discovery](https://docs.byteplus.com/en/docs/vmp/service-discovery).<br><br>* For many conventional applications, middleware, hardware, and systems, the Prometheus open source community offers multiple types of exporters for metric collection. For more details, refer to [Exporters and integrations](https://prometheus.io/docs/instrumenting/exporters/). For configuration methods, refer to the following topics:<br><br>   * [NGINX exporter integration](https://docs.byteplus.com/en/docs/vmp/Integrating-through-Nginx-Exporter)<br><br>   * [Redis exporter integration](https://docs.byteplus.com/en/docs/vmp/Integrating-through-Redis-Exporter)<br><br>   * [MySQL exporter integration](https://docs.byteplus.com/en/docs/vmp/Integrating-through-MySQL-Exporter)<br><br>   * [PostgreSQL exporter integration](https://docs.byteplus.com/en/docs/vmp/Integrating-through-PostgreSQL-Exporter)<br><br>   * [MongoDB exporter integration](https://docs.byteplus.com/en/docs/vmp/Integrating-through-MongoDB-Exporter)<br><br>   * [Elasticsearch exporter integration](https://docs.byteplus.com/en/docs/vmp/Integrating-through-ElasticSearch-Exporter)<br><br>   * [RabbitMQ exporter integration](https://docs.byteplus.com/en/docs/vmp/Integrating-through-RabbitMQ-Exporter)<br><br>* You can also create a custom exporter based on the client library provided by Prometheus. The Prometheus community officially supports languages including Go, Java, Python, and Ruby. For more details, refer to the [official documentation of Github](https://prometheus.io/docs/instrumenting/writing_exporters/). |



3. Configure custom collection: You can configure custom collection in the cluster. For more details, refer to [Service discovery](https://docs.byteplus.com/en/docs/vmp/service-discovery) and [How do I create CRD resources such as ServiceMonitor in a cluster](https://docs.byteplus.com/en/docs/vmp/How-do-I-create-Custom-Resource-Definition-resources-such-as-ServiceMonitor-in-a-cluster).

   * ServiceMonitor: [Configuring Service discovery through ServiceMonitor](https://docs.byteplus.com/en/docs/vke/Configuring-Service-discovery-through-ServiceMonitor)

   * PodMonitor: [Configuring Service discovery through PodMonitor](https://docs.byteplus.com/en/docs/vke/Configuring-Service-discovery-through-PodMonitor)

4. Query metrics.


<span id="MqJzoxSP"></span>
### Elastic Compute Service (ECS)

Elastic Compute Service (ECS) also serves as a common business deployment environment. You can deploy your business in the ECS environment. VMP allows hosted collectors to collect basic resource data and business data on the target ECS instance.

ECS can be integrated with VMP in two different ways, of which the differences are described in the following table.


|Integration methods |Integration description |Solution characteristics |References |
|---|---|---|---|
|Cloud Monitor integration |The Cloud Monitor integration tasks in the integration center are used to collect basic metrics of ECS from Cloud Monitor. |The configuration is easy. When you create a Cloud Monitor integration task, select ECS as the cloud service. However, the metric latency is relatively high because Cloud Monitor serves as an intermediary. |[Cloud Monitor integration](https://docs.byteplus.com/en/docs/vmp/Monitoring-cloud-services) |
|ECS integration |The ECS integration tasks in the integration center are used to directly collect metrics of ECS.<br><br><br>* **Basic metrics**: cloud\-monitor\-agent or open source node\-exporter can be used to obtain basic ECS metrics.<br><br>* **Business metrics**: Custom business metrics deployed in ECS can be obtained. |* Compared with Cloud Monitor integrating tasks, the collection link is shorter with lower latency. It is suitable for scenarios that are sensitive to metric latency.<br><br>* ECS metrics can be directly collected and sent to VMP workspaces. However, you need to manually enable the metrics interface in ECS, whose configuration is complex.<br><br>* It is compatible with open source node\-exporter, and you can deploy node\-exporter on ECS to collect metrics.<br><br>* In addition to basic metrics, it also supports the collection of business metrics deployed in ECS. |* [ECS integration](https://docs.byteplus.com/en/docs/vmp/ECS-monitoring)<br><br>* [Monitoring ECS instances](https://docs.byteplus.com/en/docs/vmp/Monitoring-ECS-instances)<br><br>* [Monitoring applications in ECS instances](https://docs.byteplus.com/en/docs/vmp/Monitoring-applications-in-an-ECS-instance) |


<span id="iHVGbwsY"></span>
### Other cloud services

If you need to use VMP to monitor other cloud services of , you can use one of the following methods of integrating a cloud service with VMP:


* **Cloud Monitor integration**: For cloud services that are integrated with Cloud Monitor, you can integrate Cloud Monitor with VMP to deliver a one\-stop, end\-to\-end collection and storage, and comprehensive centralized monitoring management experience. For more details, refer to [Cloud Monitor integration](https://docs.byteplus.com/en/docs/vmp/Monitoring-cloud-services).

* **Cloud services already integrated with VMP**: Some cloud services of  are already integrated with VMP and you only need to bind a workspace. For more details, refer to [Other cloud service integration](https://docs.byteplus.com/en/docs/vmp/Other_cloud_service_integration).


<span id="gW6NV3Kr"></span>
### Self\-built IDC/Third\-party clouds

When your business is deployed in a self\-built IDC or a third\-party cloud, you can also use VMP to monitor basic resources and businesses. Procedure:


1. Establish network connections:  Connect the networks of self\-built IDCs or third\-party clouds to the network of BytePlus over the public network or a dedicated connection to ensure that business environments can access VMP workspaces as expected.  For more details, refer to [Accessing a workspace over the public network by using a proxy](https://docs.byteplus.com/en/docs/vmp/Using-proxy-to-connect-workspace-form-internet) and [Accessing a workspace across clouds by using the dedicated connection and PrivateLink](https://docs.byteplus.com/en/docs/vmp/Achieving_cross-cloud_access_to_workspaces_by_using_DC_and_PrivateLink).


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Due to the long network path and poor reliability of public network access, it is recommended to only use this method during initial validation and to avoid using the method in an online production environment.</div>



2. Deploy a collection agent: Use the deployment script to deploy the VM Agent collector in a custom cluster. For more details, refer to [Monitoring custom Kubernetes clusters](https://docs.byteplus.com/en/docs/vmp/Monitoring_custom_Kubernetes_clusters).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can perform the following steps to deploy the VM Agent collector:</div>



* <div data-tips="true" data-tips-type="default">Obtain the script. For more details, refer to <a href="https://docs.byteplus.com/en/docs/vmp/Obtaining-a-script">Obtaining the script</a>.</div>


* <div data-tips="true" data-tips-type="default">Use the script. For more details, refer to <a href="https://docs.byteplus.com/en/docs/vmp/Script-use-guide">Using the script</a>.</div>


* <div data-tips="true" data-tips-type="default">Deploy the VM Agent collector. For more details, refer to <a href="https://docs.byteplus.com/en/docs/vmp/Deploying-the-VM-Agent">Deploying VM Agent</a>.</div>


* <div data-tips="true" data-tips-type="default">Perform O&M. For more details, refer to the following topics:</div>


   * <div data-tips="true" data-tips-type="default"><a href="https://docs.byteplus.com/en/docs/vmp/Managing-the-VM-Agent">Managing VM Agent</a></div>


   * <div data-tips="true" data-tips-type="default"><a href="https://docs.byteplus.com/en/docs/vmp/Scaling-up-components">Agent scale\-out</a></div>


   * <div data-tips="true" data-tips-type="default"><a href="https://docs.byteplus.com/en/docs/vmp/Alerting-and-maintenance-suggestions">Alerting and O&M suggestions</a>.</div>


3. (Optional) Expose metrics. Expose the basic and business metrics of Kubernetes clusters based on your business requirements.



|Observability Project |References |
|---|---|
|Cluster basic observability |* When you deploy the VM Agent collector by using the script, node\-exporter (node metrics) and kube\-state\-metrics ( operational status metrics of Kubernetes resources) are also installed by default. kubelet/kubelet\-cadvisor (container runtime statistics metrics) is also installed by default. Therefore, after you deploy the prometheus\-agent by using the script, it will automatically collect container basic metrics of the custom Kubernetes cluster.<br><br>* For other metrics, you need to deploy the exporter based on the actual cluster environment and configure collection. For more details, refer to [Service discovery](https://docs.byteplus.com/en/docs/vmp/service-discovery). For example, if you need to monitor the GPU in your custom cluster, refer to [Monitoring GPU in custom Kubernetes clusters](https://docs.byteplus.com/en/docs/vmp/Using-VMP-to-monitor-Graphics-Processing-Units-in-a-self-built-cluster). |
|Business observability & middleware observability |The configuration method is consistent with that of VKE cluster observability. For more details, refer to the preceding content. |



4. Configure collection.


<span id="SI4sZXpw"></span>
### Third\-party cloud service

If your business is deployed on a third\-party cloud service, you can also use VMP to monitor the cloud service and business. For an example, refer to [Monitoring Tencent Cloud resources](https://docs.byteplus.com/en/docs/vmp/Monitoring_Tencent_Cloud_resources).

<span id="ezLMcyzT"></span>
## Query metrics

<span id="Nf1Y6n9Q"></span>
### Query methods

VMP supports the query syntax of open source Prometheus. You can query service metrics by using [PromQL](https://docs.byteplus.com/en/docs/vmp/What-is-PromQL) statements. You can query metrics by using one of the following methods:


* Query metrics by writing code. For more details, refer to [Using the Go language to write and query data in workspaces](https://docs.byteplus.com/en/docs/vmp/Writing_and_querying_workspace_data_using_Golang).

* Query metrics by using the Explore feature of VMP. For more details, refer to [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).

* Query metrics by using Grafana.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can deploy custom Grafana in VKE clusters and ECS instances. For more details, see <a href="https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster">Deploying Grafana in a VKE cluster and accessing workspaces</a>, and <a href="https://docs.byteplus.com/en/docs/ecs/Deliver_instance_monitoring_information_to_Entrusted_Prometheus_service">Delivering instance monitoring data to VMP</a>.</div>


<span id="KGkNnbVv"></span>
### Metric list

The following table shows the metrics of common  services.


|Product name |Metric list |
|---|---|
|Vital Kubernetes Engine (VKE) |* Basic metrics: [API server metrics](https://docs.byteplus.com/en/docs/vmp/Common-metrics-of-Vital-Kubernetes-Engine)<br><br>* For more details of metrics, refer to the following topics:<br><br>   * [official documentation of node-exporter](https://github.com/prometheus/node_exporter)<br><br>   * [official documentation of kube-state-metrics](https://github.com/kubernetes/kube-state-metrics/tree/main/docs)<br><br>   * [official documentation of cAdvisor](https://github.com/google/cadvisor/blob/master/docs/storage/prometheus.md)<br><br>   * [official documentation of DCGM](https://docs.nvidia.com/datacenter/cloud-native/gpu-telemetry/latest/index.html) |
|Elastic Compute Service (ECS) |For more details, refer to [ECS metrics](https://docs.byteplus.com/en/docs/vmp/ecs-metrics). |
|Cloud Monitor |For more details, refer to [Cloud Monitor metric queries](https://console.byteplus.com/cloud_monitor/docs).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If Cloud Monitor is integrated with VMP, when the metrics from Cloud Monitor are written into a VMP workspace, the metrics are appended with the suffix <code>SubNamespace_Namespace</code>. The metric names are in the following format: <code>MetricName_SubNamespace_Namespace</code>. Example: <code>CPUUser_Instance_VCM_ECS</code>.</div><br> |
|Microservices Engine |For more details, refer to [Microservices Engine metrics](https://docs.byteplus.com/en/docs/vmp/Common-metrics-of-Microservices-Engine). |
|API Gateway |Refer to [API Gateway metrics](https://docs.byteplus.com/en/docs/vmp/Basic-metrics-of-API-Gateway). |


<span id="6vZp76xC"></span>
### Monitoring dashboard


1. VMP provides monitoring dashboards for common services, including:

   * VKE cluster resource dashboard

   * Preset cloud service dashboard. For more details, refer to [Preset dashboard](https://docs.byteplus.com/en/docs/vmp/Dashboard-overview).

2. Use Grafana. You can deploy Grafana and construct monitoring dashboards. You can deploy Grafana in VKE clusters or self\-built Kubernetes clusters.

   * Deployment: [Deploying Grafana in a VKE cluster and accessing workspaces.](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster)


<span id="WyisS9sD"></span>
### Advanced usage


* Cross\-workspace query: [Creating an aggregation query workspace](https://docs.byteplus.com/en/docs/vmp/Creating_an_aggregate_query_workspace).

* Cross\-region query: [Achieving cross-region access to workspaces by using CEN and PrivateLink](https://docs.byteplus.com/en/docs/vmp/Achieving_cross-region_access_to_workspaces_by_using_CEN_and_PrivateLink).


<span id="u5vyyI47"></span>
## Common FAQs

<span id="R8Q49qEB"></span>
### **How do I troubleshoot if I cannot query the expected metric?** 

Refer to [Why am I unable to view expected metrics?](https://docs.byteplus.com/en/docs/vmp/unable-to-query-expected-metrics)

<span id="i026Q1wy"></span>
### **How do I expose metrics?** 

Prometheus mainly pulls metric endpoints on a scheduled basis.


* If your business references the Prometheus SDK, you can develop by yourself to expose a metrics port.

* If the service does not expose metrics, you can use Exporter to call the service interface or data to obtain original metrics and then convert the metrics into Prometheus format to expose a metrics port.


<span id="VDHQtDZS"></span>
### **How do I collect metrics?** 

In most cases, VMP uses the prometheus\-agent to collect metrics and send the metrics to the specified workspace.

<span id="bv69MMlx"></span>
### **How do I know which metrics of which services to collect?** 

Native Prometheus supports the configuration of various service discovery jobs. For more details, refer to the [official documentation of Prometheus](https://Prometheus.io/docs/Prometheus/latest/configuration/configuration/).

In the Kubernetes cluster, prometheus\-operator is often introduced to use Custom Resource Definition (CRD) to define the collection configuration. For more details, refer to the [official documentation of Prometheus](https://Prometheus-operator.dev/docs/api-reference/api/).

Commonly used CRD resources include:


* ServiceMonitor

* PodMonitor


In addition, you can also quickly configure collection by using service/pod annotations. For more details, refer to [Service discovery](https://docs.byteplus.com/en/docs/vmp/service-discovery).
