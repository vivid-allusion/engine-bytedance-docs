---
title: "Application scenarios"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/application_scenarios"
---

This topic describes the common application scenarios of Database Transmission Service (DTS).

<span id=".5pWw5o2u6L-B56e7"></span>
## Data migration

BytePlus Database Transmission Service (DTS) supports schema migration, full data migration, and incremental data migration, and facilitates seamless cloud migration with zero downtime.

Traditional migration methods can not process and supplement the incremental data generated during the migration of existing data. Therefore, it is necessary to stop the business of the source database, that is, stop migration to ensure data consistency. When dealing with large data volumes or low\-performance migration links, the process can be time\-consuming, resulting in business interruptions that last for hours or even days, which is often unacceptable in a production environment.

With BytePlus's Database Transmission Service (DTS), you can seamlessly migrate your data to the cloud with a single click and reduce downtime to the minute level. The advantages of smooth migration to the cloud through DTS are as follows:


* **Wide range of applications**

   * Applicable to multiple instance types: RDS for MySQL, Cache for Redis, Document Database for MongoDB, RDS for PostgreSQL, and RDS for SQL Server.

   * Applicable to multiple access methods: BytePlus instances, instances connected over public network, and virtual private clouds (VPCs).

   * Applicable to multiple network scenarios: public network or VPC, etc.

* **Migration stage**

   The entire cloud migration process includes the following stages:

   1. Schema migration

   2. Full data migration

   3. Incremental data catch\-up

   4. Incremental data migration

   5. Post\-schema migration

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">To ensure the performance of data migration and the stability of the migration task, some database migration objects will be created after the incremental migration is completed. The objects that need to undergo post\-schema migration include:      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">RDS for MySQL: trigger, event.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">PostgreSQL: ordinary trigger, event trigger, RULE, exclusive constraint, foreign key constraint, check constraint, Domain constraint, and Sequence value setting.      </div>
      

   When the "incremental data migration" stage is entered, the data between the source database and the target database can be kept in sync (there may be a delay depending on the service load of the source instance). You can perform business verification in the target database. After the business verification is successful and there is no delay, you can switch the business to the target database to achieve smooth migration.


<span id=".5pWw5o2u5ZCM5q2l"></span>
## Data synchronization

DTS provides the data synchronization feature. This function supports real\-time synchronization of incremental data between the production and disaster recovery centers, ensuring data consistency and security.

The database availability determines the continuity of upper\-layer services. In production scenarios, databases may experience service interruptions due to irresistible factors such as server hardware failures, network failures, and power system failures. Therefore, building a co\-city or remote disaster recovery environment for the database is a conventional and effective solution to improve database availability. The DTS data synchronization function can synchronize the primary database data to the disaster recovery database in real time, so as to build a stable and efficient disaster recovery environment at a lower cost.

<span id=".5pWw5o2u6K6i6ZiF"></span>
## Data subscription

DTS provides the data subscription feature. This feature allows you to obtain and consume incremental data from the source database in real time, which is suitable for scenarios including asynchronous business decoupling.

DTS utilizes a subscription\-based model to achieve a loosely coupled design between upstream and downstream services. This makes the entire business system simpler, more reliable, and adaptable to rapid business growth.

In some business scenarios, the backend may involve complex logic. Waiting for all of it to complete before returning a result could prevent users from finishing the process in a timely manner. Moreover, the execution of this complex backend logic often depends on numerous prerequisites. A failure in any single link can obstruct the entire business process, and as a result, users may frequently perceive system anomalies. A good experience can not be provided for users in such scenarios. By leveraging subscription tasks to decouple and defer complex business logic for asynchronous processing, DTS not only enhances user efficiency in completing workflows but also relaxes the strict latency requirements and improves fault tolerance for backend operations.
