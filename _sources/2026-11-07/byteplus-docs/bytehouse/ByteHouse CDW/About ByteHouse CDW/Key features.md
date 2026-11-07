---
title: "Key features"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-key-features"
---

<span id="separate-storage-and-computing-layers"></span>
## **Cloud native data warehouse**


* **Cloud native architecture**: Follows the cloud native design philosophy, realizing storage, calculation, and service tiering decoupling. Features infinite storage capacity, elastic scaling of computation, and always\-online services.

* **Lossless elasticity**: Storage is based on object storage with infinite capacity and elastic scaling; Compute resources are based on containers, enabling second\-level scaling.

* **Multi\-level resource isolation**: Implements multi\-level resource isolation mechanism, including isolation between tenants providing physical\-level, cluster\-level isolation; Read\-write isolation, offering physical\-level isolation for computing resources with different read\-write workloads; User/business isolation, based on smart dynamic load management, provides isolation at business logic level and for computing resources, ensuring stable operation for mixed and complex tasks, preventing resource contention, and providing reliable, stable, and consistent SLA guarantees.


<span id="1267dfcd"></span>
### **Real\-time data warehouse**


* **Real\-time data analysis**: ByteHouse can quickly handle complex queries under large\-scale data sets, providing low latency (ms\-level) data analysis capability; Suitable for real\-time business analysis, real\-time data dashboards, and other scenarios.

* **Streaming data analysis**: Supports Kafka streams, MySQL CDC, and other data for real\-time access, ensuring exact\-once accuracy, and analyzes incoming data in real time, suitable for applications in real\-time clickstream analysis, real\-time monitoring, etc.


<span id="0c05040a"></span>
### **Offline data warehouse**


* **High performance**: ByteHouse utilizes columnar storage, vectorized query engine, distributed execution plans, and indices, which can swiftly process complex queries under large\-scale data sets, providing high\-performance data analysis capabilities.

* **ELT, sustained operation for complex tasks**: ByteHouse supports ELT data warehouse development (BSP, Operator Spill, asynchronous execution),  **"complex processing tasks are reliable and stable";**  It integrates with ecosystems like Dataleap, DBT, Airflow, and DolphinScheduler, supporting a one\-stop ELT capability for data warehouse development.

* **Multi\-source integration**: ByteHouse offers one\-stop data synchronization and migration tools for ClickHouse, S3/OBS/OSS/TOS, etc., helping users migrate seamlessly to ByteHouse.


<span id="6dd66857"></span>
### **Ecosystem integration**


* **SQL ecosystem**: Compatible with MySQL syntax, ClickHouse syntax, ANSI SQL syntax; facilitates seamless migration of source databases like ClickHouse, MySQL to ByteHouse, without the need for application layer modifications.

* **BI ecosystem:**  Supports BI tool ecosystems like FineBI, Tableau, ABI, PowerBI, QuickBI, Metabase.

* **IDE ecosystem**: Supports database management tool ecosystems like DBeaver, DataGrip, Navicat, SQL Workbench.

* **Data development** & **scheduling ecosystem**: Supports tool ecosystems such as Dataleap, DBT, Airflow, DolphinScheduler.


<span id="388ba72c"></span>
### Connectivity


* ByteHouse Cloud Data Warehouse Edition provides various developer tools for a smooth integration experience. Users can access and manage ByteHouse services using various programming languages through ByteHouse Console, ByteHouse CLI, and SDKs.


<span id="e67ed72e"></span>
### **Full hosting** & **compliance**


* **Full hosting, maintenance\-free**: ByteHouse provides a one\-stop self\-service platform including database management, queries, development, integration, ecosystem tools, and more; it offers comprehensive system monitoring, load metrics, and supports customizable alerts to help users understand business status and troubleshoot issues.

* **Enterprise\-level security**:

   * Authentication: Username/password management, access key (AK/SK) support.

   * Access Control: Combines with the IAM permissions system, supports an RBAC (Role\-Based Access Control) model, using different policies to manage your security objects.

   * Fine\-grained access control with column and row\-level security helps administrators define and manage different scenarios.

   * Data Encryption: End\-to\-end data encryption, support for TLS during transmission.


<span id="35198f41"></span>
### **Cost reduction and efficiency improvement**


* **Storage Cost Reduction**: Storage costs align with object storage and are charged on a pay\-as\-you\-go basis.

* **Compute Cost Reduction**: Compute resources are based on lossless elasticity, with strategies such as automatic start\-stop and auto\-scaling to reduce compute costs by more than 20%.

* **Compute performance**: Through the use of dedicated servers, virtual warehouse local disk, distributed cache, and a global secondary index, the performance aligns with an architecture that integrates computing and storage.
