---
title: "Basic concepts"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Basic_concepts"
---

This article summarizes the basic concepts involved in the use of E\-MapReduce, making it convenient for you to look up and understand the relevant concepts.

<span id="通用概念"></span>
## General concepts


|**Concept** |**Note** |
|---|---|
|EMR |EMR stands for E\-MapReduce and usually refers to a managed Hadoop big data environment provided through cloud services. Within the scope of this document, it specifically refers to the E\-MapReduce big data platform of BytePlus, which is a brand concept that includes multiple product types. |
|Serverless |Serverless architecture is a resource model in cloud computing. Developers only need to focus on code and business logic, without managing complex software and hardware configurations. EMR Serverless relies on the BytePlus platform to provide server maintenance, control resource scaling, and ensure service availability. |
|Cluster |An independent group of machines in the E\-MapReduce product that provides some basic engine services for higher\-level business. Each E\-MapReduce cluster consists of multiple BytePlus ECS instances. |
|ECS instance |A resource set composed of CPU, memory, and cloud disks, with each resource logically corresponding to a computing hardware entity in the data center. |
|Node |An E\-MapReduce cluster consists of multiple types of instance nodes, including primary instance nodes (Master), core instance nodes (Core), and compute instance nodes (Task). The service processes deployed on different instance nodes vary, and the tasks they are responsible for are also different. For example:<br><br><br>* Primary instance node (Master): The node for deploying cluster service management and control components, such as the ResourceManager of Hadoop YARN.<br><br>* Core instance node (Core): Nodes managed by the primary instance node. The Datanode service of Hadoop HDFS runs on core instance nodes and saves all data. At the same time, core instance nodes also deploy compute services to execute computing tasks. For example, the NodeManager service of Hadoop YARN.<br><br>* Compute instance node (Task): Instance nodes dedicated to computing, which do not save HDFS data. The data to be computed comes from Core nodes and TOS, so Task nodes are often used as elastic nodes that can be scaled out or in at any time; they mainly deploy the NodeManager service, and the number of Task nodes can be changed at any time to achieve cluster elasticity, with a minimum value of 0. |
|Region & Availability zone |* Region: Refers to different geographic areas where physical data centers are located.<br><br>   * To reduce access latency and improve download speed, it is recommended to purchase ECS in the region closest to the required service. After resources are purchased, the region cannot be changed.<br><br>* Availability zone (AZ): Refers to a physically isolated area within the same region, with independent power and network infrastructure.<br><br>   * A region typically consists of multiple availability zones. Only different availability zones within the same region can communicate with each other over the intranet, and are connected by low\-latency links. Availability zones in different regions are completely isolated. |
|Cloud disk & local disk |* Cloud disk: A block\-level storage product that uses a distributed triple\-replica mechanism to provide 99.9999999% data reliability for ECS instances.<br><br>* Local disk: The local hard disk device on the physical machine where the ECS instance resides. It offers excellent storage I/O performance and cost\-effectiveness for massive storage, but data reliability depends on the physical machine's reliability, posing a risk of single points of failure. |
|AK/SK |**Access Key ID** (AK) and **Secret Access Key** (SK) are security credentials for requesting BytePlusAPI. After registering a cloud account on the BytePlusofficial website, you can generate this information on the [IAM Console](https://console.byteplus.com/iam/identitymanage/user) pages. These credentials are used to identify users and to perform signature verification when accessing EMR, other cloud products, or connecting third\-party tools. Please store them securely and keep them confidential. If there is a risk of leakage, disable or update them promptly. |
|Metadata |Metadata is data that describes information about data, providing context, structure, and meaning for the data. The metadata of this system is managed and served by LAS Formation. |
|Private network |Private network (VPC) provides intranet security isolation for your cloud environment. Private networks in different VPCs cannot communicate with each other. |
|Security group |A security group is a collection of security rules with stateful inspection and packet filtering capabilities. It can control inbound and outbound traffic for cloud server instances within the security group and serves as an important network security isolation mechanism for cloud servers. |
|Public IP |Public IP EIP (Elastic IP) provides independent public IP resources, including public IP addresses and public network bandwidth services, enabling cloud resources to access the Internet. |
|Tag |Consists of a key\-value pair. After using tags to identify resources with the same characteristics, such as resources belonging to the same organization or having the same purpose, you can easily retrieve and manage resources based on tags. |
|Project |BytePlus cloud resource management method provided for customers, used for centralized orchestration and management of cloud resources. For example, you can group resources based on "project", and then manage permissions and query billing based on the project. |
|Resource queue |It is a form of providing computing resources, isolating and controlling resources through logical grouping. Pay\-As\-You\-Go enables the use of public queues, while Subscription enables the use of a dedicated queue. |
|Preheating capability |Provides a dedicated SparkSQL service that is started in advance. When submitting SQL jobs, they are directly submitted to this preheated SparkSQL service, bypassing the conventional resource application phase, effectively reducing latency distortion for jobs measured in seconds caused by startup time. |
|FE (Frontend) |FE is the frontend node of Doris/StarRocks, responsible for managing metadata, handling client connections, query planning, query scheduling, and other functions. Each FE node retains a complete copy of metadata in memory, so every FE node can provide identical services. |
|BE(Backend) |BE is the backend node of Doris/StarRocks, responsible for data storage, SQL execution, and other tasks. |
|CN(Compute Node) |* In the integrated storage and compute architecture, CN nodes provide additional computing resources for queries only and do not store data.<br><br>* Under the storage\-compute separation architecture, CN local disks are only used to cache hot data to accelerate queries. |
|CU |CU is the unit for measuring resources, and queue capacity is expressed in CU. 1CU= 1 vCPU 4GiB Memory。 In this system, resource parameters must be set in CU. |
|Elastic resources |This is a type of capacity provided by dedicated queues, supporting elastic scaling up or down based on queue resource load to accommodate business scenarios with workloads that fluctuate over time. In this case, the business only needs to purchase fixed resources sufficient for daily requirements, and any upward fluctuation in resources is purchased as elastic resources. |
|Namespace |Kubernetes namespaces allocate cluster resources among multiple users and applications. These namespaces are the foundation of a multi\-tenant environment. |
|DDL |Data Definition Language (DDL). For example, operations such as creating tables and creating views. |
|DML |Data Manipulation Language (DML). For example, INSERT, UPDATE, and DELETE operations. |
|DQL |Data Query Language (DQL). For example, SELECT operations. |
|SQL job |A job that directly submits Spark SQL statements is called an SQL job. Submission is supported via a graphical interface or JDBC connection. |
|Spark JAR job |This generally refers to job types such as Spark Core, PySpark, and MLlib, which can be submitted through a visual interface or via the SDK provided by the system. |
|Function |The system provides open\-source functions, including Spark built\-in functions and user\-defined functions (UDF). |


<span id="计费概念"></span>
## Billing concepts


|**Concept** |**Note** |
|---|---|
|Subscription |Also known as prepaid, this is a payment method where fees are paid before using resources. It is suitable for scenarios where computing and storage resources are relatively fixed. The minimum purchase duration for EMR subscription is one month. |
|Pay\-As\-You\-Go |Also known as postpaid, this is a payment method where fees are paid after using resources. It allows more flexible starting and stopping of EMR clusters. |
