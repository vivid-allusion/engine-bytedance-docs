---
title: "What is E-MapReduce"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/What_is_E-MapReduce"
---

BytePlus E\-MapReduce (EMR) is an enterprise\-level big data analytics system built on the open\-source Hadoop ecosystem. It is fully compatible with open source and provides integration and management for ecosystem components such as Hadoop, Spark, Ray, Hive, Presto, Doris, StarRocks, Hudi, Iceberg, and Lance. EMR supports storage, querying, and analysis of massive datasets, offers elastic scalability and on\-demand usage at lower cost, and can be combined with data development and governance suites as well as other product capabilities to deliver end\-to\-end data ingestion, analysis, and mining capabilities. This helps users easily build enterprise big data platforms and migrate data to the cloud, reduces the threshold for operations and maintenance, and accelerates data insights and business decision\-making.

The advantages of EMR compared to self\-built Hadoop are as follows: EMR provides a one\-click solution for cluster creation and management, including host selection, cluster setup, cluster configuration, runtime monitoring, parameter configuration, job execution, and cluster monitoring and alerting. EMR enables users to be freed from the heavy workload of cluster\-related hardware procurement, software installation, deployment and testing, cluster management, and maintenance, allowing them to focus on data application development.


|**Comparison dimensions** |BytePlus**EMR engine** |**Self\-built Hadoop cluster** |
|---|---|---|
|**Cost** |Low cost, supports on\-demand purchase (Subscription/Pay\-As\-You\-Go), flexible adjustment of cluster resources, no additional license fees required |Fixed resources, low resource utilization, license fees required for distributions |
|**Ease of use** |Deployment and installation can be completed within minutes, with flexible adjustment of cluster resources |Fixed cluster resources, manual integration of components required, and a long deployment cycle |
|**Stability** |100% compatible with open\-source community versions, supported by enterprise\-level optimizations and extensive compatibility and stability testing |Compatibility and stability must be ensured manually, requiring extensive validation and testing before production deployment |
|**Elasticity** |Clusters can be created and destroyed on demand, and storage and compute resources can be dynamically adjusted based on rules and cluster load |No automatic elasticity capability; operations and maintenance personnel must determine whether to scale the cluster based on cluster load. |
|**Security** |Based on BytePlus ecosystem enterprise\-grade data security and authentication solutions, supports fine\-grained permission control, and supports RBAC mode. |Open\-source community data security solutions are incomplete and cannot meet production requirements. |
|**Performance** |Cluster specifications are parameter\-tuned by default, with feature\-level performance optimization for core components. |Open\-source version requires self\-tuning for performance, which is challenging. |
|**Ecosystem** |Open\-source ecosystem is integrated with BytePlus ecosystem, with performance and functionality optimized based on ECS, TOS, and other features, and seamless integration with data products such as DataLeap. |Community open\-source ecosystem does not provide a smooth experience for multi\-product combinations in the cloud. |
|**Service** |Professional big data expert services and after\-sales maintenance support. |A big data maintenance team needs to be established, and problem resolution is difficult. |


<span id="d6c917f9"></span>
## Product types

BytePlus EMR currently offers three product types: EMR on ECS, EMR on VKE, and EMR Serverless, to meet the needs of customers with different business requirements and technical backgrounds.


|Form |Description |
|---|---|
|EMR on ECS |BytePlus EMR on ECS is a product form that deploys the big data platform on BytePlus Elastic Compute Service (ECS). With EMR on ECS, after creating an EMR cluster, users only need simple configuration and minimal ongoing maintenance to efficiently utilize computing and storage resources. It combines the big data processing capabilities of EMR with the containerized deployment capabilities of ECS, allowing users to flexibly configure EMR clusters according to enterprise requirements and architectural choices, and to adapt to various complex data processing and analysis scenarios. |
|EMR on VKE |BytePlus EMR on VKE is based on containerized services and open\-source big data engines, providing a platform for rapid deployment, flexible scaling, and efficient, secure big data service deployment. With EMR on VKE, you can reduce the operational and maintenance effort for underlying cluster resources, allowing greater focus on big data tasks themselves. |
|EMR Serverless |BytePlus EMR Serverless is a product form under the EMR public cloud product framework that provides fully managed big data services (Serverless), offering plug\-and\-play, highly elastic big data services. Uses enterprise\-grade enhanced components fully compatible with the open\-source technology stack, currently offering service types including Spark, Presto, StarRocks, Doris, Hive, and more. |
