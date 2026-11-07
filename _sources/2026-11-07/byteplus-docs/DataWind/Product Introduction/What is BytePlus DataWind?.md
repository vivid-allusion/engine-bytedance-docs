---
title: "What is BytePlus DataWind?"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/What_is_BytePlus_DataWind"
---

<span id="_1-产品简介"></span>
# 1. Product overview

DataWind is an all\-in\-one data analysis and collaboration platform that supports self\-service analysis of data at the scale of hundreds of billions. It enables seamless integration across the entire process, from data ingestion, data integration, and query analysis to organization\-wide collaboration and sharing. Through visualizations such as data portals, digital dashboards, and management cockpits, it empowers business users to achieve DataWind and unlock the value of data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f089058a164e45de896355288f7bc7cb~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-产品介绍"></span>
# 2. Product introduction

The functional architecture of the DataWind product can be divided into the following six layers, viewed from the bottom up:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d76108a9a9c4a3a865d3b89a4ea1d98~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-1-数据接入"></span>
## 2.1 Data ingestion

Typically, the first step in a BI application is to complete **data source integration**. DataWind supports obtaining data from business databases, Excel/CSV files, business data entry on DataWind, external platform data (such as advertising domain, content domain, and so on), as well as real\-time and offline data warehouses. Currently, it supports more than 40 types of data connections.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2de6140320554d4fbe2b327442af3bad~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-查询引擎"></span>
## 2.2 Query engine

After completing the data connection, analysis and computation on the application side require the support of an analysis engine. DataWind supports two modes: one is the built\-in storage and computation engine ByteHouse, which enables self\-service analysis of massive datasets at the scale of hundreds of billions. In most analytical scenarios (such as grouping, proportion, comparison, sorting, and so on), the proprietary ByteHouse query engine delivers at least a hundredfold increase in computation speed. The other mode is the direct connection engine, which interacts directly with the database and can be used when database performance is sufficient.

<span id="_2-3-数据建模"></span>
## 2.3 Data modeling

After connecting to the data source, data can be loaded into the product by writing SQL or by loading raw tables directly into the product. However, these tables usually require some simple secondary processing to become analyzable datasets.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c7adfff239042669747976d7a6c7b29~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* For data that has already undergone complex processing and only requires simple data join/union operations, character type settings, filtering, and similar actions, simple data processing and editing can be performed at this stage to create datasets for analysis.

* When data processing is highly complex, it is necessary to build ETL pipelines. DataWind offers easy\-to\-use AI+BI visual modeling features for users with some data technical skills, such as feature engineering, machine learning, and natural language processing.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/868e4b5f826a491c95c0b6e2607b501b~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-数据分析"></span>
## 2.4 Data analysis

All operations in the data analysis phase are performed through mouse clicks and visual drag\-and\-drop actions, and data scripts are automatically parsed into visual charts. Currently, there is a rich chart library, flexible query and analysis capabilities, as well as simple and easy\-to\-use computational analysis features. At the same time, built\-in attribution algorithms help users gain insights into anomalies.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6c4bef572e264ae288c086a28a366adf~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-5-数据展示"></span>
## 2.5 Data presentation

For application endpoints, multi\-platform applications can be implemented, supporting analytics dashboards, mobile devices, embedding in other applications, and large screens for multi\-platform experiences. It is also deeply integrated with various common IM office products, such as Lark, DingTalk, and WeCom, enabling online collaborative data work.

<span id="_2-6-数据场景"></span>
## 2.6 Data scenarios

Data processed through the one\-stop data analysis and collaboration platform can ultimately be used in a variety of scenarios, including business decision analysis, market trend analysis, sales forecasting, growth analysis, inventory analysis, anomaly diagnosis, channel analysis, and user profiling insights.

<span id="_3-产品优势"></span>
# 3. Product advantages

<span id="2eb5c334"></span>
### 3.1 Product advantages

 **(1) Easy to use: No learning curve enables frontline staff to use it out of the box**

DataWind provide a no learning curve, visual interface, allowing each team within your company to easily complete data processing through drag\-and\-drop actions and build business data dashboards. According to different business scenarios, DataWind can also provide your company with DataWind achieving fully self\-service data analysis with no learning curve, and helping your company build a data\-driven culture for all employees. Currently, within ByteDance, DataWind supports self\-service analytics for almost all business lines, covering the vast majority of employees' self\-service analytics needs. It operates more than 200,000 active dashboards daily, supports over 5 million large\-scale data queries, and has surpassed 50,000 daily active users. Among some enterprise customers, daily active usage has also reached several thousand to over ten thousand.

 **(2) BI+AI: Large model capabilities and modeling and attribution analysis reveal business truth**

The analytics assistant provided by DataWind is built on large model capabilities, offering users an accessible data visualization query and analysis solution. It enables several core intelligent scenarios, such as natural language\-driven data insights and conversational, automated analysis guidance, reshaping the data analysis process, further expanding enterprise data consumption, and promoting data accessibility.

