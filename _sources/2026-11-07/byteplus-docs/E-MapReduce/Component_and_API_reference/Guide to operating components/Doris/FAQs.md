---
title: "FAQs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/doris_faqs"
---

<span id="查询报错：failed-to-get-scan-range-no-queryable-replica-found-in-tablet-xxxx。"></span>
## Query error: Failed to get scan range, no queryable replica found in tablet: xxxx.

**A1：** 

This issue occurs because the corresponding tablet does not have any queryable replicas. Common causes may include BE node failures, missing replicas, and so on.

You can first use the `show tablet tablet_id` statement, then execute the subsequent `show proc` statement to view the replica information for this tablet and check whether the replicas are complete. You can also use `show proc "/cluster_balance"` to check the progress of replica scheduling and repair within the cluster.

For commands related to data replica management, refer to: [Data replica management](https://doris.apache.org/zh-CN/docs/admin-manual/maint-monitor/tablet-repair-and-balance).

<span id="show-backends-frontends-查看到的信息不完整。"></span>
## The information displayed by show backends/frontends is incomplete.

**A2：** 

After executing statements such as `show backends/frontends`, you may find that some columns in the results are missing content. For example, the show backends result may not display disk capacity information.

This issue typically occurs when the cluster has multiple FE nodes. If you connect to a non\-Master FE node to execute these statements, you will see incomplete information. This is because some information only exists on the Master FE node. For example, disk usage information for BE nodes. Therefore, only by connecting directly to the Master FE can you obtain complete information.

Of course, you can also set the session variable `set forward_to_master=true;` to true before executing these statements. After this setting, subsequent information query statements will automatically be forwarded to the Master FE to retrieve results. This way, regardless of which FE node you are connected to, you can obtain complete results.

<span id="data-size-exceeds-quota。"></span>
## data size exceeds quota。

Error: data size exceeds quota

Cause: The quota has been exhausted. Use show data to check the data volume and quota for a specific database.

Solution:

ALTER DATABASE xxx_doris_t1 SET DATA QUOTA 30TB;

For more operational methods, refer to the [official Doris website](https://doris.apache.org/docs/1.2/admin-manual/config/fe-config?_highlight=data&_highlight=size&_highlight=exceeds&_highlight=quota#default_db_data_quota_bytes)
