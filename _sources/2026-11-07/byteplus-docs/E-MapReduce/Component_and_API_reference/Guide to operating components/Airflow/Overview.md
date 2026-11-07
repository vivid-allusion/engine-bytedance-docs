---
title: "Overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/airflow-overview"
---

<span id="_1-airflow-是什么？"></span>
## 1 What is Airflow?

Airflow is an open\-source component that provides a programmable approach for authoring, scheduling, and monitoring workflows.

In Airflow, workflows are constructed as directed acyclic graphs (DAGs) composed of individual tasks. The Airflow Scheduler executes specific tasks based on a series of Workers, following the dependency relationships defined by the DAG. Its Webserver offers a rich user interface, allowing users to visualize the current workflow status, review historical runs, monitor execution, and, when necessary, troubleshoot issues by viewing execution logs.

Additionally, Airflow provides a comprehensive set of command\-line utilities, enabling users to efficiently perform complex debugging before DAG files are formally deployed to production.

Defining workflows in code enhances maintainability, enables better version management through VCS, and improves testability and collaboration.

<span id="_2-emr-airflow-优势"></span>
## 2 EMR Airflow advantages


|Features |Note |
|---|---|
|**Automated installation and deployment** |Before the cluster is officially created, or for specific types of clusters that already exist but have not yet introduced the Airflow service, you only need to simply check and submit to enable Airflow capabilities in the cluster to meet your production needs. |
|**High performance and high availability in production** |EMR fully leverages the capabilities of the new version of Airflow and, combined with actual cluster conditions, plans an appropriate topology to meet your dual requirements for high performance and high availability of components in production. |
|**Multi\-dimensional scaling based on actual load** |When your production workload changes, use the Worker configuration provided on the page to adjust the scaling strategy for Worker processes within a single node to maximize resource utilization; furthermore, you can leverage EMR cluster scaling capabilities to adjust the number of cluster nodes as needed. |
|**Open\-source compatibility and a comprehensive software stack** |EMR ensures that the Airflow service within the cluster is 100% open\-source compatible, allowing you to migrate to the cloud smoothly without modifying production code. EMR provides a complete compute engine software stack and integrates Hive, Spark, Flink, Presto, Trino, and other Providers into Airflow, enabling you to directly coordinate multiple compute engines within the cluster. |


<span id="_3-部署拓扑"></span>
## 3 Deployment topology


| |**Airflow\-Webserver** |**Airflow\-Scheduler** |**Airflow\-Worker** |
|---|---|---|---|
|**master** |*  |*  |*  |
|**core** | |*  |*  |
|**task** | | |*  |


<span id="_4-文档指引"></span>
## 4 Documentation guide


* To quickly preview Airflow features and experience programmable workflow scheduling, refer to [Quickstart](https://docs.byteplus.com/docs/E-MapReduce/109183).

* To learn about Airflow configuration and tuning, refer to [Key configurations](https://docs.byteplus.com/docs/E-MapReduce/109191).

* To further understand how Airflow integrates with compute engines and explore production\-oriented case studies, refer to:

   * For basic usage, see: [code sample](https://docs.byteplus.com/docs/E-MapReduce/109190)

   * For advanced usage, see: [Advanced usage](https://docs.byteplus.com/docs/E-MapReduce/109185)

   * For best practices, see: [Best practices](https://docs.byteplus.com/docs/E-MapReduce/109187)

* For more production FAQs and points to note, visit [FAQs and important notes](https://docs.byteplus.com/docs/E-MapReduce/109184)  **.**
