---
title: "Serverless StarRocks TPC-H Note"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Serverless_StarRocks_TPC-H_Note"
---

<span id="tpc-h-基准测试说明"></span>
## TPC\-H Note

TPC\-H is a test suite developed by the Transaction Processing Performance Council (TPC) in the United States to simulate decision support applications. It includes a complete set of business\-oriented ad\-hoc queries and concurrent data modifications.

TPC\-H models real production environments and simulates a data warehouse for a sales system. This test contains a total of eight tables, with the data volume configurable from 1 GB to 3 TB. The benchmark includes 22 queries, with the main evaluation metric being the response time for each query, meaning the time required from submitting the query to receiving the result.

This article introduces the detailed procedure for executing the TPC\-H benchmark test on a Volcano Engine EMR Serverless StarRocks instance.

<span id="_1-创建serverless-实例"></span>
## 1. Create a Serverless instance

Refer to the documentation for creating a Serverless StarRocks instance: [Create instances](https://docs.byteplus.com/docs/E-MapReduce/109096)

<span id="_2-准备测试工具"></span>
## 2. Prepare the test tool


1. Download the test tool provided by Volcano Engine EMR.


<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f574b54026d63eab0e855b638a160f81.gz" name="tpch-tools-starrocks.tar.gz">tpch-tools-starrocks.tar.gz</Attachment>



2. Upload the test tool to the planned execution location. Recommended execution locations are as follows:

   1. Recommendation: Upload to the working directory of a Volcano Engine ECS within the same VPC as the Serverless instance, with network connectivity.

   2. Not recommended: Connecting to StarRocks via a public IP to perform performance testing, as this involves large volumes of test data transfer and significant network overhead.

3. Extract the test tool.


```shell
tar -xvf tpch-tools-starrocks.tar.gz
```


<span id="_3-开展-tpc-h-性能测试"></span>
## 3. Conduct TPC\-H performance testing

<span id="_3-1-build测试工具"></span>
### 3.1 Build the test tool

```shell
cd tpch-tools-starrocks
./bin/build-tpch-dbgen.sh
```


<span id="_3-2-修改配置文件"></span>
### 3.2 Modify the configuration file

```shell
vim ./conf/starrocks-cluster.conf
```


The configuration items are described as follows:


|Configuration item |Default value |Recommended configuration |Note |
|---|---|---|---|
|FE_HOST |127.0.0.1 |See the description below |StarRocks FE connection address |
|FE_HTTP_PORT |8030 |8030 |StarRocks FE HTTP port |
|FE_QUERY_PORT |9030 |9030 |StarRocks FE query port |
|USER |root |See the description below |StarRocks user |
|PASSWORD |Empty |See the description below |StarRocks user password |
|DB |tpch |tpch |Target database for StarRocks TPC\-H execution |


Recommended configuration:


* FE_HOST: Use the domain name or IP address indicated in the instance details page (internal address).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_960f7cce7456de3edf99f714511b79fa.png) </span>

* USER&PASSWORD: Refer to [User management](https://docs.byteplus.com/docs/E-MapReduce/109095) to create the corresponding engine user, and enter their username and password.


<span id="_3-3-生成数据"></span>
### 3.3 Generate data


* Use the test tool to generate test data, where:

   * {scale_factor} indicates the data scale and can be set to 1, 100, 1000, or 10000

   * Data generation takes a long time; it is recommended to run in the background without interruption.


```shell
nohup ./bin/gen-tpch-data.sh -s {scale_factor} &
```


<span id="_3-4-创建测试表"></span>
### 3.4 Create test tables


* Use the test tool to connect to the engine and create test tables, where:

   * {scale_factor} indicates the data scale, corresponding to the data scale specified during data generation, and can be set to 1, 100, 1000, or 10000

   * The test tool will connect to the engine based on the configuration file information modified in Step 2.


```shell
./bin/create-tpch-tables.sh -s {scale_factor}
```


<span id="_3-5-导入测试数据"></span>
### 3.5 Import test data


* Use the test tool to import test data into the engine. The import process takes a long time, so it is recommended to keep the backend running without interruption.


```shell
nohup ./bin/load-tpch-data.sh &
```


<span id="_3-6-执行查询"></span>
### 3.6 Execute queries


* Use the test tool to run the TPC\-H benchmark, which includes 22 SQL statements. The execution time is long, so it is recommended to keep the backend running without interruption. Specifically:

   * {scale_factor} indicates the data scale, corresponding to the data scale specified when generating data. You can enter 1, 100, 1000, or 10000.

   * By default, each SQL statement is executed three times, and the optimal performance result is output.


```shell
nohup ./bin/run-tpch-queries.sh -s {scale_factor} &
```
