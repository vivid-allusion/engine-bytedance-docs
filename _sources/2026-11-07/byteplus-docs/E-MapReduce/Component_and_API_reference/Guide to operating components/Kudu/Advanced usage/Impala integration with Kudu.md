---
title: "Impala integration with Kudu"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Impala_integration_with_Kudu"
---

<span id="_1-impala-简介"></span>
## 1 Introduction to Impala

Impala is a distributed massively parallel processing (MPP) compute engine. With Impala, you can quickly query and analyze Kudu data. For more information, see: [Impala overview](https://docs.byteplus.com/docs/E-MapReduce/109292).

<span id="_2-使用前提"></span>
## 2 Prerequisites


1. An EMR cluster containing the Kudu and Impala component services has been created. For details, see: [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. Currently, the Kudu and Impala components are available through an allowlist. You can apply for access via [Impala integration with Kudu](https://docs.byteplus.com/docs/E-MapReduce/109317).


<span id="_3-impala-集成-kudu"></span>
## 3 Impala integration with Kudu

After installing Impala and Kudu in Volcano Engine E\-MapReduce (EMR), you need to configure the address of the Kudu Master in Impala.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If Impala and Kudu are installed together, kudu_master_hosts will be set automatically and manual configuration is not required.</div>



1. Log in to the [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the left navigation pane, select and enter the **Cluster List \> Cluster Name \> Service List \> Impala** page.

3. Click the **Service Parameters** tab, and search for the parameter: **kudu_master_hosts.** 

4. Set the value of the parameter to the address of the **Kudu Master**, as shown below:

   For information on obtaining the **Kudu Master** address, see: [Basic Kudu operations](https://docs.byteplus.com/docs/E-MapReduce/109318).

5. After configuring the parameters, click the **Save** button in the upper right corner, then in Service Operations, **restart** the Impalad service.


<span id="_4-使用-impala-访问-kudu"></span>
## 4 Accessing Kudu with Impala

The following section describes how to access Kudu using Impala, including creating tables, writing data, and querying data. This guide primarily uses the impala\-shell tool.

<span id="_4-1-impala-shell"></span>
### 4.1 impala\-shell

impala\-shell is a command\-line tool that can connect directly to Impala. When Impala is installed in Volcano Engine EMR, impala\-shell is included in the system environment variables by default. You can SSH to any impalad machine and use impala\-shell.

For login methods, see: [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

For example:

```shell
root@emr-3432jdr2za2uxxx-core-1:~# impala-shell
***********************************************************************************
Welcome to the Impala shell.
(Impala Shell v3.4.1-RELEASE (eb1ed66) built on Fri Sep 16 15:03:38 CST 2022)

The SET command shows the current value of all shell and query options.
***********************************************************************************
[emr-3432jdr2za2uxxx-core-1:21000] default>
```


<span id="_4-2-创建-kudu-表"></span>
### 4.2 Create a Kudu table

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
[emr-3432jdr2za2uxx-core-1:21000] default> CREATE TABLE my_first_table
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
Fetched 1 row(s) in 2.36s
```


<span id="_4-3-写入数据"></span>
### 4.3 Write data

```shell
[emr-3432jdr2za2uxx-core-1:21000] default> insert into my_first_table values(1, 'Tom');
Query: insert into my_first_table values(1, 'Tom')
Query submitted at: 2022-09-28 11:48:46 (Coordinator: http://emr-3432jdr2za2uxx-core-1:25000)
Query progress can be monitored at: http://emr-3432jdr2za2uxx-core-1:25000/query_plan?query_id=f74dc7a765xxx:15c929b200000000
Modified 1 row(s), 0 row error(s) in 5.76s
```


<span id="_4-4-查询数据"></span>
### 4.4 Query data

```shell
[emr-3432jdr2za2uxx-core-1:21000] default> select * from my_first_table;
Query: select * from my_first_table
Query submitted at: 2022-09-28 11:49:22 (Coordinator: http://emr-3432jdr2za2uxx-core-1:25000)
Query progress can be monitored at: http://emr-3432jdr2za2uxx-core-1:25000/query_plan?query_id=87477e01xxx:8a3f74d300000000
+----+------+
| id | name |
+----+------+
| 1  | Tom  |
+----+------+
Fetched 1 row(s) in 0.33s
```
