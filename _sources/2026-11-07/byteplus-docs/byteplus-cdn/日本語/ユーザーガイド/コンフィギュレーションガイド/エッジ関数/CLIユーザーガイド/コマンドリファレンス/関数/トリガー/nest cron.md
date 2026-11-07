---
title: "nest cron"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-cron-jp"
---

ローカル関数に関連付けられたCronトリガーを管理します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">このコマンドを使用するには、BytePlusアカウントのAccess Key IDとSecret Access Keyを設定する必要があります。<a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-jp">Access Key IDとSecret Access Keyを設定する</a>を参照してください。</div>


* <div data-tips="true" data-tips-type="tip">このコマンドは関数プロジェクトのルートディレクトリで実行する必要があります。<code>nest init</code>を使用して関数プロジェクトを作成する必要があります。</div>


* <div data-tips="true" data-tips-type="tip">ローカル関数に関連付けられたCronトリガー情報はローカルに保存されません。エッジ関数 CLIは、エッジ関数サーバー上でローカル関数に関連付けられたCronトリガーを管理します。そのため、このコマンドを実行する際は、ローカル関数に関数IDが設定されていることを確認してください。</div>



<span id="説明"></span>
## 説明

Cronトリガーを作成して、定期的なタスクを設定できます。Cronトリガーは、指定された時間に関数コード内のcronイベントを自動的にトリガーします。コード内でcronイベントをリッスンし、処理する必要があります。

<span id="サブコマンド"></span>
## サブコマンド

<span id="list"></span>
### list

```shell
npx nest cron list --function <function_id_or_name> --page <page_number> --desc --output <output>
```


ローカル関数に関連付けられたCronトリガーのリストを表示します。


* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数 CLIは`Error: function id required`エラーを返します。

* `<page_number>`: *integer, optional*

   * ページ分割表示のページ番号。デフォルトは1です。

* `--desc`: *boolean, optional*:

   * Cronトリガーを名前で降順にソートします。デフォルトは昇順です。

* `<output>`: *string, optional*:

   * リスト形式。

      * `table` (デフォルト): テーブル形式。

      * `json`: JSON形式。

      * `yaml`: YAML形式。


<span id="tasks"></span>
### tasks

```shell
npx nest cron tasks <cron_job_name>  --function <function_id_or_name> --page <page_number> --desc --output <output>
```


指定されたCronトリガーのタスク実行記録を表示します。


* `<cron_job_name>`: *string, required*

   * Cronトリガーの名前。

* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数 CLIは`Error: function id required`エラーを返します。

* `<page_number>`: *integer, optional*

   * ページ分割表示のページ番号。デフォルトは1です。

* `--desc`: *boolean, optional*:

   * タスクIDで降順にソートします。デフォルトは昇順です。


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


Cronトリガーを作成します。


* `<cron_job_name>`: *string, required*

   * Cronトリガーの名前。

      * 1つの関数内で、トリガー名は一意である必要があります。

      * 長さは128文字以内である必要があります。

* `<cron_expression>`: *string, required*

   * Cron式。[サポートされているCron式](https://docs.byteplus.com/docs/byteplus-cdn/docs-cron-triggers#supportedcron)を参照してください。

* `<description>`: *string, optional*

   * Cronトリガーの説明。

* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数 CLIは`Error: function id required`エラーを返します。

* `<parameter>`: *string, optional*

   * カスタムパラメータ。関数実行時、エッジ関数はこのパラメータを[CronEvent](https://docs.byteplus.com/docs/byteplus-cdn/docs/byteplus-cdn/docs_cn-CronEvent-jp)に渡します。

* `--single`: *boolean, optional*

   * cronイベントがランダムなエッジノードでトリガーされます。デフォルトでは、cronイベントはすべてのエッジノードでトリガーされます。


例えば、以下のコマンドでcronjob1という名前のCronトリガーを作成できます。Cron式は5分ごとの実行を示しています。

```shell
npx nest cron create cronjob1 -e " */5 * * * *"
```


npx cron listを使用して、作成したCronトリガーを表示できます。

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


指定されたCronトリガーの設定を更新します。


* `<cron_job_name>`: *string, required*

   * Cronトリガーの名前。

* `<cron_expression>`: *string, required*

   * Cron式。[サポートされているCron式](https://docs.byteplus.com/docs/byteplus-cdn/docs-cron-triggers-jp#%E3%82%B5%E3%83%9D%E3%83%BC%E3%83%88%E3%81%95%E3%82%8C%E3%81%A6%E3%81%84%E3%82%8Bcron%E5%BC%8F)を参照してください。

* `<description>`: *string, optional*

   * Cronトリガーの説明。

* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数 CLIは`Error: function id required`エラーを返します。

* `<parameter>`: *string, optional*

   * カスタムパラメータ。関数実行時、エッジ関数はこのパラメータを[CronEvent](https://docs.byteplus.com/docs/byteplus-cdn/docs/byteplus-cdn/docs-CronEvent-jp)に渡します。

* `--single`: *boolean, optional*

   * cronイベントがランダムなエッジノードでトリガーされます。デフォルトでは、cronイベントはすべてのエッジノードでトリガーされます。


<span id="delete"></span>
### delete

```shell
npx nest cron delete <cron_job_name> --function <function_id_or_name>
```


指定されたCronトリガーを削除します。


* `<cron_job_name>`: *string, required*

   * Cronトリガーの名前。

* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数 CLIは`Error: function id required`エラーを返します。


<span id="start"></span>
### start

```shell
npx nest cron start <cron_job_name> --function <function_id_or_name>
```


指定されたCronトリガーを有効にします。


* `<cron_job_name>`: *string, required*

   * Cronトリガーの名前。

* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数 CLIは`Error: function id required`エラーを返します。


有効化後、npx cron listを使用してCronトリガーのステータスを確認できます。

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


指定されたCronトリガーを無効にします。


* `<cron_job_name>`: *string, required*

   * Cronトリガーの名前。

* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数 CLIは`Error: function id required`エラーを返します。


無効化後、npx cron listを使用してCronトリガーのステータスを確認できます。

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


Cronトリガーのタスクログを表示します。


* `<cron_job_name>`: *string, required*

   * Cronトリガーの名前。

* `<task_id>`: *string, required*

   * タスクID。`npx nest cron tasks`コマンドを使用して、CronトリガーのタスクID（TASKID）を取得できます。

* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数 CLIは`Error: function id required`エラーを返します。


```shell
$ npx nest cron logs cronjob1 1374895809465100791
+---------------------+--------+---------------+
|     CREATETIME      | STATUS |   RESPONSE    |
+---------------------+--------+---------------+
| 2025-01-08 15:10:00 | failed | cron resp err |
+---------------------+--------+---------------+
```
