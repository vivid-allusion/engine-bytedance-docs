---
title: "nest functions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-function-cn"
---

对本地函数或远端函数进行增删改查操作。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">本命令需要您设置您的 BytePlus 账号的 Access Key ID 和 Secret Access Key。参见 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn">设置您的 Access Key ID 和 Secret Access Key</a>。</div>


* <div data-tips="true" data-tips-type="tip">本命令需要在一个函数项目的根目录下运行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn">nest init</a> 创建一个函数项目。</div>



<span id="子命令"></span>
## 子命令

<span id="get"></span>
### get

```shell
npx nest functions get <function_id_or_name> 

npx nest functions get --remote <function_id> 
```


获取本地函数或远端函数的信息。


* `<function_id_or_name>`：*string，required*

   * 本地函数的 ID 或名称。

* `--remote`：*boolean，optional*

   * 获取远端函数的信息。默认获取本地函数的信息：

      * 您可以通过 `<function_id>` 或 `<function_name>` 获取本地函数的信息。

      * 您只能通过 `<function_id>` 获取远端函数的信息。


<span id="list"></span>
### list

```shell
npx nest functions list --page <page_number> --desc -s <status> --remote
```


获取函数列表。


* `<page_number>`：*integer，optional*

   * 列表分页显示的页码。默认为 1。

* `--desc`：*boolean，optional*：

   * 按函数 ID 降序排序。默认为按函数 ID 升序排序。

* `<status>`：*string，optional*

   * 函数的状态。

      * running：运行中。

      * unassociated：未关联域名。

      * configuring：配置中。

* `--remote`：*boolean，optional*：

   * 列表仅包括远端函数。默认仅包括本地函数。


```shell
npx nest functions list
+----+------+------+--------------+--------------------------+---------+-------------+---------+
| ID | NAME | TYPE |    ENTRY     |          REGION          | PROJECT | DESCRIPTION | DEFAULT |
+----+------+------+--------------+--------------------------+---------+-------------+---------+
|    | test | js   | src/index.js | Outside Chinese Mainland |         |             | true    |
+----+------+------+--------------+--------------------------+---------+-------------+---------+
```


<span id="create"></span>
### create

```shell
npx nest functions create --name <function_name> --description <function_description> --entry <path_to_entry_file> --project <project> --sync --cn
```


在函数项目中创建一个函数。您运行该命令时，边缘函数 CLI 会提示您输入函数名称、选择函数模板、入口文件的位置和名称、所属 BytePlus 项目、函数描述等信息。然后，边缘函数 CLI 会根据您输入的信息创建一个本地函数。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">每个 BytePlus 账号下的函数名称需唯一。名称的规则如下：</div>


   * <div data-tips="true" data-tips-type="tip">支持英文字母、数字和连字符（\-）。</div>


   * <div data-tips="true" data-tips-type="tip">长度不超过 128 个字符。</div>


* <div data-tips="true" data-tips-type="tip">您可以选择的函数模板取决于您是否设置了 Access Key ID 和 Secret Access Key：</div>


   * <div data-tips="true" data-tips-type="tip">如果您没有设置 Access Key ID 和 Secret Access Key，您只能使用 HelloWorld 模板。</div>


   * <div data-tips="true" data-tips-type="tip">如果您设置了 Access Key ID 和 Secret Access Key ，您可以使用边缘函数支持的所有模板。</div>


* `<function_name>`：*string，required*

   * 函数名称。

* `<function_description>`：*string，optional*

   * 函数描述。

* `<path_to_entry_file>`：*string，required*

   * 入口文件的路径。入口文件是本地函数执行的起点。该参数指定的入口文件必须存在。

* `<project>`：*string，optional*

   * 函数所属的项目。默认为 `default`。

* `--sync`：*boolean，optional*

   * 同时创建对应的远端函数。默认不创建对应的远端函数。

* `--cn`：*boolean，optional*

   * 函数的发布地域是否仅限于中国内地。默认不限制函数的发布地域。


```shell
$ npx nest functions create --name test0111 --entry src/index.js
==> [info]: Creating a new function test0111 locally.✔
```


<span id="update"></span>
### update

```shell
npx nest functions update <function_id_or_name> --new-name <new_function_name> --new-description <new_function_description> --new-id <new_function_id> --new-entry <path_to_entry_file> --sync
```


按函数 ID 或名称修改函数名称和描述。


* `<function_id_or_name>`：*string，required*

   * 本地函数的 ID 或名称。

* `<new_function_name>`：*string，optional*

   * 函数名称。

* `<new_function_description>`：*string，optional*

   * 新的函数描述。

* `<path_to_entry_file>`：*string，optional*

   * 入口文件的路径。入口文件是本地函数执行的起点。默认为项目配置文件中的入口文件的路径。

* `--sync`：*boolean，optional*

   * 同时更新对应的远端函数。默认不更新对应的远端函数。

* `--default`：*boolean，optional*

   * 把本函数设置为默认函数。默认不把本函数设置为默认函数。在一个函数项目中，默认函数只能有一个。

* `<new_function_id>`：*boolean，optional*

      * 新的函数 ID。


<span id="pull"></span>
### pull

```shell
npx nest functions pull <function_id> --env
```


把远端函数的代码同步到本地函数。


* `<function_id>`：*string，required*

   * 函数 ID。

* `--env`：*boolean，optional*

   * 把远端函数的环境变量同步到本地函数。默认不把远端函数的环境变量同步到本地函数。


<span id="delete"></span>
### delete

```shell
npx nest functions delete <function_id> --sync
```


按函数 ID 删除本地函数。该命令会删除项目配置文件中 `functions` 字段下关于指定的函数 ID 的配置信息，但不会删除本地函数的代码。


* `<function_id>`：*string，required*

   * 函数 ID。

* `--sync`：*boolean，optional*

   * 同时删除对应的远端函数。默认不删除对应的远端函数。
