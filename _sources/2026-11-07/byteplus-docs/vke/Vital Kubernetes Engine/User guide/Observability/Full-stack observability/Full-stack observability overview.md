---
title: "Full-stack observability overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Full-stack_observability_overview"
---

Cloud\-native full\-stack observability uses non\-intrusive technology for applications to collect observability data such as performance metrics, API calls, and kernel events at the application layer, network layer, and kernel layer for service troubleshooting. It delivers high performance during data collection. This topic describes the architecture, advantages, and applicable scenarios of full\-stack observability.

<span id=".5LqR5Y6f55Sf5YWo5qCI6KeC5rWL5LuL57uN"></span>
## Introduction to cloud\-native full\-stack observability

Cloud\-native full\-stack observability, built on eBPF, achieves high\-performance, non\-intrusive, full\-stack data collection. It fully supports in\-depth observability at the kernel level and automatically parses application protocols such as HTTP(S), DNS, and gRPC Unary/Streaming used with the high\-performance application protocol parsing module. It integrates Kubernetes metadata to provide a non\-intrusive full\-stack observability capability at the resource, network, and application layers. In addition, data collection based on eBPF is used to construct topologies to break down observability data silos and deliver an interactive experience centered on topologies. Vertically, it uses Kubernetes native resources as an index to perform drill\-down analysis and associate metrics, logs, events, tracing, and other observability data. Horizontally, it breaks down observability data silos by using flows.

Cloud\-native full\-stack observability provides the following features:


1. **High\-performance, non\-intrusive, and full\-stack data collection built on eBPF:**  Cloud\-native full\-stack observability, built on eBPF, achieves full\-stack data collection with no code intrusion. It fully supports in\-depth observability at the kernel level and automatically parses application layer protocols such as HTTP(S), DNS, gRPC Unary/Streaming,  Redis, PG, and MySQL used with the high\-performance application layer protocol parsing module. It provides a full\-stack observability capability with no code intrusion at the resource, network, and application layers.

2. **Observability data silo breakdown through topologies:**  Cloud\-native full\-stack observability delivers an interactive experience centered on topologies based on traditional monitoring and observability models. Vertically, it uses Kubernetes native resources as an index to associate metrics, logs, events, tracing, profiling, and other observability data. Horizontally, it breaks down observability data silos by using flows and traces.


<span id=".5LqR5Y6f55Sf5YWo5qCI6KeC5rWL5p625p6E"></span>
## Cloud\-native full\-stack observability architecture

Built based on the basic observability capabilities of traditional containers, cloud\-native full\-stack observability uses eBPF to enhance full\-stack collection capabilities. It collects observability data from the kernel, runtime, storage layer, network layer, and application layer. Combined with a high\-performance application\-layer protocol resolution model, it achieves comprehensive top\-down observability coverage. Observability data is automatically associated with Kubernetes metadata, and standardized semantics are used to connect traffic with resources.

Microscope Agent functions as a core data plane add\-on for cloud\-native full\-stack observability. It supports a collection add\-on extension mechanism, which extends collection capabilities by using add\-ons. Its collection scope follows a top\-down approach, which comprehensively covers user\-space frameworks, system libraries, the network layer, the storage layer, and the runtime environment.

<span id=".5YW45Z6L5bqU55So5Zy65pmv"></span>
## Typical application scenarios

<span id=".5pyN5Yqh5ZON5bqU5oWi"></span>
### Slow service response

Slow service response is a common issue in cloud\-native environments, which is attributable to multiple causes. During troubleshooting, the common method is to first check whether the issue originates from the application or the network. After you confirm the affected scope, you can use logs, events, or kernel analysis to identify root causes.


* **Identify resources with long service response times:**  When you receive an alert or error, or when you view and sort the list of resources, a resource, such as the Deployment, StatefulSet, or Pod, with a long service response time is identified.

* **View API performance of a resource in resource details:**  View the application performance of the API for a resource to narrow the affected scope to a specific API.

* **View metrics to identify the affected scope:**  View various metrics, such as service requests, errors and exceptions, service latency, and network communication. Analyze the relationships among these metrics to identify the affected scope (application or network).

* **View single call records:**  In resource details or topology details, view single call records on both the client and server sides, including the request and response headers, body, and other metadata. Combine the data with kernel call information to further identify the affected scope.

* **View logs/events to identify root causes:**  On the Log management and Event management pages of the VKE console, view the logs and events for the corresponding resources and affected scopes to identify root causes and resolve issues.


<span id=".5pyN5Yqh5ouT5omR5oSf55-l"></span>
### Service topology awareness

As technology and deployment architectures become increasingly complex, after an issue occurs, not only issue identification but also impact analysis becomes challenging. In some cases, a topology chart is required.


* **Service relationship awareness:**  During abnormality identification, you need to know traffic entries, workloads, the running status of each workload, and whether internal or external add\-on dependencies exist. Then, you can know the affected scope and perform appropriate troubleshooting. A service topology significantly facilitates abnormality identification.

* **Dependency and impact analysis:**  During abnormality identification, the issue often occurs in downstream dependencies. When these dependencies lack sufficient observability, further analysis becomes impossible. Therefore, analyzing upstream and downstream dependencies in service topologies is crucial. A call graph is generated by associating upstream and downstream call relationships through performance metrics for application calls and network communications. The chart enables you to view dependencies and metric changes between upstream and downstream entities to quickly identify whether issues exist with upstream or downstream dependencies.
