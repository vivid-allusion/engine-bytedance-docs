---
title: "Guide to selecting EMR product forms"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Guide_to_selecting_EMR_product_forms"
---

<span id="03d48748"></span>
## Introduction to EMR deployment types

BytePlus E\-MapReduce (EMR) offers multiple deployment modes, including those based on ECS instances, VKE clusters, and Serverless architecture. Different deployment types vary in use cases, product features, billing methods, and SLA, and are designed for different users.


|Product form |Service mode |Customer maintenance scope |Product maintenance scope |Product features |
|---|---|---|---|---|
|EMR Serverless |Fully managed |* Correctness and stability of the business workflow logic |* Stability of the job execution infrastructure, such as compute, storage, and network<br><br>* Stability of the open\-source component service itself<br><br>* Stability and reliability of the product console and OpenAPI |* Maintenance is easy for customers, as only business\-related jobs require maintenance.<br><br>* Low flexibility of the execution environment |
|EMR on VKE |Semi\-managed |* Correctness and stability of the business workflow logic<br><br>* Stability of the open\-source component service itself<br><br>* Stability of the job execution infrastructure, such as Kubernetes clusters, storage, and network |* Stability and reliability of the product console and OpenAPI |* Maintenance costs are higher compared to the Serverless form<br><br>* High flexibility of the execution environment |
|EMR on ECS ||* Correctness and stability of the business workflow logic<br><br>* Stability of the open\-source component service itself<br><br>* Stability of the job execution infrastructure, such as compute, storage, and network |* Stability and reliability of the product console and OpenAPI |* Maintenance costs are higher compared to the Serverless form<br><br>* High flexibility of the execution environment |


<span id="162026d4"></span>
## Detailed description of EMR types

<span id="14bd2d25"></span>
### EMR Serverless

EMR Serverless is a fully managed service that is fully compatible with open source, featuring out\-of\-the\-box usability, second\-level elasticity, zero maintenance, and custom images, enabling users to focus more on their business. The EMR Serverless deployment mode is suitable for cloud data warehouses, hybrid cloud data warehouses, large model data preprocessing, offline inference for large models, and many other use cases. With the Serverless architecture, users only need to configure computing requirements and do not need to be aware of underlying infrastructure details or maintenance. Big data and AI developers can also easily use the EMR Serverless service.

<span id="274e623e"></span>
#### **Fully managed service**

EMR Serverless provides fully managed multi\-engine services for Spark, Ray, Presto, Doris, StarRocks, and more, with 100% open source compatibility. Users do not need to worry about maintaining underlying infrastructure and can focus on their business.

<span id="1f1003ba"></span>
#### **Second\-level scaling**

Users can achieve second\-level computing capacity expansion during expected and unexpected business peaks by configuring elastic resources for queues, meeting rapid business growth needs. Using elastic resources reduces the need for fixed, always\-on resources, improves overall resource utilization, and decreases unnecessary idle resource costs.

<span id="6ab17e83"></span>
#### **Custom environment**

Users can flexibly add custom libraries and Python packages based on the EMR base image to build custom images tailored to their needs.

<span id="79fa0ffe"></span>
#### **SLA**

