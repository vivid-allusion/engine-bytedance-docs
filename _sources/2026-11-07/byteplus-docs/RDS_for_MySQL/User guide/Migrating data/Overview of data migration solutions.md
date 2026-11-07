---
title: "Overview of data migration solutions"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/overview_of_data_migration_solutions"
---

This article mainly introduces the data sources supported by RDS for MySQL, as well as an overview of migration solutions via database transmission service (DTS).

<span id="06pZ1niQ"></span>
## Supported data sources


|**Source database Version** |**Target database** |**Configuration Guide** |
|---|---|---|
|* MySQL 5.7<br><br>* MySQL 8.0<br><br><br> |MySQL |* [Synchronizing to BytePlus RDS for MySQL](https://docs.byteplus.com/en/docs/DTS/synchronizing_to_byteplus_rds_for_mysql_rdsmysql?lang=en)<br><br>* [Synchronizing to BytePlus veDB for MySQL](https://docs.byteplus.com/en/docs/DTS/Synchronizing_to_Volcano_Engine_veDB_for_MySQL?lang=en)<br><br>* [Synchronizing to MySQL connected over public network](https://docs.byteplus.com/en/docs/DTS/synchronizing_to_public_network_rdsmysql?lang=en)<br><br>* [Synchronizing to MySQL connected over express network](https://docs.byteplus.com/en/docs/DTS/synchronizing_to_express_network_rdsmysql?lang=en) |
||Elasticsearch |* [Synchronizing to BytePlus Cloud Search](https://docs.byteplus.com/en/docs/DTS/Synchronizing_to_Volcengine_Cloud_Search_Service?lang=en)<br><br>* [Synchronizing to Elasticsearch connected over express network](https://docs.byteplus.com/en/docs/DTS/Synchronizing_to_ElasticSearch_connected_over_express_network?lang=en)<br><br>* [Synchronizing to Elasticsearch connected over public network](https://docs.byteplus.com/en/docs/DTS/Synchronizing_to_Cloud_Search_connected_over_public_network?lang=en) |


<span id="8jtjsBrb"></span>
## Overview of data migration solutions

<span id=".5L2_55So5LyY5Yq_"></span>
## Use advantages

**Wide range of applications**


* Applicable to a diverse range of instance types: Data center, third\-party cloud, self\-managed ECS instances;

* Applicable to multiple network scenarios: Internet, VPC, and other network types.


**No\-downtime migration**

No\-downtime migration Incremental migration will not interrupt the services while data updates are synced in real time, with the shutdown time reduced to only several minutes.

<span id=".5pWw5o2u6L-B56e75rWB56iL"></span>
## Data migration process

Data Migration Process For data migration by DTS, follow the steps below


1. Preparation: Before using DTS for data migration, you must make some preparations for the source or destination database to meet the environment requirements of DTS. For more information, refer to [Preparations](https://docs.byteplus.com/en/docs/RDS_for_MySQL/preparations).

2. With several simple operations in the console, you can easily create a migration task. For more information, refer to [Creating and initiating a migration task](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_and_initiating_a_migration_task).

3. Migration task management: You can view metrics such as Full migration, RPS for incremental migration, and Incremental migration of BPS of the current task. For more information, refer to [Viewing Progress of a Migration Task](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_migration_progress).

4. Ending a data migration task: If you do not need a migration task after data migration and service switch, you can end the data migration task. For more information, refer to [Ending a migration task](https://docs.byteplus.com/en/docs/RDS_for_MySQL/ending_a_migration_task).
