---
title: "Observability overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Observability-overview"
---

distributed With the widespread use of Kubernetes, cloud\-native architecture poses new challenges to observability. In the context of microservices and containerization, you need to fully understand the running status of applications and Kubernetes infrastructure, quickly locate and resolve issues, and collect and analyze data on the running status of applications and clusters for continuous improvement. This ensures a secure and reliable operating environment.

This topic introduces the composition of the Vital Kubernetes Engine (VKE) observability system, as well as best practices for building a VKE observability system by using the cloud services of BytePlus.

<span id=".a3ViZXJuZXRlcy3nmoTlj6_op4LmtYvmjJHmiJg="></span>
## Observability challenges posed by Kubernetes

The Kubernetes system poses the following challenges to observability:


* **Complex architecture**: The Kubernetes system consists of the control plane and data plane, and contains various add\-ons that communicate with each other. Observability must provide comprehensive coverage.

* **Dynamic resources**: In the Kubernetes cluster, resources such as pods and services are dynamically created and assigned IP addresses. When you recreate pods, new resources and IP addresses are allocated to the pods. You need to perform dynamic monitoring on the creation and deletion of these resources, as well as the utilization of underlying resources.

* **Microservices architecture**: In the context of microservices and containerization, traditional applications are separated into multiple add\-ons based on the microservices architecture, and the replicas of each add\-on can be autoscaled based on your business requirements. Therefore, the requirements for troubleshooting are high.


In response to the observability challenges posed by the Kubernetes system, especially when cluster size quickly increases, the efficient and reliable observability capabilities of the Kubernetes system ensure system stability.

<span id=".5Y-v6KeC5rWL5oCn5p625p6E"></span>
## Observability architecture

In cloud\-native architecture, observability consists of three pillars, including **logging**, **distributed tracing**, and **metrics**.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91d76e4c52ea7e069b67f487ce3f3034.png) </span>


* **Logging**: Logs and events record discrete system behaviors and states, which can be used to analyze program behavior. When a program encounters an error, you can identify the error cause and resolve the error by using logs and events. Outputting logs is easy for an application, but collecting and analyzing logs can be complex. In scenarios with tens of thousands of cluster nodes, rapidly scrolling event information, and terabytes of text, transmission and aggregation are not simple tasks. Therefore, specialized systems need to be integrated to collect, store, view, and retrieve logs.

* **Tracing**: In cloud\-native systems where applications are deployed and managed as microservices, tracing is not limited to the call stack. An external request often requires the coordinated response of multiple internal services. In this case, the complete trace spans multiple services within the cluster. It includes both the network transmission information between services and the call stack information within each service. Therefore, tracing in cloud\-native systems is also referred to as **end\-to\-end tracing**. Tracing is mainly used for troubleshooting. For example, it helps you identify which part of the trace or which method encounters an error or is blocked, and identify whether the input and output meet expectations.

* **Metrics**: Metrics refer to the aggregation of statistics on a specific type of information in the system. For example, the usage, utilization, and quota of cluster nodes. Metrics are mainly used for monitoring and alerting. When certain metrics reach risk thresholds, alerts are triggered to enable automatic processing or to notify the administrator to intervene.


<span id=".5pel5b-X77yIbG9nZ2luZ--8iQ=="></span>
### Logging

VKE provides persistent storage and query features for cluster logs by using [TLS](https://docs.byteplus.com/en/docs/tls/What_is_TLS).


|Project |Description |
|---|---|
|Log type |Multiple types of logs for clusters and applications are supported, including:<br><br><br>* **Container log**: Container standard output logs, such as stderr and stdout logs, and container file path logs are supported.<br><br>* **Add\-on log**: The logs of the ingress\-nginx add\-on are supported.<br><br>* **Control plane add\-on log**: Control plane add\-on logs are supported. The add\-ons include kube\-apiserver, kube\-scheduler, kube\-controller\-manager, and etcd. |
|Log storage |Large volumes of data can be persistently stored, with stable performance and ease of reading and writing. |
|Retrieval and analysis |Keywords can be used to search for logs and quickly locate abnormal events. SQL can also be used for real\-time statistics and analysis of logs to quickly obtain key data. |
|Visualization |Query and analysis results can be visualized. Multi\-dimensional statistical chart types and custom interactive dashboards are supported to facilitate real\-time data monitoring and operations. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">TLS supports query and analysis in seconds for large volumes of data, provides efficient and real\-time log processing tools, facilitates the use of log data, and effectively improves operation and maintenance capabilities as well as data analysis efficiency. After a cluster fails, you can view historical log information in TLS for troubleshooting.</div>


<span id=".5LqL5Lu277yIZXZlbnRz77yJ"></span>
### Events

Kubernetes events are objects that indicate what happens within clusters, nodes, pods, or containers. These objects are typically generated in response to changes within the Kubernetes system. Kubernetes events help you understand the health status and performance of clusters. Events are generally classified into two types:


* **Warning event**: Indicates that this event transitions between unexpected states.

* **Normal event**: Indicates that the expected state is consistent with the current state.


VKE provides persistent storage and query features for cluster events by using [TLS](https://docs.byteplus.com/en/docs/tls/What_is_TLS) **.** 

<span id=".5oyH5qCH77yIbWV0cmljc--8iQ=="></span>
### Metrics

VKE achieves the collection, monitoring, and alerting of metrics for clusters, basic resources, and applications by using solutions of , such as cloud native observability (basic observability and full\-stack observability), application performance observability, and AI observability.


|Solution introduction |Solution introduction |Related documentation |
|---|---|---|
|Basic observability |Cloud native basic observability is achieved through VMP of BytePlus. It uses high\-availability collectors deployed in clusters to monitor cluster resources, control plane services, networks, and workloads.<br><br>Service discovery methods, such as ServiceMonitor and PodMonitor, can be used to achieve discovery and monitoring of custom services within clusters. |[Basic observability overview](https://docs.byteplus.com/en/docs/vke/Monitoring-overview) |
|Full\-stack observability |Cloud\-native full\-stack observability, built on eBPF, achieves high\-performance, non\-intrusive, full\-stack data collection. It fully supports in\-depth observability at the kernel level and automatically parses application protocols such as HTTP(S), DNS, and gRPC Unary/Streaming when used with the high\-performance application protocol parsing module. It integrates Kubernetes metadata to provide a non\-intrusive full\-stack observability capability at the resource, network, and application layers. |[Full-stack observability overview](https://docs.byteplus.com/en/docs/vke/Full-stack_observability_overview) |
|Application performance observability |Application performance observability, built on the APMPlus service of BytePlus, supports end\-to\-end monitoring capabilities for basic resource performance, service and code layers, and the health status of online application operations. It can be integrated with Java, Go, Python, and other applications, such as large models, LLMs, and agents, through methods such as a self\-developed agent and OpenTelemetry for end\-to\-end monitoring, which provides richer capabilities for restoring abnormal scenarios. Core features include service monitoring, trace analysis, error analysis, log monitoring, custom monitoring, alerting tasks, and other features. |[Application performance observability](https://docs.byteplus.com/en/docs/vke/Application_performance_observability) |
|AI observability |When you deploy large language models (LLMs) in a VKE cluster, you can analyze the AI profiling results of specified containers. This facilitates detection and optimization throughout the LLM life cycle, including training, inference, and optimization. |[AI Profiling](https://docs.byteplus.com/en/docs/vke/AI_Profiling) |


&nbsp;