[EMR Serverless 服务等级协议](https://docs.byteplus.com/docs/undefined/68da347342e561058e056cdb)

<span id="7098de5e"></span>
#### Billing method

Supports three billing methods: Pay\-As\-You\-Go, Subscription, and Subscription plus Pay\-As\-You\-Go. For details, see [EMR Serverless billing items](https://www.volcengine.com/docs/6491/1391986).

<span id="b1a3aeb3"></span>
### EMR on ECS

EMR's semi\-managed mode based on ECS provides a more comprehensive set of over 36 big data ecosystem components, including Hadoop and Spark. Computing and storage resources belong to the user, who can log in to ECS for custom operations. This mode features storage\-compute separation, minute\-level elasticity, and flexible self\-maintenance. This deployment mode allows users to better control the infrastructure and utilize ECS features, such as Spot Instance and Elastic Scheduled Instance (ESI). The advantage of this deployment mode lies in its control and flexibility. EMR on ECS is suitable for use cases such as cloud\-native data lakehouse, real\-time data warehouse, offline or batch data analysis, and real\-time or streaming computation.

The EMR on ECS deployment mode requires users to maintain the underlying resources and EMR cluster themselves. Users need to have experience in big data operations and maintenance. To resolve product usage issues, you can submit a ticket for assistance. To obtain professional big data solutions and training services, you can purchase as needed.

<span id="79f964a5"></span>
#### **ECS semi\-managed**

EMR on ECS provides a more comprehensive set of over 36 big data ecosystem components, including Hadoop and Spark. Computing and storage resources belong to the user's account. Users can log in to ECS and operate independently. EMR on ECS supports both storage\-compute separation and integrated architectures, allowing data to be stored in Object Storage (TOS) or HDFS. This deployment mode enables users to better control the infrastructure and utilize ECS features; for example, during elastic scaling, supports Spot Instance and Elastic Scheduled Instance (ESI).

EMR on ECS allows users to select the instance type and specifications for deploying EMR services. Users can comprehensively consider actual business needs and costs to select the optimal cost\-performance instance for deploying EMR services.

<span id="8aee3016"></span>
#### **Minute\-level elasticity**

EMR on ECS provides multiple types of elastic scaling and payment methods, offering minute\-level elasticity to support rapid business growth. Supports two types of elastic scaling: time\-based specifications and YARN load metrics. Supports multiple payment methods, including Pay\-As\-You\-Go, Spot Instance, and Elastic Scheduled Instance (ESI).

<span id="731bf4a8"></span>
#### **Custom environment**

Users can use the cluster script feature in the EMR console to batch select nodes and run specified scripts to meet personalized requirements. For example, installing third\-party software and modifying the cluster runtime environment.

<span id="2338add5"></span>
#### **Flexible user\-managed maintenance**

Users can log in to ECS to perform operations independently, such as environment configuration and issue analysis. In this deployment mode, the compute and storage resources are associated with the user's account,BytePlus the EMR team does not have permission to log in to or operate user resources and EMR clusters, and users are responsible for maintaining the EMR service themselves. The EMR console provides comprehensive monitoring and maintenance capabilities, supporting node scaling, service start and stop, log viewing, and more. It is strongly recommended that users configure alerts for key metrics and address related issues promptly.

<span id="7da8be4b"></span>
#### **SLA**

[E-MapReduce服务等级协议](https://docs.byteplus.com/docs/undefined/68da347242e561058e056956)

<span id="76fc5b4e"></span>
#### Billing method

Both Subscription and Pay\-As\-You\-Go billing methods are supported. The cost of an EMR cluster consists of EMR service fees, ECS product fees, TOS product fees, EBS product fees, and the external network traffic fees of the primary node. Among these, the EMR service fees are related to the ECS instance type selected for the cluster. For more details, please refer to [Billing items](https://docs.byteplus.com/docs/undefined/6a1d545680c5b1053bb8773f).

<span id="a69232ba"></span>
### EMR on VKE

EMR service running on the container service (Volcengine Kubernetes Engine, VKE). This service allows users to run big data and AI workloads on VKE clusters, enabling tidal mixed operation of online, offline, and AI workloads to maximize resource utilization, while offering the flexibility of semi\-managed services. EMR on VKE is suitable for use cases such as hybrid deployment of offline/online/AI workloads, large model data preprocessing, and offline inference for large models.

The EMR on VKE deployment mode requires users to maintain the underlying resources and EMR clusters themselves. Users need to have experience in big data and K8s operations and maintenance. To consult about product usage issues, submit a ticket. For professional big data solutions and training services, you can purchase as needed.

<span id="18a8fb26"></span>
#### **VKE semi\-managed**

EMR on VKE provides engine services such as Spark, Ray, Celeborn, and Hive, using a compute\-storage separation architecture. Compute and storage resources are associated with the user's account. Users can log in to ECS and VKE consoles to operate independently. This deployment mode supports user control of infrastructure and the use of VKE features, such as elastic scaling of nodes and Elastic Container Instance (VCI).

<span id="4960cd69"></span>
#### **Elastic Container Instance (VCI) task scheduling**

Supports users in scheduling Spark and other jobs using Elastic Container Instance (VCI), with resources allocated on demand within seconds, eliminating the need for always\-on resources.

<span id="de85e296"></span>
#### **Hybrid deployment of offline, online, and AI workloads.** 

Supports users in deploying EMR virtual clusters on existing VKE clusters, with the resource engine uniformly scheduled by K8S, enabling dynamic hybrid scheduling of online, offline, and AI workloads to maximize resource utilization. Unified underlying infrastructure and operations system to avoid resource silos.

<span id="34133cb1"></span>
#### **Custom image**

Supports users in flexibly integrating custom libraries and Python packages based on the EMR base image to build custom images tailored to their needs.

<span id="806a19cf"></span>
#### **Flexible user\-managed maintenance**

Supports users in logging in to the VKE console to perform operations, configure the VKE cluster, and analyze issues independently. In this deployment model, computing and storage resources belong to the user's account, BytePlus the EMR team has no authority to log in to or operate user resources, including VKE clusters and EMR virtual clusters. Users are responsible for maintaining EMR services themselves. The EMR console provides comprehensive monitoring and maintenance capabilities, supporting job monitoring, Pod resource configuration changes, and more. It is strongly recommended that users configure alerts for key metrics and address related issues promptly.

<span id="592ef891"></span>
#### **SLA**

[E-MapReduce服务等级协议](https://docs.byteplus.com/docs/undefined/68da347242e561058e056956)

<span id="596aca93"></span>
#### Billing method

The cost of an EMR cluster consists of EMR service fees, VKE management fees, ECS product fees, TOS product fees, EBS product fees, and external network traffic fees. Among these, EMR service fees are related to the specifications and quantity of Pod resources actually used by the EMR virtual cluster.
