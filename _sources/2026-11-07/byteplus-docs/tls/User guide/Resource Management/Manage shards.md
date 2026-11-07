---
title: "Manage shards"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Managing_shards"
---

A log shard is the smallest unit for data storage and read\-write operations in Torch log service (TLS). Each shard provides a certain data read and write capacity.

<span id=".5YiG5Yy65qaC6L-w"></span>
## Shard overview

A log topic consists of one or more shards. Each topic uses MD5 to define the entire range of all shards, and each shard provides a certain data read and write capacity. You can specify the number of shards when creating a log topic. TLS also supports enhancing the reading and writing performance of the topic dynamically by enabling automatic sharding or manual split shard features. Shard operations such as splitting or merging change the shard status, but TLS only charges for shards that are in the read\-write state.

<span id=".6K-75YaZ6IO95Yqb"></span>
### Read\-write capacity

Each log shard provides a certain level of read and write capability. For detailed information, please refer to the table below.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">This is a non\-mandatory requirement. When data read/write operations exceed the read/write capacity of the log shard, the system will provide service to the best of its ability, but does not guarantee service quality.</div>



|Limitations |Limitation |
|---|---|
|Read QPS |100 times per second |
|Write QPS |500 times per second |
|Read traffic |20 MiB/s |
|Write traffic |5 MiB/s |


&nbsp;

&nbsp;

The number of shards incurs certain costs. Try to plan shard quantities reasonably based on your business traffic. We recommend that you set a relatively small number of shards and enable auto split. TLS will automatically split shards if read and write capacity is continuously exceeded for 5 minutes. This ensures higher performance and avoids unnecessary charges due to excessive idle shards.

<span id=".5YiG5Yy66IyD5Zu0"></span>
### Shard range

The MD5 range of a log topic defines its overall range. Intervals of all read\-write shards within the topic are left\-closed and right\-open intervals. These intervals constitute the full MD5 range of the log topic. When creating a log topic, you must specify the number of shards. TLS automatically divides the topic's MD5 range evenly based on this number. Shards can also be split. The two new shards will cover the MD5 range of the original shards.

If you read data via TLS API, you need to specify the shard ID where the data is stored. For shard ID, you can go to topic details page on the console, or view shard list via DescribeShards.

When writing data, choose either load balancing mode or HashKey mode.


* Load balancing mode (default): Each data packet is written randomly to any available read\-write shard.

* HashKey mode: Specify the MD5 key value and write data to the shard whose range includes that key.


For example, a log topic named NewTopic contains three read\-write shards and one read\-only shard. The shard IDs, statuses, and ranges are as follows:


|Shard ID |Status |Range |
|---|---|---|
|Shard 0 |Read and write |[00000000000000000000000000000000,80000000000000000000000000000000) |
|Shard 1 |Read only |[80000000000000000000000000000000,ffffffffffffffffffffffffffffffff) |
|Shard 2 |Read and write |[80000000000000000000000000000000,c0000000000000000000000000000000) |
|Shard 3 |Read and write |[c0000000000000000000000000000000,ffffffffffffffffffffffffffffffff) |


When writing data, if the MD5 Key is specified as 5F, the data will be written to shard 0 that contains 5F; if the MD5 Key is specified as 8C, the data will be written to shard 2 that contains 8C.

<span id=".5YiG5Yy654q25oCB"></span>
### Shard status

TLS provides the following two shard statuses:


* Read and write: The current shard supports both writing and reading data. This type of shard is typically newly created or split and supports splitting and merging.

* Read only: Data in the current shard can only be consumed. new data cannot be written. After data in a read\-only shard expires and is deleted, TLS will automatically delete the shard. Read\-only shards are typically old shards that have been split. They will not be billed and can not be split.


If you create a topic, all shards are in read\-write status. After the shard is split, the original read\-write shard becomes read\-only. New data can not be written in. This also creates multiple new read\-write shards that can handle subsequent data write traffic.

<span id=".5YiG6KOC5YiG5Yy6"></span>
## Split shard

TLS supports shard split feature. If data traffic of a read\-write shard exceeds its service capacity, shard can be split into smaller ones. This feature helps to expand the overall read and write capacity of the log topic. After the shard is split, the original shard maintains its MD5 range. At the same time, the original shard becomes read\-only. After the data in this original shard expires and is deleted, the shard is automatically removed. The split also creates multiple new read\-write shards. The MD5 range of original shard is evenly distributed to each new shard.

TLS supports both manual and automatic split for shards.


