---
title: "nest cron"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-cron-cn"
---

管理本地函数所关联的 Cron 触发器。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">本命令需要您设置您的 BytePlus 账号的 Access Key ID 和 Secret Access Key。参见 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn">设置您的 Access Key ID 和 Secret Access Key</a>。</div>


* <div data-tips="true" data-tips-type="tip">本命令需要在一个函数项目的根目录下运行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn">nest init</a> 创建一个函数项目。</div>


* <div data-tips="true" data-tips-type="tip">本地函数所关联的 Cron 触发器信息不保存在本地。边缘函数 CLI 在边缘函数服务端管理本地函数关联的 Cron 触发器。因此，在运行本命令时，确保您的本地函数需要有一个函数 ID。</div>



<span id="描述"></span>
## 描述

您可以创建 Cron 触发器来创建定期任务，Cron 触发器会在指定时间自动触发函数代码中的 cron 事件。您需要在代码中监听并处理 cron 事件。

<span id="子命令"></span>
## 子命令

<span id="list"></span>
### list

```shell
npx nest cron list --function <function_id_or_name> --page <page_number> --desc --output <output>
```


查看本地函数关联的 Cron 触发器的列表。


* `<function_id_or_name>`：*string，optional*

   * 函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。如果您通过函数名称指定的本地函数还没有函数 ID，边缘函数 CLI 会返回错误 `Error: function id required`。

* `<page_number>`：*integer，optional*

   * 列表分页显示的页码。默认为 1。

* `--desc`：*boolean，optional*：

   * 按 Cron 触发器名称降序排序。默认为按 Cron 触发器名称升序排序。

* `<output>`：*string，optional*：

   * 列表格式。

      * `table`（默认）：表格。

      * `json`：JSON 格式。

      * `yaml`：yaml 格式。


<span id="tasks"></span>
### tasks

```shell
npx nest cron tasks <cron_job_name>  --function <function_id_or_name> --page <page_number> --desc --output <output>
```


查看指定的 Cron 触发器的任务执行记录。


* `<cron_job_name>`：*string，required*

   * Cron 触发器的名称。

* `<function_id_or_name>`：*string，optional*

   * 函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。如果您通过函数名称指定的本地函数还没有函数 ID，边缘函数 CLI 会返回错误 `Error: function id required`。

* `<page_number>`：*integer，optional*

   * 列表分页显示时的页码。默认为 1。

* `--desc`：*boolean，optional*：

   * 按任务 ID 触发器名称降序排序。默认为按任务 ID 升序排序。


```shell
$ npx nest cron tasks cronjob1
+----------------------+--------------+--------+-----------+---------------------+
|        TASKID        |  EXPRESSION  | STATUS | PARAMETER |     CREATETIME      |
+----------------------+--------------+--------+-----------+---------------------+
|   179853752656576418 |  */5 * * * * | FAILED |           | 2025-01-08 14:55:00 |
|  3281844070291308207 |  */5 * * * * | FAILED |           | 2025-01-08 15:00:00 |
|   562818166848625350 |  */5 * * * * | FAILED |           | 2025-01-08 15:05:00 |
|  1374895809465100791 |  */5 * * * * | FAILED |           | 2025-01-08 15:10:00 |
| 23615883122759736315 |  */5 * * * * | FAILED |           | 2025-01-08 15:15:00 |
+----------------------+--------------+--------+-----------+---------------------+
```


<span id="create"></span>
### create

```shell
npx nest cron create <cron_job_name> -e <cron_expression> --description <description> --function <function_id_or_name> --param <parameter> --single
```


创建一个 Cron 触发器。


* `<cron_job_name>`：*string，required*

   * Cron 触发器的名称。

      * 在一个函数中，触发器的名称必须唯一。

      * 长度不超过 128 个字符。

