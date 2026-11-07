---
title: "What is Volcengine Kubernetes Engine"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/What-is-Vital-Kubernetes-Engine"
---

Vital Kubernetes Engine (VKE) deeply integrates with the new generation of cloud\-native technologies to provide high\-performance Kubernetes container cluster management services with containers at their core. VKE enables you to create highly available Kubernetes clusters with a few clicks in the cloud, perform the visualized full\-lifecycle management of containerized applications, and quickly create containerized applications.

<span id=".5Li65LuA5LmI6YCJ5oup5a655Zmo5pyN5Yqh"></span>
## Why VKE

VKE, as a container cluster management service managed in the cloud, deeply integrates with high\-performance computing, networking, and storage services of BytePlus. The computing services include Elastic Compute Service (ECS) and Elastic Bare Metal (EBM). The networking services include Virtual Private Cloud (VPC), Elastic IP Address (EIP), and Cloud Load Balancer (CLB). The storage services include Elastic Block Storage (EBS), Torch Object Storage (TOS), and FileNAS. In addition, VKE connects to multiple cloud services, such as [Container Registry (CR)](https://docs.byteplus.com/en/docs/cr/what-is-cr), [Code Pipeline (CP)](https://docs.byteplus.com/en/docs/cp/What_is_Code_Pipeline), [Vital Managed Service for Prometheus (VMP)](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus), [Torch Log Service (TLS)](https://docs.byteplus.com/en/docs/tls/What_is_TLS). This achieves an end\-to\-end workflow for cloud\-native applications, including building, deployment, releasing, and monitoring. This way, the requirements of application\-to\-microservice transformation, DevOps\-related continuous delivery, machine learning, massive rapid autoscaling, and other scenarios can be met. The following table displays the main differences between VKE and self\-built Kubernetes and the advantages of VKE.


|Feature |Vital Kubernetes Engine (VKE) |Self\-built Kubernetes |
|---|---|---|
|Cluster management |You can quickly create clusters in the console. In addition, GPU Compute Service and EBM computing services are supported. Kubernetes versions on which stability testing and security hardening are performed are provided. |You are required to manually deploy clusters and explore and develop features by yourself. |
|Network management |High\-performance networking add\-ons are provided, and multiple networking models are supported. |You are required to select networking add\-ons in the community for adaptation. |
|Storage management |Storage services including BytePlus EBS, TOS, and FileNAS are supported and standard Container Storage Interface (CSI) add\-ons are provided. |You are required to build storage services and develop a CSI by yourself. |
|Application management |Both canary deployment and blue\-green deployment are supported. Both application monitoring and autoscaling are supported. |You are required to explore and develop the related features by yourself. |
|Operation and maintenance management |You can upgrade the Kubernetes version with a few clicks. In addition, manual scaling and autoscaling on clusters are supported. High\-performance log collection agents are supported to collect logs from containers, add\-ons, control planes, and other dimensions. VKE connects to VMP to monitor clusters, add\-ons, and applications. |You are required to manually deploy monitoring and log systems. |
|Service guarantee |A professional container support team is available in BytePlus to guarantee the normal operation of massive businesses in ByteDance, which accumulates a lot of best practices and management experience. A service level agreement (SLA) defining service availability level metrics and compensation regulations is available. |A professional service team needs to be established, with no SLA guarantee. |
|Security management |Fully managed VKE has various isolation levels with default security hardening. The all\-around network security isolation control is combined with fine\-grained access control to ensure security and high availability of services and data. |You are required to ensure environmental security. |
|Relevant service |VKE can connect to various cloud services for covering DevOps, machine learning, and other scenarios. The services include CR, CP, VMP, TLS, MSE, and big data services. |You are required to build and connect to relevant services by yourself. |


<span id=".5a655Zmo57G75Z6L"></span>
## Container types

VKE enables you to build clusters by using ECS and Vital Container Instance (VCI). In addition, you can use basic ECS and VCI resources in clusters. This way, you can flexibly select business deployment modes based on your business requirements. On this basis, VKE provides standard Kubernetes application scheduling, orchestration, and observability capabilities.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4516aeeff887b9e17fbc76699077c997.png) </span>

The following table displays the differences between containers of different types and their characteristics.


