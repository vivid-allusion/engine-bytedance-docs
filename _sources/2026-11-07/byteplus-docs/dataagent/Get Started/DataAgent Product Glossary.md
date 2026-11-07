---
title: "DataAgent Product Glossary"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/DataAgent_Product_Glossary"
---

This document explains the meanings of terms related to DataAgent to help you better understand and use the product.

<span id="a469ed39"></span>
# Intelligent agent


|Name |Definition |Alias |
|---|---|---|
|Intelligent agent |An AI system built on large language models (LLM) that can understand natural language, perform tasks, and interact with users through conversation, possessing autonomous decision\-making and learning capabilities. In this product, it refers to the Intelligent Analysis Agent or Intelligent Marketing Agent. |Agent |
|Intelligent Analysis Agent |The Intelligent Analysis Agent is an expert advisor based on AI deep reasoning and big data analytics, combining the deep reasoning capabilities of large models, flexible intelligent querying, and in\-depth research report functions. |Analysis Agent |
|Intelligent Marketing Agent |The Intelligent Marketing Agent is a comprehensive digital marketing intelligence tool built on AI deep reasoning and big data analytics, integrating two core modules: the Marketing Interaction Assistant and Intelligent Marketing Strategy. |Marketing Agent |
|Marketing Interaction Assistant |The Marketing Interaction Assistant is a conversational marketing hub that combines real\-time customer profile insights with an AI decision engine. It enables full\-scenario intelligent interaction from customer needs analysis, benefit recommendation, to profile updates through purchase intent identification, intelligent script generation, precise product recommendation, and end\-to\-end task automation. Closed\-loop management across multiple systems enhances customer conversion efficiency and operational precision. | |
|Intelligent Marketing Strategy Agent |The Intelligent Marketing Strategy Agent is a digital marketing decision hub based on AI deep reasoning and big data analytics. Through an intelligent closed loop of "goal input\-strategy generation\-task configuration\-dynamic optimization," it achieves full\-process automation from marketing element analysis, intelligent audience segmentation, to omnichannel strategy output, providing enterprises with an "AI chief strategist" decision system capable of second\-level response and continuous evolution. | |
|Natural language |Languages used daily by humans (such as Chinese and English); agents achieve human\-computer interaction by understanding and generating natural language. | |
|Prompt |Instructions or questions entered by users into agents to guide them in generating specific responses or performing tasks. Design quality directly affects output effectiveness. |Prompt keywords, instruction input |
|Large language model |Pre\-trained language models with a massive number of parameters (such as *Doubao*), possessing powerful natural language understanding and generation capabilities, serve as the core foundation of agents. |LLM, large language model |
|Enterprise knowledge engine |This is the dedicated knowledge hub for agents, centrally storing and managing various enterprise knowledge assets, and providing knowledge support for agents. Both the intelligent analysis agent and the intelligent marketing agent have enterprise knowledge engine capabilities.<br><br><br>* In the intelligent analysis agent: the enterprise knowledge engine is the dedicated knowledge hub for in\-depth research, supporting the upload of enterprise private documents. Through intelligent matching and structured extraction, internal knowledge is accurately injected into the analysis process. It complements online search, ensuring research conclusions are both timely and have business depth.<br><br>* In the intelligent marketing agent: the enterprise knowledge engine is the underlying capability of the marketing interaction assistant, providing end\-to\-end knowledge construction, management capabilities, and intelligent AI application capabilities. It supports enterprise\-level users in building general enterprise knowledge engines, customizing AI applications, and ensures data security through refined permission management. Includes general enterprise knowledge engine and main enterprise knowledge engine. |Knowledge base |
|Knowledge configuration |Knowledge configuration refers to the process of configuring knowledge for the enterprise knowledge engine of the intelligent analysis agent, supporting the upload of enterprise private documents. The configured knowledge will be automatically labeled as three types: business knowledge, analysis framework, and analysis report. | |
|Semantic model |A model that annotates and maps business\-related semantics for dataset metadata (such as names and fields), used to enhance agents' understanding of data and the accuracy of question answering. | |
|Unstructured data |Data without a fixed format (such as text, images, or videos); agents need to use multimodal technologies to process this type of data. |Heterogeneous data |
|Vectorization |Converting data into numerical vectors (embedding representations) enables agents to calculate semantic similarity and perform efficient retrieval. |Embedding representation, embedding |
|Dialogue |The process in which an agent and a user complete tasks through multiple rounds of natural language interaction. Maintaining context consistency is necessary for coherent communication. |Conversation |


