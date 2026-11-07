---
title: "Overview"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/datasail-overview"
---

DataSail is a stable and efficient data synchronization platform dedicated to providing high\-speed and stable data synchronization capability between rich heterogeneous data sources. It supports the entire process of real\-time data reception, processing, and distribution. Currently, it supports more than thirty heterogeneous data sources with incremental, full, and upsert solutions for stable and high\-speed batch and streaming data synchronization under various complex network environments.

<span id="_1-使用限制"></span>
## 1 Usage Restrictions


* Support is limited to structured data synchronization (e.g., RDS), and semi\-structured or unstructured data (HDFS, TXT, etc., the specific synchronization data must be abstracted into structured data). Data integration only supports data synchronization that can be abstracted into logical two\-dimensional tables; it does not support synchronizing completely unstructured data stored in TOS to LAS.

* The Exclusive Integrated Resource Group is located in the BytePlus VPC network. If the data source is in a classic network, the network between the data source and the Exclusive Resource Group cannot be connected. It is suggested that you migrate the data source to the VPC network as the current version requires that the data source and the data integration resource group are in the same VPC network.

* **Data integration tasks rely solely on the Exclusive Data Transmission Service Resource Group**. Therefore, before using the dataset functionality, you need to first create an Exclusive Data Transmission Service Resource Group in the Tenant Console.

* When sub\-users have different permission policies such as DataLeapSailReadOnlyAccess, DataLeapSailFullAccess, and DataLeapFullAccess, related data integration operations will be restricted accordingly, see [Permission descriptions](https://docs.byteplus.com/docs/dataleap/datasail_permission).


<span id="_2-离线集成简介"></span>
## 2 Batch Integration Overview

The provided batch data synchronization capability supports synchronizing data from the source database to the target database according to the scheduling interval, achieving data transfer between heterogeneous data sources.

See details:[Batch data synchronization](https://docs.byteplus.com/docs/undefined/68995f6b838a1e0515795823).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In data integration tasks, datasets related to Hive, HDFS, Doris, and StarRocks in EMR clusters support cluster versions other than EMR\-2.X.</div>


<span id="_3-流式集成简介"></span>
## 3 Streaming Integration Overview

The provided streaming data synchronization ability synchronizes data from the source database to the target database in real time, ensuring the target database consistently mirrors the source database.

See details:[Streaming data synchronization](https://docs.byteplus.com/docs/undefined/689966c7f35d1404fa275c8b).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In data integration tasks, datasets related to Hive, HDFS, Doris, and StarRocks in EMR clusters support cluster versions other than EMR\-2.X.</div>


<span id="0881807b"></span>
## 4 Solution Overview

Global DataSail Integration Solution, supports full database synchronous in real\-time, sub\-database sub\-table division in real\-time, batch full database synchronization, real\-time data collection, and near\-real\-time full database synchronization solutions:


* [Real-time full database synchronization (new version)](https://docs.byteplus.com/docs/undefined/689b1aeca8453604ecb6337b):A one\-click, real\-time full\-database synchronization solution supports all\-incremental, integrated synchronization between various data sources. The plan first synchronizes the full amount of source data through offline tasks, then collects the data to the target database via real\-time incremental sync tasks.

* [Real-time database and table sharding (new version)](https://docs.byteplus.com/docs/undefined/689b193ea8453604ecb62a9a):A one\-click real\-time sub\-database sub\-table solution, supporting the synchronization of tables with the same Schema from multiple instances in multiple databases, to a single table at the target side with one click.

* [Offline full database synchronization (new version)](https://docs.byteplus.com/docs/undefined/689b1adaf37c16052e13023e):The offline full\-database synchronization plan can periodically and synchronize the entire database's table data to the target side. This plan includes five types: Offline Full\-Database Synchronization (One\-time Full),Offline Full\-Database Synchronization (Periodic Full),Offline Full\-Database Synchronization (One\-time Incremental),Offline Full\-Database Synchronization (Periodic Incremental),Offline Full\-Database Synchronization (One\-time Full Periodic Incremental).

* [Real-time data collection plan (new version)](https://docs.byteplus.com/docs/undefined/689b1727c8e31605211d21b3):The real\-time data collection plan supports the real\-time collection of incremental data from the source database to the message queue. When the incremental data is large or fluctuates, it is recommended to perform intermediate data caching steps first.


<span id="_4-数据源"></span>
## 5 Data Sources

The data sources for data synchronization need to be registered under the project console first, and network connectivity tested. After successful registration, the data source can be used in data integration tasks.


* Batch data sources include: MySQL, HDFS, Hive, LAS, SQLServer, Oracle, TOS, etc.;

* Streaming data sources include: Kafka, BMQ, DataSail, RocketMQ, and others.


See [Supported data sources](https://docs.byteplus.com/docs/undefined/68a557100b8de0051050c0e3)

<span id="_5-网络联通方案"></span>
## 6 Network Connectivity Solutions

Before using the data synchronization feature, ensure that the Data Integration Resource Group is connected to the database network. Based on the network environment of the database, choose an appropriate network solution to establish connectivity.

The current network environments for databases include Private network (VPC), public network, and local IDC network.


* Private network: Unlike traditional classic networks, a Private Network VPC (Virtual Private Cloud) is a customizable virtual network environment that creates isolation for cloud resources and is self\-configured and managed.

* Public network: A database type that supports access to the public network.

* Local IDC network: Your own locally constructed data center network environment, isolated from cloud resources.


For different network solutions, see details:[Network connectivity solution](https://docs.byteplus.com/docs/dataleap/network_connectivity_solution).

<span id="_6-任务运行参数说明"></span>
## 7 Task Operating Parameters Description


* Expected Maximum Concurrency:

   Within a DataSail task, this specifies the maximum number of threads that can be used to concurrently read data from the source or write data to the target. The concurrency value affects data synchronization efficiency, but due to factors such as resource constraints and task characteristics, the actual concurrency value may be less than or equal to this value. The desired maximum concurrency value only limits the maximum concurrency value and does not represent the actual concurrency value. The actual concurrency value is allocated based on the available resources in the integrated resource group.

   If you want to specify the actual concurrency value, you can use the advanced parameters: job.reader.reader_parallelism_num and job.writer.writer_parallelism_num.See [Advanced parameters](https://docs.byteplus.com/docs/dataleap/advanced_parameters).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you don't specify a concurrency limit using advanced parameters, the actual concurrency is automatically calculated. Actual concurrency = min(automatically calculated concurrency，expected maximum concurrency).   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you specify a concurrency limit using advanced parameters, the actual concurrency = min(specified read and write concurrency，expected maximum concurrency).   </div>
   

* Dirty Data:

   Data that fails field mapping during data integration tasks and is rejected due to issues like invalid format or exceptions during data transfer from source to target database is considered "dirty data." For example, data fails to be written when trying to write String type source data into an INT type target field due to inappropriate type conversion.

   Dirty data will not be successfully written to the destination. You can configure the maximum tolerance number/percentage of dirty data during synchronization task configuration. If configured to 0, no dirty data is allowed, and the task will fail and exit.
