---
title: "Resource-intensive activity statistics (pg_profile)"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/pg_profile"
---

pg_profile is a tool that can collect resource usage statistics in the database to help users analyze and optimize the database.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

pg_profile is based on PostgreSQL’s built\-in statistics views ([pg_stat_statements](https://www.postgresql.org/docs/14/pgstatstatements.html?spm=a2c4g.11186623.0.0.7722610dof14n3)) and community extension ([pg_stat_kcache](https://docs.byteplus.com/en/docs/RDS_for_PG/statistics_on_system_read_or_write_information-pg_stat_kcache)), fully written in PL/pgSQL, with no external libraries or software required. pg_profile depends on the dblink, pg_stat_statements, and pg_stat_kcache extensions. Among them, pg_stat_kcache is optional. Enabling pg_stat_kcache provides more information collection features.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Add pg_stat_statements to the shared_preload_libraries parameter.

* (Optional) Add pg_stat_kcache to the shared_preload_libraries parameter.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Storing sampling information will consume disk space. pg_profile has an automatic cleanup mechanism; pay attention to data preservation.

* Sampling is time\-consuming and does not require frequent execution; the recommended sampling frequency is 1 to 2 times per hour.


<span id=".5Yib5bu65LiO5Yig6Zmk5o-S5Lu2"></span>
## Create and delete extension


* Create extension

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">A super account is required to create the extension.   </div>
   

   ```sql
   CREATE EXTENSION pg_profile;
   ```
   

* Delete extension

   ```sql
   DROP EXTENSION pg_profile;
   ```
   


<span id=".5L2_55So5o-S5Lu2"></span>
## Extension usage

The pg_profile extension requires coordination between two databases during use: one database is sampled, and the other stores the collected statistical information. These two databases can be created in different PostgreSQL instances or within the same PostgreSQL instance. Below, the server database refers to the sampled database, and the profile database refers to the database storing statistical information, explaining the usage process of the pg_profile extension.

During sampling, the profile database sends a request to the server database, which samples its information upon receiving the request and returns the sampling results to profile. Profile stores the received results in tables within the profile database.

<span id=".MS4g5YeG5aSHIFNlcnZlciDmlbDmja7lupPjgII="></span>
### 1. Prepare the Server database.


1. Create a Server database.

   ```sql
   CREATE DATABASE server;
   ```
   

2. Connect to the Server database and create an extension.

   ```sql
   \c server
   CREATE EXTENSION pg_stat_statements;
   CREATE EXTENSION pg_stat_kcache;
   
   server=# \dx
                                               List of installed extensions
           Name        | Version |   Schema   |                              Description                               
   --------------------+---------+------------+------------------------------------------------------------------------
    pg_stat_kcache     | 2.2.3   | public     | Kernel statistics gathering
    pg_stat_statements | 1.9     | public     | track planning and execution statistics of all SQL statements executed
    plpgsql            | 1.0     | pg_catalog | PL/pgSQL procedural language
   ...
   ```
   


<span id=".Mi4g5YeG5aSHIHByb2ZpbGUg5pWw5o2u5bqT44CC"></span>
### 2. Prepare the profile database.


1. Create a profile database.

   ```sql
   CREATE DATABASE profile;
   ```
   

2. Connect to the profile database and create an extension.

   ```sql
   \c profile
   CREATE EXTENSION plpgsql;
   CREATE EXTENSION dblink;
   CREATE EXTENSION pg_profile;
   
   postgres=> \c profile
   You are now connected to database "profile" as user "test_account".
   profile=> \dx
                                      List of installed extensions
       Name    | Version |   Schema   |                         Description                          
   ------------+---------+------------+--------------------------------------------------------------
    dblink     | 1.2     | public     | connect to other PostgreSQL databases from within a database
    pg_profile | 4.4     | public     | PostgreSQL load profile repository and report builder
    plpgsql    | 1.0     | pg_catalog | PL/pgSQL procedural language
   ...
   ```
   


<span id=".My4g5Yib5bu6IFNlcnZlciDov57mjqXjgII="></span>
### 3. Create a Server connection.

```sql
profile=> SELECT create_server('server', 'host=$server数据库所在实例的连接地址 dbname=server port=$server数据库所在实例的端口号 user=$server数据库的高权限账号 password=$账号对应的密码');
 create_server 
---------------
             2
(1 row)
```



|**Parameter** |**Sample** |**Parameter description** |
|---|---|---|
|server |server |Connection name, custom. |
|host |127.0.0.1 |Connection address of the instance hosting the server database:<br><br>1) If the profile database and server database are on the same instance, configure this parameter as 127.0.0.1<br><br>2) If the profile database and server database are on different instances, configure this parameter as the Public network address of the instance hosting the server database |
|port |5432 |Port of the instance hosting the server database |
|dbname |server |Database name on the server side |
|user |test_account |Super account of the instance hosting the server database |
|password |xxxxxx |Password corresponding to the Account. |