* Auto split: After automatic sharding is enabled, if a read\-write shard exceeds service capacity for 5 consecutive minutes, TLS automatically splits the shard. You can enable automatic sharding and set the maximum number of splits when creating or modifying a log topic. For steps on auto split shard, see [Automatic split shards](https://docs.byteplus.com/docs/tls/Managing_shards#.6Ieq5Yqo5YiG6KOC5YiG5Yy6).

* Manual split: If automatic sharding is not enabled and the read\-write traffic exceeds service capacity, you can manually split shards in time based on your business volume. The number of manually split shards is also limited by the number of maximum shards. For instructions on manually splitting shards, see [Manually split shards](https://docs.byteplus.com/docs/tls/Managing_shards#.5omL5Yqo5YiG6KOC5YiG5Yy6).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="default">We recommend that you enable automatic sharding. Otherwise, if data volume exceeds read\-write capacity of the shard, data write traffic will be restricted.</div>


<span id=".6Ieq5Yqo5YiG6KOC5YiG5Yy6"></span>
### Automatic split shards

For example, after creating a log topic and enabling the auto split feature, to set up auto split while creating a log topic, see [Log topic](https://docs.byteplus.com/docs/tls/Managing_topics) for details.


1.  Log in to[ TLS console](https://console.byteplus.com/tls).

2. Select the region where log service is located from the top navigation bar.

3. On the left navigation bar, select **Resource Management** \> **Project** .

4. On the **Project** page, find the specified project and click the project name.

5. In the **Topic** section, find the specified log topic and click **Edit** in the **Actions** column.

6. Reset the parameters related to automatic sharding.

   
   |Parameters |Description |
   |---|---|
   |Automatic sharding |Automatic sharding can be enabled or disabled.<br><br><br>* Enabled: If the data volume exceeds the existing shard service capacity for 5 consecutive minutes, TLS automatically splits shards based on data volume to meet business needs. However, the number of shards after splitting can not exceed the maximum splits. New shards created within the last 15 minutes will not split automatically.<br><br>* Disabled: automatic sharding is not enabled. |
   |Maximum number of splits |Maximum number of shard splits, i.e., the maximum number of read\-write shards after splitting. The value range is 1 to 256.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The number of maximum shards is required to set only when <strong>Automatic sharding</strong> is enabled.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The number of <strong>Maximum shards</strong> must exceed the number of current <strong>shards</strong>. Otherwise, TLS can not split shards automatically.</div><br> |
   

5. Click **Reset**.


<span id=".5omL5Yqo5YiG6KOC5YiG5Yy6"></span>
### Manually split shards


1.  Log in to[ TLS console](https://console.byteplus.com/tls).

2. Select the region where log service is located from the top navigation bar.

3. On the left navigation bar, select **Resource Management** \> **Project** .

4. On the **Project** page, locate the specified project and click the project name.

5. On the **Topic** tab, you can split shards as follows.   

   * Split from topic list:

      In topic list, hover over the number of shards and then the shard list will show. Locate the shard that is in **read and write** status and click **Split** in the **Actions** column.

   * Split from shard list:

      * Split a single shard: In topic list, click **Detail** in **Actions** column of specified topic. In **Shard List** section, locate the target shard in **Read and write status**, and click **Split** in **Actions** column.

      * Batch split: Select the shards that are in **read\-write status**, and then click **Batch Split**.

6. Enter the number of splits, and then click **Confirm**.

   * The number of splits must be a power of 2, such as 2, 4, 8, or 16.

   * After splitting, the total number of shards that are in read\-write status can not exceed 256.


<span id="23ac2539"></span>
## Merge shards

TLS supports manual shard merge. When read\-write performance is excessive, you can merge shards to avoid unnecessary costs caused by too many idle shards. After merging, data in the original shards can still be consumed, but new data can not be written.

Shard merging means combining two adjacent **read\-write** shards into a new **read\-write** shard. The MD5 range of the merged shard will include both original MD5 ranges, and the original **read\-write** shards will become **read\-only**.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div>



* <div data-tips="true" data-tips-type="default">Only manual merging of shards is supported. When you click merge, the system automatically merges the adjacent shard on the right.</div>


* <div data-tips="true" data-tips-type="default">Merging the last read\-write shard is not supported.</div>


* <div data-tips="true" data-tips-type="default">Merging read\-only shards is not supported.</div>


1. Log in to [TLS console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. On the left navigation pane, select **Resource management**  **\> Project**.

4. On the **Project** page, locate the specified project and click the project name.

5. In the **Log Topic** tab, locate the log topic with shards to be merged.

6. Hover your mouse over the number of log topic shards to display the shard list. Find the specified **read\-write state** shard and click **Merge** in the **Actions** column.


<span id=".5p-l55yL5YiG5Yy65YiX6KGo"></span>
## View shard list

After creating a log topic, you can view the shard list on log details page.


1.  Log in to[ TLS console](https://console.byteplus.com/tls).

2. Select the region where log service is located from the top navigation bar.

3. On the left navigation bar, select **Resource Management** \> **Project** .

4. On the **Project** page, locate the specified project and click the project name.

5. On the **Log Topic** tab, find the target log topic and click **Action**  column  **Details** .

6. In the **Shard list** section, view the shard list.

   
   |Display item |Description |
   |---|---|
   |Shard ID |The unique ID of the shard in the topic. It is specified by the TLS backend. The shard ID starts from 0. |
   |Status |Shard statuses, include:<br><br><br>* Read and write: The current shard supports both writing and reading data. Shards in this status are usually newly created or split.<br><br>* Read only: Data in the current shard can only be consumed. New data can not be written. Shards in this status are usually old shards that have been split.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Read\-only shards are not billed.   </div><br>    |
   |Shard range |MD5 range of the shard The range of each interval is left\-closed and right\-open. |
   |Stop writing time |The last time log data was written to the current shard. |
