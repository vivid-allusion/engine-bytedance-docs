---
title: "Best practices for container scenario observability"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Best_practices_for_container_scenario_observability"
---

Anomalies in a Kubernetes cluster may come from the control plane, nodes, network, storage, workloads, or applications themselves. Production environments require an observability system that covers the control plane, data plane, and business systems. You need to combine information, such as metrics, Kubernetes events, and logs, to understand the system status. This topic first describes the basics of Kubernetes observability and the observability capabilities provided by VKE, and then describes best practices for observing the control plane, data plane, and business systems.

<span id="wxjonMxe"></span>
## Kubernetes observability basics

Anomalies in Kubernetes may occur at different layers. Understanding these layers and the commonly used observability signals helps clarify what each observability capability is designed to address. Observability in a Kubernetes cluster is not only used for post\-incident troubleshooting but also for early risk detection, failure recovery support, and continuous performance analysis and capacity optimization.

<span id="f01B0hF5"></span>
### Observability layers

From the perspective of observability, a Kubernetes cluster can be divided into three layers: the control plane, data plane, and business systems. Each layer has different responsibilities and emits different signals, and anomalies across layers can affect one another. For example, insufficient node resources may prevent Pods from being scheduled, network anomalies may cause application access failures, and a running Pod does not necessarily mean that the business system is healthy. Therefore, complete Kubernetes observability requires attention to the control plane, data plane, and business systems simultaneously. You cannot determine whether clusters and services are healthy only based on basic resource metrics such as CPU and memory.

The following table describes the main observability targets and focus areas for each layer:


|Observability layer |Observability target |Observability focus |
|---|---|---|
|Control plane |Control plane components such as kube\-apiserver, kube\-scheduler, kube\-controller\-manager, and etcd. |Whether core capabilities such as cluster API, resource scheduling, and state reconciliation are functioning normally. |
|Data plane |Nodes, networks, storage, GPU/RDMA, and components deployed in the cluster. |Whether cluster resources are sufficient to properly host and support workload execution. |
|Business systems |Workloads, Pods, containers, and business applications. |Whether application containers in the cluster are running normally and whether business services are healthy. |


<span id="g14AN3C9"></span>
### **Observability data types**

When analyzing the operation of a Kubernetes cluster and its workloads, you typically need to use multiple types of observability data together. Different data types focus on different aspects. Relying on any single type alone can only reflect a partial picture, making it difficult to determine the scope of impact or the root cause. Combining metrics, logs, and Kubernetes events is what enables a complete analysis chain during troubleshooting.


|Observability target |Main purpose |
|---|---|
|Metric |Continuously monitor the status of cluster resources, components, Kubernetes objects, and services, and use the data for dashboards and alerts.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Metrics can include basic resource metrics such as CPU and memory, component running metrics, Kubernetes object status metrics, and business metrics such as request volume, error rate, and latency. Observing an anomaly in a single metric typically only describes a symptom. To determine the scope of impact and the root cause, you need to cross\-analyze it with other observability data.</div><br> |
|Log |Record detailed information about the runtime behavior of components or applications. |
|Kubernetes events |Record events that occur during the lifecycle of Kubernetes objects, such as scheduling, startup, and volume mounting.<br><br>When analyzing specific Kubernetes objects, you also need to check the current status of those objects to confirm whether the actual runtime behavior matches expectations. When an anomaly occurs, the typical approach is to first detect the issue through metrics, then progressively identify the cause using Kubernetes events, object states, and logs. Metrics, Kubernetes events, logs, and Kubernetes object states each focus on different aspects, so they are generally used in combination during analysis. |


<span id="Qcu0CuEc"></span>
## VKE observability capabilities