|Container type |Standard container |Elastic container |
|---|---|---|
|Infrastructure |Elastic Compute Service (ECS) |Vital Container Instance (VCI) |
|Main characteristics |* **Various nodes**: Nodes are rich in types and specifications. The supported types include x86\-based nodes, heterogeneous nodes, and bare metal nodes.<br><br>* **One\-stop container management**: Application scheduling, logging, monitoring, and operation and maintenance management are supported at the container level. You can perform one\-stop management on containerized applications, such as deploying, releasing, and monitoring.<br><br>* **Multi\-card sharing**: Each container can use the computing power and memory resources of multiple GPUs on the same node. The computing power and memory that a container can use are no longer limited to one GPU. This feature improves the utilization of GPU fragments.<br><br>* **Enhanced scheduling capability**: Various container scheduling capabilities are available, including Gang scheduling, Capacity scheduling, load\-aware scheduling, and topology\-aware scheduling. |* **Ready to use**: You can deploy applications only by submitting container images without the need to plan or create nodes. This way, you can focus on business innovation.<br><br>* **Ultra scalability**: With second\-level autoscaling, you do not need to estimate cluster capacity and business traffic in advance. Sufficient cluster capacity is provided, which ensures successful scaling.<br><br>* **Security isolation**: Built based on secure sandboxed containers, it provides virtual machine\-level security and resource isolation capabilities. This allows each instance to run in an exclusive kernel and does not share infrastructure resources with other instances.<br><br>* **Reduced cost**: You can create this type of instance based on your business requirements. It does not generate fees when it is idle because it uses the pay\-as\-you\-go billing method. This reduces your usage costs. |
|Billing method |It uses the pay\-as\-you\-go billing method. You are charged based on the usage of infrastructure resources. |It uses the pay\-as\-you\-go billing method. You are only charged based on resource usage. |
|Application scenarios |* Applications are separated into microservices.<br><br>* Agile development accelerates iteration.<br><br>* DevOps\-related continuous delivery.<br><br>* Massive rapid autoscaling. |* **Highly elastic businesses**: Businesses that have significant peak and off\-peak hours, such as live\-streaming, e\-commerce, and social media.<br><br>* **Job\-based businesses**:<br><br>   * Data processing types: big data computing, machine learning, and scientific computing.<br><br>   * Event\-driven types: video recording, transcoding, and IoT.<br><br>   * CI/CD, GitLab Runner, and Jenkins.<br><br>* **Online business management** |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on VCI and its limits, refer to <a href="https://docs.byteplus.com/en/docs/vke/What-is-Vital-Container-Instance">What is VCI</a>?</div>


<span id=".5Lqn5ZOB5p625p6E"></span>
## Service architecture


<Tabs>
<Tab zoneid="ltkesPfKt4" title="Inference architecture">
<TabTitle>Inference architecture</TabTitle>

VKE deeply integrates with the new generation of cloud\-native AI technologies to provide capabilities such as deployment acceleration, application orchestration, and resource scheduling for AI workloads.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_38fe5e0beb6dc8f2fe111ac0508b0e59.png) </span>


</Tab>
<Tab zoneid="lBnDmXFoNY" title="Model acceleration">
<TabTitle>Model acceleration</TabTitle>

By leveraging the point\-to\-point (P2P) technology and model loading tools, VKE can deploy the complete DeepSeek\-R1\-671B model on over one hundred GPUs within minutes, which greatly reduces model deployment duration.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bfd8b84c22e02ba8c7d0572aa2a1a34c.png) </span>


</Tab>
<Tab zoneid="J6QKSfv38f" title="PD disaggregation">
<TabTitle>PD disaggregation</TabTitle>

The prefill phase is separated from the decode phase, and prefill instances and decode instances can be dynamically scaled based on composite metrics.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e7d18564eece2f920533de665660c961.png) </span>


</Tab>
</Tabs>


<span id=".5a2m5Lmg6LWE5rqQ"></span>
## References


* [Terms](https://docs.byteplus.com/en/docs/vke/Terms)

* [Getting started](https://docs.byteplus.com/en/docs/vke/Quick-guide)

* [FAQs](https://docs.byteplus.com/en/docs/vke/What-is-the-general-process-of-running-applications-using-VKE)

* [Dependencies between VKE and other cloud services](https://docs.byteplus.com/en/docs/vke/Dependencies-between-VKE-and-other-cloud-services)

* [Kubernetes official website](https://kubernetes.io/)
