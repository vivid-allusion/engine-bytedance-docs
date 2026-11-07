---
title: "EMR Serverless use cases"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_Serverless_use_cases"
---

<span id="8b73f2fe"></span>
## EMR Serverless queue use cases

<span id="0d2b2ed8"></span>
### Cloud data warehouse construction

**Cloud data warehouse**

Driven by rapidly growing business needs, enterprises build data warehouses to enable agile iteration, achieve low\-cost adaptation between open\-source systems and legacy systems, break down data silos, and meet large\-scale data processing scenarios.


* **Professional cloud migration:**  Tool\-based migration solutions support multi\-source data migration to the cloud, site relocation, and synchronization.

* **Efficient data construction:**  Seamless integration with DataLeap enables integration, development, and operations governance for comprehensive data infrastructure.

* **Diverse data warehouse applications:**  Integration with the internal ecosystem enables BI reporting, OLAP analysis, and data exploration.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5868ef3765334141abfb1d02ec1c354f~tplv-goo7wpa0wc-image.image) </span>

<span id="7f516c09"></span>
#### Big data log analytics

Helps enterprises better understand business operations, identify issues and optimization opportunities, and thereby improve operational efficiency and decision quality, such as network security analysis, application performance analysis, business analysis, and marketing analysis.


* **Extreme cost optimization:**  Cloud\-native lakehouse architecture with storage\-compute separation and hot\-cold tiering enables precise cost control.

* **Reduced operations overhead:**  Addresses log collection, real\-time and offline processing and analysis, eliminating unnecessary operations.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3bce477bbad44a087b16f643c5d9103~tplv-goo7wpa0wc-image.image) </span>

<span id="1395d6ec"></span>
#### **Refined operations**

Supports industries such as e\-commerce, finance, automotive, and gaming to mine data assets, unlock data value, and help enterprises improve operational efficiency, decision quality, precision services, and customer satisfaction, while significantly reducing operational costs.


* **In\-depth business data mining:**  Supports EB\-level massive data analytics and refined analysis and operations for hundreds of millions of Daily Active Users (DAUs).

* **Timely business insights:**  Real\-time elastic scaling and high\-performance computing engines meet sudden business growth.

* **Rapid response to business needs:**  Seamless integration and rich ecosystem meet diverse requirements for rapid business iteration.


<span id="f809d761"></span>
### Hybrid cloud architecture solutions

<span id="88ffc8cb"></span>
#### Background note

Hybrid cloud refers to an architecture in which applications and data platforms are deployed using both public and private clouds simultaneously. This architecture allows enterprises to manage cluster capacity according to their development stage and specific business needs, routing workloads to the public cloud during peak periods to achieve flexible scaling and pay\-as\-you\-go IT costs.

By upgrading to this architecture, enterprises not only achieve flexible resource allocation and scaling, but also ensure that sensitive data and critical workloads are controlled within the private cloud. This helps reduce the scale and cost of private infrastructure, and cleverly enables high availability and disaster recovery capabilities for IT.

<span id="4525faa9"></span>
#### Scenario overview

The customer is a leading online education technology company in China. The data platform department is dedicated to building a unified data service platform, with more than 10,000 CPU cores in machines providing data services within the IDC. With the rise of emerging businesses and the development of overseas operations, the computing resources of the data platform are severely overloaded between 9:00 and 11:00 every morning, resulting in significant task queuing and backlog. From the end of 2023 to Q1 2024, the customer worked closely with the BytePlus EMR team, going through several stages including research, adaptation, trial operation, and official launch. The solution is now successfully online. By the end of April, the customer's peak daily cloud computing usage is expected to reach 2,000 cores, with more than 8 hours of elastic computing usage per day. This has greatly shortened the construction cycle of the customer's IDC, improved platform stability, and reduced computing costs.


* Customer Hadoop infrastructure: Hadoop: 3.3.4, Spark: 3.3.3, Kyuubi: 1.7.3

* Core requirements: cost reduction, elastic scaling, and integration capabilities for monitoring/logging and other ecosystem components


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7678530d4cf46e3882500a45858a031~tplv-goo7wpa0wc-image.image) </span>

<span id="281c2382"></span>
#### Main capability highlights


1. **Unified Submit Job interface**

* **Web service**: Provides a unified API and service, allowing users to Submit Job from different cloud environments, including private cloud.

* **Client library**: Provides client libraries for Java and other programming languages, simplifying the Submit Job process.

