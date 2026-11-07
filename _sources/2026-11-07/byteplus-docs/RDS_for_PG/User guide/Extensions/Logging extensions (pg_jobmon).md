---
title: "Logging extensions (pg_jobmon)"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/pg_jobmon"
---

pg_jobmon extension provides PostgreSQL with a non\-transactional logging mechanism for transactions and functions to retain log information when transactions or functions fail. Even if your functions or transactions are Failed for any reason, the logged information will not be rolled back, thus ensuring the safety of critical log data.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

pg_jobmon extension is only supported on PostgreSQL instances version 14 and above. To use this extension, select the appropriate instance version when you create instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* pg_partman extension depends on the dblink extension. The dblink extension can be created using the following statement.

   ```sql
   CREATE EXTENSION dblink;
   -- configure dblink related parameters
   INSERT INTO test_schema.dblink_mapping_jobmon (host, username, pwd) VALUES ('127.***.***.1', 'test_user', 'test@123');
   ```
   


<span id=".5Yib5bu65LiO5Yig6Zmk5o-S5Lu2"></span>
## Create and delete extension


* Create extension

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">A super account is required to create the extension.   </div>
   

```sql
CREATE EXTENSION pg_jobmon;
```



* Delete extension


```sql
DROP EXTENSION pg_jobmon;
```


<span id=".5L2_55So5o-S5Lu2"></span>
## Extension usage

<span id=".5Yib5bu65L2c5Lia"></span>
### Create a task

Functions below allow you to create job, add steps to a job, and update step state.

```sql
-- create job and several steps
select test_schema.add_job('job1');
select test_schema.add_step(1, 'job1_step1');
select  test_schema.sql_step(1,  'job1_step2',  'select pg_sleep(3)');
```


<span id=".5p-l55yL5L2c5Lia"></span>
### View task

Functions below allow you to view job detail:


* *show_job*

* *show_job_like*

* *show_job_status*

* *show_detail*


```sql
test_db=> -- view job
test_db=> select test_schema.show_job('job1');
                                           show_job
----------------------------------------------------------------------------------------------
 (1,test_user,JOB1,"2025-04-17 21:25:09.684233+08","2025-04-17 21:25:13.427808+08",OK,579004)
(1 row)

test_db=> select test_schema.show_job_like('job');
                                        show_job_like
----------------------------------------------------------------------------------------------
 (1,test_user,JOB1,"2025-04-17 21:25:09.684233+08","2025-04-17 21:25:13.427808+08",OK,579004)
(1 row)

test_db=> select test_schema.show_job_status('job1', 'OK');
                                       show_job_status
----------------------------------------------------------------------------------------------
 (1,test_user,JOB1,"2025-04-17 21:25:09.684233+08","2025-04-17 21:25:13.427808+08",OK,579004)
(1 row)

test_db=> select test_schema.show_detail(1);
                                                  show_detail
----------------------------------------------------------------------------------------------------------------
 (1,1,job1_step1,"2025-04-17 21:25:09.696224+08",,,,)
 (1,2,job1_step2,"2025-04-17 21:25:10.38315+08","2025-04-17 21:25:13.416171+08",3.033021,OK,"Rows affected: 1")
(2 rows)
```


<span id=".57uT5p2f5L2c5Lia"></span>
### End task

```sql
-- end job
select  test_schema.close_job(1);
select test_schema.check_job_status();
```
