---
title: "quickstart"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/doris_quickstart"
---

This article introduces the detailed procedure and related configurations for creating a Doris cluster.

<span id="_1-创建集群"></span>
## 1. Create a cluster

Cluster creation consists of four steps: software settings \-\-\> hardware settings \-\-\> other settings \-\-\> preview and confirmation.

<span id="_1-1-软件设置"></span>
### 1.1 Software settings

You can create a cluster from the cluster list interface. When creating a cluster, select the **Interactive Query \> Doris** cluster type. Select the appropriate product version as needed.

To learn about the differences between product versions, click Version Description to view the release records

<span id="_1-2-硬件设置"></span>
### 1.2 Hardware settings

In the hardware settings step, select the network and instance resources for the cluster.


* VPC/subnet cannot be changed after the cluster is created. Please plan the network appropriately. Downstream applications such as BI tools need to access the Doris FE service. Ensure that BI tools and the Doris cluster are in the same VPC or use a public IP.

* Instance node types are divided into Master and Core. Master nodes deploy FE, Core nodes deploy BE. Plan computing resources and disk space appropriately based on business requirements and data growth. It is recommended to use ultra\-fast SSD or higher disks for BE nodes.


<span id="_1-3-其他设置"></span>
### 1.3 Other settings

In the other settings step, enter and set the cluster name and machine key or password.

<span id="_1-4-预览确认"></span>
### 1.4 Preview and confirmation

Finally, preview the relevant parameters set in the previous steps. After confirming they are correct, review and check the box to agree to the service terms, then immediately create the cluster.

<span id="_2-配置修改"></span>
## 2. Configuration modification

After the cluster is successfully created, you can directly use the Doris service. To modify the relevant Doris configurations, select the Doris cluster to manage in the cluster management interface, and go to **Cluster Management \-\-\> Service List \-\-\> Doris Service \-\-\> Service Parameters** to view or modify the corresponding parameters.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Save and restart the relevant components after modifying parameters.</div>


<span id="_3-查询数据"></span>
## 3. Query data

After the Doris service is started, use the MySQL client or other MySQL tools to connect to the Doris service to create databases, tables, and so on, and perform data insertion and queries in the table. The following uses the MySQL client as an example to demonstrate how to connect to the Doris cluster and execute related SQL operations.


1. Use the MySQL client to connect to Doris FE.


{FE ip} is the IP address of any node where the Doris cluster FE is located.

```plain
mysql -h{FE ip} -P9030 -uroot
```



2. Create a database after logging in


```plain
mysql> create database db_demo;
```



3. Create a table under the database


```plain
mysql> use db_demo;
mysql> CREATE TABLE table_hash
(
    k1 DATE,
    k2 DECIMAL(10, 2) DEFAULT "10.5",
    k3 CHAR(10) COMMENT "string column",
    k4 INT NOT NULL DEFAULT "1" COMMENT "int column"
)
DUPLICATE KEY(k1, k2)
COMMENT "my first table"
PARTITION BY RANGE(k1)
(
    PARTITION p1 VALUES LESS THAN ("2020-02-01"),
    PARTITION p2 VALUES LESS THAN ("2020-03-01"),
    PARTITION p3 VALUES LESS THAN ("2020-04-01")
)
DISTRIBUTED BY HASH(k1) BUCKETS 32
PROPERTIES (
    "replication_num" = "1"
);
```



4. Insert data


```plain
INSERT INTO table_hash select '2017-02-01', 1, 'value1', 1;
INSERT INTO table_hash select '2020-03-03', 5.7, 'value2', 2;
INSERT INTO table_hash select '2020-03-15', 8, 'value3', 3;
```



5. Query data


```plain
mysql> select * from table_hash;
+------------+------+--------+------+
| k1         | k2   | k3     | k4   |
+------------+------+--------+------+
| 2017-02-01 |    1 | value1 |    1 |
| 2020-03-15 |    8 | value3 |    3 |
| 2020-03-03 |  5.7 | value2 |    2 |
+------------+------+--------+------+
3 rows in set (0.01 sec)
```
