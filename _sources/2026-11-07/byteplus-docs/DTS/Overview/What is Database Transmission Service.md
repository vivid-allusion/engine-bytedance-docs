---
title: "What is Database Transmission Service"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/about_database_transmission_service"
---

Database Transmission Service (DTS) is a data stream service that integrates data migration, data synchronization, and data subscription. It supports data interaction between data sources such as relational databases and non\-relational databases, reducing the complexity of data circulation between databases. It helps you seamlessly migrate databases to the cloud without interrupting business operations, easily build high\-availability database disaster recovery architectures through real\-time synchronization channels. At the same time, you can freely consume real\-time incremental data from cloud databases via data subscription based on your needs.

<span id=".5Lqn5ZOB5LyY5Yq_"></span>
## **Product features**


* **One\-stop data flow service:**  supports multi\-mode migration and synchronization, compatible with mainstream databases like MySQL, PostgreSQL, MongoDB and Redis.

* **Zero\-downtime data verification:**  Performs precise checks and comparisons of data differences between source and target databases without service interruption, accurately identifying structural discrepancies.

* **Pre\-migration assessment:**  Provides pre\-evaluation before migration to identify potential issues in advance, reduce migration risks, and improve success rates.

* **Real\-time uncremental data subscription:**  Supports multiple database types with on\-demand data consumption, well\-suited for asynchronous business decoupling scenarios.


<span id="I1biZ5O2"></span>
## Product advantages

DTS supports data transmission of relational and non\-relational databases. Compared with third\-party migration tools, DTS can more conveniently create and manage rich, high\-performance, high\-security and reliable transmission links.


* **Rich and diverse scenarios**

   * It supports the migration of multiple database engines, and the business interruption time window caused by the migration is shortened to the minute.

   * It supports data transmission through public and virtual private cloud networks.

   * It supports the migration task configuration only to incremental migration, realizing pure incremental synchronization from the source database to the target database.

* **Easy to operate and visualize**

   * It provides a visual management interface and a wizard\-based task configuration, allowing customers to easily complete data migration.

   * The migration progress is quantitatively displayed, and the console displays the full migration percentage and incremental migration data delay.

   * The migration rate of full and incremental migration is displayed graphically, and the link specifications can be adjusted in real time to maximize the utilization of link resources.

* **Secure and reliable data**

   * The instance is highly available, and the node has a high degree of recovery and healing capabilities, with recovery in seconds.

   * It supports breakpoint transmission. After the link exception is interrupted and returns to normal, it can automatically append the data of the interrupted time period.

* **Full and incremental integration:**  Supports deduplication and concurrent synchronization of both full and incremental data, improving transmission speed and minimizing data rollback risks.

* **AI data pipeline:**  Supports heterogeneous data synchronization between MySQL and Milvus and other sources, with built\-in automated vectorization capabilities that eliminate the need for additional service deployment, significantly reducing the cost of building and maintaining AI data pipelines.


<span id="1nDJ9P3W"></span>
## Architecture principles

DTS provides a non\-stop migration solution and supports multiple migration types, such as schema migration, full data migration, and incremental data migration.


* **Data migration**

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fa41843ddfb59f2d02d90b05b5a25c36.png) </span>

   * **Schema migration**: Reads the source database and table schema definition syntax and reassembles it into the syntax format of the target database.

   * **Full migration**: Fully read the content of the source table and write it to the corresponding target table.

   * **Incremental migration**: Parses and replays the target database incremental log to achieve online data migration.

   * **Post\-schema migration**: To ensure the performance of data migration and the stability of the migration task, some database migration object will be created after the incremental migration is complete. The objects that need to undergo post\-schema migration include:

      * RDS for MySQL: trigger, event.

      * RDS for PostgreSQL: ordinary trigger, event trigger, RULE, exclusive constraint, foreign key constraint, check constraint, Domain constraint, and Sequence value setting.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, the full\-incremental feature is only supported for RDS for MySQL migration tasks. The architecture of tasks with this feature enabled differs from that of tasks without it. For details, refer to <a href="https://docs.byteplus.com/en/docs/DTS/architecture_principles">What is full\-incremental feature?</a>.   </div>
   

* **Data synchronization**

&nbsp;

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_86f03b13bb735f42e544750234c3626d.png) </span>



&nbsp;

   * **Schema initialization**: Reads the source database and table schema definition syntax and reassembles it into the syntax format of the target database.

   * **Full initialization**: Fully read the content of the source table and write it to the corresponding target table.

   * **Incremental synchronization**: Parses and replays the target database incremental log to achieve online data synchronization.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, the full\-incremental feature is only supported for RDS for MySQL synchronization tasks. The architecture of tasks with this feature enabled differs from that of tasks without it. For details, refer to <a href="https://docs.byteplus.com/en/docs/DTS/architecture_principles">What is full\-incremental feature?</a>.   </div>
   

* **Data subscription**

&nbsp;

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a90e6f1a95a1364f6c7283ccf08306e3.png) </span>



&nbsp;

   * **Full subscription**: Fully reads the content of the source table and converts it into a ProtoBuf structure. Currently only supports BytePlus Proto, Canal Proto, Canal JSON, or Avro formats, and pushes it to the corresponding message queue.

   * **Incremental subscription**: Resolves the incremental logs of the source database and converts them into a ProtoBuf structure. Currently only supports BytePlus Proto, Canal Proto, Canal JSON, or Avro formats, and pushes them to the corresponding message queue.

   * **Database and table schema subscription**: Converts the source database and table schema into a ProtoBuf structure. Currently only supports BytePlus Proto, Canal Proto, Canal JSON, or Avro formats, and pushes it to the corresponding message queue.


<span id=".5bqU55So5Zy65pmv"></span>
## Application scenarios

DTS supports the application scenarios of smooth database migration. Its incremental migration feature ensures business continuity, synchronizes data changes in real time, and reduces downtime to the minute level. For details, refer to [Application scenarios](https://docs.byteplus.com/en/docs/DTS/application_scenarios).
