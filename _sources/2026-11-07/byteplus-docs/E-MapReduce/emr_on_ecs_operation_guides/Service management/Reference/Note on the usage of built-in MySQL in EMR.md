---
title: "Note on the usage of built-in MySQL in EMR"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Note_on_the_usage_of_built_in_MySQL_in_EMR"
---

<span id="fa94db7e"></span>
## prerequisites

Complete the creation of the EMR cluster.

<span id="772c2c0d"></span>
## Note on component usage


|Component |Service |Database name |Note on the reasons for built\-in RDS dependency |
|---|---|---|---|
|Hive |Hive Metastore |hive |Used only in non\-high\-availability clusters to store metadata\-related information |
|Ranger |Ranger Admin |ranger |Used only in non\-high\-availability clusters to store ranger metadata and permission policy information |
|Airflow |WebServer<br><br>Scheduler |airflow |Used only in non\-high\-availability clusters to store and coordinate scheduling workflows |
|DolphinScheduler |MasterServer<br><br>WorkerServer<br><br>ApiServer<br><br>AlertServer |dolphinscheduler |Used only in non\-high\-availability clusters to store and coordinate scheduling workflows |
|Ossa |Ossa Server<br><br>Ossa Gateway |Ossa |Used for interaction with DataLeap to store job submissions from DataLeap |


<span id="7c0f9896"></span>
## Accessing the built\-in MySQL

In the EMR cluster, the built\-in MySQL database is used to store metadata and configuration information for each component. You can access the built\-in MySQL database by following these steps:


1. Obtain the MySQL password:


You can obtain the MySQL user's password on the `master-1-1` machine in the cluster. The password is stored in a text file at the following location: `/root/.emr/secret`.


2. Connect to the MySQL database:


```SQL
/opt/emr/current/dbservice/bin/mysql -h {master-1-1 IP} -u root -p
--Enter {rootPassword}
```
