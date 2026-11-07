---
title: "EMR on ECS use cases"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_on_ECS_use_cases"
---

<span id="应用场景"></span>
## Use cases

<span id="_1-云原生数据湖仓"></span>
### **Cloud\-native data lakehouse**

The data lakehouse is a new type of data architecture that combines a data lake and a data warehouse, enabling more flexible, efficient, and scalable data management. It helps enterprises better understand and utilize their data assets, enhancing business value. For example, in the internet industry, enterprises need to build a data analytics platform to aggregate app and log data, analyze customer behavior to support precision marketing, and assist in decision\-making analysis. However, when building an open\-source big data platform in\-house, enterprises often face challenges such as significant workforce investment in management and maintenance, high resource costs, and lack of flexibility.

BytePlus EMR provides a rich set of mainstream open\-source big data components, is 100% open\-source compatible, and supports seamless migration and long\-term evolution. It offers enterprise\-level component optimization and management capabilities, helping enterprises reduce development and operations costs and improve efficiency. A single architecture supports a comprehensive data lakehouse solution, enabling EB\-level data warehouses, in\-lake warehouse creation, and integrated lakehouse capabilities. In conjunction with BytePlus the big data development and governance suite DataLeap and the full\-domain data integration product DataSail, a one\-stop data integration, development, and governance solution can be achieved.

<span id="_2-实时数仓"></span>
### **Real\-time data warehouse**

The real\-time data warehouse has high requirements for data timeliness, data serving, and concurrency. Offline analytics systems cannot meet these needs. The real\-time data warehouse scenario has the following characteristics:


* Supports streaming data ingestion, with data visible within seconds;

* Supports high\-concurrency data services, with tens of thousands of QPS;

* Second\-level or sub\-second data query performance;

* Supports real\-time Data Metrics aggregation and multidimensional analysis.


Enterprises can build a real\-time data warehouse based on EMR Doris/StarRocks. After data is ingested, it undergoes streaming computation. Detailed data enters the ODS layer of the Doris/StarRocks cluster, aggregated data is computed and enters the DWS layer, and Data Metrics are calculated and stored in the ADS layer. Data supports online updates. Doris/StarRocks provides services for the data application layer, supporting online and offline query analysis, with hundreds of thousands of QPS.

<span id="_3-离线-批量数据分析"></span>
### **Offline/batch data analysis**

Offline processing and analysis of massive data is a common scenario in big data analytics systems. Enterprises collect, import, clean, and transform data from various types of business system data sources, then process and organize it to meet the requirements of business analysis models. This supports each business department in making analytical decisions based on unified and centralized data. The offline/batch data analysis scenario has the following characteristics:


* Large data volumes, typically reaching the TB to PB scale;

* Different types of data sources exist, such as files, logs, and structured data;

* Data processing timeliness requirements are at the level of tens of minutes, hours, or days, with low real\-time demands;

* Massive data processing adopts distributed parallel processing, and computing and storage resources can be flexibly scaled based on data volume.


For example, in the internet industry, multiple data sources such as online banking logs, marketing systems, and transaction systems are collected to analyze and count customer behavior, supporting precision marketing applications. After enterprises extract the required data to the big data platform, it is stored in Hive/HDFS, or stored in object storage TOS using a compute\-storage separation architecture. Every day at fixed times, data is processed through Hive/Spark computing engines to generate relevant application metrics and statistical data, which are made available for data application access on T+1 day.

<span id="_4-实时-流式计算"></span>
### **Real\-time/streaming computing**

With the growth of business demands such as IoT, real\-time risk control, and real\-time monitoring, real\-time data processing and analysis are becoming increasingly important in big data analytics scenarios. Data streams need to be collected and accessed in real time, then processed and analyzed in real time, and actions triggered accordingly. The real\-time/streaming computing scenario has the following characteristics:


* Extremely high processing time requirements, at the millisecond to second level;

* Processing data volumes reach hundreds of megabytes per second;

* Data formats are mainly various network protocol formats;

* High consumption of computing resources.


Taking the Internet of Vehicles industry as an example, enterprises collect driving and battery data from hundreds of new energy vehicles in real time. They then perform real\-time analysis and generate alerts. The data is collected with a granularity of one minute, and daily increments reach tens of gigabytes. Data is aggregated to the big data platform via Kafka or Pulsar message queues. Real\-time metric computation at the millisecond level is performed using the Flink stream processing engine. The computation results are stored in the OLAP engine or RDS for real\-time data display on the platform.