* **Authentication and authorization**: Integrates mechanisms such as OAuth and Kerberos to ensure that only authorized users can Submit Job.

2. **Network communication layer**

* **VPN/VPC**: Establishes cross\-cloud virtual private networks through cloud infrastructure to ensure secure and isolated data transmission.

* **Data transfer optimization**: Utilizes technologies such as compression and encryption to improve the efficiency and security of data transmission.

3. **Data management layer**

* **Data synchronization service**: Provides cross\-cloud data synchronization capabilities to ensure data consistency.

* **Data lake integration**: Supports multiple data lake solutions, such as Amazon S3 and Azure Data Lake.

4. **Job scheduler**

* **Kyuubi Server**: Acts as the core of job scheduling, receiving job submission requests and distributing jobs to the appropriate computing resources.

* **Multi\-tenancy support**: Kyuubi's multi\-tenancy feature allows different users or teams to share computing resources while maintaining isolation.

* **High availability**: Ensures high availability of Kyuubi Server through service discovery and load balancing mechanisms.

5. **Monitoring and logging system**

* **Monitoring interface**: Provides a real\-time job monitoring interface that displays job status, resource usage, and performance metrics.

* **Log collection**: Collects job execution logs to facilitate troubleshooting and performance analysis.

* **Alert mechanism**: Sets alert rules to send notifications when job execution is abnormal or resource usage exceeds limits.


<span id="16a6c9da"></span>
#### Product advantages


* **Distributed and multi\-tenancy support**: Kyuubi's design enables robust support for distributed environments and multi\-tenancy scenarios, allowing each tenant to have their own resource configuration and isolation strategy.

* **High availability and load balancing**: Communication between Kyuubi Server and Engine supports service discovery and load balancing, ensuring high availability and strong performance of the system.

* **Flexible resource sharing levels**: Kyuubi supports different levels of resource sharing, such as each connection or each user exclusively using an engine, or all users sharing a single engine, providing flexible options for various business scenarios.

* **Byte internal engine capabilities:**  EMR Serverless uses Byte's continuously optimized Spark and other engines at its core, delivering 2.7 times the performance compared to open\-source engines. It also integrates Byte's Native Engine Bolt by default, providing an additional performance boost of nearly 40% over the original Java version.


<span id="9d862e45"></span>
#### Solution value


* Out\-of\-the\-box

* Elastic scaling, resource response within seconds

* Unlimited resource scaling; Pay\-As\-You\-Go offers greater flexibility than purchasing resources

* Technology stack aligned with IDC, transparent to business, experience consistent with self\-built solutions


<span id="7c4ae09d"></span>
### Real\-time SQL analysis

As big data technology evolves rapidly, SQL remains the core tool for large\-scale data processing and analysis due to its versatility and ease of use. Within the big data SQL ecosystem, Hive serves as a classic technical foundation. Through its SQL\-like HiveQL interface, users can aggregate, perform ad hoc queries, and conduct offline analysis on massive data stored in HDFS and compatible storage systems without needing to understand the intricacies of distributed computing. Hive continues to be a crucial cornerstone for enterprises building data warehouses.

However, when data scales exceed TB and reach PB levels, and businesses demand real\-time and interactive query responses, the traditional batch processing mode of Hive can no longer meet these requirements. To address this challenge, **Presto** emerged as a SQL engine optimized for real\-time big data queries. Through technological innovation, it retains SQL's ease of use while enabling efficient analysis of large\-scale data, making it the core choice for real\-time SQL scenarios.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d14b2ee770df4b1592dfff8f06cf3914~tplv-goo7wpa0wc-image.image) </span>

<span id="8f1a5962"></span>
## EMR Serverless instance use cases

StarRocks/Doris can handle multidimensional analysis, high\-concurrency queries, pre\-calculation, and real\-time analytical queries with a single system, reducing system complexity and the cost of developing and maintaining multiple technology stacks. StarRocks/Doris adopts an MPP (massively parallel processing) architecture, fully utilizing all node resources and significantly improving query performance.

<span id="f3cec9a2"></span>
### **Real\-time data warehouse**

Real\-time data warehouses have high requirements for data timeliness, data serving, and concurrency, which offline analysis systems cannot meet. StarRocks supports real\-time data updates and deletions, making it suitable for scenarios that require frequent data updates:


* Supports streaming ingestion, with data visible within seconds;

* Supports high\-concurrency data services, supporting tens of thousands of QPS;

