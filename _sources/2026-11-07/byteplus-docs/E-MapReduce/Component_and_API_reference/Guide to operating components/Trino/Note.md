---
title: "Note"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/trino_note"
---

Trino (or PrestoSQL) is a highly parallel distributed query engine suitable for efficient, low\-latency query analytics scenarios. Trino does not store data itself, but supports access to multiple data sources through connectors, and also enables analysis of data from multiple data sources within a single query, that is, federated queries.

<span id="_1-组件说明"></span>
## 1 Component note

Volcano Engine E\-MapReduce (EMR) Trino adopts a hybrid deployment model with YARN, where the Coordinator is deployed on the primary node, and the Worker and YARN NodeManager are deployed together on the same node, each occupying part of the node's resources, with the allocation ratio customizable by the user.

The overall architecture of Trino is shown in the following diagram:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2cdd9133ead61c6f5b2e0baae2472d66.png) </span>


* **Trino Coordinator**: Responsible for receiving and parsing SQL statements, generating and optimizing query plans, and then orchestrating and scheduling tasks to Worker nodes for execution. At the same time, the Coordinator is also responsible for managing the operational status of Worker nodes.

* **Trino Worker**: Responsible for executing tasks dispatched by the Coordinator, obtaining and processing data from target data sources via the Connector. The Coordinator ultimately retrieves results from Worker nodes, aggregates them, and returns the final result to the client.

* **Trino Connector**: Trino does not store data itself, but accesses external data sources through the Connector, which can be regarded as the driver for the data source.

* **Trino CLI**: The command\-line tool provided by Trino, allowing users to connect to the Trino Coordinator node and submit SQL queries via the command line.


<span id="_2-更多信息"></span>
## 2 More information

Next, you can continue to explore the following Trino related articles:


* [Basic usage](https://docs.byteplus.com/docs/E-MapReduce/109531): Learn how to access Trino using CLI, JDBC, Hue, Airflow, and other methods.

* [Advanced usage](https://docs.byteplus.com/docs/E-MapReduce/109534): Learn about some advanced features of EMR Trino, such as connector configuration, resource group configuration, Web UI as a service, and high availability support.

* [FAQs](https://docs.byteplus.com/docs/E-MapReduce/109526): Learn about some frequently encountered issues and how to resolve them.


To learn more detailed information about Trino, refer to the [Trino official documentation](https://trino.io/docs/current/index.html) or the [official papers](https://trino.io/paper.html).
