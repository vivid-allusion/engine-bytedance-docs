---
title: "Performance whitepaper"
product: "Document Database for MongoDB"
product_code: "mongodb"
section: "Document"
source: "https://docs.byteplus.com/en/docs/mongodb/performance-whitepaper"
---

This topic describes how to use YCSB to test Document Database for MongoDB instances and presents the performance results. Follow the steps in this topic to reproduce the tests, compare different configurations, and better understand the performance characteristics of your database system.

<span id="iTlDaBKh"></span>
## Test environment


* Both the ECS instance and Document Database for MongoDB instances to be tested are in the same region and availability zone. For this test, it is China (Guangzhou) Availability Zone A.

* The network type for both is VPC, and both the ECS instances and MongoDB instances are in the same VPC.

* Document Database for MongoDB instances used for testing:

   * Instance configuration: Replica set instances with specifications of 2 cores 4 GiB, 4 cores 8 GiB, 8 cores 16 GiB, 16 cores 32 GiB, and 16 cores 64 GiB.

   * Storage type: SSD local disks (physical server) and ESSD FlexPL volumes (volume architecture), with 500 GiB of storage space for both.

   * Database version: MongoDB 4.4.

* ECS instances used for testing:

   * Instance configuration: ECS instances with 8 cores and 16 GiB specifications (specification code `ecs.c6e.2xlarge`).

   * Storage type: ESSD PL0 volumes, with 40 GiB of storage space.

   * Operating system version: Debian 10.


<span id="bDj8G8rV"></span>
## Test tool

