---
title: "Benefits"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Benefits"
---

Vital Kubernetes Engine (VKE) features ease of use, flexible scaling, high availability, high security, and high reliability. It can help you quickly build and deploy containerized applications to improve the efficiency and quality of your business. This topic describes the benefits of VKE and its differences from self\-built Kubernetes.

<span id=".dmtlLeS8mOWKvw=="></span>
## Benefits of VKE

<span id=".5YWo5qCI5Yqg6YCf"></span>
### Supporting AI innovation


* AI application orchestration: Inference services are orchestrated based on frameworks such as vLLM, SGLang, and Dynamo to provide efficient deployment capabilities for AI scenarios.

* AI model acceleration: The KV Cache service accelerates AI image loading and improves model performance.

* GPU resource colocation: GPU resources can be released for offline tasks during the off\-peak hours of online tasks and multiple models can be deployed on the same GPU. This improves the utilization of GPU resources.

* Resource autoscaling: Prefill and decode instances can be independently scaled to reduce scaling latency and improve token throughput.


<span id=".5Y-v6KeG5YyW5Lqk5LqS"></span>
### Visual interaction


* VKE provides an interactive interface that aligns with common user habits and offers user\-friendly guided workflows.

* The operation logic of features such as cluster management and containerized application building is simplified.

* Node management is visualized throughout the lifecycle.

* The deployment efficiency of containerized workloads is improved.

* Fine\-grained monitoring of the usage of underlying resources is performed in real time to improve the efficiency of application management.


<span id=".566A5Y2V5piT55So"></span>
### Ease of use


* A one\-stop service is provided to manage containerized applications throughout the lifecycle, including building, deployment, monitoring, and operation and maintenance. This way, you can focus on business development.

* You can create Kubernetes clusters with a few clicks on the visual interactive interface, manage multiple types of nodes, and mix virtual machines and physical machines.

* You can upgrade the Kubernetes versions of clusters and nodes with a few clicks on the Web user interface (UI).

* A standard Helm template is deeply integrated to achieve an out\-of\-the\-box experience.


<span id=".5p6B6Ie05by55oCn"></span>
### Ultra scalability


* The flexible scaling capabilities, including scale\-out, enable you to flexibly adjust resource configuration based on your business requirements and improve the scalability and reliability of the system.

* The enterprise\-level container management capabilities featuring high performance, high reliability, and ultra scalability are provided. In addition, VKE supports distributed cloud\-native capabilities, including centralized on\-premises and cloud resource management, disaster recovery, and cross\-cloud scalability.

* Vital Container Instance (VCI) is seamlessly integrated to provide Kubernetes orchestration and support startup in seconds, high\-concurrency provisioning, and secure isolation for sandbox containers.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Using VCI in VKE helps you focus on building applications. You do not need to purchase or manage underlying infrastructure such as Elastic Compute Service (ECS) instances. You are only charged for the resources consumed by your containers. For more information, refer to <a href="https://docs.byteplus.com/en/docs/vke/What-is-Vital-Container-Instance">What is VCI</a>?   </div>
   

* You can quickly configure autoscaling policies on the Web UI, which effortlessly achieves scaling for nodes and workloads. This can handle variable and sudden traffic surges during peak hours.


<span id=".56iz5a6a5Y-v6Z2g"></span>
### Stability and reliability


* To maximize the stability and availability of containerized businesses in clusters, VKE offers the following features: a fully managed container cluster environment, a high\-availability control plane, and automatic recovery and high\-availability configurations that support containers.

* A wide range of security mechanisms is provided, including network isolation, access control, and image security, to ensure the security of applications.

* Comprehensive network security isolation control and end\-to\-end data encryption are supported. Identity and Access Management (IAM) works with the role\-based access control (RBAC) authorization system. Fine\-grained permission management and complete auditing capabilities are supported.

* Efficient and reliable observability is provided to the Kubernetes systems based on BytePlus Cloud Monitor and Vital Managed Service for Prometheus (VMP).


