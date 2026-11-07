---
title: "Values"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Values"
---

The Values Pipeline connector can be used as a Data Sink in the Pipeline to write data to standard output. This document describes how to set up the Values Pipeline connector.

<span id="1d2650b5"></span>
## Usage Restrictions


* The Values Pipeline connector currently only supports usage in **Flink 1.16\-volcano** and higher engine versions.

* The Values Pipeline connector is only used during data debugging stages and is not recommended for production use.


<span id="77f32682"></span>
## **Connector Features**


* Automatic Table Creation

* Synchronized Table Structure Changes

* Real\-time Data Synchronization


<span id="cf377529"></span>
## **How to Create a Pipeline**

Reading data from MySQL to sync to Values can be defined as follows:

```YAML
source:
  type: mysql
  name: MySQL Source
  hostname: 127.0.0.1
  port: 3306
  username: admin
  password: pass
  tables: adb.\., bdb.user_table_[0-9]+, [app|web].order_\.
  server-id: 5401-5404

sink:
  type: values
  name: Values Sink

pipeline:
  name: MySQL to Values Pipeline
  parallelism: 2
```


<span id="fed25470"></span>
## **Pipeline Connector Configuration**


|**Option** |**Required** |**Default** |**Type** |**Description** |
|---|---|---|---|---|
|type |required |(none) |String |Specify the connector to use, setting it to 'values'. |
|name |optional |(none) |String |The name of the Sink. |
