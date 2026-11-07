---
title: "Upstream overview"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Upstream_overview"
---

Upstream is an abstraction of the backend of an APIG instance. You can abstract backend applications with the same functionality as an Upstream, enabling decoupling of routing and backend applications, and providing more flexible support for scenarios such as canary release and multi\-version management of backend applications. This article explains the concept and role of Upstream.

<span id=".57G75Z6L"></span>
## Type

The API gateway currently supports multiple upstream types. Detailed descriptions are provided in the following table.


|**Upstream type** |Descriptions |
|---|---|
|Elastic Compute Service |* Supports connecting to BytePlus Elastic Compute Service (ECS) instances. You can group multiple ECS instances within the same VPC as a single Upstream to serve as the gateway routing backend. When the API gateway receives traffic, it can distribute the traffic to different Elastic Compute Service instances based on a load balancing strategy.<br><br>* An Upstream of the Elastic Compute Service type can represent multiple Elastic Compute Service servers. |
|Vital Kubernetes Engine |* Supports integration with Vital Kubernetes Engine (VKE). You can encapsulate services deployed in a VKE cluster as an Upstream, which serves as the backend for gateway routing.<br><br>* The API gateway can automatically aggregate all Services with the same name from every cluster in the upstream source—that is, Services with identical Namespace, Service, and Port names—and treat them as a single application. Implement traffic management within and across clusters by combining Upstream configuration and routing weight configuration.<br><br>* A Vital Kubernetes Engine\-type Upstream can abstract Services with the same name in one or more clusters. |
|Function Service |* Supports connection to BytePlus's Function Service, triggering function code logic via HTTP or HTTPS traffic over public or private networks. You can encapsulate a published function as an Upstream to serve as the backend for gateway routing. When the API gateway receives traffic, the current function will be triggered and executed, and its execution result will be returned to the API gateway.<br><br>* A Function Service type Upstream can abstract a function. |
|Fixed domain name |* Support connecting to fixed domain names. When the API gateway receives traffic, it can forward the incoming traffic to a specified domain name.<br><br>* An Upstream of the fixed domain name type can represent a domain name. |
|Static IP |* Supports connecting to a fixed IP and allows access traffic to be forwarded to a fixed IP address. When the API gateway receives traffic, it can distribute the traffic to different IP addresses based on a load balancing strategy.<br><br>* An Upstream of the fixed IP type can represent multiple IP addresses. |


<span id=".5L2_55So5Zy65pmv"></span>
## Application scenarios


* **Traffic distribution across upstream types**

   A route supports connecting to multiple upstream types. By configuring the traffic weight of multiple upstreams in routing, you can achieve traffic distribution across upstream types. For example: application deployment across upstream types, and application migration.

* **Canary release and multi\-version management**

   A route can connect to multiple upstreams. By configuring the traffic weights of multiple Upstreams in the routing configuration, you distribute traffic among them. For example, multiple versions of an application are deployed on multiple groups of Elastic Compute Service instances, with each group abstracted as an Upstream to achieve multi\-version management of the application.

* **Traffic management across K8S clusters**

   A group of applications with the same Namespace, Service, and Port across multiple K8S clusters is abstracted as a single Upstream. At this point, the API gateway's routing only needs to connect to a single Upstream to achieve cross\-cluster traffic management. For example, application high\-availability deployment scenarios, such as deploying an application in namespaces with the same name across multiple clusters, or deploying multiple versions of an application in namespaces with the same name across multiple clusters.

* **Traffic management within the K8S cluster**

   In practical applications, traffic management within a K8S cluster and traffic management across K8S clusters can be combined. For example, in a high\-availability deployment of an application, during updates, multiple canary label versions are deployed in the same K8S cluster and namespace. At this point, you can further configure multiple canary versions of the current application on the API gateway side, based on the labels set on the VKE side (corresponding to `spec.template.metadata.labels` in the Deployment YAML). Subsequently, by configuring, in the routing, the traffic weights for multiple canary labels under the current Upstream, traffic can be distributed among multiple versions within the cluster.
