---
title: "Access Kudu using Impala"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Access_Kudu_using_Impala"
---

<span id="_1-使用前提"></span>
## **1 Prerequisites for use**


1. An EMR cluster with Kudu and Impala component services has been created. For details, see: [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. Currently, the Kudu and Impala components are only available to users on the allowlist. You can apply for access via [Access Kudu using Impala](https://docs.byteplus.com/docs/E-MapReduce/109295).


<span id="_2-impala-集成-kudu"></span>
## 2 Impala integration with Kudu

After installing Impala and Kudu in Volcano Engine E\-MapReduce (EMR), you need to configure the address of the Kudu Master in Impala.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If Impala and Kudu are installed together, kudu_master_hosts will be set automatically and manual configuration is not required.</div>



1. Log in to the [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the left navigation bar, select and enter the **Cluster List \> Cluster Name \> Service List \> Impala** page.

3. Click the **Service Parameters** tab, and search for the parameter: **kudu_master_hosts.** 

4. Set the parameter value to the address of **Kudu Master**, as shown below:

   For details on obtaining the **Kudu Master** address, see: [Basic Kudu operations](https://docs.byteplus.com/docs/undefined/69a9680572f3410570217c40) **.** 

5. After completing the parameter configuration, click the **Save** button in the upper right corner, then **Restart** the Impalad service in Service Operations.


<span id="_3-使用-impala-访问-kudu"></span>
## 3 Access Kudu using Impala

<span id="_3-1-impala-shell"></span>
### 3.1 impala\-shell

Impala\-shell is a command\-line tool that can directly connect to Impala. When Impala is installed in Volcano Engine EMR, impala\-shell is automatically added to the system environment variables. You can SSH to the master\-1 node and use impala\-shell. For login methods, see: [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

If the cluster has enabled LDAP authentication, refer to the documentation: [Impala-shell tool](https://docs.byteplus.com/docs/E-MapReduce/109294) to use impala\-shell.

For example:

```shell
root@emr-4nw5w1f78f3l0xxx-master-1:~# impala-shell
/opt/emr/2.0.0/impala-3.4.1/shell/impala-shell-3.4.1-RELEASE/ext-py2/bitarray-0.9.0-py2.7-linux-x86_64.egg/bitarray/_bitarray.py:3: UserWarning: Module backports was already imported from None, but /usr/lib/python2.7/dist-packages is being added to sys.path
Starting Impala Shell without Kerberos authentication
Opened TCP connection to emr-4nw5w1f78f3l0xxx-master-1:21000
Connected to emr-4nw5w1f78f3l0xxx-master-1:21000
Server version: impalad version 3.4.1-RELEASE RELEASE (build eb1ed66fa435a722fa8c6a7c58ff53edc10c572e)
***********************************************************************************
Welcome to the Impala shell.
(Impala Shell v3.4.1-RELEASE (eb1ed66) built on Fri Sep 16 15:03:38 CST 2022)
 
Want to know what version of Impala you're connected to? Run the VERSION command to
find out!
***********************************************************************************
[emr-4nw5w1f78f3l0xxx-master-1:21000] default>
```


<span id="_3-2-创建-kudu-表"></span>
### 3.2 Create a Kudu table

```shell
CREATE TABLE my_first_table
(
  id BIGINT,
  name STRING,
  PRIMARY KEY(id)
)
PARTITION BY HASH PARTITIONS 16
STORED AS KUDU
TBLPROPERTIES ('kudu.num_tablet_replicas' = '1');
```


For example:

```shell
[emr-4nw5w1f78f3l0xxx-master-1:21000] default> CREATE TABLE my_first_table
                                                 > (
                                                 >   id BIGINT,
                                                 >   name STRING,
                                                 >   PRIMARY KEY(id)
                                                 > )
                                                 > PARTITION BY HASH PARTITIONS 16
                                                 > STORED AS KUDU
                                                 > TBLPROPERTIES ('kudu.num_tablet_replicas' = '1');


Query: CREATE TABLE my_first_table
(
  id BIGINT,
  name STRING,
  PRIMARY KEY(id)
)
PARTITION BY HASH PARTITIONS 16
STORED AS KUDU
TBLPROPERTIES ('kudu.num_tablet_replicas' = '1')
+-------------------------+
| summary                 |
+-------------------------+
| Table has been created. |
+-------------------------+
Fetched 1 row(s) in 7.00s
```


<span id="_3-3-写入数据"></span>
### 3.3 Write data

```shell
[emr-4nw5w1f78f3l0xxx-core-1:21000] default> insert into my_first_table values(1, 'Tom');
Query: insert into my_first_table values(1, 'Tom')
Query submitted at: 2022-09-28 11:48:46 (Coordinator: http://emr-4nw5w1f78f3l0xxx-core-1:25000)
Query progress can be monitored at: http://emr-4nw5w1f78f3l0xxx-core-1:25000/query_plan?query_id=f74dc7a765df77a3:15c929b200000000
Modified 1 row(s), 0 row error(s) in 5.76s
```


<span id="_3-4-查询数据"></span>
### 3.4 Query data

```shell
[emr-4nw5w1f78f3l0xxx-master-1:21000] default> select * from my_first_table;
Query: select * from my_first_table
Query submitted at: 2022-10-17 18:49:49 (Coordinator: http://emr-4nw5w1f78f3l0xxx-core-1:25000)
Query progress can be monitored at: http://emr-4nw5w1f78f3l0xxx-core-1:25000/query_plan?query_id=7b44cc81e2374b76:0066f4bf00000000
+----+------+
| id | name |
+----+------+
| 1  | Tom  |
+----+------+
Fetched 1 row(s) in 1.28s
```
