---
title: "FAQs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/trino_faqs"
---

<span id="q1：为什么修改配置后，trino-服务重启异常"></span>
## **Q1: Why does the Trino service fail to restart after modifying the configuration?** 

Unlike other service components, Trino enforces strict validation of configuration items. If any configuration change does not pass Trino's validation (for example, if the configuration item's name or value is unrecognized, or if there are redundant configuration items), the service will fail to start properly. Therefore, before making configuration changes, carefully check whether the configuration items are correct. If a service startup failure occurs due to changes in service parameters, roll back the operation first, verify correctness, and then reapply the configuration.

<span id="q2：为什么-keystore-证书会发生变更"></span>
## **Q2: Why does the keystore certificate change?** 

Typically, changes to the keystore certificate are transparent to users. EMR verifies the validity of the keystore certificate each time the Trino service starts. In the following situations, a new keystore certificate will be generated:


1. The keystore certificate has expired.

2. The keystore certificate file is corrupted.

3. The keystore password has changed.


If you copy the keystore certificate file to other nodes or use it locally, you need to manually synchronize the updated keystore certificate file after the keystore certificate is refreshed.

<span id="q3：任务执行出现-query-exceeded-max-memory-size-错误"></span>
## **Q3: The error 'Query exceeded max memory size' occurs during task execution**

This issue occurs when the cluster\-level memory limit is exhausted. The solution is to increase the value of the `query.max-memory` parameter. This parameter is a cluster\-level limit and specifies the maximum memory that a query can aggregate across all nodes.

<span id="q4：任务执行出现-query-exceeded-local-memory-limit-错误"></span>
## **Q4: The error 'Query exceeded local memory limit' occurs during task execution**

The solution is to increase the value of the `query.max-memory-per-node` parameter to 40% of the memory of the instance where the worker node resides. This parameter determines the maximum memory a query can use on a node.

The following are recommendations to avoid memory issues:


* For join operations, tasks may fail when a larger table is on the right side. Ideally, place smaller tables on the right side of the join and larger tables on the left side.

* Join and aggregation operators that build hash tables are CPU\- and memory\-intensive. Therefore, if the data volume is large, it is recommended to enable the spill policy.