<span id=".5Liw5a-M55qE6LCD5bqm6IO95Yqb"></span>
### Various scheduling capabilities


* The scheduling capabilities and policies of native kube\-scheduler are extended to enable you to configure the Binpack/Spread policy for nodes and GPUs.

* Various job scheduling capabilities, including Gang scheduling and Capacity scheduling, are available to improve the success rate of executing containerized applications and the utilization of cluster resources.

* You can set ResourcePolicy scheduling based on custom resource policies (ResourcePolicy) to support workloads with different priority levels.

* Pods are preferentially scheduled to nodes with lower loads through the load\-aware scheduling capability based on node load statistics to balance loads among nodes.

* The resource management capability of Kubernetes is enhanced based on Katalyst and the topology\-aware scheduling capability is available to improve resource utilization and reduce costs.


<span id=".5YWo6Z2i5oul5oqx5LqR5Y6f55Sf"></span>
### Fully compatible with cloud\-native services

Based on mainstream Kubernetes implementations in the industry, VKE is fully compatible with native Kubernetes APIs and kubectl to provide a complete set of features for containerized applications. The features include rapid deployment, policy\-based scheduling, service discovery, and dynamic autoscaling.

<span id=".5peg57yd6ZuG5oiQ"></span>
### Seamless integration

BytePlus Code Pipeline (CP), Container Registry (CR), Torch Log Service (TLS), VMP, and Cloud Monitor are seamlessly integrated to provide a one\-stop container management service.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b557f3dd04cd3f7a64087705fe8ea301.png) </span>

<span id=".dmtlLeS4juiHquW7ui1rdWJlcm5ldGVzLeWvueavlA=="></span>
## Differences between VKE and self\-built Kubernetes

VKE is certified for Kubernetes conformance and is fully compatible with native Kubernetes. Compared with the self\-managed Kubernetes, VKE leverages the stable and reliable IaaS capabilities of BytePlus, supports various workloads, provides rapid autoscaling, and helps improve resource utilization. In addition, the self\-developed VPC\-CNI add\-on connects container networks to Virtual Private Clouds (VPCs) without performance loss, which significantly improves container network performance. Combining the experience of large\-scale container practices within ByteDance, BytePlus outputs a comprehensive set of container best practices to support large\-scale clusters and scenarios featuring high scalability.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cba44f87e9eab3b5ebeca330cb8c6164.png) </span>

The following table displays the differences between VKE and self\-built Kubernetes clusters.


|Item |VKE |Self\-managed Kubernetes |
|---|---|---|
|Cost |* Master nodes in clusters are fully managed.<br><br>* A professional service is provided. |* Master nodes in clusters consume a large number of resources.<br><br>* R&D and O&M costs are high. |
|Scalability |Offers ultra scalability with high performance and reliability, including:<br><br><br>* Horizontal Pod Autoscaling (HPA) is supported.<br><br>* ClusterAutoscaler is supported.<br><br>* VCI can be seamlessly integrated to provide serverless and containerized compute services. |HPA is supported. |
|Integration of cloud services |Services such as BytePlus Application Load Balancer (ALB), Cloud Load Balancer (CLB), NAS, Torch Object Storage (TOS), TLS, and Application Mesh Service (AMS) are integrated. This provides a complete set of cloud\-based container management capabilities. |You are required to perform self\-managed integration. |
|Practice experience |* VKE is verified by a large number of users.<br><br>* Massive computing and storage resources of ByteDance are reused to achieve greater scalability and cost\-effectiveness. |You are required to practice through trial and error. |
|Performance and optimization |* High\-performance servers are provided.<br><br>* VPC\-CNI improves network performance. |Network overhead is high. |
|Security |* A professional cloud security center is available.<br><br>* Image vulnerabilities are scanned. |* Manual fixing is required.<br><br>* No immediate solution is available.<br><br>* Security issues take longer to remediate. |
