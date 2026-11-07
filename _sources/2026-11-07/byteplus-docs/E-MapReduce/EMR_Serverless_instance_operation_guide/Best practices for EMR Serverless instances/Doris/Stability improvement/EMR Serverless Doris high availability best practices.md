---
title: "EMR Serverless Doris high availability best practices"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_Serverless_Doris_high_availability_best_practices"
---

This article introduces the high availability implementation of Doris core components—FE nodes and BE nodes. It outlines load balancing solutions for FE across multiple scenarios, as well as the high availability capabilities of BE based on the integrated storage and compute architecture, providing guidance for stable cluster operation.

<span id="04ac22c3"></span>
## FE high availability best practices: Multi\-scenario load balancing solutions

As the "entry point and scheduling core" of the Doris cluster, FE achieves high availability through **load balancing + automatic failover**. Specifically, there are three types of scenarios, covering different requirements from Serverless to custom development:

<span id="49f069f6"></span>
### EMR Serverless Doris instance: Out\-of\-the\-box high availability

Applicable to scenarios using the EMR Serverless version of Doris. No additional configuration is required; high availability is achieved directly by leveraging platform capabilities:


* **Configuration method**: When creating an EMR Serverless Doris instance, simply select the **high availability** option. The platform will automatically deploy multiple FE nodes and associate them with the load balancing component (PLB).

* **Access method**: After the instance is created, users only need to access the instance's corresponding **intranet address** to automatically connect to the PLB with load balancing enabled.

* **High availability principle**: PLB continuously monitors the operational status of all backend FE nodes and distributes requests using a "round\-robin" strategy. When an FE node fails, PLB automatically bypasses the faulty node and forwards requests to healthy nodes, ensuring uninterrupted service.


<span id="54de80ee"></span>
### Application layer code: Custom retry and load balancing

Applicable to scenarios requiring independent control of load balancing logic (such as customized business systems), where fault detection and retry must be implemented at the code level:


* **Core logic**: Embed a "load balancing + fault retry" mechanism in the application code. When the connection to an FE node fails, the system automatically switches to another configured FE node.

* **Key operation**: You must enter multiple Doris frontend node addresses\*\*\*\* (at least two, to avoid single\-point dependency) in the code configuration in advance to ensure there are backup nodes available for switching in case of failure.

* **Advantages**: Highly flexible, allowing adjustment of retry attempts and switching strategies (such as round\-robin, random, weighted, and more) according to business scenarios to meet personalized requirements.


<span id="be4376c6"></span>
### MySQL JDBC Connector: Automatic retry based on driver capabilities

Applicable to scenarios where Doris is connected via the MySQL JDBC Connector (such as Java applications), leveraging the native capabilities of the JDBC driver to achieve high availability directly:


* **Configuration method**: Add the "loadbalance" identifier to the JDBC connection URL and specify multiple FE node addresses; the driver will automatically handle load balancing and retries.

* **Standard connection format**:


```Plain
jdbc:mysql:loadbalance://[host1][:port],[host2][:port][,[host3][:port]]...[/[database]][?propertyName1=propertyValue1[&propertyName2=propertyValue2]...]
```



* **Core principle**: The JDBC driver periodically checks the availability of each FE node and distributes requests using a built\-in round\-robin strategy. When a node fails, the driver automatically retries other healthy nodes, requiring no additional handling in business code.


<span id="53e34551"></span>
## BE high availability practices: Architecture design based on integrated storage and compute

As the "data storage and compute core" of the Doris cluster, BE achieves high availability through **multi\-replica storage + automatic adaptation to node changes**, based on an integrated storage and compute architecture by default. This is divided into three parts: "basic capabilities", "node adaptation", and "architectural limitations":

<span id="a7b17c4a"></span>
### Basic high availability capability: Multi\-replica ensures both data and service reliability

The default Doris cluster (integrated storage and compute mode) already provides basic high availability, primarily relying on the "3\-node BE + three\-replica Tablet" architecture:


* **Node deployment requirements**: By default, at least three BE nodes must be deployed to form a cluster and avoid single points of failure.

* **Data storage logic**: Doris divides data into "Tablets" (data shards), with each Tablet storing **three replicas** by default, and the three replicas are distributed across different BE nodes.

* **High availability assurance**:

   1. Data reliability: Even if a BE node fails, the Tablet replicas it stores can be recovered from replicas on other nodes, eliminating the risk of data loss.

   2. Service availability: In three\-replica mode, if a single BE node experiences an issue (such as a crash or disconnection), the cluster still has two healthy replicas providing read and write services, ensuring business queries are not affected.

   3. Performance gain: Increasing the number of Tablet replicas (for example, from 3 to 4) can further enhance the system's high\-concurrency query capability—multiple replicas can respond to different requests simultaneously, distributing computational load.


<span id="aa59132f"></span>
### Node change adaptation: Automatically ensure high availability during scaling operations

When the number of BE nodes changes (such as scaling out due to business growth or scaling in to reduce resource redundancy), Doris can automatically adapt without stopping services, ensuring uninterrupted high availability during scaling:


* **Core mechanism: Tablet automatic migration**: Node changes trigger the cluster's "Tablet balancing scheduler", and the system dynamically adjusts the distribution of Tablet replicas based on the number of nodes:

   * Scale\-out scenario: After adding new BE nodes, the cluster automatically migrates some Tablet replicas from original nodes to the new nodes, ensuring balanced storage and computational load across all BE nodes;

   * Scale\-in scenario: Before taking down BE nodes, the cluster first migrates all Tablet replicas from the node to other healthy BE nodes. After migration is complete, the node is taken down, ensuring that the number of replicas for each Tablet always remains at the default of 3 (or the user\-configured value), without affecting data reliability;

* **Administrator operation advantage**: There is no need to manually perform complex operations such as "data redistribution" or "replica migration"; simply initiate scaling commands, and the cluster automatically completes subsequent adaptation, reducing operation and maintenance costs.


<span id="e23cd725"></span>
### Limitations of the integrated storage\-compute architecture

Although the integrated storage\-compute architecture can ensure high availability and query performance, it has clear limitations in terms of cost, complexity, and elasticity, and should be used with consideration of business scenarios:


* **Higher cost**: To ensure data reliability, at least 3 data replicas must be maintained, resulting in storage resource usage being "three times the actual data volume"; and as data volume grows, storage and compute resources must be expanded simultaneously (storage and compute are bound), which may lead to compute resource redundancy (for example, insufficient storage but surplus compute capacity);

* **High architectural complexity**: Maintaining data consistency across multiple replicas (such as replica synchronization and replica completion during failure recovery) increases the complexity of underlying cluster scheduling and monitoring;

* **Poor elasticity experience**: Scaling triggers automatic Tablet migration, which consumes cluster resources (such as network bandwidth and IO). The larger the data volume, the longer the migration takes, and cluster query performance may be affected during this period.
