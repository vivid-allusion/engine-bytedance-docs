---
title: "Thread pool"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Thread_pool"
---

This topic describes the thread pool feature provided by RDS for MySQL.

<span id=".5Yqf6IO95LuL57uN"></span>
## Function introduction

RDS for MySQL uses a one\-thread\-per\-connection model, where the server assigns a dedicated thread to serve each connection. When there are too many concurrent database connections, the performance of the MySQL server drops sharply. To address this issue, RDS for MySQL provides the Thread Pool feature, which uses a specified number of server threads to handle a large number of connections and ensure service stability.

<span id=".5pSv5oyB54mI5pys"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.32_20230615 and above.

* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.32_20230615 and above.

* MySQL 8.4 version, and the kernel minor version is MySQL 8.4.7_20260415 and above.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can view the kernel minor version of an instance by <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details">Viewing instance information</a>. If the kernel minor version of your instance is not within the supported kernel minor version range, you can <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version">Manually upgrading the instance kernel minor version</a>.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limitation

Instances in the RDS for MySQL 8.0.26 version series do not currently support this feature.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

<span id=".57q_56iL5rGg55u45YWz5Y-v5L-u5pS55Y-C5pWw"></span>
### Modifiable thread pool parameters

You can adjust the thread pool by modifying the following modifiable parameters.


|Parameter name |Description |
|---|---|
|loose_thread_pool_enabled |Whether the thread pool is enabled. RDS for MySQL is ON (enabled) by default.<br><br><br>* MySQL 5.7:<br><br>   * For **MySQL 5.7.44_20260415 and later** instances: When the value of the `loose_thread_handling_switch_mode` parameter is `handling_switch_new` or `handling_switch_all`, modifying this parameter does not require an instance restart; otherwise, an instance restart is required.<br><br>   * For instances with kernel versions **earlier than MySQL 5.7.44_20260415**, modifying this parameter requires an instance restart.<br><br>* MySQL 8.0:<br><br>   * For **MySQL 8.0.32_20260415 and later** instances: When the value of the `loose_thread_handling_switch_mode` parameter is `handling_switch_new` or `handling_switch_all`, modifying this parameter does not require an instance restart; otherwise, an instance restart is required.<br><br>   * For instances with kernel versions earlier than **MySQL 8.0.32_20260415**, modifying this parameter requires an instance restart.<br><br>* MySQL 8.4: Modifying this parameter requires an instance restart. |
|loose_thread_pool_size |The number of thread groups. RDS for MySQL sets a reasonable value based on the instance rules, and this parameter can be modified without restarting the instance. |
|loose_thread_pool_oversubscribe |The maximum number of threads allowed in each thread group. The Default value is 16. Modifying this Parameter does not require restarting the instance. |
|loose_thread_handling_switch_mode<br><br> |Thread pool dynamic enable and disable feature. Values are as follows:<br><br><br>* `handling_switch_off`: Disables the thread pool dynamic start and stop feature.<br><br>* `handling_switch_new`: Only new connections adopt the new connection‑handling mode, while existing connections remain unchanged.<br><br>* `handling_switch_all`: Both new and existing connections are migrated to the new connection‑handling mode.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is only supported on <strong>MySQL 5.7.44_20260415 and later</strong> and <strong>MySQL 8.0.32_20260415 and later</strong> instances.</div><br> |


<span id=".57q_56iL5rGg54q25oCB5p-l6K-i"></span>
### Querying thread pool state

You can use the following command to query the thread pool state.

```sql
mysql> show status like 'Threadpool%';
+---------------------------------------+-------+
| Variable_name                         | Value |
+---------------------------------------+-------+
| Threadpool_active_threads             | 1     |
| Threadpool_all_threads                | 3     |
| Threadpool_dump_threads               | 0     |
| Threadpool_extra_connection_count     | 4     |
| Threadpool_high_prio_queue_len        | 0     |
| Threadpool_listener_threads           | 1     |
| Threadpool_low_prio_queue_len         | 0     |
| Threadpool_sleep_threads              | 1     |
| Threadpool_stalled_groups_last_period | 0     |
| Threadpool_wait_threads               | 0     |
+---------------------------------------+-------+
10 rows in set (0.00 sec)
```


Thread pool state variables:


|Parameter name |Description |
|---|---|
|Threadpool_active_threads |Number of active threads in the thread pool |
|Threadpool_all_threads |Total number of threads in the thread pool |
|Threadpool_dump_threads |Quantity of Binlog_dump threads |
|Threadpool_extra_connection_count |Quantity of connections that log on through the management port |
|Threadpool_high_prio_queue_len |Thread pool high\-priority queue length |
|Threadpool_listener_threads |Listener thread quantity |
|Threadpool_low_prio_queue_len |Thread pool low priority queue length |
|Threadpool_sleep_threads |Sleeping thread quantity |
|Threadpool_stalled_groups_last_period |Whether a stall occurred in the previous monitoring cycle |
|Threadpool_wait_threads |Number of blocked threads in the thread pool |
