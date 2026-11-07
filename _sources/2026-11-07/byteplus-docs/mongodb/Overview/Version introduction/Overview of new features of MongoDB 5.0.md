---
title: "Overview of new features of MongoDB 5.0"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/mongodb-5-features"
---

This topic introduces the main new features of MongoDB 5.0.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more details on MongoDB 5.0 features, refer to <a href="https://www.mongodb.com/docs/v5.0/release-notes/5.0/#release-notes-for-mongodb-5.0">MongoDB 5.0 release notes</a>.</div>


<span id=".5Y6f55Sf5pSv5oyB5pe25bqP5pWw5o2u"></span>
## Native support for time series data

MongoDB 5.0 natively supports time series data, providing features like time series collections and clustered indexes. This enhances the speed of building and running time series applications, reduces disk usage for data and indexes, and delivers better performance and greater scalability. It expands MongoDB's application scenarios in areas such as IoT, financial analysis, log parsing, and logistics.

You can create a time series collection by specifying the `{ timeseries: { timeField: "timestamp" } }` field in the `db.createCollection()` command when creating a collection. For more details, refer to [Create a Time Series Collection](https://www.mongodb.com/docs/v5.0/core/timeseries-collections/#create-a-time-series-collection).

<span id="stable-api"></span>
## Stable API

MongoDB's Stable API (also known as Versioned API) defines the most commonly used set of commands for applications to read and write data, create collections and indexes, and perform other common tasks. Stable API decouples the application lifecycle from the database lifecycle, allowing your application to use a specified version of the MongoDB API. This ensures that the application can continue to run without code modifications, even with frequent database upgrades or improvements.

Stable API supports MongoDB in adding new features to the database in each API version (such as adding parameters, aggregation operators, and new commands). It also guarantees the compatibility of new API versions with earlier ones. You can run new and existing API versions simultaneously on the same server, enabling you to experience and use new MongoDB features more quickly and conveniently.

For more details, refer to [Stable API](https://www.mongodb.com/docs/v5.0/reference/stable-api/#stable-api).

<span id=".d3JpdGUtY29uY2Vybi3pu5jorqQtbWFqb3JpdHkt57qn5Yir"></span>
## Write concern defaults to majority level

Starting from MongoDB 5.0, `Write Concern` defaults to the `majority` level. This means a write operation is only committed and returns success when it is applied to the `primary node` and persisted in the logs of most `secondary nodes`, thereby enhancing data reliability. For more details about `Write Concern`, refer to [Write Concern](https://www.mongodb.com/docs/v5.0/reference/write-concern/#write-concern).

<span id=".5paw54mILW1vbmdvZGItc2hlbGw="></span>
## New MongoDB shell

MongoDB 5.0 introduces the new MongoDB shell (mongosh), which includes features like syntax highlighting, smart auto\-completion, and contextual help, providing more specific error messages and a modern command\-line experience. For more details about new MongoDB shell, refer to [mongosh](https://www.mongodb.com/docs/mongodb-shell/install/).

<span id=".6ZW_5pe26Ze06L-Q6KGM55qE5b-r54Wn5p-l6K-i"></span>
## Long\-running snapshot queries

MongoDB 5.0 supports executing long\-running queries on real\-time transactional databases while reading data in a consistent state, increasing the versatility and resilience of application read operations. For more details about long\-running snapshot queries, refer to [Query Documents](https://www.mongodb.com/docs/v5.0/tutorial/long-running-queries/#perform-long-running-snapshot-queries).

<span id=".5Y-v5oGi5aSN55qE57Si5byV5Yib5bu65Lu75Yqh"></span>
## Restorable index creation tasks

Starting from MongoDB 5.0, if an index creation task is unexpectedly interrupted, the task is saved to disk and automatically resumes from its original state after a node restart, eliminating the need to rerun the creation task. For more details, refer to [Index Builds on Populated Collections](https://www.mongodb.com/docs/v5.0/core/index-creation/#build-failure-and-recovery).

<span id=".c2NoZW1hLXZhbGlkYXRpb24t5aKe5by6"></span>
## Enhancements for schema validation

Schema Validation is a method for managing and controlling MongoDB data applications. MongoDB 5.0 optimizes schema validation by supporting the `validate` command to discover inconsistencies in collections and return descriptive error messages. This makes it easier to understand documents that do not comply with collection validator rules and the reasons for non\-compliance, helping you quickly identify and correct error codes affecting validation rules. For more details, refer to [db.collection.validate()](https://www.mongodb.com/docs/v5.0/reference/method/db.collection.validate/#db.collection.validate--).

<span id=".5Zyo57q_5pWw5o2u6YeN5paw5YiG54mH"></span>
## Online data resharding

MongoDB 5.0 allows you to change a collection's shard key using the `reshardCollection` command while your business is running. This enables you to adjust the shard key as needed based on changes in business load. The entire process requires no downtime, involves no complex data migration operations, and is simple and efficient. The `reshardCollection` command syntax is as follows.

```Bash
reshardCollection: "<database>.<collection>", key: <shardkey>
```


The description of each parameter in the command syntax is shown in the table below.


|Parameter |Description |
|---|---|
|database |Name of collection to be resharded. |
|collection |Name of database to be resharded. |
|shardkey |The name of the shard key. |


For more details about the `reshardCollection` command, refer to [reshardCollection](https://www.mongodb.com/docs/v5.0/reference/command/reshardCollection/#reshardcollection).