<span id="be9d1e1a"></span>
# Dataset


|Name |Term definition |Alias |
|---|---|---|
|Dataset |A dataset refers to a data model composed of one or more tables and serves as the data source for agents. Before configuring data for an agent, it is necessary to establish a data connection in the "Dataset" module, import the data into DataAgent, and complete data vectorization. | |
|Full table |A full table is a data storage or partitioning method whose core feature is that, in each partition (usually divided by date or other time dimensions), it stores all the latest status data of the research object or business entity as of the date corresponding to that partition. | |
|Incremental table |An incremental table is a data partitioning method opposite to a full table. Its characteristic is that, in each partition (usually divided by time period), only the data added or changed during that period is stored, rather than all data as of that period. | |
|Associated dataset |An associated dataset refers to multiple datasets that are linked through field matching and can be used together according to business scenarios, thereby forming a dataset that meets specific data requirements. | |
|Field |Fields include two attributes: dimension and metric.<br><br><br>* A dimension is a perspective for dividing and analyzing data and refers to a non\-aggregated field (such as date, author UID, and so on).<br><br>* A metric is an attribute that measures data through various aggregation methods and is often presented in numerical form (such as the number of submissions by an author). | |
|Expression |An expression can be written in SQL and is used to obtain target data. For example, the original table contains the field price (with a value of 19.99). Using round(price) produces the integer amount field rounded_price (with a value of 20). | |
|Function |A function is a predefined operation that can be invoked during data processing to implement various data processing capabilities, such as the toMonth and toDateTime functions used for time conversion in the above expression. | |
|Synchronization |Periodically transfer data from the specified database to the DataAgent database.<br><br><br>* Scheduled synchronization: You can set the start time to synchronize data on a schedule, and historical data synchronization is supported.<br><br>* Manual synchronization: Only the initial synchronization is performed, and subsequent updates are not automatic. To synchronize again, you must manually click the "Synchronize" button. | |
|Dependency |A dependency refers to the correlation between different nodes or tasks in data processing workflows. This correlation determines the execution order and conditions of tasks, ensuring the orderly and effective processing of data. Dependencies are mainly divided into two types: scheduling dependencies and recommended dependencies.<br><br><br>* Scheduling dependencies typically refer to the upstream and downstream relationships between periodic scheduling nodes during data synchronization and data development. Tasks are scheduled to run upstream and downstream nodes in an orderly manner based on node dependencies. That is, downstream nodes are only started after upstream nodes have run successfully, ensuring timely production of valid business data.<br><br>* Recommended dependencies refer to cases where, in partitioned LAS data sources, the system can automatically construct data source partition detection tasks and automatically configure scheduling dependencies. When the detection task verifies that the upstream partition is ready, it will actually trigger the execution of the day's task instance (this dependency type is not supported for data sources without partitions). | |
|Parameter |A parameter is a variable that can be flexibly adjusted and applied to calculated fields, enabling dynamic logic solutions for a single calculated field or an entire chart. When the parameter value changes, the calculation logic corresponding to the field expression also changes. | |
|Primary key |The primary key is the field or combination of fields in a dataset used to uniquely identify each record. After setting the primary key, data can be quickly located and retrieved, thereby improving query efficiency. | |
|Partition |Partitioning is a mechanism that divides a dataset into multiple independent parts in physical storage according to specific rules, such as time, region, and so on. By partitioning, the amount of data scanned during queries can be reduced, system processing pressure can be distributed, and data query and management efficiency can be improved. This is especially suitable for large\-scale datasets. | |
|Shard |Sharding is a method of splitting a dataset and evenly distributing it across multiple nodes in a distributed storage environment according to the rules of the sharding field. The core purpose is to avoid performance bottlenecks caused by centralized storage of data, and to improve data query and processing speed through parallel processing across multiple nodes. | |
|Sampling field |A sampling field is a specific field used as the basis for sampling when performing sample queries on a dataset. The system performs a HASH operation on this field by default to select a portion of data samples, thereby ensuring that the query results are representative while reducing the amount of data processed and improving query response speed. | |
|Sampling ratio |The sampling ratio refers to the proportion of data samples extracted based on the sampling field in a visualization query relative to the total amount of data in the dataset. The smaller this ratio, the fewer samples are extracted, resulting in lower computational and transmission load during queries and faster response speed for visualization queries. | |
|Data lifecycle |The data lifecycle refers to the management mechanism in which, throughout the entire process from the generation to the cleanup of a dataset, the system automatically cleans up useless or expired data according to preset date rules, such as retention duration, cleanup cycle, and so on, in order to reasonably release storage resources and ensure efficient system operation. | |