YCSB 0.17.0 is used in this test. YCSB is a performance testing tool that supports various databases implemented by Java language. For specific installation and usage method, refer to [YCSB](https://github.com/brianfrankcooper/YCSB/tree/master/mongodb).

<span id="7TNEr2Q2"></span>
## Test scenario

This test covers Load (data loading) and five read/write ratio scenarios. The corresponding read/write ratios for each scenario are as follows.


|**Scenario** |**Read/write ratio** |**readproportion** |**updateproportion** |
|---|---|---|---|
|Load |\- |\- |\- |
|Read\-only |100:0 |100 |0 |
|Read\-intensive |95:5 |95 |5 |
|Read/write balance |50:50 |50 |50 |
|Write\-instensive |5:95 |5 |95 |
|Write\-only |0:100 |0 |100 |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The Load scenario is the data loading phase, used to evaluate bulk write performance and does not involve read/write ratios.</div>


The `threads`, `recordcount`, and `operationcount` values for different MongoDB instance specifications in this test are as follows.


|**Instance specification** |**threads** |**recordcount and operationcount** |
|---|---|---|
|2 cores 4 GiB |8 |2000000 |
|4 cores 8 GiB |16 |4000000 |
|8 cores 16 GiB |32 |8000000 |
|16 cores 32 GiB |64 |16000000 |
|16 cores 64 GiB |96 |32000000 |


For CPU core count and memory configuration of each specification, refer to [Product specifications](https://docs.byteplus.com/en/docs/mongodb/product-specification).

<span id="eXPNuTlA"></span>
## Test method


1. In the target MongoDB instance, add the primary private IP of the ECS instance to the allowlist. For detailed instructions, refer to [Editing allowlist](https://docs.byteplus.com/en/docs/mongodb/edit-allowlist). For how to obtain the primary private IP address, refer to [Viewing IPv4/IPv6 addresses](https://docs.byteplus.com/en/docs/ecs/Viewing-IPv4-or-IPv6-addresses).

2. Remotely log in to the ECS instance. For the procedure, refer to [Login overview](https://docs.byteplus.com/en/docs/ecs/Overview-1).

3. Load test data into the MongoDB instance.

   ```Bash
   ./bin/ycsb load mongodb -s -threads <num> -p workload=site.ycsb.workloads.CoreWorkload -p mongodb.batchsize=1 -p mongodb.url='<url>' -p recordcount=<num> 
   ```
   

   You need to replace the following parameters:

   * `threads`: The number of concurrent client threads, used to simulate different concurrency pressures. Replace this parameter with the actual value based on the test scenario.

   * `mongodb.url`: The connection address of the MongoDB instance, which must be enclosed in single English quotes. The format is `mongodb://<user>:<password>@<host:port>/ycsb?replicaSet=<replicaSetName>&w=1`. For information on how to obtain the connection address, refer to [Viewing connection address](https://docs.byteplus.com/en/docs/mongodb/addresses-introduction).

   * `recordcount`: The total number of records loaded into the MongoDB instance. Replace this parameter with the actual value based on the test scenario.

4. Execute the performance stress testing command.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Enabling the <code>operationProfiling.mode</code> parameter may affect instance performance. It is recommended to set the parameter value to <code>off</code> before performing performance stress testing. For parameter settings, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modify-parameter?lang=en">Modifying instance parameters</a>.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To ensure a unified command template for various read/write ratio scenarios, <code>-p mongodb.upsert=true</code> is retained in this test command. This parameter only takes effect in <code>update</code> operations, where it converts updates on non\-existent documents into inserts. It is not triggered in pure read scenarios (<code>readproportion=100</code>) and does not affect read performance test results.   </div>
   

   ```Bash
   ./bin/ycsb run mongodb -s -threads <num> -p workload=site.ycsb.workloads.CoreWorkload -p mongodb.upsert=true -p mongodb.batchsize=1 -p mongodb.url='<url>' -p recordcount=<num> -p operationcount=<num> -p requestdistribution=zipfian -p readproportion=<num> -p updateproportion=<num>
   ```
   

   You need to replace the following parameters:

   * `mongodb.url`: The connection address of the MongoDB instance, which must be enclosed in single English quotes. The format is `mongodb://<user>:<password>@<host:port>/ycsb?replicaSet=<replicaSetName>&w=1`. For information on how to obtain the connection address, refer to [Viewing connection address](https://docs.byteplus.com/en/docs/mongodb/addresses-introduction).

   * `recordcount`: The total number of records loaded into the MongoDB instance. Replace this parameter with the actual value based on the test scenario.

   * `operationcount`: The total number of operations for read/write tests, usually consistent with the `recordcount` value. Replace this parameter with the actual value based on the test scenario.

   * `readproportion`: The proportion of read operations, with a value range of 0 to 100. Replace this parameter with the actual value based on the test scenario.

   * `updateproportion`: The proportion of write operations, with a value range of 0 to 100. Replace this parameter with the actual value based on the test scenario.


<span id="6ghnPCBC"></span>
## Test results

<span id="Q3sKHq1y"></span>
### Measurement metrics


|**Measurement metrics** |**Unit** |**tip** |
|---|---|---|
|Throughput |ops/s |Client test throughput (that is, the number of read and write operations). |
|RAL |μs |Average latency of read operations. |
|WAL |μs |Average latency of write operations. |


<span id="fgawPcOH"></span>
### Test results details

Based on the test scenarios and configurations above, we tested instances on both physical server and volume architectures. The results are as follows.


<Tabs>
<Tab zoneid="8VU6KtdP" title="Physical server instances">
<TabTitle>Physical server instances</TabTitle>

**Load**


|**Instance specification** |**Throughput (ops/s)**  |**RAL (μs)**  |**WAL (μs)**  |
|---|---|---|---|
|2 cores 4 GiB |8465 |\- |940 |
|4 cores 8 GiB |16737 |\- |951 |
|8 cores 16 GiB |28690 |\- |1110 |
|16 cores 32 GiB |44069 |\- |1447 |
|16 cores 64 GiB |33403 |\- |2869 |


**100:0**


|**Instance specification** |**Throughput (ops/s)**  |**RAL (μs)**  |**WAL (μs)**  |
|---|---|---|---|
|2 cores 4 GiB |18488 |429 |\- |
|4 cores 8 GiB |35370 |448 |\- |
|8 cores 16 GiB |61968 |638 |\- |
|16 cores 32 GiB |92147 |688 |\- |
|16 cores 64 GiB |71877 |1329 |\- |


**95:5**


|**Instance specification** |**Throughput (ops/s)**  |**RAL (μs)**  |**WAL (μs)**  |
|---|---|---|---|
|2 cores 4 GiB |13128 |586 |990 |
|4 cores 8 GiB |26439 |581 |992 |
|8 cores 16 GiB |48214 |807 |1083 |
|16 cores 32 GiB |72593 |852 |1311 |
|16 cores 64 GiB |57930 |1600 |2661 |


**50:50**


|**Instance specification** |**Throughput (ops/s)**  |**RAL (μs)**  |**WAL (μs)**  |
|---|---|---|---|
|2 cores 4 GiB |7629 |780 |1308 |
|4 cores 8 GiB |15751 |748 |1274 |
|8 cores 16 GiB |28706 |844 |1413 |
|16 cores 32 GiB |47265 |943 |1752 |
|16 cores 64 GiB |38708 |1544 |3403 |


**5:95**


|**Instance specification** |**Throughput (ops/s)**  |**RAL (μs)**  |**WAL (μs)**  |
|---|---|---|---|
|2 cores 4 GiB |5393 |942 |1507 |
|4 cores 8 GiB |11415 |875 |1424 |
|8 cores 16 GiB |21139 |844 |1542 |
|16 cores 32 GiB |31959 |923 |2051 |
|16 cores 64 GiB |23262 |1540 |4255 |


**0:100**


|**Instance specification** |**Throughput (ops/s)**  |**RAL (μs)**  |**WAL (μs)**  |
|---|---|---|---|
|2 cores 4 GiB |5265 |\- |1515 |
|4 cores 8 GiB |11415 |\- |1451 |
|8 cores 16 GiB |20426 |\- |1560 |
|16 cores 32 GiB |30776 |\- |2072 |
|16 cores 64 GiB |18120 |\- |5290 |





</Tab>
<Tab zoneid="aheszt4f" title="Volume instances">
<TabTitle>Volume instances</TabTitle>

**Load**


|**Instance specification** |**Throughput (ops/s)**  |**RAL (μs)**  |**WAL (μs)**  |
|---|---|---|---|
|2 cores 4 GiB |11830 |\- |672 |
|4 cores 8 GiB |18843 |\- |844 |
|8 cores 16 GiB |27469 |\- |1160 |
|16 cores 32 GiB |46829 |\- |1362 |
|16 cores 64 GiB |29071 |\- |3297 |


**100:0**


|**Instance specification** |**Throughput (ops/s)**  |**RAL (μs)**  |**WAL (μs)**  |
|---|---|---|---|
|2 cores 4 GiB |28319 |255 |\- |
|4 cores 8 GiB |45338 |349 |\- |
|8 cores 16 GiB |79352 |400 |\- |
|16 cores 32 GiB |96126 |659 |\- |
|16 cores 64 GiB |85928 |1113 |\- |


**95:5**


|**Instance specification** |**Throughput (ops/s)**  |**RAL (μs)**  |**WAL (μs)**  |
|---|---|---|---|
|2 cores 4 GiB |17800 |427 |798 |
|4 cores 8 GiB |28387 |534 |1039 |
|8 cores 16 GiB |54050 |565 |1036 |
|16 cores 32 GiB |86080 |717 |1073 |
|16 cores 64 GiB |73731 |1250 |2187 |


**50:50**


|**Instance specification** |**Throughput (ops/s)**  |**RAL (μs)**  |**WAL (μs)**  |
|---|---|---|---|
|2 cores 4 GiB |8874 |675 |1120 |
|4 cores 8 GiB |16556 |700 |1224 |
|8 cores 16 GiB |31328 |756 |1275 |
|16 cores 32 GiB |39356 |1454 |1779 |
|16 cores 64 GiB |44814 |1693 |2567 |


**5:95**


|**Instance specification** |**Throughput (ops/s)**  |**RAL (μs)**  |**WAL (μs)**  |
|---|---|---|---|
|2 cores 4 GiB |6648 |801 |1219 |
|4 cores 8 GiB |11467 |912 |1274 |
|8 cores 16 GiB |23199 |1097 |1376 |
|16 cores 32 GiB |21739 |2835 |2939 |
|16 cores 64 GiB |27463 |1851 |3572 |


**0:100**


|**Instance specification** |**Throughput (ops/s)**  |**RAL (μs)**  |**WAL (μs)**  |
|---|---|---|---|
|2 cores 4 GiB |6315 |\- |1262 |
|4 cores 8 GiB |11508 |\- |1384 |
|8 cores 16 GiB |22445 |\- |1420 |
|16 cores 32 GiB |20563 |\- |3099 |
|16 cores 64 GiB |25690 |\- |3729 |





</Tab>
</Tabs>


<span id="MCkNO9ME"></span>
### Test result analysis


* **Read\-intensive scenarios (100:0, 95:5)** 

   Volume throughput outperforms local disks across all specifications, with the gap widening as the read percentage increases.

* **Write\-intensive scenarios (5:95, 0:100)** 

   The gap narrows, and volumes are still slightly better overall, especially at mid‑to‑low specifications.

* **Balanced read/write scenarios (50:50)** 

   Volumes perform better than local disks in most specifications and are about the same in a few.

* **Load scenarios**

   Local disks perform better than volumes, and the gap is larger at higher specifications.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">At 16 cores and 32 GiB, local disks outperform volumes in write‑intensive and read‑write balanced scenarios, since the I/O capacity can make full use of the direct‑connect advantage of local disks. When choosing this specification, it's recommended to evaluate it against your actual business model.</div>


* <div data-tips="true" data-tips-type="default">Overall, for read\-intensive or read\-write balanced workloads, volumes provide more stable performance; for write\-intensive workloads, especially high\-specification instances, local disks offer greater advantages in specific scenarios.</div>