The visual modeling provided by DataWind allows business teams to build, schedule, and execute complex ETL tasks through visual drag\-and\-drop operations. By integrating AI components and data mining algorithms, complex data processing becomes simple.

The attribution analysis offered by DataWind uses built\-in algorithms to achieve one\-click business data attribution, automatically detects abnormal data, supports scenario\-based automatic attribution analysis and intelligent alert monitoring, and helps businesses uncover the real causes behind data fluctuations.

 **(3) Fast collaboration: Office integration enables efficient data collaboration**

DataWind is highly open and extensible, allowing tight integration with enterprise applications to meet personalized enterprise needs. In particular, collaboration with online office tools enables you and your team to access data insights anytime, anywhere, assign responsibility for issue follow\-up, and manage business risks. Specifically:


* **Office integration for online collaborative work**: DataWind can integrate with various office tools used by your company, such as DataWind, DingTalk, WeCom, and custom\-built enterprise apps. It pushes data anomalies to the relevant personnel or groups in real time or via monitoring alerts, ensuring that data anomalies are actively pushed to the responsible personnel or groups for timely action.

* **Embedded analytics, seamless integration with enterprise platforms**: DataWind can be seamlessly integrated into your proprietary enterprise platforms, providing embedded real\-time data, reports, dashboards, and more to achieve data interconnectivity.

* **Hierarchical data permission management**: DataWind can tailor an enterprise domain for each company, integrate with enterprise SSO, or provide a complete account system. Supports hierarchical permission management for all administrative levels within the enterprise; supports hierarchical authorization management for different projects across business lines and departments.


 **(4) Growth enablement: Matrix synergy to meet business growth needs**

Based on the robust product matrix of BytePlus, DataWind can be combined with growth marketing products to deliver marketing growth solutions such as private domain traffic operations, public domain traffic operations, and marketing growth analysis. It can also be integrated with data middle platform products to form end\-to\-end data solutions. Specifically:


* By leveraging DataWind, CDP, and GMP, we can build a **digital operations platform** for your enterprise. Through data analysis and insight, as well as refined audience segmentation, a more effective data\-driven business operation system can be established, enabling you to build a digital platform that connects multiple data sources and constructs an intelligent consumer growth system.

* We can leverage DataWind to conduct in\-depth data analysis, identify potential issues, and use product capabilities such as attribution analysis to pinpoint key user groups. These groups can be synchronized to the CDP for targeted insights and refined operations. Finally, by tracking and analyzing changes in key metrics based on CDP and DataWind, we can validate the results, continuously iterate on operational strategies, and truly achieve a closed loop from DataWinds to **decision\-making and execution** for you.

* We can closely integrate with data products such as DataLeap for data development and governance, and LAS for lakehouse analytics services, to build a **one\-stop data platform solution** for you, covering data ingestion, data integration, data asset management, and data application.


<span id="471cc519"></span>
### 3.2 Technical advantages

 **(1) High performance: Trillion\-level data volume, second\-level queries**

DataWind features a self\-developed, high\-speed columnar storage OLAP engine, ByteHouse, created by an expert team. This engine addresses the industry's performance challenges in large\-scale multidimensional data analysis, truly enabling second\-level queries on trillion\-level data volumes, and maximally meeting the massive data application needs of large groups or rapidly growing enterprises. At the same time, DataWind adopts technologies such as multi\-level data aggregation and hot/cold data tiering to further improve query performance and optimize storage costs.

 **(2) Big data: Highly scalable distributed cloud\-native architecture**

DataWind adopts a distributed cloud\-native architecture, with K8s containerized deployment and built\-in big data components such as Spark, Flink, and HDFS, offering strong scalability to support large\-scale data storage and computing. It also features strong openness, enabling integration and linkage with existing enterprise data platforms in modules such as data permissions and task scheduling, thereby achieving enterprise\-wide data interconnectivity.

 **(3) Real\-time: Experience real\-time data import and updates**

DataWind supports building real\-time data pipelines based on Kafka, Flink, and ByteHouse. Leveraging ByteHouse's proprietary UniqMergeTree, it supports real\-time data updates, improves data timeliness and visibility, helps enterprises perform real\-time data analysis, and enables the creation of real\-time data dashboards.

 **(4) Openness: Achieve data interconnectivity and customized requirements**

DataWind is highly open, providing comprehensive support for integration and deployment with customers' existing systems, including embedded analytics, plugin marketplace, data portal, office integration, and big data integration.

<span id="_4-产品流程"></span>
# 4. Product workflow

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f1104e6c840423398c0eca2ce5f12c9~tplv-goo7wpa0wc-image.image) </span>

<span id="_5-入门学习"></span>
# 5. Getting started

To quickly get started with DataWind for the first time, it is recommended to read [User Learning Paths](https://docs.byteplus.com/docs/DataWind/User_Learning_Paths).