<span id="c76aaf98"></span>
# Visual modeling


|Name |Term definition |Alias |
|---|---|---|
|Data modeling |The process of cleansing, processing, and producing metadata according to a specific data processing logic is called data modeling. |Data processing |
|Canvas |The core interface for visual modeling, which supports constructing data processing workflows by dragging operators and establishing connections. | |
|Operator |Functional module units on the canvas that provide specific capabilities such as data input, processing, computation, or output, presented in the form of blocks. | |
|Connection |A directed arrow connecting two operators on the canvas, indicating the direction of data flow and dependency relationships. | |
|Dataset |The foundational modeling tool for data preparation, offering basic multi\-table association data modeling capabilities. It also serves as a data container that can be used by products, including ClickHouse datasets and Hive datasets. | |
|Real\-time task |A visual modeling task for instant processing and computation of continuously updated data streams, typically used in real\-time analytics scenarios. |Streaming task |
|Offline task |A visual modeling task executed based on periodically updated data sources (such as daily or hourly), relying on scheduled or manual triggers to run. | |


<span id="1157a0a9"></span>
# Data connection


|Name |Term definition |Alias |
|---|---|---|
|Data connection |Used to configure communication parameters with external data sources, establishing a connection channel between the system and databases or data services. This is a prerequisite for data querying, analysis, and modeling. |Data source integration |
|Data source |A storage system or service that provides data, including relational databases, NoSQL, and more. Access requires configuration through a data connection. |Database |
|Extraction |The process of extracting data from source systems (such as databases, files, APIs, and so on) and transferring it to target storage or computing engines.<br><br><br>* Offline extraction: Extracts data offline into the DataAgent's built\-in high\-performance storage and computing engine. Most supported databases currently support offline extraction by default.<br><br>* Real\-time extraction: Extracts data in real time into the engine for storage, supported only for data sources such as Kafka and Pulsar. | |
|Direct connection |Directly access the source database to execute queries, leveraging the database's native computing capabilities to avoid the overhead of data migration. | |
|Server |The network address of a physical or virtual host that provides data services; it is one of the core parameters in data connection configuration. |Host, IP address |
|Port |The network port number on the server used for communication with specific services (for example, the default for MySQL is 3306), which, together with the server address, forms the connection endpoint. |Communication port |
|VPC |Virtual Private Cloud (VPC), which provides an isolated network environment for data connections, ensuring the security of data transmission. |Private network, dedicated network |


<span id="4a6cb955"></span>
# Project center


|Name |Term definition |Alias |
|---|---|---|
|Project |An independent business workspace within the system, divided based on business topics or departments, providing resource isolation and access control. Project members can collaborate within this space to complete operations such as data connection, visual modeling, and data preview. | |
|Project resources |All entity objects belonging to a specific project, including datasets, data connections, visualization tasks, dashboards, and many others, are governed by the project's permission system. | |
|User group |A collection of users with the same permission roles, used to manage project members' data access and operation permissions in batches. | |


<span id="43cbcccb"></span>
# Permissions


|Name |Term definition |Alias |
|---|---|---|
|System |System refers to the entire BytePlus system. |BytePlus |
|Product |Product refers to the DataAgent product. |DataAgent |
|Primary account |The primary account can be regarded as a special user (called the root user), who is the owner of cloud service resources and the entity for resource measurement and billing. The primary account has all permissions under the account by default. |Primary user, system administrator |
|Sub\-account |A sub\-account is created by a BytePlus account (primary account) or an IAM user with management permissions. |Sub\-user |
|Row\-level permission control |Restrict users' access to specific rows in a dataset through data filtering conditions (for example, only allowing access to data from their own department), achieving row\-level data security management. |RLS（Row\-Level Security） |
|Column\-level permission control |Restrict user access to specific columns in a dataset by using field allowlists and blocklists (such as masking sensitive fields) to achieve column\-level security control. |CLS（Column\-Level Security） |
