---
title: "Run the TPC-DS Benchmark on an EMR on ECS cluster"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Run_the_TPC-DS_Benchmark_on_an_EMR_on_ECS_cluster"
---

<span id="背景信息"></span>
## Context

The TPC\-DS testing mechanism is the next\-generation decision support system benchmark introduced by the TPC organization to replace TPC\-H. This document describes how to run all 99 SQL queries of TPC\-DS on an EMR cluster.

<span id="操作流程"></span>
## Procedure


* [步骤一：创建EMR集群](https://docs.byteplus.com/docs/E-MapReduce/109260#%E6%AD%A5%E9%AA%A4%E4%B8%80%EF%BC%9A%E5%88%9B%E5%BB%BAemr%E9%9B%86%E7%BE%A4)

* [步骤二：创建TPC-DS Benchmark 工具并编译打包数据生成器](https://docs.byteplus.com/docs/E-MapReduce/109260#%E6%AD%A5%E9%AA%A4%E4%BA%8C%EF%BC%9A%E5%88%9B%E5%BB%BAtpc-ds-benchmark-%E5%B7%A5%E5%85%B7%E5%B9%B6%E7%BC%96%E8%AF%91%E6%89%93%E5%8C%85%E6%95%B0%E6%8D%AE%E7%94%9F%E6%88%90%E5%99%A8)

* [步骤三：生成并加载数据](https://docs.byteplus.com/docs/E-MapReduce/109260#%E6%AD%A5%E9%AA%A4%E4%B8%89%EF%BC%9A%E7%94%9F%E6%88%90%E5%B9%B6%E5%8A%A0%E8%BD%BD%E6%95%B0%E6%8D%AE)

* [步骤四：运行TPC-DS SQL](https://docs.byteplus.com/docs/E-MapReduce/109260#%E6%AD%A5%E9%AA%A4%E5%9B%9B%EF%BC%9A%E8%BF%90%E8%A1%8Ctpc-ds-sql)


<span id="步骤一：创建emr集群"></span>
### Step 1: Create an EMR cluster


1. Create an EMR cluster. For detailed procedure, see: [集群创建](https://docs.byteplus.com/docs/undefined/68da347342e561058e056b92)

   1. Cluster type: Hadoop

   2. Instance specifications: To achieve better performance, for integrated storage and compute scenarios, core instances are recommended to be big data type; for storage\-compute separation scenarios, core instances are recommended to be local SSD type. To quickly complete all procedures with a small\-scale cluster, core instances can also be selected as general\-purpose instances with 8 vCPU and 32 GiB.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Caution: Pay attention to the HDFS replication factor. Always ensure that the total capacity of the cluster's data disks is more than three times the size of the dataset.   </div>
   

2. Log in to the ECS instance via SSH. For details, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).


<span id="步骤二：创建tpc-ds-benchmark-工具并编译打包数据生成器"></span>
### Step 2: Create the TPC\-DS Benchmark tool and compile and package the data generator


1. Download the TPC\-DS Benchmark tool: Download it via the link to our pre\-compiled and packaged testing tool.

   
   |hadoop2x version |hadoop3x version |
   |---|---|
   |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a593a1a2a8847a26ff8012193b507e41.zip" name="hive-testbench-hdp2.zip">hive-testbench-hdp2.zip</Attachment><br> |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_19b2ff7136d7ab35151b92aff0f9ebb3.zip" name="hive-testbench-hdp3.zip">hive-testbench-hdp3.zip</Attachment><br> |
   

2. Download the file.

3. Upload the zip file to the EMR cluster. This step takes Linux as the local operating system as an example. The command is as follows:

   ```bash
   #Password method
   scp hive-testbench-{hdpx}.zip root@*.*.*.*:/opt
   #Key pair method:
   scp -i  **.pem  hive-testbench-{hdpx}.zip root@*.*.*.*:/opt
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For the key pair method, you must first restrict permissions by running chmod 600 \*\*.pem. The key pair can only be downloaded when it is created!   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For clusters with storage\-compute separation, you can also upload files to TOS for downloading! For detailed usage, refer to: <a href="https://docs.byteplus.com/docs/undefined/69a968353f58f805314f0f02">Proton overview</a>   </div>
   

4. Extract the uploaded zip file on the EMR cluster

   ```bash
   unzip hive-testbench-{hdpx}.zip
   ```
   

5. Grant permissions to the uploaded benchmark test suite:

   ```bash
   cd /opt
   chmod 777 -R hive-testbench-{hdpx}
   ```
   

6. Compile and package the data generator

   1. For git\-based download, data generation is required. The detailed steps are as follows:

      1. Enter the directory:

      ```bash
      cd /opt/hive-testbench-{hdpx}
      ```
      

      2. Use the TPC\-DS toolkit to compile and package the data generator:

      ```bash
      ./tpcds-build.sh
      ```
      

   2. If downloaded locally, the Volcano Engine EMR installation package is already compiled. The jar package is located at: /opt/hive\-testbench\-{hdpx}/tpcds\-gen/target/tpcds\-gen\-1.0\-SNAPSHOT.jar, and the Maven tool is also compiled and located in /opt/hive\-testbench\-{hdpx}.


<span id="步骤三：生成并加载数据"></span>
### Step 3: Generate and load data

<span id="注意事项"></span>
#### Important notes

<span id="_1-使用说明"></span>
##### 1. Usage instructions


1. To use the git download address, modify the hive command to the Volcano Engine EMR command. For details, refer to [Overview](https://docs.byteplus.com/docs/E-MapReduce/109251).

2. To use other formats, change the default format of the tool package provided by Volcano, which is **FORMAT**=parquet.

3. To ensure data accuracy, use the 3x version to query data imported by Spark, as the tool package provided by Volcano includes scripts for importing data with Spark due to partial incompatibility of Hive write formats in the open\-source Spark 3.2.1 version.


<span id="_2-如何从指定位置开始运行脚本"></span>
##### 2. How to run the script from a specified position

Since TPCDS contains multiple SQL files, the script runs from the first SQL by default. In some scenarios, it may be necessary to skip certain SQL files and start from a specific one. For such cases, you can modify the script. Taking hive_perftest.py as an example, at line 41 of the script, that is:

```bash
for s in res.split('\n'):
```


Add the following code before and after this for loop:

```bash
continue_flag = True
start_sql =  "query64.sql"
for s in res.split('\n'):
    if  s == start_sql:
                continue_flag = False
    if  continue_flag:
        continue
    log_name = "/opt/hive-testbench-{hdpx}/log/hiveon{engine}/{dir}/{sql}.log".format(engine=engine, sql=s, dir=start_time)
    cmd = "-f /opt/hive-testbench-{hdpx}/sample-queries-tpcds/{sql} > {dir} 2>&1".format(sql=s, dir=log_name)
    cmd = base + cmd
    res = subprocess.run(cmd, shell=True)
    with open(log_name, 'r') as f:
        with open(res_log, 'a') as log:
```


Here, `query64.sql` is the starting SQL. Replace it with your desired starting SQL as needed.

<span id="前置步骤"></span>
#### Prerequisite steps


1. Import the user "tpcdstest" in the console. For detailed instructions, see: [User management](https://docs.byteplus.com/docs/E-MapReduce/105426).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>The script provided by Volcano Engine uses the tpcdstest user by default. Importing with other users may result in failure.</strong>   </div>
   

2. [Optional] If Ranger permissions are enabled, you need to grant permissions to the user tpcdstest in Ranger. For details on granting permissions, refer to the official documentation [Overview](https://docs.byteplus.com/docs/undefined/69aa39aa3002e40527bca427)for granting HDFS, Hive, and Yarn permissions to imported users.


```bash
su tpcdstest
bash
```


<span id="脚本执行"></span>
#### Script execution

<span id="存算一体场景"></span>
##### Integrated storage and compute scenario


1. Run the setup script


```bash
#The DATABASE in the tpcds-setup.sh script is the actual database being written to.
#Parameter 1: FORMAT is the table format generated by running the script. The default value is parquet. Supported formats are orc, parquet, and textfile. You can also set the global variable by using export FORMAT=parquet.

#Parameter 2: $SCALE - data scale, needs to be replaced.
#Parameter 3: Data storage path. passwd: the password of the import user, which is configured by the user during import.

#Run in the background, hivesql command for importing into internal tables
FORMAT=parquet nohup ./tpcds-setup.sh {SCALE} /hivedata {passwd} &
#Run in the background, sparksql command for importing into internal tables
FORMAT=parquet nohup ./tpcds-setup-sparksql.sh {SCALE} /hivedata {passwd} &
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6207ee15779e6b9f0f4f2fccf043cb3d.png) </span>

<span id="存算分离场景"></span>
##### Disaggregated storage and compute scenario

<span id="使用tos"></span>
###### Use tos


1. Create a tos bucket or file system for storage.

   1. For instructions on creating the TOS bucket, see: [TOS Quick Start](https://www.volcengine.com/docs/6349/74830)

2. Run the setup script

   ```bash
   #Parameter 1: FORMAT is the table format generated by running the script. The default value is parquet. Supported formats are orc, parquet, and textfile.
   #Parameter 2: $SCALE - data scale, needs to be replaced.
   #Parameter 3: Data storage path. passwd: the password of the import user, which is configured by the user during import.
   
   #hivesql import command
   nohup FORMAT=parquet ./tpcds-setup.sh {SCALE} 'tos://您的bucket name/hivedata' {passwd} &
   #sparksql import command can also be used
   nohup FORMAT=parquet ./tpcds-setup-sparksql.sh {SCALE} 'tos://您的bucket name/hivedata' {passwd} &
   ```
   


<span id="步骤四：运行tpc-ds-sql"></span>
### Step 4: Run TPC\-DS SQL

This step describes how to run TPC\-DS using Hive and Spark, mainly using the scripts provided in the toolkit as examples. You can also run your commonly used query scripts, which will not be discussed further here.

<span id="hive"></span>
#### Hive


1. Start the Python script:


```bash
nohup python3 /opt/hive-testbench-{hdpx}/hive_perftest.py --db_name={DB} --hive_pwd={pwd} --test_engine={engine} --cluster_type={is_ha} --resultPwd={logdir} --cluster_version={version} &
```


**Parameter description:** 


|Parameter name |Required |Note |
|---|---|---|
| |Yes |Name of the DB to query. Example: tpcds_bin_partitioned_parquet_2 |
| |Yes |Password of the import user, which is configured by the user during import. |
| |Yes |Query engine. Options: tez, mr, spark |
| |No |Whether it is an HA cluster. Options: HA, NHA. If not specified, the default is HA. |
| |No |Log generation path. You can customize it. If not specified, the default is /opt/hive\-testbench\-{hdpx}/log/hivesql/1 |
| |No |Cluster version number. The default is 3.5.0/2.4.0. For versions higher than 3.5.0/2.4.0, this can be omitted. For versions lower than this, you need to specify the version number. |



2. Query result description: The query results are located in the log path specified above. Select the corresponding date to enter the folder and view the results. Among them:

   1. a_finish.log indicates the execution time and result of each SQL.

   2. b_finish.csv contains the execution time of each SQL. When opened locally, it is in Excel format.

   3. The remaining \*.sql.log files contain the execution logs of each SQL.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7cc4f3ba1dbf40c689ff789cc3801f27.png) </span>


3. If a particular SQL fails and needs to be debugged individually, you can log in to emr\-master\-1 and run the following command:


```bash
#Replace parameters as needed: pwd: hive password, i: the number of the query to execute, DB: the database to query
beeline -n tpcdstest -p {pwd} -u 'jdbc:hive2://localhost:2181/{DB};serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=hiveserver2?tez.queue.name=default' --hiveconf hive.tez.container.size=6144  -i /opt/hive-testbench-{hdpx}/settings/hivetest.sql -f /opt/hive-testbench-{hdpx}/sample-queries-tpcds/query{i}.sql
```


<span id="spark"></span>
#### Spark


1. Start the Spark query script


```bash
nohup python3 /opt/hive-testbench-{hdpx}/sparksql_perftest.py --db_name={DB} --resultPwd={logdir} &
```



|Parameter name |Required |Note |
|---|---|---|
| |Yes |Name of the DB to query. Example: tpcds_bin_partitioned_parquet_2 |
| |No |Generate the log path. You can customize it; if not specified, the default location is: /opt/hive\-testbench\-{hdpx}/log/sparksql/1 |



2. Query result description: The query results are located in the log path specified above. Select the corresponding date to enter the folder and view the results. Among them:

   1. a_finish.log indicates the execution time and result of each SQL.

   2. b_finish.csv contains the execution time of each SQL. When opened locally, it is in Excel format.

   3. The remaining \*.sql.log files contain the execution logs of each SQL.

3. To debug a specific SQL statement that did not pass, execute the following command:


```bash
#Replace parameters as needed: DB: the database to query; i: the index of the query being executed
spark-sql --master yarn --driver-memory 10g --executor-memory 5g  --num-executors 60  --database {DB} -v -f /opt/hive-testbench-{hdpx}/spark-queries-tpcds/q$i.sql
```
