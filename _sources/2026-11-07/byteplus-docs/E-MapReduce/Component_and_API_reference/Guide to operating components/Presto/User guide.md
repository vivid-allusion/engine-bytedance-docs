---
title: "User guide"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/presto_User_guide"
---

Presto (or PrestoDB), as an open\-source distributed query and analytics engine based on the MPP architecture, supports PB\-level big data query and analytics, and allows connections to multiple data sources, such as Hive, TOS, MySQL, Hudi, Iceberg, and Kafka, among others. At the same time, it also supports querying data from multiple data sources within a single query, that is, federated queries.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This document introduces the usage guide for the semi\-managed EMR version of the Presto component. For the usage guide of the fully managed EMR Serverless component, see: <a href="https://docs.byteplus.com/docs/E-MapReduce/95186">Basic usage</a>.</div>


<span id="_1-组件说明"></span>
## 1 Component description


* **Presto Coordinator**: The Coordinator serves as the coordination node of Presto, receiving user query requests, generating execution plans, scheduling distributed tasks, and managing Worker nodes.

* **Presto Worker**: The Worker acts as the working node for executing distributed tasks in Presto, running on each Core node and Task node, with only one instance started per node.

* **Presto Connector**: The Connector can be understood as analogous to a database driver, enabling Presto to connect to and operate on target data sources.

* **Presto Cli**: The Cli serves as the command\-line tool for Presto, allowing users to connect to the Coordinator node to submit SQL queries.


Volcano Engine E\-MapReduce (EMR) Presto adopts a hybrid deployment model with YARN, where the Coordinator is deployed on the primary node, while the Worker and YARN NodeManager are deployed on the same node, each occupying a portion of the node's resources, with the allocation ratio customizable by the user.

<span id="_2-更多信息"></span>
## 2 More information

Next, you can visit:


* [Basic usage](https://docs.byteplus.com/docs/E-MapReduce/109364): Learn how to access Presto using the Cli command line, JDBC, Hue, Airflow, and more.

* [Advanced usage](https://docs.byteplus.com/docs/E-MapReduce/109369): Learn about some advanced features of EMR Presto, such as Connector configuration, resource group configuration, built\-in Hive UDF/UADF support, service\-based Web UI, and high availability support.

* [FAQs](https://docs.byteplus.com/docs/E-MapReduce/109368): Learn about some frequently encountered issues and how to resolve them.


To learn more details about Presto, refer to the [Presto official documentation](https://prestodb.io/docs/current/).
