---
title: "Slow SQL analysis"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Slow_SQL_analysis"
---

<span id="_1-审计日志"></span>
## Audit log

<span id="_1-1-创建审计日志库与表"></span>
### Create audit log database and tables

```sql
CREATE DATABASE starrocks_audit_db__;

CREATE TABLE starrocks_audit_db__.starrocks_audit_tbl__ (
  `queryId`           VARCHAR(64)                COMMENT "查询的唯一ID",
  `timestamp`         DATETIME         NOT NULL  COMMENT "查询开始时间",
  `queryType`         VARCHAR(12)                COMMENT "查询类型（query, slow_query, connection）",
  `clientIp`          VARCHAR(32)                COMMENT "客户端IP",
  `user`              VARCHAR(64)                COMMENT "查询用户名",
  `authorizedUser`    VARCHAR(64)                COMMENT "用户唯一标识，既user_identity",
  `resourceGroup`     VARCHAR(64)                COMMENT "资源组名",
  `catalog`           VARCHAR(32)                COMMENT "Catalog名",
  `db`                VARCHAR(96)                COMMENT "查询所在数据库",
  `state`             VARCHAR(8)                 COMMENT "查询状态（EOF，ERR，OK）",
  `errorCode`         VARCHAR(512)               COMMENT "错误码",
  `queryTime`         BIGINT                     COMMENT "查询执行时间（毫秒）",
  `scanBytes`         BIGINT                     COMMENT "查询扫描的字节数",
  `scanRows`          BIGINT                     COMMENT "查询扫描的记录行数",
  `returnRows`        BIGINT                     COMMENT "查询返回的结果行数",
  `cpuCostNs`         BIGINT                     COMMENT "查询CPU耗时（纳秒）",
  `memCostBytes`      BIGINT                     COMMENT "查询消耗内存（字节）",
  `stmtId`            INT                        COMMENT "SQL语句增量ID",
  `isQuery`           TINYINT                    COMMENT "SQL是否为查询（1或0）",
  `feIp`              VARCHAR(128)               COMMENT "执行该语句的FE IP",
  `stmt`              VARCHAR(1048576)           COMMENT "原始SQL语句",
  `digest`            VARCHAR(32)                COMMENT "慢SQL指纹",
  `planCpuCosts`      DOUBLE                     COMMENT "查询规划阶段CPU占用（纳秒）",
  `planMemCosts`      DOUBLE                     COMMENT "查询规划阶段内存占用（字节）"
) ENGINE = OLAP
DUPLICATE KEY (`queryId`, `timestamp`, `queryType`)
COMMENT "审计日志表"
PARTITION BY RANGE (`timestamp`) ()
DISTRIBUTED BY HASH (`queryId`) BUCKETS 3 
PROPERTIES (
  "dynamic_partition.time_unit" = "DAY",
  "dynamic_partition.start" = "-30",  --Indicates that only audit information from the last 30 days is retained. Adjust as needed.
  "dynamic_partition.end" = "3",
  "dynamic_partition.prefix" = "p",
  "dynamic_partition.buckets" = "3",
  "dynamic_partition.enable" = "true",
  "replication_num" = "3"  --If the number of BE nodes in the cluster is not greater than 3, the replica count can be adjusted to 1. Adjustment is not recommended for production clusters.
);
```


<span id="_1-2-安装审计日志插件"></span>
### Install audit log plugin


