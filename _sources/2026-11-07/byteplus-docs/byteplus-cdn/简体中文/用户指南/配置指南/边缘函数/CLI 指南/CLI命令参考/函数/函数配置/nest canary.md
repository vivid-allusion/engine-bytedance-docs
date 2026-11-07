---
title: "nest canary"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-canary-cn"
---

管理本地函数的灰度环境。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">本命令需要您设置您的 BytePlus 账号的 Access Key ID 和 Secret Access Key。参见 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn">设置您的 Access Key ID 和 Secret Access Key</a>。</div>


* <div data-tips="true" data-tips-type="tip">本命令需要在一个函数项目的根目录下运行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn">nest init</a> 创建一个函数项目。</div>


* <div data-tips="true" data-tips-type="tip">本地函数的环境变量不保存在本地。边缘函数 CLI 在边缘函数服务端管理本地函数的环境变量。因此，在运行本命令时，确保您的本地函数需要有一个函数 ID。</div>



<span id="子命令"></span>
## 子命令

<span id="list"></span>
### list

```shell
npx nest canary list --canary --continents <continent1,continent2,...> --countries <country1,country2,...> --function <function_id_or_name>
```


获取灰度环境中的边缘节点。


* `--canary`：*boolean，optional*

   * 是否仅展示灰度环境中的边缘节点。默认为否。

* `<continent1,continent2,...>`：*string，optional*

   * 边缘节点所在的大洲。多个大洲的名称之间用英文逗号间隔。例如 `Asia,Europe`。

* `<country1,country2,...>`：*string，optional*

   * 边缘节点所在的国家或地区。多个国家或地区的名称之间用英文逗号间隔。例如 `China,France`。

* `<function_id_or_name>`：*string，optional*

   * 函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。如果您通过函数名称指定的本地函数还没有函数 ID，边缘函数 CLI 会返回错误 `Error: function id required`。


```shell
$ npx nest canary list
+---------+-----------+--------+
| COUNTRY | CONTINENT | CANARY |
+---------+-----------+--------+
| China   | Asia      | NO     |
+---------+-----------+--------+
```


<span id="add"></span>
### add

```shell
npx nest canary add --countries <country1,country2,...> --function <function_id_or_name>
```


把位于指定国家或地区的边缘节点添加到灰度环境。


* `<country1,country2,...>`：*string，required*

   * 边缘节点所在的国家或地区。多个国家或地区的名称之间用英文逗号间隔。例如 `China,France`。

* `<function_id_or_name>`：*string，optional*

   * 函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。如果您通过函数名称指定的本地函数还没有函数 ID，边缘函数 CLI 会返回错误 `Error: function id required`。


<span id="delete"></span>
### delete

```shell
npx nest canary delete --countries <country1,country2,...> --function <function_id_or_name>
```


从灰度环境中删除位于指定国家或地区的边缘节点。


* `<country1,country2,...>`：*string，required*

   * 边缘节点所在的国家或地区。多个国家或地区的名称之间用英文逗号间隔。例如 `China,France`。

* `<function_id_or_name>`：*string，optional*

   * 函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。如果您通过函数名称指定的本地函数还没有函数 ID，边缘函数 CLI 会返回错误 `Error: function id required`。
