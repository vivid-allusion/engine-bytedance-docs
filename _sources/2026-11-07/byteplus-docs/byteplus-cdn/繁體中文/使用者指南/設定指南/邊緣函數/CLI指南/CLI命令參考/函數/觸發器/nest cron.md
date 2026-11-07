---
title: "nest cron"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-cron-cn-zh-tw"
---

管理本地函數所關聯的 Cron 觸發器。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">本指令需要您設定您的 BytePlus 帳號的 Access Key ID 和 Secret Access Key。參見 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn-zh-tw">設定您的 Access Key ID 和 Secret Access Key</a></div>


* <div data-tips="true" data-tips-type="tip">本指令需要在一個函數專案的根目錄下執行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn-zh-tw">nest init</a> 建立一個函數專案</div>


* <div data-tips="true" data-tips-type="tip">本地函數所關聯的 Cron 觸發器資訊不保存在本地。邊緣函數 CLI 在邊緣函數服務端管理本地函數關聯的 Cron 觸發器。因此，在執行本指令時，請確保您的本地函數需要有一個函數 ID</div>



<span id="描述"></span>
## 描述

您可以建立 Cron 觸發器來建立定期任務，Cron 觸發器會在指定時間自動觸發函數程式碼中的 cron 事件。您需要在程式碼中監聽並處理 cron 事件

<span id="子指令"></span>
## 子指令

<span id="list"></span>
### list

```shell
npx nest cron list --function <function_id_or_name> --page <page_number> --desc --output <output>
```


查看本地函數關聯的 Cron 觸發器清單


* `<function_id_or_name>`：*string，optional*

   * 函數 ID 或函數名稱。該參數是一個全域參數。參見 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn-zh-tw)。預設為 [本地函數清單](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#list) 中的預設函數。如果您透過函數名稱指定的本地函數還沒有函數 ID，邊緣函數 CLI 會返回錯誤 `Error: function id required`

* `<page_number>`：*integer，optional*

   * 清單分頁顯示的頁碼。預設為 1

* `--desc`：*boolean，optional*

   * 按 Cron 觸發器名稱降冪排序。預設為按 Cron 觸發器名稱升冪排序

* `<output>`：*string，optional*

   * 清單格式：

      * `table`（預設）：表格

      * `json`：JSON 格式

      * `yaml`：yaml 格式


<span id="tasks"></span>
### tasks

```shell
npx nest cron tasks <cron_job_name>  --function <function_id_or_name> --page <page_number> --desc --output <output>
```


查看指定的 Cron 觸發器的任務執行記錄


* `<cron_job_name>`：*string，required*

   * Cron 觸發器的名稱

* `<function_id_or_name>`：*string，optional*

   * 函數 ID 或函數名稱。該參數是一個全域參數。參見 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn-zh-tw)。預設為 [本地函數清單](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#list) 中的預設函數。如果您透過函數名稱指定的本地函數還沒有函數 ID，邊緣函數 CLI 會返回錯誤 `Error: function id required`

* `<page_number>`：*integer，optional*

   * 清單分頁顯示時的頁碼。預設為 1

* `--desc`：*boolean，optional*

   * 按任務 ID 觸發器名稱降冪排序。預設為按任務 ID 升冪排序


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


建立一個 Cron 觸發器


* `<cron_job_name>`：*string，required*

   * Cron 觸發器的名稱：

      * 在一個函數中，觸發器的名稱必須唯一

      * 長度不超過 128 個字元

* `<cron_expression>`：*string，required*

   * Cron 表達式。參見 [支援的 Cron 表達式](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-cron-triggers-cn-zh-tw#%E6%94%AF%E6%8F%B4%E7%9A%84-cron-%E8%A1%A8%E9%81%94%E5%BC%8F)

* `<description>`：*string，optional*

   * Cron 觸發器的描述

* `<function_id_or_name>`：*string，optional*

   * 函數 ID 或函數名稱。該參數是一個全域參數。參見 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。預設為 [本地函數清單](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#list) 中的預設函數。如果您透過函數名稱指定的本地函數還沒有函數 ID，邊緣函數 CLI 會返回錯誤 `Error: function id required`

* `<parameter>`：*string，optional*

   * 自訂參數。在函數執行時，邊緣函數把該參數傳遞給 [CronEvent](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-CronEvent-cn-zh-tw)

* `--single`：*boolean，optional*

   * cron 事件在隨機的一個邊緣節點觸發。預設為 cron 事件在所有邊緣節點被觸發


例如，您透過下面的指令建立一個名稱為 cronjob1 的 Cron 觸發器。Cron 表達式表示每五分鐘執行一次

```shell
npx nest cron create cronjob1 -e " */5 * * * *"
```


您可以透過 npx cron list 查看您建立的 Cron 觸發器

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


更新指定的 Cron 觸發器的設定


* `<cron_job_name>`：*string，required*

   * Cron 觸發器的名稱。在一個函數中，觸發器的名稱必須唯一

* `<cron_expression>`：*string，required*

   * Cron 表達式。參見 [支援的 Cron 表達式](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-cron-triggers-cn-zh-tw#%E6%94%AF%E6%8F%B4%E7%9A%84-cron-%E8%A1%A8%E9%81%94%E5%BC%8F)

* `<description>`：*string，optional*

   * Cron 觸發器的描述

* `<function_id_or_name>`：*string，optional*

   * 函數 ID 或函數名稱。該參數是一個全域參數。參見 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn-zh-tw)。預設為 [本地函數清單](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#list) 中的預設函數。如果您透過函數名稱指定的本地函數還沒有函數 ID，邊緣函數 CLI 會返回錯誤 `Error: function id required`

* `<parameter>`：*string，optional*

   * 自訂參數。在函數執行時，邊緣函數把該參數傳遞給 [CronEvent](https://docs.byteplus.com/docs/byteplus-cdn/docs/byteplus-cdn/docs_cn-CronEvent-cn-zh-tw)

* `--single`：*boolean，optional*

   * cron 事件在隨機的一個邊緣節點觸發。預設為 cron 事件在所有邊緣節點被觸發