* Second\-level or sub\-second data query performance;

* Supports real\-time aggregation of Data Metrics and multidimensional analysis.


Enterprises can build real\-time data warehouses based on EMR Doris/StarRocks. After data is ingested, it undergoes streaming computation; detailed data enters the ODS layer of the Doris/StarRocks cluster, aggregated data enters the DWS layer, and Data Metrics are stored in the ADS layer after computation. Data supports online updates. Doris/StarRocks provides services for the data application layer, supporting both online and offline query analysis, and supporting hundreds of thousands of QPS.

<span id="0024840e"></span>
### OLAP multidimensional analysis

StarRocks is a high\-performance analytical database designed specifically for OLAP (Online Analytical Processing) queries. It can be integrated with various BI (Business Intelligence) tools, which means StarRocks can be used as a data source for direct data querying and analysis within these tools. This integration capability enables enterprises to leverage StarRocks's powerful analytical features together with the visualization and reporting functions of BI tools, allowing for more effective data insights and decision\-making.

StarRocks supports standard SQL interfaces, making it easy to connect with various BI tools such as Tableau, Power BI, Looker, and more. These tools typically provide graphical interfaces, enabling users to build complex queries and dashboards through drag\-and\-drop operations without writing complex SQL code. StarRocks's high\-performance query engine ensures that BI tools can quickly respond to user query requests and deliver real\-time data analysis results, even when processing large\-scale datasets. StarRocks's compatibility is not limited to traditional BI tools; it also supports integration with modern, cloud\-based BI platforms such as BytePlus Intelligent Data Insight Platform DataWind. This broad compatibility allows StarRocks to adapt to different business scenarios and technology stacks, providing users with flexible options for data access and analysis.

By leveraging StarRocks and its standardized integration capabilities with various BI tools, enterprises can support their data analytics platform use cases, enabling management decision\-makers and data analysts to extract value from data more intuitively and rapidly, thereby supporting business decisions.

<span id="0e03c340"></span>
## Serverless Presto use cases

In the era of big data, SQL, as the universal language for data analytics, plays a pivotal role in processing large\-scale datasets. Despite the rapid evolution of big data technologies, Hive remains a solid cornerstone in the big data SQL domain. It provides a SQL\-like query interface—HiveQL—which allows users to easily aggregate, perform ad hoc queries, and analyze large\-scale data stored in HDFS or other compatible storage systems, without needing to deeply understand the complexities of underlying distributed computing. Presto integrates with Hive Metastore to obtain metadata information for Hive tables. Presto's Hive connector enables direct communication with Hive Metastore, allowing access to metadata such as schema, table names, and column names of Hive tables, and uses this information to build query plans and determine data locations.

When dealing with data at the terabyte or even petabyte scale, Presto is purpose\-built and optimized for big data queries. It retains the ease of use of SQL and introduces numerous innovative technologies to achieve efficient querying of large\-scale data. Presto fully utilizes the high\-speed memory of modern hardware, storing intermediate results in memory instead of traditional disks, which greatly reduces I/O operations and significantly improves query speed. Presto's SQL syntax is closer to traditional SQL, making it excel in interactive query and real\-time analytics scenarios, while Hive is more suitable for batch processing and offline analytics scenarios.

Presto performs exceptionally well in scenarios requiring fast, interactive queries across multiple data sources, such as ad hoc analytics, business intelligence reporting, and real\-time data exploration. The ability to connect to multiple storage systems without requiring ETL makes it an ideal choice for building a unified data access layer and enabling cross\-source analytics.

Serverless Presto supports rapid deployment and event\-driven operation, perfectly aligning with the event\-driven model of the Serverless architecture. In terms of fault tolerance and simplified deployment, the stateless nature makes it easier for Serverless applications to achieve high scalability, provides stronger fault tolerance, and also simplifies deployment and maintenance.

Enterprises can choose to use Serverless Presto at the initial stage of building a data warehouse, and it also supports deploying Presto on an existing data warehouse. Cross\-source queries between Presto and the original data warehouse can be achieved through simple metadata configuration. When submitting queries, users can select Presto or Spark based on the use case and the data to be queried.

In summary, Presto offers significant advantages over Hive in query speed, in\-memory computation, data source support, SQL syntax, built\-in functions and operators, performance optimization, and use cases. These advantages make Presto an ideal choice for interactive data analysis, especially in use cases that require real\-time or near real\-time results.
