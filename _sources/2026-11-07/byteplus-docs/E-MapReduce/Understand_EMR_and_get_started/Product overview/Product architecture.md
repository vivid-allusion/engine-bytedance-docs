---
title: "Product architecture"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Product_architecture"
---

<span id="产品架构"></span>
## EMR on ECS

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c55b4d467b70476796dd60e54960a3ff~tplv-goo7wpa0wc-image.image) </span>

**Infrastructure:**  Based on BytePluscloud servers (ECS), public IP addresses (EIP), elastic block storage (EBS), object storage (TOS), and virtual private cloud (VPC), EMR is provided with a deployment environment featuring elastic scalability, high reliability, high performance, and secure isolation.

**Data storage:**  The HDFS distributed file system supports massive structured and unstructured data storage, supports multiple efficient formats to meet the requirements of different analytics engines, and integrates with TOS object storage to achieve highly available, low\-cost data storage. Supports multiple data lake storage formats such as Hudi, Iceberg, and Delta Lake, helping enterprises build data lake solutions.

**Resource scheduling:**  Based on the Hadoop resource management components Yarn and Kubernetes, unified resource management and scheduling are provided for higher\-level applications.

**Open\-source engines:**  Provides a rich set of mainstream open\-source ecosystem components, 100% open\-source compatible, and continuously optimized based on internal ByteDance practices. Covers offline analytics, real\-time computing, interactive analytics, OLAP databases, NoSQL databases, cloud search, data science, data development, access control, and other fields, meeting the requirements of various big data use cases.

**Operations management:**  Supports cluster creation and provisioning, one\-click deployment, unified operations management capabilities, cluster elastic expansion and scaling, as well as one\-stop operations capabilities for monitoring, alerting, configuration, and log viewing of each component.

<span id="4995aed5"></span>
## EMR on VKE


* **Infrastructure:**  Based on Volcano Engine container servers (VKE), elastic containers (VCI), and object storage (TOS), EMR is provided with a deployment environment featuring elastic scalability, high reliability, high performance, and secure isolation.

* **Open\-source engines:**  100% open\-source compatible, provides integration and management of components such as Spark, Hive, Celeborn, and Volcano, covering offline analytics, interactive queries, data science, data development, access control, and other fields, meeting the requirements of various big data use cases.

* **Operations management:**  Supports cluster creation and provisioning, one\-click deployment, unified operations management capabilities, cluster elastic scaling, as well as one\-stop operations capabilities for monitoring, alerting, configuration, log viewing, and job management of each component.


<span id="d40beee2"></span>
## EMR Serverless

EMR Serverless is divided into Serverless queues and Serverless instances.

<span id="c6459c8e"></span>
### EMR Serverless queues

EMR Serverless queues cover engines such as Spark, Presto, Hive, and Ray. They adopt a high\-performance storage\-compute separation architecture, achieving unified lake, warehouse, and AI integration. Key features include cost advantages, data reliability, and unified scheduling for multiple workloads.

**Core advantages of the storage\-compute separation architecture**


* Costs are reduced by more than two times compared to storage\-compute integrated architecture.

* Compute and storage resources can be elastically scaled on demand at a fine granularity.

* Object storage provides twelve nines of reliability.

* Unified resource pool scheduling for multiple workloads.

* Unified transparent storage and mutual access for multiple workloads.


The architecture of EMR Serverless queues is divided into four layers:


* **Storage layer**

   * BytePlusObject storage TOS (standard storage, infrequent access storage, archive storage)

   * Supports unified format storage for file buckets, object buckets, and more.

   * Supports multiple lake table formats: Hudi, Iceberg, DeltaLake, and Paimon.

* **Compute layer**

   * Unified scheduling based on K8S.

   * Supports batch/offline workloads, AI workloads, and interactive/real\-time workloads.

   * Unified resource pool scheduling for multiple workloads.

* **Acceleration layer**

   * Self\-developed storage acceleration engine Proton: optimizes object storage access performance.

   * Self\-developed compute acceleration engine Bolt: vectorized execution enhances compute performance.

   * AI data preprocessing acceleration optimization.

* **Service layer**

   * Lake/warehouse/AI construction service LAS.

   * Unified metadata management.

   * Unified permission management.

   * Lake table management and optimization.


<span id="404efa67"></span>
### EMR Serverless instances

EMR Serverless instances cover the StarRocks and Doris engines, providing **storage\-compute integrated** and **storage\-compute separated** deployment options, flexibly supporting various business scenarios and choices.