VKE provides end\-to\-end cluster observability capabilities, including metric monitoring, log collection, Kubernetes event management, and alerting. VKE is deeply integrated with observability services such as Cloud Monitor and Torch Log Service (TLS) to help you promptly detect anomalies, quickly locate issues, and continuously optimize cluster performance. For more information, see [Observability overview](https://docs.byteplus.com/en/docs/vke/Observability-overview).

<span id="XBC7coiI"></span>
### Metric

Metrics continuously record the runtime status of clusters, components, Kubernetes objects, and business workloads as time series data, serving as the data foundation for building monitoring dashboards and configuring alerts. By continuously collecting and analyzing metrics, you can promptly detect resource bottlenecks, component anomalies, and business performance degradation, and perform capacity planning and trend analysis based on historical data.

VKE is integrated with [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus?lang=en). After enabling cloud\-native observability, you can use VMP to collect, store, and query Kubernetes\-related metrics. Based on these metrics, VKE provides observability capabilities for container services and scenarios such as the control plane, network, storage, and AI. For Prometheus\-format metrics exposed by your business applications, you can also use the service discovery capability of VKE to discover and collect metrics. For details, see the following documentation:


* [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability)

* [Service discovery](https://docs.byteplus.com/en/docs/vke/Service-discovery)


<span id="6kszHSCh"></span>
### Log

Logs record detailed information about the runtime behavior of Kubernetes components and business applications in text form, serving as the primary basis for identifying the root cause of specific errors. Compared with metrics, logs carry richer context and can directly reflect error stacks, request parameters, and abnormal states. Logs are suitable for in\-depth investigation of issues that metric alerts cannot cover.

VKE is integrated with [TLS](https://docs.byteplus.com/en/docs/tls/What_is_TLS?lang=en), which provides log collection, storage, retrieval, and analysis capabilities.  


* [Container logs](https://docs.byteplus.com/en/docs/vke/Collecting-container-logs?lang=en): Collect standard output logs and file logs generated by containers running in the cluster.

* [Control plane component logs](https://docs.byteplus.com/en/docs/vke/Collecting-control-plane-add-on-logs?lang=en): Collect logs of control plane components such as kube\-apiserver, kube\-scheduler, kube\-controller\-manager, and etcd.


<span id="9QFVVBqW"></span>
### Kubernetes events

Kubernetes events are natively generated by the Kubernetes control plane. They record state changes and anomalies of various objects in the cluster during lifecycle processes such as scheduling, startup, and scaling. Unlike logs and metrics, Kubernetes events come directly from the control plane and can reflect underlying infrastructure issues such as scheduling failures, insufficient resources, and image pull failures. They are an effective supplement to metrics and logs.

VKE supports viewing native Kubernetes events in clusters. By default, events are retained only for a short period. For long\-term storage and historical queries, you can use event persistence to synchronize event data to [TLS](https://docs.byteplus.com/en/docs/tls/What_is_TLS?lang=en). For details, see [Configuring and viewing persistent events](https://docs.byteplus.com/en/docs/vke/Configuring-and-viewing-persistent-events).

<span id="UPMzCC5G"></span>
### Alerting

In a cloud\-native system, alerts are an important way to ensure stable cluster operation. Unlike traditional alerts that focus primarily on CPU and memory usage, alerts in cloud\-native scenarios come from a wider range of sources: from infrastructure\-level resource monitoring metrics, to application\-level log content, and to native Kubernetes cluster events. These alerts provide broader coverage and finer granularity. For different types of observability data, VKE supports multiple alerting methods to address different monitoring requirements and O&M scenarios, as shown in the following table:


|Observability data types |Alert capability description |References |
|---|---|---|
|Metric |Provide metric\-based alerting capabilities through VMP, with alert configuration and preset alert templates tailored for Kubernetes scenarios. |* [Configuring alerts](https://docs.byteplus.com/en/docs/vke/Configuring_alerts)<br><br>* [Preset alert templates](https://docs.byteplus.com/en/docs/vke/Preset_alert_templates) |
|Logs/Events |Provide log/event\-based alerting through TLS, allowing you to configure alert policies based on log search and analysis results. |* [Quickly configuring log-based alerts](https://docs.byteplus.com/en/docs/tls/Quickly_set_up_log_alarm)<br><br>* [Creating alert policies](https://docs.byteplus.com/en/docs/tls/create_alarm_policies) |


<span id="1a3FITxA"></span>
## Observability best practices

When you build a Kubernetes observability system in a production environment, we recommend following these principles:


* **Cover key layers**: Focus on the control plane, data plane, and business systems simultaneously. Avoid focusing only on a single component or basic resource metrics.

* **Build based on the actual scope of use**: Establish corresponding observability capabilities as needed based on the networking, storage, AI resources, and VKE add\-ons actually used by the cluster, to avoid unnecessary investment.

* **Focus on the final business status**: In addition to the status of Kubernetes objects and infrastructure, core business workloads require business metrics and alerts that reflect service quality.

* **Use multiple observability signals together**: When an anomaly occurs, cross\-analyze metrics, Kubernetes object states, events, and logs rather than relying on a single signal.


<span id="NugnkrmW"></span>
### Control plane

The Kubernetes control plane is responsible for core functions such as cluster APIs, resource scheduling, state reconciliation, cloud resource control, and metadata storage. Its main components include kube\-apiserver, kube\-scheduler, kube\-controller\-manager, cloud\-controller\-manager, and etcd. Control plane anomalies may affect operations such as resource creation, scaling, scheduling, and state updates.

In day\-to\-day monitoring, we recommend focusing on the runtime status of control plane components, API request latency and error rates, and etcd read/write performance and storage capacity. For details, see [Control plane service observability](https://docs.byteplus.com/en/docs/vke/Control-plane-service-observability). To further analyze control plane component logs, you can ingest the logs into TLS for analysis and alerting. For more information, see [Collecting control plane component logs](https://docs.byteplus.com/en/docs/vke/Collecting-control-plane-add-on-logs).

<span id="XwCiIt9y"></span>
### Data plane

The data plane is responsible for actually hosting business workloads. Based on actual cluster usage, you need to establish observability capabilities for nodes, networks, storage, AI resources, and VKE components deployed in user clusters.

<span id="etXShYYr"></span>
#### Nodes

Node anomalies may make Pods on the node unavailable and may also affect the normal startup of new Pods. In addition to CPU, memory, and disk usage, you need to monitor whether nodes are in the Ready state and whether abnormal conditions (such as disk pressure and memory pressure) exist.

With [container service observability](https://docs.byteplus.com/en/docs/vke/VKE-observability), you can view the node status and the usage of resources, such as CPU, memory, and disk.  


* Whether nodes are running normally.

* Whether there are anomalies or capacity risks in resources such as CPU, memory, and disk.


In addition to basic status and resource usage, you also need to monitor the status of key node components. For node failures related to the kubelet, runtime, GPU, and other components, you can use the check and self\-healing observability capability provided by VKE. For details, see [Check and auto-recovery observability](https://docs.byteplus.com/en/docs/vke/Check_Self-healing_Observation).

<span id="IfMhQMSr"></span>
#### Network

Kubernetes networking involves different paths such as service discovery, business ingress, and Pod networking. You can establish observability capabilities for scenarios such as DNS, Ingress, and CNI. Network issues are often reflected as access timeouts, connection failures, or DNS resolution anomalies. Therefore, during observability, you need to check the status of network components and determine the actual impact based on business request results. The following table describes the details.


|Observability target |Scenario description |References |
|---|---|---|
|DNS |DNS anomalies may affect Service access and domain name resolution. If your workloads depend on cluster DNS, you can use DNS service observability to view DNS\-related runtime status. |[DNS service observability](https://docs.byteplus.com/en/docs/vke/DNS-service-observability) |
|Ingress |For applications that expose services externally through Ingress, you need to monitor the runtime status of Ingress itself in addition to the backend workloads and Pods. |* [Ingress service observability](https://docs.byteplus.com/en/docs/vke/Ingress-observability)<br><br>* [Best practices for observability of custom Nginx Ingress controllers](https://docs.byteplus.com/en/docs/vke/Best-practices-for-monitoring-custom-Nginx-Ingress-controllers) |
|CNI |CNI network anomalies may affect communication between Pods and access from Pods to other services. |[CNI network observability](https://docs.byteplus.com/en/docs/vke/CNI-network-observability) |


<span id="GvR9kyYu"></span>
#### Storage

For storage, you can focus on CSI components, the storage path, and the storage usage of containers. Storage issues can manifest as mount failures, unavailable volumes, or insufficient container filesystem or ephemeral storage. Therefore, you need to monitor both component status and actual usage.


|Observability target |Scenario description |References |
|---|---|---|
|CSI storage |CSI components and related storage paths. |[CSI storage observability](https://docs.byteplus.com/en/docs/vke/CSI-storage-observability) |
|Container storage |Usage of container filesystems and ephemeral storage for Pods. |[Container storage observability](https://docs.byteplus.com/en/docs/vke/Container_storage_observability) |


<span id="Y39z9mqB"></span>
#### AI resources

For workloads that use AI infrastructure resources such as GPU and RDMA, you need to monitor not only the status of Kubernetes objects but also the status and usage of the underlying acceleration resources.  


* [AI resource observability](https://docs.byteplus.com/en/docs/vke/AI-resource-observability?lang=en): Monitor AI infrastructure resources (such as GPU and RDMA) in clusters.

* [AI training job monitoring](https://docs.byteplus.com/en/docs/vke/Monitoring-AI-training-Jobs?lang=en): Monitor the status and resource usage of AI jobs in clusters from the dimension of AI training jobs.


<span id="mKGF5I4r"></span>
### Business systems

When you build an observability system for business systems in a production environment, focus on the following aspects:


* **Runtime status**: Whether Workloads, Pods, and containers are running normally.

* **Application status**: Whether applications can provide services normally and whether business metrics meet expectations.


Normally\-running Kubernetes objects do not necessarily mean that the underlying business and services are functioning correctly. Therefore, business system observability is more than just checking whether workloads, Pods, and containers are alive. You also need to monitor request success rates, latency, and whether key dependencies are healthy.

<span id="4DIjzaqN"></span>
#### Workloads, Pods, and containers

Workloads, Pods, and containers reflect the runtime status of services in Kubernetes. With [container service observability](https://docs.byteplus.com/en/docs/vke/VKE-observability), you can view runtime status and resource usage at the workload, Pod, and container levels.  


* Whether workloads are running normally.

* Whether Pods and containers are in the expected state.

* Whether resource usage, such as CPU and memory usage, is abnormal.


When a Pod or container enters an abnormal state such as `Pending`, `CrashLoopBackOff`, `ImagePullBackOff`, or `OOMKilled`, you can analyze the specific cause based on Kubernetes object states, events, and logs. These anomalies usually indicate issues at different stages, such as scheduling, startup, image pulling, resource limits, or process execution. The troubleshooting direction should be determined based on the stage at which the anomaly occurs.

<span id="0HhxogHk"></span>
#### Business applications

For core services, in addition to the runtime status of Kubernetes objects, you need to observe the final service quality from a business perspective.  


* Request volume.

* Request error rate.

* Request latency.

* Business success rate.

* Key downstream dependencies.


These metrics need to be defined based on your specific business requirements. You should first use business metrics to determine whether the final business service is functioning normally, and then analyze the root cause using Kubernetes and infrastructure\-related information. For core services with clear service level objectives (SLOs), you can further build monitoring and alerting based on SLOs.

If your business already exposes Prometheus\-format metrics, you can use the cluster [service discovery](https://docs.byteplus.com/en/docs/vke/Service-discovery) capability to discover and collect metrics. ServiceMonitor and PodMonitor address Prometheus metric discovery and collection, but they do not constitute a complete application observability system. To further observe application\-layer, network\-layer, and other information, you can use full\-stack observability capabilities. For details, see the following documentation:


* [Full-stack observability overview](https://docs.byteplus.com/en/docs/vke/Full-stack_observability_overview)

* [Enabling full-stack observability](https://docs.byteplus.com/en/docs/vke/Network-and-application-observability)