* `<cron_expression>`：*string，required*

   * Cron 表达式。参见 [支持的 Cron 表达式](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-cron-triggers-cn#%E5%90%AF%E5%8A%A8%E6%88%96%E5%81%9C%E7%94%A8-cron-%E8%A7%A6%E5%8F%91%E5%99%A8)。

* `<description>`：*string，optional*

   * Cron 触发器的描述。

* `<function_id_or_name>`：*string，optional*

   * 函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。如果您通过函数名称指定的本地函数还没有函数 ID，边缘函数 CLI 会返回错误 `Error: function id required`。

* `<parameter>`：*string，optional*

   * 自定义参数。在函数执行时，边缘函数把该参数传递给 [CronEvent](https://docs.byteplus.com/docs/byteplus-cdn/docs/byteplus-cdn/docs_cn-CronEvent-cn)。

* `--single`：*boolean，optional*

   * cron 事件在随机的一个边缘节点触发。默认为 cron 事件在所有边缘节点被触发。


例如，您通过下面的命令创建一个名称为 cronjob1 的 Cron 触发器。Cron 表达式表示每五分钟执行一次。

```shell
npx nest cron create cronjob1 -e " */5 * * * *"
```


您可以通过 npx cron list 查看您创建的 Cron 触发器。

```shell
$ npx nest cron list
+----------+--------------+-----------+--------+-----------+-------------+---------------------+
|   NAME   |  EXPRESSION  |  STATUS   |  TYPE  | PARAMETER | DESCRIPTION |     UPDATETIME      |
+----------+--------------+-----------+--------+-----------+-------------+---------------------+
| cronjob1 |  */5 * * * * | UNKNOWN   | GLOBAL |           |             | 2025-01-08 14:52:55 |
+----------+--------------+-----------+--------+-----------+-------------+---------------------+
```


<span id="update"></span>
### update

```shell
npx nest cron update <cron_job_name> -e <cron_expression> --function <function_id_or_name> --param <parameter> --single
```


更新指定的 Cron 触发器的配置。


* `<cron_job_name>`：*string，required*

   * Cron 触发器的名称。在一个函数中，触发器的名称必须唯一。

* `<cron_expression>`：*string，required*

   * Cron 表达式。参见 [支持的 Cron 表达式](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-cron-triggers-cn#supportedcron)。

* `<description>`：*string，optional*

   * Cron 触发器的描述。

* `<function_id_or_name>`：*string，optional*

   * 函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。如果您通过函数名称指定的本地函数还没有函数 ID，边缘函数 CLI 会返回错误 `Error: function id required`。

* `<parameter>`：*string，optional*

   * 自定义参数。在函数执行时，边缘函数把该参数传递给 [CronEvent](https://docs.byteplus.com/docs/byteplus-cdn/docs/byteplus-cdn/docs_cn-CronEvent-cn)。

* `--single`：*boolean，optional*

   * cron 事件在随机的一个边缘节点触发。默认为 cron 事件在所有边缘节点被触发。


<span id="delete"></span>
### delete

```shell
npx nest cron delete <cron_job_name> --function <function_id_or_name>
```


删除指定的 Cron 触发器。


* `<cron_job_name>`：*string，required*

   * Cron 触发器的名称。

* `<function_id_or_name>`：*string，optional*

   * 函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。如果您通过函数名称指定的本地函数还没有函数 ID，边缘函数 CLI 会返回错误 `Error: function id required`。


<span id="start"></span>
### start

```shell
npx nest cron start <cron_job_name> --function <function_id_or_name>
```


启用指定的 Cron 触发器。


* `<cron_job_name>`：*string，required*

   * Cron 触发器的名称。

* `<function_id_or_name>`：*string，optional*

   * 函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。如果您通过函数名称指定的本地函数还没有函数 ID，边缘函数 CLI 会返回错误 `Error: function id required`。


启用后，您可以通过 npx cron list 查看 Cron 触发器的状态。

```shell
$ npx nest cron list
+----------+--------------+-----------+--------+-----------+-------------+---------------------+
|   NAME   |  EXPRESSION  |  STATUS   |  TYPE  | PARAMETER | DESCRIPTION |     UPDATETIME      |
+----------+--------------+-----------+--------+-----------+-------------+---------------------+
| cronjob1 |  */5 * * * * | SCHEDULED | GLOBAL |           |             | 2025-01-08 14:52:55 |
+----------+--------------+-----------+--------+-----------+-------------+---------------------+
```


<span id="stop"></span>
### stop

```shell
npx nest cron stop <cron_job_name> --function <function_id_or_name>
```


停用指定的 Cron 触发器。


* `<cron_job_name>`：*string，required*

   * Cron 触发器的名称。

* `<function_id_or_name>`：*string，optional*

   * 函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。如果您通过函数名称指定的本地函数还没有函数 ID，边缘函数 CLI 会返回错误 `Error: function id required`。


停用后，您可以通过 npx cron list 查看 Cron 触发器的状态。

```shell
$ npx nest cron list
+----------+--------------+----------+--------+-----------+-------------+---------------------+
|   NAME   |  EXPRESSION  |  STATUS  |  TYPE  | PARAMETER | DESCRIPTION |     UPDATETIME      |
+----------+--------------+----------+--------+-----------+-------------+---------------------+
| cronjob1 |  */5 * * * * | DISABLED | GLOBAL |           |             | 2025-01-08 15:16:18 |
+----------+--------------+----------+--------+-----------+-------------+---------------------+
```


<span id="logs"></span>
### logs

```shell
npx nest cron logs <cron_job_name> <task_id> --function <function_id_or_name>
```


查看 Cron 触发器的任务日志。


* `<cron_job_name>`：*string，required*

   * Cron 触发器的名称。

* `<task_id>`：*string，required*

   * 任务 ID。您可以通过 `npx nest cron tasks` 命令获取 Cron 触发器的任务 ID（TASKID）。

* `<function_id_or_name>`：*string，optional*

   * 函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。如果您通过函数名称指定的本地函数还没有函数 ID，边缘函数 CLI 会返回错误 `Error: function id required`。


```shell
$ npx nest cron logs cronjob1 1374895809465100791
+---------------------+--------+---------------+
|     CREATETIME      | STATUS |   RESPONSE    |
+---------------------+--------+---------------+
| 2025-01-08 15:10:00 | failed | cron resp err |
+---------------------+--------+---------------+
```
