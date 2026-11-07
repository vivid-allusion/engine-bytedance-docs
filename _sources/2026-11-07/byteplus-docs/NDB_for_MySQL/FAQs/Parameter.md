---
title: "Parameter"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Parameter_faq"
---

<span id=".5Zyo5Y-C5pWw566h55CG5Lit5Li65LuA5LmI5om-5LiN5Yiw6ZyA6KaB5L-u5pS555qE5Y-C5pWw77yf"></span>
### Why can't I find the parameter I need to modify in parameter management?

For security and stability reasons, only some parameters can be modified currently. If you do not find the parameter to be modified, you can [submit a ticket](https://console.byteplus.com/workorder/create) for technical support.

<span id=".5L-u5pS55Y-C5pWw5ZCO77yM6ZyA6KaB6YeN5ZCv5a6e5L6L5ZCX77yf"></span>
### Does modifying parameters require an instance restart?

Some parameter changes require an instance restart. Check whether [Restart instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Restarting_instances) operation is needed on the **Modifying parameters** page in the console. For details, refer to [Modifying parameters](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_parameters).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Instance restart will cause connection interruptions. Schedule businesses accordingly before restarting. We recommend you restart instances during off\-peak hours and ensure that applications have an automatic reconnection mechanism.</div>


<span id=".5aaC5L2V5p-l6K-i5LqR5pWw5o2u5bqTLXZlZGItbXlzcWwt54mI5LiN5pSv5oyB5L-u5pS555qE5Y-C5pWw55qE6K6-5a6a5YC877yf"></span>
### How to query the values of non\-modifiable parameters in NDB for MySQL?

You can log on to [Database Workbench](https://console.byteplus.com/dbw) and use the SQL statement `SHOW variables like 'parameter name';` to view it.

<span id=".6KGo5ZCN5aSn5bCP5YaZLWxvd2VyLWNhc2UtdGFibGUtbmFtZXMt5Y-C5pWw5pSv5oyB5L-u5pS55ZCX77yf"></span>
### Is the `lower_case_table_names` parameter modifiable?

During instance creation, you can configure case sensitivity for table names. This parameter can not be modified after the instance is provisioned.

<span id=".5aaC5L2V5L-u5pS5LXZlZGItbXlzcWwt5a6e5L6L55qE5pyA5aSn6L-e5o6l5pWw77yf"></span>
### How to modify the max connections for NDB for MySQL instance?

The default value of max connections depends on the [node specification](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications). You can modify it via the console and API. For details, refer to [Modifying max connections](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_maximum_connections)

<span id=".5aaC5L2V5L-u5pS5LXZlZGItbXlzcWwt5oWiLXNxbC3nmoTlrprkuYnml7bplb_vvJ8="></span>
### How to modify the slow query threshold for NDB for MySQL instances?

The slow query threshold is defined by the `long_query_time` parameter, with a default value of 1 second. You can modify it in the **Parameter management** tab. For steps, refer to [Modifying parameters](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_parameters).

<span id=".5aaC5L2V5p-l55yLLXZlZGItbXlzcWwt5Y-C5pWw55qE6K-m57uG5LuL57uN77yf"></span>
### How to view detailed descriptions of NDB for MySQL parameters?

On the parameter configuration page, place the mouse on the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fcfeed03b2b27a9bdf5d01d6db1fbc40.png)<sub> </sub></span>icon after the target parameter name to view the description of the parameter.

NDB for MySQL is 100% compatible with MySQL community edition. You may also refer to the [Parameter reference](https://dev.mysql.com/doc/refman/8.0/en/server-system-variable-reference.html) in MySQL community.

<span id="Uq00Mgab"></span>
### How do I enable binlog for NDB for MySQL?

The binlog of NDB for MySQL is enabled by default and cannot be disabled.


* Storage policy: Files are retained for 5 days by default. Binlog files older than 5 days will be automatically deleted.

* Modify the save duration

   * If the instance minor version is NDB for MySQL 3.0, you can set the binlog retention period by modifying the `vedb_binlog_expire_logs_seconds` parameter value (the value range is 0 to 4294967295 seconds, and the default value is 432000). 0 means do not automatically delete binlog files.

   * If the instance minor version is NDB for MySQL 2.0, modifying the retention period is not allowed.


<span id="wtA9BuUe"></span>
### When I modify the `collation_server` or `character_set_server` parameters, an `InvalidParameter` error message appears.

The `collation_server` parameter and the `character_set_server` parameter must be consistent. That is, the collation must belong to the current character set. Therefore, you can set the above two parameters to be consistent at the same time, or set a parameter separately to be consistent with another parameter.

<span id="wlH4zR1T"></span>
### The parameter modification value is within the editable range, but the error `InvalidParameter_NotDivisible` is displayed?

Some parameter values ​​are required to be divisible by specific values, so the control performs integer divisibility check. The parameters involved in the verification are as follows:


* `max_binlog_stmt_cache_size` must be divisible by 4096.

* `query_alloc_block_size` and `range_alloc_block_size` must be divisible by 1024.

* `join_buffer_size` must be divisible by 128.


<span id="4z9GaBVw"></span>
### Are the modified parameters effective globally? Is it possible to modify the parameters of only a certain node?

Parameter modifications to NDB for MySQL are globally effective and apply to all nodes. Modifying parameters for a specific node is currently not supported.

<span id="J3ssNe9c"></span>
### After modifying parameters that require an instance restart, how long does it take to restart?

Under normal circumstances, the restart time for each compute node is approximately 5 minutes. For example, if the instance contains two compute nodes, it takes about 10 minutes to restart the entire instance.

<span id="ijuZYpKk"></span>
### Do modified parameters take effect immediately? Can it take effect at a specified time?

When modifying parameters, you can select execution mode. You can choose to **Execute now** or **Execute during maintainable window**. For details about the maintenance window, see [Configuring maintenance window](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Configuring_maintenance_window).

<span id="RAgkq0gk"></span>
### How do I cancel a pending parameter modification task?

You can cancel a pending parameter modification event in the scheduled event list on the console. For details, see [Cancelling the scheduled events](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Cancelling_the_scheduled_events).
