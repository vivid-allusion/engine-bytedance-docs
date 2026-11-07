---
title: "Basic Kudu operations"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Basic_Kudu_operations"
---

This article introduces common basic Kudu operation commands. You can directly execute Kudu commands in the Volcano Engine E\-MapReduce (EMR) cluster to perform operations.

<span id="_1-使用前提"></span>
## 1 Prerequisites


1. An EMR cluster containing the Kudu component service has been created. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. Currently, the Kudu component is open through an allowlist. You can apply for access using [Basic Kudu operations](https://docs.byteplus.com/docs/E-MapReduce/109318).


<span id="_2-确定-kudu-master-地址"></span>
## 2 Determine the Kudu Master address


1. Log in to the [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the left navigation bar, select and enter the **Cluster List \> Cluster Name \> Service List \> Kudu** page.

3. Click to expand Kudu Master to display the list of Kudu Master machines.


<span id="_3-基本操作"></span>
## 3 Basic operations

<span id="_3-1-登录-emr-集群节点"></span>
### 3.1 Log in to an EMR cluster node


* Option 1: Log in to one of the Kudu Master nodes using SSH. For details, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

* Option 2: You can use the ECS ID of the host named emr\-master\-1 in the EMR cluster **Kudu** component service deployment topology to jump to the cloud server instance page. Click the **Remote Connection** button in the upper right corner, enter the root password set during cluster creation, and access the remote terminal.


After logging in to the cluster, you can directly execute relevant Kudu commands in the Shell.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The domain naming conventions for nodes may differ between EMR versions. Therefore, the "emr\-master\-1 host name" above can be adjusted according to EMR's <a href="https://docs.byteplus.com/docs/E-MapReduce/104402">Domain name rules</a>.</div>


* <div data-tips="true" data-tips-type="tip">The following command examples are only for non\-HA cluster operations. For HA clusters, you need to add the remaining master and core addresses.</div>



<span id="_3-2-查看-master-列表"></span>
### 3.2 View the Master list

```shell
kudu master list <kudu master list>
```


For example:

```shell
kudu master list emr-3432jdr2za2uxxx-master-1,emr-3432jdr2za2uxxx-core-1,emr-3432jdr2za2uxxx-core-2
```


Output:

```shell
uuid               |             rpc-addresses              |   role
----------------------------------+----------------------------------------+----------
 50213849661a4075b82cecb8xxx | emr-3432jdr2za2uxxx-master-1:7051 | FOLLOWER
 f6bbd253a730485897870f73xxx | emr-3432jdr2za2uxxx-core-1:7051   | FOLLOWER
 9bf836ce63604edaa62f5b71xxx | emr-3432jdr2za2uxxx-core-2:7051   | LEADER
```


<span id="_3-3-查看-tablet-server-列表"></span>
### 3.3 View the Tablet Server list

```shell
kudu tserver list <kudu master list>
```


For example:

```shell
kudu tserver list emr-3432jdr2za2uxxx-master-1,emr-3432jdr2za2uxxx-core-1,emr-3432jdr2za2uxxx-core-2
```


Output:

```shell
uuid               |            rpc-addresses
----------------------------------+--------------------------------------
1fa382bfaa5445f095f2f9xxx | emr-3432jdr2za2uxxx-core-1:7050
da522576521b4fa6913416xxx | emr-3432jdr2za2uxxx-core-2:7050
```


<span id="_3-4-查看集群健康状态"></span>
### 3.4 View cluster health status

```shell
kudu cluster ksck <kudu master list>
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This command must be executed by first switching to the kudu user using the su kudu command.</div>


For example:

```shell
kudu cluster ksck emr-3432jdr2za2uxxx-master-1,emr-3432jdr2za2uxxx-core-1,emr-3432jdr2za2uxxx-core-2
```


Output:

```shell
Master Summary
               UUID               |              Address              | Status
----------------------------------+-----------------------------------+---------
 50213849661a4075b82cecxxx | emr-3432jdr2za2uxxx-master-1 | HEALTHY
 9bf836ce63604edaa62f5bxxx | emr-3432jdr2za2uxxx-core-2   | HEALTHY
 f6bbd253a730485897870fxxx | emr-3432jdr2za2uxxx-core-1   | HEALTHY

Flags of checked categories for Master:
        Flag         |                            Value                            |         Master
---------------------+-------------------------------------------------------------+-------------------------
 builtin_ntp_servers | 0.pool.ntp.org,1.pool.ntp.org,2.pool.ntp.org,3.pool.ntp.org | all 3 server(s) checked
 time_source         | system                                                      | all 3 server(s) checked

Tablet Server Summary
               UUID               |               Address                | Status  | Location | Tablet Leaders | Active Scanners
----------------------------------+--------------------------------------+---------+----------+----------------+-----------------
 1fa382bfaa5445f095f2f9xxx | emr-3432jdr2za2uxxx-core-1:7050 | HEALTHY | <none>   |       1        |       0
 da522576521b4fa6913416xxx | emr-3432jdr2za2uxxx-core-2:7050 | HEALTHY | <none>   |       1        |       0

Tablet Server Location Summary
 Location |  Count
----------+---------
 <none>   |       2

Flags of checked categories for Tablet Server:
        Flag         |                            Value                            |      Tablet Server
---------------------+-------------------------------------------------------------+-------------------------
 builtin_ntp_servers | 0.pool.ntp.org,1.pool.ntp.org,2.pool.ntp.org,3.pool.ntp.org | all 2 server(s) checked
 time_source         | system                                                      | all 2 server(s) checked

Version Summary
 Version |         Servers
---------+-------------------------
 1.14.0  | all 5 server(s) checked

Tablet Summary
Summary by table
 Name | RF | Status  | Total Tablets | Healthy | Recovering | Under-replicated | Unavailable
------+----+---------+---------------+---------+------------+------------------+-------------
 test | 1  | HEALTHY | 2             | 2       | 0          | 0                | 0

Tablet Replica Count Summary
   Statistic    | Replica Count
----------------+---------------
 Minimum        | 1
 First Quartile | 1
 Median         | 1
 Third Quartile | 1
 Maximum        | 1

Total Count Summary
                | Total Count
----------------+-------------
 Masters        | 3
 Tablet Servers | 2
 Tables         | 1
 Tablets        | 2
 Replicas       | 2

OK
```


<span id="_3-5-查看所有表"></span>
### 3.5 View all tables

```shell
kudu table list <kudu master list>
```


For example:

```shell
kudu table list emr-3432jdr2za2uxxx-master-1,emr-3432jdr2za2uxxx-core-1,emr-3432jdr2za2uxxx-core-2
```


<span id="_3-6-查看表定义"></span>
### 3.6 View table definitions

```shell
kudu table describe <kudu master list> <table name>
```


For example:

```shell
kudu table describe emr-3432jdr2za2uxxx-master-1,emr-3432jdr2za2uxxx-core-1,emr-3432jdr2za2uxxx-core-2 test
```


Output:

```shell
TABLE test (
    id INT32 NOT NULL,
    name STRING NOT NULL,
    PRIMARY KEY (id)
)
HASH (id) PARTITIONS 2 SEED 100
OWNER root
REPLICAS 1
```