Return result example:

```sql
profile=> select show_servers();
                                     show_servers
---------------------------------------------------------------------------------------
 (local,"dbname=profile port=5432",t,,)
 (server,"host=127.0.0.1 dbname=server port=5432 user=test_account password=xxxxxx",t,,)
(2 rows)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After creating the server connection, a profile database connection is automatically created, which is the connection named local in the above return result example.</div>


<span id=".NC4g5L-u5pS5IHByb2ZpbGUg5pWw5o2u5bqT6L-e5o6l55qE5L-h5oGv77yM6YWN572u5a-G56CB44CC"></span>
### 4. Modify the profile database connection information and configure the Password.

```sql
profile=> SELECT set_server_connstr('local','host=127.0.0.1 dbname=profile port=5432 user=test_account password=xxxxxx');
 set_server_connstr 
--------------------
                  1
(1 row)

profile=> select show_servers();
                                          show_servers                                          
------------------------------------------------------------------------------------------------
 (server,"host=127.0.0.1 dbname=server port=5432 user=test_account password=xxxxxx",t,,)
 (local,"host=127.0.0.1 dbname=profile port=5432 user=test_account password=xxxxxx",t,,)
(2 rows)
```


&nbsp;

<span id=".NS4g5Yid5qyh6L-b6KGM5pWw5o2u6YeH6ZuG44CC"></span>
### 5. Perform initial data collection.

```sql
profile=> SELECT take_sample();
       take_sample       -------------------------
 (local,OK,00:00:01.03)
 (server,OK,00:00:00.99)
(2 rows)
```


<span id=".Ni4g5a-5IHNlcnZlciDmlbDmja7lupPov5vooYzljovmtYvlkI7vvIzlho3mrKHov5vooYzph4fpm4bjgII="></span>
### 6. Collect data again after conducting stress testing on the server database.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The following commands must be executed in the client command line window. Ensure the client has PostgreSQL client installed.</div>


* <div data-tips="true" data-tips-type="tip">pgbench is a simple program for running benchmarks on PostgreSQL. For more command usages, refer to the <a href="https://www.postgresql.org/docs/14/pgbench.html">PostgreSQL official documentation</a>.</div>



```sql
pgbench -h postgresxxxxxx.rds-pg.ivolces.com -p 5432 -U test_account -c 100 -j 2 -T 300 -s 100 -i server   -- Stress testing 100 clients, each client with 2 threads, stress test for 300s, data amount with 100 scale factors
```



|Parameter |Sample |Parameter description |
|---|---|---|
|\-U |test_account |Super account of the instance where the server database is located. |
|\-h |postgresxxxxxx.rds\-pg.ivolces.com |Server database instance connection address. |
|\-p |5432 |Instance port. |
|\-s |100 |100 means creating 10,000,000 rows of data in the pgbench_accounts table. |
|\-i dbname |server |Database to be tested. |
|\-T |300 |Stress test 300s |
|\-c |100 |Client concurrent processes 100. |
|\-j |2 |Number of threads per client. |


Connect to the instance where the profile database is located and collect data again.

```sql
profile=> SELECT take_sample();
      take_sample       
------------------------
 (server,OK,00:00:00.5)
 (local,OK,00:00:00.39)
(2 rows)

profile=> SELECT * FROM show_samples('server');
 sample |      sample_time       | sizes_collected | dbstats_reset | bgwrstats_reset | archstats_reset
--------+------------------------+-----------------+---------------+-----------------+-----------------
      1 | 2024-11-17 22:14:45+08 | t               |               |                 | 
      2 | 2024-11-17 22:15:08+08 | t               |               |                 | 
      3 | 2024-11-18 19:27:40+08 | t               |               |                 | 
(3 rows)
```


<span id=".Ny4g5bCG6YeH6ZuG57uT5p6c55Sf5oiQ5oql5ZGK44CC"></span>
### 7. Generate a report from the collected results.

At two methods can be used to export the collected results to the local machine.


* Method 1: Execute the following command in the profile database using psql:

   ```sql
   \o report_1_2.html
   SELECT get_report('server',1,2);
   ```
   

* Method 2: Execute the following command in the local client command line:


```sql
$psql -Aqtc "SELECT get_report('server',1,2)" -o report_server_1_2.html -d profile -h xxxxxx -p 5432 -U test_account
Password for user test_account: 
$ ls -l
total 316
-rw-r--r-- 1 postgres postgres 322748 Nov 17 22:16 report_server_1_2.html
```


Report sample: [report_server_1_2.html](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_82ff581b41fcb2936255f31c7f412a23.zip).

<span id=".5YW25LuW"></span>
## Others

For more information, refer to [GitHub - zubkov-andrei/pg_profile at 4.4](https://github.com/zubkov-andrei/pg_profile/tree/4.4).
