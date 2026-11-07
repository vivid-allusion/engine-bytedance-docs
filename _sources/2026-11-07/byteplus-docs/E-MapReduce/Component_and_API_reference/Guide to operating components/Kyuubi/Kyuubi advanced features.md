---
title: "Kyuubi advanced features"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Kyuubi_advanced_features"
---

This article introduces some concepts related to Kyuubi and the usage of its advanced features.

<span id="_1-引擎支持"></span>
## 1 Engine support

Volcano Engine E\-MapReduce (EMR) Kyuubi provides out\-of\-the\-box support for Spark3 On YARN mode. Engines such as Flink, Trino, and Spark2 have not been verified, and production\-ready support is not currently promised.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To use other engines with Kyuubi, you can switch by configuring kyuubi.engine.type. For details on configuration changes, see <a href="https://docs.byteplus.com/docs/E-MapReduce/105412">Manage service configuration parameters</a>.</div>


<div data-tips="true" data-tips-type="warning">Caution: kyuubi.engine.type is an experimental configuration. When a value other than SPARK_SQL is selected, the sharing level is restricted to CONNECTION, which conflicts with the kyuubi.engine.share.level configuration.</div>


All Kyuubi engines mentioned below refer to Spark3 engines running On YARN.

<span id="_2-引擎共享等级"></span>
## 2 Engine sharing levels

According to the kyuubi.engine.share.level configuration provided in the kyuubi\-defaults configuration file, you can define the engine sharing level for the Kyuubi service.

The supported sharing levels and their corresponding meanings are described as follows:


|Sharing level |Meaning |Remarks |
|---|---|---|
|CONNECTION |Each session exclusively uses one engine |Each connection incurs significant engine creation overhead when first established. |
|USER |Each user exclusively uses one engine |Out\-of\-the\-box configuration. |
|GROUP |Each resource group uses one engine | |
|SERVER |Each cluster uses one engine |The lowest isolation level requires administrators to have sufficient confidence in cluster security. |


<span id="_3-正确配置-kyuubi-引擎"></span>
## 3 Correctly configuring the Kyuubi engine

The Kyuubi engine is essentially a computing engine submitted via spark\-submit. The final configuration of this engine can come from multiple sources and follows a certain priority order for overrides.

<span id="_3-1-通过-spark-defaults-conf"></span>
### 3.1 Via spark\-defaults.conf

As with other Spark jobs, the primary source for the Kyuubi engine is the definition in the spark\-defaults.conf file.

<span id="_3-2-通过-kyuubi-defaults-conf"></span>
### 3.2 Via kyuubi\-defaults.conf

Furthermore, Kyuubi also supports directly adding Spark configurations in its own kyuubi\-defaults.conf configuration file. The configurations defined in this file will override those with the same name in spark\-defaults.conf.

<span id="_3-3-通过-jdbc-connection-url"></span>
### 3.3 Via JDBC Connection URL

When using Kyuubi via JDBC, you can directly define connection\-level configurations in the connection string. For Static SQL and other Spark Core configurations (such as spark.executor.memory), if a new engine instance is created for this connection, these configurations will also take effect.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For related configuration documentation, refer to:</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://spark.apache.org/docs/latest/configuration.html#runtime-sql-configuration">Spark Runtime SQL Configuration</a>, effective for each connection.</div>


* <div data-tips="true" data-tips-type="tip"><a href="https://spark.apache.org/docs/latest/configuration.html#static-sql-configuration">Static SQL and Spark Core Configuration</a>, whether it takes effect depends on whether an engine instance is created for this connection.</div>


* <div data-tips="true" data-tips-type="tip">For EMR\-3.7.3 and later versions, Kyuubi sets the default value of <code>spark.dynamicAllocation.enabled</code> to <code>true</code> for the Spark3 engine. You can modify the configuration to disable dynamic resource allocation or adjust related parameters.</div>


* <div data-tips="true" data-tips-type="tip">For EMR\-3.8.0 and later versions, based on cluster specifications, Kyuubi sets default values for several resource configuration parameters for the Spark3 engine: <code>spark.executor.cores</code>, <code>spark.executor.memory</code>, <code>spark.driver.cores</code>, and <code>spark.driver.memory</code>. You can update these parameters by modifying the configuration.</div>



<span id="_3-4-通过-set-syntax"></span>
### 3.4 Via SET syntax

For this method, refer to the official documentation guide, [Set Command](https://spark.apache.org/docs/latest/sql-ref-syntax-aux-conf-mgmt-set.html).

<span id="_3-5-租户级别引擎配置"></span>
### 3.5 Tenant\-level engine configuration

In Kyuubi, to support more fine\-grained tenant\-level engine configuration, the kyuubi\-defaults.conf configuration file allows you to define such configurations in the form of `___{username}___.{config_key}`. There must be three consecutive underscores _ on both sides of the username, and the `.` symbol is used to separate the specific `config_key` from the prefix.

This type of configuration only takes effect at the time of **engine creation**. Its priority is higher than `spark-defaults` and `kyuubi-defaults`, but it will be overridden by configurations provided by `JDBC Connection URL` and `Set Command`.

The following are some configuration examples.

```bash
# For system defaults
spark.master=local
spark.sql.adaptive.enabled=true 

# For a user named kent
___kent___.spark.master=yarn
___kent___.spark.sql.adaptive.enabled=false 

# For a user named bob
___bob___.spark.master=spark://master:7077
___bob___.spark.executor.memory=8g
```


<span id="_4-引擎复用与-subdomain-定义"></span>
## 4 Engine reuse and subdomain definition

The following scenarios are based on the USER sharing level.

The Spark engine submitted by Kyuubi remains active for a period after a job is completed. During the engine's lifetime, subsequent jobs can reuse the original engine directly, eliminating the overhead of waiting for engine creation and significantly improving job performance. This lifetime is determined by the configuration `kyuubi.session.engine.idle.timeout`, with a default value of `PT30M` (that is, 30 minutes).

For the same user, in actual production environments, it may be desirable to run jobs in different engines based on different job types. In Kyuubi, this requirement can be met by configuring `kyuubi.engine.share.level.subdomain`.

This is a connection\-level configuration. By specifying it directly in the relevant connection configuration parameters, jobs for this connection can be submitted to different subdomains.

```bash
beeline -n user1 -p user1_password -u "jdbc:hive2://master-1-1:10009/biz1?kyuubi.engine.share.level.subdomain=biz1" \
  -f query1.sql

beeline -n user1 -p user1_password -u "jdbc:hive2://master-1-1:10009/biz2?kyuubi.engine.share.level.subdomain=biz2" \
  -f query2.sql

beeline -n user1 -p user1_password -u "jdbc:hive2://master-1-1:10009/biz3?kyuubi.engine.share.level.subdomain=biz3" \
  -f query3.sql
```
