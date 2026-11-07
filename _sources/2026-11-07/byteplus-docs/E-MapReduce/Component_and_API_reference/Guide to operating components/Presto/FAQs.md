---
title: "FAQs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/presto_faqs"
---

<span id="q1：为什么修改配置后，presto-服务重启异常"></span>
## Q1: Why does Presto service fail to restart after modifying the configuration?

Unlike other service components, Presto enforces strict validation of configuration items. If any changes to configuration items do not pass Presto's validation (such as unrecognized configuration item names or values, redundant configuration items, and so on), the service will fail to start properly. Therefore, before making changes to the configuration, carefully check whether the configuration items are correct. If a service startup failure occurs due to changes in service parameters, roll back the operation first, verify correctness, and then reconfigure.

<span id="q2：为什么-keystore-证书会发生变更"></span>
## Q2: Why does the keystore certificate change?

Typically, changes to the keystore certificate are transparent to users. EMR verifies the validity of the keystore certificate each time the Presto service starts. If any of the following situations occur, a new keystore certificate will be generated:


1. The keystore certificate has expired.

2. The keystore certificate file is corrupted.

3. The keystore password has changed.


If you copy the keystore certificate file to other nodes or use it locally, you must manually synchronize the updated keystore certificate file after the certificate is refreshed.

<span id="q3：任务执行出现-query-exceeded-max-memory-size-错误"></span>
## **Q3: The error 'Query exceeded max memory size' occurs during task execution**

This issue occurs when the cluster\-level memory limit is exhausted. The solution is to increase the value of the `query.max-memory` parameter. This parameter is a cluster\-level limit and specifies the maximum memory that queries can aggregate across all nodes.

<span id="q4：任务执行出现-query-exceeded-local-memory-limit-错误"></span>
## **Q4: The error 'Query exceeded local memory limit' occurs during task execution**

The solution is to increase the value of the `query.max-memory-per-node` parameter to 40% of the memory of the instance where the worker node is located. This parameter determines the maximum memory that a query can use on a node.

The following are recommendations for avoiding memory issues:


* For join operations, tasks may fail when larger tables are placed on the right side. Ideally, place smaller tables on the right side of the join and larger tables on the left side.

* Join and aggregation operators that build hash tables are CPU\- and memory\-intensive. Therefore, it is recommended to enable the spill strategy when the data volume is large.


<span id="1942fd0b"></span>
## Q5: The error 'The node may have crashed or be under too much load' occurs during task execution

When the workload is too large and the cluster size is small, this error may occur. It is recommended that users increase the service memory or resolve the issue by scaling out and other methods.

<span id="e6ba41fe"></span>
## Q6: After updating the hive.properties configuration and restarting the service, the changes to hive.properties did not take effect

Please make modifications in **Console \> on ECS \> Cluster Name \> Service Management \> Hive \> Service Parameters \> Configuration File**. Changes made in this module will not have the issue of not taking effect.
