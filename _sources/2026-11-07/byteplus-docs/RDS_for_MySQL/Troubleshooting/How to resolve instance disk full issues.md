---
title: "How to resolve instance disk full issues"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/How_to_resolve_instance_disk_full_issues"
---

When using RDS for MySQL, if the disk usage is too high, the instance is set to read\-only, preventing write and update operations. This article describes several common causes and their solutions.

<span id="问题确认"></span>
## Confirming the issue

You can confirm the current disk usage of the instance by checking the disk usage monitoring item.


1. On the Instances page, click the instance name of the target instance to enter the Instances page.

2. Click the Monitoring and alarm tab at the top of the page.

3. Under the **Resource monitoring** category, view **Disk usage**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_970582dffa4ca780954c6e7ea22fab2b.png) </span>


<span id="快速止损"></span>
## Immediate mitigation

If disk usage is near or at 100%, you can reduce it by expanding the instance storage space or enabling the binlog available storage space switch.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">RDS for MySQL provides the <code>disk usage</code> metric. You can configure an alert policy for an instance to set an alert threshold for its disk usage. When disk usage exceeds the threshold, you receive a timely alert, preventing the instance from being set to a read\-only state due to a full disk. For more information, refer to <a href="https://www.volcengine.com/docs/6313/140424">Creating alert policies</a>.</div>


<span id="_1-扩容实例存储空间"></span>
### 1. Expand instance storage space

Expanding the instance storage space increases the disk limit.

For instructions, refer to the following documents:


* [Regular modification of specification](https://www.volcengine.com/docs/6313/75369)

* [Temporary upgrade](https://www.volcengine.com/docs/6313/587740)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Temporary upgrade is currently an invitation\-only feature of RDS for MySQL. To use it, <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000178">submit a ticket</a> to apply.</div>


<span id="_2-打开binlog可用存储空间开关"></span>
### 2. Turn on the binlog available storage space switch

An unreasonable binlog retention policy may cause binlogs to consume a large amount of disk space. Refer to [Cause analysis](https://www.volcengine.com/docs/6313/1411542#%E5%8E%9F%E5%9B%A0%E5%AE%9A%E4%BD%8D%E5%8F%8A%E8%A7%A3%E5%86%B3) to check binlog usage. If you confirm that binlogs are consuming excessive disk space, modify the local binlog retention policy and enable the Available storage space switch to prevent the disk from being filled by binlogs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Primary\-secondary replication in MySQL relies on binlogs. Retaining too few binlogs can interrupt the replication links for secondary and read\-only nodes, impacting instance availability.</div>


**Procedure**


1. On the Instances page, click the instance name of the target instance to enter the Instances page.

2. At the top of the page, click the Backups tab.

3. On the Backups page, click the **Backup policy** subtab and then click Edit for **Local binlog retention policy**.

4. In the dialog box on the right, enable the **Available storage space** switch and click **OK**. The setting for available binlog storage space will take effect.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5fbed6625242b81faa6038aa16d04b1c.png) </span>

<span id="原因定位及解决"></span>
## Cause analysis

High storage space usage in a MySQL instance can be caused by data fragmentation, oversized binlogs, oversized relay logs, or oversized temporary files. Solutions for these four reasons are provided in the following sections.

<span id="_1-数据出现空洞"></span>
### 1. Data holes

**Cause analysis**

In MySQL, especially when using the InnoDB storage engine, data files may consume more disk space because of 'holes' (free space). This typically occurs after many insert, update, and delete operations, leading to data holes and increased disk usage. Run the following command to obtain the table state:

```sql
SHOW TABLE STATUS LIKE <Table name with potential data holes>;
```


Check the `Data_free` field. A large value for `Data_free` indicates numerous data holes.

**Solution**

Run the following command to perform table optimization and eliminate data holes.

```sql
OPTIMIZE TABLE '<Table name with data fragmentation>';
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When executing <code>OPTIMIZE TABLE</code>, MySQL applies a write lock on the table until the operation is complete. This means that during the optimization process, other Read/Write operations on the table are blocked, which may cause application latency or Timeout. The optimization process may consume a large amount of System resources, especially when the table size is large, which may affect the overall performance of the Database. For large tables, the execution time of <code>OPTIMIZE TABLE</code> can be long, which may lead to long\-term locks and potential application interruptions. Therefore, execute <code>OPTIMIZE TABLE</code> during off\-peak hours or use an <a href="https://www.volcengine.com/docs/6313/97982">OnlineDDL task</a> to perform this operation.</div>


<span id="_2-binlog-数据过大"></span>
### 2. Binlog data is too large

This issue may be caused by two situations: an unreasonable binlog retention policy or the generation of large transactions.

<span id="binlog-保留策略不合理"></span>
#### Unreasonable binlog retention policy

**Cause analysis**

When the [binlog retention policy](https://www.volcengine.com/docs/6313/97306) configured for the instance is unreasonable, the binlog may not be cleaned up in time, thus consuming excessive disk space.

**Solution**

Adjust the binlog retention policy to manage its disk usage.

<span id="有大事务产生"></span>
#### Large transactions occurred

**Cause analysis**

When a large transaction occurs (such as a delete operation on a table), it may generate an oversized binlog file. This type of binlog file cannot be split, resulting in a single file consuming a large amount of disk space.

**Solution**


1. Split transactions to avoid creating large ones.

2. Expand the instance storage space.

3. Adjust the binlog retention policy so the binlog file can be cleared quickly.


<span id="_3-relay-log-过大"></span>
### 3. Oversized relay log

**Cause analysis**

In MySQL, the generation of a large number of relay logs is usually related to issues in the primary\-secondary replication process. Common reasons include:


1. Insufficient resources on the secondary and read\-only nodes slow down data synchronization, causing relay logs to accumulate.

2. A high write load on the primary node generates a large volume of binlogs, requiring the secondary database to process a large number of relay logs.


**Solutions**


1. Expand compute resources to accelerate data synchronization.

2. Optimize the write policy to avoid generating a large volume of binlogs in a short period.


<span id="_4-临时文件过大"></span>
### 4. Oversized temporary files

**Cause analysis**

Oversized temporary files are often caused by complex queries, insufficient memory, and poor query design. Optimize queries, adjust memory configuration, and monitor temporary table usage to effectively reduce the creation of temporary files.

**Solutions**


1. Expand memory so more temporary tables can be processed in memory.

2. Optimize SQL queries by reducing complexity, avoiding unnecessary JOINs and subqueries, and using appropriate indexes to improve query performance and reduce the creation of temporary files.