1. [Download](https://releases.mirrorship.cn/resources/AuditLoader.zip) the AuditLoader installation package.


This plugin is compatible with all currently maintained StarRocks versions.


2. Extract the installation package and locate the audit log plugin for the corresponding version.

   Extract auditloader.zip to generate the following files:

   * **auditloader.jar**: The program jar package compiled from the audit plugin code.

   * **plugin.properties**: The plugin property file, which provides description information for the audit plugin within the StarRocks cluster. No modification is required.

   * **plugin.conf**: The plugin configuration file, which provides configuration parameters for Stream Load writes at the plugin's underlying layer. This file must be modified according to cluster information. It is generally recommended to only modify the `user` and `password` information.

3. Modify the configuration file plugin.conf.


```sql
# StarRocks user. 
user=xxx

# StarRocks user's password
password=xxx
```



4. Repackage the above files.


```sql
zip -q -m -r auditloader.zip auditloader.jar plugin.conf plugin.properties
```



5. Install the log plugin.

   1. Distribute the compressed package to all machines running FE nodes. Ensure that all compressed packages are stored in the same path; otherwise, the plugin installation will fail. After distribution is complete, copy the absolute path of the compressed package.

   ```sql
   cp auditloader.zip /data01/starrocks3/plugins/
   ```
   

   2. Run the following command in StarRocks to install.

   ```sql
   INSTALL PLUGIN FROM "/data01/starrocks3/plugins/auditloader.zip";
   ```
   

   3. Check installation status

   ```sql
   SHOW PLUGINS
   
   
   MySQL [demo]> show plugins;
   +---------------------------+-------+-------------------------------------------------------------------------+---------+-------------+----------------------------------------------+--------+--------------------------------------------+-----------+------------+
   | Name                      | Type  | Description                                                             | Version | JavaVersion | ClassName                                    | SoName | Sources                                    | Status    | Properties |
   +---------------------------+-------+-------------------------------------------------------------------------+---------+-------------+----------------------------------------------+--------+--------------------------------------------+-----------+------------+
   | __builtin_AuditLogBuilder | AUDIT | builtin audit logger                                                    | 0.12.0  | 1.8.31      | com.starrocks.qe.AuditLogBuilder             | NULL   | Builtin                                    | INSTALLED | {}         |
   | AuditLoader               | AUDIT | load audit log to starrocks, and user can view the statistic of queries | 3.0.0   | 1.8.0       | com.starrocks.plugin.audit.AuditLoaderPlugin | NULL   | /data01/starrocks3/plugins/auditloader.zip | INSTALLED | {}         |
   +---------------------------+-------+-------------------------------------------------------------------------+---------+-------------+----------------------------------------------+--------+--------------------------------------------+-----------+------------+
   ```
   

6. Find SQL statements longer than 10 seconds.


```sql
select *  from starrocks_audit_db__.starrocks_audit_tbl__  where  queryTime > 10000 limit 10;
```


<span id="_2-慢sql优化"></span>
## Slow SQL optimization


1. Open the StarRocks web interface


http://xxx.xxx.xxx.xxx:8030/query

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The web browser must be able to access the FE node network. If the connection is not possible, the FE node needs to <a href="https://www.volcengine.com/docs/6401/68687">bind a public IP</a>.</div>



2. Connect to the StarRocks service. Before executing SQL, run the following statement to enable profile.


```sql
set enable_profile = true;
```



3. Execute the query SQL


Sample SQL: TPCDS Q1

```sql
SELECT l_returnflag,
       l_linestatus,
       sum(l_quantity) AS sum_qty,
       sum(l_extendedprice) AS sum_base_price,
       sum(l_extendedprice * (1 - l_discount)) AS sum_disc_price,
       sum(l_extendedprice * (1 - l_discount) * (1 + l_tax)) AS sum_charge,
       avg(l_quantity) AS avg_qty,
       avg(l_extendedprice) AS avg_price,
       avg(l_discount) AS avg_disc,
       count(*) AS count_order
FROM lineitem
WHERE l_shipdate <= date '1998-12-01' - interval '90' DAY
GROUP BY l_returnflag,
         l_linestatus
ORDER BY l_returnflag,
         l_linestatus
```



4. Open the Query Profile page in the StarRocks web UI and locate the SQL you just executed


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2075b1b27d7587cecf526bc91d25bc4d.png) </span>


5. Analyze the slow parts of the query on the SQL's Profile page


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b69800cad444631f0ee795b10e4d7197.png) </span>


