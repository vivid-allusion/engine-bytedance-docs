---
title: "Terms"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/terms"
---

This topic introduces the basic terms commonly used in BytePlus Cloud Search.

<span id="实例（Instance）"></span>
## Instance

BytePlus Cloud Search provides functions on a per\-instance basis. An instance represents an independent search service that consists of multiple nodes. Different types of nodes provide different capabilities, such as data nodes, dedicated master nodes and visualization tool nodes. Each instance is defined with a unique ID and a customized name.

Instance is also called "cluster" in cloud service.

<span id="索引（Index）"></span>
## Node Type

Cloud Search clusters support multiple node types. Before you create a node, familiarize yourself with the functionality of each node and decide if it is necessary to create the node based on your business needs.


* **Data node**


Data nodes store index data. They are mainly used to perform operations on documents including create, read, update, delete (CRUD operations), and aggregations.


* **Dedicated master node**


Dedicated master nodes are used to ensure the stability of clusters. The dedicated master node feature is disabled by default. When the feature is enabled, the number of nodes is fixed to 3 by default. This allows the system to effectively select the master nodes when a network failure occurs.


* **Kibana/Dashboards node**


Kibana nodes and dashboards nodes are used to deploy data visualization tools. When a Cloud Search instance is created, a data visualization tool node is deployed by default. You can use this node to view and interact with index data or visually display and analyze data in charts.


* **Coordinating node**


Coordinating nodes are used to decouple read and write requests, offload requests from data nodes, and ensure the stability of clusters. Coordinating nodes are only designed to receive and distribute query requests, and process statistical and query results.


* **Warm data node**


Warm data nodes are used to store time series data that is accessed infrequently and updated rarely, such as data logs that are not frequently queried or historical records. Warm data nodes reduce storage costs and improve instance processing performance.


* **Cold data node**


Cold data nodes can be used to store searchable snapshots.

<span id="26b23ede"></span>
## Index

An index is a collection of documents and has a mapping that defines the schema of its documents. It is the fundamental unit of storage in Elasticsearch, a logical namespace for storing data that share similar characteristics.

Index is equivalent to "database" in a relational database.

<span id="b3609468"></span>
## Type

A type is a logical class or partition of an index. In Elasticsearch 5.x and earlier versions, an index can store multiple types of documents. In Elasticsearch V6.x, an index can store only one type of document. In Elasticsearch V7.x, the type of an index can only be `_doc`. Therefore, this term is deprecated in version 7.x and later. For more information, please see [Removal of mapping types](https://www.elastic.co/guide/en/elasticsearch/reference/7.17/removal-of-types.html).

Type is equivalent to "table" in a relational database.

<span id="43e5fb21"></span>
## Document

Elasticsearch serializes and stores data in the form of JSON documents. A document is a set of fields and the basic unit that can be indexed. In Elasticsearch, instead of searching for data based on row and column, you index, search for, sort, and filter documents.

Document is equivalent to "row" in a relational database.

<span id="fdfce527"></span>
## Field

Field is the minimum unit of a document and are key\-value pairs that contain searchable data. An indexed document contains data and metadata. Metadata fields are prefixed with an underscore like `_source`, `_index` and `_id`.

Field is equivalent to "column" in a relational database.

<span id="74a6e893"></span>
## Mapping

A mapping defines the data type for each field, how the field should be indexed, and how it should be stored.

Mapping is equivalent to "schema" in a relational database.

The following table summarizes the similarity of terms in Cloud Search and relational database.


|**Cloud Search** |**Relational Database** |
|---|---|
|index |database |
|type |table |
|document |row |
|field |column |
|mapping |schema |


<span id="分片（Shard）"></span>
## Shard

A shard is an underlying read\-write unit and serves as a partition of data in an index. An index can be divided into multiple shards and these shards are distributed among different nodes to improve concurrency performance.

Shards are classified into primary shards (original shards) and replica shards (copies of the primary shards). Primary shards hold authoritative data, and replica shards provide failover. Data is firstly written into a primary shard. Once successful, it is then written into replica shards. When the system recovers data, the data held by the primary shard prevails.
