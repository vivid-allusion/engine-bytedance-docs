---
title: "Task scheduler expanding (pg_cron)"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pg_cron"
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

## Extension usage

### Create extension

Use a super account to create the extension by executing the following command in the postgres database.

```sql
create extension pg_cron;
```

### Delete extension

Execute the following command to delete the extension.

```sql
drop extension pg_cron CASCADE;
```

### Extension usage

#### Creating a scheduled task

pg_cron provides two functions, `cron.schedule()` and `cron.schedule_in_database()`, to create scheduled tasks.

* `cron.schedule()`

   The usage syntax of the `cron.schedule()` function is as follows:

   ```sql
   cron.schedule ('<计划>', '<任务>');
   cron.schedule ('<名称>', '<计划>', '<任务>');
   ```

   Usage example:

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2e9dc6ccc44a36ccd1b88ca269b5fd9c.png)

* `cron.schedule_in_database()` function

   The usage syntax of the `cron.schedule_in_database()` function is as follows:

   ```sql
   cron.schedule_in_database ('<名称>', '<计划>', '<任务>', '<数据库>', '<用户>', '<是否生效>');
   ```

   Usage example:

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_11cb2418ddcd50427e3cd4491d4c75d2.png)

   > **tip**

   * > The `cron.schedule_in_database()` function cannot specify the User. In `cron.schedule_in_database ('<Name>', '<Schedule>', '<Task>', '<Database>', '<User>', '<Is enabled>')`, the `'<User>'` can only be filled with `NULL`.

   * > AI Native Database Platform does not provide PostgreSQL "super user" accounts for users. Do not try to use a PostgreSQL "super user" account to use this extension, otherwise an error is reported.

#### View scheduled tasks

You can view configured scheduled tasks in the cron.job table.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dfb51e0b739c3915fd18352980a934ff.png)

And view the task status and execution status in the cron.job_run_details table.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f67685a51fbc9600f2e4eeea68b87289.png)

#### Modify scheduled tasks

The syntax for modifying a scheduled task is as follows:

```sql
cron.alter_job ('<任务id>', '<计划>', '<任务>', '<数据库>', '<用户>', '<是否生效>');
```

Examples:

> **tip**

> `cron.alter_job()` function cannot specify a user. `cron.alter_job ('<Task ID>', '<schedule>', '<task>', '<Database>', '<User>', '<enabled>')` requires `'<User>'` to be filled with `NULL` only.

#### Cancel a scheduled task

The syntax for canceling a scheduled task is as follows:

```sql
cron.unschedule ('<任务id>');
cron.unschedule ('<名称>');
```

Examples:

#### ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a6d3602c6e11bdfed411f912b055213a.png)

#### Authorizing a general user to use the extension

The syntax for authorizing a general user to use the extension is as follows:

```sql
grant USAGE on SCHEMA cron to other-user;
```

Examples:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2263498376effa8098b053612fe4ef5a.png)

> **tip**

> Ordinary users cannot execute `cron.schedule_in_database()` and `cron.alter_job()` functions.

## Related parameters

You need to use the following two parameters while using the pg_cron extension:

* `shared_preload_libraries`: before creating the pg_cron extension, modify this parameter to add the `pg_cron` value.

* `cron.log_run`: enables or disables logging all running tasks to the cron.job_run_details table, which is enabled by default. This parameter accepts `on` and `off` values, with the default value of `on`.
