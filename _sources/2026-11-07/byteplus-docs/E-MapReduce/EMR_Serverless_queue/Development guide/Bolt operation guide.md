---
title: "Bolt operation guide"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Bolt_operation_guide"
---

<span id="8ae4b190"></span>
## Introduction to Bolt

Bolt is a vectorized execution engine implemented in C++, combined with runtime LLVM Codegen technology, which significantly improves parallel execution efficiency on multi\-core CPUs. By replacing the traditional Java engine in distributed SQL query engines Spark and Presto, Bolt delivers 2 to 5 times better performance than open\-source products, greatly accelerating query speed and reducing resource costs.

This article introduces how to use Bolt in Serverless EMR.

<span id="831ab5c9"></span>
## Enable Bolt for exclusive queues

When creating an exclusive queue, you can select EngineRuntime as Bolt to enable Bolt for the queue. Jobs running in the Default compute group of this queue will, by default, run in the Bolt environment.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a3c252c0d5fa46cc80369a2ac7147b4e~tplv-goo7wpa0wc-image.image) </span>

If you do not want to use the Bolt environment, you can manually specify the parameter: `set emr.serverless.bolt.enabled=false`.

<span id="e490192d"></span>
## Enable Bolt for existing queues

To enable Bolt for an existing queue, you can edit the compute group and update EngineRuntime. After modifying EngineRuntime to Bolt and saving, Bolt will be enabled by default for the queue.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/028b13ebe2464924a58cf5612e2e27b5~tplv-goo7wpa0wc-image.image) </span>

<span id="c68273f7"></span>
## Implement Bolt at the job level

To enable Bolt at the job level in a public queue or a non\-Bolt exclusive queue, you can use job parameters.

```SQL
set emr.serverless.bolt.enabled=true
```


<span id="aadf521d"></span>
## Create a Bolt compute group

When creating a Spark warehouse or Presto warehouse, you can select EngineRuntime as Bolt to enable Bolt for the compute group. The EngineRuntime value for the compute group will, by default, match that of its associated queue. A compute group with Bolt enabled will, by default, run in the Bolt environment. If Bolt execution fails, it will automatically route to the default environment.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8fa3c2ce97b487888ee32c300c1aa66~tplv-goo7wpa0wc-image.image) </span>

<span id="07e838a7"></span>
## Enable Bolt for existing compute groups

For Spark compute groups, you can edit the compute group to enable Bolt. Enabling Bolt requires restarting the compute group.

For Presto compute groups, editing to enable Bolt is currently not supported. To enable Bolt, you need to recreate the Presto compute group.

<span id="5c07ae67"></span>
## Bolt billing

When using Bolt acceleration capabilities, users pay the corresponding acceleration fees based on the CUH consumed by the actual job. For detailed billing rules, see [Bolt acceleration engine pricing details](https://docs.byteplus.com/docs/E-MapReduce/Billing_for_Bolt).
