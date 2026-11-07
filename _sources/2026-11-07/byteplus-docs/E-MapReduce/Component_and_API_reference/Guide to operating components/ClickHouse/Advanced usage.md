---
title: "Advanced usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/clickhouse_advanced_usage"
---

This article introduces advanced features related to ClickHouse clusters.

<span id="_1-前提条件"></span>
## 1. Prerequisites

A Volcano Engine E\-MapReduce (EMR) cluster type that includes **ClickHouse** has been created. For details, see [Quickstart](https://docs.byteplus.com/docs/E-MapReduce/109198).

<span id="_2-用户管理"></span>
## 2. User management

You can view or modify configurations on the ClickHouse service parameter configuration page. This step will create a user named test in the ClickHouse cluster, with the users configured in the **server\-users** configuration file.


1. Log in to the [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the left navigation pane, click **Cluster List \> Cluster Details \> Service List \> ClickHouse Service \> Service Parameters** to enter the ClickHouse service parameter page, and click the **Add Custom Parameter** button.

3. In the Add Custom Parameter window, select the server\-users configuration file from the configuration file parameter dropdown, and add the following parameters:

   ```toml
   ## test is the username
   users.test.profile ## The default profile name used by the test user; here, the default profile is used
   users.test.quota ## The default quota configuration used by the test user; here, the default quota is used
   users.test.password ## The password for the test user; here, 123456 is used as a temporary password
   users.test.networks.ip ## Network configuration: IP is set to ::/0, other fields are left empty, indicating that any IP can connect
   users.test.networks.host_regexp ## Allowed hostname regular expression; default is empty.
   users.test.networks.host ## Allowed hostnames; default is empty.
   ```
   


The final parameter configuration result is as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_28d7e631562ae750c05050f0f87181dc.png) </span>


4. After the parameter configuration is complete, click the **Service Operation \> Restart** button in the upper right corner to restart the ClickHouse node. Then, log in to the Core node remotely and check the /etc/emr/clickhouse/users.xml configuration to confirm whether test exists. For login methods, see [Quickstart](https://docs.byteplus.com/docs/E-MapReduce/109198).

5. Run the following command to view the configuration file:

   ```shell
   cat /etc/emr/clickhouse/users.xml
   ```
   


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fc752ce94cfd8a91a1b5062cbefa2478.png) </span>


6. After confirming that the user exists, run the following command to start the ClickHouse client and log in directly using the new user and password:

   ```bash
   clickhouse-client --user test --password 123456
   ```
   


<span id="_3-生命周期管理"></span>
## 3. Lifecycle management

Data stored in ClickHouse is generally quite real\-time, and the usage frequency of historical data gradually decreases. In some cases, old data may not be accessed at all. Therefore, managing the lifecycle of ClickHouse table data can effectively reduce cluster storage costs.

ClickHouse currently supports TTL settings at both the table and column levels, and also supports various types of data operations.

The following uses table\-level TTL as an example to introduce the lifecycle feature of ClickHouse:

```sql
CREATE TABLE example_table
(
    d DateTime,
    a Int
)
ENGINE = MergeTree
PARTITION BY toYYYYMM(d)
ORDER BY d
TTL d + INTERVAL 1 MONTH DELETE,
    d + INTERVAL 1 WEEK TO VOLUME 'aaa',
    d + INTERVAL 2 WEEK TO DISK 'bbb';
```


In the above example, a MergeTree table is defined, and its data will be migrated over time:


1. Data older than one month will be deleted directly, which is the default behavior.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended to use the DELTE mode. Other modes require manual management of disk capacity.   </div>
   

2. Data older than one week will be moved to VOLUME 'aaa';

3. Data older than two weeks will be moved to DISK 'bbb'.


For more information, see the [official documentation](https://clickhouse.com/docs/en/engines/table-engines/mergetree-family/mergetree#table_engine-mergetree-ttl).

<span id="_4-冷热分层设置"></span>
## 4. Hot and cold tiered storage settings

For certain ClickHouse tables, there are still scenarios where historical data is queried infrequently. In such cases, TTL cannot be used directly to delete data, so hot and cold tiering can be configured to reduce storage costs. On Volcano Engine Cloud, we recommend using TOS as cold storage.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Hot and cold tiering currently only supports EMR\-3.1.0 and above clusters.</div>



1. In the left navigation bar, click **Cluster List \> Cluster Details \> Service List \> ClickHouse Service \> Service Parameters** to access the ClickHouse service parameters page.

2. On the service parameters page, click to select the "**server\-metrika**" configuration file.

3. In the "**storage_configuration**" parameter, modify the CoreGroup configuration and add the following two configuration sections:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f690275a0d96294c6e4f579ba5159b08.png) </span>

   1. A TOS disk needs to be created:

      ```xml
      <storage_configuration>
          ...
          <disks>
              <tos>
                  <type>s3</type>
                  <endpoint></endpoint>
                  <access_key_id>your_access_key_id</access_key_id>
                  <secret_access_key>your_secret_access_key</secret_access_key>
                  <region></region>
                  <connect_timeout_ms>10000</connect_timeout_ms>
                  <request_timeout_ms>5000</request_timeout_ms>
                  <retry_attempts>10</retry_attempts>
                  <single_read_retries>4</single_read_retries>
                  <min_bytes_for_seek>1000</min_bytes_for_seek>
                  <metadata_path>/var/lib/clickhouse/disks/s3/</metadata_path>
                  <cache_enabled>true</cache_enabled>
                  <cache_path>/var/lib/clickhouse/disks/s3/cache/</cache_path>
                  <skip_access_check>false</skip_access_check>
              </tos>
          </disks>
          ...
      </storage_configuration>
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the Endpoint uses Volcano Engine's TOS, the configuration items must meet the following requirements:      </div>
      

         1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The HTTP protocol must be used.      </div>
      

         2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The format must be [bucket\-name] + [TOS S3 type Endpoint] + [key]      </div>
      

         3. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">It must end with "/"      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Example: http://emr\-hzw.tos\-s3\-cn\-beijing.ivolces.com/ClickHouse/      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For TOS Endpoint, refer to <a href="https://www.volcengine.com/docs/6349/107356">official documentation</a>.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">region: Fill in the actual region, for example, cn\-beijing.      </div>
      

   2. Create a Storage policy:

      ```xml
      <storage_configuration>    
          <policies>
              <tos_cold>
                  <volumes>
                      <main>
                          <disk>default</disk>
                      </main>
                      <external>
                          <disk>tos</disk>
                      </external>
                  </volumes>
                  <move_factor>0.2</move_factor>
              </tos_cold>
          </policies>
       </storage_configuration>
      ```
      


The following is an XML template. The five parameters **endpoint, access_key_id, secret_access_key, region, move_factor** are key information and must be modified according to different configurations:

```xml
<disks>
    <disk1>
        <path>/data01/clickhouse/</path>
        <keep_free_space_bytes>10485760</keep_free_space_bytes>
    </disk1>
    <tos>
        <type>s3</type>
        <endpoint>http://emr.tos-s3-cn-beijing.ivolces.com/Clickhouse-emr/</endpoint>
        <access_key_id>AK</access_key_id>
        <secret_access_key>SK</secret_access_key>
        <region>cn-beijing</region>
        <connect_timeout_ms>10000</connect_timeout_ms>
        <request_timeout_ms>5000</request_timeout_ms>
        <retry_attempts>10</retry_attempts>
        <single_read_retries>4</single_read_retries>
        <min_bytes_for_seek>1000</min_bytes_for_seek>
        <metadata_path>/var/lib/clickhouse/disks/s3/</metadata_path>
        <cache_enabled>true</cache_enabled>
        <cache_path>/var/lib/clickhouse/disks/s3/cache/</cache_path>
        <skip_access_check>false</skip_access_check>
    </tos>
</disks>
<policies>
    <default>
        <volumes>
            <single>
                <disk>disk1</disk>
            </single>
        </volumes>
    </default>
    <tos_cold>
        <volumes>
            <main>
                <disk>disk1</disk>
            </main>
            <external>
                <disk>tos</disk>
            </external>
        </volumes>
        <move_factor>0.1</move_factor>
    </tos_cold>
</policies>
```



4. After completing the parameter configuration, connect to the ClickHouse cluster client using remote login, and specify the Storage policy when creating a table:


```sql
CREATE TABLE table_with_non_default_policy (
    EventDate Date,
    OrderID UInt64,
    BannerID UInt64,
    SearchPhrase String
) ENGINE = MergeTree
ORDER BY (OrderID, BannerID)
PARTITION BY toYYYYMM(EventDate)
SETTINGS storage_policy = 'tos_cold'
```



5. Insert data:


```sql
insert into table_with_non_default_policy select '2022-09-09', rand(), rand(), 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' from numbers(100000000);
```
