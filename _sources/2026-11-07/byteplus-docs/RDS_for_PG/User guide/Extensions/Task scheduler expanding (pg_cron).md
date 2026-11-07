---
title: "Task scheduler expanding (pg_cron)"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/task_scheduler_expanding-pg_cron"
---

pg_cron is a cron\-based PostgreSQL task scheduler extension. Its syntax is the same as cron and can execute PostgreSQL commands directly from the database.

Time\-based scheduling adopts the standard cron syntax, where \* means running at any time, and specific numbers mean running only at those times.

```sql
┌───────────── 分钟：0~59
│ ┌────────────── 小时：0~23
│ │ ┌─────────────── 日期：1~31
│ │ │ ┌──────────────── 月份：1~12
│ │ │ │ ┌───────────────── 一周中的某一天：0~6，0 表示周日。
│ │ │ │ │                  
│ │ │ │ │
│ │ │ │ │
* * * * *
```


<span id=".5o-S5Lu255qE5L2_55So"></span>
## Extension usage

<span id=".5Yib5bu65o-S5Lu2"></span>
### Create extension


1. Modify parameter `shared_preload_libraries` to add the value `pg_cron`. For detailed information on modifying parameters, please refer to [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_parameters).

2. Use a super account to create the extension by executing the following command in the postgres database.


```sql
create extension pg_cron;
```


<span id=".5Yig6Zmk5o-S5Lu2"></span>
### Delete extension

Execute the following command to delete the extension.

```sql
drop extension pg_cron CASCADE;
```


<span id=".5L2_55So5o-S5Lu2"></span>
### Extension usage

<span id=".5Yib5bu65a6a5pe25Lu75Yqh"></span>
#### Creating a scheduled task

pg_cron provides two functions, `cron.schedule()` and `cron.schedule_in_database()`, to create scheduled tasks.


* `cron.schedule()`

   The usage syntax of the `cron.schedule()` function is as follows:

   ```sql
   cron.schedule ('<计划>', '<任务>');
   cron.schedule ('<名称>', '<计划>', '<任务>');
   ```
   

   Usage example:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_843aac154929dbd6f7a86a43ef50337d.png) </span>

* `cron.schedule_in_database()` function

   The usage syntax of the `cron.schedule_in_database()` function is as follows:

   ```sql
   cron.schedule_in_database ('<名称>', '<计划>', '<任务>', '<数据库>', '<用户>', '<是否生效>');
   ```
   

   Usage example:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1e9f651c94f5af8b97ecdedf59b984b6.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <code>cron.schedule_in_database()</code> function cannot specify the User. In <code>cron.schedule_in_database ('<Name>', '<Schedule>', '<Task>', '<Database>', '<User>', '<Is enabled>')</code>, the <code>'<User>'</code> can only be filled with <code>NULL</code>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">RDS for PostgreSQL does not open "super user" accounts to users. Do not try to use a PostgreSQL "super user" account to use this extension, otherwise an error is reported.   </div>
   


<span id=".5p-l55yL5a6a5pe25Lu75Yqh"></span>
#### View scheduled tasks

You can view configured scheduled tasks in the cron.job table.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d38d7209c7a8a7ad16d9fbbc51e35be6.png) </span>

And view the task status and execution status in the cron.job_run_details table.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_08722d93dd52e310dca546b077994bef.png) </span>

<span id=".5L-u5pS55a6a5pe25Lu75Yqh"></span>
#### Modify scheduled tasks

The syntax for modifying a scheduled task is as follows:

```sql
cron.alter_job ('<任务id>', '<计划>', '<任务>', '<数据库>', '<用户>', '<是否生效>');
```


Examples:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9ad5aca22eab610fd5a95c0303d6e39f.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>cron.alter_job()</code> function cannot specify a user. <code>cron.alter_job ('<Task ID>', '<schedule>', '<task>', '<Database>', '<User>', '<enabled>')</code> requires <code>'<User>'</code> to be filled with <code>NULL</code> only.</div>


<span id=".5Y-W5raI5a6a5pe25Lu75Yqh"></span>
#### Cancel a scheduled task

The syntax for canceling a scheduled task is as follows:

```sql
cron.unschedule ('<任务id>');
cron.unschedule ('<名称>');
```


Examples:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_96f92a5e73d86811c43efc2adf5b02e9.png) </span>

<span id=".5o6I5p2D5pmu6YCa55So5oi35L2_55So5o-S5Lu2"></span>
#### Authorizing a general user to use the extension

The syntax for authorizing a general user to use the extension is as follows:

```sql
grant USAGE on SCHEMA cron to other-user;
```


Examples:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_acf8d73438b107180ff90e7a64eaa631.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Ordinary users cannot execute <code>cron.schedule_in_database()</code> and <code>cron.alter_job()</code> functions.</div>


<span id=".55u45YWz5Y-C5pWw"></span>
## Related parameters

You need to use the following two parameters while using the pg_cron extension:


* `shared_preload_libraries`: before creating the pg_cron extension, modify this parameter to add the `pg_cron` value.

* `cron.log_run`: enables or disables logging all running tasks to the cron.job_run_details table, which is enabled by default. This parameter accepts `on` and `off` values, with the default value of `on`.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For more information about how to modify parameters, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_parameters">Modifying parameters</a>.</div>


* <div data-tips="true" data-tips-type="tip">After modifying <code>shared_preload_libraries</code> and <code>cron.log_run</code> parameters, restart the instance to apply the changes.</div>
