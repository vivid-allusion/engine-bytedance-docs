---
title: "Product introduction"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/intro"
---

ByteHouse is a data warehouse product independently developed by BytePlus, providing stronger query services and data writing performance on massive data. Applications include multidimensional analysis of massive data, machine learning model evaluation, microservice monitoring and statistics, etc.

ByteHouse has made a series of performance optimizations based on ByteHouse's rich scenarios, as well as pain points in the OLAP industry. These improvements are designed to shorten query execution time, optimize resource utilization, and provide a smoother data analytics experience. Through intelligent optimization algorithms and advanced execution technologies, ByteHouse is better able to handle a variety of complex query scenarios. Some of the deep customization features are listed below:


* **Multi\-scene table engine:** 

   * High Availability Engine: Solve the problem of cluster instability caused by inappropriate use of the open\-source ReplicatedMergeTree engine for ZooKeeper.

   * Real\-time data engine: supports at\-least once semantics, can automatically switch between master and standby writes, stable and high availability.

   * Unique engine: support upsert function, data synchronization insert deduplicate.

* **Extended data type:** 

   * Map: suitable for scenarios where the business changes frequently. Through optimization, the write and query performance can be maintained almost equal to that of normal columns.

   * Bitmap: supports a large amount of data for complex calculations (intersection, union, complement, etc.), suitable for expressing a large number of entity ID sets with specific relationships, such as the user label table with tens of millions or even billions of level user_ids, user segmentation can return results in seconds.

* **Optimizer:**  It is the only ClickHouse optimizer solution in the industry. ByteHouse self\-developed optimizer is based on four major optimization directions: RBO (rule\-based optimization capability), CBO (cost\-based optimization capability), distributed plan optimization, and high\-order optimization capability.

* **Multi\-level storage:**  This method involves automatically transitioning hot data to cold storage (S3 / HDFS), sacrificing some query performance of cold data to alleviate the issue of business storage space growing continuously.