1. Through the profile, you can see the total time is 12 seconds. Most of the time is spent on InputEmptyTime in Pipeline (id=0) of Fragment 0, indicating that the dependent Pipeline executes slowly.

   ```sql
   Pipeline (id=0):
          - PendingTime: 12s457ms
            - InputEmptyTime: 12s461ms
              - __MAX_OF_InputEmptyTime: 12s461ms
              - __MIN_OF_InputEmptyTime: 12s461ms
              - FirstInputEmptyTime: 1s557ms
                - __MAX_OF_FirstInputEmptyTime: 12s461ms
                - __MIN_OF_FirstInputEmptyTime: 71.864us
              - FollowupInputEmptyTime: 10s904ms
                - __MAX_OF_FollowupInputEmptyTime: 12s461ms
                - __MIN_OF_FollowupInputEmptyTime: 0ns
   Pipeline (id=1):
          - ActiveTime: 116.114us
          - BlockByInputEmpty: 2
          - BlockByOutputFull: 0
          - BlockByPrecondition: 0
          - DegreeOfParallelism: 1
          - DriverPrepareTime: 52.421us
          - DriverTotalTime: 12s463ms
          - OverheadTime: 15.322us
          - PeakDriverQueueSize: 0
          - PendingTime: 12s455ms
            - InputEmptyTime: 12s463ms
              - FirstInputEmptyTime: 12s463ms
              - FollowupInputEmptyTime: 123.778us
            - OutputFullTime: 0ns
            - PendingFinishTime: 0ns
            - PreconditionBlockTime: 0ns
   ```
   

2. The last Pipeline (id=5) of Fragment 1 has a high proportion of time spent on PendingTime.

   ```sql
   - PendingTime: 12s451ms
              - __MAX_OF_PendingTime: 12s456ms
              - __MIN_OF_PendingTime: 12s447ms
              - InputEmptyTime: 12s454ms
                - __MAX_OF_InputEmptyTime: 12s456ms
                - __MIN_OF_InputEmptyTime: 12s450ms
                - FirstInputEmptyTime: 12s454ms
                  - __MAX_OF_FirstInputEmptyTime: 12s456ms
                  - __MIN_OF_FirstInputEmptyTime: 12s450ms
                - FollowupInputEmptyTime: 2.322us
                  - __MAX_OF_FollowupInputEmptyTime: 4.837us
                  - __MIN_OF_FollowupInputEmptyTime: 0ns
   ```
   

3. Pipeline (id=0) of Fragment 2 has a high ActiveTime and low PendingTime, indicating that Pipeline (id=0) takes a long time to execute.

   ```sql
   Pipeline (id=0):
            - ActiveTime: 11s606ms
              - __MAX_OF_ActiveTime: 11s967ms
              - __MIN_OF_ActiveTime: 11s239ms
            - PendingTime: 391.728ms
              - __MAX_OF_PendingTime: 722.636ms
              - __MIN_OF_PendingTime: 167.023ms
   Pipeline (id=1):
            - ActiveTime: 7s808ms
            - PendingTime: 1s462ms
              - __MAX_OF_PendingTime: 1s678ms
              - __MIN_OF_PendingTime: 1s251ms
   Pipeline (id=2):
            - ActiveTime: 250.294us
   ```
   

   In Pipeline (id=0), expression calculation time accounts for a high proportion, indicating that due to the large number of rows, expression calculation takes longer.

   ```sql
   PROJECT (plan_node_id=1):
       CommonMetrics:
               - OperatorTotalTime: 8s728ms
                  - __MAX_OF_OperatorTotalTime: 9s30ms
                  - __MIN_OF_OperatorTotalTime: 8s291ms
               - PullRowNum: 5.916B (5915582721)
                  - __MAX_OF_PullRowNum: 192.590M (192590370)
                  - __MIN_OF_PullRowNum: 177.111M (177110504)
        UniqueMetrics:
                - CommonSubExprComputeTime: 4s346ms
                  - __MAX_OF_CommonSubExprComputeTime: 4s547ms
                  - __MIN_OF_CommonSubExprComputeTime: 4s71ms
   ```
   

   In Pipeline (id=1), AGGREGATE_STREAMING_SINK execution time is long, indicating

   ```sql
   AGGREGATE_STREAMING_SINK (plan_node_id=2):
               - OperatorTotalTime: 7s597ms
                  - __MAX_OF_OperatorTotalTime: 7s978ms
                  - __MIN_OF_OperatorTotalTime: 7s190ms
   ```
