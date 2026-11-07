---
title: "nest cron"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-cron-en"
---

Manages Cron triggers associated with local functions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This command requires you to set up your BytePlus account's access key ID and secret access key. See <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-en">Set Your Access Key ID and Secret Access Key</a>.</div>


* <div data-tips="true" data-tips-type="tip">This command needs to be run in the root directory of a function project. You need to use <code>nest init</code> to create a function project.</div>


* <div data-tips="true" data-tips-type="tip">Cron trigger information associated with local functions is not saved locally. The Edge Functions CLI manages the Cron triggers associated with local functions on the Edge Functions server. Therefore, ensure that your local function has a function ID when running this command.</div>



<span id="description"></span>
## Description

You can create Cron triggers to set up periodic tasks. Cron triggers will automatically trigger the cron event in the function code at specified times. You need to listen for and handle the cron event in your code.

<span id="subcommands"></span>
## Subcommands

<span id="list"></span>
### list

```shell
npx nest cron list --function <function_id_or_name> --page <page_number> --desc --output <output>
```


View the list of Cron triggers associated with the local function.


* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.

* `<page_number>`: *integer, optional*

   * Page number for paginated display. Default is 1.

* `--desc`: *boolean, optional*:

   * Sort Cron triggers by name in descending order. Default is ascending order.

* `<output>`: *string, optional*:

   * List format.

      * `table` (default): Table format.

      * `json`: JSON format.

      * `yaml`: YAML format.


<span id="tasks"></span>
### tasks

```shell
npx nest cron tasks <cron_job_name>  --function <function_id_or_name> --page <page_number> --desc --output <output>
```


View the task execution records of a specified Cron trigger.


* `<cron_job_name>`: *string, required*

   * Name of the Cron trigger.

      * Within a function, the trigger name must be unique.

      * The length must not exceed 128 characters.

* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.

* `<page_number>`: *integer, optional*

   * Page number for paginated display. Default is 1.

* `--desc`: *boolean, optional*:

   * Sort by task ID in descending order. Default is ascending order.


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


Create a Cron trigger.


* `<cron_job_name>`: *string, required*

   * Name of the Cron trigger.

* `<cron_expression>`: *string, required*

   * Cron expression. See [Supported Cron Expressions](https://docs.byteplus.com/docs/byteplus-cdn/docs-cron-triggers#supportedcron).

* `<description>`: *string, optional*

   * Description of the Cron trigger.

* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.

* `<parameter>`: *string, optional*

   * Custom parameter. Edge Functions passes this parameter to [CronEvent](https://docs.byteplus.com/docs/byteplus-cdn/docs/byteplus-cdn/docs_cn-CronEvent-en) when the function executes.

* `--single`: *boolean, optional*

   * The cron event is triggered on a random edge node. By default, the cron event is triggered on all edge nodes.


For example, you can create a Cron trigger named cronjob1 with the following command. The Cron expression indicates execution every five minutes.

```shell
npx nest cron create cronjob1 -e " */5 * * * *"
```


You can view the Cron trigger you created using npx cron list.

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


Update the configuration of a specified Cron trigger.


* `<cron_job_name>`: *string, required*

   * Name of the Cron trigger.

* `<cron_expression>`: *string, required*

   * Cron expression. See [Supported Cron Expressions](https://docs.byteplus.com/docs/byteplus-cdn/docs-cron-triggers#supported-cron-expressions).

* `<description>`: *string, optional*

   * Description of the Cron trigger.

* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.

* `<parameter>`: *string, optional*

   * Custom parameter. Edge Functions passes this parameter to [CronEvent](https://docs.byteplus.com/docs/byteplus-cdn/docs/byteplus-cdn/docs-CronEvent) when the function executes.

* `--single`: *boolean, optional*

   * The cron event is triggered on a random edge node. By default, the cron event is triggered on all edge nodes.


<span id="delete"></span>
### delete

```shell
npx nest cron delete <cron_job_name> --function <function_id_or_name>
```


Delete a specified Cron trigger.


* `<cron_job_name>`: *string, required*

   * Name of the Cron trigger.

* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.


<span id="start"></span>
### start

```shell
npx nest cron start <cron_job_name> --function <function_id_or_name>
```


Enable a specified Cron trigger.


* `<cron_job_name>`: *string, required*

   * Name of the Cron trigger.

* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.


After enabling, you can check the status of the Cron trigger using npx cron list.

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


Disable a specified Cron trigger.


* `<cron_job_name>`: *string, required*

   * Name of the Cron trigger.

* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.


After disabling, you can check the status of the Cron trigger using npx cron list.

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


View the task logs of a Cron trigger.


* `<cron_job_name>`: *string, required*

   * Name of the Cron trigger.

* `<task_id>`: *string, required*

   * Task ID. You can get the task ID (TASKID) of a Cron trigger using the `npx nest cron tasks` command.

* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.


```shell
$ npx nest cron logs cronjob1 1374895809465100791
+---------------------+--------+---------------+
|     CREATETIME      | STATUS |   RESPONSE    |
+---------------------+--------+---------------+
| 2025-01-08 15:10:00 | failed | cron resp err |
+---------------------+--------+---------------+
```
