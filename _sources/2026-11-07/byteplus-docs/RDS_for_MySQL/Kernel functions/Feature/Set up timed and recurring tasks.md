---
title: "Set up timed and recurring tasks"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Set_up_timed_and_recurring_tasks"
---

This topic describes two methods to set up timed and recurring tasks: using MySQL's Event Scheduler and using Database Workshop (DBW).

<span id=".6IOM5pmv5L-h5oGv"></span>
## Creating scheduled and periodic tasks using MySQL's Event Scheduler

<span id="04RUEvrg"></span>
### Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.44_20260215 and above.

* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.43_20260215 and above.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">If the MySQL version does not meet the requirements, using the Event Scheduler is not recommended. In older versions, after a switchover between primary and secondary nodes, the event statuses can become unsynchronized, causing event scheduling to fail.</div>


* <div data-tips="true" data-tips-type="default">If you created an event on an unsupported MySQL version and later upgraded to a supported version, we recommend deleting and recreating all previous timed tasks. Otherwise, these tasks will still fail to schedule after a switchover between primary and secondary nodes.</div>


* <div data-tips="true" data-tips-type="default">You can view the kernel minor version of an instance by <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details">Viewing instance information</a>. If the kernel minor version of your instance is not within the supported kernel minor version range, you can <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version">Manually upgrading the instance kernel minor version</a>.</div>



<span id="dvrWCBhU"></span>
### Instructions

<span id="VK4AwuOW"></span>
#### Setting parameters

Before using Event Scheduler, set the `event_scheduler` and `loose_event_replica_consistent` parameters to `ON` first.

<span id="EagjlvBo"></span>
#### Creating a scheduled task

The syntax for creating a scheduled task is as follows:

```SQL
CREATE EVENT [IF NOT EXISTS] event_name
ON SCHEDULE schedule
[ENABLE | DISABLE]
DO
  sql_statement;
```


Where `event_name` is the task name, `sql_statement` is the SQL statement for the task, and `schedule` is the execution cycle. For specific usage, refer to the following examples:


* Example 1: A one\-time task (automatically inserts a record into the log table after 1 hour).


```SQL
CREATE EVENT insert_log_once
ON SCHEDULE AT CURRENT_TIMESTAMP + INTERVAL 1 HOUR
DO
  INSERT INTO my_log (message, created_at) VALUES ('任务已自动执行', NOW());
```



* Example 2: A recurring task (automatically cleans up expired order data older than 30 days once a day).


```SQL
CREATE EVENT purge_old_orders
ON SCHEDULE EVERY 1 DAY
DO
  DELETE FROM orders WHERE create_time < DATE_SUB(NOW(), INTERVAL 30 DAY);
```



* Example 3: A recurring task with a validity period (aggregates data every 1 hour from the beginning to the end of the month).


```SQL
CREATE EVENT hourly_report
ON SCHEDULE EVERY 1 HOUR
  STARTS '2024-01-01 00:00:00'
  ENDS '2024-01-31 23:59:59'
  DO
    CALL generate_hourly_report();
```


<span id="U5BYyijm"></span>
#### Viewing scheduled task information

Execute the following statement to view all scheduled tasks:

```SQL
SHOW EVENTS;
```


<span id="76IpSMLv"></span>
#### Deleting a scheduled task

The syntax for deleting a scheduled task is as follows:

```SQL
DROP EVENT [IF EXISTS] event_name
```


Replace `event_name` with the name of the task to be deleted.

<span id=".5L2_55SoLWRidy3kuLotbXlzcWwt5Yib5bu65a6a5pe25Lu75Yqh5ZKM5ZGo5pyf5oCn5Lu75Yqh"></span>
## Creating scheduled and periodic tasks for MySQL using DBW

In Database Workshop (DBW), you can create scheduled or periodic tasks for RDS for MySQL. For details on creating scheduled or periodic tasks, refer to [Task management](https://docs.byteplus.com/en/docs/DBW/task-management-for-mysql).

<span id="IhZtSXhE"></span>
## Precautions

Both MySQL's native Event Scheduler and Database Workshop (DBW) can create and manage timed and recurring tasks. The timed and recurring tasks created through these two methods are independent and execute separately. We recommend using only one method. Before doing so, first clear any scheduled and recurring tasks created by the other method.
