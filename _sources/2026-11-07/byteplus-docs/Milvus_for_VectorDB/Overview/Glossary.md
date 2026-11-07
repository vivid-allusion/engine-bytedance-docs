---
title: "Glossary"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Glossary"
---

This topic summarizes the terms related to the instances of Milvus for VectorDB.

|**Term** |**Description** |
|---|---|
|Region |Geographic location of the data. |
|Availability zones |Abbreviated as AZ. Each region contains multiple isolated areas called availability zones. |
|Instance |The basic unit for cloud resource management in Milvus for VectorDB. The performances vary depending on the specifications (CPU cores, memory size, and others) of the instances. |
|High availability |Abbreviated as HA. It is the multi\-node deployment switch in Milvus for VectorDB. After you enable this feature, the number of instance nodes must be at least two to ensure continuous business availability. |
|Service nodes |A service node consists of a metadata database service, a proxy, an index node, and a data node. |
|Compute nodes |Like service nodes, this is a sales mode concept and is essentially a Query Node. |
|Metadata database service |Responsible for storing and managing the global metadata of the database. It is the brain of the cluster, recording the definitions and states of all logical objects, such as collections, partitions, indexes, field structures, and permissions, to ensure data consistency and coordination in the distributed cluster. |
|Proxy |Acts as an intermediary layer between query nodes, data nodes, and other nodes. It receives, parses, and routes client requests, coordinates resource scheduling for the distributed cluster, and ensures high availability and load balancing. |
|Index node |Index nodes are used to build indexes. Index nodes do not need to stay resident in memory and can be implemented using a serverless framework. |
|Data node |Data nodes retrieve incremental log data by subscribing to the log proxy, handle mutation requests, package the log data into log backups, and store them in object storage. |
|Query node |Query nodes retrieve incremental log data by subscribing to the log proxy, convert it into continuously growing segments, load historical data from TOS, and perform hybrid searches between vector and scalar data. |
|VPC |Virtual Private Cloud. A VPC is an isolated network environment with higher security and performance than traditional classic networks. |
|Internal address |The address for accessing a Milvus instance from a private network, for example, when an ECS instance and a Milvus instance are in the same VPC. |
|Subnet |A subnet is a segment of the VPC allocated within a specified availability zone, providing private IP addresses to cloud resources such as cloud servers and cloud load balancers. |
